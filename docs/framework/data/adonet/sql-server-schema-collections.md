---
title: SQL Server 스키마 컬렉션
ms.date: 03/30/2017
ms.assetid: c6403cc3-d78b-4f85-bab1-ada7a3446ec5
ms.openlocfilehash: 0f65bbf2534eb7167baacb1405a8ce6e9769c23f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794324"
---
# <a name="sql-server-schema-collections"></a>SQL Server 스키마 컬렉션
Microsoft .NET Framework Data Provider for SQL Server는 공통 스키마 컬렉션뿐만 아니라 다른 스키마 컬렉션도 추가적으로 지원합니다. 지원되는 스키마 컬렉션은 현재 사용하고 있는 SQL Sever 버전에 따라 조금씩 다를 수 있습니다. 지원 되는 스키마 컬렉션의 목록을 확인 하려면 인수 없이 **GetSchema** 메서드를 호출 하거나 스키마 컬렉션 이름 "MetaDataCollections"을 사용 합니다. 그러면 지원되는 스키마 컬렉션의 목록, 각자 지원하는 제약 조건 수 및 사용하는 식별자 부분 수가 포함된 <xref:System.Data.DataTable>이 반환됩니다.  
  
## <a name="databases"></a>데이터베이스  
  
|ColumnName|DataType|설명|  
|----------------|--------------|-----------------|  
|database_name|String|데이터베이스의 이름입니다.|  
|dbid|Int16|데이터베이스 ID입니다.|  
|create_date|DateTime|데이터베이스를 만든 날짜입니다.|  
  
## <a name="foreign-keys"></a>외래 키  
  
|ColumnName|DataType|Description|  
|----------------|--------------|-----------------|  
|CONSTRAINT_CATALOG|문자열|제약 조건이 속하는 카탈로그입니다.|  
|CONSTRAINT_SCHEMA|String|제약 조건을 포함하는 스키마입니다.|  
|CONSTRAINT_NAME|String|이름입니다.|  
|TABLE_CATALOG|String|제약 조건이 속하는 테이블 이름입니다.|  
|TABLE_SCHEMA|String|해당 테이블을 포함하는 스키마입니다.|  
|TABLE_NAME|String|테이블 이름|  
|CONSTRAINT_TYPE|String|제약 조건의 형식입니다. "FOREIGN KEY"만 허용됩니다.|  
|IS_DEFERRABLE|String|제약 조건의 지연 가능 여부를 지정합니다. NO를 반환합니다.|  
|INITIALLY_DEFERRED|문자열|제약 조건의 초기 지연 가능 여부를 지정합니다. NO를 반환합니다.|  
  
## <a name="indexes"></a>인덱스  
  
|ColumnName|DataType|Description|  
|----------------|--------------|-----------------|  
|constraint_catalog|문자열|인덱스가 속하는 카탈로그입니다.|  
|constraint_schema|String|해당 인덱스를 포함하는 스키마입니다.|  
|constraint_name|String|인덱스의 이름입니다.|  
|table_catalog|문자열|인덱스가 연결되는 테이블 이름입니다.|  
|table_schema|String|인덱스가 연결되는 테이블을 포함하는 스키마입니다.|  
|table_name|String|테이블 이름입니다.|  
|index_name|문자열|인덱스 이름입니다.|  
  
### <a name="indexes-sql-server-2008"></a>Indexes(SQL Server 2008)  
 .NET Framework 버전 3.5 SP1 및 SQL Server 2008부터는 새로운 공간 유형, 파일 스트림 및 스파스 열을 지원하도록 Indexes 스키마 컬렉션에 다음과 같은 열이 추가되었습니다. 이러한 열은 이전 버전의 .NET Framework 및 SQL Server에서는 지원되지 않습니다.  
  
|ColumnName|DataType|Description|  
|----------------|--------------|-----------------|  
|type_desc|String|인덱스 형식은 다음 중 하나입니다.<br /><br /> -   HEAP<br />-클러스터형<br />-비클러스터형<br />-   XML<br />-   SPATIAL|  
  
## <a name="indexcolumns"></a>IndexColumns  
  
