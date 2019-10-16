---
title: 명령 및 매개 변수
ms.date: 03/30/2017
ms.assetid: b623f810-d871-49a5-b0f5-078cc3c34db6
ms.openlocfilehash: 1d0c3adb56e5ff44b5c5e065ac040f25584a1946
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784959"
---
# <a name="commands-and-parameters"></a>명령 및 매개 변수
데이터 소스에 대한 연결을 설정한 후에는 <xref:System.Data.Common.DbCommand> 개체를 사용하여 명령을 실행하고 데이터 소스에서 결과를 반환할 수 있습니다. 명령은 현재 사용하는 .NET Framework 데이터 공급자의 명령 생성자 중 하나를 사용하여 만들 수 있습니다. 생성자는 데이터 소스에서 실행하는 SQL 문, <xref:System.Data.Common.DbConnection> 개체 또는 <xref:System.Data.Common.DbTransaction> 개체와 같은 선택적 인수를 사용할 수 있습니다. 이러한 개체를 명령의 속성으로 구성할 수도 있습니다. 또한 <xref:System.Data.Common.DbConnection.CreateCommand%2A> 개체의 `DbConnection` 메서드를 사용하여 특정 연결에 대한 명령을 만들 수 있습니다. 명령을 통해 실행되는 SQL 문은 <xref:System.Data.Common.DbCommand.CommandText%2A> 속성을 사용하여 구성할 수 있습니다.  
  
 .NET Framework에 포함된 각 .NET Framework 데이터 공급자에는 `Command` 개체가 있습니다. .NET Framework Data Provider for OLE DB에는 <xref:System.Data.OleDb.OleDbCommand> 개체가 있고, .NET Framework Data Provider for SQL Server에는 <xref:System.Data.SqlClient.SqlCommand> 개체가 있으며, .NET Framework Data Provider for ODBC와 .NET Framework Data Provider for Oracle에는 각각 <xref:System.Data.Odbc.OdbcCommand> 개체와 <xref:System.Data.OracleClient.OracleCommand> 개체가 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [명령 실행](executing-a-command.md)  
 ADO.NET `Command` 개체 및 이 개체를 사용하여 데이터 소스에 대해 쿼리와 명령을 실행하는 방법을 설명합니다.  
  
 [매개 변수 및 매개 변수 데이터 형식 구성](configuring-parameters-and-parameter-data-types.md)  
 방향, 데이터 형식 및 매개 변수 구문을 포함하여 `Command` 매개 변수로 작업하는 방법을 설명합니다.  
  
 [CommandBuilder를 사용하여 명령 생성](generating-commands-with-commandbuilders.md)  
 명령 작성기를 사용하여 단일 테이블 SELECT 명령이 들어 있는 `DataAdapter`에 대해 INSERT, UPDATE 및 DELETE 명령을 자동으로 생성하는 방법을 설명합니다.  
  
 [데이터베이스에서 단일 값 가져오기](obtaining-a-single-value-from-a-database.md)  
 `ExecuteScalar` 개체의 `Command` 메서드를 사용하여 데이터베이스 쿼리에서 단일 값을 반환하는 방법을 설명합니다.  
  
 [명령을 사용하여 데이터 수정](using-commands-to-modify-data.md)  
 데이터 공급자를 사용하여 저장 프로시저 또는 DDL(데이터 정의 언어) 문을 실행하는 방법을 설명합니다.  
  
## <a name="see-also"></a>참고자료

- [DataAdapter 및 DataReader](dataadapters-and-datareaders.md)
- [DataSet, DataTable 및 DataView](./dataset-datatable-dataview/index.md)
- [데이터 소스에 연결](connecting-to-a-data-source.md)
- [ADO.NET 개요](ado-net-overview.md)
