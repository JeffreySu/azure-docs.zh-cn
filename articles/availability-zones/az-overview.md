---
title: 什么是 Azure 可用性区域？ | Microsoft Docs
description: 若要在 Azure 中创建具有高可用性和弹性的应用程序，可用性区域提供了可用于运行资源的物理独立位置。
services: ''
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: ''
ms.assetid: ''
ms.service: azure
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/02/2019
ms.author: cynthn
ms.custom: mvc I am an ITPro and application developer, and I want to protect (use Availability Zones) my applications and data against data center failure (to build Highly Available applications).
ms.openlocfilehash: 557757fc4d99fe57ad545e9d2eebcce61ddb3a8f
ms.sourcegitcommit: 62d3a040280e83946d1a9548f352da83ef852085
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59268715"
---
# <a name="what-are-availability-zones-in-azure"></a>什么是 Azure 中的可用性区域？
可用性区域是一个高可用性产品/服务，在数据中心发生故障时可以保护应用程序和数据。 可用性区域是 Azure 区域中独特的物理位置。 每个区域由一个或多个数据中心组成，这些数据中心配置了独立电源、冷却和网络。 为确保能够进行复原，所有已启用的区域中必须至少有三个单独的区域。 区域中可用性区域的物理隔离可以在发生数据中心故障的情况下保护应用程序和数据。 区域冗余服务可跨可用性区域复制应用程序和数据，以防范单点故障。 Azure 凭借可用性区域提供一流的 99.99% VM 运行时间 SLA。 完整 [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) 说明了 Azure 作为整体的保证可用性。

Azure 区域中的可用性区域是容错域和更新域的组合。 例如，如果在 Azure 区域的三个区域中创建三个或更多 VM，则 VM 将有效分布在三个容错域和三个更新域中。 Azure 平台会识别更新域上的此分布，以确保不同区域中的 VM 不会同时更新。

通过将计算、存储、网络和数据资源共置在一个区域并将其复制到其他区域，在应用程序体系结构中内置高可用性。 支持可用性区域的 Azure 服务划分为两类：

- **区域服务** – 将资源（例如虚拟机、托管磁盘和 IP 地址）固定到特定的区域，或
- **区域冗余服务** – 平台自动跨区域复制（例如区域冗余存储和 SQL 数据库）。

若要在 Azure 上实现全面的业务连续性，可结合使用可用性区域和 Azure 区域对来构建应用程序体系结构。 可以使用 Azure 区域中的可用性区域以同步方式复制应用程序和数据以实现高可用性，并以异步方式跨 Azure 区域复制以实现灾难恢复保护。
 
![地区中发生故障的一个区域的概念视图](./media/az-overview/az-graphic-two.png)

## <a name="regions-that-support-availability-zones"></a>支持可用性区域的地区

- 美国中部
- 美国东部
- 美国东部 2
- 法国中部
- 北欧
- 东南亚 
- 英国南部&#42;
- 西欧
- 美国西部 2



## <a name="services-that-support-availability-zones"></a>支持可用性区域的服务
支持可用性区域的 Azure 服务有：

- Linux 虚拟机
- Windows 虚拟机
- 虚拟机规模集
- 托管磁盘
- 标准负载均衡器&#42;
- 标准公共 IP 地址&#42;
- 区域冗余存储
- SQL 数据库
- 事件中心
- 服务总线（仅限高级层）
- VPN 网关
- ExpressRoute
- 应用程序网关（预览版）

&#42;在英国南部 2019 年 3 月 25 日之前创建的资源很快将转换为区域冗余。 2019 年 3 月 25 日之后创建的资源将立即区域冗余。

## <a name="services-resiliency"></a>服务复原能力
所有 Azure 管理服务，旨在从免受区域级故障中复原。 范围的故障，在区域中的一个或多个可用性区域故障具有较小故障半径相比整个区域的故障。 从区域级故障的管理服务在区域中或从另一个 Azure 区域，azure 可以恢复。 Azure 中的区域，以避免影响客户资源在区域内跨可用性区域部署任何失败一次执行关键维护一个区域。

## <a name="pricing"></a>定价
在可用性区域中部署虚拟机不会产生额外的费用。 当两个或更多个 VM 部署在一个 Azure 区域中的两个或更多个可用性区域时，可获得 99.99% VM 运行时间 SLA。 会产生可用性区域间 VM 到 VM 的数据传输费用。 有关详细信息，请查看[带宽定价](https://azure.microsoft.com/pricing/details/bandwidth/)页。


## <a name="get-started-with-availability-zones"></a>可用性区域入门
- [创建虚拟机](../virtual-machines/windows/create-portal-availability-zone.md)
- [添加托管磁盘使用 PowerShell](../virtual-machines/windows/attach-disk-ps.md#add-an-empty-data-disk-to-a-virtual-machine)
- [创建区域冗余虚拟机规模集](../virtual-machine-scale-sets/virtual-machine-scale-sets-use-availability-zones.md)
- [具有区域冗余前端使用标准负载均衡器跨区域负载均衡 Vm](../load-balancer/load-balancer-standard-public-zone-redundant-cli.md)
- [使用具有区域性前端的标准负载均衡器在区域内的负载均衡 Vm](../load-balancer/load-balancer-standard-public-zonal-cli.md)
- [区域冗余存储](../storage/common/storage-redundancy-zrs.md)
- [SQL 数据库](../sql-database/sql-database-high-availability.md#zone-redundant-configuration)
- [事件中心异地灾难恢复](../event-hubs/event-hubs-geo-dr.md#availability-zones)
- [服务总线异地灾难恢复](../service-bus-messaging/service-bus-geo-dr.md#availability-zones)
- [创建区域冗余的虚拟网关](../vpn-gateway/create-zone-redundant-vnet-gateway.md)


## <a name="next-steps"></a>后续步骤
- [快速入门模板](https://aka.ms/azqs)
