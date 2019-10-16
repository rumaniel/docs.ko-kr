---
title: IHostSyncManager 인터페이스
ms.date: 03/30/2017
api_name:
- IHostSyncManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSyncManager
helpviewer_keywords:
- IHostSyncManager interface [.NET Framework hosting]
ms.assetid: 2e081a37-6a28-4c93-b7ab-1c96a464637c
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 200da8b87b52a29c2b075d1e06929031d3f588b7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61769631"
---
# <a name="ihostsyncmanager-interface"></a>IHostSyncManager 인터페이스
CLR (공용 언어 런타임)에서 Win32 동기화 함수를 사용 하는 대신 호스트를 호출 하 여 동기화 기본 형식을 만들 수 있도록 하는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[CreateAutoEvent 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-createautoevent-method.md)|자동 재설정 이벤트 개체를 만듭니다.|  
|[CreateCrst 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-createcrst-method.md)|동기화에 대 한 임계 영역 개체를 만듭니다.|  
|[CreateCrstWithSpinCount 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-createcrstwithspincount-method.md)|동기화에 대 한 스핀 수를 사용 하 여 임계 영역 개체를 만듭니다.|  
|[CreateManualEvent 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-createmanualevent-method.md)|수동 재설정 이벤트 개체를 만듭니다.|  
|[CreateMonitorEvent 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-createmonitorevent-method.md)|자동 재설정 이벤트를 모니터링 대상된 개체를 만듭니다.|  
|[CreateRWLockReaderEvent 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-createrwlockreaderevent-method.md)|판독기 잠금 구현 하기 위한 수동 재설정 이벤트 개체를 만듭니다.|  
|[CreateRWLockWriterEvent 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-createrwlockwriterevent-method.md)|기록기 잠금 구현에 대 한 자동 재설정 이벤트 개체를 만듭니다.|  
|[CreateSemaphore 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-createsemaphore-method.md)|만듭니다는 [IHostSemaphore](../../../../docs/framework/unmanaged-api/hosting/ihostsemaphore-interface.md) 대기 이벤트에 대 한 세마포를 사용 하 여 CLR에 대 한 개체입니다.|  
|[SetCLRSyncManager 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-setclrsyncmanager-method.md)|집합의 [ICLRSyncManager](../../../../docs/framework/unmanaged-api/hosting/iclrsyncmanager-interface.md) 현재 연결할 인스턴스 `IHostSyncManager` 인스턴스.|  
  
## <a name="remarks"></a>설명  
 CLR은 호스트의 구현을 검색 `IHostSyncManager` 를 호출 하 여 합니다 [ihostcontrol:: Gethostmanager](../../../../docs/framework/unmanaged-api/hosting/ihostcontrol-gethostmanager-method.md) 메서드는 `IID` IID_IHostSyncManager의 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRSyncManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrsyncmanager-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
