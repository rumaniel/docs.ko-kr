---
title: '방법: 체인 축 메서드 호출 (LINQ to XML) (Visual Basic)'
ms.date: 07/20/2015
ms.assetid: e4e22942-39bd-460f-b3c0-9f09e53d3aa9
ms.openlocfilehash: 8c607915d83c49958e3aa86c9625fa1311a2274b
ms.sourcegitcommit: eb9ff6f364cde6f11322e03800d8f5ce302f3c73
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68709831"
---
# <a name="how-to-chain-axis-method-calls-linq-to-xml-visual-basic"></a>방법: 체인 축 메서드 호출 (LINQ to XML) (Visual Basic)
코드에 사용할 수 있는 일반적인 방법은 축 메서드를 호출한 다음 확장명 메서드 축 중 하나를 호출하는 것입니다.  
  
 요소의 컬렉션을 반환하며 `Elements`의 이름이 포함된 두 축인 <xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType> 메서드와 <xref:System.Xml.Linq.Extensions.Elements%2A?displayProperty=nameWithType> 메서드가 있습니다. 이러한 두 축을 결합하여 트리의 특정 깊이에서 지정된 이름의 모든 요소를 찾을 수 있습니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 <xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType> 및 <xref:System.Xml.Linq.Extensions.Elements%2A?displayProperty=nameWithType>를 사용하여 모든 `Name` 요소의 모든 `Address` 요소에 있는 모든 `PurchaseOrder` 요소를 찾습니다.  
  
 이 예제에서는 XML 문서로을 사용합니다. [샘플 XML 파일: 여러 구매 주문(LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-multiple-purchase-orders-linq-to-xml.md).  
  
```vb  
Dim purchaseOrders As XElement = XElement.Load("PurchaseOrders.xml")  
Dim names As IEnumerable(Of XElement) = _  
    From el In purchaseOrders.<PurchaseOrder>.<Address>.<Name> _  
    Select el  
For Each e As XElement In names  
    Console.WriteLine(e)  
Next  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Name>Ellen Adams</Name>  
<Name>Tai Yee</Name>  
<Name>Cristian Osorio</Name>  
<Name>Cristian Osorio</Name>  
<Name>Jessica Arnold</Name>  
<Name>Jessica Arnold</Name>  
```  
  
 이는 `Elements` 축의 구현 중 하나가 <xref:System.Collections.Generic.IEnumerable%601>의 <xref:System.Xml.Linq.XContainer>에 대한 확장 메서드이기 때문에 작동합니다. <xref:System.Xml.Linq.XElement>는 <xref:System.Xml.Linq.XContainer>에서 파생되므로 <xref:System.Xml.Linq.Extensions.Elements%2A?displayProperty=nameWithType> 메서드에 대한 호출의 결과에 대해 <xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType> 메서드를 호출할 수 있습니다.  
  
## <a name="example"></a>예제  
 중간에 상위 요소가 있을 수도 있고 없을 수도 있는 특정 요소 깊이에서 모든 요소를 검색하려는 경우가 있습니다. 예를 들어, 다음 문서에서 `ConfigParameter` 요소의 자식인 모든 `Customer` 요소를 검색하고 `ConfigParameter` 요소의 자식인 `Root`는 검색하지 않으려고 할 수 있습니다.  
  
```xml  
<Root>  
  <ConfigParameter>RootConfigParameter</ConfigParameter>  
  <Customer>  
    <Name>Frank</Name>  
    <Config>  
      <ConfigParameter>FirstConfigParameter</ConfigParameter>  
    </Config>  
  </Customer>  
  <Customer>  
    <Name>Bob</Name>  
    <!--This customer doesn't have a Config element-->  
  </Customer>  
  <Customer>  
    <Name>Bill</Name>  
    <Config>  
      <ConfigParameter>SecondConfigParameter</ConfigParameter>  
    </Config>  
  </Customer>  
</Root>  
```  
  
 이렇게 하려면 <xref:System.Xml.Linq.Extensions.Elements%2A?displayProperty=nameWithType> 축을 다음과 같이 사용하면 됩니다.  
  
```vb  
Dim root As XElement = XElement.Load("Irregular.xml")  
Dim configParameters As IEnumerable(Of XElement) = _  
    root.<Customer>.<Config>.<ConfigParameter>  
For Each cp As XElement In configParameters  
    Console.WriteLine(cp)  
Next  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<ConfigParameter>FirstConfigParameter</ConfigParameter>  
<ConfigParameter>SecondConfigParameter</ConfigParameter>  
```  
  
## <a name="example"></a>예제  
 다음 예제에서는 네임스페이스에 있는 XML에 대한 동일한 기법을 보여 줍니다. 자세한 내용은 [네임 스페이스 개요 (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md)를 참조 하세요.  
  
 이 예제에서는 XML 문서로을 사용합니다. [샘플 XML 파일: 네임스페이스에서 여러 구매 주문](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-multiple-purchase-orders-in-a-namespace.md).  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim purchaseOrders As XElement = XElement.Load("PurchaseOrdersInNamespace.xml")  
        Dim names As IEnumerable(Of XElement) = _  
            From el In purchaseOrders.<aw:PurchaseOrder>.<aw:Address>.<aw:Name> _  
            Select el  
        For Each e As XElement In names  
            Console.WriteLine(e)  
        Next  
    End Sub  
End Module  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<aw:Name xmlns:aw="http://www.adventure-works.com">Ellen Adams</aw:Name>  
<aw:Name xmlns:aw="http://www.adventure-works.com">Tai Yee</aw:Name>  
<aw:Name xmlns:aw="http://www.adventure-works.com">Cristian Osorio</aw:Name>  
<aw:Name xmlns:aw="http://www.adventure-works.com">Cristian Osorio</aw:Name>  
<aw:Name xmlns:aw="http://www.adventure-works.com">Jessica Arnold</aw:Name>  
<aw:Name xmlns:aw="http://www.adventure-works.com">Jessica Arnold</aw:Name>  
```  
  
## <a name="see-also"></a>참고자료

- [LINQ to XML 축(Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes.md)
