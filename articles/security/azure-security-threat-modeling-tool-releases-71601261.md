---
title: Threat Modeling Tool 发行版 - Microsoft Threat Modeling Tool - Azure | Microsoft Docs
description: 阐述 Threat Modeling Tool 的发行说明
services: security
documentationcenter: na
author: jegeib
manager: jegeib
editor: jegeib
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/25/2019
ms.author: jegeib
ms.openlocfilehash: 55c781d0c6284de1382c9d3e614621c40963194b
ms.sourcegitcommit: a7331d0cc53805a7d3170c4368862cad0d4f3144
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55302904"
---
# <a name="threat-modeling-tool-update-release-71601261---1292019"></a>Threat Modeling Tool 更新版 7.1.60126.1 - 2019 年 1 月 29 日

Microsoft Threat Modeling Tool 7.1.60126.1 版已于 2019 年 1 月 29 日发布，包含以下更改：

- .NET 所需的最低版本已增至 [.Net 4.7.1](http://go.microsoft.com/fwlink/?LinkId=863262)。
- 由于 .NET 依赖关系，Windows 所需的最低版本已增至 [Windows 10 周年更新](https://blogs.windows.com/windowsexperience/2016/08/02/how-to-get-the-windows-10-anniversary-update/#HTkoK5Zdv0g2F2Zq.97)。
- 模型验证切换功能已添加到此工具的“选项”菜单中。
- 威胁属性中的多个链接已更新。
- 对此工具的主屏幕进行了些许 UX 更改。
- Threat Modeling Tool 现在继承了主机操作系统的 TLS 设置，并在需要 TLS 1.2 或更高版本的环境中受支持。

## <a name="feature-changes"></a>功能更改

### <a name="model-validation-option"></a>“模型验证”选项

根据客户反馈，已向该工具添加一个选项以启用或禁用模型验证。 以前，如果模板使用两个对象之间的单个单向数据流，你可能会在“消息”框中收到一条错误消息指示：ObjectsName 至少需要一个“Any”。 禁用模型验证将阻止在视图中显示这些警告。

可在“文件”->“设置”->“选项”菜单中找到打开和关闭模型验证的切换选项。 此设置的默认值为“禁用”。

![“模型验证”选项](./media/azure-security-threat-modeling-tool-releases-71601261/tmt_model_validation_option.png)

## <a name="system-requirements"></a>系统要求

- 支持的操作系统
  - [Microsoft Windows 10 周年更新](https://blogs.windows.com/windowsexperience/2016/08/02/how-to-get-the-windows-10-anniversary-update/#HTkoK5Zdv0g2F2Zq.97)或更高版本
- 所需的 .NET 版本
  - [.Net 4.7.1](http://go.microsoft.com/fwlink/?LinkId=863262) 或更高版本
- 其他要求
  - 需要建立 Internet 连接才能接收工具和模板的更新。

## <a name="known-issues"></a>已知问题

### <a name="unsupported-systems"></a>不受支持的系统

#### <a name="issue"></a>问题

无法安装 .NET 4.7.1 或更高版本的 Windows 10 系统的用户，例如 Windows 10 企业版 LTSB（版本 1507），将无法在升级后打开该工具。 这些较旧版本的 Windows 不再是 Threat Modeling Tool 的支持平台，不应安装最新更新。

#### <a name="workaround"></a>解决方法

已安装最新更新的 Windows 10 企业版 LTSB （版本 1507）的用户可以通过“应用和功能”中的卸载对话框，还原到以前版本的 Threat Modeling Tool。

## <a name="documentation-and-feedback"></a>文档和反馈

- Threat Modeling Tool 的文档位于 [docs.microsoft.com](https://docs.microsoft.com/azure/security/azure-security-threat-modeling-tool)，其中包含[有关如何使用该工具](https://docs.microsoft.com/azure/security/azure-security-threat-modeling-tool-getting-started)的信息。

## <a name="next-steps"></a>后续步骤

下载最新版本的 [Microsoft Threat Modeling Tool](https://aka.ms/threatmodelingtool)。