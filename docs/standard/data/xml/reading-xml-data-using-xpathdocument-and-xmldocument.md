---
title: XPathDocument 및 XmlDocument를 사용하여 XML 데이터 읽기
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 5711b225-6aa2-4e4f-9898-19f2d518ad1a
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 68d19784bab8a5d5a1994ea139b5631f56c7c680
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54580423"
---
# <a name="reading-xml-data-using-xpathdocument-and-xmldocument"></a>XPathDocument 및 XmlDocument를 사용하여 XML 데이터 읽기
두 가지 방법으로 <xref:System.Xml.XPath?displayProperty=nameWithType> 네임스페이스에서 XML 문서를 읽을 수 있습니다. 하나는 읽기 전용 <xref:System.Xml.XPath.XPathDocument> 클래스를 사용하여 XML 문서를 읽는 것이고 다른 하나는 <xref:System.Xml.XmlDocument> 네임스페이스에서 편집 가능한 <xref:System.Xml?displayProperty=nameWithType> 클래스를 사용하여 XML 문서를 읽는 것입니다.  
  
## <a name="reading-xml-documents-using-the-xpathdocument-class"></a>XPathDocument 클래스를 사용하여 XML 문서 읽기  
 <xref:System.Xml.XPath.XPathDocument> 클래스는 XPath 데이터 모델을 사용하여 빠른 속도의 읽기 전용 메모리 내 XML 문서 표현을 제공합니다. 6개 생성자 중 하나를 사용하여 <xref:System.Xml.XPath.XPathDocument> 클래스의 인스턴스가 생성됩니다. 이러한 생성자를 사용하면 XML 파일에 대한 <xref:System.IO.Stream> 경로뿐 아니라 <xref:System.IO.TextReader>, <xref:System.Xml.XmlReader> 또는 `string` 개체를 사용하여 XML 문서를 읽을 수 있습니다.  
  
 다음 예제에서는 <xref:System.Xml.XPath.XPathDocument> 클래스의 `string` 생성자를 사용하여 XML 문서를 읽는 방법을 보여 줍니다.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
```  
  
## <a name="reading-xml-documents-using-the-xmldocument-class"></a>XmlDocument 클래스를 사용하여 XML 문서 읽기  
 <xref:System.Xml.XmlDocument> 클래스는 W3C DOM(문서 개체 모델) Level 1 Core 및 DOM Level 2 Core를 구현하는 XML 문서의 편집 가능한 메모리 내 표현입니다. 세 가지 생성자 중 하나를 사용하여 <xref:System.Xml.XmlDocument> 클래스의 인스턴스가 생성됩니다. 매개 변수 없이 <xref:System.Xml.XmlDocument> 클래스 생성자를 호출하여 비어 있는 새 <xref:System.Xml.XmlDocument> 개체를 만들 수 있습니다. 생성자를 호출한 후 <xref:System.Xml.XmlDocument.Load%2A> 메서드를 사용하여 XML 파일의 <xref:System.Xml.XmlDocument> 경로뿐 아니라 <xref:System.IO.Stream>, <xref:System.IO.TextReader> 또는 <xref:System.Xml.XmlReader> 개체에서 새 `string` 개체로 XML 데이터를 로드합니다.  
  
 다음 예제에서는 매개 변수 없이 <xref:System.Xml.XmlDocument> 클래스 생성자 및 <xref:System.Xml.XmlDocument.Load%2A> 메서드를 사용하여 XML 문서를 읽는 방법을 보여 줍니다.  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("books.xml")  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("books.xml");  
```  
  
