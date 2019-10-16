---
title: WCF의 큐
ms.date: 03/30/2017
ms.assetid: e98d76ba-1acf-42cd-b137-0f8214661112
ms.openlocfilehash: 27c92b0f728b909de16a059485a38ff7fb0fb765
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69913386"
---
# <a name="queuing-in-wcf"></a>WCF의 큐
이 섹션에서는 WCF (Windows Communication Foundation)에서 대기 중인 통신을 사용 하는 방법을 설명 합니다.  
  
## <a name="queues-as-a-wcf-transport-binding"></a>큐를 WCF 전송 바인딩으로  
 WCF에서 계약은 교환할 대상을 지정 합니다. 계약은 비즈니스 종속 또는 애플리케이션별 메시지 교환입니다. 메시지를 교환하는 데 사용되는 메커니즘(또는 "방법")은 바인딩에 지정됩니다. WCF의 바인딩은 메시지 교환에 대 한 세부 정보를 캡슐화 합니다. 또한 다양한 전송 모양과 바인딩이 나타내는 프로토콜을 제어할 수 있도록 구성 노브를 사용자에게 노출합니다. WCF의 큐는 다른 전송 바인딩과 마찬가지로 처리 되며이는 많은 큐 응용 프로그램에 큰 장점입니다. 대부분의 큐 애플리케이션은 다른 RPC(원격 프로시저 호출) 스타일 분산 애플리케이션과 다르게 작성되어 사용 및 유지 관리가 어려울 수 있습니다. WCF를 사용 하 여 배포 응용 프로그램을 작성 하는 스타일은 거의 동일 하므로 더 쉽게 따르고 유지 관리할 수 있습니다. 교환 메커니즘을 비즈니스 논리와 분리하여 애플리케이션별 코드를 적용하지 않고도 전송을 변경하거나 쉽게 구성할 수 있습니다. 다음 그림에서는 MSMQ를 전송으로 사용하는 WCF 서비스 및 클라이언트의 구조를 보여 줍니다.  
  
 ![대기 중인 응용 프로그램 다이어그램](../../../../docs/framework/wcf/feature-details/media/distributed-queue-figure.jpg "분산 큐-그림")  
  
 이전 그림에서 볼 수 있듯이 클라이언트와 서비스는 애플리케이션 의미 즉, 계약과 구현만 정의해야 합니다. 서비스는 기본 설정을 사용하여 대기 중인 바인딩을 구성합니다. 클라이언트는 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 를 사용 하 여 WCF 클라이언트를 서비스에 생성 하 고 서비스에 메시지를 보내는 데 사용할 바인딩을 설명 하는 구성 파일을 생성 합니다. 따라서 대기 중인 메시지를 보내기 위해 클라이언트는 WCF 클라이언트를 인스턴스화하고 해당 클라이언트에 대 한 작업을 호출 합니다. 그러면 메시지가 전송 큐로 보내진 다음 대상 큐로 전송됩니다. 대기 중인 통신의 모든 복잡한 과정이 메시지를 보내고 받는 애플리케이션에서 숨겨집니다.  
  
 WCF의 대기 중인 바인딩에 대 한 주의 사항은 다음과 같습니다.  
  
- WCF의 기본 대기 중인 바인딩이 큐를 사용 하는 이중 통신을 지원 하지 않기 때문에 모든 서비스 작업은 단방향 이어야 합니다. 양방향 통신 샘플 ([양방향 통신](../../../../docs/framework/wcf/samples/two-way-communication.md))에서는 2 1 방향 계약을 사용 하 여 큐를 사용 하는 이중 통신을 구현 하는 방법을 보여 줍니다.  
  
- 메타 데이터 교환을 사용 하 여 WCF 클라이언트를 생성 하려면 WCF 클라이언트를 생성 하는 데 직접 쿼리할 수 있도록 서비스에 추가 HTTP 끝점이 필요 하며, 대기 중인 통신을 적절 하 게 구성 하는 바인딩 정보를 가져옵니다.  
  
- 대기 중인 바인딩에 따라 WCF 외부의 추가 구성이 필요 합니다. 예를 <xref:System.ServiceModel.NetMsmqBinding> 들어 WCF와 함께 제공 되는 클래스에는 메시지 큐 (MSMQ)를 최소한으로 구성 하는 것 뿐만 아니라 바인딩을 구성 해야 합니다.  
  
 다음 섹션에서는 MSMQ를 기반으로 하는 WCF와 함께 제공 되는 대기 중인 특정 바인딩에 대해 설명 합니다.  
  
