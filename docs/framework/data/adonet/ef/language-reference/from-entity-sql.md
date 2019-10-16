---
title: FROM(Entity SQL)
ms.date: 03/30/2017
ms.assetid: ff3e3048-0d5d-4502-ae5c-9187fcbd0514
ms.openlocfilehash: 2334a30009d6bef9544d2ca1e0ab923a7441d6f2
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833827"
---
# <a name="from-entity-sql"></a>FROM(Entity SQL)
[SELECT](select-entity-sql.md) 문에 사용 되는 컬렉션을 지정 합니다.

## <a name="syntax"></a>구문

```sql
FROM expression [ ,...n ] AS C
```

## <a name="arguments"></a>인수

`expression` \
`SELECT` 문에서 소스로 사용할 컬렉션을 생성하는 모든 유효한 쿼리 식입니다.

## <a name="remarks"></a>설명

`FROM` 절은 하나 이상의 `FROM` 절 항목이 쉼표로 구분된 목록입니다. `FROM` 절을 사용하여 `SELECT` 문의 소스를 하나 이상 지정할 수 있습니다. 가장 단순한 형태의 `FROM` 절은 다음 예제와 같이 `SELECT` 문에서 소스로 사용되는 컬렉션 및 별칭을 식별하는 단일 쿼리 식입니다.

`FROM C as c`

## <a name="from-clause-items"></a>FROM 절 항목

각 `FROM` 절 항목은 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 쿼리의 소스 컬렉션을 참조합니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 단순 `FROM` 절 항목, `FROM` 절 항목 및 `JOIN FROM` 절 항목과 같은 `APPLY FROM` 절 항목의 클래스를 지원합니다. 각 `FROM` 절 항목에 대해서는 다음 단원에서 자세히 설명합니다.

### <a name="simple-from-clause-item"></a>단순 FROM 절 항목

가장 단순한 `FROM` 절 항목은 컬렉션 및 별칭을 식별하는 단일 식입니다. 식은 단순히 엔터티 집합이거나 하위 쿼리 또는 컬렉션 형식인 다른 모든 식일 수 있습니다. 예를 들면 다음과 같습니다.

```sql
LOB.Customers as c
```

별칭 지정은 선택 사항입니다. 위에서 설명한 FROM 절 항목의 대체 지정은 다음과 같을 수 있습니다.

```sql
LOB.Customers
```

별칭이 지정되지 않은 경우 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 컬렉션 식을 기반으로 별칭을 생성합니다.

### <a name="join-from-clause-item"></a>JOIN FROM 절 항목

`JOIN FROM` 절 항목은 두 `FROM` 절 항목 간의 조인을 나타냅니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 Cross Join, Inner Join, Left Outer Join, Right Outer Join 및 Full Outer Join을 지원합니다. 이러한 모든 조인은 Transact-sql에서 지원 되는 방식과 유사 하 게 지원 됩니다. Transact-sql에서와 같이 `JOIN`과 관련 된 두 개의 `FROM` 절 항목은 독립적 이어야 합니다. 즉, 상호 관련될 수 없습니다. 이러한 경우 `CROSS APPLY` 또는 `OUTER APPLY`를 사용할 수 있습니다.

#### <a name="cross-joins"></a>Cross Join

`CROSS JOIN` 쿼리 식에서는 다음 예제와 같이 두 컬렉션의 Cartesian 곱을 생성합니다.

`FROM C AS c CROSS JOIN D as d`

#### <a name="inner-joins"></a>Inner Join

`INNER JOIN`에서는 다음 예제와 같이 두 컬렉션의 제한된 Cartesian 곱을 생성합니다.

`FROM C AS c [INNER] JOIN D AS d ON e`

위의 쿼리 식에서는 `ON` 조건이 true인 오른쪽 컬렉션의 모든 요소와 왼쪽 컬렉션의 모든 요소 쌍으로 이루어진 조합을 처리합니다. `ON` 조건이 지정되지 않은 경우 `INNER JOIN`은 `CROSS JOIN`이 됩니다.

