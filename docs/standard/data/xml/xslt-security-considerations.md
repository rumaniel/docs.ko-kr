---
title: XSLT 보안 고려 사항
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: fea695be-617c-4977-9567-140e820436fc
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 77f29cb14af90854fa18f421acbeb701928bcd76
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50034367"
---
# <a name="xslt-security-considerations"></a>XSLT 보안 고려 사항
XSLT 언어에는 강력하며 유연성 있는 풍부한 기능이 있습니다. 이러한 기능은 유용하지만 외부 소스에서 악용할 수도 있습니다. XSLT를 안전하게 사용하려면 XSLT를 사용할 때 발생하는 보안 문제 유형을 이해하고 이러한 위험 요소를 완화하기 위한 기본적인 전략을 알아야 합니다.  
  
## <a name="xslt-extensions"></a>XSLT 확장명  
 가장 많이 사용되는 두 가지 XSLT 확장은 스타일시트 스크립팅과 확장 개체입니다. 이러한 확장을 사용하면 XSLT 프로세서에서 코드를 실행할 수 있습니다.  
  
-   확장 개체는 프로그래밍 기능을 XSLT(XSL Transformations)에 추가합니다.  
  
-   `msxsl:script` 확장 요소를 사용하여 스타일시트에 스크립트를 포함할 수 있습니다.  
  
### <a name="extension-objects"></a>확장명 개체  
 <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A> 메서드를 사용하여 확장 개체를 추가합니다. 확장 개체를 지원하려면 FullTrust 권한 집합이 필요합니다. 이 권한 집합은 확장명 개체 코드를 실행할 때 권한 높이기가 일어나지 않도록 합니다. FullTrust 권한 없이 <xref:System.Xml.Xsl.XsltArgumentList.AddExtensionObject%2A> 메서드를 호출하려고 시도하면 보안 예외가 throw됩니다.  
  
### <a name="style-sheet-scripts"></a>스타일시트 스크립트  
 `msxsl:script` 확장명 요소를 사용하여 스타일시트에 스크립트를 포함할 수 있습니다. 스크립트 지원은 <xref:System.Xml.Xsl.XslCompiledTransform> 클래스의 선택적 기능으로 기본적으로 비활성화되어 있습니다. 스크립트를 활성화하려면 <xref:System.Xml.Xsl.XsltSettings.EnableScript%2A?displayProperty=nameWithType> 속성을 `true`로 설정하고 <xref:System.Xml.Xsl.XsltSettings> 개체를 <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> 메서드에 전달합니다.  
  
#### <a name="guidelines"></a>지침  
 신뢰할 수 있는 소스에서 스타일시트를 가져온 경우에만 스크립팅을 활성화합니다. 스타일시트의 소스를 확인할 수 없는 경우 또는 신뢰할 수 있는 소스에서 스타일시트를 가져오지 않은 경우 XSLT 설정 인수에 대해 `null`을 전달합니다.  
  
## <a name="external-resources"></a>외부 리소스  
 XSLT 언어에는 프로세서가 URI 참조를 확인해야 하는 `xsl:import`, `xsl:include`, `document()` 함수 등의 기능이 있습니다. <xref:System.Xml.XmlResolver> 클래스를 사용하여 외부 리소스를 확인할 수 있습니다. 다음 두 가지 경우에 외부 리소스를 확인해야 할 수 있습니다.  
  
-   스타일시트를 컴파일할 때 <xref:System.Xml.XmlResolver> 및 `xsl:import` 확인에 `xsl:include`가 사용되는 경우  
  
-   변환을 실행할 때 <xref:System.Xml.XmlResolver>를 사용하여 `document()` 함수를 확인하는 경우  
  
    > [!NOTE]
    >  `document()` 클래스에서 <xref:System.Xml.Xsl.XslCompiledTransform> 함수는 기본적으로 비활성화되어 있습니다. 이 기능을 활성화하려면 <xref:System.Xml.Xsl.XsltSettings.EnableDocumentFunction%2A?displayProperty=nameWithType> 속성을 `true`로 설정하고 <xref:System.Xml.Xsl.XsltSettings> 개체를 <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> 메서드에 전달합니다.  
  
 <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> 및 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 메서드는 각각 인수의 하나로 <xref:System.Xml.XmlResolver>를 사용하는 오버로드를 포함합니다. <xref:System.Xml.XmlResolver>가 지정되지 않을 경우 기본 <xref:System.Xml.XmlUrlResolver>가 자격 증명 없이 사용됩니다.  
  
#### <a name="guidelines"></a>지침  
 신뢰할 수 있는 소스에서 스타일시트를 가져온 경우에만 `document()` 함수를 활성화합니다.  
  
 다음 목록에서는 <xref:System.Xml.XmlResolver> 개체를 지정하려 할 수 있는 경우에 대해 설명합니다.  
  
-   XSLT 처리에 인증을 요구하는 네트워크 리소스에 대한 액세스 권한이 필요할 경우 <xref:System.Xml.XmlResolver>를 필요한 자격 증명과 함께 사용할 수 있습니다.  
  
-   XSLT 처리가 액세스할 수 있는 리소스를 제한하려면 <xref:System.Xml.XmlSecureResolver>를 올바른 권한 집합으로 사용할 수 있습니다. 사용자가 제어하지 않거나 신뢰할 수 없는 리소스를 열어야 하는 경우에는 <xref:System.Xml.XmlSecureResolver> 클래스를 사용합니다.  
  
-   동작을 사용자 지정하기 위해 사용자의 고유한 <xref:System.Xml.XmlResolver> 클래스를 구현하고 사용하여 리소스를 확인할 수 있습니다.  
  
-   외부 리소스에 액세스하지 않도록 하려면 `null` 인수에 대해 <xref:System.Xml.XmlResolver>을 지정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [XSLT 변환](../../../../docs/standard/data/xml/xslt-transformations.md)  
- [XSLT 처리 중 외부 리소스 확인](../../../../docs/standard/data/xml/resolving-external-resources-during-xslt-processing.md)  
- [코드 액세스 보안](../../../../docs/framework/misc/code-access-security.md)
