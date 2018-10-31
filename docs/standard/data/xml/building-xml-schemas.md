---
title: XML 스키마 빌드
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
ms.assetid: 8a5ea56c-0140-4b51-8997-875ae6a8e0cb
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 10b2471d13d410826cec3404725117649442297b
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48842621"
---
# <a name="building-xml-schemas"></a>XML 스키마 빌드
<xref:System.Xml.Schema?displayProperty=nameWithType> 네임스페이스의 클래스는 W3C(World Wide Web 컨소시엄) XML 스키마 권장 사항에 정의된 구조에 매핑되며 이 클래스를 사용하여 메모리 내 XML 스키마를 빌드할 수 있습니다.  
  
## <a name="building-an-xml-schema"></a>XML 스키마 빌드  
 다음 코드 예제에서는 SOM API를 사용하여 메모리 내 고객 XML 스키마를 빌드합니다.  
  
### <a name="creating-element-and-attributes"></a>요소 및 특성 만들기  
 이 코드 예제에서는 자식 요소, 특성 및 해당 형식을 먼저 만든 후 최상위 요소를 만들어 상향식으로 고객 스키마를 빌드합니다.  
  
 다음 코드 예제에서는 SOM의 `FirstName` 및 `LastName` 클래스를 사용하여 고객 스키마의 `CustomerId` 특성 외에도 <xref:System.Xml.Schema.XmlSchemaElement> 및 <xref:System.Xml.Schema.XmlSchemaAttribute> 요소를 만듭니다. XML 스키마에서 <xref:System.Xml.Schema.XmlSchemaElement.Name%2A> 및 <xref:System.Xml.Schema.XmlSchemaElement> 요소의 "name" 특성에 해당하는 <xref:System.Xml.Schema.XmlSchemaAttribute> 및 `<xs:element />` 클래스의 `<xs:attribute />` 속성과는 별도로 `defaultValue`, `fixedValue`, `form` 등의 스키마가 허용하는 다른 모든 특성은 <xref:System.Xml.Schema.XmlSchemaElement> 및 <xref:System.Xml.Schema.XmlSchemaAttribute> 클래스에 해당 속성이 있습니다.  
  
 [!code-cpp[XmlSchemaCreateExample#2](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaCreateExample/CPP/XmlSchemaCreateExample.cpp#2)]
 [!code-csharp[XmlSchemaCreateExample#2](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaCreateExample/CS/XmlSchemaCreateExample.cs#2)]
 [!code-vb[XmlSchemaCreateExample#2](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaCreateExample/VB/XmlSchemaCreateExample.vb#2)]  
  
### <a name="creating-schema-types"></a>스키마 형식 만들기  
 요소 및 특성 내용은 해당 형식에 의해 정의됩니다. 기본 제공 스키마 형식 중 하나가 있는 요소 및 특성을 만들려면 <xref:System.Xml.Schema.XmlSchemaElement.SchemaTypeName%2A> 클래스를 사용하는 기본 제공 형식의 정규화된 해당 이름으로 <xref:System.Xml.Schema.XmlSchemaElement> 또는 <xref:System.Xml.Schema.XmlSchemaAttribute> 클래스의 <xref:System.Xml.XmlQualifiedName> 속성을 설정합니다. 요소 및 특성에 대한 사용자 정의 형식을 만들려면 <xref:System.Xml.Schema.XmlSchemaSimpleType> 또는 <xref:System.Xml.Schema.XmlSchemaComplexType> 클래스를 사용하여 새 단순 형식 또는 복합 형식을 만듭니다.  
  
> [!NOTE]
>  요소 또는 특성의 익명 자식으로서 이름이 지정되지 않은 단순 형식 또는 복합 형식을 만들려면(특성에는 단순 형식만 적용됨) <xref:System.Xml.Schema.XmlSchemaElement.SchemaType%2A> 또는 <xref:System.Xml.Schema.XmlSchemaElement> 클래스의 <xref:System.Xml.Schema.XmlSchemaAttribute> 속성 대신 <xref:System.Xml.Schema.XmlSchemaElement.SchemaTypeName%2A> 또는 <xref:System.Xml.Schema.XmlSchemaElement> 클래스의 <xref:System.Xml.Schema.XmlSchemaAttribute> 속성을 이름이 지정되지 않은 단순 형식 또는 복합 형식으로 설정합니다.  
  
 XML 스키마는 다른 단순 형식(기본 제공 또는 사용자 정의)에서 제한에 의해 익명 단순 형식 및 이름이 지정된 단순 형식이 파생되거나 다른 단순 형식의 목록 또는 통합으로 구성되도록 허용합니다. <xref:System.Xml.Schema.XmlSchemaSimpleTypeRestriction> 클래스로 기본 제공 `xs:string` 형식을 제한하여 단순 형식을 만듭니다. 또한 <xref:System.Xml.Schema.XmlSchemaSimpleTypeList> 또는 <xref:System.Xml.Schema.XmlSchemaSimpleTypeUnion> 클래스를 사용하여 list 또는 union 형식을 만들 수 있습니다. <xref:System.Xml.Schema.XmlSchemaSimpleType.Content%2A?displayProperty=nameWithType> 속성은 단순 형식 제한인지 또는 list나 union 형식 제한인지를 나타냅니다.  
  
 다음 코드 예제에서 `FirstName` 요소 형식은 기본 제공 형식 `xs:string`이고, `LastName` 요소 형식은 기본 제공 형식 `xs:string`의 제한인 명명된 단순 형식으로, `MaxLength` 패싯 값이 20이며, `CustomerId` 특성 형식은 기본 제공 형식 `xs:positiveInteger`입니다. `Customer` 요소는 파티클이 `FirstName` 및 `LastName` 요소의 시퀀스이고 특성에 `CustomerId` 특성이 포함된 익명 복합 형식입니다.  
  
> [!NOTE]
>  <xref:System.Xml.Schema.XmlSchemaChoice> 또는 <xref:System.Xml.Schema.XmlSchemaAll> 클래스를 복합 형식의 파티클로 사용하여 `<xs:choice />` 또는 `<xs:all />` 의미 체계를 복제할 수 있습니다.  
  
 [!code-cpp[XmlSchemaCreateExample#3](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaCreateExample/CPP/XmlSchemaCreateExample.cpp#3)]
 [!code-csharp[XmlSchemaCreateExample#3](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaCreateExample/CS/XmlSchemaCreateExample.cs#3)]
 [!code-vb[XmlSchemaCreateExample#3](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaCreateExample/VB/XmlSchemaCreateExample.vb#3)]  
  
### <a name="creating-and-compiling-schemas"></a>스키마 만들기 및 컴파일  
 이때 SOM API를 사용하여 자식 요소와 특성, 해당 형식 및 최상위 `Customer` 요소가 메모리 내에 생성됩니다. 다음 코드 예제에서는 <xref:System.Xml.Schema.XmlSchema> 클래스를 사용하여 스키마 요소를 만들고 <xref:System.Xml.Schema.XmlSchema.Items%2A?displayProperty=nameWithType> 속성을 사용하여 최상위 요소 및 형식을 이 스키마 요소에 추가한 다음 <xref:System.Xml.Schema.XmlSchemaSet> 클래스를 사용하여 전체 스키마를 컴파일하고 콘솔에 작성합니다.  
  
 [!code-cpp[XmlSchemaCreateExample#4](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaCreateExample/CPP/XmlSchemaCreateExample.cpp#4)]
 [!code-csharp[XmlSchemaCreateExample#4](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaCreateExample/CS/XmlSchemaCreateExample.cs#4)]
 [!code-vb[XmlSchemaCreateExample#4](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaCreateExample/VB/XmlSchemaCreateExample.vb#4)]  
  
 <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A?displayProperty=nameWithType> 메서드는 XML 스키마의 규칙에 대해 고객 스키마의 유효성을 검사하고 post-schema-compilation 속성을 사용할 수 있게 합니다.  
  
> [!NOTE]
>  SOM API의 모든 post-schema-compilation 속성은 Post-Schema-Validation-Infoset과 다릅니다.  
  
 <xref:System.Xml.Schema.ValidationEventHandler>에 추가된 <xref:System.Xml.Schema.XmlSchemaSet>는 콜백 메서드 `ValidationCallback`을 호출하여 스키마 유효성 검사 경고 및 오류를 처리하는 대리자입니다.  
  
 다음은 전체 코드 예제 및 콘솔에 작성된 고객 스키마입니다.  
  
 [!code-cpp[XmlSchemaCreateExample#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlSchemaCreateExample/CPP/XmlSchemaCreateExample.cpp#1)]
 [!code-csharp[XmlSchemaCreateExample#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaCreateExample/CS/XmlSchemaCreateExample.cs#1)]
 [!code-vb[XmlSchemaCreateExample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaCreateExample/VB/XmlSchemaCreateExample.vb#1)]  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema xmlns:tns="http://www.tempuri.org" targetNamespace="http://www.tempuri.org" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
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
```  
  
## <a name="see-also"></a>참고 항목

- [XML 스키마 개체 모델 개요](../../../../docs/standard/data/xml/xml-schema-object-model-overview.md)  
- [XML 스키마 읽기 및 쓰기](../../../../docs/standard/data/xml/reading-and-writing-xml-schemas.md)  
- [XML 스키마 통과](../../../../docs/standard/data/xml/traversing-xml-schemas.md)  
- [XML 스키마 편집](../../../../docs/standard/data/xml/editing-xml-schemas.md)  
- [XML 스키마 포함하기 또는 가져오기](../../../../docs/standard/data/xml/including-or-importing-xml-schemas.md)  
- [스키마 컴파일을 위한 XmlSchemaSet](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)  
- [Post-Schema Compilation Infoset](../../../../docs/standard/data/xml/post-schema-compilation-infoset.md)