|ColumnName|DataType|설명|  
|----------------|--------------|-----------------|  
|constraint_catalog|문자열|인덱스가 속하는 카탈로그입니다.|  
|constraint_schema|문자열|해당 인덱스를 포함하는 스키마입니다.|  
|constraint_name|문자열|인덱스의 이름입니다.|  
|table_catalog|문자열|인덱스가 연결되는 테이블 이름입니다.|  
|table_schema|문자열|인덱스가 연결되는 테이블을 포함하는 스키마입니다.|  
|table_name|String|테이블 이름입니다.|  
|column_name|String|인덱스가 연결되는 ColumnName입니다.|  
|ordinal_position|Int32|열 서수 위치입니다.|  
|KeyType|Byte|개체의 형식입니다.|  
|index_name|String|인덱스 이름입니다.|  
  
## <a name="procedures"></a>절차  
  
|ColumnName|DataType|Description|  
|----------------|--------------|-----------------|  
|SPECIFIC_CATALOG|String|카탈로그의 특정 이름입니다.|  
|SPECIFIC_SCHEMA|String|스키마의 특정 이름입니다.|  
|SPECIFIC_NAME|String|카탈로그의 특정 이름입니다.|  
|ROUTINE_CATALOG|String|저장 프로시저가 속하는 카탈로그입니다.|  
|ROUTINE_SCHEMA|String|저장 프로시저를 포함하는 스키마입니다.|  
|ROUTINE_NAME|String|저장 프로시저의 이름입니다.|  
|ROUTINE_TYPE|String|저장 프로시저에 대해서는 PROCEDURE를 반환하고 함수에 대해서는 FUNCTION을 반환합니다.|  
|CREATED|DateTime|프로시저가 만들어진 시간입니다.|  
|LAST_ALTERED|DateTime|프로시저가 마지막으로 수정된 시간입니다.|  
  
## <a name="procedure-parameters"></a>Procedure Parameters  
  
|ColumnName|DataType|Description|  
|----------------|--------------|-----------------|  
|SPECIFIC_CATALOG|String|이 항목이 매개 변수인 프로시저의 카탈로그 이름입니다.|  
|SPECIFIC_SCHEMA|문자열|이 매개 변수가 속하는 프로시저가 포함된 스키마입니다.|  
|SPECIFIC_NAME|문자열|이 매개 변수가 속하는 프로시저의 이름입니다.|  
|ORDINAL_POSITION|Int32|1에서 시작하는 매개 변수의 서수 위치이며, 프로시저의 반환 값인 경우 0입니다.|  
|PARAMETER_MODE|String|입력 매개 변수이면 IN을, 출력 매개 변수이면 OUT을, 입력/출력 매개 변수이면 INOUT을 각각 반환합니다.|  
|IS_RESULT|문자열|함수인 프로시저의 결과를 나타내는 경우 YES를 반환합니다. 그렇지 않으면 NO를 반환합니다.|  
|AS_LOCATOR|String|로케이터로 선언되는 경우 YES를 반환합니다. 그렇지 않으면 NO를 반환합니다.|  
|PARAMETER_NAME|String|매개 변수의 이름입니다. 함수의 반환 값에 해당하면 NULL입니다.|  
|DATA_TYPE|문자열|시스템 제공 데이터 형식입니다.|  
|CHARACTER_MAXIMUM_LENGTH|Int32|이진 또는 문자 데이터 형식의 최대 문자 길이입니다. 그렇지 않으면 NULL을 반환합니다.|  
|CHARACTER_OCTET_LENGTH|Int32|이진 또는 문자 데이터 형식의 최대 길이(바이트)입니다. 그렇지 않으면 NULL을 반환합니다.|  
|COLLATION_CATALOG|String|매개 변수의 데이터 정렬에 대한 카탈로그 이름입니다. 해당 문자 형식 중 하나가 아니면 NULL을 반환합니다.|  
|COLLATION_SCHEMA|String|항상 NULL을 반환합니다.|  
|COLLATION_NAME|String|매개 변수의 데이터 정렬 이름입니다. 해당 문자 형식 중 하나가 아니면 NULL을 반환합니다.|  
|CHARACTER_SET_CATALOG|문자열|매개 변수 문자 집합의 카탈로그 이름입니다. 해당 문자 형식 중 하나가 아니면 NULL을 반환합니다.|  
|CHARACTER_SET_SCHEMA|String|항상 NULL을 반환합니다.|  
|CHARACTER_SET_NAME|String|매개 변수 문자 집합의 이름입니다. 해당 문자 형식 중 하나가 아니면 NULL을 반환합니다.|  
|NUMERIC_PRECISION|Byte|근접한 숫자 데이터의 정밀도, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터입니다. 그렇지 않으면 NULL을 반환합니다.|  
|NUMERIC_PRECISION_RADIX|Int16|근접한 숫자 데이터의 정밀도 기수, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터입니다. 그렇지 않으면 NULL을 반환합니다.|  
|NUMERIC_SCALE|Int32|근접한 숫자 데이터의 배율, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터입니다. 그렇지 않으면 NULL을 반환합니다.|  
|DATETIME_PRECISION|Int16|매개 변수 형식이 datetime 또는 smalldatetime이면 소수로 나타낸 시간(초)의 정밀도입니다. 그렇지 않으면 NULL을 반환합니다.|  
|INTERVAL_TYPE|String|NULL입니다. 나중에 SQL Server에서 사용하도록 예약되었습니다.|  
|INTERVAL_PRECISION|Int16|NULL입니다. 나중에 SQL Server에서 사용하도록 예약되었습니다.|  
  
