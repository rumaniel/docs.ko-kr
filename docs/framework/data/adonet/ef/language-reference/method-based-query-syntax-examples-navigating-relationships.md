---
title: '메서드 기반 쿼리 구문 예제: 관계 탐색'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a0bfa4b1-99e5-4dd1-9912-4b825a9dc25c
ms.openlocfilehash: 0060f14319bb0dfbed597e59dfe44666c4cfbe84
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854451"
---
# <a name="method-based-query-syntax-examples-navigating-relationships"></a>메서드 기반 쿼리 구문 예제: 관계 탐색
Entity Framework의 탐색 속성은 연결의 end에서 엔터티를 찾는 데 사용 되는 바로 가기 속성입니다. 탐색 속성을 사용하면 엔터티 간에 탐색하거나 연결 집합을 통해 관련 엔터티 간에 탐색할 수 있습니다. 이 항목에서는 LINQ to Entities 쿼리의 탐색 속성을 통해 관계를 탐색 하는 방법에 대 한 메서드 기반 쿼리 구문 예제를 제공 합니다.  
  
 이 예제에서 사용하는 AdventureWorks Sales 모델에서는 AdventureWorks 샘플 데이터베이스의 Contact, Address, Product, SalesOrderHeader 및 SalesOrderDetail 테이블을 사용합니다.  
  
 이 항목의 예제에서는 다음 `using` / `Imports` 문을 사용 합니다.  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="example"></a>예제  
 메서드 기반 쿼리 구문을 사용하는 다음 예제에서는 <xref:System.Linq.Queryable.SelectMany%2A> 메서드를 사용하여 성이 "Zhou"인 연락처의 모든 주문을 가져옵니다. `Contact.SalesOrderHeader` 탐색 속성을 사용하여 각 연락처의 `SalesOrderHeader` 개체 컬렉션을 가져옵니다.  
  
 [!code-csharp[DP L2E Examples#SelectEachContactsOrders_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selecteachcontactsorders_mq)]
 [!code-vb[DP L2E Examples#SelectEachContactsOrders_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selecteachcontactsorders_mq)]  
  
## <a name="example"></a>예제  
 메서드 기반 쿼리 구문을 사용하는 다음 예제에서는 <xref:System.Linq.Queryable.Select%2A> 메서드를 사용하여 성이 "Zhou"인 각 연락처의 총 금액 합계와 연락처 ID를 모두 가져옵니다. `Contact.SalesOrderHeader` 탐색 속성을 사용하여 각 연락처의 `SalesOrderHeader` 개체 컬렉션을 가져옵니다. `Sum` 메서드는 `Contact.SalesOrderHeader` 탐색 속성을 사용하여 각 연락처의 모든 주문에 대한 총 금액을 더합니다.  
  
 [!code-csharp[DP L2E Examples#SelectEachContactsOrders2_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selecteachcontactsorders2_mq)]
 [!code-vb[DP L2E Examples#SelectEachContactsOrders2_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selecteachcontactsorders2_mq)]  
  
## <a name="example"></a>예제  
 메서드 기반 쿼리 구문의 다음 예제에서는 성이 "Zhou"인 연락처의 모든 주문을 가져옵니다. `Contact.SalesOrderHeader` 탐색 속성을 사용하여 각 연락처의 `SalesOrderHeader` 개체 컬렉션을 가져옵니다. 연락처의 이름과 주문은 익명 형식으로 반환됩니다.  
  
 [!code-csharp[DP L2E Examples#SelectEachContactsOrders3_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selecteachcontactsorders3_mq)]
 [!code-vb[DP L2E Examples#SelectEachContactsOrders3_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selecteachcontactsorders3_mq)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 `SalesOrderHeader.Address` 및 `SalesOrderHeader.Contact` 탐색 속성을 사용하여 서로 연결된 `Address` 및 `Contact` 개체의 컬렉션을 가져옵니다. Seattle 시로 가는 각 주문에 대한 연락처의 성, 주소, 판매 주문 번호 및 총 주문 금액이 익명 형식으로 반환됩니다.  
  
 [!code-csharp[DP L2E Examples#GetOrderInfoThruRelationships_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#getorderinfothrurelationships_mq)]
 [!code-vb[DP L2E Examples#GetOrderInfoThruRelationships_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#getorderinfothrurelationships_mq)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Where` 메서드를 사용하여 2003년 12월 1일 이후의 주문을 찾은 다음 `order.SalesOrderDetail` 탐색 속성을 사용하여 각 주문의 세부 사항을 가져옵니다.  
  
 [!code-csharp[DP L2E Examples#WhereNavProperty](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#wherenavproperty)]
 [!code-vb[DP L2E Examples#WhereNavProperty](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#wherenavproperty)]  
  
## <a name="see-also"></a>참고자료

- [관계, 탐색 속성 및 외래 키](/ef/ef6/fundamentals/relationships)
- [LINQ to Entities에서 쿼리](queries-in-linq-to-entities.md)
