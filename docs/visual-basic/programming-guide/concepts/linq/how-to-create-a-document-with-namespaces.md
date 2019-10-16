---
title: '방법: 네임 스페이스를 사용 하 여 문서 만들기 (LINQ to XML) (Visual Basic)'
ms.date: 07/20/2015
ms.assetid: cc5b0d4d-360c-4ada-94fa-2d2916e989be
ms.openlocfilehash: c61076da5616d98673c4b9258125e3ff0c8821aa
ms.sourcegitcommit: eb9ff6f364cde6f11322e03800d8f5ce302f3c73
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68710450"
---
# <a name="how-to-create-a-document-with-namespaces-linq-to-xml-visual-basic"></a>방법: 네임 스페이스를 사용 하 여 문서 만들기 (LINQ to XML) (Visual Basic)
이 항목에서는 Visual Basic에서 네임스페이스를 사용하여 문서를 만드는 방법을 보여 줍니다.  
  
 Visual Basic에서 XML 리터럴을 사용할 때 사용자는 하나의 전역 기본 XML 네임스페이스를 정의할 수 있습니다. 이 네임스페이스는 XML 리터럴과 XML 속성의 기본 네임스페이스입니다. 기본 XML 네임스페이스는 프로젝트 수준이나 파일 수준에서 정의될 수 있습니다. 기본 XML 네임스페이스가 파일 수준에서 정의되면 프로젝트 수준의 기본 네임스페이스가 무시됩니다.  
  
 다른 네임스페이스를 정의하고 해당 네임스페이스의 네임스페이스 접두사를 지정할 수도 있습니다.  
  
 `Imports` 키워드를 사용하여 기본 네임스페이스와 접두사가 포함된 네임스페이스를 모두 정의할 수 있습니다.  
  
 자세한 내용은 [Visual Basic의 XML 리터럴 소개](../../../../visual-basic/programming-guide/concepts/linq/introduction-to-xml-literals.md)를 참조 하세요.  
  
 기본 XML 네임스페이스는 요소에만 적용되고 특성에는 적용되지 않습니다. 특성은 기본적으로 항상 네임스페이스에 없습니다. 그러나 네임스페이스 접두사를 사용하여 특성을 네임스페이스에 배치할 수 있습니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 네임스페이스가 포함된 문서를 만듭니다.  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <aw:Root>  
                <aw:Child aw:Att="attvalue"/>  
            </aw:Root>  
        Console.WriteLine(root)  
    End Sub  
End Module  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com">  
  <aw:Child aw:Att="attvalue" />  
</aw:Root>  
```  
  
## <a name="example"></a>예제  
 이 예제에서는 두 네임스페이스가 포함된 문서를 만듭니다. 두 네임스페이스 중 하나는 기본 네임스페이스입니다.  
  
```vb  
Imports <xmlns="http://www.adventure-works.com">  
Imports <xmlns:fc="www.fourthcoffee.com">  
  
Module Module1  
  
    Sub Main()  
        Dim root As XElement = _  
            <Root>  
                <Child Att="attvalue"/>  
                <fc:Child2>child2 content</fc:Child2>  
            </Root>  
        Console.WriteLine(root)  
    End Sub  
  
End Module  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root xmlns:fc="www.fourthcoffee.com" xmlns="http://www.adventure-works.com">  
  <Child Att="attvalue" />  
  <fc:Child2>child2 content</fc:Child2>  
</Root>  
```  
  
## <a name="example"></a>예제  
 다음 예제에서는 네임스페이스 접두사가 포함된 여러 네임스페이스가 포함된 문서를 만듭니다.  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 XML 트리를 serialize할 때 각 요소가 지정된 네임스페이스에 있도록 필요에 따라 네임스페이스 선언을 생성합니다.  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
Imports <xmlns:fc="www.fourthcoffee.com">  
  
Module Module1  
  
    Sub Main()  
        Dim root As XElement = _  
            <aw:Root>  
                <fc:Child>  
                    <aw:DifferentChild>other content</aw:DifferentChild>  
                </fc:Child>  
                <aw:Child2>c2 content</aw:Child2>  
                <fc:Child3>c3 content</fc:Child3>  
            </aw:Root>  
        Console.WriteLine(root)  
    End Sub  
  
End Module  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<aw:Root xmlns:fc="www.fourthcoffee.com" xmlns:aw="http://www.adventure-works.com">  
  <fc:Child>  
    <aw:DifferentChild>other content</aw:DifferentChild>  
  </fc:Child>  
  <aw:Child2>c2 content</aw:Child2>  
  <fc:Child3>c3 content</fc:Child3>  
</aw:Root>  
```  
  
## <a name="see-also"></a>참고자료

- [네임 스페이스 개요 (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md)
