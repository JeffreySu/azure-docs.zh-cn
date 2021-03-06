---
title: Azure SQL 数据库机器学习服务 （预览版） 的主要区别
description: 本主题介绍 Azure SQL 数据库机器学习服务（使用 R）和 SQL Server 机器学习服务之间的主要差异。
services: sql-database
ms.service: sql-database
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.reviewer: carlrab
manager: cgronlun
ms.date: 03/01/2019
ms.openlocfilehash: 57ea52c179376e8378680f436d396ffaf9357f68
ms.sourcegitcommit: 5fbca3354f47d936e46582e76ff49b77a989f299
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2019
ms.locfileid: "57771844"
---
# <a name="key-differences-between-machine-learning-services-in-azure-sql-database-preview-and-sql-server"></a>Azure SQL 数据库 （预览版） 中的机器学习服务和 SQL Server 之间的主要差异

（使用 R) 的 Azure SQL 数据库机器学习服务 （预览版） 中的功能是类似于[SQL Server 机器学习服务](https://docs.microsoft.com/sql/advanced-analytics/what-is-sql-server-machine-learning)。 以下是一些重要差异。

> [!IMPORTANT]
> Azure SQL 数据库机器学习服务当前处于公共预览状态。
> 此预览版在提供时没有附带服务级别协议，不建议将其用于生产工作负荷。 某些功能可能不受支持或者受限。
> 有关详细信息，请参阅 [Microsoft Azure 预览版补充使用条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)。

## <a name="language-support"></a>语言支持

SQL Server 通过[扩展性框架](https://docs.microsoft.com/sql/advanced-analytics/concepts/extensibility-framework)支持 R 和 Python。 SQL 数据库不支持这两种语言。 主要差异为：

- R 是 SQL 数据库中唯一受支持的语言。 目前不支持 Python。
- R 版本为 3.4.4。
- 无需通过 `sp_configure` 配置 `external scripts enabled`。 [注册](sql-database-machine-learning-services-overview.md#signup)后，即会为 SQL 数据库启用机器学习。

## <a name="package-management"></a>包管理

SQL 数据库和 SQL Server 之间的 R 程序包管理和安装工作存在差异。 差异为：

- 通过 [sqlmlutils](https://github.com/Microsoft/sqlmlutils) 或 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 安装 R 程序包。
- 程序包无法执行出站网络调用。 这一限制是类似于[机器学习服务的默认防火墙规则](https://docs.microsoft.com//sql/advanced-analytics/security/firewall-configuration)在 SQL Server 中，但不能更改 SQL 数据库中。
- 不支持依赖于外部运行时（例如 Java）的程序包，也不支持需要访问 OS API 才能安装或使用的程序包。

## <a name="resource-governance"></a>资源调控

无法通过 [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor) 和外部资源池限制 R 资源。

公共预览期间 R 资源设置为最多 20%的 SQL 数据库资源，并取决于你选择哪个服务层。 有关详细信息，请参阅 [Azure SQL 数据库购买模型](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers)。

### <a name="insufficient-memory-error"></a>内存不足错误

如果没有适用于 R 的内存不足，将获取一条错误消息。 常见错误消息如下：

- 无法与请求 id 为 'R' 脚本的运行时进行通信: * * *。 请检查 'R' 运行时的要求
- 执行 sp_execute_external_script，错误为 HRESULT 0x80004004 'R' 脚本时出错。 ...发生外部脚本错误:"...无法分配 C 函数 R_AllocStringBuffer 中的内存 (0 Mb)"
- 外部脚本时出错：错误： 无法分配大小的向量。

内存使用情况取决于用于 R 脚本和正在执行的并行查询数。 如果收到以上错误，可以缩放数据库以较高的服务层，若要解决此问题。

## <a name="next-steps"></a>后续步骤

- 有关一般信息，请参阅 [SQL Server 机器学习服务](https://docs.microsoft.com/sql/advanced-analytics)文档
- 如需了解如何在 Azure SQL 数据库中使用机器学习服务（使用 R），请参阅[快速入门指南](sql-database-connect-query-r.md)。
- 有关详细信息，请参阅 [SQL Server R 语言教程](https://docs.microsoft.com/sql/advanced-analytics/tutorials/sql-server-r-tutorials)