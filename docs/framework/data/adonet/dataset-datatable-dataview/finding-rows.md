---
title: 행 찾기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5da300e2-74c0-4d13-9202-fc20ed8212d8
ms.openlocfilehash: ad10557a55b498fe004bff6ce89801e975e7138b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786322"
---
# <a name="finding-rows"></a>행 찾기
<xref:System.Data.DataView.Find%2A>의 <xref:System.Data.DataView.FindRows%2A> 및 <xref:System.Data.DataView> 메서드를 사용하여 행의 정렬 키 값에 따라 행을 검색할 수 있습니다. **Find** 및 **findrows** 메서드에서 검색 값의 대/소문자 구분은 기본 <xref:System.Data.DataTable>의 **CaseSensitive** 속성에 의해 결정 됩니다. 검색 값이 기존 정렬 키 값 전체와 일치해야 결과를 반환할 수 있습니다.  
  
 **Find** 메서드는 검색 조건과 일치 <xref:System.Data.DataRowView> 하는의 인덱스와 함께 정수를 반환 합니다. 검색 조건과 일치 하는 행이 두 개 이상 있으면 첫 번째 일치 하는 **DataRowView** 의 인덱스만 반환 됩니다. 일치 하는 항목이 없으면 **Find** 는-1을 반환 합니다.  
  
 여러 행과 일치 하는 검색 결과를 반환 하려면 **Findrows** 메서드를 사용 합니다. **Findrows** 는 **DataView**에서 일치 하는 모든 행을 참조 하는 **DataRowView** 배열을 반환 한다는 점을 제외 하 고 **Find** 메서드와 똑같이 작동 합니다. 일치 하는 항목이 없으면 **DataRowView** 배열이 비어 있게 됩니다.  
  
 **Find** 또는 **findrows** 메서드를 사용 하려면 **ApplyDefaultSort** 를 **true** 로 설정 하거나 **sort** 속성을 사용 하 여 정렬 순서를 지정 해야 합니다. 정렬 순서를 지정하지 않으면 예외가 throw됩니다.  
  
 **Find** 및 **findrows** 메서드는 값 배열을 입력으로 사용 합니다 .이 값의 길이는 정렬 순서의 열 수와 일치 합니다. 하나의 열에 대해 정렬하는 경우에는 하나의 값을 전달할 수 있습니다. 정렬 순서에 여러 열이 포함된 경우에는 개체 배열을 전달합니다. 여러 열에 대해 정렬 하는 경우 개체 배열의 값은 **DataView**의 **sort** 속성에 지정 된 열의 순서와 일치 해야 합니다.  
  
 다음 코드 예제에서는 단일 열 정렬 순서를 사용 하 여 **DataView** 에 대해 호출 되는 **Find** 메서드를 보여 줍니다.  
  
```vb  
Dim custView As DataView = _  
  New DataView(custDS.Tables("Customers"), "", _  
  "CompanyName", DataViewRowState.CurrentRows)  
  
Dim rowIndex As Integer = custView.Find("The Cracker Box")  
  
If rowIndex = -1 Then  
  Console.WriteLine("No match found.")  
Else  
  Console.WriteLine("{0}, {1}", _  
    custView(rowIndex)("CustomerID").ToString(), _  
    custView(rowIndex)("CompanyName").ToString())  
End If  
```  
  
```csharp  
DataView custView = new DataView(custDS.Tables["Customers"], "",   
  "CompanyName", DataViewRowState.CurrentRows);  
  
int rowIndex = custView.Find("The Cracker Box");  
  
if (rowIndex == -1)  
  Console.WriteLine("No match found.");  
else  
  Console.WriteLine("{0}, {1}",  
    custView[rowIndex]["CustomerID"].ToString(),  
    custView[rowIndex]["CompanyName"].ToString());  
```  
  
 **Sort** 속성이 여러 열을 지정 하는 경우 다음 코드 예제와 같이 **sort** 속성에 지정 된 순서에 따라 각 열에 대 한 검색 값을 사용 하 여 개체 배열을 전달 해야 합니다.  
  
```vb  
Dim custView As DataView = _  
  New DataView(custDS.Tables("Customers"), "", _  
  "CompanyName, ContactName", _  
  DataViewRowState.CurrentRows)  
  
Dim foundRows() As DataRowView = _  
  custView.FindRows(New object() {"The Cracker Box", "Liu Wong"})  
  
If foundRows.Length = 0 Then  
  Console.WriteLine("No match found.")  
Else  
  Dim myDRV As DataRowView  
  For Each myDRV In foundRows  
    Console.WriteLine("{0}, {1}", _  
      myDRV("CompanyName").ToString(), myDRV("ContactName").ToString())  
  Next  
End If  
```  
  
```csharp  
DataView custView = new DataView(custDS.Tables["Customers"], "",  
  "CompanyName, ContactName",  
  DataViewRowState.CurrentRows);  
  
DataRowView[] foundRows =   
  custView.FindRows(new object[] {"The Cracker Box", "Liu Wong"});  
  
if (foundRows.Length == 0)  
  Console.WriteLine("No match found.");  
else  
  foreach (DataRowView myDRV in foundRows)  
    Console.WriteLine("{0}, {1}", myDRV["CompanyName"].ToString(),   
      myDRV["ContactName"].ToString());  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Data.DataTable>
- <xref:System.Data.DataView>
- [DataView](dataviews.md)
- [ADO.NET 개요](../ado-net-overview.md)