### <a name="msmq"></a>MSMQ  
 WCF의 대기 중인 전송에서는 대기 중인 통신에 MSMQ를 사용 합니다.  
  
 MSMQ는 Windows의 선택적 구성 요소로 제공되고 NT 서비스로 실행됩니다. MSMQ는 전송 큐에서 전송할 메시지를 캡처하여 대상 큐로 전달합니다. MSMQ 큐 관리자는 전송 중에 메시지가 손실되지 않도록 신뢰할 수 있는 메시지 전송 프로토콜을 구현합니다. 이 프로토콜에는 네이티브 프로토콜이나 SRMP(SOAP Reliable Messaging Protocol)와 같은 SOAP 기반 프로토콜이 해당됩니다.  
  
 MSMQ의 큐는 트랜잭션 큐이거나 비트랜잭션 큐입니다. 트랜잭션 큐를 통해 메시지를 캡처하여 트랜잭션에 전달한 다음 큐에 영구적으로 저장할 수 있습니다. 트랜잭션 큐로 보낸 메시지는 순서대로 한 번에 정확하게 전송됩니다. 비트랜잭션 큐를 사용하여 일시적 메시지와 지속성 메시지를 모두 보낼 수 있습니다. 비트랜잭션 큐로 보낸 메시지는 안정적인 전송 보증을 제공하지 않기 때문에 메시지가 손실될 수 있습니다.  
  
 Active Directory 디렉터리 서비스에 등록된 Windows ID를 사용하여 MSMQ 큐를 보안할 수도 있습니다. MSMQ를 설치할 때 Active Directory 통합을 설치할 수 있습니다. 이 경우 컴퓨터가 Windows 도메인 네트워크에 속해야 합니다.  
  
 MSMQ에 대 한 자세한 내용은 [msmq (메시지 큐) 설치](../../../../docs/framework/wcf/samples/installing-message-queuing-msmq.md)를 참조 하십시오.  
  
### <a name="netmsmqbinding"></a>NetMsmqBinding  
 NetMsmqBinding >는 wcf에서 MSMQ를 사용 하 여 통신 하는 두 개의 wcf 끝점을 제공 하는 대기 중인 바인딩입니다. [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/netmsmqbinding.md) 따라서 바인딩은 MSMQ에 특정한 속성을 노출합니다. 그러나 모든 MSMQ 기능과 속성이 `NetMsmqBinding`에 노출되는 것은 아닙니다. 압축 `NetMsmqBinding`은 대부분의 고객에게 적합한 최적의 기능들로 디자인되었습니다.  
  
 `NetMsmqBinding`에서는 여기에서 지금까지 설명한 핵심 큐 개념을 바인딩에 대한 속성의 형태로 나타냅니다. 이러한 속성은 메시지를 전송 및 전달하는 방법을 MSMQ에 알려 줍니다. 속성 범주에 대한 자세한 내용은 다음 단원을 참조하세요. 자세한 내용은 특정 속성을 자세히 설명 하는 개념 항목을 참조 하세요.  
  
#### <a name="exactlyonce-and-durable-properties"></a>ExactlyOnce 및 Durable 속성  
 `ExactlyOnce` 및 `Durable` 속성은 큐 사이에서 메시지가 전송되는 방법에 영향을 줍니다.  
  
- `ExactlyOnce`: (기본값) `true` 로 설정 된 경우 대기 중인 채널은 메시지 (배달 된 경우)가 중복 되지 않았는지 확인 합니다. 또한 메시지가 손실되지 않습니다. 메시지를 전달할 수 없거나 메시지를 전달하기 전에 메시지 TTL(Time-To-Live)이 만료되면 실패 메시지가 배달 실패 이유와 함께 배달 못 한 편지 큐에 기록됩니다. `false`로 설정된 경우 대기 중인 채널에서 메시지를 전송하려고 시도합니다. 이 경우 필요에 따라 배달 못한 편지 큐를 선택할 수 있습니다.  
  
- `Durable:``true`(기본값)로 설정되어 있으면 대기 중인 채널에서 MSMQ를 통해 메시지를 디스크에 영구히 저장합니다. 따라서 MSMQ 서비스를 중지했다가 다시 시작하면 디스크에 있는 메시지가 대상 큐에 전송되거나 서비스에 전달됩니다. `false`로 설정되어 있으면 메시지가 임시 저장소에 저장되므로 MSMQ 서비스를 중지했다가 다시 시작하면 손실됩니다.  
  
 `ExactlyOnce` 신뢰할 수 있는 전송을 위해 MSMQ에 트랜잭션 큐가 필요합니다. 또한 MSMQ에서 트랜잭션 큐를 읽으려면 트랜잭션이 필요합니다. 따라서 `NetMsmqBinding`을 사용할 때 `ExactlyOnce`가 `true`로 설정되어 있는 경우 메시지를 보내거나 받으려면 트랜잭션이 필요합니다. 마찬가지로 `ExactlyOnce`가 `false`일 때의 임시 메시징의 경우와 마찬가지로 MSMQ에 비트랜잭션 큐가 있어야 가장 효율적입니다. 따라서 `ExactlyOnce`를 `false`로 설정하거나 durable을 `false`로 설정하면 트랜잭션을 사용하여 메시지를 보내거나 받을 수 없습니다.  
  
