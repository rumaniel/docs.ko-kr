---
title: Serialization
ms.date: 10/22/2008
ms.technology: dotnet-standard
ms.assetid: bebb27ac-9712-4196-9931-de19fc04dbac
author: KrzysztofCwalina
ms.openlocfilehash: 0259bf82e74cbca7df8da246ca2e6ba7ef4542b3
ms.sourcegitcommit: 9ee6cd851b6e176a5811ea28ed0d5935c71950f9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68868520"
---
# <a name="serialization"></a>Serialization
Serialization은 개체를 쉽게 유지 하거나 전송할 수 있는 형식으로 변환 하는 프로세스입니다. 예를 들어 개체를 serialize 하 고, HTTP를 사용 하 여 인터넷을 통해 전송 하 고, 대상 컴퓨터에서 deserialize 할 수 있습니다.  
  
 .NET Framework는 다양 한 serialization 시나리오에 최적화 된 세 가지 주요 serialization 기술을 제공 합니다. 다음 표에서는 이러한 기술 및 해당 기술과 관련된 기본 Framework 형식을 보여 줍니다.  
  
|**기술 이름**|**기본 형식**|**시나리오**|  
|-------------------------|--------------------|-------------------|  
|**데이터 계약 Serialization**|<xref:System.Runtime.Serialization.DataContractAttribute> <br /> <xref:System.Runtime.Serialization.DataMemberAttribute> <br /> <xref:System.Runtime.Serialization.DataContractSerializer> <br /> <xref:System.Runtime.Serialization.NetDataContractSerializer> <br /> <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> <br /> <xref:System.Runtime.Serialization.ISerializable>|일반 지속성<br />웹 서비스<br />JSON|  
|**XML Serialization**|<xref:System.Xml.Serialization.XmlSerializer>|XML 모양에 대 한 모든 권한이 있는 XML 형식|  
|**런타임 Serialization (이진 및 SOAP)**|<xref:System.SerializableAttribute> <br /> <xref:System.Runtime.Serialization.ISerializable> <br /> <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> <br /> <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>|.NET Remoting|  
  
 **✓ DO** serialization 새 형식을 디자인할 때 고려해 야 합니다.  
  
## <a name="choosing-the-right-serialization-technology-to-support"></a>지원할 올바른 Serialization 기술 선택  
 **✓ CONSIDER** 데이터 계약 Serialization을 지 원하는 지속 또는 웹 서비스에서 사용 하 여의 인스턴스 해 보십시오.  
  
 **✓ CONSIDER** 형식이 serialize 될 때 생성 되는 XML 형식 보다 자세히 제어 해야 하는 경우 대신 또는 데이터 계약 Serialization 함께 XML Serialization을 지원 합니다.  
  
 이는 XML 특성을 생성 하는 등의 데이터 계약 Serialization에서 지원 하지 않는 XML 구문을 사용 해야 하는 일부 상호 운용성 시나리오에서 필요할 수 있습니다.  
  
 **✓ CONSIDER** .NET Remoting 경계를 넘어 이동 하 여의 인스턴스 필요 런타임 Serialization을 지원 합니다.  
  
 **X AVOID** 이유로 일반 지 속성에 대 한 런타임 Serialization 또는 XML 직렬화를 지원 합니다. 대신 데이터 계약 Serialization을 사용 하는 것이 좋습니다.  
  
