---
title: 단락 및 해당 스타일 검색(C#)
ms.date: 07/20/2015
ms.assetid: c2f767f8-57b1-4b4b-af04-89ffb1f7067d
ms.openlocfilehash: ec59ef0ac36f8691ca93a4c21c5379118ee0491f
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253069"
---
# <a name="retrieving-the-paragraphs-and-their-styles-c"></a>단락 및 해당 스타일 검색(C#)
이 예제에서는 WordprocessingML 문서에서 단락 노드를 검색하는 쿼리를 작성합니다. 또한 각 단락의 스타일도 식별합니다.  
  
 이 쿼리는 스타일 목록에서 기본 스타일을 검색하는 이전 예제 [기본 단락 스타일 찾기(C#)](./finding-the-default-paragraph-style.md)의 쿼리를 기반으로 합니다. 이 정보는 쿼리에서 스타일이 명시적으로 설정되지 않은 단락의 스타일을 식별할 수 있도록 하는 데 필요합니다. 단락 스타일은 `w:pPr` 요소를 통해 설정되며 단락이 이 요소를 포함하지 않으면 기본 스타일로 서식이 지정됩니다.  
  
 이 항목에서는 몇 가지 쿼리 부분의 의미에 대해 설명한 다음 작동하는 전체 예제의 일부로 쿼리를 보여 줍니다.  
  
## <a name="example"></a>예  
 문서의 모든 단락과 단락 스타일을 검색하는 쿼리의 소스는 다음과 같습니다.  
  
```csharp  
xDoc.Root.Element(w + "body").Descendants(w + "p")  
```  
  
 이 식은 이전 예제 [기본 단락 스타일 찾기(C#)](./finding-the-default-paragraph-style.md)의 쿼리 소스와 유사합니다. 주요 차이점은 이 식에서는 <xref:System.Xml.Linq.XContainer.Descendants%2A> 축 대신 <xref:System.Xml.Linq.XContainer.Elements%2A> 축을 사용하는 것입니다. 섹션이 포함된 문서에서 단락은 본문 요소의 직접적 자식이 아니고 계층 구조에서 두 수준 아래에 있기 때문에 쿼리에서는 <xref:System.Xml.Linq.XContainer.Descendants%2A> 축을 사용합니다. 코드에서는 <xref:System.Xml.Linq.XContainer.Descendants%2A> 축을 사용하여 문서에서 섹션을 사용하는지 여부에 대한 작업을 합니다.  
  
## <a name="example"></a>예  
 쿼리에서는 `let` 절을 사용하여 스타일 노드가 포함된 요소를 확인합니다. 요소가 없으면 `styleNode`가 `null`로 설정됩니다.  
  
```csharp  
let styleNode = para.Elements(w + "pPr").Elements(w + "pStyle").FirstOrDefault()  
```  
  
 `let` 절에서는 먼저 <xref:System.Xml.Linq.XContainer.Elements%2A> 축을 사용하여 `pPr`이라는 모든 요소를 찾은 다음 <xref:System.Xml.Linq.Extensions.Elements%2A> 확장 메서드를 사용하여 `pStyle`이라는 모든 자식 요소를 찾고, 마지막으로 <xref:System.Linq.Enumerable.FirstOrDefault%2A> 표준 쿼리 연산자를 사용하여 컬렉션을 singleton으로 변환합니다. 컬렉션이 비어 있으면 `styleNode`가 `null`로 설정됩니다. 이 방법은 `pStyle` 하위 노드를 찾을 때 유용합니다. `pPr` 자식 노드가 없으면 코드에서 예외를 throw하지 않고, 대신 `styleNode`가 `null`로 설정됩니다. 이는 이 `let` 절의 원하는 동작입니다.  
  
 쿼리에서는 두 멤버 `StyleName` 및 `ParagraphNode`가 있는 익명 형식의 컬렉션을 프로젝션합니다.  
  
## <a name="example"></a>예  
 이 예제에서는 WordprocessingML 문서를 처리하여 WordprocessingML 문서에서 단락 노드를 검색합니다. 또한 각 단락의 스타일도 식별합니다. 이 예제는 이 자습서의 이전 예제를 기반으로 합니다. 새 쿼리는 아래에 있는 코드의 주석에서 호출됩니다.  
  
 이 예제의 소스 문서 만들기에 대한 지침은 [원본 Office Open XML 문서 만들기(C#)](./creating-the-source-office-open-xml-document.md)에서 찾을 수 있습니다.  
  
 이 예제에서는 WindowsBase 어셈블리의 클래스를 사용하고 <xref:System.IO.Packaging?displayProperty=nameWithType> 네임스페이스의 형식을 사용합니다.  
  
```csharp  
const string fileName = "SampleDoc.docx";  
  
const string documentRelationshipType = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument";  
const string stylesRelationshipType = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles";  
const string wordmlNamespace = "http://schemas.openxmlformats.org/wordprocessingml/2006/main";  
XNamespace w = wordmlNamespace;  
  
XDocument xDoc = null;  
XDocument styleDoc = null;  
  
using (Package wdPackage = Package.Open(fileName, FileMode.Open, FileAccess.Read))  
{  
    PackageRelationship docPackageRelationship = wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault();  
    if (docPackageRelationship != null)  
    {  
        Uri documentUri = PackUriHelper.ResolvePartUri(new Uri("/", UriKind.Relative), docPackageRelationship.TargetUri);  
        PackagePart documentPart = wdPackage.GetPart(documentUri);  
  
        //  Load the document XML in the part into an XDocument instance.  
        xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()));  
  
        //  Find the styles part. There will only be one.  
        PackageRelationship styleRelation = documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault();  
        if (styleRelation != null)  
        {  
            Uri styleUri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri);  
            PackagePart stylePart = wdPackage.GetPart(styleUri);  
  
            //  Load the style XML in the part into an XDocument instance.  
            styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()));  
        }  
    }  
}  
  
string defaultStyle =   
    (string)(  
        from style in styleDoc.Root.Elements(w + "style")  
        where (string)style.Attribute(w + "type") == "paragraph"&&  
              (string)style.Attribute(w + "default") == "1"  
              select style  
    ).First().Attribute(w + "styleId");  
  
// Following is the new query that finds all paragraphs in the  
// document and their styles.  
var paragraphs =  
    from para in xDoc  
                 .Root  
                 .Element(w + "body")  
                 .Descendants(w + "p")  
    let styleNode = para  
                    .Elements(w + "pPr")  
                    .Elements(w + "pStyle")  
                    .FirstOrDefault()  
    select new  
    {  
        ParagraphNode = para,  
        StyleName = styleNode != null ?  
            (string)styleNode.Attribute(w + "val") :  
            defaultStyle  
    };  
  
foreach (var p in paragraphs)  
    Console.WriteLine("StyleName:{0}", p.StyleName);  
```  
  
 [원본 Office Open XML 문서 만들기(C#)](./creating-the-source-office-open-xml-document.md)에서 설명하는 문서에 적용할 경우 이 예제의 결과는 다음과 같습니다.  
  
```output  
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
 다음 항목 [단락의 텍스트 검색(C#)](./retrieving-the-text-of-the-paragraphs.md)에서는 단락의 텍스트를 검색하기 위한 쿼리를 만듭니다.  
  
## <a name="see-also"></a>참고 항목

- [자습서: WordprocessingML 문서에서 내용 조작(C#)](./shape-of-wordprocessingml-documents.md)
