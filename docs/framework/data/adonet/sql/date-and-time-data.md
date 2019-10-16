---
title: 날짜 및 시간 데이터
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.openlocfilehash: 90a70eaa2b5aeb8ef1f1659d7912b9ae5abc4eca
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794243"
---
# <a name="date-and-time-data"></a>날짜 및 시간 데이터
SQL Server 2008에서는 날짜 및 시간 정보를 처리하기 위한 새로운 데이터 형식을 지원합니다. 새로운 데이터 형식에는 개별 날짜 형식과 시간 형식을 비롯하여 보다 큰 범위의 확장된 데이터 형식, 정밀도 및 표준 시간대 인식 기능이 포함됩니다. .NET Framework 버전 3.5 SP(서비스 팩) 1부터는 .NET Framework Data Provider for SQL Server(<xref:System.Data.SqlClient>)에 SQL Server 2008 데이터베이스 엔진의 새로운 모든 기능이 완벽하게 지원됩니다. SqlClient에서 이러한 새 기능을 사용하려면 .NET Framework 3.5 SP1 이상을 설치해야 합니다.  
  
 SQL Server 2008 이전의 SQL Server 버전에서는 날짜 및 시간 값으로 작업할 때 `datetime` 및 `smalldatetime`의 두 가지 데이터 형식만 사용할 수 있었습니다. 두 데이터 형식 모두 날짜 값과 시간 값을 모두 포함하므로 날짜나 시간 값만 가지고 작업하기 어려웠습니다. 또한 이들 데이터 형식은 1753년 영국에 양력이 도입된 이후의 날짜만 지원합니다. 이와 같은 이전 데이터 형식은 표준 시간대를 고려하지 않으므로 여러 표준 시간대에서 발생하는 데이터를 처리하기도 어렵습니다.  
  
 SQL Server 데이터 형식에 대한 자세한 내용은 SQL Server 온라인 설명서를 참조하세요. 다음 표에서는 날짜 및 시간 데이터에 대한 초급 수준의 항목을 버전별로 보여 줍니다.  
  
 **SQL Server 온라인 설명서**  
  
