---
title: Azure Stack 上的 Kubernetes 部署故障排除 |Microsoft Docs
description: 了解如何排查 Azure Stack 上的 Kubernetes 部署。
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.author: mabrigg
ms.date: 04/02/2019
ms.reviewer: waltero
ms.lastreviewed: 03/20/2019
ms.openlocfilehash: 2a9eccfa109292b7d142092f69f4a664b0ff8f20
ms.sourcegitcommit: a60a55278f645f5d6cda95bcf9895441ade04629
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2019
ms.locfileid: "58878122"
---
# <a name="troubleshoot-kubernetes-deployment-to-azure-stack"></a>Kubernetes 部署到 Azure Stack 故障排除

*适用于Azure Stack 集成系统和 Azure Stack 开发工具包*

> [!Note]  
> Azure Stack 上的 Kubernetes 现为预览版。 在预览目前不支持 azure Stack 离线的场景中。

以下文章讨论了如何排查 Kubernetes 群集问题。 可以按部署所需的元素查看部署警报以及部署的状态。 可能需要从 Azure Stack 或托管 Kubernetes 的 Linux VM 收集部署日志。 此外，可能还需要与 Azure Stack 管理员联系，以从管理终结点检索日志。

## <a name="overview-of-kubernetes-deployment"></a>Kubernetes 部署概述

开始排查群集问题之前，可能需要查看 Azure Stack Kubernetes 群集部署过程。 该部署使用 Azure 资源管理器解决方案模板来为群集创建 VM 并安装 ACS 引擎。

### <a name="kubernetes-deployment-workflow"></a>Kubernetes 部署工作流

下图显示了用于部署群集的一般过程。

![部署 Kubernetes 过程](media/azure-stack-solution-template-kubernetes-trouble/002-Kubernetes-Deploy-Flow.png)

### <a name="deployment-steps"></a>部署步骤

1. 从市场项收集输入参数。

    输入设置 Kubernetes 群集所需的值，包括：
    -  **用户名**：构成 Kubernetes 群集和 DVM 的 Linux 虚拟机的用户名。
    -  **SSH 公钥**：用于向所有作为 Kubernetes 群集和 DVM 的一部分创建的 Linux 计算机授权的密钥。
    -  **服务主体**：供 Kubernetes Azure 云提供商使用的 ID。 创建服务主体时标识为应用程序 ID 的客户端 ID。 
    -  **客户端机密**：创建服务主体时创建的密钥。

2. 创建部署 VM 和自定义脚本扩展。
    -  使用市场 Linux 映像 **Ubuntu Server 16.04 LTS** 创建部署 Linux VM。
    -  下载并运行从 marketplace 的自定义脚本扩展。 该脚本是“用于 Linux 2.0 的自定义脚本”。
    -  运行 DVM 自定义脚本。 该脚本执行以下任务：
        1. 从 Azure 资源管理器元数据终结点获取库终结点。
        2. 从 Azure 资源管理器元数据终结点获取 Active Directory 资源 ID。
        3. 为 ACS 引擎加载 API 模型。
        4. 将 ACS 引擎部署到 Kubernetes 群集，然后将 Azure Stack 云配置文件保存到 `/etc/kubernetes/azurestackcloud.json`。
3. 创建主 VM。

4. 下载并运行自定义脚本扩展。

5. 运行主脚本。

    该脚本执行以下任务：
    - 安装 etcd、Docker 和 Kubernetes 资源（如 kubelet）。 etcd 是一种分布式键值存储，用于跨一组计算机存储数据。 Docker 支持基本功能操作系统级别虚拟化（称为容器）。 Kubelet 是在每个 Kubernetes 节点上运行的节点代理。
    - 设置了**etcd**服务。
    - 设置了**kubelet**服务。
    - 启动 kubelet。 此任务涉及以下步骤：
        1. 启动 API 服务。
        2. 启动控制器服务。
        3. 启动计划程序服务。
6. 创建代理 VM。

7. 下载并运行自定义脚本扩展。

7. 运行代理脚本。 代理自定义脚本执行以下任务：
    - 将安装**etcd**。
    - 设置了**kubelet**服务。
    - 加入 Kubernetes 群集。

## <a name="steps-for-troubleshooting"></a>故障排除步骤

可以在支持 Kubernetes 群集的 VM 上收集日志。 还可以查看部署日志。 可能还需要与 Azure Stack 管理员联系，以便验证你需要使用的 Azure Stack 版本并从与部署相关的 Azure Stack 获取日志。

