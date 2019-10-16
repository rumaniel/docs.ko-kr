---
title: '방법: XSLT 스타일에서 주석을 사용 하 여 LINQ to XML 트리 변환 (Visual Basic)'
ms.date: 07/20/2015
ms.assetid: 08e91fa2-dac2-4463-9ef1-87b1ac3fa890
ms.openlocfilehash: aa0561ecc26139d191107521a8bb5fc2889332cd
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71835066"
---
# <a name="how-to-use-annotations-to-transform-linq-to-xml-trees-in-an-xslt-style-visual-basic"></a>방법: XSLT 스타일에서 주석을 사용 하 여 LINQ to XML 트리 변환 (Visual Basic)
주석을 사용하여 XML 트리를 쉽게 변환할 수 있습니다.  
  
 일부 XML 문서는 "혼합 내용이 포함된 문서 중심적"입니다. 이러한 문서를 사용하는 경우 요소의 자식 노드 모양을 반드시 알아야 할 필요가 없습니다. 예를 들어, 텍스트가 포함된 노드는 다음과 같을 수 있습니다.  
  
```xml  
<text>A phrase with <b>bold</b> and <i>italic</i> text.</text>  
```  
  
 지정된 텍스트 노드에는 자식 `<b>` 및 `<i>` 요소가 임의의 개수만큼 있을 수 있습니다. 이 방법은 다양 한 상황 (예: 일반 단락, 글머리 기호 단락 및 비트맵과 같은 다양 한 자식 요소를 포함할 수 있는 페이지)으로 확장 됩니다. 표의 셀에는 텍스트, 드롭다운 목록 또는 비트맵이 포함될 수 있습니다. 문서 중심 XML의 기본 특징 중 하나는 특정 요소에 포함될 자식 요소에 대해 알 수 없다는 것입니다.  
  
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
  
```vb  
Imports <xmlns:xf="http://www.microsoft.com/LinqToXmlTransform/2007">  
  
Module Module1  
    Dim at As XName = GetXmlNamespace(xf) + "ApplyTransforms"  
  
    Sub Main()  
        Dim root As XElement = _  
            <Root>  
                <Paragraph>This is a sentence with <b>bold</b> and <i>italic</i> text.</Paragraph>  
                <Paragraph>More text.</Paragraph>  
            </Root>  
  
        ' Replace Paragraph with p.  
        For Each el In root...<Paragraph>  
            ' same idea as xsl:apply-templates  
            el.AddAnnotation( _  
                <para>  
                    <<%= at %>></>  
                </para>)  
        Next  
  
        ' The XForm function, shown later in this topic, accomplishes the transform  
        Dim newRoot As XElement = XForm(root)  
        Console.WriteLine(newRoot)  
    End Sub  
End Module  
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
  
```vb  
Imports <xmlns:xf="http://www.microsoft.com/LinqToXmlTransform/2007">  
  
Module Module1  
    Dim at As XName = GetXmlNamespace(xf) + "ApplyTransforms"  
  
    Sub Main()  
        Dim data As XElement = _  
            <Root>  
                <Data>20</Data>  
                <Data>10</Data>  
                <Data>3</Data>  
            </Root>  
  
        ' While adding annotations, you can query the source tree all you want,  
        ' as the tree is not mutated while annotating.  
        data.AddAnnotation( _  
            <Root>  
                <<%= at %>/>  
                <Average>  
                    <%= _  
                        String.Format("{0:F4}", _  
                        data.Elements("Data") _  
                        .Select(Function(z) CDec(z)).Average()) _  
                    %>  
                </Average>  
                <Sum>  
                    <%= _  
                        data.Elements("Data").Select(Function(z) CInt(z)).Sum() _  
                    %>  
                </Sum>  
            </Root> _  
        )  
  
        Console.WriteLine("Before Transform")  
        Console.WriteLine("----------------")  
        Console.WriteLine(data)  
        Console.WriteLine(vbNewLine)  
  
        ' The XForm function, shown later in this topic, accomplishes the transform  
        Dim newData As XElement = XForm(data)  
  
        Console.WriteLine("After Transform")  
        Console.WriteLine("----------------")  
        Console.WriteLine(newData)  
    End Sub  
End Module   
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```console
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
  
이 함수의 의사(pseudo) 코드는 매우 간단합니다.  
  
> 함수는 XElement를 인수로 사용 하 여 XElement를 반환 합니다.
>   
> 요소에 XElement 주석이 있으면 새 XElement을 반환 합니다.  
>    - 새 XElement의 이름은 주석 요소의 이름입니다.  
>    - 모든 특성이 주석에서 새 노드로 복사 됩니다.  
>    - 특수 노드 xf: ApplyTransforms이 인식 되 고 원본 요소의 자식 노드가 반복 되는 예외를 제외 하 고 모든 자식 노드가 주석에 복사 됩니다. 원본 자식 노드가 XElement이 아닌 경우 새 트리로 복사 됩니다. 소스 자식이 XElement 인 경우이 함수를 재귀적으로 호출 하 여 변환 됩니다.
>  
> 요소에 주석이 추가 되지 않은 경우:  
>    - 새 XElement 반환  
>        - 새 XElement의 이름은 원본 요소의 이름입니다.  
>        - 모든 특성이 소스 요소에서 대상의 요소로 복사 됩니다.  
>        - 모든 자식 노드가 원본 요소에서 복사 됩니다.  
>        - 원본 자식 노드가 XElement이 아닌 경우 새 트리로 복사 됩니다. 소스 자식이 XElement 인 경우이 함수를 재귀적으로 호출 하 여 변환 됩니다.  

이 함수의 구현은 다음과 같습니다.  
  
```vb  
' Build a transformed XML tree per the annotations.  
Function XForm(ByVal source As XElement) As XElement  
    If source.Annotation(Of XElement)() IsNot Nothing Then  
        Dim anno As XElement = source.Annotation(Of XElement)()  
        Return _  
            <<%= anno.Name.ToString() %>>  
                <%= anno.Attributes() %>  
                <%= anno.Nodes().Select(Function(n As XNode) _  
                    GetSubNodes(n, source)) %>  
            </>  
    Else  
        Return _  
            <<%= source.Name %>>  
                <%= source.Attributes() %>  
                <%= source.Nodes().Select(Function(n) GetExpandedNodes(n)) %>  
            </>  
    End If  
