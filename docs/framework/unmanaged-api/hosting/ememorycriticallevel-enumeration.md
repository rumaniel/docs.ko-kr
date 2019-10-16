---
title: EMemoryCriticalLevel 열거형
ms.date: 03/30/2017
api_name:
- EMemoryCriticalLevel
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EMemoryCriticalLevel
helpviewer_keywords:
- EMemoryCriticalLevel enumeration [.NET Framework hosting]
ms.assetid: 2ca8a7a2-7b54-4ba3-8e73-277c7df485f3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 26b3761ab49f36c5f687ff2c62882667e044d299
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67774223"
---
# <a name="ememorycriticallevel-enumeration"></a>EMemoryCriticalLevel 열거형
특정 메모리 할당이 요청 되었으나 처리할 수 없는 경우 오류의 영향을 나타내는 값을 포함 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum {  
    eTaskCritical      = 0,  
    eAppDomainCritical = 1,  
    eProcessCritical   = 2  
} EMemoryCriticalLevel;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|설명|  
|------------|-----------------|  
|`eAppDomainCritical`|할당이 할당 요청한 도메인에서 관리 되는 코드를 실행 하는 것에 대 한 중요 한 임을 나타냅니다. 메모리를 할당할 수 없는 경우 CLR 도메인에 여전히 사용할 수 있는지를 보장할 수 없습니다. 호스트에 할당할 수 없는 경우 수행할 작업을 결정 합니다. 중단을 CLR에 지시할 수 있습니다 합니다 `AppDomain` 자동으로 계속에서 메서드를 호출 하 여 실행 되도록 허용 하거나 [ICLRPolicyManager](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-interface.md)합니다.|  
|`eProcessCritical`|할당 프로세스에서 관리 되는 코드의 실행에 중요 한 임을 나타냅니다. 이 값은 종료자를 실행 하는 경우 시작 하는 동안 및 사용 됩니다. 메모리를 할당할 수 없으면 CLR 프로세스에서 사용할 수 없습니다. 할당이 실패 하면 CLR은 효과적으로 사용할 수 없습니다. CLR에 대 한 모든 후속 호출 HOST_E_CLRNOTAVAILABLE를 사용 하 여 실패합니다.|  
|`eTaskCritical`|할당이 할당 요청한 작업을 실행 하는 중요 한 임을 나타냅니다. 메모리를 할당할 수 없으면 CLR 태스크가 실행 될 수 있도록 보장할 수 없습니다. CLR 장애가 발생 한 <xref:System.Threading.ThreadAbortException> 물리적 연산 시스템 스레드에서 합니다.|  
  
## <a name="remarks"></a>설명  
 에 정의 된 메모리 할당 메서드를 [IHostMemoryManager](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-interface.md) 하 고 [IHostMAlloc](../../../../docs/framework/unmanaged-api/hosting/ihostmalloc-interface.md) 인터페이스는이 형식의 매개 변수를 사용 합니다. 오류의 심각도 따라 호스트 여부를 결정할 수 할당 요청이 즉시 실패 또는 처리할 수 있습니다 때까지 기다립니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRMemoryNotificationCallback 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrmemorynotificationcallback-interface.md)
- [호스팅 열거형](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
