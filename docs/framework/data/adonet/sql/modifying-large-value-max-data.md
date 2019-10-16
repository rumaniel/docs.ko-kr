---
title: ADO.NET에서 큰 값(최대값) 데이터 수정
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8aca5f00-d80e-4320-81b3-016d0466f7ee
ms.openlocfilehash: 0f029c81dd6ba5cd5202e6e59f33edd7cf8c0b90
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894445"
---
# <a name="modifying-large-value-max-data-in-adonet"></a>ADO.NET에서 큰 값(최대값) 데이터 수정
LOB(Large Object) 데이터 형식은 최대 행 크기 8KB를 초과하는 형식입니다. SQL Server에서는 `max`, `varchar` 및 `nvarchar` 데이터 형식에 사용할 수 있는 `varbinary` 지정자를 제공하여 2^32바이트에 이르는 큰 값도 스토리지할 수 있습니다. 테이블 열 및 Transact-SQL 변수에서는 `varchar(max)`, `nvarchar(max)` 또는 `varbinary(max)` 데이터 형식을 지정할 수 있습니다. ADO.NET에서는 `max`를 사용하여 `DataReader` 데이터 형식을 가져올 수 있을 뿐 아니라 특별한 처리 없이도 입력 및 출력 매개 변수 값을 모두 지정할 수 있습니다. 큰 `varchar` 데이터 형식의 경우에는 데이터를 점진적으로 검색하고 업데이트할 수 있습니다.  
  
 `max` 데이터 형식은 비교 및 연결 작업에 사용할 수 있으며, 비교를 수행할 경우에는 Transact-SQL 변수로 사용합니다. 또한 SELECT 문의 DISTINCT, ORDER BY, GROUP BY 절에는 물론 집계, 조인 및 하위 쿼리에도 사용할 수 있습니다.  
  
 다음 표에는 SQL Server 온라인 설명서의 문서에 대한 링크가 나와 있습니다.  
  
 **SQL Server 온라인 설명서**  
  
