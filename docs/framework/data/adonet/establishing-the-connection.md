---
title: 연결 설정
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3af512f3-87d9-4005-9e2f-abb1060ff43f
ms.openlocfilehash: c4e782b670bfc74a651ce38457c05d9acfcf0e8c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783902"
---
# <a name="establishing-the-connection"></a>연결 설정
Microsoft SQL Server에 연결하려면 .NET Framework Data Provider for SQL Server의 <xref:System.Data.SqlClient.SqlConnection> 개체를 사용합니다. OLE DB 데이터 소스에 연결하려면 .NET Framework Data Provider for OLE DB의 <xref:System.Data.OleDb.OleDbConnection> 개체를 사용합니다. ODBC 데이터 소스에 연결하려면 .NET Framework Data Provider for ODBC의 <xref:System.Data.Odbc.OdbcConnection> 개체를 사용합니다. Oracle 데이터 소스에 연결하려면 .NET Framework Data Provider for Oracle의 <xref:System.Data.OracleClient.OracleConnection> 개체를 사용합니다. 연결 문자열을 안전 하 게 저장 하 고 검색 하려면 [연결 정보 보호](protecting-connection-information.md)를 참조 하세요.  
  
## <a name="closing-connections"></a>연결 닫기  
 사용이 끝나면 해당 연결이 풀로 반환되도록 닫아 두는 것이 좋습니다. Visual Basic 또는 C#의 `Using` 블록은 처리되지 않은 예외가 발생하더라도 코드에 블록이 있으면 연결을 자동으로 제거합니다. 자세한 내용은 [Using 문](../../../csharp/language-reference/keywords/using-statement.md) 및 [using 문](../../../visual-basic/language-reference/statements/using-statement.md) 을 참조 하세요.  
  
 사용 중인 공급자에 대해 연결 개체의 `Close` 또는 `Dispose` 메서드를 사용할 수도 있습니다. 명시적으로 닫히지 않은 연결은 풀에 추가되거나 반환되지 않을 수 있습니다. 예를 들어, 범위를 벗어났지만 명시적으로 닫히지 않은 연결은 최대 풀 크기에 도달했으며 여전히 유효한 경우에만 연결 풀로 반환됩니다. 자세한 내용은 [OLE DB, ODBC 및 Oracle 연결 풀링](ole-db-odbc-and-oracle-connection-pooling.md)을 참조 하세요.  
  
> [!NOTE]
> 호출 하지 마세요 `Close` 또는 `Dispose` 에 **연결**, **DataReader**, 또는 다른 관리 개체에는 `Finalize` 클래스의 메서드. 종료자에서는 클래스에 직접 속한 관리되지 않는 리소스만 해제합니다. 클래스에 관리되지 않는 리소스가 없는 경우 클래스 정의에 `Finalize` 메서드를 포함하지 마세요. 자세한 내용은 [가비지 수집](../../../standard/garbage-collection/index.md)합니다.  
  
> [!NOTE]
> 연결이 연결 풀에서 반환될 경우에는 실제로 해제된 것이 아니므로 연결이 연결 풀에서 반입되거나 연결 풀로 반환되는 경우 서버에서 로그인 및 로그아웃 이벤트가 발생하지 않습니다. 자세한 내용은 [SQL Server 연결 풀링(ADO.NET)](sql-server-connection-pooling.md)을 참조하세요.  
  
