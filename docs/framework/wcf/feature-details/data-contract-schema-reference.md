---
title: 데이터 계약 스키마 참조
ms.date: 03/30/2017
helpviewer_keywords:
- data contracts [WCF], schema reference
ms.assetid: 9ebb0ebe-8166-4c93-980a-7c8f1f38f7c0
ms.openlocfilehash: e736b963fe081832995cdc8d9c2ab41ac34cf980
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425379"
---
# <a name="data-contract-schema-reference"></a>데이터 계약 스키마 참조

이 항목에서는 XML serialization에 대한 CLR(공용 언어 런타임) 형식을 설명하기 위해 <xref:System.Runtime.Serialization.DataContractSerializer> 에서 사용하는 XSD(XML 스키마) 하위 집합에 대해 설명합니다.

## <a name="datacontractserializer-mappings"></a>DataContractSerializer 매핑

합니다 `DataContractSerializer` 메타 데이터 끝점을 사용 하는 Windows Communication Foundation (WCF) 서비스에서 메타 데이터를 내보낼 때 CLR 형식을 XSD에 매핑합니다 또는 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)합니다. 자세한 내용은 [데이터 계약 Serializer](../../../../docs/framework/wcf/feature-details/data-contract-serializer.md)합니다.

또한 WSDL(웹 서비스 기술 언어) 또는 XSD 문서에 액세스하여 서비스 또는 클라이언트에 대한 데이터 계약을 생성하기 위해 Svcutil.exe를 사용하는 경우 `DataContractSerializer` 는 XSD를 CLR 형식에 매핑합니다.

이 문서에 명시된 요구 사항을 준수하는 XML 스키마 인스턴스만 `DataContractSerializer`를 사용하여 CLR 형식에 매핑할 수 있습니다.

### <a name="support-levels"></a>지원 수준

`DataContractSerializer` 는 지정된 XML 스키마 기능에 대해 다음과 같은 수준의 지원을 제공합니다.

- **지원**. `DataContractSerializer`를 사용하여 이 기능에서 CLR 형식 또는 특성(또는 둘 다)으로 명시적 매핑이 지원됩니다.

- **무시**. `DataContractSerializer`가 가져온 스키마에 이 기능을 사용할 수 있지만 코드 생성에 영향을 주지는 않습니다.

- **사용할 수 없음**. `DataContractSerializer` 는 이 기능을 사용하여 스키마 가져오기 작업을 지원하지 않습니다. 예를 들어, 이러한 기능을 사용하는 스키마를 통해 WSDL에 액세스하는 경우 Svcutil.exe는 대신 <xref:System.Xml.Serialization.XmlSerializer> 로 대체됩니다. 이 기능은 기본적으로 설정됩니다.

## <a name="general-information"></a>일반 정보

