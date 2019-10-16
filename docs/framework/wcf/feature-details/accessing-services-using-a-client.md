---
title: 클라이언트를 사용하여 서비스 액세스
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c8329832-bf66-4064-9034-bf39f153fc2d
ms.openlocfilehash: 0923fa70907a4846924395483c86e541cd88f284
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964974"
---
# <a name="accessing-services-using-a-client"></a>클라이언트를 사용하여 서비스 액세스
클라이언트 응용 프로그램은 WCF 클라이언트 또는 채널 개체를 만들고 구성 하 고 사용 하 여 서비스와 통신 해야 합니다. [WCF 클라이언트 개요](../../../../docs/framework/wcf/wcf-client-overview.md) 항목에서는 기본 클라이언트 및 채널 개체를 만들고 사용 하는 것과 관련 된 개체 및 단계에 대해 간략하게 설명 합니다.  
  
 이 항목에서는 시나리오에 따라 유용할 수 있는 클라이언트 및 채널 개체와 클라이언트 응용 프로그램과 관련된 몇 가지 문제에 대한 자세한 정보를 제공합니다.  
  
## <a name="overview"></a>개요  
 이 항목에서는 다음과 관련된 동작 및 문제에 대해 설명합니다.  
  
- 채널 및 세션 수명  
  
- 예외 처리  
  
- 블로킹 문제 이해  
  
- 대화형으로 채널 초기화  
  
### <a name="channel-and-session-lifetimes"></a>채널 및 세션 수명  
 WCF (Windows Communication Foundation) 응용 프로그램에는 두 가지 범주의 채널, 데이터 그램 및 세션 포함 됩니다.  
  
 *데이터 그램* 채널은 모든 메시지를 상관 관계가 없는 하는 채널입니다. 데이터그램 채널을 사용할 경우 입력 또는 출력 작업이 실패해도 일반적으로 다음 작업이 영향을 받지 않으며 동일한 채널을 다시 사용할 수 있습니다. 이 때문에 데이터그램 채널은 실패하지 않습니다.  
  
 그러나 *세션* 채널은 다른 끝점에 대 한 연결을 사용 하는 채널입니다. 한쪽의 세션 메시지는 항상 다른 쪽의 동일한 세션과 상호 관련됩니다. 또한 한 세션이 성공한 것으로 간주되려면 해당 세션의 두 참가자가 모두 대화 요구 사항이 충족되었다고 동의해야 합니다. 동의할 수 없는 경우 세션 채널이 실패할 수 있습니다.  
  
 첫 번째 작업을 호출하여 명시적 또는 암시적으로 클라이언트를 엽니다.  
  
> [!NOTE]
> 알림을 받는 시기가 세션 구현에 따라 달라지므로 실패한 세션 채널을 명시적으로 검색하려는 시도는 일반적으로 유용하지 않습니다. 예를 들어 신뢰할 수 있는 세션을 사용하지 않는 <xref:System.ServiceModel.NetTcpBinding?displayProperty=nameWithType>은 TCP 연결의 세션을 표시하므로 서비스 또는 클라이언트의 <xref:System.ServiceModel.ICommunicationObject.Faulted?displayProperty=nameWithType> 이벤트를 수신 대기하면 네트워크 오류가 발생할 경우 신속하게 알림을 받습니다. 그러나 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement?displayProperty=nameWithType>를 사용하는 바인딩으로 설정된 신뢰할 수 있는 세션은 소규모 네트워크 오류로부터 서비스를 분리합니다. 적절한 기간 내에 세션을 다시 설정할 수 있는 경우 보다 긴 기간 동안 중단이 계속될 때까지 신뢰할 수 있는 세션에 대해 구성된 동일한 바인딩이 실패하지 않습니다.  
  
 채널을 응용 프로그램 계층에 노출하는 대부분의 시스템 제공 바인딩은 기본적으로 세션을 사용하지만 <xref:System.ServiceModel.BasicHttpBinding?displayProperty=nameWithType>은 사용하지 않습니다. 자세한 내용은 [를 사용 하 여 세션](../../../../docs/framework/wcf/using-sessions.md)합니다.  
  
### <a name="the-proper-use-of-sessions"></a>적절한 세션 사용  
 세션은 전체 메시지 교환이 완료되었는지 여부 및 양쪽에서 성공했다고 간주하는지 여부를 확인하는 방법을 제공합니다. 호출 응용 프로그램은 하나의 try 블록 내에서 채널을 열고 사용한 후 닫는 것이 좋습니다. 세션 채널이 열려 있고 <xref:System.ServiceModel.ICommunicationObject.Close%2A?displayProperty=nameWithType> 메서드를 한 번 호출한 후 해당 호출이 성공적으로 반환되면 세션이 성공했습니다. 이 경우 성공은 바인딩에서 지정한 모든 배달 보증이 충족되었으며 다른 쪽이 <xref:System.ServiceModel.ICommunicationObject.Abort%2A?displayProperty=nameWithType>를 호출하기 전에 채널에서 <xref:System.ServiceModel.ICommunicationObject.Close%2A>를 호출하지 않았음을 의미합니다.  
  
 다음 섹션에서는 이 클라이언트 접근 방법의 예를 제공합니다.  
  
