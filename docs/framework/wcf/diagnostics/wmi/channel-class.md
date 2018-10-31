---
title: Channel 클래스
ms.date: 03/30/2017
ms.assetid: d9fae2ca-209c-4341-a0f5-6b79d1a67776
ms.openlocfilehash: 108d5f8e3cd092863dbd48e2bb9d180798b091a4
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50197875"
---
# <a name="channel-class"></a>Channel 클래스
채널  
  
## <a name="syntax"></a>구문  
  
```csharp
class Channel  
{  
  string LocalAddress;  
  Endpoint ref;  
  string RemoteAddress;  
  string SessionId;  
  string Type;  
};  
```  
  
## <a name="methods"></a>메서드  
 Channel 클래스는 메서드를 정의하지 않습니다.  
  
## <a name="properties"></a>속성  
 Channel 클래스에는 다음 속성이 있습니다.  
  
### <a name="localaddress"></a>LocalAddress  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 채널에 대한 로컬 끝점입니다.  
  
### <a name="ref"></a>ref  
 데이터 형식: Endpoint  
  
 액세스 형식: 읽기 전용  
  
 채널이 연결되는 엔드포인트에 대한 참조입니다.  
  
### <a name="remoteaddress"></a>RemoteAddress  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 채널과 연결된 원격 주소입니다.  
  
### <a name="sessionid"></a>SessionId  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 현재 세션 ID(있는 경우)입니다.  
  
### <a name="type"></a>형식  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 채널 형식입니다.  
  
## <a name="requirements"></a>요구 사항  
  
|MOF|Servicemodel.mof에 선언되어 있습니다.|  
|---------|-----------------------------------|  
|네임스페이스|root\ServiceModel에 정의되어 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.ServiceModel.Channels.ChannelBase>
