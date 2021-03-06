---
title: 教程：Azure Active Directory 与 TINFOIL SECURITY 集成 | Microsoft Docs
description: 了解如何在 Azure Active Directory 和 TINFOIL SECURITY 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 03/27/2019
ms.author: jeedes
ms.openlocfilehash: a4e64bf6899d3384e0dadc9c2b4ce2fd5d092385
ms.sourcegitcommit: 04716e13cc2ab69da57d61819da6cd5508f8c422
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58849421"
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a>教程：Azure Active Directory 与 TINFOIL SECURITY 集成

本教程介绍如何将 TINFOIL SECURITY 与 Azure Active Directory (Azure AD) 集成。
将 TINFOIL SECURITY 与 Azure AD 集成可提供以下优势：

* 可以在 Azure AD 中控制谁有权访问 TINFOIL SECURITY。
* 可让用户使用其 Azure AD 帐户自动登录到 TINFOIL SECURITY（单一登录）。
* 可在中心位置（即 Azure 门户）管理帐户。

如果要了解有关 SaaS 应用与 Azure AD 集成的更多详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)。
如果还没有 Azure 订阅，可以在开始前[创建一个免费帐户](https://azure.microsoft.com/free/)。

## <a name="prerequisites"></a>先决条件

若要配置 Azure AD 与 TINFOIL SECURITY 的集成，需要以下项：

* 一个 Azure AD 订阅。 如果你没有 Azure AD 环境，可以在[此处](https://azure.microsoft.com/pricing/free-trial/)获取一个月的试用版。
* 已启用 TINFOIL SECURITY 单一登录的订阅

## <a name="scenario-description"></a>方案描述

本教程会在测试环境中配置和测试 Azure AD 单一登录。

* TINFOIL SECURITY 支持 **IDP** 发起的 SSO

## <a name="adding-tinfoil-security-from-the-gallery"></a>从库中添加 TINFOIL SECURITY

若要配置 TINFOIL SECURITY 与 Azure AD 的集成，需从库中将 TINFOIL SECURITY 添加到托管 SaaS 应用列表。

**若要从库中添加 TINFOIL SECURITY，请执行以下步骤：**

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。

    ![“Azure Active Directory”按钮](common/select-azuread.png)

2. 转到“企业应用”，并选择“所有应用”选项。

    ![“企业应用程序”边栏选项卡](common/enterprise-applications.png)

3. 若要添加新应用程序，请单击对话框顶部的“新建应用程序”按钮。

    ![“新增应用程序”按钮](common/add-new-app.png)

4. 在搜索框中键入 **TINFOIL SECURITY**，在结果面板中选择“TINFOIL SECURITY”，然后单击“添加”按钮添加该应用程序。

     ![结果列表中的“TINFOIL SECURITY”](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录

在本部分，我们基于名为 **Britta Simon** 的测试用户来配置并测试 TINFOIL SECURITY 的 Azure AD 单一登录。
若要正常使用单一登录，需要在 Azure AD 用户与 TINFOIL SECURITY 相关用户之间建立链接关系。

若要配置并测试 TINFOIL SECURITY 的 Azure AD 单一登录，需要完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configure-azure-ad-single-sign-on)** - 使用户能够使用此功能。
2. **[配置 TINFOIL SECURITY 单一登录](#configure-tinfoil-security-single-sign-on)** - 在应用程序端配置单一登录设置。
3. **[创建 Azure AD 测试用户](#create-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
4. **[分配 Azure AD 测试用户](#assign-the-azure-ad-test-user)** - 使 Britta Simon 能够使用 Azure AD 单一登录。
5. **[创建 TINFOIL SECURITY 测试用户](#create-tinfoil-security-test-user)** - 在 TINFOIL SECURITY 中创建 Britta Simon 的对应用户，并将其关联到其在 Azure AD 中的表示形式。
6. **[测试单一登录](#test-single-sign-on)** - 验证配置是否正常工作。

### <a name="configure-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

在本部分中，将在 Azure 门户中启用 Azure AD 单一登录。

若要配置 TINFOIL SECURITY 的 Azure AD 单一登录，请执行以下步骤：

1. 在 [Azure 门户](https://portal.azure.com/)中的“TINFOIL SECURITY”应用程序集成页上，选择“单一登录”。

    ![配置单一登录链接](common/select-sso.png)

2. 在**选择单一登录方法**对话框中，选择 **SAML/WS-Fed**模式以启用单一登录。

    ![单一登录选择模式](common/select-saml-option.png)

3. 在“使用 SAML 设置单一登录”页上，单击“编辑”图标以打开“基本 SAML 配置”对话框。

    ![编辑基本 SAML 配置](common/edit-urls.png)

4. 在“基本 SAML 配置”部分中，用户不必执行任何步骤，因为该应用已经与 Azure 预先集成。

    ![TINFOIL SECURITY 域和 URL 单一登录信息](common/preintegrated.png)

5. TINFOIL SECURITY 应用程序需要特定格式的 SAML 断言，因此，需要在 SAML 令牌属性配置中添加自定义属性映射。 以下屏幕截图显示了默认属性的列表。 单击“编辑”图标打开“用户属性”对话框 ****  **** 。

        ![图像](common/edit-attribute.png)

6. 除上述属性以外，TINFOIL SECURITY 应用程序还要求在 SAML 响应中传回其他几个属性。 在“用户属性”对话框的“用户声明”部分执行以下步骤，以便添加 SAML 令牌属性，如下表所示：

    | 名称 | 源属性 |
    | ------------------- | -------------|
    | 帐户 ID | UXXXXXXXXXXXXX |

    a. 单击“添加新声明”以打开“管理用户声明”对话框。

    ![图像](common/new-save-attribute.png)

    ![图像](common/new-attribute-details.png)

    b. 在“名称”文本框中，键入为该行显示的属性名称。

    c. 将“命名空间”留空。

    d. 选择“源”作为“属性”。

    e. 在“源属性”文本框中，粘贴稍后将在本教程中获取的帐户 ID 值。

    f. 单击“确定”

    g. 单击“ **保存**”。

7. 在“SAML 签名证书”部分中，单击“编辑”按钮以打开“SAML 签名证书”对话框。

    ![编辑 SAML 签名证书](common/edit-certificate.png)

8. 在“SAML 签名证书”部分中，复制**指纹**并将其保存在计算机上。

    ![复制指纹值](common/copy-thumbprint.png)

9. 在“设置 TINFOIL SECURITY”部分，根据要求复制相应的 URL。

    ![复制配置 URL](common/copy-configuration-urls.png)

    a. 登录 URL

    b. Azure AD 标识符

    c. 注销 URL

### <a name="configure-tinfoil-security-single-sign-on"></a>配置 TINFOIL SECURITY 单一登录

1. 在另一 Web 浏览器窗口中，以管理员身份登录到 TINFOIL SECURITY 公司站点。

2. 在顶部菜单栏中，单击“我的帐户”。
   
    ![仪表板](./media/tinfoil-security-tutorial/ic798971.png "Dashboard")

3. 单击“安全”。
   
    ![安全](./media/tinfoil-security-tutorial/ic798972.png "安全")

4. 在“单一登录”配置页上，执行以下步骤：
   
    ![单一登录](./media/tinfoil-security-tutorial/ic798973.png "单一登录")
   
    a. 选择“启用 SAML”。
   
    b. 单击“手动配置”。
   
    c. 在“SAML 发布 URL”文本框中，粘贴从 Azure 门户复制的“登录 URL”值。
   
    d. 在“SAML 证书指纹”文本框中，粘贴从“SAML 签名证书”部分复制的“指纹”值。
  
    e. 复制“你的帐户 ID”值，将此值粘贴在 Azure 门户中“添加属性”部分下的“属性值”文本框中。
   
    f. 单击“ **保存**”。

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

在本部分中，通过授予 Britta Simon 访问 TINFOIL SECURITY 的权限，使她能够使用 Azure 单一登录。

1. 在 Azure 门户中，依次选择“企业应用程序”、“所有应用程序”、“TINFOIL SECURITY”。

    ![“企业应用程序”边栏选项卡](common/enterprise-applications.png)

2. 在应用程序列表中，选择“TINFOIL SECURITY”。

    ![“应用程序”列表中的“TINFOIL SECURITY”链接](common/all-applications.png)

3. 在左侧菜单中，选择“用户和组”。

    ![“用户和组”链接](common/users-groups-blade.png)

4. 单击“添加用户”按钮，然后在“添加分配”对话框中选择“用户和组”。

    ![“添加分配”窗格](common/add-assign-user.png)

5. 在“用户和组”对话框中，选择“用户”列表中的 Britta Simon，然后单击屏幕底部的“选择”按钮。

6. 如果你在 SAML 断言中需要任何角色值，请在“选择角色”对话框中从列表中为用户选择合适的角色，然后单击屏幕底部的“选择”按钮。

7. 在“添加分配”对话框中，单击“分配”按钮。

### <a name="create-tinfoil-security-test-user"></a>创建 TINFOIL SECURITY 测试用户

要使 Azure AD 用户能够登录到 TINFOIL SECURITY，必须将其预配到 TINFOIL SECURITY 中。 对于 TINFOIL SECURITY，需手动完成预配。

**若要预配用户，请执行以下步骤：**

1. 如果用户是企业帐户的一部分，你则需要联系 [TINFOIL SECURITY 支持团队](https://www.tinfoilsecurity.com/contact)以创建用户帐户。

1. 如果用户是常规 TINFOIL SECURITY SaaS 用户，则该用户可向任何用户站点添加协作者。 这会触发向指定的电子邮件发送邀请以创建新 TINFOIL SECURITY 用户帐户的过程。

> [!NOTE]
> 可使用任何其他 TINFOIL SECURITY 用户帐户创建工具或使用 TINFOIL SECURITY 提供的 API 来预配 Azure AD 用户帐户。
> 

### <a name="test-single-sign-on"></a>测试单一登录 

在本部分中，使用访问面板测试 Azure AD 单一登录配置。

在访问面板中单击“TINFOIL SECURITY”磁贴时，应会自动登录到设置了 SSO 的 TINFOIL SECURITY。 有关访问面板的详细信息，请参阅 [Introduction to the Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)（访问面板简介）。

## <a name="additional-resources"></a>其他资源

- [有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [什么是使用 Azure Active Directory 的应用程序访问和单一登录？](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [什么是 Azure Active Directory 中的条件访问？](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