- 스키마 네임스페이스에 대해서는 [XML Schema](https://go.microsoft.com/fwlink/?LinkId=95475)에서 설명합니다. 이 문서에서는 접두사 "xs"가 사용됩니다.

- 스키마 네임스페이스가 아닌 네임스페이스를 가진 특성은 무시됩니다.

- 이 문서에서 설명한 주석을 제외한 모든 주석이 무시됩니다.

### <a name="xsschema-attributes"></a>\<xs: schema >: 특성

|특성|DataContract|
|---------------|------------------|
|`attributeFormDefault`|무시됩니다.|
|`blockDefault`|무시됩니다.|
|`elementFormDefault`|정규화되어야 합니다. `DataContractSerializer`에서 스키마를 지원하려면 모든 요소가 정규화되어야 합니다. 설정 하거나이 작업을 수행할 수 있습니다 xs:schema/@elementFormDefault 을 "qualified" 또는 설정 하 여 xs:element/@form 각 개별 요소 선언에 "qualified"로 합니다.|
|`finalDefault`|무시됩니다.|
|`Id`|무시됩니다.|
|`targetNamespace`|지원되며 데이터 계약 네임스페이스에 매핑됩니다. 이 특성을 지정하지 않으면 빈 네임스페이스가 사용됩니다. 예약된 된 네임 스페이스를 사용할 수 없습니다. `http://schemas.microsoft.com/2003/10/Serialization/`합니다.|
|`version`|무시됩니다.|

### <a name="xsschema-contents"></a>\<xs:schema>: contents

|목차|스키마|
|--------------|------------|
|`include`|지원됩니다. `DataContractSerializer` 는 xs:include 및 xs:import를 지원합니다. 그러나 Svcutil.exe는 로컬 파일에서 메타데이터를 로드할 때 다음 `xs:include/@schemaLocation` 및 `xs:import/@location` 참조를 제한합니다. 이러한 경우 스키마 파일 목록은 `include` 가 아닌 out-of-band 메커니즘을 통해 전달해야 합니다. `include`된 스키마 문서는 무시됩니다.|
|`redefine`|사용할 수 없습니다. 보안상의 이유로 `xs:redefine` 는 `DataContractSerializer` 을 사용할 수 없습니다. `x:redefine` 을 사용하려면 `schemaLocation` 을 따라야 합니다. 상황에 따라 DataContract를 사용하는 Svcutil.exe는 `schemaLocation`사용을 제한합니다.|
|`import`|지원됩니다. `DataContractSerializer` 는 `xs:include` 및 `xs:import`를 지원합니다. 그러나 Svcutil.exe는 로컬 파일에서 메타데이터를 로드할 때 다음 `xs:include/@schemaLocation` 및 `xs:import/@location` 참조를 제한합니다. 이러한 경우 스키마 파일 목록은 `include` 가 아닌 out-of-band 메커니즘을 통해 전달해야 합니다. `include`된 스키마 문서는 무시됩니다.|
|`simpleType`|지원됩니다. `xs:simpleType` 단원을 참조하십시오.|
|`complexType`|지원되며 데이터 계약으로 매핑됩니다. `xs:complexType` 단원을 참조하십시오.|
|`group`|무시됩니다. `DataContractSerializer` 는 `xs:group`, `xs:attributeGroup`및 `xs:attribute`사용을 지원하지 않습니다. 이러한 선언은 `xs:schema`의 자식으로 무시되며 `complexType` 또는 기타 지원되는 구문 내에서 참조할 수 없습니다.|
|`attributeGroup`|무시됩니다. `DataContractSerializer` 는 `xs:group`, `xs:attributeGroup`및 `xs:attribute`사용을 지원하지 않습니다. 이러한 선언은 `xs:schema`의 자식으로 무시되며 `complexType` 또는 기타 지원되는 구문 내에서 참조할 수 없습니다.|
|`element`|지원됩니다. GED(전역 요소 선언)를 참조하십시오.|
|`attribute`|무시됩니다. `DataContractSerializer` 는 `xs:group`, `xs:attributeGroup`및 `xs:attribute`사용을 지원하지 않습니다. 이러한 선언은 `xs:schema`의 자식으로 무시되며 `complexType` 또는 기타 지원되는 구문 내에서 참조할 수 없습니다.|
|`notation`|무시됩니다.|

## <a name="complex-types--xscomplextype"></a>복합 형식 – \<xs:complexType >

### <a name="general-information"></a>일반 정보

각 복합 형식 \<xs:complexType > 데이터 계약에 매핑됩니다.

### <a name="xscomplextype-attributes"></a>\<xs:complexType >: 특성

|특성|스키마|
|---------------|------------|
|`abstract`|false이어야 합니다(기본값).|
|`block`|사용할 수 없습니다.|
|`final`|무시됩니다.|
|`id`|무시됩니다.|
|`mixed`|false이어야 합니다(기본값).|
|`name`|지원되며 데이터 계약 이름에 매핑됩니다. 이름에 마침표가 있는 경우 형식을 내부 형식에 매핑하려 합니다. 예를 들어, `A.B` 라는 복합 형식은 `A`라는 데이터 계약 이름을 가진 형식의 내부 형식인 데이터 계약 형식으로 매핑되지만 이러한 데이터 계약 형식이 있는 경우에만 가능합니다. 둘 이상의 중첩 수준이 가능합니다. 예를 들어, `A.B.C` 가 내부 형식일 수 있지만 `A` 및 `A.B` 가 모두 있는 경우에만 가능합니다.|

### <a name="xscomplextype-contents"></a>\<xs:complexType>: contents

|목차|스키마|
|--------------|------------|
|`simpleContent`|확장을 사용할 수 없습니다.<br /><br /> 제한은 `anySimpleType`에서만 허용됩니다.|
|`complexContent`|지원됩니다. "상속"을 참조하십시오.|
|`group`|사용할 수 없습니다.|
|`all`|사용할 수 없습니다.|
|`choice`|사용할 수 없음|
|`sequence`|지원되며 데이터 계약의 데이터 멤버에 매핑됩니다.|
|`attribute`|한 가지 예외를 포함하여 use="prohibited"인 경우에도 사용할 수 없습니다. 표준 Serialization 스키마 네임스페이스에서 선택적 특성만 지원됩니다. 이러한 특성은 데이터 계약 프로그래밍 모델의 데이터 멤버에 매핑되지 않습니다. 현재 이러한 하나의 특성만 의미가 있으며, 여기에 대해서는 ISerializable 단원에서 설명합니다. 다른 특성은 모두 무시됩니다.|
|`attributeGroup`|사용할 수 없습니다. WCF v1 릴리스에서 `DataContractSerializer` 존재를 무시 `attributeGroup` 내에서 `xs:complexType`합니다.|
|`anyAttribute`|사용할 수 없습니다.|
|(비어 있음)|데이터 멤버 없이 데이터 계약에 매핑됩니다.|

### <a name="xssequence-in-a-complex-type-attributes"></a>\<나타나는 > 복합 유형에: 특성

|특성|스키마|
|---------------|------------|
|`id`|무시됩니다.|
|`maxOccurs`|1이어야 합니다(기본값).|
|`minOccurs`|1이어야 합니다(기본값).|

### <a name="xssequence-in-a-complex-type-contents"></a>\<나타나는 > 복합 유형에: 콘텐츠

|목차|스키마|
|--------------|------------|
|`element`|각 인스턴스는 데이터 멤버에 매핑됩니다.|
|`group`|사용할 수 없습니다.|
|`choice`|사용할 수 없습니다.|
|`sequence`|사용할 수 없습니다.|
|`any`|사용할 수 없습니다.|
|(비어 있음)|데이터 멤버 없이 데이터 계약에 매핑됩니다.|

## <a name="elements--xselement"></a>요소 – \<xs: element >

### <a name="general-information"></a>일반 정보

`<xs:element>` 는 다음과 같은 컨텍스트에서 발생할 수 있습니다.

- 이 요소는 `<xs:sequence>`내에서 발생할 수 있으며, 일반(비컬렉션) 데이터 계약의 데이터 멤버에 대해 설명합니다. 이 경우 `maxOccurs` 특성은 1이어야 합니다. (값 0이 허용되지 않는 경우).

- 이 요소는 `<xs:sequence>`내에서 발생할 수 있으며, 컬렉션 데이터 계약의 데이터 멤버에 대해 설명합니다. 이 경우 `maxOccurs` 특성은 1보다 크거나 "unbounded"여야 합니다.

- 이 요소는 `<xs:schema>` 내에서 GED(전역 요소 선언)로 발생할 수 있습니다.

### <a name="xselement-with-maxoccurs1-within-an-xssequence-data-members"></a>\<xs: element > maxoccurs=1 내는 \<나타나는 > (데이터 멤버)

|특성|스키마|
|---------------|------------|
|`ref`|사용할 수 없습니다.|
|`name`|지원되며 데이터 멤버 이름에 매핑됩니다.|
|`type`|지원되며 데이터 멤버 형식에 매핑됩니다. 자세한 내용은 형식/기본 매핑을 참조하십시오. 지정되지 않고 요소에 익명 형식이 없는 경우 `xs:anyType` 으로 간주됩니다.|
|`block`|무시됩니다.|
|`default`|사용할 수 없습니다.|
|`fixed`|사용할 수 없습니다.|
|`form`|정규화되어야 합니다. 이 특성은 `elementFormDefault` 에서 `xs:schema`를 통해 설정할 수 있습니다.|
|`id`|무시됩니다.|
|`maxOccurs`|1|
|`minOccurs`|데이터 멤버의 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 속성에 매핑됩니다.`IsRequired` 가 1인 경우 `minOccurs` 는 true입니다.|
|`nillable`|형식 매핑에 영향을 줍니다. 형식/기본 매핑을 참조하십시오.|

### <a name="xselement-with-maxoccurs1-within-an-xssequence-collections"></a>\<xs: element > maxOccurs를 사용 하 여 > 내에서 1을 \<나타나는 > (컬렉션)

- <xref:System.Runtime.Serialization.CollectionDataContractAttribute>에 매핑됩니다.

- 컬렉션 형식에서 하나의 xs:element만 xs:sequence 내에 허용됩니다.

 컬렉션은 다음 형식 중 하나일 수 있습니다.

- 정규 컬렉션(예: 배열)

- 사전 컬렉션(값을 다른 값에 매핑. 예: <xref:System.Collections.Hashtable>)

- 사전과 키/값 쌍 형식의 배열 간 유일한 차이는 생성된 프로그래밍 모델에 있습니다. 지정된 형식이 사전 컬렉션임을 나타내는 데 사용할 수 있는 스키마 주석 메커니즘이 있습니다.

`ref`, `block`, `default`, `fixed`, `form`및 `id` 특성에 대한 규칙이 비컬렉션의 경우와 동일합니다. 기타 특성은 다음 표에 포함되어 있습니다.

|특성|스키마|
|---------------|------------|
|`name`|지원되며 <xref:System.Runtime.Serialization.CollectionDataContractAttribute.ItemName%2A> 특성의 `CollectionDataContractAttribute` 속성에 매핑됩니다.|
|`type`|지원되며 컬렉션에 저장된 형식에 매핑됩니다.|
|`maxOccurs`|1보다 크거나 "unbounded"입니다. DC 스키마는 "unbounded"를 사용해야 합니다.|
|`minOccurs`|무시됩니다.|
|`nillable`|형식 매핑에 영향을 줍니다. 이 특성은 사전 컬렉션에서 무시됩니다.|

### <a name="xselement-within-an-xsschema-global-element-declaration"></a>\<xs: element > 내는 \<xs: schema > 전역 요소 선언

- 스키마의 형식과 동일한 이름 및 네임스페이스가 있거나 익명 형식을 정의하는 GED(전역 요소 선언)가 형식과 연결된 것으로 간주합니다.

- 스키마 내보내기: 연결된 GED가 생성된 모든 단순 및 복합 형식에 대해 생성됩니다.

- Deserialization/serialization: 연결된 GED가 형식에 대해 루트 요소로 사용됩니다.

- 스키마 가져오기: 다음 규칙을 따르는 경우(형식을 정의하지 않는 한) 연결된 GED가 필요 없으며 무시됩니다.

|특성|스키마|
|---------------|------------|
|`abstract`|연결된 GED에 대해 false이어야 합니다.|
|`block`|연결된 GED에서 사용할 수 없습니다.|
|`default`|연결된 GED에서 사용할 수 없습니다.|
|`final`|연결된 GED에 대해 false이어야 합니다.|
|`fixed`|연결된 GED에서 사용할 수 없습니다.|
|`id`|무시됩니다.|
|`name`|지원됩니다. 연결된 GED의 정의를 참조하십시오.|
|`nillable`|연결된 GED에 대해 true이어야 합니다.|
|`substitutionGroup`|연결된 GED에서 사용할 수 없습니다.|
|`type`|지원되며 요소에 익명 형식이 포함되어 있는 경우 연결된 GED의 연결된 형식과 일치해야 합니다.|

### <a name="xselement-contents"></a>\<xs: element >: 콘텐츠

|목차|스키마|
|--------------|------------|
|`simpleType`|지원됩니다.*|
|`complexType`|지원됩니다.*|
|`unique`|무시됩니다.|
|`key`|무시됩니다.|
|`keyref`|무시됩니다.|
|(비어 있음)|지원됩니다.|

\* 사용 하는 경우는 `simpleType` 고 `complexType,` 요소 이름에서 파생 된 생성 된 이름을 사용 하 여 명명 된 데이터 계약이 작성 되 고 익명 데이터 계약이 없는 없다는 점을 제외 하면 익명 형식에 대 한 매핑을 익명이 아닌 형식에서와 동일 합니다. 다음 목록에는 익명 형식에 대한 규칙이 포함되어 있습니다.

- WCF 구현 세부 정보: 경우는 `xs:element` 이름에 마침표가 없는, 익명 형식은 외부 데이터 계약 형식의 내부 형식에 매핑됩니다. 이름에 마침표가 있는 경우 결과 데이터 계약 형식은 내부 형식이 아닌 독립적입니다.

- 내부 형식의 생성된 데이터 계약 이름은 외부 형식의 데이터 계약 이름 다음에 마침표, 요소 이름 및 문자열 "Type"이 옵니다.

- 이러한 이름을 가진 데이터 계약이 이미 존재하는 경우 이름에 "1", "2", "3" 등을 추가하여 고유 이름으로 만듭니다.

## <a name="simple-types---xssimpletype"></a>단순 형식- \<xs:simpleType >

### <a name="xssimpletype-attributes"></a>\<xs:simpleType >: 특성

|특성|스키마|
|---------------|------------|
|`final`|무시됩니다.|
|`id`|무시됩니다.|
|`name`|지원되며 데이터 계약 이름에 매핑됩니다.|

### <a name="xssimpletype-contents"></a>\<xs:simpleType >: 콘텐츠

|목차|스키마|
|--------------|------------|
|`restriction`|지원됩니다. 열거형 데이터 계약에 매핑됩니다. 이 특성은 열거형 패턴과 일치하지 않는 경우 무시됩니다. `xs:simpleType` 제한 단원을 참조하십시오.|
|`list`|지원됩니다. 열거형 데이터 계약에 플래그됩니다. `xs:simpleType` 목록 단원을 참조하십시오.|
|`union`|사용할 수 없습니다.|

### <a name="xsrestriction"></a>\<xs:restriction>

- 복합 형식 제한은 base="`xs:anyType`"에만 지원됩니다.

- `xs:string` 이외의 제한 패싯이 없는 `xs:enumeration` 의 단순 형식 제한은 열거형 데이터 계약에 매핑됩니다.

- 다른 모든 단순 형식 제한은 형식이 제한하는 형식에 매핑됩니다. 예를 들어, `xs:int` 제한은 `xs:int` 자체와 마찬가지로 정수로 매핑됩니다. 기본 형식 매핑에 대 한 자세한 내용은 형식/기본 매핑을 참조 하십시오.

### <a name="xsrestriction-attributes"></a>\<xs: restriction >: 특성

|특성|스키마|
|---------------|------------|
|`base`|지원되는 단순 형식 또는 `xs:anyType`이어야 합니다.|
|`id`|무시됩니다.|

### <a name="xsrestriction-for-all-other-cases-contents"></a>\<xs: restriction > 다른 모든 사례: 콘텐츠

|목차|스키마|
|--------------|------------|
|`simpleType`|있는 경우 지원되는 기본 형식에서 파생되어야 합니다.|
|`minExclusive`|무시됩니다.|
|`minInclusive`|무시됩니다.|
|`maxExclusive`|무시됩니다.|
|`maxInclusive`|무시됩니다.|
|`totalDigits`|무시됩니다.|
|`fractionDigits`|무시됩니다.|
|`length`|무시됩니다.|
|`minLength`|무시됩니다.|
|`maxLength`|무시됩니다.|
|`enumeration`|무시됩니다.|
|`whiteSpace`|무시됩니다.|
|`pattern`|무시됩니다.|
|(비어 있음)|지원됩니다.|

## <a name="enumeration"></a>열거형

### <a name="xsrestriction-for-enumerations-attributes"></a>\<xs: restriction > 열거형에 대 한: 특성

|특성|스키마|
|---------------|------------|
|`base`|있는 경우 `xs:string`이어야 합니다.|
|`id`|무시됩니다.|

### <a name="xsrestriction-for-enumerations-contents"></a>\<xs: restriction > 열거형에 대 한: 콘텐츠

|목차|스키마|
|--------------|------------|
|`simpleType`|있는 경우 데이터 계약(이 단원)에서 지원하는 열거형 제한이어야 합니다.|
|`minExclusive`|무시됩니다.|
|`minInclusive`|무시됩니다.|
|`maxExclusive`|무시됩니다.|
|`maxInclusive`|무시됩니다.|
|`totalDigits`|무시됩니다.|
|`fractionDigits`|무시됩니다.|
|`length`|사용할 수 없습니다.|
|`minLength`|사용할 수 없습니다.|
|`maxLength`|사용할 수 없습니다.|
|`enumeration`|지원됩니다. 열거형 "ID"는 무시되고 "value"는 열거형 데이터 계약의 값 이름에 매핑됩니다.|
|`whiteSpace`|사용할 수 없습니다.|
|`pattern`|사용할 수 없습니다.|
|(비어 있음)|지원되며 비어 있는 열거형 형식에 매핑됩니다.|

 다음 코드는 C# 열거형 클래스를 보여 줍니다.

```csharp
public enum MyEnum
{
  first = 3,
  second = 4,
  third =5
}
```

이 클래스는 `DataContractSerializer`에 의해 다음 스키마에 매핑됩니다. 열거형 값이 1부터 시작하는 경우 `xs:annotation` 블록이 생성되지 않습니다.

```xml
<xs:simpleType name="MyEnum">
  <xs:restriction base="xs:string">
    <xs:enumeration value="first">
      <xs:annotation>
        <xs:appinfo>
          <EnumerationValue xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
          3
          </EnumerationValue>
        </xs:appinfo>
      </xs:annotation>
    </xs:enumeration>
    <xs:enumeration value="second">
      <xs:annotation>
        <xs:appinfo>
          <EnumerationValue xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
          4
          </EnumerationValue>
        </xs:appinfo>
      </xs:annotation>
    </xs:enumeration>
  </xs:restriction>
</xs:simpleType>
```

### <a name="xslist"></a>\<xs:list>

`DataContractSerializer` 는 `System.FlagsAttribute` 로 표시된 열거형 형식을 `xs:list` 에서 파생된 `xs:string`에 매핑합니다. 다른 `xs:list` 변형은 지원되지 않습니다.

### <a name="xslist-attributes"></a>\<xs: list >: 특성

|특성|스키마|
|---------------|------------|
|`itemType`|사용할 수 없습니다.|
|`id`|무시됩니다.|

### <a name="xslist-contents"></a>\<xs:list>: contents

|목차|스키마|
|--------------|------------|
|`simpleType`|`xs:string` 패싯을 사용하는 `xs:enumeration` 에서의 제한이어야 합니다.|

열거형 값이 2의 거듭제곱으로 진행되지 않는 경우(플래그의 경우 기본값) 값은 `xs:annotation/xs:appInfo/ser:EnumerationValue` 요소에 저장됩니다.

예를 들어, 다음 코드는 열거형 형식을 플래그합니다.

```csharp
[Flags]
public enum AuthFlags
{
  AuthAnonymous = 1,
  AuthBasic = 2,
  AuthNTLM = 4,
  AuthMD5 = 16,
  AuthWindowsLiveID = 64,
}
```

이 형식이 다음 스키마에 매핑됩니다.

```xml
<xs:simpleType name="AuthFlags">
    <xs:list>
      <xs:simpleType>
        <xs:restriction base="xs:string">
          <xs:enumeration value="AuthAnonymous" />
          <xs:enumeration value="AuthBasic" />
          <xs:enumeration value="AuthNTLM" />
          <xs:enumeration value="AuthMD5">
            <xs:annotation>
              <xs:appinfo>
                <EnumerationValue xmlns="http://schemas.microsoft.com/2003/10/Serialization/">16</EnumerationValue>
              </xs:appinfo>
            </xs:annotation>
          </xs:enumeration>
          <xs:enumeration value="AuthWindowsLiveID">
            <xs:annotation>
              <xs:appinfo>
                <EnumerationValue xmlns="http://schemas.microsoft.com/2003/10/Serialization/">64</EnumerationValue>
              </xs:appinfo>
            </xs:annotation>
          </xs:enumeration>
        </xs:restriction>
      </xs:simpleType>
    </xs:list>
  </xs:simpleType>
```

## <a name="inheritance"></a>상속

### <a name="general-rules"></a>일반 규칙

데이터 계약을 다른 데이터 계약에서 상속할 수 있습니다. 이러한 데이터 계약은 기본 계약에 매핑되고 `<xs:extension>` XML 스키마 구문을 사용하여 확장 형식에 의해 파생됩니다.

데이터 계약을 컬렉션 데이터 계약에서 상속할 수 없습니다.

예를 들어, 다음 코드는 데이터 계약입니다.

```csharp
[DataContract]
public class Person
{
  [DataMember]
  public string Name;
}
[DataContract]
public class Employee : Person
{
  [DataMember]
  public int ID;
}
```

이 데이터 계약은 다음 XML 스키마 형식 선언에 매핑됩니다.

```xml
<xs:complexType name="Employee">
 <xs:complexContent mixed="false">
  <xs:extension base="tns:Person">
   <xs:sequence>
    <xs:element minOccurs="0" name="ID" type="xs:int"/>
   </xs:sequence>
  </xs:extension>
 </xs:complexContent>
</xs:complexType>
<xs:complexType name="Person">
 <xs:sequence>
  <xs:element minOccurs="0" name="Name"
    nillable="true" type="xs:string"/>
 </xs:sequence>
</xs:complexType>
```

### <a name="xscomplexcontent-attributes"></a>\<xs:complexContent >: 특성

|특성|스키마|
|---------------|------------|
|`id`|무시됩니다.|
|`mixed`|false이어야 합니다.|

### <a name="xscomplexcontent-contents"></a>\<xs:complexContent >: 콘텐츠

|목차|스키마|
|--------------|------------|
|`restriction`|base="`xs:anyType`"인 경우를 제외하고 사용할 수 없습니다. 후자는 `xs:restriction` 의 콘텐츠를 `xs:complexContent`컨테이너 바로 아래에 배치하는 것과 같습니다.|
|`extension`|지원됩니다. 데이터 계약 상속에 매핑됩니다.|

### <a name="xsextension-in-xscomplexcontent-attributes"></a>\<xs: extension >에서 \<xs:complexContent >: 특성

|특성|스키마|
|---------------|------------|
|`id`|무시됩니다.|
|`base`|지원됩니다. 이 형식이 상속되는 기본 데이터 계약 형식에 매핑됩니다.|

### <a name="xsextension-in-xscomplexcontent-contents"></a>\<xs: extension >에서 \<xs:complexContent >: 콘텐츠

규칙은 `<xs:complexType>` 콘텐츠에서와 같습니다.

`<xs:sequence>` 를 제공하는 경우 멤버 요소가 파생된 데이터 계약에 있는 추가 데이터 멤버에 매핑됩니다.

파생된 형식에 기본 형식의 요소와 동일한 이름을 가진 요소가 포함된 경우 중복 요소 선언이 고유하게 생성된 이름을 가진 데이터 멤버에 매핑됩니다. 고유한 이름을 찾을 때까지 양의 정수가 데이터 멤버 이름("member1", "member2" 등)에 추가됩니다. 반대의 경우는 다음과 같습니다.

- 파생된 데이터 계약에 기본 데이터 계약의 데이터 멤버와 동일한 이름을 가진 데이터 멤버가 있는 경우 `DataContractSerializer` 는 이 해당 요소를 파생된 형식으로 생성합니다.

- 파생된 데이터 계약에 기본 데이터 계약의 데이터 멤버와 동일한 이름을 가졌지만 형식은 다른 데이터 멤버가 포함된 경우 `DataContractSerializer` 는 기본 형식 및 파생된 형식 선언 모두에서 `xs:anyType` 형식의 요소와 함께 스키마를 가져옵니다. 원래 형식 이름은 `xs:annotations/xs:appInfo/ser:ActualType/@Name`에 유지됩니다.

이 두 변형을 통해 스키마는 모호한 콘텐츠 모델을 가질 수 있으며 각 데이터 멤버의 순서에 따라 달라집니다.

## <a name="typeprimitive-mapping"></a>형식/기본 매핑

`DataContractSerializer` 는 XML 스키마 기본 형식에 대해 다음 매핑을 사용합니다.

|XSD 형식|.NET 형식|
|--------------|---------------|
|`anyType`|<xref:System.Object>.|
|`anySimpleType`|<xref:System.String>.|
|`duration`|<xref:System.TimeSpan>.|
|`dateTime`|<xref:System.DateTime>.|
|`dateTimeOffset`|오프셋의 경우<xref:System.DateTime> 및 <xref:System.TimeSpan> . 아래 DateTimeOffset Serialization을 참조하십시오.|
|`time`|<xref:System.String>.|
|`date`|<xref:System.String>.|
|`gYearMonth`|<xref:System.String>.|
|`gYear`|<xref:System.String>.|
|`gMonthDay`|<xref:System.String>.|
|`gDay`|<xref:System.String>.|
|`gMonth`|<xref:System.String>.|
|`boolean`|<xref:System.Boolean>|
|`base64Binary`|<xref:System.Byte> 배열입니다.|
|`hexBinary`|<xref:System.String>.|
|`float`|<xref:System.Single>.|
|`double`|<xref:System.Double>.|
|`anyURI`|<xref:System.Uri>.|
|`QName`|<xref:System.Xml.XmlQualifiedName>.|
|`string`|<xref:System.String>.|
|`normalizedString`|<xref:System.String>.|
|`token`|<xref:System.String>.|
|`language`|<xref:System.String>.|
|`Name`|<xref:System.String>.|
|`NCName`|<xref:System.String>.|
|`ID`|<xref:System.String>.|
|`IDREF`|<xref:System.String>.|
|`IDREFS`|<xref:System.String>.|
|`ENTITY`|<xref:System.String>.|
|`ENTITIES`|<xref:System.String>.|
|`NMTOKEN`|<xref:System.String>.|
|`NMTOKENS`|<xref:System.String>.|
|`decimal`|<xref:System.Decimal>.|
|`integer`|<xref:System.Int64>.|
|`nonPositiveInteger`|<xref:System.Int64>.|
|`negativeInteger`|<xref:System.Int64>.|
|`long`|<xref:System.Int64>.|
|`int`|<xref:System.Int32>.|
|`short`|<xref:System.Int16>.|
|`Byte`|<xref:System.SByte>.|
|`nonNegativeInteger`|<xref:System.Int64>.|
|`unsignedLong`|<xref:System.UInt64>.|
|`unsignedInt`|<xref:System.UInt32>.|
|`unsignedShort`|<xref:System.UInt16>.|
|`unsignedByte`|<xref:System.Byte>.|
|`positiveInteger`|<xref:System.Int64>.|

## <a name="iserializable-types-mapping"></a>ISerializable 형식 매핑

.NET Framework 버전 1.0에서에서 <xref:System.Runtime.Serialization.ISerializable> 지 속성이 나 데이터 전송을 위해 개체를 serialize 하는 일반 메커니즘으로 도입 되었습니다. 구현 하는 여러.NET Framework 형식을 `ISerializable` 응용 프로그램 간에 전달할 수 있습니다. <xref:System.Runtime.Serialization.DataContractSerializer> 는 기본적으로 `ISerializable` 클래스에 대한 지원을 제공합니다. `DataContractSerializer` 는 형식의 QName(정규화된 이름)에 의해서만 달라지는 효율적인 속성 컬렉션인 `ISerializable` 구현 스키마 형식을 매핑합니다. 예를 들어, 합니다 `DataContractSerializer` 매핑합니다 <xref:System.Exception> 된 다음 XSD 형식에 `http://schemas.datacontract.org/2004/07/System` 네임 스페이스입니다.

```xml
<xs:complexType name="Exception">
 <xs:sequence>
  <xs:any minOccurs="0" maxOccurs="unbounded"
      namespace="##local" processContents="skip"/>
 </xs:sequence>
 <xs:attribute ref="ser:FactoryType"/>
</xs:complexType>
```

데이터 계약 Serialization 스키마에서 선언한 선택적 특성 `ser:FactoryType` 은 형식을 deserialize할 수 있는 팩터리 클래스를 참조합니다. 팩터리 클래스는 사용 중인 `DataContractSerializer` 인스턴스의 알려진 형식 컬렉션의 일부여야 합니다. 알려진된 형식에 대 한 자세한 내용은 참조 하세요. [데이터 계약 알려진 형식을](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)합니다.

## <a name="datacontract-serialization-schema"></a>DataContract Serialization 스키마

`DataContractSerializer` 에서 내보낸 여러 스키마는 다음과 같은 특별한 데이터 계약 Serialization 네임스페이스의 형식, 요소 및 특성을 사용합니다.

`http://schemas.microsoft.com/2003/10/Serialization`

다음은 전체 데이터 계약 Serialization 스키마 선언입니다.

```xml
<xs:schema attributeFormDefault="qualified"
   elementFormDefault="qualified"
   targetNamespace =
    "http://schemas.microsoft.com/2003/10/Serialization/"
   xmlns:xs="http://www.w3.org/2001/XMLSchema"
   xmlns:tns="http://schemas.microsoft.com/2003/10/Serialization/">

 <!-- Top-level elements for primitive types. -->
 <xs:element name="anyType" nillable="true" type="xs:anyType"/>
 <xs:element name="anyURI" nillable="true" type="xs:anyURI"/>
 <xs:element name="base64Binary"
       nillable="true" type="xs:base64Binary"/>
 <xs:element name="boolean" nillable="true" type="xs:boolean"/>
 <xs:element name="byte" nillable="true" type="xs:byte"/>
 <xs:element name="dateTime" nillable="true" type="xs:dateTime"/>
 <xs:element name="decimal" nillable="true" type="xs:decimal"/>
 <xs:element name="double" nillable="true" type="xs:double"/>
 <xs:element name="float" nillable="true" type="xs:float"/>
 <xs:element name="int" nillable="true" type="xs:int"/>
 <xs:element name="long" nillable="true" type="xs:long"/>
 <xs:element name="QName" nillable="true" type="xs:QName"/>
 <xs:element name="short" nillable="true" type="xs:short"/>
 <xs:element name="string" nillable="true" type="xs:string"/>
 <xs:element name="unsignedByte"
       nillable="true" type="xs:unsignedByte"/>
 <xs:element name="unsignedInt"
       nillable="true" type="xs:unsignedInt"/>
 <xs:element name="unsignedLong"
       nillable="true" type="xs:unsignedLong"/>
 <xs:element name="unsignedShort"
       nillable="true" type="xs:unsignedShort"/>

 <!-- Primitive types introduced for certain .NET simple types. -->
 <xs:element name="char" nillable="true" type="tns:char"/>
 <xs:simpleType name="char">
  <xs:restriction base="xs:int"/>
 </xs:simpleType>

 <!-- xs:duration is restricted to an ordered value space,
    to map to System.TimeSpan -->
 <xs:element name="duration" nillable="true" type="tns:duration"/>
 <xs:simpleType name="duration">
  <xs:restriction base="xs:duration">
   <xs:pattern
     value="\-?P(\d*D)?(T(\d*H)?(\d*M)?(\d*(\.\d*)?S)?)?"/>
   <xs:minInclusive value="-P10675199DT2H48M5.4775808S"/>
   <xs:maxInclusive value="P10675199DT2H48M5.4775807S"/>
  </xs:restriction>
 </xs:simpleType>

 <xs:element name="guid" nillable="true" type="tns:guid"/>
 <xs:simpleType name="guid">
  <xs:restriction base="xs:string">
   <xs:pattern value="[\da-fA-F]{8}-[\da-fA-F]{4}-[\da-fA-F]{4}-[\da-fA-F]{4}-[\da-fA-F]{12}"/>
  </xs:restriction>
 </xs:simpleType>

 <!-- This is used for schemas exported from ISerializable type. -->
 <xs:attribute name="FactoryType" type="xs:QName"/>
</xs:schema>
```

다음 항목에 주의해야 합니다.

- `ser:char` 은 <xref:System.Char>형식의 유니코드 문자를 표시하기 위해 도입됩니다.

- `valuespace` 의 `xs:duration` 는 <xref:System.TimeSpan>에 매핑될 수 있도록 정렬된 집합으로 축소됩니다.

- `FactoryType` 은 <xref:System.Runtime.Serialization.ISerializable>에서 파생된 형식에서 내보낸 스키마에서 사용됩니다.

## <a name="importing-non-datacontract-schemas"></a>DataContract가 아닌 스키마 가져오기

`DataContractSerializer` 에는 `ImportXmlTypes` XSD 프로필을 준수하지 않는 스키마를 가져올 수 있는 `DataContractSerializer` 옵션이 포함되어 있습니다. <xref:System.Runtime.Serialization.XsdDataContractImporter.Options%2A> 속성을 참조하십시오. 이 옵션을 `true` 로 설정하면 맞지 않는 스키마 형식을 허용하고, 이러한 형식을 다음 구현에 매핑하고, <xref:System.Xml.Serialization.IXmlSerializable> 이 <xref:System.Xml.XmlNode> 의 배열을 래핑할 수 있습니다(클래스 이름만 다름).

```csharp
[GeneratedCodeAttribute("System.Runtime.Serialization", "3.0.0.0")]
[System.Xml.Serialization.XmlSchemaProviderAttribute("ExportSchema")]
[System.Xml.Serialization.XmlRootAttribute(IsNullable=false)]
public partial class Person : object, IXmlSerializable
{
  private XmlNode[] nodesField;
  private static XmlQualifiedName typeName =
new XmlQualifiedName("Person","http://Microsoft.ServiceModel.Samples");
  public XmlNode[] Nodes
  {
    get {return this.nodesField;}
    set {this.nodesField = value;}
  }
  public void ReadXml(XmlReader reader)
  {
    this.nodesField = XmlSerializableServices.ReadNodes(reader);
  }
  public void WriteXml(XmlWriter writer)
  {
    XmlSerializableServices.WriteNodes(writer, this.Nodes);
  }
  public System.Xml.Schema.XmlSchema GetSchema()
  {
    return null;
  }
  public static XmlQualifiedName ExportSchema(XmlSchemaSet schemas)
  {
    XmlSerializableServices.AddDefaultSchema(schemas, typeName);
    return typeName;
  }
}
```

## <a name="datetimeoffset-serialization"></a>DateTimeOffset Serialization

<xref:System.DateTimeOffset> 은 기본 형식으로 취급되지 않습니다. 대신 두 부분으로 구성된 복합 요소로 serialize됩니다. 첫 번째 부분은 날짜/시간을 표시하고 두 번째 부분은 날짜/시간의 오프셋을 표시합니다. 다음 코드에서는 serialize된 DateTimeOffset 값의 예를 보여 줍니다.

```xml
<OffSet xmlns:a="http://schemas.datacontract.org/2004/07/System">
  <DateTime i:type="b:dateTime" xmlns=""
    xmlns:b="http://www.w3.org/2001/XMLSchema">2008-08-28T08:00:00
  </DateTime>
  <OffsetMinutes i:type="b:short" xmlns=""
   xmlns:b="http://www.w3.org/2001/XMLSchema">-480
   </OffsetMinutes>
</OffSet>
```

스키마는 다음과 같습니다.

```xml
<xs:schema targetNamespace="http://schemas.datacontract.org/2004/07/System">
   <xs:complexType name="DateTimeOffset">
      <xs:sequence minOccurs="1" maxOccurs="1">
         <xs:element name="DateTime" type="xs:dateTime"
         minOccurs="1" maxOccurs="1" />
         <xs:element name="OffsetMinutes" type="xs:short"
         minOccurs="1" maxOccurs="1" />
      </xs:sequence>
   </xs:complexType>
</xs:schema>
```

## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- <xref:System.Runtime.Serialization.XsdDataContractImporter>
- [데이터 계약 사용](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)
