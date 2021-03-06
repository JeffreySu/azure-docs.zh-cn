---
title: 了解 Azure IoT 中心消息路由 | Microsoft Docs
description: 开发人员指南 - 如何使用消息路由发送设备到云的消息。 包含有关发送遥测和非遥测数据的信息。
author: ash2017
manager: briz
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 08/13/2018
ms.author: asrastog
ms.openlocfilehash: dc5bfe6b431659b7b99140eb29a0e64922a42275
ms.sourcegitcommit: 30a0007f8e584692fe03c0023fe0337f842a7070
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57576325"
---
# <a name="use-iot-hub-message-routing-to-send-device-to-cloud-messages-to-different-endpoints"></a>使用 IoT 中心消息路由到不同的终结点发送设备到云的消息

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-partial.md)]

消息路由使你能够以自动、可缩放以及可靠的方式将消息从设备发送到云服务。 消息路由可用于： 

* **发送设备遥测消息以及事件**（即设备生命周期事件和设备孪生更改事件）到内置终结点和自定义终结点。 了解有关[路由终结点](#routing-endpoints)。

* **在将数据路由到各个终结点之前对数据进行筛选**，筛选方法是通过应用丰富的查询。 消息路由允许你查询消息属性和消息正文以及设备孪生标记和设备孪生属性。 深入了解如何使用[消息路由中的查询](iot-hub-devguide-routing-query-syntax.md)。

IoT 中心需要这些服务终结点的写入权限，以便使用消息路由。 如果通过 Azure 门户配置终结点，则为你添加必要权限。 请确保将服务配置为支持预期吞吐量。 在首次配置 IoT 解决方案时，可能需要监视附加终结点，并针对实际负载进行任意的必要调整。

IoT 中心为所有“设备到云”消息传递定义[通用格式](iot-hub-devguide-messages-construct.md)，以实现跨协议的互操作性。 如果某条消息与多个路由匹配，而这些路由指向同一终结点，则 IoT 中心仅向该终结点传递一次消息。 因此无需在服务总线队列或主题中配置重复数据删除。 在分区队列中，分区相关性可保障消息排序。 使用本教程了解如何[配置消息路由](tutorial-routing.md)。

## <a name="routing-endpoints"></a>路由终结点

IoT 中心有一个默认的内置终结点（消息/事件），此终结点与事件中心兼容。 可以通过将订阅中的其他服务链接到中心来创建要将消息路由到的[自定义终结点](iot-hub-devguide-endpoints.md#custom-endpoints)。 IoT 中心目前支持将以下服务作为自定义终结点：

### <a name="built-in-endpoint"></a>内置终结点

可以使用标准[事件中心集成和 SDK](iot-hub-devguide-messages-read-builtin.md) 接收来自内置终结点（消息/事件）的设备到云的消息。 创建一个路由后，数据将停止流向内置的端点，除非该终结点创建一个路由。

### <a name="azure-blob-storage"></a>Azure Blob 存储

IoT 中心支持将数据写入 Azure Blob 存储中[Apache Avro](https://avro.apache.org/)以及 JSON 格式。 要编码 JSON 格式的功能是在 IoT 中心现已推出，除美国东部、 美国西部和欧洲西部之外的所有区域中预览。 默认值为 AVRO。 配置 blob 存储终结点时，可以仅设置的编码格式。 不能编辑现有终结点的格式。 在使用 JSON 编码时，必须将 contentType 设置为 JSON 和到 utf-8 消息中的 contentEncoding[系统属性](iot-hub-devguide-routing-query-syntax.md#system-properties)。 可以选择专门使用 IoT 中心创建或更新 REST API 的编码格式[RoutingStorageContainerProperties](https://docs.microsoft.com/rest/api/iothub/iothubresource/createorupdate#routingstoragecontainerproperties)，在 Azure 门户[Azure CLI](https://docs.microsoft.com/cli/azure/iot/hub/routing-endpoint?view=azure-cli-latest)或[AzurePowershell](https://docs.microsoft.com/powershell/module/az.iothub/add-aziothubroutingendpoint?view=azps-1.3.0)。 下图显示了如何在 Azure 门户中选择的编码格式。

![Blob 存储终结点编码](./media/iot-hub-devguide-messages-d2c/blobencoding.png)

IoT 中心将在消息达到特定大小或在经过一定的事件后，对消息进行批处理并将数据写入 Blob。 IoT 中心默认为以下文件命名约定：

```
{iothub}/{partition}/{YYYY}/{MM}/{DD}/{HH}/{mm}
```

你可以使用任何文件命名约定，但必须使用所有列出的令牌。 如果没有要写入的数据，IoT 中心会写入到一个空 blob。

当路由到 blob 存储，我们建议登记 blob，然后循环访问它们，以确保所有容器都读取而无需进行任何假设分区。 分区范围可能会发生更改期间[Microsoft 启动故障转移](iot-hub-ha-dr.md#microsoft-initiated-failover)或 IoT 中心[手动故障转移](iot-hub-ha-dr.md#manual-failover-preview)。 可以使用[列表 Blob API](https://docs.microsoft.com/rest/api/storageservices/list-blobs)要枚举的 blob 列表。 请参阅下面的示例作为指导。

   ```csharp
        public void ListBlobsInContainer(string containerName, string iothub)
        {
            var storageAccount = CloudStorageAccount.Parse(this.blobConnectionString);
            var cloudBlobContainer = storageAccount.CreateCloudBlobClient().GetContainerReference(containerName);
            if (cloudBlobContainer.Exists())
            {
                var results = cloudBlobContainer.ListBlobs(prefix: $"{iothub}/");
                foreach (IListBlobItem item in results)
                {
                    Console.WriteLine(item.Uri);
                }
            }
        }
   ```

### <a name="service-bus-queues-and-service-bus-topics"></a>服务总线队列和服务总线主题

用作 IoT 中心终结点的服务总线队列和主题不得启用**会话**或**重复检测**选项。 如果启用了其中任一选项，该终结点会在 Azure 门户中显示为**无法访问**。

### <a name="event-hubs"></a>事件中心

除了与事件中心兼容的内置终结点外，还可以将数据路由到事件中心类型的自定义终结点。 

## <a name="reading-data-that-has-been-routed"></a>读取已路由的数据

可以按照此[教程](tutorial-routing.md)配置一个路由。

使用以下教程了解如何从终结点读取消息。

* 从[内置终结点](quickstart-send-telemetry-node.md)进行读取

* 从 [Blob 存储](../storage/blobs/storage-blob-event-quickstart.md)进行读取

* 从[事件中心](../event-hubs/event-hubs-dotnet-standard-getstarted-send.md)进行读取

* 从[服务总线队列](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)进行读取

* 从[服务总线主题](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)进行读取

## <a name="fallback-route"></a>回退路由

回退路由将所有不满足任何现有路由上的查询条件的消息发送到与[事件中心](/azure/event-hubs/)兼容的内置事件中心（消息/事件）。 如果已启用消息路由，则可以启用此回退路由功能。 创建一个路由后，数据停止流向该内置-中-终结点，除非该终结点创建一个路由。 如果没有到内置终结点的路由并且已启用回退路由，则仅与路由上的任何查询条件不匹配的消息将被发送到内置终结点。 此外，如果已删除现有路由，必须启用回退路由才能接收内置终结点处的所有数据。 

可以在 Azure 门户->“消息路由”边栏选项卡中启用/禁用回退路由。 还可以将 Azure 资源管理器用于 [FallbackRouteProperties](/rest/api/iothub/iothubresource/createorupdate#fallbackrouteproperties) 来为回退路由使用自定义终结点。

## <a name="non-telemetry-events"></a>非遥测事件

除了设备遥测外，消息路由也能够发送设备孪生更改事件和设备生命周期事件。 例如，如果使用数据源创建一个设置为到**设备孪生更改事件**的路由，IoT 中心会将消息发送到包含设备孪生更改的终结点。 同样，如果使用数据源创建一个设置为到**设备生命周期事件**的路由，IoT 中心将一条消息，此消息指示是否已删除或创建了设备。 

[IoT 中心还集成了 Azure 事件网格](iot-hub-event-grid.md)来发布事件以支持基于这些事件的工作流的实时集成和自动化。 请参阅[消息路由和事件网格之间的主要区别](iot-hub-event-grid-routing-comparison.md)来了解哪种更适合你的方案。

## <a name="testing-routes"></a>测试路由

在创建新路由或编辑现有路由时，应通过示例消息来测试路由查询。 可以测试单个路由或一次测试所有路由，并且在测试期间，不会有消息被路由到终结点。 可以使用 Azure 门户、Azure 资源管理器、Azure PowerShell 和 Azure CLI 来进行测试。 结果有助于确定是否与查询匹配的示例消息、 消息与该查询不匹配或测试无法运行，因为示例消息或查询语法不正确。 若要了解详细信息，请参阅[测试路由](/rest/api/iothub/iothubresource/testroute)和[测试所有路由](/rest/api/iothub/iothubresource/testallroutes)。

## <a name="latency"></a>Latency

使用内置终结点路由设备到云遥测消息时，在创建第一个路由后，端到端延迟略微增大。

在大多数情况下，延迟的平均增为不超过 500 毫秒。 可以使用路由：消息/事件的消息延迟或 d2c.endpoints.latency.builtIn.events IoT 中心指标来监视延迟。 在创建第一个路由后创建或删除任何路由不会影响端到端延迟。

## <a name="monitoring-and-troubleshooting"></a>监视和故障排除

IoT 中心提供了多个与路由和终结点相关的指标，使你能够大致了解你的中心的运行状况和已发送的消息数。 你可以组合来自多项指标的信息来确定问题的根本原因。 例如，使用指标**路由： 删除的遥测消息数**或**d2c.telemetry.egress.dropped**来标识时它们不符合任何路由的查询已删除的消息数和回退路由被禁用。 [IoT 中心指标](iot-hub-metrics.md)列出了默认为 IoT 中心启用的所有指标。

可以使用 REST API[获取终结点运行状况](https://docs.microsoft.com/de-de/rest/api/iothub/iothubresource/getendpointhealth#iothubresource_getendpointhealth)若要获取[运行状况状态](iot-hub-devguide-endpoints.md#custom-endpoints)终结点。 我们建议使用[IoT 中心度量值](iot-hub-metrics.md)与相关的路由的消息延迟，以识别和调试错误终结点运行状况时出现故障或不正常。 例如，对于事件中心的终结点类型，可以监视**d2c.endpoints.latency.eventHubs**。 IoT 中心已建立的最终一致的运行状况状态时，不正常的终结点的状态将更新为正常。

通过使用 Azure Monitor [诊断设置](../iot-hub/iot-hub-monitor-resource-health.md)中的路由诊断日志，可以跟踪发生在路由查询和终结点运行状况的评估期间、由 IoT 中心所察觉到的错误，例如某个终结点已失效。 进行自定义处理，可以将这些诊断日志发送到 Azure Monitor 日志、 事件中心或 Azure 存储中。

## <a name="next-steps"></a>后续步骤

* 若要了解如何创建消息路由，请参阅[使用路由处理 IoT 中心的设备到云消息](tutorial-routing.md)。

* [如何发送设备到云消息](quickstart-send-telemetry-node.md)

* 有关可以用来发送设备到云消息的 SDK 的详细信息，请参阅 [Azure IoT SDK](iot-hub-devguide-sdks.md)。
