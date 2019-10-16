---
title: XML 형식 지원 구현 참고 사항
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 26b071f3-1261-47ef-8690-0717f5cd93c1
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 817d48e15f3a1d370e1953ca9c9aa8e10baa7f29
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916028"
---
# <a name="xml-type-support-implementation-notes"></a>XML 형식 지원 구현 참고 사항
이 항목에서는 자세히 알아야 할 몇 가지 구현 정보에 대해 설명합니다.  
  
## <a name="list-mappings"></a>목록 매핑  
 <xref:System.Collections.IList>, <xref:System.Collections.ICollection>, <xref:System.Collections.IEnumerable>, **Type[]** 및 <xref:System.String> 형식을 사용하여 XSD(XML 스키마 정의 언어) 목록 형식을 나타낼 수 있습니다.  
  
## <a name="union-mappings"></a>통합 매핑  
 <xref:System.Xml.Schema.XmlAtomicValue> 또는 <xref:System.String> 형식을 사용하여 통합 형식을 나타낼 수 있습니다. 그러므로 소스 형식 또는 대상 형식은 항상 <xref:System.String> 또는 <xref:System.Xml.Schema.XmlAtomicValue>여야 합니다.  
  
 <xref:System.Xml.Schema.XmlSchemaDatatype> 개체가 목록 형식을 나타내는 경우 이 개체는 입력 문자열 값을 하나 이상의 개체 목록으로 변환합니다. <xref:System.Xml.Schema.XmlSchemaDatatype>이 통합 형식을 나타내는 경우 입력 값을 통합 멤버 형식으로 구문 분석하려고 시도합니다. 구문 분석이 실패하면 다음 통합 멤버로 변환이 시도되는 등 변환이 성공할 때까지 시도되며 시도할 다른 멤버 형식이 없으면 예외가 throw됩니다.  
  
## <a name="differences-between-clr-and-xml-data-types"></a>CLR 형식과 XML 데이터 형식의 차이  
 다음에서는 CLR 형식과 XML 데이터 형식 간에 발생할 수 있는 불일치 및 이에 대한 처리 방법을 설명합니다.  
  
> [!NOTE]
> `xs` 접두사는 <https://www.w3.org/2001/XMLSchema> 및 네임스페이스 URI에 매핑됩니다.
  
### <a name="systemtimespan-and-xsduration"></a>System.TimeSpan 및 xs:duration  
 다르지만 동등한 특정 기간 값이 있다는 점에서 `xs:duration` 형식은 부분적으로 정렬됩니다. 이는 `xs:duration` 형식의 경우 1개월(P1M)과 같은 값은 32일(P32D)보다 작고 27일(P27D)보다 크며 28일, 29일 또는 30일과 같음을 의미합니다.  
  
 <xref:System.TimeSpan> 클래스는 이러한 부분 정렬을 지원하지 않습니다. 대신 이 클래스는 1년과 1개월에 대해 각각 365일과 30일의 특정 일 수를 선택합니다.  
  
 `xs:duration` 형식에 대한 자세한 내용은 W3C [XML Schema Part 2: Datatypes Recommendation](https://www.w3.org/TR/xmlschema-2/)(XML 스키마 2부: Datatypes 권장 사항)을 참조하세요.
  
### <a name="xstime-gregorian-date-types-and-systemdatetime"></a>xs:time, 양력 날짜 형식 및 System.DateTime  
 `xs:time` 값을 <xref:System.DateTime> 개체에 매핑하면 <xref:System.DateTime.MinValue> 필드를 사용하여 <xref:System.DateTime>, <xref:System.DateTime.Year%2A> 및 <xref:System.DateTime.Month%2A>와 같은 <xref:System.DateTime.Day%2A> 개체의 날짜 속성이 가능한 가장 작은 <xref:System.DateTime> 값으로 초기화됩니다.  
  
 마찬가지로 `xs:gMonth`, `xs:gDay`, `xs:gYear`, `xs:gYearMonth` 및 `xs:gMonthDay`의 인스턴스도 <xref:System.DateTime> 개체에 매핑됩니다. <xref:System.DateTime> 개체에서 사용되지 않는 속성은 <xref:System.DateTime.MinValue>의 속성으로 초기화됩니다.  
  
> [!NOTE]
> 콘텐츠 형식이 <xref:System.DateTime.Year%2A?displayProperty=nameWithType>로 지정된 경우 `xs:gMonthDay` 값을 사용할 수 없습니다. 이 경우 <xref:System.DateTime.Year%2A?displayProperty=nameWithType> 값은 항상 1904로 설정됩니다.  
  
### <a name="xsanyuri-and-systemuri"></a>xs:anyURI 및 System.Uri  
 상대 URI를 나타내는 `xs:anyURI`의 인스턴스가 <xref:System.Uri>로 매핑될 경우에는 <xref:System.Uri> 개체에 기본 URI가 없습니다.  
  
## <a name="see-also"></a>참고 항목

- [System.Xml 클래스의 형식 지원](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)
