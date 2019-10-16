---
title: DataView 만들기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b1cc02d1-23b1-4439-a998-0da1899f3442
ms.openlocfilehash: 3e1c31dac458594eee70ddd99469aca7cf63b848
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785481"
---
# <a name="creating-a-dataview"></a>DataView 만들기
<xref:System.Data.DataView>를 만드는 방법은 두 가지입니다. **DataView** 생성자를 사용 하거나의 <xref:System.Data.DataTable.DefaultView%2A> <xref:System.Data.DataTable>속성에 대 한 참조를 만들 수 있습니다. **DataView** 생성자는 비어 있거나, **datatable** 을 단일 인수로 사용 하거나, 필터 조건, 정렬 조건 및 행 상태 필터와 함께 **datatable** 을 사용할 수 있습니다. **DataView**에 사용할 수 있는 추가 인수에 대 한 자세한 내용은 [데이터 정렬 및 필터링](sorting-and-filtering-data.md)을 참조 하세요.  
  
 Dataview **가 만들어질** 때와 **Sort**, **RowFilter**또는 **Rowstatefilter** 속성이 모두 수정 될 때 **dataview** 에 대 한 인덱스가 작성 되기 때문에 초기에 **DataView**를 만들 때 순서 또는 필터링 조건을 생성자 인수로 정렬 합니다. 정렬 또는 필터 조건을 지정 하지 않고 **dataview** 를 만든 후 나중에 **sort**, **RowFilter**또는 **rowstatefilter** 속성을 설정 하면 **인덱스는 나중** 에 두 번 이상 빌드됩니다. 정렬 또는 필터 속성을 수정할 때 생성 됩니다.  
  
 인수를 사용 하지 않는 생성자를 사용 하 여 **dataview** 를 만드는 경우에는 **테이블** 속성을 설정할 때까지 **dataview** 를 사용할 수 없습니다.  
  
 다음 코드 예제에서는 **dataview** 생성자를 사용 하 여 **dataview** 를 만드는 방법을 보여 줍니다. **RowFilter**, **Sort** 열 및 **DataViewRowState** 는 **DataTable**과 함께 제공 됩니다.  
  
```vb  
Dim custDV As DataView = New DataView(custDS.Tables("Customers"), _  
    "Country = 'USA'", _  
    "ContactName", _  
    DataViewRowState.CurrentRows)  
```  
  
```csharp  
DataView custDV = new DataView(custDS.Tables["Customers"],   
    "Country = 'USA'",   
    "ContactName",   
    DataViewRowState.CurrentRows);  
```  
  
 다음 코드 예제에서는 테이블의 **DefaultView** 속성을 사용 하 여 **DataTable** 의 기본 **DataView** 에 대 한 참조를 가져오는 방법을 보여 줍니다.  
  
```vb  
Dim custDV As DataView = custDS.Tables("Customers").DefaultView  
```  
  
```csharp  
DataView custDV = custDS.Tables["Customers"].DefaultView;  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Data.DataTable>
- <xref:System.Data.DataView>
- [DataView](dataviews.md)
- [데이터 정렬 및 필터링](sorting-and-filtering-data.md)
- [DataTable](datatables.md)
- [ADO.NET 개요](../ado-net-overview.md)
