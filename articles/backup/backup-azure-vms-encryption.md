---
title: 备份和还原加密的 Azure Vm 使用 Azure 备份服务
description: 本文介绍如何备份和还原使用 Azure 磁盘加密功能加密的 VM。
services: backup
author: geetha
manager: vijayts
ms.service: backup
ms.topic: conceptual
ms.date: 7/10/2018
ms.author: geetha
ms.openlocfilehash: 28126df0dfd9a03e93a76fa5071331603c4819a4
ms.sourcegitcommit: 04716e13cc2ab69da57d61819da6cd5508f8c422
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58851023"
---
# <a name="back-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a>使用 Azure 备份来备份和还原已加密的虚拟机
本文介绍使用 Azure 备份来备份和还原虚拟机 (VM) 的步骤。 此外，提供有关受支持的方案、先决条件以及针对错误案例的疑难解答步骤的详细信息。

## <a name="supported-scenarios"></a>支持的方案

 只有使用 Azure 资源管理器部署模型的已加密 VM 才支持备份和还原。 使用经典部署模型的 VM 不支持备份和还原。 使用 Azure 磁盘加密的 Windows 和 Linux VM 支持备份和还原加密的 VM。 磁盘加密使用 Windows 的行业标准 BitLocker 功能和 Linux 的 dm-crypt 功能提供磁盘加密。 下表显示了加密类型和对 VM 的支持。

   |  | BEK + KEK VM | 仅限 BEK 的 VM |
   | --- | --- | --- |
   | **非托管 VM**  | 是 | 是  |
   | **托管 VM**  | 是 | 是  |

   > [!NOTE]
   > Azure 备份支持使用独立密钥加密的 Vm。 目前不支持属于用于加密 VM 的证书的一部分的任何密钥。
   >

## <a name="prerequisites"></a>必备组件
* 已使用 [Azure 磁盘加密](../security/azure-security-disk-encryption.md)将 VM 加密。

* 已创建恢复服务保管库，并已遵循[为备份准备环境](backup-azure-arm-vms-prepare.md)中的步骤设置存储复制。

* 备份功能已获得 Key Vault 的访问权限，其中包含加密 VM 的秘钥和机密。

## <a name="back-up-an-encrypted-vm"></a>备份加密 VM
使用以下步骤设置备份目标、定义策略、配置项目和触发备份。

