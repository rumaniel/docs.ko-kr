---
title: 데이터 보기 수정
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 697a3991-b660-4a5a-8a54-1a2304ff158e
ms.openlocfilehash: 3e811410ea9fdd4be0cbd84b895483f69f58b0d0
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786050"
---
# <a name="modifying-dataviews"></a>데이터 보기 수정
<xref:System.Data.DataView>를 사용하여 원본 테이블의 데이터 행을 추가, 삭제 또는 수정할 수 있습니다. **Dataview를** 사용 하 여 기본 테이블의 데이터를 수정 하는 기능은 **dataview**의 세 가지 부울 속성 중 하나를 설정 하 여 제어 됩니다. 이러한 속성에는 <xref:System.Data.DataView.AllowNew%2A>, <xref:System.Data.DataView.AllowEdit%2A> 및 <xref:System.Data.DataView.AllowDelete%2A>가 있습니다. 기본적으로 **true** 로 설정 됩니다.  
  
 **AllowNew** 가 **true**인 경우 <xref:System.Data.DataView.AddNew%2A> **DataView** 의 메서드를 사용 하 여 새 <xref:System.Data.DataRowView>를 만들 수 있습니다. <xref:System.Data.DataTable> **DataRowView** 의 <xref:System.Data.DataRowView.EndEdit%2A> 메서드가 호출 될 때까지 새 행은 실제로 내부에 추가 되지 않습니다. <xref:System.Data.DataRowView.CancelEdit%2A> **DataRowView** 의 메서드를 호출 하면 새 행이 삭제 됩니다. 또한 한 번에 하나의 **DataRowView** 편집할 수 있습니다. 보류 중인 행이 있는 동안 **DataRowView** 의 **AddNew** 또는 **BeginEdit** 메서드를 호출 하면 보류 중인 행에서 **EndEdit** 가 암시적으로 호출 됩니다. **EndEdit** 가 호출 되 면 변경 내용이 기본 **datatable** 에 적용 되며, 나중에 **Datatable**, **DataSet** **또는의 AcceptChanges 또는 RejectChanges 메서드를 사용 하 여 커밋하거나 거부할 수 있습니다. DataRow** 개체입니다. **AllowNew** 가 **false**이면 **DataRowView**의 **AddNew** 메서드를 호출 하면 예외가 throw 됩니다.  
  
 **Allowedit** 이 **True**인 경우 **DataRowView**을 통해 **DataRow** 의 내용을 수정할 수 있습니다. EndEdit를 사용 하 여 기본 행의 변경 내용을 확인 하거나 **DataRowView**를 사용 하 여 변경 내용을 **DataRowView** 수 있습니다. 행은 한 번에 하나씩만 편집할 수 있습니다. 보류 중인 행이 있는 동안 **DataRowView** 의 **AddNew** 또는 **BeginEdit** 메서드를 호출 하는 경우 **EndEdit** 는 보류 중인 행에서 암시적으로 호출 됩니다. **EndEdit** 가 호출 되 면 제안 된 변경 내용이 기본 **DataRow** 의 **현재** 행 버전에 배치 되 고, 나중에의 **AcceptChanges** 또는 **RejectChanges** 메서드 **를 사용 하 여 커밋하거나 거부할 수 있습니다. DataTable**, **DataSet**또는 **DataRow** 개체입니다. **Allowedit** 이 **False**인 경우 **DataView**에서 값을 수정 하려고 하면 예외가 throw 됩니다.  
  
 기존 **DataRowView** 을 편집 하는 경우 기본 **DataTable** 의 이벤트는 제안 된 변경 내용으로 계속 발생 합니다. 기본 **DataRow**에서 **EndEdit** 또는 **CancelEdit** 를 호출 하면 **DataRowView**에서 **EndEdit** 또는 **CancelEdit** 가 호출 되었는지 여부에 관계 없이 보류 중인 변경 내용이 적용 되거나 취소 됩니다.  
  
 **Allowdelete** 가 **True**인 경우 **Dataview** 또는 **DataRowView** 개체의 **delete** 메서드를 사용 하 여 **dataview** 에서 행을 삭제할 수 있으며 행은 기본 **DataTable**에서 삭제 됩니다. 나중에 **AcceptChanges** 또는 **RejectChanges** 를 사용 하 여 삭제를 커밋하거나 거부할 수 있습니다. **Allowdelete** 가 **False**인 경우 **DataView** 또는 **DataRowView**의 **Delete** 메서드를 호출 하면 예외가 throw 됩니다.  
  
 다음 코드 예제 **에서는 dataview를** 사용 하 여 행을 삭제 하 고 **dataview**를 사용 하 여 기본 테이블에 새 행을 추가 합니다.  
  
```vb  
Dim custTable As DataTable = custDS.Tables("Customers")  
Dim custView As DataView = custTable.DefaultView  
custView.Sort = "CompanyName"  
  
custView.AllowDelete = False  
  
Dim newDRV As DataRowView = custView.AddNew()  
newDRV("CustomerID") = "ABCDE"  
newDRV("CompanyName") = "ABC Products"  
newDRV.EndEdit()  
```  
  
```csharp  
DataTable custTable = custDS.Tables["Customers"];  
DataView custView = custTable.DefaultView;  
custView.Sort = "CompanyName";  
  
custView.AllowDelete = false;  
  
DataRowView newDRV = custView.AddNew();  
newDRV["CustomerID"] = "ABCDE";  
newDRV["CompanyName"] = "ABC Products";  
newDRV.EndEdit();  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Data.DataTable>
- <xref:System.Data.DataView>
- <xref:System.Data.DataRowView>
- [DataView](dataviews.md)
- [ADO.NET 개요](../ado-net-overview.md)