## <a name="supporting-data-contract-serialization"></a>데이터 계약 Serialization 지원  
 형식은 형식 <xref:System.Runtime.Serialization.DataContractAttribute> 에를 적용 하 <xref:System.Runtime.Serialization.DataMemberAttribute> 고 형식의 멤버 (필드 및 속성)에를 적용 하 여 데이터 계약 Serialization을 지원할 수 있습니다.  
  
 **✓ CONSIDER** 형식을 부분 신뢰 환경에서 사용할 수 있는 경우 형식 공용 데이터 멤버를 표시 합니다.  
  
 완전 신뢰에서 데이터 계약 serializer는 public이 아닌 형식과 멤버를 serialize 및 deserialize 할 수 있지만 부분 신뢰에서는 public 멤버만 serialize 및 deserialize 할 수 있습니다.  
  
 **✓ DO** 되어 있는 모든 속성에 getter와 setter 구현 <xref:System.Runtime.Serialization.DataMemberAttribute>합니다. 데이터 계약 serializer에는 형식에 대해 getter와 setter를 모두 사용할 수 있어야 serializable로 간주할 수 있습니다. .NET Framework 3.5 s p 1에서는 일부 컬렉션 속성이 가져오기 전용 일 수 있습니다. 부분 신뢰에서 사용하지 않을 형식의 경우에는 두 속성 접근자 중 하나 또는 둘 다 public이 아닐 수 있습니다.  
  
 **✓ CONSIDER** 역직렬화 된 인스턴스의 초기화에 대 한 serialization 콜백을 사용 하 여 합니다.  
  
 개체가 deserialize될 때는 생성자가 호출되지 않습니다. 규칙에 대 한 예외가 있습니다. Deserialization 중에로 <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 표시 된 컬렉션의 생성자가 호출 됩니다. 따라서 일반 생성 중에 실행 되는 모든 논리는 serialization 콜백 중 하나로 구현 되어야 합니다.  
  
 `OnDeserializedAttribute`가장 일반적으로 사용 되는 콜백 특성입니다. 패밀리의 다른 특성으로는 <xref:System.Runtime.Serialization.OnDeserializingAttribute>, <xref:System.Runtime.Serialization.OnSerializingAttribute> 및 <xref:System.Runtime.Serialization.OnSerializedAttribute>가 있습니다. 이 특성은 deserialization하기 전, serialization하기 전 및 마지막으로 serialization한 후에 각각 실행되는 콜백을 표시하는 데 사용할 수 있습니다.  
  
 **✓ CONSIDER** 를 사용 하 여는 <xref:System.Runtime.Serialization.KnownTypeAttribute> 복잡 한 개체 그래프를 역직렬화 할 때 사용 해야 하는 구체적인 형식을 나타냅니다.  
  
 **✓ DO** 를 만들거나 직렬화 형식을 변경할 때 뒤로 및 앞으로 호환성을 고려해 야 합니다.  
  
 이후 버전의 형식에 대한 serialize된 스트림을 현재 버전의 형식으로 deserialize할 수 있고, 그 반대로 deserialize할 수도 있습니다.  
  
 데이터 계약 특성에 명시적 매개 변수를 사용 하 여 계약을 유지 해야 하는 경우를 제외 하 고, 개인 및 내부용으로 데이터 멤버의 이름, 형식 또는 순서를 변경할 수 없는지 확인 해야 합니다. .  
  
 직렬화 가능 형식을 변경할 때 serialization의 호환성을 테스트 합니다. 이 경우에는 새 버전을 이전 버전으로 deserialize하거나 이전 버전을 새 버전으로 deserialize하십시오.  
  
 **✓ CONSIDER** 구현 <xref:System.Runtime.Serialization.IExtensibleDataObject> 형식의 서로 다른 버전 간 왕복 수 있도록 합니다.  
  
 이 인터페이스를 사용하면 serializer에서 라운드트립하는 동안 데이터가 손실되지 않습니다. <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A?displayProperty=nameWithType> 속성은 현재 버전에 알려지지 않은 형식의 이후 버전의 데이터를 저장 하는 데 사용 되므로 해당 데이터 멤버에 저장할 수 없습니다. 이후 버전으로 현재 버전을 직렬화 하 고 역직렬화 하는 경우에는 serialize 된 스트림에서 추가 데이터를 사용할 수 있습니다.  
  
