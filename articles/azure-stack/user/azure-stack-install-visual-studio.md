---
title: 安装 Visual Studio 并连接到 Azure Stack | Microsoft Docs
description: 了解安装 Visual Studio 并连接到 Azure Stack 所需的步骤
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.service: azure-stack
ms.custom: vs-azure
ms.workload: azure-vs
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/04/2019
ms.author: sethm
ms.reviewer: unknown
ms.lastreviewed: 01/04/2019
ms.openlocfilehash: 274240aab54f27f36734516026e9feebf64ae4b5
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55248106"
---
# <a name="install-visual-studio-and-connect-to-azure-stack"></a>安装 Visual Studio 并连接到 Azure Stack

*适用于：Azure Stack 集成系统和 Azure Stack 开发工具包*

可以使用 Visual Studio 将 Azure 资源管理器[模板](azure-stack-arm-templates.md)写入和部署到 Azure Stack。 这篇文章中的步骤引导您完成上安装 Visual Studio [Azure Stack](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop)，或如果你打算使用通过 Azure Stack 外部的计算机上[VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)。

## <a name="install-visual-studio"></a>安装 Visual Studio

1. 下载并运行此 [Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)。  

2. 打开“Microsoft Web 平台安装程序”。

3. 搜索**Visual Studio Community 2015 with Microsoft Azure SDK-2.9.6**。 依次单击“添加”、“安装”。

4. 卸载**Microsoft Azure PowerShell**安装 Azure SDK 的一部分。

    ![WebPI 安装步骤的屏幕截图](./media/azure-stack-install-visual-studio/image1.png) 

5. [安装适用于 Azure Stack 的 PowerShell](azure-stack-powershell-install.md)

6. 安装完成后，重启操作系统。

## <a name="connect-to-azure-stack-with-azure-ad"></a>使用 Azure AD 连接到 Azure Stack

1. 启动 Visual Studio。

2. 在“视图”菜单中，选择“云资源管理器”。

3. 在新窗格中选择“添加帐户”，然后使用 Azure Active Directory (Azure AD) 凭据登录。  

    ![登录并连接到 Azure Stack 后的 Cloud Explorer 屏幕截图](./media/azure-stack-install-visual-studio/image2.png)

登录后，可以[部署模板](azure-stack-deploy-template-visual-studio.md)或浏览可用的资源类型和资源组以创建自己的模板。  

## <a name="connect-to-azure-stack-with-ad-fs"></a>使用 AD FS 连接到 Azure Stack

1. 启动 Visual Studio。

2. 在“工具”中选择“选项”。

3. 展开**导航窗格**中的“环境”，然后选择“帐户”。

4. 选择“添加”，然后输入“用户 Azure 资源管理器终结点”。  
  对于 Azure Stack 开发工具包，URL 是： `https://management.local.azurestack/external`。  
  对于 Azure Stack 集成系统，URL 是： `https://management.[Region}.[External FQDN]`。

    ![X](./media/azure-stack-install-visual-studio/image5.png)

5. 选择 **添加** 。  

    Visual Studio 调用 Azure 资源管理器，并发现终结点，包括身份验证终结点，用于 Azure Directory 联合身份验证服务 (AD FS)。

    ![登录并连接到 Azure Stack 后的 Cloud Explorer 屏幕截图](./media/azure-stack-install-visual-studio/image6.png)

6. 在“视图”菜单中，选择“Cloud Explorer”。

1. 选择“添加帐户”并使用 AD FS 凭据登录。  

    ![云资源管理器](./media/azure-stack-install-visual-studio/image7.png)

    Cloud Explorer 将查询可用的订阅。 可以选择一个要管理的可用订阅。

    ![云资源管理器](./media/azure-stack-install-visual-studio/image8.png)

8. 浏览现有的资源或资源组，或者部署模板。

## <a name="next-steps"></a>后续步骤

 - 详细了解 Visual Studio[并排比较](https://msdn.microsoft.com/library/ms246609.aspx)与其他 Visual Studio 版本。
 - [为 Azure Stack 开发模板](azure-stack-develop-templates.md)。