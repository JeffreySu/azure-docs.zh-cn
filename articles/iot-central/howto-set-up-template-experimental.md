---
title: 在 Azure IoT Central 应用程序中设置设备模板 | Microsoft Docs
description: 了解如何使用度量、设置、属性、规则和仪表板设置设备模板。
author: viv-liu
ms.author: viviali
ms.date: 01/30/2019
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: b5ec8df9ff08aace69680c188f9ab05e944ce891
ms.sourcegitcommit: 3aa0fbfdde618656d66edf7e469e543c2aa29a57
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2019
ms.locfileid: "55734566"
---
# <a name="set-up-a-device-template-new-ui-design"></a>创建设备模板（新 UI 设计）

设备模板是一个蓝图，用于定义可连接到 Azure IoT Central 应用程序的某种设备的特征和行为。

例如，生成人员可以为连接到 IoT 的风扇创建设备模板，其中包含：

- 温度遥测度量

- 风扇电机错误事件度量

- 风扇运行状态度量

- 风扇速度设置

- 位置属性

- 发送警报的规则

- 显示设备全方位视图的仪表板

在此设备模板中，操作员可以创建和连接名为 **fan-1** 和 **fan-2** 等的真实风扇设备。 所有风扇都具有度量、设置、属性、规则和仪表板，应用程序用户可对其进行监视和管理。

> [!NOTE]
> 只有构建人员和管理员可以创建、编辑和删除设备模板。 任何用户都可以在“Device Explorer”页中基于现有的设备模板创建设备。

[!INCLUDE [iot-central-experimental-note](../../includes/iot-central-experimental-note.md)]

## <a name="create-a-device-template"></a>创建设备模板

1. 转到“设备模板”页。

2. 若要创建空白模板，请先单击“+”，再输入新设备模板的名称（如“制冷器”）。 然后选择“创建”：

   ![以“Refrigerator”作为模板名称的设备详细信息页](./media/howto-set-up-template-experimental/devicedetailspage.png)

4. 此时，系统会将你转到新设备模板的“设备详细信息”页。 IoT Central 在你创建设备模板时自动创建模拟设备。 使用模拟设备，可以在连接实际设备前先测试应用程序行为。

下面各部分介绍了“设备模板”页上的每个选项卡。

## <a name="measurements"></a>度量

度量是来自设备的数据。 可将多个度量添加到设备模板，以匹配设备的功能。

- 遥测度量是设备在一段时间内收集的数字型数据点。 它们以连续数据流的形式显示。 例如温度。
- 事件度量是表示设备上发生的重要事情的时间点数据。 严重级别表示事件的重要程度。 例如风扇电机错误。
- **状态**度量表示设备或其组件在一段时间内的状态。 例如，可将“正在运行”和“已停止”定义为风扇模式的两种可能状态。

### <a name="create-a-telemetry-measurement"></a>创建遥测度量

若要添加新的遥测度量，请单击“+ 新建度量”，选择“遥测”作为度量类型，再在窗体中输入详细信息。

> [!NOTE]
> 设备模板中的字段名称必须与相应设备代码中的属性名称匹配，这样，在连接真实设备后，应用程序中才会显示遥测度量。 在后续部分继续定义设备模板的过程中配置设置、设备属性和命令时，也必须做到这一点。

例如，可以添加新的温度遥测度量：

| 显示名称        | 字段名称    |  单位    | Min   |Max|
| --------------------| ------------- |-----------|-------|---|
| 温度         | temp          |  degC     |  0    |100|

![包含温度度量详细信息的“创建遥测”窗体](./media/howto-set-up-template-experimental/measurementsform.png)

在你单击“保存”后，“温度”度量便会出现在度量列表中。 不久便能看到模拟设备中的温度数据的可视化效果。

> [!NOTE]
> 遥测度量的数据类型是一个浮点数。

### <a name="create-an-event-measurement"></a>创建事件度量

若要添加新的事件度量，请单击“+ 新建度量”，并选择“事件”作为度量类型。 在“创建事件”窗体中输入详细信息。

提供了事件“显示名称”、“字段名称”和“严重性”的详细信息。 可以从三个严重性级别中进行选择：“错误”、“警告”和“信息”。

例如，可以添加新的“风扇电机错误”事件。

| 显示名称        | 字段名称    |  默认严重性 |
| --------------------| ------------- |-----------|
| 风扇电机错误     | fanmotorerror |  错误    |

![包含风扇电机事件详细信息的“创建事件”窗体](./media/howto-set-up-template-experimental/eventmeasurementsform.png)

在你单击“保存”后，“风扇电机错误”度量便会出现在度量列表中。 不久便能看到模拟设备中的事件数据的可视化效果。

若要查看事件的更多详细信息，请单击图表中的事件图标：

![“风扇电机错误”事件详细信息](./media/howto-set-up-template-experimental/eventmeasurementsdetail.png)

> [!NOTE]
> 事件度量的数据类型为字符串。

### <a name="create-a-state-measurement"></a>创建状态度量