### <a name="handling-exceptions"></a>예외 처리  
 클라이언트 응용 프로그램의 예외 처리는 단순합니다. 하나의 try 블록 내에서 채널을 열고 사용한 후 닫으면 예외가 throw되지 않는 한 대화가 성공합니다. 일반적으로 예외가 throw되면 대화가 중단됩니다.  
  
> [!NOTE]
> `using` 문(`Using` Visual Basic)은 사용 하지 않는 것이 좋습니다. 이는 `using` 문의 끝에서 예외가 발생하여 사용자가 확인해야 하는 다른 예외를 마스킹할 수 있기 때문입니다. 자세한 내용은 [Close 및 Abort를 사용 하 여 WCF 클라이언트 리소스 해제](../../../../docs/framework/wcf/samples/use-close-abort-release-wcf-client-resources.md)를 참조 하세요.  
  
 다음 코드 예제에서는 `using` 문이 아니라 try/catch 블록을 사용한 권장되는 클라이언트 패턴을 보여 줍니다.  
  
 [!code-csharp[FaultContractAttribute#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/client.cs#3)]
 [!code-vb[FaultContractAttribute#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/client.vb#3)]  
  
> [!NOTE]
> <xref:System.ServiceModel.ICommunicationObject.State%2A?displayProperty=nameWithType> 속성 값 확인은 경합 상태이며 채널을 다시 사용할지 또는 닫을지 결정하는 데 사용하지 않는 것이 좋습니다.  
  
 데이터그램 채널은 닫을 때 예외가 발생하는 경우에도 실패하지 않습니다. 또한 보안 대화를 사용하여 인증할 수 없는 비이중 클라이언트는 일반적으로 <xref:System.ServiceModel.Security.MessageSecurityException?displayProperty=nameWithType>을 throw합니다. 그러나 보안 대화를 사용하는 이중 클라이언트가 인증할 수 없는 경우 클라이언트는 대신 <xref:System.TimeoutException?displayProperty=nameWithType>을 수신합니다.  
  
 응용 프로그램 수준에서 오류 정보를 사용 하는 방법에 대 한 자세한 내용은 [계약 및 서비스에서 오류 지정 및 처리](../../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)를 참조 하세요. 예상 되는 [예외](../../../../docs/framework/wcf/samples/expected-exceptions.md) 는 예상 되는 예외를 설명 하 고이를 처리 하는 방법을 보여줍니다. 채널을 개발할 때 발생 하는 오류를 처리 하는 방법에 대 한 자세한 내용은 [예외 및 오류 처리](../../../../docs/framework/wcf/extending/handling-exceptions-and-faults.md)를 참조 하세요.  
  
### <a name="client-blocking-and-performance"></a>클라이언트 차단 및 성능  
 응용 프로그램에서 동기적으로 request-reply 작업을 호출하는 경우 클라이언트는 반환 값이 수신되거나 <xref:System.TimeoutException?displayProperty=nameWithType> 같은 예외가 throw될 때까지 차단됩니다. 이 동작은 로컬 동작과 유사합니다. 응용 프로그램에서 WCF 클라이언트 개체 또는 채널에 대 한 작업을 동기적으로 호출 하면 클라이언트는 채널 계층에서 네트워크에 데이터를 쓸 수 있을 때까지 또는 예외가 throw 될 때까지 반환 하지 않습니다. <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A?displayProperty=nameWithType>를 `true`로 설정하여 작업을 표시함으로써 지정된 단방향 메시지 교환 패턴은 일부 클라이언트의 응답을 향상시키지만 바인딩 및 이미 전송된 메시지에 따라 단방향 작업이 차단될 수도 있습니다. 단방향 작업은 메시지 교환에만 사용됩니다. 자세한 내용은 [단방향 서비스](../../../../docs/framework/wcf/feature-details/one-way-services.md)합니다.  
  
 큰 데이터 청크는 메시지 교환 패턴에 관계없이 클라이언트 처리 속도를 저하시킬 수 있습니다. 이러한 문제를 처리 하는 방법을 이해 하려면 [대량 데이터 및 스트리밍](../../../../docs/framework/wcf/feature-details/large-data-and-streaming.md)을 참조 하세요.  
  
 작업이 완료 되는 동안 응용 프로그램에서 더 많은 작업을 수행 해야 하는 경우 WCF 클라이언트가 구현 하는 서비스 계약 인터페이스에 비동기 메서드 쌍을 만들어야 합니다. 이 작업을 수행 하는 가장 쉬운 방법은 `/async` [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)에서 스위치를 사용 하는 것입니다. 예는 [방법: 서비스 작업을 비동기적](../../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md)으로 호출 합니다.  
  
 클라이언트 성능 향상에 대 한 자세한 내용은 [중간 계층 클라이언트 응용 프로그램](../../../../docs/framework/wcf/feature-details/middle-tier-client-applications.md)을 참조 하세요.  
  
### <a name="enabling-the-user-to-select-credentials-dynamically"></a>사용자가 동적으로 자격 증명을 선택할 수 있도록 설정  
 <xref:System.ServiceModel.Dispatcher.IInteractiveChannelInitializer> 인터페이스를 사용하면 응용 프로그램이 시간 제한 타이머가 시작되기 전에 채널을 만드는 데 사용할 자격 증명을 사용자가 선택할 수 있도록 하는 사용자 인터페이스를 표시할 수 있습니다.  
  
 응용 프로그램 개발자는 삽입된 <xref:System.ServiceModel.Dispatcher.IInteractiveChannelInitializer>를 두 가지 방법으로 사용할 수 있습니다. 클라이언트 응용 프로그램은 채널을 <xref:System.ServiceModel.ClientBase%601.DisplayInitializationUI%2A?displayProperty=nameWithType> 열기 <xref:System.ServiceModel.IClientChannel.DisplayInitializationUI%2A?displayProperty=nameWithType> 전에 또는 (또는 비동기 버전)를 호출 하거나 ( *명시적* 방법) 첫 번째 작업 ( *암시적* 방법)을 호출할 수 있습니다.  
  
 암시적 방법을 사용하는 경우 응용 프로그램은 <xref:System.ServiceModel.ClientBase%601> 또는 <xref:System.ServiceModel.IClientChannel> 확장에서 첫 번째 작업을 호출해야 합니다. 다른 작업을 호출하면 예외가 throw됩니다.  
  
 명시적 방법을 사용하는 경우 애플리케이션은 다음 단계를 순서대로 수행해야 합니다.  
  
1. <xref:System.ServiceModel.ClientBase%601.DisplayInitializationUI%2A?displayProperty=nameWithType> 또는 <xref:System.ServiceModel.IClientChannel.DisplayInitializationUI%2A?displayProperty=nameWithType>(또는 비동기 버전)를 호출합니다.  
  
2. 이니셜라이저가 반환되면 <xref:System.ServiceModel.ICommunicationObject.Open%2A> 개체 또는 <xref:System.ServiceModel.IClientChannel> 속성에서 반환된 <xref:System.ServiceModel.IClientChannel> 개체에서 <xref:System.ServiceModel.ClientBase%601.InnerChannel%2A?displayProperty=nameWithType> 메서드를 호출합니다.  
  
3. 작업을 호출합니다.  
  
 프로덕션 품질 응용 프로그램에서는 명시적 방법을 사용하여 사용자 인터페이스 프로세스를 제어하는 것이 좋습니다.  
  
 암시적 방법을 사용하는 애플리케이션은 사용자 인터페이스 이니셜라이저를 호출하지만, 애플리케이션 사용자가 바인딩에 대한 전송 시간 제한 내에 응답하지 않을 경우 사용자 인터페이스가 반환될 때 예외가 throw됩니다.  
  
## <a name="see-also"></a>참고자료

- [이중 서비스](../../../../docs/framework/wcf/feature-details/duplex-services.md)
- [방법: 단방향 및 요청-회신 계약을 사용 하 여 서비스 액세스](../../../../docs/framework/wcf/feature-details/how-to-access-wcf-services-with-one-way-and-request-reply-contracts.md)
- [방법: 이중 계약을 사용 하 여 서비스 액세스](../../../../docs/framework/wcf/feature-details/how-to-access-services-with-a-duplex-contract.md)
- [방법: WSE 3.0 서비스 액세스](../../../../docs/framework/wcf/feature-details/how-to-access-a-wse-3-0-service-with-a-wcf-client.md)
- [방법: ChannelFactory 사용](../../../../docs/framework/wcf/feature-details/how-to-use-the-channelfactory.md)
- [방법: 비동기적으로 서비스 작업 호출](../../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md)
- [중간 계층 클라이언트 응용 프로그램](../../../../docs/framework/wcf/feature-details/middle-tier-client-applications.md)
