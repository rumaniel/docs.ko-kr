---
title: XML 스키마 통과
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
ms.assetid: cce69574-5861-4a30-b730-2e18d915d8ee
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6040a7aa8f3244ea0ce2e66042537bc45c347b05
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70037848"
---
# <a name="traversing-xml-schemas"></a>XML 스키마 통과

SOM(스키마 개체 모델) API를 사용하여 XML 스키마를 통과하면 SOM에 저장된 요소, 특성 및 형식에 액세스할 수 있습니다. SOM에 로드된 XML 스키마를 통과하는 것은 SOM API를 사용하여 XML 스키마를 편집하는 첫 번째 단계이기도 합니다.

## <a name="traversing-an-xml-schema"></a>XML 스키마 통과

다음 <xref:System.Xml.Schema.XmlSchema> 클래스 속성에서는 XML 스키마에 추가된 모든 전역 항목의 컬렉션에 액세스할 수 있습니다.

|속성|컬렉션 또는 배열에 저장된 개체 형식|
|--------------|---------------------------------------------------|
|<xref:System.Xml.Schema.XmlSchema.Elements%2A>|<xref:System.Xml.Schema.XmlSchemaElement>|
|<xref:System.Xml.Schema.XmlSchema.Attributes%2A>|<xref:System.Xml.Schema.XmlSchemaAttribute>|
|<xref:System.Xml.Schema.XmlSchema.AttributeGroups%2A>|<xref:System.Xml.Schema.XmlSchemaAttributeGroup>|
|<xref:System.Xml.Schema.XmlSchema.Groups%2A>|<xref:System.Xml.Schema.XmlSchemaGroup>|
|<xref:System.Xml.Schema.XmlSchema.Includes%2A>|<xref:System.Xml.Schema.XmlSchemaExternal>, <xref:System.Xml.Schema.XmlSchemaInclude>, <xref:System.Xml.Schema.XmlSchemaImport> 또는 <xref:System.Xml.Schema.XmlSchemaRedefine>|
|<xref:System.Xml.Schema.XmlSchema.Items%2A>|<xref:System.Xml.Schema.XmlSchemaObject>(모든 전역 수준 요소, 특성 및 형식에 대한 액세스 제공)|
|<xref:System.Xml.Schema.XmlSchema.Notations%2A>|<xref:System.Xml.Schema.XmlSchemaNotation>|
|<xref:System.Xml.Schema.XmlSchema.SchemaTypes%2A>|<xref:System.Xml.Schema.XmlSchemaType>, <xref:System.Xml.Schema.XmlSchemaSimpleType>, <xref:System.Xml.Schema.XmlSchemaComplexType>|
|<xref:System.Xml.Schema.XmlSchema.UnhandledAttributes%2A>|<xref:System.Xml.XmlAttribute>(스키마 네임스페이스에 속하지 않은 특성에 대한 액세스 제공)|

> [!NOTE]
> <xref:System.Xml.Schema.XmlSchema.Items%2A> 속성을 제외하고 위의 표에 나열된 모든 속성은 스키마를 컴파일해야 사용할 수 있는 PSCI(Post-Schema-Compilation-Infoset) 속성입니다. <xref:System.Xml.Schema.XmlSchema.Items%2A> 속성은 스키마를 컴파일하기 전에 모든 전역 수준 요소, 특성 및 형식에 액세스하여 이를 편집하는 데 사용할 수 있는 pre-schema-compilation 속성입니다.
>
> <xref:System.Xml.Schema.XmlSchema.UnhandledAttributes%2A> 속성은 스키마 네임스페이스에 속하지 않은 모든 특성에 대한 액세스를 제공합니다. 이러한 특성은 스키마 프로세서로 처리되지 않습니다.

다음 코드 예제에서는 [XML 스키마 빌드](../../../../docs/standard/data/xml/building-xml-schemas.md) 항목에서 만든 고객 스키마를 트래버스하는 예를 보여줍니다. 이 코드 예제에서는 위에서 설명한 컬렉션을 사용하여 스키마를 통과하는 것을 보여 주고 스키마의 모든 요소와 특성을 콘솔에 작성합니다.

이 샘플은 다음과 같은 단계로 고객 스키마를 통과합니다.

1. 고객 스키마를 새 <xref:System.Xml.Schema.XmlSchemaSet> 개체에 추가한 다음 컴파일합니다. 스키마를 읽거나 컴파일할 때 발생하는 모든 스키마 유효성 검사 경고 및 오류는 <xref:System.Xml.Schema.ValidationEventHandler> 대리자에서 처리됩니다.

