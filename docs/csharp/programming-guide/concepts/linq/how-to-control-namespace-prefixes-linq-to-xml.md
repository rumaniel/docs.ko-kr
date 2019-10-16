---
title: '방법: 네임스페이스 접두사 제어(C#)(LINQ to XML)'
ms.date: 07/20/2015
ms.assetid: 64de5186-b81a-4ddd-8327-8693df59a01b
ms.openlocfilehash: 5b836be46001b660547532311b1b507ff234975f
ms.sourcegitcommit: eb9ff6f364cde6f11322e03800d8f5ce302f3c73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68710158"
---
# <a name="how-to-control-namespace-prefixes-c-linq-to-xml"></a>방법: 네임스페이스 접두사 제어(C#)(LINQ to XML)
이 항목에서는 XML 트리를 serialize할 때 네임스페이스 접두사를 제어하는 방법에 대해 설명합니다.  
  
 대부분의 경우에는 네임스페이스 접두사를 제어할 필요가 없습니다.  
  
 그러나 일부 XML 프로그래밍 도구를 사용할 때는 네임스페이스 접두사를 특수하게 제어해야 합니다. 예를 들어, 특정 네임스페이스 접두사를 참조하는 포함된 XPath 식이 들어 있는 XSLT 스타일시트나 XAML 문서를 조작할 수 있습니다. 이 경우 해당 문서가 특정 접두사를 사용하여 serialize되어야 합니다.  
  
 이는 네임스페이스 접두사를 제어해야 하는 가장 일반적인 경우입니다.  
  
 네임스페이스 접두사를 제어하는 또 다른 일반적인 경우는 사용자가 XML 문서를 수동으로 편집하도록 하고 사용자가 입력하기 편한 네임스페이스 접두사를 만들려고 할 때입니다. 예를 들어, XSD 문서를 생성할 수 있습니다. 스키마 규칙에서는 스키마 네임스페이스의 접두사로 `xs` 또는 `xsd`를 사용하도록 제안합니다.  
  
 네임스페이스 접두사를 제어하려면 네임스페이스를 선언하는 특성을 삽입합니다. 특정 접두사가 포함된 네임스페이스를 선언하는 경우 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 serialize할 때 네임스페이스 접두사를 고려하려고 합니다.  
  
 접두사가 포함된 네임스페이스를 선언하는 특성을 만들려면 특성 이름의 네임스페이스가 <xref:System.Xml.Linq.XNamespace.Xmlns%2A>이고 특성의 이름이 네임스페이스 접두사인 특성을 만듭니다. 특성 값은 네임스페이스의 URI입니다.  
  
## <a name="example"></a>예  
 이 예제에서는 두 네임스페이스를 선언한 다음 `http://www.adventure-works.com` 네임스페이스가 `aw` 접두사를 갖고 `www.fourthcoffee.com`네임스페이스가 `fc` 접두사를 갖도록 지정합니다.  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XNamespace fc = "www.fourthcoffee.com";  
XElement root = new XElement(aw + "Root",  
    new XAttribute(XNamespace.Xmlns + "aw", "http://www.adventure-works.com"),  
    new XAttribute(XNamespace.Xmlns + "fc", "www.fourthcoffee.com"),  
    new XElement(fc + "Child",  
        new XElement(aw + "DifferentChild", "other content")  
    ),  
    new XElement(aw + "Child2", "c2 content"),  
    new XElement(fc + "Child3", "c3 content")  
);  
Console.WriteLine(root);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com" xmlns:fc="www.fourthcoffee.com">  
  <fc:Child>  
    <aw:DifferentChild>other content</aw:DifferentChild>  
  </fc:Child>  
  <aw:Child2>c2 content</aw:Child2>  
  <fc:Child3>c3 content</fc:Child3>  
</aw:Root>  
```  
  
## <a name="see-also"></a>참고 항목

- [네임스페이스 개요(LINQ to XML)(C#)](namespaces-overview-linq-to-xml.md)
