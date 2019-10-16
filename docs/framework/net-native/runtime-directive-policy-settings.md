---
title: 런타임 지시문 정책 설정
ms.date: 03/30/2017
ms.assetid: cb52b1ef-47fd-4609-b69d-0586c818ac9e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 33253c249842824a529f4e8b24d4ca4228733041
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049210"
---
# <a name="runtime-directive-policy-settings"></a>런타임 지시문 정책 설정

> [!NOTE]
> 이 항목은 시험판 소프트웨어인 .NET Native Developer Preview를 참조합니다. 이 Preview 버전은 [Microsoft Connect 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=394611)에서 다운로드할 수 있습니다(등록 필요).

.NET 네이티브의 런타임 지시문 정책 설정에 따라 런타임의 형식 및 형식 멤버 사용 가능 여부가 결정됩니다. 필요한 메타데이터가 없으면 리플렉션, serialization/deserialization 또는 .NET Framework 형식을 COM 또는 Windows 런타임으로 마샬링하는 기능을 사용하는 작업이 실패할 수 있으며 예외가 throw됩니다. 가장 일반적인 예외는 [MissingMetadataException](missingmetadataexception-class-net-native.md) 및 [MissingInteropDataException](missinginteropdataexception-class-net-native.md)(interop의 경우)입니다.

런타임 정책 설정은 런타임 지시문(.rd.xml) 파일에 의해 제어됩니다. 각 런타임 지시문은 어셈블리([\<Assembly>](assembly-element-net-native.md) 요소), 형식([\<Type>](type-element-net-native.md) 요소) 또는 메서드([\<Method>](method-element-net-native.md) 요소)와 같은 특정 프로그램 요소에 대한 정책을 정의합니다. 지시문에는 다음 섹션에서 설명하는 리플렉션 정책 형식, serialization 정책 형식 및 interop 정책 형식을 정의하는 하나 이상의 특성이 포함됩니다. 특성의 값에 따라 정책 설정이 정의됩니다.

## <a name="policy-types"></a>정책 형식

런타임 지시문 파일은 리플렉션, serialization 및 interop의 세 가지 정책 형식 범주를 인식합니다.

