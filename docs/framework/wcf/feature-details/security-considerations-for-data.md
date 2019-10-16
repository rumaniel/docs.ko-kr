---
title: 데이터에 대한 보안 고려 사항
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a7eb98da-4a93-4692-8b59-9d670c79ffb2
ms.openlocfilehash: 4114c974da9c108f641aebdb69f32fb3b0c484c9
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591523"
---
# <a name="security-considerations-for-data"></a>데이터에 대한 보안 고려 사항

Windows Communication Foundation (WCF)에서 데이터를 처리할 때 위협 범주 개수를 고려해 야 합니다. 다음 표에는 데이터 처리와 관련하여 가장 중요한 위협 클래스가 나열되어 있습니다. WCF는 이러한 위협을 완화 하는 도구를 제공 합니다.

신뢰할 수 없는 데이터를 받을 때 서비스 거부, 데이터는 시간이 오래 걸리는 계산을 시켜는 많은 양의 메모리, 스레드, 사용 가능한 연결 또는 프로세서 주기 등 다양 한 리소스에 액세스 하 고 받는 쪽을 발생할 수 있습니다. 서버에 대한 서비스 거부 공격이 발생하면 서버의 작동이 중단되고 서버가 다른 올바른 클라이언트에서 보낸 메시지를 처리하지 못할 수 있습니다.

들어오는 데이터가 있으면 코드를 실행 하 고 받는 쪽 신뢰할 수 없는 악의적인 코드 실행이 원치 않게 합니다.

정보 공개 원격 공격자에 게 하려는 것 보다 많은 정보를 공개 하는 방식으로 해당 요청에 응답 하도록 수신 파티를 강제로 수행 합니다.

## <a name="user-provided-code-and-code-access-security"></a>사용자 제공 코드 및 코드 액세스 보안

Windows Communication Foundation (WCF) 인프라의 자릿수는 사용자가 제공 되는 코드를 실행 합니다. 예를 들어, <xref:System.Runtime.Serialization.DataContractSerializer> serialization 엔진은 사용자 제공 속성 `set` 접근자 및 `get` 접근자를 호출할 수 있으며, WCF 채널 인프라의 사용자가 제공한 파생된 클래스를 호출할 수도 있습니다는 <xref:System.ServiceModel.Channels.Message> 클래스입니다.

코드를 작성할 때는 보안상 취약한 부분이 없도록 해야 합니다. 예를 들어, 데이터 멤버 속성이 정수 형식인 데이터 계약 형식을 만들고 `set` 접근자 구현에서 속성 값을 기반으로 배열을 할당하는 경우 악의적인 메시지에 이 데이터 멤버에 대한 매우 큰 값이 포함되어 있으면 서비스 거부 공격을 받을 가능성이 있습니다. 일반적으로 들어오는 데이터를 기반으로 할당을 수행하거나 사용자 제공 코드에서 시간이 오래 걸리는 처리를 수행하는 것은 피해야 합니다(특히 들어오는 데이터의 양이 적어도 처리 시간이 오래 걸릴 수 있는 경우). 사용자 제공 코드의 보안 분석을 수행할 때는 모든 실패의 경우(즉, 예외가 throw되는 모든 코드 분기)도 고려해야 합니다.

사용자 제공 코드의 한 예로 각 작업에 대한 서비스 구현 내에 있는 코드를 들 수 있습니다. 이 경우 서비스 구현의 보안에 대해서도 신경을 써야 합니다. 작업을 구현할 때 실수로 보안을 설정하지 않아서 서비스 거부 공격에 노출되는 경우도 많습니다. 문자열을 받아서 데이터베이스에서 이름이 해당 문자열로 시작하는 고객의 목록을 반환하는 작업을 예로 들 수 있습니다. 용량이 큰 데이터베이스로 작업하는 경우 전달되는 문자열이 단지 한 글자인 경우 사용자 코드가 사용 가능한 메모리 전체 크기보다 큰 메시지를 만들려고 해서 전체 서비스가 실패할 수 있습니다. (한 <xref:System.OutOfMemoryException> .NET Framework에서 복구할 수 없는 및 항상 응용 프로그램의 종료를 야기 합니다.)

다양한 확장 지점에 악의적인 코드가 들어가지 않도록 해야 합니다. 부분 신뢰에서 실행하거나, 부분적으로 신뢰할 수 있는 어셈블리의 형식을 처리하거나, 부분적으로 신뢰할 수 있는 코드에서 사용할 수 있는 구성 요소를 만드는 경우 특히 그렇습니다. 자세한 내용은 뒷부분의 "부분 신뢰 위협"을 참조하십시오.

부분 신뢰에서 실행하는 경우 데이터 계약 serialization 인프라에서는 데이터 계약 프로그래밍 모델의 제한된 하위 집합만 지원합니다. 예를 들어 <xref:System.SerializableAttribute> 특성을 사용한 전용 데이터 멤버 또는 형식은 지원되지 않습니다. 자세한 내용은 [부분 신뢰](../../../../docs/framework/wcf/feature-details/partial-trust.md)합니다.

## <a name="avoiding-unintentional-information-disclosure"></a>의도하지 않은 정보 공개 방지

보안을 염두에 두고 serialize 가능 형식을 디자인하는 경우 정보 공개는 고려해야 할 중요한 사항입니다.

다음 사항을 고려하십시오.

- <xref:System.Runtime.Serialization.DataContractSerializer> 프로그래밍 모델에서는 serialization 동안 형식 또는 어셈블리 외부의 개인 및 내부 데이터가 노출될 수 있습니다. 또한 스키마를 내보내는 동안 형식의 셰이프가 노출될 수 있으므로 형식의 serialization 프로젝션을 이해해야 합니다. 노출되지 않도록 하려면 serialize하지 않도록 설정해야 합니다. 예를 들어, 데이터 계약의 경우 <xref:System.Runtime.Serialization.DataMemberAttribute> 특성을 적용하지 않을 수 있습니다.

- 사용하는 serializer에 따라 같은 형식에 여러 개의 serialization 프로젝션이 있을 수 있습니다. 같은 형식이 <xref:System.Runtime.Serialization.DataContractSerializer> 에 사용한 경우와 <xref:System.Xml.Serialization.XmlSerializer>에 사용한 경우에 노출하는 데이터 집합이 다를 수도 있습니다. 실수로 잘못된 serializer를 사용하면 정보가 공개될 수 있습니다.

- 레거시 RPC(원격 프로시저 호출)/인코딩 모드에서 <xref:System.Xml.Serialization.XmlSerializer> 를 사용하면 보내는 쪽의 개체 그래프의 셰이프가 받는 쪽에 실수로 노출될 수 있습니다.

## <a name="preventing-denial-of-service-attacks"></a>서비스 거부 공격 방지

### <a name="quotas"></a>할당량

받는 쪽에서 많은 양의 메모리를 할당하도록 하면 서비스 거부 공격이 발생할 수 있습니다. 이 단원에서는 용량이 큰 메시지로 인해 발생하는 메모리 소비 문제를 주로 설명하지만 다른 공격이 발생할 수도 있습니다. 예를 들어, 메시지의 처리 시간이 과도하게 오래 걸릴 수 있습니다.

서비스 거부 공격은 주로 할당량을 사용하여 완화시킬 수 있습니다. 할당량을 초과하면 대개 <xref:System.ServiceModel.QuotaExceededException> 예외가 throw됩니다. 할당량이 없는 경우에는 악의적인 메시지가 사용 가능한 모든 메모리에 액세스하여 <xref:System.OutOfMemoryException> 예외가 발생하거나 사용 가능한 모든 스택에 액세스하여 <xref:System.StackOverflowException>이 발생할 수 있습니다.

할당량 초과 시나리오는 복구가 가능합니다. 실행 중인 서비스에서 발생한 경우 현재 처리 중인 메시지를 삭제하면 서비스를 계속 실행하면서 메시지를 더 처리할 수 있습니다. 그러나 메모리 부족 및 스택 오버플로 시나리오 되지 않으며.NET Framework에서 복구할 수 이러한 예외가 발생 하면 서비스가 종료 합니다.

WCF에서 할당량은 사전 할당과 관계가 하지 않습니다. 예를 들어, 다양한 클래스에 있는 <xref:System.ServiceModel.Channels.TransportBindingElement.MaxReceivedMessageSize%2A> 할당량이 128KB로 설정된 경우 각 메시지에 자동으로 128KB가 할당되는 것은 아닙니다. 실제로 할당되는 양은 실제로 들어오는 메시지 크기에 따라 다릅니다.

