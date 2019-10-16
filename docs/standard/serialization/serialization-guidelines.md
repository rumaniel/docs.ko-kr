---
title: Serialization 지침
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- serialization, guidelines
- binary serialization, guidelines
ms.assetid: ebbeddff-179d-443f-bf08-9c373199a73a
ms.openlocfilehash: 603306ad4a739f168716fd7f6169a79923585b82
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645057"
---
# <a name="serialization-guidelines"></a>Serialization 지침
이 문서에서는 serialize될 API를 디자인할 때 고려해야 할 지침을 보여 줍니다.  

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]
  
 .NET에서는 다양한 serialization 시나리오에 적합한 세 가지의 기본 serialization 기술을 제공합니다. 다음 표에서는 이러한 기술 및 해당 기술과 관련된 기본 .NET 형식을 보여 줍니다.  
  
|기술|관련 클래스|노트|  
|----------------|----------------------|-----------|  
|데이터 계약 Serialization|<xref:System.Runtime.Serialization.DataContractAttribute><br /><br /> <xref:System.Runtime.Serialization.DataMemberAttribute><br /><br /> <xref:System.Runtime.Serialization.DataContractSerializer><br /><br /> <xref:System.Runtime.Serialization.NetDataContractSerializer><br /><br /> <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer><br /><br /> <xref:System.Runtime.Serialization.ISerializable>|일반 지속성<br /><br /> 웹 서비스<br /><br /> JSON|  
|XML Serialization|<xref:System.Xml.Serialization.XmlSerializer>|XML 형식 <br />모든 권한 포함|  
|런타임 -Serialization(이진 및 SOAP)|<xref:System.SerializableAttribute><br /><br /> <xref:System.Runtime.Serialization.ISerializable><br /><br /> <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter><br /><br /> <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>|.NET Remoting|  
  
 새로운 형식을 디자인할 때 이러한 기술 중 해당 형식(있는 경우)이 지원해야 하는 기술을 결정해야 합니다. 다음 지침은 이러한 기술을 선택하는 방법과 해당 지원을 제공하는 방법에 대해 설명합니다. 이 지침은 애플리케이션 또는 라이브러리를 구현하는 데 사용해야 하는 serialization 기술을 선택하는 데 도움을 주기 위해 만든 것은 아닙니다. 이 지침은 API 디자인과 직접 관련되어 있지 않으므로 이 항목의 범위 내에 포함되어 있지 않습니다.  
  
## <a name="guidelines"></a>지침  
  
- 새로운 형식을 디자인할 때는 serialization을 고려해야 합니다.  
  
     프로그램에서 형식의 인스턴스를 유지하거나 전송해야 할 수 있으므로 serialization은 형식에 대해 중요한 디자인 고려 사항입니다.  
  
### <a name="choosing-the-right-serialization-technology-to-support"></a>지원할 올바른 Serialization 기술 선택  
 지정된 형식은 하나 이상의 serialization 기술을 지원하거나 serialization 기술을 전혀 지원하지 않을 수 있습니다.  
  
- 형식의 인스턴스가 웹 서비스에서 유지되거나 사용되어야 하는 경우 *데이터 계약 serialization*을 지원하는 것이 좋습니다.  
  
- 형식이 직렬화될 때 생성되는 XML 형식을 더 구체적으로 제어해야 하는 경우 데이터 계약 serialization 대신 또는 데이터 계약 serialization과 함께 *XML serialization*을 지원하는 것이 좋습니다.  
  
     이러한 지원은 XML 특성을 생성하는 등의 목적으로 데이터 계약 serialization에서 지원하지 않는 XML 구문을 사용해야 하는 일부 상호 운용성 시나리오에 필요할 수 있습니다.  
  
- 형식의 인스턴스에서 .NET Remoting 경계 간에 이동해야 하는 경우 *런타임 serialization*을 지원하는 것이 좋습니다.  
  
- 일반적인 지속성 이유만으로는 런타임 serialization 또는 XML serialization을 지원하지 마십시오. 대신 데이터 계약 serialization을 사용하십시오.  
  