> [!NOTE]
> 바인딩의 설정을 기반으로 올바른 큐(트랜잭션 또는 비트랜잭션)가 만들어지는지 확인합니다. `ExactlyOnce`가 `true`이면 트랜잭션 큐를 사용하고, 그렇지 않으면 비트랜잭션 큐를 사용합니다.  
  
#### <a name="dead-letter-queue-properties"></a>배달 못한 편지 큐 속성  
 배달 못한 편지 큐는 배달하지 못한 메시지를 저장하는 데 사용됩니다. 배달 못한 편지 큐에서 메시지를 읽는 보정 논리를 작성할 수 있습니다.  
  
 대부분의 큐 시스템에서는 시스템 차원의 배달 못한 편지 큐를 제공합니다. MSMQ에서는 비트랜잭션 큐에 배달하지 못한 메시지를 위한 시스템 차원의 비트랜잭션 배달 못한 편지 큐와 트랜잭션 큐에 배달하지 못한 메시지를 위한 시스템 차원의 트랜잭션 배달 못한 편지 큐를 제공합니다.  
  
 서로 다른 대상 큐에 메시지를 보내는 여러 클라이언트가 MSMQ 서비스를 공유하는 경우 클라이언트가 보내는 모든 메시지는 동일한 배달 못한 편지 큐로 이동됩니다. 이것이 항상 좋은 것은 아닙니다. 격리를 강화 하기 위해의 [!INCLUDE[wv](../../../../includes/wv-md.md)] WCF 및 MSMQ는 사용자가 배달에 실패 한 메시지를 저장 하도록 지정할 수 있는 사용자 지정 배달 못 한 편지 큐 (또는 응용 프로그램별 배달 못한 편지 큐)를 제공 합니다. 따라서 클라이언트 간에 동일한 배달 못한 편지 큐를 공유하지 않습니다.  
  
 바인딩에는 다음과 같은 두 가지 속성이 필요합니다.  
  
- `DeadLetterQueue`: 이 속성은 배달 못 한 편지 큐가 요청 되었는지 여부를 나타내는 열거형입니다. 요청 시 열거형에는 배달 못 한 편지 큐도 포함됩니다. 값은 `None`, `System` 및 `Custom`입니다. 이러한 속성의 해석에 대 한 자세한 내용은 [배달 못 한 편지 큐를 사용 하 여 메시지 전송 오류 처리](../../../../docs/framework/wcf/feature-details/using-dead-letter-queues-to-handle-message-transfer-failures.md) 를 참조 하세요.  
  
- `CustomDeadLetterQueue`: 이 속성은 응용 프로그램별 배달 못 한 편지 큐의 URI (Uniform Resource Identifier) 주소입니다. 인 경우 `DeadLetterQueue`필요 합니다.`Custom` 을 선택 합니다.  
  
#### <a name="poison-message-handling-properties"></a>포이즌 메시지 처리 속성  
 서비스에서 트랜잭션의 대상 큐에 있는 메시지를 읽을 때 서비스에서 여러 가지 이유로 메시지를 처리하지 못할 수 있습니다. 그러면 메시지를 큐에 넣고 다시 읽습니다. 반복적으로 실패하는 메시지를 처리하려면 바인딩에서 포이즌 메시지 처리 속성을 구성할 수 있습니다. `ReceiveRetryCount`, `MaxRetryCycles`, `RetryCycleDelay` 및 `ReceiveErrorHandling`의 네 가지 속성이 있습니다. 이러한 속성에 대 한 자세한 내용은 [포이즌 메시지 처리](../../../../docs/framework/wcf/feature-details/poison-message-handling.md)를 참조 하세요.  
  
#### <a name="security-properties"></a>보안 속성  
 MSMQ는 큐의 ACL(액세스 제어 목록) 또는 인증된 메시지 보내기와 같은 고유한 보안 모델을 노출합니다. `NetMsmqBinding`은 이러한 보안 속성을 전송 보안 설정의 일부로 노출합니다. 전송 보안의 바인딩에는 `MsmqAuthenticationMode` 및 `MsmqProtectionLevel`의 두 가지 속성이 있습니다. 이러한 속성의 설정은 MSMQ가 구성되는 방법에 따라 다릅니다. 자세한 내용은 [전송 보안을 사용 하 여 메시지 보안](../../../../docs/framework/wcf/feature-details/securing-messages-using-transport-security.md)설정을 참조 하세요.  
  
 전송 보안 이외에 메시지 보안을 사용하여 실제 SOAP 메시지를 보안할 수 있습니다. 자세한 내용은 [메시지 보안을 사용 하 여 메시지](../../../../docs/framework/wcf/feature-details/securing-messages-using-message-security.md)보안을 참조 하세요.  
  
 또한 `MsmqTransportSecurity`는 `MsmqEncryptionAlgorithm` 및 `MsmqHashAlgorithm`의 두 가지 속성을 노출합니다. 이러한 속성은 메시지의 큐 간 전송 암호화와 서명 해시에 대해 선택하는 서로 다른 알고리즘의 열거형입니다.  
  