- 리플렉션 정책 형식은 런타임에 리플렉션에 사용할 수 있는 메타데이터를 결정합니다.

  - `Activate` - 인스턴스를 활성화할 수 있도록 생성자에 대한 런타임 액세스를 제어합니다.

  - `Browse` - 프로그램 요소에 대한 정보 쿼리를 제어합니다.

  - `Dynamic` - 동적 프로그래밍을 사용할 수 있도록 모든 형식 및 멤버에 대한 런타임 액세스를 제어합니다.

  다음 표에는 리플렉션 정책 형식과 해당 형식을 사용할 수 있는 프로그램 요소가 나와 있습니다.

  |요소|Activate|Browse|Dynamic|
  |-------------|--------------|------------|-------------|
  |[\<Application>](application-element-net-native.md)|✓|✓|✓|
  |[\<Assembly>](assembly-element-net-native.md)|✓|✓|✓|
  |[\<AttributeImplies>](attributeimplies-element-net-native.md)|✓|✓|✓|
  |[\<Event>](event-element-net-native.md)||✓|✓|
  |[\<Field>](field-element-net-native.md)||✓|✓|
  |[\<GenericParameter>](genericparameter-element-net-native.md)|✓|✓|✓|
  |[\<ImpliesType>](impliestype-element-net-native.md)|✓|✓|✓|
  |[\<Method>](method-element-net-native.md)||✓|✓|
  |[\<MethodInstantiation>](methodinstantiation-element-net-native.md)||✓|✓|
  |[\<Namespace>](namespace-element-net-native.md)|✓|✓|✓|
  |[\<Parameter>](parameter-element-net-native.md)|✓|✓|✓|
  |[\<Property>](property-element-net-native.md)||✓|✓|
  |[\<Subtypes>](subtypes-element-net-native.md)|✓|✓|✓|
  |[\<Type>](type-element-net-native.md)|✓|✓|✓|
  |[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|✓|✓|✓|
  |[\<TypeParameter>](typeparameter-element-net-native.md)|✓|✓|✓|

- Serialization 정책 형식에 따라 런타임에 serialization 및 deserialization에 사용할 수 있는 메타데이터가 결정됩니다.

  - `Serialize` - Newtonsoft JSON serializer 등의 타사 라이브러리를 통해 형식 인스턴스를 serialize할 수 있도록 생성자, 필드 및 속성에 대한 런타임 액세스를 제어합니다.

  - `DataContractSerializer` - <xref:System.Runtime.Serialization.DataContractSerializer> 클래스가 형식 인스턴스를 serialize할 수 있도록 생성자, 필드 및 속성에 대한 런타임 액세스를 제어합니다.

  - `DataContractJsonSerializer` - <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 클래스가 형식 인스턴스를 serialize할 수 있도록 생성자, 필드 및 속성에 대한 런타임 액세스를 제어합니다.

  - `XmlSerializer` - <xref:System.Xml.Serialization.XmlSerializer> 클래스가 형식 인스턴스를 serialize할 수 있도록 생성자, 필드 및 속성에 대한 런타임 액세스를 제어합니다.

  다음 표에는 serialization 정책 형식과 해당 형식을 사용할 수 있는 프로그램 요소가 나와 있습니다.

  |요소|Serialize|DataContractSerializer|DataContractJsonSerializer|XmlSerializer|
  |-------------|---------------|----------------------------|--------------------------------|-------------------|
  |[\<Application>](application-element-net-native.md)|✓|✓|✓|✓|
  |[\<Assembly>](assembly-element-net-native.md)|✓|✓|✓|✓|
  |[\<AttributeImplies>](attributeimplies-element-net-native.md)|✓|✓|✓|✓|
  |[\<Event>](event-element-net-native.md)|||||
  |[\<Field>](field-element-net-native.md)|✓||||
  |[\<GenericParameter>](genericparameter-element-net-native.md)|✓|✓|✓|✓|
  |[\<ImpliesType>](impliestype-element-net-native.md)|✓|✓|✓|✓|
  |[\<Method>](method-element-net-native.md)|||||
  |[\<MethodInstantiation>](methodinstantiation-element-net-native.md)|||||
  |[\<Namespace>](namespace-element-net-native.md)|✓|✓|✓|✓|
  |[\<Parameter>](parameter-element-net-native.md)|✓|✓|✓|✓|
  |[\<Property>](property-element-net-native.md)|✓||||
  |[\<Subtypes>](subtypes-element-net-native.md)|✓|✓|✓|✓|
  |[\<Type>](type-element-net-native.md)|✓|✓|✓|✓|
  |[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|✓|✓|✓|✓|
  |[\<TypeParameter>](typeparameter-element-net-native.md)|✓|✓|✓|✓|

- interop 정책 형식에 따라 런타임에 참조 형식, 값 형식 및 함수 포인터를 COM 및 Windows 런타임으로 전달하는 데 사용할 수 있는 메타데이터가 결정됩니다.

  - `MarshalObject` - 참조 형식에 대해 COM 및 Windows 런타임으로의 네이티브 마샬링을 제어합니다.

  - `MarshalDelegate` - 대리자 형식을 함수 포인터로 마샬링하는 네이티브 마샬링을 제어합니다.

  - `MarshalStructure` - 값 형식에 대해 COM 및 Windows 런타임으로의 네이티브 마샬링을 제어합니다.

  다음 표에는 interop 정책 형식과 해당 형식을 사용할 수 있는 프로그램 요소가 나와 있습니다.

  |요소|MarshalObject|MarshalDelegate|MarshalStructure|
  |-------------|-------------------|---------------------|----------------------|
  |[\<Application>](application-element-net-native.md)|✓|✓|✓|
  |[\<Assembly>](assembly-element-net-native.md)|✓|✓|✓|
  |[\<AttributeImplies>](attributeimplies-element-net-native.md)|✓|✓|✓|
  |[\<Event>](event-element-net-native.md)||||
  |[\<Field>](field-element-net-native.md)||||
  |[\<GenericParameter>](genericparameter-element-net-native.md)|✓|✓|✓|
  |[\<ImpliesType>](impliestype-element-net-native.md)|✓|✓|✓|
  |[\<Method>](method-element-net-native.md)||||
  |[\<MethodInstantiation>](methodinstantiation-element-net-native.md)||||
  |[\<Namespace>](namespace-element-net-native.md)|✓|✓|✓|
  |[\<Parameter>](parameter-element-net-native.md)|✓|✓|✓|
  |[\<Property>](property-element-net-native.md)||||
  |[\<Subtypes>](subtypes-element-net-native.md)|✓|✓|✓|
  |[\<Type>](type-element-net-native.md)|✓|✓|✓|
  |[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|✓|✓|✓|
  |[\<TypeParameter>](typeparameter-element-net-native.md)|✓|✓|✓|

## <a name="policy-settings"></a>정책 설정

각 정책 형식은 다음 표에 나와 있는 값 중 하나로 설정할 수 있습니다. 형식 멤버를 나타내는 요소는 기타 요소와는 다른 정책 설정 집합을 지원합니다.

|정책 설정|설명|`Assembly`, `Namespace`, `Type` 및 `TypeInstantiation` 요소|`Event`, `Field`, `Method`, `MethodInstantiation` 및 `Property` 요소|
|--------------------|-----------------|-----------------------------------------------------------------------|--------------------------------------------------------------------------------|
|`All`|.NET 네이티브 도구 체인에서 제거하지 않는 모든 형식과 멤버에 대해 정책을 사용하도록 설정합니다.|✓||
|`Auto`|해당 프로그램 요소에 대한 정책 형식으로 기본 정책을 사용해야 함을 지정합니다. 이 설정은 해당 정책 형식에 대해 정책을 생략하는 것과 같습니다. `Auto`는 보통 부모 요소에서 정책이 상속됨을 나타내는 데 사용됩니다.|✓|✓|
|`Excluded`|특정 프로그램 요소에 대해 정책을 사용하지 않음을 나타냅니다. 예를 들어<br /><br /> `<Type Name="BusinessClasses.Person" Browse="Excluded" Dynamic="Excluded" />`<br /><br /> 런타임 지시문은 `BusinessClasses.Person` 클래스의 메타데이터를 검색하거나 `Person` 개체를 동적으로 인스턴스화 및 수정하는 데 사용할 수 없음을 지정합니다.|✓|✓|
|`Included`|부모 형식의 메타데이터를 사용할 수 있는 경우 정책을 사용하도록 설정합니다.||✓|
|`Public`|도구 체인이 형식 또는 멤버를 불필요한 것으로 결정하여 제거하는 경우가 아니면 public 형식 또는 멤버에 대해 정책을 사용하도록 설정합니다. 이 설정은 도구 체인에서 불필요한 것으로 결정하는 public 형식 및 멤버도 항상 사용할 수 있도록 하는 `Required Public`과는 다릅니다.|✓||
|`PublicAndInternal`|도구 체인이 형식 또는 멤버를 불필요한 것으로 결정하여 제거하는 경우가 아니면 public 및 내부 형식이나 멤버에 대해 정책을 사용하도록 설정합니다. 이 설정은 도구 체인에서 불필요한 것으로 결정하는 public 및 내부 형식과 멤버도 항상 사용할 수 있도록 하는 `Required PublicAndInternal`과는 다릅니다.|✓||
|`Required`|멤버가 사용된 것으로 표시되어도 멤버에 대한 정책이 사용되며 메타데이터가 제공됨을 나타냅니다.||✓|
|`Required Public`|public 형식 또는 멤버에 대해 정책을 사용하도록 설정하며 public 형식 또는 멤버의 메타데이터를 항상 사용할 수 있습니다. 이 설정은 도구 체인이 필요하다고 결정하는 public 형식과 멤버의 메타데이터만 제공하는 `Public`과는 다릅니다.|✓||
|`Required PublicAndInternal`|public 및 내부 형식 또는 멤버에 대해 정책을 사용하도록 설정하며 public 및 내부 형식 또는 멤버의 메타데이터를 항상 사용할 수 있습니다. 이 설정은 도구 체인이 필요하다고 결정하는 public 및 내부 형식과 멤버의 메타데이터만 제공하는 `PublicAndInternal`과는 다릅니다.|✓||
|`Required All`|도구 체인이 사용 여부에 관계없이 모든 형식과 멤버를 유지해야 하도록 지정하고 해당 형식과 멤버에 대해 정책을 사용하도록 설정합니다.|✓||

## <a name="see-also"></a>참고자료

- [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)
- [런타임 지시문 요소](runtime-directive-elements.md)