#### <a name="left-outer-joins-and-right-outer-joins"></a>Left Outer Join 및 Right Outer Join

`OUTER JOIN` 쿼리 식에서는 다음 예제와 같이 두 컬렉션의 제한된 Cartesian 곱을 생성합니다.

`FROM C AS c LEFT OUTER JOIN D AS d ON e`

위의 쿼리 식에서는 `ON` 조건이 true인 오른쪽 컬렉션의 모든 요소와 왼쪽 컬렉션의 모든 요소 쌍으로 이루어진 조합을 처리합니다. `ON` 조건이 false이면 식에서 값이 Null인 오른쪽 요소와 쌍을 이루는 왼쪽 요소의 단일 인스턴스를 처리합니다.

`RIGHT OUTER JOIN`은 유사한 방식으로 표현할 수 있습니다.

#### <a name="full-outer-joins"></a>Full Outer Join

명시적 `FULL OUTER JOIN`에서는 다음 예제와 같이 두 컬렉션의 제한된 Cartesian 곱을 생성합니다.

`FROM C AS c FULL OUTER JOIN D AS d ON e`

위의 쿼리 식에서는 `ON` 조건이 true인 오른쪽 컬렉션의 모든 요소와 왼쪽 컬렉션의 모든 요소 쌍으로 이루어진 조합을 처리합니다. `ON` 조건이 false이면 식에서 값이 Null인 오른쪽 요소와 쌍을 이루는 왼쪽 요소의 단일 인스턴스를 처리합니다. 또한 값이 Null인 왼쪽 요소와 쌍을 이루는 오른쪽 요소의 단일 인스턴스를 처리합니다.

> [!NOTE]
> Transact-sql에서 SQL-92과의 호환성을 유지 하기 위해 외부 키워드는 선택 사항입니다. 따라서 `LEFT JOIN`, `RIGHT JOIN` 및 `FULL JOIN`은 `LEFT OUTER JOIN`, `RIGHT OUTER JOIN` 및 `FULL OUTER JOIN`과 같습니다.

### <a name="apply-clause-item"></a>APPLY 절 항목

