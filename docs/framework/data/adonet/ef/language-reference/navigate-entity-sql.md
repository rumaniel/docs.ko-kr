---
title: NAVIGATE (Entity SQL)
ms.date: 03/30/2017
ms.assetid: f107f29d-005f-4e39-a898-17f163abb1d0
ms.openlocfilehash: 2c6c2ae4c593da1d5fe8cdf3015eb0e31e4b12b5
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70249947"
---
# <a name="navigate-entity-sql"></a>NAVIGATE (Entity SQL)

엔터티 사이에 설정된 관계를 탐색합니다.

## <a name="syntax"></a>구문

```
navigate(instance-expression, [relationship-type], [to-end [, from-end] ])
```

## <a name="arguments"></a>인수

`instance-expression`엔터티의 인스턴스입니다.

`relationship-type`CSDL (개념 스키마 정의 언어) 파일에서 관계의 형식 이름입니다. 는 `relationship-type` 네임 스페이스 > \<로 한정 됩니다\< . 관계 유형 이름 >입니다.

`to`관계의 끝입니다.

`from`관계의 시작 부분입니다.

## <a name="return-value"></a>반환 값

끝 End의 카디널리티가 1인 경우 반환 값은 `Ref<T>`이고, 끝 End의 카디널리티가 n인 경우 반환 값은 `Collection<Ref<T>>`입니다.

## <a name="remarks"></a>설명

관계는 EDM (엔터티 데이터 모델)의 첫 번째 클래스 구문입니다. 둘 이상의 엔터티 형식 간에 관계를 설정할 수 있으며 사용자는 한쪽(엔터티)에서 다른 쪽으로 관계를 탐색할 수 있습니다. `from` 및 `to` 는 관계 내의 이름 확인에 모호성이 없는 경우에 한해 조건부로 사용 가능합니다.

NAVIGATE는 O 및 C 공간에서 유효합니다.

탐색 구문의 일반적인 형태는 다음과 같습니다.

navigate(`instance-expression`, `relationship-type`, [ `to-end` [, `from-end` ] ] )

예를 들어:

```sql
Select o.Id, navigate(o, OrderCustomer, Customer, Order)
From LOB.Orders as o
```

여기서 OrderCustomer는 `relationship`이고, Customer와 Order는 각각 관계의 `to-end` (고객)와 `from-end` (주문)입니다. Ordercustomer가 n:1 관계 이면 탐색 식의 결과 형식은 Ref\<Customer >입니다.

이 식이 좀 더 단순화된 형태는 다음과 같습니다.

```sql
Select o.Id, navigate(o, OrderCustomer)
From LOB.Orders as o
```

마찬가지로, 다음 형식의 쿼리에서 navigate 식은 > > Ref\<Order < 컬렉션을 생성 합니다.

```sql
Select c.Id, navigate(c, OrderCustomer, Order, Customer)
From LOB.Customers as c
```

인스턴스 식은 엔터티/참조 형식이어야 합니다.

## <a name="example"></a>예제

다음 Entity SQL 쿼리는 NAVIGATE 연산자를 사용하여 Address 및 SalesOrderHeader 엔터티 형식 사이에 설정된 관계를 탐색합니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.

1. [방법: StructuralType 결과](../how-to-execute-a-query-that-returns-structuraltype-results.md)를 반환 하는 쿼리를 실행 합니다.

2. 다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.

 [!code-csharp[DP EntityServices Concepts 2#NAVIGATE](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#navigate)]

## <a name="see-also"></a>참고자료

- [엔터티 SQL 참조](entity-sql-reference.md)
- [방법: Navigate 연산자를 사용 하 여 관계 탐색](navigate-entity-sql.md)