많은 할당량을 전송 계층에서 사용할 수 있습니다. 이러한 할당량은 사용 중인 특정 전송 채널(HTTP, TCP 등)에서 적용됩니다. 이 항목에서는 이러한 할당량 중 일부에 대해 설명하며 자세한 내용은 [Transport Quotas](../../../../docs/framework/wcf/feature-details/transport-quotas.md)에 나와 있습니다.

### <a name="hashtable-vulnerability"></a>해시 테이블 취약성

데이터 계약에 해시 테이블 또는 컬렉션이 포함된 경우 취약성이 존재합니다. 해시 테이블에 많은 수의 값을 삽입할 때 이러한 값이 동일한 해시 값을 생성할 경우 문제가 발생합니다. 이 방식은 DOS 공격으로 사용될 수 있습니다.  MaxReceivedMessageSize 바인딩 할당량을 설정 하 여이 취약성을 완화할 수 있습니다. 이러한 공격 방지를 위해 이 할당량을 설정할 때는 주의가 필요합니다. 이 할당량은 WCF 메시지 크기에 상한을 둡니다. 또한 데이터 계약에서는 해시 테이블 또는 컬렉션을 사용하지 않도록 하십시오.

## <a name="limiting-memory-consumption-without-streaming"></a>스트리밍을 사용하지 않는 경우 메모리 소비 제한

큰 메시지에 대한 보안 모델은 스트리밍 사용 여부에 따라 달라집니다. 스트리밍을 사용하지 않는 기본적인 경우에는 메시지가 메모리에 버퍼링됩니다. 이 경우 <xref:System.ServiceModel.Channels.TransportBindingElement.MaxReceivedMessageSize%2A> 또는 시스템 제공 바인딩에서 <xref:System.ServiceModel.Channels.TransportBindingElement> 할당량을 사용하면 액세스할 수 있는 최대 메시지 크기를 제한하여 용량이 큰 메시지 문제를 방지할 수 있습니다. 서비스는 여러 개의 메시지를 동시에 처리할 수 있으며 이 경우 메시지는 모두 메모리에 들어갑니다. 스로틀 기능을 사용하여 이 위협을 완화합니다.

`MaxReceivedMessageSize` 는 메시지당 메모리 소비량에 대한 상한을 지정하지는 않지만 상수 계수 이내로 제한합니다. 예를 들어, `MaxReceivedMessageSize` 가 1MB인 경우 1MB의 메시지를 받아서 deserialize하면 deserialize된 개체 그래프를 포함하기 위해 추가 메모리가 필요하기 때문에 총 메모리 소비량은 1MB를 훨씬 초과합니다. 따라서 들어오는 데이터가 많지 않아도 대량의 메모리를 소비할 수 있는 serialize 가능한 형식은 만들지 않는 것이 좋습니다. 예를 들어 데이터 계약을 "MyContract"를 추가로 개인 필드 100 및 50 선택적인 데이터 멤버 필드가 XML 생성을 사용 하 여 인스턴스화할 수 없습니다 "\<MyContract / >"입니다. 이 XML은 150개 필드에 해당되는 메모리에 액세스합니다. 데이터 멤버는 기본적으로 선택 사항입니다. 이러한 형식이 배열의 일부인 경우에는 문제가 복잡해집니다.

`MaxReceivedMessageSize` 만으로는 모든 서비스 거부 공격을 방지하기에 충분하지 않습니다. 예를 들어, 들어오는 메시지에서 deserializer에 여러 층으로 중첩된 개체 그래프(한 개체에 포함된 개체에 또 개체가 포함되는 등)의 deserialize를 요구할 수 있습니다. <xref:System.Runtime.Serialization.DataContractSerializer> 와 <xref:System.Xml.Serialization.XmlSerializer> 는 모두 중첩된 방식으로 메서드를 호출하여 이러한 그래프를 deserialize합니다. 메서드 호출이 너무 많이 중첩되면 <xref:System.StackOverflowException>을 복구하지 못할 수 있습니다. <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement.MaxDepth%2A> 할당량을 설정하여 이 항목의 뒷부분 "안전한 XML 사용" 단원에 설명된 대로 XML 중첩의 수준을 제한하면 이 위협을 완화할 수 있습니다.

이진 XML 인코딩을 사용하는 경우에는 특히 `MaxReceivedMessageSize` 에 추가로 할당량을 설정하는 것이 중요합니다. 이진 인코딩을 사용하는 것은 압축과 비슷한 면이 있습니다. 들어오는 메시지의 바이트 수가 적어도 표현하는 데이터는 많을 수 있습니다. 따라서 `MaxReceivedMessageSize` 제한에 맞는 메시지도 완전히 확장된 상태에서는 훨씬 더 많은 메모리를 차지할 수 있습니다. 이러한 XML 관련 위협을 완화하려면 이 항목 뒷부분의 "안전한 XML 사용" 단원에 설명된 대로 모든 XML 판독기 할당량을 올바르게 설정해야 합니다.

## <a name="limiting-memory-consumption-with-streaming"></a>스트리밍 시 메모리 소비 제한

스트리밍할 때 `MaxReceivedMessageSize` 를 작게 설정하여 서비스 거부 공격으로부터 시스템을 보호할 수 있습니다. 그러나 스트리밍과 관련된 보다 복잡한 시나리오도 가능합니다. 예를 들어, 파일 업로드 서비스에서 사용 가능한 전체 메모리보다 큰 파일을 받는 경우가 있습니다. 이 경우 데이터가 거의 메모리에 버퍼링되지 않고 메시지가 디스크로 직접 스트리밍될 것을 예상하고 `MaxReceivedMessageSize` 를 매우 큰 값으로 설정합니다. 악의적인 메시지 수에 예제의 경우 스트리밍하는 대신 데이터를 버퍼링 WCF를 강제로 어떤 이유로 든 `MaxReceivedMessageSize` 메시지 사용 가능한 모든 메모리 액세스에 대해 더 이상 보호 합니다.

이 완화 하려면 특정 할당량 설정이 다양 한 WCF 데이터 처리 구성 요소에 버퍼링 하는 제한 합니다. 이 중 가장 중요한 것은 다양한 전송 바인딩 요소 및 표준 바인딩에 대한 `MaxBufferSize` 속성입니다. 스트리밍 시 메시지당 할당하려는 최대 메모리 크기를 고려해서 이 할당량을 설정해야 합니다. 이 설정은 `MaxReceivedMessageSize`와 마찬가지로 메모리 소비량에 대한 절대 최대값을 지정하지 않으며 상수 계수 이내로 제한합니다. 또한 `MaxReceivedMessageSize`와 마찬가지로 여러 메시지를 동시에 처리하는 경우를 생각해야 합니다.

### <a name="maxbuffersize-details"></a>MaxBufferSize 세부 정보

`MaxBufferSize` 속성 제한 모든 대량 버퍼링 WCF 않습니다. 예를 들어 WCF SOAP 헤더 및 SOAP 오류 뿐 아니라 읽기 순서가 자연스럽 전송 최적화 메커니즘 MTOM (Message) 메시지의 않은 것으로 발견 되는 MIME 파트에 항상 버퍼링 합니다. 이 설정은 이러한 모든 경우 버퍼링 크기를 제한합니다.

WCF는이 전달 하 여 수행 된 `MaxBufferSize` 버퍼링 할 수 있는 다양 한 구성 요소에는 값입니다. 예를 들어, <xref:System.ServiceModel.Channels.Message.CreateMessage%2A> 클래스의 일부 <xref:System.ServiceModel.Channels.Message> 오버로드는 `maxSizeOfHeaders` 매개 변수를 사용합니다. Wcf는 `MaxBufferSize` SOAP 헤더 버퍼링 크기를 제한 하려면이 매개 변수 값입니다. <xref:System.ServiceModel.Channels.Message> 클래스를 직접 사용하는 경우 이 매개 변수를 설정하는 것이 중요합니다. 일반적으로 할당량 매개 변수를 사용 하는 WCF에는 구성 요소를 사용 하는 경우이 반드시 이러한 매개 변수의 보안 의미를 이해 하 고 올바르게 설정 해야 합니다.

MTOM 메시지 인코더에는 또한 `MaxBufferSize` 설정이 있습니다. 표준 바인딩을 사용하는 경우 이 설정은 자동으로 전송 수준 `MaxBufferSize` 값으로 설정됩니다. 그러나 MTOM 메시지 인코더 바인딩 요소를 사용하여 사용자 지정 바인딩을 생성하는 경우에는 `MaxBufferSize` 속성을 스트리밍을 사용할 때 안전한 값으로 설정해야 합니다.

