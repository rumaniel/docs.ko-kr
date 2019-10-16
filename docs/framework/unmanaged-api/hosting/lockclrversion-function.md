---
title: LockClrVersion 함수
ms.date: 03/30/2017
api_name:
- LockClrVersion
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- LockClrVersion
helpviewer_keywords:
- LockClrVersion function [.NET Framework hosting]
ms.assetid: 1318ee37-c43b-40eb-bbe8-88fc46453d74
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6742293c1970198ef3d5f5da7d75a0c78e78045c
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67768416"
---
# <a name="lockclrversion-function"></a>LockClrVersion 함수
호스트가 명시적으로 CLR을 초기화 하기 전에 프로세스 내에서 사용할는 버전의 CLR (공용 언어 런타임)을 결정할 수 있습니다.  
  
 .NET Framework 4에서이 함수에 사용 되지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT LockClrVersion (  
    [in] FLockClrVersionCallback   hostCallback,  
    [in] FLockClrVersionCallback  *pBeginHostSetup,  
    [in] FLockClrVersionCallback  *pEndHostSetup  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `hostCallback`  
 [in] 초기화 시 CLR에서 호출 되는 함수입니다.  
  
 `pBeginHostSetup`  
 [in] 해당 초기화 CLR을 알리기 위해 호스트에서 호출 될 함수를 시작 합니다.  
  
 `pEndHostSetup`  
 [in] 해당 초기화 CLR을 알리기 위해 호스트에서 호출 될 함수 완료 되었습니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음 값 외에도 WinError.h에 정의 된 대로 표준 COM 오류 코드를 반환 합니다.  
  
|반환 코드|Description|  
|-----------------|-----------------|  
|S_OK|메서드가 완료되었습니다.|  
|E_INVALIDARG|인수 중 하나 이상이 null입니다.|  
  
## <a name="remarks"></a>설명  
 호스트에서는 `LockClrVersion` CLR을 초기화 하기 전에 합니다. `LockClrVersion` 형식의 콜백을 모두 3 개의 매개 변수를 [FLockClrVersionCallback](../../../../docs/framework/unmanaged-api/hosting/flockclrversioncallback-function-pointer.md)합니다. 이 형식은 다음과 같이 정의 됩니다.  
  
```cpp  
typedef HRESULT ( __stdcall *FLockClrVersionCallback ) ();  
```  
  
 다음 단계는 런타임 초기화 시 발생합니다.  
  
1. 호스트 호출 [CorBindToRuntimeEx](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md) 또는 다른 런타임 초기화 함수 중 하나입니다. 또는 호스트 COM 개체 활성화를 사용 하 여 런타임을 초기화할 수 없습니다.  
  
2. 런타임에서 호출 하 여 지정 된 함수는 `hostCallback` 매개 변수입니다.  
  
3. 지정 된 함수의 `hostCallback` 다음 호출 시퀀스를 사용 하는 합니다.  
  
    - 에 지정 된 함수는 `pBeginHostSetup` 매개 변수입니다.  
  
    - `CorBindToRuntimeEx` (또는 다른 런타임 초기화 함수)입니다.  
  
    - [ICLRRuntimeHost::SetHostControl](../../../../docs/framework/unmanaged-api/hosting/iclrruntimehost-sethostcontrol-method.md).  
  
    - [ICLRRuntimeHost::Start](../../../../docs/framework/unmanaged-api/hosting/iclrruntimehost-start-method.md).  
  
    - 에 지정 된 함수는 `pEndHostSetup` 매개 변수입니다.  
  
 모든 호출은 `pBeginHostSetup` 에 `pEndHostSetup` 단일 스레드 또는 파이버를 동일한 논리 스택과 수행 되어야 합니다. 이 스레드는 스레드에서 다를 수 있습니다 `hostCallback` 라고 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [사용되지 않는 CLR 호스팅 함수](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
