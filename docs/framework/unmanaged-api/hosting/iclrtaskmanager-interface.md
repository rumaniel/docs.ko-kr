---
title: ICLRTaskManager 인터페이스
ms.date: 03/30/2017
api_name:
- ICLRTaskManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTaskManager
helpviewer_keywords:
- ICLRTaskManager interface [.NET Framework hosting]
ms.assetid: 2bd55e0c-001b-41fd-b29d-f01670fe8216
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 19ef7cb78791496de76e5741f8254ee88563c776
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61763375"
---
# <a name="iclrtaskmanager-interface"></a>ICLRTaskManager 인터페이스
메서드는 CLR (공용 언어 런타임) 호스트 하는 명시적으로 요청을 허용 하는 새 작업 만들기, 현재 실행 중인 작업을 가져오고 설정 언어와 작업에 대 한 문화권을 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[CreateTask 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-createtask-method.md)|CLR에서 만든 새 명시적으로 요청 [ICLRTask](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md) 인스턴스.|  
|[GetCurrentTask 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-getcurrenttask-method.md)|가져옵니다는 `ICLRTask` 현재 실행 중인 태스크를 나타내는 인스턴스입니다.|  
|[GetCurrentTaskType 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-getcurrenttasktype-method.md)|현재 실행 중인 작업의 형식을 가져옵니다.|  
|[SetLocale 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-setlocale-method.md)|호스트에서 현재 실행 중인 작업에 대 한 로캘 식별자가 수정 하는 CLR에 알립니다.|  
|[SetUILocale 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-setuilocale-method.md)|호스트에서 현재 실행 중인 작업에서 사용자 인터페이스 로캘 식별자를 수정에 공용 언어 런타임을 알립니다.|  
  
## <a name="remarks"></a>설명  
 호스트 된 환경에서 실행 중인 각 태스크 호스트 쪽에 대 한 두 표현 (인스턴스의 [IHostTask](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)) 및 clr (인스턴스의 [ICLRTask](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)). 호스트 또는 CLR 작업의 만들기를 시작할 수 있지만 호스트 측 표현을 호스트와 작업에 대 한 CLR 간의 성공적인 통신을 위해 해당 CLR 쪽 표현으로 연결 되어야 합니다. 두 개체가 생성 되어 인스턴스화하기 전에 운영 체제 스레드에서 관리 코드를 실행 해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)
- [IHostTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)
- [IHostTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