## <a name="xml-based-streaming-attacks"></a>XML 기반 스트리밍 공격

`MaxBufferSize` 단독으로 충분 하지 않습니다 확인 WCF 스트리밍이 예상 되는 경우 버퍼링를 강제 적용할 수 없습니다. 예를 들어 WCF XML 판독기 항상 버퍼는 전체 XML 요소 시작 태그를 새 요소를 읽기 시작할 때입니다. 이렇게 하면 네임스페이스와 특성이 올바르게 처리됩니다. `MaxReceivedMessageSize`가 크게(예: 큰 파일을 직접 디스크로 스트리밍하는 시나리오가 가능하도록) 구성된 경우 메시지 본문 전체가 거대한 XML 요소 시작 태그인 악의적인 메시지가 구성될 수 있습니다. 이 메시지를 읽으려고 하면 <xref:System.OutOfMemoryException>이 발생합니다. 이 여러 가능한 XML 기반 서비스 거부 공격 모든 완화 될 수 있는이 항목의 뒷부분 "안전한 XML 사용" 섹션에서 설명 하는 XML 판독기 할당량을 사용 하 여 중입니다. 스트리밍을 사용할 때는 이러한 할당량을 모두 설정하는 것이 특히 중요합니다.

### <a name="mixing-streaming-and-buffering-programming-models"></a>스트리밍과 버퍼링 프로그래밍 모델 혼합

동일한 서비스에서 스트리밍과 비스트리밍 프로그래밍 모델을 혼합하여 사용하는 경우 여러 가지 공격이 발생할 수 있습니다. <xref:System.IO.Stream> 을 받는 작업과 일부 사용자 정의 형식의 배열을 받는 작업의 두 가지 작업이 있는 서비스 계약을 가정할 수 있습니다. 또한 첫 번째 작업에서 큰 스트림을 처리할 수 있도록 `MaxReceivedMessageSize` 가 큰 값으로 설정되었다고 가정합니다. 그러나 이 경우 용량이 큰 메시지가 두 번째 작업으로도 전송될 수 있으며 작업이 호출되기 전에 deserializer가 데이터를 메모리에 배열로 버퍼링할 수 있습니다. 그러면 deserializer에서 작업에 사용하는 메시지 본문의 크기가 `MaxBufferSize` 할당량으로 제한되지 않아 서비스 거부 공격이 발생할 수 있습니다.

이러한 이유로 동일한 계약에서 스트리밍 기반 작업과 비스트리밍 작업을 혼합하지 않는 것이 좋습니다. 두 가지 프로그래밍 모델을 반드시 혼합해야 하는 경우에는 다음 주의 사항에 따르십시오.

- <xref:System.Runtime.Serialization.IExtensibleDataObject> 의 <xref:System.ServiceModel.ServiceBehaviorAttribute.IgnoreExtensionDataObject%2A> 속성을 <xref:System.ServiceModel.ServiceBehaviorAttribute> 로 설정하여 `true`기능을 끕니다. 그러면 계약에 속한 멤버만 deserialize됩니다.

- <xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A> 의 <xref:System.Runtime.Serialization.DataContractSerializer> 속성을 안전한 값으로 설정합니다. 이 할당량은 <xref:System.ServiceModel.ServiceBehaviorAttribute> 특성에서나 구성을 통해서도 사용할 수 있습니다. 이 할당량은 한 deserialize 에피소드에서 deserialize되는 개체의 수를 제한합니다. 일반적으로 메시지 계약에 있는 각 작업 매개 변수 또는 메시지 본문은 한 에피소드로 deserialize됩니다. 배열을 deserialize할 때는 각 배열 항목이 개별 개체로 계산됩니다.

- 모든 XML 판독기 할당량을 안전한 값으로 설정합니다. <xref:System.Xml.XmlDictionaryReaderQuotas.MaxDepth%2A>, <xref:System.Xml.XmlDictionaryReaderQuotas.MaxStringContentLength%2A>및 <xref:System.Xml.XmlDictionaryReaderQuotas.MaxArrayLength%2A> 에 주의하고 비스트리밍 작업의 문자열을 피해야 합니다.

- 알려진 형식의 목록을 검토하며 이러한 형식은 언제든지 인스턴스화할 수 있다는 것에 주의합니다. 이 항목 뒷부분의 "의도하지 않은 형식이 로드되는 것을 방지" 단원을 참조하십시오.

- 많은 데이터를 버퍼링하는 <xref:System.Xml.Serialization.IXmlSerializable> 인터페이스를 구현하는 형식을 사용하지 마십시오. 이러한 형식을 알려진 형식의 목록에 추가하지 마십시오.

- <xref:System.Xml.XmlElement>, <xref:System.Xml.XmlNode> 배열, <xref:System.Byte> 배열 또는 계약에서 <xref:System.Runtime.Serialization.ISerializable> 을 구현하는 형식을 사용하지 마십시오.

- <xref:System.Xml.XmlElement>, <xref:System.Xml.XmlNode> 배열, <xref:System.Byte> 배열 또는 알려진 형식 목록에서 <xref:System.Runtime.Serialization.ISerializable> 을 구현하는 형식을 사용하지 마십시오.

위의 주의 사항은 비스트리밍 작업에서 <xref:System.Runtime.Serialization.DataContractSerializer>를 사용하는 경우에 적용됩니다. <xref:System.Xml.Serialization.XmlSerializer>에는 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.MaxItemsInObjectGraph%2A> 할당량을 보호하는 기능이 없기 때문에 이를 사용하는 경우 같은 서비스에서 스트리밍 및 비스트리밍 프로그래밍 모델을 혼합해서는 안 됩니다.

### <a name="slow-stream-attacks"></a>느린 스트림 공격

스트리밍 서비스 거부 공격의 범주에는 메모리 소비가 포함되지 않으며, 대신 느린 데이터 발신자 또는 수신자가 포함됩니다. 데이터를 보내거나 받는 작업을 기다리는 동안 스레드 및 사용 가능한 연결 등의 리소스가 소모됩니다. 이러한 상황은 악의적인 공격의 결과로 발생하거나 올바른 발신자/수신자의 네트워크 연결이 느린 경우 발생할 수 있습니다.

이러한 공격을 완화하려면 전송 시간 제한을 올바르게 설정합니다. 자세한 내용은 [전송 할당량](../../../../docs/framework/wcf/feature-details/transport-quotas.md)합니다. 둘째, 사용 하지 마십시오 동기 `Read` 또는 `Write` WCF의 스트림을 사용 하 여 작업 하는 경우에 작업입니다.

## <a name="using-xml-safely"></a>안전하게 XML 사용

> [!NOTE]
> 이 단원에서는 XML에 대한 내용을 다루지만 이 정보는 JSON(JavaScript Object Notation) 문서에도 적용됩니다. 할당량도 [Mapping Between JSON and XML](../../../../docs/framework/wcf/feature-details/mapping-between-json-and-xml.md)을 사용하여 비슷하게 작동합니다.

### <a name="secure-xml-readers"></a>보안 XML 판독기

XML Infoset WCF의 모든 메시지 처리의 기본을 형성 합니다. 신뢰할 수 없는 소스로부터 XML 데이터를 받을 경우에는 완화해야 할 여러 가지 서비스 거부 공격이 발생할 수 있습니다. WCF는 특수 한 보안 XML 판독기를 제공합니다. 이러한 판독기는 WCF (텍스트, 이진 또는 MTOM)의 표준 인코딩 중 하나를 사용 하는 경우 자동으로 생성 됩니다.

이러한 판독기의 보안 기능 중 일부는 항상 활성화되어 있습니다. 예를 들어, 판독기는 서비스 거부 공격의 소스가 될 가능성이 있으므로 올바른 SOAP 메시지에 표시되어서는 안 되는 DTD(문서 종류 정의)를 처리하지 않습니다. 다른 보안 기능에는 구성해야 할 판독기 할당량이 포함되며, 이에 대해서는 다음 단원에서 설명합니다.

