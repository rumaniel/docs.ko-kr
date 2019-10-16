---
title: ICLRRuntimeInfo::IsLoadable 메서드
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.IsLoadable
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::IsLoadable
helpviewer_keywords:
- IsLoadable method [.NET Framework hosting]
- ICLRRuntimeInfo::IsLoadable method [.NET Framework hosting]
ms.assetid: 205ca53b-e78e-49b2-9a46-2a7823e96b8c
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4937c86be434ef5e97ec72763b7c53d5435bcaf4
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67774030"
---
# <a name="iclrruntimeinfoisloadable-method"></a>ICLRRuntimeInfo::IsLoadable 메서드
이 인터페이스와 연결 된 런타임 고려 현재 프로세스에 로드할 수 있는지 여부를 나타내는 프로세스에 이미 로드 될 수 있는 다른 런타임과 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT IsLoadable(  
        [out, retval] BOOL *pbLoadable);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pbLoadable`  
 [out] `true` 이 런타임에서이 고, 그렇지 않으면 현재 프로세스에 로드 수 있으면 `false`합니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다.  
  
|HRESULT|설명|  
|-------------|-----------------|  
|S_OK|메서드가 완료되었습니다.|  
|E_POINTER|`pbLoadable`가 null입니다.|  
  
## <a name="remarks"></a>설명  
 다른 런타임 프로세스에 이미 로드 하 고이 인터페이스와 연결 된 런타임 in-process side-by-side-실행에 로드할 수 있습니다 `pbLoadable` 반환 `true`합니다. 두 개의 런타임 side-by-side-in-process로 실행할 수 없는 경우 `pbLoadable` 반환 `false`합니다. 예를 들어,는 CLR (공용 언어 런타임) 버전 4-side-by-side CLR 버전 2.0 사용 하 여 동일한 프로세스에서 또는 CLR 버전 1.1 실행할 수 있습니다. 그러나 CLR 버전 1.1 및 CLR 버전 2.0-병렬 처리를 실행할 수 없습니다.  
  
 런타임 없는 프로세스에 로드 되는 경우이 메서드는 항상 반환 `true`합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MetaHost.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRRuntimeInfo 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
- [호스팅](../../../../docs/framework/unmanaged-api/hosting/index.md)