## <a name="tables"></a>테이블  
  
|ColumnName|DataType|Description|  
|----------------|--------------|-----------------|  
|TABLE_CATALOG|문자열|테이블의 카탈로그입니다.|  
|TABLE_SCHEMA|String|해당 테이블을 포함하는 스키마입니다.|  
|TABLE_NAME|String|테이블 이름입니다.|  
|TABLE_TYPE|String|테이블 형식입니다. VIEW 또는 BASE TABLE일 수 있습니다.|  
  
## <a name="columns"></a>열  
  
|ColumnName|DataType|Description|  
|----------------|--------------|-----------------|  
|TABLE_CATALOG|String|테이블의 카탈로그입니다.|  
|TABLE_SCHEMA|String|해당 테이블을 포함하는 스키마입니다.|  
|TABLE_NAME|String|테이블 이름입니다.|  
|COLUMN_NAME|문자열|열 이름입니다.|  
|ORDINAL_POSITION|Int32|열 ID 번호입니다.|  
|COLUMN_DEFAULT|문자열|열 기본값입니다.|  
|IS_NULLABLE|String|열의 Null 허용 여부입니다. 이 열에서 NULL을 허용하는 경우 YES를 반환합니다. 그렇지 않으면 No가 반환됩니다.|  
|DATA_TYPE|String|시스템 제공 데이터 형식입니다.|  
|CHARACTER_MAXIMUM_LENGTH|Int32 - Sql8, Int16 - Sql7|이진 데이터, 문자 데이터 또는 텍스트 및 이미지 데이터의 최대 문자 길이입니다. 그렇지 않으면 NULL이 반환됩니다.|  
|CHARACTER_OCTET_LENGTH|Int32 - SQL8, Int16 - Sql7|이진 데이터, 문자 데이터 또는 텍스트 및 이미지 데이터의 최대 길이(바이트)입니다. 그렇지 않으면 NULL이 반환됩니다.|  
|NUMERIC_PRECISION|부호 없는 바이트|근접한 숫자 데이터의 정밀도, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터입니다. 그렇지 않으면 NULL이 반환됩니다.|  
|NUMERIC_PRECISION_RADIX|Int16|근접한 숫자 데이터의 정밀도 기수, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터입니다. 그렇지 않으면 NULL이 반환됩니다.|  
|NUMERIC_SCALE|Int32|근접한 숫자 데이터의 배율, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터입니다. 그렇지 않으면 NULL이 반환됩니다.|  
|DATETIME_PRECISION|Int16|datetime 및 SQL-92 간격 데이터 형식의 하위 형식 코드입니다. 다른 데이터 형식의 경우 NULL이 반환됩니다.|  
|CHARACTER_SET_CATALOG|String|열이 문자 데이터 또는 텍스트 데이터 형식이면 문자 집합이 있는 데이터베이스를 나타내는 master가 반환됩니다. 그렇지 않으면 NULL이 반환됩니다.|  
|CHARACTER_SET_SCHEMA|문자열|항상 NULL을 반환합니다.|  
|CHARACTER_SET_NAME|String|이 열이 문자 데이터 또는 텍스트 데이터 형식인 경우 문자 집합에 대해 고유 이름을 반환합니다. 그렇지 않으면 NULL이 반환됩니다.|  
|COLLATION_CATALOG|String|열이 문자 데이터 또는 텍스트 데이터 형식이면 정렬이 정의된 데이터베이스를 나타내는 master를 반환합니다. 그렇지 않으면 이 열은 NULL입니다.|  
  