1. 审阅[部署状态](#review-deployment-status)和从主节点在 Kubernetes 群集中检索日志。
2. 确保使用最新版本的 Azure Stack。 如果不确定使用的是哪个版本，请与 Azure Stack 管理员联系。
3.  查看 VM 创建文件。 可能遇到了以下问题：  
    - 公钥可能无效。 查看创建的密钥。  
    - 创建 VM 可能触发了内部错误或触发了创建错误。 许多因素（包括 Azure Stack 订阅的容量限制）都可能导致错误。
    - 请确保 VM 的完全限定的域名 (FQDN) 开头重复的前缀。
4.  如果 VM **正常**，请评估 DVM。 如果 DVM 有一条错误消息：

    - 公钥可能无效。 查看创建的密钥。  
    - 需要与 Azure Stack 管理员联系，以使用特权终结点检索 Azure Stack 的日志。 有关详细信息，请参阅 [Azure Stack 诊断工具](https://docs.microsoft.com/azure/azure-stack/azure-stack-diagnostics)。
5. 如果对部署有疑问，可以在 [Azure Stack 论坛](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack)中提问，或查看是否已经有人回答了该问题。 

## <a name="review-deployment-status"></a>查看部署状态

部署 Kubernetes 群集时，可以查看部署状态以检查任何问题。

1. 打开 [Azure Stack 门户](https://portal.local.azurestack.external)。
2. 选择“资源组”，然后选择在部署 Kubernetes 群集时使用的资源组名称。
3. 依次选择“部署”、“部署名称”。

    ![故障排除](media/azure-stack-solution-template-kubernetes-trouble/azure-stack-kub-trouble-report.png)

4.  查看故障排除窗口。 部署的每个资源提供以下信息：
    
    | 属性 | 描述 |
    | ----     | ----        |
    | 资源 | 资源的名称。 |
    | Type | 资源提供程序和资源的类型。 |
    | 状态 | 项状态。 |
    | 时间戳 | 时间的 UTC 时间戳。 |
    | 操作详细信息 | 操作详细信息，例如操作中涉及的资源提供程序、资源终结点和资源名称。 |

    每个项都有绿色或红色的状态图标。

## <a name="review-deployment-logs"></a>查看部署日志

如果在 Azure Stack 门户不提供足够的信息，以便进行故障排除或克服部署失败下, 一步是深入到群集日志。 若要手动检索部署日志，通常需要连接到群集的主虚拟机之一。 更简单的另一种方法是下载并运行以下[Bash 脚本](https://aka.ms/AzsK8sLogCollectorScript)Azure Stack 团队提供的。 此脚本连接到此 DVM 和群集的虚拟机、 收集相关的系统和群集日志，并将它们下载到工作站。

### <a name="prerequisites"></a>必备组件

你将需要在用于管理 Azure Stack 的计算机上的 Bash 提示符。 在 Windows 计算机上，你可以获取一个 Bash 提示通过安装[Git 的 Windows](https://git-scm.com/downloads)。 安装后，寻找_Git Bash_开始菜单中。

### <a name="retrieving-the-logs"></a>检索日志

请执行以下步骤收集并下载群集日志：

1. 打开 Bash 提示符。 在 Windows 计算机中，打开_Git Bash_或运行： `C:\Program Files\Git\git-bash.exe`。

2. 通过在 Bash 提示符中运行以下命令下载日志收集器脚本：

    ```Bash  
    mkdir -p $HOME/kuberneteslogs
    cd $HOME/kuberneteslogs
    curl -O https://raw.githubusercontent.com/msazurestackworkloads/azurestack-gallery/master/diagnosis/getkuberneteslogs.sh
    chmod 744 getkuberneteslogs.sh
    ```

3. 该脚本所需的信息查找并运行它：

    | 参数           | 描述                                                                                                      | 示例                                                                       |
    |---------------------|------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
    | -d, --vmd-host      | 公共 IP 或此 DVM 的完全限定的域名 (FQDN)。 虚拟机名称开头`vmd-`。 | IP:192.168.102.38<br>DNS: vmd myk8s.local.cloudapp.azurestack.external |
    | -h、--help  | 打印命令的用法。 | |
    | -i、--identity-file | 创建 Kubernetes 群集时，RSA 私钥文件传递到 marketplace 项。 需要远程连接到 Kubernetes 节点中。 | C:\data\id_rsa.pem (Putty)<br>~/.ssh/id_rsa (SSH)
    | -m, --master-host   | 公共 IP 或 Kubernetes 主节点的完全限定的域名 (FQDN)。 虚拟机名称开头`k8s-master-`。 | IP:192.168.102.37<br>FQDN: k8s-12345.local.cloudapp.azurestack.external      |
    | -u、--user          | 创建 Kubernetes 群集时，用户名将传递给 marketplace 项。 需要远程连接到 Kubernetes 节点中 | azureuser （默认值） |


   当您添加参数值时，你的命令可能如下所示：

    ```Bash  
    ./getkuberneteslogs.sh --identity-file "C:\id_rsa.pem" --user azureuser --vmd-host 192.168.102.37
     ```

4. 在几分钟后，该脚本将输出到一个名为目录收集的日志`KubernetesLogs_{{time-stamp}}`。 其中每个虚拟机属于群集找到一个目录。

    日志收集器脚本还将在日志文件中查找错误并包括故障排除步骤，如果它恰好发现一个已知的问题。 请确保正在运行的脚本，以提高查找已知的问题的可能性的最新版本。

> [!Note]  
> 请查看此 GitHub[存储库](https://github.com/msazurestackworkloads/azurestack-gallery/tree/master/diagnosis)若要了解有关日志收集器脚本的更多详细信息。

## <a name="next-steps"></a>后续步骤

[将 Kubernetes 部署到 Azure Stack](azure-stack-solution-template-kubernetes-deploy.md)

[（适用于 Azure Stack 操作员） 添加到 Marketplace 的 Kubernetes 群集](../azure-stack-solution-template-kubernetes-cluster-add.md)

[Azure 上的 Kubernetes](https://docs.microsoft.com/azure/container-service/kubernetes/container-service-kubernetes-walkthrough)