End Function  
  
Private Function GetSubNodes(ByVal n As XNode, ByVal s As XElement) As Object  
    Dim annoEl As XElement = TryCast(n, XElement)  
    If annoEl IsNot Nothing Then  
        If annoEl.Name = at Then  
            Return s.Nodes().Select(Function(n2 As XNode) GetExpandedNodes(n2))  
        End If  
    End If  
    Return n  
End Function  
  
Private Function GetExpandedNodes(ByVal n2 As XNode) As XNode  
    Dim e2 As XElement = TryCast(n2, XElement)  
    If e2 Is Nothing Then  
        Return n2  
    Else  
        Return XForm(e2)  
    End If  
End Function  
```  
  
## <a name="complete-example"></a>완성된 예제  
 다음 코드는 `XForm` 함수가 포함된 전체 예제입니다. 이 코드에는 이러한 유형의 변환에 대한 몇 가지 일반적인 사용이 포함되어 있습니다.  
  
```vb  
Imports System  
Imports System.Collections.Generic  
Imports System.Linq  
Imports System.Text  
Imports System.Xml  
Imports System.Xml.Linq  
  
Imports <xmlns:xf="http://www.microsoft.com/LinqToXmlTransform/2007">  
  
Module Module1  
    Dim at As XName = GetXmlNamespace(xf) + "ApplyTransforms"  
  
    ' Build a transformed XML tree per the annotations.  
    Function XForm(ByVal source As XElement) As XElement  
        If source.Annotation(Of XElement)() IsNot Nothing Then  
            Dim anno As XElement = source.Annotation(Of XElement)()  
            Return _  
                <<%= anno.Name.ToString() %>>  
                    <%= anno.Attributes() %>  
                    <%= anno.Nodes().Select(Function(n As XNode) _  
                        GetSubNodes(n, source)) %>  
                </>  
        Else  
            Return _  
                <<%= source.Name %>>  
                    <%= source.Attributes() %>  
                    <%= source.Nodes().Select(Function(n) GetExpandedNodes(n)) %>  
                </>  
        End If  
    End Function  
  
    Private Function GetSubNodes(ByVal n As XNode, ByVal s As XElement) As Object  
        Dim annoEl As XElement = TryCast(n, XElement)  
        If annoEl IsNot Nothing Then  
            If annoEl.Name = at Then  
                Return s.Nodes().Select(Function(n2 As XNode) GetExpandedNodes(n2))  
            End If  
        End If  
        Return n  
    End Function  
  
    Private Function GetExpandedNodes(ByVal n2 As XNode) As XNode  
        Dim e2 As XElement = TryCast(n2, XElement)  
        If e2 Is Nothing Then  
            Return n2  
        Else  
            Return XForm(e2)  
        End If  
    End Function  
  
    Sub Main()  
        Dim root As XElement = _  
<Root Att1='123'>  
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
  
        ' Each of the following serves the same semantic purpose as  
        ' XSLT templates and sequence constructors.  
  
        ' Replace Child with NewChild.  
        For Each el In root.<Child>  
            el.AddAnnotation(<NewChild><%= CStr(el) %></NewChild>)  
        Next  
  
        ' Replace first GC with GrandChild, add an attribute.  
        For Each el In root...<GC>.Take(1)  
            el.AddAnnotation(<GrandChild ANewAttribute='999'><%= CStr(el) %></GrandChild>)  
        Next  
  
        ' Replace Other with NewOther, add new child elements around original content.  
        For Each el In root.<Other>  
            el.AddAnnotation( _  
                <NewOther>  
                    <MyNewChild>1</MyNewChild>  
                    <<%= at %>></>  
                    <ChildThatComesAfter/>  
                </NewOther>)  
        Next  
  
        ' Change name of element that has mixed content.  
        root...<SomeMixedContent>(0).AddAnnotation( _  
                <MixedContent><<%= at %>></></MixedContent>)  
  
        ' Replace <b> with <Bold>.  
        For Each el In root...<b>  
            el.AddAnnotation(<Bold><<%= at %>></></Bold>)  
        Next  
  
        ' Replace <i> with <Italic>.  
        For Each el In root...<i>  
            el.AddAnnotation(<Italic><<%= at %>></></Italic>)  
        Next  
  
        Console.WriteLine("Before Transform")  
        Console.WriteLine("----------------")  
        Console.WriteLine(root)  
        Console.WriteLine(vbNewLine)  
        Dim newRoot As XElement = XForm(root)  
  
        Console.WriteLine("After Transform")  
        Console.WriteLine("----------------")  
        Console.WriteLine(newRoot)  
    End Sub  
End Module   
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```console
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
  
## <a name="see-also"></a>참조

- [Visual Basic (Advanced LINQ to XML 프로그래밍)](../../../../visual-basic/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)
