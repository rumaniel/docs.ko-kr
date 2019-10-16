---
title: 단락 및 해당 스타일 (Visual Basic) 검색
ms.date: 07/20/2015
ms.assetid: d9ed2238-d38e-4ad4-b88b-db7859df9bde
ms.openlocfilehash: 3c6554c44c95db13aada0d9edf96cc2df595c6d1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61787038"
---
# <a name="retrieving-the-paragraphs-and-their-styles-visual-basic"></a>단락 및 해당 스타일 (Visual Basic) 검색
이 예제에서는 WordprocessingML 문서에서 단락 노드를 검색하는 쿼리를 작성합니다. 또한 각 단락의 스타일도 식별합니다.  
  
 이 쿼리는 이전 예의 쿼리 기반 [(Visual Basic)의 기본 단락 스타일 찾기](../../../../visual-basic/programming-guide/concepts/linq/finding-the-default-paragraph-style.md), 스타일 목록에서 기본 스타일을 검색 하는 합니다. 이 정보는 쿼리에서 스타일이 명시적으로 설정되지 않은 단락의 스타일을 식별할 수 있도록 하는 데 필요합니다. 단락 스타일은 `w:pPr` 요소를 통해 설정되며 단락이 이 요소를 포함하지 않으면 기본 스타일로 서식이 지정됩니다.  
  
 이 항목에서는 몇 가지 쿼리 부분의 의미에 대해 설명한 다음 작동하는 전체 예제의 일부로 쿼리를 보여 줍니다.  
  
## <a name="example"></a>예제  
 문서의 모든 단락과 단락 스타일을 검색하는 쿼리의 소스는 다음과 같습니다.  
  
```vb  
xDoc.Root.<w:body>...<w:p>  
```  
  
 이 식은 이전 예제에서는 쿼리의 원본을 비슷합니다 [(Visual Basic)의 기본 단락 스타일 찾기](../../../../visual-basic/programming-guide/concepts/linq/finding-the-default-paragraph-style.md)합니다. 주요 차이점은 이 식에서는 <xref:System.Xml.Linq.XContainer.Descendants%2A> 축 대신 <xref:System.Xml.Linq.XContainer.Elements%2A> 축을 사용하는 것입니다. 섹션이 포함된 문서에서 단락은 본문 요소의 직접적 자식이 아니고 계층 구조에서 두 수준 아래에 있기 때문에 쿼리에서는 <xref:System.Xml.Linq.XContainer.Descendants%2A> 축을 사용합니다. 코드에서는 <xref:System.Xml.Linq.XContainer.Descendants%2A> 축을 사용하여 문서에서 섹션을 사용하는지 여부에 대한 작업을 합니다.  
  
## <a name="example"></a>예제  
 쿼리에서는 `Let` 절을 사용하여 스타일 노드가 포함된 요소를 확인합니다. 요소가 없으면 `styleNode`가 `Nothing`로 설정됩니다.  
  
```vb  
Let styleNode As XElement = para.<w:pPr>.<w:pStyle>.FirstOrDefault()  
```  
  
 `Let` 절에서는 먼저 <xref:System.Xml.Linq.XContainer.Elements%2A> 축을 사용하여 `pPr`이라는 모든 요소를 찾은 다음 <xref:System.Xml.Linq.Extensions.Elements%2A> 확장 메서드를 사용하여 `pStyle`이라는 모든 자식 요소를 찾고, 마지막으로 <xref:System.Linq.Enumerable.FirstOrDefault%2A> 표준 쿼리 연산자를 사용하여 컬렉션을 singleton으로 변환합니다. 컬렉션이 비어 있으면 `styleNode`가 `Nothing`로 설정됩니다. 이 방법은 `pStyle` 하위 노드를 찾을 때 유용합니다. `pPr` 자식 노드가 없으면 코드에서 예외를 throw하지 않고, 대신 `styleNode`가 `Nothing`로 설정됩니다. 이는 이 `Let` 절의 원하는 동작입니다.  
  
 쿼리에서는 두 멤버 `StyleName` 및 `ParagraphNode`가 있는 익명 형식의 컬렉션을 프로젝션합니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 WordprocessingML 문서를 처리하여 WordprocessingML 문서에서 단락 노드를 검색합니다. 또한 각 단락의 스타일도 식별합니다. 이 예제는 이 자습서의 이전 예제를 기반으로 합니다. 새 쿼리는 아래에 있는 코드의 주석에서 호출됩니다.  
  
 이 예제에서 원본 문서 만들기에 대 한 지침을 찾을 수 있습니다 [는 원본 Office Open XML 문서 만들기 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-the-source-office-open-xml-document.md)합니다.  
  
 이 예제에서는 WindowsBase 어셈블리의 클래스를 사용하고 <xref:System.IO.Packaging?displayProperty=nameWithType> 네임스페이스의 형식을 사용합니다.  
  
