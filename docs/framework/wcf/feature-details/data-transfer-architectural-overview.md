---
title: 데이터 전송 아키텍처 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data transfer [WCF], architectural overview
ms.assetid: 343c2ca2-af53-4936-a28c-c186b3524ee9
ms.openlocfilehash: 2b3d35a959c91bf82d5661f328353cedefe663f6
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963246"
---
# <a name="data-transfer-architectural-overview"></a>데이터 전송 아키텍처 개요
WCF (Windows Communication Foundation)는 메시징 인프라로 간주할 수 있습니다. WCF는 메시지를 받고, 처리하고, 추가 작업을 위해 사용자 코드로 디스패치하거나, 사용자 코드에서 제공된 데이터로부터 메시지를 생성하고 이 메시지를 대상에 전달할 수 있습니다. 고급 개발자를 대상으로 한 이 항목에서는 메시지 및 포함된 데이터를 처리하기 위한 아키텍처에 대해 설명합니다. 데이터를 주고 받는 방법을 보다 간단하게, 작업에 초점을 두고 설명하는 내용은 [Specifying Data Transfer in Service Contracts](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)을 참조하십시오.  
  
> [!NOTE]
> 이 항목에서는 WCF 개체 모델을 검사 하 여 표시 되지 않는 WCF 구현 세부 정보에 대해 설명 합니다. 문서화된 구현 세부 정보와 관련하여 두 가지 주의해야 할 점이 있습니다. 첫째, 설명은 간결하지만 실제 구현은 최적화 또는 다른 이유로 인해 훨씬 복잡할 수 있습니다. 둘째, 문서화된 사항을 비롯한 특정 구현 세부 정보에 의존해서는 안 됩니다. 이러한 사항은 버전이 변경되는 경우 또는 서비스 릴리스에서 예고 없이 변경될 수 있기 때문입니다.  
  
