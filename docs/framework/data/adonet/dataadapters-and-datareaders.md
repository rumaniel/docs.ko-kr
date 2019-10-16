---
title: DataAdapters 및 DataReaders
ms.date: 03/30/2017
ms.assetid: cc952ca2-ec19-46ab-9189-15174b52cb74
ms.openlocfilehash: 20c6d514e70d2e4db451e0fff02e72688bf7d0ba
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786641"
---
# <a name="dataadapters-and-datareaders"></a>DataAdapters 및 DataReaders
ADO.NET **DataReader** 를 사용 하 여 데이터베이스에서 앞 으로만 이동 가능한 읽기 전용 데이터 스트림을 검색할 수 있습니다. 결과는 쿼리가 실행 될 때 반환 되 고 **DataReader**의 **Read** 메서드를 사용 하 여 요청할 때까지 클라이언트의 네트워크 버퍼에 저장 됩니다. **DataReader** 를 사용 하면 데이터를 사용할 수 있는 즉시 검색 하 고 (기본적으로) 한 번에 한 행만 메모리에 저장 하 여 시스템 오버 헤드를 줄임으로써 응용 프로그램 성능이 향상 될 수 있습니다.  
  
 <xref:System.Data.Common.DataAdapter>는 데이터 소스에서 데이터를 검색하고 <xref:System.Data.DataSet> 내의 테이블을 채우는 데 사용됩니다. `DataAdapter`는 `DataSet`의 변경 내용을 다시 데이터 소스에 적용합니다. `DataAdapter`는 .NET Framework 데이터 공급자의 `Connection` 개체를 사용하여 데이터 소스에 연결하며 `Command` 개체를 사용하여 데이터 소스에서 데이터를 검색하고 변경 내용을 데이터 소스에 적용합니다.  
  
 .NET Framework에 포함된 각 .NET Framework 데이터 공급자에는 <xref:System.Data.Common.DbDataReader> 및 <xref:System.Data.Common.DbDataAdapter> 개체가 있습니다. .NET Framework Data Provider for OLE DB에는 <xref:System.Data.OleDb.OleDbDataReader> 및 <xref:System.Data.OleDb.OleDbDataAdapter> 개체가 있고 .NET Framework Data Provider for SQL Server에는 <xref:System.Data.SqlClient.SqlDataReader> 및 <xref:System.Data.SqlClient.SqlDataAdapter> 개체가 있으며 .NET Framework Data Provider for ODBC에는 <xref:System.Data.Odbc.OdbcDataReader> 및 <xref:System.Data.Odbc.OdbcDataAdapter> 개체가 있고 .NET Framework Data Provider for Oracle에는 <xref:System.Data.OracleClient.OracleDataReader> 및 <xref:System.Data.OracleClient.OracleDataAdapter> 개체가 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [DataReader를 사용하여 데이터 검색](retrieving-data-using-a-datareader.md)  
 ADO.NET **DataReader** 개체와이 개체를 사용 하 여 데이터 소스에서 결과 스트림을 반환 하는 방법에 대해 설명 합니다.  
  
 [DataAdapter에서 데이터 집합 채우기](populating-a-dataset-from-a-dataadapter.md)  
 `DataSet`를 사용하여 테이블, 열 및 행으로 `DataAdapter`을 채우는 방법을 설명합니다.  
  
 [DataAdapter 매개 변수](dataadapter-parameters.md)  
 `DataAdapter`의 열 내용을 명령 매개 변수에 매핑하는 방법을 비롯하여 `DataSet`의 명령 속성에 매개 변수를 사용하는 방법을 설명합니다.  
  
 [데이터 집합에 기존 제약 조건 추가](adding-existing-constraints-to-a-dataset.md)  
 `DataSet`에 기존 제약 조건을 추가하는 방법을 설명합니다.  
  
 [DataAdapter DataTable 및 DataColumn 매핑](dataadapter-datatable-and-datacolumn-mappings.md)  
 `DataTableMappings`에 대해 `ColumnMappings` 및 `DataAdapter`를 설정하는 방법을 설명합니다.  
  
 [쿼리 결과를 통해 페이징](paging-through-a-query-result.md)  
 쿼리 결과를 데이터 페이지로 보는 예제를 제공합니다.  
  
 [DataAdapter로 데이터 원본 업데이트](updating-data-sources-with-dataadapters.md)  
 `DataAdapter`를 사용하여 `DataSet`의 변경 내용을 데이터베이스에 적용하는 방법을 설명합니다.  
  
 [DataAdapter 이벤트 처리](handling-dataadapter-events.md)  
 `DataAdapter` 이벤트와 이벤트 사용 방법을 설명합니다.  
  
 [DataAdapter를 사용하여 일괄 작업 수행](performing-batch-operations-using-dataadapters.md)  
 `DataSet`의 업데이트를 적용할 때 SQL Server로의 라운드트립 횟수를 줄여 애플리케이션의 성능을 향상시키는 방법을 설명합니다.  
  
## <a name="see-also"></a>참고자료

- [데이터 소스에 연결](connecting-to-a-data-source.md)
- [명령 및 매개 변수](commands-and-parameters.md)
- [트랜잭션 및 동시성](transactions-and-concurrency.md)
- [DataSet, DataTable 및 DataView](./dataset-datatable-dataview/index.md)
- [ADO.NET 개요](ado-net-overview.md)