```vb  
Imports <xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">  
  
Module Module1  
    Private Function GetStyleOfParagraph(ByVal styleNode As XElement, ByVal defaultStyle As String) As String  
        If (styleNode Is Nothing) Then  
            Return defaultStyle  
        Else  
            Return styleNode.@w:val  
        End If  
    End Function  
  
    Sub Main()  
        Dim fileName = "SampleDoc.docx"  
  
        Dim documentRelationshipType = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument"  
        Dim stylesRelationshipType = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles"  
        Dim wordmlNamespace = "http://schemas.openxmlformats.org/wordprocessingml/2006/main"  
  
        Dim xDoc As XDocument = Nothing  
        Dim styleDoc As XDocument = Nothing  
        Using wdPackage As Package = Package.Open(fileName, FileMode.Open, FileAccess.Read)  
            Dim docPackageRelationship As PackageRelationship = wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault()  
            If (docPackageRelationship IsNot Nothing) Then  
                Dim documentUri As Uri = PackUriHelper.ResolvePartUri(New Uri("/", UriKind.Relative), docPackageRelationship.TargetUri)  
                Dim documentPart As PackagePart = wdPackage.GetPart(documentUri)  
  
                '  Load the document XML in the part into an XDocument instance.  
                xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()))  
  
                '  Find the styles part. There will only be one.  
                Dim styleRelation As PackageRelationship = documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault()  
                If (styleRelation IsNot Nothing) Then  
                    Dim styleUri As Uri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri)  
                    Dim stylePart As PackagePart = wdPackage.GetPart(styleUri)  
  
                    '  Load the style XML in the part into an XDocument instance.  
                    styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()))  
                End If  
            End If  
        End Using  
  
        Dim defaultStyle As String = _  
            ( _  
                From style In styleDoc.Root.<w:style> _  
                Where style.@w:type = "paragraph" And _  
                      style.@w:default = "1" _  
                Select style _  
            ).First().@w:styleId  
  
        ' Following is the new query that finds all paragraphs in the  
        ' document and their styles.  
        Dim paragraphs = _  
            From para In xDoc.Root.<w:body>...<w:p> _  
        Let styleNode As XElement = para.<w:pPr>.<w:pStyle>.FirstOrDefault() _  
        Select New With { _  
            .ParagraphNode = para, _  
            .StyleName = GetStyleOfParagraph(styleNode, defaultStyle) _  
        }  
  
        For Each p In paragraphs  
            Console.WriteLine("StyleName:{0}", p.StyleName)  
        Next  
  
    End Sub  
End Module  
```  
  
 이 예제에서 설명 하는 문서에 적용 하면 다음 출력이 생성 [는 원본 Office Open XML 문서 만들기 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/creating-the-source-office-open-xml-document.md)합니다.  
  
```  
StyleName:Heading1  
StyleName:Normal  
StyleName:Normal  
StyleName:Normal  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Normal  
StyleName:Normal  
StyleName:Normal  
StyleName:Code  
```  
  
## <a name="next-steps"></a>다음 단계  
 다음 항목인 [(Visual Basic) 단락의 텍스트 검색](../../../../visual-basic/programming-guide/concepts/linq/retrieving-the-text-of-the-paragraphs.md), 단락의 텍스트를 검색 하는 쿼리를 만들어야 합니다.  
  
## <a name="see-also"></a>참고자료

- [자습서: (Visual Basic) WordprocessingML 문서에서 내용 조작](../../../../visual-basic/programming-guide/concepts/linq/tutorial-manipulating-content-in-a-wordprocessingml-document.md)
