---
title: 教程：Azure Active Directory 与 Workspot Control 集成 | Microsoft Docs
description: 了解如何在 Azure Active Directory 和 Workspot Control 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3ea8e4e9-f61f-4f45-b635-b0e306eda3d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/12/2018
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 97f375c6f48d3dc497eb59e76f19fc64cf906b56
ms.sourcegitcommit: 5839af386c5a2ad46aaaeb90a13065ef94e61e74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2019
ms.locfileid: "57886494"
---
# <a name="tutorial-azure-active-directory-integration-with-workspot-control"></a>教程：Azure Active Directory 与 Workspot Control 集成

在本教程中，了解如何将 Workspot Control 与 Azure Active Directory (Azure AD) 集成。

将 Workspot Control 与 Azure AD 集成提供以下优势：

- 可在 Azure AD 中控制谁有权访问 Workspot Control。
- 可让用户使用其 Azure AD 帐户自动登录到 Workspot Control（单一登录）。
- 可在中心位置（即 Azure 门户）管理帐户。

如需了解有关 SaaS 应用与 Azure AD 集成的详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](../manage-apps/what-is-single-sign-on.md)。

## <a name="prerequisites"></a>必备组件

若要配置 Azure AD 与 Workspot Control 的集成，需要以下项目：

- Azure AD 订阅
- 已启用 Workspot Control 单一登录的订阅

> [!NOTE]
> 为了测试本教程中的步骤，我们不建议使用生产环境。

测试本教程中的步骤应遵循以下建议：

