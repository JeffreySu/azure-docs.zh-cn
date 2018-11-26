---
title: 什么是并行文档？ - 自定义翻译
titleSuffix: Azure Cognitive Services
description: 并行文档是配对的文档，其中的一个文档是另一个文档的翻译。 该对中的一个文档包含采用源语言的句子，另一个文档包含这些句子的目标语言翻译。
author: rajdeep-in
manager: christw
ms.service: cognitive-services
ms.component: custom-translator
ms.date: 11/13/2018
ms.author: v-rada
ms.topic: article
ms.openlocfilehash: e9214314bab40e3ce402fed84f429f3542519240
ms.sourcegitcommit: 1f9e1c563245f2a6dcc40ff398d20510dd88fd92
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/14/2018
ms.locfileid: "51626742"
---
# <a name="what-are-parallel-documents"></a>什么是并行文档？

并行文档是配对的文档，其中的一个文档是另一个文档的翻译。 该对中的一个文档包含采用源语言的句子，另一个文档包含这些句子的目标语言翻译。
无论将哪种语言标记为“源”或“目标”，并行文档都可用于朝任一方向训练翻译系统。

## <a name="use-of-parallel-documents"></a>使用并行文档

系统使用并行文档来实现以下目的：

1.  了解单词、短语和句子在两种语言之间的一般映射方式。

2.  了解如何根据周围短语处理相应的上下文。 某个单词的翻译成不一定总与另一种语言的单词完全相同。

最佳做法是，确保在文档的源与目标语言版本之间建立 1 对 1 的句子对应关系。

上传的文档专用于每个工作区，可在任意数量的项目或训练中使用。 从文档中提取的句子作为 Unicode 纯文本文件单独存储在存储库中，并可删除。 不要使用自定义翻译作为文档存储库，否则无法以上传文档时所用的格式下载这些文档。

## <a name="recommendations"></a>建议

如果项目特定于领域（类别），则文档应该与该类别中的术语相一致。 生成的翻译系统的质量取决于文档集中的句子数以及句子的质量。 文档中包含特定于类别的单词的不同用法示例越多，翻译过程中系统的表现就越好。

至少需要有 10,000 个并行句子才能训练一个系统。 作为最佳做法，可以不断添加更多的并行内容并重新训练，以提高翻译系统的质量。

Microsoft 要求上传到自定义翻译的文档不违反第三方的版权或知识产权。 有关详细信息，请参阅[使用条款](https://azure.microsoft.com/support/legal/cognitive-services-terms/)。
使用门户上传文档不会改变文档本身的知识产权所有权。

## <a name="next-steps"></a>后续步骤

- 了解如何在自定义翻译中使用[字典](what-is-dictionary.md)。