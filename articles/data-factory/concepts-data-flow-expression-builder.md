---
title: Azure 数据工厂映射数据流表达式生成器
description: Azure 数据工厂映射数据流的表达式生成器
author: kromerm
ms.author: makromer
ms.reviewer: douglasl
ms.service: data-factory
ms.topic: conceptual
ms.date: 01/30/2019
ms.openlocfilehash: a65ba66b91b89cca7a41b7276a0ee4790088d5a1
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2019
ms.locfileid: "56212336"
---
# <a name="azure-data-factory-mapping-data-flow-expression-builder"></a>Azure 数据工厂映射数据流表达式生成器

[!INCLUDE [notes](../../includes/data-factory-data-flow-preview.md)]

Azure 数据工厂映射数据流中提供了表达式框，可在其中输入数据转换表达式。 请在这些框中使用数据流中的列、字段、变量、参数和函数。 若要生成表达式，请使用表达式生成器。单击转换中的表达式文本框即可启动表达式生成器。 选择转换的列时，有时还会看到“计算列”选项。 单击该选项也会启动表达式生成器。

![表达式生成器](media/data-flow/expression.png "表达式生成器")

表达式生成器工具默认使用文本编辑器选项。 自动填写功能从整个 Azure 数据工厂数据流对象模型读取数据，并支持语法检查和突出显示。

![表达式生成器自动填写](media/data-flow/expb1.png "表达式生成器自动填写")

## <a name="currently-working-on-field"></a>“当前正在处理”字段

![表达式生成器](media/data-flow/exp3.png "当前正在处理")

在表达式生成器 UI 的左上方，可以看到一个名为“当前正在处理”的字段，以及你当前正在处理的字段的名称。 在 UI 中生成的表达式只会应用到当前正在处理的字段。 若要转换另一个字段，请保存当前工作，使用此下拉列表选择另一个字段，然后为其他字段生成表达式。

## <a name="data-preview-in-debug-mode"></a>调试模式下的数据预览

![表达式生成器](media/data-flow/exp4b.png "表达式数据预览")

处理表达式时，可以选择性地在 Azure 数据工厂数据流设计图面上打开“调试”模式，以便在生成表达式的过程中，实时预览该表达式生成的数据结果。 为表达式启用实时调试。

![调试模式](media/data-flow/debugbutton.png "调试按钮")


![表达式生成器](media/data-flow/exp5.png "表达式数据预览")

## <a name="comments"></a>注释

使用单行和多行注释语法将注释添加到表达式：

![注释](media/data-flow/comments.png "注释")

## <a name="regular-expressions"></a>正则表达式

Azure 数据工厂数据流表达式语言（[此处提供了完整参考文档](http://aka.ms/dataflowexpressions)）支持包含正则表达式语法的函数。 使用正则表达式函数时，表达式生成器会尝试将反斜杠 (\) 解释为转义字符序列。 在正则表达式中使用反斜杠时，请将整个正则表达式括在居中圆点符号 ` ` 中，或使用双反斜杠。

使用居中圆点符号的示例

```
regex_replace('100 and 200', `(\d+)`, 'digits')
```

或使用双斜杠

```
regex_replace('100 and 200', '(\\d+)', 'digits')
```

## <a name="addressing-array-indexes"></a>寻址数组索引

使用返回数组的表达式函数时，请使用方括号 [] 来寻址返回数组对象中的特定索引。 数组从 1 开始。

![表达式生成器数组](media/data-flow/expb2.png "表达式数据预览")