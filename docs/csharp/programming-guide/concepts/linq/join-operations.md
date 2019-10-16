---
title: 조인 작업(C#)
ms.date: 07/20/2015
ms.assetid: 5105e0da-1267-4c00-837a-f0e9602279b8
ms.openlocfilehash: 95661e2d0d7f4f0e75c1fa1b10e1f322923189b1
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69592087"
---
# <a name="join-operations-c"></a>조인 작업(C#)
두 데이터 소스를 *조인*하는 것은 한 데이터 소스의 개체를 공통 특성을 공유하는 다른 데이터 소스의 개체와 연결하는 것입니다.  
  
 서로 간의 관계를 직접 적용할 수 없는 데이터 소스를 대상으로 하는 쿼리에서는 조인이 중요한 작업입니다. 개체 지향 프로그래밍에서 데이터 소스 간의 관계를 직접 적용할 수 없다는 것은 모델링되지 않은 개체 간에 상관 관계가 있음을 의미할 수 있습니다(예: 단방향 관계에서 반대 방향을 사용). 단방향 관계의 예로는 Customer 클래스가 City 형식 속성을 포함하는데 City 클래스는 Customer 개체의 컬렉션인 속성을 포함하지 않는 경우가 있습니다. City 개체 목록이 있는 경우 각 구/군/시의 모든 고객을 찾으려면 조인 작업을 사용하면 됩니다.  
  
 LINQ 프레임워크에 제공되는 조인 메서드는 <xref:System.Linq.Enumerable.Join%2A> 및 <xref:System.Linq.Enumerable.GroupJoin%2A>입니다. 이러한 메서드는 키가 같은지 여부에 따라 두 데이터 소스의 일치 여부를 확인하는 조인인 동등 조인을 수행합니다. 비교를 위해 Transact-SQL에서는 '같음'이 아닌 '보다 작음' 연산자와 같은 조인 연산자를 지원합니다. 관계형 데이터베이스 용어에서 <xref:System.Linq.Enumerable.Join%2A>은 내부 조인을 구현합니다. 내부 조인은 다른 데이터 집합에 일치하는 항목이 있는 개체만 반환하는 유형의 조인입니다. <xref:System.Linq.Enumerable.GroupJoin%2A> 메서드에는 관계형 데이터베이스 측면에 직접 상응하는 기능이 없지만 내부 조인 및 왼쪽 우선 외부 조인의 상위 집합을 구현합니다. 왼쪽 우선 외부 조인은 다른 데이터 소스에 서로 관련된 요소가 없더라도 첫 번째(왼쪽) 데이터 소스의 각 요소를 반환하는 조인입니다.  
  
 다음 그림에서는 내부 조인 또는 왼쪽 우선 외부 조인에 포함된 두 집합 및 해당 집합 내의 요소를 개념적으로 보여줍니다.  
  
 ![내부/외부를 보여주는 두 개의 겹치는 원](./media/join-operations/join-method-overlapping-circles.png)  
  
## <a name="methods"></a>메서드  
  
|메서드 이름|설명|C# 쿼리 식 구문|추가 정보|  
|-----------------|-----------------|---------------------------------|----------------------|  
|Join|키 선택기 함수를 기준으로 두 시퀀스를 조인한 다음 값 쌍을 추출합니다.|`join … in … on … equals …`|<xref:System.Linq.Enumerable.Join%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Join%2A?displayProperty=nameWithType>|  
|GroupJoin|키 선택기 함수를 기준으로 두 시퀀스를 조인한 다음 결과로 생성된 일치 항목을 요소마다 그룹화합니다.|`join … in … on … equals … into …`|<xref:System.Linq.Enumerable.GroupJoin%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.GroupJoin%2A?displayProperty=nameWithType>|  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Linq>
- [표준 쿼리 연산자 개요(C#)](./standard-query-operators-overview.md)
- [익명 형식](../../classes-and-structs/anonymous-types.md)
- [조인 및 교차곱 쿼리 작성](../../../../framework/data/adonet/sql/linq/formulate-joins-and-cross-product-queries.md)
- [join 절](../../../language-reference/keywords/join-clause.md)
- [방법: 복합 키를 사용하여 조인](../../linq-query-expressions/how-to-join-by-using-composite-keys.md)
- [방법: 서로 다른 파일의 콘텐츠 조인(LINQ)(C#)](./how-to-join-content-from-dissimilar-files-linq.md)
- [방법: Join 절 결과를 순서대로 정렬](../../linq-query-expressions/how-to-order-the-results-of-a-join-clause.md)
- [방법: 사용자 지정 조인 작업 수행](../../linq-query-expressions/how-to-perform-custom-join-operations.md)
- [방법: 그룹화 조인 수행](../../linq-query-expressions/how-to-perform-grouped-joins.md)
- [방법: 내부 조인 수행](../../linq-query-expressions/how-to-perform-inner-joins.md)
- [방법: 왼쪽 우선 외부 조인 수행](../../linq-query-expressions/how-to-perform-left-outer-joins.md)
- [방법: 여러 소스로 개체 컬렉션 채우기(LINQ)(C#)](./how-to-populate-object-collections-from-multiple-sources-linq.md)
