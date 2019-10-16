---
title: XslCompiledTransform 클래스에 대한 입력
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 834049f1-ab41-449e-9f10-4a1d0701bc48
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 043c37a17375bf2dcdad9e4b429cfca7b96ef7cb
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966965"
---
# <a name="inputs-to-the-xslcompiledtransform-class"></a>XslCompiledTransform 클래스에 대한 입력
<xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 메서드는 소스 문서에 대한 세 가지 입력 형식을 허용합니다. 즉, <xref:System.Xml.XPath.IXPathNavigable> 인터페이스를 구현하는 개체, 소스 문서를 읽는 <xref:System.Xml.XmlReader> 개체 또는 문자열 URI를 허용합니다.  
  
> [!NOTE]
> 기본적으로 <xref:System.Xml.Xsl.XslCompiledTransform> 클래스는 공백을 유지합니다. 이러한 점은 [W3C XSLT 1.0 권장 사항의 섹션 3.4](https://www.w3.org/TR/xslt.html#strip)과 일치합니다.  
  
## <a name="ixpathnavigable-interface"></a>IXPathNavigable 인터페이스  
 <xref:System.Xml.XPath.IXPathNavigable> 인터페이스는 <xref:System.Xml.XmlNode> 및 <xref:System.Xml.XPath.XPathDocument> 클래스에서 구현됩니다. 이 클래스는 XML 데이터의 메모리 내 캐시를 나타냅니다.  
  
- <xref:System.Xml.XmlNode> 클래스는 W3C DOM(문서 개체 모델)을 기반으로 하며 편집 기능이 있습니다.  
  
- <xref:System.Xml.XPath.XPathDocument> 클래스는 XPath 데이터 모델을 기반으로 하는 읽기 전용 데이터 저장소입니다. <xref:System.Xml.XPath.XPathDocument>는 XSLT 처리에 권장되는 클래스입니다. 이 클래스는 <xref:System.Xml.XmlNode> 클래스와 비교하여 속도가 더 빠릅니다.  
  
> [!NOTE]
> 변형은 문서 전체에 적용됩니다. 즉, 문서 루트 노드 이외의 노드에 전달해도 변환 프로세스에서 로드된 문서의 모든 노드에 액세스할 수 있습니다. 노드 조각을 변형하려면 노드 조각만 포함하는 개체를 만들고 이 개체를 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 메서드에 전달해야 합니다. 자세한 내용은 [방법: 노드 조각 변환](../../../../docs/standard/data/xml/how-to-transform-a-node-fragment.md)을 참조하세요.  
  
 다음 예제에서는 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A?displayProperty=nameWithType> 메서드를 통해 transform.xsl 스타일시트를 사용하여 books.xml 파일을 books.html 파일로 변형합니다. books.xml 및 transform.xsl 파일은 [방법: 어셈블리를 사용하여 XSLT 변형 수행](../../../../docs/standard/data/xml/how-to-perform-an-xslt-transformation-by-using-an-assembly.md) 항목에 있습니다.  
  
 [!code-csharp[XslCompiledTransform.Transform2#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XslCompiledTransform.Transform2/CS/Program.cs#1)]
 [!code-vb[XslCompiledTransform.Transform2#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XslCompiledTransform.Transform2/VB/Module1.vb#1)]  
  
## <a name="xmlreader-object"></a>XmlReader 개체  
 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 메서드는 모든 자식을 통해 <xref:System.Xml.XmlReader>의 현재 노드로부터 로드합니다. 그러면 문서의 일부를 컨텍스트 문서로 사용할 수 있습니다. <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 메서드가 반환된 후 <xref:System.Xml.XmlReader>가 컨텍스트 문서 끝 뒤의 다음 노드에 배치됩니다. 문서 끝에 도달하면 <xref:System.Xml.XmlReader>가 EOF(파일 끝)에 배치됩니다.  
  
 다음 예제에서는 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A?displayProperty=nameWithType> 메서드를 통해 transform.xsl 스타일시트를 사용하여 books.xml 파일을 books.html 파일로 변형합니다. books.xml 및 transform.xsl 파일은 [방법: 어셈블리를 사용하여 XSLT 변형 수행](../../../../docs/standard/data/xml/how-to-perform-an-xslt-transformation-by-using-an-assembly.md) 항목에 있습니다.  
  
 [!code-csharp[XslCompiledTransform.Transform2#2](../../../../samples/snippets/csharp/VS_Snippets_Data/XslCompiledTransform.Transform2/CS/Program.cs#2)]
 [!code-vb[XslCompiledTransform.Transform2#2](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XslCompiledTransform.Transform2/VB/Module1.vb#2)]  
  
## <a name="string-uri"></a>문자열 URI  
 소스 문서 URI를 XSLT 입력으로 지정할 수도 있습니다. <xref:System.Xml.XmlResolver>를 사용하여 URI를 확인할 수 있습니다. 사용할 <xref:System.Xml.XmlResolver>를 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 메서드에 전달하여 지정할 수 있습니다. <xref:System.Xml.XmlResolver>를 지정하지 않으면 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 메서드는 자격 증명 없이 기본 <xref:System.Xml.XmlUrlResolver>를 사용합니다.  
  
 다음 예제에서는 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A?displayProperty=nameWithType> 메서드를 통해 transform.xsl 스타일시트를 사용하여 books.xml 파일을 books.html 파일로 변형합니다. books.xml 및 transform.xsl 파일은 [방법: 어셈블리를 사용하여 XSLT 변형 수행](../../../../docs/standard/data/xml/how-to-perform-an-xslt-transformation-by-using-an-assembly.md) 항목에 있습니다.  
  
 [!code-csharp[XslCompiledTransform.Transform2#3](../../../../samples/snippets/csharp/VS_Snippets_Data/XslCompiledTransform.Transform2/CS/Program.cs#3)]
 [!code-vb[XslCompiledTransform.Transform2#3](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XslCompiledTransform.Transform2/VB/Module1.vb#3)]  
  
 자세한 내용은 [XSLT 처리 중 외부 리소스 확인](../../../../docs/standard/data/xml/resolving-external-resources-during-xslt-processing.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [XSLT 변환](../../../../docs/standard/data/xml/xslt-transformations.md)
