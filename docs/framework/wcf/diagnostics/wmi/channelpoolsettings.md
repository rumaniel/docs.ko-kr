---
title: ChannelPoolSettings
ms.date: 03/30/2017
ms.assetid: d3f475bd-f780-4bbe-b291-339387322964
ms.openlocfilehash: 8900af77d0d385bb68b4b85e1d15be57bb7a8d14
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61963980"
---
# <a name="channelpoolsettings"></a>ChannelPoolSettings
ChannelPoolSettings  
  
## <a name="syntax"></a>구문  
  
```csharp
class ChannelPoolSettings  
{  
  datetime IdleTimeout;  
  datetime LeaseTimeout;  
  sint32 MaxOutboundChannelsPerEndpoint;  
};  
```  
  
## <a name="methods"></a>메서드  
 ChannelPoolSettings 클래스는 메서드를 정의하지 않습니다.  
  
## <a name="properties"></a>속성  
 ChannelPoolSettings 클래스에는 다음과 같은 속성이 있습니다.  
  
### <a name="idletimeout"></a>IdleTimeout  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 연결이 끊어지기 전에 유휴 상태일 수 있는 최대 시간입니다.  
  
### <a name="leasetimeout"></a>LeaseTimeout  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 시간 제한을 초과하기 전에 대여 작업을 완료하기 위한 최대 시간입니다.  
  
### <a name="maxoutboundchannelsperendpoint"></a>MaxOutboundChannelsPerEndpoint  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 각 엔드포인트에 대한 최대 아웃바운드 채널 수입니다.  
  
## <a name="requirements"></a>요구 사항  
  
|MOF|Servicemodel.mof에 선언되어 있습니다.|  
|---------|-----------------------------------|  
|네임스페이스|root\ServiceModel에 정의되어 있습니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Channels.ChannelPoolSettings>
