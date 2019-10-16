---
title: IHostSecurityManager::OpenThreadToken 메서드
ms.date: 03/30/2017
api_name:
- IHostSecurityManager.OpenThreadToken
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSecurityManager::OpenThreadToken
helpviewer_keywords:
- IHostSecurityManager::OpenThreadToken method [.NET Framework hosting]
- OpenThreadToken method [.NET Framework hosting]
ms.assetid: d5999052-8bf0-4a9e-8621-da6284406b18
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c1beeb0ff6b2e3493f0814fc3371f189bd4d485d
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67778016"
---
# <a name="ihostsecuritymanageropenthreadtoken-method"></a>IHostSecurityManager::OpenThreadToken 메서드
현재 실행 중인 스레드와 연결 된 임의 액세스 토큰을 엽니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT OpenThreadToken (  
    [in]  DWORD    dwDesiredAccess,   
    [in]  BOOL     bOpenAsSelf,   
    [out] HANDLE   *phThreadToken  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `dwDesiredAccess`  
 [in] 스레드 토큰에 대 한 액세스 요청된 유형을 지정 하는 액세스 값의 마스크입니다. 이러한 값은 win32에서 정의 `OpenThreadToken` 함수입니다. 요청 된 액세스 형식은 토큰의 임의 액세스 제어 목록 (DACL) 액세스 권한 부여 또는 거부의 서식을 결정할 수에 대 한 조정 됩니다.  
  
 `bOpenAsSelf`  
 [in] `true` ; 호출 스레드에 대 한 프로세스의 보안 컨텍스트를 사용 하 여 액세스 검사 수행 수를 지정 하려면 `false` 자체 호출 스레드에 대 한 보안 컨텍스트를 사용 하 여 액세스 검사를 수행할 수를 지정 합니다. 스레드는 클라이언트를 가장 하는 경우에 클라이언트 프로세스의 보안 컨텍스트 수 있습니다.  
  
 `phThreadToken`  
 [out] 새로 열린된 액세스 토큰에 대 한 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|`OpenThreadToken` 성공적으로 반환 합니다.|  
|HOST_E_CLRNOTAVAILABLE|프로세스에는 CLR (공용 언어 런타임)에 로드 되지 또는 CLR 상태인는 관리 코드를 실행 하거나 호출을 처리할 수 없습니다.|  
|HOST_E_TIMEOUT|호출 시간이 초과 되었습니다.|  
|HOST_E_NOT_OWNER|호출자가 잠금을 소유 하지 않습니다.|  
|HOST_E_ABANDONED|이벤트가 차단 된 스레드가 취소 된 또는 파이버를 대기 하 고 있습니다.|  
|E_FAIL|알 수 없는 치명적인 오류가 발생 했습니다. 메서드 E_FAIL을 반환 하는 경우 CLR은 프로세스 내에서 사용할 수 없습니다. 메서드를 호스트 하는 데 대 한 후속 호출 HOST_E_CLRNOTAVAILABLE를 반환 합니다.|  
  
## <a name="remarks"></a>설명  
 `IHostSecurityManager::OpenThreadToken` 동작 마찬가지로 동일한 이름의 해당 Win32 함수를 제외 하 고 Win32 함수에서는 호출자가 임의의 스레드 핸들을 전달 하는 동안 요소를 `IHostSecurityManager::OpenThreadToken` 호출 스레드와 연결 된 토큰에만 엽니다.  
  
 `HANDLE` 형식은 COM 규격, 즉, 해당 크기는 운영 체제, 특정 및 사용자 지정 마샬링 필요 합니다. 따라서이 토큰은 CLR과 호스트 간의 프로세스 내 에서만 사용 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IHostSecurityContext 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritycontext-interface.md)
- [IHostSecurityManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-interface.md)
