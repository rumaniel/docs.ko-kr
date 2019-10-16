---
title: DataRelation 추가
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a4a564fb-c1c4-4135-b6c2-b030e51195e4
ms.openlocfilehash: 8157d296636d0f8661a35af35de561f5cc49c30b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784813"
---
# <a name="adding-datarelations"></a>DataRelation 추가
여러 <xref:System.Data.DataSet> 개체가 포함된 <xref:System.Data.DataTable>에서는 <xref:System.Data.DataRelation> 개체를 사용하여 하나의 테이블을 다른 테이블에 연관시키거나, 테이블 사이를 탐색하거나, 연관된 테이블의 자식 또는 부모 행을 반환할 수 있습니다.  
  
 **Datarelation** 을 만드는 데 필요한 인수는 만들어지는 **datarelation** 의 이름과 관계의 부모 및 자식 열로 사용 되는 열에 <xref:System.Data.DataColumn> 대 한 하나 이상의 참조의 배열입니다. **DataRelation**을 만든 후에는이를 사용 하 여 테이블 간에 이동 하 고 값을 검색할 수 있습니다.  
  
 <xref:System.Data.UniqueConstraint> **DataRelation** <xref:System.Data.ForeignKeyConstraint> 을에 추가 하면 기본적으로 부모 테이블 및에 대 한가 자식 테이블에 추가됩니다.<xref:System.Data.DataSet> 이러한 기본 제약 조건에 대 한 자세한 내용은 [DataTable 제약 조건](datatable-constraints.md)을 참조 하세요.  
  
 다음 코드 예제에서는에 두 개의 <xref:System.Data.DataTable> 개체를 <xref:System.Data.DataSet>사용 하 여 DataRelation을 만듭니다. 각 <xref:System.Data.DataTable> 에는 두 <xref:System.Data.DataTable> 개체 간의 링크 역할을 하는 **CustID**라는 열이 포함 되어 있습니다. 이 예에서는 단일 **DataRelation** 을의 **관계** <xref:System.Data.DataSet>컬렉션에 추가 합니다. 예제의 첫 번째 인수는 만들 **DataRelation** 의 이름을 지정 합니다. 두 번째 인수는 부모 **datacolumn** 을 설정 하 고 세 번째 인수는 자식 **datacolumn**을 설정 합니다.  
  
```vb  
customerOrders.Relations.Add("CustOrders", _  
  customerOrders.Tables("Customers").Columns("CustID"), _  
  customerOrders.Tables("Orders").Columns("CustID"))  
```  
  
```csharp  
customerOrders.Relations.Add("CustOrders",  
  customerOrders.Tables["Customers"].Columns["CustID"],  
  customerOrders.Tables["Orders"].Columns["CustID"]);  
```  
  
 또한 **DataRelation** 에는 **중첩** 된 속성이 있습니다 .이 속성을 **true**로 설정 하면를 사용 하 여 <xref:System.Data.DataSet.WriteXml%2A> XML 요소로 작성 될 때 자식 테이블의 행이 부모 테이블의 연결 된 행 내에 중첩 됩니다. 자세한 내용은 [데이터 세트에서 XML 사용](using-xml-in-a-dataset.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [DataSet, DataTable 및 DataView](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