1. [대량 값 데이터 형식 사용](https://go.microsoft.com/fwlink/?LinkId=120498)  
  
## <a name="large-value-type-restrictions"></a>큰 값 형식 제한 사항  
 다음 제한 사항은 `max` 데이터 형식에 적용되며, 보다 작은 데이터 형식에 대해서는 존재하지 않습니다.  
  
- `sql_variant`에는 큰 `varchar` 데이터 형식이 포함될 수 없습니다.  
  
- 큰 `varchar` 열은 인덱스에 키 열로 지정할 수 없으며 클러스터링되지 않은 인덱스에 포함된 열에는 사용할 수 있습니다.  
  
- 큰 `varchar` 열은 키 열을 분할하는 데 사용할 수 없습니다.  
  
## <a name="working-with-large-value-types-in-transact-sql"></a>Transact-SQL에서 큰 값 형식 사용  
 Transact-SQL `OPENROWSET` 함수는 원격 데이터 연결 및 액세스를 한 번에 실행합니다. 이 함수에는 OLE DB 데이터 소스에서 원격 데이터에 액세스하는 데 필요한 모든 연결 정보가 들어 있습니다. `OPENROWSET`은 쿼리의 FROM 절에서 테이블 이름인 것처럼 참조할 수 있습니다. 또한 OLE DB 공급자의 기능에 따라 INSERT, UPDATE 또는 DELETE 문의 대상 테이블로 참조할 수도 있습니다.  
  
 `OPENROWSET` 함수에서는 `BULK` 행 집합 공급자를 추가하여 대상 테이블로 데이터를 로드하지 않고 파일에서 직접 데이터를 읽어올 수 있습니다. 따라서 간단한 INSERT SELECT 문에서 `OPENROWSET`을 사용할 수 있습니다.  
  
 옵션 `OPENROWSET BULK` 인수를 사용 하면 데이터 읽기의 시작 및 종료 지점, 오류 처리 방법 및 데이터 해석 방법을 효과적으로 제어할 수 있습니다. 예를 들어, 데이터 파일을 `varbinary`, `varchar` 또는 `nvarchar` 형식의 단일 행 및 단일 열 행 집합으로 읽도록 지정할 수 있습니다. 전체 구문과 옵션을 보려면 SQL Server 온라인 설명서를 참조하세요.  
  
 다음 예제에서는 AdventureWorks 샘플 데이터베이스의 ProductPhoto 테이블에 사진을 삽입합니다. 공급자를 사용 `BULK OPENROWSET` 하는 경우 모든 열에 값을 삽입 하지 않더라도 명명 된 열 목록을 제공 해야 합니다. 이 경우 기본 키는 ID 열로 정의되며 열 목록에서 생략할 수 있습니다. 또한 `OPENROWSET` 문의 끝에 상관 관계 이름을 제공해야 하며, 이 경우 ThumbnailPhoto입니다. 이렇게 하면 파일이 로드되는 `ProductPhoto` 테이블의 열과 연결됩니다.  
  
```sql  
INSERT Production.ProductPhoto (  
    ThumbnailPhoto,   
    ThumbnailPhotoFilePath,   
    LargePhoto,   
    LargePhotoFilePath)  
SELECT ThumbnailPhoto.*, null, null, N'tricycle_pink.gif'  
FROM OPENROWSET   
    (BULK 'c:\images\tricycle.jpg', SINGLE_BLOB) ThumbnailPhoto  
```  
  
## <a name="updating-data-using-update-write"></a>UPDATE .WRITE를 사용하여 데이터 업데이트  
 Transact-SQL UPDATE 문에는 `varchar(max)`, `nvarchar(max)` 또는 `varbinary(max)` 열의 내용을 수정하기 위한 새로운 WRITE 구문이 들어 있습니다. 이 구문을 사용하면 데이터를 부분적으로 업데이트할 수 있습니다. 다음은 약식으로 나타낸 UPDATE .WRITE 구문입니다.  
  
 UPDATE  
  
 { *\<object>* }  
  
 SET  
  
 { *column_name* = {. WRITE ( *expression* , @Offset , @Length )}  
  
 WRITE 메서드는 *column_name* 값의 섹션이 수정 되도록 지정 합니다. 식은 *column_name*에 복사 되는 값이 고, `@Offset` 은 식이 `@Length` 작성 되는 시작점 이며, 인수는 열에 있는 섹션의 길이입니다.  
  
|조건|작업|  
|--------|----------|  
|식이 NULL로 설정된 경우|`@Length`이 무시 되 고 *column_name* 의 값이 지정 `@Offset`된에서 잘립니다.|  
|`@Offset`NULL|업데이트 작업은 기존 *column_name* 값의 끝에 식을 추가 하 고 `@Length` 무시 됩니다.|  
|`@Offset`이 column_name 값의 길이보다 큰 경우|SQL Server에서 오류를 반환합니다.|  
|`@Length`NULL|업데이트 작업을 통해 `@Offset`부터 `column_name` 값 끝 사이에 있는 모든 데이터가 제거됩니다.|  
  
> [!NOTE]
> `@Offset`과 `@Length`는 모두 음수일 수 없습니다.  
  
## <a name="example"></a>예제  
 이 Transact-SQL 예제에서는 AdventureWorks 데이터베이스에 있는 Document 테이블의 `nvarchar(max)` 열인 DocumentSummary에서 값의 일부를 업데이트합니다. 'components'라는 단어는 대체 단어, 기존 데이터에서 대체할 단어의 시작 위치(오프셋) 및 대체할 문자 수(길이)를 지정하여 'features'라는 단어로 대체됩니다. 이 예제에는 결과를 비교하기 위해 UPDATE 문 앞뒤에 SELECT 문이 포함되어 있습니다.  
  
```sql
USE AdventureWorks;  
GO  
--View the existing value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety components of your bicycle.  
  
--Modify a single word in the DocumentSummary column  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
WHERE DocumentID = 3 ;  
GO   
--View the modified value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety features of your bicycle.  
```  
  
## <a name="working-with-large-value-types-in-adonet"></a>ADO.NET에서 큰 값 형식 사용  
 결과 집합을 반환 하는 <xref:System.Data.SqlClient.SqlParameter> 데를 <xref:System.Data.SqlClient.SqlDataReader> <xref:System.Data.SqlClient.SqlDataAdapter> `DataSet`사용하거나를 사용 하 여 결과 집합을 반환 하거나를 사용 /하 여 ADO.NET에서 대량 값 형식을 사용할 수 있습니다. `DataTable` 큰 값 형식과 관련된 작은 값의 데이터 형식을 작업하는 방식에는 차이가 없습니다.  
  
### <a name="using-getsqlbytes-to-retrieve-data"></a>GetSqlBytes를 사용하여 데이터 검색  
 `GetSqlBytes`의 <xref:System.Data.SqlClient.SqlDataReader> 메서드를 사용하면 `varbinary(max)` 열의 내용을 검색할 수 있습니다. 다음 코드 조각에서는 <xref:System.Data.SqlClient.SqlCommand>라는 `cmd` 개체는 테이블에서 `varbinary(max)` 데이터를 선택하고 <xref:System.Data.SqlClient.SqlDataReader>라는 `reader` 개체는 데이터를 <xref:System.Data.SqlTypes.SqlBytes>로 검색하는 것으로 가정합니다.  
  
```vb  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection)  
While reader.Read()  
    Dim bytes As SqlBytes = reader.GetSqlBytes(0)  
End While  
```  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBytes bytes = reader.GetSqlBytes(0);  
    }  
```  
  
### <a name="using-getsqlchars-to-retrieve-data"></a>GetSqlChars를 사용하여 데이터 검색  
 `GetSqlChars`의 <xref:System.Data.SqlClient.SqlDataReader> 메서드를 사용하면 `varchar(max)` 또는 `nvarchar(max)` 열의 내용을 검색할 수 있습니다. 다음 코드 조각에서는 <xref:System.Data.SqlClient.SqlCommand>라는 `cmd` 개체는 테이블에서 `nvarchar(max)` 데이터를 선택하고 <xref:System.Data.SqlClient.SqlDataReader>라는 `reader` 개체는 데이터를 검색하는 것으로 가정합니다.  
  
```vb  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection)  
While reader.Read()  
    Dim buffer As SqlChars = reader.GetSqlChars(0)  
