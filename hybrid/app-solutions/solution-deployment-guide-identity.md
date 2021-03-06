---
title: 为 Azure 和 Azure Stack Hub 应用配置混合云标识
description: 了解如何为 Azure 和 Azure Stack Hub 应用配置混合云标识。
author: BryanLa
ms.topic: article
ms.date: 11/05/2019
ms.author: bryanla
ms.reviewer: anajod
ms.lastreviewed: 11/05/2019
ms.openlocfilehash: cfe2001fcbf91f3ec0d94a7ee257b23ba89065ee
ms.sourcegitcommit: 962334135b63ac99c715e7bc8fb9282648ba63c9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2021
ms.locfileid: "104895340"
---
# <a name="configure-hybrid-cloud-identity-for-azure-and-azure-stack-hub-apps"></a>为 Azure 和 Azure Stack Hub 应用配置混合云标识

了解如何为 Azure 和 Azure Stack Hub 应用配置混合云标识。

在全局 Azure 和 Azure Stack Hub 中，有两个选项可用于授予对应用的访问权限。

 * 当 Azure Stack Hub 与 Internet 建立了不间断的连接时，可以使用 Azure Active Directory (Azure AD)。
 * 当 Azure Stack Hub 从 Internet 断开了连接时，可以使用 Azure Directory 联合身份验证服务 (AD FS)。

使用服务主体向 Azure Stack Hub 应用授予访问权限，以便在 Azure Stack Hub 中使用 Azure 资源管理器进行部署或配置。

在此解决方案中，你将构建一个示例环境来完成以下任务：

> [!div class="checklist"]
> - 在全局 Azure 和 Azure Stack Hub 中建立混合标识
> - 检索用于访问 Azure Stack Hub API 的令牌。

必须拥有 Azure Stack Hub 操作员权限才能完成此解决方案中的步骤。

> [!Tip]  
> ![混合支柱图](./media/solution-deployment-guide-cross-cloud-scaling/hybrid-pillars.png)  
> Microsoft Azure Stack Hub 是 Azure 的扩展。 Azure Stack Hub 将云计算的灵活性和创新性带入本地环境，并支持唯一的混合云，允许你在任何地方构建和部署混合应用。  
> 
> [混合应用设计注意事项](overview-app-design-considerations.md)一文回顾了设计、部署和运行混合应用所需的软件质量要素（位置、可伸缩性、可用性、复原能力、可管理性和安全性）。 这些设计注意事项有助于优化混合应用设计，从而最大限度地减少生产环境中的难题。

## <a name="create-a-service-principal-for-azure-ad-in-the-portal"></a>在门户中创建适用于 Azure AD 的服务主体

如果已使用 Azure AD 部署 Azure Stack Hub 作为标识存储，则可以创建服务主体，就像对 Azure 所做的那样。 [使用应用标识访问资源](/azure-stack/operator/azure-stack-create-service-principals#manage-an-azure-ad-app-identity)介绍了如何通过门户执行这些步骤。 在开始之前，请确保你具有[所需的 Azure AD 权限](/azure/azure-resource-manager/resource-group-create-service-principal-portal#required-permissions)。

## <a name="create-a-service-principal-for-ad-fs-using-powershell"></a>使用 PowerShell 创建适用于 AD FS 的服务主体

如果已使用 AD FS 部署 Azure Stack Hub，则可以使用 PowerShell 创建服务主体、为角色分配访问权限以及使用该标识从 PowerShell 登录。 [使用应用标识访问资源](/azure-stack/operator/azure-stack-create-service-principals#manage-an-ad-fs-app-identity)介绍了如何使用 PowerShell 执行所需步骤。

## <a name="using-the-azure-stack-hub-api"></a>使用 Azure Stack Hub API

[Azure Stack Hub API](/azure-stack/user/azure-stack-rest-api-use) 解决方案将引导你完成检索令牌以访问 Azure Stack Hub API 的过程。

## <a name="connect-to-azure-stack-hub-using-powershell"></a>使用 PowerShell 连接到 Azure Stack Hub

[在 Azure Stack Hub 中使用 PowerShell 启动并运行](/azure-stack/operator/azure-stack-powershell-install)快速入门演练了安装 Azure PowerShell 并连接到 Azure Stack Hub 安装所要执行的步骤。

### <a name="prerequisites"></a>必备条件

你需要已连接到 Azure AD 的 Azure Stack Hub 安装，以及可访问的订阅。 如果没有 Azure Stack Hub 安装，则可以按照以下说明设置 [Azure Stack 开发工具包 (ASDK)](/azure-stack/asdk/asdk-install)。

#### <a name="connect-to-azure-stack-hub-using-code"></a>使用代码连接到 Azure Stack Hub

若要使用代码连接到 Azure Stack Hub，请使用 Azure 资源管理器终结点 API 获取 Azure Stack Hub 安装的身份验证和图终结点。 然后使用 REST 请求进行身份验证。 可以在 [GitHub](https://github.com/shriramnat/HybridARMApplication) 上找到示例客户端应用程序。

>[!Note]
>除非所选语言的 Azure SDK 支持 Azure API 配置文件，否则该 SDK 可能无法与 Azure Stack Hub 配合使用。 若要了解有关 Azure API 配置文件的详细信息，请参阅[管理 API 版本配置文件](/azure-stack/user/azure-stack-version-profiles)一文。

## <a name="next-steps"></a>后续步骤

- 若要了解有关如何在 Azure Stack Hub 中处理标识的详细信息，请参阅 [Azure Stack Hub 的标识体系结构](/azure-stack/operator/azure-stack-identity-architecture)。
- 若要详细了解 Azure 云模式，请参阅[云设计模式](/azure/architecture/patterns)。
