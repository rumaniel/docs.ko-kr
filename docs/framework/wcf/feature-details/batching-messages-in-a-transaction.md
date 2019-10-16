---
title: 트랜잭션에서 메시지 일괄 처리
ms.date: 03/30/2017
helpviewer_keywords:
- batching messages [WCF]
ms.assetid: 53305392-e82e-4e89-aedc-3efb6ebcd28c
ms.openlocfilehash: a517dc4e143b561a17bb3715b69be393bee2b21e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64585022"
---
# <a name="batching-messages-in-a-transaction"></a>트랜잭션에서 메시지 일괄 처리
대기 중인 애플리케이션은 트랜잭션을 사용하여 정확하고 안정적인 메시지 배달을 수행합니다. 트랜잭션은 비용이 많이 드는 작업이나 메시지 처리량을 상당히 줄일 수 있습니다. 메시지 처리량을 향상시키기 위한 한가지 방법은 애플리케이션이 단일 트랜잭션 내에서 여러 메시지를 읽고 처리하는 것입니다. 성능이 좋아질수록 복구 작업도 늘어납니다. 즉, 일괄 처리하는 메시지 수가 증가하면 트랜잭션이 롤백 되는 경우 필요한 복구 작업의 크기도 증가합니다. 트랜잭션 및 세션에서 일괄 처리하는 메시지 사이에는 차이가 있습니다. A *세션* 단일 응용 프로그램에서 처리 되 고 하나의 단위로 커밋된는 관련된 메시지의 그룹화입니다. 세션은 일반적으로 관련 메시지 그룹을 함께 처리해야 하는 경우 사용됩니다. 이러한 예로 온라인 쇼핑 웹 사이트를 들 수 있습니다. *일괄 처리* 관련 없는 메시지 처리량을 증가 시키는 방식으로 메시지를 여러 처리 하는 데 사용 합니다. 세션에 대 한 자세한 내용은 참조 하십시오 [세션에서 대기 중인 메시지 그룹화](../../../../docs/framework/wcf/feature-details/grouping-queued-messages-in-a-session.md)합니다. 또한 일괄 처리하는 메시지는 하나의 애플리케이션에 의해 처리되고 하나의 단위로 커밋되지만 일괄 처리하는 메시지 간에 관계가 없을 수 있습니다. 한 트랜잭션의 메시지를 일괄 처리하는 것이 애플리케이션이 실행되는 방법을 변경하지 않는 가장 적절한 방법입니다.  
  
## <a name="entering-batching-mode"></a>일괄 처리 모드 시작  
 <xref:System.ServiceModel.Description.TransactedBatchingBehavior> 끝점 동작은 일괄 처리를 제어합니다. 서비스 끝점에이 끝점 동작이 추가 Windows Communication Foundation (WCF) 트랜잭션에서 메시지 일괄 처리에 알려 줍니다. 트랜잭션이 필요한 메시지만 일괄 처리에 배치 된 모든 메시지의 경우 트랜잭션이 필요 하 고 작업에서 보낸 메시지만 표시 `TransactionScopeRequired`  =  `true` 하 고 `TransactionAutoComplete`  =  `true` 됩니다 일괄 처리에 대 한 것으로 간주 합니다. 서비스 계약의 모든 작업으로 표시 됩니다 `TransactionScopeRequired`  =  `false` 하 고 `TransactionAutoComplete`  =  `false`, 다음 일괄 처리 모드 시작 되지 않습니다.  
  
## <a name="committing-a-transaction"></a>트랜잭션 커밋  
 일괄 처리된 트랜잭션은 다음을 기준으로 커밋됩니다.  
  
- `MaxBatchSize`. <xref:System.ServiceModel.Description.TransactedBatchingBehavior> 동작의 속성입니다. 이 속성은 일괄 처리로 배치되는 최대 메시지 수를 결정합니다. 이 값에 도달하면 일괄 처리가 커밋됩니다. 값은 엄격하게 제한하지 않으며 이 값의 메시지를 받기 전에 일괄 처리를 커밋할 수 있습니다.  
  
- `Transaction Timeout`. 트랜잭션 시간 제한의 80%가 경과한 후, 일괄 처리가 커밋되고 새 일괄 처리가 만들어 집니다. 이는 완료할 트랜잭션의 지정된 시간이 20% 이하로 남은 경우, 일괄 처리가 커밋된다는 의미입니다.  
  
- `TransactionScopeRequired`. WCF에는 발견 한 경우 메시지의 일괄 처리를 처리 하는 동안 `TransactionScopeRequired`  =  `false`, 일괄 처리를 커밋하고 새 일괄 처리를 사용 하 여 첫 번째 메시지를 받을 때 다시 열립니다 `TransactionScopeRequired`  =  `true` 고 `TransactionAutoComplete`  = `true`.  
  
- 메시지가 더 이상 큐에 없는 경우 `MaxBatchSize`에 도달하지 않았거나 트랜잭션 시간 제한의 80%가 경과하지 않았더라도 현재 일괄 처리가 커밋됩니다.  
  
## <a name="leaving-batching-mode"></a>일괄 처리 모드 종료  
 일괄 처리 메시지로 인해 트랜잭션이 중단되는 경우 다음 단계가 수행됩니다.  
  
