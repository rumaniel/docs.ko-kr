---
title: 명령 트리에서 SQL 생성 - 최선의 방법
ms.date: 03/30/2017
ms.assetid: 71ef6a24-4c4f-4254-af3a-ffc0d855b0a8
ms.openlocfilehash: 9859c7df941ae6681c991001e0d1e5a50c7ffc60
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855008"
---
# <a name="generating-sql-from-command-trees---best-practices"></a>명령 트리에서 SQL 생성 - 최선의 방법

출력 쿼리 명령 트리는 SQL로 표현 가능한 쿼리를 유사하게 모델링합니다. 그러나 출력 명령 트리에서 SQL을 생성할 때 공급자 작성기에 대한 특정한 공통적 문제가 있습니다. 이 항목에서는 이러한 문제에 대해 설명하며, 그 다음 항목에서는 동일한 공급자가 이러한 문제를 처리하는 방법을 보여 줍니다.

## <a name="group-dbexpression-nodes-in-a-sql-select-statement"></a>SQL SELECT 문에서 DbExpression 노드 그룹화

일반적인 SQL 문에는 다음과 같은 모양의 중첩 구조가 있습니다.

```sql
SELECT …
FROM …
WHERE …
GROUP BY …
ORDER BY …
```

하나 이상의 절이 비어 있을 수 있습니다.  중첩된 SELECT 문은 어떤 줄에서든 발생할 수 있습니다.

쿼리 명령 트리를 SQL SELECT 문으로 변환하는 경우 관계형 연산자마다 하위 쿼리가 하나씩 생성됩니다. 그러나 이 경우 읽기 어려운 불필요한 중첩 하위 쿼리가 생성되며,  일부 데이터 저장소에서는 쿼리 성능이 저하될 수 있습니다.

예를 들어, 다음과 같은 쿼리 명령 트리를 살펴보겠습니다.

```
Project (
a.x,
   a = Filter(
      b.y = 5,
      b = Scan("TableA")
   )
)
```

비효율적인 변환에서는 다음을 생성합니다.

```sql
SELECT a.x
FROM (   SELECT *
         FROM TableA as b
         WHERE b.y = 5) as a
```

모든 관계식 노드가 새로운 SQL SELECT 문이 됩니다.

따라서 정확성을 유지하면서 가능한 한 많은 식 노드를 단일 SQL SELECT 문에 집계해야 합니다.

위의 예제에 대한 이러한 집계의 결과는 다음과 같습니다.

```sql
SELECT b.x
FROM TableA as b
WHERE b.y = 5
```

## <a name="flatten-joins-in-a-sql-select-statement"></a>SQL SELECT 문에서 조인 평면화

여러 노드를 단일 SQL SELECT 문에 집계하는 예로 여러 조인 식을 단일 SQL SELECT 문에 집계하는 경우를 들 수 있습니다. DbJoinExpression은 두 입력 간의 단일 조인을 나타냅니다. 그러나 단일 SQL SELECT 문의 일부로 둘 이상의 조인을 지정할 수 있습니다. 이 경우 지정된 순서대로 조인이 수행됩니다.

왼쪽 편 조인(다른 조인의 왼쪽 자식으로 나타나는 조인)은 단일 SQL SELECT 문으로 보다 쉽게 평면화할 수 있습니다. 예를 들어, 다음과 같은 쿼리 명령 트리를 살펴보겠습니다.

```
InnerJoin(
   a = LeftOuterJoin(
   b = Extent("TableA")
   c = Extent("TableB")
   ON b.y = c.x ),
   d = Extent("TableC")
   ON a.b.y = d.z
)
```

이 트리는 다음으로 올바르게 변환될 수 있습니다.

```sql
SELECT *
FROM TableA as b
LEFT OUTER JOIN TableB as c ON b.y = c.x
INNER JOIN TableC as d ON b.y = d.z
```

그러나 왼쪽 편 조인이 아닌 조인은 쉽게 평면화할 수 없으므로 평면화하려고 하면 안 됩니다. 다음 쿼리 명령 트리의 조인을 예로 들 수 있습니다.

```
InnerJoin(
   a = Extent("TableA")
   b = LeftOuterJoin(
   c = Extent("TableB")
   d = Extent("TableC")
   ON c.y = d.x),
   ON a.z = b.c.y
)
```

이 조인은 하위 쿼리가 포함된 SQL SELECT 문으로 변환됩니다.

```sql
SELECT *
FROM TableA as a
INNER JOIN (SELECT *
   FROM TableB as c
   LEFT OUTER JOIN TableC as d
   ON c.y = d.x) as b
ON b.y = d.z
```