## <a name="supporting-xml-serialization"></a>XML Serialization 지원  
 데이터 계약 Serialization은 .NET Framework의 기본 serialization 기술 이지만 데이터 계약 Serialization에서 지원 하지 않는 serialization 시나리오가 있습니다. 예를 들어 serializer에서 생성하거나 사용하는 XML의 모양을 완전히 제어할 수 있는 권한이 없습니다. 이러한 세밀 한 제어가 필요한 경우 XML Serialization을 사용 해야 하며이 serialization 기술을 지원 하도록 형식을 디자인 해야 합니다.  
  
 **X AVOID** 생성 되는 XML의 모양을 제어 하는 매우 강력한 이유가 없다면 형식을 XML Serialization을 위해 특별히 디자인 합니다. 이 serialization 기술은 앞의 섹션에서 설명한 데이터 계약 Serialization으로 대체되었습니다.  
  
 **✓ CONSIDER** 구현는 <xref:System.Xml.Serialization.IXmlSerializable> 인터페이스는 serialize 된 XML의 모양 XML Serialization 특성을 적용 하 여 제공 된 것 보다 더 많은 제어 하려는 경우. 인터페이스 <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> 의 두 메서드 (및 <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A>)를 사용 하면 serialize 된 XML 스트림을 완전히 제어할 수 있습니다. 를 `XmlSchemaProviderAttribute`적용 하 여 형식에 대해 생성 되는 XML 스키마를 제어할 수도 있습니다.  
  
## <a name="supporting-runtime-serialization"></a>런타임 Serialization 지원  
 런타임 Serialization은 .NET Remoting에 사용 되는 기술입니다. .NET Remoting을 사용 하 여 형식을 전송할 것으로 생각 되는 경우 런타임 Serialization을 지원 하는지 확인 해야 합니다.  
  
 를 적용 <xref:System.SerializableAttribute>하 여 런타임 Serialization에 대 한 기본 지원을 제공할 수 있으며, 더 많은 고급 시나리오에는 간단한 런타임 직렬화 가능 패턴 <xref:System.Runtime.Serialization.ISerializable> (구현 및 Serialization 생성자 제공)을 구현 하는 작업이 포함 됩니다.  
  
 **✓ CONSIDER** 형식을.NET Remoting과 함께 사용 될 경우 런타임 Serialization을 지원 합니다. 예를 들어 네임 <xref:System.AddIn?displayProperty=nameWithType> 스페이스는 .net Remoting을 사용 하므로 추가 기능 간에 `System.AddIn` 교환 되는 모든 형식은 런타임 Serialization을 지원 해야 합니다.  
  
 **✓ CONSIDER** 완벽 하 게 serialization 프로세스 제어 하려는 경우 런타임 직렬화 가능 패턴을 구현 합니다. 데이터가 serialize 또는 deserialize될 때 데이터를 변환하려는 경우를 예로 들 수 있습니다.  
  
 이 패턴은 아주 단순합니다. <xref:System.Runtime.Serialization.ISerializable> 인터페이스를 구현하고, 개체가 deserialize될 때 사용되는 특별한 생성자를 제공하기만 하면 됩니다.  
  
 **✓ DO** serialization 생성자를 보호 하 고 입력 하 고이 예제에 표시 된 대로 정확 하 게 명명 된 두 개의 매개 변수를 제공 합니다.  
  
```csharp
[Serializable]  
public class Person : ISerializable
{  
    protected Person(SerializationInfo info, StreamingContext context)
    {  
        // ...  
    }  
}  
```
  
 **✓ DO** 구현에서 <xref:System.Runtime.Serialization.ISerializable> 멤버가 명시적으로 합니다.  
  
 **✓ DO** 링크 요청에 적용 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=nameWithType> 구현 합니다. 이렇게 하면 완전히 신뢰할 수 있는 코어 및 런타임 Serializer만 멤버에 액세스할 수 있습니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *받고 재인쇄 되었습니다는 피어슨 교육, inc. 프레임 워크 디자인 지침 [에서 사용 권한입니다. 다시 사용할 수 있는 .net 라이브러리에 대 한 규칙, 관용구 및](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 패턴, Microsoft Windows 개발 시리즈의 일부로 addison-Wesley Professional에서 2008 년 10 월 22 일에 게시 된 Krzysztof Cwalina 및 Brad abrams 성*  
  
## <a name="see-also"></a>참고자료

- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
- [사용 지침](../../../docs/standard/design-guidelines/usage-guidelines.md)
