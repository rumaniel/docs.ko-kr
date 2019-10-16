---
title: XML 스키마 편집
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
ms.assetid: fa09c8e5-c2b9-49d2-bb0d-40330cd13e4d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: bd40677b3b21a4ee1b237656ea2814badbbcd593
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70040763"
---
# <a name="editing-xml-schemas"></a>XML 스키마 편집

XML 스키마 편집 기능은 SOM(스키마 개체 모델)의 중요한 기능 중 하나입니다. SOM의 모든 pre-schema-compilation 속성을 사용하여 XML 스키마에서 기존 값을 변경할 수 있습니다. 그런 다음 XML 스키마를 다시 컴파일하여 변경 내용을 적용할 수 있습니다.

SOM에 로드된 스키마를 편집하는 첫 번째 단계는 스키마를 통과하는 것입니다. 스키마를 편집하기 전에 SOM API를 사용하여 스키마를 통과하는 방법을 잘 알아야 합니다. 또한 PSCI(Post-Schema-Compilation-Infoset)의 pre-schema-compilation 속성과 post-schema-compilation 속성에 대해 잘 알아야 합니다.

## <a name="editing-an-xml-schema"></a>XML 스키마 편집

이 단원에서는 [XML 스키마 빌드](../../../../docs/standard/data/xml/building-xml-schemas.md) 항목에서 만든 고객 스키마를 편집하는 두 코드 예제가 제공됩니다. 첫 번째 코드 예제는 새 `PhoneNumber` 요소를 `Customer` 요소에 추가하며 두 번째 코드 예제는 새 `Title` 특성을 `FirstName` 요소에 추가합니다. 또한 첫 번째 샘플에서는 post-schema-compilation <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=nameWithType> 컬렉션을 사용하여 고객 스키마를 통과하며 두 번째 코드 예제에서는 pre-schema-compilation <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=nameWithType> 컬렉션을 사용합니다.

### <a name="phonenumber-element-example"></a>PhoneNumber 요소 예제

이 첫 번째 코드 예제에서는 새 `PhoneNumber` 요소를 고객 스키마의 `Customer` 요소에 추가합니다. 이 코드 예제는 다음과 같은 단계로 고객 스키마를 편집합니다.

1. 고객 스키마를 새 <xref:System.Xml.Schema.XmlSchemaSet> 개체에 추가한 다음 컴파일합니다. 스키마를 읽거나 컴파일할 때 발생하는 모든 스키마 유효성 검사 경고 및 오류는 <xref:System.Xml.Schema.ValidationEventHandler> 대리자에서 처리됩니다.

2. <xref:System.Xml.Schema.XmlSchema> 속성을 반복하여 <xref:System.Xml.Schema.XmlSchemaSet>에서 컴파일된 <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> 개체를 검색합니다. 스키마가 컴파일되므로 PSCI(Post-Schema-Compilation-Infoset) 속성에 액세스할 수 있습니다.

3. `PhoneNumber` 클래스를 사용하여 <xref:System.Xml.Schema.XmlSchemaElement> 요소를 만들고, `xs:string` 및 <xref:System.Xml.Schema.XmlSchemaSimpleType> 클래스를 사용하여 <xref:System.Xml.Schema.XmlSchemaSimpleTypeRestriction> 단순 형식 제한을 만들고, 이 제한의 <xref:System.Xml.Schema.XmlSchemaSimpleTypeRestriction.Facets%2A> 속성에 패턴 패싯을 추가하고 이 제한을 단순 형식의 <xref:System.Xml.Schema.XmlSchemaSimpleType.Content%2A> 속성에 추가하고 단순 형식을 <xref:System.Xml.Schema.XmlSchemaElement.SchemaType%2A> 요소의 `PhoneNumber`에 추가합니다.

4. post-schema-compilation <xref:System.Xml.Schema.XmlSchemaElement> 컬렉션의 <xref:System.Xml.Schema.XmlSchemaObjectTable.Values%2A> 컬렉션에서 각 <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=nameWithType>를 반복합니다.

5. 요소의 <xref:System.Xml.Schema.XmlSchemaElement.QualifiedName%2A>이 `"Customer"`인 경우 `Customer` 클래스를 사용하여 <xref:System.Xml.Schema.XmlSchemaComplexType> 요소의 복합 형식을 얻고 <xref:System.Xml.Schema.XmlSchemaSequence> 클래스를 사용하여 복합 형식의 sequence 파티클을 얻습니다.

6. 기존 `PhoneNumber` 및 `FirstName` 요소가 포함된 시퀀스의 pre-schema-compilation `LastName` 컬렉션을 사용하여 이 시퀀스에 새 <xref:System.Xml.Schema.XmlSchemaSequence.Items%2A> 요소를 추가합니다.

