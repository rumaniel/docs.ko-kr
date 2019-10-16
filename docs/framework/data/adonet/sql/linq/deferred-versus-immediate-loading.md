---
title: 지연된 로드 및 즉시 로드 비교
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d1d7247f-a3b7-460b-b342-5c1a2365aa1a
ms.openlocfilehash: 2045cab19e7400f94888297571a172de1578094d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794132"
---
# <a name="deferred-versus-immediate-loading"></a>지연된 로드 및 즉시 로드 비교
개체를 쿼리하는 경우 실제로는 요청한 개체만 검색합니다. 합니다 *관련* 개체는 동시에 자동으로 페치 되지 않습니다. (자세한 내용은 [관계 간 쿼리](querying-across-relationships.md).) 관련 개체에 액세스할 때 검색 요청을 생성하기 때문에 관련 개체가 아직 로드되지 않았다는 사실을 확인할 수 없습니다.  
  
 예를 들어 특정 주문 집합을 쿼리 한 다음 가끔 특정 고객에 게 전자 메일 알림을 보낼 수 있습니다. 처음부터 매 주문마다 모든 고객 데이터를 검색할 필요는 없습니다. 지연된 로드를 사용하여 반드시 검색해야 할 때까지 추가 정보의 검색을 연기할 수 있습니다. 다음 예제를 참조하세요.  
  
 [!code-csharp[DLinqQueryConcepts#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#1)]
 [!code-vb[DLinqQueryConcepts#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#1)]  
  
 반대의 경우도 마찬가지입니다. 고객과 주문 데이터를 동시에 확인해야 하는 애플리케이션이 있는 경우 두 데이터 집합이 모두 필요합니다. 결과를 얻으면 바로 애플리케이션에 각 고객에 대한 주문 정보가 필요합니다. 각 고객의 주문에 대한 쿼리를 개별적으로 전송하는 것은 바람직하지 않습니다. 이 경우에는 고객과 주문 데이터를 함께 검색하는 것이 좋습니다.  
  
 [!code-csharp[DLinqQueryConcepts#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#2)]
 [!code-vb[DLinqQueryConcepts#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#2)]  
  
 또한 외적 쿼리를 생성하고 모든 관련 데이터를 하나의 큰 프로젝션으로 검색하여 쿼리에서 고객과 주문을 조인할 수 있습니다. 그러나 이 결과는 엔터티가 아닙니다. 자세한 내용은 [LINQ to SQL 개체 모델](the-linq-to-sql-object-model.md)을 참조 하세요. 엔터티는 ID를 포함하며 사용자가 수정할 수 있는 개체이지만 이 결과는 변경할 수도 유지할 수도 없는 프로젝션입니다. 더욱 심각한 문제는 결합된 조인 출력에서 각 주문에 대해 각 고객이 반복되므로 많은 중복 데이터가 검색된다는 점입니다.  
  
 실제로 필요한 것은 관련 개체 집합을 동시에 검색하는 것입니다. 집합은 그래프의 구분된 섹션이므로 실제로 사용할 데이터보다 많거나 적게 검색하지는 않게 됩니다. 이를 위해 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 개체 모델 영역을 즉시 로드하기 위해 <xref:System.Data.Linq.DataLoadOptions>를 제공합니다. 메서드에는 다음이 포함됩니다.  
  
- <xref:System.Data.Linq.DataLoadOptions.LoadWith%2A> 메서드 - 주 대상과 관련된 데이터를 즉시 로드합니다.  
  
- <xref:System.Data.Linq.DataLoadOptions.AssociateWith%2A> 메서드 - 특정 관계에 대해 검색한 개체를 필터링합니다.  
  
## <a name="see-also"></a>참고자료

- [쿼리 개념](query-concepts.md)
