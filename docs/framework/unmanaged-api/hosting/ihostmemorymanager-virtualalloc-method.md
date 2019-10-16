---
title: IHostMemoryManager::VirtualAlloc 메서드
ms.date: 03/30/2017
api_name:
- IHostMemoryManager.VirtualAlloc
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMemoryManager::VirtualAlloc
helpviewer_keywords:
- VirtualAlloc method [.NET Framework hosting]
- IHostMemoryManager::VirtualAlloc method [.NET Framework hosting]
ms.assetid: 4dff3646-a050-4bd9-ac31-fe307e8637ec
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9a0764cb212a95412a4dcf9455b7648ee863951e
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67767671"
---
# <a name="ihostmemorymanagervirtualalloc-method"></a>IHostMemoryManager::VirtualAlloc 메서드
역할을 해당 하는 Win32 함수에 대 한 논리적 래퍼입니다. Win32 구현의 `VirtualAlloc` 예약 하거나 호출 프로세스의 가상 주소 공간에서 페이지의 영역을 커밋합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT VirtualAlloc (  
    [in]  void*   pAddress,  
    [in]  SIZE_T  dwSize,  
    [in]  DWORD   flAllocationType,  
    [in]  DWORD   flProtect,  
    [in]  EMemoryCriticalLevel dwCriticalLevel,  
    [out] void**  ppMem  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pAddress`  
 [in] 할당할 영역의 시작 주소에 대 한 포인터입니다.  
  
 `dwSize`  
 [in] 영역의 바이트 크기입니다.  
  
 `flAllocationType`  
 [in] 메모리 할당의 형식입니다.  
  
 `flProtect`  
 [in] 할당할 페이지 영역에 대 한 메모리 보호 합니다.  
  
 `dwCriticalLevel`  
 [in] [EMemoryCriticalLevel](../../../../docs/framework/unmanaged-api/hosting/ememorycriticallevel-enumeration.md) 영향 할당 오류를 나타내는 값입니다.  
  
 `ppMem`  
 [out] 요청을 처리 하지 못한 경우 null을 할당 된 메모리의 시작 주소에 대 한 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|설명|  
|-------------|-----------------|  
|S_OK|`VirtualAlloc` 성공적으로 반환 합니다.|  
|HOST_E_CLRNOTAVAILABLE|프로세스에는 CLR (공용 언어 런타임)에 로드 되지 또는 CLR 상태인는 관리 코드를 실행 하거나 호출을 처리할 수 없습니다.|  
|HOST_E_TIMEOUT|호출 시간이 초과 되었습니다.|  
|HOST_E_NOT_OWNER|호출자가 잠금을 소유 하지 않습니다.|  
|HOST_E_ABANDONED|이벤트가 차단 된 스레드가 취소 된 또는 파이버를 대기 하 고 있습니다.|  
|E_FAIL|알 수 없는 치명적인 오류가 발생 했습니다. 메서드 E_FAIL을 반환 하는 경우 CLR은 프로세스 내에서 사용할 수 없습니다. 메서드를 호스트 하는 데 대 한 후속 호출 HOST_E_CLRNOTAVAILABLE를 반환 합니다.|  
|E_OUTOFMEMORY|할당 요청을 완료 하려면 사용할 수 있는 메모리가 부족 합니다.|  
  
## <a name="remarks"></a>설명  
 호출 하 여 프로세스의 주소 공간에서 영역을 예약 `VirtualAlloc`합니다. `pAddress` 하려는 메모리 블록의 시작 주소를 포함 하는 매개 변수입니다. 이 매개 변수는 일반적으로 설정 하는 null입니다. 운영 체제는 프로세스에 사용할 수 있는 사용 가능한 주소 범위 레코드를 유지합니다. `pAddress` null 값에는 시스템에서 판단 되는 영역을 예약 하도록 지정 합니다. 또는 메모리 블록에 대 한 특정 시작 주소를 제공할 수 있습니다. 두 경우 모두 출력 매개 변수 `ppMem` 할당된 된 메모리에 대 한 포인터로 반환 됩니다. 함수 자체에 HRESULT 값을 반환 합니다.  
  
 Win32 `VirtualAlloc` 함수에는 한 `ppMem` 매개 변수를 대신 할당된 된 메모리에 대 한 포인터를 반환 합니다. 자세한 내용은 Windows 플랫폼 설명서를 참조 하십시오.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IHostMemoryManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-interface.md)