1. 전체 일괄 처리 메시지가 롤백됩니다.  
  
2. 읽는 메시지 수가 최대 일괄 처리 크기의 두 배를 초과할 때까지 메시지를 한 번에 하나씩 읽습니다.  
  
3. 일괄 처리 모드가 다시 시작됩니다.  
  
## <a name="choosing-the-batch-size"></a>일괄 처리 크기 선택  
 일괄 처리 크기는 애플리케이션에 따라 달라집니다. 애플리케이션의 최적 일괄 처리 크기를 결정하는 데 가장 적절한 방법은 직접 경험하는 것입니다. 일괄 처리 크기 선택 시 애플리케이션의 실제 배포 모델에 따라 크기를 선택해야 합니다. 예를 들어, 애플리케이션을 배포할 때 원격 시스템에서 SQL Server가 필요하고 큐 및 SQL Server가 포함된 트랜잭션이 필요한 경우 이 구성을 실제로 실행하여 일괄 처리 크기를 결정하는 것이 가장 바람직합니다.  
  
## <a name="concurrency-and-batching"></a>동시성 및 일괄 처리  
 처리량을 증가시키기 위해 여러 일괄 처리를 동시에 실행할 수도 있습니다. `ConcurrencyMode.Multiple`에서 `ServiceBehaviorAttribute`을 설정하여 동시 일괄 처리를 수행할 수 있습니다.  
  
 *서비스 스로틀* 서비스에서 얼마나 많은 최대 동시 호출 수를 나타내는 데 사용 되는 서비스 동작입니다. 일괄 처리에서 사용하는 경우 이 동작은 동시에 실행할 수 있는 일괄 처리 수로 해석됩니다. 서비스 스로틀을 설정 하지 않으면 WCF는 최대 동시 호출을 16 기본값은입니다. 따라서 기본적으로 일괄 처리 동작이 추가된 경우, 동시에 최대 16개의 일괄 처리를 수행할 수 있습니다. 사용자 성능을 기준으로 서비스 스로틀 및 일괄 처리를 조정하는 것이 가장 바람직합니다. 예를 들어, 큐에 100개의 메시지가 있고 20개를 일괄 처리하려는 경우 처리량에 따라 일괄 처리를 조정하지 않은 것처럼 16개의 트랜잭션을 수행할 수 있기 때문에, 최대 동시 호출을 16으로 설정하는 것이 유용하지 않을 수 있습니다. 따라서 성능을 세부적으로 조정하는 경우 동시 일괄 처리를 설정하지 않거나 올바른 서비스 스로틀 크기로 동시 일괄 처리를 설정합니다.  
  
## <a name="batching-and-multiple-endpoints"></a>일괄 처리 및 여러 엔드포인트  
 엔드포인트는 주소 및 계약으로 구성됩니다. 동일한 바인딩을 공유하는 여러 엔드포인트가 있을 수 있습니다. 두 개의 엔드포인트가 동일한 바인딩을 공유하고 URI(Uniform Resource Identifier) 또는 큐 주소를 수신 대기할 수 있습니다. 두 개의 엔드포인트를 동일한 큐에서 읽는 경우, 트랜잭션된 일괄 처리 동작이 양쪽 엔드포인트에 추가되고 지정된 일괄 처리 크기 간에 충돌될 수 있습니다. 이러한 동작은 두 개의 트랜잭션된 일괄 처리 동작 간에 지정된 최소 일괄 처리 크기로 일괄 처리를 구현하여 확인합니다. 이 시나리오에서 엔드포인트 중 하나가 트랜잭션된 일괄 처리를 지정하지 않은 경우, 양쪽 엔드포인트 모두 일괄 처리를 사용하지 않습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 구성 파일에서 `TransactedBatchingBehavior`를 지정하는 방법을 보여 줍니다.  
  
```xml  
<behaviors>
  <endpointBehaviors>
    <behavior name="TransactedBatchingBehavior"
              maxBatchSize="100" />
  </endpointBehaviors>
</behaviors>
```  
  
 다음 예제에서는 코드에서 <xref:System.ServiceModel.Description.TransactedBatchingBehavior>를 지정하는 방법을 보여 줍니다.  
  
```csharp
using (ServiceHost serviceHost = new ServiceHost(typeof(OrderProcessorService)))
{
     ServiceEndpoint sep = ServiceHost.AddServiceEndpoint(typeof(IOrderProcessor), new NetMsmqBinding(), "net.msmq://localhost/private/ServiceModelSamplesTransacted");
     sep.Behaviors.Add(new TransactedBatchingBehavior(100));
     
     // Open the ServiceHost to create listeners and start listening for messages.
    serviceHost.Open();
  
    // The service can now be accessed.
    Console.WriteLine("The service is ready.");
    Console.WriteLine("Press <ENTER> to terminate service.");
    Console.WriteLine();
    Console.ReadLine();
  
    // Close the ServiceHostB to shut down the service.
    serviceHost.Close();
}  
```  
  
## <a name="see-also"></a>참고자료

- [큐 개요](../../../../docs/framework/wcf/feature-details/queues-overview.md)
- [WCF의 큐](../../../../docs/framework/wcf/feature-details/queuing-in-wcf.md)