XML 판독기를 사용 하 여 직접 작업 하는 경우 (같은 또는 직접 작업할 때는 사용자 고유의 사용자 지정 인코더를 작성 하는 경우는 <xref:System.ServiceModel.Channels.Message> 클래스)를 항상 WCF 보안 판독기를 사용 하 여 신뢰할 수 없는 데이터로 작업할 가능성이 있는 경우. <xref:System.Xml.XmlDictionaryReader.CreateTextReader%2A>클래스에 있는 <xref:System.Xml.XmlDictionaryReader.CreateBinaryReader%2A>, <xref:System.Xml.XmlDictionaryReader.CreateMtomReader%2A> 또는 <xref:System.Xml.XmlDictionaryReader> 의 정적 팩터리 메서드 오버로드 중 하나를 호출하여 보안 판독기를 만듭니다. 판독기를 만들 때 보안 할당량 값을 전달합니다. `Create` 메서드 오버로드를 호출하지 마십시오. 이러한 WCF 판독기를 만들지 마십시오. 대신 이 단원에서 설명한 보안 기능으로 보호되지 않는 판독기를 만듭니다.

### <a name="reader-quotas"></a>판독기 할당량

보안 XML 판독기에는 5개의 구성 가능한 할당량이 있습니다. 일반적으로 이러한 할당량은 인코딩 바인딩 요소 또는 표준 바인딩에서 `ReaderQuotas` 속성을 사용하거나 판독기를 만들 때 전달된 <xref:System.Xml.XmlDictionaryReaderQuotas> 개체를 사용하여 구성합니다.

#### <a name="maxbytesperread"></a>MaxBytesPerRead

이 할당량은 요소 시작 태그와 해당 특성을 읽을 때 단일 `Read` 작업에서 읽는 바이트 수를 제한합니다. 비스트리밍 작업의 경우 요소 이름 자체는 할당량 계산에서 제외됩니다. <xref:System.Xml.XmlDictionaryReaderQuotas.MaxBytesPerRead%2A> 가 중요한 이유는 다음과 같습니다.

- 요소 이름과 해당 특성은 읽을 때 항상 메모리에 버퍼링됩니다. 따라서 스트리밍이 예상되는 경우에 스트리밍 모드에서 과다한 버퍼링이 일어나는 것을 방지하려면 이 할당량을 올바르게 설정해야 합니다. 발생하는 실제 버퍼링 크기에 대한 자세한 내용은 `MaxDepth` 할당량 단원을 참조하십시오.

- XML 특성이 너무 많으면 특성 이름의 고유성을 확인해야 하기 때문에 처리 시간이 과도하게 오래 걸릴 수 있습니다. `MaxBytesPerRead` 는 이 위협을 완화합니다.

#### <a name="maxdepth"></a>MaxDepth

이 할당량은 XML 요소의 최대 중첩 깊이를 제한합니다. 예를 들어, 문서 "\<는 >\<B >\<C / >\</B > \< /A >"는 중첩 깊이가 3입니다. <xref:System.Xml.XmlDictionaryReaderQuotas.MaxDepth%2A> 가 중요한 이유는 다음과 같습니다.

- `MaxDepth` 는 `MaxBytesPerRead`와 상호 작용합니다. 판독기는 항상 현재 요소와 모든 상위 요소의 데이터를 메모리에 유지하기 때문에 판독기의 최대 메모리 소비량은 이 두 설정을 곱한 값에 비례합니다.

- 여러 층으로 중첩된 개체 그래프를 deserialize할 때 deserializer가 전체 스택에 액세스하여 복구할 수 없는 <xref:System.StackOverflowException>이 throw될 수 있습니다. XML 중첩과 <xref:System.Runtime.Serialization.DataContractSerializer> 및 <xref:System.Xml.Serialization.XmlSerializer>모두의 개체 중첩 사이에는 직접적인 상관 관계가 있습니다. `MaxDepth` 를 사용하면 이 위협을 완화할 수 있습니다.

#### <a name="maxnametablecharcount"></a>MaxNameTableCharCount

이 할당량은 판독기의 *nametable*크기를 제한합니다. nametable에는 XML 문서를 처리할 때 표시되는 특정 문자열(예: 네임스페이스 및 접두사)이 포함됩니다. 이러한 문자열은 메모리에 버퍼링되기 때문에 스트리밍이 예상되는 경우 과도한 버퍼링을 방지하려면 이 할당량을 설정합니다.

#### <a name="maxstringcontentlength"></a>MaxStringContentLength

이 할당량은 XML 판독기에서 반환하는 최대 문자열 크기를 제한합니다. 이 할당량은 XML 판독기 자체에서는 메모리 소비량을 제한하지 않지만 판독기를 사용하는 구성 요소의 메모리 소비량을 제한합니다. 예를 들어, <xref:System.Runtime.Serialization.DataContractSerializer> 가 <xref:System.Xml.XmlDictionaryReaderQuotas.MaxStringContentLength%2A>로 보안이 설정된 판독기를 사용하는 경우에는 이 할당량보다 큰 문자열을 deserialize하지 않습니다. <xref:System.Xml.XmlDictionaryReader> 클래스를 직접 사용할 경우 일부 메서드는 이 할당량을 준수하지 않으며 문자열을 읽도록 특별히 설계된 메서드(예: <xref:System.Xml.XmlDictionaryReader.ReadContentAsString%2A> 메서드)만 이 할당량을 준수합니다. 판독기에 대한 <xref:System.Xml.XmlReader.Value%2A> 속성은 이 할당량의 영향을 받지 않기 때문에 이 할당량이 제공하는 보호가 필요한 경우에는 사용해서는 안 됩니다.

#### <a name="maxarraylength"></a>MaxArrayLength

이 할당량은 바이트 배열을 포함하여 XML 판독기가 반환하는 기본 형식 배열의 최대 크기를 제한합니다. 이 할당량은 XML 판독기 자체의 메모리 소비량은 제한하지 않지만 판독기를 사용하는 모든 구성 요소의 메모리 소비량을 제한합니다. 예를 들어, <xref:System.Runtime.Serialization.DataContractSerializer> 가 <xref:System.Xml.XmlDictionaryReaderQuotas.MaxArrayLength%2A>로 보안이 설정된 판독기를 사용하는 경우에는 이 할당량보다 큰 바이트 배열을 deserialize하지 않습니다. 단일 계약에서 스트리밍 및 버퍼링 프로그래밍 모델을 혼합하려는 경우에는 이 할당량을 설정하는 것이 중요합니다. <xref:System.Xml.XmlDictionaryReader> 클래스를 직접 사용하는 경우에는 특정 기본 형식의 배열을 크기에 관계없이 읽도록 특별히 설계된 메서드(예: <xref:System.Xml.XmlDictionaryReader.ReadInt32Array%2A>)만 이 할당량을 준수합니다.

## <a name="threats-specific-to-the-binary-encoding"></a>이진 인코딩과 관련된 위협

이진 XML 인코딩을 지 원하는 WCF에 포함 되어는 *사전 문자열* 기능입니다. 큰 문자열을 몇 바이트만 사용하여 인코딩할 수 있습니다. 이렇게 하면 성능은 크게 향상되지만 완화해야 할 새로운 서비스 거부 위협이 발생합니다.

사전에는 *정적* 사전과 *동적*사전의 두 가지 종류가 있습니다. 정적 사전은 이진 인코딩에서 짧은 코드로 표현할 수 있는 긴 문자열이 포함된 기본 제공 목록입니다. 이 문자열 목록은 판독기를 만들 때 고정되며 수정할 수 없습니다. 기본적으로 WCF를 사용 하는 정적 사전의 문자열 중는 사전 확장 공격에 여전히 사용 될 수 있지만 한 심각한 서비스 거부 위협을 야기할 정도로 큰 것입니다. 사용자가 직접 정적 사전을 제공하는 고급 시나리오에서 큰 사전 문자열을 사용하는 경우에는 특히 주의해야 합니다.

동적 사전 기능을 통해 메시지에서 직접 문자열을 정의하고 짧은 코드에 연결할 수 있습니다. 문자열과 코드 사이의 이러한 매핑은 그 뒤의 메시지에서 문자열을 다시 보낼 필요 없이 이미 정의된 코드를 활용할 수 있도록 전체 통신 세션 동안 메모리에 보존됩니다. 이러한 문자열의 길이는 임의로 지정되기 때문에 정적 사전에 사용되는 것보다 큰 위협을 야기할 수 있습니다.

완화가 필요한 첫 번째 위협은 동적 사전(문자열과 코드 사이의 매핑 테이블)이 너무 커질 가능성입니다. 이 사전은 여러 메시지에 걸쳐 확장될 수 있기 때문에 각 메시지에만 별도로 적용되는 `MaxReceivedMessageSize` 할당량으로 보호할 수 없습니다. 따라서 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.MaxSessionSize%2A> 에 사전의 크기를 제한하는 별도의 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement> 속성이 존재합니다.

