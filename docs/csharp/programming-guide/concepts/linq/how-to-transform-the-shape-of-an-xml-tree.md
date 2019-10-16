---
title: '방법: XML 트리의 모양 변환(C#)'
ms.date: 07/20/2015
ms.assetid: 93c5d426-dea2-4709-a991-60204de42e8f
ms.openlocfilehash: c6f78decdcc32d202f4a0f1e51a012dce8aa7d6c
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69592226"
---
# <a name="how-to-transform-the-shape-of-an-xml-tree-c"></a>방법: XML 트리의 모양 변환(C#)
XML 문서의 *모양*은 요소 이름, 특성 이름 및 계층 구조의 특징을 나타냅니다.  
  
 XML 문서의 모양을 변경해야 하는 경우가 있습니다. 예를 들어, 다른 요소 및 특성 이름이 필요한 다른 시스템에 기존 XML 문서를 보내야 할 수 있습니다. 문서를 살펴보면서 필요에 따라 요소를 삭제하고 요소의 이름을 바꿀 수 있지만 함수 생성을 사용하면 읽고 유지 관리하기가 더 쉬운 코드가 생성됩니다. 함수 생성에 대한 자세한 내용은 [함수 생성(LINQ to XML)(C#)](./functional-construction-linq-to-xml.md)을 참조하세요.  
  
 첫 번째 예제에서는 XML 문서의 구성을 변경하고 트리의 한 위치에서 다른 위치로 복합 요소를 이동합니다.  
  
 이 항목의 두 번째 예제에서는 소스 문서와 모양이 다른 XML 문서를 만들고 요소 이름의 대/소문자를 변경한 다음 일부 요소의 이름을 바꾸고 소스 트리의 일부 요소를 변환된 트리 외부에 둡니다.  
  
## <a name="example"></a>예  
 다음 코드에서는 포함된 쿼리 식을 사용하여 XML 파일의 모양을 변경합니다.  
  
 이 예제의 소스 XML 문서에는 `Customers` 요소 아래에 모든 고객이 포함된 `Root` 요소가 들어 있습니다. 또한 `Orders` 요소 아래에 모든 주문이 포함된 `Root` 요소도 포함되어 있습니다. 이 예제에서는 각 고객의 주문이 `Orders` 요소에 있는 `Customer` 요소에 포함되어 있는 새 XML 트리를 만듭니다. 원래 문서에도 `CustomerID` 요소에 `Order` 요소가 포함되어 있습니다. 이 요소는 모양이 다시 변경된 문서에서 제거됩니다.  
  
 이 예제에서는 XML 문서로을 사용합니다. [샘플 XML 파일: Customers 및 Orders(LINQ to XML)](./sample-xml-file-customers-and-orders-linq-to-xml-2.md).  
  
```csharp  
XElement co = XElement.Load("CustomersOrders.xml");  
XElement newCustOrd =  
    new XElement("Root",  
        from cust in co.Element("Customers").Elements("Customer")  
        select new XElement("Customer",  
            cust.Attributes(),  
            cust.Elements(),  
            new XElement("Orders",  
                from ord in co.Element("Orders").Elements("Order")  
                where (string)ord.Element("CustomerID") == (string)cust.Attribute("CustomerID")  
                select new XElement("Order",  
                    ord.Attributes(),  
                    ord.Element("EmployeeID"),  
                    ord.Element("OrderDate"),  
                    ord.Element("RequiredDate"),  
                    ord.Element("ShipInfo")  
                )  
            )  
        )  
    );  
Console.WriteLine(newCustOrd);  
```  
  
 이 코드의 결과는 다음과 같습니다.  
  
```xml  
<Root>  
  <Customer CustomerID="GREAL">  
    <CompanyName>Great Lakes Food Market</CompanyName>  
    <ContactName>Howard Snyder</ContactName>  
    <ContactTitle>Marketing Manager</ContactTitle>  
    <Phone>(503) 555-7555</Phone>  
    <FullAddress>  
      <Address>2732 Baker Blvd.</Address>  
      <City>Eugene</City>  
      <Region>OR</Region>  
      <PostalCode>97403</PostalCode>  
      <Country>USA</Country>  
    </FullAddress>  
    <Orders />  
  </Customer>  
  <Customer CustomerID="HUNGC">  
    <CompanyName>Hungry Coyote Import Store</CompanyName>  
    <ContactName>Yoshi Latimer</ContactName>  
    <ContactTitle>Sales Representative</ContactTitle>  
    <Phone>(503) 555-6874</Phone>  
    <Fax>(503) 555-2376</Fax>  
    <FullAddress>  
      <Address>City Center Plaza 516 Main St.</Address>  
      <City>Elgin</City>  
      <Region>OR</Region>  
      <PostalCode>97827</PostalCode>  
      <Country>USA</Country>  
    </FullAddress>  
    <Orders />  
  </Customer>  
  . . .  
```  
  
## <a name="example"></a>예  
 이 예제에서는 일부 요소의 이름을 바꾸고 일부 특성을 요소로 변환합니다.  
  
 코드에서는 `ConvertAddress` 개체의 목록을 반환하는 <xref:System.Xml.Linq.XElement>를 호출합니다. 메서드의 인수는 `Address` 특성의 값이 `Type`인 `"Shipping"` 복합 요소를 확인하는 쿼리입니다.  
  
 이 예제에서는 XML 문서로을 사용합니다. [샘플 XML 파일: 일반적인 구매 주문(LINQ to XML)](./sample-xml-file-typical-purchase-order-linq-to-xml-1.md).  
  
```csharp  
static IEnumerable<XElement> ConvertAddress(XElement add)  
{  
    List<XElement> fragment = new List<XElement>() {  
        new XElement("NAME", (string)add.Element("Name")),  
        new XElement("STREET", (string)add.Element("Street")),  
        new XElement("CITY", (string)add.Element("City")),  
        new XElement("ST", (string)add.Element("State")),  
        new XElement("POSTALCODE", (string)add.Element("Zip")),  
        new XElement("COUNTRY", (string)add.Element("Country"))  
    };  
    return fragment;  
}  
  
static void Main(string[] args)  
{  
    XElement po = XElement.Load("PurchaseOrder.xml");  
    XElement newPo = new XElement("PO",  
        new XElement("ID", (string)po.Attribute("PurchaseOrderNumber")),  
        new XElement("DATE", (DateTime)po.Attribute("OrderDate")),  
        ConvertAddress(  
            (from el in po.Elements("Address")  
            where (string)el.Attribute("Type") == "Shipping"  
            select el)  
            .First()  
        )  
    );  
    Console.WriteLine(newPo);  
}  
```  
  
 이 코드의 결과는 다음과 같습니다.  
  
```xml  
<PO>  
  <ID>99503</ID>  
  <DATE>1999-10-20T00:00:00</DATE>  
  <NAME>Ellen Adams</NAME>  
  <STREET>123 Maple Street</STREET>  
  <CITY>Mill Valley</CITY>  
  <ST>CA</ST>  
  <POSTALCODE>10999</POSTALCODE>  
  <COUNTRY>USA</COUNTRY>  
</PO>  
```  
