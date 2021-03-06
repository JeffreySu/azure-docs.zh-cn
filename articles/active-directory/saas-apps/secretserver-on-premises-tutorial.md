---
title: 教程：Azure Active Directory 与 Secret Server (On-Premises) 的集成 | Microsoft Docs
description: 了解如何在 Azure Active Directory 与 Secret Server (On-Premises) 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: be4ba84a-275d-4f71-afce-cb064edc713f
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2018
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9167a5ed72e6fec2ca03cc97d1d41dd6cd4aaba6
ms.sourcegitcommit: a60a55278f645f5d6cda95bcf9895441ade04629
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2019
ms.locfileid: "58885836"
---
# <a name="tutorial-azure-active-directory-integration-with-secret-server-on-premises"></a>教程：Azure Active Directory 与 Secret Server (On-Premises) 的集成

本教程介绍如何将 Secret Server (On-Premises) 与 Azure Active Directory (Azure AD) 集成。

将 Secret Server (On-Premises) 与 Azure AD 集成可获得以下优势：

- 可在 Azure AD 中控制谁有权访问 Secret Server (On-Premises)。
- 可让用户使用其 Azure AD 帐户自动登录到 Secret Server (On-Premises)（单一登录）。
- 可在中心位置（即 Azure 门户）管理帐户。

如需了解有关 SaaS 应用与 Azure AD 集成的详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](../manage-apps/what-is-single-sign-on.md)。

## <a name="prerequisites"></a>必备组件

若要配置 Azure AD 与 Secret Server (On-Premises) 的集成，需要准备好以下各项：

- Azure AD 订阅
- 已启用 Secret Server (On-Premises) 单一登录的订阅

> [!NOTE]
> 为了测试本教程中的步骤，我们不建议使用生产环境。

测试本教程中的步骤应遵循以下建议：

