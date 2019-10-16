---
title: XML 스키마 포함하기 또는 가져오기
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
ms.assetid: fe1b4a11-37f4-4e1a-93c9-239f4fe736c0
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 45f6b402ae01b7f762f8ef10dcfb0bc46f949db6
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59343573"
---
# <a name="including-or-importing-xml-schemas"></a>XML 스키마 포함하기 또는 가져오기
XML 스키마에 `<xs:import />`, `<xs:include />` 및 `<xs:redefine />` 요소를 포함시킬 수 있습니다. 이 스키마 요소는 이를 포함하거나 가져오는 스키마의 구조를 보완하는 데 사용할 수 있는 다른 XML 스키마를 참조할 수 있습니다. SOM(스키마 개체 모델) API에서 <xref:System.Xml.Schema.XmlSchemaImport>, <xref:System.Xml.Schema.XmlSchemaInclude> 및 <xref:System.Xml.Schema.XmlSchemaRedefine> 클래스는 이러한 요소에 매핑됩니다.  
  
## <a name="including-or-importing-an-xml-schema"></a>XML 스키마 포함하기 또는 가져오기  
 다음 코드 예제는 주소 스키마를 사용하여 [XML 스키마 빌드](../../../../docs/standard/data/xml/building-xml-schemas.md) 항목에서 만든 고객 스키마를 보완합니다. 주소 스키마로 고객 스키마를 보완하면 고객 스키마에서 주소 형식을 사용할 수 있습니다.  
  
 `<xs:include />` 또는 `<xs:import />` 요소를 사용하여 주소 스키마의 구성 요소를 그대로 사용하거나 `<xs:redefine />` 요소를 사용하여 고객 스키마의 필요에 맞게 구성 요소를 수정함으로써 주소 스키마를 통합할 수 있습니다. 주소 스키마에는 고객 스키마에 포함된 것과는 다른 `targetNamespace`가 있기 때문에 `<xs:import />` 요소 및 가져오기 의미 체계가 사용됩니다.  
  
 이 코드 예제에서는 다음과 같은 단계로 주소 스키마를 포함합니다.  
  
1. 고객 스키마 및 주소 스키마를 새 <xref:System.Xml.Schema.XmlSchemaSet> 개체에 추가한 다음 컴파일합니다. 스키마를 읽거나 컴파일할 때 발생하는 모든 스키마 유효성 검사 경고 및 오류는 <xref:System.Xml.Schema.ValidationEventHandler> 대리자에서 처리됩니다.  
  
2. <xref:System.Xml.Schema.XmlSchema> 속성을 반복하여 <xref:System.Xml.Schema.XmlSchemaSet>의 고객 스키마와 주소 스키마에 대해 컴파일된 <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> 개체를 검색합니다. 스키마가 컴파일되므로 PSCI(Post-Schema-Compilation-Infoset) 속성에 액세스할 수 있습니다.  
  
3. <xref:System.Xml.Schema.XmlSchemaImport> 개체를 만들고, 가져오기의 <xref:System.Xml.Schema.XmlSchemaImport.Namespace%2A> 속성을 주소 스키마의 네임스페이스로 설정하고, 가져오기의 <xref:System.Xml.Schema.XmlSchemaExternal.Schema%2A> 속성을 주소 스키마의 <xref:System.Xml.Schema.XmlSchema> 개체로 설정하고, 가져오기를 고객 스키마의 <xref:System.Xml.Schema.XmlSchema.Includes%2A> 속성에 추가합니다.  
  
4. <xref:System.Xml.Schema.XmlSchema> 클래스의 <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> 및 <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> 메서드를 사용하여 고객 스키마의 수정된 <xref:System.Xml.Schema.XmlSchemaSet> 개체를 다시 처리하고 컴파일하여 콘솔에 작성합니다.  
  
