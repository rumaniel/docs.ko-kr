---
title: XmlSerializer 클래스 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XmlSerializer [WCF], using
ms.assetid: c680602d-39d3-44f1-bf22-8e6654ad5069
ms.openlocfilehash: 07c0df0cfb40e8c75532b73f133e32dcb369a3ec
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045205"
---
# <a name="using-the-xmlserializer-class"></a>XmlSerializer 클래스 사용

WCF (Windows Communication Foundation)에서는 두 가지 serialization 기술을 사용 하 여 응용 프로그램의 데이터를 클라이언트와 서비스 간에 전송 되는 XML로 변환할 수 있습니다 .이 프로세스를 serialization 이라고 합니다.

## <a name="datacontractserializer-as-the-default"></a>기본값인 DataContractSerializer

기본적으로 WCF는 클래스 <xref:System.Runtime.Serialization.DataContractSerializer> 를 사용 하 여 데이터 형식을 serialize 합니다. 이 serializer는 다음 형식을 지원합니다.

- 기본 형식(예: 정수, 문자열 및 바이트 배열) 및 기본 형식으로 처리되는 <xref:System.Xml.XmlElement> 및 <xref:System.DateTime> 같은 일부 특수 형식

- 데이터 계약 형식(<xref:System.Runtime.Serialization.DataContractAttribute> 특성으로 표시된 형식)

- <xref:System.SerializableAttribute> 인터페이스를 구현하는 형식을 포함하여 <xref:System.Runtime.Serialization.ISerializable> 특성으로 표시된 형식

- <xref:System.Xml.Serialization.IXmlSerializable> 인터페이스를 구현하는 형식

- 많은 제네릭 컬렉션 형식을 비롯한 많은 일반 컬렉션 형식

많은 .NET Framework 형식이 후자의 두 범주에 해당 하므로 serialize 할 수 있습니다. serialize할 수 있는 형식의 배열도 serialize할 수 있습니다. 전체 목록은 [서비스 계약에서 데이터 전송 지정](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)을 참조 하세요.

데이터 <xref:System.Runtime.Serialization.DataContractSerializer>계약 형식과 함께 사용 되는는 새 WCF 서비스를 작성 하는 데 권장 되는 방법입니다. 자세한 내용은 [데이터 계약 사용](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)을 참조 하세요.

## <a name="when-to-use-the-xmlserializer-class"></a>XmlSerializer 클래스 사용 시기

WCF는 <xref:System.Xml.Serialization.XmlSerializer> 클래스도 지원 합니다. 클래스 <xref:System.Xml.Serialization.XmlSerializer> 는 WCF에 고유 하지 않습니다. ASP.NET 웹 서비스에서 사용 하는 것과 동일한 serialization 엔진입니다. <xref:System.Xml.Serialization.XmlSerializer> 클래스는 <xref:System.Runtime.Serialization.DataContractSerializer> 클래스보다 훨씬 더 제한된 형식 집합을 지원하지만 결과 XML을 보다 강력하게 제어할 수 있으며 XSD(XML 스키마 정의 언어) 표준의 더 많은 부분을 지원합니다. 또한 이 클래스에는 serialize할 수 있는 형식의 선언적 특성이 필요 없습니다. 자세한 내용은 .NET Framework 설명서의 XML Serialization 항목을 참조 하십시오. <xref:System.Xml.Serialization.XmlSerializer> 클래스는 데이터 계약 형식을 지원하지 않습니다.

Visual Studio에서 Svcutil.exe 또는 **서비스 참조 추가** 기능을 사용 하 여 타사 서비스에 대 한 클라이언트 코드를 생성 하거나 타사 스키마에 액세스 하는 경우 적절 한 serializer가 자동으로 선택 됩니다. 스키마가 <xref:System.Runtime.Serialization.DataContractSerializer>와 호환되지 않으면 <xref:System.Xml.Serialization.XmlSerializer>가 선택됩니다.

## <a name="manually-switching-to-the-xmlserializer"></a>XmlSerializer로 수동 전환

