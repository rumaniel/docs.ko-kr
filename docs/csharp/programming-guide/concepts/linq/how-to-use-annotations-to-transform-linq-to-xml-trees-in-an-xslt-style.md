---
title: '방법: XSLT 스타일에서 주석을 사용하여 LINQ to XML 트리 변환(C#)'
ms.date: 07/20/2015
ms.assetid: 12a95902-a6b7-4a1e-ad52-04a518db226f
ms.openlocfilehash: d6975601855e736082662ffb0319b5c6563cedc6
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253270"
---
# <a name="how-to-use-annotations-to-transform-linq-to-xml-trees-in-an-xslt-style-c"></a>방법: XSLT 스타일에서 주석을 사용하여 LINQ to XML 트리 변환(C#)
주석을 사용하여 XML 트리를 쉽게 변환할 수 있습니다.  
  
 일부 XML 문서는 "혼합 내용이 포함된 문서 중심적"입니다. 이러한 문서를 사용하는 경우 요소의 자식 노드 모양을 반드시 알아야 할 필요가 없습니다. 예를 들어, 텍스트가 포함된 노드는 다음과 같을 수 있습니다.  
  
```xml  
<text>A phrase with <b>bold</b> and <i>italic</i> text.</text>  
```  
  
 지정된 텍스트 노드에는 자식 `<b>` 및 `<i>` 요소가 임의의 개수만큼 있을 수 있습니다. 이 방법은 많은 다른 상황으로 확장됩니다. 예를 들어 일반 단락, 글머리 기호 단락 및 비트맵과 같은 다양한 자식 요소를 포함할 수 있는 페이지로 확장될 수 있습니다. 표의 셀에는 텍스트, 드롭다운 목록 또는 비트맵이 포함될 수 있습니다. 문서 중심 XML의 기본 특징 중 하나는 특정 요소에 포함될 자식 요소에 대해 알 수 없다는 것입니다.  
  
 변환할 요소의 자식에 대해 반드시 자세히 알아야 할 필요가 없는 트리에서 요소를 변환하려면 주석을 사용하는 이 방법이 효과적인 방법입니다.  
  
 이 방법을 요약하면 다음과 같습니다.  
  
- 첫째, 트리의 요소에 대체 요소로 주석을 답니다.  
  
- 둘째, 전체 트리를 반복하여 각 요소를 주석으로 대체하는 새 트리를 만듭니다. 이 예제에서는 `XForm`이라는 함수에서 새 트리의 반복과 생성을 구현합니다.  
  
 이 방법을 자세히 살펴보면 다음과 같습니다.  
  
- 모양을 변환할 요소의 집합을 반환하는 LINQ to XML 쿼리를 하나 이상 실행합니다. 쿼리의 각 요소에 새 <xref:System.Xml.Linq.XElement> 개체를 주석으로 추가합니다. 이 새 요소는 변환된 새 트리에서 주석이 달린 요소를 대체합니다. 예제에 나와 있듯이 이 코드는 간단하게 작성할 수 있습니다.  
  
- 주석으로 추가된 새 요소는 새 자식 노드를 포함할 수 있으며 원하는 모양의 하위 트리를 형성할 수 있습니다.  
  
- 특별한 규칙이 있습니다. 새 요소의 자식 노드가 이 목적을 위해 구성된 다른 네임스페이스(이 예제에서는 네임스페이스가 `http://www.microsoft.com/LinqToXmlTransform/2007`임)에 있으면 해당 자식 요소가 새 트리에 복사되지 않습니다. 대신 네임스페이스가 위에서 언급한 특수 네임스페이스이고 요소의 로컬 이름이 `ApplyTransforms`이면 소스 트리에 있는 요소의 자식 노드가 반복되고 새 트리에 복사됩니다. 단, 주석이 달린 자식 요소는 이러한 규칙에 따라 스스로 변환됩니다.  
  