7. 마지막으로, <xref:System.Xml.Schema.XmlSchema> 클래스의 <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> 및 <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> 메서드를 사용하여 수정된 <xref:System.Xml.Schema.XmlSchemaSet> 개체를 다시 처리하고 컴파일하여 콘솔에 작성합니다.

다음은 전체 코드 예제입니다.

[!code-cpp[XmlSchemaEditExample1#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaEditExample1/CPP/XmlSchemaEditExample1.cpp#1)]
[!code-csharp[XmlSchemaEditExample1#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaEditExample1/CS/XmlSchemaEditExample1.cs#1)]
[!code-vb[XmlSchemaEditExample1#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaEditExample1/VB/XmlSchemaEditExample1.vb#1)]

다음은 [XML 스키마 빌드](../../../../docs/standard/data/xml/building-xml-schemas.md) 항목에서 만든 고객 스키마를 수정한 예제입니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema xmlns:tns="http://www.tempuri.org" targetNamespace="http://www.tempuri.org" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="Customer">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="FirstName" type="xs:string" />
        <xs:element name="LastName" type="tns:LastNameType" />
        <xs:element name="PhoneNumber">           <xs:simpleType>             <xs:restriction base="xs:string">               <xs:pattern value="\d{3}-\d{3}-\d(4)" />             </xs:restriction>           </xs:simpleType>         </xs:element>
      </xs:sequence>
      <xs:attribute name="CustomerId" type="xs:positiveInteger" use="required" /
>
    </xs:complexType>
  </xs:element>
  <xs:simpleType name="LastNameType">
    <xs:restriction base="xs:string">
      <xs:maxLength value="20" />
    </xs:restriction>
  </xs:simpleType>
</xs:schema>
```

### <a name="title-attribute-example"></a>Title 특성 예제

이 두 번째 코드 예제에서는 새 `Title` 특성을 고객 스키마의 `FirstName` 요소에 추가합니다. 첫 번째 코드 예제에서 `FirstName` 요소의 형식은 `xs:string`입니다. `FirstName` 요소가 문자열 내용과 함께 특성을 가지려면 그 형식을 단순 내용 확장 내용 모델이 있는 복합 형식으로 변경해야 합니다.

이 코드 예제는 다음과 같은 단계로 고객 스키마를 편집합니다.

1. 고객 스키마를 새 <xref:System.Xml.Schema.XmlSchemaSet> 개체에 추가한 다음 컴파일합니다. 스키마를 읽거나 컴파일할 때 발생하는 모든 스키마 유효성 검사 경고 및 오류는 <xref:System.Xml.Schema.ValidationEventHandler> 대리자에서 처리됩니다.

2. <xref:System.Xml.Schema.XmlSchema> 속성을 반복하여 <xref:System.Xml.Schema.XmlSchemaSet>에서 컴파일된 <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> 개체를 검색합니다. 스키마가 컴파일되므로 PSCI(Post-Schema-Compilation-Infoset) 속성에 액세스할 수 있습니다.

3. `FirstName` 클래스를 사용하여 <xref:System.Xml.Schema.XmlSchemaComplexType> 요소에 대한 새 복합 형식을 만듭니다.

4. `xs:string` 및 <xref:System.Xml.Schema.XmlSchemaSimpleContent> 클래스를 사용하여 <xref:System.Xml.Schema.XmlSchemaSimpleContentExtension>의 기본 형식으로 새 단순 내용 확장을 만듭니다.

5. `Title` 클래스를 사용하여 <xref:System.Xml.Schema.XmlSchemaAttribute>의 <xref:System.Xml.Schema.XmlSchemaAttribute.SchemaTypeName%2A>으로 새 `xs:string` 특성을 만들고 이 특성을 단순 내용 확장에 추가합니다.

6. 단순 내용의 내용 모델을 단순 내용 확장으로 설정하고 복합 형식의 내용 모델을 단순 내용으로 설정합니다.

7. 새 복합 형식을 pre-schema-compilation <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=nameWithType> 컬렉션에 추가합니다.

8. 스키마 사전 컴파일 <xref:System.Xml.Schema.XmlSchemaObject> 컬렉션의 각 <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=nameWithType>를 반복합니다.

> [!NOTE]
> `FirstName` 요소는 스키마에서 전역 요소가 아니므로 <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=nameWithType> 또는 <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=nameWithType> 컬렉션에서 사용할 수 없습니다. 이 코드 예제에서는 먼저 `FirstName` 요소를 찾아서 `Customer` 요소를 찾습니다.
>
> 첫 번째 코드 예제에서는 post-schema-compilation <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=nameWithType> 컬렉션을 사용하여 스키마를 통과했습니다. 이 샘플에서는 pre-schema-compilation <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=nameWithType> 컬렉션을 사용하여 스키마를 통과합니다. 두 컬렉션은 모두 스키마에서 전역 요소에 대한 액세스를 제공하지만 <xref:System.Xml.Schema.XmlSchema.Items%2A> 컬렉션을 반복하면 스키마에서 모든 전역 요소를 반복해야 하므로 시간이 더 많이 걸리며 PSCI 속성이 없습니다. <xref:System.Xml.Schema.XmlSchema.Elements%2A?displayProperty=nameWithType>, <xref:System.Xml.Schema.XmlSchema.Attributes%2A?displayProperty=nameWithType>, <xref:System.Xml.Schema.XmlSchema.SchemaTypes%2A?displayProperty=nameWithType> 등의 PSCI 컬렉션에서는 전역 요소, 특성 및 형식과 해당 PSCI 속성에 직접 액세스할 수 있습니다.

1. <xref:System.Xml.Schema.XmlSchemaObject>가 <xref:System.Xml.Schema.XmlSchemaElement.QualifiedName%2A>이 `"Customer"`인 요소일 경우 `Customer` 클래스를 사용하여 <xref:System.Xml.Schema.XmlSchemaComplexType> 요소의 복합 형식을 얻고 <xref:System.Xml.Schema.XmlSchemaSequence> 클래스를 사용하여 복합 형식의 sequence 파티클을 얻습니다.

2. 스키마 사전 컴파일 <xref:System.Xml.Schema.XmlSchemaParticle> 컬렉션의 각 <xref:System.Xml.Schema.XmlSchemaSequence.Items%2A?displayProperty=nameWithType>를 반복합니다.

3. <xref:System.Xml.Schema.XmlSchemaParticle>이 <xref:System.Xml.Schema.XmlSchemaElement.QualifiedName%2A>이 `"FirstName"`인 요소일 경우 <xref:System.Xml.Schema.XmlSchemaElement.SchemaTypeName%2A> 요소의 `FirstName`을 새 `FirstName` 복합 형식으로 설정합니다.

4. 마지막으로, <xref:System.Xml.Schema.XmlSchema> 클래스의 <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> 및 <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> 메서드를 사용하여 수정된 <xref:System.Xml.Schema.XmlSchemaSet> 개체를 다시 처리하고 컴파일하여 콘솔에 작성합니다.

다음은 전체 코드 예제입니다.

[!code-cpp[XmlSchemaEditExample2#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaEditExample2/CPP/XmlSchemaEditExample2.cpp#1)]
[!code-csharp[XmlSchemaEditExample2#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaEditExample2/CS/XmlSchemaEditExample2.cs#1)]
[!code-vb[XmlSchemaEditExample2#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaEditExample2/VB/XmlSchemaEditExample2.vb#1)]

다음은 [XML 스키마 빌드](../../../../docs/standard/data/xml/building-xml-schemas.md) 항목에서 만든 고객 스키마를 수정한 예제입니다.

```xml
<?xml version="1.0" encoding=" utf-8"?>
<xs:schema xmlns:tns="http://www.tempuri.org" targetNamespace="http://www.tempuri.org" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="Customer">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="FirstName" type="tns:FirstNameComplexType" />
        <xs:element name="LastName" type="tns:LastNameType" />
      </xs:sequence>
      <xs:attribute name="CustomerId" type="xs:positiveInteger" use="required" /
>
    </xs:complexType>
  </xs:element>
  <xs:simpleType name="LastNameType">
    <xs:restriction base="xs:string">
      <xs:maxLength value="20" />
    </xs:restriction>
  </xs:simpleType>
  <xs:complexType name="FirstNameComplexType">     <xs:simpleContent>       <xs:extension base="xs:string">         <xs:attribute name="Title" type="xs:string" />       </xs:extension>     </xs:simpleContent>   </xs:complexType>
</xs:schema>
```

## <a name="see-also"></a>참고 항목

- [XML 스키마 개체 모델 개요](../../../../docs/standard/data/xml/xml-schema-object-model-overview.md)
- [XML 스키마 읽기 및 쓰기](../../../../docs/standard/data/xml/reading-and-writing-xml-schemas.md)
- [XML 스키마 빌드](../../../../docs/standard/data/xml/building-xml-schemas.md)
- [XML 스키마 통과](../../../../docs/standard/data/xml/traversing-xml-schemas.md)
- [XML 스키마 포함하기 또는 가져오기](../../../../docs/standard/data/xml/including-or-importing-xml-schemas.md)
- [스키마 컴파일을 위한 XmlSchemaSet](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)
- [Post-Schema Compilation Infoset](../../../../docs/standard/data/xml/post-schema-compilation-infoset.md)
