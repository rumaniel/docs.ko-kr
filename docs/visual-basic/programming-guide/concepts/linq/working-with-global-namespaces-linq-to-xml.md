---
title: 전역 네임스페이스 작업(Visual Basic)(LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 0a8064d5-e02f-4315-ad48-6deaa443a2f0
ms.openlocfilehash: 9aab6f7175c905fcb3e82829f131f52b3d9368ac
ms.sourcegitcommit: eb9ff6f364cde6f11322e03800d8f5ce302f3c73
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68710380"
---
# <a name="working-with-global-namespaces-visual-basic-linq-to-xml"></a>전역 네임스페이스 작업(Visual Basic)(LINQ to XML)
Visual Basic에서 xml 리터럴의 주요 기능 중 하나는 `Imports` 문을 사용 하 여 xml 네임 스페이스를 선언 하는 기능입니다. 이 기능을 사용하여 접두사를 사용하는 XML 네임스페이스를 선언하거나 기본 XML 네임스페이스를 선언할 수 있습니다.  
  
 이 기능은 두 가지 상황에서 유용합니다. 첫째, XML 리터럴에서 선언된 네임스페이스는 포함 식에까지 영향을 미치지 않습니다. 전역 네임스페이스를 선언하면 네임스페이스와 함께 포함 식을 사용하기 위해 수행해야 하는 작업량이 줄어듭니다. 둘째, XML 속성과 함께 네임스페이스를 사용하기 위해 전역 네임스페이스를 선언해야 합니다.  
  
 프로젝트 수준에서 전역 네임스페이스를 선언할 수 있습니다. 또한 모듈 수준에서 전역 네임스페이스를 선언할 수도 있습니다. 모듈 수준 전역 네임스페이스는 프로젝트 수준 전역 네임스페이스를 무시합니다. 마지막으로 XML 리터럴에서 전역 네임스페이스를 재정의할 수 있습니다.  
  
 전역적으로 선언된 네임스페이스에 있는 XML 속성이나 XML 리터럴을 사용하는 경우 Visual Studio에서 XML 속성이나 XML 리터럴을 마우스로 가리키면 확장된 이름을 볼 수 있습니다. 도구 설명에 확장된 이름이 표시됩니다.  
  
 <xref:System.Xml.Linq.XNamespace> 메서드를 사용하여 전역 네임스페이스에 해당하는 `GetXmlNamespace` 개체를 가져올 수 있습니다.  
  
## <a name="examples-of-global-namespaces"></a>전역 네임스페이스의 예제  
 다음 예제에서는 `Imports` 문을 사용하여 기본 전역 네임스페이스를 선언한 다음 XML 리터럴을 사용하여 해당 네임스페이스에서 <xref:System.Xml.Linq.XElement> 개체를 초기화합니다.  
  
```vb  
Imports <xmlns="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = <Root/>  
        Console.WriteLine(root)  
    End Sub  
End Module  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root xmlns="http://www.adventure-works.com" />  
```  
  
 다음 예제에서는 접두사가 포함된 전역 네임스페이스를 선언한 다음 XML 리터럴을 사용하여 요소를 초기화합니다.  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = <aw:Root/>  
        Console.WriteLine(root)  
    End Sub  
End Module  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com" />  
```  
  
## <a name="global-namespaces-and-embedded-expressions"></a>전역 네임스페이스 및 포함 식  
 XML 리터럴에서 선언된 네임스페이스는 포함 식에까지 영향을 미치지 않습니다. 다음 예제에서는 기본 네임스페이스를 선언한 다음 `Child` 요소에 대한 포함 식을 사용합니다.  
  
```vb  
Dim root As XElement = _  
    <Root xmlns="http://www.adventure-works.com">  
        <%= <Child/> %>  
    </Root>  
Console.WriteLine(root)  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root xmlns="http://www.adventure-works.com">  
  <Child xmlns="" />  
</Root>  
```  
  
 보다시피 생성되는 XML에는 기본 네임스페이스의 선언이 포함됩니다. 따라서 `Child` 요소는 네임스페이스에 없습니다.  
  
 포함 식에서 다음과 같이 네임스페이스를 다시 선언할 수 있습니다.  
  
```vb  
Dim root As XElement = _  
    <Root xmlns="http://www.adventure-works.com">  
        <%= <Child xmlns="http://www.adventure-works.com"/> %>  
    </Root>  
Console.WriteLine(root)  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root xmlns="http://www.adventure-works.com">  
  <Child xmlns="http://www.adventure-works.com" />  
</Root>  
```  
  
 그러나 이 방법은 전역 기본 네임스페이스보다 사용하기가 더 불편합니다. 따라서 전역 기본 네임스페이스를 사용하는 것이 더 좋습니다. 전역 기본 네임스페이스를 사용하면 네임스페이스를 선언하지 않고 XML 리터럴을 사용할 수 있습니다. 생성되는 XML은 전역적으로 선언된 기본 네임스페이스에 있습니다.  
  
```vb  
Imports <xmlns="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = <Root>  
                                   <%= <Child/> %>  
                               </Root>  
        Console.WriteLine(root)  
    End Sub  
End Module  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root xmlns="http://www.adventure-works.com">  
  <Child />  
</Root>  
```  
  
## <a name="using-namespaces-with-xml-properties"></a>XML 속성과 함께 네임스페이스 사용  
 네임스페이스에 있는 XML 트리로 작업하는 경우 XML 속성을 사용하고 있으면 XML 속성도 올바른 네임스페이스에 있도록 전역 네임스페이스를 사용해야 합니다. 다음 예제에서는 네임스페이스에 XML 트리를 선언한 다음 `Child` 요소의 수를 출력합니다.  
  
```vb  
Dim root As XElement = _  
    <Root xmlns="http://www.adventure-works.com">  
        <Child>content</Child>  
    </Root>  
Console.WriteLine(root.<Child>.Count())  
```  
  
 이 예제는 `Child` 요소가 없음을 나타냅니다. 이 예제의 결과는 다음과 같습니다.  
  
```  
0  
```  
  
 그러나 기본 전역 네임스페이스를 선언하는 경우 XML 리터럴과 XML 속성이 모두 기본 전역 네임스페이스에 있습니다.  
  
```vb  
Imports <xmlns="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <Root>  
                <Child>content</Child>  
            </Root>  
        Console.WriteLine(root.<Child>.Count())  
    End Sub  
End Module  
```  
  
 이 예제는 `Child` 요소가 하나 있음을 나타냅니다. 이 예제의 결과는 다음과 같습니다.  
  
```  
1  
```  
  
 접두사가 포함된 전역 네임스페이스를 선언하면 XML 리터럴과 XML 속성 모두에 접두사를 사용할 수 있습니다.  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <aw:Root>  
                <aw:Child>content</aw:Child>  
            </aw:Root>  
        Console.WriteLine(root.<aw:Child>.Count())  
    End Sub  
End Module  
```  
  
## <a name="xnamespace-and-global-namespaces"></a>XNamespace 및 전역 네임스페이스  
 <xref:System.Xml.Linq.XNamespace> 메서드를 사용하여 `GetXmlNamespace` 개체를 가져올 수 있습니다.  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = <aw:Root/>  
        Dim xn As XNamespace = GetXmlNamespace(aw)  
        Console.WriteLine(xn)  
    End Sub  
End Module  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```  
http://www.adventure-works.com  
```  
  
## <a name="see-also"></a>참고자료

- [네임 스페이스 개요 (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md)
