---
title: 为 ASC for IoT 预览版创建自定义警报 | Microsoft Docs
description: 为 ASC for IoT 创建并分配自定义设备警报。
services: ascforiot
documentationcenter: na
author: mlottner
manager: barbkess
editor: ''
ms.assetid: d1757868-da3d-4453-803a-7e3a309c8ce8
ms.service: ascforiot
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2019
ms.author: mlottner
ms.openlocfilehash: 591000f251d384b961569f9d7ca09ae93edea617
ms.sourcegitcommit: cf971fe82e9ee70db9209bb196ddf36614d39d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58541711"
---
# <a name="quickstart-create-custom-alerts"></a>快速入门：创建自定义警报

> [!IMPORTANT]
> ASC for IoT 目前以公开预览版提供。
> 此预览版在提供时没有附带服务级别协议，不建议将其用于生产工作负荷。 某些功能可能不受支持或者受限。 有关详细信息，请参阅 [Microsoft Azure 预览版补充使用条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)。

使用自定义安全组和警报，可以充分利用端到端的安全信息和分类设备知识来确保提高整个 IoT 解决方案的安全性。 

## <a name="why-use-custom-alerts"></a>为何要使用自定义警报？ 

可以最清楚地了解自己的 IoT 设备。

对于完全了解其预期设备行为的客户，ASC for IoT 可将这种了解转化为设备行为策略，并在背离预期的正常行为时发出警报。

## <a name="security-groups"></a>安全组

使用安全组可以定义设备的逻辑组，并集中管理设备的安全状态。

这些组可以表示具有特定硬件的设备、部署在某个位置的设备，或适合具体需求的其他任何组。

安全组由名为 **SecurityGroup** 的安全模块孪生标记属性定义。 更改此属性的值可以更改设备的安全组。  

默认情况下，IoT 中心内的每个 IoT 解决方案都有一个名为 **default** 的安全组。

使用安全组可将设备分组为逻辑类别。 创建组之后，请将其分配到所选的自定义警报，以最大程度地提高端到端解决方案的效率。 

## <a name="customize-an-alert"></a>自定义警报

1. 打开 IoT 中心。 
2. 依次选择“安全性”、“自定义警报”。 
3. 选择要将自定义设置应用到的安全组。 
4. 单击“添加自定义警报”
5. 输入警报名称（请注意，创建警报后无法更改警报名称）。 
6. 从下拉列表中选择自定义警报行为。 
7. 编辑所需的属性，然后单击“确定”。
8. 请务必单击“保存”。 如果不保存新警报，下一次关闭 IoT 中心时会删除该警报。

 
## <a name="alerts-available-for-customization"></a>可自定义的警报

下表提供了可自定义的警报的摘要。

| 严重性 | Name                                                                                                    | 数据源 | 说明                                                                                                                                     |
|----------|---------------------------------------------------------------------------------------------------------|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| 低      | 自定义警报 - AMQP 协议中云到设备的消息数目不在允许的范围内          | IoT 中心     | 时间窗口中云到设备的消息（AMQP 协议）数量不在配置的允许范围内                                  |
| 低      | 自定义警报 - AMQP 协议中已拒绝的云到设备的消息数目不在允许的范围内 | IoT 中心     | 时间窗口中由设备拒绝的云到设备的消息（AMQP 协议）数量不在配置的允许范围内 |
| 低      | 自定义警报 - AMQP 协议中设备到云的消息数目不在允许的范围内          | IoT 中心     | 时间窗口中设备到云的消息（AMQP 协议）数量不在配置的允许范围内                                  |
| 低      | 自定义警报 - 直接方法调用数目不在允许的范围内                              | IoT 中心     | 时间窗口中的直接方法调用数量不在配置的允许范围内                                                     |
| 低      | 自定义警报 - 文件上传数目不在允许的范围内                                       | IoT 中心     | 时间窗口中的文件上传数量不在配置的允许范围内                                                              |
| 低      | 自定义警报 - HTTP 协议中云到设备的消息数目不在允许的范围内          | IoT 中心     | 时间窗口中云到设备的消息（HTTP 协议）数量不在配置的允许范围内                                  |
| 低      | 自定义警报 - HTTP 协议中已拒绝的云到设备的消息数目不在允许的范围内 | IoT 中心     | 时间窗口中由设备拒绝的云到设备的消息（HTTP 协议）数量不在配置的允许范围内 |
| 低      | 自定义警报 - HTTP 协议中设备到云的消息数目不在允许的范围内          | IoT 中心     | 时间窗口中设备到云的消息（HTTP 协议）数量不在配置的允许范围内                                  |
| 低      | 自定义警报 - MQTT 协议中云到设备的消息数目不在允许的范围内          | IoT 中心     | 时间窗口中云到设备的消息（MQTT 协议）数量不在配置的允许范围内                                  |
| 低      | 自定义警报 - MQTT 协议中已拒绝的云到设备的消息数目不在允许的范围内 | IoT 中心     | 时间窗口中由设备拒绝的云到设备的消息（MQTT 协议）数量不在配置的允许范围内 |
| 低      | 自定义警报 - MQTT 协议中设备到云的消息数目不在允许的范围内          | IoT 中心     | 时间窗口中设备到云的消息（MQTT 协议）数量不在配置的允许范围内                                  |
| 低      | 自定义警报 - 命令队列清除数目不在允许的范围内                               | IoT 中心     | 时间窗口中的命令队列清除数量不在配置的允许范围内                                                      |
| 低      | 自定义警报 - 孪生更新数目不在允许的范围内                                       | IoT 中心     | 时间窗口中的孪生更新数量不在配置的允许范围内                                                              |
| 低      | 自定义警报 - 未授权的操作数目不在允许的范围内                            | IoT 中心     | 时间窗口中未授权的操作数量不在配置的允许范围内                                                   |
| 低      | 自定义警报 - 活动连接数目不在允许的范围内                                        | 代理       | 时间窗口中的活动连接数量不在配置的允许范围内                                                        |
| 低      | 自定义警报 - 与不允许的 IP 建立了出站连接                              | 代理       | 与不允许的 IP 建立了出站连接                                                                                  |
| 低      | 自定义警报 - 失败的本地登录次数不在允许的范围内                                | 代理       | 时间窗口中失败的本地登录次数不在配置的允许范围内                                                       |
| 低      | 自定义警报 - 不允许某个用户登录                                                      | 代理       | 不允许某个本地用户登录到设备                                                                                        |
| 低      | 自定义警报 - 不允许执行某个进程                                               | 代理       | 不允许在设备上执行某个进程 |          |

## <a name="next-steps"></a>后续步骤

请转到下一篇文章了解如何部署安全代理...

> [!div class="nextstepaction"]
> [部署安全代理](select-deploy-agent.md)