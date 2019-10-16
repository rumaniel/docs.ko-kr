---
ms.openlocfilehash: be9933e177954dc0aced81a550ef92f2c2ca08f4
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804519"
---
### <a name="xslt-style-sheet-exception-message-changed"></a>XSLT 스타일 시트 예외 메시지가 변경됨

|   |   |
|---|---|
|세부 정보|.NET Framework 4.5에서 XSLT 파일이 너무 복잡할 경우 오류 메시지의 텍스트는 &quot;스타일시트가 너무 복잡합니다.&quot; 이전 버전에서 오류 메시지는 &quot;XSLT 컴파일 오류입니다.&quot;였습니다. 오류 메시지 텍스트에 종속되어 있는 애플리케이션 코드는 더 이상 작동하지 않습니다. 그러나 예외 형식은 동일하게 유지되므로 이 변경은 실제 영향을 미쳐서는 안 됩니다.|
|제안 해결 방법|이 오류 조건에서 새 메시지를 예상하여 예외 메시지에 따라 응용 프로그램 코드를 업데이트하거나 더욱 좋은 방법은 변경되지 않는 예외 형식(<xref:System.Xml.Xsl.XsltException?displayProperty=name>)에만 종속되도록 코드를 업데이트합니다.|
|범위|Microsoft Edge|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Type)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Xml.XmlReader)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Xml.XPath.IXPathNavigable)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Reflection.MethodInfo,System.Byte[],System.Type[])?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.String,System.Xml.Xsl.XsltSettings,System.Xml.XmlResolver)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Xml.XmlReader,System.Xml.Xsl.XsltSettings,System.Xml.XmlResolver)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Xml.XPath.IXPathNavigable,System.Xml.Xsl.XsltSettings,System.Xml.XmlResolver)?displayProperty=nameWithType></li></ul>|