1. [날짜 및 시간 데이터 사용](https://go.microsoft.com/fwlink/?LinkID=98361)  
  
## <a name="datetime-data-types-introduced-in-sql-server-2008"></a>SQL Server 2008에 도입된 날짜/시간 데이터 형식  
 다음 표에서는 새로운 날짜 및 시간 데이터 형식에 대해 설명합니다.  
  
|SQL Server 데이터 형식|Description|  
|--------------------------|-----------------|  
|`date`|`date` 데이터 형식은 하루 단위이며 범위는 01년 1월 1일부터 9999년 12월 31일까지입니다. 기본값은 1900년 1월 1일입니다. 이 데이터 형식의 스토리지 크기는 3바이트입니다.|  
|`time`|`time` 데이터 형식은 24시간제를 기준으로 시간 값만 저장합니다. `time` 데이터 형식은 100나노초 단위이며 범위는 00:00:00.0000000부터 23:59:59.9999999까지입니다. 기본값은 00:00:00.0000000(자정)입니다. `time` 데이터 형식은 초에 대해 소수로 표현되는 사용자 정의 정밀도를 지원하며 지정된 정밀도에 따라 스토리지 크기는 3바이트에서 6바이트까지의 범위 내에서 달라집니다.|  
|`datetime2`|`datetime2` 데이터 형식은 `date` 및 `time` 데이터 형식의 범위와 정밀도를 하나의 데이터 형식으로 통합합니다.<br /><br /> 이 형식의 기본값과 문자열 리터럴 형식은 `date` 및 `time` 데이터 형식에 정의된 것과 동일합니다.|  
|`datetimeoffset`|`datetimeoffset` 데이터 형식은 `datetime2`의 모든 기능을 포함하며 표준 시간대 오프셋 기능을 추가로 지원합니다. 표준 시간대 오프셋은 [+&#124;-] HH: MM로 표시 됩니다. HH는 00부터 14까지의 두 자리 숫자로, 표준 시간대 오프셋의 시간을 나타냅니다. MM은 00부터 59까지의 두 자리 숫자로, 표준 시간대 오프셋의 분을 나타냅니다. 시간 형식은 100나노초까지 지원합니다. 필수 값인 + 또는 - 부호는 현지 시간을 얻기 위해 표준 시간대 오프셋을 UTC(Universal Time Coordinate 또는 그리니치 표준시)에 더할 것인지 또는 UTC에서 뺄 것인지를 나타냅니다.|  
  
> [!NOTE]
> `Type System Version` 키워드 사용에 대한 자세한 내용은 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>을 참조하세요.  
  
## <a name="date-format-and-date-order"></a>날짜 형식 및 날짜 순서  
 SQL Server에서 날짜 및 시간 값을 구문 분석하는 방법은 형식 시스템 버전과 서버 버전뿐만 아니라 서버의 기본 언어 설정과 형식 설정에 따라 달라집니다. 특정 언어의 날짜 형식에 사용할 수 있는 날짜 문자열이라도 다른 언어와 날짜 형식 설정을 사용하는 연결에서 쿼리를 실행할 경우 인식되지 않을 수 있습니다.  
  
 Transact-SQL SET LANGUAGE 문은 날짜 부분의 순서를 결정하는 DATEFORMAT을 암시적으로 설정합니다. 연결에 SET DATEFORMAT Transact-SQL 문을 사용하면 날짜 부분을 MDY, DMY, YMD, YDM, MYD 또는 DYM 순서로 정렬하여 날짜 값을 명확하게 나타낼 수 있습니다.  
  
 연결에 DATEFORMAT을 지정하지 않으면 SQL Server에서는 연결과 관련된 기본 언어를 사용합니다. 예를 들어 '01/02/03'의 경우 언어가 영어(미국)로 설정된 서버에서는 MDY(January 2, 2003)로 해석되고 언어가 영어(영국)로 설정된 서버에서는 DMY(February 1, 2003)로 해석됩니다. 연도는 세기 값의 구분 기준 날짜를 정의하는 SQL Server의 연도 구분 규칙을 사용하여 결정됩니다. 자세한 내용은 SQL Server 온라인 설명서의 [두 자리 연도 구분 옵션](https://go.microsoft.com/fwlink/?LinkId=120473) 을 참조 하십시오.  
  
> [!NOTE]
> YDM 날짜 형식은 문자열 형식에서 `date`, `time`, `datetime2` 또는 `datetimeoffset`으로 변환할 경우 지원되지 않습니다.  
  
 SQL Server 날짜 및 시간 데이터를 해석 하는 방법에 대 한 자세한 내용은 SQL Server 2008 온라인 설명서의 [날짜 및 시간 데이터 사용](https://go.microsoft.com/fwlink/?LinkID=98361) 을 참조 하십시오.  
  
## <a name="datetime-data-types-and-parameters"></a>날짜/시간 데이터 형식 및 매개 변수  
 새 날짜 및 시간 데이터 형식을 지원하기 위해 다음 열거형이 <xref:System.Data.SqlDbType>에 추가되었습니다.  
  
- `SqlDbType.Date`  
  
- `SqlDbType.Time`  
  
- `SqlDbType.DateTime2`  
  
- `SqlDbType.DateTimeOffSet`  

<xref:System.Data.SqlClient.SqlParameter> 위의<xref:System.Data.SqlDbType> 열거형 중 하나를 사용 하 여의 데이터 형식을 지정할 수 있습니다. 

> [!NOTE]
> 의 속성`DbType` 을 로`SqlDbType.Date`설정할수없습니다. `SqlParameter`

 또한 <xref:System.Data.SqlClient.SqlParameter> 개체의 <xref:System.Data.SqlClient.SqlParameter.DbType%2A> 속성을 특정 `SqlParameter` 열거형 값으로 설정하면 일반적인 방식으로 <xref:System.Data.DbType>의 형식을 지정할 수 있습니다. <xref:System.Data.DbType> 및 `datetime2` 데이터 형식을 지원하기 위해 다음 열거형 값이 `datetimeoffset`에 추가되었습니다.  
  
- DbType.DateTime2  
  
- DbType.DateTimeOffset  
  
 이러한 새 열거형은 이전 버전의 .NET Framework에서 사용할 수 있는 `Date`, `Time` 및 `DateTime` 열거형을 보완합니다.  
  
 매개 변수 개체의 .NET Framework 데이터 공급자 형식은 매개 변수 개체 값의 .NET Framework 형식이나 매개 변수 개체의 `DbType`에서 유추됩니다. 새 날짜 및 시간 데이터 형식을 지원하기 위해 도입된 새 <xref:System.Data.SqlTypes> 데이터 형식은 없습니다. 다음 표에서는 SQL Server 2008 날짜 및 시간 데이터 형식과 CLR 데이터 형식 간의 매핑에 대해 설명합니다.  
  
|SQL Server 데이터 형식|.NET Framework 형식|System.Data.SqlDbType|System.Data.DbType|  
|--------------------------|-------------------------|---------------------------|------------------------|  
|날짜|System.DateTime|날짜|날짜|  
|Time|System.TimeSpan|시간|시간|  
|Datetime2|System.DateTime|DateTime2|DateTime2|  
|Datetimeoffset|System.DateTimeOffset|DateTimeOffset|DateTimeOffset|  
|Datetime|System.DateTime|DateTime|DateTime|  
|smalldatetime|System.DateTime|DateTime|DateTime|  
  
### <a name="sqlparameter-properties"></a>SqlParameter 속성  
 다음 표에서는 날짜 및 시간 데이터 형식과 관련된 `SqlParameter` 속성에 대해 설명합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|<xref:System.Data.SqlClient.SqlParameter.IsNullable%2A>|값이 nullable인지 여부를 가져오거나 설정합니다. 서버에 null 매개 변수 값을 보낼 때는 <xref:System.DBNull>(Visual Basic에서는 `null`)이 아니라 `Nothing`을 지정해야 합니다. 데이터베이스 null에 대한 자세한 내용은 [Handling Null Values](handling-null-values.md)를 참조하세요.|  
|<xref:System.Data.SqlClient.SqlParameter.Precision%2A>|값을 나타내는 데 사용되는 최대 자릿수를 가져오거나 설정합니다. 날짜 및 시간 데이터 형식에서는 이 설정이 무시됩니다.|  
|<xref:System.Data.SqlClient.SqlParameter.Scale%2A>|, `Time` `DateTime2`및 에대해값의시간부분을확인하는소수자릿수를가져오거나설정합니다.`DateTimeOffset` 기본값은 0이며 이는 값에서 실제 자릿수가 유추되어 서버에 전송됨을 의미합니다.|  
|<xref:System.Data.SqlClient.SqlParameter.Size%2A>|날짜 및 시간 데이터 형식에서 무시됩니다.|  
|<xref:System.Data.SqlClient.SqlParameter.Value%2A>|매개 변수 값을 가져오거나 설정합니다.|  
|<xref:System.Data.SqlClient.SqlParameter.SqlValue%2A>|매개 변수 값을 가져오거나 설정합니다.|  
  
> [!NOTE]
> 시간 값이 0보다 작거나 24시간보다 크면 <xref:System.ArgumentException>이 throw됩니다.  
  
### <a name="creating-parameters"></a>매개 변수 만들기  
 <xref:System.Data.SqlClient.SqlParameter> 개체는 해당 생성자를 사용하거나, <xref:System.Data.SqlClient.SqlCommand>의 <xref:System.Data.SqlClient.SqlCommand.Parameters%2A> 메서드를 호출하여 `Add`<xref:System.Data.SqlClient.SqlParameterCollection> 컬렉션에 추가하는 방법으로 만들 수 있습니다. `Add` 메서드는 생성자 인수 또는 기존 매개 변수 개체를 입력으로 사용합니다.  
  
 이 항목의 다음 섹션에서는 날짜 및 시간 매개 변수를 지정하는 방법에 대한 예제를 제공합니다. 매개 변수 사용에 대 한 추가 예제는 [매개 변수 및 매개 변수 데이터 형식](../configuring-parameters-and-parameter-data-types.md) 및 [DataAdapter 매개 변수](../dataadapter-parameters.md)구성을 참조 하세요.  
  
### <a name="date-example"></a>Date 예제  
 다음 코드 조각에서는 `date` 매개 변수를 지정하는 방법을 보여 줍니다.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Date";  
parameter.SqlDbType = SqlDbType.Date;  
parameter.Value = "2007/12/1";  
```  
  
```vb  
Dim parameter As New SqlParameter()  
parameter.ParameterName = "@Date"  
parameter.SqlDbType = SqlDbType.Date  
parameter.Value = "2007/12/1"  
```  
  
### <a name="time-example"></a>Time 예제  
 다음 코드 조각에서는 `time` 매개 변수를 지정하는 방법을 보여 줍니다.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@time";  
parameter.SqlDbType = SqlDbType.Time;  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
```vb  
Dim parameter As New SqlParameter()  
parameter.ParameterName = "@Time"  
parameter.SqlDbType = SqlDbType.Time  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
### <a name="datetime2-example"></a>Datetime2 예제  
 다음 코드 조각에서는 날짜 부분과 시간 부분이 모두 포함된 `datetime2` 매개 변수를 지정하는 방법을 보여 줍니다.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Datetime2";  
parameter.SqlDbType = SqlDbType.DateTime2;  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
```vb  
Dim parameter As New SqlParameter()  
parameter.ParameterName = "@Datetime2"  
parameter.SqlDbType = SqlDbType.DateTime2  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
### <a name="datetimeoffset-example"></a>DateTimeOffSet 예제  
 다음 코드 예제에서는 날짜, 시간 및 표준 시간대 오프셋이 0으로 설정된 `DateTimeOffSet` 매개 변수를 지정하는 방법을 보여 줍니다.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@DateTimeOffSet";  
parameter.SqlDbType = SqlDbType.DateTimeOffSet;  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
```vb  
Dim parameter As New SqlParameter()  
parameter.ParameterName = "@DateTimeOffSet"  
parameter.SqlDbType = SqlDbType.DateTimeOffSet  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
### <a name="addwithvalue"></a>AddWithValue  
 다음 코드 조각에서 볼 수 있는 것처럼 `AddWithValue`의 <xref:System.Data.SqlClient.SqlCommand> 메서드를 사용하여 매개 변수를 제공할 수도 있습니다. 그러나 `AddWithValue` 메서드를 사용할 경우 매개 변수에 <xref:System.Data.SqlClient.SqlParameter.DbType%2A> 또는 <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A>을 지정할 수 없습니다.  
  
```csharp  
command.Parameters.AddWithValue(   
    "@date", DateTimeOffset.Parse("16660902"));  
```  
  
```vb  
command.Parameters.AddWithValue( _  
    "@date", DateTimeOffset.Parse("16660902"))  
```  
  
 매개 `@date` 변수는 서버의 `date`, `datetime`또는 `datetime2` 데이터 형식에 매핑될 수 있습니다. 새 `datetime` 데이터 형식을 사용할 때는 인스턴스의 데이터 형식을 매개 변수의 <xref:System.Data.SqlDbType> 속성에 명시적으로 설정해야 합니다. <xref:System.Data.SqlDbType.Variant>를 사용하거나 암시적으로 매개 변수 값을 제공할 경우 `datetime` 및 `smalldatetime` 데이터 형식에 대한 이전 버전과의 호환성에 문제가 발생할 수 있습니다.  
  
 다음 표에서는 각 CLR 형식에서 유추되는 `SqlDbTypes`을 보여 줍니다.  
  
|CLR 형식|유추되는 SqlDbType|  
|--------------|------------------------|  
|DateTime|SqlDbType.DateTime|  
|TimeSpan|SqlDbType.Time|  
|DateTimeOffset|SqlDbType.DateTimeOffset|  
  
## <a name="retrieving-date-and-time-data"></a>날짜 및 시간 데이터 검색  
 다음 표에서는 SQL Server 2008 날짜 및 시간 값을 검색하는 데 사용되는 메서드에 대해 설명합니다.  
  
|SqlClient 메서드|Description|  
|----------------------|-----------------|  
|<xref:System.Data.SqlClient.SqlDataReader.GetDateTime%2A>|지정된 열 값을 <xref:System.DateTime> 구조체로 검색합니다.|  
|<xref:System.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|지정된 열 값을 <xref:System.DateTimeOffset> 구조체로 검색합니다.|  
|<xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>|필드의 기본 공급자별 형식을 반환합니다. 새 날짜 및 시간 형식의 경우 `GetFieldType`과 동일한 형식을 반환합니다.|  
|<xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>|지정된 열의 값을 검색합니다. 새 날짜 및 시간 형식의 경우 `GetValue`와 동일한 형식을 반환합니다.|  
|<xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>|지정된 배열의 값을 검색합니다.|  
|<xref:System.Data.SqlClient.SqlDataReader.GetSqlString%2A>|열 값을 <xref:System.Data.SqlTypes.SqlString>으로 검색합니다. 데이터를 <xref:System.InvalidCastException>으로 표현할 수 없으면 `SqlString`이 발생합니다.|  
|<xref:System.Data.SqlClient.SqlDataReader.GetSqlValue%2A>|열 데이터를 해당 기본 `SqlDbType`으로 검색합니다. 새 날짜 및 시간 형식의 경우 `GetValue`와 동일한 형식을 반환합니다.|  
|<xref:System.Data.SqlClient.SqlDataReader.GetSqlValues%2A>|지정된 배열의 값을 검색합니다.|  
|<xref:System.Data.SqlClient.SqlDataReader.GetString%2A>|Type System Version이 SQL Server 2005로 설정되어 있는 경우 열 값을 문자열로 검색합니다. 데이터를 문자열로 표현할 수 없으면 <xref:System.InvalidCastException>이 발생합니다.|  
|<xref:System.Data.SqlClient.SqlDataReader.GetTimeSpan%2A>|지정된 열 값을 <xref:System.TimeSpan> 구조체로 검색합니다.|  
|<xref:System.Data.SqlClient.SqlDataReader.GetValue%2A>|지정된 열 값을 기본 CLR 형식으로 검색합니다.|  
|<xref:System.Data.SqlClient.SqlDataReader.GetValues%2A>|배열의 열 값을 검색합니다.|  
|<xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>|결과 집합의 메타데이터를 설명하는 <xref:System.Data.DataTable>을 반환합니다.|  
  
> [!NOTE]
> SQL Server에서 in-process로 실행되는 코드에는 새 날짜 및 시간 `SqlDbTypes`이 지원되지 않습니다. 이러한 형식 중 하나를 서버에 전달하면 예외가 발생합니다.  
  
## <a name="specifying-date-and-time-values-as-literals"></a>날짜 및 시간 값을 리터럴로 지정  
 여러 가지 리터럴 문자열 형식을 사용하여 날짜 및 시간 데이터 형식을 지정할 수 있습니다. 이렇게 하면 SQL Server에서는 이러한 리터럴 문자열 형식을 런타임에 평가하여 내부 날짜/시간 구조체로 변환합니다. SQL Server에서는 작은따옴표(')로 묶인 날짜 및 시간 데이터를 인식합니다. 다음 예제에서는 몇 가지 형식을 보여 줍니다.  
  
- `'October 15, 2006'`과 같은 알파벳 날짜 형식  
  
- `'10/15/2006'`과 같은 숫자 날짜 형식  
  
- `'20061015'`(ISO 표준 날짜 형식을 사용할 경우 2006년 10월 15일로 해석됨)와 같은 구분되지 않은 문자열 형식  
  
> [!NOTE]
> 날짜 및 시간 데이터 형식의 모든 리터럴 문자열 형식 및 기타 기능에 대한 자세한 내용은 SQL Server 온라인 설명서를 참조하세요.  
  
 시간 값이 0보다 작거나 24시간보다 크면 <xref:System.ArgumentException>이 throw됩니다.  
  
## <a name="resources-in-sql-server-2008-books-online"></a>SQL Server 2008 온라인 설명서 리소스  
 SQL Server 2008에서의 날짜 및 시간 값 사용 방법은 SQL Server 2008 온라인 설명서의 다음 리소스를 참조하세요.  
  
|항목|Description|  
|-----------|-----------------|  
|[날짜 및 시간 데이터 형식 및 함수 (Transact-sql)](https://go.microsoft.com/fwlink/?LinkId=98360)|모든 Transact-SQL 날짜 및 시간 데이터 형식 및 함수에 대한 개요를 제공합니다.|  
|[날짜 및 시간 데이터 사용](https://go.microsoft.com/fwlink/?LinkId=98361)|날짜 및 시간 데이터 형식과 함수를 비롯하여 이러한 데이터 형식의 사용 방법에 대한 정보를 제공합니다.|  
|[데이터 형식 (Transact-sql)](https://go.microsoft.com/fwlink/?LinkId=98362)|SQL Server 2008에 제공되는 시스템 데이터 형식에 대해 설명합니다.|  
  
## <a name="see-also"></a>참고자료

- [SQL Server 데이터 형식 매핑](../sql-server-data-type-mappings.md)
- [매개 변수 및 매개 변수 데이터 형식 구성](../configuring-parameters-and-parameter-data-types.md)
- [SQL Server 데이터 형식 및 ADO.NET](sql-server-data-types.md)
- [ADO.NET 개요](../ado-net-overview.md)