#### <a name="supporting-data-contract-serialization"></a>데이터 계약 Serialization 지원  
 형식은 형식에 <xref:System.Runtime.Serialization.DataContractAttribute>를 적용하고 형식의 멤버(필드 및 속성)에 <xref:System.Runtime.Serialization.DataMemberAttribute>를 적용하여 데이터 계약 serialization을 지원할 수 있습니다.  
  
 [!code-csharp[SerializationGuidelines#1](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#1)]
 [!code-vb[SerializationGuidelines#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#1)]  
  
1. 부분 신뢰에서 사용할 수 있는 형식의 경우 형식의 데이터 멤버를 public으로 표시하는 것이 좋습니다. 완전 신뢰에서는 데이터 계약 serializer가 public이 아닌 형식 및 멤버를 serialize 및 deserialize할 수 있지만 부분 신뢰에서는 public 형식만 serialize 및 deserialize할 수 있습니다.  
  
2. Data-MemberAttribute가 있는 모든 속성에 대해 getter 및 setter를 구현하십시오. serialize 가능한 형식으로 간주되게 하려면 데이터 계약 serializer에 getter와 setter가 필요합니다. 부분 신뢰에서 사용하지 않을 형식의 경우에는 두 속성 접근자 중 하나 또는 둘 다 public이 아닐 수 있습니다.  
  
     [!code-csharp[SerializationGuidelines#2](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#2)]
     [!code-vb[SerializationGuidelines#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#2)]  
  
3. deserialize된 인스턴스의 초기화에 serialization 콜백을 사용하는 것이 좋습니다.  
  
     개체가 deserialize될 때는 생성자가 호출되지 않습니다. 따라서 정상적인 생성이 수행되는 동안 실행되는 논리는 모두 *serialization 콜백* 중 하나로 구현되어야 합니다.  
  
     [!code-csharp[SerializationGuidelines#3](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#3)]
     [!code-vb[SerializationGuidelines#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#3)]  
  
     <xref:System.Runtime.Serialization.OnDeserializedAttribute> 특성은 가장 일반적으로 사용되는 콜백 특성입니다. 패밀리의 다른 특성은 다음과 같습니다. <xref:System.Runtime.Serialization.OnDeserializingAttribute>,    
    <xref:System.Runtime.Serialization.OnSerializingAttribute> 및 <xref:System.Runtime.Serialization.OnSerializedAttribute> 이 특성은 deserialization하기 전, serialization하기 전 및 마지막으로 serialization한 후에 각각 실행되는 콜백을 표시하는 데 사용할 수 있습니다.  
  
4. <xref:System.Runtime.Serialization.KnownTypeAttribute>를 사용하여 복합 개체 그래프를 deserialize할 때 사용되어야 하는 추상 형식을 나타내는 것이 좋습니다.  
  
     예를 들어 deserialize된 데이터 멤버의 형식이 추상 클래스로 표현되는 경우 직렬 변환기가 인스턴스화할 추상 형식을 결정하고 멤버에 할당하려면 *알려진 형식* 정보가 필요합니다. 특성을 사용하여 알려진 형식을 지정하지 않으면 알려진 형식을 serializer 생성자에 전달하여 명시적으로 serializer에 전달하거나 구성 파일에 지정해야 합니다.  
  
     [!code-csharp[SerializationGuidelines#4](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#4)]
     [!code-vb[SerializationGuidelines#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#4)]  
  
     **Person** 클래스를 컴파일할 때 알려진 형식 목록을 정적으로 알 수 없는 경우 **KnownTypeAttribute**가 런타임에 알려진 형식 목록을 반환하는 메서드를 가리킬 수도 있습니다.  
  
5. serialize 가능한 형식을 만들거나 변경할 때 이전 버전과의 호환성과 이후 버전과의 호환성을 사용하는 것이 좋습니다.  
  
     이후 버전의 형식에 대한 serialize된 스트림을 현재 버전의 형식으로 deserialize할 수 있고, 그 반대로 deserialize할 수도 있습니다. 데이터 계약 특성에 명시적 매개 변수를 사용하여 계약을 유지할 목적으로 특별히 주의하는 경우를 제외하면 private 멤버이거나 내부 멤버인 경우를 포함하여 데이터 멤버는 이후 버전의 형식에서 해당 멤버의 이름, 형식 또는 순서를 변경할 수 없습니다. 이 경우에는 새 버전을 이전 버전으로 deserialize하거나 이전 버전을 새 버전으로 deserialize하십시오.  
  
6. 서로 다른 버전의 형식 간에 라운드트립이 가능하도록 <xref:System.Runtime.Serialization.IExtensibleDataObject> 인터페이스를 구현하는 것이 좋습니다.  
  
     이 인터페이스를 사용하면 serializer에서 라운드트립하는 동안 데이터가 손실되지 않습니다. <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> 속성은 현재 버전에서는 알 수 없는 이후 버전 형식의 모든 데이터를 저장합니다. 이후에 현재 버전을 이후 버전으로 직렬화하거나 deserialize하면 **ExtensionData** 속성 값을 통해 직렬화된 스트림에서 추가 데이터를 사용할 수 있습니다.  
  
     [!code-csharp[SerializationGuidelines#5](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#5)]
     [!code-vb[SerializationGuidelines#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#5)]  
  
     자세한 내용은 [호환 가능한 데이터 계약](../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)을 참조하세요.  
  
#### <a name="supporting-xml-serialization"></a>XML Serialization 지원  
 데이터 계약 serialization은 .NET Framework의 기본 serialization 기술이지만 데이터 계약 serialization에서 지원하지 않는 serialization 시나리오가 있습니다. 예를 들어 serializer에서 생성하거나 사용하는 XML의 모양을 완전히 제어할 수 있는 권한이 없습니다. 이러한 충분한 제어 권한이 필요한 경우 *XML serialization*을 사용해야 하며 이 serialization 기술을 지원하기 위한 형식을 디자인해야 합니다.  
  
1. 생성된 XML의 모양을 제어해야 하는 확실한 이유가 있지 않으면 XML Serialization에 맞게 형식을 디자인하지 마십시오. 이 serialization 기술은 앞의 섹션에서 설명한 데이터 계약 Serialization으로 대체되었습니다.  
  
     즉, 형식이 XML Serialization과 함께 사용될 것이라는 사실을 알고 있지 않으면 <xref:System.Xml.Serialization> 네임스페이스의 특성을 새 형식에 적용하지 마십시오. 다음 예제에서는 생성된 XML의 모양을 제어하는 데 **System.Xml.Serialization**을 사용하는 방법을 보여 줍니다.  
  
     [!code-csharp[SerializationGuidelines#6](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#6)]
     [!code-vb[SerializationGuidelines#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#6)]  
  
2. XML Serialization 특성을 적용하는 방법보다 serialize된 XML의 모양을 더 구체적으로 제어하려면 <xref:System.Xml.Serialization.IXmlSerializable> 인터페이스를 구현하는 것이 좋습니다. 인터페이스의 두 가지 방법 <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> 고 <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A>, serialize 된 XML 스트림을 완전히 제어할 수 있습니다. <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> 특성을 적용하여 형식에 대해 생성되는 XML 스키마를 제어할 수도 있습니다.  
  
#### <a name="supporting-runtime-serialization"></a>런타임 Serialization 지원  
 *Runtime serialization*은 .NET Remoting에 사용되는 기술입니다. .NET Remoting을 사용하여 형식이 전송될 것으로 판단되면 해당 형식이 런타임 serialization을 지원하는지 확인해야 합니다.  
  
 <xref:System.SerializableAttribute> 특성을 적용하여 *런타임 serialization*에 대한 기본 지원을 제공할 수 있으며 고급 시나리오에는 단순한 *런타임 직렬화 가능 패턴*의 구현이 포함됩니다. <xref:System.Runtime.Serialization.ISerializable>을 구현하고 serialization 생성자를 제공해야 합니다.  
  
1. .NET Remoting과 함께 형식을 사용하지 않는 경우 런타임 serialization을 지원하는 것이 좋습니다. 예를 들어 <xref:System.AddIn> 네임스페이스는 .NET Remoting을 사용하므로 **System.AddIn** 추가 기능 간에 교환된 모든 형식이 런타임 serialization을 지원해야 합니다.  
  
     [!code-csharp[SerializationGuidelines#7](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#7)]
     [!code-vb[SerializationGuidelines#7](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#7)]  
  
2. serialization 프로세스를 완전하게 제어하려면 *런타임 직렬화 가능 패턴*을 구현하는 것이 좋습니다. 데이터가 serialize 또는 deserialize될 때 데이터를 변환하려는 경우를 예로 들 수 있습니다.  
  
     이 패턴은 아주 단순합니다. <xref:System.Runtime.Serialization.ISerializable> 인터페이스를 구현하고, 개체가 deserialize될 때 사용되는 특별한 생성자를 제공하기만 하면 됩니다.  
  
     [!code-csharp[SerializationGuidelines#8](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#8)]
     [!code-vb[SerializationGuidelines#8](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#8)]  
  
3. serialization 생성자를 보호되도록 설정하고 여기에 나와 있는 샘플에 표시된 대로 입력하고 이름을 지정한 두 개의 매개 변수를 제공하십시오.  
  
     [!code-csharp[SerializationGuidelines#9](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#9)]
     [!code-vb[SerializationGuidelines#9](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#9)]  
  
4. ISerializable 멤버를 명시적으로 구현하십시오.  
  
     [!code-csharp[SerializationGuidelines#10](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#10)]
     [!code-vb[SerializationGuidelines#10](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#10)]  
  
5. **ISerializable.GetObjectData** 구현에 링크 요구를 적용합니다. 그러면 완전히 신뢰되는 코어 및 런타임 serializer만 멤버에 액세스할 수 있습니다.  
  
     [!code-csharp[SerializationGuidelines#11](../../../samples/snippets/csharp/VS_Snippets_CFX/serializationguidelines/cs/source.cs#11)]
     [!code-vb[SerializationGuidelines#11](../../../samples/snippets/visualbasic/VS_Snippets_CFX/serializationguidelines/vb/source.vb#11)]  
  
## <a name="see-also"></a>참고자료

- [데이터 계약 사용](../../../docs/framework/wcf/feature-details/using-data-contracts.md)
- [데이터 계약 직렬 변환기](../../../docs/framework/wcf/feature-details/data-contract-serializer.md)
- [데이터 계약 직렬 변환기에서 지원하는 형식](../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)
- [이진 serialization](binary-serialization.md)
- [.NET remoting](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/72x4h507(v=vs.100))
- [XML 및 SOAP serialization](xml-and-soap-serialization.md)
- [보안 및 Serialization](../../../docs/framework/misc/security-and-serialization.md)