대부분의 다른 할당량과 달리, 이 할당량은 메시지를 쓸 때에도 적용됩니다. 메시지를 읽는 동안 할당량이 초과되면 일반적인 경우와 마찬가지로 `QuotaExceededException` 이 throw됩니다. 메시지를 쓰는 동안 할당량이 초과되면 할당량을 초과하는 모든 문자열은 동적 사전 기능을 사용하지 않고 그대로 작성됩니다.

### <a name="dictionary-expansion-threats"></a>사전 확장 위협

사전 확장으로부터 심각한 이진 관련 공격이 발생할 수 있습니다. 문자열 사전 기능을 본격적으로 사용하는 경우에는 작은 이진 형식이 완전히 확장된 텍스트 형식에서 매우 큰 메시지로 바뀔 수도 있습니다. 동적 사전 문자열의 확장 비율은 동적 사전 문자열이 전체 사전의 최대 크기를 초과하지 않도록 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.MaxSessionSize%2A> 할당량에 의해 제한됩니다.

<xref:System.Xml.XmlDictionaryReaderQuotas.MaxNameTableCharCount%2A>, `MaxStringContentLength`및 `MaxArrayLength` 속성은 메모리 소비만 제한합니다. 보통은 메모리 사용이 이미 `MaxReceivedMessageSize`에 의해 제한되기 때문에 스트리밍을 사용하지 않는 경우 따로 위협을 완화할 필요가 없습니다. 그러나 `MaxReceivedMessageSize` 에서는 확장 전의 바이트 수를 계산합니다. 이진 인코딩을 사용할 때 메모리 소비는 `MaxReceivedMessageSize`를 초과할 수 있으며 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.MaxSessionSize%2A>비율로만 제한됩니다. 따라서 이진 인코딩을 사용하는 경우에는 항상 모든 판독기 할당량(특히 <xref:System.Xml.XmlDictionaryReaderQuotas.MaxStringContentLength%2A>)을 설정하는 것이 중요합니다.

이진 인코딩을 <xref:System.Runtime.Serialization.DataContractSerializer>와 함께 사용할 때 `IExtensibleDataObject` 인터페이스를 사전 확장 공격에 악용할 수 있습니다. 이 인터페이스는 기본적으로 계약에 속해 있지 않은 임의의 데이터에 무제한의 스토리지를 제공합니다. `MaxSessionSize` 와 `MaxReceivedMessageSize` 를 곱한 값이 문제를 야기하지 않을 정도로 낮은 할당량을 설정한 경우에는 이진 인코딩을 사용할 때 `IExtensibleDataObject` 기능을 비활성화합니다. `IgnoreExtensionDataObject` 특성에서 `true` 속성을 `ServiceBehaviorAttribute` 로 설정합니다. 또는 `IExtensibleDataObject` 인터페이스를 구현하지 않습니다. 자세한 내용은 [호환 가능한 데이터 계약](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)을 참조하세요.

### <a name="quotas-summary"></a>할당량 요약

다음 표에는 할당량에 대한 지침이 요약되어 있습니다.

|조건|설정할 중요 할당량|
|---------------|-----------------------------|
|스트리밍 없음이나 작은 메시지 스트리밍, 텍스트 또는 MTOM 인코딩|`MaxReceivedMessageSize`, `MaxBytesPerRead`및 `MaxDepth`|
|스트리밍 없음이나 작은 메시지 스트리밍, 이진 인코딩|`MaxReceivedMessageSize`, `MaxSessionSize`및 모든 `ReaderQuotas`|
|큰 메시지 스트리밍, 텍스트 또는 MTOM 인코딩|`MaxBufferSize` 및 모든 `ReaderQuotas`|
|큰 메시지 스트리밍, 이진 인코딩|`MaxBufferSize`, `MaxSessionSize`및 모든 `ReaderQuotas`|

- 스트리밍을 사용하는 경우에는 큰 메시지나 작은 메시지를 스트리밍하는지에 관계없이 항상 전송 수준 시간 제한을 설정하고 동시 읽기/쓰기를 사용하지 말아야 합니다.

- 할당량을 정하기 어려울 때는 개방적으로 놓아두지 말고 안전한 값을 설정하십시오.

## <a name="preventing-malicious-code-execution"></a>악의적인 코드 실행 방지

다음 일반 위협 클래스에서는 코드를 실행하여 의도하지 않은 결과를 일으킬 수 있습니다.

- deserializer가 악의적이거나, 안전하지 않거나, 보안과 관련된 형식을 로드합니다.

- 들어오는 메시지에서는 deserializer에 대해 일반적으로는 안전한 형식의 인스턴스가 의도하지 않은 결과를 일으키도록 구성합니다.

다음 단원에서는 이러한 위협에 대해 자세히 설명합니다.

## <a name="datacontractserializer"></a>DataContractSerializer

<xref:System.Xml.Serialization.XmlSerializer>에 대한 보안 정보는 관련 설명서를 참조하십시오. <xref:System.Xml.Serialization.XmlSerializer>의 보안 모델은 <xref:System.Runtime.Serialization.DataContractSerializer>의 경우와 비슷하며 세부 내용에서만 주로 다릅니다. 예를 들어, <xref:System.Xml.Serialization.XmlIncludeAttribute> 특성은 <xref:System.Runtime.Serialization.KnownTypeAttribute> 특성 대신 형식 포함에 사용됩니다. 그러나 <xref:System.Xml.Serialization.XmlSerializer> 의 고유한 위협 몇 가지에 대해서는 이 항목의 뒷부분에서 설명합니다.

### <a name="preventing-unintended-types-from-being-loaded"></a>의도하지 않은 형식이 로드되는 것을 방지

형식이 악의적이든, 보안 관련 부작용이 있을 뿐이든지에 관계없이 의도하지 않은 형식을 로드하면 심각한 결과가 발생할 수 있습니다. 형식에 악용할 수 있는 보안 취약성이 포함되어 있거나, 생성자 또는 클래스 생성자에서 보안 관련 작업을 수행하거나, 메모리 사용량이 커서 서비스 거부 공격을 일으키거나, 복구할 수 없는 예외를 throw할 수도 있습니다. 형식에는 형식이 로드되면 인스턴스가 만들어지기 전에 바로 실행되는 클래스 생성자가 있을 수 있습니다. 그렇기 때문에 deserializer에서 로드할 수 있는 형식 집합을 제어하는 것이 중요합니다.

<xref:System.Runtime.Serialization.DataContractSerializer> 는 느슨하게 결합된 방식으로 deserialize됩니다. 여기서는 들어오는 데이터로부터 CLR(공용 언어 런타임) 형식과 어셈블리 이름을 읽지 않습니다. 이는 <xref:System.Xml.Serialization.XmlSerializer>의 동작과 비슷하지만 <xref:System.Runtime.Serialization.NetDataContractSerializer>, <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>및 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>의 동작과는 다릅니다. 느슨한 결합에서는 원격 공격자가 임의의 형식을 이용하여 메시지에 형식 이름을 지정하는 것만으로 로드되도록 할 수 없기 때문에 어느 정도 안전을 강화할 수 있습니다.

<xref:System.Runtime.Serialization.DataContractSerializer> 에서는 항상 현재 계약에 따라 예상되는 형식을 로드할 수 있습니다. 예를 들어, 데이터 계약에 `Customer`형식의 데이터 멤버가 있으면 <xref:System.Runtime.Serialization.DataContractSerializer> 에서 이 데이터 멤버를 deserialize할 때 `Customer` 형식을 로드할 수 있습니다.

또한 <xref:System.Runtime.Serialization.DataContractSerializer> 에서는 다형성을 지원합니다. 데이터 멤버를 <xref:System.Object>로 선언할 수 있지만 들어오는 데이터에 `Customer` 인스턴스가 포함될 수도 있습니다. 이는 다음 메커니즘 중 하나를 통해 deserializer에 `Customer` 형식이 "알려진" 경우에만 가능합니다.

- 형식에 적용되는<xref:System.Runtime.Serialization.KnownTypeAttribute> 특성.

- 형식 목록을 반환하는 메서드를 지정하는 `KnownTypeAttribute` 특성.

- `ServiceKnownTypeAttribute` 특성.

- `KnownTypes` 구성 섹션.

- serializer를 직접 사용하는 경우에는 알려진 형식 목록이 생성 중에 <xref:System.Runtime.Serialization.DataContractSerializer> 에 명시적으로 전달됩니다.

이러한 각 메커니즘은 deserializer에서 로드할 수 있는 형식을 더 추가하여 노출 영역을 넓힙니다. 알려진 형식 목록에 악의적이거나 의도하지 않은 형식이 추가되지 않도록 이러한 각각의 메커니즘을 제어해야 합니다.

