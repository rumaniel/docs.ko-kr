---
title: 세션 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- sessions [WCF]
ms.assetid: 864ba12f-3331-4359-a359-6d6d387f1035
ms.openlocfilehash: 671e650a494d314ec1da1957eaae91e2d1811213
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69952833"
---
# <a name="using-sessions"></a>세션 사용
WCF (Windows Communication Foundation) 응용 프로그램에서 *세션* 은 메시지 그룹을 대화에 연결 합니다. WCF 세션은 ASP.NET 응용 프로그램에서 사용할 수 있는 세션 개체와 다르며, 다른 동작을 지원 하 고 다양 한 방법으로 제어 됩니다. 이 항목에서는 WCF 응용 프로그램에서 세션을 사용 하는 기능과 사용 방법에 대해 설명 합니다.  
  
## <a name="sessions-in-windows-communication-foundation-applications"></a>Windows Communication Foundation 애플리케이션의 세션  
 서비스 계약에서 세션이 필요하도록 지정할 경우 해당 계약은 모든 호출(즉, 호출을 지원하는 기본 메시지 교환)이 동일한 대화의 일부가 되도록 지정합니다. 계약이 세션을 허용하지만 특정 세션이 필요 없음을 지정하는 경우, 클라이언트는 세션을 연결하여 설정하거나 설정하지 않을 수 있습니다. 세션이 종료되고 메시지가 동일한 채널을 통해 전송될 경우 예외가 throw됩니다.  
  
 WCF 세션에는 다음과 같은 주요 개념 기능이 있습니다.  
  
- 이러한 기능은 호출 애플리케이션(WCF 클라이언트)에 의해 명시적으로 시작되고 종료됩니다.  
  
- 한 세션 동안 배달된 메시지는 수신된 순서대로 처리됩니다.  
  
- 세션은 메시지 그룹을 대화에 연결합니다. 여러 유형의 상관 관계를 사용할 수 있습니다. 예를 들어, 공유된 네트워크 연결을 기반으로 메시지와 연결될 수 있는 세션 기반 채널이 있는 반면 메시지 본문의 공유 태그를 기반으로 메시지와 연결될 수 있는 세션 기반 채널도 있습니다. 세션에서 파생될 수 있는 기능은 상관 관계의 특성에 따라 다릅니다.  
  
- WCF 세션과 연결 된 일반 데이터 저장소는 없습니다.  
  
 ASP.NET 응용 프로그램의 <xref:System.Web.SessionState.HttpSessionState?displayProperty=nameWithType> 클래스와이 클래스에서 제공 하는 기능에 대해 잘 알고 있는 경우 해당 종류의 세션과 WCF 세션 간에 다음과 같은 차이점을 알 수 있습니다.  
  
- ASP.NET 세션은 항상 서버에서 시작 됩니다.  
  
- ASP.NET 세션은 암시적으로 순서가 지정 되지 않습니다.  
  
- ASP.NET 세션은 요청에 대해 일반 데이터 저장소 메커니즘을 제공 합니다.  
  
 이 항목에서는 다음을 설명합니다.  
  
- 서비스 모델 계층에서 세션 기반 바인딩을 사용하는 경우 기본 실행 동작  
  
- WCF 세션 기반 시스템 제공 바인딩이 제공 하는 기능 유형입니다.  
  
- 세션 요구 사항을 선언하는 계약을 만드는 방법  
  
- 세션의 생성과 종료 및 세션과 서비스 인스턴스와의 관계를 이해하고 제어하는 방법  
  
## <a name="default-execution-behavior-using-sessions"></a>세션을 사용한 기본 실행 동작  
 세션을 초기화하려는 바인딩은 *세션 기반* 바인딩에서 호출됩니다. 서비스 계약에서는 서비스 계약 인터페이스(또는 클래스)의 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=nameWithType> 속성을 <xref:System.ServiceModel.SessionMode?displayProperty=nameWithType> 열거형 값 중 하나로 설정하여 세션 기반 바인딩을 필요로 하거나 허용하거나 거부하도록 지정합니다. 기본적으로이 속성의 값은입니다 <xref:System.ServiceModel.SessionMode.Allowed>. 즉, 클라이언트가 WCF 서비스 구현과 함께 세션 기반 바인딩을 사용 하는 경우 서비스는 제공 된 세션을 설정 하 고 사용 합니다.  
  
 WCF 서비스가 클라이언트 세션을 허용 하는 경우 기본적으로 다음 기능이 사용 됩니다.  
  
1. WCF 클라이언트 개체 간의 모든 호출은 동일한 서비스 인스턴스에 의해 처리 됩니다.  
  
2. 다른 세션 기반 바인딩은 추가 기능을 제공합니다.  
  