## <a name="connecting-to-sql-server"></a>SQL Server 연결  
 .NET Framework Data Provider for SQL Server에서는 OLE DB(ADO) 연결 문자열 형식과 유사한 연결 문자열 형식을 지원합니다. 유효한 문자열 형식 이름 및 값은 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> 개체의 <xref:System.Data.SqlClient.SqlConnection> 속성을 참조하세요. <xref:System.Data.SqlClient.SqlConnectionStringBuilder> 클래스를 사용하여 런타임에 구문상 유효한 연결 문자열을 만들 수도 있습니다. 자세한 내용은 [연결 문자열 작성기](connection-string-builders.md)를 참조하세요.  
  
 다음 코드 예제에서는 SQL Server 데이터베이스에 대해 연결을 만들어 여는 방법을 보여 줍니다.  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New SqlConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (SqlConnection connection = new SqlConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
```  
  
### <a name="integrated-security-and-aspnet"></a>통합 보안 및 ASP.NET  
 트러스트된 연결이라고도 하는 SQL Server 통합 보안은 연결 문자열에 사용자 ID와 암호를 노출하지 않아 안전하게 SQL Server에 연결할 수 있으므로 연결 인증에 권장되는 방식입니다. 통합 보안에서는 실행 중인 프로세스의 현재 보안 ID, 즉 토큰을 사용합니다. 데스크톱 응용 프로그램의 경우에는 일반적으로 현재 로그온한 사용자의 ID입니다.  
  
 ASP.NET 응용 프로그램의 보안 ID는 여러 가지 서로 다른 옵션 중 하나로 설정할 수 있습니다. SQL Server에 연결할 때 ASP.NET 응용 프로그램에서 사용 하는 보안 id를 더 잘 이해 하려면 [ASP.NET 가장](https://docs.microsoft.com/previous-versions/aspnet/xh507fc5(v=vs.100)), [ASP.NET 인증](https://docs.microsoft.com/previous-versions/aspnet/eeyk640h(v=vs.100))및 [방법을 참조 하세요. Windows 통합 보안](https://docs.microsoft.com/previous-versions/aspnet/bsz5788z(v=vs.100))을 사용 하 여 SQL Server에 액세스 합니다.  
  
## <a name="connecting-to-an-ole-db-data-source"></a>OLE DB 데이터 소스 연결  
 OLE DB에 대 한 .NET Framework Data Provider는 **OleDbConnection** 개체를 사용 하 여 OLE DB를 사용 하 여 노출 된 데이터 원본에 대 한 연결을 제공 합니다 (예를 들어 OLE DB에 대 한 SQL Server 공급자).  
  
 .NET Framework Data Provider for OLE DB의 경우 연결 문자열 형식은 ADO에서 사용되는 연결 문자열 형식과 동일하지만, 다음과 같은 예외가 있습니다.  
  
- **공급자** 키워드가 필요 합니다.  
  
- **URL**, **원격 공급자**및 **원격 서버** 키워드는 지원 되지 않습니다.  
  
 OLE DB 연결 문자열에 대한 자세한 내용은 <xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A> 항목을 참조하세요. <xref:System.Data.OleDb.OleDbConnectionStringBuilder>를 사용하여 런타임에 연결 문자열을 만들 수도 있습니다.  
  
> [!NOTE]
> **OleDbConnection** 개체는 OLE DB 공급자와 관련 된 동적 속성을 설정 하거나 검색 하는 것을 지원 하지 않습니다. OLE DB 공급자의 연결 문자열에 전달할 수 있는 속성만 지원됩니다.  
  
 다음 코드 예제에서는 OLE DB 데이터 소스에 대해 연결을 만들어 여는 방법을 보여 줍니다.  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New OleDbConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (OleDbConnection connection =   
  new OleDbConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
```  
  
## <a name="do-not-use-universal-data-link-files"></a>유니버설 데이터 링크 파일 사용 안 함  
 UDL (Universal Data Link) 파일에 **OleDbConnection** 에 대 한 연결 정보를 제공할 수 있습니다. 그러나 이렇게 하지 않는 것이 좋습니다. UDL 파일은 암호화되지 않으므로 연결 문자열 정보를 일반 텍스트로 노출시킵니다. UDL 파일은 애플리케이션에 대해 외부 파일 기반 리소스이므로 .NET Framework를 사용하여 보호할 수 없습니다.  
  
## <a name="connecting-to-an-odbc-data-source"></a>ODBC 데이터 소스 연결  
 ODBC에 대 한 .NET Framework Data Provider는 **odbcconnection.connectionstring** 개체를 사용 하 여 odbc를 통해 노출 된 데이터 원본에 대 한 연결을 제공 합니다.  
  
 .NET Framework Data Provider for ODBC의 경우 연결 문자열 형식은 ODBC 연결 문자열 형식에 최대한 일치하도록 디자인되었습니다. 또한 ODBC DSN(데이터 소스 이름)을 제공할 수 있습니다. **Odbcconnection.connectionstring** 에 대 한 자세한 내용은를 참조 <xref:System.Data.Odbc.OdbcConnection>하십시오.  
  
 다음 코드 예제에서는 ODBC 데이터 소스에 대해 연결을 만들어 여는 방법을 보여 줍니다.  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New OdbcConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (OdbcConnection connection =   
  new OdbcConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
```  
  
## <a name="connecting-to-an-oracle-data-source"></a>Oracle 데이터 소스 연결  
 Oracle의 .NET Framework Data Provider는 **OracleConnection** 개체를 사용 하 여 oracle 데이터 원본에 대 한 연결을 제공 합니다.  
  
 .NET Framework Data Provider for Oracle의 경우 연결 문자열 형식은 MSDAORA(OLE DB Provider for Oracle) 연결 문자열 형식에 최대한 일치하도록 디자인되었습니다. **OracleConnection**에 대 한 자세한 내용은를 참조 <xref:System.Data.OracleClient.OracleConnection>하십시오.  
  
 다음 코드 예제에서는 Oracle 데이터 소스에 대해 연결을 만들어 여는 방법을 보여 줍니다.  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New OracleConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (OracleConnection connection =   
  new OracleConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
OracleConnection nwindConn = new OracleConnection("Data Source=MyOracleServer;Integrated Security=yes;");  
nwindConn.Open();  
```  
  
## <a name="see-also"></a>참고자료

- [데이터 소스에 연결](connecting-to-a-data-source.md)
- [연결 문자열](connection-strings.md)
- [OLE DB, ODBC 및 Oracle 연결 풀링](ole-db-odbc-and-oracle-connection-pooling.md)
- [ADO.NET 개요](ado-net-overview.md)
