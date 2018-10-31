---
title: XslTransform에 대한 XmlDocument 입력
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 97115892-410a-4657-ab47-1e14dfba73f8
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e83cf82aee57b1f40f695700d8d0b38c12e0ac39
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48836683"
---
# <a name="xmldocument-input-to-xsltransform"></a>XslTransform에 대한 XmlDocument 입력
<xref:System.Xml.XmlDocument> 클래스는 XML 문서에 편집 기능을 제공합니다. <xref:System.Xml.Xsl.XslTransform.Transform%2A> 메서드로 보내기 전에 XML을 편집 또는 수정해야 하는 경우 XML을 <xref:System.Xml.XmlDocument>에 로드하고 편집한 다음 <xref:System.Xml.Xsl.XslTransform>으로 보냅니다.  
  
> [!NOTE]
>  <xref:System.Xml.Xsl.XslTransform> 클래스는 [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)]에서 사용되지 않습니다. <xref:System.Xml.Xsl.XslCompiledTransform> 클래스를 사용하여 XSLT(Extensible Stylesheet Language for Transformations) 변환을 수행할 수 있습니다. 자세한 내용은 [XslCompiledTransform 클래스 사용](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md) 및 [XslTransform 클래스에서 마이그레이션](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)을 참조하세요.  
  
 <xref:System.Xml.XmlDocument>는 <xref:System.Xml.XPath.IXPathNavigable> 인터페이스를 구현하므로 편집한 후 문서를 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 메서드로 보낼 수 있습니다.  
  
 <xref:System.Xml.XmlDocument>의 편집 기능 때문에 <xref:System.Xml.XmlDocument> 클래스를 변환의 입력으로 사용하면 XSLT(Extensible Stylesheet Language for Transformations) 변환에 <xref:System.Xml.XPath.XPathDocument>를 사용하는 것보다 성능이 떨어집니다. 이것은 <xref:System.Xml.XPath.XPathDocument>가 내부 저장소로 인해 XPath(XML Path Language) 쿼리에 최적화되었기 때문입니다.  
  
## <a name="example"></a>예  
 다음 코드 예제에서는 <xref:System.Xml.XmlDocument>를 <xref:System.Xml.Xsl.XslTransform>에 보내고 출력을 <xref:System.Xml.XmlReader>로 보내는 방법을 보여 줍니다.  
  
```vb  
Dim doc as XmlDocument = new XmlDocument()  
doc.Load("books.xml")  
Dim trans As XslTransform = new XslTransform()  
trans.Load("book.xsl")  
Dim rdr As XmlReader = trans.Transform(doc, Nothing, Nothing)  
while (rdr.Read())  
end while  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
doc.Load("books.xml");  
XslTransform trans = new XslTransform();  
trans.Load("book.xsl");  
XmlReader rdr = trans.Transform(doc, null, null);  
while (rdr.Read()) {}  
```  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlDocument>  
- [XslTransform 클래스를 사용하여 XSLT 변형](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)  
- [XslTransform 클래스의 XSLT 프로세서 구현](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)  
- [변형 과정에서 XPathNavigator의 역할](../../../../docs/standard/data/xml/xpathnavigator-in-transformations.md)  
- [변형 과정에서 XPathNodeIterator의 역할](../../../../docs/standard/data/xml/xpathnodeiterator-in-transformations.md)  
- [XslTransform에 대한 XPathDocument 입력](../../../../docs/standard/data/xml/xpathdocument-input-to-xsltransform.md)  
- [XslTransform에 대한 XmlDataDocument 입력](../../../../docs/standard/data/xml/xmldatadocument-input-to-xsltransform.md)
