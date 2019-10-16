---
title: 지원되지 않는 식(Entity SQL)
ms.date: 03/30/2017
ms.assetid: 5e79da7e-e78a-413c-8fb0-f3f9cd84f579
dev_langs:
- sql
ms.openlocfilehash: 956fe117eb0c59392c3999046bc70deaed268ac6
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70248777"
---
# <a name="unsupported-expressions"></a>지원 되지 않는 식

이 항목에서는에서 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]지원 되지 않는 transact-sql 식에 대해 설명 합니다. 자세한 내용은 [Transact-sql과 Entity SQL 다른 방법](how-entity-sql-differs-from-transact-sql.md)을 참조 하세요.

## <a name="quantified-predicates"></a>정량화 된 조건자

Transact-sql은 다음 형식의 구문을 허용 합니다.

```sql
sal > all (select salary from employees)
sal > any (select salary from employees)
```

이와 달리 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 이러한 생성이 지원되지 않습니다. 대신 이와 동등한 식을 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서 다음과 같이 쓸 수 있습니다.

```sql
not exists(select 0 from employees as e where sal <= e.salary)
exists(select 0 from employees as e where sal > e.salary)
```

## <a name="-operator"></a>* 연산자

Transact-sql은 SELECT 절에서 * 연산자를 사용 하 여 모든 열이 투영 되어야 함을 나타낼 수 있습니다. 이는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 지원되지 않습니다.

## <a name="see-also"></a>참고자료

- [Entity SQL 개요](entity-sql-overview.md)
- [Entity SQL과 Transact-SQL의 차이점](how-entity-sql-differs-from-transact-sql.md)
