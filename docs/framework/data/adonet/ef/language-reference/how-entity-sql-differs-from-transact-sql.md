---
title: Entity SQL과 Transact-SQL의 차이점
ms.date: 03/30/2017
ms.assetid: 9c9ee36d-f294-4c8b-a196-f0114c94f559
ms.openlocfilehash: e0af0a415d812337d6abf449e9ee170526c3df0c
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833717"
---
# <a name="how-entity-sql-differs-from-transact-sql"></a>Entity SQL과 Transact-SQL의 차이점
이 항목에서는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 와 transact-sql의 차이점에 대해 설명 합니다.  
  
## <a name="inheritance-and-relationships-support"></a>상속 및 관계 지원  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]은 개념적 엔터티 스키마를 직접 다루며 상속 및 관계와 같은 개념적 모델 기능을 지원합니다.  
  
 상속 작업을 할 때 상위 형식 인스턴스 컬렉션에서 하위 형식의 인스턴스를 선택하는 것이 유용할 때가 많습니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]의 [oftype](oftype-entity-sql.md) 연산자 (C#시퀀스의 `oftype`와 유사)는이 기능을 제공합니다.  
  
## <a name="support-for-collections"></a>컬렉션 지원  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 컬렉션을 고급 엔터티로 취급합니다. 예를 들어:  
  
- 컬렉션 식은 `from` 절에서 유효합니다.  
  
- 하위 쿼리 `in` 및 `exists`는 모든 컬렉션을 허용하도록 일반화되었습니다.  
  
     하위 쿼리는 일종의 컬렉션입니다. `e1 in e2` 및 `exists(e)`는 이러한 작업을 수행하는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 구문입니다.  
  
- 컬렉션에 대해 `union`, `intersect`, `except` 등의 Set 작업이 수행됩니다.  
  
- 컬렉션에 조인이 수행됩니다.  
  
## <a name="support-for-expressions"></a>식 지원  
 Transact-sql에는 하위 쿼리 (테이블)와 식 (행 및 열)이 있습니다.  
  
 컬렉션 및 중첩 컬렉션을 지원 하기 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 위해에서는 모든 것을 식으로 만듭니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]Transact-sql 보다 더 쉽게 구성할 수 있습니다. 모든 식은 어디에서 나 사용할 수 있습니다. 쿼리 식은 항상 프로젝션된 형식의 컬렉션을 생성하며, 컬렉션 식이 허용된 곳이라면 어디서든 쿼리 식을 사용할 수 있습니다. 에서 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]지원 되지 않는 transact-sql 식에 대 한 자세한 내용은 [지원 되지 않는 식](unsupported-expressions-entity-sql.md)을 참조 하세요.  
  
 다음은 모두 유효한 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 쿼리입니다.  
  
```sql  
1+2 *3  
"abc"  
row(1 as a, 2 as b)  
{ 1, 3, 5}   
e1 union all e2  
set(e1)  
```  
  
