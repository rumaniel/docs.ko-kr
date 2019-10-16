---
title: 문서 작성 및 저장
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 097b0cb1-5743-4c3a-86ef-caf5cbe6750d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a35e06837ac35a743a3f0424cb2a7ad5bbeb5400
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64589957"
---
# <a name="saving-and-writing-a-document"></a>문서 작성 및 저장
<xref:System.Xml.XmlDocument>를 로드하고 저장할 경우 저장된 문서는 다음과 같이 원래 문서와 다를 수 있습니다.  
  
- <xref:System.Xml.XmlDocument.PreserveWhitespace%2A> 메서드를 호출하기 전에 `true` 속성을 <xref:System.Xml.XmlDocument.Save%2A>로 설정한 경우 문서 내의 공백이 출력에서 유지되며 `false`로 설정한 경우 <xref:System.Xml.XmlDocument>는 출력을 자동으로 들여씁니다.  
  
- 특성 사이에 있는 모든 공백은 단일 공백 문자로 줄어듭니다.  
  
- 요소 사이에 있는 공백이 변경됩니다. 유효 공백은 유지되고 무효 공백은 유지되지 않습니다. 그러나 문서를 저장할 때 기본적으로 <xref:System.Xml.XmlTextWriter> **Indenting** 모드를 사용하여 출력이 읽기 쉽도록 정리됩니다.  
  
- 특성 값 주위에 사용된 작은따옴표는 기본적으로 큰따옴표로 변경됩니다. <xref:System.Xml.XmlTextReader.QuoteChar%2A>의 <xref:System.Xml.XmlTextWriter> 속성을 사용하여 인용 문자를 작은따옴표나 큰따옴표로 설정할 수 있습니다.  
  
- 기본적으로 `{`과 같은 숫자 엔터티는 확장됩니다.  
  
- 입력 문서에 있는 바이트 순서 표시는 유지되지 않습니다. 명시적으로 다른 인코딩을 지정하는 XML 선언을 하지 않으면 UCS-2는 UTF-8로 저장됩니다.  
  
- 파일이나 스트림에 <xref:System.Xml.XmlDocument>를 쓸 경우 출력된 내용은 문서의 내용과 같습니다. 즉, <xref:System.Xml.XmlDeclaration>은 문서에 포함되어 있고 문서를 쓸 때 사용되는 인코딩이 선언 노드에 지정된 인코딩과 같은 경우에만 쓰여집니다.  
  
## <a name="writing-an-xmldeclaration"></a>XmlDeclaration 쓰기  
 <xref:System.Xml.XmlDocument> 및 <xref:System.Xml.XmlDeclaration>의 <xref:System.Xml.XmlNode.OuterXml%2A> 메서드 외에도 <xref:System.Xml.XmlNode.InnerXml%2A>, <xref:System.Xml.XmlNode.WriteTo%2A> 및 <xref:System.Xml.XmlDocument>의 <xref:System.Xml.XmlDocument.Save%2A> 및 <xref:System.Xml.XmlDocument.WriteContentTo%2A> 멤버는 XML 선언을 만듭니다.  
  
 <xref:System.Xml.XmlDocument>, <xref:System.Xml.XmlNode.OuterXml%2A>, <xref:System.Xml.XmlDocument.InnerXml%2A>, <xref:System.Xml.XmlDocument.Save%2A> 및 <xref:System.Xml.XmlDocument.WriteTo%2A> 메서드의 <xref:System.Xml.XmlDocument.WriteContentTo%2A> 속성의 경우 XML 선언에 쓰여질 인코딩을 <xref:System.Xml.XmlDeclaration> 노드에서 가져옵니다. <xref:System.Xml.XmlDeclaration> 노드가 없으면 <xref:System.Xml.XmlDeclaration>이 쓰여지지 않습니다. <xref:System.Xml.XmlDeclaration> 노드에 인코딩이 없으면 XML 선언에 인코딩이 쓰여지지 않습니다.  
  
 <xref:System.Xml.XmlDocument.Save%2A?displayProperty=nameWithType> 및 <xref:System.Xml.XmlDocument.Save%2A?displayProperty=nameWithType> 메서드는 항상 <xref:System.Xml.XmlDeclaration>을 씁니다. 이러한 메서드는 쓰려는 작성기에서 인코딩을 가져옵니다. 즉, 작성기의 인코딩 값이 문서와 <xref:System.Xml.XmlDeclaration> 개체의 인코딩을 재정의합니다. 예를 들어, 다음 코드에서는 `out.xml` 출력 파일에서 찾은 XML 선언에 인코딩을 쓰지 않습니다.  
  
