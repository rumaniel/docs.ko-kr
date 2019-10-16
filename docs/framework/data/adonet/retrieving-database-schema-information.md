---
title: 데이터베이스 스키마 정보 검색
ms.date: 03/30/2017
ms.assetid: 79038d52-f122-4fd4-9bfb-aaa22d6a114b
ms.openlocfilehash: 26b234e35a0d0849914d87b61f4e8c8a87599448
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782732"
---
# <a name="retrieving-database-schema-information"></a>데이터베이스 스키마 정보 검색
데이터베이스에서 스키마 정보를 가져오려면 스키마 검색 프로세스를 사용합니다. 스키마 검색을 사용 하면 응용 프로그램에서 관리 되는 공급자가 지정 된 데이터베이스의 데이터베이스 스키마 ( *메타 데이터*라고도 함)에 대 한 정보를 찾아 반환 하도록 요청할 수 있습니다. 테이블, 열 및 저장 프로시저 같은 다양한 데이터베이스 스키마 요소는 스키마 컬렉션을 통해 노출됩니다. 각 스키마 컬렉션에는 사용하는 공급자와 관련된 다양한 스키마 정보가 들어 있습니다.  
  
 .NET Framework 관리 되는 각 공급자는 **Connection** 클래스에서 **getschema** 메서드를 구현 하며 **getschema** 메서드에서 반환 되는 스키마 정보는 형식 <xref:System.Data.DataTable>으로 제공 됩니다. **GetSchema** 메서드는 반환할 스키마 컬렉션을 지정 하 고 반환 되는 정보의 양을 제한 하는 선택적 매개 변수를 제공 하는 오버 로드 된 메서드입니다.  
  
 OLE DB, ODBC, Oracle 및 SqlClient에 대 한 .NET Framework 데이터 공급자는 **DataReader**의 열 메타 데이터를 설명 하는 DataTable을 반환 하는 **getschematable** 메서드를 제공 합니다.  
  
 또한 .NET Framework Data Provider for OLE DB에서는 <xref:System.Data.OleDb.OleDbConnection.GetOleDbSchemaTable%2A> 개체의 <xref:System.Data.OleDb.OleDbConnection> 메서드를 사용하여 스키마 정보를 노출합니다. 인수로 반환 <xref:System.Data.OleDb.OleDbSchemaGuid> 되는 스키마 정보를 식별 하는와 반환 된 열에 대 한 제한의 배열을 사용 하 여 **getoledbschematable은** 합니다. **Getoledbschematable은** 는 요청 <xref:System.Data.DataTable> 된 스키마 정보를 사용 하 여 채워진를 반환 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [GetSchema 및 Schema 컬렉션](getschema-and-schema-collections.md)  
 **GetSchema** 메서드와이 메서드를 사용 하 여 데이터베이스에서 스키마 정보를 검색 하 고 제한 하는 방법을 설명 합니다.  
  
 스키마 제한  
 **GetSchema**에서 사용할 수 있는 스키마 제한 사항을 설명 합니다.  
  
 [공통 스키마 컬렉션](common-schema-collections.md)  
 모든 .NET Framework 관리 공급자에서 지원하는 모든 공통 스키마 컬렉션에 대해 설명합니다.  
  
 [SQL Server 스키마 컬렉션](sql-server-schema-collections.md)  
 .NET Framework Provider for SQL Server에서 지원하는 스키마 컬렉션에 대해 설명합니다.  
  
 [Oracle 스키마 컬렉션](oracle-schema-collections.md)  
 .NET Framework Provider for Oracle에서 지원하는 스키마 컬렉션에 대해 설명합니다.  
  
 [ODBC 스키마 컬렉션](odbc-schema-collections.md)  
 ODBC 드라이버의 스키마 컬렉션에 대해 설명합니다.  
  
 [OLE DB 스키마 컬렉션](ole-db-schema-collections.md)  
 OLE DB 공급자의 스키마 컬렉션에 대해 설명합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.Data.Common.DbConnection.GetSchema%2A>  
 <xref:System.Data.Common.DbConnection> 클래스의 **GetSchema** 메서드에 대해 설명 합니다.  
  
 <xref:System.Data.Odbc.OdbcConnection.GetSchema%2A>  
 <xref:System.Data.Odbc.OdbcConnection> 클래스의 **GetSchema** 메서드에 대해 설명 합니다.  
  
 <xref:System.Data.OleDb.OleDbConnection.GetSchema%2A>  
 <xref:System.Data.OleDb.OleDbConnection> 클래스의 **GetSchema** 메서드에 대해 설명 합니다.  
  
 <xref:System.Data.OracleClient.OracleConnection.GetSchema%2A>  
 <xref:System.Data.OracleClient.OracleConnection> 클래스의 **GetSchema** 메서드에 대해 설명 합니다.  
  
 <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A>  
 <xref:System.Data.SqlClient.SqlConnection> 클래스의 **GetSchema** 메서드에 대해 설명 합니다.  
  
 <xref:System.Data.Common.DbDataReader.GetSchemaTable%2A>  
 <xref:System.Data.Common.DbDataReader> 클래스의 **getschematable 평가할** 때이 메서드에 대해 설명 합니다.  
  
 <xref:System.Data.Odbc.OdbcDataReader.GetSchemaTable%2A>  
 <xref:System.Data.Odbc.OdbcDataReader> 클래스의 **getschematable 평가할** 때이 메서드에 대해 설명 합니다.  
  
 <xref:System.Data.OleDb.OleDbDataReader.GetSchemaTable%2A>  
 <xref:System.Data.OleDb.OleDbDataReader> 클래스의 **getschematable 평가할** 때이 메서드에 대해 설명 합니다.  
  
 <xref:System.Data.OracleClient.OracleDataReader.GetSchemaTable%2A>  
 <xref:System.Data.OracleClient.OracleDataReader> 클래스의 **getschematable 평가할** 때이 메서드에 대해 설명 합니다.  
  
 <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>  
 <xref:System.Data.SqlClient.SqlDataReader> 클래스의 **getschematable 평가할** 때이 메서드에 대해 설명 합니다.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET에서 데이터 검색 및 수정](retrieving-and-modifying-data.md)
- [ADO.NET 개요](ado-net-overview.md)