2. <xref:System.Xml.Schema.XmlSchema> 속성을 반복하여 <xref:System.Xml.Schema.XmlSchemaSet>에서 컴파일된 <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> 개체를 검색합니다. 스키마가 컴파일되므로 PSCI(Post-Schema-Compilation-Infoset) 속성에 액세스할 수 있습니다.

3. 각 요소 이름을 콘솔에 작성하는 post-schema-compilation <xref:System.Xml.Schema.XmlSchemaElement> 컬렉션의 <xref:System.Xml.Schema.XmlSchemaObjectTable.Values%2A> 컬렉션에서 각 <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=nameWithType>를 반복합니다.

4. `Customer` 클래스를 사용하여 <xref:System.Xml.Schema.XmlSchemaComplexType> 요소의 복합 형식을 얻습니다.

5. 복합 형식에 특성이 있을 경우 <xref:System.Collections.IDictionaryEnumerator>가 각 <xref:System.Xml.Schema.XmlSchemaAttribute>를 열거하도록 하고 그 이름을 콘솔에 작성합니다.

6. <xref:System.Xml.Schema.XmlSchemaSequence> 클래스를 사용하여 복합 형식의 sequence 파티클을 얻습니다.

7. 각 자식 요소의 이름을 콘솔에 작성하는 <xref:System.Xml.Schema.XmlSchemaElement> 컬렉션에서 각 <xref:System.Xml.Schema.XmlSchemaSequence.Items%2A?displayProperty=nameWithType>를 반복합니다.

다음은 전체 코드 예제입니다.

[!code-cpp[XmlSchemaTraverseExample#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaTraverseExample/CPP/XmlSchemaTraverseExample.cpp#1)]
[!code-csharp[XmlSchemaTraverseExample#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaTraverseExample/CS/XmlSchemaTraverseExample.cs#1)]
[!code-vb[XmlSchemaTraverseExample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaTraverseExample/VB/XmlSchemaTraverseExample.vb#1)]

<xref:System.Xml.Schema.XmlSchemaElement.ElementSchemaType%2A?displayProperty=nameWithType> 속성이 사용자 정의 단순 형식 또는 복합 형식인 경우 이 속성은 <xref:System.Xml.Schema.XmlSchemaSimpleType> 또는 <xref:System.Xml.Schema.XmlSchemaComplexType>일 수 있습니다. 또한 W3C XML 스키마 권장 사항에 정의된 기본 제공 데이터 형식 중 하나인 경우 <xref:System.Xml.Schema.XmlSchemaDatatype>일 수도 있습니다. 고객 스키마에서 <xref:System.Xml.Schema.XmlSchemaElement.ElementSchemaType%2A> 요소의 `Customer`은 <xref:System.Xml.Schema.XmlSchemaComplexType>이고 `FirstName` 및 `LastName` 요소는 <xref:System.Xml.Schema.XmlSchemaSimpleType>입니다.

[XML 스키마 빌드](../../../../docs/standard/data/xml/building-xml-schemas.md) 항목의 코드 예제에서는 <xref:System.Xml.Schema.XmlSchemaComplexType.Attributes%2A?displayProperty=nameWithType> 컬렉션을 사용하여 `Customer` 요소에 `CustomerId` 특성을 추가했습니다. 이 속성은 pre-schema-compilation 속성입니다. 해당 Post-Schema-Compilation-Infoset 속성은 형식 파생을 통해 상속된 특성을 비롯하여 복합 형식의 모든 특성을 보유하는 <xref:System.Xml.Schema.XmlSchemaComplexType.AttributeUses%2A?displayProperty=nameWithType> 컬렉션입니다.

## <a name="see-also"></a>참고 항목

- [XML 스키마 개체 모델 개요](../../../../docs/standard/data/xml/xml-schema-object-model-overview.md)
- [XML 스키마 읽기 및 쓰기](../../../../docs/standard/data/xml/reading-and-writing-xml-schemas.md)
- [XML 스키마 빌드](../../../../docs/standard/data/xml/building-xml-schemas.md)
- [XML 스키마 편집](../../../../docs/standard/data/xml/editing-xml-schemas.md)
- [XML 스키마 포함하기 또는 가져오기](../../../../docs/standard/data/xml/including-or-importing-xml-schemas.md)
- [스키마 컴파일을 위한 XmlSchemaSet](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)
- [Post-Schema Compilation Infoset](../../../../docs/standard/data/xml/post-schema-compilation-infoset.md)
