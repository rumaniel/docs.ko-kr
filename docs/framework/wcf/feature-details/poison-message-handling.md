---
title: 포이즌 메시지 처리
ms.date: 03/30/2017
ms.assetid: 8d1c5e5a-7928-4a80-95ed-d8da211b8595
ms.openlocfilehash: 4813629f5ceec1c1b50dfcebe901f4bc25392ec7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69909835"
---
# <a name="poison-message-handling"></a>포이즌 메시지 처리
*포이즌 메시지* 는 응용 프로그램에 대 한 최대 배달 시도 횟수를 초과한 메시지입니다. 큐 기반 응용 프로그램에서 오류로 인해 메시지를 처리할 수 없는 경우 이러한 상황이 발생할 수 있습니다. 안정성 요청을 충족하려면 대기 중인 응용 프로그램이 트랜잭션에서 메시지를 받습니다. 대기 중인 메시지를 받은 트랜잭션을 중단하면 메시지가 큐에 남으므로 새 트랜잭션에서 해당 메시지가 다시 시도됩니다. 트랜잭션의 중단 문제가 해결되지 않은 경우에는 수신 응용 프로그램이 최대 전달 시도 횟수를 초과할 때까지 같은 메시지를 받고 중단하는 루프에 갇히고, 포이즌 메시지가 발생합니다.  
  
 메시지는 여러 가지 이유로 포이즌 메시지가 될 수 있습니다. 가장 일반적인 이유는 응용 프로그램마다 고유하기 때문입니다. 예를 들어 응용 프로그램이 큐에서 메시지를 읽고 일부 데이터베이스 처리를 수행하면 응용 프로그램이 데이터베이스에 대한 잠금을 얻지 못해 트랜잭션이 중단될 수 있습니다. 데이터베이스 트랜잭션이 중단되었기 때문에 메시지가 큐에 남아 있으며 이로 인해 두 번째에서는 응용 프로그램이 메시지를 다시 읽고 데이터베이스에 대한 잠금을 얻도록 시도합니다. 메시지에 잘못된 정보가 들어 있는 경우 해당 메시지는 포이즌 메시지가 될 수도 있습니다. 예를 들면, 구매 주문서에 잘못된 고객 번호가 포함될 수 있습니다. 이 경우 응용 프로그램이 트랜잭션을 중단하고 메시지가 포이즌 메시지가 되도록 지정할 수 있습니다.  
  
 경우에 따라 메시지가 응용 프로그램에 디스패치되지 않을 수도 있습니다. WCF (Windows Communication Foundation) 계층에서는 메시지에 잘못 된 프레임이 있거나, 잘못 된 메시지 자격 증명이 연결 되었거나, 잘못 된 작업 헤더가 있는 경우와 같이 메시지 문제를 찾을 수 있습니다. 이러한 경우 응용 프로그램이 메시지를 받지는 않지만 메시지가 포이즌 메시지가 될 수 있으며 그러한 메시지는 수동으로 처리할 수 있습니다.  
  
## <a name="handling-poison-messages"></a>포이즌 메시지 처리  
 WCF에서 포이즌 메시지 처리는 응용 프로그램에 디스패치할 수 없는 메시지를 처리 하는 수신 응용 프로그램이 나 응용 프로그램에 디스패치 되었지만 응용 프로그램 전용으로 인해 처리 되지 않는 메시지를 처리 하는 메커니즘을 제공 합니다. 이유. 포이즌 메시지 처리는 대기 중인 사용 가능한 각 바인딩에서 다음 속성으로 구성됩니다.  
  
- `ReceiveRetryCount`. 응용 프로그램 큐에서 응용 프로그램으로 메시지 전달을 다시 시도하는 최대 횟수를 나타내는 정수 값입니다. 기본값은 5입니다. 이 값은 데이터베이스의 임시 교착 상태처럼 문제 해결을 즉시 다시 시도하는 경우 충분합니다.  
  
