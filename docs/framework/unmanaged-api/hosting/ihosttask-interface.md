---
title: IHostTask 인터페이스
ms.date: 03/30/2017
api_name:
- IHostTask
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTask
helpviewer_keywords:
- IHostTask interface [.NET Framework hosting]
ms.assetid: a71dbbd5-64b8-47eb-9f03-8e8c85fbe2bc
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cb15da31d91565d49df83099045f742866eebcaa
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61992838"
---
# <a name="ihosttask-interface"></a>IHostTask 인터페이스
CLR (공용 언어 런타임) 작업을 관리 하는 호스트와 통신할 수 있도록 하는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[Alert 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttask-alert-method.md)|현재 작업의 시작을 호스트 하는 요청 `IHostTask` 인스턴스 작업을 중단할 수 있도록 합니다.|  
|[GetPriority 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttask-getpriority-method.md)|현재 태스크의 스레드 우선 순위 수준을 가져옵니다 `IHostTask` 인스턴스.|  
|[Join 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttask-join-method.md)|현재 작업까지 호출 작업을 차단 `IHostTask` 인스턴스가 완료 되 면 지정 된 시간 간격이 경과 하면 또는 [ihosttask:: Alert](../../../../docs/framework/unmanaged-api/hosting/ihosttask-alert-method.md) 라고 합니다.|  
|[SetCLRTask 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttask-setclrtask-method.md)|연결 프로그램 [ICLRTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md) 인스턴스를 현재 `IHostTask` 인스턴스.|  
|[SetPriority 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttask-setpriority-method.md)|현재 태스크에 대 한 호스트에서 스레드 우선 순위를 조정 하도록 요청 수준 `IHostTask` 인스턴스.|  
|[Start 메서드](../../../../docs/framework/unmanaged-api/hosting/ihosttask-start-method.md)|호스트 작업 요청 현재 `IHostTask` 코드를 실행할 수 있는 라이브 상태로 일시 중단 된에서 인스턴스.|  
  
## <a name="remarks"></a>설명  
 정의한 메서드를 호출 하는 CLR `IHostTask` 수준 등 작업을 시작 하려면 해당 스레드 우선 순위를 설정 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)
- [ICLRTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)
- [IHostTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
