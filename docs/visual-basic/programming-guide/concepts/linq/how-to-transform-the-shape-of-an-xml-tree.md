---
title: '방법: (Visual Basic) XML 트리의 모양 변형'
ms.date: 07/20/2015
ms.assetid: 84b60854-48b2-452c-87f2-77d53e1d653a
ms.openlocfilehash: 067bf56b8dff994080ba78147d992b97a56867cb
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61615001"
---
# <a name="how-to-transform-the-shape-of-an-xml-tree-visual-basic"></a>방법: (Visual Basic) XML 트리의 모양 변형
XML 문서의 *모양*은 요소 이름, 특성 이름 및 계층 구조의 특징을 나타냅니다.  
  
 XML 문서의 모양을 변경해야 하는 경우가 있습니다. 예를 들어, 다른 요소 및 특성 이름이 필요한 다른 시스템에 기존 XML 문서를 보내야 할 수 있습니다. 문서를 살펴보면서 필요에 따라 요소를 삭제하고 요소의 이름을 바꿀 수 있지만 함수 생성을 사용하면 읽고 유지 관리하기가 더 쉬운 코드가 생성됩니다. 함수 생성에 대 한 자세한 내용은 참조 하세요. [함수 생성 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/functional-construction-linq-to-xml.md)합니다.  
  
 첫 번째 예제에서는 XML 문서의 구성을 변경하고 트리의 한 위치에서 다른 위치로 복합 요소를 이동합니다.  
  
 이 항목의 두 번째 예제에서는 소스 문서와 모양이 다른 XML 문서를 만들고 요소 이름의 대/소문자를 변경한 다음 일부 요소의 이름을 바꾸고 소스 트리의 일부 요소를 변환된 트리 외부에 둡니다.  
  
## <a name="example"></a>예제  
 다음 코드에서는 포함된 쿼리 식을 사용하여 XML 파일의 모양을 변경합니다.  
  
 이 예제의 소스 XML 문서에는 `Customers` 요소 아래에 모든 고객이 포함된 `Root` 요소가 들어 있습니다. 또한 `Orders` 요소 아래에 모든 주문이 포함된 `Root` 요소도 포함되어 있습니다. 이 예제에서는 각 고객의 주문이 `Orders` 요소에 있는 `Customer` 요소에 포함되어 있는 새 XML 트리를 만듭니다. 원래 문서에도 `CustomerID` 요소에 `Order` 요소가 포함되어 있습니다. 이 요소는 모양이 다시 변경된 문서에서 제거됩니다.  
  
 이 예제에서는 XML 문서로을 사용합니다. [샘플 XML 파일: Customers 및 Orders(LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-customers-and-orders-linq-to-xml.md).  
  
```vb  
Dim co As XElement = XElement.Load("CustomersOrders.xml")  
Dim newCustOrd = _  
    <Root>  
        <%= From cust In co.<Customers>.<Customer> _  
            Select _  
            <Customer>  
                <%= cust.Attributes() %>  
                <%= cust.Elements() %>  
                <Orders>  
                    <%= From ord In co.<Orders>.<Order> _  
                        Where ord.<CustomerID>.Value = cust.@CustomerID _  
                        Select _  
                        <Order>  
                            <%= ord.Attributes() %>  
                            <%= ord.<EmployeeID> %>  
                            <%= ord.<OrderDate> %>  
                            <%= ord.<RequiredDate> %>  
                            <%= ord.<ShipInfo> %>  
                        </Order> _  
                    %>  
                </Orders>  
            </Customer> _  
        %>  
    </Root>  
Console.WriteLine(newCustOrd)  
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
  
## <a name="example"></a>예제  
 이 예제에서는 일부 요소의 이름을 바꾸고 일부 특성을 요소로 변환합니다.  
  
 코드에서는 `ConvertAddress` 개체의 목록을 반환하는 <xref:System.Xml.Linq.XElement>를 호출합니다. 메서드의 인수는 `Address` 특성의 값이 `Type`인 `"Shipping"` 복합 요소를 확인하는 쿼리입니다.  
  
 이 예제에서는 XML 문서로을 사용합니다. [샘플 XML 파일: 일반적인 구매 주문(LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-typical-purchase-order-linq-to-xml.md).  
  
```vb  
Function ConvertAddress(ByVal add As XElement) As IEnumerable(Of XElement)  
    Dim fragment = New List(Of XElement)  
    fragment.Add(<NAME><%= add.<Name>.Value %></NAME>)  
    fragment.Add(<STREET><%= add.<Street>.Value %></STREET>)  
    fragment.Add(<CITY><%= add.<City>.Value %></CITY>)  
    fragment.Add(<ST><%= add.<State>.Value %></ST>)  
    fragment.Add(<POSTALCODE><%= add.<Zip>.Value %></POSTALCODE>)  
    fragment.Add(<COUNTRY><%= add.<Country>.Value %></COUNTRY>)  
    Return fragment  
End Function  
  
Sub Main()  
    Dim po As XElement = XElement.Load("PurchaseOrder.xml")  
    Dim newPo As XElement = _  
        <PO>  
            <ID><%= po.@PurchaseOrderNumber %></ID>  
            <DATE><%= CDate(po.@OrderDate) %></DATE>  
            <%= _  
                ConvertAddress( _  
                (From el In po.<Address> _  
                Where el.@Type = "Shipping" _  
                Select el) _  
                .First() _  
                ) _  
            %>  
        </PO>  
    Console.WriteLine(newPo)  
End Sub  
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
  
## <a name="see-also"></a>참고자료

- [프로젝션 및 변형 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/projections-and-transformations-linq-to-xml.md)