- 除非必要，请勿使用生产环境。
- 如果没有 Azure AD 试用环境，可以[获取一个月的试用版](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>方案描述
在本教程中，将在测试环境中测试 Azure AD 单一登录。 本教程中概述的方案包括两个主要构建基块：

1. 从库中添加 Workspot Control
2. 配置和测试 Azure AD 单一登录

## <a name="adding-workspot-control-from-the-gallery"></a>从库中添加 Workspot Control
要配置 Workspot Control 与 Azure AD 的集成，需要从库中将 Workspot Control 添加到托管 SaaS 应用列表。

若要从库中添加 Workspot Control，请执行以下步骤：

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。 

    ![图像](./media/workspotcontrol-tutorial/selectazuread.png)

2. 导航到“企业应用程序”。 然后转到“所有应用程序”。

    ![图像](./media/workspotcontrol-tutorial/a_select_app.png)
    
3. 若要添加新应用程序，请单击对话框顶部的“新建应用程序”按钮。

    ![图像](./media/workspotcontrol-tutorial/a_new_app.png)

4. 在搜索框中键入“Workspot Control”，在结果面板中选择“Workspot Control”，然后单击“添加”按钮添加该应用程序。

     ![图像](./media/workspotcontrol-tutorial/tutorial_workspotcontrol_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录

在本部分中，基于名为“Britta Simon”的测试用户配置和测试 Workspot Control 的 Azure AD 单一登录。

若要运行单一登录，Azure AD 需要知道与 Azure AD 用户相对应的 Workspot Control 用户。 换句话说，需要建立 Azure AD 用户与 Workspot Control 中相关用户之间的关联关系。

若要配置和测试 Workspot Control 的 Azure AD 单一登录，需要完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configure-azure-ad-single-sign-on)** - 使用户能够使用此功能。
2. **[创建 Azure AD 测试用户](#create-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
3. **[创建 Workspot Control 测试用户](#create-a-workspot-control-test-user)** - 在 Workspot Control 中创建 Britta Simon 的对应用户，并将其链接到该用户的 Azure AD 表示形式。
4. **[分配 Azure AD 测试用户](#assign-the-azure-ad-test-user)** - 使 Britta Simon 能够使用 Azure AD 单一登录。
5. **[测试单一登录](#test-single-sign-on)** - 验证配置是否正常工作。

### <a name="configure-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

在本部分中，将在 Azure 门户中启用 Azure AD 单一登录并在 Workspot Control 应用程序中配置单一登录。

若要配置 Workspot Control 的 Azure AD 单一登录，请执行以下步骤：

1. 在 [Azure 门户](https://portal.azure.com/)中的 Workspot Control 应用程序集成页上，选择“单一登录”。

    ![图像](./media/workspotcontrol-tutorial/B1_B2_Select_SSO.png)

2. 在“选择单一登录方法”对话框中，选择 SAML 模式以启用单一登录。

    ![图像](./media/workspotcontrol-tutorial/b1_b2_saml_sso.png)

3. 在“设置 SAML 单一登录”页上，单击“编辑”按钮，以打开“基本 SAML 配置”对话框。

    ![图像](./media/workspotcontrol-tutorial/b1-domains_and_urlsedit.png)

4. 如果要在 IDP 发起的模式下配置应用程序，请在“基本 SAML 配置”部分中执行以下步骤：

    ![图像](./media/workspotcontrol-tutorial/tutorial_workspotcontrol_url.png)

    a. 在“标识符”文本框中，使用以下模式键入 URL：`https://<INSTANCENAME>-saml.workspot.com/saml/metadata`

    b. 在“回复 URL”文本框中，使用以下模式键入 URL：`https://<INSTANCENAME>-saml.workspot.com/saml/assertion`

    c. 如果要在 SP 发起的模式下配置应用程序，请单击“设置其他 URL”，并执行以下步骤：

     ![图像](./media/workspotcontrol-tutorial/tutorial_workspotcontrol_url1.png)

    在“登录 URL”文本框中，使用以下模式键入 URL：`https://<INSTANCENAME>-saml.workspot.com/`

    > [!NOTE]
    > 这些不是实际值。 请使用实际的“标识符”、“回复 URL”和“登录 URL”更新这些值。 请联系 [Workspot Control 客户端支持团队](mailto:support@workspot.com)来获取这些值。 

5. 在“使用 SAML 设置单一登录”页的“SAML 签名证书”部分中，单击“下载”以下载“证书 (Base64)”并将其保存在计算机上。

    ![图像](./media/workspotcontrol-tutorial/tutorial_workspotcontrol_certficate.png) 

6. 在“设置 Workspot Control”部分中，根据要求复制响应的 URL。

    请注意，URL 可能指明以下信息：

    a. 登录 URL

    b. Azure AD 标识符

    c. 注销 URL

    ![图像](./media/workspotcontrol-tutorial/d1_samlsonfigure.png) 

7. 在另一个 Web 浏览器窗口中，以安全管理员身份登录到 Workspot Contro。

8. 在页面顶部的工具栏中，单击“设置”，然后导航到“SAML” **** ****。

    ![图像](./media/workspotcontrol-tutorial/tutorial_workspotcontrol_setup.png)

9. 在“安全断言标记语言配置”页上，执行以下步骤：
 
    ![图像](./media/workspotcontrol-tutorial/tutorial_workspotcontrol_saml.png)

    a. 在“实体 ID”文本框中，粘贴从 Azure 门户复制的“Azure Ad 标识符”值。   

    b. 在“登录服务 URL”文本框中，粘贴从 Azure 门户复制的“登录 URL”值。

    c. 在“注销服务 URL”文本框中，粘贴从 Azure 门户复制的“注销 URL”值。 

    d. 单击“更新文件”按钮，将从 Azure 门户下载的 base-64 编码证书上传到 X.509 证书中。

    e. 单击“ **保存**”。

### <a name="create-an-azure-ad-test-user"></a>创建 Azure AD 测试用户

本部分的目的是在 Azure 门户中创建名为 Britta Simon 的测试用户。

1. 在 Azure 门户的左侧窗格中，依次选择“Azure Active Directory”、“用户”和“所有用户”。

    ![图像](./media/workspotcontrol-tutorial/d_users_and_groups.png)

2. 选择屏幕顶部的“新建用户”。

    ![图像](./media/workspotcontrol-tutorial/d_adduser.png)

3. 在“用户属性”中，按照以下步骤操作。

    ![图像](./media/workspotcontrol-tutorial/d_userproperties.png)

    a. 在“名称”字段中，输入 BrittaSimon。
  
    b. 在中**用户名**字段中，键入**brittasimon\@yourcompanydomain.extension**  
    例如： BrittaSimon@contoso.com

    c. 选择“属性”，再选择“显示密码”复选框，然后记下“密码”框中显示的值。

    d. 选择“创建”。
 
### <a name="create-a-workspot-control-test-user"></a>创建 Workspot Control 测试用户

为了使 Azure AD 用户能够登录 Workspot Control，必须将他们预配到 Workspot Control 中。 在 Workspot Control 中，预配属于手动任务。

**若要预配用户帐户，请执行以下步骤：**

1. 以安全管理员身份登录 Workspot Control。

2. 在页面顶部的工具栏中，单击“用户”，然后导航到“添加用户” **** ****。

    ![图像](./media/workspotcontrol-tutorial/tutorial_workspotcontrol_adduser.png)

3. 在“添加新用户”页面上，执行以下步骤：

    ![图像](./media/workspotcontrol-tutorial/tutorial_workspotcontrol_addnewuser.png)

    a. 在“名字”文本框中，输入用户的名字，如 Britta。

    b. 在“姓氏”文本框中，输入用户的姓氏，例如 **simon**。

    c. 在中**电子邮件**文字框中，输入类似的用户的电子邮件**Brittasimon\@contoso.com**。

    d. 从“角色”下拉列表中选择相应的用户角色。

    e. 从“组”下拉列表中选择相应的用户组。

    f. 单击“添加用户”。

### <a name="assign-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分中，通过授予 Britta Simon 访问 Workspot Control 的权限，以支持其使用 Azure 单一登录。

1. 在 Azure 门户中，选择“企业应用程序”，然后选择“所有应用程序”。

    ![图像](./media/workspotcontrol-tutorial/d_all_applications.png)

2. 在应用程序列表中，选择“Workspot Control”。

    ![图像](./media/workspotcontrol-tutorial/tutorial_workspotcontrol_app.png)

3. 在左侧菜单中，选择“用户和组”。

    ![图像](./media/workspotcontrol-tutorial/d_leftpaneusers.png)

4. 选择“添加”按钮，然后在“添加分配”对话框中选择“用户和组”。

    ![图像](./media/workspotcontrol-tutorial/d_assign_user.png)

4. 在“用户和组”对话框中，选择“用户”列表中的 Britta Simon，然后单击屏幕底部的“选择”按钮。

5. 在“添加分配”对话框中，选择“分配”按钮。
    
### <a name="test-single-sign-on"></a>测试单一登录

在本部分中，使用访问面板测试 Azure AD 单一登录配置。

在访问面板中单击“Workspot Control”磁贴，即可自动登录到 Workspot Control 应用程序。
有关访问面板的详细信息，请参阅[访问面板简介](../active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他资源

* [有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表](tutorial-list.md)
* [Azure Active Directory 的应用程序访问与单一登录是什么？](../manage-apps/what-is-single-sign-on.md)
