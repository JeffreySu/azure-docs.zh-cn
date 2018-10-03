---
title: 在 Azure Monitor 中创建、查看和管理活动日志警报
description: 如何从 Azure 门户、资源模板和 PowerShell 创建活动日志警报。
author: msvijayn
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 09/15/2018
ms.author: vinagara
ms.component: alerts
ms.openlocfilehash: 526c50fa4d261a30738c3f24d537fe5e0d765f6d
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "46951298"
---
# <a name="create-view-and-manage-activity-log-alerts-using-azure-monitor"></a>使用 Azure Monitor 创建、查看和管理活动日志警报  

## <a name="overview"></a>概述
活动日志警报是新发生的活动日志事件与警报中指定的条件匹配时激活的警报。

这些警报针对 Azure 资源，可以使用 Azure 资源管理器模板来创建。 此外，还可以在 Azure 门户中创建、更新或删除它们。 通常，可以创建活动日志警报，以便在 Azure 订阅中的资源发生特定更改时接收通知（通常限于特定资源组或资源）。 例如，你可能希望在删除 **myProductionResourceGroup**（示例资源组）中的任何虚拟机时接收通知，或者，可能希望在任何新角色分配到订阅中的用户时接收通知。

> [!IMPORTANT]
> 无法通过活动日志警报创建界面创建服务运行状况警报通知。 若要了解有关创建和使用服务运行状况通知的详细信息，请参阅[接收有关服务运行状况通知的活动日志警报](monitoring-activity-log-alerts-on-service-notifications.md)。

## <a name="manage-alert-rules-for-activity-log-using-azure-portal"></a>使用 Azure 门户管理活动日志的警报规则

> [!NOTE]

>  创建警报规则时，请确保：

> - 范围中的订阅不同于创建警报的订阅。
- 条件必须是配置警报所依据的级别/状态/调用方/资源组/资源 ID/资源类型/事件类别。
- 警报配置 JSON 中没有“anyOf”条件或嵌套的条件（简单而言，只允许一个 allOf，而不允许更多的 allOf/anyOf）。
- 当类别是“管理”时， 必须在警报中至少指定上述条件之一。 不能创建每次在活动日志中创建事件时激活的警报。

### <a name="create-an-alert-rule-for-an-activity-log-using-azure-portal"></a>使用 Azure 门户创建活动日志的警报规则

请按以下过程操作：

1. 在 Azure 门户中，选择“监视” > “警报”
2. 单击“警报”窗口顶部的“新建警报规则”。

     ![新建警报规则](./media/monitor-alerts-unified/AlertsPreviewOption.png)

     此时将显示“创建规则”窗口。

      ![新建警报规则选项](./media/monitoring-activity-log-alerts-new-experience/create-new-alert-rule-options.png)

3. 在“定义警报条件”下提供以下信息，然后单击“完成”。

    - **警报目标：** 查看并选择新警报的目标，使用“按订阅筛选” / “按资源类型筛选”，并从显示的列表中选择资源或资源组。

    > [!NOTE]

    > 可以为活动日志信号选择资源、资源组或整个订阅。

    **预警目标示例视图** ![选择目标](./media/monitoring-activity-log-alerts-new-experience/select-target.png)

    - 在“目标条件”下，单击“添加条件”，将会显示目标的所有可用信号，包括来自各种**活动日志**的那些信号；**监视服务**名称中追加了类别名称。

    - 从**活动日志**类型的各种可能操作的显示列表中选择信号。

    可为此目标信号选择日志历史记录时间线和相应的警报逻辑：

    **添加条件屏幕**

    ![添加条件](./media/monitoring-activity-log-alerts-new-experience/add-criteria.png)

    **历史记录时间**：可以绘制在过去 6/12/24 小时内或过去一周内为所选操作提供的事件。

    **警报逻辑**：

     - **事件级别** - 事件的严重性级别。 “详细”、“信息性”、“警告”、“错误”或“严重”。
     - **状态**：事件的状态。 例如，“已启动”、“失败”或“成功”。
     - **事件发起者**：也称为“调用方”；执行操作的用户的电子邮件地址或 Azure Active Directory 标识符。

        应用了警报逻辑的示例信号图：

        ![ 已选择条件](./media/monitoring-activity-log-alerts-new-experience/criteria-selected.png)

4. 在“定义警报规则详细信息”下提供以下详细信息：

    - **警报规则名称** – 新警报规则的名称
    - **说明** – 新警报规则的说明
    - **将警报保存到资源组** – 选择要在其中保存此新规则的资源组。

5. 在“操作组”下，从下拉菜单中指定要分配到此新警报规则的操作组。 或者，[创建新的操作组](monitoring-action-groups.md)并将其分配到新规则。 若要创建新组，请单击“+ 新建组”。

