---
title: '샘플 XML 파일: 3에서 여러 구매 주문'
ms.date: 07/20/2015
ms.assetid: 03f754c6-89f7-4143-8456-4963044be7e5
ms.openlocfilehash: 4f7a25b9b56c5d37d45ee46928f3d4ceb3607c35
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61787012"
---
# <a name="sample-xml-file-multiple-purchase-orders-in-a-namespace"></a>샘플 XML 파일: 네임스페이스에서 여러 구매 주문
다음 XML 파일은 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 설명서의 다양한 예제에서 사용됩니다. 이 파일에는 몇 가지 구매 주문이 포함되어 있습니다. XML은 네임스페이스에 있습니다.  
  
## <a name="purchaseordersinnamespacexml"></a>PurchaseOrdersInNamespace.xml  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<aw:PurchaseOrders xmlns:aw="http://www.adventure-works.com">  
  <aw:PurchaseOrder aw:PurchaseOrderNumber="99503" aw:OrderDate="1999-10-20">  
    <aw:Address aw:Type="Shipping">  
      <aw:Name>Ellen Adams</aw:Name>  
      <aw:Street>123 Maple Street</aw:Street>  
      <aw:City>Mill Valley</aw:City>  
      <aw:State>CA</aw:State>  
      <aw:Zip>10999</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:Address>  
    <aw:Address aw:Type="Billing">  
      <aw:Name>Tai Yee</aw:Name>  
      <aw:Street>8 Oak Avenue</aw:Street>  
      <aw:City>Old Town</aw:City>  
      <aw:State>PA</aw:State>  
      <aw:Zip>95819</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:Address>  
    <aw:DeliveryNotes>Please leave packages in shed by driveway.</aw:DeliveryNotes>  
    <aw:Items>  
      <aw:Item aw:PartNumber="872-AA">  
        <aw:ProductName>Lawnmower</aw:ProductName>  
        <aw:Quantity>1</aw:Quantity>  
        <aw:USPrice>148.95</aw:USPrice>  
        <aw:Comment>Confirm this is electric</aw:Comment>  
      </aw:Item>  
      <aw:Item aw:PartNumber="926-AA">  
        <aw:ProductName>Baby Monitor</aw:ProductName>  
        <aw:Quantity>2</aw:Quantity>  
        <aw:USPrice>39.98</aw:USPrice>  
        <aw:ShipDate>1999-05-21</aw:ShipDate>  
      </aw:Item>  
    </aw:Items>  
  </aw:PurchaseOrder>  
  <aw:PurchaseOrder aw:PurchaseOrderNumber="99505" aw:OrderDate="1999-10-22">  
    <aw:Address aw:Type="Shipping">  
      <aw:Name>Cristian Osorio</aw:Name>  
      <aw:Street>456 Main Street</aw:Street>  
      <aw:City>Buffalo</aw:City>  
      <aw:State>NY</aw:State>  
      <aw:Zip>98112</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:Address>  
    <aw:Address aw:Type="Billing">  
      <aw:Name>Cristian Osorio</aw:Name>  
      <aw:Street>456 Main Street</aw:Street>  
      <aw:City>Buffalo</aw:City>  
      <aw:State>NY</aw:State>  
      <aw:Zip>98112</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:Address>  
    <aw:DeliveryNotes>Please notify me before shipping.</aw:DeliveryNotes>  
    <aw:Items>  
      <aw:Item aw:PartNumber="456-NM">  
        <aw:ProductName>Power Supply</aw:ProductName>  
        <aw:Quantity>1</aw:Quantity>  
        <aw:USPrice>45.99</aw:USPrice>  
      </aw:Item>  
    </aw:Items>  
  </aw:PurchaseOrder>  
  <aw:PurchaseOrder aw:PurchaseOrderNumber="99504" aw:OrderDate="1999-10-22">  
    <aw:Address aw:Type="Shipping">  
      <aw:Name>Jessica Arnold</aw:Name>  
      <aw:Street>4055 Madison Ave</aw:Street>  
      <aw:City>Seattle</aw:City>  
      <aw:State>WA</aw:State>  
      <aw:Zip>98112</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:Address>  
    <aw:Address aw:Type="Billing">  
      <aw:Name>Jessica Arnold</aw:Name>  
      <aw:Street>4055 Madison Ave</aw:Street>  
      <aw:City>Buffalo</aw:City>  
      <aw:State>NY</aw:State>  
      <aw:Zip>98112</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:Address>  
    <aw:Items>  
      <aw:Item aw:PartNumber="898-AZ">  
        <aw:ProductName>Computer Keyboard</aw:ProductName>  
        <aw:Quantity>1</aw:Quantity>  
        <aw:USPrice>29.99</aw:USPrice>  
      </aw:Item>  
      <aw:Item aw:PartNumber="898-AM">  
        <aw:ProductName>Wireless Mouse</aw:ProductName>  
        <aw:Quantity>1</aw:Quantity>  
        <aw:USPrice>14.99</aw:USPrice>  
      </aw:Item>  
    </aw:Items>  
  </aw:PurchaseOrder>  
</aw:PurchaseOrders>  
```  
  
## <a name="see-also"></a>참고자료

- [샘플 XML 문서(LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-documents-linq-to-xml.md)