End While  
```  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
{  
    SqlChars buffer = reader.GetSqlChars(0);  
}  
```  
  
### <a name="using-getsqlbinary-to-retrieve-data"></a>GetSqlBinary를 사용하여 데이터 검색  
 `GetSqlBinary`의 <xref:System.Data.SqlClient.SqlDataReader> 메서드를 사용하면 `varbinary(max)` 열의 내용을 검색할 수 있습니다. 다음 코드 조각에서는 <xref:System.Data.SqlClient.SqlCommand>라는 `cmd` 개체는 테이블에서 `varbinary(max)` 데이터를 선택하고 <xref:System.Data.SqlClient.SqlDataReader>라는 `reader` 개체는 데이터를 <xref:System.Data.SqlTypes.SqlBinary> 스트림으로 검색하는 것으로 가정합니다.  
  
```vb  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection)  
While reader.Read()  
    Dim binaryStream As SqlBinary = reader.GetSqlBinary(0)  
End While  
```  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBinary binaryStream = reader.GetSqlBinary(0);  
    }  
```  
  
### <a name="using-getbytes-to-retrieve-data"></a>GetBytes를 사용하여 데이터 검색  
 `GetBytes`의 <xref:System.Data.SqlClient.SqlDataReader> 메서드에서는 지정된 열 오프셋의 바이트 스트림을 지정된 배열 오프셋에서 시작하는 바이트 배열로 읽어들입니다. 다음 코드 조각에서는 <xref:System.Data.SqlClient.SqlDataReader>라는 `reader` 개체가 바이트 배열에서 바이트를 검색하는 것으로 가정합니다. `GetSqlBytes`와 달리 `GetBytes`에는 배열 버퍼의 크기가 필요합니다.  
  
```vb  
While reader.Read()  
    Dim buffer(4000) As Byte  
    Dim byteCount As Integer = _  
    CInt(reader.GetBytes(1, 0, buffer, 0, 4000))  