若要添加新的状态度量，请单击“+ 新建度量”按钮，并选择“状态”作为度量类型。 在“创建状态”窗体中输入详细信息。

提供了状态“显示名称”、“字段名称”和“值”的详细信息。 每个值还可能附带一个显示名称，在图表和表格中显示该值时，会使用该名称。

例如，可以添加新的“风扇模式”状态，其中包含设备可以发送的两个可能值：“正在运行”和“已停止”。

| 显示名称 | 字段名称    |  值 1   | 显示名称 | 值 2    |显示名称  | 
| -------------| ------------- |----------- | -------------| -----------| -------------|
| 风扇模式     | fanmode       |  1         | 正在运行    |     0      | 已停止      |

![带有风扇模式详细信息的“编辑状态”窗体](./media/howto-set-up-template-experimental/statemeasurementsform.png)

在你单击“保存”后，“风扇模式”状态度量便会出现在度量列表中。 不久便能看到模拟设备中的状态数据的可视化效果。

如果设备在短时间内发送了过多的数据点，状态度量会以不同的视觉效果显示。 单击图表可查看相应时间段内按时间顺序显示的所有数据点。 还可以缩小时间范围，以查看图表上绘制的度量值。

> [!NOTE]
> 状态度量的数据类型为字符串。

## <a name="settings"></a>设置

设置用于控制设备。 使用设置，操作员可以向设备提供输入。 可将多个设置添加到设备模板。这些设置将在“设置”选项卡上显示为可供操作员使用的磁贴。 可以添加多种类型的设置：数字、文本、日期、切换开关、选取列表和部分标签。

设置可以处于三种状态之一。 设备会报告这些状态。

- **已同步**：设备已更改为反映设置值。

- **Pending**：设备当前正在更改为设置值。

- **错误**：设备返回了错误。

例如，可以单击“设置”，并输入新的“数字”设置，从而添加新的风扇速度设置：

| 显示名称  | 字段名称    |  单位  | 小数 |初始|
| --------------| ------------- |---------| ---------|---- |
| 风扇速度     | fanSpeed      | RPM     | 2        | 0   |

![包含速度设置详细信息的“配置编号”窗体](./media/howto-set-up-template-experimental/settingsform.png)

在你选择“保存”后，“风扇速度”设置便会显示为磁贴。 操作员可以在“Device Explorer”页上使用此设置来更改设备的风扇速度。

## <a name="properties"></a>属性

属性是与设备关联的元数据，如设备位置和序列号。 将多个属性添加到设备模板，这些属性在“属性”选项卡上显示为磁贴。属性可以有数字、文本、日期、切换、设备属性、标签或位置等类型。 操作员可以在创建设备时指定属性的值，并随时可以编辑这些值。 设备属性是只读的，从设备发送到应用程序。 操作员无法更改设备属性。 当实际设备连接后，“设备属性”磁贴在应用程序中更新。

有两种类别的属性：

- 设备向 IoT Central 应用程序报告的设备属性。 设备属性是设备报告的只读值，当实际设备连接后在应用程序中更新。
- 存储在应用程序中、可由操作员编辑的应用程序属性。 设备无法识别应用程序属性。

例如，在“属性”选项卡上，可以将设备的最近一次维修日期添加为新的“日期”属性（应用程序属性）：

| 显示名称  | 字段名称 | 初始值   |
| --------------| -----------|-----------------|
| 最后维修日期      | lastServiced        | 2019 年 1 月 29 日     |

![“属性”选项卡上的“配置最近一次维修日期”窗体](./media/howto-set-up-template-experimental/propertiesform.png)

在你选择“保存”后，设备的最近一次维修日期便会显示为磁贴。

创建磁贴后，可以在“Device Explorer”中更改应用程序属性值。

### <a name="create-a-location-property-through-azure-maps"></a>通过 Azure Maps 创建位置属性

可以在 Azure IoT Central 中为位置数据提供地理上下文，并映射街道地址的任何纬度和经度坐标。 也可以映射纬度和经度坐标。 Azure Maps 在 IoT Central 中启用此功能。

你可以添加两种类型的位置属性：

- **作为应用程序属性的位置**：存储在应用程序中。 设备无法识别应用程序属性。
- **设备位置属性**，由设备向应用程序报告。

#### <a name="add-location-as-an-application-property"></a>添加应用程序位置属性

可以在 IoT Central 应用程序中使用 Azure Maps 将位置属性创建为应用程序属性。 例如，可以添加设备安装地址：

1. 转到“属性”选项卡。

2. 在库中，选择“位置”。

3. 配置位置的显示名称、字段名称和初始值（可选）。

    | 显示名称  | 字段名称 | 初始值 |
    | --------------| -----------|---------| 
    | 安装地址 | installAddress | Microsoft, 1 Microsoft Way, Redmond, WA 98052   |

   ![带有位置详细信息的“配置位置”窗体](./media/howto-set-up-template-experimental/locationcloudproperty2.png)

   有两种支持的格式可以添加位置：
   - **作为地址的位置**
   - **作为坐标的位置**