- 除非必要，请勿使用生产环境。
- 如果没有 Azure AD 试用环境，可以[获取一个月的试用版](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>方案描述
在本教程中，会在测试环境中测试 Azure AD 单一登录。 本教程中概述的方案包括两个主要构建基块：

1. 从库中添加 Secret Server (On-Premises)
1. 配置和测试 Azure AD 单一登录

## <a name="adding-secret-server-on-premises-from-the-gallery"></a>从库中添加 Secret Server (On-Premises)
若要配置 Secret Server (On-Premises) 与 Azure AD 的集成，需要从库中将 Secret Server (On-Premises) 添加到托管 SaaS 应用列表。

**若要从库中添加 Secret Server (On-premises)，请执行以下步骤：**

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。 

    ![“Azure Active Directory”按钮][1]

1. 导航到“企业应用程序”。 然后转到“所有应用程序”。

    ![“企业应用程序”边栏选项卡][2]
    
1. 若要添加新应用程序，请单击对话框顶部的“新建应用程序”按钮。

    ![“新增应用程序”按钮][3]

1. 在搜索框中键入 **Secret Server (On-Premises)**，在结果面板中选择“Secret Server (On-Premises)”，然后单击“添加”按钮添加该应用程序。

    ![结果列表中的“Secret Server (On-Premises)”](./media/secretserver-on-premises-tutorial/tutorial_secretserver_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录

在本部分，我们将基于名为“Britta Simon”的测试用户配置和测试 Secret Server (On-Premises) 的 Azure AD 单一登录。

若要运行单一登录，Azure AD 需要知道与 Azure AD 用户相对应的 Secret Server (On-Premises) 用户。 换句话说，需要在 Azure AD 用户与 Secret Server (On-Premises) 中相关用户之间建立链接关系。

若要配置和测试 Secret Server (On-Premises) 的 Azure AD 单一登录，需要完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configure-azure-ad-single-sign-on)** - 使用户能够使用此功能。
1. **[创建 Azure AD 测试用户](#create-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
1. **[创建 Secret Server (On-Premises) 测试用户](#create-a-secret-server-on-premises-test-user)** - 在 Secret Server (On-Premises) 中创建 Britta Simon 的对应用户，并将其关联到用户的 Azure AD 表示形式。
1. **[分配 Azure AD 测试用户](#assign-the-azure-ad-test-user)** - 使 Britta Simon 能够使用 Azure AD 单一登录。
1. **[测试单一登录](#test-single-sign-on)** - 验证配置是否正常工作。

### <a name="configure-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

在本部分，我们将在 Azure 门户中启用 Azure AD 单一登录，并在 Secret Server (On-Premises) 应用程序中配置单一登录。

**若要与 Secret Server (On-premises) 配置 Azure AD 单一登录，请执行以下步骤：**

1. 在 Azure 门户中的“Secret Server (On-Premises)”应用程序集成页上，单击“单一登录”。

    ![配置单一登录链接][4]

1. 在“单一登录”对话框中，选择“基于 SAML 的单一登录”作为“模式”以启用单一登录。

    ![“单一登录”对话框](./media/secretserver-on-premises-tutorial/tutorial_secretserver_samlbase.png)

1. 在“Secret Server (On-Premises) 域和 URL”部分，如果要在“IDP”发起的模式下配置应用程序，请执行以下步骤：

    ![Secret Server (On-Premises) 域和 URL 单一登录信息](./media/secretserver-on-premises-tutorial/tutorial_secretserver_url.png)

    a. 在中**标识符**文本框中，输入用户选择的值，例如： `https://secretserveronpremises.azure`

    b. 在“回复 URL”文本框中，使用以下模式键入 URL： `https://<SecretServerURL>/SAML/AssertionConsumerService.aspx`

    > [!NOTE]
    > 上面所示的“实体 ID”只是一个示例。可以任意选择用于在 Azure AD 中标识 Secret Server 实例的唯一值。 需要将此“实体 ID”发送到 [Secret Server (On-Premises) 客户端支持团队](https://thycotic.force.com/support/s/)，让他们在其一端进行配置。 有关详细信息，请阅读[此文](https://thycotic.force.com/support/s/article/Configuring-SAML-in-Secret-Server)。

1. 如果要在 SP 发起的模式下配置应用程序，请选中“显示高级 URL 设置”，并执行以下步骤：

    ![Secret Server (On-Premises) 域和 URL 单一登录信息](./media/secretserver-on-premises-tutorial/tutorial_secretserver_url1.png)

    在“登录 URL”文本框中，使用以下模式键入 URL： `https://<SecretServerURL>/login.aspx`
     
    > [!NOTE] 
    > 这些不是实际值。 请使用实际的“回复 URL”和“注销 URL”更新这些值。 请联系 [Secret Server (On-Premises) 客户端支持团队](https://thycotic.force.com/support/s/)获取这些值。

1. 在“SAML 签名证书”部分中，单击“证书(base64)”，并在计算机上保存证书文件。

    ![证书下载链接](./media/secretserver-on-premises-tutorial/tutorial_secretserver_certificate.png)

1. 选中“显示高级证书签名设置”并选择“对 SAML 响应和断言进行签名”作为“签名选项”。

    ![签名选项](./media/secretserver-on-premises-tutorial/signing.png)

1. 单击“保存”按钮。

    ![配置单一登录“保存”按钮](./media/secretserver-on-premises-tutorial/tutorial_general_400.png)
    
1. 在“Secret Server (On-Premises) 配置”部分，单击“配置 Secret Server (On-Premises)”打开“配置登录”窗口。 从“快速参考”部分中复制“注销 URL”、“SAML 实体 ID”和“SAML 单一登录服务 URL”。

    ![Secret Server (On-Premises) 配置](./media/secretserver-on-premises-tutorial/tutorial_secretserver_configure.png)

1. 若要在 **Secret Server (On-Premises)** 端配置单一登录，需要将下载的**证书 (Base64)、注销 URL、SAML 单一登录服务 URL** 以及 **SAML 实体 ID** 发送给 [Secret Server (On-Premises) 支持团队](https://thycotic.force.com/support/s/)。 他们会对此进行设置，使两端的 SAML SSO 连接均正确设置。

### <a name="create-an-azure-ad-test-user"></a>创建 Azure AD 测试用户

本部分的目的是在 Azure 门户中创建名为 Britta Simon 的测试用户。

   ![创建 Azure AD 测试用户][100]

**若要在 Azure AD 中创建的测试用户，请执行以下步骤：**

1. 在 Azure 门户的左窗格中，单击“Azure Active Directory”按钮。

    ![“Azure Active Directory”按钮](./media/secretserver-on-premises-tutorial/create_aaduser_01.png)

1. 若要显示用户列表，请转到“用户和组”，然后单击“所有用户”。

    ![“用户和组”以及“所有用户”链接](./media/secretserver-on-premises-tutorial/create_aaduser_02.png)

1. 若要打开“用户”对话框，在“所有用户”对话框顶部单击“添加”。

    ![“添加”按钮](./media/secretserver-on-premises-tutorial/create_aaduser_03.png)

1. 在“用户”对话框中，执行以下步骤：

    ![“用户”对话框](./media/secretserver-on-premises-tutorial/create_aaduser_04.png)

    a. 在“姓名”框中，键入“BrittaSimon”。

    b. 在“用户名”框中，键入用户 Britta Simon 的电子邮件地址。

    c. 选中“显示密码”复选框，然后记下“密码”框中显示的值。

    d. 单击“创建”。
 
### <a name="create-a-secret-server-on-premises-test-user"></a>创建 Secret Server (On-Premises) 测试用户

在本部分，我们将在 Secret Server (On-Premises) 中创建一个名为 Britta Simon 的用户。 与  [Secret Server (On-Premises) 支持团队](https://thycotic.force.com/support/s/) 协作，将用户添加到 Secret Server (On-Premises) 平台中。 使用单一登录前，必须先创建并激活用户。

### <a name="assign-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分，我们通过授予 Britta Simon 访问 Secret Server (On-Premises) 的权限，使其能够使用 Azure 单一登录。

![分配用户角色][200]

**若要将 Britta Simon 分配到 Secret Server (On-premises)，请执行以下步骤：**

1. 在 Azure 门户中打开应用程序视图，导航到目录视图，接着转到“企业应用程序”，并单击“所有应用程序”。

    ![分配用户][201]

1. 在应用程序列表中，选择“Secret Server (On-Premises)”。

    ![应用程序列表中的“Secret Server (On-Premises)”链接](./media/secretserver-on-premises-tutorial/tutorial_secretserver_app.png)

1. 在左侧菜单中，单击“用户和组”。

    ![“用户和组”链接][202]

1. 单击“添加”按钮。 然后在“添加分配”对话框中选择“用户和组”。

    ![“添加分配”窗格][203]

1. 在“用户和组”对话框的“用户”列表中，选择“Britta Simon”。

1. 在“用户和组”对话框中单击“选择”按钮。

1. 在“添加分配”对话框中单击“分配”按钮。

### <a name="test-single-sign-on"></a>测试单一登录

在本部分中，使用访问面板测试 Azure AD 单一登录配置。

单击访问面板中的“Secret Server (On-Premises)”磁贴时，应会自动登录到 Secret Server (On-Premises) 应用程序。
有关访问面板的详细信息，请参阅[访问面板简介](../user-help/active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他资源

* [有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表](tutorial-list.md)
* [Azure Active Directory 的应用程序访问与单一登录是什么？](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/secretserver-on-premises-tutorial/tutorial_general_01.png
[2]: ./media/secretserver-on-premises-tutorial/tutorial_general_02.png
[3]: ./media/secretserver-on-premises-tutorial/tutorial_general_03.png
[4]: ./media/secretserver-on-premises-tutorial/tutorial_general_04.png

[100]: ./media/secretserver-on-premises-tutorial/tutorial_general_100.png

[200]: ./media/secretserver-on-premises-tutorial/tutorial_general_200.png
[201]: ./media/secretserver-on-premises-tutorial/tutorial_general_201.png
[202]: ./media/secretserver-on-premises-tutorial/tutorial_general_202.png
[203]: ./media/secretserver-on-premises-tutorial/tutorial_general_203.png

