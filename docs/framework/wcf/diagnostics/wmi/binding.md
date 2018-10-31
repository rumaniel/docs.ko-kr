---
title: Binding2
ms.date: 03/30/2017
ms.assetid: 09511c6c-5749-4bb0-874e-0f0be36bfe04
ms.openlocfilehash: 84e304f3dedcbd785d6238e6cb5eb142c288b995
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50198891"
---
# <a name="binding"></a>바인딩
wmi 바인딩  
  
## <a name="syntax"></a>구문  
  
```csharp
class Binding  
{  
  BindingElement BindingElements[];  
  datetime CloseTimeout;  
  string Name;  
  string Namespace;  
  datetime OpenTimeout;  
  datetime ReceiveTimeout;  
  string Scheme;  
  datetime SendTimeout;  
};  
```  
  
## <a name="methods"></a>메서드  
 바인딩 클래스는 메서드를 정의하지 않습니다.  
  
## <a name="properties"></a>속성  
 Binding 클래스에는 다음과 같은 속성이 있습니다.  
  
### <a name="bindingelements"></a>BindingElements  
 데이터 형식: BindingElement array  
  
 액세스 형식: 읽기 전용  
  
 바인딩이 구현한 바인딩 요소의 컬렉션입니다.  
  
### <a name="closetimeout"></a>CloseTimeout  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 닫기 작업을 완료하기 위해 제공된 시간 간격입니다.  
  
### <a name="name"></a>이름  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 바인딩 이름입니다.  
  
### <a name="namespace"></a>네임스페이스  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 바인딩의 XML 네임스페이스입니다.  
  
### <a name="opentimeout"></a>OpenTimeout  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 열기 작업을 완료하기 위해 제공된 시간 간격입니다.  
  
### <a name="receivetimeout"></a>ReceiveTimeout  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 받기 작업을 완료하기 위해 제공된 시간 간격입니다.  
  
### <a name="scheme"></a>Scheme  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 바인딩이 빌드한 채널 및 수신기 팩터리에서 사용하는 URI 전송 체계입니다.  
  
### <a name="sendtimeout"></a>SendTimeout  
 데이터 형식: datetime  
  
 액세스 형식: 읽기 전용  
  
 보내기 작업을 완료하기 위해 제공된 시간 간격입니다.  
  
## <a name="requirements"></a>요구 사항  
  
|MOF|Servicemodel.mof에 선언되어 있습니다.|  
|---------|-----------------------------------|  
|네임스페이스|root\ServiceModel에 정의되어 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.ServiceModel.Channels.Binding>
