---
title: 단일 동시성 모델에서 메시지의 순서 지정 처리
ms.date: 03/30/2017
ms.assetid: a90f5662-a796-46cd-ae33-30a4072838af
ms.openlocfilehash: ecabb9a6e838b0137c538d76c554646356ea87f5
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991509"
---
# <a name="ordered-processing-of-messages-in-single-concurrency-mode"></a>단일 동시성 모델에서 메시지의 순서 지정 처리
WCF는 기본 채널이 세션 않는 한 메시지가 처리 되는 순서를 보장 하지 않습니다.  예를 들어 세션 채널이 아닌 MsmqInputChannel를 사용 하는 WCF 서비스는 메시지를 순서 대로 처리 하지 못합니다. 개발자가 주문 처리 동작에서 세션을 사용 하지 않으려는 경우가 있습니다. 이 항목에서는 서비스가 단일 동시성 모델에서 실행되고 있을 때 이 동작을 구성하는 방법을 설명합니다.  
  
## <a name="in-order-message-processing"></a>순서에 따른 메시지 처리  
 <xref:System.ServiceModel.ServiceBehaviorAttribute.EnsureOrderedDispatch%2A>라는 새 속성이 <xref:System.ServiceModel.ServiceBehaviorAttribute>에 추가되었습니다. <xref:System.ServiceModel.ServiceBehaviorAttribute.EnsureOrderedDispatch%2A>가 true로 설정되고 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A>가 <xref:System.ServiceModel.ConcurrencyMode.Single>로 설정되면 서비스에 전송된 메시지는 순서대로 처리됩니다. 다음 코드 조각에서는 이러한 특성을 설정하는 방법을 보여 줍니다.  
  
```csharp
[ServiceBehavior(ConcurrencyMode = ConcurrencyMode.Single, EnsureOrderedDispatch = true )]  
    class Service : IService  
    {  
         // ...  
    }  
```  
  
 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A>가 다른 값으로 설정되면 <xref:System.InvalidOperationException>이 throw됩니다.  
  
## <a name="see-also"></a>참고자료

- [세션, 인스턴스 및 동시성](../../../../docs/framework/wcf/feature-details/sessions-instancing-and-concurrency.md)
- [동시성](../../../../docs/framework/wcf/samples/concurrency.md)
