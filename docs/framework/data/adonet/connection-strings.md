---
title: ADO.NET의 연결 문자열
ms.date: 10/10/2018
ms.assetid: 745c5f95-2f02-4674-b378-6d51a7ec2490
ms.openlocfilehash: 8f726ca71ba955ef542d15e0e8318c2b310e607e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784910"
---
# <a name="connection-strings-in-adonet"></a>ADO.NET의 연결 문자열

연결 문자열에는 데이터 공급자에서 데이터 소스에 매개 변수로 전달되는 초기화 정보가 있습니다. 데이터 공급자는 연결 문자열을 <xref:System.Data.Common.DbConnection.ConnectionString?displayProperty=nameWithType> 속성의 값으로 받습니다. 공급자는 연결 문자열을 구문 분석 하 여 구문이 올바르고 키워드가 지원 되는지 확인 합니다. 그런 다음 <xref:System.Data.Common.DbConnection.Open?displayProperty=nameWithType> 메서드는 구문 분석 된 연결 매개 변수를 데이터 원본에 전달 합니다. 데이터 원본은 추가 유효성 검사를 수행 하 고 연결을 설정 합니다.

## <a name="connection-string-syntax"></a>연결 문자열 구문

연결 문자열은 세미콜론으로 구분 된 키/값 매개 변수 쌍의 목록입니다.

```
keyword1=value; keyword2=value;
```

키워드는 대/소문자를 구분 하지 않습니다. 그러나 값은 데이터 원본에 따라 대/소문자를 구분 하지 않을 수 있습니다. 키워드와 값 모두 [공백 문자](https://en.wikipedia.org/wiki/Whitespace_character#Unicode)를 포함할 수 있습니다. 선행 및 후행 공백은 키워드 및 따옴표 붙지 않은 값에서 무시 됩니다.

값에 세미콜론, [유니코드 제어 문자](https://en.wikipedia.org/wiki/Unicode_control_characters)또는 선행 또는 후행 공백이 포함 된 경우 작은따옴표 또는 큰따옴표로 묶어야 합니다. 예를 들어:

```
Keyword=" whitespace  ";
Keyword='special;character';
```

묶는 문자는 포함 하는 값 내에서 발생 하지 않을 수 있습니다. 따라서 작은따옴표를 포함 하는 값은 큰따옴표로만 묶을 수 있으며 그 반대의 경우도 마찬가지입니다.

```
Keyword='double"quotation;mark';
Keyword="single'quotation;mark";
```

두 가지 문자를 함께 사용 하 여 바깥쪽 문자를 이스케이프할 수도 있습니다.

```
Keyword="double""quotation";
Keyword='single''quotation';
```

따옴표 자체와 등호는 이스케이프를 요구 하지 않으므로 다음 연결 문자열을 사용할 수 있습니다.

```
Keyword=no "escaping" 'required';
Keyword=a=b=c
```

각 값은 다음 세미콜론 또는 문자열의 끝까지 읽기 때문에 두 번째 예제의 값은이 `a=b=c`고 마지막 세미콜론은 선택 사항입니다.

모든 연결 문자열은 위에서 설명한 것과 동일한 기본 구문을 공유 합니다. 그러나 인식 되는 키워드 집합은 공급자에 따라 다르며 *ODBC*와 같은 이전 api의 연도 이상으로 발전 했습니다. *.NET Framework* data provider for *SQL Server* (`SqlClient`)는 이전 api의 많은 키워드를 지원 하지만 일반적으로 더 유연 하며 대부분의 일반적인 연결 문자열 키워드에 대 한 동의어를 허용 합니다.

실수를 입력 하면 오류가 발생할 수 있습니다. 예 `Integrated Security=true` 를 들어는 유효 `IntegratedSecurity=true` 하지만 오류가 발생 합니다.

유효성 검사 사용자 입력에서 런타임에 수동으로 생성 된 연결 문자열은 문자열 삽입 공격에 취약 하 고 데이터 원본의 보안을 위협 합니다. 이러한 문제를 해결 하기 위해 *ADO.NET* 2.0에는 각 *.NET Framework* 데이터 공급자에 대 한 [연결 문자열 빌더가](connection-string-builders.md) 도입 되었습니다. 이러한 연결 문자열 작성기는 매개 변수를 강력한 형식의 속성으로 노출 하 고, 연결 문자열을 데이터 원본으로 보내기 전에 유효성을 검사할 수 있도록 합니다.

## <a name="in-this-section"></a>섹션 내용

[연결 문자열 작성기](connection-string-builders.md)\
`ConnectionStringBuilder` 클래스를 사용하여 런타임에 유효한 연결 문자열을 구성하는 방법을 보여 줍니다.

[연결 문자열 및 구성 파일](connection-strings-and-configuration-files.md)\
구성 파일에서 연결 문자열을 저장하고 검색하는 방법을 보여 줍니다.

[연결 문자열 구문](connection-string-syntax.md)\
`SqlClient`, `OracleClient`, `OleDb` 및 `Odbc`에 대한 공급자별 연결 문자열을 구성하는 방법을 설명합니다.

[연결 정보 보호](protecting-connection-information.md)\
데이터 소스 연결에 사용되는 정보를 보호하는 기법을 보여 줍니다.

## <a name="see-also"></a>참고자료

- [데이터 소스에 연결](/cpp/data/odbc/connecting-to-a-data-source)
- [ADO.NET 개요](ado-net-overview.md)
