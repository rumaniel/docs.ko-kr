---
title: DataTable에 데이터 추가
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d6aa8474-7bde-48f7-949d-20dc38a1625b
ms.openlocfilehash: 2a001ac8b3d4b8cd9618b3ced7bdf578ebae2e22
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786599"
---
# <a name="adding-data-to-a-datatable"></a>DataTable에 데이터 추가
<xref:System.Data.DataTable>을 만들고 열 및 제약 조건을 사용하여 해당 테이블의 구조를 정의한 후에는 새 데이터 행을 테이블에 추가할 수 있습니다. 새 행을 추가하려면 새 변수의 형식을 <xref:System.Data.DataRow>로 선언합니다. 메서드를 <xref:System.Data.DataTable.NewRow%2A> 호출 하면 새 DataRow 개체가 반환 됩니다. 그런 다음 **DataTable** 은에 <xref:System.Data.DataColumnCollection>정의 된 대로 테이블의 구조를 기반으로 DataRow 개체를 만듭니다.  
  
 다음 예제에서는 **NewRow** 메서드를 호출 하 여 새 행을 만드는 방법을 보여 줍니다.  
  
```vb  
Dim workRow As DataRow = workTable.NewRow()  
```  
  
```csharp  
DataRow workRow = workTable.NewRow();  
```  
  
 그러면 다음 예제와 같이 인덱스나 열 이름을 사용하여 새로 추가된 행을 조작할 수 있습니다.  
  
```vb  
workRow("CustLName") = "Smith"  
workRow(1) = "Smith"  
```  
  
```csharp  
workRow["CustLName"] = "Smith";  
workRow[1] = "Smith";  
```  
  
 새 행에 데이터를 삽입 한 후에는 다음 코드에 나와 있는 것 처럼 **add** 메서드를 <xref:System.Data.DataRowCollection>사용 하 여에 행을 추가 합니다.  
  
```vb  
workTable.Rows.Add(workRow)  
```  
  
```csharp  
workTable.Rows.Add(workRow);  
```  
  
 다음 예제와 같이 **Add** 메서드를 호출 하 여로 <xref:System.Object>형식화 된 값의 배열을 전달 하 여 새 행을 추가할 수도 있습니다.  
  
```vb  
workTable.Rows.Add(new Object() {1, "Smith"})  
```  
  
```csharp  
workTable.Rows.Add(new Object[] {1, "Smith"});  
```  
  
 **Object**로 형식화 된 값 배열을 **Add** 메서드에 전달 하면 테이블 안에 새 행이 생성 되 고 해당 열 값이 개체 배열의 값으로 설정 됩니다. 배열 값은 테이블에 나타나는 순서에 따라 해당 열과 순서대로 대응합니다.  
  
 다음 예에서는 새로 만든 **Customers** 테이블에 10 개의 행을 추가 합니다.  
  
```vb  
Dim workRow As DataRow  
Dim i As Integer  
  
For i = 0 To 9  
  workRow = workTable.NewRow()  
  workRow(0) = i  
  workRow(1) = "CustName" & I.ToString()  
  workTable.Rows.Add(workRow)  
Next  
```  
  
```csharp  
DataRow workRow;  
  
for (int i = 0; i <= 9; i++)   
{  
  workRow = workTable.NewRow();  
  workRow[0] = i;  
  workRow[1] = "CustName" + i.ToString();  
  workTable.Rows.Add(workRow);  
}  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Data.DataColumnCollection>
- <xref:System.Data.DataRow>
- <xref:System.Data.DataRowCollection>
- <xref:System.Data.DataTable>
- [DataTable에서 데이터 조작](manipulating-data-in-a-datatable.md)
- [ADO.NET 개요](../ado-net-overview.md)
