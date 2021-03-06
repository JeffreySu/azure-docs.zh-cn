---
title: 入站/出站 IP 地址 - Azure 应用服务 | Microsoft Docs
description: 介绍如何在应用服务中使用入站和出站 IP 地址，以及如何查找应用的此类信息。
services: app-service
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2018
ms.author: cephalin
ms.custom: seodec18
ms.openlocfilehash: 96f580532d9ea45dd767e32c2451243e83af66ea
ms.sourcegitcommit: 0dd053b447e171bc99f3bad89a75ca12cd748e9c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/26/2019
ms.locfileid: "58480798"
---
# <a name="inbound-and-outbound-ip-addresses-in-azure-app-service"></a>Azure 应用服务中的入站和出站 IP 地址

[Azure 应用服务](overview.md)是一个多租户服务（[应用服务环境](environment/intro.md)除外）。 不在应用服务环境中（不在[隔离层](https://azure.microsoft.com/pricing/details/app-service/)中）的应用与其他应用共享网络基础结构。 因此，应用的入站和出站 IP 地址可能不同，在某些情况下甚至可能会更改。 

[应用服务环境](environment/intro.md)使用专用网络基础结构，因此，应用服务环境中运行的应用将获取静态专用 IP 地址用于入站和出站连接。

## <a name="when-inbound-ip-changes"></a>入站 IP 更改时

不管横向扩展的实例数如何，每个应用只有一个入站 IP 地址。 执行以下操作之一时，入站 IP 地址可能会更改：

- 删除应用，然后在不同的资源组中重新创建它。
- 删除资源组和区域组合中的最后一个应用，然后重新创建它。
- 在证书续订等操作期间删除现有的 SSL 绑定（请参阅[续订证书](app-service-web-tutorial-custom-ssl.md#renew-certificates)）。

## <a name="get-static-inbound-ip"></a>获取静态入站 IP

有时，你可能需要对应用使用专用静态 IP 地址。 若要获取静态入站 IP 地址，需要配置[基于 IP 的 SSL 绑定](app-service-web-tutorial-custom-ssl.md#bind-your-ssl-certificate)。 如果并不真正需要使用 SSL 功能来保护应用，甚至可以上传一个自签名证书来实现此绑定。 在基于 IP 的 SSL 绑定中，证书将绑定到 IP 地址本身，因此，应用服务会预配一个静态 IP 地址来实现此目的。 

## <a name="when-outbound-ips-change"></a>出站 IP 更改时

不管横向扩展的实例数如何，每个应用在任意给定时间具有指定数目的出站 IP 地址。 从应用服务应用发起的任何出站连接（例如，与后端数据库的连接）使用某个出站 IP 地址作为源 IP 地址。 无法预先知道给定的应用实例要使用哪个 IP 地址来发起出站连接，因此，后端服务必须向应用的所有出站 IP 地址开放其防火墙。

在较低层（“基本”、“标准”和“高级”）与“高级 V2”层之间缩放应用时，应用的出站 IP 地址集会发生更改。

可以找到的所有出站 IP 地址可以使用您的应用程序，而不考虑定价层，通过查找一套`possibleOutboundIPAddresses`属性中或在**其他出站 IP 地址**字段中**属性** Azure 门户边栏选项卡。 请参阅[查找出站 IP](#find-outbound-ips)。

## <a name="find-outbound-ips"></a>查找出站 IP

若要在 Azure 门户中查找应用当前使用的出站 IP 地址，请单击应用左侧导航窗格中的“属性”。 中列出**出站 IP 地址**字段。

在 [Cloud Shell](../cloud-shell/quickstart.md) 中运行以下命令也可以找到相同的信息。

```azurecli-interactive
az webapp show --resource-group <group_name> --name <app_name> --query outboundIpAddresses --output tsv
```

```azurepowershell
(Get-AzWebApp -ResourceGroup <group_name> -name <app_name>).OutboundIpAddresses
```

若要查找_所有_可能出站 IP 地址为你的应用，而不考虑定价层中，单击**属性**应用的左侧导航窗格中。 中列出**其他出站 IP 地址**字段。

在 [Cloud Shell](../cloud-shell/quickstart.md) 中运行以下命令也可以找到相同的信息。

```azurecli-interactive
az webapp show --resource-group <group_name> --name <app_name> --query possibleOutboundIpAddresses --output tsv
```

```azurepowershell
(Get-AzWebApp -ResourceGroup <group_name> -name <app_name>).PossibleOutboundIpAddresses
```

## <a name="next-steps"></a>后续步骤

了解如何按源 IP 地址限制入站流量。

> [!div class="nextstepaction"]
> [静态 IP 限制](app-service-ip-restrictions.md)
