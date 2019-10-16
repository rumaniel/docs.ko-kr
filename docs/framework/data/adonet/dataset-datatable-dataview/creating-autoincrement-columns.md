---
title: AutoIncrement 열 만들기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: cf09732a-ab54-4d98-89e2-4d0a1f28fbce
ms.openlocfilehash: 5e4a36829107480a44980c7210b39c21231c67f4
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786446"
---
# <a name="creating-autoincrement-columns"></a>AutoIncrement 열 만들기
열에 고유 값을 지정하려면 테이블에 새 행을 추가할 때 열 값이 자동으로 증가하도록 설정합니다. 자동 증분 <xref:System.Data.DataColumn>을 만들려면 열의 <xref:System.Data.DataColumn.AutoIncrement%2A> 속성을 **true**로 설정 합니다. 그런 <xref:System.Data.DataColumn> 다음은 <xref:System.Data.DataColumn.AutoIncrementSeed%2A> 속성에 정의 된 값으로 시작 하 고, 각 행을 추가 하 여 **AutoIncrement** 열의 값이 열의 <xref:System.Data.DataColumn.AutoIncrementStep%2A> 속성에 정의 된 값 만큼 증가 합니다.  
  
 **AutoIncrement** 열의 경우 <xref:System.Data.DataColumn.ReadOnly%2A> **DataColumn** 의 속성을 **true**로 설정 하는 것이 좋습니다.  
  
 다음 예제에서는 200으로 시작하여 3씩 증가하여 추가되는 열을 만드는 방법을 보여 줍니다.  
  
```vb  
Dim workColumn As DataColumn = workTable.Columns.Add( _  
    "CustomerID", typeof(Int32))  
workColumn.AutoIncrement = true  
workColumn.AutoIncrementSeed = 200  
workColumn.AutoIncrementStep = 3  
```  
  
```csharp  
DataColumn workColumn = workTable.Columns.Add(  
    "CustomerID", typeof(Int32));  
workColumn.AutoIncrement = true;  
workColumn.AutoIncrementSeed = 200;  
workColumn.AutoIncrementStep = 3;  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Data.DataColumn>
- [DataTable 스키마 정의](datatable-schema-definition.md)
- [DataTable](datatables.md)
- [ADO.NET 개요](../ado-net-overview.md)
