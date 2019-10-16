---
title: CoEEShutDownCOM 함수
ms.date: 03/30/2017
api_name:
- CoEEShutDownCOM
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CoEEShutDownCOM
helpviewer_keywords:
- CoEEShutDownCOM function [.NET Framework hosting]
ms.assetid: b634cae2-632f-4737-9be4-92d0652844d7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 164384f043a1722ace6e5c4098cb31c4327cba1e
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044067"
---
# <a name="coeeshutdowncom-function"></a>CoEEShutDownCOM 함수
CLR (공용 언어 런타임)에서 RCW (런타임 호출 가능 래퍼) 내에 포함 된 모든 인터페이스 포인터를 해제 하도록 합니다. 이는 모든 RCW 캐시를 해제 하는 효과가 있습니다. 이 전역 함수는 .NET Framework 4에서 더 이상 사용 되지 않습니다. 대신 특정 런타임에 대 한 진입점을 사용 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
void CoEEShutDownCOM ();  
```  
  
## <a name="remarks"></a>설명  
 함수 `CoEEShutDownCOM` 는 먼저 모든 컨텍스트와 모든 캐시에서 모든 rcw를 해제 한 다음 설치 프로그램에서 기존에 존재 하는 모든 중단 알림을 제거 합니다. DLL 언로드가 발생 하지 않습니다.  
  
> [!CAUTION]
> 이 함수는 프로세스에 로드 되는 모든 런타임에 영향을 줍니다.  
  
 .NET Framework 4부터 영향을 원하는 특정 런타임에이 함수에 대 한 진입점을 호출 합니다. 진입점을 가져오려면 [ICLRRuntimeInfo:: GetProcAddress](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-getprocaddress-method.md) 메서드를 호출 하 고 "CoEEShutDownCOM"를 지정 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 전역 정적 함수](../../../../docs/framework/unmanaged-api/metadata/metadata-global-static-functions.md)
