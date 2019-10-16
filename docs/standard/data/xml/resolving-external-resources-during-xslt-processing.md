---
title: XSLT 처리 중 외부 리소스 확인
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 3a59d31c-0ec5-4de6-a2a9-558531c8116e
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 0bcd45a97ab0f0b0ac462d50c18fb68f9d7bd386
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64590020"
---
# <a name="resolving-external-resources-during-xslt-processing"></a>XSLT 처리 중 외부 리소스 확인
다음과 같이 XSLT 변형 중에 외부 리소스를 확인해야 하는 몇 가지 경우가 있습니다.  
  
## <a name="using-the-xmlresolver-class"></a>XmlResolver 클래스 사용  
 <xref:System.Xml.XmlResolver> 클래스를 사용하여 외부 리소스를 확인할 수 있습니다. 다음 표에서는 XSLT 처리 중 <xref:System.Xml.XmlResolver>가 관련되는 경우를 설명합니다.  
  
|XSLT 작업|XmlResolver를 사용하여 수행하는 작업|  
|---------------|--------------------------------------|  
|스타일시트를 컴파일합니다.|스타일시트의 URI를 확인합니다.<br /><br /> 및<br /><br /> `xsl:import` 또는 `xsl:include` 요소에서 URI 참조를 확인합니다.|  
|스타일시트를 실행합니다.|컨텍스트 문서의 URI를 확인합니다.<br /><br /> 및<br /><br /> XSLT `document()` 함수에서 URI 참조를 확인합니다.|  
  
 <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> 및 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 메서드는 <xref:System.Xml.XmlResolver> 개체를 해당 인수의 하나로 사용하는 오버로드를 포함합니다. <xref:System.Xml.XmlResolver>가 지정되지 않을 경우 기본 <xref:System.Xml.XmlUrlResolver>가 자격 증명 없이 사용됩니다.  
  
 다음 목록에서는 <xref:System.Xml.XmlResolver> 개체를 지정하려 할 수 있는 경우에 대해 설명합니다.  
  
- XSLT 처리에 인증을 요구하는 네트워크 리소스에 대한 액세스 권한이 필요할 경우 <xref:System.Xml.XmlResolver>를 필요한 자격 증명과 함께 사용할 수 있습니다.  
  
- XSLT 처리가 액세스할 수 있는 리소스를 제한하려면 <xref:System.Xml.XmlSecureResolver>를 올바른 권한 집합으로 사용할 수 있습니다. 제어하지 못하거나 신뢰할 수 없는 리소스를 열어야 하는 경우 <xref:System.Xml.XmlSecureResolver> 클래스를 사용합니다.  
  
- 동작을 사용자 지정하기 위해 사용자의 고유한 <xref:System.Xml.XmlResolver> 클래스를 구현하고 사용하여 리소스를 확인할 수 있습니다.  
  
- 외부 리소스에 액세스하지 않도록 하려면 `null` 인수에 대해 <xref:System.Xml.XmlResolver>을 지정할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 네트워크 리소스에 저장된 스타일시트를 컴파일합니다. <xref:System.Xml.XmlUrlResolver> 개체는 스타일시트에 액세스하는 데 필요한 자격 증명을 지정합니다.  
  
 [!code-csharp[XslCompiledTransform.Load#11](../../../../samples/snippets/csharp/VS_Snippets_Data/XslCompiledTransform.Load/CS/Xslt_Load_v2.cs#11)]
 [!code-vb[XslCompiledTransform.Load#11](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XslCompiledTransform.Load/VB/Xslt_Load_v2.vb#11)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.Xsl.XslCompiledTransform>
- <xref:System.Xml.Xsl.XsltSettings>
- [XSLT 변환](../../../../docs/standard/data/xml/xslt-transformations.md)
