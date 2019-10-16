---
title: 형식화된 데이터 세트에 주석 지정
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f82aaa62-321e-4c8a-b51b-9d1114700170
ms.openlocfilehash: 351175b96d354a264a9280018ce21de8870beda2
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784797"
---
# <a name="annotating-typed-datasets"></a>형식화된 데이터 세트에 주석 지정
주석을 사용하면 원본으로 사용하는 스키마를 수정하지 않고 형식화된 <xref:System.Data.DataSet>의 요소 이름을 수정할 수 있습니다. 기본 스키마의 요소 이름을 수정 하면 형식화 된 데이터 **집합이** 데이터 소스에 없는 개체를 참조 하 고 데이터 소스에 존재 하는 개체에 대 한 참조도 손실 됩니다.  
  
 주석을 사용 하 여 형식화 된 **데이터 집합** 의 개체 이름을 더 의미 있는 이름으로 사용자 지정 하 여, 클라이언트에서 사용할 수 있는 코드를 더 쉽게 읽고 형식화 된 **데이터 집합** 을 쉽게 만들 수 있습니다. 기본 스키마는 그대로 유지 됩니다. 예를 들어 **Northwind** 데이터베이스의 **Customers** 테이블에 대 한 다음 스키마 요소는 **customersrow** 및 <xref:System.Data.DataRowCollection> 명명 된 **고객**의 **DataRow** 개체 이름을 생성 합니다.  
  
```xml  
<xs:element name="Customers">  
  <xs:complexType>  
    <xs:sequence>  
      <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
    </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 **고객** 의 **DataRowCollection** 이름은 클라이언트 코드에서 의미가 있지만 **customersrow** 의 **DataRow** 이름은 단일 개체 이기 때문에 잘못 된 것입니다. 또한 일반적인 시나리오에서 개체를 **행** 식별자 없이 참조 하 고 대신 **고객** 개체 라고 합니다. 이 솔루션은 스키마에 주석을 달고 **DataRow** 및 **DataRowCollection** 개체의 새 이름을 식별 하는 것입니다. 다음 코드는 이전 스키마에 주석을 단 것입니다.  
  
```xml  
<xs:element name="Customers" codegen:typedName="Customer" codegen:typedPlural="Customers">  
  <xs:complexType>  
    <xs:sequence>  
      <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
    </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 **Customer** 의 **typedName** 값을 지정 하면 **DataRow** 개체 이름이 **customer**가 됩니다. **고객** 의 **typedPlural** 값을 지정 하면 **고객**의 **DataRowCollection** 이름이 유지 됩니다.  
  
 다음 표에서는 사용할 수 있는 주석을 보여 줍니다.  
  
|Annotation|Description|  
|----------------|-----------------|  
|**typedName**|개체의 이름입니다.|  
|**typedPlural**|개체 컬렉션의 이름입니다.|  
|**typedParent**|부모 관계에서 참조될 때의 개체 이름입니다.|  
|**typedChildren**|자식 관계에서 개체를 반환하기 위한 메서드의 이름입니다.|  
|**nullValue**|내부 값이 **DBNull**인 경우 값입니다. **Nullvalue** 주석에 대해서는 다음 표를 참조 하세요. 기본값은 **_throw**입니다.|  
  
 다음 표에서는 **Nullvalue** 주석에 대해 지정할 수 있는 값을 보여 줍니다.  
  
|nullValue 값|Description|  
|---------------------|-----------------|  
|*대체 값*|반환될 값을 지정합니다. 반환되는 값은 요소의 형식과 일치해야 합니다. 예를 들어, `nullValue="0"`을 사용하여 null 정수 필드에 0을 반환합니다.|  
|**_throw**|예외를 throw합니다. 기본값입니다.|  
|**_null**|기본 형식이 발견되면 null 참조를 반환하거나 예외를 throw합니다.|  
|**_empty**|문자열의 경우 **system.string**을 반환 하 고, 그렇지 않은 경우 빈 생성자에서 만든 개체를 반환 합니다. 기본 형식이 발견되면 예외를 throw합니다.|  
  
 다음 표에서는 형식화 된 **데이터 집합** 의 개체에 대 한 기본값과 사용 가능한 주석을 보여 줍니다.  
  