#### <a name="other-properties"></a>기타 속성  
 이전 속성 외에도 다음과 같은 MSMQ별 속성이 바인딩에 노출됩니다.  
  
- `UseSourceJournal`: 원본 저널링이 설정 되어 있음을 나타내는 속성입니다. 소스 저널링은 전송 큐에서 성공적으로 전송한 메시지를 추적하는 MSMQ 기능입니다.  
  
- `UseMsmqTracing`: MSMQ 추적이 설정 되어 있음을 나타내는 속성입니다. MSMQ 추적은 MSMQ 큐 관리자를 호스트하는 컴퓨터에서 메시지를 보내거나 받을 때마다 보고서 큐에 보고서 메시지를 보냅니다.  
  
- `QueueTransferProtocol`: 큐 간 메시지 전송에 사용할 프로토콜의 열거형입니다. MSMQ는 네이티브 큐 간 전송 프로토콜과 SRMP(SOAP Reliable Messaging Protocol)라는 SOAP 기반 프로토콜을 구현합니다. SRMP는 큐 간 전송에 HTTP 전송을 사용할 때 사용됩니다. SRMP 보안은 큐 간 전송에 HTTPS를 사용할 때 사용됩니다.  
  
- `UseActiveDirectory`: 큐 주소 확인에 Active Directory를 사용 해야 하는지 여부를 나타내는 부울 값입니다. 기본적으로 해제됩니다. 자세한 내용은 [서비스 끝점 및 큐 주소 지정](../../../../docs/framework/wcf/feature-details/service-endpoints-and-queue-addressing.md)을 참조 하세요.  
  
### <a name="msmqintegrationbinding"></a>MsmqIntegrationBinding  
 는 `MsmqIntegrationBinding` WCF 끝점이 C, C++, COM 또는 System. 메시징 api로 작성 된 기존 MSMQ 응용 프로그램과 통신 하도록 하려는 경우에 사용 됩니다.  
  
 바인딩 속성은 `NetMsmqBinding`에서와 같습니다. 그러나 다음과 같은 차이가 적용됩니다.  
  
- `MsmqIntegrationBinding`에 대한 작업 계약은 형식 매개 변수가 본문 형식인 <xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601> 형식의 단일 매개 변수를 사용하도록 제한됩니다.  
  
- 대부분의 MSMQ 네이티브 메시지 속성은 <xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601>에서 사용하도록 노출됩니다.  
  
- 메시지 본문 serialization 및 deserialization을 돕기 위해 XML 및 ActiveX와 같은 serializer가 제공됩니다.  
  
### <a name="sample-code"></a>예제 코드  
 MSMQ를 사용하는 WCF 서비스를 작성하는 방법에 대한 단계별 지침은 다음 항목을 참조하세요.  
  
- [방법: WCF 끝점 및 메시지 큐 응용 프로그램과 메시지 교환](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)  
  
- [방법: WCF 끝점을 사용 하 여 대기 중인 메시지 교환](../../../../docs/framework/wcf/feature-details/how-to-exchange-queued-messages-with-wcf-endpoints.md)  
  
 WCF에서 MSMQ 사용을 보여 주는 전체 코드 샘플은 다음 항목을 참조하세요.  
  
- [트랜잭션된 MSMQ 바인딩](../../../../docs/framework/wcf/samples/transacted-msmq-binding.md)  
  
- [일시 대기 통신](../../../../docs/framework/wcf/samples/volatile-queued-communication.md)  
  
- [배달 못 한 편지 큐](../../../../docs/framework/wcf/samples/dead-letter-queues.md)  
  
- [세션 및 큐](../../../../docs/framework/wcf/samples/sessions-and-queues.md)  
  
- [양방향 통신](../../../../docs/framework/wcf/samples/two-way-communication.md) 
  
- [SRMP](../../../../docs/framework/wcf/samples/srmp.md)  
  
- [메시지 큐에 대한 메시지 보안](../../../../docs/framework/wcf/samples/message-security-over-message-queuing.md)  
  
## <a name="see-also"></a>참고자료

- [서비스 엔드포인트 및 큐 주소 지정](../../../../docs/framework/wcf/feature-details/service-endpoints-and-queue-addressing.md)
- [대기 중인 애플리케이션 웹 호스팅](../../../../docs/framework/wcf/feature-details/web-hosting-a-queued-application.md)
