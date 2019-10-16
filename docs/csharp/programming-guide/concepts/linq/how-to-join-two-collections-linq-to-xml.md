---
title: '방법: 두 컬렉션 조인(LINQ to XML)(C#)'
ms.date: 07/20/2015
ms.assetid: 7b817ede-911a-4cff-9dd3-639c3fc228c9
ms.openlocfilehash: 82083a24da9a5356a8ff8e8430b61bb5d41f7c72
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253573"
---
# <a name="how-to-join-two-collections-linq-to-xml-c"></a>방법: 두 컬렉션 조인(LINQ to XML)(C#)
XML 문서의 요소나 특성은 때때로 다른 요소나 특성을 참조할 수 있습니다. 예를 들어 [샘플 XML 파일: Customers 및 Orders고객(LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md) XML 문서에는 고객 목록과 주문 목록이 포함되어 있습니다. 각 `Customer` 요소에는 `CustomerID` 특성이 포함되어 있고, 각 `Order` 요소에는 `CustomerID` 요소가 포함되어 있습니다. 각 주문의 `CustomerID` 요소는 고객의 `CustomerID` 특성을 참조합니다.  
  
 항목 [샘플 XSD 파일: Customers 및 Orders](./sample-xsd-file-customers-and-orders1.md)에는 이 문서의 유효성을 검사하는 데 사용할 수 있는 XSD가 포함되어 있습니다. 이 항목에서는 XSD의 `xs:key` 및 `xs:keyref` 기능을 사용하여 `CustomerID` 요소의 `Customer` 특성을 키로 설정하고 각 `CustomerID` 요소의 `Order` 요소와 각 `CustomerID` 요소의 `Customer` 특성 간 관계를 설정합니다.  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 `join` 절을 사용하여 이 관계를 이용할 수 있습니다.  
  
 사용 가능한 인덱스가 없기 때문에 이러한 조인의 런타임 성능은 좋지 않습니다.  
  
 `join`에 대한 자세한 내용은 [조인 작업(C#)](./join-operations.md)을 참조하세요.  
  
## <a name="example"></a>예  
 다음 예제에서는 `Customer` 요소와 `Order` 요소를 조인하고 주문의 `CompanyName` 요소가 포함된 새 XML 문서를 생성합니다.  
  
 예제에서는 쿼리를 실행하기 전에 문서가 [샘플 XSD 파일: Customer 및 Order](./sample-xsd-file-customers-and-orders1.md)의 스키마를 준수하는지 확인합니다. 이에 따라 조인 절이 항상 작동하게 됩니다.  
  
 이 쿼리에서는 먼저 모든 `Customer` 요소를 검색하고 `Order` 요소와 조인한 다음 `CustomerID`가 "K"보다 큰 고객의 주문만 선택합니다. 그런 다음 각 주문의 고객 정보가 포함된 새 `Order` 요소를 프로젝션합니다.  
  
 이 예제에서는 XML 문서로을 사용합니다. [샘플 XML 파일: Customers 및 Orders(LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md).  
  
 이 예제에서는 XSD 스키마을 사용합니다. [샘플 XSD 파일: Customer 및 Order](./sample-xsd-file-customers-and-orders1.md).  
  
 이런 방식의 조인은 성능이 좋지 않습니다. 조인은 선형 검색을 통해 수행됩니다. 성능에 도움이 될 해시 테이블이나 인덱스는 없습니다.  
  
```csharp  
XmlSchemaSet schemas = new XmlSchemaSet();  
schemas.Add("", "CustomersOrders.xsd");  
  
Console.Write("Attempting to validate, ");  
XDocument custOrdDoc = XDocument.Load("CustomersOrders.xml");  
  
bool errors = false;  
custOrdDoc.Validate(schemas, (o, e) =>  
                     {  
                         Console.WriteLine("{0}", e.Message);  
                         errors = true;  
                     });  
Console.WriteLine("custOrdDoc {0}", errors ? "did not validate" : "validated");  
  
if (!errors)  
{  
    // Join customers and orders, and create a new XML document with  
    // a different shape.  
  
    // The new document contains orders only for customers with a  
    // CustomerID > 'K'  
    XElement custOrd = custOrdDoc.Element("Root");  
    XElement newCustOrd = new XElement("Root",  
        from c in custOrd.Element("Customers").Elements("Customer")  
        join o in custOrd.Element("Orders").Elements("Order")  
                   on (string)c.Attribute("CustomerID") equals  
                      (string)o.Element("CustomerID")  
        where ((string)c.Attribute("CustomerID")).CompareTo("K") > 0  
        select new XElement("Order",  
            new XElement("CustomerID", (string)c.Attribute("CustomerID")),  
            new XElement("CompanyName", (string)c.Element("CompanyName")),  
            new XElement("ContactName", (string)c.Element("ContactName")),  
            new XElement("EmployeeID", (string)o.Element("EmployeeID")),  
            new XElement("OrderDate", (DateTime)o.Element("OrderDate"))  
        )  
    );  
    Console.WriteLine(newCustOrd);  
}  
```  
  
 이 코드의 결과는 다음과 같습니다.  
  
```output  
Attempting to validate, custOrdDoc validated  
<Root>  
  <Order>  
    <CustomerID>LAZYK</CustomerID>  
    <CompanyName>Lazy K Kountry Store</CompanyName>  
    <ContactName>John Steel</ContactName>  
    <EmployeeID>1</EmployeeID>  
    <OrderDate>1997-03-21T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LAZYK</CustomerID>  
    <CompanyName>Lazy K Kountry Store</CompanyName>  
    <ContactName>John Steel</ContactName>  
    <EmployeeID>8</EmployeeID>  
    <OrderDate>1997-05-22T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>1</EmployeeID>  
    <OrderDate>1997-06-25T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>8</EmployeeID>  
    <OrderDate>1997-10-27T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>6</EmployeeID>  
    <OrderDate>1997-11-10T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>4</EmployeeID>  
    <OrderDate>1998-02-12T00:00:00</OrderDate>  
  </Order>  
</Root>  
```  
