---
title: Azure IoT 协议网关 | Microsoft Docs
description: 如何使用 Azure IoT 协议网关扩展 IoT 中心功能及协议支持，使设备利用不由 IoT 中心本机支持的协议即可连接到该中心。
author: robinsh
manager: philmea
ms.author: robinsh
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 07/11/2017
ms.openlocfilehash: ecce53420a92713ad2dcfcc7e0fed9fc226b1d52
ms.sourcegitcommit: 8313d5bf28fb32e8531cdd4a3054065fa7315bfd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2019
ms.locfileid: "59046421"
---
# <a name="support-additional-protocols-for-iot-hub"></a>支持 IoT 中心的其他协议
Azure IoT 中心通过 MQTT、AMQP 和 HTTPS 协议以本机方式支持通信。 在某些情况下，设备或现场网关可能无法使用其中一个标准协议，并需要协议适配。 在这种情况下，可以使用自定义网关。 自定义网关通过桥接进出 IoT 中心的流量，为 IoT 中心终结点启用协议适配。 可以使用 [Azure IoT 协议网关](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md)作为自定义网关，来为 IoT 中心启用协议自适应。

## <a name="azure-iot-protocol-gateway"></a>Azure IoT 协议网关
Azure IoT 协议网关是协议自适应的框架，旨在用来与 IoT 中心进行高缩放性双向设备通信。 协议网关是一种传递组件，通过特定的协议接受设备连接。 它通过 AMQP 1.0 桥接发往 IoT 中心的流量。 

可以使用 Azure Service Fabric、Azure 云服务辅助角色或 Windows 虚拟机，以高度缩放的方式在 Azure 中部署协议网关。 此外，可将协议网关部署在本地环境中，例如现场网关。

Azure IoT 协议网关包含可让用户根据需要自定义 MQTT 协议行为的 MQTT 协议适配器。 IoT 中心对 MQTT v3.1.1 协议提供内置支持，因此，需要进行协议自定义或者对其他功能有具体要求时，应只考虑使用 MQTT 协议适配器。

MQTT 适配器还会演示用来为其他协议构建协议适配器的编程模型。 此外，借助 Azure IoT 协议网关编程模型，可对专门化处理插入自定义组件，例如自定义身份验证、消息转换、压缩/解压缩，或加密/解密设备与 IoT 中心之间的流量。

为了提供弹性，在开源软件项目中提供了 Azure IoT 协议网关和 MQTT 实现。 可以使用开放源代码项目添加对各种协议和协议版本的支持，或者为方案自定义实现。 

## <a name="next-steps"></a>后续步骤
要了解有关 Azure IoT 协议网关的详细信息以及如何使用并将其部署为 IoT 解决方案的一部分，请参阅：

* [Azure IoT 协议网关存储库在 GitHub 上](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md)
* [Azure IoT 协议网关开发人员指南](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/docs/DeveloperGuide.md)

若要深入了解如何规划 IoT 中心部署，请参阅：

* [与事件中心比较][lnk-compare]
* [缩放、高可用性和灾难恢复][lnk-scaling]
* [IoT 中心开发人员指南][lnk-devguide]

[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