## <a name="uniform-treatment-of-subqueries"></a>일관된 하위 쿼리 처리  
 테이블에 중점을 두어 Transact-sql은 하위 쿼리의 컨텍스트 해석을 수행 합니다. 예를 들어, `from` 절의 하위 쿼리는 multiset(테이블)로 간주됩니다. 하지만 동일한 하위 쿼리가 `select` 절에서 사용되면 스칼라 하위 쿼리로 간주됩니다. 마찬가지로 `in` 연산자의 좌 변에 사용 되는 하위 쿼리는 스칼라 하위 쿼리로 간주 되 고 오른쪽은 multiset 하위 쿼리로 간주 됩니다.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 이러한 구별이 없습니다. 식은 사용되는 컨텍스트와 관계없이 일관성 있게 해석되며 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]모든 하위 쿼리를 multiset 하위 쿼리로 간주 합니다. 하위 쿼리에서 스칼라 값이 필요한 경우, [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 컬렉션(여기서는 하위 쿼리)에 대해 작동하는 `anyelement` 연산자를 제공하여 컬렉션으로부터 singleton 값을 추출합니다.  
  
### <a name="avoiding-implicit-coercions-for-subqueries"></a>하위 쿼리에 대한 암시적 강제 변환 방지  
 일관된 하위 쿼리 처리의 부작용 중 하나는 하위 쿼리를 스칼라 값으로 암시적으로 변환하는 것입니다. 특히 Transact-sql에서 단일 필드를 사용 하 여 행의 multiset은 해당 데이터 형식이 필드의 스칼라 값으로 암시적으로 변환 됩니다.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 이러한 암시적 강제 변환이 지원되지 않습니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 컬렉션에서 singleton 값을 추출하도록 ANYELEMENT 연산자를 제공하며, 쿼리 식을 실행하는 중 행 래퍼가 생성되지 않도록 `select value` 절을 제공합니다.  
  
## <a name="select-value-avoiding-the-implicit-row-wrapper"></a>Select Value: 암시적 행 래퍼 방지  
 Transact-sql 하위 쿼리의 select 절은 절의 항목 주위에 행 래퍼를 암시적으로 만듭니다. 이는 스칼라 또는 개체의 컬렉션을 만들 수 없음을 의미합니다. Transact-sql을 사용 하면 하나의 필드가 있는 rowtype와 데이터 형식이 동일한 singleton 값 사이에 암시적 강제 변환을 수행할 수 있습니다.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 암시적 행 생성을 건너뛰도록 `select value` 절을 제공합니다. `select value` 절 하나에는 항목 하나만 지정할 수 있습니다. 이 절을 사용하면 `select` 절의 항목 주위에 행 래퍼가 생성되지 않으며, `select value a`와 같이 원하는 모양의 컬렉션이 만들어질 수 있습니다.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 임의의 행을 만드는 행 생성자도 제공합니다. `select`는 다음과 같이 프로젝션의 요소를 하나 이상 가지며 필드가 있는 데이터 레코드를 생성합니다.  
  
 `select a, b, c`  
  
## <a name="left-correlation-and-aliasing"></a>왼쪽 상관 관계 및 별칭 지정  
 Transact-sql에서 지정 된 범위의 식 (또는 `select` `from`와 같은 단일 절)은 같은 범위에서 이전에 정의 된 식을 참조할 수 없습니다. Sql (transact-sql 포함)의 일부 언어는 `from` 절에서 제한 된 형식을 지원 합니다.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 왼쪽 상관 관계를 `from` 절에 일반화하여 일관성 있게 처리합니다. `from` 절의 식은 추가 구문을 사용할 필요 없이 동일한 절의 이전 정의(왼쪽 정의)를 참조할 수 있습니다.  
  
 또한 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 `group by` 절을 사용하는 쿼리에 추가적인 제한을 적용합니다. 이러한 쿼리에서 `select` 절 및 `having` 절의 식은 오직 별칭을 통해서만 `group by` 키를 참조할 수 있습니다. 다음 구문은 Transact-sql에서는 유효 하지만에서는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]유효 하지 않습니다.  
  
```sql  
SELECT t.x + t.y FROM T AS t group BY t.x + t.y
```  
  
 위와 동일한 결과를 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서 얻으려면 다음 구문을 사용합니다.  
  
```sql  
SELET k FROM T AS t GROUP BY (t.x + t.y) AS k
```  
  
## <a name="referencing-columns-properties-of-tables-collections"></a>테이블(컬렉션)의 열(속성) 참조  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]의 모든 열 참조는 테이블 별칭으로 정규화해야 합니다. 다음 구문 (테이블 `a` `T`의 유효한 열 이라고 가정)은 transact-sql에서는 유효 하지만에서는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]유효 하지 않습니다.  
  
```sql  
SELECT a FROM T
```  
  
 위 구문의 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 형식은 다음과 같습니다.  
  
```sql  
SELECT t.a AS A FROM T AS t
```  
  
 `from` 절에서 테이블 별칭은 선택적 요소입니다. 테이블의 이름이 암시적 별칭으로 사용됩니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 다음 형식도 허용됩니다.  
  
```sql  
SELET Tab.a FROM Tab
```  
  
## <a name="navigation-through-objects"></a>개체 탐색  
 Transact-sql은 테이블의 (행)의 열을 참조 하는 데 "." 표기법을 사용 합니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 프로그래밍 언어에서 차용한 이 표기를 확장하여 개체의 속성 탐색을 지원합니다.  
  
 예를 들어, `p`가 Person 형식의 식이라면 다음은 이 사람의 주소 중 도시를 참조하는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 구문입니다.  
  
```sql  
p.Address.City   
```  
  
## <a name="no-support-for-"></a>*를 지원하지 않음  
 Transact-sql은 정규화 되지 않은 * 구문을 전체 행의 별칭으로 지원 하 고 해당 테이블의 필드 \* 에 대 한 바로\*가기로 정규화 된 구문 (t.)을 지원 합니다. 또한 transact-sql은 null을 포함 하는 특수 count (\*) 집계를 허용 합니다.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 * 구문을 지원하지 않습니다. 및 `select * from T` [!INCLUDE[esql](../../../../../../includes/esql-md.md)] `select value t from T as t` 형식의 transact-sql 쿼리는 각각 및`select value t1 from T1 as t1, T2 as t2...`로 표현할 수 있습니다. `select T1.* from T1, T2...` 또한 이러한 구문은 상속(값 대체성)을 처리하지만, `select *` 변형은 선언된 형식의 최상위 속성으로 제한됩니다.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 `count(*)` 집계를 지원하지 않습니다. 대신 `count(0)`를 사용하세요.  
  