## <a name="basic-architecture"></a>기본 아키텍처  
 WCF 메시지 처리 기능의 <xref:System.ServiceModel.Channels.Message> 핵심은 [메시지 클래스 사용](../../../../docs/framework/wcf/feature-details/using-the-message-class.md)에서 자세히 설명 하는 클래스입니다. WCF의 런타임 구성 요소는 두 가지 주요 부분으로 나눌 수 있습니다. 즉, <xref:System.ServiceModel.Channels.Message> 채널 스택과 서비스 프레임 워크는 클래스가 연결 지점입니다.  
  
 채널 스택은 유효한 <xref:System.ServiceModel.Channels.Message> 인스턴스와 메시지 데이터를 주고받는 일부 동작 간의 변환을 담당합니다. 보내는 쪽에서는 채널 스택이 유효한 <xref:System.ServiceModel.Channels.Message> 인스턴스를 사용하고, 처리를 수행한 다음 논리적으로 메시지 보내기에 해당하는 동작을 수행합니다. 이러한 동작은 구현에 따라 TCP 또는 HTTP 패킷 보내기, 메시지 큐에서 메시지 대기시키기, 메시지를 데이터베이스에 쓰기, 파일 공유를 위해 메시지 저장하기 또는 기타 동작이 될 수 있습니다. 가장 일반적인 동작은 네트워크 프로토콜을 통해 메시지를 보내는 것입니다. 받는 쪽에서는 이와 반대의 작업을 수행합니다. 동작(TCP 또는 HTTP 패킷의 도착 또는 기타 동작)을 감지하면 처리를 수행한 다음 채널 스택에서 이 동작을 유효한 <xref:System.ServiceModel.Channels.Message> 인스턴스로 변환합니다.  
  
 <xref:System.ServiceModel.Channels.Message> 클래스 및 채널 스택을 직접 사용 하 여 WCF를 사용할 수 있습니다. 그러나 이 방법은 어렵고 시간이 많이 걸립니다. 또한이 방법 <xref:System.ServiceModel.Channels.Message> 으로 wcf를 사용 하는 경우 개체는 메타 데이터 지원을 제공 하지 않으므로 강력한 형식의 wcf 클라이언트를 생성할 수 없습니다.  
  
 따라서 WCF에는 개체를 생성 하 고 받는 `Message` 데 사용할 수 있는 사용 하기 쉬운 프로그래밍 모델을 제공 하는 서비스 프레임 워크가 포함 되어 있습니다. 서비스 프레임 워크는 서비스 계약의 개념을 통해 서비스를 .NET Framework 형식으로 매핑하고, <xref:System.ServiceModel.OperationContractAttribute> 특성으로 표시 된 메서드만 .NET Framework 사용자 작업으로 메시지를 디스패치합니다. 자세한 내용은 [디자인을 참조 하세요. 서비스 계약](../../../../docs/framework/wcf/designing-service-contracts.md)). 이러한 메서드에는 매개 변수와 반환 값이 있을 수 있습니다. 서비스 쪽에서는 서비스 프레임워크가 들어오는 <xref:System.ServiceModel.Channels.Message> 인스턴스를 매개 변수로 변환하고, 반환 값을 나가는 <xref:System.ServiceModel.Channels.Message> 인스턴스로 변환합니다. 클라이언트 쪽에서는 반대로 수행됩니다. 예를 들어 아래의 `FindAirfare` 작업을 살펴 봅니다.  
  
 [!code-csharp[c_DataArchitecture#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#1)]
 [!code-vb[c_DataArchitecture#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#1)]  
  
 `FindAirfare` 를 클라이언트에서 호출했다고 가정합니다. 클라이언트의 서비스 프레임워크는 `FromCity` 및 `ToCity` 매개 변수를 나가는 <xref:System.ServiceModel.Channels.Message> 인스턴스로 변환하고, 보낼 채널 스택에 이를 전달합니다.  
  
 서비스 쪽에서는 <xref:System.ServiceModel.Channels.Message> 인스턴스가 채널 스택으로부터 도착할 때 서비스 프레임워크가 메시지로부터 관련 데이터를 추출하여 `FromCity` 및 `ToCity` 매개 변수를 채운 다음, 서비스측 `FindAirfare` 메서드를 호출합니다. 메서드가 반환되면 서비스 프레임워크는 반환된 정수 값과 `IsDirectFlight` 출력 매개 변수를 사용하여 이 정보가 포함된 <xref:System.ServiceModel.Channels.Message> 개체 인스턴스를 만듭니다. 그런 다음 `Message` 인스턴스를 클라이언트로 다시 보낼 채널 스택에 전달합니다.  
  
 클라이언트 쪽에서는 응답 메시지가 포함된 <xref:System.ServiceModel.Channels.Message> 인스턴스가 채널 스택으로부터 나타납니다. 서비스 프레임워크는 반환 값과 `IsDirectFlight` 값을 추출하고 이러한 값을 클라이언트의 호출자에게 반환합니다.  
  
## <a name="message-class"></a>Message 클래스  
 <xref:System.ServiceModel.Channels.Message> 클래스는 메시지를 추상적으로 표현하도록 만들어졌으나 해당 디자인은 SOAP 메시지에 강하게 연결되어 있습니다. <xref:System.ServiceModel.Channels.Message> 에는 메시지 본문, 메시지 헤더 및 메시지 속성이라는 세 가지 주요 정보가 포함되어 있습니다.  
  
## <a name="message-body"></a>메시지 본문  
 메시지 본문은 메시지의 실제 데이터 페이로드를 나타내는 부분입니다. 메시지 본문은 항상 XML Infoset으로 표시됩니다. 이는 WCF에서 만들어지거나 받은 모든 메시지가 XML 형식 이어야 한다는 것을 의미 하지는 않습니다. 메시지 형식은 메시지 본문의 해석 방법을 결정하는 채널 스택에 따라 달라집니다. 채널 스택은 메시지를 XML로 내보내거나, 다른 형식으로 변환하거나, 아예 전부 생략할 수도 있습니다. 물론 WCF에서 제공 하는 대부분의 바인딩을 사용 하는 경우 메시지 본문은 SOAP 봉투의 본문 섹션에서 XML 콘텐츠로 표현 됩니다.  
  
 `Message` 클래스가 본문을 나타내는 XML 데이터와 함께 반드시 버퍼를 포함하지는 않습니다. 논리적으로는 `Message` 가 XML Infoset을 포함하지만, 이 Infoset은 동적으로 생성될 수 있으며, 메모리에 물리적으로 존재하지는 않습니다.  
  
### <a name="putting-data-into-the-message-body"></a>데이터를 메시지 본문에 넣기  
 데이터를 메시지 본문에 넣기 위한 일관된 메커니즘은 없습니다. <xref:System.ServiceModel.Channels.Message> 클래스에는 추상 메서드인 <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%28System.Xml.XmlDictionaryWriter%29>가 있으며, 이 메서드는 <xref:System.Xml.XmlDictionaryWriter>를 사용합니다. <xref:System.ServiceModel.Channels.Message> 클래스의 각 서브클래스는 이 메서드를 재정의하고, 해당 콘텐츠를 작성하는 기능을 담당합니다. 메시지 본문은 `OnWriteBodyContent`를 생성하는 XML Infoset을 논리적으로 포함합니다. 다음 `Message` 서브클래스 예제를 참조하십시오.  
  
 [!code-csharp[c_DataArchitecture#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#2)]
 [!code-vb[c_DataArchitecture#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#2)]  
  
 물리적으로 `AirfareRequestMessage` 인스턴스에는 두 개의 문자열("fromCity" 및 "toCity")만 포함됩니다. 그러나 논리적으로는 이 메시지에 다음 XML infoset이 포함됩니다.  
  
```xml  
<airfareRequest>  
    <from>Tokyo</from>  
    <to>London</to>  
</airfareRequest>  
```  
  
 물론, 서비스 프레임워크를 사용하여 작업 계약 매개 변수로부터 이전과 같은 메시지를 만들 수 있기 때문에 일반적으로는 이 방식으로 메시지를 만들지 않습니다. 또한 <xref:System.ServiceModel.Channels.Message> 클래스에는 일반 콘텐츠 형식을 가진 메시지를 만드는 데 사용할 수 있는 정적 `CreateMessage` 메서드가 있습니다. 이러한 일반 콘텐츠 형식에는 빈 메시지, <xref:System.Runtime.Serialization.DataContractSerializer>와 함께 XML로 serialize된 개체가 포함된 메시지, SOAP 오류가 포함된 메시지, <xref:System.Xml.XmlReader>로 표시되는 XML이 포함된 메시지 등이 있습니다.  
  
### <a name="getting-data-from-a-message-body"></a>메시지 본문에서 데이터 가져오기  
 메시지 본문에 저장된 데이터를 추출하는 방법으로는 다음 두 가지가 있습니다.  
  
- <xref:System.ServiceModel.Channels.Message.WriteBodyContents%28System.Xml.XmlDictionaryWriter%29> 메서드를 호출하고 XML 작성기에서 전달하면 한 번에 메시지 본문 전체를 가져올 수 있습니다. 전체 메시지 본문이 이 작성기에 작성되어 있습니다. 전체 메시지 본문을 한 번에 가져오는 것을 *메시지 쓰기*라고도 합니다. 쓰기는 주로 메시지를 보낼 때 채널 스택에서 수행합니다. 채널 스택의 일부는 일반적으로 전체 메시지 본문에 대한 액세스 권한, 인코딩 권한, 전송 권한을 가집니다.  
  
- 메시지 본문에서 정보를 가져오는 또 다른 방법은 <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents> 를 호출하고 XML 판독기를 가져오는 것입니다. 그런 다음 필요에 따라 판독기에서 메서드를 호출하여 메시지 본문에 순차적으로 액세스할 수 있습니다. 메시지 본문을 하나씩 가져오는 것을 *메시지 읽기*라고도 합니다. 메시지 읽기는 주로 메시지를 받을 때 서비스 프레임워크에서 사용합니다. 예를 들어 <xref:System.Runtime.Serialization.DataContractSerializer> 를 사용 중일 때 서비스 프레임워크는 본문에 대해 XML 판독기를 가져오고 이를 deserialization 엔진에 전달합니다. 그러면 이 엔진은 메시지를 요소별로 읽기 시작하고 해당 개체 그래프를 생성합니다.  
  
 메시지 본문은 한 번만 검색할 수 있습니다. 이를 통해 정방향 스트림을 사용할 수 있습니다. 예를 들어 <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%28System.Xml.XmlDictionaryWriter%29> 으로부터 읽은 <xref:System.IO.FileStream> 재정의를 쓰고, 결과를 XML Infoset으로 반환할 수 있습니다. 파일의 시작 부분으로 "되감기" 하지 않아도 됩니다.  
  
 `WriteBodyContents` 및 `GetReaderAtBodyContents` 메서드는 해당 메시지 본문이 전에 검색된 적이 없는지 확인한 다음 `OnWriteBodyContents` 또는 `OnGetReaderAtBodyContents`를 각각 호출하기만 하면 됩니다.  
  
## <a name="message-usage-in-wcf"></a>WCF의 메시지 사용  
 대부분의 메시지는 *보내는* 메시지(채널 스택에서 보낼 서비스 프레임워크에서 만드는 메시지) 또는 *들어오는* 메시지(채널 스택에서 전송되어 서비스 프레임워크에서 해석되는 메시지) 중 하나로 분류될 수 있습니다. 또한 채널 스택은 버퍼링 모드 또는 스트리밍 모드로 작동할 수 있으며 서비스 프레임워크는 스트리밍 또는 비스트리밍 프로그래밍 모델을 노출할 수 있습니다. 다음 표는 이러한 조합에 따라 발생 가능한 경우를 간략한 구현 정보와 함께 보여 줍니다.  
  
|메시지 유형|메시지의 본문 데이터|쓰기(OnWriteBodyContents) 구현|읽기(OnGetReaderAtBodyContents) 구현|  
|------------------|--------------------------|--------------------------------------------------|-------------------------------------------------------|  
|비스트리밍 프로그래밍 모델에서 만들어진 나가는 메시지|메시지 작성에 필요한 데이터(예: serialize하는 데 필요한 개체 및 <xref:System.Runtime.Serialization.DataContractSerializer> 인스턴스)*|저장된 데이터를 기반으로 메시지를 작성하는 사용자 지정 논리(예: `WriteObject`의 `DataContractSerializer` 호출. 단 이 serializer를 사용 중인 경우)*|`OnWriteBodyContents`를 호출하고, 결과를 버퍼링하고, 버퍼를 통해 XML 판독기를 반환|  
|스트리밍된 프로그래밍 모델에서 만들어진 나가는 메시지|작성할 데이터가 포함된 `Stream`*|<xref:System.Xml.IStreamProvider> 메커니즘을 사용하여 저장된 스트림에서 가져온 데이터 작성*|`OnWriteBodyContents`를 호출하고, 결과를 버퍼링하고, 버퍼를 통해 XML 판독기를 반환|  
|스트리밍 채널 스택에서 들어오는 메시지|네트워크를 통해 `Stream` 와 함께 들어오는 데이터를 나타내는 <xref:System.Xml.XmlReader> 개체|`XmlReader`를 사용하여 저장된 `WriteNode`로부터 콘텐츠 작성|저장된 `XmlReader`반환|  
|스트리밍되지 않은 채널 스택에서 들어오는 메시지|`XmlReader` 와 함께 본문 데이터가 포함된 버퍼|`XmlReader` 를 사용하여 저장된 `WriteNode`로부터 콘텐츠를 작성합니다.|저장된 lang 반환|  
  
 \*이러한 항목은 <xref:System.ServiceModel.Channels.BodyWriter> 클래스의 서브 클래스 `Message` 에서 직접 구현 되지 않습니다. 에 대 한 <xref:System.ServiceModel.Channels.BodyWriter>자세한 내용은 [메시지 클래스 사용](../../../../docs/framework/wcf/feature-details/using-the-message-class.md)을 참조 하세요.  
  
## <a name="message-headers"></a>메시지 헤더  
 메시지에는 헤더가 포함될 수 있습니다. 헤더는 논리적으로 이름, 네임스페이스 및 다른 속성과 연관된 XML Infoset으로 구성됩니다. `Headers` 의 <xref:System.ServiceModel.Channels.Message>속성을 사용하여 메시지 헤더에 액세스합니다. 각 헤더는 <xref:System.ServiceModel.Channels.MessageHeader> 클래스로 표현됩니다. 일반적으로 메시지 헤더는 SOAP 메시지를 사용하기 위해 구성된 채널 스택을 사용할 때 SOAP 메시지 헤더로 매핑됩니다.  
  
 메시지 헤더로 정보를 가져오고, 메시지 헤더에서 정보를 추출하는 것은 메시지 본문을 사용하는 것과 비슷합니다. 스트리밍이 지원되지 않으므로 프로세스가 다소 간단합니다. 동일한 헤더의 콘텐츠에 두 번 이상 액세스할 수 있으며, 헤더가 항상 버퍼링되도록 하여 임의의 순서로 액세스할 수 있습니다. 헤더를 통해 XML 판독기를 가져오는 데 사용할 수 있는 범용 메커니즘이 없지만 이러한 기능을 사용 하 여 읽을 `MessageHeader` 수 있는 헤더를 나타내는 WCF 내부 하위 클래스가 있습니다. 이 `MessageHeader` 형식은 사용자 지정 애플리케이션 헤더가 포함된 메시지가 들어올 경우 채널 스택에 의해 생성됩니다. 그러면 서비스 프레임워크에서 <xref:System.Runtime.Serialization.DataContractSerializer>와 같은 deserialization 엔진을 사용하여 이러한 헤더를 해석할 수 있습니다.  
  
 자세한 내용은 [메시지 클래스 사용](../../../../docs/framework/wcf/feature-details/using-the-message-class.md)을 참조 하세요.  
  
## <a name="message-properties"></a>메시지 속성  
 메시지에는 속성이 포함될 수 있습니다. *속성* 은 문자열 이름과 연결 된 .NET Framework 개체입니다. `Properties` 의 `Message`속성을 통해 속성에 액세스합니다.  
  
 일반적으로 각각 SOAP 본문과 SOAP 헤더로 매핑되는 메시지 본문과 메시지 헤더와는 달리, 메시지 속성은 일반적으로 메시지와 함께 보내거나 받지 않습니다. 메시지 속성은 주로 채널 스택의 다양한 채널 간이나 채널 스택과 서비스 모델 간에 메시지에 대한 데이터를 전달하기 위한 통신 메커니즘으로 존재합니다.  
  
 예를 들어 WCF의 일부로 포함 된 HTTP 전송 채널은 클라이언트에 응답을 보낼 때 "404 (찾을 수 없음)" 및 "500 (내부 서버 오류)"와 같은 다양 한 HTTP 상태 코드를 생성할 수 있습니다. 회신 메시지를 보내기 전에는의에 형식의 `Properties` <xref:System.ServiceModel.Channels.HttpResponseMessageProperty>개체가 포함 된 "httpresponse.cache `Message` " 라는 속성이 포함 되어 있는지 확인 합니다. 이러한 속성이 있으면 <xref:System.ServiceModel.Channels.HttpResponseMessageProperty.StatusCode%2A> 속성을 살펴보고 해당 상태 코드를 사용합니다. 이러한 속성이 없으면 기본 "200(확인)" 코드를 사용합니다.  
  
 자세한 내용은 [메시지 클래스 사용](../../../../docs/framework/wcf/feature-details/using-the-message-class.md)을 참조 하세요.  
  
### <a name="the-message-as-a-whole"></a>메시지 전체  
 지금까지 메시지의 여러 부분에 각각 액세스하는 데 사용되는 메서드를 살펴보았습니다. 그러나 <xref:System.ServiceModel.Channels.Message> 클래스는 메시지 전체를 대상으로 작동하는 메서드도 제공합니다. 예를 들어 `WriteMessage` 메서드는 XML 작성기에 전체 메시지를 작성합니다.  
  
 이렇게 하려면 전체 `Message` 인스턴스와 하나의 XML Infoset 간에 매핑이 정의되어야 합니다. 이러한 매핑은 실제로 존재 합니다. WCF는 SOAP 표준을 사용 하 여이 매핑을 정의 합니다. `Message` 인스턴스를 XML Infoset으로 작성할 때, 결과 Infoset은 해당 메시지가 포함된 유효한 SOAP 봉투입니다. 따라서 `WriteMessage` 는 일반적으로 다음 단계를 수행합니다.  
  
1. SOAP 봉투 요소 열기 태그를 씁니다.  
  
2. SOAP 헤더 요소 열기 태그를 쓰고, 모든 헤더를 작성하고, 헤더 요소를 닫습니다.  
  
3. SOAP 본문 요소 열기 태그를 씁니다.  
  
4. `WriteBodyContents` 또는 동등한 메서드를 호출하여 본문을 작성합니다.  
  
5. 본문 및 봉투 요소를 닫습니다.  
  
 이전 단계는 SOAP 표준과 밀접하게 연관되어 있습니다. 여러 버전의 SOAP가 존재하기 때문에 발생하는 문제가 있습니다. 예를 들어 사용 중인 SOAP 버전을 모르면 SOAP 봉투 요소를 올바르게 작성할 수 없습니다. 또한 복잡한 SOAP별 매핑을 완전히 해제하는 것이 좋은 경우도 있습니다.  
  
 이러한 목적을 위해 `Version` 속성이 `Message`에서 제공됩니다. 이 속성은 메시지를 작성할 때 사용할 SOAP 버전으로 설정하거나, SOAP별 매핑을 방지하도록 `None` 으로 설정할 수 있습니다. `Version` 속성이 `None`으로 설정되면 전체 메시지를 대상으로 작동하는 메서드는 메시지가 본문으로만 구성되어 있는 것처럼 작동합니다. 예를 들어 `WriteMessage` 는 앞에서 설명한 여러 단계를 수행하는 대신 `WriteBodyContents` 만 호출합니다. 들어오는 메시지에서 `Version` 이 자동으로 감지되고 올바르게 설정됩니다.  
  
## <a name="the-channel-stack"></a>채널 스택  
  
### <a name="channels"></a>채널  
 앞서 언급한 대로 채널 스택은 나가는 <xref:System.ServiceModel.Channels.Message> 인스턴스를 일부 동작(예: 네트워크를 통한 패킷 전송)으로 변환하거나 일부 동작(예: 네트워크 패킷 수신)을 들어오는 `Message` 인스턴스로 변환하는 역할을 담당합니다.  
  
 채널 스택은 시퀀스의 순서로 하나 이상의 채널로 구성됩니다. 나가는 `Message` 인스턴스는 스택의 첫 번째 채널( *맨 위 채널*이라고도 함)로 전달되며, 이 채널은 해당 인스턴스를 스택의 다음 아래 채널로 전달합니다. 메시지는 *전송 채널*이라고도 하는 마지막 채널에서 종료됩니다. 들어오는 메시지는 전송 채널에서 시작되며, 스택의 아래 채널에서 위 채널로 전달됩니다. 메시지는 보통 맨 위 채널에서부터 서비스 프레임워크로 전달됩니다. 이는 애플리케이션 메시지의 일반적인 패턴이지만 일부 채널은 조금 다르게 작동할 수 있습니다. 예를 들어 위의 채널로부터 전달되는 메시지 없이 자체 인프라 메시지를 보낼 수 있습니다.  
  
 채널은 스택을 통과하므로 여러 방법으로 메시지에서 작동할 수 있습니다. 가장 일반적인 작업은 나가는 메시지에 헤더를 추가하고, 들어오는 메시지의 헤더를 읽는 것입니다. 예를 들어 채널은 메시지의 디지털 서명을 컴퓨팅하고 이를 헤더로 추가할 수 있습니다. 또한 채널은 들어오는 메시지에서 이 디지털 서명 헤더를 검사하고, 유효한 서명이 없는 메시지가 채널 스택에서 자체 방식을 만들지 못하도록 차단합니다. 채널은 종종 메시지 속성을 설정하거나 검사하기도 합니다. 메시지 본문은 일반적으로 수정 되지 않지만, 예를 들어 WCF 보안 채널이 메시지 본문을 암호화할 수 있습니다.  
  
### <a name="transport-channels-and-message-encoders"></a>전송 채널 및 메시지 인코더  
 스택의 가장 아래쪽에 있는 채널은 나가는 <xref:System.ServiceModel.Channels.Message>를 다른 채널에서 수정된 대로 일부 동작으로 실제로 변환하는 기능을 담당합니다. 받는 쪽에서 이 채널은 다른 채널이 처리하는 `Message` 로 일부 동작을 변환하는 채널입니다.  
  
 앞에서 설명한 대로 일부 예제만 제공하기 위해서도 다양한 동작이 있을 수 있습니다. 이러한 동작으로는 다양한 프로토콜을 통한 네트워크 패킷 주고받기, 데이터베이스의 메시지 읽기 또는 쓰기, 메시지 큐에서 메시지 대기시키기 또는 제거하기 등이 있습니다. 이러한 모든 작업은 일반적으로 다음과 같은 작업을 수행 합니다. 즉, WCF`Message` 인스턴스와 송신, 수신, 읽기, 쓰기, 큐에 대기 또는 큐에서 제거 될 수 있는 실제 바이트 그룹 간의 변환이 필요 합니다. `Message` 를 바이트 그룹으로 변환하는 프로세스를 *인코딩*이라 하며, 바이트 그룹으로부터 `Message` 를 만드는 역 프로세스를 *디코딩*이라 합니다.  
  
 대부분의 전송 채널은 *메시지 인코더* 라는 구성 요소를 사용하여 인코딩 및 디코딩 작업을 수행합니다. 메시지 인코더는 <xref:System.ServiceModel.Channels.MessageEncoder> 클래스의 서브클래스입니다. `MessageEncoder`는 다양한 `ReadMessage` 및 `WriteMessage` 메서드 오버로드를 포함하여 `Message`와 바이트 그룹 사이에서 변환합니다.  
  
 보내는 쪽에서는 버퍼링 전송 채널이 상위 채널로부터 `Message` 개체를 받아서 `WriteMessage`로 전달합니다. 버퍼링 전송 채널은 바이트 배열을 다시 가져온 다음 이를 사용하여 해당 동작(예: 이러한 바이트를 유효한 TCP 패킷으로 패키지화하고 올바른 대상으로 이를 보냄)을 수행합니다. 스트리밍 전송 채널은 먼저 `Stream` 을 만든 다음(예: 나가는 TCP 연결을 통해), 메시지를 작성하는 적합한 `Stream` 오버로드로 보내기 위해 필요한 `Message` 과 `WriteMessage` 를 모두 전달합니다.  
  
 받는 쪽에서는 버퍼링 전송 채널이 (들어오는 TCP 패킷 등으로부터) 들어오는 바이트를 배열로 추출하고, `ReadMessage` 를 호출하여 채널 스택 위쪽으로 전달할 수 있는 `Message` 개체를 가져옵니다. 스트리밍 전송 채널은 `Stream` 개체(예: 들어오는 TCP 연결을 통한 네트워크 스트림)를 만들고 이를 `ReadMessage` 로 전달하여 `Message` 개체를 다시 가져옵니다.  
  
 전송 채널과 메시지 인코더를 반드시 분리해야 하는 것은 아니지만 메시지 인코더를 사용하지 않는 전송 채널을 작성할 수 있습니다. 단, 분리를 하게 되면 컴퍼지션이 쉽다는 장점이 있습니다. 전송 채널이 기본 <xref:System.ServiceModel.Channels.MessageEncoder>만 사용 하는 한, 모든 WCF 또는 타사 메시지 인코더를 사용할 수 있습니다. 마찬가지로, 일반적으로 모든 전송 채널에서 동일한 인코더를 사용할 수 있습니다.  
  
### <a name="message-encoder-operation"></a>메시지 인코더 작업  
 인코더의 일반적인 작업을 설명하려면 다음 네 가지 경우를 고려하는 것이 좋습니다.  
  
|작업|주석|  
|---------------|-------------|  
|인코딩, 버퍼링|버퍼링 모드에서는 인코더가 보통 다양한 크기의 버퍼를 만든 다음 이를 통해 XML 작성기를 만듭니다. 그런 다음 인코딩되는 메시지에서 <xref:System.ServiceModel.Channels.Message.WriteMessage%28System.Xml.XmlWriter%29> 를 호출합니다. 이 메시지는 이 항목의 <xref:System.ServiceModel.Channels.Message.WriteBodyContents%28System.Xml.XmlDictionaryWriter%29>에 대한 이전 단원에서 설명한 것처럼 `Message` 를 사용하여 헤더와 본문을 차례로 작성합니다. 그런 다음 사용할 전송 채널에 대해 바이트 배열로 표시되는 버퍼의 콘텐츠가 반환됩니다.|  
|인코딩, 스트리밍|스트리밍 모드에서는 작업이 위의 모드와 비슷하지만 좀 더 간단합니다. 버퍼링할 필요가 없기 때문입니다. XML 작성기는 일반적으로 스트림을 통해 만들어지며, <xref:System.ServiceModel.Channels.Message.WriteMessage%28System.Xml.XmlWriter%29> 에서 `Message` 가 호출되어 이 작성기에 이를 작성합니다.|  
|디코딩, 버퍼링|버퍼링 모드에서 디코딩할 때는 버퍼링된 데이터가 포함된 특별한 `Message` 서브클래스가 일반적으로 만들어집니다. 메시지의 헤더가 읽히고, 메시지 본문에 배치된 XML 판독기가 만들어집니다. 이는 <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents>와 함께 반환될 판독기입니다.|  
|디코딩, 스트리밍|스트리밍 모드에서 디코딩할 때는 특별한 메시지 서브클래스가 일반적으로 만들어집니다. 스트림은 모든 헤더를 읽고 이를 메시지 본문에 배치할 수 있는 고급 기능입니다. 그런 다음 XML 판독기가 스트림을 통해 만들어집니다. 이는 <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents>와 함께 반환될 판독기입니다.|  
  
 인코더는 다른 기능도 수행할 수 있습니다. 예를 들어 인코더는 XML 판독기 및 작성기를 풀링할 수 있습니다. 필요할 때마다 새 XML 판독기나 작성기를 만들려면 비용이 많이 듭니다. 그러므로 일반적으로 인코더는 구성 가능한 크기의 작성기 풀과 판독기 풀을 유지 관리합니다. 앞에서 설명한 인코더 작업에 대 한 설명에서 "XML 판독기/작성기 만들기" 구문이 사용 될 때마다 일반적으로 "풀에서 하나를 사용 하거나, 사용할 수 없는 경우 하나를 만듭니다."를 의미 합니다. 인코더(및 디코딩하는 동안 인코더가 만드는 `Message` 서브클래스)는 작성기와 반환기가 더 이상 필요하지 않을 때(예: `Message` 가 닫힐 때) 이들을 풀로 반환하는 논리를 포함합니다.  
  
 WCF는 추가 사용자 지정 형식을 만들 수 있지만 세 가지 메시지 인코더를 제공 합니다. 제공되는 형식에는 텍스트, 이진 및 MTOM(Message Transmission Optimization Mechanism)이 있습니다. 자세한 내용은 [Choosing a Message Encoder](../../../../docs/framework/wcf/feature-details/choosing-a-message-encoder.md)에 설명되어 있습니다.  
  
### <a name="the-istreamprovider-interface"></a>IStreamProvider 인터페이스  
 스트리밍된 본문을 포함하고 있는 보내는 메시지를 XML 작성기에 쓸 때 <xref:System.ServiceModel.Channels.Message> 는 <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%28System.Xml.XmlDictionaryWriter%29> 구현에서 다음과 유사한 호출의 시퀀스를 사용합니다.  
  
- 스트림 앞에 필요한 정보를 씁니다(예: 여는 XML 태그).  
  
- 스트림을 씁니다.  
  
- 스트림 뒤에 필요한 정보를 씁니다(예: 닫는 XML 태그).  
  
 이는 텍스트 XML 인코딩과 유사한 인코딩을 사용하여 작동합니다. 그러나 일부 인코딩은 XML infoset 정보(예: XML 요소의 시작 및 끝 태그)를 요소 내에 포함된 데이터와 함께 사용하지 않습니다. 예를 들어 MTOM 인코딩에서 메시지는 여러 부분으로 나누어집니다. 하나의 부분에는 실제 요소 콘텐츠의 다른 부분에 대한 참조가 포함될 수 있는 XML infoset이 포함됩니다. XML Infoset이 일반적으로 스트리밍된 콘텐츠와 비교하여 작으므로 Infoset을 버퍼링하고 쓴 다음 스트리밍된 방법으로 콘텐츠를 쓰는 것이 좋습니다. 즉, 이는 닫는 요소 태그가 작성될 때까지는 스트림을 쓰면 안 된다는 것을 의미합니다.  
  
 이를 위해 <xref:System.Xml.IStreamProvider> 인터페이스가 사용됩니다. 인터페이스에는 작성할 스트림을 반환하는 <xref:System.Xml.IStreamProvider.GetStream> 메서드가 있습니다. <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%28System.Xml.XmlDictionaryWriter%29> 에서 스트리밍된 메시지 본문을 쓰는 올바른 방법은 다음과 같습니다.  
  
1. 스트림 앞에 필요한 정보를 씁니다(예: 여는 XML 태그).  
  
2. 쓸 스트림을 반환하는 `WriteValue` 구현과 함께 <xref:System.Xml.XmlDictionaryWriter> 를 사용하는 <xref:System.Xml.IStreamProvider>에서 `IStreamProvider` 오버로드를 호출합니다.  
  
3. 스트림 뒤에 필요한 정보를 씁니다(예: 닫는 XML 태그).  
  
 이 방법을 사용하면 <xref:System.Xml.IStreamProvider.GetStream> 을 호출하고 스트리밍된 데이터를 작성할 때 XML 작성기를 선택할 수 있습니다. 예를 들어 텍스트 및 이진 XML 작성기는 이를 즉각 호출하고 시작 및 끝 태그 사이에서 스트리밍된 콘텐츠를 작성합니다. MTOM 작성기는 메시지의 적절한 일부를 쓸 준비가 되면 나중에 <xref:System.Xml.IStreamProvider.GetStream> 을 호출할지 결정할 수 있습니다.  
  
## <a name="representing-data-in-the-service-framework"></a>서비스 프레임워크에서 데이터 표시  
 이 항목의 "기본 아키텍처" 단원에 설명 된 것 처럼 서비스 프레임 워크는 메시지 데이터와 실제 `Message` 인스턴스의 사용자에 게 친숙 한 프로그래밍 모델 간에 변환 하는 작업을 담당 하는 WCF의 일부입니다. 일반적으로 메시지 교환은 서비스 프레임 워크에서 <xref:System.ServiceModel.OperationContractAttribute> 특성으로 표시 된 .NET Framework 메서드로 표시 됩니다. 메서드는 일부 매개 변수에서 사용할 수 있으며, 반환 값 또는 out 매개 변수(또는 둘 다)를 반환할 수 있습니다. 서비스 쪽에서는 입력 매개 변수가 들어오는 메시지를 나타내며, 반환 값 및 out 매개 변수는 나가는 메시지를 나타냅니다. 클라이언트 쪽에서는 그 반대입니다. 매개 변수 및 해당 반환 값을 사용하여 메시지를 설명하는 프로그래밍 모델은 [Specifying Data Transfer in Service Contracts](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)에서 자세하게 설명합니다. 이 단원에서는 간략한 개요만 제공합니다.  
  
## <a name="programming-models"></a>프로그래밍 모델  
 WCF 서비스 프레임 워크는 메시지를 설명 하는 다섯 가지 프로그래밍 모델을 지원 합니다.  
  
### <a name="1-the-empty-message"></a>1. 빈 메시지  
 이는 가장 간단한 경우입니다. 들어오는 빈 메시지를 설명하기 위해 입력 매개 변수를 사용하지 않습니다.  
  
 [!code-csharp[C_DataArchitecture#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#3)]
 [!code-vb[C_DataArchitecture#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#3)]  
  
 나가는 빈 메시지를 설명하기 위해 void 반환 값을 사용하고 out 매개 변수를 사용하지 않습니다.  
  
 [!code-csharp[C_DataArchitecture#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#4)]
 [!code-vb[C_DataArchitecture#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#4)]  
  
 이는 단방향 작업 계약과는 다릅니다.  
  
 [!code-csharp[C_DataArchitecture#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#5)]
 [!code-vb[C_DataArchitecture#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#5)]  
  
 `SetDesiredTemperature` 예제에서는 양방향 메시지 교환 패턴을 설명합니다. 작업에서 메시지가 반환되지만 비어 있습니다. 작업에서 오류를 반환할 수 있습니다. "Lightbulb 설정" 예제에서 메시지 교환 패턴은 단방향이므로 설명을 위해 나가는 메시지가 없습니다. 이 경우 서비스는 클라이언트로 반환되는 모든 상태를 통신할 수 없습니다.  
  
### <a name="2-using-the-message-class-directly"></a>2. Message 클래스 직접 사용  
 작업 계약에서 직접 <xref:System.ServiceModel.Channels.Message> 클래스(또는 해당 서브클래스 중 하나)를 사용할 수 있습니다. 이 경우에는 서비스 프레임워크가 추가 처리 없이 작업에서 채널 스택으로, 또는 그 반대로 `Message`를 전달합니다.  
  
 `Message` 를 직접 사용하는 두 가지 주요 사례가 있습니다. 사용자의 메시지를 설명하기에 충분한 유연성을 제공하는 다른 프로그래밍 모델이 없을 때 이를 고급 시나리오에 사용할 수 있습니다. 예를 들어 메시지 헤더가 될 파일의 속성과 메시지 본문이 될 파일의 내용으로 메시지를 설명하기 위해 디스크의 파일을 사용할 수 있습니다. 그런 다음, 다음과 유사한 항목을 만들 수 있습니다.  
  
 [!code-csharp[C_DataArchitecture#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#6)]
 [!code-vb[C_DataArchitecture#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#6)]  
  
 작업 계약에서 `Message` 의 두 번째 일반적인 용도는 서비스가 특정 메시지 콘텐츠에 대해 고려하지 않고 메시지에서 검정 상자의 역할을 수행하는 경우입니다. 예를 들어 메시지를 다른 여러 받는 사람에게 전달하는 서비스가 있을 수 있습니다. 계약은 다음과 같이 작성될 수 있습니다.  
  
 [!code-csharp[C_DataArchitecture#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#7)]
 [!code-vb[C_DataArchitecture#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#7)]  
  
 Action = "*" 줄은 메시지 디스패치를 효과적으로 해제 하 고 `IForwardingService` 계약에 전송 된 모든 메시지가 `ForwardMessage` 작업에 적용 되도록 합니다. (일반적으로 디스패처는 메시지의 "Action" 헤더를 검사 하 여 의도 한 작업을 결정 합니다. Action = "\*"은 "동작 헤더의 모든 가능한 값"을 의미 합니다. Action = "\*"과 (와) 메시지를 매개 변수로 사용 하는 조합은 가능한 모든 메시지를 받을 수 있기 때문에 "유니버설 계약" 이라고 합니다. 가능한 모든 메시지를 보내려면 메시지를 반환 값으로 사용 하 고를 " `ReplyAction` \*"로 설정 합니다. 이렇게 하면 사용자가 반환하는 `Message` 개체를 사용하여 이 헤더를 제어할 수 있으므로 서비스 프레임워크가 자체 Action 헤더에 추가되지 않도록 할 수 있습니다.  
  
### <a name="3-message-contracts"></a>3. 메시지 계약  
 WCF는 *메시지 계약*이라는 메시지를 설명 하는 선언적 프로그래밍 모델을 제공 합니다. 이 모델은 [Using Message Contracts](../../../../docs/framework/wcf/feature-details/using-message-contracts.md)에 자세히 설명되어 있습니다. 기본적으로 전체 메시지는 <xref:System.ServiceModel.MessageBodyMemberAttribute> 및 <xref:System.ServiceModel.MessageHeaderAttribute> 와 같은 특성을 사용 하는 단일 .NET Framework 형식으로 표시 되며 메시지 계약 클래스의 어떤 부분이 메시지의 어떤 부분에 매핑되는지 설명 합니다.  
  
 `Message` 클래스를 직접 사용하는 것만큼 많은 제어를 할 수는 없지만, 메시지 계약을 사용하여 결과 `Message` 인스턴스에 대해 여러 가지 제어를 할 수 있습니다. 예를 들어 메시지 본문은 종종 여러 가지 정보로 구성되며, 이러한 정보는 각각 자체 XML 요소로 표시됩니다. 이러한 요소는 본문에서 직접 발생할 수도 있고(*bare* 모드), 포함된 XML 요소에서 *wrapped* 가 될 수도 있습니다. 메시지 계약 프로그래밍 모델을 사용하면 bare-wrapped 모드를 결정하고 래퍼 이름과 네임스페이스를 제어할 수 있게 됩니다.  
  
 메시지 계약의 다음 코드 예제에서는 이러한 기능을 보여 줍니다.  
  
 [!code-csharp[C_DataArchitecture#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#9)]
 [!code-vb[C_DataArchitecture#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#9)]  
  
 <xref:System.ServiceModel.MessageBodyMemberAttribute>, <xref:System.ServiceModel.MessageHeaderAttribute>또는 기타 관련 특성과 함께 serialize하도록 표시된 항목이 serialize 가능해야 메시지 계약에 참여할 수 있습니다. 자세한 내용은이 항목의 뒷부분에 나오는 "Serialization" 단원을 참조 하십시오.  
  
### <a name="4-parameters"></a>4. 매개 변수  
 여러 데이터에 대해 작동하는 작업을 설명하려는 개발자는 종종 메시지 계약이 제공하는 일정 정도의 제어를 필요로 하지 않습니다. 예를 들어 새 서비스를 만들 때 사용자는 보통 bare-wrapped 모드나 래퍼 요소 이름을 결정하지 않으려고 합니다. 이러한 결정을 내리려면 웹 서비스와 SOAP에 대해 잘 알고 있어야 합니다.  
  
 WCF 서비스 프레임 워크는 사용자에 게 이러한 선택 항목을 적용 하지 않고도 관련 된 여러 가지 정보를 보내거나 받기 위한 가장 효율적이 고, 상호 운용 가능한 SOAP 표현을 자동으로 선택할 수 있습니다. 이러한 여러 가지 정보를 작업 계약의 매개 변수 또는 반환 값으로 설명하기만 해도 이를 수행할 수 있습니다. 예를 들어 다음 작업 계약을 확인해 보십시오.  
  
 [!code-csharp[C_DataArchitecture#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#11)]
 [!code-vb[C_DataArchitecture#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#11)]  
  
 서비스 프레임워크는`customerID`, `item`, `quantity`라는 세 가지의 정보를 모두 메시지 본문에 삽입하고, `SubmitOrderRequest`라는 래퍼 요소에서 이들을 래핑하도록 자동으로 결정합니다.  
  
 보다 복잡한 메시지 계약 또는 `Message` 기반 프로그래밍 모델로 이동해야 하는 특별한 이유가 없다면 작업 계약 매개 변수의 간단한 목록으로 보내거나 받을 정보를 설명하는 것이 좋습니다.  
  
### <a name="5-stream"></a>5. 스트림  
 메시지 계약의 단독 메시지 본문 부분으로 또는 작업 계약에서 `Stream`(또는 해당 서브클래스 중 하나)을 사용하는 것은 위에서 설명한 항목과 별도의 프로그래밍 모델로 고려될 수 있습니다. 이 방법으로 `Stream` 을 사용하면 사용자의 자체 스트리밍 호환 가능 `Message` 서브클래스를 간결하게 작성할 수 있으므로, 사용자의 계약을 스트리밍 방식으로 유일하게 사용할 수 있습니다. 자세한 내용은 [대량 데이터 및 스트리밍](../../../../docs/framework/wcf/feature-details/large-data-and-streaming.md)을 참조 하세요.  
  
 `Stream` 또는 해당 서브클래스 중 하나를 이 방법으로 사용할 때는 serializer가 호출되지 않습니다. 나가는 메시지의 경우 특별한 스트리밍 `Message` 서브클래스가 만들어지고, <xref:System.Xml.IStreamProvider> 인터페이스의 단원에서 설명한 대로 스트림이 작성됩니다. 들어오는 메시지의 경우 서비스 프레임워크가 들어오는 메시지에 대해 `Stream` 서브클래스를 만들고 이를 해당 작업에 제공합니다.  
  
## <a name="programming-model-restrictions"></a>프로그래밍 모델 제한  
 위에서 설명한 프로그래밍 모델은 임의로 조합할 수 없습니다. 예를 들어 작업이 메시지 계약 형식을 수락할 경우 해당 메시지 계약이 유일한 입력 매개 변수가 되어야 합니다. 뿐만 아니라 해당 작업은 빈 메시지(void의 반환 형식) 또는 기타 메시지 계약을 반환해야 합니다. 이러한 프로그래밍 모델 제한 사항은 각 특정 프로그래밍 모델에 대 한 항목에 설명 되어 있습니다. 메시지 [계약 사용](../../../../docs/framework/wcf/feature-details/using-message-contracts.md), [메시지 클래스 사용](../../../../docs/framework/wcf/feature-details/using-the-message-class.md), [대량 데이터 및 스트리밍](../../../../docs/framework/wcf/feature-details/large-data-and-streaming.md)  
  
## <a name="message-formatters"></a>메시지 포맷터  
 위에서 설명한 프로그래밍 모델은 *메시지 포맷터* 라는 구성 요소를 서비스 프레임워크로 플러그 인함으로써 지원됩니다. 메시지 포맷터는 클라이언트 및 서비스 WCF <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> 클라이언트 <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter> 에서 각각 사용 하기 위해 또는 인터페이스, 또는 둘 다를 구현 하는 형식입니다.  
  
 메시지 포맷터는 일반적으로 동작별로 플러그 인됩니다. 예를 들어 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> 는 데이터 계약 메시지 포맷터를 플러그 인합니다. 이는 서비스 쪽의 <xref:System.ServiceModel.Dispatcher.DispatchOperation.Formatter%2A> 메서드에서 <xref:System.ServiceModel.Description.IOperationBehavior.ApplyDispatchBehavior%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Dispatcher.DispatchOperation%29> 를 올바른 포맷터로 설정하거나 클라이언트 쪽의 <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A> 메서드에서 <xref:System.ServiceModel.Description.IOperationBehavior.ApplyClientBehavior%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Dispatcher.ClientOperation%29> 를 올바른 포맷터로 설정함으로써 수행됩니다.  
  
 다음 표에서는 메시지 포맷터가 구현할 수 있는 메서드를 나열합니다.  
  
|인터페이스|메서드|작업|  
|---------------|------------|------------|  
|<xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter>|<xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter.DeserializeRequest%28System.ServiceModel.Channels.Message%2CSystem.Object%5B%5D%29>|들어오는 `Message` 를 작업 매개 변수로 변환합니다.|  
|<xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter>|<xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter.SerializeReply%28System.ServiceModel.Channels.MessageVersion%2CSystem.Object%5B%5D%2CSystem.Object%29>|작업 반환 값/출력 매개 변수로부터 나가는 `Message` 만들기|  
|<xref:System.ServiceModel.Dispatcher.IClientMessageFormatter>|<xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.SerializeRequest%28System.ServiceModel.Channels.MessageVersion%2CSystem.Object%5B%5D%29>|작업 매개 변수로부터 나가는 `Message` 만들기|  
|<xref:System.ServiceModel.Dispatcher.IClientMessageFormatter>|<xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.DeserializeReply%28System.ServiceModel.Channels.Message%2CSystem.Object%5B%5D%29>|들어오는 `Message` 를 반환 값/출력 매개 변수로 변환|  
  
## <a name="serialization"></a>Serialization  
 메시지 계약 또는 매개 변수를 사용 하 여 메시지 내용을 설명할 때마다 serialization을 사용 하 여 .NET Framework 형식과 XML Infoset 표현 간에 변환 해야 합니다. Serialization은 WCF의 다른 위치에서 사용 됩니다. 예 <xref:System.ServiceModel.Channels.Message> 를 들어에는 개체로 deserialize 된 메시지의 전체 본문을 읽는 데 사용할 수 있는 제네릭 <xref:System.ServiceModel.Channels.Message.GetBody%2A> 메서드가 있습니다.  
  
 WCF는 매개 변수 및 메시지 부분 <xref:System.Runtime.Serialization.DataContractSerializer> 을 serialize 및 deserialize 하는 데 사용할 수 있는 두 가지 serialization 기술인 및를 `XmlSerializer`지원 합니다. 그뿐 아니라 사용자 지정 serializer도 작성할 수 있습니다. 그러나 WCF의 다른 부분 (예: 제네릭 `GetBody` 메서드 또는 SOAP 오류 serialization)은 <xref:System.Runtime.Serialization.XmlObjectSerializer> 서브 클래스 (<xref:System.Runtime.Serialization.DataContractSerializer> 및 <xref:System.Runtime.Serialization.NetDataContractSerializer>은 <xref:System.Xml.Serialization.XmlSerializer>제외)만 사용 하도록 제한 될 수 있습니다. 또는만 사용 하도록 하드 코드 될 수도 있습니다. <xref:System.Runtime.Serialization.DataContractSerializer>입니다.  
  
 는 `XmlSerializer` ASP.NET 웹 서비스에서 사용 되는 serialization 엔진입니다. `DataContractSerializer` 는 새 데이터 계약 프로그래밍 모델을 이해하는 새 serialization 엔진입니다. `DataContractSerializer` 가 기본 선택되며, `XmlSerializer` 를 사용할지 여부는 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.DataContractFormatAttribute%2A> 특성을 사용하여 작업별로 지정할 수 있습니다.  
  
 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> 및 <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior> 는 `DataContractSerializer` 와 `XmlSerializer`각각에 대해 메시지 포맷터에서의 플러그 인을 담당하는 작업 동작입니다. <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> 동작은 실제로 <xref:System.Runtime.Serialization.XmlObjectSerializer>를 비롯하여 <xref:System.Runtime.Serialization.NetDataContractSerializer> 에서 파생되는 모든 serializer와 함께 작동할 수 있습니다. 자세한 내용은 독립 실행형 Serialization 사용에 설명되어 있습니다. 해당 동작은 `CreateSerializer` 가상 메서드 오버로드 중 하나를 호출하여 serializer를 가져옵니다. 다른 serializer를 플러그 인하려면 새 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> 서브클래스를 만들고, 두 `CreateSerializer` 오버로드를 모두 재정의합니다.  
  
## <a name="see-also"></a>참고자료

- [서비스 계약에서 데이터 전송 지정](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)
