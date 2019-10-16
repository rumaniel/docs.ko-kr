---
title: '방법: 네임 스페이스의 XML에 대 한 쿼리 작성 (Visual Basic)'
ms.date: 07/20/2015
ms.assetid: 7d4131b5-3288-414f-b77c-b2edc2a1f465
ms.openlocfilehash: 71e66791b41e26ea13f828ef6239a8db9a9365b0
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71835002"
---
# <a name="how-to-write-queries-on-xml-in-namespaces-visual-basic"></a>방법: 네임 스페이스의 XML에 대 한 쿼리 작성 (Visual Basic)
네임스페이스에 있는 XML에 대한 쿼리를 작성하려면 올바른 네임스페이스를 가진 <xref:System.Xml.Linq.XName> 개체를 사용해야 합니다.  
  
 Visual Basic을 사용하는 경우 가장 일반적인 방법은 전역 네임스페이스를 정의한 다음 전역 네임스페이스를 사용하는 XML 속성과 XML 리터럴을 사용하는 것입니다. XML 리터럴의 case 요소가 기본적으로 네임스페이스에 있는 전역 기본 네임스페이스를 정의할 수 있습니다. 또는 접두사를 사용하여 전역 네임스페이스를 정의한 다음 필요한 경우 XML 리터럴과 XML 속성에서 접두사를 사용할 수 있습니다. XML의 다른 형태와 마찬가지로 기본적으로 특성은 항상 네임스페이스에 없습니다.  
  
 이 항목의 첫 번째 예제 집합에서는 기본 네임스페이스에 XML 트리를 만드는 방법을 보여 줍니다. 두 번째 예제 집합에서는 접두사가 포함된 네임스페이스에 XML 트리를 만드는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 기본 네임스페이스에 있는 XML 트리를 만든 다음 요소의 컬렉션을 검색합니다.  
  
```vb  
Imports <xmlns="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <Root>  
                <Child>1</Child>  
                <Child>2</Child>  
                <Child>3</Child>  
                <AnotherChild>4</AnotherChild>  
                <AnotherChild>5</AnotherChild>  
                <AnotherChild>6</AnotherChild>  
            </Root>  
        Dim c1 As IEnumerable(Of XElement) = _  
            From el In root.<Child> _  
            Select el  
        For Each el As XElement In c1  
            Console.WriteLine(el.Value)  
        Next  
    End Sub  
End Module  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```console  
1  
2  
3  
```  
  
## <a name="example"></a>예제  
 그러나 Visual Basic의 경우에는 접두사가 포함된 네임스페이스를 사용하는 XML 트리에 쿼리를 작성하는 방법과 기본 네임스페이스를 사용하는 XML 트리에 쿼리를 작성하는 방법이 상당히 다릅니다. 일반적으로 `Imports` 문을 사용하여 접두사가 포함된 네임스페이스를 가져옵니다. 그런 다음 XML 트리를 생성할 때 요소 및 특성 이름에 해당 접두사를 사용합니다. 또한 XML 속성을 사용하여 XML 트리를 쿼리할 때도 접두사를 사용합니다.  
  
 다음 예제에서는 접두사가 포함된 네임스페이스에 있는 XML 트리를 만든 다음 요소의 컬렉션을 검색합니다.  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <aw:Root>  
                <aw:Child>1</aw:Child>  
                <aw:Child>2</aw:Child>  
                <aw:Child>3</aw:Child>  
                <aw:AnotherChild>4</aw:AnotherChild>  
                <aw:AnotherChild>5</aw:AnotherChild>  
                <aw:AnotherChild>6</aw:AnotherChild>  
            </aw:Root>  
        Dim c1 As IEnumerable(Of XElement) = _  
            From el In root.<aw:Child> _  
            Select el  
        For Each el As XElement In c1  
            Console.WriteLine(CInt(el))  
        Next  
    End Sub  
End Module  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```console  
1  
2  
3  
```  
  
## <a name="see-also"></a>참조

- [네임 스페이스 개요 (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md)
