---
title: 데이터 보기 관리
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0b67fab5-1722-4d2b-bfc1-247a75f0f1ee
ms.openlocfilehash: 5e85fccddf6359791ea702667a36b44f611815dc
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784498"
---
# <a name="managing-dataviews"></a>데이터 보기 관리
<xref:System.Data.DataViewManager>를 사용하여 <xref:System.Data.DataView>의 모든 테이블에 대한 뷰 설정을 관리할 수 있습니다. 관계를 탐색 하는 표와 같이 여러 테이블에 바인딩하려는 컨트롤이 있는 경우에는 **DataViewManager** 이 적합 합니다.  
  
 **DataViewManager** 에는 <xref:System.Data.DataViewSetting> <xref:System.Data.DataSet>에 있는 테이블의 뷰 설정을 설정 하는 데 사용 되는 개체의 컬렉션이 포함 되어 있습니다. 에 <xref:System.Data.DataViewSettingCollection> 는 **데이터 집합**의 각 테이블에 대 한 하나의 <xref:System.Data.DataViewSetting> 개체가 포함 되어 있습니다. 해당 **DataViewSetting**를 사용 하 여 참조 되는 테이블의 기본 **ApplyDefaultSort**, **Sort**, **RowFilter**및 **rowstatefilter** 속성을 설정할 수 있습니다. 이름 또는 서 수 참조를 기준으로 특정 테이블에 대 한 **DataViewSetting** 를 참조 하거나 해당 특정 테이블 개체에 대 한 참조를 전달할 수 있습니다. **DataViewSettings** 속성을 사용 하 여 **DataViewManager** 에서 **DataViewSetting** 개체의 컬렉션에 액세스할 수 있습니다.  
  
 다음 코드 예제에서는 SQL Server **Northwind** 데이터베이스 테이블 **고객**, **주문**및 **주문 세부 정보**를 사용 하 여 **데이터 집합** 을 채우고, 테이블 간의 관계를 만들고, **DataViewManager** 를 사용 하 여 기본 **DataView** 설정을 설정 하 고 **DataViewManager**에 **DataGrid** 를 바인딩합니다. 이 예에서는 테이블의 기본 키 (**ApplyDefaultSort** = **true**)를 기준으로 정렬 하 여 **데이터 집합** 의 모든 테이블에 대 한 기본 **DataView** 설정을 설정 하 고 **Customers** 테이블의 정렬 순서를 다음으로 수정 합니다. **CompanyName**을 기준으로 정렬 합니다.  
  
```vb  
' Assumes connection is a valid SqlConnection to Northwind.  
' Create a Connection, DataAdapters, and a DataSet.  
Dim custDA As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT CustomerID, CompanyName FROM Customers", connection)  
Dim orderDA As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT OrderID, CustomerID FROM Orders", connection)  
Dim ordDetDA As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT OrderID, ProductID, Quantity FROM [Order Details]", connection)  
  
Dim custDS As DataSet = New DataSet()  
  
' Open the Connection.  
connection.Open()  
  
    ' Fill the DataSet with schema information and data.  
    custDA.MissingSchemaAction = MissingSchemaAction.AddWithKey  
    orderDA.MissingSchemaAction = MissingSchemaAction.AddWithKey  
    ordDetDA.MissingSchemaAction = MissingSchemaAction.AddWithKey  
  
    custDA.Fill(custDS, "Customers")  
    orderDA.Fill(custDS, "Orders")  
    ordDetDA.Fill(custDS, "OrderDetails")  
  
    ' Close the Connection.  
    connection.Close()  
  
    ' Create relationships.  
    custDS.Relations.Add("CustomerOrders", _  
          custDS.Tables("Customers").Columns("CustomerID"), _  
          custDS.Tables("Orders").Columns("CustomerID"))  
  
    custDS.Relations.Add("OrderDetails", _  
          custDS.Tables("Orders").Columns("OrderID"), _  
          custDS.Tables("OrderDetails").Columns("OrderID"))  
  
' Create default DataView settings.  
Dim viewManager As DataViewManager = New DataViewManager(custDS)  
  
Dim viewSetting As DataViewSetting  
For Each viewSetting In viewManager.DataViewSettings  
  viewSetting.ApplyDefaultSort = True  
Next  
  
viewManager.DataViewSettings("Customers").Sort = "CompanyName"  
  
' Bind to a DataGrid.  
Dim grid As System.Windows.Forms.DataGrid = New System.Windows.Forms.DataGrid()  
grid.SetDataBinding(viewManager, "Customers")  
```  
  
```csharp  
// Assumes connection is a valid SqlConnection to Northwind.  
// Create a Connection, DataAdapters, and a DataSet.  
SqlDataAdapter custDA = new SqlDataAdapter(  
  "SELECT CustomerID, CompanyName FROM Customers", connection);  
SqlDataAdapter orderDA = new SqlDataAdapter(  
  "SELECT OrderID, CustomerID FROM Orders", connection);  
SqlDataAdapter ordDetDA = new SqlDataAdapter(  
  "SELECT OrderID, ProductID, Quantity FROM [Order Details]", connection);  
  
DataSet custDS = new DataSet();  
  
// Open the Connection.  
connection.Open();  
  
    // Fill the DataSet with schema information and data.  
    custDA.MissingSchemaAction = MissingSchemaAction.AddWithKey;  
    orderDA.MissingSchemaAction = MissingSchemaAction.AddWithKey;  
    ordDetDA.MissingSchemaAction = MissingSchemaAction.AddWithKey;  
  
    custDA.Fill(custDS, "Customers");  
    orderDA.Fill(custDS, "Orders");  
    ordDetDA.Fill(custDS, "OrderDetails");  
  
    // Close the Connection.  
    connection.Close();  
  
    // Create relationships.  
    custDS.Relations.Add("CustomerOrders",  
          custDS.Tables["Customers"].Columns["CustomerID"],  
          custDS.Tables["Orders"].Columns["CustomerID"]);  
  
    custDS.Relations.Add("OrderDetails",  
          custDS.Tables["Orders"].Columns["OrderID"],  
          custDS.Tables["OrderDetails"].Columns["OrderID"]);  
  
// Create default DataView settings.  
DataViewManager viewManager = new DataViewManager(custDS);  
  
foreach (DataViewSetting viewSetting in viewManager.DataViewSettings)  
  viewSetting.ApplyDefaultSort = true;  
  
viewManager.DataViewSettings["Customers"].Sort = "CompanyName";  
  
// Bind to a DataGrid.  
System.Windows.Forms.DataGrid grid = new System.Windows.Forms.DataGrid();  
grid.SetDataBinding(viewManager, "Customers");  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Data.DataSet>
- <xref:System.Data.DataViewManager>
- <xref:System.Data.DataViewSetting>
- <xref:System.Data.DataViewSettingCollection>
- [DataView](dataviews.md)
- [ADO.NET 개요](../ado-net-overview.md)
