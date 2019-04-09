---
title: 教程：Azure Active Directory 与 Percolate 的集成 | Microsoft Docs
description: 了解如何在 Azure Active Directory 与 Percolate 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: 355f9659-b378-44c9-aa88-236e9b529a53
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 04/01/2019
ms.author: jeedes
ms.openlocfilehash: 166a9daed40c03ed603d9ecaf4db2d49da0bf93d
ms.sourcegitcommit: a60a55278f645f5d6cda95bcf9895441ade04629
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2019
ms.locfileid: "58887034"
---
# <a name="tutorial-azure-active-directory-integration-with-percolate"></a>教程：Azure Active Directory 与 Percolate 的集成

本教程介绍如何将 Percolate 与 Azure Active Directory (Azure AD) 集成。
将 Percolate 与 Azure AD 集成可提供以下优势：

* 可以在 Azure AD 中控制谁有权访问 Percolate。
* 可让用户使用其 Azure AD 帐户自动登录到 Percolate（单一登录）。
* 可在中心位置（即 Azure 门户）管理帐户。

如果要了解有关 SaaS 应用与 Azure AD 集成的更多详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)。
如果还没有 Azure 订阅，可以在开始前[创建一个免费帐户](https://azure.microsoft.com/free/)。

## <a name="prerequisites"></a>先决条件

若要配置 Azure AD 与 Percolate 的集成，需要准备好以下各项：

* 一个 Azure AD 订阅。 如果没有 Azure AD 环境，可以获取一个[免费帐户](https://azure.microsoft.com/free/)。
* 已启用 Percolate 单一登录的订阅

## <a name="scenario-description"></a>方案描述

本教程会在测试环境中配置和测试 Azure AD 单一登录。

* Percolate 支持 **SP** 和 **IDP** 发起的 SSO

## <a name="adding-percolate-from-the-gallery"></a>从库中添加 Percolate

若要配置 Percolate 与 Azure AD 的集成，需要从库中将 Percolate 添加到托管 SaaS 应用列表。

**若要从库中添加 Percolate，请执行以下步骤：**

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。

    ![“Azure Active Directory”按钮](common/select-azuread.png)

2. 转到“企业应用”，并选择“所有应用”选项。

    ![“企业应用程序”边栏选项卡](common/enterprise-applications.png)

3. 若要添加新应用程序，请单击对话框顶部的“新建应用程序”按钮。

    ![“新增应用程序”按钮](common/add-new-app.png)

4. 在搜索框中键入 **Percolate**，在结果面板中选择“Percolate”，然后单击“添加”按钮添加该应用程序。

     ![结果列表中的“Percolate”](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录

在本部分，我们基于名为 **Britta Simon** 的测试用户来配置并测试 Percolate 的 Azure AD 单一登录。
若要正常使用单一登录，需要在 Azure AD 用户与 Percolate 相关用户之间建立链接关系。

若要配置并测试 Percolate 的 Azure AD 单一登录，需要完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configure-azure-ad-single-sign-on)** - 使用户能够使用此功能。
2. **[配置 Percolate 单一登录](#configure-percolate-single-sign-on)** - 在应用程序端配置单一登录设置。
3. **[创建 Azure AD 测试用户](#create-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
4. **[分配 Azure AD 测试用户](#assign-the-azure-ad-test-user)** - 使 Britta Simon 能够使用 Azure AD 单一登录。
5. **[创建 Percolate 测试用户](#create-percolate-test-user)** - 在 Percolate 中创建 Britta Simon 的对应用户，并将其关联到其在 Azure AD 中的表示形式。
6. **[测试单一登录](#test-single-sign-on)** - 验证配置是否正常工作。

### <a name="configure-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

在本部分中，将在 Azure 门户中启用 Azure AD 单一登录。

若要配置 Percolate 的 Azure AD 单一登录，请执行以下步骤：

1. 在 [Azure 门户](https://portal.azure.com/)中的“Percolate”应用程序集成页上，选择“单一登录”。

    ![配置单一登录链接](common/select-sso.png)

2. 在**选择单一登录方法**对话框中，选择 **SAML/WS-Fed**模式以启用单一登录。

    ![单一登录选择模式](common/select-saml-option.png)

3. 在“使用 SAML 设置单一登录”页上，单击“编辑”图标以打开“基本 SAML 配置”对话框。

    ![编辑基本 SAML 配置](common/edit-urls.png)

4. 在“基本 SAML 配置”部分，若要在“IDP 发起的模式”下配置应用程序，用户无需执行任何步骤，因为该应用已预先集成到 Azure。 **** 

    ![Percolate 域和 URL 单一登录信息](common/preintegrated.png)

5. 如果要在 SP 发起的模式下配置应用程序，请单击“设置其他 URL”，并执行以下步骤：

    ![Percolate 域和 URL 单一登录信息](common/metadata-upload-additional-signon.png)

    在“登录 URL”文本框中，键入 URL：`https://percolate.com/app/login`

6. 在“设置 SAML 单一登录”页的“SAML 签名证书”部分中，单击“复制”按钮，以复制“应用联合元数据 URL”，并将它保存在计算机上。

    ![证书下载链接](common/copy-metadataurl.png)

7. 在“设置 Percolate”部分，根据要求复制相应的 URL。

    ![复制配置 URL](common/copy-configuration-urls.png)

    a. 登录 URL

    b. Azure AD 标识符

    c. 注销 URL

### <a name="configure-percolate-single-sign-on"></a>配置 Percolate 单一登录

1. 在另一个 Web 浏览器窗口中，以管理员身份登录到 Percolate。

2. 在主页的左侧，单击“设置”。
    
    ![配置单一登录](./media/percolate-tutorial/configure01.png)

3. 在菜单栏的左侧，单击“组织”下的“SSO”。

    ![配置单一登录](./media/percolate-tutorial/configure02.png)

    a. 在“登录 URL”文本框中，粘贴从 Azure 门户复制的“登录 URL”值。

    b. 在“实体 ID”文本框中，粘贴从 Azure 门户复制的“Azure AD 标识符”值。

    c. 在记事本中，打开从 Azure 门户下载的 base-64 编码证书，复制其内容，然后将其粘贴到“x509 证书”框中。 **** 

    d. 在“电子邮件属性”文本框中，键入 **emailaddress**。

    e. “标识提供者元数据 URL”字段是可选的；如果已从 Azure 门户复制了“应用联合元数据 URL”，请将其粘贴到“标识提供者元数据 URL”文本框中。

    f. 对于“是否应该对 AuthNRequests 签名?”，请选择“否”。

    g. 对于“启用 SSO 自动预配”，请选择“否”。

    h. 单击“ **保存**”。

### <a name="create-an-azure-ad-test-user"></a>创建 Azure AD 测试用户 

本部分的目的是在 Azure 门户中创建名为 Britta Simon 的测试用户。

1. 在 Azure 门户的左侧窗格中，依次选择“Azure Active Directory”、“用户”和“所有用户”。

    ![“用户和组”以及“所有用户”链接](common/users.png)

2. 选择屏幕顶部的“新建用户”。

    ![“新建用户”按钮](common/new-user.png)

3. 在“用户属性”中，按照以下步骤操作。

    ![“用户”对话框](common/user-properties.png)

    a. 在“名称”字段中，输入 BrittaSimon。
  
    b. 在“用户名”字段中键入 brittasimon@yourcompanydomain.extension。 例如： BrittaSimon@contoso.com

    c. 选中“显示密码”复选框，然后记下“密码”框中显示的值。

    d. 单击“创建”。

### <a name="assign-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分，我们通过授予 Britta Simon 访问 Percolate 的权限，使其能够使用 Azure 单一登录。

1. 在 Azure 门户中，依次选择“企业应用程序”、“所有应用程序”、“Percolate”。

    ![“企业应用程序”边栏选项卡](common/enterprise-applications.png)

2. 在“应用程序”列表中，选择“Percolate”。

    ![“应用程序”列表中的“Percolate”链接](common/all-applications.png)

3. 在左侧菜单中，选择“用户和组”。

    ![“用户和组”链接](common/users-groups-blade.png)

4. 单击“添加用户”按钮，然后在“添加分配”对话框中选择“用户和组”。

    ![“添加分配”窗格](common/add-assign-user.png)

5. 在“用户和组”对话框中，选择“用户”列表中的 Britta Simon，然后单击屏幕底部的“选择”按钮。

6. 如果你在 SAML 断言中需要任何角色值，请在“选择角色”对话框中从列表中为用户选择合适的角色，然后单击屏幕底部的“选择”按钮。

7. 在“添加分配”对话框中，单击“分配”按钮。

### <a name="create-percolate-test-user"></a>创建 Percolate 测试用户

若要使 Azure AD 用户能够登录到 Percolate，必须将其预配到 Percolate 中。 在 Percolate 中，预配是一项手动任务。

**若要预配用户帐户，请执行以下步骤：**

1. 以管理员身份登录到 Percolate。

2. 在菜单栏的左侧，单击“组织”下的“用户”，并导航到“新建用户”。

    ![配置单一登录](./media/percolate-tutorial/configure03.png)

3. 在“创建用户”页上执行以下步骤：

    ![配置单一登录](./media/percolate-tutorial/configure04.png)

    a. 在“电子邮件”文本框中，输入用户的电子邮件，例如 brittasimon@contoso.com。 **** 

    b. 在“全名”文本框中输入用户的姓名，例如  **Brittasimon**。 **** 

    c. 单击“创建用户”。

### <a name="test-single-sign-on"></a>测试单一登录 

在本部分中，使用访问面板测试 Azure AD 单一登录配置。

在访问面板中单击“Percolate”磁贴时，应会自动登录到设置了 SSO 的 Percolate。 有关访问面板的详细信息，请参阅 [Introduction to the Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)（访问面板简介）。

## <a name="additional-resources"></a>其他资源

- [ 有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表 ](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Azure Active Directory 的应用程序访问与单一登录是什么？ ](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Azure Active Directory 中的条件访问是什么？](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
