---
title: '방법: 네임스페이스로 문서 만들기(C#)(LINQ to XML)'
ms.date: 07/20/2015
ms.assetid: 37e63c57-f86d-47ac-88a7-2c2d107def30
ms.openlocfilehash: 180dc5138f8f21b3e52e4a8b3cee4748cafdd0f5
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69593889"
---
# <a name="how-to-create-a-document-with-namespaces-c-linq-to-xml"></a>방법: 네임스페이스로 문서 만들기(C#)(LINQ to XML)
이 항목에서는 네임스페이스를 사용하여 문서를 만드는 방법을 보여 줍니다.  
  
## <a name="example"></a>예  
 네임스페이스에 포함되는 요소나 특성을 만들려면 먼저 <xref:System.Xml.Linq.XNamespace> 개체를 선언하고 초기화합니다. 그런 다음 추가 연산자 오버로드를 사용하여 네임스페이스를 문자열로 표현된 로컬 이름과 결합합니다.  
  
 다음 예제에서는 네임스페이스가 하나 포함된 문서를 만들고 기본적으로 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]은 기본 네임스페이스를 사용하여 이 문서를 serialize합니다.  
  
```csharp  
// Create an XML tree in a namespace.  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = new XElement(aw + "Root",  
    new XElement(aw + "Child", "child content")  
);  
Console.WriteLine(root);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root xmlns="http://www.adventure-works.com">  
  <Child>child content</Child>  
</Root>  
```  
  
## <a name="example"></a>예  
 다음 예제에서는 네임스페이스가 하나 포함된 문서를 만들고 네임스페이스 접두사가 포함된 네임스페이스를 선언하는 특성도 만듭니다. 접두사가 포함된 네임스페이스를 선언하는 특성을 만들려면 특성 이름이 네임스페이스 접두사이고 이 이름이 <xref:System.Xml.Linq.XNamespace.Xmlns%2A> 네임스페이스에 포함되는 특성을 만듭니다. 이 특성의 값은 네임스페이스의 URI입니다.  
  
```csharp  
// Create an XML tree in a namespace, with a specified prefix  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = new XElement(aw + "Root",  
    new XAttribute(XNamespace.Xmlns + "aw", "http://www.adventure-works.com"),  
    new XElement(aw + "Child", "child content")  
);  
Console.WriteLine(root);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com">  
  <aw:Child>child content</aw:Child>  
</aw:Root>  
```  
  
## <a name="example"></a>예  
 다음 예제에서는 두 네임스페이스가 포함된 문서를 만드는 방법을 보여 줍니다. 두 네임스페이스 중 하나는 기본 네임스페이스이고 다른 하나는 접두사가 포함된 네임스페이스입니다.  
  
 루트 요소에 네임스페이스 특성을 포함하면 `http://www.adventure-works.com`이 기본 네임스페이스가 되도록 네임스페이스가 serialize되고 `www.fourthcoffee.com`이 "fc"의 접두사를 사용하여 serialize됩니다. 기본 네임스페이스를 선언하는 특성을 만들려면 네임스페이스 없이 이름이 "xmlns"인 특성을 만듭니다. 특성 값은 기본 네임스페이스 URI입니다.  
  
```csharp  
// The http://www.adventure-works.com namespace is forced to be the default namespace.  
XNamespace aw = "http://www.adventure-works.com";  
XNamespace fc = "www.fourthcoffee.com";  
XElement root = new XElement(aw + "Root",  
    new XAttribute("xmlns", "http://www.adventure-works.com"),  
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
<Root xmlns="http://www.adventure-works.com" xmlns:fc="www.fourthcoffee.com">  
  <fc:Child>  
    <DifferentChild>other content</DifferentChild>  
  </fc:Child>  
  <Child2>c2 content</Child2>  
  <fc:Child3>c3 content</fc:Child3>  
</Root>  
```  
  
## <a name="example"></a>예  
 다음 예제에서는 네임스페이스 접두사가 있는 두 가지 네임스페이스가 포함된 문서를 만듭니다.  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XNamespace fc = "www.fourthcoffee.com";  
XElement root = new XElement(aw + "Root",  
    new XAttribute(XNamespace.Xmlns + "aw", aw.NamespaceName),  
    new XAttribute(XNamespace.Xmlns + "fc", fc.NamespaceName),  
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
  
## <a name="example"></a>예  
 동일한 결과를 얻는 또 다른 방법은 <xref:System.Xml.Linq.XNamespace> 개체를 선언하고 만드는 대신 확장된 이름을 사용하는 것입니다.  
  
 이 방법에는 성능과 관련된 문제가 있습니다. 확장된 이름이 포함된 문자열을 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에 전달할 때마다 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 이름을 구문 분석하고 원자화된 네임스페이스를 찾은 다음 원자화된 이름을 찾아야 합니다. 이 과정에는 CPU 시간이 필요합니다. 성능이 중요한 경우에는 <xref:System.Xml.Linq.XNamespace> 개체를 명시적으로 선언하고 사용할 수 있습니다.  
  
 성능이 중요한 경우 자세한 내용을 보려면 [XName 개체의 사전 원자화(LINQ to XML)(C#)](./pre-atomization-of-xname-objects-linq-to-xml.md)를 참조하세요.  
  
```csharp  
// Create an XML tree in a namespace, with a specified prefix  
XElement root = new XElement("{http://www.adventure-works.com}Root",  
    new XAttribute(XNamespace.Xmlns + "aw", "http://www.adventure-works.com"),  
    new XElement("{http://www.adventure-works.com}Child", "child content")  
);  
Console.WriteLine(root);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com">  
  <aw:Child>child content</aw:Child>  
</aw:Root>  
```  
  
## <a name="see-also"></a>참고 항목

- [네임스페이스 개요(LINQ to XML)(C#)](namespaces-overview-linq-to-xml.md)
