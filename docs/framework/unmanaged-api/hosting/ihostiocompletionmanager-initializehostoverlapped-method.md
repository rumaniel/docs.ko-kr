---
title: IHostIoCompletionManager::InitializeHostOverlapped 메서드
ms.date: 03/30/2017
api_name:
- IHostIoCompletionManager.InitializeHostOverlapped
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostIoCompletionManager::InitializeHostOverlapped
helpviewer_keywords:
- IHostIoCompletionManager::InitializeHostOverlapped method [.NET Framework hosting]
- InitializeHostOverlapped method [.NET Framework hosting]
ms.assetid: c35199bf-bc47-4901-b467-4e8a37644bbb
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ac7014962b99ac167e8192c13b2bae5ca92470f0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69948519"
---
# <a name="ihostiocompletionmanagerinitializehostoverlapped-method"></a>IHostIoCompletionManager::InitializeHostOverlapped 메서드
호스트에 비동기 i/o 요청에 사용 되는 Win32 `OVERLAPPED` 구조에 추가할 사용자 지정 데이터를 초기화할 수 있는 기회를 제공 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT InitializeHostOverlapped (  
    [in] void* pvOverlapped  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pvOverlapped`  
 진행 I/o 요청에 포함 될 `OVERLAPPED` Win32 구조체에 대 한 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|`InitializeHostOverlapped`성공적으로 반환 되었습니다.|  
|HOST_E_CLRNOTAVAILABLE|CLR (공용 언어 런타임)이 프로세스에 로드 되지 않았거나 CLR이 관리 코드를 실행할 수 없거나 호출을 성공적으로 처리할 수 없는 상태에 있습니다.|  
|HOST_E_TIMEOUT|호출 시간이 초과 되었습니다.|  
|HOST_E_NOT_OWNER|호출자가 잠금을 소유 하지 않습니다.|  
|HOST_E_ABANDONED|차단 된 스레드나 파이버에서 대기 하는 동안 이벤트를 취소 했습니다.|  
|E_FAIL|알 수 없는 치명적인 오류가 발생 했습니다. 메서드가 E_FAIL을 반환 하는 경우 프로세스 내에서 더 이상 CLR을 사용할 수 없습니다. 호스팅 메서드에 대 한 후속 호출은 HOST_E_CLRNOTAVAILABLE을 반환 합니다.|  
|E_OUTOFMEMORY|요청한 리소스를 할당 하는 데 사용할 수 있는 메모리가 부족 합니다.|  
  
## <a name="remarks"></a>설명  
 Windows 플랫폼 함수는 `OVERLAPPED` 구조체를 사용 하 여 비동기 i/o 요청에 대 한 상태를 저장 합니다. CLR은 `InitializeHostOverlapped` 메서드를 호출 하 여 호스트에 사용자 지정 데이터 `OVERLAPPED` 를 인스턴스에 추가할 수 있는 기회를 제공 합니다.  
  
> [!IMPORTANT]
> 사용자 지정 데이터 블록의 시작 부분을 가져오려면 호스트에서 `OVERLAPPED` 구조체의 크기 (`sizeof(OVERLAPPED)`)로 오프셋을 설정 해야 합니다.  
  
 E_OUTOFMEMORY의 반환 값은 호스트가 사용자 지정 데이터를 초기화 하지 못했음을 나타냅니다. 이 경우 CLR은 오류를 보고 하 고 호출에 실패 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRIoCompletionManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclriocompletionmanager-interface.md)
- [GetHostOverlappedSize 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-gethostoverlappedsize-method.md)
- [IHostIoCompletionManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-interface.md)