```vb  
Dim doc As New XmlDocument()  
Dim tw As XmlTextWriter = New XmlTextWriter("out.xml", Nothing)  
doc.Load("text.xml")  
doc.Save(tw)  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
XmlTextWriter tw = new XmlTextWriter("out.xml", null);  
doc.Load("text.xml");  
doc.Save(tw);  
```  
  
 <xref:System.Xml.XmlDocument.Save%2A> 메서드의 경우 <xref:System.Xml.XmlWriter.WriteStartDocument%2A> 클래스의 <xref:System.Xml.XmlWriter> 메서드를 사용하여 XML 선언을 씁니다. 따라서 <xref:System.Xml.XmlWriter.WriteStartDocument%2A> 메서드를 덮어쓰면 문서의 시작 부분을 쓰는 방법이 변경됩니다.  
  
 <xref:System.Xml.XmlNode.OuterXml%2A>, <xref:System.Xml.XmlDeclaration.WriteTo%2A> 및 <xref:System.Xml.XmlNode.InnerXml%2A>의 <xref:System.Xml.XmlDeclaration> 멤버의 경우 <xref:System.Xml.XmlDeclaration.Encoding%2A> 속성을 설정하지 않으면 인코딩이 쓰여지지 않습니다. 그렇지 않은 경우 XML 선언에 쓰여지는 인코딩은 <xref:System.Xml.XmlDeclaration.Encoding%2A> 속성에서 찾은 인코딩과 같습니다.  
  
## <a name="writing-document-content-using-the-outerxml-property"></a>OuterXml 속성을 사용하여 문서 내용 작성  
 <xref:System.Xml.XmlNode.OuterXml%2A> 속성은 Microsoft에서 W3C(World Wide Web 컨소시엄) XML DOM(문서 개체 모델) 표준을 확장한 결과입니다. <xref:System.Xml.XmlNode.OuterXml%2A> 속성을 사용하여 전체 XML 문서의 태그를 가져오거나 단일 노드 및 해당 자식 노드의 태그만 가져올 수 있습니다. <xref:System.Xml.XmlNode.OuterXml%2A>은 지정된 노드 및 모든 자식 노드를 나타내는 태그를 반환합니다.  
  
 다음 코드 예제에서는 문서 전체를 문자열로 저장하는 방법을 보여 줍니다.  
  
```vb  
Dim mydoc As New XmlDocument()  
' Perform application needs here, like mydoc.Load("myfile");  
' Now save the entire document to a string variable called "xml".  
Dim xml As String = mydoc.OuterXml  
```  
  
```csharp  
XmlDocument mydoc = new XmlDocument();  
// Perform application needs here, like mydoc.Load("myfile");  
// Now save the entire document to a string variable called "xml".  
string xml = mydoc.OuterXml;  
```  
  
 다음 코드 예제에서는 문서 요소만 저장하는 방법을 보여 줍니다.  
  
```vb  
' For the content of the Document Element only.  
Dim xml As String = mydoc.DocumentElement.OuterXml  
```  
  
```csharp  
// For the content of the Document Element only.  
string xml = mydoc.DocumentElement.OuterXml;  
```  
  
 이와는 반대로 자식 노드의 내용이 필요한 경우 <xref:System.Xml.XmlNode.InnerText%2A> 속성을 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [XML DOM(문서 개체 모델)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