4. 单击“ **保存**”。 操作员可以在“Device Explorer”中更新位置值。

#### <a name="add-location-as-a-device-property"></a>添加设备位置属性

可以将位置属性创建为由设备报告的设备属性。 例如，如果想要跟踪设备位置，则可以：

1. 转到“属性”选项卡。

2. 从库中选择“设备属性”。

3. 配置显示名称和字段名称，再选择“位置”作为数据类型：

    | 显示名称  | 字段名称 | 数据类型 |
    | --------------| -----------|-----------|
    | 设备位置 | deviceLocation | 位置  |

   > [!NOTE]
   > 字段名称必须与相应设备代码中的属性名称匹配

   ![带有位置详细信息的“配置设备属性”窗体](./media/howto-set-up-template-experimental/locationdeviceproperty2.png)

在实际设备连接后，添加为设备属性的位置便会使用设备发送的值进行更新。 现在，你已经配置了位置属性，将能够[添加一个地图以在设备仪表板中直观显示位置](#add-an-azure-maps-location-in-the-dashboard)。

## <a name="commands"></a>命令

命令用于远程管理设备。 使用命令，操作员可以对设备运行命令。 可将多个命令添加到设备模板。这些命令将在“命令”选项卡上显示为可供操作员使用的磁贴。 作为设备的构建人员，你可以根据需要灵活地定义命令。

命令与设置有何不同？

* **设置**：设置是要应用于设备的配置。 除非你更改，否则设备一直采用相应配置。 例如，你希望设置冰箱的温度，即使冰箱重新启动也需要保持该设置。

* **命令**：使用命令，可以从 IoT Central 对设备即时远程运行命令。 如果未连接设备，则命令超时并失败。 例如，想要重新启动设备的情况。

例如，可以选择“命令”选项卡，单击“+ 新建命令”，再输入新命令详细信息，从而添加新的“回显”命令：

| 显示名称  | 字段名称 | 默认超时 | 数据类型 |
| --------------| -----------|---------------- | --------- |
| 回显命令  | echo       |  30             | text      |

![包含 echo 详细信息的“配置命令”窗体](./media/howto-set-up-template-experimental/commandsecho.png)

在你选择“保存”后，“回显”命令便会显示为磁贴，并可供在“Device Explorer”中使用（当实际设备连接后）。 命令的字段名称必须与相应设备代码中的属性名称匹配，这样，命令才能成功运行。

## <a name="rules"></a>规则

操作员可以使用规则近乎实时地监视设备。 规则会自动调用操作，例如，在触发规则时发送电子邮件。 目前只有一种类型的规则：

- 当选定的设备遥测超过指定的阈值时，会触发遥测规则。 [详细了解遥测规则](howto-create-telemetry-rules-experimental.md?toc=/azure/iot-central-experimental/toc.json&bc=/azure/iot-central-experimental/breadcrumb/toc.json)。

## <a name="dashboard"></a>仪表板

操作员可以转到仪表板来查看有关设备的信息。 构建人员可在此页中添加磁贴，以帮助操作员了解设备的行为。 可将多个仪表板磁贴添加到设备模板。 可以添加多种类型的仪表板磁贴，如图像、折线图、条形图、关键绩效指标 (KPI)、设置和属性，以及标签。

例如，可以选择“仪表板”选项卡和库中的磁贴，从而添加“设置和属性”磁贴，以显示所选设置和属性的当前值：

![带有设置和属性详细信息的“配置设备详细信息”窗体](./media/howto-set-up-template-experimental/dashboardsettingsandpropertiesform.png)

此时，如果查看“Device Explorer”中的仪表板，操作员可以看到磁贴。

### <a name="add-an-azure-maps-location-in-the-dashboard"></a>在仪表板中添加 Azure Maps 位置

如果已配置位置属性，可使用设备仪表板中的地图来直观呈现位置。

1. 转到“仪表板”选项卡。

1. 在“设备仪表板”中，从库中选择“地图”。

1. 为地图指定标题。 下面的示例采用“安装位置”标题。 然后，选择之前在“属性”选项卡上配置的位置属性。在下面的示例中，选择的是“安装地址”。

   ![带有标题和属性详细信息的“配置地图”窗体](./media/howto-set-up-template-experimental/locationcloudproperty5map.png)

4. 选择“保存”。 地图图块现在显示所选的位置。

可以根据需要重设地图大小。 此时，如果查看“Device Explorer”中的仪表板，操作员可以看到你已配置的所有仪表板磁贴，包括位置地图也可见。

## <a name="next-steps"></a>后续步骤

了解如何在 Azure IoT Central 应用程序中使用设备模板后，你可以：

> [!div class="nextstepaction"]
> [创建新设备模板版本](howto-version-devicetemplate.md?toc=/azure/iot-central-experimental/toc.json&bc=/azure/iot-central-experimental/breadcrumb/toc.json)