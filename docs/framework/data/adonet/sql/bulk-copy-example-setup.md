---
title: 대량 복사 예제 설정
ms.date: 03/30/2017
ms.assetid: d4dde6ac-b8b6-4593-965a-635c8fb2dadb
ms.openlocfilehash: ac09ed85315aee7c6b29952916088ebe6e301eb9
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794425"
---
# <a name="bulk-copy-example-setup"></a>대량 복사 예제 설정
<xref:System.Data.SqlClient.SqlBulkCopy> 클래스를 사용하면 SQL Server 테이블에만 데이터를 쓸 수 있습니다. 이 항목에 표시 된 코드 샘플은 SQL Server 예제 데이터베이스 **AdventureWorks**를 사용 합니다. 코드 샘플에서는 기존 테이블을 변경하지 않도록 사용자가 먼저 만드는 테이블에 데이터를 씁니다.  
  
 **BulkCopyDemoMatchingColumns** 및 **BulkCopyDemoDifferentColumns** 테이블은 둘 다 **AdventureWorks** **Production. Products** 테이블을 기반으로 합니다. 이러한 테이블을 사용 하는 코드 샘플에서는 데이터를 **Production** 테이블에서 이러한 샘플 테이블 중 하나로 추가 합니다. **BulkCopyDemoDifferentColumns** 테이블은 샘플에서 원본 데이터의 열을 대상 테이블에 매핑하는 방법을 보여 주는 경우 사용 됩니다. **BulkCopyDemoMatchingColumns** 는 대부분의 다른 샘플에 사용 됩니다.  
  
 일부 코드 샘플에서는 <xref:System.Data.SqlClient.SqlBulkCopy> 클래스 하나로 여러 테이블에 쓰는 방법을 보여 줍니다. 이러한 샘플의 경우 **대량 Copydemoorderheader** 및 **대량 Copydemoorderdetail** 테이블이 대상 테이블로 사용 됩니다. 이러한 테이블은 **AdventureWorks**의 **SalesOrderHeader** 및 **SalesOrderDetail** 테이블을 기반으로 합니다.  
  
> [!NOTE]
> **SqlBulkCopy** only를 사용 하는 구문을 보여 주기 위해 **SqlBulkCopy** 코드 샘플이 제공 됩니다. 소스 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있으면 Transact-SQL `INSERT … SELECT` 문을 사용하여 데이터를 더 쉽고 빠르게 복사할 수 있습니다.  
  
## <a name="table-setup"></a>테이블 설정  
 코드 샘플을 올바르게 실행하는 데 필요한 테이블을 만들려면 SQL Server 데이터베이스에서 다음 Transact-SQL 문을 실행해야 합니다.  
  
```  
USE AdventureWorks  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoMatchingColumns]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoMatchingColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoMatchingColumns]([ProductID] [int] IDENTITY(1,1) NOT NULL,  
    [Name] [nvarchar](50) NOT NULL,  
    [ProductNumber] [nvarchar](25) NOT NULL,  
 CONSTRAINT [PK_ProductID] PRIMARY KEY CLUSTERED  
(  
    [ProductID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoDifferentColumns]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoDifferentColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoDifferentColumns]([ProdID] [int] IDENTITY(1,1) NOT NULL,  
    [ProdNum] [nvarchar](25) NOT NULL,  
    [ProdName] [nvarchar](50) NOT NULL,  
 CONSTRAINT [PK_ProdID] PRIMARY KEY CLUSTERED  
(  
    [ProdID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderHeader]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderHeader]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderHeader]([SalesOrderID] [int] IDENTITY(1,1) NOT NULL,  
    [OrderDate] [datetime] NOT NULL,  
    [AccountNumber] [nvarchar](15) NULL,  
 CONSTRAINT [PK_SalesOrderID] PRIMARY KEY CLUSTERED  
(  
    [SalesOrderID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderDetail]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderDetail]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderDetail]([SalesOrderID] [int] NOT NULL,  
    [SalesOrderDetailID] [int] NOT NULL,  
    [OrderQty] [smallint] NOT NULL,  
    [ProductID] [int] NOT NULL,  
    [UnitPrice] [money] NOT NULL,  
 CONSTRAINT [PK_LineNumber] PRIMARY KEY CLUSTERED  
(  
    [SalesOrderID] ASC,  
    [SalesOrderDetailID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
```  
  
## <a name="see-also"></a>참고자료

- [SQL Server에서 대량 복사 작업](bulk-copy-operations-in-sql-server.md)
- [ADO.NET 개요](../ado-net-overview.md)
