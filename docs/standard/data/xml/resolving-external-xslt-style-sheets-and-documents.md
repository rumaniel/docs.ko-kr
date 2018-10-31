---
title: 외부 XSLT 스타일시트 및 문서 확인
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 920cfe3b-d525-4bb2-abf6-9431651f9cf9
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 39e8afd8c22ca757141d2a7b556b115f8380e731
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48847492"
---
# <a name="resolving-external-xslt-style-sheets-and-documents"></a>외부 XSLT 스타일시트 및 문서 확인
다음과 같이 변환 중에 외부 리소스를 확인해야 하는 몇 가지 경우가 있습니다.  
  
> [!NOTE]
>  <xref:System.Xml.Xsl.XslTransform> 클래스는 [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)]에서 사용되지 않습니다. <xref:System.Xml.Xsl.XslCompiledTransform> 클래스를 사용하여 XSLT(Extensible Stylesheet Language for Transformations) 변환을 수행할 수 있습니다.  
  
 다음과 같이 변환 중에 외부 리소스를 확인해야 하는 몇 가지 경우가 있습니다.  
  
-   <xref:System.Xml.Xsl.XslTransform.Load%2A> 중에 외부 스타일시트를 찾는 경우  
  
-   <xref:System.Xml.Xsl.XslTransform.Load%2A> 중에 스타일시트에 있는 모든 `<xsl:include>` 또는 `<xsl:import>` 요소를 확인하는 경우  
  
-   <xref:System.Xml.Xsl.XslTransform.Transform%2A> 중에 `document()` 함수를 확인하는 경우  
  
## <a name="using-the-xmlresolver-class"></a>XmlResolver 클래스 사용  
 네트워크 리소스에 액세스하기 위해 인증이 필요한 경우 <xref:System.Xml.Xsl.XslTransform.Load%2A> 매개 변수를 사용하여 필요한 자격 증명 속성 집합을 갖는 <xref:System.Xml.XmlResolver> 개체를 전달할 수 있는 <xref:System.Xml.XmlResolver> 메서드를 사용합니다.  
  
 다음 표에서는 사용하려는 사용자 지정 <xref:System.Xml.XmlResolver>가 있거나 다른 자격 증명을 지정해야 하는 경우 외부 리소스 확인이 필요한 시기에 따라 필요한 작업의 목록을 보여 줍니다.  
  
|확인이 필요한 프로세스|필요한 작업|  
|--------------------------------------|-------------------|  
|<xref:System.Xml.Xsl.XslTransform.Load%2A> 중에 스타일시트 찾기|스타일시트가 자격 증명을 요구하는 리소스에 있는 경우 <xref:System.Xml.Xsl.XslTransform.Load%2A>를 매개 변수로 사용하는 오버로드된 <xref:System.Xml.XmlResolver> 메서드를 지정합니다.|  
|<xref:System.Xml.Xsl.XslTransform.Load%2A> 중에 `<xsl:include>` 또는 `<xsl:import>` 확인|매개 변수로 <xref:System.Xml.Xsl.XslTransform.Load%2A>를 사용하는 오버로드된 <xref:System.Xml.XmlResolver> 메서드를 지정합니다. <xref:System.Xml.XmlResolver>를 사용하여 `import` 또는 `include` 문에서 참조하는 스타일시트를 로드합니다. `null`로 전달하는 경우에는 외부 리소스가 확인되지 않습니다.|  
|변형 중에 모든 `document()` 함수 확인|<xref:System.Xml.XmlResolver> 인수를 사용하는 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 메서드를 통해 변환 중에 <xref:System.Xml.XmlResolver>를 지정합니다.|  
  
 `document()` 함수는 입력 스트림에서 제공하는 초기 XML 데이터뿐 아니라 스타일시트의 다른 XML 리소스도 검색합니다. 이 함수를 사용하면 어느 위치에 있는 XML 데이터도 포함시킬 수 있으므로 <xref:System.Xml.XmlResolver> 메서드에 `null` 값이 제공된 <xref:System.Xml.Xsl.XslTransform.Transform%2A>는 `document()` 함수가 실행되지 않도록 합니다. `document()` 함수를 사용하려면 적절한 권한을 설정하고 <xref:System.Xml.Xsl.XslTransform.Transform%2A>를 매개 변수로 사용하는 <xref:System.Xml.XmlResolver> 메서드를 사용합니다.  
  
 <xref:System.Xml.Xsl.XslTransform.Load%2A> 메서드 및 이 메서드에서 <xref:System.Xml.XmlResolver>를 사용하는 방법에 대한 자세한 내용은 <xref:System.Xml.Xsl.XslTransform.Load%28System.String%2CSystem.Xml.XmlResolver%29?displayProperty=nameWithType>를 참조하세요.  
  
 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 메서드가 호출되면 로드 시 제공된 증명 정보에 따라 권한이 판별되어 해당 권한 집합이 전체 변형 프로세스에 지정됩니다. `document()` 함수에서 해당 권한 집합에 없는 권한을 요구하는 작업을 시작하려고 하면 예외가 throw됩니다.  
  
## <a name="see-also"></a>참고 항목

- [XslTransform 클래스를 사용하여 XSLT 변형](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)  
- [XslTransform 클래스의 XSLT 프로세서 구현](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)  
- [XslTransform 출력](../../../../docs/standard/data/xml/outputs-from-an-xsltransform.md)  
- [여러 저장소에서의 XSLT 변환](../../../../docs/standard/data/xml/xslt-transformations-over-different-stores.md)  
- [스타일시트 매개 변수 및 확장명 개체의 XsltArgumentList](../../../../docs/standard/data/xml/xsltargumentlist-for-style-sheet-parameters-and-extension-objects.md)  
- [\<msxsl:script>를 사용한 XSLT 스타일시트 스크립트](../../../../docs/standard/data/xml/xslt-stylesheet-scripting-using-msxsl-script.md)  
- [msxsl:node-set() 함수에 대한 지원](../../../../docs/standard/data/xml/support-for-the-msxsl-node-set-function.md)  
- [변형 과정에서 XPathNavigator의 역할](../../../../docs/standard/data/xml/xpathnavigator-in-transformations.md)  
- [변형 과정에서 XPathNodeIterator의 역할](../../../../docs/standard/data/xml/xpathnodeiterator-in-transformations.md)  
- [XslTransform에 대한 XPathDocument 입력](../../../../docs/standard/data/xml/xpathdocument-input-to-xsltransform.md)  
- [XslTransform에 대한 XmlDataDocument 입력](../../../../docs/standard/data/xml/xmldatadocument-input-to-xsltransform.md)  
- [XslTransform에 대한 XmlDocument 입력](../../../../docs/standard/data/xml/xmldocument-input-to-xsltransform.md)
