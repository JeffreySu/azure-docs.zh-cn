---
title: Azure PowerShell 脚本 - 创建 Azure Cosmos DB SQL API 帐户
description: Azure PowerShell 脚本示例 - 创建 Azure Cosmos DB SQL API 帐户
ms.service: cosmos-db
author: markjbrown
ms.author: mjbrown
ms.subservice: cosmosdb-sql
ms.devlang: PowerShell
ms.topic: sample
ms.date: 05/10/2017
ms.reviewer: sngun
ms.openlocfilehash: 18b2f2d22edcd74717464bbefa530d27ebc7a3f3
ms.sourcegitcommit: f24fdd1ab23927c73595c960d8a26a74e1d12f5d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58497015"
---
# <a name="azure-cosmos-db-create-a-sql-api-account-using-powershell"></a>Azure Cosmos DB：使用 PowerShell 创建 SQL API 帐户

此示例 PowerShell 脚本创建一个 Azure Cosmos DB API 帐户。 

[!INCLUDE [updated-for-az](../../../includes/updated-for-az.md)]

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a>示例脚本

[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-and-configure-database/create-and-configure-database.ps1?highlight=9,12-15,18,21-23,26-29,32-37 "Create an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a>清理部署

运行脚本示例后，可以使用以下命令删除资源组以及与其关联的所有资源。

```powershell
Remove-AzResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>脚本说明

此脚本使用以下命令。 表中的每条命令均链接到特定于命令的文档。

| 命令 | 说明 |
|---|---|
| [New-AzResourceGroup](https://docs.microsoft.com/powershell/module/az.resources/new-azresourcegroup) | 创建用于存储所有资源的资源组。 |
| [New-AzResource](https://docs.microsoft.com/powershell/module/az.resources/new-azresource) | 创建用于托管数据库或弹性池的逻辑服务器。 |
| [Remove-AzResourceGroup](https://docs.microsoft.com/powershell/module/az.resources/remove-azresourcegroup) | 删除资源组，包括所有嵌套的资源。 |
|||

## <a name="next-steps"></a>后续步骤

有关 Azure PowerShell 的详细信息，请参阅 [Azure PowerShell 文档](https://docs.microsoft.com/powershell/)。

可以在 [Azure Cosmos DB PowerShell 脚本](../powershell-samples.md)中找到其他 Azure Cosmos DB PowerShell 脚本示例。