- `MaxRetryCycles`. 최대 재시도 주기 수를 나타내는 정수 값입니다. 재시도 주기는 응용 프로그램 큐에서 재시도 하위 큐로 메시지를 전송하고, 구성 가능한 지연 시간 이후 재시도 하위 큐에서 전달을 다시 시도할 응용 프로그램 큐로 메시지를 다시 전송하는 것으로 구성됩니다. 기본값은 2입니다. [!INCLUDE[wv](../../../../includes/wv-md.md)]에서는 메시지가 최대 (`ReceiveRetryCount` +1) * (`MaxRetryCycles` + 1)회까지 시도됩니다. `MaxRetryCycles`는 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서 무시됩니다.  
  
- `RetryCycleDelay`. 재시도 주기 사이의 지연 시간입니다. 기본값은 30분입니다. `MaxRetryCycles` 및 `RetryCycleDelay`는 함께 정기적인 지연 시간 이후 재시도로 문제를 해결하는 문제 해결 메커니즘을 제공합니다. 예를 들면, 이 핸들은 SQL Server의 보류 중인 트랜잭션 커밋에 설정된 잠긴 행을 처리합니다.  
  
- `ReceiveErrorHandling`. 최대 재시도 횟수만큼 시도한 후에 전달하지 못한 메시지에 대해 수행할 작업을 나타내는 열거입니다. 이 값은 Fault, Drop, Reject 및 Move일 수 있습니다. 기본 옵션은 Fault입니다.  
  
- Fault. 이 옵션은 `ServiceHost`에 오류를 일으키는 수신기에 오류를 보냅니다. 애플리케이션이 큐의 메시지를 계속 처리하려면 외부 메커니즘을 통해 애플리케이션 큐에서 메시지를 제거해야 합니다.  
  
- Drop. 이 옵션은 포이즌 메시지를 삭제하므로 메시지가 응용 프로그램에 전달되지 않습니다. 메시지의 `TimeToLive` 속성이 이 시점에서 만료되면 메시지가 보낸 사람의 배달 못 한 큐에 표시될 수 있습니다. 그렇지 않으면 메시지는 아무 곳에서도 표시되지 않습니다. 이 옵션은 메시지가 손실된 경우 사용자가 수행할 작업을 지정하지 않았음을 나타냅니다.  
  
- Reject. 이 옵션은 [!INCLUDE[wv](../../../../includes/wv-md.md)]에서만 사용할 수 있습니다. 이 옵션은 메시지 큐(MSMQ)에 응용 프로그램이 메시지를 받을 수 없는 전송 큐 관리자에게 부정 승인을 다시 보내도록 지시합니다. 이 메시지는 전송 큐 관리자의 배달 못한 편지 큐에 배치됩니다.  
  
- Move. 이 옵션은 [!INCLUDE[wv](../../../../includes/wv-md.md)]에서만 사용할 수 있습니다. 이 옵션은 포이즌 메시지 처리 응용 프로그램이 나중에 처리할 수 있도록 포이즌 메시지를 포이즌 메시지 큐로 이동합니다. 포이즌 메시지 큐는 응용 프로그램 큐의 하위 큐입니다. 포이즌 메시지 처리 응용 프로그램은 포이즌 큐에서 메시지를 읽는 WCF 서비스 일 수 있습니다. 포이즌 큐는 응용 프로그램 큐의 하위 큐 이며, oison로 주소를 지정할 수 있습니다. 여기서\< *machine-name* 은 큐가 있는 컴퓨터의 이름입니다;p.>/ 가 있으며 *Applicationqueue* 는 응용 프로그램별 큐의 이름입니다.  
  
 다음은 메시지에 대한 최대 전달 시도 횟수입니다.  
  
- [!INCLUDE[wv](../../../../includes/wv-md.md)]의 경우, ((ReceiveRetryCount+1) * (MaxRetryCycles + 1))  
  
- [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]의 경우, (ReceiveRetryCount + 1)  
  
