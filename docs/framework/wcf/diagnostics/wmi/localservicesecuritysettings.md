---
title: LocalServiceSecuritySettings
ms.date: 03/30/2017
ms.assetid: 490aa0e5-5242-4f8d-b505-5ec6287633b4
ms.openlocfilehash: 15304630eb8a14e01d4815ddddc84cd32796fdcf
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61963451"
---
# <a name="localservicesecuritysettings"></a>LocalServiceSecuritySettings
LocalServiceSecuritySettings  
  
## <a name="syntax"></a>구문  
  
```csharp
class LocalServiceSecuritySettings  
{  
  boolean DetectReplays;  
  datetime InactivityTimeout;  
  datetime IssuedCookieLifetime;  
  sint32 MaxCachedCookies;  
  datetime MaxClockSkew;  
  sint32 MaxPendingSessions;  
  sint32 MaxStatefulNegotiations;  
  datetime NegotiationTimeout;  
  boolean ReconnectTransportOnFailure;  
  sint32 ReplayCacheSize;  
  datetime ReplayWindow;  
  datetime SessionKeyRenewalInterval;  
  datetime SessionKeyRolloverInterval;  
  datetime TimestampValidityDuration;  
};  
```  
  
## <a name="methods"></a>메서드  
 LocalServiceSecuritySettings 클래스는 메서드를 정의하지 않습니다.  
  
## <a name="properties"></a>속성  
 LocalServiceSecuritySettings 클래스에는 다음과 같은 속성이 있습니다.  
  
### <a name="detectreplays"></a>DetectReplays  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 채널에 대한 재생 공격이 검색되어 자동으로 처리되는지 여부를 지정하는 부울 값입니다.  
  
### <a name="inactivitytimeout"></a>InactivityTimeout  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 서비스가 지원하는 보류 중인 보안 세션의 최대 수입니다.  
  
### <a name="issuedcookielifetime"></a>IssuedCookieLifetime  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 모든 새 보안 쿠키에 발급된 수명을 지정하는 TimeSpan입니다.  
  
### <a name="maxcachedcookies"></a>MaxCachedCookies  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 캐시될 수 있는 최대 쿠키 수입니다.  
  
### <a name="maxclockskew"></a>MaxClockSkew  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 통신하는 두 상대방의 시스템 시계 사이의 최대 시간 차이를 지정하는 TimeSpan입니다.  
  
### <a name="maxpendingsessions"></a>MaxPendingSessions  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 서비스에서 보류 중인 최대 연결 수입니다.  
  
### <a name="maxstatefulnegotiations"></a>MaxStatefulNegotiations  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 동시에 활성화될 수 있는 보안 협상의 수입니다.  
  
### <a name="negotiationtimeout"></a>NegotiationTimeout  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 서버와 클라이언트 간 보안 협상 단계에 대한 최대 기간을 지정하는 TimeSpan입니다.  
  
### <a name="reconnecttransportonfailure"></a>ReconnectTransportOnFailure  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 WS-Reliable Messaging을 사용하는 연결에서 전송 실패 후 다시 연결을 시도할지 여부를 지정하는 부울 값입니다.  
  
### <a name="replaycachesize"></a>ReplayCacheSize  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 재생 검색에 사용되는 캐시된 nonces 수입니다.  
  
### <a name="replaywindow"></a>ReplayWindow  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 개별 메시지 nonce를 사용할 수 있는 기간을 지정하는 TimeSpan입니다.  
  
### <a name="sessionkeyrenewalinterval"></a>SessionKeyRenewalInterval  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 해당 기간이 지나면 개시자가 보안 세션에 대한 키를 갱신할 수 있는 기간을 지정하는 TimeSpan입니다.  
  
### <a name="sessionkeyrolloverinterval"></a>SessionKeyRolloverInterval  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 키 갱신 중에 들어오는 메시지에서 이전 세션 키를 사용할 수 있는 시간 간격을 지정하는 TimeSpan입니다.  
  
### <a name="timestampvalidityduration"></a>TimestampValidityDuration  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 타임스탬프를 사용할 수 있는 기간을 지정하는 TimeSpan입니다.  
  
## <a name="requirements"></a>요구 사항  
  
|MOF|Servicemodel.mof에 선언되어 있습니다.|  
|---------|-----------------------------------|  
|네임스페이스|root\ServiceModel에 정의되어 있습니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>
