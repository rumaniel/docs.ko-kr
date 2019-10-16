---
title: 집계 함수(Entity SQL)
ms.date: 03/30/2017
ms.assetid: acfd3149-f519-4c6e-8fe1-b21d243a0e58
ms.openlocfilehash: c79071e73763b56c0dde906499f3eef1d296ce0c
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251346"
---
# <a name="aggregate-functions-entity-sql"></a>집계 함수(Entity SQL)
집계는 컬렉션을 그룹 작업의 일부분인 스칼라로 압축하는 언어 구문입니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 집계의 형식은 다음 두 가지입니다.  
  
- [!INCLUDE[esql](../../../../../../includes/esql-md.md)]식의 어디에서 나 사용할 수 있는 컬렉션 함수입니다. 이 함수는 프로젝션의 집계 함수를 사용하며 컬렉션에 대한 해당 동작을 예측합니다. 컬렉션 함수는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서 집계를 지정하는 데 주로 사용되는 모드입니다.  
  
- GROUP BY 절을 포함하는 쿼리 식의 그룹 집계. Transact-sql에서와 같이 그룹 집계는 DISTINCT 및 ALL을 집계 입력에 대 한 한정자로 받아들입니다.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]는 먼저 식을 컬렉션 함수로 해석 하려고 하며 식이 SELECT 식의 컨텍스트에 있는 경우이를 그룹 집계로 해석 합니다.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)][Grouppartition](grouppartition-entity-sql.md)이라는 특수 집계 연산자를 정의 합니다. 이 연산자를 사용 하면 그룹화 된 입력 집합에 대 한 참조를 가져올 수 있습니다. 이를 통해 보다 고급 기능의 그룹화 쿼리를 사용할 수 있습니다. 이 경우 GROUP BY 절의 결과는 그룹 집계 또는 컬렉션 함수 이외의 장소에 사용될 수 있습니다.  
  
## <a name="collection-functions"></a>컬렉션 함수  
 컬렉션 함수는 컬렉션에 대해 작업을 수행하고 스칼라 값을 반환합니다. 예를 들어, `orders`가 모든 `orders`의 컬렉션인 경우 다음 식을 사용하여 가장 빠른 운송 날짜를 계산할 수 있습니다.  
  
 `min(select value o.ShipDate from LOB.Orders as o)`  
  
## <a name="group-aggregates"></a>그룹 집계  
 그룹 집계는 GROUP BY 절에 정의된 대로 그룹 결과에 대해 계산됩니다. GROUP BY 절은 데이터를 그룹으로 분할합니다. 결과의 각 그룹별로 집계 함수가 적용되고 각 그룹의 요소를 집계 계산에 대한 입력으로 사용하여 개별 집계가 계산됩니다. SELECT 식에 GROUP BY 절이 사용되는 경우에는 그룹화 식 이름, 집계 또는 상수 식만 프로젝션, HAVING 또는 ORDER BY 절에 있을 수 있습니다.  
  
 다음 예제에서는 각 제품에 대해 주문된 평균 수량을 계산합니다.  
  
 `select p, avg(ol.Quantity) from LOB.OrderLines as ol`  
  
 `group by ol.Product as p`  
  
 SELECT 식에서 GROUP BY 절을 명시적으로 사용하지 않고 그룹 집계를 사용할 수도 있습니다. 모든 요소가 단일 그룹으로 간주되며, 이는 상수를 기준으로 그룹화를 지정하는 것과 같습니다.  
  
 `select avg(ol.Quantity) from LOB.OrderLines as ol`  
  
 `select avg(ol.Quantity) from LOB.OrderLines as ol group by 1`  
  
 GROUP BY 절에서 사용되는 식은 WHERE 절 식에 표시되는 동일한 이름 확인 범위를 사용하여 계산됩니다.  
  
## <a name="see-also"></a>참고자료

- [함수](functions-entity-sql.md)
