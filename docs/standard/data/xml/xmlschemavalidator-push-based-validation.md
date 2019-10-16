---
title: XmlSchemaValidator 밀어넣기 기반 유효성 검사
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 911d4460-dd91-4958-85b2-2ca3299f9ec6
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a420a134eda6c62758b0d218e3c0a4a4922b048c
ms.sourcegitcommit: d7c298f6c2e3aab0c7498bfafc0a0a94ea1fe23e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72250052"
---
# <a name="xmlschemavalidator-push-based-validation"></a>XmlSchemaValidator 밀어넣기 기반 유효성 검사

<xref:System.Xml.Schema.XmlSchemaValidator> 클래스는 밀어넣기 기반 방식으로 XML 스키마에 대해 XML 데이터의 유효성을 검사할 수 있는 효과적인 고성능 메커니즘을 제공합니다. 예를 들어, <xref:System.Xml.Schema.XmlSchemaValidator> 클래스를 사용하면 XML 문서로 serialize한 다음 유효성 검사 XML 판독기를 사용하여 문서를 다시 구문 분석할 필요 없이 내부에서 직접 XML Infoset의 유효성을 검사할 수 있습니다.

사용자 지정 XML 데이터 소스에 대한 유효성 검사 엔진을 만드는 등의 고급 시나리오에서 또는 유효성 검사 XML 작성기를 만드는 방법으로 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스를 사용할 수 있습니다.

다음은 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스를 사용하여 `contosoBooks.xml` 스키마에 대해 `contosoBooks.xsd` 파일의 유효성을 검사하는 예제입니다. 이 예제에서는 <xref:System.Xml.Serialization.XmlSerializer> 클래스를 사용하여 `contosoBooks.xml` 파일을 deserialize하고 노드 값을 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스의 메서드에 전달합니다.

> [!NOTE]
> 이 예제는 이 항목의 전체 단원에서 사용됩니다.

