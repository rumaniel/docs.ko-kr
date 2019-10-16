---
title: ServiceModel 트랜잭션 구성
ms.date: 03/30/2017
helpviewer_keywords:
- transactions [WCF], ServiceModel configuration
ms.assetid: 5636067a-7fbd-4485-aaa2-8141c502acf3
ms.openlocfilehash: d5bb81c618e3b27df32763948dbe56c9b37995e6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61747708"
---
# <a name="servicemodel-transaction-configuration"></a>ServiceModel 트랜잭션 구성
Windows Communication Foundation (WCF) 서비스의 트랜잭션을 구성 하기 위한 세 가지 특성을 제공 합니다. `transactionFlow`, `transactionProtocol`, 및 `transactionTimeout`합니다.  
  
## <a name="configuring-transactionflow"></a>transactionFlow 구성  
 WCF 제공 포함 미리 정의 된 바인딩 중 대부분은 `transactionFlow` 및 `transactionProtocol` 특성을 특정 트랜잭션 흐름 프로토콜을 사용 하 여 특정 끝점에 대해 들어오는 트랜잭션을 허용 하도록 바인딩을 구성할 수 있도록 합니다. 또한 `transactionFlow` 요소와 해당 `transactionProtocol` 특성을 사용하여 고유의 사용자 지정 바인딩을 만들 수 있습니다. 구성 요소를 설정 하는 방법에 대 한 자세한 내용은 참조 하세요. [ \<바인딩 >](../../../../docs/framework/misc/binding.md) 하 고 [WCF 구성 스키마](../../../../docs/framework/configure-apps/file-schema/wcf/index.md)합니다.  
  
 `transactionFlow` 특성은 바인딩을 사용하는 서비스 엔드포인트에 대해 트랜잭션 흐름을 사용할지 여부를 지정합니다.  
  
## <a name="configuring-transactionprotocol"></a>transactionProtocol 구성  
 `transactionProtocol` 특성은 바인딩을 사용하는 서비스 엔드포인트에서 사용할 트랜잭션 프로토콜을 지정합니다.  
  
 다음은 지정된 바인딩에서 WS-AtomicTransaction 프로토콜을 사용하고 트랜잭션 흐름을 지원하도록 구성하는 구성 섹션의 예입니다.  
  
```xml  
<netNamedPipeBinding>  
   <binding name="test"  
      closeTimeout="00:00:10"  
      openTimeout="00:00:20"   
      receiveTimeout="00:00:30"  
      sendTimeout="00:00:40"  
      transactionFlow="true"  
      transactionProtocol="WSAtomicTransactionOctober2004"  
      hostNameComparisonMode="WeakWildcard"  
      maxBufferSize="1001"  
      maxConnections="123"   
      maxReceivedMessageSize="1000">  
   </binding>  
</netNamedPipeBinding>  
```  
  
## <a name="configuring-transactiontimeout"></a>transactionTimeout 구성  
 구성할 수 있습니다는 `transactionTimeout` WCF 서비스에 대 한 특성을 `behavior` 구성 파일의 요소입니다. 다음 코드에서는 이 작업을 수행하는 방법에 대해 설명합니다.  
  
```xml  
<configuration>  
   <system.serviceModel>  
      <behaviors>  
         <behavior name="NewBehavior" transactionTimeout="00:01:00" /> <!-- 1 minute timeout -->  
      </behaviors>  
   </system.serviceModel>  
</configuration>  
```  
  
 `transactionTimeout` 특성은 서비스에서 만들어진 새 트랜잭션이 완료되어야 하는 기간을 지정합니다. 새 트랜잭션을 설정하는 작업에 대한 <xref:System.Transactions.TransactionScope> 시간 제한으로 사용됩니다. <xref:System.ServiceModel.OperationBehaviorAttribute>가 적용되면 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> 속성이 `true`로 설정됩니다.  
  
 시간 제한은 트랜잭션을 만든 시점으로부터 2단계 커밋 프로토콜의 1단계를 완료할 때까지의 기간을 지정합니다.  
  
 `service` 구성 섹션에 이 특성이 설정되어 있으면 <xref:System.ServiceModel.OperationBehaviorAttribute>를 사용하여 해당 서비스에 대한 하나 이상의 메서드를 적용해야 합니다. 여기서 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> 속성은 `true`로 설정됩니다.  
  
 이 `transactionTimeout` 구성 설정과 <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A> 속성 사이에서 더 작은 값이 시간 제한 값으로 사용됩니다.  
  
## <a name="see-also"></a>참고자료

- [\<binding>](../../../../docs/framework/misc/binding.md)
- [WCF 구성 스키마](../../../../docs/framework/configure-apps/file-schema/wcf/index.md)
