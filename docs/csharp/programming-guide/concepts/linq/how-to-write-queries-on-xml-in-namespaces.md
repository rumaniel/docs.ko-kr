---
title: '방법: 네임스페이스에서 XML로 쿼리 작성(C#)'
ms.date: 07/20/2015
ms.assetid: 7c54df81-15e4-4091-8c81-a87637029130
ms.openlocfilehash: 1ded47ced44bebfda92b96f4dc908f1c1b2bbf6b
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253186"
---
# <a name="how-to-write-queries-on-xml-in-namespaces-c"></a>방법: 네임스페이스에서 XML로 쿼리 작성(C#)
네임스페이스에 있는 XML에 대한 쿼리를 작성하려면 올바른 네임스페이스를 가진 <xref:System.Xml.Linq.XName> 개체를 사용해야 합니다.  
  
 C#의 경우 가장 일반적인 방법은 URI가 포함된 문자열을 사용하여 <xref:System.Xml.Linq.XNamespace>를 초기화한 다음 추가 연산자 오버로드를 사용하여 네임스페이스를 로컬 이름과 결합하는 것입니다.  
  
 이 항목의 첫 번째 예제 집합에서는 기본 네임스페이스에 XML 트리를 만드는 방법을 보여 줍니다. 두 번째 예제 집합에서는 접두사가 포함된 네임스페이스에 XML 트리를 만드는 방법을 보여 줍니다.  
  
## <a name="example"></a>예  
 다음 예제에서는 기본 네임스페이스에 있는 XML 트리를 만든 다음 요소의 컬렉션을 검색합니다.  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = XElement.Parse(  
@"<Root xmlns='http://www.adventure-works.com'>  
    <Child>1</Child>  
    <Child>2</Child>  
    <Child>3</Child>  
    <AnotherChild>4</AnotherChild>  
    <AnotherChild>5</AnotherChild>  
    <AnotherChild>6</AnotherChild>  
</Root>");  
IEnumerable<XElement> c1 =  
    from el in root.Elements(aw + "Child")  
    select el;  
foreach (XElement el in c1)  
    Console.WriteLine((int)el);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```output  
1  
2  
3  
```  
  
## <a name="example"></a>예  
 C#의 경우 쿼리를 작성하는 대상이 접두사가 포함된 네임스페이스를 사용하는 XML 트리인지 기본 네임스페이스를 사용하는 XML 트리인지에 관계없이 동일한 방식으로 쿼리를 작성합니다.  
  
 다음 예제에서는 접두사가 포함된 네임스페이스에 있는 XML 트리를 만든 다음 요소의 컬렉션을 검색합니다.  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = XElement.Parse(  
@"<aw:Root xmlns:aw='http://www.adventure-works.com'>  
    <aw:Child>1</aw:Child>  
    <aw:Child>2</aw:Child>  
    <aw:Child>3</aw:Child>  
    <aw:AnotherChild>4</aw:AnotherChild>  
    <aw:AnotherChild>5</aw:AnotherChild>  
    <aw:AnotherChild>6</aw:AnotherChild>  
</aw:Root>");  
IEnumerable<XElement> c1 =  
    from el in root.Elements(aw + "Child")  
    select el;  
foreach (XElement el in c1)  
    Console.WriteLine((int)el);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```output  
1  
2  
3  
```  
  
## <a name="see-also"></a>참고 항목

- [네임스페이스 개요(LINQ to XML)(C#)](namespaces-overview-linq-to-xml.md)