알려진 형식이 범위 내에 있으면 계약에서 실제로 사용이 금지되어 있는 경우에도 언제든지 로드하고 형식의 인스턴스를 만들 수 있습니다. 예를 들어, 위 메커니즘 중 하나를 사용하여 알려진 형식 목록에 "MyDangerousType" 형식을 추가하는 경우를 가정할 수 있습니다. 이는 다음을 의미합니다.

- `MyDangerousType` 이 로드되고 클래스 생성자가 실행됩니다.

- 문자열 데이터 멤버가 있는 데이터 계약을 deserialize하는 경우에도 악의적인 메시지로 인해 `MyDangerousType` 인스턴스가 만들어질 수 있습니다. 속성 setter와 같은 `MyDangerousType`내의 코드가 실행될 수 있습니다. 그러고 나면 deserializer에서 이 인스턴스를 문자열 데이터 멤버에 할당하려고 하고 실패하며 예외를 일으킵니다.

알려진 형식 목록을 반환하는 메서드를 쓰거나 <xref:System.Runtime.Serialization.DataContractSerializer> 생성자에 직접 목록을 전달할 때는 목록을 준비하는 코드가 안전하며 신뢰할 수 있는 데이터만 다루는지 확인해야 합니다.

구성에 알려진 형식을 지정하는 경우에는 구성 파일이 안전한지 확인해야 합니다. 구성에는 항상 강력한 이름을 사용하되(형식이 상주하는 서명된 어셈블리의 공개 키 지정) 로드할 형식의 버전은 지정하지 마십시오. 가능한 경우에는 형식 로더에서 자동으로 최신 버전을 선택합니다. 구성에서 특정 버전을 지정 하는 경우 다음 위험이 실행 합니다. 형식 수 이후 버전에서 해결 될 수 있는 보안 취약점이 있지만 구성에서 명시적으로 지정 되어 있으므로 여전히 취약 한 버전 로드 합니다.

알려진 형식이 너무 많은 다른 결과 있습니다. <xref:System.Runtime.Serialization.DataContractSerializer> serialize 하며 deserialize 각 형식에 대 한 진입점을 사용 하 여 응용 프로그램 도메인에서 serialization/deserialization 코드의 캐시를 만듭니다. 애플리케이션 도메인이 실행되고 있는 동안에는 이 캐시를 결코 지울 수 없습니다. 따라서 애플리케이션에 사용되는 알려진 형식이 많다는 것을 알고 있는 공격자는 이 모든 형식을 deserialize하여 캐시에 과도한 메모리가 사용되게 만들 수 있습니다.

### <a name="preventing-types-from-being-in-an-unintended-state"></a>형식이 의도하지 않은 상태가 되는 것을 방지

형식에 적용해야 할 내부 일관성 제약 조건이 있을 수 있습니다. deserialization 중에 이러한 제약 조건을 무시하지 않도록 주의해야 합니다.

다음 형식 예는 우주선의 기밀식 출입구 상태를 나타내며 안쪽 문과 바깥쪽 문을 동시에 열어 둘 수 없다는 제약 조건을 적용합니다.

