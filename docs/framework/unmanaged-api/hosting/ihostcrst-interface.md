---
title: IHostCrst 인터페이스
ms.date: 03/30/2017
api_name:
- IHostCrst
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostCrst
helpviewer_keywords:
- IHostCrst interface [.NET Framework hosting]
ms.assetid: ac298ebd-0815-47e4-a823-30b31baab903
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 939f100e8ee386642a29c33827a8339caf0467b9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61967832"
---
# <a name="ihostcrst-interface"></a>IHostCrst 인터페이스
스레딩에 대 한 중요 한 섹션의 호스트의 표현으로 사용 됩니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[Enter 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostcrst-enter-method.md)|중요 섹션에 진입 합니다.|  
|[Leave 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostcrst-leave-method.md)|임계 영역을 유지합니다.|  
|[SetSpinCount 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostcrst-setspincount-method.md)|중요 섹션의 스핀 수를 설정합니다.|  
|[TryEnter 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostcrst-tryenter-method.md)|중요 섹션 및 보고서 성공 또는 실패를 즉시 입력 하려고 합니다.|  
  
## <a name="remarks"></a>설명  
 `IHostCrst` 와 같은 Win32 함수를 사용 하는 대신는 CLR (공용 언어 런타임) 임계 영역을 호스트의 표시와 직접 통신 하도록 허용 `EnterCriticalSection` 또는 `LeaveCriticalSection`합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRSyncManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrsyncmanager-interface.md)
- [IHostSyncManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
