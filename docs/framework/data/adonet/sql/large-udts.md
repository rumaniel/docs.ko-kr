---
title: 큰 UDT
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 420ae24e-762b-4e09-b4c3-2112c470ee49
ms.openlocfilehash: 33f4263c747ac2590234493ec7cb9e6048ed2b96
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794017"
---
# <a name="large-udts"></a>큰 UDT
개발자는 UDT(사용자 정의 형식)를 통해 SQL Server 데이터베이스에 CLR(공용 언어 런타임) 개체를 저장하여 서버의 스칼라 형식 시스템을 확장할 수 있습니다. UDT에는 단일 SQL Server 시스템 데이터 형식으로 구성된 일반적인 별칭 데이터 형식과는 달리 여러 요소 및 동작이 포함될 수 있습니다.  
  
> [!NOTE]
> 큰 UDT에 대한 지원이 향상된 SqlClient를 활용하려면 .NET Framework 3.5 SP1 이상을 설치해야 합니다.  
  
 이전에는 UDT의 최대 크기가 8KB로 제한되었습니다. 그러나 SQL Server 2008에서는 <xref:Microsoft.SqlServer.Server.Format.UserDefined> 형식인 UDT에 대해 이 제한이 제거되었습니다.  
  
 사용자 정의 형식에 대한 자세한 내용은 현재 사용하고 있는 SQL Server 버전에 해당하는 SQL Server 온라인 설명서 버전을 참조하세요.  
  
 **SQL Server 온라인 설명서**  
  
