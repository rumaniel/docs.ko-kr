---
title: ReliableSessionBindingElement
ms.date: 03/30/2017
ms.assetid: effda125-b8d3-4de6-8c0e-f59f5ea8f6eb
ms.openlocfilehash: 2e2e36486c3788cd714ffd0ed545fbb14f831476
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50197043"
---
# <a name="reliablesessionbindingelement"></a>ReliableSessionBindingElement
ReliableSessionBindingElement  
  
## <a name="syntax"></a>구문  
  
```csharp
class ReliableSessionBindingElement : BindingElement  
{  
  datetime AcknowledgementInterval;  
  boolean FlowControlEnabled;  
  datetime InactivityTimeout;  
  sint32 MaxPendingChannels;  
  sint32 MaxRetryCount;  
  sint32 MaxTransferWindowSize;  
  boolean Ordered;  
  integer ReliableMessagingVersion;  
};  
```  
  
## <a name="methods"></a>메서드  
 ReliableSessionBindingElement 클래스는 메서드를 정의하지 않습니다.  
  
## <a name="properties"></a>속성  
 ReliableSessionBindingElement 클래스에는 다음과 같은 속성이 있습니다.  
  
### <a name="acknowledgementinterval"></a>AcknowledgementInterval  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 팩터리에서 만든 신뢰할 수 있는 채널의 메시지 소스에 승인을 보내기 전에 대상이 대기하는 시간입니다.  
  
### <a name="flowcontrolenabled"></a>FlowControlEnabled  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 흐름 제어 활성화 여부를 지정하는 부울 값입니다.  
  
### <a name="inactivitytimeout"></a>InactivityTimeout  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 통신 상대방이 메시지를 보내지 않아도 채널에서 오류로 간주하지 않도록 허용하는 최대 기간을 지정합니다.  
  
### <a name="maxpendingchannels"></a>MaxPendingChannels  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 수신기에서 수락하기까지 대기할 수 있는 최대 채널 수입니다.  
  
### <a name="maxretrycount"></a>MaxRetryCount  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 신뢰할 수 있는 채널이 기본 채널에서 `Send`를 호출하여 아직 승인을 받지 않은 메시지를 다시 전송하기 위해 시도할 수 있는 최대 횟수입니다.  
  
### <a name="maxtransferwindowsize"></a>MaxTransferWindowSize  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 신뢰할 수 있는 세션에 대한 최대 전송 창 크기입니다.  
  
### <a name="ordered"></a>Ordered  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 메시지가 전송된 순서대로 도착하도록 보장하는지 여부를 지정하는 부울 값입니다.  
  
### <a name="reliablemessagingversion"></a>ReliableMessagingVersion  
 데이터 형식: integer  
  
 액세스 형식: 읽기 전용  
  
 신뢰할 수 있는 세션에 사용된 WS-ReliableMessaging 프로토콜을 지정하는 정수입니다.  
  
## <a name="requirements"></a>요구 사항  
  
|MOF|Servicemodel.mof에 선언되어 있습니다.|  
|---------|-----------------------------------|  
|네임스페이스|root\ServiceModel에 정의되어 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement>