[!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 두 가지 종류의 `APPLY`인 `CROSS APPLY`와 `OUTER APPLY`를 지원합니다.

`CROSS APPLY`에서는 오른쪽 요소를 계산하여 구한 컬렉션 요소와 왼쪽 컬렉션의 각 요소로 이루어진 고유한 쌍을 생성합니다. `CROSS APPLY`를 사용하면 다음의 연관된 컬렉션 예제와 같이 오른쪽 식의 기능이 왼쪽의 요소에 종속됩니다.

`SELECT c, f FROM C AS c CROSS APPLY c.Assoc AS f`

`CROSS APPLY`의 동작은 조인 목록과 유사합니다. 오른쪽의 식이 빈 컬렉션으로 계산되면 `CROSS APPLY`에서 왼쪽 요소의 해당 인스턴스에 대해 쌍을 생성하지 않습니다.

`OUTER APPLY`는 오른쪽의 식이 빈 컬렉션으로 계산되는 경우에도 쌍이 생성된다는 점을 제외하고 `CROSS APPLY`와 유사합니다. 다음은 `OUTER APPLY`의 예제입니다.

`SELECT c, f FROM C AS c OUTER APPLY c.Assoc AS f`

> [!NOTE]
> Transact-sql에서와 달리 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에는 명시적 unnest 단계가 필요 하지 않습니다.

> [!NOTE]
> `CROSS` 및 `OUTER APPLY` 연산자는 SQL Server 2005에서 도입 되었습니다. 경우에 따라 쿼리 파이프라인에서 `CROSS APPLY` 및/또는 `OUTER APPLY` 연산자가 포함된 Transact-SQL을 생성할 수 있습니다. SQL Server 2005 이전 SQL Server 버전을 비롯 한 일부 백엔드 공급자는 이러한 연산자를 지원 하지 않으므로 이러한 백 엔드 공급자에서는 이러한 쿼리를 실행할 수 없습니다.
>
> 출력 쿼리에 `CROSS APPLY` 및/또는 `OUTER APPLY` 연산자가 포함될 수 있는 일부 일반적인 시나리오는 페이징이 포함된 상호 관련된 하위 쿼리, 상호 관련된 하위 쿼리 또는 탐색으로 생성된 컬렉션에 대한 AnyElement, 요소 선택기를 허용하는 그룹화 메서드를 사용하는 LINQ 쿼리, `CROSS APPLY` 또는 `OUTER APPLY`가 명시적으로 지정된 쿼리, `DEREF` 구문에 대한 `REF` 구문이 있는 쿼리 등입니다.

## <a name="multiple-collections-in-the-from-clause"></a>FROM 절의 여러 컬렉션

`FROM` 절에는 둘 이상의 컬렉션이 쉼표로 구분되어 포함될 수 있습니다. 이 경우 컬렉션은 함께 조인되는 것으로 가정됩니다. 이러한 조인을 N-Way CROSS JOIN으로 간주하세요.

다음 예제에서 `C` 및 `D`은 독립 된 컬렉션 이지만 `c.Names`는 `C`에 종속 됩니다.

```sql
FROM C AS c, D AS d, c.Names AS e
```

위의 예제는 다음 예제와 논리적으로 같습니다.

`FROM (C AS c JOIN D AS d) CROSS APPLY c.Names AS e`

## <a name="left-correlation"></a>왼쪽 상관 관계
 `FROM` 절의 항목은 위의 절에서 지정된 항목을 참조할 수 있습니다. 다음 예제에서 `C` 및 `D`는 독립된 컬렉션이지만 `c.Names`는 `C`에 종속됩니다.

```sql
from C as c, D as d, c.Names as e
```

위의 구문은 다음 구문과 논리적으로 같습니다.

```sql
from (C as c join D as d) cross apply c.Names as e
```

## <a name="semantics"></a>의미 체계

논리적으로, `FROM` 절의 컬렉션은 1-way Cross Join의 경우를 제외하고 `n`-way Cross Join의 일부인 것으로 가정됩니다. `FROM` 절의 별칭은 왼쪽에서 오른쪽으로 처리되고 나중에 참조하기 위해 현재 범위에 추가됩니다. `FROM` 절은 행의 multiset을 생성하는 것으로 가정됩니다. 해당 컬렉션 항목의 단일 요소를 나타내는 `FROM` 절의 각 항목에 대해 하나의 필드가 있습니다.

`FROM` 절은 논리적으로 Row(c, d, e) 형식의 행 multiset을 생성합니다. 여기서 c, d, e 필드는 `C`, `D` 및 `c.Names`의 요소 형식인 것으로 가정됩니다.

[!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 범위에 있는 각 단순 `FROM` 절 항목에 대해 별칭을 생성합니다. 예를 들어, 다음 FROM 절 조각에서 범위에 생성된 이름은 c, d, e입니다.

```sql
from (C as c join D as d) cross apply c.Names as e
```

@No__t-0 (Transact-sql과 달리)에서 `FROM` 절은 범위에 별칭을 도입 합니다. 이러한 컬렉션의 열(속성)에 대한 모든 참조는 해당 별칭으로 정규화해야 합니다.

## <a name="pulling-up-keys-from-nested-queries"></a>중첩 쿼리에서 키 끌어오기

중첩 쿼리에서 키를 끌어와야 하는 특정 쿼리 유형은 지원되지 않습니다. 예를 들어, 다음 쿼리는 유효합니다.

```sql
select c.Orders from Customers as c
```

그러나 다음 쿼리는 중첩 쿼리에 키가 없으므로 유효하지 않습니다.

```sql
select {1} from {2, 3}
```

## <a name="see-also"></a>참조

- [엔터티 SQL 참조](entity-sql-reference.md)
- [쿼리 식](query-expressions-entity-sql.md)
- [null 허용 구조적 형식](nullable-structured-types-entity-sql.md)
