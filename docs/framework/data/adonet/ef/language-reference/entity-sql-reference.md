---
title: 엔터티 SQL 참조
ms.date: 03/30/2017
ms.assetid: 61ce7ee1-ffe2-477d-8a9f-835b0a11d900
ms.openlocfilehash: 9b666b83674cb2374409e321a2b715e9910bdd0e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62034270"
---
# <a name="entity-sql-reference"></a>엔터티 SQL 참조

이 섹션에서는 Entity SQL 참조 문서를 포함합니다. 이 문서에서는 요약 하 고 Entity SQL 연산자를 범주별으로 그룹화 합니다.

## <a name="arithmetic-operators"></a>산술 연산자

산술 연산자는 하나 이상의 숫자 데이터 형식으로 구성된 두 식에 대해 수치 연산을 수행합니다. 다음 표에서 Entity SQL 산술 연산자를 나열합니다.

|연산자|사용|
|--------------|---------|
|[+(더하기)](add.md)|더하기|
|[/(나누기)](divide-entity-sql.md)|나누기|
|[% (모듈로)](modulo-entity-sql.md)|나누기의 나머지를 반환합니다.|
|[*(곱하기)](multiply-entity-sql.md)|곱하기|
|[-(음수)](negative-entity-sql.md)|부정|
|[-(빼기)](subtract-entity-sql.md)|빼기|

## <a name="canonical-functions"></a>정식 함수

정식 함수는 모든 데이터 공급자에서 지원되며 모든 쿼리 기술에 사용될 수 있습니다. 다음 표에서 정식 함수를 나열합니다.

|함수|형식|
|--------------|----------|
|[집계 Entity SQL 정식 함수](aggregate-canonical-functions.md)|집계 Entity SQL 정식 함수를 설명합니다.|
|[수학 정식 함수](math-canonical-functions.md)|수학 Entity SQL 정식 함수를 설명합니다.|
|[문자열 정식 함수](string-canonical-functions.md)|문자열 Entity SQL 정식 함수를 설명합니다.|
|[날짜 및 시간 정식 함수](date-and-time-canonical-functions.md)|날짜 및 시간 Entity SQL 정식 함수를 설명합니다.|
|[비트 정식 함수](bitwise-canonical-functions.md)|비트 Entity SQL 정식 함수에 설명 합니다.|
|[기타 정식 함수](other-canonical-functions.md)|비트, 날짜/시간, 문자열, 수식, 집계 등으로 분류되지 않는 함수에 대해 설명합니다.|

## <a name="comparison-operators"></a>비교 연산자

비교 연산자는 `Byte`, `Int16`, `Int32`, `Int64`, `Double`, `Single`, `Decimal`, `String`, `DateTime`, `Date`, `Time`, `DateTimeOffset` 형식에 대해 정의됩니다. 비교 연산자를 적용하기 전에 피연산자에 대해 암시적 형식 승격이 발생합니다. 비교 연산자는 항상 부울 값을 생성합니다. 피연산자 중 하나 이상이 `null`이면 결과는 `null`입니다.

`Boolean` 형식과 같이 ID를 가진 모든 개체 형식에 대해 같음 및 다름이 정의됩니다. ID를 가진 기본 개체가 아닌 개체가 같은 ID를 공유할 경우 서로 같다고 간주됩니다. 다음 표에서 Entity SQL 비교 연산자를 나열합니다.

|연산자|설명|
|--------------|-----------------|
|[=(같음)](equals-entity-sql.md)|두 식이 같은지 비교합니다.|
|[>(보다 큼)](greater-than-entity-sql.md)|두 식을 비교하여 왼쪽 식의 값이 오른쪽 식의 값보다 큰지 여부를 결정합니다.|
|[>=(크거나 같음)](greater-than-or-equal-to-entity-sql.md)|두 식을 비교하여 왼쪽 식의 값이 오른쪽 식의 값보다 크거나 같은지 여부를 결정합니다.|
|[됩니다 \[되지\] NULL](isnull-entity-sql.md)|쿼리 식이 null인지 여부를 결정합니다.|
|[<(보다 작음)](less-than-entity-sql.md)|두 식을 비교하여 왼쪽 식의 값이 오른쪽 식의 값보다 작은지 여부를 결정합니다.|
|[<=(작거나 같음)](less-than-or-equal-to-entity-sql.md)|두 식을 비교하여 왼쪽 식의 값이 오른쪽 식의 값보다 작거나 같은지 여부를 결정합니다.|
|[\[NOT\] BETWEEN](between-entity-sql.md)|식의 결과 값이 지정된 범위에 속하는지 여부를 결정합니다.|
|[\!= (같지 않음)](not-equal-to-entity-sql.md)|두 식을 비교 하 여 왼쪽된 식이 오른쪽 식과 같지 않습니다 여부를 결정 합니다.|
|[\[NOT\] LIKE](like-entity-sql.md)|특정 문자열이 지정된 패턴과 일치하는지 여부를 결정합니다.|