[!code-csharp[DataContractAttribute#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/datacontractattribute/cs/overview.cs#3)]
[!code-vb[DataContractAttribute#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/datacontractattribute/vb/overview.vb#3)]

공격자는 이와 같이 악의적인 메시지를 보내서 제약 조건을 피해 개체를 잘못된 상태가 되도록 할 수 있으며 이로 인해 의도하지 않은 예기치 못한 결과가 발생할 수 있습니다.

```xml
<SpaceStationAirlock>
    <innerDoorOpen>true</innerDoorOpen>
    <outerDoorOpen>true</outerDoorOpen>
</SpaceStationAirlock>
```

다음과 같은 사항에 주의하면 이러한 상황을 피할 수 있습니다.

- <xref:System.Runtime.Serialization.DataContractSerializer> 에서 대부분의 클래스를 deserialize할 때는 생성자가 실행되지 않습니다. 따라서 생성자에서 수행하는 상태 관리를 사용하지 마십시오.

- 콜백을 사용하여 개체가 유효한 상태에 있는지 확인합니다. <xref:System.Runtime.Serialization.OnDeserializedAttribute> 특성으로 표시된 콜백은 deserialization이 완료된 후에 실행되며 전체 상태를 확인하고 수정할 수 있기 때문에 특히 유용합니다. 자세한 내용은 [버전 독립적 Serialization 콜백](../../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md)합니다.

- 속성 setter의 특정 호출 순서를 사용하도록 데이터 계약 형식을 디자인하지 마십시오.

- <xref:System.SerializableAttribute> 특성으로 표시된 레거시 형식은 주의해서 사용해야 합니다. 이들 중 다 수는 신뢰할 수 있는 데이터만 사용에 대 한.NET Framework remoting과 함께 작동 하도록 설계 되었습니다. 이 특성으로 표시된 기존 형식은 상태 안전을 고려하지 않은 디자인일 가능성이 있습니다.

- 상태 안전에 관해서는 데이터의 존재를 보장하기 위해 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 특성의 <xref:System.Runtime.Serialization.DataMemberAttribute> 속성을 사용하지 마십시오. 데이터는 항상 `null`, `zero` 또는 `invalid`일 수 있습니다.

- 신뢰할 수 없는 데이터 소스에서 deserialize된 개체 그래프를 먼저 검사하지 않고 신뢰해서는 안 됩니다. 각 개체의 상태가 일관되어도 개체 그래프 전체는 그렇지 않을 수 있습니다. 또한 개체 그래프 유지 모드가 사용하지 않도록 설정되어 있더라도 deserialize된 그래프에 같은 개체에 대한 참조가 여러 개 있거나 순환 참조가 있을 수 있습니다. 자세한 내용은 [Serialization 및 Deserialization](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md)합니다.

### <a name="using-the-netdatacontractserializer-securely"></a>안전한 NetDataContractSerializer 사용

<xref:System.Runtime.Serialization.NetDataContractSerializer> 는 형식에 대한 밀접한 결합을 사용하는 serialization 엔진입니다. 이는 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 및 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>와 비슷합니다. 즉, 들어오는 데이터에서.NET Framework 어셈블리 및 형식 이름을 읽어 인스턴스화할 형식을 결정 합니다. 이 serialization 엔진;에서 연결의 제공 된 방법이 없기 WCF의 일부는 아니지만 사용자 지정 코드를 작성 해야 합니다. `NetDataContractSerializer` .NET Framework remoting에서 WCF로의 마이그레이션을 용이 하 게 기본적으로 제공 됩니다. 자세한 내용은의 관련 섹션을 참조 하세요 [Serialization 및 Deserialization](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md)합니다.

메시지 자체에서 로드할 형식을 지정할 수 있기 때문에 <xref:System.Runtime.Serialization.NetDataContractSerializer> 메커니즘은 본질적으로 안전하지 않으며 신뢰할 수 있는 데이터에만 사용해야 합니다. 형식을 제한하는 안전한 형식 바인더를 작성하여 안전한 형식만 로드할 수도 있습니다( <xref:System.Runtime.Serialization.NetDataContractSerializer.Binder%2A> 속성 사용).

신뢰할 수 있는 데이터와 함께 사용하는 경우라도, 들어오는 데이터에서 로드할 형식을 불충분하게 지정할 수가 있습니다. 특히 <xref:System.Runtime.Serialization.NetDataContractSerializer.AssemblyFormat%2A> 속성이 <xref:System.Runtime.Serialization.Formatters.FormatterAssemblyStyle.Simple>로 설정되어 있으면 더욱 그렇습니다. 애플리케이션의 디렉터리나 전역 어셈블리 캐시에 액세스할 수 있는 사람은 로드할 형식을 악의적인 형식으로 대체할 수 있습니다. 사용 권한을 올바르게 설정하여 항상 애플리케이션 디렉터리와 전역 어셈블리 캐시의 보안을 보장해야 합니다.

일반적으로 부분적으로 신뢰할 수 있는 코드에서 `NetDataContractSerializer` 인스턴스에 액세스하거나 그 외의 방식으로 서로게이트 선택기(<xref:System.Runtime.Serialization.ISurrogateSelector>) 또는 serialization 바인더(<xref:System.Runtime.Serialization.SerializationBinder>)를 제어하는 경우 코드에서 serialization/deserialization 프로세스를 상당 부분 제어할 수 있습니다. 예를 들어 임의의 형식을 삽입하거나, 정보 노출을 일으키거나, 결과 개체 그래프 또는 serialize된 데이터를 변조하거나, 결과적으로 serialize된 스트림을 오버플로시킬 수 있습니다.

`NetDataContractSerializer` 와 관련된 다른 보안 문제는 악의적인 코드 실행 위협이 아닌 서비스 거부입니다. `NetDataContractSerializer`를 사용할 때는 항상 <xref:System.Runtime.Serialization.NetDataContractSerializer.MaxItemsInObjectGraph%2A> 할당량을 안전한 값으로 설정해야 합니다. 크기가 이 할당량에 의해서만 제한되는 개체 배열을 할당하는, 작은 악의적인 메시지를 쉽게 작성할 수 있습니다.

### <a name="xmlserializer-specific-threats"></a>XmlSerializer 관련 위협

<xref:System.Xml.Serialization.XmlSerializer> 보안 모델은 <xref:System.Runtime.Serialization.DataContractSerializer>의 경우와 비슷합니다. 그러나 <xref:System.Xml.Serialization.XmlSerializer>에 고유하게 나타나는 위협도 있습니다.

<xref:System.Xml.Serialization.XmlSerializer> 에서는 런타임에 실제로 serialize 및 deserialize를 수행하는 *serialization 어셈블리* 를 생성하며 이러한 어셈블리는 임시 파일 디렉터리에 생성됩니다. 다른 프로세스 또는 사용자에게 해당 디렉터리에 대한 권한이 있는 경우에는 serialization/deserialization 코드를 임의의 코드로 덮어쓸 수도 있습니다. 그러면 <xref:System.Xml.Serialization.XmlSerializer> 에서 serialization/deserialization 코드 대신 보안 컨텍스트를 사용하여 이 코드를 실행합니다. 이 문제를 방지하려면 임시 파일 디렉터리에서 사용 권한이 올바르게 설정되었는지 확인해야 합니다.

<xref:System.Xml.Serialization.XmlSerializer> 에는 실행 시에 새로 생성하는 대신 미리 생성된 serialization 어셈블리를 사용하는 모드가 있습니다. 이 모드는 <xref:System.Xml.Serialization.XmlSerializer> 에서 적절한 serialization 어셈블리를 찾을 수 있을 때마다 트리거됩니다. <xref:System.Xml.Serialization.XmlSerializer> 에서는 serialize할 형식이 포함된 어셈블리에 사용된 것과 같은 키를 사용하여 serialization 어셈블리가 서명되었는지 확인합니다. 그러면 악의적인 어셈블리가 serialization 어셈블리로 위장하는 것을 방지할 수 있습니다. 그러나 serialize 가능 형식이 포함된 어셈블리가 서명되지 않은 경우에는 <xref:System.Xml.Serialization.XmlSerializer> 에서 이 확인을 수행할 수 없으며 이름만 정확하면 지정된 어셈블리를 그냥 사용합니다. 그러면 악의적인 코드를 실행할 수 있습니다. serialize 가능한 형식이 포함된 어셈블리에 항상 서명을 하거나 애플리케이션의 디렉터리 및 전역 어셈블리 캐시에 대한 액세스를 엄격하게 제어하여 악의적인 어셈블리가 들어오는 것을 막아야 합니다.

<xref:System.Xml.Serialization.XmlSerializer> 는 서비스 거부 공격을 받을 수 있습니다. <xref:System.Xml.Serialization.XmlSerializer> 에는 `MaxItemsInObjectGraph` 에서 사용할 수 있는 것과 같은 <xref:System.Runtime.Serialization.DataContractSerializer>할당량이 없습니다. 따라서 오로지 메시지 크기로만 제어되는 임의 개수의 개체를 deserialize합니다.

### <a name="partial-trust-threats"></a>부분 신뢰 위협

부분 신뢰로 실행되는 코드와 관련된 위협에 대해 다음 사항을 고려해야 합니다. 이러한 위협에는 부분적으로 신뢰할 수 있는 악의적인 코드, 그리고 다른 공격 시나리오와 결합된 부분적으로 신뢰할 수 있는 악의적인 코드(예: 특정 문자열을 생성한 다음 deserialize하는 부분 신뢰 코드)가 포함됩니다.

- serialization 구성 요소를 사용할 때는 serialization 시나리오 전체가 어설션 범위 내에 있고 신뢰할 수 없는 데이터나 개체를 처리하지 않는 경우에도 이러한 식의 사용 전에 권한을 어설션하면 안 됩니다. 보안 취약성으로 이어질 수 있기 때문입니다.

- 부분적으로 신뢰할 수 있는 코드에서 확장 지점(서로게이트), serialize되는 형식 또는 기타 방법을 통해 프로세스를 제어하는 경우, 부분 신뢰된 코드는 serializer에서 대량의 데이터를 serialize된 스트림으로 출력하여 이 스트림의 수신자에게 DoS(서비스 거부)를 일으킬 수 있습니다. DoS 위협에 민감한 대상의 데이터를 serialize하는 경우에는 부분적으로 신뢰할 수 있는 형식을 serialize하거나 기타 방식으로 부분적으로 신뢰할 수 있는 형식의 serialization 제어를 허용하지 말아야 합니다.

- 부분적으로 신뢰할 수 있는 코드에 대 한 액세스를 허용 하는 경우에 <xref:System.Runtime.Serialization.DataContractSerializer> 인스턴스이거나 제어할 합니다 [데이터 계약 서로게이트](../../../../docs/framework/wcf/extending/data-contract-surrogates.md), 다양 한 serialization/deserialization 프로세스에 대 한 제어를 행사할 수 있습니다. 예를 들어 임의의 형식을 삽입하거나, 정보 노출을 일으키거나, 결과 개체 그래프 또는 serialize된 데이터를 변조하거나, 결과적으로 serialize된 스트림을 오버플로시킬 수 있습니다. 이에 해당하는 <xref:System.Runtime.Serialization.NetDataContractSerializer> 위협에 대한 설명은 "안전한 NetDataContractSerializer 사용" 단원을 참조하십시오.

- <xref:System.Runtime.Serialization.DataContractAttribute> 특성이 형식(또는 <xref:System.SerializableAttribute> 로 표시되어 있지만 <xref:System.Runtime.Serialization.ISerializable>이 아닌 형식)에 적용되면 deserializer에서는 모든 생성자가 public이 아니거나 요청에 의해 보호되지 않더라도 이러한 형식의 인스턴스를 만들 수 있습니다.

- deserialize된 데이터가 신뢰되었고 알려진 모든 형식이 신뢰할 수 있는 형식인 것이 확실한 경우가 아니면 deserialization 결과를 신뢰하지 마십시오. 부분 신뢰에서 실행되는 경우에는 알려진 형식이 애플리케이션 구성 파일에서 로드되지 않지만 컴퓨터 구성 파일에서는 로드됩니다.

- 서로게이트가 추가된 <xref:System.Runtime.Serialization.DataContractSerializer> 인스턴스를 부분적으로 신뢰할 수 있는 코드에 전달하면 코드에서 서로게이트의 수정 가능한 설정을 변경할 수 있습니다.

- deserialize된 개체의 경우 XML 판독기나 그 내부의 데이터가 부분적으로 신뢰할 수 있는 코드에서 왔으면 deserialize된 결과 개체를 신뢰할 수 없는 데이터와 마찬가지로 취급해야 합니다.

- <xref:System.Runtime.Serialization.ExtensionDataObject> 형식에 공개 멤버가 없다고 해서 그 내부의 데이터가 안전한 것은 아닙니다. 예를 들어, 권한이 있는 데이터 소스에서 일부 데이터가 들어 있는 개체로 deserialize한 다음 해당 개체를 부분적으로 신뢰할 수 있는 코드로 전달하면 부분적으로 신뢰할 수 있는 코드에서 개체를 serialize하여 `ExtensionDataObject` 에서 데이터를 읽을 수 있습니다. 권한이 있는 데이터 소스에서 나중에 부분적으로 신뢰할 수 있는 코드로 전달할 개체로 deserialize하는 경우에는 <xref:System.Runtime.Serialization.DataContractSerializer.IgnoreExtensionDataObject%2A> 를 `true` 로 설정하는 것이 좋습니다.

- <xref:System.Runtime.Serialization.DataContractSerializer> 및 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 는 완전 신뢰로 private, protected, internal 및 public 멤버의 serialization을 지원합니다. 그러나 부분 신뢰에서는 public 멤버만 serialize될 수 있습니다. 애플리케이션에서 public 멤버가 아닌 멤버를 serialize하려고 하면 <xref:System.Security.SecurityException> 이 throw됩니다.

    부분 신뢰에서 internal 또는 protected internal 멤버가 serialize될 수 있도록 허용하려면 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 어셈블리 특성을 사용합니다. 이 특성을 사용하면 어셈블리에서 internal 멤버가 일부 다른 어셈블리에 표시되도록 선언할 수 있습니다. 이 경우 internal 멤버가 serialize되도록 하려는 어셈블리는 internal 멤버가 System.Runtime.Serialization.dll에 표시되도록 선언합니다.

    이 방법의 장점은 상승된 코드 생성 경로가 필요하지 않다는 것입니다.

    이와 동시에 두 가지 주요 단점이 있습니다.

    첫 번째 단점은 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 특성의 선택 속성이 어셈블리 수준이라는 것입니다. 즉, 특정 클래스만 internal 멤버가 serialize되도록 지정할 수는 없습니다. 물론 <xref:System.Runtime.Serialization.DataMemberAttribute> 특성을 특정 internal 멤버에 추가하지 않는 방법으로 해당 멤버를 serialize하지 않도록 선택할 수 있습니다. 이와 마찬가지로 개발자는 약간의 표시 문제가 있지만 멤버를 private 또는 protected 대신 internal로 만들도록 선택할 수도 있습니다.

    두 번째 단점은 여전히 private 또는 protected 멤버를 지원하지 않는다는 것입니다.

    부분 신뢰에서 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 특성의 사용을 보려면 다음 프로그램을 사용해 보십시오.

    [!code-csharp[CDF_WCF_SecurityConsiderationsForData#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/cdf_wcf_securityconsiderationsfordata/cs/program.cs#1)]

    위의 예제에서 `PermissionsHelper.InternetZone` 은 부분 신뢰의 <xref:System.Security.PermissionSet> 에 해당합니다. 이제 없이 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 특성을 응용 프로그램은 실패를 throw 한 <xref:System.Security.SecurityException> 나타내는 public이 아닌 멤버가 부분 신뢰에서 직렬화 할 수 없습니다.

    그러나 다음 줄을 소스 파일에 추가하면 프로그램이 성공적으로 실행됩니다.

    [!code-csharp[CDF_WCF_SecurityConsiderationsForData#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/cdf_wcf_securityconsiderationsfordata/cs/program.cs#2)]

## <a name="other-state-management-concerns"></a>기타 상태 관리 고려 사항

개체 상태 관리에 대해 설명이 필요한 고려 사항이 몇 가지 더 있습니다.

- 스트리밍 전송에서 스트림 기반의 프로그래밍 모델을 사용할 때 메시지 처리는 메시지가 도착하는 즉시 이루어집니다. 메시지 발신자가 스트리밍 도중에 콘텐츠가 더 예상되는 상황에서 보내기 작업을 중단하면 코드는 예측할 수 없는 상태가 될 수 있습니다. 일반적으로 스트림이 완전할 것으로 기대하지 말고 스트림 기반 작업에서 스트림이 중단된 경우에 복원할 수 없는 작업은 수행하지 마십시오. 스트리밍 본문 뒤의 메시지 형식이 잘못된 경우에도 마찬가지입니다. SOAP 봉투의 끝 태그가 없거나 두 번째 메시지 본문이 있는 경우를 예로 들 수 있습니다.

- `IExtensibleDataObject` 기능을 사용하면 중요한 데이터가 공개될 수 있습니다. `IExtensibleObjectData` 를 통해 신뢰할 수 없는 소스에서 데이터 계약으로 데이터를 받아들이고 나중에 메시지가 서명되는 보안 채널을 통해 해당 데이터를 다시 내보내면 전혀 알지 못하는 데이터를 보증하게 될 수 있습니다. 또한 알려진 데이터와 알려지지 않은 데이터를 모두 고려하면 보내는 전반적인 상태가 잘못될 수도 있습니다. 확장 데이터 속성을 선택적으로 `null` 로 설정하거나 `IExtensibleObjectData` 기능을 선택적으로 비활성화하여 이러한 상황을 방지할 수 있습니다.

## <a name="schema-import"></a>스키마 가져오기

일반적으로 스키마를 가져와서 형식을 생성하는 과정은 웹 서비스에서 [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 를 사용하여 클라이언트 클래스를 생성할 때와 같이 디자인할 때만 발생합니다. 그러나 보다 고급 시나리오에서는 런타임에 스키마를 처리할 수도 있습니다. 이 경우 서비스 거부 위험에 노출될 수 있습니다. 일부 스키마는 가져오는 데 시간이 오래 걸릴 수 있습니다. 신뢰할 수 없는 소스에서 스키마가 들어올 가능성이 있는 경우에는 이러한 시나리오에서 <xref:System.Xml.Serialization.XmlSerializer> 스키마 가져오기 구성 요소를 사용하지 마십시오.

## <a name="threats-specific-to-aspnet-ajax-integration"></a>ASP.NET AJAX 통합과 관련된 위협

구현 하는 경우 <xref:System.ServiceModel.Description.WebScriptEnablingBehavior> 또는 <xref:System.ServiceModel.Description.WebHttpBehavior>, WCF는 XML 및 JSON 메시지를 수락할 수 있는 끝점을 노출 합니다. 그러나 XML 판독기와 JSON 판독기에서 모두 사용하는 판독기 할당량 집합은 하나밖에 없습니다. 일부 할당량 설정은 이 중 하나의 판독기에는 적합하지만 다른 판독기에는 너무 클 수 있습니다.

`WebScriptEnablingBehavior`를 구현할 때 사용자는 엔드포인트에서 JavaScript 프록시를 노출할 수 있습니다. 다음과 같은 보안 문제를 고려해야 합니다.

- JavaScript 프록시를 검사하여 서비스에 대한 정보(작업 이름, 매개 변수 이름 등)를 가져올 수 있습니다.

- JavaScript 엔드포인트를 사용하는 경우 중요한 정보와 개인 정보를 클라이언트 웹 브라우저 캐시에 보존할 수 있습니다.

## <a name="a-note-on-components"></a>구성 요소 참조

WCF는 유연 하 게 사용자 시스템입니다. 이 항목의 내용 중 대부분은 가장 일반적인 WCF 사용 시나리오에 집중합니다. 그러나 WCF는 다양 한 방법으로 제공 하는 구성 요소를 작성 하는 것이 같습니다. 이러한 구성 요소를 사용하는 경우의 보안 영향에 대해 알아야 합니다. 특히 다음과 같습니다.

- XML 판독기를 사용해야 하는 경우에는 다른 판독기 대신 <xref:System.Xml.XmlDictionaryReader> 클래스에서 제공하는 판독기를 사용합니다. 안전한 판독기는 <xref:System.Xml.XmlDictionaryReader.CreateTextReader%2A>, <xref:System.Xml.XmlDictionaryReader.CreateBinaryReader%2A>또는 <xref:System.Xml.XmlDictionaryReader.CreateMtomReader%2A> 메서드를 사용하여 만들어집니다. <xref:System.Xml.XmlReader.Create%2A> 메서드를 사용하지 마십시오. 판독기는 항상 안전한 할당량으로 구성해야 합니다. Wcf에서 serialization 엔진은 WCF에서 보안 XML 판독기를 사용 하는 경우에 안전 합니다.

- <xref:System.Runtime.Serialization.DataContractSerializer> 를 사용하여 신뢰할 수 없는 데이터를 deserialize할 때는 항상 <xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A> 속성을 설정해야 합니다.

- 메시지를 만들 때 `maxSizeOfHeaders`에서 제공하는 보호가 충분하지 않은 경우에는 `MaxReceivedMessageSize` 매개 변수를 설정합니다.

- 인코더를 만들 때는 항상 `MaxSessionSize` 및 `MaxBufferSize`등의 관련 할당량을 구성합니다.

- XPath 메시지 필터를 사용할 때는 <xref:System.ServiceModel.Dispatcher.XPathMessageFilter.NodeQuota%2A> 를 설정하여 필터에서 방문하는 XML 노드의 수를 제한합니다. 여러 노드를 방문하지 않으면 컴퓨팅 시간이 오래 걸리는 XPath 식은 사용하지 마십시오.

- 일반적으로 할당량을 수락하는 구성 요소를 사용하는 경우에는 보안상의 영향을 이해하고 안전한 값으로 설정해야 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Xml.XmlDictionaryReader>
- <xref:System.Xml.Serialization.XmlSerializer>
- [데이터 계약 알려진 형식](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)
