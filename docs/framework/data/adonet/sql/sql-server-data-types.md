---
title: SQL Server 데이터 형식 및 ADO.NET
ms.date: 03/30/2017
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.openlocfilehash: 642fe0d541aca01d6ffb2d9279c4d0fa91eadb63
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780843"
---
# <a name="sql-server-data-types-and-adonet"></a>SQL Server 데이터 형식 및 ADO.NET
SQL Server와 .NET Framework는 서로 다른 형식 시스템을 기반으로 하기 때문에 데이터가 손실될 가능성이 있습니다. .NET Framework Data Provider for SQL Server(<xref:System.Data.SqlClient>)에서는 데이터 무결성을 유지하기 위해 SQL Server 데이터로 작업할 때 형식화된 접근자 메서드를 제공합니다. <xref:System.Data.SqlDbType> 클래스의 열거형을 사용하여 <xref:System.Data.SqlClient.SqlParameter> 데이터 형식을 지정할 수 있습니다.  
  
 SQL Server와 .NET Framework 데이터 형식 간의 데이터 형식 매핑을 설명 하는 테이블 및 자세한 내용은 [SQL Server 데이터 형식 매핑](../sql-server-data-type-mappings.md)을 참조 하세요.  
  
 SQL Server 2008에서는 날짜와 시간, 구조화된 데이터, 반구조적 데이터 및 구조화되지 않은 데이터로 작업해야 하는 비즈니스 요구 사항을 충족하도록 디자인된 새로운 데이터 형식을 지원합니다. 이러한 데이터 형식에 대한 내용은 SQL Server 2008 온라인 설명서에 나와 있습니다.  
  
 애플리케이션에서 사용할 수 있는 SQL Server 데이터 형식은 현재 사용하고 있는 SQL Server 버전에 따라 다릅니다. 자세한 내용은 다음 표에서 해당되는 SQL Server 온라인 설명서 버전을 참조하세요.  
  
 **SQL Server 온라인 설명서**  
  
1. [데이터 형식 (데이터베이스 엔진)](https://go.microsoft.com/fwlink/?LinkID=107468)  
  
## <a name="in-this-section"></a>섹션 내용  
 [SqlTypes 및 DataSet](sqltypes-and-the-dataset.md)  
 `SqlTypes`의 `DataSet`에 대한 형식 지원에 대해 설명합니다.  
  
 [Null 값 처리](handling-null-values.md)  
 null 값 및 3중값 논리로 작업하는 방법을 보여 줍니다.  
  
 [GUID 및 uniqueidentifier 값 비교](comparing-guid-and-uniqueidentifier-values.md)  
 SQL Server 및 .NET Framework에서 GUID 및 uniqueidentifier 값으로 작업하는 방법을 보여 줍니다.  
  
 [날짜 및 시간 데이터](date-and-time-data.md)  
 SQL Server 2008에서 지원하는 새로운 날짜 및 시간 데이터 형식의 사용 방법에 대해 설명합니다.  
  
 [큰 UDT](large-udts.md)  
 SQL Server 2008에서 지원하는 큰 값 UDT에서 데이터를 검색하는 방법을 보여 줍니다.  
  
 [SQL Server의 XML 데이터](xml-data-in-sql-server.md)  
 SQL Server에서 검색한 XML 데이터로 작업하는 방법을 설명합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.Data.DataSet>  
 `DataSet` 클래스와 해당 멤버 전체에 대해 설명합니다.  
  
 <xref:System.Data.SqlTypes>  
 `SqlTypes` 네임스페이스와 해당 멤버 전체에 대해 설명합니다.  
  
 <xref:System.Data.SqlDbType>  
 `SqlDbType` 열거형과 해당 멤버 전체에 대해 설명합니다.  
  
 <xref:System.Data.DbType>  
 `DbType` 열거형과 해당 멤버 전체에 대해 설명합니다.  
  
## <a name="see-also"></a>참고자료

- [SQL Server 데이터 형식 매핑](../sql-server-data-type-mappings.md)
- [매개 변수 및 매개 변수 데이터 형식 구성](../configuring-parameters-and-parameter-data-types.md)
- [테이블 반환 매개 변수](table-valued-parameters.md)
- [SQL Server 이진 및 큰 값 데이터](sql-server-binary-and-large-value-data.md)
- [ADO.NET 개요](../ado-net-overview.md)
