---
title: Azure AD Connect Health - 警报目录 | Microsoft Docs
description: 此文档介绍 Azure AD Connect Health 中所有警报的目录。
services: active-directory
documentationcenter: ''
author: zhiweiwangmsft
manager: maheshu
editor: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2018
ms.author: zhiweiw
ms.openlocfilehash: 6803d0a5cff45736013a840451b940ef7108bca1
ms.sourcegitcommit: 34e0b4a7427f9d2a74164a18c3063c8be967b194
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="azure-active-directory-connect-health-alert-catalog"></a>Azure Active Directory Connect Health 警报目录 

Azure AD Connect Health 服务发送警报指示标识基础结构运行不正常。 本文包括每个警报的警报标题、说明和修正步骤。 <br />
错误、警告和预警是 Connect Health 服务生成的三个警报阶段。 强烈建议立即对触发的警报采取措施。 <br />
在成功的情况下，将解除 Azure AD Connect Health 警报。 Azure AD Connect Health 代理将定期检测并向服务报告成功的情况。 某些警报的解除取决于时间。 换句话说，如果在警报生成后的 72 小时内未观察到相同的错误条件，则警报会自动解除。

## <a name="general-alerts"></a>常规警报

| 警报名称 | 说明 | 补救 |
| --- | --- | ----- |
| 运行状况服务数据不是最新的 | 在一台或多台服务器上运行的运行状况代理未连接到运行状况服务，且运行状况服务未收到来自此服务器的最新数据。 运行状况服务处理的最后数据已过去 2 小时。 | 请确保运行状况代理具有到以下服务和终结点的出站连接。 [阅读详细信息](active-directory-aadconnect-health-data-freshness.md) |

## <a name="alerts-for-azure-ad-connect-sync"></a>Azure AD Connect 警报（同步）

| 警报名称 | 说明 | 补救 |
| --- | --- | ----- |
| Azure AD Connect 同步服务未运行 | Microsoft Azure AD Sync Windows 服务未运行，或无法启动。 因此，对象将无法与 Azure Active Directory 进行同步。 | 启动 Microsoft Azure Active Directory 同步服务</b> <ol> <li>依次单击“开始”和“运行”，键入“Services.msc”，然后单击“确定”<b></b><b></b><b></b><b></b>。</li> <li>找到“Microsoft Azure AD 同步服务”，然后检查是否已启动该服务<b></b>。 如果未启动该服务，请右键单击该服务，然后单击“启动”<b></b>。 | 
| 从 Azure Active Directory 导入失败 | 从 Azure Active Directory 连接器执行的导入操作失败。 |  请调查导入操作的事件日志错误，以获取更多详细信息。  |
| 由于身份验证失败，与 Azure Active Directory 的连接失败 | 由于身份验证失败，与 Azure Active Directory 的连接失败。 因此，对象将无法与 Azure Active Directory 进行同步。  | 请调查事件日志错误，以获取更多详细信息。 |
| 导出到 Active Directory 失败 | 到 Active Directory 连接器的导出操作失败。 | 请调查导出操作的事件日志错误，以获取更多详细信息。 | 
| 从 Active Directory 导入失败 | 从 Active Directory 导入失败。 因此，可能无法导入此林中某些域中的对象。 | <li>验证 DC 连接</li> <li>手动重新运行导入</li> <li> 请调查导入操作的事件日志错误，以获取更多详细信息。 | 
| 导出到 Azure Active Directory 失败 | 到 Azure Active Directory 连接器的导出操作失败。 因此，可能无法将某些对象成功导出到 Azure Active Directory。 | 请调查导出操作的事件日志错误，以获取更多详细信息。 |
| 在过去的 120 分钟内，密码哈希同步检测信号已跳过 | 在过去的 120 分钟内，密码哈希同步未与 Azure Active Directory 建立连接。 因此，密码不会与 Azure Active Directory 进行同步。 | 重启 Microsoft Azure Active Directory 同步服务：</b><br> 当前正在运行的任何同步操作都会中断。 如果没有正在进行的同步操作，可选择执行以下步骤。<br> 1.依次单击“开始”和“运行”，键入“Services.msc”，然后单击“确定”<b></b><b></b><b></b><b></b>。<br> 2.找到“Microsoft Azure AD Sync”并右键单击，然后单击“重启”<b></b><b></b>。 | 
| 检测到高 CPU 使用率 | CPU 消耗百分比超出此服务器上的建议阈值。 | <li>这可能是 CPU 消耗的临时峰值。 请在“监视”部分查看 CPU 使用情况趋势。</li><li>检查服务器上 CPU 使用情况消耗最高的前几个进程。<ol type="a"><li>可使用任务管理器或执行以下 PowerShell 命令： <br> <i>get-process \| Sort-Object -Descending CPU \| Select-Object -First 10</i></li><li>如果存在消耗高 CPU 使用情况的意外进程，请使用以下 PowerShell 命令停止这些进程： <br> stop-process -ProcessName [name of the process]<i></i></li></li></ol><li>如果上述列表中所示的进程为预期在服务器上运行的进程，且 CPU 消耗持续接近阈值，请考虑重新评估此服务器的部署要求。</li><li>作为自动防故障选项，可考虑重启服务器。 |
| 检测到高内存消耗 | 服务器的内存消耗百分比已超出此服务器的建议阈值。 | 检查服务器上消耗最高内存的前几个进程。 可使用任务管理器或执行以下 PowerShell 命令：<br> <i>get-process \| Sort-Object -Descending WS \| Select-Object -First 10</i> </br> 如果存在消耗高内存的意外进程，请使用以下 PowerShell 命令停止这些进程：<br>stop-process -ProcessName [name of the process]<i></i></li><li> 如果上述列表中所示的进程为预期在服务器上运行的进程，请考虑重新评估此服务器的部署要求。</li><li>作为自动防故障选项，可考虑重启服务器。 | 
| 密码哈希同步已停止运行 | 密码哈希同步已停止。 因此，密码不会与 Azure Active Directory 进行同步。 | 重启 Microsoft Azure Active Directory 同步服务： <br /> 当前正在运行的任何同步操作都会中断。 如果没有正在进行的同步操作，可选择执行以下步骤。 <br /> <ol> <li>依次单击“开始”和“运行”，键入“Services.msc”，然后单击“确定”<b></b><b></b><b></b><b></b>。</li> <li>找到“Microsoft Azure AD Sync”并右键单击，然后单击“重启”<b></b><b></b>。</li> </ol> </p>  | 
| 导出到 Azure Active Directory 的操作已停止。 已达到意外删除阈值 | 到 Azure Active Directory 的导出操作失败。 要删除的对象数多于配置的阈值。 因此，未导出任何对象。 | <li> 标记为要删除的对象数超出了设定的阈值。 请确保该结果是你所需要的。</li> <li> 若要继续导出，请执行以下步骤： <ol type="a"> <li>通过运行 Disable-ADSyncExportDeletionThreshold 禁用阈值</li> <li>启动同步服务管理器</li> <li>在类型为 Azure Active Directory 的连接器上运行导出</li> <li>成功导出对象后，通过运行以下命令启用阈值：Enable-ADSyncExportDeletionThreshold</li> </ol> </li> |

