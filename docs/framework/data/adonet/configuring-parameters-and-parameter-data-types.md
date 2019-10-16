---
title: 매개 변수 및 매개 변수 데이터 형식 구성
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 537d8a2c-d40b-4000-83eb-bc1fcc93f707
ms.openlocfilehash: 638e8177060c489a7469f80adde68cb9ba266365
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2019
ms.locfileid: "65879964"
---
# <a name="configuring-parameters-and-parameter-data-types"></a>매개 변수 및 매개 변수 데이터 형식 구성

Command 개체는 매개 변수를 통해 SQL 문이나 저장 프로시저에 값을 전달하여 형식 검사 및 유효성 검사 기능을 제공합니다. 명령 텍스트와 달리 매개 변수 입력은 실행 코드가 아니라 리터럴 값으로 처리됩니다. 따라서 매개 변수화된 명령을 사용하면 공격자가 서버의 보안을 손상시키는 명령을 SQL 문에 삽입하는 "SQL 삽입" 공격을 막을 수 있습니다.

매개 변수화된 명령을 사용하면 데이터베이스 서버가 들어오는 명령을 올바르게 캐시된 쿼리 계획과 정확하게 일치시킬 수 있기 때문에 쿼리 실행 성능도 높일 수 있습니다. 자세한 내용은 [실행 계획 캐싱 및 재사용](/sql/relational-databases/query-processing-architecture-guide#execution-plan-caching-and-reuse) 하 고 [매개 변수 및 실행 계획 재사용](/sql/relational-databases/query-processing-architecture-guide#PlanReuse)합니다. 매개 변수화된 명령은 이러한 보안 및 성능상의 이점 외에도 데이터 소스에 전달되는 값을 구성하는 편리한 방법을 제공합니다.

<xref:System.Data.Common.DbParameter> 개체는 해당 생성자를 사용하거나 <xref:System.Data.Common.DbCommand.DbParameterCollection%2A> 컬렉션의 `Add` 메서드를 호출하여 <xref:System.Data.Common.DbParameterCollection> 에 추가하는 방법으로 만들 수 있습니다. `Add` 메서드는 데이터 공급자에 따라 생성자 인수 또는 기존 매개 변수 개체를 입력으로 사용합니다.

## <a name="supplying-the-parameterdirection-property"></a>ParameterDirection 속성 제공

매개 변수를 추가할 때 입력 매개 변수 이외의 매개 변수에 대해서는 <xref:System.Data.ParameterDirection> 속성을 제공해야 합니다. 다음 표에서는 `ParameterDirection` 열거형에 사용할 수 있는 <xref:System.Data.ParameterDirection> 값을 보여 줍니다.

|멤버 이름|설명|
|-----------------|-----------------|
|<xref:System.Data.ParameterDirection.Input>|입력 매개 변수입니다. 이 값이 기본값입니다.|
|<xref:System.Data.ParameterDirection.InputOutput>|입력과 출력 모두 수행할 수 있는 매개 변수입니다.|
|<xref:System.Data.ParameterDirection.Output>|출력 매개 변수입니다.|
|<xref:System.Data.ParameterDirection.ReturnValue>|저장 프로시저, 기본 제공 함수 또는 사용자 정의 함수 등의 작업에서 반환되는 값을 나타내는 매개 변수입니다.|

## <a name="working-with-parameter-placeholders"></a>매개 변수 자리 표시자를 사용 하 여 작업

매개 변수 자리 표시자의 구문은 데이터 소스에 따라 다릅니다. .NET Framework 데이터 공급자는 매개 변수와 매개 변수 자리 표시자를 다르게 지정하여 명명 작업을 처리합니다. 이 구문은 다음 표에서 설명하는 것과 같이 특정 데이터 소스에 맞게 사용자 지정됩니다.

|데이터 공급자|매개 변수 명명 구문|
|-------------------|-----------------------------|
|<xref:System.Data.SqlClient>|`@`*parametername*형식의 명명된 매개 변수를 사용합니다.|
|<xref:System.Data.OleDb>|물음표(`?`)로 표시된 위치 매개 변수 마커를 사용합니다.|
|<xref:System.Data.Odbc>|물음표(`?`)로 표시된 위치 매개 변수 마커를 사용합니다.|
|<xref:System.Data.OracleClient>|`:`*parmname* (또는 *parmname*) 형식의 명명된 매개 변수를 사용합니다.|

## <a name="specifying-parameter-data-types"></a>매개 변수 데이터 형식 지정

매개 변수의 데이터 형식을.NET Framework 데이터 공급자와 관련이 있습니다. 값 변환 유형을 지정 하는 `Parameter` 데이터 원본에 값을 전달 하기 전에.NET Framework 데이터 공급자 형식입니다. `Parameter` 개체의 `DbType` 속성을 특정 `Parameter` 으로 설정하면 일반적인 방식으로 <xref:System.Data.DbType>의 형식을 지정할 수도 있습니다.

.NET Framework 데이터 공급자 형식을 `Parameter` 개체의.NET Framework 형식에서 유추 됩니다는 `Value` 의 `Parameter` 개체를 또는 `DbType` 의 `Parameter` 개체입니다. 다음 표에서는 `Parameter` 값으로 전달되는 개체 또는 지정한 `Parameter` 을 기반으로 유추한 `DbType`형식을 보여 줍니다.

|.NET Framework 형식|DbType|SqlDbType|OleDbType|OdbcType|OracleType|
|-------------------------|------------|---------------|---------------|--------------|----------------|
|<xref:System.Boolean>|Boolean|비트|부울|비트|Byte|
|<xref:System.Byte>|Byte|TinyInt|UnsignedTinyInt|TinyInt|Byte|
|byte[]|이항|VarBinary입니다. 바이트 배열이 VarBinary의 최대 크기 보다 큰 8000 바이트이 암시적 변환은 수행 되지 것입니다. 바이트 배열이 8000 바이트 보다 큰를 명시적으로 설정 된 <xref:System.Data.SqlDbType>합니다.|VarBinary|이항|Raw|
|<xref:System.Char>| |char에서 <xref:System.Data.SqlDbType> 을 유추하는 것은 지원되지 않습니다.|Char|Char|Byte|
|<xref:System.DateTime>|DateTime|DateTime|DBTimeStamp|DateTime|DateTime|
|<xref:System.DateTimeOffset>|DateTimeOffset|SQL Server 2008의 DateTimeOffset. SQL Server 2008보다 이전 버전의 SQL Server에서는 DateTimeOffset에서 <xref:System.Data.SqlDbType> 을 유추하는 기능이 지원되지 않습니다.|||DateTime|
|<xref:System.Decimal>|Decimal|Decimal|Decimal|Numeric|숫자|
|<xref:System.Double>|Double|Float|Double|Double|Double|
|<xref:System.Single>|Single|Real|Single|Real|Float|
|<xref:System.Guid>|Guid|UniqueIdentifier|Guid|UniqueIdentifier|Raw|
|<xref:System.Int16>|Int16|SmallInt|SmallInt|SmallInt|Int16|
|<xref:System.Int32>|Int32|Int|Int|Int|Int32|
|<xref:System.Int64>|Int64|BigInt|BigInt|BigInt|숫자|
|<xref:System.Object>|개체|변형|변형|Object에서 OdbcType을 유추하는 것은 지원되지 않습니다.|Blob|
|<xref:System.String>|문자열|NVarChar. 문자열이 NVarChar의 최대 크기인 4000자보다 길면 이 암시적 변환은 수행되지 않습니다. 문자열이 4000자보다 긴 경우에는 <xref:System.Data.SqlDbType>을 명시적으로 설정합니다.|VarWChar|NVarChar|NVarChar|
|<xref:System.TimeSpan>|시간|SQL Server 2008의 Time입니다. SQL Server 2008보다 이전 버전의 SQL Server에서는 TimeSpan에서 <xref:System.Data.SqlDbType> 을 유추하는 기능이 지원되지 않습니다.|DBTime|시간|DateTime|
|<xref:System.UInt16>|UInt16|UInt16에서 <xref:System.Data.SqlDbType> 을 유추하는 것은 지원되지 않습니다.|UnsignedSmallInt|Int|UInt16|
|<xref:System.UInt32>|UInt32|UInt32에서 <xref:System.Data.SqlDbType> 을 유추하는 것은 지원되지 않습니다.|UnsignedInt|BigInt|UInt32|
|<xref:System.UInt64>|UInt64|UInt64에서 <xref:System.Data.SqlDbType> 을 유추하는 것은 지원되지 않습니다.|UnsignedBigInt|Numeric|숫자|
||AnsiString|VarChar|VarChar|VarChar|VarChar|
||AnsiStringFixedLength|Char|Char|Char|Char|
||통화|Money|통화|`OdbcType` 에서 `Currency` 을 유추하는 것은 지원되지 않습니다.|숫자|
||날짜|SQL Server 2008의 Date. SQL Server 2008보다 이전 버전의 SQL Server에서는 Date에서 <xref:System.Data.SqlDbType> 을 유추하는 기능이 지원되지 않습니다.|DBDate|날짜|DateTime|
||SByte|SByte에서 <xref:System.Data.SqlDbType> 을 유추하는 것은 지원되지 않습니다.|TinyInt|SByte에서 `OdbcType` 을 유추하는 것은 지원되지 않습니다.|SByte|
||StringFixedLength|NChar|WChar|NChar|NChar|
||시간|SQL Server 2008의 Time입니다. SQL Server 2008보다 이전 버전의 SQL Server에서는 Time에서 <xref:System.Data.SqlDbType> 을 유추하는 기능이 지원되지 않습니다.|DBTime|시간|DateTime|
||VarNumeric|VarNumeric에서 <xref:System.Data.SqlDbType> 을 유추하는 것은 지원되지 않습니다.|VarNumeric|VarNumeric에서 `OdbcType` 을 유추하는 것은 지원되지 않습니다.|숫자|
|사용자 정의 형식( <xref:Microsoft.SqlServer.Server.SqlUserDefinedAggregateAttribute>가 포함된 개체)|공급자에 따라 Object 또는 String(SqlClient는 항상 Object를 반환하고 Odbc는 항상 String을 반환하며 OleDb 관리 데이터 공급자는 둘 중 하나를 볼 수 있음)|<xref:Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute> 가 있으면 SqlDbType.Udt, 그렇지 않으면 Variant|값이 null이면 OleDbType.VarWChar, 그렇지 않으면 OleDbType.Variant|OdbcType.NVarChar|지원되지 않음|

> [!NOTE]
> decimal 형식에서 다른 형식으로의 변환은 decimal 값을 0에 가장 가까운 정수 값으로 반올림하는 축소 변환입니다. 변환 결과를 대상 형식으로 표현할 수 없는 경우에는 <xref:System.OverflowException> 이 throw됩니다.

> [!NOTE]
> Null 매개 변수 값을 보내면 서버를 지정 해야 합니다 <xref:System.DBNull>이 아니라 `null` (`Nothing` Visual basic에서). 시스템에서 null 값은 값이 없는 빈 개체입니다. <xref:System.DBNull> 은 null 값을 나타내는 데 사용됩니다. 데이터베이스 null에 대한 자세한 내용은 [Handling Null Values](./sql/handling-null-values.md)를 참조하세요.

## <a name="deriving-parameter-information"></a>매개 변수 정보 파생

`DbCommandBuilder` 클래스를 사용하여 저장 프로시저에서 매개 변수를 파생할 수 있습니다. `SqlCommandBuilder` 및 `OleDbCommandBuilder` 클래스는 모두 정적 메서드인 `DeriveParameters`를 제공합니다. 이 메서드는 자동으로 명령 개체의 매개 변수 컬렉션을 저장 프로시저의 매개 변수 정보로 채웁니다. `DeriveParameters` 는 명령에 대한 기존 매개 변수 정보를 모두 덮어씁니다.

> [!NOTE]
> 매개 변수 정보를 파생하는 경우 해당 정보를 검색하는 데 데이터 소스에 대한 추가 라운드트립이 필요하므로 성능이 저하됩니다. 디자인 타임에 매개 변수 정보를 알고 있으면 매개 변수를 명시적으로 설정하여 애플리케이션의 성능을 향상시킬 수 있습니다.

자세한 내용은 [commandbuilder를 사용 하를 사용 하 여 명령 생성](generating-commands-with-commandbuilders.md)합니다.

## <a name="using-parameters-with-a-sqlcommand-and-a-stored-procedure"></a>SqlCommand 및 저장된 프로시저를 사용 하 여 매개 변수를 사용 하 여

저장 프로시저는 데이터 구동 애플리케이션에 많은 이점을 제공합니다. 저장 프로시저를 사용하면 데이터베이스 작업이 단일 명령으로 캡슐화되고, 최고의 성능을 나타내도록 최적화되며, 추가 보안 기능을 통해 향상될 수 있습니다. 뒤에 매개 변수 인수를 SQL 문으로 사용 하 여 저장된 프로시저 이름을 전달 하 여 저장된 프로시저를 호출할 수 있지만 합니다 <xref:System.Data.Common.DbCommand.Parameters%2A> ADO.NET의 컬렉션 <xref:System.Data.Common.DbCommand> 개체를 사용 하면 보다 분명 하 게 저장된 프로시저를 정의할 수 있습니다 매개 변수를 output 매개 변수를 액세스 및 값을 반환 합니다.

> [!NOTE]
> 매개 변수화된 문은 `sp_executesql,` 을 사용하여 서버에서 실행되므로 쿼리 계획을 다시 사용할 수 있습니다. `sp_executesql` 일괄 처리의 로컬 커서 또는 변수는 `sp_executesql`을 호출하는 일괄 처리에 표시되지 않습니다. 데이터베이스 컨텍스트의 변경은 `sp_executesql` 문의 실행이 끝날 때까지만 지속됩니다. 자세한 내용은 [sp_executesql (TRANSACT-SQL)](/sql/relational-databases/system-stored-procedures/sp-executesql-transact-sql)합니다.

<xref:System.Data.SqlClient.SqlCommand> 에 매개 변수를 사용하여 SQL Server 저장 프로시저를 실행할 때는 <xref:System.Data.SqlClient.SqlCommand.Parameters%2A> 컬렉션에 추가된 매개 변수 이름이 저장 프로시저에 있는 매개 변수 마커 이름과 일치해야 합니다. .NET Framework Data Provider for SQL Server는 SQL 문이나 저장된 프로시저에 매개 변수를 전달 하기 위한 물음표 (?) 자리 표시자를 지원 하지 않습니다. 대신 저장 프로시저의 매개 변수를 명명된 매개 변수로 처리하여 일치하는 매개 변수 마커를 검색합니다. 예를 들어 `CustOrderHist` 저장 프로시저는 `@CustomerID`라는 매개 변수를 사용하여 정의됩니다. 따라서 코드에서 이 저장 프로시저를 실행하는 경우 `@CustomerID`라는 매개 변수도 함께 사용해야 합니다.

```sql
CREATE PROCEDURE dbo.CustOrderHist @CustomerID varchar(5)
```

### <a name="example"></a>예제

다음 예제에서는 `Northwind` 샘플 데이터베이스에 있는 SQL Server 저장 프로시저를 호출하는 방법을 보여 줍니다. 이 저장 프로시저는 이름이 `dbo.SalesByCategory` 이고, 데이터 형식이 `@CategoryName` 인 `nvarchar(15)`이라는 입력 매개 변수를 포함합니다. 이 코드는 using 블록 내에 새 <xref:System.Data.SqlClient.SqlConnection> 을 만들어 프로시저가 종료될 때 연결이 삭제되도록 합니다. <xref:System.Data.SqlClient.SqlCommand> 와 <xref:System.Data.SqlClient.SqlParameter> 개체가 만들어지고 해당 속성이 설정됩니다. <xref:System.Data.SqlClient.SqlDataReader> 가 `SqlCommand` 를 실행한 후 저장 프로시저에서 결과 집합을 반환하고 콘솔 창에 출력을 표시합니다.

> [!NOTE]
> `SqlCommand` 와 `SqlParameter` 개체를 만든 다음 별도의 문에서 속성을 설정하는 대신 오버로드된 생성자 중 하나를 사용하여 단일 문에서 여러 속성을 설정하는 방법을 사용할 수도 있습니다.

[!code-csharp[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/CS/source.cs#1)]
[!code-vb[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/VB/source.vb#1)]

## <a name="using-parameters-with-an-oledbcommand-or-odbccommand"></a>OleDbCommand 또는 OdbcCommand에 매개 변수 사용

<xref:System.Data.OleDb.OleDbCommand> 또는 <xref:System.Data.Odbc.OdbcCommand>에 매개 변수를 사용할 때는 `Parameters` 컬렉션에 추가된 매개 변수의 순서가 저장 프로시저에 정의된 매개 변수의 순서와 일치해야 합니다. .NET Framework Data Provider for OLE DB 및.NET Framework Data Provider for ODBC 자리 표시자로 저장된 프로시저에서 매개 변수를 처리 하 고 순서 대로 매개 변수 값을 적용 합니다. 또한 반환 값 매개 변수는 `Parameters` 컬렉션에 첫 번째 매개 변수로 추가되어야 합니다.

.NET Framework Data Provider for OLE DB 및.NET Framework Data Provider for ODBC는 SQL 문이나 저장된 프로시저에 매개 변수 전달에 대 한 명명 된 매개 변수를 지원 하지 않습니다. 이 경우 다음 예제와 같이 물음표(?) 자리 표시자를 사용해야 합니다.

```sql
SELECT * FROM Customers WHERE CustomerID = ?
```

따라서 `Parameter` 개체가 `Parameters` 컬렉션에 추가된 순서가 매개 변수에 대한 ? 자리 표시자의 위치와 일치해야 합니다.

### <a name="oledb-example"></a>OleDb 예제

```vb
Dim command As OleDbCommand = New OleDbCommand( _
  "SampleProc", connection)
command.CommandType = CommandType.StoredProcedure

Dim parameter As OleDbParameter = command.Parameters.Add( _
  "RETURN_VALUE", OleDbType.Integer)
parameter.Direction = ParameterDirection.ReturnValue

parameter = command.Parameters.Add( _
  "@InputParm", OleDbType.VarChar, 12)
parameter.Value = "Sample Value"

parameter = command.Parameters.Add( _
  "@OutputParm", OleDbType.VarChar, 28)
parameter.Direction = ParameterDirection.Output
```

```csharp
OleDbCommand command = new OleDbCommand("SampleProc", connection);
command.CommandType = CommandType.StoredProcedure;

OleDbParameter parameter = command.Parameters.Add(
  "RETURN_VALUE", OleDbType.Integer);
parameter.Direction = ParameterDirection.ReturnValue;

parameter = command.Parameters.Add(
  "@InputParm", OleDbType.VarChar, 12);
parameter.Value = "Sample Value";

parameter = command.Parameters.Add(
  "@OutputParm", OleDbType.VarChar, 28);
parameter.Direction = ParameterDirection.Output;
```

## <a name="odbc-example"></a>Odbc 예제

```vb
Dim command As OdbcCommand = New OdbcCommand( _
  "{ ? = CALL SampleProc(?, ?) }", connection)
command.CommandType = CommandType.StoredProcedure

Dim parameter As OdbcParameter = command.Parameters.Add("RETURN_VALUE", OdbcType.Int)
parameter.Direction = ParameterDirection.ReturnValue

parameter = command.Parameters.Add( _
  "@InputParm", OdbcType.VarChar, 12)
parameter.Value = "Sample Value"

parameter = command.Parameters.Add( _
  "@OutputParm", OdbcType.VarChar, 28)
parameter.Direction = ParameterDirection.Output
```

```csharp
OdbcCommand command = new OdbcCommand( _
  "{ ? = CALL SampleProc(?, ?) }", connection);
command.CommandType = CommandType.StoredProcedure;

OdbcParameter parameter = command.Parameters.Add( _
  "RETURN_VALUE", OdbcType.Int);
parameter.Direction = ParameterDirection.ReturnValue;

parameter = command.Parameters.Add( _
  "@InputParm", OdbcType.VarChar, 12);
parameter.Value = "Sample Value";

parameter = command.Parameters.Add( _
  "@OutputParm", OdbcType.VarChar, 28);
parameter.Direction = ParameterDirection.Output;
```

## <a name="see-also"></a>참고자료

- [명령 및 매개 변수](commands-and-parameters.md)
- [DataAdapter 매개 변수](dataadapter-parameters.md)
- [ADO.NET에서 데이터 형식 매핑](data-type-mappings-in-ado-net.md)
- [ADO.NET 개요](ado-net-overview.md)
