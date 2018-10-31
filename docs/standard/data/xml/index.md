---
title: XML 문서 및 데이터
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: e695047f-3c0f-4045-8708-5baea91cc380
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3b5c774d566766936ebe043f264040ce26b8e9e3
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50202961"
---
# <a name="xml-documents-and-data"></a>XML 문서 및 데이터
.NET Framework에서 XML 인식 응용 프로그램을 쉽게 작성할 수 있도록 하는 종합적이고 통합된 클래스 집합을 제공합니다. 다음 네임스페이스의 클래스에서는 XML 구문 분석 및 작성, 메모리에서의 XML 데이터 편집, 데이터 유효성 검사 및 XSLT 변형을 지원합니다.  
  
-   <xref:System.Xml>  
  
-   <xref:System.Xml.XPath>  
  
-   <xref:System.Xml.Xsl>  
  
-   <xref:System.Xml.Schema>  
  
-   <xref:System.Xml.Linq>  
  
 전체 목록은 [System.Xml Namespaces](https://msdn.microsoft.com/library/gg145036.aspx) 웹 페이지를 참조하세요.  
  
 이러한 네임스페이스의 클래스는 W3C(World Wide Web 컨소시엄) 권장 사항을 지원합니다. 예:  
  
-   <xref:System.Xml.XmlDocument?displayProperty=nameWithType> 클래스는 [W3C DOM(문서 개체 모델) Level 1 Core](https://www.w3.org/TR/REC-DOM-Level-1/) 및 [DOM Level 2 Core](https://www.w3.org/TR/DOM-Level-2-Core/) 권장 사항을 구현합니다.  
  
-   <xref:System.Xml.XmlReader?displayProperty=nameWithType> 및 <xref:System.Xml.XmlWriter?displayProperty=nameWithType> 클래스는 [W3C XML 1.0](https://www.w3.org/TR/2006/REC-xml-20060816/) 및 [XML의 네임스페이스](https://www.w3.org/TR/REC-xml-names/) 권장 사항을 지원합니다.  
  
-   <xref:System.Xml.Schema.XmlSchemaSet?displayProperty=nameWithType> 클래스의 스키마는 [W3C XML 스키마 1장: 구조](https://www.w3.org/TR/xmlschema-1/) 및 [XML 스키마 2장: 데이터 형식](https://www.w3.org/TR/xmlschema-2/) 권장 사항을 지원합니다.  
  
-   <xref:System.Xml.Xsl?displayProperty=nameWithType> 네임스페이스의 클래스는 [W3C XSLT 1.0](https://www.w3.org/TR/xslt) 권장 사항을 준수하는 XSLT 변환을 지원합니다.  
  
 .NET Framework의 XML 클래스는 다음과 같은 이점을 제공합니다.  
  
-   **생산성** [LINQ to XML](https://msdn.microsoft.com/library/f0fe21e9-ee43-4a55-b91a-0800e5782c13)을 사용하면 XML을 사용하여 더욱 쉽게 프로그래밍하고 SQL과 유사한 쿼리 환경을 제공합니다.  
  
-   **확장성** .NET Framework의 XML 클래스는 추상 기본 클래스와 가상 메서드를 사용하여 확장 가능합니다. 예를 들어, 캐시 스트림을 로컬 디스크에 저장하는 <xref:System.Xml.XmlUrlResolver> 클래스의 파생 클래스를 만들 수 있습니다.  
  
-   **플러그형 아키텍처** .NET Framework는 구성 요소를 서로 이용할 수 있고, 구성 요소 간에 데이터를 스트리밍할 수 있는 아키텍처를 제공합니다. 예를 들어 <xref:System.Xml.XPath.XPathDocument> 또는 <xref:System.Xml.XmlDocument> 개체와 같은 데이터 저장소는 <xref:System.Xml.Xsl.XslCompiledTransform> 클래스를 사용하여 변형할 수 있고, 출력이 다른 저장소로 스트리밍되거나 웹 서비스에서 스트림으로 반환됩니다.  
  
-   **성능.** 응용 프로그램 성능 개선을 위해 .NET Framework의 일부 XML 클래스는 다음과 같은 특징을 가진 스트리밍 기반 모델을 지원합니다.  
  
    -   앞으로만 이동 가능한 끌어오기 모델 구문 분석을 위한 최소 캐시(<xref:System.Xml.XmlReader>)  
  
    -   앞으로만 이동 가능한 유효성 검사(<xref:System.Xml.XmlReader>)  
  
    -   노드 생성이 단일 가상 노드로 최소화되지만 문서에 임의로 액세스할 수 있는 커서 스타일 탐색(<xref:System.Xml.XPath.XPathNavigator>).  
  
     성능 향상을 위해 XSLT 처리가 필요할 때마다 <xref:System.Xml.XPath.XPathDocument> 클래스를 사용합니다. <xref:System.Xml.Xsl.XslCompiledTransform>는  클래스와 함께 효율적으로 사용하도록 디자인된 XPath 쿼리를 위한 최적화된 읽기 전용 저장소입니다.  
  
-   **ADO.NET과의 통합** XML 클래스 및 [ADO.NET](../../../../docs/framework/data/adonet/index.md)은 관계형 데이터와 XML을 하나로 결합하도록 긴밀히 통합되어 있습니다. <xref:System.Data.DataSet> 클래스는 데이터베이스에서 파생된 데이터의 메모리 내 캐시입니다. <xref:System.Data.DataSet> 클래스에서는 <xref:System.Xml.XmlReader> 및 <xref:System.Xml.XmlWriter> 클래스를 사용하여 XML을 읽고 쓰며, 내부 관계형 스키마 구조를 XSD(XML 스키마)로 유지할 수 있을 뿐 아니라 XML 문서의 스키마 구조를 예측할 수도 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [XML 처리 옵션](../../../../docs/standard/data/xml/xml-processing-options.md)  
 XML 데이터를 처리하는 옵션에 대해 설명합니다.  
  
 [메모리 내 XML 데이터 처리](../../../../docs/standard/data/xml/processing-xml-data-in-memory.md)  
 메모리 내 XML 데이터 처리에 대한 세 가지 모델을 설명합니다. [LINQ to XML](https://msdn.microsoft.com/library/f0fe21e9-ee43-4a55-b91a-0800e5782c13), <xref:System.Xml.XmlDocument> 클래스(W3C 문서 개체 모델 기반) 및 <xref:System.Xml.XPath.XPathDocument> 클래스(XPath 데이터 모델 기반).  
  
 [XSLT 변환](../../../../docs/standard/data/xml/xslt-transformations.md)  
 XSLT 프로세서의 사용 방법에 대해 설명합니다.  
  
 [XML SOM(스키마 개체 모델)](../../../../docs/standard/data/xml/xml-schema-object-model-som.md)  
 <xref:System.Xml.Schema.XmlSchema> 클래스를 제공하여 XSD(XML 스키마)를 빌드 및 조작하고 스키마를 로드 및 편집하는 데 사용되는 클래스에 대해 설명합니다.  
  
 [XML과 관계형 데이터 및 ADO.NET의 통합](../../../../docs/standard/data/xml/xml-integration-with-relational-data-and-adonet.md)  
 .NET Framework에서 <xref:System.Data.DataSet> 개체 및 <xref:System.Xml.XmlDataDocument> 개체를 사용하여 관계형 데이터와 계층형 데이터에 실시간으로 동시에 액세스할 수 있는 방법에 대해 설명합니다.  
  
 [XML 문서의 네임스페이스 관리](../../../../docs/standard/data/xml/managing-namespaces-in-an-xml-document.md)  
 <xref:System.Xml.XmlNamespaceManager> 클래스를 사용하여 네임스페이스 정보를 저장하고 유지 관리하는 방법을 설명합니다.  
  
 [System.Xml 클래스의 형식 지원](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)  
 XML 데이터 형식을 CLR 형식으로 매핑하는 방법, XML 데이터 형식을 변환하는 방법 및 <xref:System.Xml> 클래스의 기능을 지원하는 기타 형식을 설명합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)  
 ADO.NET을 사용하여 데이터에 액세스하는 방법에 대한 정보를 제공합니다.  
  
 [보안](../../../../docs/standard/security/index.md)  
 .NET Framework 보안 시스템을 개략적으로 설명합니다.  
  