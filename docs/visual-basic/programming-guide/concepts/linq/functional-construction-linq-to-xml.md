---
title: 함수 생성 (LINQ to XML) (Visual Basic)
ms.date: 07/20/2015
ms.assetid: feac4273-39ab-43ae-bab7-4059c807a785
ms.openlocfilehash: a942d4a0fa4c33cf4699c5825ea05403bdfce48f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64618329"
---
# <a name="functional-construction-linq-to-xml-visual-basic"></a>함수 생성 (LINQ to XML) (Visual Basic)
[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서는 *함수 생성*이라는 XML 요소를 만드는 강력한 방법을 제공합니다. 함수 생성은 단일 문으로 XML 트리를 만드는 기능입니다.  
  
 함수 생성을 가능하게 하는 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 프로그래밍 인터페이스의 몇 가지 주요 기능은 다음과 같습니다.  
  
- <xref:System.Xml.Linq.XElement> 생성자는 내용에 대한 다양한 형식의 인수를 사용합니다. 예를 들어, 자식 요소가 되는 다른 <xref:System.Xml.Linq.XElement> 개체를 전달할 수 있으며 요소의 특성이 되는 <xref:System.Xml.Linq.XAttribute> 개체를 전달할 수 있습니다. 또는 문자열로 변환되고 요소의 텍스트 내용이 되는 다른 모든 형식의 개체를 전달할 수 있습니다.  
  
- <xref:System.Xml.Linq.XElement> 생성자는 `params` 형식의 <xref:System.Object> 배열을 사용하므로 생성자에 개수에 관계없이 개체를 전달할 수 있습니다. 따라서 복잡한 내용을 가진 요소를 만들 수 있습니다.  
  
- 개체가 <xref:System.Collections.Generic.IEnumerable%601>을 구현하는 경우 개체의 컬렉션이 열거되고 컬렉션의 모든 항목이 추가됩니다. 컬렉션에 <xref:System.Xml.Linq.XElement> 또는 <xref:System.Xml.Linq.XAttribute> 개체가 포함되어 있으면 컬렉션의 각 항목이 개별적으로 추가됩니다. 이것은 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리의 결과를 생성자에 전달할 수 있도록 하기 때문에 중요합니다.  
  
 예를 들면 다음과 같습니다.  
  
 이러한 기능을 사용 하는 XML 트리를 만드는 및 결과 사용 하는 코드를 쓸 XML 리터럴을 사용 하는 코드를 작성할 수 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] XML 트리를 만들면 쿼리:  
  
```vb  
Dim srcTree As XElement = _  
    <Root>  
        <Element>1</Element>  
        <Element>2</Element>  
        <Element>3</Element>  
        <Element>4</Element>  
        <Element>5</Element>  
    </Root>  
Dim xmlTree As XElement = _  
    <Root>  
        <Child>1</Child>  
        <Child>2</Child>  
        <%= From el In srcTree.Elements() _  
            Where CInt(el) > 2 _  
            Select el %>  
    </Root>  
Console.WriteLine(xmlTree)  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root>  
  <Child>1</Child>  
  <Child>2</Child>  
  <Element>3</Element>  
  <Element>4</Element>  
  <Element>5</Element>  
</Root>  
```  
  
## <a name="see-also"></a>참고자료

- [XML 트리 만들기 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-xml-trees.md)
