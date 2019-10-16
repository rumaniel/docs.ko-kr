---
title: 데이터 세트 콘텐츠 복사
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: cb846617-2b1a-44ff-bd7f-5835f5ea37fa
ms.openlocfilehash: d8a7762c4ec5d650295ca0626180285723549051
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786521"
---
# <a name="copying-dataset-contents"></a>데이터 세트 콘텐츠 복사
원본 데이터에 영향을 주지 않고 <xref:System.Data.DataSet> 데이터 작업을 수행 하거나 데이터 **집합**에서 데이터의 하위 집합을 사용 하 여 작업을 수행할 수 있도록의 복사본을 만들 수 있습니다. **데이터 집합**을 복사할 때 다음을 수행할 수 있습니다.  
  
- 스키마, 데이터, 행 상태 정보 및 행 버전을 포함 하 여 **데이터 집합**의 정확한 복사본을 만듭니다.  
  
- 기존 **데이터 집합**의 스키마를 포함 하지만 수정 된 행만 포함 하는 **데이터 집합** 을 만듭니다. 수정 된 모든 행을 반환 하거나 특정 **DataRowState**을 지정할 수 있습니다. 행 상태에 대 한 자세한 내용은 [행 상태 및 행 버전](row-states-and-row-versions.md)을 참조 하세요.  
  
- 행을 복사 하지 않고 **데이터 집합** 의 스키마 또는 관계형 구조만 복사 합니다. <xref:System.Data.DataTable>를 사용하여 행을 기존 <xref:System.Data.DataTable.ImportRow%2A>로 가져올 수 있습니다.  
  
 스키마와 데이터를 모두 포함 하는 데이터 **집합** 의 정확한 복사본을 만들려면 <xref:System.Data.DataSet.Copy%2A> **데이터 집합**의 메서드를 사용 합니다. 다음 코드 예제에서는 **데이터 집합**의 정확한 복사본을 만드는 방법을 보여 줍니다.  
  
```vb  
Dim copyDataSet As DataSet = customerDataSet.Copy()  
```  
  
```csharp  
DataSet copyDataSet = customerDataSet.Copy();  
```  
  
 스키마를 포함 하 고 **추가**, **수정**또는 **삭제** 된 행을 나타내는 데이터만 포함 하는 데이터 <xref:System.Data.DataSet.GetChanges%2A> **집합** 의 복사본을 만들려면 **데이터 집합**의 메서드를 사용 합니다. **GetChanges** 를 사용 하 여 **GetChanges**를 호출할 때 **DataRowState** 값을 전달 하 여 지정 된 행 상태의 행만 반환할 수도 있습니다. 다음 코드 예제에서는 **GetChanges**를 호출할 때 **DataRowState** 를 전달 하는 방법을 보여 줍니다.  
  
```vb  
' Copy all changes.  
Dim changeDataSet As DataSet = customerDataSet.GetChanges()  
' Copy only new rows.  
Dim addedDataSetAs DataSet = _  
    customerDataSet.GetChanges(DataRowState.Added)  
```  
  
```csharp  
// Copy all changes.  
DataSet changeDataSet = customerDataSet.GetChanges();  
// Copy only new rows.  
DataSet addedDataSet= customerDataSet.GetChanges(DataRowState.Added);  
```  
  
 스키마만 포함 하는 **데이터 집합** 의 복사본을 만들려면 **dataset**의 메서드 <xref:System.Data.DataSet.Clone%2A> 를 사용 합니다. 또한 **DataTable**의 **ImportRow** 메서드를 사용 하 여 복제 된 **데이터 집합** 에 기존 행을 추가할 수 있습니다. **ImportRow** 는 지정 된 테이블에 데이터, 행 상태 및 행 버전 정보를 추가 합니다. 열 값은 열 이름이 일치하고 데이터 형식이 호환되는 위치에만 추가됩니다.  
  
 다음 코드 예에서는 **데이터 집합** 의 복제본을 만든 다음 원래 **데이터 집합** 의 행을 **CountryRegion** 열 값이 "독일" 인 고객에 대 한 **데이터 집합** 복제본의 **customers** 테이블에 추가 합니다. ".  
  
```vb  
Dim customerDataSet As New DataSet  
        customerDataSet.Tables.Add(New DataTable("Customers"))  
        customerDataSet.Tables("Customers").Columns.Add("Name", GetType(String))  
        customerDataSet.Tables("Customers").Columns.Add("CountryRegion", GetType(String))  
        customerDataSet.Tables("Customers").Rows.Add("Juan", "Spain")  
        customerDataSet.Tables("Customers").Rows.Add("Johann", "Germany")  
        customerDataSet.Tables("Customers").Rows.Add("John", "UK")  
  
Dim germanyCustomers As DataSet = customerDataSet.Clone()  
  
Dim copyRows() As DataRow = _  
  customerDataSet.Tables("Customers").Select("CountryRegion = 'Germany'")  
  
Dim customerTable As DataTable = germanyCustomers.Tables("Customers")  
Dim copyRow As DataRow  
  
For Each copyRow In copyRows  
  customerTable.ImportRow(copyRow)  
Next  
```  
  
```csharp  
DataSet customerDataSet = new DataSet();  
customerDataSet.Tables.Add(new DataTable("Customers"));  
customerDataSet.Tables["Customers"].Columns.Add("Name", typeof(string));  
customerDataSet.Tables["Customers"].Columns.Add("CountryRegion", typeof(string));  
customerDataSet.Tables["Customers"].Rows.Add("Juan", "Spain");  
customerDataSet.Tables["Customers"].Rows.Add("Johann", "Germany");  
customerDataSet.Tables["Customers"].Rows.Add("John", "UK");  
  
DataSet germanyCustomers = customerDataSet.Clone();  
  
DataRow[] copyRows =   
  customerDataSet.Tables["Customers"].Select("CountryRegion = 'Germany'");  
  
DataTable customerTable = germanyCustomers.Tables["Customers"];  
  
foreach (DataRow copyRow in copyRows)  
  customerTable.ImportRow(copyRow);  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Data.DataSet>
- <xref:System.Data.DataTable>
- [DataSet, DataTable 및 DataView](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