6. 若要在创建规则后启用规则，请单击“创建后启用规则”选项对应的“是”。
7. 单击“创建警报规则”。

    随即为活动日志创建了新的警报规则，同时，窗口的右上角会显示一条确认消息。

    可以启用、禁用、编辑或删除规则。 [详细了解](#view-and-manage-activity-log-alert-rules-in-azure-portal)如何管理活动日志规则。


另外，可以通过简单的类比来理解在活动日志上创建警报规则时可以基于的条件，那就是通过 [Azure 门户中的活动日志](monitoring-overview-activity-logs.md#query-the-activity-log-in-the-azure-portal)浏览或筛选事件。 在 Azure Monitor - 活动日志中，可以筛选或查找所需的事件，然后使用“添加活动日志警报”按钮创建警报，然后按照教程中上文所述的步骤 4 继续前进。
    
 ![ 从活动日志添加警报](./media/monitoring-activity-log-alerts-new-experience/add-activity-log.png)
    

### <a name="view-and-manage-activity-log-alert-rules-in-azure-portal"></a>在 Azure 门户中查看和管理活动日志警报规则

1. 在 Azure 门户中，单击“监视” > “警报”，然后单击窗口左上角的“管理规则”。

    ![ 管理警报规则](./media/monitoring-activity-log-alerts-new-experience/manage-alert-rules.png)

    此时将显示可用规则的列表。

2. 搜索要修改的活动日志规则。

    ![ 搜索活动日志警报规则](./media/monitoring-activity-log-alerts-new-experience/searth-activity-log-rule-to-edit.png)

    可以使用可用的筛选器（“订阅”、“资源组”、“资源”、“信号类型”或“状态”）来查找想要编辑的活动规则。

    > [!NOTE]

    > 只能编辑“说明”、“目标条件”和“操作组”。

3.  选择规则并双击以编辑规则选项。 进行所需的更改，然后单击“保存”。

    ![ 管理警报规则](./media/monitoring-activity-log-alerts-new-experience/activity-log-rule-edit-page.png)

4.  可以禁用、启用或删除规则。 根据步骤 2 中的详述选择规则后，在窗口顶部选择相应的选项。


## <a name="manage-alert-rules-for-activity-log-using-azure-resource-template"></a>使用 Azure 资源模板管理活动日志的警报规则
若要使用资源管理器模板创建活动日志警报，需要创建 `microsoft.insights/activityLogAlerts` 类型的资源。 然后，填充所有相关属性。 下面是用于创建活动日志警报的模板。

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not the alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for the Action group."
      }
    }
  },
  "resources": [   
    {
      "type": "Microsoft.Insights/activityLogAlerts",
      "apiVersion": "2017-04-01",
      "name": "[parameters('activityLogAlertName')]",      
      "location": "Global",
      "properties": {
        "enabled": "[parameters('activityLogAlertEnabled')]",
        "scopes": [
            "[subscription().id]"
        ],        
        "condition": {
          "allOf": [
            {
              "field": "category",
              "equals": "Administrative"
            },
            {
              "field": "operationName",
              "equals": "Microsoft.Resources/deployments/write"
            },
            {
              "field": "resourceType",
              "equals": "Microsoft.Resources/deployments"
            }
          ]
        },
        "actions": {
          "actionGroups":
          [
            {
              "actionGroupId": "[parameters('actionGroupResourceId')]"
            }
          ]
        }
      }
    }
  ]
}
```
对于此演练，上面的示例 json 可以保存为（例如）sampleActivityLogAlert.json，并且可以使用 [Azure 门户中的 Azure 资源管理器](../azure-resource-manager/resource-group-template-deploy-portal.md)进行部署。

> [!NOTE]
> 新的活动日志警报规则可能需要最多 5 分钟才变为活动状态。

## <a name="manage-alert-rules-for-activity-log-using-powershell-cli-or-api"></a>使用 PowerShell、CLI 或 API 管理活动日志的警报规则
[Azure Monitor - 活动日志警报 API](https://docs.microsoft.com/rest/api/monitor/activitylogalerts) 是一个 REST API 并且与 Azure 资源管理器 REST API 完全兼容。 因此，可以使用资源管理器 cmdlet 和 Azure CLI 通过 Powershell 使用它。

下面展示了之前在[资源模板部分](#manage-alert-rules-for-activity-log-using-azure-resource-template)中显示的示例资源模板 (sampleActivityLogAlert.json) 通过 Azure 资源管理器 PowerShell cmdlet 进行使用的情况：
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myRG" -TemplateFile sampleActivityLogAlert.json -TemplateParameterFile sampleActivityLogAlert.parameters.json
```
其中，sampleActivityLogAlert.parameters.json 包含为创建警报规则时所需的参数提供的值。

下面展示了之前在[资源模板部分](#manage-alert-rules-for-activity-log-using-azure-resource-template)中显示的示例资源模板 (sampleActivityLogAlert.json) 通过 Azure CLI 中的 Azure 资源管理器命令进行使用的情况：

```azurecli
az group deployment create --resource-group myRG --template-file sampleActivityLogAlert.json --parameters @sampleActivityLogAlert.parameters.json
```
其中，sampleActivityLogAlert.parameters.json 包含为创建警报规则时所需的参数提供的值。


## <a name="next-steps"></a>后续步骤

- [活动日志的 Webhook 架构](monitoring-activity-log-alerts-webhook.md)
- [活动日志概述](monitoring-activity-log-alerts.md) 
- 详细了解[操作组](monitoring-action-groups.md)。  
- 了解[服务运行状况通知](monitoring-service-notifications.md)。