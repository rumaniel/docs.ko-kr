---
title: Serialization 및 Deserialization
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3d71814c-bda7-424b-85b7-15084ff9377a
ms.openlocfilehash: 085186eae034314437d5a0c1fe90e6cdf6902c5e
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045846"
---
# <a name="serialization-and-deserialization"></a>Serialization 및 Deserialization
WCF (Windows Communication Foundation)에는 <xref:System.Runtime.Serialization.DataContractSerializer>새로운 serialization 엔진인가 포함 되어 있습니다. 는 <xref:System.Runtime.Serialization.DataContractSerializer> .NET Framework 개체와 XML을 양방향으로 변환 합니다. 이 항목에서는 serializer가 작동하는 방식에 대해 설명합니다.  
  
 .NET Framework 개체를 serialize 할 때 serializer는 새 *데이터 계약* 모델을 포함 하 여 다양 한 serialization 프로그래밍 모델을 인식 합니다. 지원되는 형식의 전체 목록은 [Types Supported by the Data Contract Serializer](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)을 참조하십시오. 데이터 계약에 대한 소개는 [Using Data Contracts](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)을 참조하십시오.  
  
 XML을 deserialize할 때 serializer에서는 <xref:System.Xml.XmlReader> 및 <xref:System.Xml.XmlWriter> 클래스를 사용합니다. 또한 WCF 이진 XML <xref:System.Xml.XmlDictionaryReader> 형식을 <xref:System.Xml.XmlDictionaryWriter> 사용 하는 경우와 같은 일부 경우에 최적화 된 XML을 생성할 수 있도록 및 클래스를 지원 합니다.  
  
 WCF에는 <xref:System.Runtime.Serialization.NetDataContractSerializer>도우미 serializer 인도 포함 되어 있습니다. 는 <xref:System.Runtime.Serialization.NetDataContractSerializer> serialize 된 데이터의 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 일부로 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> .NET Framework 형식 이름도 내보내기 때문에 및 serializer와 유사 합니다. 그리고 serialize 측과 deserialize 측에서 동일한 형식을 공유할 때 사용됩니다. <xref:System.Runtime.Serialization.DataContractSerializer> 및 <xref:System.Runtime.Serialization.NetDataContractSerializer> 는 모두 공통 기본 클래스인 <xref:System.Runtime.Serialization.XmlObjectSerializer>에서 파생됩니다.  
  
> [!WARNING]
> <xref:System.Runtime.Serialization.DataContractSerializer> 는 20 미만의 16진수 값이 있는 제어 문자를 포함하는 문자열을 XML 엔터티로 serialize합니다. 이렇게 하면 wcf 서비스에 이러한 데이터를 보낼 때 WCF가 아닌 클라이언트에서 문제가 발생할 수 있습니다.  
  
## <a name="creating-a-datacontractserializer-instance"></a>DataContractSerializer 인스턴스 만들기  
 <xref:System.Runtime.Serialization.DataContractSerializer> 의 인스턴스를 구성하는 작업은 중요한 단계입니다. 구성한 후에는 어떤 설정도 변경할 수 없습니다.  
  
