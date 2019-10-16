---
title: IHostMemoryManager::VirtualQuery 메서드
ms.date: 03/30/2017
api_name:
- IHostMemoryManager.VirtualQuery
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMemoryManager::VirtualQuery
helpviewer_keywords:
- IHostMemoryManager::VirtualQuery method [.NET Framework hosting]
- VirtualQuery method [.NET Framework hosting]
ms.assetid: 757af1e6-b9e8-49e7-b5db-342be3aa205f
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 16d146766786f129d6da38bde1126ce8afe5e70f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963685"
---
# <a name="ihostmemorymanagervirtualquery-method"></a>IHostMemoryManager::VirtualQuery 메서드
해당 Win32 함수에 대 한 논리 래퍼로 사용 됩니다. 의 `VirtualQuery` Win32 구현은 호출 프로세스의 가상 주소 공간에 있는 페이지 범위에 대 한 정보를 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT VirtualQuery (  
    [in]  void*    lpAddress,  
    [out] void*    lpBuffer,  
    [in]  SIZE_T   dwLength,  
    [out] SIZE_T*  pResult  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `lpAddress`  
 진행 쿼리할 가상 메모리의 주소에 대 한 포인터입니다.  
  
 `lpBuffer`  
 제한이 지정 된 메모리 영역에 대 한 정보를 포함 하는 구조체에 대 한 포인터입니다.  
  
 `dwLength`  
 진행 가 `lpBuffer` 가리키는 버퍼의 크기 (바이트)입니다.  
  
 `pResult`  
 제한이 정보 버퍼에서 반환 된 바이트 수에 대 한 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|`VirtualQuery`성공적으로 반환 되었습니다.|  
|HOST_E_CLRNOTAVAILABLE|CLR (공용 언어 런타임)이 프로세스에 로드 되지 않았거나 CLR이 관리 코드를 실행할 수 없거나 호출을 성공적으로 처리할 수 없는 상태에 있습니다.|  
|HOST_E_TIMEOUT|호출 시간이 초과 되었습니다.|  
|HOST_E_NOT_OWNER|호출자가 잠금을 소유 하지 않습니다.|  
|HOST_E_ABANDONED|차단 된 스레드나 파이버에서 대기 하는 동안 이벤트를 취소 했습니다.|  
|E_FAIL|알 수 없는 치명적인 오류가 발생 했습니다. 메서드가 E_FAIL을 반환 하는 경우 프로세스 내에서 더 이상 CLR을 사용할 수 없습니다. 호스팅 메서드에 대 한 후속 호출은 HOST_E_CLRNOTAVAILABLE을 반환 합니다.|  
  
## <a name="remarks"></a>설명  
 `VirtualQuery`호출 프로세스의 가상 주소 공간에 있는 페이지 범위에 대 한 정보를 제공 합니다. 이 구현에서는 `pResult` 매개 변수의 값을 정보 버퍼에서 반환 된 바이트 수로 설정 하 고 HRESULT 값을 반환 합니다. Win32 `VirtualQuery` 함수에서 반환 값은 버퍼 크기입니다. 자세한 내용은 Windows 플랫폼 설명서를 참조 하세요.  
  
> [!IMPORTANT]
> 운영 체제의 구현 `VirtualQuery` 에는 교착 상태가 발생 하지 않으며 사용자 코드에서 일시 중단 된 임의 스레드를 사용 하 여 완료 될 때까지 실행할 수 있습니다. 이 메서드의 호스팅된 버전을 구현 하는 경우 매우 주의 해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IHostMemoryManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostmemorymanager-interface.md)