End While  
```  
  
```csharp  
while (reader.Read())  
{  
    byte[] buffer = new byte[4000];  
    long byteCount = reader.GetBytes(1, 0, buffer, 0, 4000);  
}  
```  
  
### <a name="using-getvalue-to-retrieve-data"></a>GetValue를 사용하여 데이터 검색  
 `GetValue`의 <xref:System.Data.SqlClient.SqlDataReader> 메서드에서는 지정된 열 오프셋의 값을 배열로 읽어들입니다. 다음 코드 조각에서는 <xref:System.Data.SqlClient.SqlDataReader>라는 `reader` 개체가 첫 번째 열 오프셋에서 이진 데이터를 검색한 다음 두 번째 열 오프셋에서 문자열 데이터를 검색하는 것으로 가정합니다.  
  
```vb  
While reader.Read()  
    ' Read the data from varbinary(max) column  
    Dim binaryData() As Byte = CByte(reader.GetValue(0))  
  
    ' Read the data from varchar(max) or nvarchar(max) column  
    Dim stringData() As String = Cstr((reader.GetValue(1))  
End While  
```  
  
```csharp  
while (reader.Read())  
{  
    // Read the data from varbinary(max) column  
    byte[] binaryData = (byte[])reader.GetValue(0);  
  
    // Read the data from varchar(max) or nvarchar(max) column  
    String stringData = (String)reader.GetValue(1);  
}  
```  
  
## <a name="converting-from-large-value-types-to-clr-types"></a>큰 값 형식을 CLR 형식으로 변환  
 `varchar(max)` 같은 문자열 변환 메서드를 사용하면 `nvarchar(max)` 또는 `ToString` 열의 내용을 변환할 수 있습니다. 다음 코드 조각에서는 <xref:System.Data.SqlClient.SqlDataReader>라는 `reader` 개체가 데이터를 검색하는 것으로 가정합니다.  
  
```vb  
While reader.Read()  
    Dim str as String = reader(0).ToString()  
    Console.WriteLine(str)  
End While  
```  
  
```csharp  
while (reader.Read())  
{  
     string str = reader[0].ToString();  
     Console.WriteLine(str);  
}  
```  
  
### <a name="example"></a>예제  
 다음 코드에서는 `LargePhoto` 데이터베이스의 `ProductPhoto` 테이블에서 이름과 `AdventureWorks` 개체를 검색한 다음 이를 파일에 저장합니다. 어셈블리는 <xref:System.Drawing> 네임스페이스에 대한 참조로 컴파일해야 합니다.  <xref:System.Data.SqlClient.SqlDataReader.GetSqlBytes%2A>의 <xref:System.Data.SqlClient.SqlDataReader> 메서드는 <xref:System.Data.SqlTypes.SqlBytes> 속성을 노출하는 `Stream` 개체를 반환합니다. 이 코드에서는이를 사용 하 여 `Bitmap` 새 개체를 만든 다음 Gif `ImageFormat`에 저장 합니다.  
  
 [!code-csharp[DataWorks LargeValueType.Photo#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks LargeValueType.Photo/CS/source.cs#1)]
 [!code-vb[DataWorks LargeValueType.Photo#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks LargeValueType.Photo/VB/source.vb#1)]  
  
## <a name="using-large-value-type-parameters"></a>큰 값 형식 매개 변수 사용  
 <xref:System.Data.SqlClient.SqlParameter> 개체에 큰 값 형식을 사용하는 방식과 <xref:System.Data.SqlClient.SqlParameter> 개체에 작은 값 형식을 사용하는 방식은 같습니다. 다음 예제와 같이 많은 값 형식을 <xref:System.Data.SqlClient.SqlParameter> 값으로 검색할 수 있습니다. 이 코드에서는 AdventureWorks 샘플 데이터베이스에 다음 GetDocumentSummary 저장 프로시저가 있는 것으로 가정합니다. 저장 프로시저는 이라는 @DocumentID 입력 매개 변수를 사용 하 고 @DocumentSummary output 매개 변수에서 documentsummary 열의 내용을 반환 합니다.  
  
```sql
CREATE PROCEDURE GetDocumentSummary   
(  
    @DocumentID int,  
    @DocumentSummary nvarchar(MAX) OUTPUT  
)  
AS  
SET NOCOUNT ON  
SELECT  @DocumentSummary=Convert(nvarchar(MAX), DocumentSummary)  
FROM    Production.Document  
WHERE   DocumentID=@DocumentID  
```  
  
### <a name="example"></a>예제  
 ADO.NET 코드에서는 <xref:System.Data.SqlClient.SqlConnection> 및 <xref:System.Data.SqlClient.SqlCommand> 개체를 만들어 GetDocumentSummary 저장 프로시저를 실행하고 큰 값 형식으로 저장되는 문서 요약을 검색할 수 있습니다. 이 코드는 @DocumentID 입력 매개 변수의 값을 전달 하 고 콘솔 창에서 @DocumentSummary 출력 매개 변수로 다시 전달 된 결과를 표시 합니다.  
  
 [!code-csharp[DataWorks LargeValueType.Param#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks LargeValueType.Param/CS/source.cs#1)]
 [!code-vb[DataWorks LargeValueType.Param#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks LargeValueType.Param/VB/source.vb#1)]  
  
## <a name="see-also"></a>참고자료

- [SQL Server 이진 및 큰 값 데이터](sql-server-binary-and-large-value-data.md)
- [SQL Server 데이터 형식 매핑](../sql-server-data-type-mappings.md)
- [ADO.NET에서 SQL Server 데이터 작업](sql-server-data-operations.md)
- [ADO.NET 개요](../ado-net-overview.md)