### <a name="configure-backup"></a>配置备份
1. 如果已打开恢复服务保管库，请转到下一步。 如果未打开恢复服务保管库，而是位于 Azure 门户中，请选择“所有服务”。

   a. 在资源列表中，键入“恢复服务”。

   b. 开始键入时，会根据输入筛选该列表。 出现“**恢复服务保管库**”时，请选择它。

      ![恢复服务保管库](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

    c. 此时会显示恢复服务保管库列表。 从列表中选择保管库。

     此时会打开选定的保管库仪表板。
1. 从保管库下显示的项目列表中，选择“备份”开始备份加密的 VM。

      ![“备份”边栏选项卡](./media/backup-azure-vms-encryption/select-backup.png)
1. 在“备份”磁贴中，选择“备份目标”。

      ![“方案”边栏选项卡](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
1. 在“工作负荷在哪里运行?”下，选择“Azure”。 下**要备份什么？**，选择**虚拟机**。 然后选择“确定”。

   ![打开“方案”边栏选项卡](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
1. 在“选择备份策略”下，选择要应用到保管库的备份策略。 然后选择“确定”。

      ![选择备份策略](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    将会列出默认策略的详细信息。 如果要创建策略，请从下拉列表中选择“新建”。 选择“确定”后，备份策略将与保管库相关联。

1. 选择要与指定策略关联的已加密 VM，并选择“确定”。

      ![选择加密 VM](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
1. 此页面显示与所选加密 VM 相关联的 Key Vault 的消息。 备份需要 Key Vault 中密钥和机密的只读访问权限。 它使用这些权限来备份密钥和机密以及关联的 VM。<br>
你是否**成员用户**，启用备份进程将无缝获得访问密钥保管库中，而无需任何用户干预即可备份加密 Vm。

   ![加密 VM 消息](./media/backup-azure-vms-encryption/member-user-encrypted-vm-warning-message.png)

   对于**来宾用户**，必须授予备份服务访问密钥保管库的权限，才能进行备份。 可按照以下部分中所述的步骤提供这些权限

   ![加密 VM 消息](./media/backup-azure-vms-encryption/guest-user-encrypted-vm-warning-message.png)

    现已定义保管库的所有设置，接下来请选择页面底部的“启用备份”。 “启用备份”会将策略部署到保管库和 VM。

1. 下一个阶段的准备工作是安装 VM 代理，或确保 VM 代理已安装。 若要执行相同的操作，请遵循[为备份准备环境](backup-azure-arm-vms-prepare.md)中的步骤。

### <a name="trigger-a-backup-job"></a>触发备份作业
遵循[将 Azure VM 备份到恢复服务保管库](backup-azure-arm-vms.md)中的步骤触发备份作业。

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a>继续备份已备份的启用了加密的 VM  
如果已备份恢复服务保管库中的 Vm 启用了加密更高版本的则必须将权限向后，访问密钥保管库的备份，若要继续。 可遵循[下一部分中的步骤](#provide-permissions)提供这些权限。 或者，可以遵循 [PowerShell 文档](backup-azure-vms-automation.md)的“启用备份”部分中的 PowerShell 步骤。

## <a name="provide-permissions"></a>提供的权限
使用以下步骤提供有关 Azure 备份来访问密钥保管库并对加密 Vm 执行备份的相关权限。
1. 选择“所有服务”并搜索“Key Vault”。

    ![Key Vault](./media/backup-azure-vms-encryption/search-key-vault.png)

1. 从 Key Vault 列表中，选择与加密 VM 关联的且需要备份的 Key Vault。

     ![Key Vault 选择](./media/backup-azure-vms-encryption/select-key-vault.png)

1. 依次选择“访问策略”、“新增”。

    ![新增](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)

1. 选择“选择主体”，在搜索框中键入“备份管理服务”。

    ![备份服务搜索](./media/backup-azure-vms-encryption/search-backup-service.png)

1. 依次选择“备份管理服务”、“选择”。

    ![备份服务选择](./media/backup-azure-vms-encryption/select-backup-service.png)

1. 在“从模板配置(可选)”下，选择“Azure 备份”。 “密钥权限”和“机密权限”中已预先填充所需的权限。 如果 VM 是使用“仅限 BEK”加密的，则仅机密权限是必需的，因此必须删除“密钥权限”的选择内容。

    ![Azure 备份选择](./media/backup-azure-vms-encryption/select-backup-template.png)

1. 选择“确定”。 请注意，“备份管理服务”已添加到“访问策略”中。

    ![访问策略](./media/backup-azure-vms-encryption/backup-service-access-policy.png)

1. 选择“保存”，为备份服务授予所需的权限。

    ![备份访问策略](./media/backup-azure-vms-encryption/save-access-policy.png)

成功提供权限后，可继续为加密的 VM 启用备份。

## <a name="restore-an-encrypted-vm"></a>还原已加密的 VM
除了以前提供的对带有 Azure AD 的 Azure 加密 VM 还原支持外，Azure 备份现在还支持还原[不带 Azure AD 的 Azure 加密 VM](https://docs.microsoft.com/azure/security/azure-security-disk-encryption-prerequisites-aad)。<br>

若要还原已加密的 VM，请先遵循[选择 VM 还原配置](backup-azure-arm-restore-vms.md#choose-a-vm-restore-configuration)的“还原已备份的磁盘”部分中所述的步骤来还原磁盘。 之后，可以使用以下选项之一：

* 遵循[从已还原的磁盘创建 VM](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) 中的 PowerShell 步骤从已还原的磁盘创建完整 VM。
* 或者，[使用模板自定义已还原的 VM](backup-azure-arm-restore-vms.md#use-templates-to-customize-a-restored-vm)，以便从已还原的磁盘创建 VM。 只能对 2017 年 4 月 26 日以后创建的恢复点使用模板。

## <a name="troubleshooting-errors"></a>排查错误
| Operation | 错误详细信息 | 解决方法 |
| --- | --- | --- |
|备份 | 错误代码：UserErrorKeyVaultPermissionsNotConfigured<br><br>错误消息：Azure 备份服务对 Key Vault 没有足够的权限，无法备份加密的虚拟机。 | 应遵循[上一部分中的步骤](#provide-permissions)为备份服务提供这些权限。 或者，可以遵循[使用 PowerShell 备份和还原虚拟机](backup-azure-vms-automation.md#enable-protection)一文“启用保护”部分中的 PowerShell 步骤执行操作。 |  
| 还原 | 无法还原此加密的 VM，因为与此 VM 关联的 Key Vault 不存在。 |通过[什么是 Azure 密钥保管库？](../key-vault/key-vault-overview.md)，创建密钥保管库。 参阅[使用 Azure 备份还原 Key Vault 密钥和机密](backup-azure-restore-key-secret.md)来还原密钥和机密（如果不存在）。 |
| 还原 | 错误代码：UserErrorKeyVaultKeyDoesNotExist<br><br> 错误消息：无法还原此加密 VM，因为与之关联的密钥不存在。 |参阅[使用 Azure 备份还原 Key Vault 密钥和机密](backup-azure-restore-key-secret.md)来还原密钥和机密（如果不存在）。 |
| 还原 | 错误代码：ProviderAuthorizationFailed/UserErrorProviderAuthorizationFailed<br><br>错误消息：备份服务没有权限访问订阅中的资源。 |如前所述，请先遵循[选择 VM 还原配置](backup-azure-arm-restore-vms.md#choose-a-vm-restore-configuration)的“还原已备份的磁盘”部分中所述的步骤来还原磁盘。 之后，使用 PowerShell [从已还原的磁盘创建 VM](backup-azure-vms-automation.md#create-a-vm-from-restored-disks)。 |