## <a name="input-alias-redirecting"></a>입력 별칭 리디렉션

입력 별칭 리디렉션을 설명하기 위해 DbFilterExpression, DbProjectExpression, DbCrossJoinExpression, DbJoinExpression, DbSortExpression, DbGroupByExpression, DbApplyExpression 및 DbSkipExpression과 같은 관계식의 구조를 살펴보겠습니다.

이러한 각 형식에는 입력 컬렉션을 설명하는 하나 이상의 입력 속성이 있으며, 각 입력에 해당하는 바인딩 변수는 컬렉션 순회 중에 해당 입력의 각 요소를 나타내는 데 사용됩니다. 바인딩 변수는 DbFilterExpression의 조건자 속성이나 DbProjectExpression의 Projection 속성 등에서 입력 요소를 참조할 때 사용됩니다.

더 많은 관계식 노드를 단일 SQL SELECT 문에 집계하고 관계식의 일부(예: DbProjectExpression의 Projection 속성 일부)인 식을 계산하는 경우 여러 식 바인딩이 단일 익스텐트로 리디렉션되어야 하므로 사용하는 바인딩 변수는 입력의 별칭과 동일하지 않을 수 있습니다.  이 문제를 별칭 이름 바꾸기라고 합니다.

이 항목의 첫 번째 예제를 살펴보겠습니다. 기본 변환을 수행하고 Projection a.x (DbPropertyExpression(a, x))를 변환하는 경우 입력의 별칭을 바인딩 변수와 일치하도록 "a"로 지정했으므로 `a.x`로 변환하는 것이 올바릅니다.  그러나 두 노드를 단일 SQL SELECT 문에 집계하는 경우에는 입력의 별칭이 "b"로 지정되었으므로 동일한 DbPropertyExpression을 `b.x`로 변환해야 합니다.

## <a name="join-alias-flattening"></a>조인 별칭 평면화

출력 명령 트리의 다른 모든 관계식과 달리 DbJoinExpression은 각각 입력 중 하나에 해당하는 두 열로 구성된 행인 결과 형식을 출력합니다. DbPropertyExpression을 작성 하 여 조인에서 시작 된 스칼라 속성에 액세스 하는 경우에는 다른 DbPropertyExpression을 사용 합니다.

예로 예제 2의 "a.b.y"와 예제 3의 "b.c.y"를 들 수 있습니다. 그러나 해당 SQL 문에서 이들은 "b.y"로 참조됩니다. 이렇게 별칭이 다시 지정되는 것을 조인 별칭 평면화라고 합니다.

## <a name="column-name-and-extent-alias-renaming"></a>열 이름 및 익스텐트 별칭 이름 바꾸기

조인이 있는 SQL SELECT 쿼리가 프로젝션을 사용하여 완료되어야 하는 경우 입력에서 참여하는 열을 모두 열거하면 둘 이상의 입력에 동일한 열 이름이 있을 수 있으므로 이름 충돌이 발생할 수 있습니다. 충돌을 방지하려면 열에 서로 다른 이름을 사용합니다.

또한 조인을 평면화할 때 참여하는 테이블(또는 하위 쿼리)에 충돌하는 별칭이 있을 수 있습니다. 이 경우 충돌하는 별칭의 이름을 바꿔야 합니다.

## <a name="avoid-select-"></a>SELECT * 사용 금지

기본 테이블에서 선택하기 위해 `SELECT *`를 사용하지 마세요. Entity Framework 응용 프로그램의 저장소 모델에는 데이터베이스 테이블에 있는 열의 하위 집합만 포함 될 수 있습니다. 이 경우 `SELECT *`는 잘못된 결과를 생성할 수 있습니다. 대신, 참여하는 식의 결과 형식에서 열 이름을 사용하여 참여하는 모든 열을 지정해야 합니다.

## <a name="reuse-of-expressions"></a>식의 재사용

식은 Entity Framework 전달 된 쿼리 명령 트리에서 재사용할 수 있습니다. 각 식이 쿼리 명령 트리에서 한 번만 나타난다고 가정하지 마십시오.

## <a name="mapping-primitive-types"></a>기본 형식 매핑

개념적(EDM) 형식을 공급자 형식에 매핑하는 경우 가능한 모든 값이 들어가도록 가장 넓은 형식(Int32)에 매핑해야 합니다. 또한 BLOB 형식과 같은 많은 작업에 사용할 수 없는 형식 (예: `ntext` SQL Server)에는 매핑되지 않습니다.

## <a name="see-also"></a>참고자료

- [SQL 생성](sql-generation.md)