- 이 방법은 XSL의 변환 사양과 다소 유사합니다. 일련의 노드를 선택하는 쿼리는 템플릿에 대한 XPath 식과 유사합니다. 주석으로 저장된 새 <xref:System.Xml.Linq.XElement>를 만들 코드는 XSL의 시퀀스 생성자와 유사하고 `ApplyTransforms` 요소는 XSL의 `xsl:apply-templates` 요소와 기능 면에서 유사합니다.  
  
- 이 방법을 사용하는 경우의 한 가지 이점은 쿼리를 만들 때 항상 수정되지 않은 소스 트리에 대한 쿼리를 작성한다는 점입니다. 트리의 수정이 작성하고 있는 쿼리에 미치는 영향에 대해 우려할 필요가 없습니다.  
  
## <a name="transforming-a-tree"></a>트리 변환  
 이 첫 번째 예제에서는 모든 `Paragraph` 노드의 이름을 `para`로 바꿉니다.  
  
```csharp  
XNamespace xf = "http://www.microsoft.com/LinqToXmlTransform/2007";  
XName at = xf + "ApplyTransforms";  
  
XElement root = XElement.Parse(@"  
<Root>  
    <Paragraph>This is a sentence with <b>bold</b> and <i>italic</i> text.</Paragraph>  
    <Paragraph>More text.</Paragraph>  
</Root>");  
  
// replace Paragraph with para  
foreach (var el in root.Descendants("Paragraph"))  
    el.AddAnnotation(  
        new XElement("para",  
            // same idea as xsl:apply-templates  
            new XElement(xf + "ApplyTransforms")  
        )  
    );  
  
// The XForm method, shown later in this topic, accomplishes the transform  
XElement newRoot = XForm(root);  
  
Console.WriteLine(newRoot);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```xml  
<Root>  
  <para>This is a sentence with <b>bold</b> and <i>italic</i> text.</para>  
  <para>More text.</para>  
</Root>  
```  
  
## <a name="a-more-complicated-transform"></a>더욱 복잡한 변환  
 다음 예제에서는 트리를 쿼리하고 `Data` 요소의 평균과 합계를 계산한 다음 계산 결과를 새 요소로 트리에 추가합니다.  
  
```csharp  
XNamespace xf = "http://www.microsoft.com/LinqToXmlTransform/2007";  
XName at = xf + "ApplyTransforms";  
  
XElement data = new XElement("Root",  
    new XElement("Data", 20),  
    new XElement("Data", 10),  
    new XElement("Data", 3)  
);  
  
// while adding annotations, you can query the source tree all you want,  
// as the tree is not mutated while annotating.
var avg = data.Elements("Data").Select(z => (Decimal)z).Average();
data.AddAnnotation(  
    new XElement("Root",  
        new XElement(xf + "ApplyTransforms"),  
        new XElement("Average", $"{avg:F4}"),
        new XElement("Sum",  
            data  
            .Elements("Data")  
            .Select(z => (int)z)  
            .Sum()  
        )  
    )  
);  
  
Console.WriteLine("Before Transform");  
Console.WriteLine("----------------");  
Console.WriteLine(data);  
Console.WriteLine();  
Console.WriteLine();  
  
// The XForm method, shown later in this topic, accomplishes the transform  
XElement newData = XForm(data);  
  
Console.WriteLine("After Transform");  
Console.WriteLine("----------------");  
Console.WriteLine(newData);  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```output  
Before Transform  
----------------  
<Root>  
  <Data>20</Data>  
  <Data>10</Data>  
  <Data>3</Data>  
</Root>  
  
After Transform  
----------------  
<Root>  
  <Data>20</Data>  
  <Data>10</Data>  
  <Data>3</Data>  
  <Average>11.0000</Average>  
  <Sum>33</Sum>  
</Root>  
```  
  
## <a name="effecting-the-transform"></a>변환에 영향 미치기  
 작은 함수인 `XForm`은 주석이 달린 원래 트리에서 변환된 새 트리를 만듭니다.  
  