## <a name="logical-and-case-expression-operators"></a>논리 및 case 식 연산자

논리 연산자는 조건의 진위 여부를 테스트합니다. CASE 식은 부울 식 집합을 계산하여 결과를 결정합니다. 다음 표에서 논리 및 CASE 식 연산자를 나열합니다.

|연산자|설명|
|--------------|-----------------|
|[& & (논리적 AND)](and-entity-sql.md)|논리적 AND|
|[\! (논리적 NOT)](not-entity-sql.md)|논리적 NOT|
|[&#124;&#124;(논리적 OR)](or-entity-sql.md)|논리적 OR|
|[CASE](case-entity-sql.md)|부울 식 집합을 계산하여 결과를 확인합니다.|
|[THEN](then-entity-sql.md)|결과 [때](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb387119(v=vs.100)) 절 true로 평가 될 때입니다.|

## <a name="query-operators"></a>쿼리 연산자

쿼리 연산자는 엔터티 데이터를 반환하는 쿼리 식을 정의하는 데 사용됩니다. 다음 표에서 쿼리 연산자를 나열합니다.

|연산자|사용|
|--------------|---------|
|[FROM](from-entity-sql.md)|에 사용 되는 컬렉션을 지정 [선택](select-entity-sql.md) 문입니다.|
|[GROUP BY](group-by-entity-sql.md)|쿼리에 의해 반환 된 개체 그룹을 지정 합니다 ([선택](select-entity-sql.md)) 식 배치 됩니다.|
|[GroupPartition](grouppartition-entity-sql.md)|집계가 관련되는 그룹 파티션에서 예측된 인수 값의 컬렉션을 반환합니다.|
|[HAVING](having-entity-sql.md)|그룹이나 집계에 대한 검색 조건을 지정합니다.|
|[LIMIT](limit-entity-sql.md)|사용 된 [ORDER BY](order-by-entity-sql.md) 수행된 된 물리적 페이징 절.|
|[ORDER BY](order-by-entity-sql.md)|반환 되는 개체에 사용 되는 정렬 순서를 지정 된 [선택](select-entity-sql.md) 문입니다.|
|[SELECT](select-entity-sql.md)|쿼리 결과로 반환되는 프로젝션의 요소를 지정합니다.|
|[SKIP](skip-entity-sql.md)|사용 된 [ORDER BY](order-by-entity-sql.md) 수행된 된 물리적 페이징 절.|
|[TOP](top-entity-sql.md)|쿼리 결과에서 첫 번째 행 집합만 반환됨을 지정합니다.|
|[WHERE](where-entity-sql.md)|쿼리에서 반환된 데이터를 조건에 따라 필터링합니다.|

## <a name="reference-operators"></a>참조 연산자

참조는 특정 엔터티 집합 내의 특정 엔터티를 가리키는 논리 포인터(외래 키)입니다. Entity SQL 생성, 해체 및 참조를 탐색 하려면 다음 연산자를 지원 합니다.

|연산자|사용|
|--------------|---------|
|[CREATEREF](createref-entity-sql.md)|엔터티 집합의 엔터티에 대한 참조를 만듭니다.|
|[DEREF](deref-entity-sql.md)|참조 값을 역참조하고 이 역참조의 결과를 생성합니다.|
|[KEY](key-entity-sql.md)|참조 또는 엔터티 식의 키를 추출합니다.|
|[NAVIGATE](navigate-entity-sql.md)|엔터티 형식 간의 관계를 탐색할 수 있습니다.|
|[REF](ref-entity-sql.md)|엔터티 인스턴스에 대한 참조를 반환합니다.|

## <a name="set-operators"></a>집합 연산자

Entity SQL에는 다양 한 강력한 집합 연산을 제공합니다. 여기에 UNION, INTERSECT, EXCEPT, 같은 TRANSACT-SQL 연산자와 유사한 집합 연산자 및 EXISTS입니다. 또한 entity SQL 중복 항목 제거 (SET), 멤버 자격 테스트 (IN) 및 조인 (JOIN)에 대 한 연산자를 지원 합니다. 다음 표에서 Entity SQL 집합 연산자를 나열합니다.

|연산자|사용|
|--------------|---------|
|[ANYELEMENT](anyelement-entity-sql.md)|다중값 컬렉션에서 요소를 추출합니다.|
|[EXCEPT](except-entity-sql.md)|쿼리 식에서 EXCEPT 피연산자 오른쪽 쿼리 식에서 반환 되지 않습니다는 EXCEPT 연산자의 왼쪽에 고유한 값의 컬렉션을 반환 합니다.|
|[\[NOT\] EXISTS](exists-entity-sql.md)|컬렉션이 비어 있는지 확인합니다.|
|[FLATTEN](flatten-entity-sql.md)|여러 컬렉션의 컬렉션을 하나의 결합된 컬렉션으로 변환합니다.|
|[\[NOT\] IN](in-entity-sql.md)|컬렉션에 일치하는 값이 있는지 여부를 확인합니다.|
|[INTERSECT](intersect-entity-sql.md)|INTERSECT 피연산자의 왼쪽과 오른쪽에 있는 두 쿼리 식에서 반환된 고유한 값의 컬렉션을 반환합니다.|
|[OVERLAPS](overlaps-entity-sql.md)|두 컬렉션에 공통 요소가 있는지 여부를 확인합니다.|
|[SET](set-entity-sql.md)|중복 요소가 모두 제거된 새 컬렉션을 생성하여 개체 컬렉션을 집합으로 변환하는 데 사용됩니다.|
|[UNION](union-entity-sql.md)|두 개 이상의 쿼리 결과를 단일 컬렉션으로 결합합니다.|

## <a name="type-operators"></a>형식 연산자

Entity SQL 식 (값)을 생성, 쿼리 및 조작의 유형을 허용 하는 작업을 제공 합니다. 다음 표에서 형식을 사용 하는 데 사용 되는 연산자를 나열 합니다.

|연산자|사용|
|--------------|---------|
|[CAST](cast-entity-sql.md)|데이터 형식의 식을 다른 형식의 식으로 변환합니다.|
|[COLLECTION](collection-entity-sql.md)|에 사용 된 [함수](function-entity-sql.md) 엔터티 형식 또는 복합 형식의 컬렉션을 선언 하는 작업.|
|[IS \[NOT\] OF](isof-entity-sql.md)|식의 형식이 지정된 형식 또는 그 하위 형식인지 여부를 확인합니다.|
|[OFTYPE](oftype-entity-sql.md)|쿼리 식에서 특정 형식을 가진 개체 컬렉션을 반환합니다.|
|[명명된 형식 생성자](named-type-constructor-entity-sql.md)|엔터티 형식이나 복합 형식의 인스턴스를 만드는 데 사용됩니다.|
|[MULTISET](multiset-entity-sql.md)|값 목록에서 multiset 인스턴스를 만듭니다.|
|[ROW](row-entity-sql.md)|값 하나 이상을 기반으로 하여 구조적으로 형식화된 익명 레코드를 생성합니다.|
|[TREAT](treat-entity-sql.md)|특정 기본 형식의 개체를 지정된 파생 형식의 개체로 처리합니다.|

## <a name="other-operators"></a>기타 연산자

다음 표에서 다른 Entity SQL 연산자를 나열합니다.

|연산자|사용|
|--------------|---------|
|[+(문자열 연결)](string-concatenation-entity-sql.md)|Entity SQL에서 문자열을 연결 하는 데 사용 합니다.|
|[. (멤버 액세스)](member-access-entity-sql.md)|구조 개념적 모델 형식 인스턴스의 속성 또는 필드 값에 액세스하는 데 사용됩니다.|
|[--(설명)](comment-entity-sql.md)|Entity SQL 주석을 포함 합니다.|
|[FUNCTION](function-entity-sql.md)|Entity SQL 쿼리에서 실행할 수 있는 인라인 함수를 정의합니다.|

## <a name="see-also"></a>참고자료

- [Entity SQL 언어](entity-sql-language.md)
