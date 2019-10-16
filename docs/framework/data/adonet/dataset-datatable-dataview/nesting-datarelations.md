---
title: DataRelation 중첩
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 9530f9c9-dd98-4b93-8cdb-40d7f1e8d0ab
ms.openlocfilehash: 971a1bddc40521dc7381ecb2e39709c0fed282ed
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785988"
---
# <a name="nesting-datarelations"></a>DataRelation 중첩
데이터의 관계형 표현에서 각 테이블에는 열이나 열 집합을 사용하여 서로 연결시키는 행이 포함되어 있습니다. ADO.NET <xref:System.Data.DataSet>에서 각 테이블 사이의 관계는 <xref:System.Data.DataRelation>을 사용하여 구현됩니다. **DataRelation**을 만들 때 열의 부모-자식 관계는 관계를 통해서만 관리 됩니다. 테이블과 열은 별개의 엔터티입니다. XML에서 제공하는 데이터의 계층적 표현에서 부모-자식 관계는 중첩된 자식 요소를 포함하는 부모 요소에 의해 표현됩니다.  
  
 **데이터 집합이** 와 <xref:System.Xml.XmlDataDocument> 동기화 되거나 **WriteXml**을 사용 하 여 XML 데이터로 작성 되는 경우 자식 개체의 중첩을 용이 하 게 하기 위해 **DataRelation** 은 **중첩** 된 속성을 노출 합니다. **DataRelation** 의 **Nested** 속성을 **true** 로 설정 하면 XML 데이터로 작성 되거나 **XmlDataDocument**와 동기화 될 때 관계의 자식 행이 부모 열에 중첩 됩니다. **DataRelation** 의 **Nested** 속성은 기본적으로 **false**입니다.  
  
 예를 들어 다음 **데이터 집합**을 고려 합니다.  
  
```vb  
' Assumes connection is a valid SqlConnection.  
Dim customerAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT CustomerID, CompanyName FROM Customers", connection)  
Dim orderAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT OrderID, CustomerID, OrderDate FROM Orders", connection)  
  
connection.Open()  
  
Dim dataSet As DataSet = New DataSet("CustomerOrders")  
customerAdapter.Fill(dataSet, "Customers")  
orderAdapter.Fill(dataSet, "Orders")  
  
connection.Close()  
  
Dim customerOrders As DataRelation = dataSet.Relations.Add( _  
  "CustOrders", dataSet.Tables("Customers").Columns("CustomerID"), _  
  dataSet.Tables("Orders").Columns("CustomerID"))  
```  
  
```csharp  
// Assumes connection is a valid SqlConnection.  
SqlDataAdapter customerAdapter = new SqlDataAdapter(  
  "SELECT CustomerID, CompanyName FROM Customers", connection);  
SqlDataAdapter orderAdapter = new SqlDataAdapter(  
  "SELECT OrderID, CustomerID, OrderDate FROM Orders", connection);  
  
connection.Open();  
  
DataSet dataSet = new DataSet("CustomerOrders");  
customerAdapter.Fill(dataSet, "Customers");  
orderAdapter.Fill(dataSet, "Orders");  
  
connection.Close();  
  
DataRelation customerOrders = dataSet.Relations.Add(  
  "CustOrders", dataSet.Tables["Customers"].Columns["CustomerID"],  
  dataSet.Tables["Orders"].Columns["CustomerID"]);  
```  
  
 **DataRelation** 개체의 **Nested** **속성이이 데이터 집합에**대해 **true** 로 설정 되어 있지 않기 때문에이 데이터 **집합이** XML 데이터로 표현 될 때 자식 개체는 부모 요소 내에 중첩 되지 않습니다. 관련 데이터 **집합**을 포함 하는 데이터 **집합** 의 XML 표현을 중첩 되지 않은 데이터 관계로 변환 하면 성능이 저하 될 수 있습니다. 데이터 관계를 중첩하는 것이 좋습니다. 이렇게 하려면 **Nested** 속성을 **true**로 설정 합니다. 그런 다음 XSLT 스타일시트에서 하향 계층 구조적인 XPath 쿼리 식을 사용하여 데이터를 찾고 변환하는 코드를 작성합니다.  
  
 다음 코드 예제에서는 **데이터 집합**에 대해 **WriteXml** 를 호출한 결과를 보여 줍니다.  
  
```xml  
<CustomerOrders>  
  <Customers>  
    <CustomerID>ALFKI</CustomerID>  
    <CompanyName>Alfreds Futterkiste</CompanyName>  
  </Customers>  
  <Customers>  
    <CustomerID>ANATR</CustomerID>  
    <CompanyName>Ana Trujillo Emparedados y helados</CompanyName>  
  </Customers>  
  <Orders>  
    <OrderID>10643</OrderID>  
    <CustomerID>ALFKI</CustomerID>  
    <OrderDate>1997-08-25T00:00:00</OrderDate>  
  </Orders>  
  <Orders>  
    <OrderID>10692</OrderID>  
    <CustomerID>ALFKI</CustomerID>  
    <OrderDate>1997-10-03T00:00:00</OrderDate>  
  </Orders>  
  <Orders>  
    <OrderID>10308</OrderID>  
    <CustomerID>ANATR</CustomerID>  
    <OrderDate>1996-09-18T00:00:00</OrderDate>  
  </Orders>  
</CustomerOrders>  
```  
  
 **Customers** 요소와 **Orders** 요소는 형제 요소로 표시 됩니다. **Orders** 요소가 해당 부모 요소의 자식으로 표시 되도록 하려면 **DataRelation** 의 **Nested** 속성을 **true** 로 설정 하 고 다음을 추가 해야 합니다.  
  
```vb  
customerOrders.Nested = True  
```  
  
```csharp  
customerOrders.Nested = true;  
```  
  
 다음 코드에서는 결과 출력이 표시 되는 모양을 보여 줍니다. **Orders** 요소는 해당 부모 요소 내에 중첩 됩니다.  
  
```xml  
<CustomerOrders>  
  <Customers>  
    <CustomerID>ALFKI</CustomerID>  
    <Orders>  
      <OrderID>10643</OrderID>  
      <CustomerID>ALFKI</CustomerID>  
      <OrderDate>1997-08-25T00:00:00</OrderDate>  
    </Orders>  
    <Orders>  
      <OrderID>10692</OrderID>  
      <CustomerID>ALFKI</CustomerID>  
      <OrderDate>1997-10-03T00:00:00</OrderDate>  
    </Orders>  
    <CompanyName>Alfreds Futterkiste</CompanyName>  
  </Customers>  
  <Customers>  
    <CustomerID>ANATR</CustomerID>  
    <Orders>  
      <OrderID>10308</OrderID>  
      <CustomerID>ANATR</CustomerID>  
      <OrderDate>1996-09-18T00:00:00</OrderDate>  
    </Orders>  
    <CompanyName>Ana Trujillo Emparedados y helados</CompanyName>  
  </Customers>  
</CustomerOrders>  
```  
  
## <a name="see-also"></a>참고자료

- [데이터 집합에서 XML 사용](using-xml-in-a-dataset.md)
- [DataRelation 추가](adding-datarelations.md)
- [DataSet, DataTable 및 DataView](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