### <a name="specifying-the-root-type"></a>루트 형식 지정  
 *루트 형식* 은 serialize 또는 deserialize되는 인스턴스의 형식입니다. <xref:System.Runtime.Serialization.DataContractSerializer> 에는 여러 개의 생성자 오버로드가 있지만, 최소한 `type` 매개 변수를 사용하여 루트 형식을 지정해야 합니다.  
  
 특정 루트 형식에 대해 만들어진 serializer는 해당 형식이 루트 형식에서 파생된 경우가 아니라면 다른 형식을 serialize하거나 deserialize하는 데 사용할 수 없습니다. 다음 예제에서는 두 개의 클래스가 나옵니다.  
  
 [!code-csharp[c_StandaloneDataContractSerializer#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_standalonedatacontractserializer/cs/source.cs#1)]
 [!code-vb[c_StandaloneDataContractSerializer#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_standalonedatacontractserializer/vb/source.vb#1)]  
  
 이 코드에서는 `DataContractSerializer` 클래스의 인스턴스를 serialize하거나 deserialize하는 데에만 사용할 수 있는 `Person` 의 인스턴스를 구성합니다.  
  
 [!code-csharp[c_StandaloneDataContractSerializer#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_standalonedatacontractserializer/cs/source.cs#2)]
 [!code-vb[c_StandaloneDataContractSerializer#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_standalonedatacontractserializer/vb/source.vb#2)]  
  
### <a name="specifying-known-types"></a>알려진 형식 지정  
 Serialize되는 형식 중 <xref:System.Runtime.Serialization.KnownTypeAttribute> 특성이나 일부 다른 메커니즘을 사용하여 아직 처리되지 않은 형식에 다형성이 포함되는 경우, 알려진 가능한 형식 목록을 `knownTypes` 매개 변수를 사용하여 serializer의 생성자에게 전달해야 합니다. 알려진된 형식에 대 한 자세한 내용은 참조 하세요. [데이터 계약 알려진 형식을](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)합니다.  
  
 다음 예제에서는 특정 형식의 컬렉션인 `LibraryPatron`이 포함된 클래스 `LibraryItem`을 보여 줍니다. 두 번째 클래스는 `LibraryItem` 형식을 정의합니다. 세 번째와 네 번째 클래스인`Book` 및 `Newspaper`는 `LibraryItem` 클래스에서 상속됩니다.  
  
 [!code-csharp[c_StandaloneDataContractSerializer#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_standalonedatacontractserializer/cs/source.cs#3)]  
 [!code-vb[c_StandaloneDataContractSerializer#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_standalonedatacontractserializer/vb/source.vb#3)]  
  
 다음 코드에서는 `knownTypes` 매개 변수를 사용하여 serializer의 인스턴스를 구성합니다.  
  
 [!code-csharp[c_StandaloneDataContractSerializer#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_standalonedatacontractserializer/cs/source.cs#4)]
 [!code-vb[c_StandaloneDataContractSerializer#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_standalonedatacontractserializer/vb/source.vb#4)]  
  
### <a name="specifying-the-default-root-name-and-namespace"></a>기본 루트 이름 및 네임스페이스 지정  
 일반적으로 개체가 serialize되면 데이터 계약 이름과 네임스페이스에 따라 가장 바깥쪽 XML 요소의 기본 이름과 네임스페이스가 결정됩니다. 모든 내부 요소의 이름은 데이터 멤버 이름을 따르며 해당 네임스페이스는 데이터 계약의 네임스페이스와 동일합니다. 다음 예제에서는 `Name` 및 `Namespace` 클래스의 생성자에 <xref:System.Runtime.Serialization.DataContractAttribute> 및 <xref:System.Runtime.Serialization.DataMemberAttribute> 값을 설정합니다.  
  
 [!code-csharp[c_StandaloneDataContractSerializer#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_standalonedatacontractserializer/cs/source.cs#5)]
 [!code-vb[c_StandaloneDataContractSerializer#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_standalonedatacontractserializer/vb/source.vb#5)]  
  
 `Person` 클래스의 인스턴스를 serialize하면 다음과 유사한 XML이 생성됩니다.  
  
```xml  
<PersonContract xmlns="http://schemas.contoso.com">  
  <AddressMember>  
    <StreetMember>123 Main Street</StreetMember>  
   </AddressMember>  
</PersonContract>  
```  
  
 그러나 `rootName` 및 `rootNamespace` 매개 변수의 값을 <xref:System.Runtime.Serialization.DataContractSerializer> 생성자에 전달하여 루트 요소의 기본 이름과 네임스페이스를 사용자 지정할 수 있습니다. `rootNamespace` 는 데이터 멤버에 해당하는 포함된 요소의 네임스페이스에 영향을 주지 않고, 가장 바깥쪽 요소의 네임스페이스에만 영향을 줍니다.  
  
 이러한 값은 <xref:System.Xml.XmlDictionaryString> 클래스의 인스턴스나 문자열로 전달하여, 이진 XML 형식을 통해 최적화할 수 있습니다.  
  
### <a name="setting-the-maximum-objects-quota"></a>최대 개체 할당량 설정  
 일부 `DataContractSerializer` 생성자 오버로드에는 `maxItemsInObjectGraph` 매개 변수가 있습니다. 이 매개 변수는 serializer가 단일 <xref:System.Runtime.Serialization.XmlObjectSerializer.ReadObject%2A> 메서드 호출에서 serialize하거나 deserialize하는 최대 개체 수를 결정합니다. 이 메서드는 항상 하나의 루트 개체를 읽지만 이 개체의 데이터 멤버에 다른 개체가 있을 수 있으며, 마찬가지로 그러한 개체에도 다른 개체가 있을 수 있습니다. 기본값은 65536입니다. 배열을 serialize하거나 deserialize할 때 모든 배열 항목은 개별 개체로 계산됩니다. 또한 일부 개체에는 큰 메모리 표현이 있을 수 있으므로 서비스 거부 공격을 방지하기에 이 할당량만으로 충분하지 않을 수 있습니다. 자세한 내용은 [데이터에 대 한 보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-for-data.md)합니다. 이 할당량을 기본값보다 크게 늘려야 할 경우 데이터를 읽고 쓸 때 보내는 측(serialize)과 받는 측(deserialize)에 모두 적용되므로 양측에서 값을 늘려야 합니다.  
  
### <a name="round-trips"></a>라운드트립  
 *라운드트립* 은 개체가 한 번에 deserialize 및 다시 serialize될 때 발생합니다. 예를 들면 XML에서 개체 인스턴스로 이동하고 다시 XML 스트림으로 이동합니다.  
  
 일부 `DataContractSerializer` 생성자 오버로드에는 기본적으로 `ignoreExtensionDataObject` 로 설정된 `false` 매개 변수가 있습니다. 이 기본 모드에서는 데이터 계약에서 <xref:System.Runtime.Serialization.IExtensibleDataObject> 인터페이스를 구현하는 한, 라운드트립 시 이전 버전을 통해 최신 버전의 데이터 계약에서 다시 이 최신 버전으로 데이터 손실 없이 데이터를 보낼 수 있습니다. 예를 들어 `Person` 데이터 계약의 버전 1에 `Name` 및 `PhoneNumber` 데이터 멤버가 들어 있고 버전 2에서 `Nickname` 멤버를 추가한다고 가정합니다. `IExtensibleDataObject` 가 구현되면 버전 2에서 버전 1로 정보를 보낼 때 `Nickname` 데이터가 저장된 다음 다시 serialize될 때 다시 내보내집니다. 따라서 라운드트립 시 데이터가 손실되지 않습니다. 자세한 내용은 이전 [버전과 호환 되는 데이터 계약](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md) 및 [데이터 계약 버전 관리](../../../../docs/framework/wcf/feature-details/data-contract-versioning.md)를 참조 하세요.  
  
#### <a name="security-and-schema-validity-concerns-with-round-trips"></a>라운드트립과 관련된 보안 및 스키마 유효성 검사 문제  
 라운드트립 시 보안 관련 문제가 있을 수 있습니다. 예를 들어 잘못 사용된 엄청난 양의 데이터를 deserialize하고 저장하면 보안상 위험이 따를 수 있습니다. 특히 디지털 서명이 포함된 경우 확인할 방법이 없는 이러한 데이터를 다시 내보낼 경우 보안 문제가 있을 수 있습니다. 예를 들면 이전 시나리오의 경우 버전 1 엔드포인트에서 악의적인 데이터가 포함된 `Nickname` 값을 서명할 수 있습니다. 마지막으로 스키마 유효성 검사 문제가 있을 수 있는데, 엔드포인트에서 명시된 계약을 엄격히 준수하는 데이터를 항상 내보내고 다른 값은 내보내지 않을 수 있습니다. 이전 예제의 경우 버전 1 엔드포인트 계약에는 `Name` 및 `PhoneNumber`만 내보낸다고 명시되어 있는데, 스키마 유효성 검사를 사용 중일 때 추가 `Nickname` 값을 내보내면 유효성 검사에 실패하게 됩니다.  
  
#### <a name="enabling-and-disabling-round-trips"></a>라운드트립 사용 및 사용 안 함  
 라운드트립을 해제하려면 <xref:System.Runtime.Serialization.IExtensibleDataObject> 인터페이스를 구현하지 않도록 합니다. 형식에 대한 제어 권한이 없을 경우 `ignoreExtensionDataObject` 매개 변수를 `true` 로 설정하여 동일한 결과를 얻을 수 있습니다.  
  
### <a name="object-graph-preservation"></a>개체 그래프 유지  
 다음 코드에서처럼 serializer는 일반적으로 개체 ID를 고려하지 않습니다.  
  
 [!code-csharp[c_StandaloneDataContractSerializer#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_standalonedatacontractserializer/cs/source.cs#6)]
 [!code-vb[c_StandaloneDataContractSerializer#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_standalonedatacontractserializer/vb/source.vb#6)]  
  
 다음 코드에서는 구매 주문서를 만듭니다.  
  
 [!code-csharp[c_StandaloneDataContractSerializer#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_standalonedatacontractserializer/cs/source.cs#7)]
 [!code-vb[c_StandaloneDataContractSerializer#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_standalonedatacontractserializer/vb/source.vb#7)]  
  
 `billTo` 및 `shipTo` 필드는 동일한 개체 인스턴스에 설정됩니다. 그러나 생성된 XML은 복제된 정보를 복제하는데, 다음과 유사한 XML이 생성됩니다.  
  
```xml  
<PurchaseOrder>  
  <billTo><street>123 Main St.</street></billTo>  
  <shipTo><street>123 Main St.</street></shipTo>  
</PurchaseOrder>  
```  
  
 그러나 이 방법은 다음과 같이 바람직하지 않은 특성을 갖습니다.  
  
- 성능. 데이터 복제가 비효율적입니다.  
  
- 순환 참조. 개체가 다른 개체를 통해 자신을 참조하는 경우에도, 복제로 serialize하면 무한 루프가 발생합니다. 이 경우 serializer가 <xref:System.Runtime.Serialization.SerializationException> 을 throw합니다.  
  
- 의미. 경우에 따라 두 개의 참조가 똑같은 두 개의 개체로 이루어지는 것이 아니라, 하나의 동일한 개체로 이루어지도록 하는 것이 중요합니다.  
  
 이러한 이유로 인해, 일부 `DataContractSerializer` 생성자 오버로드에는 기본값이 `preserveObjectReferences` 인 `false`매개 변수가 있습니다. 이 매개 변수를로 `true`설정 하면 WCF가 이해 하는 개체 참조를 인코딩하는 특수 한 방법이 사용 됩니다. `true`로 설정된 경우 XML 코드 예제는 이제 다음과 유사합니다.  
  
```xml  
<PurchaseOrder ser:id="1">  
  <billTo ser:id="2"><street ser:id="3">123 Main St.</street></billTo>  
  <shipTo ser:ref="2"/>  
</PurchaseOrder>  
```  
  
 "Ser" 네임 스페이스는 표준 serialization 네임 스페이스를 `http://schemas.microsoft.com/2003/10/Serialization/`참조 합니다. 각 데이터 부분은 단 한 번만 serialize되고 이 데이터에 ID 번호가 제공됩니다. 이후 사용에서는 이미 serialize된 데이터를 참조하게 됩니다.  
  
> [!IMPORTANT]
> 데이터 계약 `XMLElement`에 "id" 및 "ref" 특성이 모두 있으면 "ref" 특성이 적용되는 "id" 특성은 무시됩니다.  
  
 이 모드의 제한 사항을 파악하는 것도 중요합니다.  
  
- `DataContractSerializer` 가 `preserveObjectReferences` 로 설정된 상태에서, `true` 에서 생성한 XML은 다른 기술과 상호 운용할 수 없고, 또한 `DataContractSerializer` 가 `preserveObjectReferences` 로 설정된 상태에서는 다른 `true`인스턴스에서만 이 XML에 액세스할 수 있습니다.  
  
- 이 기능에 대해서는 메타데이터(스키마)가 지원되지 않습니다. 생성된 스키마는 `preserveObjectReferences` 가 `false`로 설정된 경우에만 유효합니다.  
  
- 이 기능으로 인해 serialization 및 deserialization 프로세스 실행 속도가 느려질 수 있습니다. 데이터를 복제하지 않아도 되지만 이 모드에서 추가 개체 비교를 수행해야 합니다.  
  
> [!CAUTION]
> `preserveObjectReferences` 모드를 사용하는 경우, `maxItemsInObjectGraph` 값을 올바른 할당량으로 설정하는 것이 특히 중요합니다. 이 모드에서 배열이 처리되는 방식 때문에, 공격자가 `maxItemsInObjectGraph` 할당량에 의해서만 제한되는 과다한 메모리 소비를 일으키는 작은 악의적인 메시지를 쉽게 작성할 수 있습니다.  
  
### <a name="specifying-a-data-contract-surrogate"></a>데이터 계약 서로게이트 지정  
 일부 `DataContractSerializer` 생성자 오버로드에는 `dataContractSurrogate` 로 설정될 수 있는 `null`매개 변수가 있습니다. 그렇지 않으면 이 오버로드를 사용하여 *인터페이스를 구현하는 형식인*데이터 계약 서로게이트 <xref:System.Runtime.Serialization.IDataContractSurrogate> 를 지정할 수 있습니다. 그러면 인터페이스를 사용하여 serialization 및 deserialization 프로세스를 사용자 지정할 수 있습니다. 자세한 내용은 [데이터 계약 서로게이트](../../../../docs/framework/wcf/extending/data-contract-surrogates.md)를 참조 하세요.  
  
## <a name="serialization"></a>Serialization  
 다음과 같은 정보는 <xref:System.Runtime.Serialization.XmlObjectSerializer>및 <xref:System.Runtime.Serialization.DataContractSerializer> 클래스를 포함하여, <xref:System.Runtime.Serialization.NetDataContractSerializer> 에서 상속되는 모든 클래스에 적용됩니다.  
  
### <a name="simple-serialization"></a>간단한 Serialization  
 개체를 serialize하는 가장 기본적인 방법은 개체를 <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteObject%2A> 메서드에 전달하는 것입니다. 그리고 세 개의 오버로드가 있는데, 각각 <xref:System.IO.Stream>, <xref:System.Xml.XmlWriter>또는 <xref:System.Xml.XmlDictionaryWriter>에 쓰기 위한 오버로드입니다. <xref:System.IO.Stream> 오버로드를 사용하면 UTF-8 인코딩 형식의 XML로 출력됩니다. <xref:System.Xml.XmlDictionaryWriter> 오버로드를 사용하면 serializer는 이진 XML에 대한 출력을 최적화합니다.  
  
 <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteObject%2A> 메서드를 사용 하는 경우 serializer는 래퍼 요소의 기본 이름과 네임 스페이스를 사용 하 여 내용과 함께 씁니다 (이전 "기본 루트 이름 및 네임 스페이스 지정" 섹션 참조).  
  
 다음 예제에서는 <xref:System.Xml.XmlDictionaryWriter>를 사용하여 작성하는 방법에 대해 설명합니다.  
  
 [!code-csharp[c_StandaloneDataContractSerializer#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_standalonedatacontractserializer/cs/source.cs#8)]
 [!code-vb[c_StandaloneDataContractSerializer#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_standalonedatacontractserializer/vb/source.vb#8)]  
  
 이렇게 하면 다음과 유사한 XML이 생성됩니다.  
  
```xml  
<Person>  
  <Name>Jay Hamlin</Name>  
  <Address>123 Main St.</Address>  
</Person>  
```  
  
### <a name="step-by-step-serialization"></a>단계별 Serialization  
 각각 끝 요소를 작성하고 개체 내용을 작성하며 래퍼 요소를 닫으려면, <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteStartObject%2A>, <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteObjectContent%2A>및 <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteEndObject%2A> 메서드를 사용합니다.  
  
> [!NOTE]
> 이러한 메서드의 <xref:System.IO.Stream> 오버로드가 없습니다.  
  
 이러한 단계별 serialization을 사용하는 방법은 일반적으로 두 가지가 있습니다. 한 가지 방법은 다음 예제와 같이, 특성 또는 설명 등의 내용을 `WriteStartObject` 와 `WriteObjectContent`사이에 삽입하는 방법입니다.  
  
 [!code-csharp[c_StandaloneDataContractSerializer#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_standalonedatacontractserializer/cs/source.cs#9)]
 [!code-vb[c_StandaloneDataContractSerializer#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_standalonedatacontractserializer/vb/source.vb#9)]  
  
 이렇게 하면 다음과 유사한 XML이 생성됩니다.  
  
```xml  
<Person serializedBy="myCode">  
  <Name>Jay Hamlin</Name>  
  <Address>123 Main St.</Address>  
</Person>  
```  
  
 또 다른 일반적인 방법은 다음 코드에서처럼, <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteStartObject%2A> 및 <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteEndObject%2A> 를 전혀 사용하지 않고 사용자 지정 래퍼 요소를 작성하거나 래퍼 작성도 함께 건너뛰는 방법입니다.  
  
 [!code-csharp[c_StandaloneDataContractSerializer#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_standalonedatacontractserializer/cs/source.cs#10)]
 [!code-vb[c_StandaloneDataContractSerializer#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_standalonedatacontractserializer/vb/source.vb#10)]  
  
 이렇게 하면 다음과 유사한 XML이 생성됩니다.  
  
```xml  
<MyCustomWrapper>  
  <Name>Jay Hamlin</Name>  
  <Address>123 Main St.</Address>  
</MyCustomWrapper>  
```  
  
> [!NOTE]
> 단계별 serialization을 사용하면 스키마에 유효하지 않은 XML이 생성될 수 있습니다.  
  
## <a name="deserialization"></a>Deserialization  
 다음과 같은 정보는 <xref:System.Runtime.Serialization.XmlObjectSerializer>및 <xref:System.Runtime.Serialization.DataContractSerializer> 클래스를 포함하여, <xref:System.Runtime.Serialization.NetDataContractSerializer> 에서 상속되는 모든 클래스에 적용됩니다.  
  
 개체를 deserialize하는 가장 기본적인 방법은 <xref:System.Runtime.Serialization.XmlObjectSerializer.ReadObject%2A> 메서드 오버로드 중 하나를 호출하는 것입니다. 그리고 세 개의 오버로드가 있는데, 이 각 오버로드는 <xref:System.Xml.XmlDictionaryReader>, `XmlReader`또는 `Stream`을 사용하여 읽기 위한 오버로드입니다. `Stream` 오버로드는 할당량으로 보호되지 않고 신뢰할 수 있는 데이터를 읽는 데만 사용해야 하는 텍스트 <xref:System.Xml.XmlDictionaryReader> 를 만듭니다.  
  
 또한 `ReadObject` 메서드가 반환하는 개체는 적합한 형식으로 캐스팅되어야 합니다.  
  
 다음 코드에서는 <xref:System.Runtime.Serialization.DataContractSerializer> 및 <xref:System.Xml.XmlDictionaryReader>의 인스턴스를 구성하고 `Person` 인스턴스를 deserialize합니다.  
  
 [!code-csharp[c_StandaloneDataContractSerializer#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_standalonedatacontractserializer/cs/source.cs#11)]
 [!code-vb[c_StandaloneDataContractSerializer#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_standalonedatacontractserializer/vb/source.vb#11)]  
  
 <xref:System.Runtime.Serialization.XmlObjectSerializer.ReadObject%2A> 메서드를 호출하기 전에, 래퍼 요소나 래퍼 요소 앞에 오는 비콘텐츠 노드에 XML 판독기를 배치합니다. 이렇게 하려면 다음 코드에서처럼, <xref:System.Xml.XmlReader.Read%2A> 의 <xref:System.Xml.XmlReader> 메서드 또는 해당 파생 항목을 호출하고 <xref:System.Xml.XmlReader.NodeType%2A>을 테스트하면 됩니다.  
  
 [!code-csharp[c_StandaloneDataContractSerializer#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_standalonedatacontractserializer/cs/source.cs#12)]
 [!code-vb[c_StandaloneDataContractSerializer#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_standalonedatacontractserializer/vb/source.vb#12)]  
  
 `ReadObject`로 판독기를 전달하기 전에 이 래퍼 요소의 특성을 읽을 수 있습니다.  
  
 간단한 `ReadObject` 오버 로드 중 하나를 사용 하는 경우 역직렬 변환기는 래퍼 요소에서 기본 이름 및 네임 스페이스를 찾고 (이전 섹션인 "기본 루트 이름 및 네임 스페이스 지정" 참조) 알 수 없는을 찾은 경우 예외를 throw 합니다. 요소인. 이전 예에서는 `<Person>` 래퍼 요소가 필요합니다. 판독기가 명명된 요소에 예상한 대로 배치되었는지 확인하기 위해 <xref:System.Runtime.Serialization.XmlObjectSerializer.IsStartObject%2A> 메서드가 호출됩니다.  
  
 이 래퍼 요소 이름을 확인하지 않도록 설정하는 방법이 있습니다. `ReadObject` 메서드의 일부 오버로드는 기본적으로 `verifyObjectName`로 설정된 부울 매개 변수 `true` 을 가져옵니다. `false`로 설정하면 래퍼 요소의 이름과 네임스페이스를 무시합니다. 이는 이전에 설명한 단계별 serialization 메커니즘을 사용하여 작성된 XML을 읽을 때 유용합니다.  
  
## <a name="using-the-netdatacontractserializer"></a>NetDataContractSerializer 사용  
 `DataContractSerializer` 와의 <xref:System.Runtime.Serialization.NetDataContractSerializer> 주요 차이점은는 `DataContractSerializer` 데이터 계약 이름을 사용 하는 반면,는 `NetDataContractSerializer` serialize 된 XML에서 전체 .NET Framework 어셈블리와 형식 이름을 출력 합니다. 즉, 정확히 동일한 형식은 serialization 엔드포인트와 deserialization 엔드포인트 간에 공유되어야 합니다. 다시 말하면 deserialize할 정확한 형식을 이미 알고 있으므로 알려진 형식 메커니즘은 `NetDataContractSerializer` 에 필요하지 않습니다.  
  
 그러나 여러 가지 문제가 발생할 수 있습니다.  
  
- 보안. XML에 deserialize되고 있는 모든 형식이 로드됩니다. 이를 악용해 악의적인 형식이 로드될 수 있습니다. `NetDataContractSerializer` 속성 또는 생성자 매개 변수로 *Serialization 바인더* 를 사용하는 경우에만, 신뢰할 수 없는 데이터에 <xref:System.Runtime.Serialization.NetDataContractSerializer.Binder%2A> 를 사용해야 합니다. 바인더는 안전한 형식만 로드할 수 있도록 허용합니다. 바인더 메커니즘은 <xref:System.Runtime.Serialization> 네임스페이스의 형식에서 사용하는 메커니즘과 동일합니다.  
  
- 버전 관리. XML에 전체 형식 및 어셈블리 이름을 사용하면 형식 버전을 관리할 수 있는 방식이 제한됩니다. 형식 이름, 네임스페이스, 어셈블리 이름 및 어셈블리 버전은 변경할 수 없습니다. <xref:System.Runtime.Serialization.NetDataContractSerializer.AssemblyFormat%2A> 속성이나 생성자 매개 변수를 <xref:System.Runtime.Serialization.Formatters.FormatterAssemblyStyle.Simple> 의 기본값 대신 <xref:System.Runtime.Serialization.Formatters.FormatterAssemblyStyle.Full> 로 설정하면, 어셈블리 버전을 변경할 수 있지만 일반 매개 변수의 형식 버전은 변경할 수 없습니다.  
  
- 상호 운용성. .NET Framework 형식 및 어셈블리 이름은 XML에 포함 되어 있으므로 .NET Framework 이외의 플랫폼에서는 결과 데이터에 액세스할 수 없습니다.  
  
- 성능. 형식 및 어셈블리 이름을 작성하면 생성되는 XML의 크기가 크게 늘어납니다.  
  
 이 메커니즘은 .NET Framework remoting에서 사용 하는 이진 또는 SOAP serialization과 비슷합니다 (특히 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>및).  
  
 `NetDataContractSerializer` 사용 방식은 `DataContractSerializer`사용 방식과 비슷하지만 다음과 같은 차이점이 있습니다.  
  
- 생성자를 사용하기 위해 루트 형식을 지정하지 않아도 됩니다. `NetDataContractSerializer`의 같은 인스턴스를 사용하여 형식을 serialize할 수 있습니다.  
  
- 생성자는 알려진 형식의 목록을 허용하지 않습니다. 형식 이름이 XML로 serialize되는 경우 알려진 형식 메커니즘은 필요하지 않습니다.  
  
- 생성자는 데이터 계약 서로게이트를 허용하지 않습니다. 대신 <xref:System.Runtime.Serialization.ISurrogateSelector> 속성에 매핑되는 `surrogateSelector` 라고 하는 <xref:System.Runtime.Serialization.NetDataContractSerializer.SurrogateSelector%2A> 매개 변수를 허용합니다. 이것이 바로 레거시 서로게이트 메커니즘입니다.  
  
- 생성자는 `assemblyFormat` 속성에 매핑되는 <xref:System.Runtime.Serialization.Formatters.FormatterAssemblyStyle> 의 <xref:System.Runtime.Serialization.NetDataContractSerializer.AssemblyFormat%2A> 이라는 매개 변수를 허용합니다. 이전에 설명한 대로 이 메커니즘은 serializer의 버전 관리 기능을 향상시키는 데 사용할 수 있으며, 이진 또는 SOAP serialization의 <xref:System.Runtime.Serialization.Formatters.FormatterAssemblyStyle> 메커니즘과 동일합니다.  
  
- 생성자는 <xref:System.Runtime.Serialization.StreamingContext> 속성에 매핑되는 `context` 라는 <xref:System.Runtime.Serialization.NetDataContractSerializer.Context%2A> 매개 변수를 허용합니다. 이 메커니즘은 정보를 serialize되고 있는 형식으로 전달할 수 있으며, 이 사용 방법은 다른 <xref:System.Runtime.Serialization.StreamingContext> 클래스에 사용된 <xref:System.Runtime.Serialization> 메커니즘의 사용 방법과 동일합니다.  
  
- <xref:System.Runtime.Serialization.NetDataContractSerializer.Serialize%2A> 및 <xref:System.Runtime.Serialization.NetDataContractSerializer.Deserialize%2A> 메서드는 <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteObject%2A> 및 <xref:System.Runtime.Serialization.XmlObjectSerializer.ReadObject%2A> 메서드의 별칭입니다. 이러한 메서드는 이진 또는 SOAP serialization에 보다 일관된 프로그래밍 모델을 제공하기 위해 존재합니다.  
  
 이러한 기능에 대 한 자세한 내용은 [이진 Serialization](../../../standard/serialization/binary-serialization.md)을 참조 하세요.  
  
 `NetDataContractSerializer` 및 `DataContractSerializer` 에서 사용하는 XML 형식은 일반적으로 호환되지 않습니다. 즉, 이러한 serializer 중 하나로 serialize하고 다른 serializer로 deserialize를 시도할 수 없습니다.  
  
 또한는 `NetDataContractSerializer` 개체 그래프의 각 노드에 대 한 전체 .NET Framework 형식 및 어셈블리 이름을 출력 하지 않습니다. 모호한 정보만을 출력하는데, 즉, 루트 개체 수준에서 다형적 경우에 대해 출력합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Runtime.Serialization.NetDataContractSerializer>
- <xref:System.Runtime.Serialization.XmlObjectSerializer>
- [이진 serialization](../../../standard/serialization/binary-serialization.md)
- [데이터 계약 직렬 변환기에서 지원하는 형식](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)
