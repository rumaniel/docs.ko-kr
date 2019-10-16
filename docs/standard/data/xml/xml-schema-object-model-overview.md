---
title: XML 스키마 개체 모델 개요
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 896a1e12-5655-42c6-8cdd-89c12862b34b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 97e2e54c534b30c3c514c9102ded0050fc154b75
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64589796"
---
# <a name="xml-schema-object-model-overview"></a>XML 스키마 개체 모델 개요
Microsoft .NET Framework의 SOM(스키마 개체 모델)은 프로그래밍 방식으로 스키마를 만들고 편집하고 유효성을 검사할 수 있는 다양한 API입니다. SOM은 DOM(문서 개체 모델)이 XML 문서에서 작동하는 것과 비슷한 방식으로 XML 스키마 문서에서 작동합니다. XML 스키마 문서는 유효한 XML 파일로, SOM에 로드된 후에는 스키마를 준수하는 다른 XML 문서의 구조와 유효성에 대한 의미를 전달합니다.  
  
 스키마는 특정 스키마에 대한 XML 문서의 구조나 모델을 지정하여 XML 문서의 클래스를 정의하는 XML 문서입니다. 스키마는 XML 문서 내용에 대한 제약 조건을 식별하고 XML 규격 문서가 준수해야 하는 용어 모음(규칙 또는 문법)을 정의하여 문서가 해당 스키마에 대해 유효한지 확인합니다. XML 문서의 유효성 검사는 문서가 스키마에 지정된 문법과 일치하는지를 확인하는 프로세스입니다.  
  
 다음은 .NET Framework의 SOM API를 사용하여 스키마를 만들고 편집하고 유효성을 검사하는 방법입니다.  
  
- 유효한 스키마를 파일로 또는 파일에서 로드 및 저장합니다.  
  
- 강력한 형식의 클래스를 사용하여 메모리 내 스키마를 만듭니다.  
  
- <xref:System.Xml.Schema.XmlSchemaSet>과 상호 작용하여 스키마를 캐시, 컴파일 및 검색합니다.  
  
- <xref:System.Xml.XmlReader.Create%2A> 클래스의 <xref:System.Xml.XmlReader> 메서드와 상호 작용하여 스키마에 대해 XML 인스턴스 문서의 유효성을 검사합니다.  
  
- 스키마를 만들고 유지 관리할 수 있는 편집기를 만듭니다.  
  
- XML 인스턴스 문서의 유효성 검사에 사용될 수 있도록 컴파일 및 저장할 수 있는 스키마를 동적으로 편집합니다.  
  
## <a name="the-schema-object-model"></a>스키마 개체 모델  
 SOM은 XML 스키마의 요소에 해당하는 <xref:System.Xml.Schema?displayProperty=nameWithType> 네임스페이스의 다양한 클래스 집합으로 구성됩니다. 예를 들어, `<xsd:schema>...</xsd:schema>` 요소는 <xref:System.Xml.Schema.XmlSchema?displayProperty=nameWithType> 클래스에 매핑되며 `<xsd:schema/>` 요소 내에 포함할 수 있는 모든 정보는 <xref:System.Xml.Schema.XmlSchema> 클래스를 사용하여 나타낼 수 있습니다. 마찬가지로 `<xsd:element>...</xsd:element>` 및 `<xsd:attribute>...</xsd:attribute>` 요소는 각각 <xref:System.Xml.Schema.XmlSchemaElement?displayProperty=nameWithType> 및 <xref:System.Xml.Schema.XmlSchemaAttribute?displayProperty=nameWithType> 클래스에 매핑됩니다. 다음 다이어그램에 표시된 <xref:System.Xml.Schema> 네임스페이스에서 XML 스키마 개체 모델을 만드는 XML 스키마의 모든 요소에 대해 이 매핑이 계속 수행됩니다.  
  
 ![System.Xml.Schema 개체 모델](./media/xml-schema-object-model-overview/xml-schema-object-model.gif)  
  
 <xref:System.Xml.Schema> 네임스페이스의 각 클래스에 대한 자세한 내용은 .NET Framework 클래스 라이브러리의 <xref:System.Xml.Schema> 네임스페이스 참조 문서를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [XML 스키마 읽기 및 쓰기](../../../../docs/standard/data/xml/reading-and-writing-xml-schemas.md)
- [XML 스키마 빌드](../../../../docs/standard/data/xml/building-xml-schemas.md)
- [XML 스키마 통과](../../../../docs/standard/data/xml/traversing-xml-schemas.md)
- [XML 스키마 편집](../../../../docs/standard/data/xml/editing-xml-schemas.md)
- [XML 스키마 포함하기 또는 가져오기](../../../../docs/standard/data/xml/including-or-importing-xml-schemas.md)
- [스키마 컴파일을 위한 XmlSchemaSet](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)
- [Post-Schema Compilation Infoset](../../../../docs/standard/data/xml/post-schema-compilation-infoset.md)