## <a name="changes-to-group-by"></a>Group By 변경  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 `group by` 키 별칭 지정을 지원합니다. `select` 절 및 `having` 절의식은이러한별칭`group by` 을 통해 키를 참조 해야 합니다. 예를 들어, 다음 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 구문을 봅니다.  
  
```sql  
SELECT k1, count(t.a), sum(t.a)
FROM T AS t
GROUP BY t.b + t.c AS k1
```  
  
 ... 는 다음 Transact-sql과 동일 합니다.  
  
```sql  
SELECT b + c, count(*), sum(a)
FROM T
GROUP BY b + c
```  
  
## <a name="collection-based-aggregates"></a>컬렉션 기반 집계  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 두 가지 종류의 집계를 지원합니다.  
  
 컬렉션 기반 집계는 컬렉션에 대해 작동하며 집계된 결과를 생성합니다. 이는 쿼리 내의 임의의 위치에 나타날 수 있으며 `group by` 절이 필요 없습니다. 예:  
  
```sql  
SELECT t.a AS a, count({1,2,3}) AS b FROM T AS t
```  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 SQL 스타일의 집계도 지원됩니다. 예를 들어:  
  
```sql  
SELECT a, sum(t.b) FROM T AS t GROUP BY t.a AS a
```  
  
## <a name="order-by-clause-usage"></a>ORDER BY 절 사용법  
Transact-sql을 사용 하면 `ORDER BY` 절을 최상위 `SELECT .. FROM .. WHERE` 블록 에서만 지정할 수 있습니다. @No__t-0에서는 중첩 된 `ORDER BY` 식을 사용할 수 있으며, 쿼리의 아무 곳에 나 배치할 수 있지만 중첩 된 쿼리의 순서 지정은 유지 되지 않습니다.  
  
```sql  
-- The following query will order the results by the last name  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact AS C1
        ORDER BY C1.LastName  
```  
  
```sql  
-- In the following query ordering of the nested query is ignored.  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
## <a name="identifiers"></a>식별자  
 Transact-sql에서 식별자 비교는 현재 데이터베이스의 데이터 정렬을 기반으로 합니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서 식별자는 항상 대/소문자를 구분하지 않고 악센트를 구분합니다. 즉, [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 악센트 부호가 있는 문자와 악센트 부호가 없는 문자를 구분합니다. 예를 들어 'a'는 'ấ'와 같지 않습니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 나타나는 모양은 같지만 서로 다른 코드 페이지에서 가져온 문자 버전을 다른 문자로 처리합니다. 자세한 내용은 [입력 문자 집합](input-character-set-entity-sql.md)을 참조 하세요.  
  
## <a name="transact-sql-functionality-not-available-in-entity-sql"></a>Entity SQL에서 사용할 수 없는 Transact-SQL 기능  
 다음 Transact-sql 기능은에서 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]사용할 수 없습니다.  
  
 DML  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 현재 DML 문(insert, update, delete)을 지원하지 않습니다.  
  
 DDL  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]의 현재 버전에서는 DDL을 지원하지 않습니다.  
  
 명령형 프로그래밍 비교  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]Transact-sql과 달리 명령적 프로그래밍에 대 한 지원을 제공 하지 않습니다. 대신 프로그래밍 언어를 사용합니다.  
  
 그룹화 함수  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 아직 CUBE, ROLLUP 및 GROUPING_SET와 같은 그룹화 함수가 지원되지 않습니다.  
  
 분석 함수  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 아직 분석 함수가 지원되지 않습니다.  
  
 기본 제공 함수, 연산자  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 Transact-sql의 기본 제공 함수 및 연산자의 하위 집합을 지원 합니다. 이러한 연산자와 함수는 주요 저장소 공급자에서 주로 지원합니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 공급자 매니페스트에 선언된 저장소별 함수를 사용합니다. 또한 Entity Framework를 사용 하 여에 대해 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 기본 제공 및 사용자 정의 기존 저장소 함수를 선언할 수 있습니다.  
  
 참고  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 쿼리 참고의 메커니즘을 제공하지 않습니다.  
  
 쿼리 결과 일괄 처리  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 쿼리 결과 일괄 처리를 지원하지 않습니다. 예를 들어 다음은 유효한 Transact-sql (일괄 처리로 보내기)입니다.  
  
```sql  
SELECT * FROM products;
SELECT * FROM catagories;
```  
  
 그러나 해당하는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]은 지원되지 않습니다.  
  
```sql  
SELECT value p FROM Products AS p;
SELECT value c FROM Categories AS c;
```  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 결과 생성 쿼리 문을 명령당 하나만 지원합니다.  
  
## <a name="see-also"></a>참고자료

- [Entity SQL 개요](entity-sql-overview.md)
- [지원되지 않는 식](unsupported-expressions-entity-sql.md)