## <a name="system-provided-session-types"></a>시스템 제공 세션 유형  
 세션 기반 바인딩은 서비스 인스턴스와 특정 세션과의 기본 연결을 지원합니다. 그러나 다른 세션 기반 바인딩은 앞서 설명한 세션 기반 인스턴스 만들기를 제어할 수 있는 기능 이외에 다른 기능을 지원합니다.  
  
 WCF는 다음과 같은 유형의 세션 기반 응용 프로그램 동작을 제공 합니다.  
  
- <xref:System.ServiceModel.Channels.SecurityBindingElement?displayProperty=nameWithType>는 통신의 양쪽 끝에서 특정 보안 대화에 동의한 보안 기반 세션을 지원합니다. 자세한 내용은 [Securing Services](../../../docs/framework/wcf/securing-services.md)합니다. 예를 들어, 보안 세션과 신뢰할 수 있는 세션 모두에 대한 지원이 포함된 <xref:System.ServiceModel.WSHttpBinding?displayProperty=nameWithType> 바인딩은 기본적으로 메시지에 대해 암호화 및 디지털 서명을 수행하는 보안 세션만 사용합니다.  
  
- <xref:System.ServiceModel.NetTcpBinding?displayProperty=nameWithType> 바인딩은 모든 메시지가 소켓 수준에서 연결을 통해 상호 연결되도록 TCP/IP 기반 세션을 지원합니다.  
  
- WS-ReliableMessaging 사양을 구현하는 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement?displayProperty=nameWithType> 요소는 신뢰할 수 있는 세션에 대한 지원을 제공합니다. 신뢰할 수 있는 세션에서는 메시지를 순서대로 정확히 한 번 배달하도록 구성하여 대화 중에 여러 노드에서 메시지가 전달되는 경우에도 메시지가 수신되도록 할 수 있습니다. 자세한 내용은 [신뢰할 수 있는 세션](../../../docs/framework/wcf/feature-details/reliable-sessions.md)합니다.  
  
- <xref:System.ServiceModel.NetMsmqBinding?displayProperty=nameWithType> 바인딩은 MSMQ 데이터그램 세션을 제공합니다. 자세한 내용은 [WCF의 큐](../../../docs/framework/wcf/feature-details/queues-in-wcf.md)합니다.  
  
 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A> 속성을 설정하면 계약에 필요한 세션 유형을 지정하지 않고 요구만 합니다.  
  
## <a name="creating-a-contract-that-requires-a-session"></a>세션이 필요한 계약 만들기  
 세션이 필요한 계약을 만들면 서비스 계약이 선언한 작업 그룹 모두가 같은 세션 내에서 실행되고 해당 메시지가 순서대로 배달되어야 합니다. 서비스 계약이 필요한 세션 지원 수준을 어설션하려면 서비스 계약 인터페이스 또는 클래스의 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=nameWithType> 속성을 <xref:System.ServiceModel.SessionMode?displayProperty=nameWithType> 열거형 값으로 설정하여 계약에서 다음을 지정합니다.  
  
- 세션이 필요한지 여부  
  
- 클라이언트가 세션을 설정하도록 허용할지 여부  
  
