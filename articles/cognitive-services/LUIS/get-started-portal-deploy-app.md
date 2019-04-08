---
title: 快速入门：使用 LUIS 门户部署应用
titleSuffix: Language Understanding - Azure Cognitive Services
description: 应用准备好将言语预测返回到客户端应用程序（例如聊天机器人）后，就需要将应用部署到预测终结点。 本快速入门将介绍如何通过创建预测终结点资源、将资源分配给应用、训练应用以及发布应用来部署应用程序。
services: cognitive-services
author: diberry
manager: nitinme
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: quickstart
ms.date: 03/11/2019
ms.author: diberry
ms.openlocfilehash: 0cf7464188bb502d77c673284cba226ce91a5725
ms.sourcegitcommit: aa3be9ed0b92a0ac5a29c83095a7b20dd0693463
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58259714"
---
# <a name="quickstart-deploy-an-app-in-the-luis-portal"></a>快速入门：在 LUIS 门户中部署应用

应用准备好将言语预测返回到客户端应用程序（例如聊天机器人）后，就需要将应用部署到预测终结点。 

本快速入门将介绍如何通过创建预测终结点资源、将资源分配给应用、训练应用以及发布应用来部署应用程序。 

## <a name="prerequisites"></a>先决条件

* [Azure 订阅](https://azure.microsoft.com/free)。
* 完成[上述门户快速入门](get-started-portal-build-app.md)或[下载并导入应用](https://github.com/Azure-Samples/cognitive-services-language-understanding/blob/master/documentation-samples/quickstarts/in-portal/build-portal-app.json)。 


## <a name="create-endpoint-resource"></a>创建终结点资源

预测终结点资源在 Azure 门户中进行创建。 此资源仅应用于终结点预测查询。 请勿使用此资源来创建对应用的更改。 

1. 登录到 **[Azure 门户](https://ms.portal.azure.com/)**。 

1. 选择左上方面板中的绿色 + 符号，然后在市场中搜索 `Cognitive Services`，然后选择它。 

1. 使用以下设置配置订阅：

    |设置|值|目的|
    |--|--|--|
    |Name|`my-cognitive-service-resource`|Azure 资源的名称。 将资源分配给 LUIS 门户中的应用时需要此名称。|
    |订阅|订阅|选择与你的帐户关联的其中某个订阅。|
    |位置|**美国西部**|此资源的 Azure 区域。|
    |定价层|**S0**|此资源的默认定价层。|
    |资源组|`my-cognitive-service-resource-group`|为所有认知服务资源创建新资源组。 完成资源后，可以删除资源组以清理订阅。 | 

    ![Azure API 选择](./media/get-started-portal-deploy-app/create-cognitive-services-resource.png) 

1. 选择“创建”以创建 Azure 资源。 

    在下一部分中，你将了解如何在 LUIS 门户中将此新资源连接到 LUIS 应用。 

## <a name="assign-the-resource-key-to-the-luis-app-in-the-luis-portal"></a>将资源关键字分配给 LUIS 门户中的 LUIS 应用

每次为 LUIS 创建新资源时，都需要将资源分配给 LUIS 应用。 分配后，除非创建新资源，否则无需再次执行此步骤。 可以创建新资源来扩展应用的区域或支持更多预测查询。 

1. 登录 [LUIS 门户](https://www.luis.ai)，从应用列表中选择“myEnglishApp”应用。

1. 在右上角的菜单中选择“管理”，然后选择“密钥和终结点”。

1. 若要添加 LUIS，请选择“分配资源 +”。

    [![将资源分配给应用](./media/get-started-portal-deploy-app/assign-resource-button.png)](./media/get-started-portal-deploy-app/assign-resource-button.png#lightbox)

1. 选择你的租户、订阅和资源名称，然后选择“分配资源”。 

    ![将资源分配给应用](./media/get-started-portal-deploy-app/assign-resource.png)

1. 在表中找到新行并复制终结点 URL。 它构造正确，用以针对用于预测的 LUIS API 终结点发出 HTTP GET 请求。 

## <a name="train-and-publish-the-app"></a>训练并发布应用 

只要准备好进行测试，就应进行训练。 每当希望当前训练的版本可从预测终结点运行时用于客户端应用程序时，就应发布应用。 

1. 如果应用未经过训练，请从右上方的菜单中选择“训练”。

1. 从右上角菜单中选择“发布”。 接受默认环境设置，然后选择“发布”。

1. 绿色的成功通知栏出现在浏览器窗口的顶部时，选择“请参阅终结点列表”链接。 

    ![在浏览器中成功发布了应用通知栏](./media/get-started-portal-deploy-app/successfully-published-notification.png)

1. 此操作会进入“密钥和终结点设置”页。 已分配资源和相应终结点 URL 的列表位于页面底部。 

1. 选择与新资源名称关联的终结点 URL。 这将打开包含正确构造的 URL Web 浏览器，以便向预测终结点运行时发出 GET 请求。 

1. URL 末尾的 `q=` 是查询的缩写，并且是用户的言语追加到 GET 请求的位置。 在 `q=` 之后，输入在上一个快速入门结束时使用的相同用户言语：

    ```Is there a form named hrf-234098```

    浏览器响应与客户端应用程序将收到的 JSON 相同：

    ```JSON
    {
    "query": "Is there a form named hrf-234098",
    "topScoringIntent": {
        "intent": "FindForm",
        "score": 0.9768753
    },
    "intents": [
        {
        "intent": "FindForm",
        "score": 0.9768753
        },
        {
        "intent": "None",
        "score": 0.0216071066
        }
    ],
    "entities": [
        {
        "entity": "hrf-234098",
        "type": "Human Resources Form Number",
        "startIndex": 22,
        "endIndex": 31
        }
      ]
    }
    ```

    此响应提供的信息比上一个教程中的默认“测试”窗格提供的信息更详细。 如果要在“测试”窗格中看到相同级别的信息，则必须发布应用。 然后，在“检查”窗格中，选择“与已发布版本进行比较”。 在发布测试窗格中使用“显示 JSON 视图”，以查看与上一步相同的 JSON。 这样可以比较当前正在使用的应用和发布到终结点的应用。

    [![比较当前正在编辑的应用和已发布版本的应用](./media/get-started-portal-deploy-app/compare-test-pane.png)](./media/get-started-portal-deploy-app/compare-test-pane.png#lightbox)


## <a name="clean-up-resources"></a>清理资源
完成此快速入门后，从顶部导航菜单中选择“我的应用”。 在列表中选中应用左侧的复选框，然后在列表上方的上下文工具栏中选择“删除”。 

[![从“我的应用”列表中删除应用](./media/get-started-portal-build-app/delete-app.png)](./media/get-started-portal-build-app/delete-app.png#lightbox)

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [确定常见意向和实体](luis-tutorial-prebuilt-intents-entities.md)