---
title: WordprocessingML 문서의 모양(C#)
ms.date: 07/20/2015
ms.assetid: 3791b5e0-c502-469b-bb75-a7bf6fdd0a94
ms.openlocfilehash: 84d893267c37ecf99a457ebb683d0451e2b4b68f
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69591051"
---
# <a name="shape-of-wordprocessingml-documents-c"></a>WordprocessingML 문서의 모양(C#)
이 항목에서는 WordprocessingML 문서의 XML 모양에 대해 소개합니다.  
  
## <a name="microsoft-office-formats"></a>Microsoft Office 형식  
 2007 Microsoft Office system의 기본 파일 형식은 Office Open XML(일반적으로 Open XML이라고 함)입니다. Open XML은 Ecma 표준이며 현재 ISO-IEC 표준 과정을 거치고 있는 XML 기반 형식입니다. Open XML에 있는 워드 프로세서 파일의 마크업 언어를 WordprocessingML이라고 합니다. 이 자습서에서는 WordprocessingML 소스 파일을 예제의 입력으로 사용합니다.  
  
 Microsoft Office 2003을 사용하는 경우 Word, Excel 및 PowerPoint 2007 파일 형식용 Microsoft Office 호환 기능 팩을 설치했으면 Office Open XML 형식으로 문서를 저장할 수 있습니다.  
  
## <a name="the-shape-of-wordprocessingml-documents"></a>WordprocessingML 문서의 모양  
 먼저 WordprocessingML 문서의 모양을 이해해야 합니다. WordprocessingML 문서에는 문서의 단락이 포함된 `w:body`라는 본문 요소가 들어 있습니다. 각 단락에는 `w:r`이라는 텍스트 실행이 하나 이상 포함되어 있습니다. 각 텍스트 실행에는 `w:t`라는 텍스트가 하나 이상 포함되어 있습니다.  
  
 다음은 매우 간단한 WordprocessingML 문서입니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<w:document  
xmlns:ve="http://schemas.openxmlformats.org/markup-compatibility/2006"  
xmlns:o="urn:schemas-microsoft-com:office:office"  
xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships"  
xmlns:m="http://schemas.openxmlformats.org/officeDocument/2006/math"  
xmlns:v="urn:schemas-microsoft-com:vml"  
xmlns:wp="http://schemas.openxmlformats.org/drawingml/2006/wordprocessingDrawing"  
xmlns:w10="urn:schemas-microsoft-com:office:word"  
xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main"  
xmlns:wne="http://schemas.microsoft.com/office/word/2006/wordml">  
  <w:body>  
    <w:p w:rsidR="00E22EB6"  
         w:rsidRDefault="00E22EB6">  
      <w:r>  
        <w:t>This is a paragraph.</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00E22EB6"  
         w:rsidRDefault="00E22EB6">  
      <w:r>  
        <w:t>This is another paragraph.</w:t>  
      </w:r>  
    </w:p>  
  </w:body>  
</w:document>  
```  
  
 이 문서에는 두 단락이 포함되어 있습니다. 두 단락에는 모두 단일 텍스트 실행이 포함되어 있고 각 텍스트 실행에는 단일 텍스트가 포함되어 있습니다.  
  
 XML 형식으로 WordprocessingML 문서의 내용을 보는 가장 쉬운 방법은 Microsoft Word를 사용하여 문서를 만들어 저장한 후 XML을 콘솔에 출력하는 다음 프로그램을 실행하는 것입니다.  
  
 이 예제에서는 WindowsBase 어셈블리의 클래스를 사용하고 <xref:System.IO.Packaging?displayProperty=nameWithType> 네임스페이스의 형식을 사용합니다.  
  
```csharp  
const string documentRelationshipType =  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument";  
const string wordmlNamespace =  
  "http://schemas.openxmlformats.org/wordprocessingml/2006/main";  
XNamespace w = wordmlNamespace;  
  
using (Package wdPackage = Package.Open("SampleDoc.docx", FileMode.Open, FileAccess.Read))  
{  
    PackageRelationship relationship =  
        wdPackage  
        .GetRelationshipsByType(documentRelationshipType)  
        .FirstOrDefault();  
    if (relationship != null)  
    {  
        Uri documentUri =  
            PackUriHelper.ResolvePartUri(  
                new Uri("/", UriKind.Relative),  
                relationship.TargetUri);  
        PackagePart documentPart = wdPackage.GetPart(documentUri);  
  
        //  Get the officeDocument part from the package.  
        //  Load the XML in the part into an XDocument instance.  
        XDocument xdoc =  
            XDocument.Load(XmlReader.Create(documentPart.GetStream()));  
        Console.WriteLine(xdoc.Root);  
    }  
}  
```  
  
## <a name="external-resources"></a>외부 리소스  
 [Office(2007) Open XML 파일 형식 소개](https://docs.microsoft.com/previous-versions/office/developer/office-2007/aa338205%28v=office.12%29)  
 [WordprocessingML의 개요](https://docs.microsoft.com/previous-versions/office/developer/office-2003/aa212812%28v=office.11%29)  
 [Anatomy of a WordProcessingML File](http://officeopenxml.com/anatomyofOOXML.php)(WordProcessingML 파일의 구조)  
 [WordprocessingML 소개](https://ericwhite.com/blog/introduction-to-wordprocessingml-series/)  
 [Office 2003: XML 참조 스키마 다운로드 페이지](https://www.microsoft.com/download/details.aspx?id=101)  
  
## <a name="see-also"></a>참고 항목

- [자습서: WordprocessingML 문서에서 내용 조작(C#)](./shape-of-wordprocessingml-documents.md)