### <a name="columns-sql-server-2008"></a>Columns(SQL Server 2008)  
 .NET Framework 버전 3.5 SP1 및 SQL Server 2008부터는 새로운 공간 유형, 파일 스트림 및 스파스 열을 지원하도록 Columns 스키마 컬렉션에 다음과 같은 열이 추가되었습니다. 이러한 열은 이전 버전의 .NET Framework 및 SQL Server에서는 지원되지 않습니다.  
  
|ColumnName|DataType|Description|  
|----------------|--------------|-----------------|  
|IS_FILESTREAM|String|열에 FILESTREAM 특성이 있으면 YES입니다.<br /><br /> 열에 FILESTREAM 특성이 없으면 NO입니다.|  
|IS_SPARSE|문자열|열이 스파스 열이면 YES입니다.<br /><br /> 열이 스파스 열이 아니면 NO입니다.|  
|IS_COLUMN_SET|String|열이 열 집합 열이면 YES입니다.<br /><br /> 열이 열 집합 열이 아니면 NO입니다.|  
  
### <a name="allcolumns-sql-server-2008"></a>AllColumns(SQL Server 2008)  
 .NET Framework 버전 3.5 SP1 및 SQL Server 2008부터는 스파스 열을 지원하도록 AllColumns 스키마 컬렉션이 추가되었습니다. AllColumns는 이전 버전의 .NET Framework 및 SQL Server에서는 지원되지 않습니다.  
  
 AllColumns는 제한 및 결과 DataTable 스키마가 Columns 스키마 컬렉션과 동일합니다. 유일한 차이점은 Columns 스키마 컬렉션에는 포함되어 있지 않은 열 집합 열이 AllColumns에는 있다는 것입니다. 다음 표에서는 이러한 열에 대해 설명합니다.  
  
|ColumnName|DataType|Description|  
|----------------|--------------|-----------------|  
|TABLE_CATALOG|String|테이블의 카탈로그입니다.|  
|TABLE_SCHEMA|문자열|해당 테이블을 포함하는 스키마입니다.|  
|TABLE_NAME|String|테이블 이름입니다.|  
|COLUMN_NAME|String|열 이름입니다.|  
|ORDINAL_POSITION|Int32|열 ID 번호입니다.|  
|COLUMN_DEFAULT|문자열|열 기본값입니다.|  
|IS_NULLABLE|문자열|열의 Null 허용 여부입니다. 이 열에서 NULL을 허용하는 경우 YES를 반환합니다. 그렇지 않으면 NO가 반환됩니다.|  
|DATA_TYPE|String|시스템 제공 데이터 형식입니다.|  
|CHARACTER_MAXIMUM_LENGTH|Int32|이진 데이터, 문자 데이터 또는 텍스트 및 이미지 데이터의 최대 문자 길이입니다. 그렇지 않으면 NULL이 반환됩니다.|  
|CHARACTER_OCTET_LENGTH|Int32|이진 데이터, 문자 데이터 또는 텍스트 및 이미지 데이터의 최대 길이(바이트)입니다. 그렇지 않으면 NULL이 반환됩니다.|  
|NUMERIC_PRECISION|부호 없는 바이트|근접한 숫자 데이터의 정밀도, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터입니다. 그렇지 않으면 NULL이 반환됩니다.|  
|NUMERIC_PRECISION_RADIX|Int16|근접한 숫자 데이터의 정밀도 기수, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터입니다. 그렇지 않으면 NULL이 반환됩니다.|  
|NUMERIC_SCALE|Int32|근접한 숫자 데이터의 배율, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터입니다. 그렇지 않으면 NULL이 반환됩니다.|  
|DATETIME_PRECISION|Int16|datetime 및 SQL-92 간격 데이터 형식의 하위 형식 코드입니다. 다른 데이터 형식의 경우 NULL이 반환됩니다.|  
|CHARACTER_SET_CATALOG|String|열이 문자 데이터 또는 텍스트 데이터 형식이면 문자 집합이 있는 데이터베이스를 나타내는 master가 반환됩니다. 그렇지 않으면 NULL이 반환됩니다.|  
|CHARACTER_SET_SCHEMA|String|항상 NULL을 반환합니다.|  
|CHARACTER_SET_NAME|String|이 열이 문자 데이터 또는 텍스트 데이터 형식인 경우 문자 집합에 대해 고유 이름을 반환합니다. 그렇지 않으면 NULL이 반환됩니다.|  
|COLLATION_CATALOG|String|열이 문자 데이터 또는 텍스트 데이터 형식이면 정렬이 정의된 데이터베이스를 나타내는 master를 반환합니다. 그렇지 않으면 이 열은 NULL입니다.|  
|IS_FILESTREAM|문자열|열에 FILESTREAM 특성이 있으면 YES입니다.<br /><br /> 열에 FILESTREAM 특성이 없으면 NO입니다.|  
|IS_SPARSE|문자열|열이 스파스 열이면 YES입니다.<br /><br /> 열이 스파스 열이 아니면 NO입니다.|  
|IS_COLUMN_SET|String|열이 열 집합 열이면 YES입니다.<br /><br /> 열이 열 집합 열이 아니면 NO입니다.|  
  