## <a name="alerts-for-active-directory-federation-services"></a>Active Directory 联合身份验证服务的警报
| 警报名称 | 说明 | 补救 |
| --- | --- | ----- |
|测试身份验证请求（综合事务）无法获取令牌 | 从此服务器启动的测试身份验证请求（综合事务）尝试 5 次后仍无法获取令牌。 这可能是由于临时网络问题、AD DS 域控制器可用性或 AD FS 服务器配置错误。  因此，联合身份验证服务处理的身份验证请求可能会失败。 代理使用本地计算机帐户上下文获取联合身份验证服务的令牌。 | 确保按照以下步骤操作，验证服务器的运行状况。<ol><li>验证场中的此服务器或其他 AD FS 服务器没有其他未解决的警报。</li><li>从 https://{your_adfs_server_name}/adfs/ls/idpinitiatedsignon.aspx 上的 AD FS 登录页面，以测试用户的身份登录，验证此问题不是临时故障</li><li>转到 <a href="https://testconnectivity.microsoft.com">https://testconnectivity.microsoft.com</a> 并选择“Office 365”选项卡。执行“Office 365 单一登录测试”。</li><li>通过在此服务器上的命令提示符执行以下命令，验证是否可从此服务器解析 AD FS 服务名称。 nslookup your_adfs_server_name</li></ol><p>如果无法解析服务名称，请参阅 FAQ 部分，了解有关添加 AD FS 服务的 HOST 文件条目和此服务器 IP 地址的说明。 这将允许此服务器上运行的综合事务模块请求一个令牌</p> | 
| 代理服务器无法访问联合服务器 | 此 AD FS 代理服务器无法与 ADFS 服务联系。 因此，此服务器处理的身份验证请求将失败。 | 执行以下步骤，验证此服务器和 AD FS 服务之间的连接。 <ol><li> 确保此服务器和 AD FS 服务之间的防火墙配置正确。 </li><li> 确保 AD FS 服务名称的 DNS 解析适当地指向位于公司网络内的 AD FS 服务。 这可通过在外围网络中为该服务器提供服务的 DNS 服务器，或通过 ADFS 服务名称的主机文件中的条目来实现。 </li><li> 通过打开此服务器上的浏览器，并访问位于 https://<your-adfs-service-name>/federationmetadata/2007-06/federationmetadata.xml 的联合元数据终结点来验证网络连接 </li> | 
| SSL 证书即将过期 | 联合服务器使用的 SSL 证书即将在 90 天内过期。 过期后，任何需要有效 SSL 连接的请求都将失败。 例如，对于 Office 365 客户，邮件客户端将无法进行身份验证。 | 更新每台 AD FS 服务器上的 SSL 证书。<ol><li>获取具有以下要求的 SSL 证书。<ol type="a"><li>增强型密钥使用至少是服务器身份验证。 </li><li>证书使用者或使用者可选名称 (SAN) 包含联合身份验证服务的 DNS 名称或适当的通配符。 例如：sso.contoso.com 或 *.contoso.com</li></ol></li><li>在本地计算机证书存储中的每台服务器上安装新的 SSL 证书。</li><li>确保 AD FS 服务帐户具有对证书私钥的读取访问权限</li></ol></p><p><b>对于 Windows Server 2008 R2 中的 AD FS 2.0：</b><ul><li>将新的 SSL 证书绑定到承载联合身份验证服务的 IIS 中的 Web 站点。 请注意，必须在每个联合服务器和联合服务器代理上执行此步骤。</li></ul></p><p><b>对于 Windows Server 2012 R2 中的 AD FS：</b><ul><li>运行以下 PowerShell 命令：set-AdfsSSLCertificate -Thumbprint {new certificate thumbprint}<i></i><br>例如：set-AdfsSSLCertificate -Thumbprint 7F92A390D1558C8A56D2E9999D22E7FF200374AC<i></i> | 
| AD FS 服务未在服务器上运行 | Active Directory 联合身份验证服务（Windows 服务）未在此服务器上运行。 针对此服务器的任何请求都将失败。 | 启动 Active Directory 联合身份验证服务（Windows 服务）：<ol><li>以管理员身份登录到服务器。</li><li> 打开 services.msc</li><li>找到“Active Directory 联合身份验证服务”。 </li><li>右键单击，然后选择“启动”。 | 
| 联合身份验证服务的 DNS 可能配置错误 | 可将 DNS 服务器配置为使用 AD FS 服务器场名称的 CNAME 记录。 建议为 AD FS 使用 A 或 AAAA 记录，以便 Windows 集成身份验证在公司网络中无缝运行。 | 确保 AD FS 场 <Farm Name> 的 DNS 记录不是 CNAME 类型。 将其配置为 A 或 AAAA 记录。 | 
| 已禁用 AD FS 审核 | 已为服务器禁用 AD FS 审核。 门户上的“AD FS 使用情况”部分将不会包括来自此服务器的数据。 | 如果未启用 AD FS 审核，请按照以下说明操作：<ol><li>在 ADFS 服务器上授予 ADFS 服务帐户“生成安全审核”权限。<li>打开服务器 gpedit.msc 上的本地安全策略。</li><li>导航到“计算机配置”\“Windows 设置”\“本地策略”\“用户权限分配” </li><li>添加 ADFS 服务帐户以具有“生成安全审核”权限。</li></li><li>从命令提示符处运行以下命令：<br>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable<i></i></li><li>更新联合身份验证服务属性以包括成功和失败审核。<li>在 ADFS 控制台中，选择“编辑联合身份验证服务属性”。</li><li>从“联合身份验证服务属性”对话框中，选择“事件”选项卡，然后选择“成功审核”和“失败审核”。</li></li></ol></p><p>完成上述步骤后，“事件查看器”中应显示 AD FS 审核事件。 要验证：<ol><li>转到“事件查看器”/“Windows 日志”/“安全”。</li><li>选择“筛选当前日志”，然后从“事件”源下拉菜单中选择“AD FS 审核”。 对于启用了 AD FS 审核的活动 AD FS 服务器，事件应对上述筛选可见。</li></ol></p><p>如果之前已按上述说明操作，但仍可看到此警报，可能是组策略对象已禁用 AD FS 审核。 根本原因可能是以下项之一：<ol><li>已删除 AD FS 服务帐户“生成安全审核”的权限。</li><li>组策略对象中的自定义脚本已基于“生成的应用程序”禁用成功和失败审核。</li><li>未启用 AD FS 配置，因此无法生成成功/失败审核。 | 
| AD FS SSL 证书为自签名证书 | 当前正在 AD FS 场中使用自签名证书作为 SSL 证书。 因此，Office 365 的电子邮件客户端身份验证将失败 | <p> 更新每台 AD FS 服务器上的 SSL 证书。 </p> <ol><li>获取具有以下要求的公开受信任的 SSL 证书。 </li><li>证书安装文件包含其私钥。 </li> <li>增强型密钥使用至少是服务器身份验证。 </li> <li>证书使用者或使用者可选名称 (SAN) 包含联合身份验证服务的 DNS 名称或适当的通配符。 例如：sso.contoso.com 或 *.contoso.com </li></ol> <p>在本地计算机证书存储中的每台服务器上安装新的 SSL 证书。 </p> <ol>确保 AD FS 服务帐户具有对证书私钥的读取访问权限。 <br /> <b>对于 Windows Server 2008R2 中的 AD FS 2.0：</b> <li>将新的 SSL 证书绑定到承载联合身份验证服务的 IIS 中的 Web 站点。 请注意，必须在每个联合服务器和联合服务器代理上执行此步骤。 </li> <br /><b>对于 Windows Server 2012 R2 中的 AD FS：</b> <li>运行以下 PowerShell 命令：set-AdfsSSLCertificate -Thumbprint {new certificate thumbprint} 例如：set-AdfsSSLCertificate -Thumbprint 7F92A390D1558C8A56D2E9999D22E7FF200374AC<i><i></i> </li> </ol> | 
| 代理服务器与联合服务器之间的信任无效 | 无法建立或续订联合服务器代理与联合身份验证服务之间的信任。 | 更新代理服务器上的代理信任证书。 重新运行代理配置向导。 |
| 已为 ADFS 禁用 Extranet 锁定保护 | Extranet 锁定保护功能在 AD FS 场上处于禁用状态。 此功能保护用户免遭来自 Internet 的暴力破解密码攻击，防止 AD DS 帐户锁定策略生效时对用户的拒绝服务攻击。 启用此功能后，如果某个用户失败的 Extranet 登录尝试次数（通过 WAP 服务器和 AD FS 进行的登录尝试）超过“ExtranetLockoutThreshold”，则 AD FS 服务器将停止处理“ExtranetObservationWindow”的进一步登录尝试。强烈建议在 AD FS 服务器上启用此功能。 | 运行以下命令，使用默认值启用 AD FS Extranet 锁定保护。<br>Set-AdfsProperties -EnableExtranetLockout $true<i></i><br><br>如果用户配置了 AD 锁定策略，请确保将“ExtranetLockoutThreshold”属性设置为低于 AD DS 锁定阈值的值<i></i>。 这样可确保丢弃已超出 AD FS 阈值的请求，并且永不验证 AD DS 服务器。 | 
| AD FS 服务帐户的服务主体名称 (SPN) 无效 | 联合身份验证服务帐户的服务主体名称未注册或不唯一。 因此，已加入域的客户端的 Windows 集成身份验证可能不是无缝的。 | 使用 [SETSPN -L ServiceAccountName<b></b>] 列出服务主体。<br>使用 [SETSPN -X<b></b>] 检查重复的服务主体名称。</p><p>如果 AD FS 服务帐户的 SPN 重复，请使用 [SETSPN -d service/namehostname<b></b>] 从重复帐户中删除 SPN</p><p>如果未设置 SPN，请使用 [SETSPN -s {Desired-SPN} {domain_name}\{service_account}<b></b>] 为联合身份验证服务帐户设置所需的 SPN。 | 
| 主要 AD FS 令牌解密证书即将过期 | 主要 AD FS 令牌解密证书不含私钥。 AD FS 无法解密来自受信任声明提供程序的令牌。 AD FS 无法解密已加密的 SSO Cookie。 最终用户无法进行身份验证，因此无法访问资源。 | 如果启用了自动证书续期，AD FS 将管理令牌解密证书。</p><p>如果手动管理证书，请遵循以下说明。<b>获取新的令牌解密证书</b>。<ol type="a"><li>确保增强型密钥使用 (EKU) 包括“密钥加密”。</li><li>使用者或使用者可选名称 (SAN) 没有任何限制。</li><li>请注意，验证令牌解密证书时，联合服务器和声明提供程序合作伙伴需要能够链接到受信任的根证书颁发机构。</li></ol><b>确定声明提供程序合作伙伴信任新令牌解密证书的方式</b><ol type="a"><li>请求合作伙伴在更新证书后拉取联合元数据。</li><li>与合作伙伴共享 新证书（.cer 文件）的公钥。 在声明提供程序合作伙伴 AD FS 服务器上，从“管理工具”菜单上启动 AD FS 管理。 在“信任关系”/“信赖方信任”下，选择为你创建的信任。 在“属性”/“加密”下，单击“浏览”以选择新的令牌解密证书，然后单击“确定”。</li></ol><b>在每个联合服务器的本地证书存储中安装证书</b>。<ul><li>确保证书安装文件在每个服务器上都有证书的私钥。</li></ul><b>确保联合身份验证服务帐户有权访问新证书的私钥。</b><b>将新证书添加到 AD FS。</b><ol type="a"><li>从“管理工具”菜单中启动 AD FS 管理</li><li>展开“服务”，然后选择“证书”</li><li>在“操作”窗格中，单击“添加令牌解密证书”</li><li>系统将显示对令牌解密有效的证书列表。 如果发现新证书未显示在列表中，需要返回并确保证书位于本地计算机个人存储中，并与私钥关联，且证书包含作为扩展密钥使用的密钥加密。</li><li>选择新的“令牌解密证书”，然后单击“确定”。</li></ol><b>将新的令牌解密证书设为主证书</b>。<ol type="a"><li>在“AD FS 管理”中选中“证书”节点之后，现在“令牌解密”下应显示两个证书：现有证书和新证书。</li><li>选择新的令牌解密证书，右键单击，然后选择“设置为主证书”。</li><li>保留旧证书作为辅助证书，以便续期。 确定不再需要旧证书进行续期或证书过期后，应计划将其删除。 </li></ol>  | 
| 主要 AD FS 令牌签名证书即将过期 | AD FS 令牌签名证书即将在 90 天内过期。 此证书无效时，AD FS 无法颁发已签名的令牌。 | <b>获取新的令牌签名证书</b>。<ol type="a"><li>确保增强型密钥使用 (EKU) 包括“数字签名”。 </li><li>使用者或使用者可选名称 (SAN) 没有任何限制。 </li><li>请注意，验证令牌签名证书时，联合服务器、资源伙伴联合服务器和信赖方应用程序服务器需要能够链接到受信任的根证书颁发机构。</li></ol><b>在每个联合服务器的本地证书存储中安装证书</b>。 <ul><li>确保证书安装文件在每个服务器上都有证书的私钥。</li></ul></li><b>确保联合身份验证服务帐户有权访问新证书的私钥。</b><b>将新证书添加到 AD FS。</b><ol type="a"><li>从“管理工具”菜单中启动 AD FS 管理。</li><li>展开“服务”，然后选择“证书”</li><li>在“操作”窗格中，单击“添加令牌签名证书”</li><li>系统将展示对令牌签名有效的证书列表。 如果发现新证书未显示在列表中，需要返回并确保证书位于本地计算机个人存储中，并与私钥关联，且证书包含数字签名 KU。</li><li>选择新的“令牌签名证书”，然后单击“确定”</li></ol><b>将令牌签名证书中的更改告知所有信赖方</b>。<ol type="a"><li>使用 AD FS 联合元数据的信赖方必须请求新的联合元数据，然后开始使用新证书。</li><li>未使用 AD FS 联合元数据的信赖方必须手动更新新令牌签名证书的公钥。 与信赖方共享 .cer 文件。</li></a><b>将新的令牌签名证书设为主证书</b>。<ol type="a"><li>在“AD FS 管理”中选中“证书”节点之后，现在“令牌签名”下应显示两个证书：现有证书和新证书。</li><li>选择新的令牌签名证书，右键单击，然后选择“设置为主证书”<b></b></li><li>保留旧证书作为辅助证书，以便续期。 确定不再需要旧证书进行续期或证书过期后，请计划将其删除。 请注意，当前用户的 SSO 会话已签名。 当前 AD FS 代理信任关系将利用使用旧证书签名和加密的令牌。 </li></ol>  | 
| 在本地证书存储中找不到 AD FS SSL 证书 | 在本地证书存储中找不到在 AD FS 数据库中指纹配置为 SSL 证书的证书。 因此，通过 SSL 的任何身份验证请求都将失败。 例如，Office 365 的电子邮件客户端身份验证将失败。 | 在本地证书存储中安装包含已配置指纹的证书。 | 
| SSL 证书已过期 | AD FS 服务的 SSL 证书已过期。 因此，任何需要有效 SSL 连接的身份验证请求都将失败。 例如：电子邮件客户端身份验证将无法对 Office 365 进行身份验证。 | 更新每台 AD FS 服务器上的 SSL 证书。<ol><li>获取具有以下要求的 SSL 证书。<li>增强型密钥使用至少是服务器身份验证。 </li><li>证书使用者或使用者可选名称 (SAN) 包含联合身份验证服务的 DNS 名称或适当的通配符。 例如：sso.contoso.com 或 *.contoso.com</li></li><li>在本地计算机证书存储中的每台服务器上安装新的 SSL 证书。</li><li>确保 AD FS 服务帐户具有对证书私钥的读取访问权限</li></ol></p><p><b>对于 Windows Server 2008 R2 中的 AD FS 2.0：</b><ul><li>将新的 SSL 证书绑定到承载联合身份验证服务的 IIS 中的 Web 站点。 请注意，必须在每个联合服务器和联合服务器代理上执行此步骤。</li></ul></p><p><b>对于 Windows Server 2012 R2 中的 AD FS：</b><ul><li>运行以下 PowerShell 命令：set-AdfsSSLCertificate -Thumbprint {new certificate thumbprint}<i></i><br> 例如：set-AdfsSSLCertificate -Thumbprint 7F92A390D1558C8A56D2E9999D22E7FF200374AC<i></i> | 
| 未启用 Azure Active Directory 所需的终结点（针对 Office 365） | 未为联合身份验证服务启用 Exchange 联机服务、Azure AD 和 Office 365 所需的以下一组终结点： <li>/adfs/services/trust/2005/usernamemixed</li><li>/adfs/services/trust/2005/windowstransport</li><li>/adfs/ls/</li> |  在联合身份验证服务上启用 Microsoft 云服务必需的终结点。<br>对于 Windows Server 2012R2 中的 AD FS，请在场中的主联合服务器上从 PowerShell 窗口中执行以下命令：<ul><li> Enable-AdfsEndpoint -TargetAddressPath /adfs/services/trust/2005/usernamemixed </li><li> Enable-AdfsEndpoint -TargetAddressPath /adfs/services/trust/2005/windowstransport </li><li> Enable-AdfsEndpoint -TargetAddressPath /adfs/ls/ </li></ul></p> | 
| 联合服务器无法连接到 AD FS 配置数据库 | AD FS 服务帐户在连接到 AD FS 配置数据库时遇到问题。 因此，此计算机上的 AD FS 服务可能无法按预期运行。 | <li> 确保 AD FS 服务帐户有权访问配置数据库。 </li><li>确保 AD FS 配置数据库服务可用且可访问。 </li> | 
| 必需的 SSL 绑定缺失或未配置 | 此联合服务器用于成功执行身份验证必需的 SSL 绑定配置错误。 因此，AD FS 无法处理任何传入请求。 | 对于 Windows Server 2012 R2</b><br>打开提升的管理命令提示符，并执行以下命令： <ol> <li> 查看当前 SSL 绑定：Get-AdfsSslCertificate<i></i> <li> 添加新绑定：netsh http add sslcert hostnameport=<federation service name>:443 certhash=0102030405060708090A0B0C0D0E0F1011121314 appid={00112233-4455-6677-8899-AABBCCDDEEFF} certstorename=MY<i></i> |
| 主要 AD FS 令牌签名证书已过期 | AD FS 令牌签名证书已过期。 此证书无效时，AD FS 无法颁发已签名的令牌。 | 如果启用了自动证书续期，AD FS 将管理更新令牌签名证书。</p><p>如果手动管理证书，请按照以下说明操作。 <ol><li><b>获取新的令牌签名证书</b>。<ol type="a"><li>确保增强型密钥使用 (EKU) 包括“数字签名”。 </li><li>使用者或使用者可选名称 (SAN) 没有任何限制。 </li><li>请记住，验证令牌签名证书时，联合服务器、资源伙伴联合服务器和信赖方应用程序服务器需要能够链接到受信任的根证书颁发机构。</li></ol></li><li><b>在每个联合服务器的本地证书存储中安装证书</b>。 <ul><li>确保证书安装文件在每个服务器上都有证书的私钥。</li></ul></li><li><b>确保联合身份验证服务帐户有权访问新证书的私钥</b>。</li><li><b>将新证书添加到 AD FS</b>。<ol type="a"><li>从“管理工具”菜单中启动 AD FS 管理。</li><li>展开“服务”，然后选择“证书”</li><li>在“操作”窗格中，单击“添加令牌签名证书”</li><li>系统将展示对令牌签名有效的证书列表。 如果发现新证书未显示在列表中，需要返回并确保证书位于本地计算机个人存储中，并与私钥关联，且证书包含数字签名 KU。</li><li>选择新的“令牌签名证书”，然后单击“确定”</li></ol></li><li><b>将令牌签名证书中的更改告知所有信赖方</b>。<ol type="a"><li>使用 AD FS 联合元数据的信赖方必须请求新的联合元数据，然后开始使用新证书。</li><li>未使用 AD FS 联合元数据的信赖方必须手动更新新令牌签名证书的公钥。 与信赖方共享 .cer 文件。</li></ol></li><li><b>将新的令牌签名证书设为主证书</b>。<ol type="a"><li>在“AD FS 管理”中选中“证书”节点之后，现在“令牌签名”下应显示两个证书：现有证书和新证书。</li><li>选择新的令牌签名证书，右键单击，然后选择“设置为主证书”<b></b></li><li>保留旧证书作为辅助证书，以便续期。 确定不再需要旧证书进行续期或证书过期后，请计划将其删除。 请记住，当前用户的 SSO 会话已签名。 当前 AD FS 代理信任关系将利用使用旧证书签名和加密的令牌。 </li></ol></li>|
| 代理服务器正在删除请求以进行拥塞控制 | 由于此代理服务器与联合服务器之间的延迟高于正常值，此代理服务器当前正在删除来自外网的请求。 因此，AD FS 代理服务器处理的身份验证请求可能会部分失败。 | <li>验证联合代理服务器和联合服务器之间的网络延迟是否在可接受的范围内。 有关“令牌请求延迟”的趋势值，请参阅“监视”部分。 延迟高于 [1500 ms] 时，应视为高延迟。如果检测到高延迟，请确保 AD FS 与 AD FS 代理服务器之间的网络没有连接问题。</li><li>请确保联合服务器的身份验证请求未重载。 “监视”部分提供了每秒令牌请求数、CPU 利用率和内存消耗的趋势视图。</li><li>如果已确认上述项正常，但此问题仍然存在，请根据相关链接中的指南，调整每个联合代理服务器上的拥塞规避设置。 | 
| 拒绝 AD FS 服务帐户访问任一证书的私钥。 | AD FS 服务帐户无权访问此计算机上的任一 AS FS 证书的私钥。 | 确保 AD FS 服务帐户可以访问存储在本地计算机证书存储中的 SSL、令牌签名和令牌解密证书。<ol> <li> 从命令行键入 MMC。</li><li>转到“文件”>“添加”/“删除管理单元”</li><li> 选择“证书”，然后单击“添加”。 -> 选择“计算机帐户”，然后单击“下一步”。 -> 选择“本地计算机”，然后单击“完成”。 单击“确定”。 </li></ol> <br>打开证书（本地计算机）/个人/证书。对于 AD FS 使用的所有证书：<ol><li>右键单击证书。</li><li>选择“所有任务”>“管理私钥”。</li><li>在“组”或“用户名”下的“安全”选项卡上，确保存在 ADFS 服务帐户。 如果未选择“添加”，则添加 AD FS 服务帐户。</li><li>选择 AD FS 服务帐户，并在“<AD FS Service Account Name> 的权限”下确保勾选了读取权限（复选标记）。 | 
| AD FS SSL 证书没有私钥 | 在没有私钥的情况下，安装了 AD FS SSL 证书。 因此，通过 SSL 的任何身份验证请求都将失败。 例如，Office 365 的电子邮件客户端身份验证将失败。 | 更新每台 AD FS 服务器上的 SSL 证书。<ol><li>获取具有以下要求的公开受信任的 SSL 证书。<ol type="a"><li>证书安装文件包含其私钥。</li><li>增强型密钥使用至少是服务器身份验证。 </li><li>证书使用者或使用者可选名称 (SAN) 包含联合身份验证服务的 DNS 名称或适当的通配符。 例如：sso.contoso.com 或 *.contoso.com</li></ol></li><li>在本地计算机证书存储中的每台服务器上安装新的 SSL 证书。</li><li>确保 AD FS 服务帐户具有对证书私钥的读取访问权限</li></ol></p><p><b>对于 Windows Server 2008 R2 中的 AD FS 2.0：</b><ul><li>将新的 SSL 证书绑定到承载联合身份验证服务的 IIS 中的 Web 站点。 请注意，必须在每个联合服务器和联合服务器代理上执行此步骤。</li></ul></p><p><b>对于 Windows Server 2012 R2 中的 AD FS：</b><ul><li>运行以下 PowerShell 命令：Set-AdfsSslCertificate -Thumbprint '<thumbprint of new cert>'<i></i> | 
| 主要 AD FS 令牌解密证书已过期 | 主要 AD FS 令牌解密证书已过期。 AD FS 无法解密来自受信任声明提供程序的令牌。 AD FS 无法解密已加密的 SSO Cookie。 最终用户无法进行身份验证，因此无法访问资源。 | <p>如果启用了自动证书续期，AD FS 将管理令牌解密证书。</p><p>如果手动管理证书，请按照以下说明操作。<ol><li><b>获取新的令牌解密证书</b>。<ul><li>确保增强型密钥使用 (EKU) 包括“密钥加密”。</li><li>使用者或使用者可选名称 (SAN) 没有任何限制。</li><li>请注意，验证令牌解密证书时，联合服务器和声明提供程序合作伙伴需要能够链接到受信任的根证书颁发机构。</li></ul></li><li><b>确定声明提供程序合作伙伴信任新令牌解密证书的方式</b><ul><li>请求合作伙伴在更新证书后拉取联合元数据。</li><li>与合作伙伴共享 新证书（.cer 文件）的公钥。 在声明提供程序合作伙伴 AD FS 服务器上，从“管理工具”菜单上启动 AD FS 管理。 在“信任关系”/“信赖方信任”下，选择为你创建的信任。 在“属性”/“加密”下，单击“浏览”以选择新的令牌解密证书，然后单击“确定”。</li></ul></li><li><b>在每个联合服务器的本地证书存储中安装证书</b>。<ul><li>确保证书安装文件在每个服务器上都有证书的私钥。</li></ul></li><li><b>确保联合身份验证服务帐户有权访问新证书的私钥</b>。</li><li><b>将新证书添加到 AD FS</b>。<ul><li>从“管理工具”菜单中启动 AD FS 管理</li><li>展开“服务”，然后选择“证书”</li><li>在“操作”窗格中，单击“添加令牌解密证书”</li><li>系统将显示对令牌解密有效的证书列表。 如果发现新证书未显示在列表中，需要返回并确保证书位于本地计算机个人存储中，并与私钥关联，且证书包含作为扩展密钥使用的密钥加密。</li><li>选择新的“令牌解密证书”，然后单击“确定”。</li></ul></li><li><b>将新的令牌解密证书设为主证书</b>。<ul><li>在“AD FS 管理”中选中“证书”节点之后，现在“令牌解密”下应显示两个证书：现有证书和新证书。</li><li>选择新的令牌解密证书，右键单击，然后选择“设置为主证书”。</li><li>保留旧证书作为辅助证书，以便续期。 确定不再需要旧证书进行续期或证书过期后，应计划将其删除。 </li></ul></li> | 

