---
title: System.Xml 클래스의 형식 지원
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 63570538-06e3-4401-ad4d-ac50be90c7bf
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 954ff12ae1ac8b4d601c35fcd76ea35b2bb3acbf
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939447"
---
# <a name="type-support-in-the-systemxml-classes"></a>System.Xml 클래스의 형식 지원
.NET Framework 버전 2.0에서는 형식 지원 기능을 포함하도록 핵심 XML 클래스가 향상되었습니다. <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlWriter> 및 <xref:System.Xml.XPath.XPathNavigator> 클래스에는 XML 스키마 형식과 CLR(공용 언어 런타임) 형식 간의 변환 기능을 비롯한 형식 지원 기능이 들어 있습니다.  
  
 .NET Framework 버전 2.0에서는 형식 지원 기능을 포함하도록 <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlWriter> 및 <xref:System.Xml.XPath.XPathNavigator> 클래스가 향상되었습니다.  
  
- <xref:System.Xml.XmlReader> 및 <xref:System.Xml.XPath.XPathNavigator> 클래스는 각각 노드에서 스키마 정보를 반환하는 **SchemaInfo** 속성을 포함하고 있습니다.  
  
- **ReadContentAs**와 **ReadElementContentAs** 및 <xref:System.Xml.XmlReader> 클래스의 메서드는 텍스트 값을 읽어온 후 단일 메서드 호출에서 CLR 값으로 변환합니다.  
  
- <xref:System.Xml.XmlWriter.WriteValue%2A> 클래스의 <xref:System.Xml.XmlWriter> 메서드는 XML을 작성할 때 CLR 형식을 XML 스키마 형식으로 변환합니다.  
  
- **ValueAs** 및 <xref:System.Xml.XPath.XPathNavigator> 클래스의 <xref:System.Xml.XPath.XPathNavigator.TypedValue%2A> 속성은 노드 값을 반환하고 단일 메서드 호출에서 이 값을 CLR 값으로 변환합니다.  
  
> [!NOTE]
> .NET Framework 버전 1.0에서는 XML 스키마와 CLR 형식 간에 변환하려면 <xref:System.Xml.XmlConvert> 클래스가 필요했습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [CLR 형식에 XML 데이터 형식 매핑](../../../../docs/standard/data/xml/mapping-xml-data-types-to-clr-types.md)  
 기본적으로 XML 데이터 형식을 CLR 형식에 매핑하는 방법을 설명합니다.  
  
 [XML 형식 지원 구현 참고 사항](../../../../docs/standard/data/xml/xml-type-support-implementation-notes.md)  
 형식 지원 구현에 대해 상세히 설명합니다.  
  
 [XML 데이터 형식 변환](../../../../docs/standard/data/xml/conversion-of-xml-data-types.md)  
 <xref:System.Xml.XmlConvert> 클래스를 사용하여 XML 스키마와 CLR 형식 간에 변환하는 방법을 설명합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [XPathNavigator를 사용하여 강력한 형식의 XML 데이터 액세스](../../../../docs/standard/data/xml/accessing-strongly-typed-xml-data-using-xpathnavigator.md)