- 이 함수의 의사(pseudo) 코드는 매우 간단합니다.  
  
```text  
The function takes an XElement as an argument and returns an XElement.   
If an element has an XElement annotation, then  
    Return a new XElement  
        The name of the new XElement is the annotation element's name.  
        All attributes are copied from the annotation to the new node.  
        All child nodes are copied from the annotation, with the  
            exception that the special node xf:ApplyTransforms is  
            recognized, and the source element's child nodes are  
            iterated. If the source child node is not an XElement, it  
            is copied to the new tree. If the source child is an  
            XElement, then it is transformed by calling this function  
            recursively.  
If an element is not annotated  
    Return a new XElement  
        The name of the new XElement is the source element's name  
        All attributes are copied from the source element to the  
            destination's element.  
        All child nodes are copied from the source element.  
        If the source child node is not an XElement, it is copied to  
            the new tree. If the source child is an XElement, then it  
            is transformed by calling this function recursively.  
```  
  
 이 함수의 구현은 다음과 같습니다.  
  
```csharp  
// Build a transformed XML tree per the annotations  
static XElement XForm(XElement source)  
{  
    XNamespace xf = "http://www.microsoft.com/LinqToXmlTransform/2007";  
    XName at = xf + "ApplyTransforms";  
  
    if (source.Annotation<XElement>() != null)  
    {  
        XElement anno = source.Annotation<XElement>();  
        return new XElement(anno.Name,  
            anno.Attributes(),  
            anno  
            .Nodes()  
            .Select(  
                (XNode n) =>  
                {  
                    XElement annoEl = n as XElement;  
                    if (annoEl != null)  
                    {  
                        if (annoEl.Name == at)  
                            return (object)(  
                                source.Nodes()  
                                .Select(  
                                    (XNode n2) =>  
                                    {  
                                        XElement e2 = n2 as XElement;  
                                        if (e2 == null)  
                                            return n2;  
                                        else  
                                            return XForm(e2);  
                                    }  
                                )  
                            );  
                        else  
                            return n;  
                    }  
                    else  
                        return n;  
                }  
            )  
        );  
    }  
    else  
    {  
        return new XElement(source.Name,  
            source.Attributes(),  
            source  
                .Nodes()  
                .Select(n =>  
                {  
                    XElement el = n as XElement;  
                    if (el == null)  
                        return n;  
                    else  
                        return XForm(el);  
                }  
                )  
        );  
    }  
}   
```  
  
## <a name="complete-example"></a>완성된 예제  
 다음 코드는 `XForm` 함수가 포함된 전체 예제입니다. 이 코드에는 이러한 유형의 변환에 대한 몇 가지 일반적인 사용이 포함되어 있습니다.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Xml;  
using System.Xml.Linq;  
  
class Program  
{  
    static XNamespace xf = "http://www.microsoft.com/LinqToXmlTransform/2007";  
    static XName at = xf + "ApplyTransforms";  
  
    // Build a transformed XML tree per the annotations  
    static XElement XForm(XElement source)  
    {  
        if (source.Annotation<XElement>() != null)  
        {  
            XElement anno = source.Annotation<XElement>();  
            return new XElement(anno.Name,  
                anno.Attributes(),  
                anno  
                .Nodes()  
                .Select(  
                    (XNode n) =>  
                    {  
                        XElement annoEl = n as XElement;  
                        if (annoEl != null)  
                        {  
                            if (annoEl.Name == at)  
                                return (object)(  
                                    source.Nodes()  
                                    .Select(  
                                        (XNode n2) =>  
                                        {  
                                            XElement e2 = n2 as XElement;  
                                            if (e2 == null)  
                                                return n2;  
                                            else  
                                                return XForm(e2);  
                                        }  
                                    )  
                                );  
                            else  
                                return n;  
                        }  
                        else  
                            return n;  
                    }  
                )  
            );  
        }  
        else  
        {  
            return new XElement(source.Name,  
                source.Attributes(),  
                source  
                    .Nodes()  
                    .Select(n =>  
                    {  
                        XElement el = n as XElement;  
                        if (el == null)  
                            return n;  
                        else  
                            return XForm(el);  
                    }  
                    )  
            );  
        }  
    }  
  