1. [CLR 사용자 정의 형식](https://go.microsoft.com/fwlink/?LinkId=98366)  
  
## <a name="retrieving-udt-schemas-using-getschema"></a>GetSchema를 사용하여 UDT 스키마 검색  
 <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A>의 <xref:System.Data.SqlClient.SqlConnection> 메서드는 데이터베이스 스키마 정보를 <xref:System.Data.DataTable>에 반환합니다. 자세한 내용은 [SQL Server 스키마 컬렉션](../sql-server-schema-collections.md)을 참조 하세요.  
  
### <a name="getschematable-column-values-for-udts"></a>UDT의 GetSchemaTable 열 값  
 <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>의 <xref:System.Data.SqlClient.SqlDataReader> 메서드는 열 메타데이터를 설명하는 <xref:System.Data.DataTable>을 반환합니다. 다음 표에서는 SQL Server 2005와 SQL Server 2008 간의 큰 UDT 열 메타데이터 차이점에 대해 설명합니다.  
  
|SqlDataReader 열|SQL Server 2005|SQL Server 2008 이상|  
|--------------------------|---------------------|-------------------------------|  
|`ColumnSize`|경우에 따라 다름|경우에 따라 다름|  
|`NumericPrecision`|255|255|  
|`NumericScale`|255|255|  
|`DataType`|`Byte[]`|UDT 인스턴스|  
|`ProviderSpecificDataType`|`SqlTypes.SqlBinary`|UDT 인스턴스|  
|`ProviderType`|21 (`SqlDbType.VarBinary`)|29 (`SqlDbType.Udt`)|  
|`NonVersionedProviderType`|29 (`SqlDbType.Udt`)|29 (`SqlDbType.Udt`)|  
|`DataTypeName`|`SqlDbType.VarBinary`|세 부분으로 구성 된 이름이 *데이터베이스. SchemaName. TypeName*.|  
|`IsLong`|경우에 따라 다름|경우에 따라 다름|  
  
## <a name="sqldatareader-considerations"></a>SqlDataReader 고려 사항  
 SQL Server 2008부터 <xref:System.Data.SqlClient.SqlDataReader>는 큰 UDT 값 검색을 지원하도록 확장되었습니다. <xref:System.Data.SqlClient.SqlDataReader>에서는 현재 사용하고 있는 SQL Server 버전뿐만 아니라 연결 문자열에 지정된 `Type System Version`에 따라 큰 UDT를 다르게 처리합니다. 자세한 내용은 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>을 참조하세요.  
  
 <xref:System.Data.SqlClient.SqlDataReader>의 다음 메서드는 <xref:System.Data.SqlTypes.SqlBinary>이 SQL Server 2005로 설정되어 있는 경우 UDT 대신 `Type System Version`를 반환합니다.  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetSqlValue%2A>  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetSqlValues%2A>  
  
 다음 메서드는 `Byte[]`이 SQL Server 2005로 설정되어 있는 경우 UDT 대신 `Type System Version`의 배열을 반환합니다.  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetValue%2A>  
  
- <xref:System.Data.SqlClient.SqlDataReader.GetValues%2A>  
  
 현재 버전의 ADO.NET에 대해서는 변환이 수행되지 않습니다.  
  
## <a name="specifying-sqlparameters"></a>SqlParameter 지정  
 다음 <xref:System.Data.SqlClient.SqlParameter> 속성은 큰 UDT로 작업할 수 있도록 확장되었습니다.  
  
|SqlParameter|설명|  
|---------------------------|-----------------|  
|<xref:System.Data.SqlClient.SqlParameter.Value%2A>|매개 변수의 값을 나타내는 개체를 가져오거나 설정합니다. 기본값은 null입니다. 이 속성은 `SqlBinary`, `Byte[]` 또는 관리 개체일 수 있습니다.|  
|<xref:System.Data.SqlClient.SqlParameter.SqlValue%2A>|매개 변수의 값을 나타내는 개체를 가져오거나 설정합니다. 기본값은 null입니다. 이 속성은 `SqlBinary`, `Byte[]` 또는 관리 개체일 수 있습니다.|  
|<xref:System.Data.SqlClient.SqlParameter.Size%2A>|확인할 매개 변수 값의 크기를 가져오거나 설정합니다. 기본값은 0입니다. 이 속성은 매개 변수 값의 크기를 나타내는 정수일 수 있습니다. 큰 UDT의 경우 UDT의 실제 크기이거나 -1(알 수 없는 경우)일 수 있습니다.|  
  
## <a name="retrieving-data-example"></a>데이터 검색 예제  
 다음 코드 조각에서는 큰 UDT 데이터를 검색하는 방법을 보여 줍니다. `connectionString` 변수는 SQL Server 데이터베이스에 대한 올바른 연결이 있다고 가정하고 `commandString` 변수는 기본 키 열이 가장 먼저 나열된 올바른 SELECT 문이 있다고 가정합니다.  
  
```csharp  
using (SqlConnection connection = new SqlConnection(   
    connectionString, commandString))  
{  
  connection.Open();  
  SqlCommand command = new SqlCommand(commandString);  
  SqlDataReader reader = command.ExecuteReader();  
  while (reader.Read())  
  {  
    // Retrieve the value of the Primary Key column.  
    int id = reader.GetInt32(0);  
  
    // Retrieve the value of the UDT.  
    LargeUDT udt = (LargeUDT)reader[1];  
  
    // You can also use GetSqlValue and GetValue.  
    // LargeUDT udt = (LargeUDT)reader.GetSqlValue(1);  
    // LargeUDT udt = (LargeUDT)reader.GetValue(1);  
  
    Console.WriteLine(  
     "ID={0} LargeUDT={1}", id, udt);  
  }  
reader.close  
}  
```  
  
```vb  
Using connection As New SqlConnection( _  
    connectionString, commandString)  
    connection.Open()  
    Dim command As New SqlCommand(commandString, connection)  
    Dim reader As SqlDataReader  
    reader = command.ExecuteReader  
  
    While reader.Read()  
      ' Retrieve the value of the Primary Key column.  
      Dim id As Int32 = reader.GetInt32(0)  
  
      ' Retrieve the value of the UDT.  
      Dim udt As LargeUDT = CType(reader(1), LargeUDT)  
  
     ' You can also use GetSqlValue and GetValue.  
     ' Dim udt As LargeUDT = CType(reader.GetSqlValue(1), LargeUDT)  
     ' Dim udt As LargeUDT = CType(reader.GetValue(1), LargeUDT)  
  
      ' Print values.  
      Console.WriteLine("ID={0} LargeUDT={1}", id, udt)  
    End While  
    reader.Close()  
End Using  
```  
  
## <a name="see-also"></a>참고자료

- [매개 변수 및 매개 변수 데이터 형식 구성](../configuring-parameters-and-parameter-data-types.md)
- [데이터베이스 스키마 정보 검색](../retrieving-database-schema-information.md)
- [SQL Server 데이터 형식 매핑](../sql-server-data-type-mappings.md)
- [SQL Server 이진 및 큰 값 데이터](sql-server-binary-and-large-value-data.md)
- [ADO.NET 개요](../ado-net-overview.md)