## <a name="alerts-for-active-directory-domain-services"></a>Azure Active Directory 域服务警报

| 警报名称 | 说明 | 补救 |
| --- | --- | ----- |
| 无法通过 LDAP ping 访问域控制器 | 无法通过 LDAP ping 访问域控制器。 这可能是由于网络问题或计算机问题所致。 因此，LDAP Ping 将失败。 |  <li>检查警报列表是否存在相关警报，例如：域控制器未在播发。 </li><li>确保受影响的域控制器有足够的磁盘空间。 空间不足将阻止 DC 将其自身作为 LDAP 服务器来播发。 </li><li> 尝试查找 PDC： <br> 在受影响的域控制器上运行 netdom query fsmo<i></i> </br> 。 <li> 确保物理网络配置/连接正确。 </li> |
| 发生了 Active Directory 复制错误 | 此域控制器发生的是复制问题，可转到“复制状态”仪表板找到该问题。 复制错误可能是由于配置不正确或其他相关问题所致。 未处理的复制错误可能会导致数据不一致。 | 有关受影响的源和目标 DC 的名称，请参阅其他详细信息。 导航到“复制状态”仪表板，并在受影响的 DC 上查找活动错误。 单击错误，以打开包含有关如何修复该特定错误的更多详细信息的边栏选项卡。| 
| 域控制器找不到 PDC | 无法通过此域控制器访问 PDC。 这将导致用户登录受到影响、组策略更改得不到应用以及系统时间同步出现问题。 | <li>检查警报列表是否存在可能影响 PDC 的相关警报，例如：域控制器未在播发。 </li> <li>尝试查找 PDC： <br> 在受影响的域控制器上运行 netdom query fsmo<i></i> </br> 。<li>确保网络正常运行。 </li> |
| 域控制器找不到全局编录服务器 | 无法从此域控制器访问全局编录服务器。 它将导致通过此域控制器尝试的身份验证失败。 | 检查警报列表中是否存在任何“域控制器未在播发”警报，其中受影响的服务器可能为 GC<b></b>。 如果不存在播发警报，请检查 SRV 记录中是否存在 GC。 可通过运行以下命令检查它们： <br> nltest \/dnsgetdc: [ForestName] \/gc<i></i> </br> 应该会列出作为 GC 播发的 DC。 如果列表为空，请检查 DNS 配置，以确保 GC 已注册 SRV 记录。 DC 可以在 DNS 中找到它们。 <br />有关全局编录疑难解答信息，请参阅<a href="https://technet.microsoft.com/library/cc961811.aspx#ECAA">作为全局编录服务器播发</a>。 | 
| 域控制器无法访问本地 SYSVOL 共享 | Sysvol 包含组策略对象中的重要元素以及要在域中的 DC 内分发的脚本。 DC 不会将其本身作为 DC 播发，并且将不会应用组策略。 | 请参阅<a href="https://support.microsoft.com/kb/2958414">如何对缺失的 SYSVOL 和 Netlogon 共享进行故障排除</a> | 
| 域控制器时间不同步 | 此域控制器的时间超出了正常的时间偏差范围。 因此，Kerberos 身份验证将失败。 | <li>重启 Windows 时间服务： <br>运行 net stop w32time，<i></i> </br> 然后在受影响的域控制器上，运行 <br>net start w32time<i></i></br> 。</li><li>重新同步时间： <br>在受影响的域控制器上，运行 w32tm \/resync<i></i></br> 。 | 
| 域控制器未在播发 | 此域控制器未正确播发其可执行的角色。 这可能是由复制、DNS 错误配置、关键服务未运行或服务器未完成初始化等问题导致的。  因此，域控制器、域成员和其他设备将找不到此域控制器。 此外，其他域控制器可能无法从此域控制器进行复制。 | 检查警报列表是否存在其他相关警报的，例如：复制已中断。 域控制器时间不同步。Netlogon 服务未运行。 DFSR 和/或 NTFRS 服务未运行。 确定并解决相关 DNS 问题：登录到受影响的域控制器。 打开系统事件日志。 如果存在事件 5774、5775 或 5781，请参阅<a href="https://msdn.microsoft.com/library/bb727055.aspx#ECAA">排查域控制器定位程序 DNS 记录注册故障</a>确定并排查相关 Windows 时间服务问题：确保 Windows 时间服务正在运行：在受影响的域控制器上运行“net start w32time”。重启 Windows 时间服务：在受影响的域控制器上依次运行“net stop w32time”和“net start w32time”<b></b><b></b><b></b>。 | 
| GPSVC 服务未运行 | 如果已停止或禁用服务，则将不会应用由管理员配置的设置，并且将无法通过组策略管理应用程序和组件。 如果禁用此服务，则依赖于组策略组件的所有组件或应用程序都将无法正常运行。  | 运行 <br>net start gpsvc<i></i></br> （在受影响的域控制器上运行）。 | 
| DFSR 和/或 NTFRS 服务未运行 | 如果 DFSR 和 NTFRS 服务均停止，域控制器将无法复制 SYSVOL 数据。 SYSVOL 数据将不一致。 | <li>如果使用 DFSR：<ol type="1" > 在受影响的域控制器上，运行“net start dfsr”<b></b>。 </li><li>如果使用 NTFRS：<ol type="1" >在受影响的域控制器上，运行“net start ntfrs”<b></b>。 </li>| 
| Netlogon 服务未运行 | 无法在此 DC 上执行登录请求、注册、身份验证和查找域控制器。 | 在受影响的域控制器上，运行“net start netlogon”<b></b> | 
| W32Time 服务未运行 | 如果停止 Windows 时间服务，日期和时间同步将不可用。 如果禁用此服务，则显式依赖于它的任何服务都将无法启动。 | 在受影响的域控制器上，运行“net start win32Time”<b></b> | 
| ADWS 服务未运行 | 如果已停止或禁用 Active Directory Web Services 服务，Active Directory PowerShell 等客户端应用程序将无法访问或管理在此服务器上本地运行的任何目录服务实例。 | 在受影响的域控制器上，运行“net start adws”<b></b> | 
| 根 PDC 当前未通过 NTP 服务器同步 | 如果未将 PDC 配置为与外部或内部时间源同步时间，PDC 仿真器使用其内部时钟，并且自身就是林的可靠时间源。 如果 PDC 自身的时间不准确，所有计算机的时间设置都不正确。 | 在受影响的域控制器上，打开命令提示符。 停止时间服务：net stop w32time</li> <li>配置外部时间源： <br> w32tm \/config \/manualpeerlist: time.windows.com \/syncfromflags:manual \/reliable:yes<i></i></br><br>注意：将 time.windows.com 替换为所需外部时间源的地址。 启动时间服务： <br> net start w32time<i></i></br> | 
| 域控制器已隔离 | 此域控制器未连接到其他任何正在运行的域控制器。 这可能是由于配置错误所致。 因此，该 DC 不会被使用，将不会从任何域控制器进行复制，也不会复制到任何域控制器。 | 启用入站和出站复制：在受影响的域控制器上，运行“repadmin /options ServerName -DISABLE_INBOUND_REPL”<b></b>。 在受影响的域控制器上，运行“repadmin /options ServerName -DISABLE_OUTBOUND_REPL”<b></b>。 创建与其他域控制器的新复制连接：<ol type="1"><li>打开“Active Directory 站点和服务”：单击“开始”菜单，指向“管理工具”，然后单击“Active Directory 站点和服务”。 </li><li>在控制台树中，依次展开“站点”和此 DC 所属的站点。 </li><li>展开“服务器”容器以显示服务器列表。 </li><li>展开此 DC 的服务器对象。 </li><li>右键单击“NTDS 设置”对象，然后单击“新建 Active Directory 域服务连接”... </li><li>从列表中选择一个服务器，然后单击“确定”。</li></ol><a href="https://support.microsoft.com/kb/230306 ">How to remove orphaned domains from Active Directory</a>（如何从 Active Directory 删除孤立域）。 |
| 已禁用出站复制 | 禁用出站复制的 DC 将无法分发任何源于其内部的更改。 | 若要在受影响的域控制器上启用出站复制，请按以下步骤操作：依次单击“开始”和“运行”，键入 cmd，然后单击“确定”。 键入以下文本，然后按 Enter：<br>repadmin /options -DISABLE_OUTBOUND_REPL<i></i> | 
| 已禁用入站复制 | 禁用入站复制的 DC 将不具有最新信息。 这可能会导致登录失败。 | 若要在受影响的域控制器上启用入站复制，请按以下步骤操作：依次单击“开始”和“运行”，键入 cmd，然后单击“确定”。 键入以下文本，然后按 Enter：<br>repadmin /options -DISABLE_INBOUND_REPL<i></i> </br> | 
| LanmanServer 服务未运行 | 如果禁用此服务，则显式依赖于它的任何服务都将无法启动。 | 在受影响的域控制器上，运行“net start LanManServer”<b></b>。 |
| Kerberos 密钥发行中心服务未运行 | 如果 KDC 服务停止，用户将无法使用 Kerberos v5 身份验证协议通过此 DC 进行身份验证。 | 在受影响的域控制器上，运行“net start kdc”<b></b>。 |
| DNS 服务未运行 | 如果 DNS 服务停止，将相应服务器用作 DNS 用途的计算机和用户将找不到资源。 | 在受影响的域控制器上，运行“net start dns”<b></b>。 |
| DC 执行了 USN 回退 | 发生 USN 回退时，之前查看过 USN 的目标域控制器不会入站复制对对象和属性所做的修改。 因为这些目标域控制器认为它们是最新的，目录服务事件日志中未报告复制错误，监视和诊断工具也未报告复制错误。 USN 回退可能会影响复制任意分区中的任何对象或属性。 已观察到的最常见负面影响是，在回退域控制器上创建的用户帐户和计算机帐户在一个或多个复制合作伙伴上不存在。 或者，源自回退域控制器的密码更新在复制合作伙伴上不存在。 | 从 USN 回退进行恢复的方法有两种： <p>从域中删除域控制器，步骤如下： <ol type="1"><li>从域控制器中删除 Active Directory，迫使其成为独立的服务器。 有关详细信息，请单击下面的文章编号，查看相应的 Microsoft 知识库文章： <br><a href="https://support.microsoft.com/kb/332199">332199</a> 使用 Active Directory 安装向导在 Windows Server 2003 和 Windows Server 2000 中强制降级时，域控制器无法正常降级。 </li> <li>关闭已降级的服务器。</li> <li>在正常运行的域控制器中，清除已降级的域控制器的元数据。 有关详细信息，请单击下面的文章编号，查看相应的 Microsoft 知识库文章： <br><a href="https://support.microsoft.com/kb/216498">216498</a> 域控制器降级失败后如何删除 Active Directory 中的数据</li> <li>如果未正确还原的域控制器托管操作主机角色，请将这些角色转移到正常的域控制器。 有关详细信息，请单击下面的文章编号，查看相应的 Microsoft 知识库文章： <br><a href="https://support.microsoft.com/kb/255504">255504</a> 使用 Ntdsutil.exe 捕获 FSMO 角色或将其转移到域控制器</li> <li>重启已降级的服务器。</li> <li>如果需要，在独立的服务器上重新安装 Active Directory。</li> <li>如果域控制器以前是全局编录，请将域控制器配置为全局编录。 有关详细信息，请单击下面的文章编号，查看相应的 Microsoft 知识库文章： <br><a href="https://support.microsoft.com/kb/313994">313994</a> 如何在 Windows 2000 中创建或移动全局编录</li> <li>如果域控制器以前托管过操作主机角色，请将操作主机角色重新转移到域控制器。 有关详细信息，请单击下面的文章编号，查看相应的 Microsoft 知识库文章： <br><a href="https://support.microsoft.com/kb/255504">255504</a> 使用 Ntdsutil.exe 捕获 FSMO 角色或将其转移到域控制器 还原正常备份的系统状态。</li></ol></p> <p>评估是否存在此域控制器的有效系统状态备份。 如果在回退的域控制器错误还原之前进行了有效的系统状态备份，且备份中包含域控制器上最近进行的更改，请通过最近的备份还原系统状态。</p> <p>也可以将快照作为备份源。 或者，可以按照下面<a href="http://technet.microsoft.com/library/dd363545(WS.10).aspx">这篇文章</a>中的“在无系统状态数据备份情况下还原以前版本的虚拟域控制器 VHD”部分中的步骤操作，将数据库设置为向自己提供新的调用 ID</p></p> |









## <a name="next-steps"></a>后续步骤
* [Azure AD Connect Health 常见问题](active-directory-aadconnect-health-faq.md)