    static void Main(string[] args)  
    {  
        XElement root = new XElement("Root",  
            new XComment("A comment"),  
            new XAttribute("Att1", 123),  
            new XElement("Child", 1),  
            new XElement("Child", 2),  
            new XElement("Other",  
                new XElement("GC", 3),  
                new XElement("GC", 4)  
            ),  
            XElement.Parse(  
              "<SomeMixedContent>This is <i>an</i> element that " +  
              "<b>has</b> some mixed content</SomeMixedContent>"),  
            new XElement("AnUnchangedElement", 42)  
        );  
  
        // each of the following serves the same semantic purpose as  
        // XSLT templates and sequence constructors  
  
        // replace Child with NewChild  
        foreach (var el in root.Elements("Child"))  
            el.AddAnnotation(new XElement("NewChild", (string)el));  
  
        // replace first GC with GrandChild, add an attribute  
        foreach (var el in root.Descendants("GC").Take(1))  
            el.AddAnnotation(  
                new XElement("GrandChild",  
                    new XAttribute("ANewAttribute", 999),  
                    (string)el  
                )  
            );  
  
        // replace Other with NewOther, add new child elements around original content  
        foreach (var el in root.Elements("Other"))  
            el.AddAnnotation(  
                new XElement("NewOther",  
                    new XElement("MyNewChild", 1),  
                    // same idea as xsl:apply-templates  
                    new XElement(xf + "ApplyTransforms"),  
                    new XElement("ChildThatComesAfter")  
                )  
            );  
  
        // change name of element that has mixed content  
        root.Descendants("SomeMixedContent").First().AddAnnotation(  
            new XElement("MixedContent",  
                new XElement(xf + "ApplyTransforms")  
            )  
        );  
  
        // replace <b> with <Bold>  
        foreach (var el in root.Descendants("b"))  
            el.AddAnnotation(  
                new XElement("Bold",  
                    new XElement(xf + "ApplyTransforms")  
                )  
            );  
  
        // replace <i> with <Italic>  
        foreach (var el in root.Descendants("i"))  
            el.AddAnnotation(  
                new XElement("Italic",  
                    new XElement(xf + "ApplyTransforms")  
                )  
            );  
  
        Console.WriteLine("Before Transform");  
        Console.WriteLine("----------------");  
        Console.WriteLine(root);  
        Console.WriteLine();  
        Console.WriteLine();  
        XElement newRoot = XForm(root);  
  
        Console.WriteLine("After Transform");  
        Console.WriteLine("----------------");  
        Console.WriteLine(newRoot);  
    }  
}  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```output  
Before Transform  
----------------  
<Root Att1="123">  
  <!--A comment-->  
  <Child>1</Child>  
  <Child>2</Child>  
  <Other>  
    <GC>3</GC>  
    <GC>4</GC>  
  </Other>  
  <SomeMixedContent>This is <i>an</i> element that <b>has</b> some mixed content</SomeMixedContent>  
  <AnUnchangedElement>42</AnUnchangedElement>  
</Root>  
  
After Transform  
----------------  
<Root Att1="123">  
  <!--A comment-->  
  <NewChild>1</NewChild>  
  <NewChild>2</NewChild>  
  <NewOther>  
    <MyNewChild>1</MyNewChild>  
    <GrandChild ANewAttribute="999">3</GrandChild>  
    <GC>4</GC>  
    <ChildThatComesAfter />  
  </NewOther>  
  <MixedContent>This is <Italic>an</Italic> element that <Bold>has</Bold> some mixed content</MixedContent>  
  <AnUnchangedElement>42</AnUnchangedElement>  
</Root>  
```  
  