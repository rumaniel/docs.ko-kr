---
title: DataRelation 탐색
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e5e673f4-9b44-45ae-aaea-c504d1cc5d3e
ms.openlocfilehash: 412f133c7cf23642ba92d54272287cb708dddc92
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784356"
---
# <a name="navigating-datarelations"></a>DataRelation 탐색
<xref:System.Data.DataRelation>의 기본 기능 중 하나는 <xref:System.Data.DataTable> 내에서 <xref:System.Data.DataSet>를 하나씩 탐색할 수 있도록 하는 것입니다. 이렇게 하면 관련 **datatable**에서 단일 **DataRow** 가 <xref:System.Data.DataRow> 지정 된 경우 하나의 **DataTable** 에서 모든 관련 개체를 검색할 수 있습니다. 예를 들어 고객 테이블과 주문 테이블 간에 **DataRelation** 을 설정한 후에는 **GetChildRows**를 사용 하 여 특정 고객 행의 모든 주문 행을 검색할 수 있습니다.  
  
 다음 코드 예에서는 **Customers** 테이블과 **데이터 집합** 의 **orders** 테이블 사이에 **DataRelation** 을 만들고 각 고객에 대 한 모든 주문을 반환 합니다.  
  
 [!code-csharp[DataWorks Data.DataTableRelation#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableRelation/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableRelation#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableRelation/VB/source.vb#1)]  
  
 다음 예제에서는 이전 예제를 기반으로 네 개의 테이블을 모두 연관시키고 각각의 관계를 탐색합니다. 이전 예에서와 같이 **CustomerID** 는 **Customers** 테이블을 **Orders** 테이블에 연결 합니다. **Customers** 테이블의 각 고객에 대해 **orders** 테이블의 모든 자식 행이 결정 되어 특정 고객에 게 포함 된 주문 수와 해당 **OrderID** 값이 반환 됩니다.  
  
 또한 확장 된 예제에서는 **OrderDetails** 및 **Products** 테이블의 값을 반환 합니다. **Orders** 테이블은 **OrderID** 를 사용 하 여 각 고객 주문, 주문 된 제품 및 수량을 확인 하는 **OrderDetails** 테이블과 관련이 있습니다. **OrderDetails** 테이블에는 주문 된 제품의 **productid** 만 포함 되어 있으므로 **OrderDetails** 은 **ProductName**을 반환 하기 위해 **productid** 를 사용 하는 **제품과** 관련 됩니다. 이 관계에서 **Products** 테이블은 부모이 고 **Order Details** 테이블은 자식입니다. 결과적으로 **OrderDetails** 테이블을 반복 하는 경우 **GetParentRow** 를 호출 하 여 관련 된 **ProductName** 값을 검색 합니다.  
  
 **Customers** 및 **Orders** 테이블에 대해 **DataRelation** 을 만들 때 **createConstraints** 플래그에 대해 값이 지정 되지 않습니다 (기본값은 **true**임). 여기서는 **Orders** 테이블의 모든 행에 부모 **Customers** 테이블에 있는 **CustomerID** 값이 있다고 가정 합니다. Customers 테이블 에존재하지않는CustomerID가Orders테이블에있는경우이발생하면<xref:System.Data.ForeignKeyConstraint> 예외가 throw 됩니다.  
  
 자식 열에 부모 열에 포함 되지 않은 값이 포함 되어 있을 경우 **DataRelation**을 추가할 때 **createConstraints** 플래그를 **false** 로 설정 합니다. 이 예에서는 **Orders** 테이블과 **OrderDetails** 테이블 간의 **DataRelation** 에 대해 **createConstraints** 플래그가 **false** 로 설정 됩니다. 이를 통해 응용 프로그램은 **OrderDetails** 테이블의 모든 레코드를 반환할 수 있으며 런타임 예외를 생성 하지 않고 **Orders** 테이블의 레코드 하위 집합만 반환할 수 있습니다. 확장된 예제는 다음과 같은 형식의 출력을 생성합니다.  
  
```  
Customer ID: NORTS  
  Order ID: 10517  
        Order Date: 4/24/1997 12:00:00 AM  
           Product: Filo Mix  
          Quantity: 6  
           Product: Raclette Courdavault  
          Quantity: 4  
           Product: Outback Lager  
          Quantity: 6  
  Order ID: 11057  
        Order Date: 4/29/1998 12:00:00 AM  
           Product: Outback Lager  
          Quantity: 3  
```  
  
 다음 코드 예는 **OrderDetails** 및 **Products** 테이블의 값이 반환 되 고 반환 되는 **Orders** 테이블에 있는 레코드의 하위 집합만 포함 된 확장 된 샘플입니다.  
  
 [!code-csharp[DataWorks Data.DataTableNavigation#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableNavigation/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableNavigation#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableNavigation/VB/source.vb#1)]  
  
## <a name="see-also"></a>참고자료

- [DataSet, DataTable 및 DataView](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