[!code-csharp[XmlSchemaValidatorExamples#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlSchemaValidatorExamples/CS/XmlSchemaValidatorExamples.cs#1)]
[!code-vb[XmlSchemaValidatorExamples#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlSchemaValidatorExamples/VB/XmlSchemaValidatorExamples.vb#1)]

이 예제에서는 `contosoBooks.xml` 파일을 입력으로 사용합니다.

[!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]

이 예제에서는 또한 `contosoBooks.xsd`를 입력으로 사용합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" targetNamespace="http://www.contoso.com/books" xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <xs:element name="bookstore">
        <xs:complexType>
            <xs:sequence>
                <xs:element maxOccurs="unbounded" name="book">
                    <xs:complexType>
                        <xs:sequence>
                            <xs:element name="title" type="xs:string" />
                            <xs:element name="author">
                                <xs:complexType>
                                    <xs:sequence>
                                        <xs:element minOccurs="0" name="name" type="xs:string" />
                                        <xs:element minOccurs="0" name="first-name" type="xs:string" />
                                        <xs:element minOccurs="0" name="last-name" type="xs:string" />
                                    </xs:sequence>
                                </xs:complexType>
                            </xs:element>
                            <xs:element name="price" type="xs:decimal" />
                        </xs:sequence>
                        <xs:attribute name="genre" type="xs:string" use="required" />
                        <xs:attribute name="publicationdate" type="xs:date" use="required" />
                        <xs:attribute name="ISBN" type="xs:string" use="required" />
                    </xs:complexType>
                </xs:element>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema>
```

## <a name="validating-xml-data-using-xmlschemavalidator"></a>XmlSchemaValidator를 사용하여 XML 데이터의 유효성 검사

XML Infoset의 유효성 검사를 시작하려면 먼저 <xref:System.Xml.Schema.XmlSchemaValidator> 생성자를 사용하여 <xref:System.Xml.Schema.XmlSchemaValidator.%23ctor%2A> 클래스의 새 인스턴스를 초기화해야 합니다.

<xref:System.Xml.Schema.XmlSchemaValidator.%23ctor%2A> 생성자는 <xref:System.Xml.XmlNameTable>, <xref:System.Xml.Schema.XmlSchemaSet>, <xref:System.Xml.XmlNamespaceManager> 개체 및 <xref:System.Xml.Schema.XmlSchemaValidationFlags> 값을 매개 변수로 사용합니다. <xref:System.Xml.XmlNameTable> 개체는 스키마 네임스페이스, XML 네임스페이스 등의 잘 알려진 네임스페이스 문자열을 분해하는 데 사용되며 단순 내용의 유효성을 검사하는 동안 <xref:System.Xml.Schema.XmlSchemaDatatype.ParseValue%2A> 메서드에 전달됩니다. <xref:System.Xml.Schema.XmlSchemaSet> 개체에는 XML Infoset의 유효성을 검사하는 데 사용되는 XML 스키마가 포함되어 있습니다. <xref:System.Xml.XmlNamespaceManager> 개체를 사용하여 유효성 검사 중에 나타난 네임스페이스를 확인할 수 있습니다. <xref:System.Xml.Schema.XmlSchemaValidationFlags> 값을 사용하여 특정 유효성 검사 기능을 비활성화할 수 있습니다.

<xref:System.Xml.Schema.XmlSchemaValidator.%23ctor%2A> 생성자에 대한 자세한 내용은 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스 참조 문서를 참조하세요.

### <a name="initializing-validation"></a>유효성 검사 초기화

<xref:System.Xml.Schema.XmlSchemaValidator> 개체를 생성한 후 <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> 개체 상태를 초기화하는 데 사용하는 오버로드된 <xref:System.Xml.Schema.XmlSchemaValidator> 메서드 두 개가 있습니다. 다음은 이 두 <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> 메서드입니다.

- <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A?displayProperty=nameWithType>

- <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A?displayProperty=nameWithType>

기본 <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A?displayProperty=nameWithType> 메서드는 <xref:System.Xml.Schema.XmlSchemaValidator> 개체를 시작 상태로 초기화하며 <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A?displayProperty=nameWithType>를 매개 변수로 사용하는 오버로드된 <xref:System.Xml.Schema.XmlSchemaObject> 메서드는 부분 유효성 검사를 위해 <xref:System.Xml.Schema.XmlSchemaValidator> 개체를 시작 상태로 초기화합니다.

두 <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> 메서드는 <xref:System.Xml.Schema.XmlSchemaValidator> 개체를 생성하거나 <xref:System.Xml.Schema.XmlSchemaValidator.EndValidation%2A>을 호출한 직후에만 호출할 수 있습니다.

<xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A?displayProperty=nameWithType> 메서드의 예제는 소개 단원의 예제를 참조하세요. <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> 메서드에 대한 자세한 내용은 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스 참조 문서를 참조하세요.

#### <a name="partial-validation"></a>부분 유효성 검사

<xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A?displayProperty=nameWithType>를 매개 변수로 사용하는 <xref:System.Xml.Schema.XmlSchemaObject> 메서드는 부분 유효성 검사를 위해 <xref:System.Xml.Schema.XmlSchemaValidator> 개체를 시작 상태로 초기화합니다.

다음 예제에서는 부분 유효성 검사를 위해 <xref:System.Xml.Schema.XmlSchemaObject> 메서드를 사용하여 <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A?displayProperty=nameWithType>를 초기화합니다. `orderNumber` 개체의 <xref:System.Xml.XmlQualifiedName> 속성이 반환하는 <xref:System.Xml.Schema.XmlSchemaObjectTable> 컬렉션에서 <xref:System.Xml.Schema.XmlSchemaSet.GlobalElements%2A>으로 스키마 요소를 선택하여 <xref:System.Xml.Schema.XmlSchemaSet> 스키마 요소를 전달합니다. 그러면 <xref:System.Xml.Schema.XmlSchemaValidator> 개체가 이 특정 요소의 유효성을 검사합니다.

```vb
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet()
schemaSet.Add(Nothing, "schema.xsd")
schemaSet.Compile()
Dim nameTable As NameTable = New NameTable()
Dim manager As XmlNamespaceManager = New XmlNamespaceManager(nameTable)

Dim validator As XmlSchemaValidator = New XmlSchemaValidator(nameTable, schemaSet, manager, XmlSchemaValidationFlags.None)
validator.Initialize(schemaSet.GlobalElements.Item(New XmlQualifiedName("orderNumber")))

validator.ValidateElement("orderNumber", "", Nothing)
validator.ValidateEndOfAttributes(Nothing)
validator.ValidateText("123")
validator.ValidateEndElement(Nothing)
```

```csharp
XmlSchemaSet schemaSet = new XmlSchemaSet();
schemaSet.Add(null, "schema.xsd");
schemaSet.Compile();
NameTable nameTable = new NameTable();
XmlNamespaceManager manager = new XmlNamespaceManager(nameTable);

XmlSchemaValidator validator = new XmlSchemaValidator(nameTable, schemaSet, manager, XmlSchemaValidationFlags.None);
validator.Initialize(schemaSet.GlobalElements[new XmlQualifiedName("orderNumber")]);

validator.ValidateElement("orderNumber", "", null);
validator.ValidateEndOfAttributes(null);
validator.ValidateText("123");
validator.ValidateEndElement(null);
```

이 예제에서는 다음 XML 스키마를 입력으로 사용합니다.

```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="orderNumber" type="xs:int" />
</xs:schema>
```

<xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> 메서드에 대한 자세한 내용은 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스 참조 문서를 참조하세요.

### <a name="adding-additional-schemas"></a>스키마 추가

<xref:System.Xml.Schema.XmlSchemaValidator.AddSchema%2A> 클래스의 <xref:System.Xml.Schema.XmlSchemaValidator> 메서드를 사용하면 유효성 검사 중에 사용되는 스키마 집합에 XML 스키마를 추가할 수 있습니다. <xref:System.Xml.Schema.XmlSchemaValidator.AddSchema%2A> 메서드를 사용하여 유효성을 검사 중인 XML Infoset에서 인라인 XML 스키마가 나타난 결과를 시뮬레이트할 수 있습니다.

> [!NOTE]
> <xref:System.Xml.Schema.XmlSchema> 매개 변수의 대상 네임스페이스는 이미 <xref:System.Xml.Schema.XmlSchemaValidator> 개체에 발생한 요소나 특성의 대상 네임스페이스와 달라야 합니다.
>
> <xref:System.Xml.Schema.XmlSchemaValidationFlags.ProcessInlineSchema?displayProperty=nameWithType> 값을 매개 변수로 <xref:System.Xml.Schema.XmlSchemaValidator.%23ctor%2A> 생성자에 전달하지 않은 경우 <xref:System.Xml.Schema.XmlSchemaValidator.AddSchema%2A> 메서드는 아무 작업도 수행하지 않습니다.

<xref:System.Xml.Schema.XmlSchemaValidator.AddSchema%2A> 메서드의 결과는 유효성을 검사 중인 현재 XML 노드 컨텍스트에 따라 다릅니다. 유효성 검사 컨텍스트에 대한 자세한 내용은 이 항목의 "유효성 검사 컨텍스트" 단원을 참조하세요.

<xref:System.Xml.Schema.XmlSchemaValidator.AddSchema%2A> 메서드에 대한 자세한 내용은 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스 참조 문서를 참조하세요.

### <a name="validating-elements-attributes-and-content"></a>요소, 특성 및 내용 유효성 검사

<xref:System.Xml.Schema.XmlSchemaValidator> 클래스는 XML Infoset에서 XML 스키마에 대해 요소, 특성 및 내용의 유효성을 검사할 수 있는 여러 메서드를 제공합니다. 다음 표에서는 이러한 메서드에 대해 설명합니다.

|메서드|설명|
|------------|-----------------|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateElement%2A>|현재 컨텍스트에서 요소 이름의 유효성을 검사합니다.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>|현재 요소 컨텍스트에서 또는 <xref:System.Xml.Schema.XmlSchemaAttribute> 메서드에 매개 변수로 전달된 <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> 개체에 대해 특성의 유효성을 검사합니다.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndOfAttributes%2A>|요소 컨텍스트에 필수 특성이 모두 있는지 확인하고 <xref:System.Xml.Schema.XmlSchemaValidator> 개체를 준비하여 요소의 자식 내용의 유효성을 검사합니다.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateText%2A>|현재 요소 컨텍스트에서 텍스트가 허용되는지 확인하고 현재 요소에 단순 내용이 있는지 확인하기 위해 텍스트를 누적합니다.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateWhitespace%2A>|현재 요소 컨텍스트에서 공백이 허용되는지 확인하고 현재 요소에 단순 내용이 있는지 확인하기 위해 공백을 누적합니다.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A>|단순 내용이 있는 요소의 데이터 형식에 따라 요소의 텍스트 내용이 유효한지 확인하고 현재 요소의 내용이 복합 내용이 있는 요소에 대해 완전한지 확인합니다.|
|<xref:System.Xml.Schema.XmlSchemaValidator.SkipToEndElement%2A>|현재 요소 내용의 유효성 검사를 생략하고 <xref:System.Xml.Schema.XmlSchemaValidator> 개체를 준비하여 부모 요소의 컨텍스트에서 내용의 유효성을 검사합니다.|
|<xref:System.Xml.Schema.XmlSchemaValidator.EndValidation%2A>|<xref:System.Xml.Schema.XmlSchemaValidationFlags.ProcessIdentityConstraints> 유효성 검사 옵션을 설정한 경우 유효성 검사를 종료하고 전체 XML 문서에 대한 identity 제약 조건을 확인합니다.|

> [!NOTE]
> <xref:System.Xml.Schema.XmlSchemaValidator> 클래스에는 앞의 표에서 설명한 각 메서드의 호출 시퀀스를 실행하고 호출을 발생시키는 상태 전환이 정의되어 있습니다. <xref:System.Xml.Schema.XmlSchemaValidator> 클래스의 특정 상태 전환에 대한 자세한 내용은 이 항목의 "XmlSchemaValidator 상태 전환" 단원을 참조하세요.

XML Infoset에서 요소, 특성 및 내용의 유효성을 검사하는 데 사용되는 메서드의 예는 이전 단원의 예제를 참조하세요. 이러한 메서드에 대한 자세한 내용은 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스 참조 문서를 참조하세요.

#### <a name="validating-content-using-an-xmlvaluegetter"></a>XmlValueGetter를 사용하여 내용 유효성 검사

<xref:System.Xml.Schema.XmlValueGetter>`delegate`를 사용하여 특성, 텍스트 또는 공백 노드의 값을 특성, 텍스트 또는 공백 노드의 XSD(XML 스키마 정의 언어) 형식과 호환되는 CLR(공용 언어 런타임) 형식으로 전달할 수 있습니다. 특성, 텍스트 또는 공백 노드의 CLR 값을 사용할 수 있는 경우 <xref:System.Xml.Schema.XmlValueGetter>`delegate`가 유용하며 `string`으로 변환하고 유효성을 검사하기 위해 다시 구문 분석하는 비용을 줄일 수 있습니다.

<xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>, <xref:System.Xml.Schema.XmlSchemaValidator.ValidateText%2A> 및 <xref:System.Xml.Schema.XmlSchemaValidator.ValidateWhitespace%2A> 메서드가 오버로드되며 특성, 텍스트 또는 공백 노드의 값을 `string` 또는 <xref:System.Xml.Schema.XmlValueGetter>`delegate`로 사용할 수 있도록 허용합니다.

<xref:System.Xml.Schema.XmlSchemaValidator> 클래스의 다음 메서드에서는 <xref:System.Xml.Schema.XmlValueGetter>`delegate`를 매개 변수로 허용합니다.

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateText%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateWhitespace%2A>

다음은 소개 단원의 <xref:System.Xml.Schema.XmlValueGetter> 클래스 예제에서 가져온 `delegate`<xref:System.Xml.Schema.XmlSchemaValidator> 예제입니다. <xref:System.Xml.Schema.XmlValueGetter>`delegate`는 특성 값을 <xref:System.DateTime> 개체로 반환합니다. <xref:System.DateTime>에서 반환된 이 <xref:System.Xml.Schema.XmlValueGetter> 개체의 유효성을 검사하기 위해 <xref:System.Xml.Schema.XmlSchemaValidator> 개체는 먼저 이 개체를 특성의 데이터 형식에 대한 ValueType으로 변환하고 변환된 값에서 패싯을 확인합니다. 여기서 ValueType은 XSD 형식에 대한 기본 CLR 매핑입니다.

```vb
Shared dateTimeGetterContent As Object

Shared Function DateTimeGetterHandle() As Object
    Return dateTimeGetterContent
End Function

Shared Function DateTimeGetter(dateTime As DateTime) As XmlValueGetter
    dateTimeGetterContent = dateTime
    Return New XmlValueGetter(AddressOf DateTimeGetterHandle)
End Function
```

```csharp
static object dateTimeGetterContent;

static object DateTimeGetterHandle()
{
    return dateTimeGetterContent;
}

static XmlValueGetter DateTimeGetter(DateTime dateTime)
{
    dateTimeGetterContent = dateTime;
    return new XmlValueGetter(dateTimeGetterHandle);
}
```

<xref:System.Xml.Schema.XmlValueGetter>`delegate`의 전체 예제는 소개 단원의 예제를 참조하세요. <xref:System.Xml.Schema.XmlValueGetter>`delegate`에 대한 자세한 내용은 <xref:System.Xml.Schema.XmlValueGetter> 및 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스 참조 문서를 참조하세요.

#### <a name="post-schema-validation-information"></a>Post-Schema-Validation-Information

<xref:System.Xml.Schema.XmlSchemaInfo> 클래스는 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스로 유효성을 검사하는 XML 노드의 Post-Schema-Validation-Information을 나타냅니다. <xref:System.Xml.Schema.XmlSchemaValidator> 클래스의 다양한 메서드에서는 <xref:System.Xml.Schema.XmlSchemaInfo> 개체를 선택적(`null`) `out` 매개 변수로 허용합니다.

유효성 검사를 성공적으로 마치면 유효성 검사 결과와 함께 <xref:System.Xml.Schema.XmlSchemaInfo> 개체가 설정됩니다. 예를 들어, <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A> 메서드를 사용하여 특성의 유효성을 검사하면 유효성 검사 결과와 함께 <xref:System.Xml.Schema.XmlSchemaInfo> 개체(지정한 경우)의 <xref:System.Xml.Schema.XmlSchemaInfo.SchemaAttribute%2A>, <xref:System.Xml.Schema.XmlSchemaInfo.SchemaType%2A>, <xref:System.Xml.Schema.XmlSchemaInfo.MemberType%2A> 및 <xref:System.Xml.Schema.XmlSchemaInfo.Validity%2A> 속성이 설정됩니다.

다음 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스 메서드에서는 <xref:System.Xml.Schema.XmlSchemaInfo> 개체를 out 매개 변수로 허용합니다.

- <xref:System.Xml.Schema.XmlSchemaValidator.SkipToEndElement%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateElement%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateElement%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A>

- <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndOfAttributes%2A>

<xref:System.Xml.Schema.XmlSchemaInfo> 클래스의 전체 예제는 소개 단원의 예제를 참조하세요. <xref:System.Xml.Schema.XmlSchemaInfo> 클래스에 대한 자세한 내용은 <xref:System.Xml.Schema.XmlSchemaInfo> 클래스 참조 문서를 참조하세요.

### <a name="retrieving-expected-particles-attributes-and-unspecified-default-attributes"></a>필요한 파티클, 특성 및 지정되지 않은 기본 특성 검색

<xref:System.Xml.Schema.XmlSchemaValidator> 클래스는 현재 유효성 검사 컨텍스트에서 필요한 파티클, 특성 및 지정되지 않은 기본 특성을 검색하는 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>, <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> 및 <xref:System.Xml.Schema.XmlSchemaValidator.GetUnspecifiedDefaultAttributes%2A> 메서드를 제공합니다.

#### <a name="retrieving-expected-particles"></a>필요한 파티클 검색

<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> 메서드는 현재 요소 컨텍스트에서 필요한 파티클이 포함된 <xref:System.Xml.Schema.XmlSchemaParticle> 개체의 배열을 반환합니다. <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> 메서드가 반환할 수 있는 유효한 파티클은 <xref:System.Xml.Schema.XmlSchemaElement> 및 <xref:System.Xml.Schema.XmlSchemaAny> 클래스의 인스턴스입니다.

내용 모델의 compositor가 `xs:sequence`인 경우 시퀀스에서 다음 파티클만 반환됩니다. 내용 모델의 compositor가 `xs:all` 또는 `xs:choice`인 경우 현재 요소 컨텍스트에서 따를 수 있는 유효한 파티클이 모두 반환됩니다.

> [!NOTE]
> <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> 메서드를 호출한 직후에 <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> 메서드를 호출할 경우 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> 메서드는 모든 전역 요소를 반환합니다.

예를 들어, XSD(XML 스키마 정의 언어) 스키마 및 이 스키마를 따르는 XML 문서에서 `book` 요소의 유효성을 검사한 후에는 `book` 요소가 현재 요소 컨텍스트입니다. <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> 메서드는 <xref:System.Xml.Schema.XmlSchemaElement> 요소를 나타내는 단일 `title` 개체가 포함된 배열을 반환합니다. 유효성 검사 컨텍스트가 `title` 요소인 경우 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> 메서드는 빈 배열을 반환합니다. <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> 요소의 유효성을 검사한 후 `title` 요소의 유효성을 검사하기 전에 `description` 메서드를 호출하면 <xref:System.Xml.Schema.XmlSchemaElement> 요소를 나타내는 단일 `description` 개체가 포함된 배열이 반환됩니다. <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> 요소의 유효성을 검사한 후 `description` 메서드를 호출하면 와일드카드를 나타내는 단일 <xref:System.Xml.Schema.XmlSchemaAny> 개체가 포함된 배열이 반환됩니다.

```vb
Dim reader As XmlReader =  XmlReader.Create("input.xml")

Dim schemaSet As New XmlSchemaSet()
schemaSet.Add(Nothing, "schema.xsd")
Dim manager As New XmlNamespaceManager(reader.NameTable)

Dim validator As New XmlSchemaValidator(reader.NameTable,schemaSet,manager,XmlSchemaValidationFlags.None)
validator.Initialize()

validator.ValidateElement("book", "", Nothing)

validator.ValidateEndOfAttributes(Nothing)
For Each element As XmlSchemaElement In validator.GetExpectedParticles()
    Console.WriteLine(element.Name)
Next

validator.ValidateElement("title", "", Nothing)
validator.ValidateEndOfAttributes(Nothing)
For Each element As XmlSchemaElement In validator.GetExpectedParticles()
    Console.WriteLine(element.Name)
Next
validator.ValidateEndElement(Nothing)

For Each element As XmlSchemaElement In validator.GetExpectedParticles()
    Console.WriteLine(element.Name)
Next

validator.ValidateElement("description", "", Nothing)
validator.ValidateEndOfAttributes(Nothing)
validator.ValidateEndElement(Nothing)

For Each particle As XmlSchemaParticle In validator.GetExpectedParticles()
    Console.WriteLine(particle.GetType())
Next

validator.ValidateElement("namespace", "", Nothing)
validator.ValidateEndOfAttributes(Nothing)
validator.ValidateEndElement(Nothing)

validator.ValidateEndElement(Nothing)
```

```csharp
XmlReader reader = XmlReader.Create("input.xml");

var schemaSet = new XmlSchemaSet();
schemaSet.Add(null, "schema.xsd");
var manager = new XmlNamespaceManager(reader.NameTable);

var validator = new XmlSchemaValidator(reader.NameTable, schemaSet, manager, XmlSchemaValidationFlags.None);
validator.Initialize();

validator.ValidateElement("book", "", null);

validator.ValidateEndOfAttributes(null);
foreach (XmlSchemaElement element in validator.GetExpectedParticles())
{
    Console.WriteLine(element.Name);
}

validator.ValidateElement("title", "", null);
validator.ValidateEndOfAttributes(null);
foreach (XmlSchemaElement element in validator.GetExpectedParticles())
{
    Console.WriteLine(element.Name);
}
validator.ValidateEndElement(null);

foreach (XmlSchemaElement element in validator.GetExpectedParticles())
{
    Console.WriteLine(element.Name);
}

validator.ValidateElement("description", "", null);
validator.ValidateEndOfAttributes(null);
validator.ValidateEndElement(null);

foreach (XmlSchemaParticle particle in validator.GetExpectedParticles())
{
    Console.WriteLine(particle.GetType());
}

validator.ValidateElement("namespace", "", null);
validator.ValidateEndOfAttributes(null);
validator.ValidateEndElement(null);

validator.ValidateEndElement(null);
```

 이 예제에서는 다음 XML을 입력으로 사용 합니다.

```xml
<xs:schema xmlns:xs="http://www.w3c.org/2001/XMLSchema">
  <xs:element name="book">
    <xs:sequence>
      <xs:element name="title" type="xs:string" />
      <xs:element name="description" type="xs:string" />
      <xs:any processContent="lax" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:element>
</xs:schema>
```

이 예제에서는 다음 XSD 스키마를 입력으로 사용 합니다.

```xml
<book>
  <title>My Book</title>
  <description>My Book's Description</description>
  <namespace>System.Xml.Schema</namespace>
</book>
```

> [!NOTE]
> <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> 클래스의 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>, <xref:System.Xml.Schema.XmlSchemaValidator.AddSchema%2A> 및 <xref:System.Xml.Schema.XmlSchemaValidator> 메서드로 인한 결과는 유효성 검사가 실행 중인 현재 컨텍스트에 따라 달라집니다. 자세한 내용은 이 항목의 “유효성 검사 컨텍스트” 단원을 참조하세요.

<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> 메서드의 예제는 소개 단원의 예제를 참조하세요. <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> 메서드에 대한 자세한 내용은 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스 참조 문서를 참조하세요.

#### <a name="retrieving-expected-attributes"></a>필요한 특성 검색

<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> 메서드는 현재 요소 컨텍스트에서 필요한 특성이 포함된 <xref:System.Xml.Schema.XmlSchemaAttribute> 개체의 배열을 반환합니다.

예를 들어, 소개 단원의 예제에서는 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> 메서드를 사용하여 `book` 요소의 모든 특성을 검색합니다.

<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> 메서드를 호출한 직후에 <xref:System.Xml.Schema.XmlSchemaValidator.ValidateElement%2A> 메서드를 호출하면 XML 문서에 나타날 수 있는 모든 특성이 반환됩니다. 그러나 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> 메서드를 한 번 이상 호출한 후 <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A> 메서드를 호출하면 현재 요소에 대해 아직 유효성을 검사하지 않은 특성이 반환됩니다.

> [!NOTE]
> <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> 클래스의 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>, <xref:System.Xml.Schema.XmlSchemaValidator.AddSchema%2A> 및 <xref:System.Xml.Schema.XmlSchemaValidator> 메서드로 인한 결과는 유효성 검사가 실행 중인 현재 컨텍스트에 따라 달라집니다. 자세한 내용은 이 항목의 “유효성 검사 컨텍스트” 단원을 참조하세요.

<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> 메서드의 예제는 소개 단원의 예제를 참조하세요. <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> 메서드에 대한 자세한 내용은 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스 참조 문서를 참조하세요.

#### <a name="retrieving-unspecified-default-attributes"></a>지정되지 않은 기본 특성 검색

<xref:System.Xml.Schema.XmlSchemaValidator.GetUnspecifiedDefaultAttributes%2A> 메서드는 요소 컨텍스트에서 <xref:System.Collections.ArrayList> 메서드를 사용하여 기본값의 유효성을 검사하지 않은 특성의 <xref:System.Xml.Schema.XmlSchemaAttribute> 개체로 지정한 <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>를 채웁니다. 요소 컨텍스트의 각 특성에서 <xref:System.Xml.Schema.XmlSchemaValidator.GetUnspecifiedDefaultAttributes%2A> 메서드를 호출한 후에 <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A> 메서드를 호출해야 합니다. 유효성을 검사 중인 XML 문서에 삽입할 기본 특성을 결정하려면 <xref:System.Xml.Schema.XmlSchemaValidator.GetUnspecifiedDefaultAttributes%2A> 메서드를 사용해야 합니다.

<xref:System.Xml.Schema.XmlSchemaValidator.GetUnspecifiedDefaultAttributes%2A> 메서드에 대한 자세한 내용은 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스 참조 문서를 참조하세요.

### <a name="handling-schema-validation-events"></a>스키마 유효성 검사 이벤트 처리

유효성을 검사하는 동안 발생한 스키마 유효성 검사 경고 및 오류는 <xref:System.Xml.Schema.XmlSchemaValidator.ValidationEventHandler> 클래스의 <xref:System.Xml.Schema.XmlSchemaValidator> 이벤트로 처리됩니다.

스키마 유효성 검사 경고의 <xref:System.Xml.Schema.XmlSeverityType> 값은 <xref:System.Xml.Schema.XmlSeverityType.Warning>이며 스키마 유효성 검사 오류의 <xref:System.Xml.Schema.XmlSeverityType> 값은 <xref:System.Xml.Schema.XmlSeverityType.Error>입니다. <xref:System.Xml.Schema.XmlSchemaValidator.ValidationEventHandler>를 지정하지 않으면 <xref:System.Xml.Schema.XmlSchemaValidationException> 값이 <xref:System.Xml.Schema.XmlSeverityType>인 모든 스키마 유효성 검사 오류에 대해 <xref:System.Xml.Schema.XmlSeverityType.Error>이 throw됩니다. 그러나 <xref:System.Xml.Schema.XmlSchemaValidationException> 값이 <xref:System.Xml.Schema.XmlSeverityType>인 스키마 유효성 검사 경고에 대해서는 <xref:System.Xml.Schema.XmlSeverityType.Warning>이 throw되지 않습니다.

다음은 소개 단원의 예제에서 가져온 것으로, 스키마 유효성 검사 중에 발생한 스키마 유효성 검사 경고 및 오류를 받는 <xref:System.Xml.Schema.ValidationEventHandler>의 예제입니다.

```vb
Shared Sub SchemaValidationEventHandler(sender As Object, e As ValidationEventArgs)

    Select Case e.Severity
        Case XmlSeverityType.Error
            Console.WriteLine(vbCrLf & "Error: {0}", e.Message)
            Exit Sub
        Case XmlSeverityType.Warning
            Console.WriteLine(vbCrLf & "Warning: {0}", e.Message)
            Exit Sub
    End Select
End Sub
```

```csharp
static void SchemaValidationEventHandler(object sender, ValidationEventArgs e)
{
    switch (e.Severity)
    {
        case XmlSeverityType.Error:
            Console.WriteLine("\nError: {0}", e.Message);
            break;
        case XmlSeverityType.Warning:
            Console.WriteLine("\nWarning: {0}", e.Message);
            break;
    }
}
```

<xref:System.Xml.Schema.ValidationEventHandler>의 전체 예제는 소개 단원의 예제를 참조하세요. 자세한 내용은 <xref:System.Xml.Schema.XmlSchemaInfo> 클래스 참조 문서를 참조하세요.

## <a name="xmlschemavalidator-state-transition"></a>XmlSchemaValidator 상태 전환

<xref:System.Xml.Schema.XmlSchemaValidator> 클래스에는 XML Infoset에서 요소, 특성 및 내용의 유효성을 검사하는 데 사용되는 각 메서드의 호출 시퀀스를 실행하고 호출을 발생시키는 상태 전환이 정의되어 있습니다.

다음 표에서는 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스의 상태 전환 및 각 상태에서 수행할 수 있는 메서드 호출의 시퀀스와 발생에 대해 설명합니다.

|State|전환|
|-----------|----------------|
|유효성 검사|<xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> (<xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A> &#124; TopLevel*) <xref:System.Xml.Schema.XmlSchemaValidator.EndValidation%2A>|
|TopLevel|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateWhitespace%2A> &#124; <xref:System.Xml.Schema.XmlSchemaValidator.ValidateText%2A> &#124; 요소|
|요소|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateElement%2A> <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>* (<xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndOfAttributes%2A> Content\*)? <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A> &#124;<br /><br /> <xref:System.Xml.Schema.XmlSchemaValidator.ValidateElement%2A> <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>\* <xref:System.Xml.Schema.XmlSchemaValidator.SkipToEndElement%2A> &#124;<br /><br /> <xref:System.Xml.Schema.XmlSchemaValidator.ValidateElement%2A> <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>\* <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndOfAttributes%2A> Content\* <xref:System.Xml.Schema.XmlSchemaValidator.SkipToEndElement%2A> &#124;|
|콘텐츠|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateWhitespace%2A> &#124; <xref:System.Xml.Schema.XmlSchemaValidator.ValidateText%2A> &#124; 요소|

> [!NOTE]
> 위 표에서 <xref:System.InvalidOperationException> 개체의 현재 상태에 따라 잘못된 시퀀스에서 메서드를 호출하면 각 메서드에 의해 <xref:System.Xml.Schema.XmlSchemaValidator>이 throw됩니다.

위의 상태 전환 표에서는 문장 부호를 사용하여 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스 상태 전환의 각 상태에 대해 호출할 수 있는 메서드와 기타 상태를 설명합니다. 사용된 문장 부호는 DTD(문서 종류 정의)에 대한 XML 표준 참조의 문장 부호와 같습니다.

다음 표에서는 위의 상태 전환 표에 나타난 문장 부호가 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스 상태 전환의 각 상태에 대해 호출할 수 있는 메서드와 기타 상태에 미치는 영향을 설명합니다.

|Symbol|설명|
|------------|-----------------|
|&#124;|세로 막대 앞이나 뒤의 메서드 또는 상태를 호출할 수 있습니다.|
|?|물음표 앞의 메서드나 상태는 선택 항목이지만 이 메서드나 상태를 호출할 경우에는 한 번만 호출할 수 있습니다.|
|*|\* 기호 앞의 메서드나 상태는 선택 항목이며 두 번 이상 호출할 수 있습니다.|

## <a name="validation-context"></a>유효성 검사 컨텍스트

XML Infoset에서 요소, 특성 및 내용의 유효성을 검사하는 데 사용하는 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스의 메서드는 <xref:System.Xml.Schema.XmlSchemaValidator> 개체의 유효성 검사 컨텍스트를 변경합니다. 예를 들어, <xref:System.Xml.Schema.XmlSchemaValidator.SkipToEndElement%2A> 메서드는 현재 요소 내용의 유효성 검사를 생략하고 <xref:System.Xml.Schema.XmlSchemaValidator> 개체를 준비하여 부모 요소의 컨텍스트에서 내용의 유효성을 검사합니다. 이 동작은 현재 요소의 모든 자식에 대한 유효성 검사를 생략하고 <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A> 메서드를 호출하는 것과 같습니다.

<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> 클래스의 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>, <xref:System.Xml.Schema.XmlSchemaValidator.AddSchema%2A> 및 <xref:System.Xml.Schema.XmlSchemaValidator> 메서드로 인한 결과는 유효성 검사가 실행 중인 현재 컨텍스트에 따라 달라집니다.

이 표에서는 XML Infoset에서 요소, 특성 및 내용의 유효성을 검사하는 데 사용하는 <xref:System.Xml.Schema.XmlSchemaValidator> 클래스의 메서드 중 하나를 호출한 후 이러한 메서드를 호출한 결과를 설명합니다.

|메서드|GetExpectedParticles|GetExpectedAttributes|AddSchema|
|------------|--------------------------|---------------------------|---------------|
|<xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A>|기본 <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> 메서드를 호출할 경우 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>는 모든 전역 요소가 포함된 배열을 반환합니다.<br /><br /> <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A>를 매개 변수로 사용하는 오버로드된 <xref:System.Xml.Schema.XmlSchemaObject> 메서드를 호출하여 요소의 부분 유효성 검사를 초기화하는 경우 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>는 <xref:System.Xml.Schema.XmlSchemaValidator> 개체가 초기화된 요소만 반환합니다.|기본 <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A> 메서드를 호출할 경우 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>는 빈 배열을 반환합니다.<br /><br /> <xref:System.Xml.Schema.XmlSchemaValidator.Initialize%2A>를 매개 변수로 사용하는 오버로드된 <xref:System.Xml.Schema.XmlSchemaObject> 메서드를 호출하여 특성의 부분 유효성 검사를 초기화하는 경우 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>는 <xref:System.Xml.Schema.XmlSchemaValidator> 개체가 초기화된 특성만 반환합니다.|전처리 오류가 없을 경우 <xref:System.Xml.Schema.XmlSchemaSet> 개체의 <xref:System.Xml.Schema.XmlSchemaValidator>에 스키마를 추가합니다.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateElement%2A>|컨텍스트 요소가 유효한 경우 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>는 컨텍스트 요소 자식으로 필요한 요소의 시퀀스를 반환합니다.<br /><br /> 컨텍스트 요소가 잘못되었으면 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>가 빈 배열을 반환합니다.|컨텍스트 요소가 유효하고 이전에 <xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>를 호출하지 않은 경우 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>는 컨텍스트 요소에 정의된 모든 특성의 목록을 반환합니다.<br /><br /> 일부 특성의 유효성을 이미 확인한 경우 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>는 유효성을 검사할 나머지 특성의 목록을 반환합니다.<br /><br /> 컨텍스트 요소가 잘못되었으면 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>가 빈 배열을 반환합니다.|위와 동일합니다.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateAttribute%2A>|컨텍스트 특성이 최상위 특성이면 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>가 빈 배열을 반환합니다.<br /><br /> 그렇지 않으면 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>는 컨텍스트 요소의 첫 번째 자식으로 필요한 요소의 시퀀스를 반환합니다.|컨텍스트 특성이 최상위 특성이면 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>가 빈 배열을 반환합니다.<br /><br /> 그렇지 않으면 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>는 유효성을 검사할 나머지 특성의 목록을 반환합니다.|위와 동일합니다.|
|<xref:System.Xml.Schema.XmlSchemaValidator.GetUnspecifiedDefaultAttributes%2A>|<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>는 컨텍스트 요소의 첫 번째 자식으로 필요한 요소의 시퀀스를 반환합니다.|<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>는 컨텍스트 요소에 대해 유효성을 검사할 필수 특성 및 선택적 특성의 목록을 반환합니다.|위와 동일합니다.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndOfAttributes%2A>|<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>는 컨텍스트 요소의 첫 번째 자식으로 필요한 요소의 시퀀스를 반환합니다.|<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>는 빈 배열을 반환합니다.|위와 동일합니다.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateText%2A>|컨텍스트 요소의 contentType이 Mixed인 경우 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>는 다음 위치에 필요한 요소의 시퀀스를 반환합니다.<br /><br /> 컨텍스트 요소의 contentType이 TextOnly 또는 Empty인 경우 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>는 빈 배열을 반환합니다.<br /><br /> 컨텍스트 요소의 contentType이 ElementOnly인 경우 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>는 다음 위치에 필요한 요소의 시퀀스를 반환하지만 유효성 검사 오류가 발생합니다.|<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>는 특성의 유효성이 검사되지 않은 컨텍스트 요소의 목록을 반환합니다.|위와 동일합니다.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateWhitespace%2A>|컨텍스트 공백이 최상위 공백이면 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>가 빈 배열을 반환합니다.<br /><br /> 그렇지 않으면 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A> 메서드의 동작이 <xref:System.Xml.Schema.XmlSchemaValidator.ValidateText%2A>와 동일하게 됩니다.|컨텍스트 공백이 최상위 공백이면 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>가 빈 배열을 반환합니다.<br /><br /> 그렇지 않으면 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A> 메서드의 동작이 <xref:System.Xml.Schema.XmlSchemaValidator.ValidateText%2A>와 동일하게 됩니다.|위와 동일합니다.|
|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A>|<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedParticles%2A>는 컨텍스트 요소(가능한 형제) 뒤에 필요한 요소의 시퀀스를 반환합니다.|<xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>는 특성의 유효성이 검사되지 않은 컨텍스트 요소의 목록을 반환합니다.<br /><br /> 컨텍스트 요소에 부모가 없을 경우 <xref:System.Xml.Schema.XmlSchemaValidator.GetExpectedAttributes%2A>는 빈 목록을 반환합니다. 컨텍스트 요소는 <xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A>가 호출된 현재 요소의 부모입니다.|위와 동일합니다.|
|<xref:System.Xml.Schema.XmlSchemaValidator.SkipToEndElement%2A>|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A>와 같습니다.|<xref:System.Xml.Schema.XmlSchemaValidator.ValidateEndElement%2A>와 같습니다.|위와 동일합니다.|
|<xref:System.Xml.Schema.XmlSchemaValidator.EndValidation%2A>|빈 배열을 반환합니다.|빈 배열을 반환합니다.|위와 동일합니다.|

> [!NOTE]
> <xref:System.Xml.Schema.XmlSchemaValidator> 클래스의 다양한 속성이 반환하는 값은 위 표의 메서드를 호출해도 변경되지 않습니다.

## <a name="see-also"></a>참조

- <xref:System.Xml.Schema.XmlSchemaValidator>
