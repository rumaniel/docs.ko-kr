---
title: XslCompiledTransform 클래스 사용
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: f9b074f6-d6f4-49dd-a093-df510bf0cf7b
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a524b80d8789567dc2aa943d7321fd49fe3c7c33
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939418"
---
# <a name="using-the-xslcompiledtransform-class"></a>XslCompiledTransform 클래스 사용
<xref:System.Xml.Xsl.XslCompiledTransform> 클래스는 Microsoft .NET Framework XSLT 프로세서입니다. 이 클래스를 사용하여 스타일시트를 컴파일하고 XSLT 변형을 실행할 수 있습니다.  
  
> [!NOTE]
> <xref:System.Xml.Xsl.XslCompiledTransform> 클래스의 전체적인 성능이 <xref:System.Xml.Xsl.XslTransform> 클래스보다 좋지만 <xref:System.Xml.Xsl.XslCompiledTransform> 클래스의 <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> 메서드는 변환에 대해 처음 호출될 때 <xref:System.Xml.Xsl.XslTransform> 클래스의 <xref:System.Xml.Xsl.XslTransform.Load%2A> 메서드보다 느리게 수행될 수 있습니다. 이는 XSLT 파일이 로드되기 전에 컴파일되어야 하기 때문입니다. 자세한 내용은 다음 블로그 게시물을 참조하세요. [XslCompiledTransform이 XslTransform보다 느리나요?](https://blogs.msdn.microsoft.com/antosha/2006/07/16/xslcompiledtransform-slower-than-xsltransform/)  
  
## <a name="in-this-section"></a>섹션 내용  
 [XslCompiledTransform 클래스에 대한 입력](../../../../docs/standard/data/xml/inputs-to-the-xslcompiledtransform-class.md)  
 사용할 수 있는 XSLT 입력 옵션에 대해 설명합니다.  
  
 [XslCompiledTransform 클래스의 출력 옵션](../../../../docs/standard/data/xml/output-options-on-the-xslcompiledtransform-class.md)  
 사용할 수 있는 XSLT 출력 옵션에 대해 설명합니다.  
  
 [XSLT 처리 중 외부 리소스 확인](../../../../docs/standard/data/xml/resolving-external-resources-during-xslt-processing.md)  
 <xref:System.Xml.XmlResolver> 클래스를 사용하여 외부 리소스를 확인하는 방법을 설명합니다.  
  
 [XSLT 스타일시트 확장](../../../../docs/standard/data/xml/extending-xslt-style-sheets.md)  
 XSLT 확장을 지원하는 방법을 설명합니다.  
  
|||  
|-|-|  
|[복구할 수 있는 XSLT 오류](../../../../docs/standard/data/xml/recoverable-xslt-errors.md)|W3C(World Wide Web 컨소시엄) XSLT 1.0 권장 사항에서 허용하는 임의 동작 및 <xref:System.Xml.Xsl.XslCompiledTransform> 클래스를 사용하여 임의 동작을 처리하는 방법을 보여 줍니다.|  
|[방법: 노드 조각 변환](../../../../docs/standard/data/xml/how-to-transform-a-node-fragment.md)|노드 조각을 변환하는 방법을 설명합니다.|  
  
## <a name="related-sections"></a>관련 단원  
 [XslTransform 클래스에서 마이그레이션](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)  
 <xref:System.Xml.Xsl.XslTransform> 클래스에서 코드를 마이그레이션하는 방법을 설명합니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.Xsl.XsltSettings>
- <xref:System.Xml.Xsl.XsltMessageEncounteredEventArgs>