### <a name="columnsetcolumns-sql-server-2008"></a>ColumnSetColumns(SQL Server 2008)  
 .NET Framework 버전 3.5 SP1 및 SQL Server 2008부터는 스파스 열을 지원하도록 ColumnSetColumns 스키마 컬렉션이 추가되었습니다. ColumnSetColumns는 이전 버전의 .NET Framework 및 SQL Server에서는 지원되지 않습니다. ColumnSetColumns 스키마 컬렉션은 열 집합에 포함된 모든 열의 스키마를 반환합니다. 다음 표에서는 이러한 열에 대해 설명합니다.  
  
|ColumnName|DataType|Description|  
|----------------|--------------|-----------------|  
|TABLE_CATALOG|String|테이블의 카탈로그입니다.|  
|TABLE_SCHEMA|String|해당 테이블을 포함하는 스키마입니다.|  
|TABLE_NAME|String|테이블 이름입니다.|  
|COLUMN_NAME|String|열 이름입니다.|  
|ORDINAL_POSITION|Int32|열 ID 번호입니다.|  
|COLUMN_DEFAULT|String|열 기본값입니다.|  
|IS_NULLABLE|String|열의 Null 허용 여부입니다. 이 열에서 NULL을 허용하는 경우 YES를 반환합니다. 그렇지 않으면 NO가 반환됩니다.|  
|DATA_TYPE|문자열|시스템 제공 데이터 형식입니다.|  
|CHARACTER_MAXIMUM_LENGTH|Int32|이진 데이터, 문자 데이터 또는 텍스트 및 이미지 데이터의 최대 문자 길이입니다. 그렇지 않으면 NULL이 반환됩니다.|  
|CHARACTER_OCTET_LENGTH|Int32|이진 데이터, 문자 데이터 또는 텍스트 및 이미지 데이터의 최대 길이(바이트)입니다. 그렇지 않으면 NULL이 반환됩니다.|  
|NUMERIC_PRECISION|부호 없는 바이트|근접한 숫자 데이터의 정밀도, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터입니다. 그렇지 않으면 NULL이 반환됩니다.|  
|NUMERIC_PRECISION_RADIX|Int16|근접한 숫자 데이터의 정밀도 기수, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터입니다. 그렇지 않으면 NULL이 반환됩니다.|  
|NUMERIC_SCALE|Int32|근접한 숫자 데이터의 배율, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터입니다. 그렇지 않으면 NULL이 반환됩니다.|  
|DATETIME_PRECISION|Int16|datetime 및 SQL-92 간격 데이터 형식의 하위 형식 코드입니다. 다른 데이터 형식의 경우 NULL이 반환됩니다.|  
|CHARACTER_SET_CATALOG|문자열|열이 문자 데이터 또는 텍스트 데이터 형식이면 문자 집합이 있는 데이터베이스를 나타내는 master가 반환됩니다. 그렇지 않으면 NULL이 반환됩니다.|  
|CHARACTER_SET_SCHEMA|String|항상 NULL을 반환합니다.|  
|CHARACTER_SET_NAME|문자열|이 열이 문자 데이터 또는 텍스트 데이터 형식인 경우 문자 집합에 대해 고유 이름을 반환합니다. 그렇지 않으면 NULL이 반환됩니다.|  
|COLLATION_CATALOG|문자열|열이 문자 데이터 또는 텍스트 데이터 형식이면 정렬이 정의된 데이터베이스를 나타내는 master를 반환합니다. 그렇지 않으면 이 열은 NULL입니다.|  
|IS_FILESTREAM|문자열|열에 FILESTREAM 특성이 있으면 YES입니다.<br /><br /> 열에 FILESTREAM 특성이 없으면 NO입니다.|  
|IS_SPARSE|String|열이 스파스 열이면 YES입니다.<br /><br /> 열이 스파스 열이 아니면 NO입니다.|  
|IS_COLUMN_SET|String|열이 열 집합 열이면 YES입니다.<br /><br /> 열이 열 집합 열이 아니면 NO입니다.|  
  