- 세션을 금지할지 여부  
  
 그러나 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A> 속성을 설정하면 계약에 필요한 세션 기반 동작 유형을 지정하지 않습니다. WCF는 런타임에 서비스에 대해 구성 된 바인딩 (통신 채널 생성)이 서비스를 구현할 때 세션을 수행 하는지 여부를 확인 하도록 지시 합니다. 또한 바인딩은 보안 동작, 전송 동작, 신뢰할 수 있는 동작 또는 이러한 동작의 조합 중에서 선택한 세션 기반 동작 유형과 함께 해당 요구 사항을 충족할 수 있습니다. 정확한 동작은 선택한 <xref:System.ServiceModel.SessionMode?displayProperty=nameWithType> 값에 따라 다릅니다. 서비스에 대해 구성된 바인딩이 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A>의 값을 준수하지 않는 경우 예외가 throw됩니다. 바인딩 및 세션을 지원하도록 바인딩이 만든 채널을 세션 기반이라고 합니다.  
  
 다음 서비스 계약은 `ICalculatorSession` 의 모든 작업이 세션 내에서 교환되도록 지정합니다. `Equals` 메서드를 제외하고 호출자에게 값을 반환하는 작업은 없습니다. 그러나 `Equals` 메서드는 매개 변수를 가져오지 않기 때문에 다른 작업에 데이터를 이미 전달한 세션 내에서 0이 아닌 값만 반환할 수 있습니다. 이 계약에서 세션이 제대로 작동해야 합니다. 특정 클라이언트와 연결된 세션 없이 서비스 인스턴스는 이 클라이언트가 보낸 이전 데이터를 알 수 없습니다.  
  
 [!code-csharp[S_Service_Session#1](../../../samples/snippets/csharp/VS_Snippets_CFX/s_service_session/cs/service.cs#1)]
 [!code-vb[S_Service_Session#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_service_session/vb/service.vb#1)]  
  
 서비스에서 세션을 허용하는 경우 클라이언트가 세션을 초기화하면 세션이 설정되어 사용됩니다. 그렇지 않으면 세션이 설정되지 않습니다.  
  
## <a name="sessions-and-service-instances"></a>세션 및 서비스 인스턴스  
 WCF에서 기본 인스턴스 만들기 동작을 사용 하는 경우 WCF 클라이언트 개체 간의 모든 호출은 동일한 서비스 인스턴스에 의해 처리 됩니다. 따라서 애플리케이션 수준에서 세션은 로컬 호출 동작과 비슷하게 애플리케이션 동작을 사용한다고 간주할 수 있습니다. 예를 들어, 로컬 개체를 만들 때 다음이 수행됩니다.  
  
- 생성자가 호출됩니다.  
  
- WCF 클라이언트 개체 참조에 대해 수행 되는 모든 후속 호출은 동일한 개체 인스턴스에 의해 처리 됩니다.  
  
- 개체 참조가 소멸되면 소멸자가 호출됩니다.  
  
 세션에서는 기본 서비스 인스턴스 동작이 사용되는 한 클라이언트와 서비스 간의 비슷한 동작을 사용할 수 있습니다. 서비스 계약에서 세션이 필요하거나 지원하는 경우 <xref:System.ServiceModel.OperationContractAttribute.IsInitiating%2A> 및 <xref:System.ServiceModel.OperationContractAttribute.IsTerminating%2A> 속성을 설정하여 하나 이상의 계약 작업을 세션 시작 또는 세션 종료로 표시할 수 있습니다.  
  
 *시작 작업* 은 새 세션의 첫 번째 작업으로 호출해야 하는 작업입니다. 하나 이상의 작업을 호출한 후에만 시작 작업이 아닌 작업을 호출할 수 있습니다. 따라서 서비스 인스턴스 시작에 해당하는 클라이언트에서 입력을 가져오도록 디자인된 시작 작업을 선언하여 해당 서비스에 맞는 특정 유형의 세션 생성자를 만들 수 있습니다. 상태는 세션과 연결되지만 서비스 개체와 연결되지는 않습니다.  
  
 반대로*종료 작업*은 기존 세션에서 마지막 메시지로 호출해야 하는 작업입니다. 기본적으로 WCF에서는 서비스와 연결된 세션이 닫힌 후에 서비스 개체 및 컨텍스트를 재활용합니다. 따라서 서비스 인스턴스의 마지막에 해당하는 기능을 수행하도록 디자인된 종료 작업을 선언하여 특정 유형의 소멸자를 만들 수 있습니다.  
  
> [!NOTE]
> 기본 동작은 로컬 생성자 및 소멸자와 비슷하지만 일치하지는 않습니다. 모든 WCF 서비스 작업은 시작 또는 종료 작업 이거나 동시에 두 작업을 모두 수행할 수 있습니다. 또한 기본적으로 횟수와 순서에 관계없이 시작 작업을 호출할 수 있습니다. <xref:System.ServiceModel.InstanceContext?displayProperty=nameWithType> 개체를 조작하여 서비스 인스턴스의 수명을 명시적으로 지정하지 않는 한 세션이 설정되고 인스턴스와 연결되면 추가 세션이 생성되지 않습니다. 마지막으로 상태는 세션과 연결되고 서비스 개체와는 연결되지 않습니다.  
  
 예를 들어 앞 `ICalculatorSession` 의 예제에서 사용 된 계약을 사용 하려면 wcf 클라이언트 개체가 먼저 다른 작업 `Clear` 을 수행 하기 전에 작업을 호출 해야 하며,이 wcf 클라이언트 개체를 사용 하는 세션은를 호출할때종료되어야합니다.`Equals` 작업. 다음 코드 예제에서는 이러한 요구 사항을 적용하는 계약을 보여 줍니다. 먼저`Clear` 를 호출하여 세션을 시작해야 하며, `Equals` 을 호출하면 세션이 끝납니다.  
  
 [!code-csharp[SCA.IsInitiatingIsTerminating#1](../../../samples/snippets/csharp/VS_Snippets_CFX/sca.isinitiatingisterminating/cs/service.cs#1)]
 [!code-vb[SCA.IsInitiatingIsTerminating#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/sca.isinitiatingisterminating/vb/service.vb#1)]  
  
 서비스는 클라이언트와 함께 세션을 시작하지 않습니다. WCF 클라이언트 응용 프로그램에서 세션 기반 채널의 수명과 세션 자체의 수명 사이에 직접적인 관계가 있습니다. 예를 들어, 클라이언트는 새 세션 기반 채널을 만들어 새 세션을 만들고 세션 기반 채널을 정상적으로 닫아서 기존 세션을 종료합니다. 클라이언트는 다음 중 하나를 호출하여 서비스 엔드포인트와 함께 세션을 시작합니다.  
  
- <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType>에 대한 호출을 통해 반환된 채널의 <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A?displayProperty=nameWithType>  
  
- <xref:System.ServiceModel.ClientBase%601.Open%2A?displayProperty=nameWithType>[ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)에서 생성 한 WCF 클라이언트 개체입니다.  
  
- WCF 클라이언트 개체의 각 형식에 대 한 시작 작업 (기본적으로 모든 작업이 시작 됨) 첫 번째 작업을 호출 하면 WCF 클라이언트 개체가 자동으로 채널을 열고 세션을 시작 합니다.  
  
 일반적으로 클라이언트는 다음 중 하나를 호출하여 서비스 엔드포인트와 함께 세션을 종료합니다.  
  
- <xref:System.ServiceModel.ICommunicationObject.Close%2A?displayProperty=nameWithType>에 대한 호출을 통해 반환된 채널의 <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A?displayProperty=nameWithType>  
  
- <xref:System.ServiceModel.ClientBase%601.Close%2A?displayProperty=nameWithType>Svcutil.exe에 의해 생성 된 WCF 클라이언트 개체입니다.  
  
- WCF 클라이언트 개체의 두 형식에 대 한 종료 작업입니다. 기본적으로 작업은 종료 되지 않으며 계약은 종료 작업을 명시적으로 지정 해야 합니다. 첫 번째 작업을 호출 하면 WCF 클라이언트 개체가 자동으로 채널을 열고 세션을 시작 합니다.  
  
 예제는 [방법: [기본 서비스 동작](../../../docs/framework/wcf/samples/default-service-behavior.md) 및 [인스턴스](../../../docs/framework/wcf/samples/instancing.md) 샘플](../../../docs/framework/wcf/feature-details/how-to-create-a-service-that-requires-sessions.md) 뿐만 아니라 세션이 필요한 서비스를 만듭니다.  
  
 클라이언트 및 세션에 대 한 자세한 내용은 [WCF 클라이언트를 사용 하 여 서비스 액세스](../../../docs/framework/wcf/feature-details/accessing-services-using-a-client.md)를 참조 하세요.  
  
## <a name="sessions-interact-with-instancecontext-settings"></a>세션이 InstanceContext 설정과 상호 작용  
 계약의 <xref:System.ServiceModel.SessionMode> 열거형과 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> 속성 간에 상호 작용이 있으며, 이를 통해 채널과 특정 서비스 개체 간의 연결을 제어합니다. 자세한 내용은 [세션, 인스턴스 및 동시성](../../../docs/framework/wcf/feature-details/sessions-instancing-and-concurrency.md)을 참조 하세요.  
  
### <a name="sharing-instancecontext-objects"></a>InstanceContext 개체 공유  
 또한 해당 연결을 직접 수행하여 <xref:System.ServiceModel.InstanceContext> 개체와 연결된 세션 기반 채널 또는 호출을 제어할 수도 있습니다. 
  
## <a name="sessions-and-streaming"></a>세션 및 스트리밍  
 전송할 데이터가 많은 경우 WCF의 스트리밍 전송 모드는 메모리에서 메시지를 전체적으로 버퍼링 하 고 처리 하는 기본 동작에 대 한 적절 한 대안입니다. 세션 기반 바인딩을 통해 스트리밍 호출이 수행될 경우 예기치 못한 동작이 발생할 수 있습니다. 모든 스트리밍 호출은 사용 중인 바인딩이 세션을 사용하도록 구성된 경우에도 세션을 지원하지 않는 하나의 채널(데이터그램 채널)을 통해 수행됩니다. 여러 클라이언트에서 세션 기반 바인딩을 통해 동일한 서비스 개체에 대한 스트리밍 호출을 수행하고, 서비스 개체의 동시성 모드가 단일 모드로 설정되고, 서비스 개체의 인스턴스 컨텍스트 모드가 `PerSession`으로 설정된 경우, 모든 호출은 데이터그램 채널을 통해 수행되므로 한 번에 하나의 호출만 처리됩니다. 하나 이상의 클라이언트의 제한 시간이 초과될 수 있습니다. 이 문제는 서비스 개체의 `InstanceContextMode` 를 `PerCall` 로 설정하거나 동시성 모드를 다중 모드로 설정하여 해결할 수 있습니다.  
  
> [!NOTE]
> 이 경우 사용할 수 있는 "세션"이 하나이기 때문에 MaxConcurrentSessions에는 영향을 주지 않습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.OperationContractAttribute.IsInitiating%2A>
- <xref:System.ServiceModel.OperationContractAttribute.IsTerminating%2A>
