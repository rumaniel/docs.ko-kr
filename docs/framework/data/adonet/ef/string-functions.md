---
title: 문자열 함수
ms.date: 03/30/2017
ms.assetid: 338f0c26-8aee-43eb-bd1a-ec0849a376b9
ms.openlocfilehash: 05b1e4d4615e496c827196849bbf8d41bc92998f
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70248258"
---
# <a name="string-functions"></a>문자열 함수
.NET Framework Data Provider for SQL Server(SqlClient)에서는 입력 `String`에 대해 연산을 수행하고 `String` 또는 숫자 값 결과를 반환하는 `String` 함수를 제공합니다. 이 함수는 SqlClient를 사용할 때 사용 가능한 SqlServer 네임스페이스에 있습니다. 공급자의 네임스페이스 속성이 있으면 특정 구문(예: 형식 및 함수)에 대해 이 공급자가 사용하는 접두사를 Entity Framework에서 찾을 수 있습니다.  
  
 다음 표에서는 SqlClient `String` 함수를 보여 줍니다.  
  
|함수|설명|  
|--------------|-----------------|  
|`ASCII(expression)`|문자열 식에서 가장 왼쪽 문자의 ASCII 코드 값을 반환합니다.<br /><br /> **인수**<br /><br /> `expression`: ASCII `String` 형식의 유효한 식입니다.<br /><br /> **반환 값**<br /><br /> `Int32`입니다.<br /><br /> **예제**<br /><br /> `SqlServer.ASCII('A')`|  
|`CHAR(expression)`|`Int32` 코드를 ASCII String으로 변환합니다.<br /><br /> **인수**<br /><br /> `expression`: `Int32`입니다.<br /><br /> **반환 값**<br /><br /> ASCII `String`입니다.<br /><br /> **예제**<br /><br /> `SqlServer.char(97)`|  
|`CHARINDEX(expression1, expression2 [, start_location])`|문자열에서 지정된 식이 시작되는 위치를 반환합니다.<br /><br /> **인수**<br /><br /> `expression1`: 찾을 문자열 시퀀스를 포함하는 식입니다. 이 식은 String(ASCII 또는 유니코드) 형식 또는 Binary 형식일 수 있습니다.<br /><br /> `expression2`: 지정된 시퀀스를 검색할 식(일반적으로 열)입니다. 이 식은 String(ASCII 또는 유니코드) 형식 또는 Binary 형식일 수 있습니다.<br /><br /> `start_location`:(선택적) i n t 64에서 expression1 검색을 시작할 문자 위치를 나타내는 Int64 (SQL Server 2000에서는 반환 되지 않음) 또는 Int32입니다. start_location이 지정되지 않았거나 음수이거나 0이면 expression2의 시작 부분에서 검색이 시작됩니다.<br /><br /> **반환 값**<br /><br /> `Int32`입니다.<br /><br /> **예제**<br /><br /> `SqlServer.CHARINDEX('h', 'habcdefgh', 2)`|  
|`DIFFERENCE(expression, expression)`|두 문자열의 `SOUNDEX` 값을 비교하여 유사성을 계산합니다.<br /><br /> **인수**<br /><br /> ASCII 또는 유니코드 `String` 형식입니다. `expression`은 상수, 변수 또는 열일 수 있습니다.<br /><br /> **반환 값**<br /><br /> 두 문자 식의 SOUNDEX 값을 비교하여 차이를 나타내는 `Int32`를 반환합니다. 범위는 0에서 4까지입니다. 0은 유사점이 적거나 없음을 나타내며 4는 유사점이 많거나 동일한 값임을 나타냅니다.<br /><br /> **예제**<br /><br /> `// The following example returns a DIFFERENCE value of 4,`<br /><br /> `//the least possible difference or the best match.`<br /><br /> `SqlServer.DIFFERENCE('Green','Greene');`|  
|`LEFT(expression, count)`|지정된 문자 수만큼 문자열의 왼쪽 부분을 반환합니다.<br /><br /> **인수**<br /><br /> `expression`: 유니코드 또는 ASCII String 형식입니다. character_expression을 명시적으로 변환하려면 CAST 함수를 사용합니다.<br /><br /> `count`: character_expression에서 반환할 문자 수를 지정하는 `Int64`(SQL Server 2000에서는 반환되지 않음) 또는 `Int32` 형식입니다.<br /><br /> **반환 값**<br /><br /> 유니코드 또는 ASCII `String`입니다.<br /><br /> **예제**<br /><br /> `SqlServer.LEFT('SQL Server', 4)`|  
|`LEN(expression)`|지정한 String 식의 후행 공백을 제외한 문자 수를 반환합니다.<br /><br /> **인수**<br /><br /> `expression`: `String` (유니코드 또는 ASCII) 형식 `Binary` 또는 형식의 식입니다.<br /><br /> **반환 값**<br /><br /> `Int32`입니다.<br /><br /> **예제**<br /><br /> `SqlServer.LEN('abcd')`|  
|`LOWER(expression)`|대문자 데이터를 소문자로 변환한 후 `String` 식을 반환합니다.<br /><br /> **인수**<br /><br /> `expression`: `String` 형식의 모든 유효한 식입니다.<br /><br /> **반환 값**<br /><br /> `String`<br /><br /> **예제**<br /><br /> `SqlServer.LOWER('AbB')`|  
|`LTRIM(expression)`|선행 공백을 제거하고 `String` 식을 반환합니다.<br /><br /> **인수**<br /><br /> `expression`: `String` 형식의 모든 유효한 식입니다.<br /><br /> **반환 값**<br /><br /> `String`<br /><br /> **예제**<br /><br /> `SqlServer.LTRIM('   d')`|  
|`NCHAR(expression)`|유니코드 표준의 정의에 따라 지정된 정수 코드에 해당하는 유니코드 `String`을 반환합니다.<br /><br /> **인수**<br /><br /> `expression`: `Int32`입니다.<br /><br /> **반환 값**<br /><br /> 유니코드 `String`입니다.<br /><br /> **예제**<br /><br /> `SqlServer.NCHAR(65)`|  
|`PATINDEX('%pattern%', expression)`|지정된 `String` 식에서 처음 발견된 패턴의 시작 위치를 반환합니다.<br /><br /> **인수**<br /><br /> `'%pattern%'`: ASCII 또는 유니코드 `String` 형식입니다. 와일드카드 문자를 사용할 수 있지만 첫 번째 또는 마지막 문자를 검색할 때 이외에는 패턴 앞뒤에 % 문자가 있어야 합니다.<br /><br /> `expression`: 지정된 패턴을 검색할 ASCII 또는 유니코드 `String`입니다.<br /><br /> **반환 값**<br /><br /> `Int32`입니다.<br /><br /> **예제**<br /><br /> `SqlServer.PATINDEX('abc', 'ab')`|  
|`QUOTENAME('char_string' [, 'quote_char'])`|입력 문자열이 유효한 SQL Server 2005 구분 식별자가 되도록 구분 기호를 추가한 유니코드 `String`을 반환합니다.<br /><br /> **인수**<br /><br /> `char_string`: 유니코드 `String`입니다.<br /><br /> `quote_char`: 구분 기호로 사용되는 단일 문자로 된 문자열입니다. 작은따옴표( ' ), 왼쪽 또는 오른쪽 대괄호( [ ] ) 또는 큰따옴표( " )일 수 있습니다. `quote_char`를 지정하지 않은 경우 대괄호가 사용됩니다.<br /><br /> **반환 값**<br /><br /> 유니코드 `String`입니다.<br /><br /> **예제**<br /><br /> `SqlServer.QUOTENAME('abc[]def')`|  
|`REPLACE(expression1, expression2, expression3)`|문자 식을 다른 문자 식으로 바꿉니다.<br /><br /> **인수**<br /><br /> `expression1`: 검색할 문자열 식입니다. `expression1`는 유니코드 또는 ASCII 문자열 형식일 수 있습니다.<br /><br /> `expression2`: 찾을 부분 문자열입니다. `expression2`는 유니코드 또는 ASCII 문자열 형식일 수 있습니다.<br /><br /> `expression3`: 대체 문자열입니다. `expression3`는 유니코드 또는 ASCII 문자열 형식일 수 있습니다.<br /><br /> **예제**<br /><br /> `SqlServer.REPLACE('aabbcc', 'bc', 'zz')`|  
|`REPLICATE(char_expression, int_expression)`|문자 식을 지정한 횟수만큼 반복합니다.<br /><br /> **인수**<br /><br /> `char_expression`: 유니코드 또는 ASCII `String` 형식입니다.<br /><br /> `int_expression`: `Int64`(SQL Server 2000에서는 지원되지 않음) 또는 `Int32`입니다.<br /><br /> **반환 값**<br /><br /> 유니코드 또는 ASCII `String` 형식입니다.<br /><br /> **예제**<br /><br /> `SqlServer.REPLICATE('aa',2)`|  
|`REVERSE(expression)`|문자 위치가 입력 문자열의 역순으로 된 유니코드 또는 ASCII String을 반환합니다.<br /><br /> **인수**<br /><br /> `expression`: 유니코드 또는 ASCII `String` 형식입니다.<br /><br /> **반환 값**<br /><br /> 유니코드 또는 ASCII `String` 형식입니다.<br /><br /> **예제**<br /><br /> `SqlServer.REVERSE('abcd')`|  
|`RIGHT(char_expression, count)`|지정된 문자 수만큼 문자열의 오른쪽 부분을 반환합니다.<br /><br /> **인수**<br /><br /> `char_expression`: 유니코드 또는 ASCII 문자열 형식입니다. character_expression을 명시적으로 변환하려면 CAST 함수를 사용합니다.<br /><br /> `count`: character_expression에서 반환할 문자 수를 지정하는 `Int64`(SQL Server 2000에서는 반환되지 않음) 또는 `Int32` 형식입니다.<br /><br /> **반환 값**<br /><br /> ASCII `String` 형식입니다.<br /><br /> **예제**<br /><br /> `SqlServer.RIGHT('SQL Server', 6)`|  
|`RTRIM(expression)`|후행 공백을 제거하고 유니코드 또는 ASCII String을 반환합니다.<br /><br /> **인수**<br /><br /> `expression`: 유니코드 또는 ASCII `String` 형식입니다.<br /><br /> **반환 값**<br /><br /> 유니코드 또는 ASCII `String` 형식입니다.<br /><br /> **예제**<br /><br /> `SqlServer.RTRIM('   d   e      ')`|  
|`SOUNDEX(expression)`|두 문자열의 유사성을 평가 하는 네 문자 (SOUNDEX) 코드를 반환 합니다. **인수**<br /><br /> `expression`: 유니코드 또는 ASCII String 형식입니다.<br /><br /> **반환 값**<br /><br /> ASCII `String`입니다. 4자(SOUNDEX) 코드는 두 문자열의 유사성을 계산하는 문자열입니다.<br /><br /> **예제**<br /><br /> `Select SqlServer.SOUNDEX('Smith'), SqlServer.SOUNDEX('Smythe') FROM {1}`<br /><br /> **전용인**<br /><br /> `----- -----  S530  S530`|  
|`SPACE(int_expression)`|반복되는 공백으로 구성된 ASCII `String`을 반환합니다.<br /><br /> **인수**<br /><br /> `int_expression`: 공백의 수를 나타내는 `Int64`(SQL Server 2000에서는 반환되지 않음) 또는 `Int32`입니다.<br /><br /> **반환 값**<br /><br /> ASCII `String`입니다.<br /><br /> **예제**<br /><br /> `SqlServer.SPACE(2)`|  
|`STR(float_expression [, length [, decimal]])`|숫자 데이터에서 변환된 ASCII `String`을 반환합니다.<br /><br /> **인수**<br /><br /> `float _expression`: 소수점이 있는 근사치(`Double`) 데이터 형식의 식입니다.<br /><br /> `length`: (선택 사항) 전체 길이를 나타내는 `Int32`입니다. 소수점, 부호, 숫자 및 공백을 포함한 길이입니다. 기본값은 10입니다.<br /><br /> `decimal`소수점 오른쪽에 있는 `Int32` 자릿수를 나타내는:(선택)입니다. decimal은 16 이하여야 합니다. decimal이 16을 초과할 경우 결과가 소수점 이하 16자릿수에서 잘립니다.<br /><br /> **반환 값**<br /><br /> ASCII `String`입니다.<br /><br /> **예제**<br /><br /> `SqlServer.STR(212.0)`|  
|`STUFF(str_expression, start, length, str_expression_to_insert)`|문자열 식에서 지정된 시작점부터 지정된 길이만큼 문자를 삭제하고 다른 문자 집합을 삽입합니다.<br /><br /> **인수**<br /><br /> `str_expression`: 유니코드 또는 ASCII `String`입니다.<br /><br /> `start:`삭제 및 삽입을 시작할 위치를 지정 하 `Int32` 는 (SQLServer2000에서반환되지않음)또는값입니다.`Int64`<br /><br /> `length`: 삭제할 문자 수를 지정하는 `Int64`(SQL Server 2000에서는 반환되지 않음) 또는 `Int32` 값입니다.<br /><br /> `str_expression_to_insert`: 유니코드 또는 ASCII `String`입니다.<br /><br /> **반환 값**<br /><br /> 유니코드 또는 ASCII `String`입니다.<br /><br /> **예제**<br /><br /> `SqlServer.STUFF('abcd', 2, 2, 'zz')`|  
|`SUBSTRING(str_expression, start, length)`|`String` 식의 일부를 반환합니다.<br /><br /> **인수**<br /><br /> `str_expression`: `String`(ASCII 또는 유니코드) 형식 또는 `Binary` 형식의 식입니다.<br /><br /> `start`: 부분 문자열이 시작되는 위치를 지정하는 `Int64`(SQL Server 2000에서는 반환되지 않음) 또는 `Int32`입니다. 1은 문자열의 첫 번째 문자를 가리킵니다.<br /><br /> `length`: 식에서 반환할 문자 수를 지정하는 `Int64`(SQL Server 2000에서는 반환되지 않음) 또는 `Int32`입니다.<br /><br /> **반환 값**<br /><br /> `String`(ASCII 또는 유니코드) 형식 또는 `Binary` 형식입니다.<br /><br /> **예제**<br /><br /> `SqlServer.SUBSTRING('abcd', 2, 2)`|  
|`UNICODE(expression)`|유니코드 표준의 정의에 따라 입력 식에 있는 첫 문자의 정수 값을 반환합니다.<br /><br /> **인수**<br /><br /> `expression`: 유니코드 `String`입니다.<br /><br /> **반환 값**<br /><br /> `Int32`입니다.<br /><br /> **예제**<br /><br /> `SqlServer.UNICODE('a')`|  
|`UPPER(expression)`|소문자 데이터를 대문자로 변환한 후 `String` 식을 반환합니다.<br /><br /> **인수**<br /><br /> `expression`: ASCII 또는 유니코드 String 형식의 식입니다.<br /><br /> **반환 값**<br /><br /> ASCII 또는 유니코드 `String` 형식입니다.<br /><br /> **예제**<br /><br /> `SqlServer.UPPER('AbB')`|  
  
 SqlClient에서 지원하는 `String` 함수에 대한 자세한 내용은 SqlClient 공급자 매니페스트에 지정한 SQL Server 버전의 설명서를 참조하세요.  
  
|SQL Server 2000|SQL Server 2005|SQL Server 2008|  
|---------------------|---------------------|---------------------|  
|[문자열 함수 (Transact-sql)](https://go.microsoft.com/fwlink/?LinkId=115915)|[문자열 함수 (Transact-sql)](https://go.microsoft.com/fwlink/?LinkId=115916)|[문자열 함수 (Transact-sql)](https://go.microsoft.com/fwlink/?LinkId=115914)|  
  
## <a name="see-also"></a>참고자료

- [Entity Framework용 SqlClient 기능](sqlclient-for-ef-functions.md)
- [Entity Framework용 SqlClient에서 알려진 문제](known-issues-in-sqlclient-for-entity-framework.md)
