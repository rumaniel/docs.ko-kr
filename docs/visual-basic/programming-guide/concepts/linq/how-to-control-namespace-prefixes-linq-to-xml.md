---
title: '방법: 컨트롤 네임 스페이스 접두사 (Visual Basic) (LINQ to XML)'
ms.date: 07/20/2015
ms.assetid: 2fcf28a5-31b6-409d-84ea-27c22f71fc9f
ms.openlocfilehash: 2b89b49aa76df526c08143cad49685386ffd5e7c
ms.sourcegitcommit: eb9ff6f364cde6f11322e03800d8f5ce302f3c73
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68709825"
---
# <a name="how-to-control-namespace-prefixes-visual-basic-linq-to-xml"></a>방법: 컨트롤 네임 스페이스 접두사 (Visual Basic) (LINQ to XML)
이 항목에서는 네임스페이스 접두사를 제어하는 방법에 대해 설명합니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>Description  
 이 예제에서는 두 네임스페이스를 선언한 다음 `http://www.adventure-works.com` 네임 스페이스에 `aw`접두사가 `www.fourthcoffee.com` 있고 네임 스페이스의 접두사가 `fc`임을 지정 합니다.  
  
### <a name="code"></a>코드  
  
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
  
### <a name="comments"></a>주석  
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