|개체/메서드/이벤트|기본값|Annotation|  
|---------------------------|-------------|----------------|  
|**DataTable**|TableNameDataTable|typedPlural|  
|**DataTable** 메서드|NewTableNameRow<br /><br /> AddTableNameRow<br /><br /> DeleteTableNameRow|typedName|  
|**DataRowCollection**|TableName|typedPlural|  
|**DataRow**|TableNameRow|typedName|  
|**DataColumn**|DataTable.ColumnNameColumn<br /><br /> DataRow.ColumnName|typedName|  
|**Property**|PropertyName|typedName|  
|**자식** 접근자|GetChildTableNameRows|typedChildren|  
|**부모** 접근자|TableNameRow|typedParent|  
|**데이터 집합** 이벤트|TableNameRowChangeEvent<br /><br /> TableNameRowChangeEventHandler|typedName|  
  
 형식화 된 **데이터 집합** 주석을 사용 하려면 XSD (XML 스키마 정의 언어) 스키마에 다음 **xmlns** 참조를 포함 해야 합니다. 데이터베이스 테이블에서 xsd를 만들려면 또는 <xref:System.Data.DataSet.WriteXmlSchema%2A> [Visual Studio에서 데이터 집합 작업](/visualstudio/data-tools/dataset-tools-in-visual-studio)을 참조 하세요.  
  
```  
xmlns:codegen="urn:schemas-microsoft-com:xml-msprop"  
```  
  
 다음은 포함 된 **Orders** 테이블과 관련 된 **Northwind** 데이터베이스의 **Customers** 테이블을 표시 하는 주석이 추가 된 샘플 스키마입니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema id="CustomerDataSet"   
      xmlns:codegen="urn:schemas-microsoft-com:xml-msprop"  
      xmlns=""   
      xmlns:xs="http://www.w3.org/2001/XMLSchema"   
      xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="CustomerDataSet" msdata:IsDataSet="true">  
    <xs:complexType>  
      <xs:choice maxOccurs="unbounded">  
        <xs:element name="Customers" codegen:typedName="Customer" codegen:typedPlural="Customers">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="CustomerID"  
codegen:typedName="CustomerID" type="xs:string" minOccurs="0" />  
              <xs:element name="CompanyName"  
codegen:typedName="CompanyName" type="xs:string" minOccurs="0" />  
              <xs:element name="Phone" codegen:typedName="Phone" codegen:nullValue="" type="xs:string" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
        <xs:element name="Orders" codegen:typedName="Order" codegen:typedPlural="Orders">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="OrderID" codegen:typedName="OrderID"  
type="xs:int" minOccurs="0" />  
              <xs:element name="CustomerID"  
codegen:typedName="CustomerID"                  codegen:nullValue="" type="xs:string" minOccurs="0" />  
              <xs:element name="EmployeeID"  
codegen:typedName="EmployeeID" codegen:nullValue="0"   
type="xs:int" minOccurs="0" />  
              <xs:element name="OrderAdapter"  
codegen:typedName="OrderAdapter" codegen:nullValue="1980-01-01T00:00:00"   
type="xs:dateTime" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
      </xs:choice>  
    </xs:complexType>  
    <xs:unique name="Constraint1">  
      <xs:selector xpath=".//Customers" />  
      <xs:field xpath="CustomerID" />  
    </xs:unique>  
    <xs:keyref name="CustOrders" refer="Constraint1"  
codegen:typedParent="Customer" codegen:typedChildren="GetOrders">  
      <xs:selector xpath=".//Orders" />  
      <xs:field xpath="CustomerID" />  
    </xs:keyref>  
  </xs:element>  
