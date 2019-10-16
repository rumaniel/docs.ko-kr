---
title: MsmqBindingElementBase
ms.date: 03/30/2017
ms.assetid: 210d41ab-a2a4-4d7a-afd2-0916c08a4015
ms.openlocfilehash: 1df4b32feda246a536183a42ac11b113bc4bb259
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61963438"
---
# <a name="msmqbindingelementbase"></a>MsmqBindingElementBase
MsmqBindingElementBase  
  
## <a name="syntax"></a>구문  
  
```csharp  
class MsmqBindingElementBase : TransportBindingElement  
{  
  string CustomDeadLetterQueue;  
  string DeadLetterQueue;  
  boolean Durable;  
  boolean ExactlyOnce;  
  sint32 MaxRetryCycles;  
  string ReceiveErrorHandling;  
  sint32 ReceiveRetryCount;  
  datetime RetryCycleDelay;  
  datetime TimeToLive;  
  boolean UseMsmqTracing;  
  boolean UseSourceJournal;  
};  
```  
  
## <a name="methods"></a>메서드  
 MsmqBindingElementBase 클래스는 메서드를 정의하지 않습니다.  
  
## <a name="properties"></a>속성  
 MsmqBindingElementBase 클래스에는 다음과 같은 속성이 있습니다.  
  
### <a name="customdeadletterqueue"></a>CustomDeadLetterQueue  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 애플리케이션별 배달 못 한 편지 큐의 위치를 포함하는 URI입니다. 이 큐에는 만료되었거나 전송 또는 전달하지 못한 메시지가 보관됩니다.  
  
### <a name="deadletterqueue"></a>DeadLetterQueue  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 사용할 배달 못 한 편지 큐의 형식을 나타내는 열거형 값입니다.  
  
### <a name="durable"></a>Durable  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 이 바인딩에서 처리하는 메시지가 지속적인지 또는 일시적인지를 나타내는 부울 값입니다.  
  
### <a name="exactlyonce"></a>ExactlyOnce  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 이 바인딩에서 처리하는 메시지가 단 한 번 수신되는지 여부를 지정하는 부울 값입니다.  
  
### <a name="maxretrycycles"></a>MaxRetryCycles  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 수신 애플리케이션으로 메시지 전달을 시도하는 최대 재시도 주기 수입니다.  
  
### <a name="receiveerrorhandling"></a>ReceiveErrorHandling  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 포이즌 메시지 처리에 대한 설정입니다.  
  
### <a name="receiveretrycount"></a>ReceiveRetryCount  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 애플리케이션 큐에서 읽은 메시지에 대해 즉시 재시도하는 최대 횟수입니다.  
  
### <a name="retrycycledelay"></a>RetryCycleDelay  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 전달하지 못한 메시지를 즉시 다시 전달하려고 시도할 때 재시도 주기 사이의 지연 시간을 지정하는 값입니다.  
  
### <a name="timetolive"></a>TimeToLive  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 이 바인딩에서 처리하는 메시지가 만료되기 전까지 큐에 머무를 수 있는 기간을 나타내는 시간 간격입니다.  
  
### <a name="usemsmqtracing"></a>UseMsmqTracing  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 이 바인딩에서 처리하는 메시지의 추적 여부를 지정하는 부울 값입니다.  
  
### <a name="usesourcejournal"></a>UseSourceJournal  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 이 바인딩에서 처리하는 메시지의 복사본을 소스 업무 일지 큐에 저장하는지 여부를 나타내는 부울 값입니다.  
  
## <a name="requirements"></a>요구 사항  
  
|MOF|Servicemodel.mof에 선언되어 있습니다.|  
|---------|-----------------------------------|  
|네임스페이스|root\ServiceModel에 정의되어 있습니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.NetMsmqBinding>
- <xref:System.ServiceModel.MsmqBindingBase>