## <a name="determining-the-encoding-of-an-xml-document"></a>XML 문서의 인코딩 결정  
 이전 단원에 표시된 것과 같이 <xref:System.Xml.XmlReader> 개체를 사용하여 XML 문서를 읽고 <xref:System.Xml.XPath.XPathDocument> 및 <xref:System.Xml.XmlDocument> 개체를 만들 수 있습니다. 그러나 <xref:System.Xml.XmlReader> 개체는 인코딩되지 않은 데이터를 읽을 수 있으며 이러한 경우 인코딩 정보를 제공하지 않습니다.  
  
 <xref:System.Xml.XmlTextReader> 클래스는 <xref:System.Xml.XmlReader> 클래스에서 상속되며 <xref:System.Xml.XmlTextReader.Encoding%2A> 속성을 사용하여 인코딩 정보를 제공합니다. 또한 <xref:System.Xml.XPath.XPathDocument> 개체 또는 <xref:System.Xml.XmlDocument> 개체를 만드는 데 사용할 수도 있습니다.  
  
 <xref:System.Xml.XmlTextReader> 클래스에서 제공하는 인코딩 정보에 대한 자세한 내용은 <xref:System.Xml.XmlTextReader.Encoding%2A> 클래스 참조 문서의 <xref:System.Xml.XmlTextReader> 속성을 참조하세요.  
  
## <a name="creating-xpathnavigator-objects"></a>XPathNavigator 개체 만들기  
 <xref:System.Xml.XPath.XPathDocument> 또는 <xref:System.Xml.XmlDocument> 개체로 XML 문서를 읽어온 후 <xref:System.Xml.XPath.XPathNavigator> 개체를 만들어 기본 XML 데이터를 선택, 평가 및 탐색할 수 있으며 일부 경우에 편집할 수도 있습니다.  
  
 <xref:System.Xml.XPath.XPathDocument> 클래스와 더불어 <xref:System.Xml.XmlDocument> 및 <xref:System.Xml.XmlNode> 클래스는 <xref:System.Xml.XPath.IXPathNavigable> 네임스페이스의 <xref:System.Xml.XPath?displayProperty=nameWithType> 인터페이스를 구현합니다. 결과적으로 세 클래스는 모두 <xref:System.Xml.XPath.IXPathNavigable.CreateNavigator%2A> 개체를 반환하는 <xref:System.Xml.XPath.XPathNavigator> 메서드를 제공합니다.  
  
### <a name="editing-xml-documents-using-the-xpathnavigator-class"></a>XPathNavigator 클래스를 사용하여 XML 문서 편집  
 <xref:System.Xml.XPath.XPathNavigator> 클래스를 사용하여 XML 데이터를 선택, 평가 및 탐색할 수 있을 뿐 아니라 XML 문서가 생성된 개체를 기반으로 XML 문서를 편집할 수도 있습니다.  
  
 <xref:System.Xml.XPath.XPathDocument> 클래스는 읽기 전용인 반면, <xref:System.Xml.XmlDocument> 클래스는 편집 가능하므로 <xref:System.Xml.XPath.XPathNavigator> 개체에서 만든 <xref:System.Xml.XPath.XPathDocument> 개체는 XML 문서를 편집하는 데 사용할 수 없는 반면, <xref:System.Xml.XmlDocument> 개체에서 만든 개체는 사용할 수 있습니다. XML 문서를 읽기만 하려면 <xref:System.Xml.XPath.XPathDocument> 클래스를 사용해야 합니다. XML 문서를 편집해야 하거나 <xref:System.Xml.XmlDocument> 클래스에서 제공하는 이벤트 처리 등의 추가 기능에 액세스해야 할 경우 <xref:System.Xml.XmlDocument> 클래스를 사용해야 합니다.  
  
 <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> 클래스의 <xref:System.Xml.XPath.XPathNavigator> 속성은 <xref:System.Xml.XPath.XPathNavigator> 개체가 XML 데이터를 편집할 수 있는지 여부를 지정합니다.  
  
 다음 표에서는 각 클래스에 대한 <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> 속성 값에 대해 설명합니다.  
  
|<xref:System.Xml.XPath.IXPathNavigable> 구현|<xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> 값|  
|--------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Xml.XPath.XPathDocument>|`false`|  
|<xref:System.Xml.XmlDocument>|`true`|  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [XPath 데이터 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [XPathNavigator를 사용하여 XML 데이터 액세스](../../../../docs/standard/data/xml/accessing-xml-data-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 XML 데이터 편집](../../../../docs/standard/data/xml/editing-xml-data-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 스키마 유효성 검사](../../../../docs/standard/data/xml/schema-validation-using-xpathnavigator.md)
