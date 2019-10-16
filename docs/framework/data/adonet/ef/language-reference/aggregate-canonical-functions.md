---
title: 집계 정식 함수
ms.date: 03/30/2017
ms.assetid: 3bcff826-ca90-41b3-a791-04d6ff0e5085
ms.openlocfilehash: 3f4bb84c45e503fc0018e7869f3b41ddab4581a6
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251349"
---
# <a name="aggregate-canonical-functions"></a>집계 정식 함수

집계는 일련의 입력 값을 단일 값으로 줄이는 식입니다. 집계는 일반적으로 SELECT 식의 GROUP BY 절과 함께 사용되며 사용할 수 있는 위치에 대한 제약 조건이 있습니다.

## <a name="aggregate-entity-sql-canonical-functions"></a>집계 Entity SQL 정식 함수

다음은 집계 Entity SQL 정식 함수입니다.

### <a name="avgexpression"></a>Avg(expression)

null이 아닌 값의 평균을 반환합니다.

**인수**

`Int32`, `Int64`, `Double` 및 `Decimal`입니다.

**반환 값**

의 `expression`형식 이거나 `null` , 모든 입력 값이 `null` 값인 경우입니다.

**예제**

[!code-csharp[DP EntityServices Concepts#EDM_AVG](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_avg)]
[!code-sql[DP EntityServices Concepts#EDM_AVG](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_avg)]

### <a name="bigcountexpression"></a>BigCount(expression)

null 값과 중복 값을 비롯한 집계의 크기를 반환합니다.

**인수**

모든 형식입니다.

**반환 값**

`Int64`입니다.

**예제**

[!code-csharp[DP EntityServices Concepts#EDM_BIGCOUNT](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_bigcount)]
[!code-sql[DP EntityServices Concepts#EDM_BIGCOUNT](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_bigcount)]

### <a name="countexpression"></a>Count(expression)

null 값과 중복 값을 비롯한 집계의 크기를 반환합니다.

**인수**

모든 형식입니다.

**반환 값**

`Int32`입니다.

**예제**

[!code-csharp[DP EntityServices Concepts#EDM_COUNT](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_count)]
[!code-sql[DP EntityServices Concepts#EDM_COUNT](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_count)]

### <a name="maxexpression"></a>Max(expression)

null이 아닌 값의 최대값을 반환합니다.

**인수**

`Byte`, `Int16`, `Int32`, `Int64`, `Byte`, `Single`, `Double`, `Decimal`, `DateTime`, `DateTimeOffset`, `Time`, `String`, `Binary`입니다.

**반환 값**

의 `expression`형식 이거나 `null` , 모든 입력 값이 `null` 값인 경우입니다.

**예제**

[!code-csharp[DP EntityServices Concepts#EDM_MAX](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_max)]
[!code-sql[DP EntityServices Concepts#EDM_MAX](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_max)]

### <a name="minexpression"></a>Min(expression)

null이 아닌 값의 최소값을 반환합니다.

**인수**

`Byte`, `Int16`, `Int32`, `Int64`, `Byte`, `Single`, `Double`, `Decimal`, `DateTime`, `DateTimeOffset`, `Time`, `String`, `Binary`입니다.

**반환 값**

의 `expression`형식 이거나 `null` , 모든 입력 값이 `null` 값인 경우입니다.

**예제**

[!code-csharp[DP EntityServices Concepts#EDM_MIN](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_min)]
[!code-sql[DP EntityServices Concepts#EDM_MIN](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_min)]

### <a name="stdevexpression"></a>StDev(expression)

null이 아닌 값의 표준 편차를 반환합니다.

**인수**

`Int32`, `Int64`, `Double`, `Decimal`입니다.

**반환 값**

`Double` 모든 입력 값이 `Null` 값인 경우 `null`입니다.

**예제**

[!code-csharp[DP EntityServices Concepts#EDM_STDEV](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_stdev)]
[!code-sql[DP EntityServices Concepts#EDM_STDEV](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_stdev)]

### <a name="stdevpexpression"></a>StDevP(expression)

모든 값의 모집단에 대한 표준 편차를 반환합니다.

**인수**

`Int32`, `Int64`, `Double`, `Decimal`입니다.

**반환 값**

`null` 이거나 `Double` ,`null` 모든 입력 값이 값 이면입니다.

**예제**

[!code-csharp[DP EntityServices Concepts#EDM_STDEVP](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_stdevp)]
[!code-sql[DP EntityServices Concepts#EDM_STDEVP](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_stdevp)]

### <a name="sumexpression"></a>Sum(expression)

null이 아닌 값의 합계를 반환합니다.

**인수**

`Int32`, `Int64`, `Double`, `Decimal`입니다.

**반환 값**

`null` 이거나 `Double` ,`null` 모든 입력 값이 값 이면입니다.

**예제**

[!code-csharp[DP EntityServices Concepts#EDM_SUM](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_sum)]
[!code-sql[DP EntityServices Concepts#EDM_SUM](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_sum)]

### <a name="varexpression"></a>Var(expression)

null이 아닌 모든 값의 분산을 반환합니다.

**인수**

`Int32`, `Int64`, `Double`, `Decimal`입니다.

**반환 값**

`null` 이거나 `Double` ,`null` 모든 입력 값이 값 이면입니다.

**예제**

[!code-csharp[DP EntityServices Concepts#EDM_VAR](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_var)]
[!code-sql[DP EntityServices Concepts#EDM_VAR](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_var)]

### <a name="varpexpression"></a>VarP(expression)

null이 아닌 모든 값의 모집단에 대한 분산을 반환합니다.

**인수**

`Int32`, `Int64`, `Double`, `Decimal`입니다.

**반환 값**

`null` 이거나 `Double` ,`null` 모든 입력 값이 값 이면입니다.

**예제**

[!code-csharp[DP EntityServices Concepts#EDM_VARP](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_varp)]
[!code-sql[DP EntityServices Concepts#EDM_VARP](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_varp)]

동일한 기능을 Microsoft SQL 클라이언트 관리 공급자에서 사용할 수 있습니다. 자세한 내용은 [Entity Framework 함수에 대 한 SqlClient](../sqlclient-for-ef-functions.md)를 참조 하세요.

## <a name="collection-based-aggregates"></a>컬렉션 기반 집계

컬렉션 기반 집계(컬렉션 함수)는 컬렉션에 대해 작업을 수행하고 값을 반환합니다. 예를 들어 ORDERS가 모든 주문의 컬렉션인 경우 다음 식을 사용 하 여 가장 빠른 운송 날짜를 계산할 수 있습니다.

```sql
min(select value o.ShipDate from LOB.Orders as o)
```

컬렉션 기반 집계 내의 식은 현재 앰비언트 이름 결정 범위 내에서 계산됩니다.

## <a name="group-based-aggregates"></a>그룹 기반 집계

그룹 기반 집계는 GROUP BY 절에 정의된 대로 그룹에 대해 계산됩니다. 결과의 각 그룹별로 각 그룹의 요소를 집계 계산에 대한 입력으로 사용하여 개별 집계가 계산됩니다. SELECT 식에 GROUP BY 절이 사용되는 경우에는 식 이름, 집계 또는 상수를 그룹화하는 식만 프로젝션 또는 ORDER BY 절에 있을 수 있습니다.

다음 예제에서는 각 제품에 대해 주문된 평균 수량을 계산합니다.

```sql
select p, avg(ol.Quantity) from LOB.OrderLines as ol
  group by ol.Product as p
```

SELECT 식에서 group by 절을 명시적으로 사용 하지 않고 그룹 기반 집계가 있을 수 있습니다. 이 경우 모든 요소는 단일 그룹으로 처리 됩니다. 이는 상수를 기준으로 그룹화를 지정 하는 것과 같습니다. 예를 들어, 다음 식을 살펴보겠습니다.

```sql
select avg(ol.Quantity) from LOB.OrderLines as ol
```

이 식은 다음 식과 같습니다.

```sql
select avg(ol.Quantity) from LOB.OrderLines as ol group by 1
```

그룹 기반 집계 내의 식은 WHERE 절 식에 표시되는 이름 확인 범위 내에서 계산됩니다.

Transact-sql에서와 마찬가지로 그룹 기반 집계도 ALL 또는 DISTINCT 한정자를 지정할 수 있습니다. DISTINCT 한정자를 지정하면 집계가 계산되기 전에 집계 입력 컬렉션에서 중복 항목이 제거됩니다. ALL 한정자를 지정하거나 어떠한 한정자도 지정하지 않으면 중복 항목이 제거되지 않습니다.

## <a name="see-also"></a>참고자료

- [정식 함수](canonical-functions.md)