## <a name="users"></a>사용자  
  
|ColumnName|DataType|Description|  
|----------------|--------------|-----------------|  
|uid|Int16|이 데이터베이스에 고유한 사용자 ID입니다. 데이터베이스 소유자는 1입니다.|  
|user_name|String|이 데이터베이스에 고유한 사용자 이름 및 그룹 이름입니다.|  
|createdate|DateTime|계정이 추가된 날짜입니다.|  
|updatedate|DateTime|계정이 마지막으로 변경된 날짜입니다.|  
  
## <a name="views"></a>뷰  
  
|ColumnName|DataType|Description|  
|----------------|--------------|-----------------|  
|TABLE_CATALOG|문자열|뷰의 카탈로그입니다.|  
|TABLE_SCHEMA|String|해당 뷰를 포함하는 스키마입니다.|  
|TABLE_NAME|String|뷰 이름입니다.|  
|CHECK_OPTION|문자열|WITH CHECK OPTION 형식입니다. 원래 뷰를 WITH CHECK OPTION을 사용하여 만든 경우 Is CASCADE입니다. 그렇지 않으면 NONE이 반환됩니다.|  
|IS_UPDATABLE|String|뷰를 업데이트할 수 있는지 여부를 지정합니다. 항상 NO를 반환합니다.|  
  
## <a name="viewcolumns"></a>ViewColumns  
  
|ColumnName|DataType|Description|  
|----------------|--------------|-----------------|  
|VIEW_CATALOG|String|뷰의 카탈로그입니다.|  
|VIEW_SCHEMA|문자열|해당 뷰를 포함하는 스키마입니다.|  
|VIEW_NAME|문자열|뷰 이름입니다.|  
|TABLE_CATALOG|String|이 뷰와 연관된 테이블의 카탈로그입니다.|  
|TABLE_SCHEMA|String|이 뷰와 연관된 테이블을 포함하는 스키마입니다.|  
|TABLE_NAME|String|뷰와 연관된 테이블의 이름입니다. 기본 테이블입니다.|  
|COLUMN_NAME|String|열 이름입니다.|  
  
## <a name="userdefinedtypes"></a>UserDefinedTypes  
  
|ColumnName|DataType|Description|  
|----------------|--------------|-----------------|  
|assembly_name|String|어셈블리의 파일 이름입니다.|  
|udt_name|String|어셈블리의 클래스 이름입니다.|  
|version_major|Object|주 버전 번호입니다.|  
|version_minor|Object|보조 버전 번호입니다.|  
|version_build|Object|빌드 번호입니다.|  
|version_revision|Object|수정 번호입니다.|  
|culture_info|Object|이 UDT와 연관된 문화권 정보입니다.|  
|public_key|Object|이 어셈블리에서 사용되는 공개 키입니다.|  
|is_fixed_length|Boolean|형식 길이가 항상 max_length와 같은지 여부를 지정합니다.|  
|max_length|Int16|형식의 최대 길이(바이트)입니다.|  
|Create_Date|DateTime|어셈블리가 만들어져 등록된 날짜입니다.|  
|Permission_set_desc|String|어셈블리의 권한 집합/보안 수준 이름입니다.|  
  
## <a name="see-also"></a>참고자료

- [데이터베이스 스키마 정보 검색](retrieving-database-schema-information.md)
- [ADO.NET 개요](ado-net-overview.md)