경우에 따라 수동으로 <xref:System.Xml.Serialization.XmlSerializer>로 전환해야 할 수도 있습니다. 예를 들어 다음과 같은 경우 수동 전환할 수 있습니다.

- ASP.NET 웹 서비스에서 WCF로 응용 프로그램을 마이그레이션할 때 새 데이터 계약 형식을 생성 하는 <xref:System.Xml.Serialization.XmlSerializer>대신 기존의 호환 형식을 다시 사용할 수 있습니다.

- 메시지에 표시되는 XML에 대한 정확한 제어가 중요하지만 WSDL(웹 서비스 기술 언어) 문서를 사용할 수 없는 경우(예: DataContractSerializer와 호환되지 않는 특정 표준화 및 게시된 스키마를 준수해야 하는 형식의 서비스를 만드는 경우)

- 레거시 SOAP 인코딩 표준을 따르는 서비스를 만드는 경우

위의 경우를 비롯한 여러 경우에서 다음 코드와 같이 <xref:System.Xml.Serialization.XmlSerializer> 특성을 서비스에 적용하여 `XmlSerializerFormatAttribute` 클래스로 수동 전환할 수 있습니다.

[!code-csharp[c_XmlSerializer#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_xmlserializer/cs/source.cs#1)]
[!code-vb[c_XmlSerializer#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_xmlserializer/vb/source.vb#1)]

## <a name="security-considerations"></a>보안 고려 사항

> [!NOTE]
> serialization 엔진을 전환할 때는 주의해야 합니다. 사용하는 serializer에 따라 같은 형식이 XML로 다르게 serialize될 수 있습니다. 실수로 잘못된 serializer를 사용하면 공개하려 하지 않았던 형식의 정보를 공개하게 될 수 있습니다.

예를 들어 <xref:System.Runtime.Serialization.DataContractSerializer> 클래스는 데이터 계약 형식을 serialize할 때 <xref:System.Runtime.Serialization.DataMemberAttribute> 특성으로 표시된 멤버만 serialize하고, <xref:System.Xml.Serialization.XmlSerializer> 클래스는 모든 public 멤버를 serialize합니다. 다음 코드의 형식을 참조하세요.

[!code-csharp[c_XmlSerializer#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_xmlserializer/cs/source.cs#2)]
[!code-vb[c_XmlSerializer#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_xmlserializer/vb/source.vb#2)]

<xref:System.Xml.Serialization.XmlSerializer> 클래스가 선택된 서비스 계약에 실수로 이러한 형식을 사용하면 의도하지 않게 `creditCardNumber` 멤버가 serialize됩니다.

<xref:System.Runtime.Serialization.DataContractSerializer> 클래스는 기본값이지만 <xref:System.ServiceModel.DataContractFormatAttribute> 특성을 서비스 계약 형식에 적용하여 서비스에 대해 명시적으로 이 클래스를 선택할 수 있습니다. 그러나 실제로 이렇게 해야 하는 경우는 없습니다.

서비스에 사용되는 serializer는 계약에서 없어서는 안 될 부분이며 다른 바인딩을 선택하거나 기타 구성 설정을 바꿔서 변경할 수 없습니다.

<xref:System.Xml.Serialization.XmlSerializer> 클래스에 적용되는 다른 중요한 보안 고려 사항은 다음과 같습니다. 먼저 <xref:System.Xml.Serialization.XmlSerializer> 클래스를 사용 하는 모든 WCF 응용 프로그램은 공개에서 보호 키로 서명 하는 것이 좋습니다. 이 권장 사항은 <xref:System.Xml.Serialization.XmlSerializer>로 수동 전환을 수행할 때와 Svcutil.exe, 서비스 참조 추가 또는 유사한 도구를 사용하여 자동 전환을 수행할 때 모두 적용됩니다. 이는 <xref:System.Xml.Serialization.XmlSerializer> serialization 엔진이 응용 프로그램과 동일한 키로 서명 된 경우 *미리 생성 된 serialization 어셈블리* 를 로드 하는 것을 지원 하기 때문입니다. 애플리케이션에 서명이 없으면 미리 생성된 serialization 어셈블리의 예상 이름과 일치하는 악성 어셈블리가 애플리케이션 폴더나 전역 어셈블리 캐시에 배치될 수 있습니다. 물론 공격자가 악성 어셈블리를 이용하려면 먼저 두 위치 중 하나에 대한 쓰기 권한을 얻어야 합니다.

<xref:System.Xml.Serialization.XmlSerializer>를 사용할 때마다 나타나는 또 다른 위협은 시스템 임시 폴더에 대한 쓰기 권한과 관련이 있습니다. Serialization <xref:System.Xml.Serialization.XmlSerializer> 엔진은이 폴더에 임시 *serialization 어셈블리* 를 만들고 사용 합니다. 시스템 임시 폴더에 대한 쓰기 권한이 있는 모든 프로세스에서 이러한 serialization 어셈블리를 악성 코드로 덮어쓸 수 있음에 유의해야 합니다.

## <a name="rules-for-xmlserializer-support"></a>XmlSerializer 지원에 대한 규칙

<xref:System.Xml.Serialization.XmlSerializer> 호환 특성을 계약 작업 매개 변수나 반환 값에 직접 적용할 수 없지만, 다음 코드와 같이 형식화된 메시지(메시지 계약 본문 부분)에 적용할 수는 있습니다.

[!code-csharp[c_XmlSerializer#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_xmlserializer/cs/source.cs#3)]
[!code-vb[c_XmlSerializer#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_xmlserializer/vb/source.vb#3)]

이러한 특성을 형식화된 메시지 멤버에 적용하면 메시지 특성에서 충돌하는 속성이 재정의됩니다. 예를 들어 다음 코드에서 `ElementName`은 `Name`을 재정의합니다.

[!code-csharp[c_XmlSerializer#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_xmlserializer/cs/source.cs#4)]
[!code-vb[c_XmlSerializer#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_xmlserializer/vb/source.vb#4)]

<xref:System.ServiceModel.MessageHeaderArrayAttribute> 특성은 <xref:System.Xml.Serialization.XmlSerializer>를 사용할 때 지원되지 않습니다.

> [!NOTE]
> 이 경우는 <xref:System.Xml.Serialization.XmlSerializer> WCF 이전에 릴리스된 다음과 같은 예외를 throw 합니다. "스키마의 최상위 수준에서 선언 된 요소에는 > 1 `maxOccurs` 을 사용할 수 없습니다. `XmlArray` 대신 `XmlArrayItem` 또는 `XmlElementAttribute`을 사용하거나 Wrapper 매개 변수 스타일을 사용하여 ‘more’에 래퍼 요소를 제공하세요." 오류를 throw합니다.
>
> 이러한 예외가 표시되면 이 경우에 해당하는지 확인하세요.

WCF는 메시지 계약 및 <xref:System.Xml.Serialization.SoapIncludeAttribute> 작업 <xref:System.Xml.Serialization.XmlIncludeAttribute> 계약에서 및 특성을 지원 하지 않습니다. 대신 <xref:System.Runtime.Serialization.KnownTypeAttribute> 특성을 사용 하십시오.

## <a name="types-that-implement-the-ixmlserializable-interface"></a>IXmlSerializable 인터페이스를 구현하는 형식

`IXmlSerializable` 인터페이스를 구현하는 형식은 `DataContractSerializer`에서 완전히 지원됩니다. 이러한 형식의 스키마를 제어하려면 <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> 특성을 항상 이러한 형식에 적용해야 합니다.

> [!WARNING]
> 다형 형식을 serialize하는 경우에는 올바른 형식이 serialize되도록 <xref:System.Xml.Serialization.XmlSchemaProviderAttribute>를 형식에 적용해야 합니다.

`IXmlSerializable`을 구현하는 형식에는 임의의 콘텐츠를 나타내는 형식, 단일 요소를 나타내는 형식 및 레거시 <xref:System.Data.DataSet> 형식 등 세 가지가 있습니다.

- 콘텐츠 형식은 `XmlSchemaProviderAttribute` 특성에 지정된 스키마 공급자 메서드를 사용합니다. 이 메서드는 `null`을 반환하지 않으며 특성의 <xref:System.Xml.Serialization.XmlSchemaProviderAttribute.IsAny%2A> 속성은 기본값인 `false`로 유지됩니다. 이는 `IXmlSerializable` 형식의 가장 일반적인 사용입니다.

- 요소 형식은 `IXmlSerializable` 형식이 루트 요소 이름을 제어해야 하는 경우에 사용됩니다. 형식을 요소 형식으로 표시하려면 <xref:System.Xml.Serialization.XmlSchemaProviderAttribute.IsAny%2A> 특성의 <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> 속성을 `true`로 설정하거나 스키마 공급자 메서드에서 `null`을 반환합니다. 스키마 공급자 메서드 사용은 요소 형식의 옵션이며 `null`에 메서드 이름 대신 `XmlSchemaProviderAttribute`을 지정할 수 있습니다. 그러나 `IsAny`가 `true`이고 스키마 공급자 메서드가 지정된 경우 메서드는 `null`을 반환해야 합니다.

- 레거시 <xref:System.Data.DataSet> 형식은 `IXmlSerializable` 특성으로 표시되지 않은 `XmlSchemaProviderAttribute` 형식입니다. 대신 이러한 형식은 스키마 생성 시 <xref:System.Xml.Serialization.IXmlSerializable.GetSchema%2A> 메서드를 사용합니다. 이 패턴은 `DataSet` 형식에 사용되고 해당 형식화된 데이터 세트은 이전 버전의 .NET Framework에서는 클래스를 파생하지만 현재는 더 이상 사용되지 않으며 레거시 용도로만 지원됩니다. 이 패턴을 사용하는 대신 `XmlSchemaProviderAttribute`를 항상 `IXmlSerializable` 형식에 적용하세요.

### <a name="ixmlserializable-content-types"></a>IXmlSerializable 콘텐츠 형식

이전에 정의한 콘텐츠 형식이며 `IXmlSerializable`을 구현하는 형식의 데이터 멤버를 serialize할 때 serializer는 데이터 멤버의 래퍼 요소를 쓰고 제어를 <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> 메서드에 전달합니다. <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> 구현은 특성을 래퍼 요소에 추가하는 것을 포함하여 모든 XML을 쓸 수 있습니다. `WriteXml`이 완료되면 serializer는 요소를 닫습니다.

이전에 정의한 콘텐츠 형식이며 `IXmlSerializable`을 구현하는 형식의 데이터 멤버를 deserialize할 때 deserializer는 데이터 멤버의 래퍼 요소에 XML 판독기를 배치하고 제어를 <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> 메서드에 전달합니다. 메서드는 시작 및 끝 태그를 비롯하여 전체 요소를 읽어야 합니다. `ReadXml` 코드는 요소가 비어 있는 경우를 처리해야 합니다. 또한 `ReadXml` 구현은 래퍼 요소의 이름이 특정한 방식으로 지정되는 데 의존해서는 안 됩니다. serializer에서 선택되는 이름은 다양할 수 있습니다.

`IXmlSerializable` 형식의 데이터 멤버 등에 다형적으로 <xref:System.Object> 콘텐츠 형식을 할당할 수 있습니다. 또한 형식 인스턴스는 null일 수 있습니다. 마지막으로 개체 그래프 유지가 활성화된 상태 및 `IXmlSerializable`로 <xref:System.Runtime.Serialization.NetDataContractSerializer>을 사용할 수 있습니다. 이러한 모든 기능을 통해 WCF serializer는 특정 특성을 래퍼 요소 ("nil" 및 "type"의 XML 스키마 인스턴스 네임 스페이스 및 "Id", "Ref", "Type" 및 "Assembly")에 연결 해야 합니다.

#### <a name="attributes-to-ignore-when-implementing-readxml"></a>ReadXml을 구현할 때 무시할 특성

제어를 `ReadXml` 코드에 전달하기 전에 deserializer는 XML 요소를 검사하고 이러한 특수 XML 특성을 검색하여 작업을 수행합니다. 예를 들어 "nil"이 `true`이면 null 값이 deserialize되고 `ReadXml`은 호출되지 않습니다. 다형성이 검색되면 요소의 콘텐츠가 다른 형식인 것처럼 deserialize됩니다. 다형적으로 할당된 형식의 `ReadXml` 구현이 호출됩니다. 어떤 경우에든 이러한 특수 특성은 deserializer에 의해 처리되므로 `ReadXml` 구현에서는 해당 특수 특성을 무시해야 합니다.

### <a name="schema-considerations-for-ixmlserializable-content-types"></a>IXmlSerializable 콘텐츠 형식의 스키마 고려 사항

스키마와 `IXmlSerializable` 콘텐츠 형식을 내보내면 스키마 공급자 메서드가 호출됩니다. <xref:System.Xml.Schema.XmlSchemaSet>가 스키마 공급자 메서드로 전달됩니다. 메서드는 유효한 스키마를 모두 스키마 집합에 추가할 수 있습니다. 스키마 집합에는 스키마를 내보낼 때 이미 알려진 스키마가 포함됩니다. 스키마 공급자 메서드는 스키마 집합에 항목을 추가해야 하는 경우 해당 네임스페이스를 가진 <xref:System.Xml.Schema.XmlSchema>가 집합에 이미 있는지 확인해야 합니다. 이미 있으면 스키마 공급자 메서드는 기존 `XmlSchema`에 새 항목을 추가해야 합니다. 없는 경우에는 새 `XmlSchema` 인스턴스를 만들어야 합니다. 이 기능은 `IXmlSerializable` 형식의 배열을 사용하는 경우에 중요합니다. 예를 들어 "B" 네임스페이스에 "A" 형식으로 내보내지는 `IXmlSerializable` 형식이 있는 경우 스키마 공급자 메서드가 호출될 때까지 스키마 집합에 "ArrayOfA" 형식을 보유할 "B"의 스키마가 이미 포함될 수 있습니다.

<xref:System.Xml.Schema.XmlSchemaSet>에 형식을 추가하는 것 외에 콘텐츠 형식의 스키마 공급자 메서드는 null이 아닌 값을 반환해야 합니다. 이 메서드는 지정된 <xref:System.Xml.XmlQualifiedName> 형식에 사용할 스키마 형식의 이름을 지정하는 `IXmlSerializable`을 반환할 수 있습니다. 이 정규화된 이름은 형식의 데이터 계약 이름과 네임스페이스로도 사용됩니다. 스키마 공급자 메서드가 반환될 때 즉시 스키마 집합에 없는 형식을 반환할 수 있습니다. 그러나 관련된 모든 형식을 내보낼 때까지, 즉 <xref:System.Runtime.Serialization.XsdDataContractExporter.Export%2A>의 모든 관련 형식에 대해 <xref:System.Runtime.Serialization.XsdDataContractExporter> 메서드가 호출되고 <xref:System.Runtime.Serialization.XsdDataContractExporter.Schemas%2A> 속성에 액세스할 때까지 형식은 스키마 집합에 있습니다. 관련된 `Schemas` 호출을 수행하기 전에 `Export` 속성에 액세스하면 <xref:System.Xml.Schema.XmlSchemaException>이 발생할 수 있습니다. 내보내기 프로세스에 대 한 자세한 내용은 [클래스에서 스키마 내보내기](../../../../docs/framework/wcf/feature-details/exporting-schemas-from-classes.md)를 참조 하세요.

스키마 공급자 메서드는 또한 사용할 <xref:System.Xml.Schema.XmlSchemaType>을 반환할 수도 있습니다. 형식은 익명이거나 익명이 아닐 수 있습니다. 익명인 경우 `IXmlSerializable` 형식을 데이터 멤버로 사용할 때마다 `IXmlSerializable` 형식의 스키마가 익명 형식으로 내보내집니다. `IXmlSerializable` 형식에 여전히 데이터 계약 이름과 네임스페이스가 있습니다. 이는 <xref:System.Runtime.Serialization.DataContractAttribute> 특성을 사용 하 여 이름을 사용자 지정할 수 없는 경우를 제외 하 고는 [데이터 계약 이름](../../../../docs/framework/wcf/feature-details/data-contract-names.md) 에 설명 된 대로 결정 됩니다. 익명이 아닌 경우 `XmlSchemaSet`의 형식 중 하나여야 합니다. 이 경우는 형식의 `XmlQualifiedName`을 반환하는 것과 같습니다.

또한 전역 요소 선언이 형식에 대해 내보내집니다. 형식에 <xref:System.Xml.Serialization.XmlRootAttribute> 특성이 적용되지 않은 경우 요소가 데이터 계약과 동일한 이름 및 네임스페이스를 갖게 되며 "nillable" 속성이 `true`가 됩니다. 이에 대 한 유일한 예외는 스키마 네임 스페이스`http://www.w3.org/2001/XMLSchema`()입니다. 형식의 데이터 계약이이 네임 스페이스에 있으면 스키마 네임 스페이스에 새 요소를 추가할 수 없으므로 해당 전역 요소가 빈 네임 스페이스에 있습니다. 형식에 `XmlRootAttribute` 특성이 적용되어 있으면 전역 요소 선언이 <xref:System.Xml.Serialization.XmlRootAttribute.ElementName%2A>, <xref:System.Xml.Serialization.XmlRootAttribute.Namespace%2A> 및 <xref:System.Xml.Serialization.XmlRootAttribute.IsNullable%2A> 속성을 사용하여 내보내집니다. `XmlRootAttribute`가 적용된 경우의 기본값은 데이터 계약 이름, 빈 네임스페이스 및 `true`인 "nillable"입니다.

레거시 데이터 세트 형식에도 동일한 전역 요소 선언 규칙이 적용됩니다. `XmlRootAttribute`는 사용자 지정 코드를 통해 추가된, 즉 스키마 공급자 메서드를 사용하거나 레거시 데이터 세트 형식의 경우 `XmlSchemaSet`를 통해 `GetSchema`에 추가된 전역 요소 선언을 재정의할 수 없습니다.

### <a name="ixmlserializable-element-types"></a>IXmlSerializable 요소 형식

`IXmlSerializable` 요소 형식은 `IsAny` 속성이 `true`로 설정되어 있거나 스키마 공급자 메서드가 `null`을 반환하도록 합니다.

요소 형식의 serialize 및 deserialize는 콘텐츠 형식의 serialize 및 deserialize와 유사합니다. 그러나 다음과 같은 중요한 차이가 있습니다.

- `WriteXml` 구현은 정확히 하나의 요소를 씁니다. 물론 이 요소는 여러 개의 자식 요소를 포함할 수 있습니다. 이 단일 요소, 여러 개의 형제 요소 또는 혼합 콘텐츠 외부의 특성을 쓰면 안 됩니다. 요소는 비어 있을 수 있습니다.

- `ReadXml` 구현은 래퍼 요소를 읽어서는 안 됩니다. `WriteXml`에서 생성하는 하나의 요소를 읽습니다.

- 예를 들어 데이터 계약의 데이터 멤버로 정기적으로 요소 형식을 serialize하는 경우 serializer는 콘텐츠 형식과 마찬가지로 `WriteXml`을 호출하기 전에 래퍼 요소를 출력합니다. 그러나 최상위 수준에서 요소 형식을 serialize할 때 serializer는 일반적으로 `WriteXml` 또는 `DataContractSerializer` 생성자에서 serializer를 생성할 때 루트 이름과 네임스페이스를 명시적으로 지정하지 않은 경우 `NetDataContractSerializer`에서 쓰는 요소를 둘러싼 래퍼 요소를 출력하지 않습니다. 자세한 내용은 [Serialization 및 Deserialization](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md)합니다.

- 생성 시 루트 이름과 네임스페이스를 지정하지 않고 최상위 수준에서 요소 형식을 serialize하는 경우 <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteStartObject%2A> 및 <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteEndObject%2A>에서 아무 작업도 수행하지 않으며 <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteObjectContent%2A>는 `WriteXml`을 호출합니다. 이 모드에서 serialize되는 개체는 `null`일 수 없으며 다형적으로 할당할 수 없습니다. 또한 개체 그래프 유지를 활성화할 수 없고 `NetDataContractSerializer`를 사용할 수 없습니다.

- 생성 시 루트 이름과 네임스페이스를 지정하지 않고 최상위 수준에서 요소 형식을 deserialize하는 경우 <xref:System.Runtime.Serialization.XmlObjectSerializer.IsStartObject%2A>가 임의 요소의 시작 부분을 찾으면 `true`를 반환합니다. <xref:System.Runtime.Serialization.XmlObjectSerializer.ReadObject%2A> 매개 변수를 `verifyObjectName`로 설정한 `true`는 실제로 개체를 읽기 전에 `IsStartObject`와 같은 방식으로 동작합니다. 그런 다음 `ReadObject`는 컨트롤을 `ReadXml` 메서드로 전달합니다.

요소 형식과 관련해서 내보낸 스키마는 스키마 공급자 메서드가 `XmlElement`에 다른 스키마를 추가할 수 있다는 점을 제외하고 이전 단원에서 설명한 대로 <xref:System.Xml.Schema.XmlSchemaSet> 형식에 대해 콘텐츠 형식과 동일합니다. 요소 형식에 `XmlRootAttribute` 특성을 사용할 수 없으며 이러한 형식에 대해 전역 요소 선언을 내보내지 않습니다.

### <a name="differences-from-the-xmlserializer"></a>XmlSerializer와의 차이점

`IXmlSerializable` 인터페이스와 `XmlSchemaProviderAttribute` 및 `XmlRootAttribute` 특성도 <xref:System.Xml.Serialization.XmlSerializer>에서 인식됩니다. 그러나 데이터 계약 모델에서 처리되는 방법에 차이가 있습니다. 아래 목록에 중요한 차이가 요약되어 있습니다.

- `XmlSerializer`에서 사용할 수 있으려면 스키마 공급자 메서드가 public이어야 하지만 public이 아니어도 데이터 계약 모델에서 사용할 수 있습니다.

- 데이터 계약 모델에서 `IsAny`가 `true`일 때는 스키마 공급자 메서드가 호출되지만 `XmlSerializer`를 사용할 때는 호출되지 않습니다.

- 콘텐츠 또는 레거시 데이터 세트 형식에 `XmlRootAttribute` 특성이 없으면 `XmlSerializer`는 빈 네임스페이스에 전역 요소 선언을 내보냅니다. 데이터 계약 모델에서 사용되는 네임스페이스는 일반적으로 앞에서 설명한 데이터 계약 네임스페이스입니다.

두 가지 serialization 기술에서 모두 사용할 형식을 만드는 경우 이러한 차이에 주의하세요.

### <a name="importing-ixmlserializable-schema"></a>IXmlSerializable 스키마 가져오기

`IXmlSerializable` 형식에서 생성된 스키마를 가져오는 경우 다음과 같은 몇 가지 가능성이 있습니다.

- 생성 된 스키마는 [데이터 계약 스키마 참조](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)에 설명 된 대로 유효한 데이터 계약 스키마 일 수 있습니다. 이 경우 스키마를 일반적인 방법으로 가져올 수 있으며 일반 데이터 계약 형식이 생성됩니다.

- 생성된 스키마가 올바른 데이터 계약 스키마가 아닐 수 있습니다. 예를 들어 스키마 공급자 메서드가 데이터 계약 모델에서 지원되지 않는 XML 특성과 관련된 스키마를 생성할 수 있습니다. 이 경우 스키마를 `IXmlSerializable` 형식으로 가져올 수 있습니다. 이 가져오기 모드는 기본적으로 설정 되지 않지만 예를 `/importXmlTypes` 들어 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)로 명령줄 스위치를 사용 하 여 쉽게 사용할 수 있습니다. 이에 대해서는 [클래스를 생성 하기 위해 스키마 가져오기](../../../../docs/framework/wcf/feature-details/importing-schema-to-generate-classes.md)에 자세히 설명 되어 있습니다. 형식 인스턴스에 대한 XML로 직접 작업해야 합니다. 보다 넓은 범위의 스키마를 지원하는 다른 serialization 기술을 사용할 수도 있습니다. `XmlSerializer` 사용에 대한 항목을 참조하세요.

- 새 형식을 생성하는 대신 프록시의 기존 `IXmlSerializable` 형식을 다시 사용할 수 있습니다. 이 경우 스키마를 가져와서 형식 생성 항목에서 설명하는 참조된 형식 기능을 사용하여 다시 사용할 형식을 나타낼 수 있습니다. 이는 다시 사용할 형식이 포함된 어셈블리를 지정하는 svcutil.exe에 `/reference` 스위치를 사용하는 것에 같습니다.

### <a name="xmlserializer-legacy-behavior"></a>XmlSerializer 레거시 동작

.NET Framework 4.0 및 이전 버전에서는 XmlSerializer가 파일에 C# 코드를 작성해서 임시 serialization 어셈블리를 생성했습니다. 그런 다음 파일이 어셈블리로 컴파일됩니다.  이 동작은 serializer가 느리게 시작하는 등의 좋지 않은 결과가 있었습니다. .NET Framework 4.5에서는 이 동작이 컴파일러를 사용하지 않고도 어셈블리를 생성할 수 있도록 변경되었습니다. 일부 개발자는 생성된 C# 코드를 보고 싶어할 수 있습니다. 다음과 같이 구성하면 이 레거시 동작을 사용하도록 지정할 수 있습니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.xml.serialization>
    <xmlSerializer tempFilesLocation='e:\temp\XmlSerializerBug' useLegacySerializerGeneration="true" />
  </system.xml.serialization>
  <system.diagnostics>
    <switches>
      <add name="XmlSerialization.Compilation" value="1" />
    </switches>
  </system.diagnostics>
</configuration>
```

Public이 아닌 새 재정의를 사용 하 여 파생 `XmlSerializer` 클래스를 직렬화 하지 못하는 경우와 같이 호환성 문제가 발생 하는 경우 다음 구성을 사용 하 여 `XMLSerializer` 레거시 동작으로 다시 전환할 수 있습니다.

```xml
<configuration>
  <appSettings>
    <add key="System:Xml:Serialization:UseLegacySerializerGeneration" value="true" />
  </appSettings>
</configuration>
```

위의 구성 대신 .NET Framework 4.5 이상 버전을 실행 하는 컴퓨터에서 다음 구성을 사용할 수 있습니다.

```xml
<configuration>
  <system.xml.serialization>
    <xmlSerializer useLegacySerializerGeneration="true"/>
  </system.xml.serialization>
</configuration>
```

> [!NOTE]
> 스위치 `<xmlSerializer useLegacySerializerGeneration="true"/>` 는 .NET Framework 4.5 이상 버전을 실행 하는 컴퓨터 에서만 작동 합니다. 위의 `appSettings` 방법은 모든 .NET Framework 버전에서 작동 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.DataContractFormatAttribute>
- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Xml.Serialization.XmlSerializer>
- <xref:System.ServiceModel.MessageHeaderArrayAttribute>
- [서비스 계약에서 데이터 전송 지정](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)
- [데이터 계약 사용](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)
- [방법: XmlSerializer를 사용 하 여 WCF 클라이언트 응용 프로그램의 시작 시간 개선](../../../../docs/framework/wcf/feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md)
