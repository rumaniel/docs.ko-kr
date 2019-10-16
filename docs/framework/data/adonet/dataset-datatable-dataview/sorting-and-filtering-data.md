---
title: 데이터 정렬 및 필터링
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fdd9c753-39df-48cd-9822-2781afe76200
ms.openlocfilehash: 09cee2f2b2c3288c835912c9f311bf2511c7b0d0
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785918"
---
# <a name="sorting-and-filtering-data"></a>데이터 정렬 및 필터링
<xref:System.Data.DataView>를 사용하면 다음과 같은 여러 가지 방법으로 <xref:System.Data.DataTable>의 데이터를 정렬 및 필터링할 수 있습니다.  
  
- <xref:System.Data.DataView.Sort%2A> 속성을 사용하여 하나 또는 여러 열의 정렬 순서를 지정하고, ASC(오름차순) 및 DESC(내림차순) 매개 변수를 포함시킬 수 있습니다.  
  
- <xref:System.Data.DataView.ApplyDefaultSort%2A> 속성을 사용하여 테이블의 기본 키 열을 기준으로 오름차순의 정렬 순서를 자동으로 만들 수 있습니다. <xref:System.Data.DataView.ApplyDefaultSort%2A>**Sort** 속성이 null 참조 또는 빈 문자열인 경우와 테이블에 기본 키가 정의 되어 있는 경우에만 적용 됩니다.  
  
- <xref:System.Data.DataView.RowFilter%2A> 속성을 사용하여 해당 열 값을 기준으로 행의 하위 집합을 지정할 수 있습니다. **RowFilter** 속성의 유효한 식에 대 한 자세한 내용은 <xref:System.Data.DataColumn.Expression%2A> <xref:System.Data.DataColumn> 클래스의 속성에 대 한 참조 정보를 참조 하세요.  
  
     데이터의 하위 집합에 대 한 동적 뷰를 제공 하는 것과는 반대로 데이터에 대 한 특정 쿼리 결과를 반환 하려는 경우에는 <xref:System.Data.DataView.Find%2A> <xref:System.Data.DataView.FindRows%2A> **DataView의 또는 메서드를 사용 하 여 RowFilter** 속성입니다. **RowFilter** 속성을 설정 하면 데이터의 인덱스가 다시 빌드되고, 응용 프로그램에 오버 헤드가 추가 되 고 성능이 저하 됩니다. **RowFilter** 속성은 바인딩된 컨트롤이 필터링 된 결과를 표시 하는 데이터 바인딩된 응용 프로그램에서 사용 하는 것이 가장 좋습니다. **Find** 및 **findrows** 메서드는 인덱스를 다시 작성할 필요 없이 현재 인덱스를 활용 합니다. **Find** 및 **findrows** 메서드에 대 한 자세한 내용은 [행 찾기](finding-rows.md)를 참조 하십시오.  
  
- <xref:System.Data.DataView.RowStateFilter%2A> 속성을 사용하면 표시할 행 버전을 지정할 수 있습니다. **DataView** 는 기본 행의 **RowState** 에 따라 노출할 행 버전을 암시적으로 관리 합니다. 예를 들어 **Rowstatefilter** 가 **DataViewRowState**로 설정 된 경우 **현재** 행 버전이 없으므로 **DataView** 는 **삭제** 된 모든 행의 **원래** 행 버전을 노출 합니다. **DataRowView**의 **RowVersion** 속성을 사용 하 여 표시 되는 행의 행 버전을 확인할 수 있습니다.  
  
     다음 표에서는 **DataViewRowState**에 대 한 옵션을 보여 줍니다.  
  
    |DataViewRowState 옵션|Description|  
    |------------------------------|-----------------|  
    |**CurrentRows**|**변경 되지 않고** **추가**되거나 **수정** 된 모든 행의 **현재** 행 버전입니다. 기본값입니다.|  
    |**강화**|**추가** 된 모든 행의 **현재** 행 버전입니다.|  
    |**Deleted**|**삭제** 된 모든 행의 **원래** 행 버전입니다.|  
    |**ModifiedCurrent**|**수정** 된 모든 행의 **현재** 행 버전입니다.|  
    |**ModifiedOriginal**|**수정** 된 모든 행의 **원래** 행 버전입니다.|  
    |**없음**|행이 없습니다.|  
    |**OriginalRows**|**변경 되지 않은**모든 행, **수정**된 행 및 **삭제** 된 행의 **원래** 행 버전입니다.|  
    |**Unchanged**|**변경 되지 않은** 모든 행의 **현재** 행 버전입니다.|  
  
 행 상태 및 행 버전에 대 한 자세한 내용은 [행 상태 및 행 버전](row-states-and-row-versions.md)을 참조 하세요.  
  
 다음 코드 예제에서는 재고 수량이 재주문 수준보다 적거나 같은 모든 제품을 표시하는 뷰를 만듭니다. 이 때 먼저 공급자 ID로 정렬한 다음 제품 이름으로 정렬하여 표시합니다.  
  
```vb  
Dim prodView As DataView = New DataView(prodDS.Tables("Products"), _  
   "UnitsInStock <= ReorderLevel", _  
   "SupplierID, ProductName", _  
   DataViewRowState.CurrentRows)  
```  
  
```csharp  
DataView prodView = new DataView(prodDS.Tables["Products"],  
   "UnitsInStock <= ReorderLevel",  
   "SupplierID, ProductName",  
   DataViewRowState.CurrentRows);  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Data.DataViewRowState>
- <xref:System.Data.DataColumn.Expression%2A?displayProperty=nameWithType>
- <xref:System.Data.DataTable>
- <xref:System.Data.DataView>
- [DataView](dataviews.md)
- [ADO.NET 개요](../ado-net-overview.md)