</xs:schema>  
```  
  
 다음 코드 예제에서는 샘플 스키마에서 만든 강력한 형식의 **데이터 집합** 을 사용 합니다. 하나 <xref:System.Data.SqlClient.SqlDataAdapter> 를 사용 하 여 **Customers** 테이블 <xref:System.Data.SqlClient.SqlDataAdapter> 을 채우고 **Orders** 테이블을 채웁니다. 강력한 형식의 **데이터 집합** 은 **datarelations**을 정의 합니다.  
  
```vb  
' Assumes a valid SqlConnection object named connection.  
Dim customerAdapter As SqlDataAdapter = New SqlDataAdapter( _  
    "SELECT CustomerID, CompanyName, Phone FROM Customers", &  
    connection)  
Dim orderAdapter As SqlDataAdapter = New SqlDataAdapter( _  
    "SELECT OrderID, CustomerID, EmployeeID, OrderAdapter FROM Orders", &  
    connection)  
  
' Populate a strongly typed DataSet.  
connection.Open()  
Dim customers As CustomerDataSet = New CustomerDataSet()  
customerAdapter.Fill(customers, "Customers")  
orderAdapter.Fill(customers, "Orders")  
connection.Close()  
  
' Add a strongly typed event.  
AddHandler customers.Customers.CustomerChanged, &  
    New CustomerDataSet.CustomerChangeEventHandler( _  
    AddressOf OnCustomerChanged)  
  
' Add a strongly typed DataRow.  
Dim newCustomer As CustomerDataSet.Customer = _  
    customers.Customers.NewCustomer()  
newCustomer.CustomerID = "NEW01"  
newCustomer.CompanyName = "My New Company"  
customers.Customers.AddCustomer(newCustomer)  
  
' Navigate the child relation.  
Dim customer As CustomerDataSet.Customer  
Dim order As CustomerDataSet.Order  
  
For Each customer In customers.Customers  
  Console.WriteLine(customer.CustomerID)  
  For Each order In customer.GetOrders()  
    Console.WriteLine(vbTab & order.OrderID)  
  Next  
Next  
  
Private Shared Sub OnCustomerChanged( _  
    sender As Object, e As CustomerDataSet.CustomerChangeEvent)  
  
End Sub  
```  
  
```csharp  
// Assumes a valid SqlConnection object named connection.  
SqlDataAdapter customerAdapter = new SqlDataAdapter(  
    "SELECT CustomerID, CompanyName, Phone FROM Customers",  
    connection);  
SqlDataAdapter orderAdapter = new SqlDataAdapter(  
    "SELECT OrderID, CustomerID, EmployeeID, OrderAdapter FROM Orders",   
    connection);  
  
// Populate a strongly typed DataSet.  
connection.Open();  
CustomerDataSet customers = new CustomerDataSet();  
customerAdapter.Fill(customers, "Customers");  
orderAdapter.Fill(customers, "Orders");  
connection.Close();  
  
// Add a strongly typed event.  
customers.Customers.CustomerChanged += new   
  CustomerDataSet.CustomerChangeEventHandler(OnCustomerChanged);  
  
// Add a strongly typed DataRow.  
CustomerDataSet.Customer newCustomer =   
    customers.Customers.NewCustomer();  
newCustomer.CustomerID = "NEW01";  
newCustomer.CompanyName = "My New Company";  
customers.Customers.AddCustomer(newCustomer);  
  
// Navigate the child relation.  
foreach(CustomerDataSet.Customer customer in customers.Customers)  
{  
  Console.WriteLine(customer.CustomerID);  
  foreach(CustomerDataSet.Order order in customer.GetOrders())  
    Console.WriteLine("\t" + order.OrderID);  
}  
  
protected static void OnCustomerChanged(object sender, CustomerDataSet.CustomerChangeEvent e)  
    {  
  
    }  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Data.DataColumnCollection>
- <xref:System.Data.DataSet>
- [형식화된 데이터 집합](typed-datasets.md)
- [DataSet, DataTable 및 DataView](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