> [!NOTE]
> 전달된 메시지에 대해서는 다시 시도하지 않습니다.  
  
 메시지 읽기를 시도한 횟수를 추적하려면 [!INCLUDE[wv](../../../../includes/wv-md.md)]에서 중단 횟수를 계산하는 지속적 메시지 속성과, 응용 프로그램 큐와 하위 큐 사이에서 메시지를 이동한 횟수를 계산하는 이동 횟수 속성을 관리합니다. WCF 채널은이를 사용 하 여 수신 다시 시도 횟수 및 재시도 주기 수를 계산 합니다. [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및[!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서 중단 횟수는 WCF 채널에 의해 메모리에서 유지 관리 되며 응용 프로그램에 오류가 발생 하면 다시 설정 됩니다. 또한 WCF 채널은 언제 든 지 메모리에 최대 256 메시지의 중단 횟수를 보유할 수 있습니다. 257번째 메시지를 읽으면 가장 오래된 메시지의 중단 횟수가 재설정됩니다.  
  
 중단 횟수와 이동 횟수 속성은 작업 컨텍스트를 통해 서비스 작업에 사용할 수 있습니다. 다음 코드 예제에서는 이러한 속성에 액세스하는 방법을 보여 줍니다.  
  
 [!code-csharp[S_UE_MSMQ_Poison#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ue_msmq_poison/cs/service.cs#1)]  
  
 WCF는 다음과 같은 두 개의 표준 대기 중인 바인딩을 제공 합니다.  
  
- <xref:System.ServiceModel.NetMsmqBinding>. 다른 WCF 끝점과의 큐 기반 통신을 수행 하는 데 적합 한 .NET Framework 바인딩입니다.  
  
- <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>. 기존 메시지 큐 응용 프로그램과 통신하는 데 적합한 바인딩입니다.  
  
> [!NOTE]
> WCF 서비스의 요구 사항에 따라 이러한 바인딩에서 속성을 변경할 수 있습니다. 전체 포이즌 메시지 처리 메커니즘은 수신 응용 프로그램에 로컬입니다. 프로세스는 수신 응용 프로그램이 최종적으로 부정 승인을 중지하고 발신자에게 다시 보내지 않으면 송신 응용 프로그램에 표시되지 않습니다. 이 경우 메시지가 발신자의 배달 못 한 큐로 이동됩니다.  
  
## <a name="best-practice-handling-msmqpoisonmessageexception"></a>모범 사례: MsmqPoisonMessageException 처리  
 서비스에서 메시지가 포이즌임을 확인하면 대기 중인 전송이 포이즌 메시지의 <xref:System.ServiceModel.MsmqPoisonMessageException>를 포함하는 `LookupId`을 throw합니다.  
  
 수신 응용 프로그램이 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 인터페이스를 구현하여 응용 프로그램에서 요청하는 모든 오류를 처리할 수 있습니다. 자세한 내용은 [오류 처리 및 보고에 대 한 제어 확장](../../../../docs/framework/wcf/samples/extending-control-over-error-handling-and-reporting.md)을 참조 하세요.  
  
 응용 프로그램에서 서비스가 큐의 남은 메시지에 액세스할 수 있도록 포이즌 메시지를 포이즌 메시지 큐로 이동하는 몇 가지 포이즌 메시지 자동 처리 작업이 필요할 수 있습니다. <xref:System.ServiceModel.Configuration.MsmqBindingElementBase.ReceiveErrorHandling%2A> 설정이 <xref:System.ServiceModel.ReceiveErrorHandling.Fault>로 설정된 경우에만 오류 처리 메커니즘을 사용하여 포이즌 메시지 예외를 수신 대기할 수 있습니다. 메시지 큐 3.0의 포이즌 메시지 샘플은 이 동작을 보여 줍니다. 다음에서는 최선의 방법을 포함하여 포이즌 메시지를 처리하는 단계를 간략히 보여 줍니다.  
  
1. 포이즌 설정이 응용 프로그램의 요구 사항을 반영하는지 확인합니다. 설정할 때 [!INCLUDE[wv](../../../../includes/wv-md.md)], [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 간 메시지 큐 기능의 차이점을 알고 있어야 합니다.  
  
2. 필요한 경우 `IErrorHandler`를 구현하여 포이즌 메시지 오류를 처리합니다. `ReceiveErrorHandling`을 `Fault`로 설정하려면 큐에서 포이즌 메시지를 제거하거나 외부 종속 문제를 해결하는 수동 메커니즘이 필요하므로 일반적인 사용법은 다음 코드처럼 `IErrorHandler`이 `ReceiveErrorHandling`로 설정된 경우 `Fault`를 구현하는 것입니다.  
  
     [!code-csharp[S_UE_MSMQ_Poison#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ue_msmq_poison/cs/poisonerrorhandler.cs#2)]  
  
3. 서비스 동작에서 사용할 수 있는 `PoisonBehaviorAttribute`를 만듭니다. 이렇게 하면 디스패처에 `IErrorHandler`가 설치됩니다. 다음 코드 예제를 참조하십시오.  
  
     [!code-csharp[S_UE_MSMQ_Poison#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ue_msmq_poison/cs/poisonbehaviorattribute.cs#3)]  
  
4. 서비스에 포이즌 동작 특성으로 주석이 달려 있어야 합니다.  

 또한 `ReceiveErrorHandling`이 `Fault`로 설정된 경우 `ServiceHost`에서 포이즌 메시지를 발생하는 데 오류가 발생합니다. 오류가 발생한 이벤트에 후크하고 서비스를 종료하며 수정 작업을 수행한 다음 다시 시작할 수 있습니다. 예를 들어 `LookupId`로 전파된 <xref:System.ServiceModel.MsmqPoisonMessageException>의 `IErrorHandler`를 기록해 둔 다음, 서비스 호스트에 오류가 발생하는 경우 `System.Messaging` API를 사용하면 `LookupId`를 사용하여 큐에서 메시지를 받고, 큐에서 메시지를 제거하고, 외부 저장소 또는 다른 큐에 메시지를 저장할 수 있습니다. 그런 다음 `ServiceHost`를 다시 시작하여 일반적인 처리를 다시 시작할 수 있습니다. [MSMQ 4.0의 포이즌 메시지 처리](../../../../docs/framework/wcf/samples/poison-message-handling-in-msmq-4-0.md) 에서는이 동작을 보여 줍니다.  
  
## <a name="transaction-time-out-and-poison-messages"></a>트랜잭션 제한 시간 및 포이즌 메시지  
 대기 중인 전송 채널과 사용자 코드 사이에 오류 클래스가 발생할 수 있습니다. 이러한 오류는 메시지 보안 계층이나 서비스 디스패치 논리와 같은 사이 계층에서 검색될 수 있습니다. 예를 들어 메시지가 응용 프로그램으로 디스패치되는 경우는 SOAP 보안 계층에서 검색되는 X.509 인증서가 없고 동작이 누락된 경우입니다. 이 경우 서비스 모델이 메시지를 삭제합니다. 메시지를 트랜잭션에서 읽고 해당 트랜잭션에 대한 결과를 제공할 수 없으므로 트랜잭션이 시간 초과되고 중단되며 메시지가 큐에 다시 배치됩니다. 즉, 특정 오류 클래스에서 트랜잭션이 바로 중단되지는 않지만 트랜잭션 제한 시간을 초과할 때가지 기다립니다. <xref:System.ServiceModel.ServiceBehaviorAttribute>를 사용하여 서비스에 대한 트랜잭션 제한 시간을 수정할 수 있습니다.  
  
 컴퓨터 전체에서 트랜잭션 제한 시간을 변경하려면 machine.config 파일을 수정하고 해당 트랜잭션 제한 시간을 설정합니다. 트랜잭션에 설정된 제한 시간에 따라 트랜잭션이 중단되어 결국 큐로 돌아가므로 해당 트랜잭션의 중단 횟수가 증가합니다. 결국 메시지는 포이즌이 되고 사용자 설정에 따라 적절히 처리됩니다.  
  
## <a name="sessions-and-poison-messages"></a>세션 및 포이즌 메시지  
 세션에서는 단일 메시지와 같은 재시도와 포이즌 메시지 처리 프로시저를 거칩니다. 포이즌 메시지에 대해 위에 나열된 속성은 전체 세션에 적용됩니다. 즉, 메시지가 거부되면 전체 세션이 다시 시도되고 최종 포이즌 메시지 큐나 발신자의 배달 못한 편지 큐로 이동합니다.  
  
## <a name="batching-and-poison-messages"></a>일괄 처리 및 포이즌 메시지  
 메시지가 포이즌 메시지가 되고 일괄 처리에 포함되면 전체 일괄 처리가 롤백되고 채널이 한 번에 하나의 메시지를 반환합니다. 일괄 처리에 대 한 자세한 내용은 [트랜잭션에서 메시지 일괄 처리](../../../../docs/framework/wcf/feature-details/batching-messages-in-a-transaction.md) 를 참조 하세요.  
  
## <a name="poison-message-handling-for-messages-in-a-poison-queue"></a>포이즌 큐의 메시지에 대한 포이즌 메시지 처리  
 메시지가 포이즌 메시지 큐에 놓이면 포이즌 메시지 처리가 종료되지 않습니다. 포이즌 메시지 큐의 메시지를 읽고 처리해야 합니다. 최종 포이즌 하위 큐에서 메시지를 읽을 때 포이즌 메시지 처리 설정의 하위 집합을 사용할 수 있습니다. `ReceiveRetryCount` 및 `ReceiveErrorHandling` 설정을 적용할 수 있습니다. `ReceiveErrorHandling`은 Drop, Reject 또는 Fault로 설정할 수 있습니다. `MaxRetryCycles`이 Move로 설정되면 `ReceiveErrorHandling`가 무시되고 예외가 throw됩니다.  
  
## <a name="windows-vista-windows-server-2003-and-windows-xp-differences"></a>Windows Vista, Windows Server 2003 및 Windows XP의 차이점  
 앞에서 설명한 대로 포이즌 메시지 처리 설정의 일부만 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에 적용됩니다. [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)], [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 및 [!INCLUDE[wv](../../../../includes/wv-md.md)]에서 메시지 큐의 주요 차이점은 포이즌 메시지 처리와 관련된 것입니다.  
  
- [!INCLUDE[wv](../../../../includes/wv-md.md)]의 메시지 큐는 하위 큐를 지원하지만 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]는 하위 큐를 지원하지 않습니다. 하위 큐는 포이즌 메시지 처리에 사용됩니다. 재시도 큐와 포이즌 큐는 포이즌 메시지 처리 설정에 따라 만들어지는 응용 프로그램 큐의 하위 큐입니다. `MaxRetryCycles`는 만들 재시도 하위 큐의 수를 지정합니다. 따라서 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 또는 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서 실행하는 경우 `MaxRetryCycles`는 무시되며 `ReceiveErrorHandling.Move`는 허용되지 않습니다.  
  
- [!INCLUDE[wv](../../../../includes/wv-md.md)]의 메시지 큐는 부정 승인을 지원하지만 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서는 지원하지 않습니다. 받는 큐 관리자에서 네거티브 승인을 사용하면 거부된 메시지가 보내는 큐 관리자의 배달 못한 편지 큐에 들어갑니다. 따라서 `ReceiveErrorHandling.Reject`는 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서 허용되지 않습니다.  
  
- [!INCLUDE[wv](../../../../includes/wv-md.md)]의 메시지 큐는 메시지 전달 시도 횟수를 보관하는 메시지 속성을 지원합니다. 이 중단 횟수 속성은 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서 사용할 수 없습니다. WCF는 메모리에서 중단 횟수를 유지 하므로 팜의 둘 이상의 WCF 서비스에서 같은 메시지를 읽을 경우이 속성에 정확한 값이 포함 되지 않을 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [큐 개요](../../../../docs/framework/wcf/feature-details/queues-overview.md)
- [Windows Vista, Windows Server 2003 및 Windows XP의 큐 기능 차이점](../../../../docs/framework/wcf/feature-details/diff-in-queue-in-vista-server-2003-windows-xp.md)
- [계약 및 서비스에서 오류 지정 및 처리](../../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)