5. 마지막으로, 고객 스키마의 <xref:System.Xml.Schema.XmlSchema.Includes%2A> 속성을 사용하여 고객 스키마로 가져온 모든 스키마를 콘솔에 재귀적으로 작성합니다. <xref:System.Xml.Schema.XmlSchema.Includes%2A> 속성에서는 스키마에 포함하거나 가져오거나 다시 정의한 요소에 액세스할 수 있습니다.  
  
 다음은 전체 코드 예제 및 콘솔에 작성된 고객 스키마와 주소 스키마입니다.  
  
 [!code-cpp[XmlSchemaImportExample#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaImportExample/CPP/XmlSchemaImportExample.cpp#1)]
 [!code-csharp[XmlSchemaImportExample#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaImportExample/CS/XmlSchemaImportExample.cs#1)]
 [!code-vb[XmlSchemaImportExample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaImportExample/VB/XmlSchemaImportExample.vb#1)]  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema xmlns:tns="http://www.tempuri.org" targetNamespace="http://www.tempuri.org" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
  <xs:import namespace="http://www.example.com/IPO" />  
  <xs:element name="Customer">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="FirstName" type="xs:string" />  
        <xs:element name="LastName" type="tns:LastNameType" />  
      </xs:sequence>  
      <xs:attribute name="CustomerId" type="xs:positiveInteger" use="required" />  
    </xs:complexType>  
  </xs:element>  
  <xs:simpleType name="LastNameType">  
    <xs:restriction base="xs:string">  
      <xs:maxLength value="20" />  
    </xs:restriction>  
  </xs:simpleType>  
</xs:schema>  
<schema targetNamespace="http://www.example.com/IPO" xmlns="http://www.w3.org/2001/XMLSchema" xmlns:ipo="http://www.example.com/IPO">  
  <annotation>  
    <documentation xml:lang="en">  
      Addresses for International Purchase order schema  
      Copyright 2000 Example.com. All rights reserved.  
    </documentation>  
  </annotation>  
  <complexType name="Address">  
    <sequence>  
      <element name="name"   type="string"/>  
      <element name="street" type="string"/>  
      <element name="city"   type="string"/>  
    </sequence>  
  </complexType>  
  <complexType name="USAddress">  
    <complexContent>  
      <extension base="ipo:Address">  
        <sequence>  
          <element name="state" type="ipo:USState"/>  
          <element name="zip"   type="positiveInteger"/>  
        </sequence>  
      </extension>  
    </complexContent>  
  </complexType>  
  <!-- other Address derivations for more countries or regions -->  
  <simpleType name="USState">  
    <restriction base="string">  
      <enumeration value="AK"/>  
      <enumeration value="AL"/>  
      <enumeration value="AR"/>  
      <!-- and so on ... -->  
    </restriction>  
  </simpleType>  
</schema>  
```  
  
 `<xs:import />`, `<xs:include />` 및 `<xs:redefine />` 요소와 <xref:System.Xml.Schema.XmlSchemaImport>, <xref:System.Xml.Schema.XmlSchemaInclude> 및 <xref:System.Xml.Schema.XmlSchemaRedefine> 클래스에 대한 자세한 내용은 [W3C XML Schema](https://www.w3.org/XML/Schema)(W3C XML 스키마) 및 <xref:System.Xml.Schema?displayProperty=nameWithType> 네임스페이스 클래스 참조 문서를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [XML 스키마 개체 모델 개요](../../../../docs/standard/data/xml/xml-schema-object-model-overview.md)
- [XML 스키마 읽기 및 쓰기](../../../../docs/standard/data/xml/reading-and-writing-xml-schemas.md)
- [XML 스키마 빌드](../../../../docs/standard/data/xml/building-xml-schemas.md)
- [XML 스키마 통과](../../../../docs/standard/data/xml/traversing-xml-schemas.md)
- [XML 스키마 편집](../../../../docs/standard/data/xml/editing-xml-schemas.md)
- [스키마 컴파일을 위한 XmlSchemaSet](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)
