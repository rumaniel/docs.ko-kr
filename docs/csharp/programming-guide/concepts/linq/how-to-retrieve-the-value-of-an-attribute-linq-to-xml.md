---
title: '방법: 특성 값 검색(LINQ to XML)(C#)'
ms.date: 07/20/2015
ms.assetid: 817bbe89-5979-4234-bf0c-46f63692ac8c
ms.openlocfilehash: 635aee3bd08618b94fb5c091f8eef212c067acef
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253376"
---
# <a name="how-to-retrieve-the-value-of-an-attribute-linq-to-xml-c"></a>방법: 특성 값 검색(LINQ to XML)(C#)
이 항목에서는 특성의 값을 가져오는 방법을 보여 줍니다. 두 가지 주요 방법이 있습니다. <xref:System.Xml.Linq.XAttribute>를 원하는 형식으로 캐스팅할 수 있습니다. 그러면 명시적 변환 연산자가 요소나 특성의 내용을 지정된 형식으로 변환합니다. 또는 <xref:System.Xml.Linq.XAttribute.Value%2A> 속성을 사용할 수 있습니다. 그러나 일반적으로 캐스팅이 더 나은 방법입니다. 특성을 nullable 형식으로 캐스팅하면 존재하지 않을 수도 있는 특성의 값을 검색하는 경우 코드를 더 간단하게 작성할 수 있습니다. 이 기법의 예제는 [방법: 요소 값 검색(LINQ to XML)(C#)](./how-to-retrieve-the-value-of-an-element-linq-to-xml.md)을 참조하세요.  
  
## <a name="example"></a>예  
 특성의 값을 검색하려면 <xref:System.Xml.Linq.XAttribute> 개체를 원하는 형식으로 캐스팅하기만 하면 됩니다.  
  
```csharp  
XElement root = new XElement("Root",  
                    new XAttribute("Attr", "abcde")  
                );  
Console.WriteLine(root);  
string str = (string)root.Attribute("Attr");  
Console.WriteLine(str);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```output  
<Root Attr="abcde" />  
abcde  
```  
  
## <a name="example"></a>예  
 다음 예제에서는 특성이 네임스페이스에 있는 경우 특성의 값을 검색하는 방법을 보여 줍니다. 자세한 내용은 [네임스페이스 개요(LINQ to XML)(C#)](namespaces-overview-linq-to-xml.md)를 참조하세요.  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = new XElement(aw + "Root",  
                    new XAttribute(aw + "Attr", "abcde")  
                );  
string str = (string)root.Attribute(aw + "Attr");  
Console.WriteLine(str);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```output  
abcde  
```  
  
## <a name="see-also"></a>참고 항목

- [LINQ to XML 축(C#)](./linq-to-xml-axes-overview.md)
