---
title: 크로스 테이블 쿼리(LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6819a16f-8656-41af-a54d-dfec0cb66366
ms.openlocfilehash: 4ab8eb9988995b4a142b1c02e82476f45285c3b8
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785622"
---
# <a name="cross-table-queries-linq-to-dataset"></a>크로스 테이블 쿼리(LINQ to DataSet)
단일 테이블을 쿼리 하는 것 외에도 LINQ to DataSet에서 테이블 간 쿼리를 수행할 수 있습니다. 이 작업은 *조인을*사용 하 여 수행 됩니다. 조인은 한 데이터 소스의 개체를 공통 특성(예: 제품 또는 연락처 ID)을 공유하는 다른 데이터 소스의 개체와 연결하는 것입니다. 개체 지향적 프로그래밍의 경우 각 개체에 다른 개체를 참조하는 멤버가 있으므로 개체 간의 관계를 탐색하기가 비교적 쉽습니다. 그러나 외부 데이터베이스 테이블에서는 관계를 탐색하기가 쉽지 않습니다. 데이터베이스 테이블에는 기본 제공 관계가 없습니다. 이러한 경우 조인 연산을 사용하여 각 소스의 요소를 연결할 수 있습니다. 예를 들어 제품 정보와 판매 정보가 들어 있는 두 테이블이 있는 경우 조인 연산을 사용하여 동일한 판매 주문에 대한 판매 정보와 제품을 연결할 수 있습니다.  
  
 프레임 [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] 워크는 및 <xref:System.Linq.Enumerable.GroupJoin%2A>의 두 조인 <xref:System.Linq.Enumerable.Join%2A> 연산자를 제공 합니다. 이러한 연산자는 키가 같은 경우에만 두 데이터 소스와 일치 하는 조인 인 *동등 조인을*수행 합니다. 이와 반대로 transact-sql은 `equals` `less than` 연산자와 같이 이외의 조인 연산자를 지원 합니다.  
  
 관계형 데이터베이스 용어에서 <xref:System.Linq.Enumerable.Join%2A>은 내부 조인을 구현합니다. 내부 조인은 상대 데이터 집합에 일치하는 항목이 있는 개체만 반환되는 조인입니다.  
  
 연산자 <xref:System.Linq.Enumerable.GroupJoin%2A> 에는 관계형 데이터베이스 측면에 직접 상응 하는 기능이 없지만 내부 조인 및 왼쪽 우선 외부 조인의 상위 집합을 구현 합니다. 왼쪽 우선 외부 조인은 두 번째 컬렉션에 상관 관계가 지정 된 요소가 없더라도 첫 번째 (왼쪽) 컬렉션의 각 요소를 반환 하는 조인입니다.  
  
 조인에 대 한 자세한 내용은 [조인 작업](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/bb397908(v=vs.120))을 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 예제에서는 AdventureWorks 샘플 데이터베이스의 `SalesOrderHeader` 및 `SalesOrderDetail` 테이블에 대해 기존 방식의 조인을 수행하여 8월의 온라인 주문을 가져옵니다.  
  
 [!code-csharp[DP LINQ to DataSet Examples#Join](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#join)]
 [!code-vb[DP LINQ to DataSet Examples#Join](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#join)]  
  
## <a name="see-also"></a>참고자료

- [데이터 집합 쿼리](querying-datasets-linq-to-dataset.md)
- [단일 테이블 쿼리](single-table-queries-linq-to-dataset.md)
- [형식화된 데이터 집합 쿼리](querying-typed-datasets.md)
- [조인 작업](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/bb397908(v=vs.120))
- [LINQ to DataSet 예제](linq-to-dataset-examples.md)
