---
title: C#에서 XML 트리 만들기(LINQ to XML)
ms.date: 08/31/2018
ms.assetid: cc74234a-0bac-4327-9c8c-5a2ead15b595
ms.openlocfilehash: a77171ebbc07e54f6988fb97aff197b4c6d31721
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69594627"
---
# <a name="creating-xml-trees-in-c-linq-to-xml"></a>C#에서 XML 트리 만들기(LINQ to XML)
이 단원에서는 C#에서 XML 트리를 만드는 방법에 대해 설명합니다.  
  
 LINQ 쿼리의 결과를 <xref:System.Xml.Linq.XElement>의 내용으로 사용하는 방법에 대한 자세한 내용은 [함수 생성(LINQ to XML)(C#)](./functional-construction-linq-to-xml.md)을 참조하세요.  
  
## <a name="constructing-elements"></a>요소 생성
 <xref:System.Xml.Linq.XElement> 및 <xref:System.Xml.Linq.XAttribute> 생성자의 시그니처를 사용하여 요소나 특성의 내용을 생성자에 인수로 전달할 수 있습니다. 생성자 중 하나의 인수 수가 고정되어 있지 않기 때문에 원하는 수의 자식 요소를 전달할 수 있습니다. 물론 이러한 각 자식 요소에는 자신의 자식 요소가 포함될 수 있습니다. 각 요소에는 원하는 수의 특성을 추가할 수 있습니다.  
  
 <xref:System.Xml.Linq.XNode>(<xref:System.Xml.Linq.XElement> 포함) 또는 <xref:System.Xml.Linq.XAttribute> 개체를 추가할 때 새 내용에 부모가 없으면 개체가 XML 트리에 추가되기만 합니다. 새 내용에 이미 부모가 있고 다른 XML 트리의 일부이면 새 내용이 복제되고 새로 복제된 내용이 XML 트리에 추가됩니다. 이 항목의 마지막 예제에서는 이에 대해 보여 줍니다.  
  
 `contacts`<xref:System.Xml.Linq.XElement>를 만들려면 다음 코드를 사용할 수 있습니다.  
  
```csharp  
XElement contacts =  
    new XElement("Contacts",  
        new XElement("Contact",  
            new XElement("Name", "Patrick Hines"),   
            new XElement("Phone", "206-555-0144"),  
            new XElement("Address",  
                new XElement("Street1", "123 Main St"),  
                new XElement("City", "Mercer Island"),  
                new XElement("State", "WA"),  
                new XElement("Postal", "68042")  
            )  
        )  
    );  
```  
  
 제대로 들여쓰는 경우 <xref:System.Xml.Linq.XElement> 개체를 생성하는 코드는 기본 XML의 구조와 매우 유사합니다.  
  
## <a name="xelement-constructors"></a>XElement 생성자  
 <xref:System.Xml.Linq.XElement> 클래스는 함수 생성을 위해 다음 생성자를 사용합니다. <xref:System.Xml.Linq.XElement>의 다른 생성자도 있지만 함수 생성에 사용되지 않기 때문에 여기에 나와 있지 않습니다.  
  
|생성자|설명|  
|-----------------|-----------------|  
|`XElement(XName name, object content)`|<xref:System.Xml.Linq.XElement>를 만듭니다. `name` 매개 변수는 요소의 이름을 지정하고, `content`는 요소의 내용을 지정합니다.|  
|`XElement(XName name)`|<xref:System.Xml.Linq.XElement>을 지정된 이름으로 초기화하여 <xref:System.Xml.Linq.XName>를 만듭니다.|  
|`XElement(XName name, params object[] content)`|<xref:System.Xml.Linq.XElement>을 지정된 이름으로 초기화하여 <xref:System.Xml.Linq.XName>를 만듭니다. 특성 및/또는 자식 요소는 매개 변수 목록의 내용에서 만들어집니다.|  
  
 `content` 매개 변수는 융통성이 매우 크기 때문에 <xref:System.Xml.Linq.XElement>의 유효한 자식인 모든 형식의 개체를 지원합니다. 이 매개 변수로 전달되는 개체의 형식에 따라 다음과 같은 규칙이 적용됩니다.  
  
- 문자열은 텍스트 내용으로 추가됩니다.  
  
- <xref:System.Xml.Linq.XElement>는 자식 요소로 추가됩니다.  
  
- <xref:System.Xml.Linq.XAttribute>는 특성으로 추가됩니다.  
  
- <xref:System.Xml.Linq.XProcessingInstruction>, <xref:System.Xml.Linq.XComment> 또는 <xref:System.Xml.Linq.XText>는 자식 내용으로 추가됩니다.  
  
- <xref:System.Collections.IEnumerable>이 열거되고 이러한 규칙이 결과에 재귀적으로 적용됩니다.  
  
- 다른 모든 형식의 경우 `ToString` 메서드가 호출되고 결과가 텍스트 내용으로 추가됩니다.  
  
### <a name="creating-an-xelement-with-content"></a>콘텐츠를 사용하여 XElement 만들기  
 메서드를 한 번 호출하여 간단한 내용이 포함된 <xref:System.Xml.Linq.XElement>를 만들 수 있습니다. 이렇게 하려면 다음과 같이 내용을 두 번째 매개 변수로 지정합니다.  
  
```csharp  
XElement n = new XElement("Customer", "Adventure Works");  
Console.WriteLine(n);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Customer>Adventure Works</Customer>  
```  
  
 모든 형식의 개체를 내용으로 전달할 수 있습니다. 예를 들어, 다음 코드에서는 부동 소수점 숫자가 내용으로 포함된 요소를 만듭니다.  
  
```csharp  
XElement n = new XElement("Cost", 324.50);  
Console.WriteLine(n);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Cost>324.5</Cost>  
```  
  
 부동 소수점 숫자는 boxing되어 생성자에 전달됩니다. boxed 숫자는 문자열로 변환되고 요소의 내용으로 사용됩니다.  
  
### <a name="creating-an-xelement-with-a-child-element"></a>자식 요소를 사용하여 XElement 만들기  
 <xref:System.Xml.Linq.XElement> 클래스의 인스턴스를 내용 인수로 전달하면 생성자가 자식 요소를 사용하여 요소를 만듭니다.  
  
```csharp  
XElement shippingUnit = new XElement("ShippingUnit",  
    new XElement("Cost", 324.50)  
);  
Console.WriteLine(shippingUnit);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<ShippingUnit>  
  <Cost>324.5</Cost>  
</ShippingUnit>  
```  
  
### <a name="creating-an-xelement-with-multiple-child-elements"></a>여러 자식 요소를 사용하여 XElement 만들기  
 많은 <xref:System.Xml.Linq.XElement> 개체를 내용으로 전달할 수 있습니다. 각 <xref:System.Xml.Linq.XElement> 개체는 자식 요소로 포함되어 있습니다.  
  
```csharp  
XElement address = new XElement("Address",  
    new XElement("Street1", "123 Main St"),  
    new XElement("City", "Mercer Island"),  
    new XElement("State", "WA"),  
    new XElement("Postal", "68042")  
);  
Console.WriteLine(address);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Address>  
  <Street1>123 Main St</Street1>  
  <City>Mercer Island</City>  
  <State>WA</State>  
  <Postal>68042</Postal>  
</Address>  
```  
  
 위의 예제를 확장하여 다음과 같이 전체 XML 트리를 만들 수 있습니다.  
  
```csharp  
XElement contacts =  
    new XElement("Contacts",  
        new XElement("Contact",  
            new XElement("Name", "Patrick Hines"),                                                   
            new XElement("Phone", "206-555-0144"),  
            new XElement("Address",  
                new XElement("Street1", "123 Main St"),  
                new XElement("City", "Mercer Island"),  
                new XElement("State", "WA"),  
                new XElement("Postal", "68042")  
            )  
        )  
    );  
Console.WriteLine(contacts);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Contacts>  
  <Contact>  
    <Name>Patrick Hines</Name>  
    <Phone>206-555-0144</Phone>  
    <Address>  
      <Street1>123 Main St</Street1>  
      <City>Mercer Island</City>  
      <State>WA</State>  
      <Postal>68042</Postal>  
    </Address>  
  </Contact>  
</Contacts>  
```  

### <a name="creating-an-xelement-with-an-xattribute"></a>XAttribute를 사용하여 XElement 만들기
 <xref:System.Xml.Linq.XAttribute> 클래스의 인스턴스를 내용 인수로 전달하면 생성자가 특성을 사용하여 요소를 만듭니다.

```csharp  
XElement phone = new XElement("Phone",  
    new XAttribute("Type", "Home"),  
    "555-555-5555");  
Console.WriteLine(phone);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Phone Type="Home">555-555-5555</Phone>
```   

### <a name="creating-an-empty-element"></a>빈 요소 만들기  
 빈 <xref:System.Xml.Linq.XElement>를 만들려면 내용을 생성자에 전달하지 않습니다. 다음 예제에서는 빈 요소를 만듭니다.  
  
```csharp  
XElement n = new XElement("Customer");  
Console.WriteLine(n);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Customer />  
```  
  
### <a name="attaching-vs-cloning"></a>추가와 복제 비교  
 위에서 설명했듯이 <xref:System.Xml.Linq.XNode>(<xref:System.Xml.Linq.XElement> 포함) 또는 <xref:System.Xml.Linq.XAttribute> 개체를 추가할 때 새 내용에 부모가 없으면 개체가 XML 트리에 추가되기만 합니다. 새 내용에 이미 부모가 있고 다른 XML 트리의 일부이면 새 내용이 복제되고 새로 복제된 내용이 XML 트리에 추가됩니다.  

다음 예제에서는 부모가 있는 요소를 트리에 추가할 때의 동작과 부모가 없는 요소를 트리에 추가할 때의 동작을 보여 줍니다.

```csharp  
// Create a tree with a child element.  
XElement xmlTree1 = new XElement("Root",  
    new XElement("Child1", 1)  
);  
  
// Create an element that is not parented.  
XElement child2 = new XElement("Child2", 2);  
  
// Create a tree and add Child1 and Child2 to it.  
XElement xmlTree2 = new XElement("Root",  
    xmlTree1.Element("Child1"),  
    child2  
);  
  
// Compare Child1 identity.  
Console.WriteLine("Child1 was {0}",  
    xmlTree1.Element("Child1") == xmlTree2.Element("Child1") ?  
    "attached" : "cloned");  
  
// Compare Child2 identity.  
Console.WriteLine("Child2 was {0}",  
    child2 == xmlTree2.Element("Child2") ?  
    "attached" : "cloned");  

// The example displays the following output:  
//    Child1 was cloned  
//    Child2 was attached  
```

## <a name="see-also"></a>참고 항목

- [XML 트리 만들기(C#)](./linq-to-xml-overview.md)
