---
title: 기본 키 정의
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2ea85959-e763-4669-8bd9-46a9dab894bd
ms.openlocfilehash: 0f87b1b730eecf0edad75bd87ca8b491b96e1d2b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784715"
---
# <a name="defining-primary-keys"></a>기본 키 정의
일반적으로 데이터베이스 테이블에는 테이블의 각 행을 고유하게 식별하는 열 또는 열 그룹이 있습니다. 이 식별 열 또는 열 그룹을 기본 키라고 합니다.  
  
 <xref:System.Data.DataColumn> 단일를의 <xref:System.Data.DataTable.PrimaryKey%2A> <xref:System.Data.DataColumn.AllowDBNull%2A> <xref:System.Data.DataColumn.Unique%2A> 로 <xref:System.Data.DataTable>식별 하면 테이블에서 자동으로 열의 속성을 **false** 로 설정 하 고 속성을 **true**로 설정 합니다. 여러 열로 된 기본 키의 경우 **Allowdbnull** 속성만 자동으로 **false**로 설정 됩니다.  
  
 의 **PrimaryKey 속성** 은 다음 예제와 같이 하나 이상의 DataColumn 개체 배열을 값으로 받습니다.<xref:System.Data.DataTable> 첫 번째 예제에서는 단일 열이 기본 키로 정의됩니다.  
  
```vb  
workTable.PrimaryKey = New DataColumn() {workTable.Columns("CustID")}  
  
' Or  
  
Dim columns(1) As DataColumn  
columns(0) = workTable.Columns("CustID")  
workTable.PrimaryKey = columns  
```  
  
```csharp  
workTable.PrimaryKey = new DataColumn[] {workTable.Columns["CustID"]};  
  
// Or  
  
DataColumn[] columns = new DataColumn[1];  
columns[0] = workTable.Columns["CustID"];  
workTable.PrimaryKey = columns;  
```  
  
 다음 예제에서는 두 열이 기본 키로 정의됩니다.  
  
```vb  
workTable.PrimaryKey = New DataColumn() {workTable.Columns("CustLName"), _  
                                         workTable.Columns("CustFName")}  
  
' Or  
  
Dim keyColumn(2) As DataColumn  
keyColumn(0) = workTable.Columns("CustLName")  
keyColumn(1) = workTable.Columns("CustFName")  
workTable.PrimaryKey = keyColumn  
```  
  
```csharp  
workTable.PrimaryKey = new DataColumn[] {workTable.Columns["CustLName"],   
                                         workTable.Columns["CustFName"]};  
  
// Or  
  
DataColumn[] keyColumn = new DataColumn[2];  
keyColumn[0] = workTable.Columns["CustLName"];  
keyColumn[1] = workTable.Columns["CustFName"];  
workTable.PrimaryKey = keyColumn;  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Data.DataTable>
- [DataTable 스키마 정의](datatable-schema-definition.md)
- [DataTable](datatables.md)
- [ADO.NET 개요](../ado-net-overview.md)
