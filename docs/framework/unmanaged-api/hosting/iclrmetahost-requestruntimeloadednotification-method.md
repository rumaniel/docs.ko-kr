---
title: ICLRMetaHost::RequestRuntimeLoadedNotification 메서드
ms.date: 03/30/2017
api_name:
- ICLRMetaHost.RequestRuntimeLoadedNotification
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMetaHost::RequestRuntimeLoadedNotification
helpviewer_keywords:
- RequestRuntimeLoadedNotification method [.NET Framework hosting]
- ICLRMetaHost::RequestRuntimeLoadedNotification method [.NET Framework hosting]
ms.assetid: 0d5ccc4d-0193-41f5-af54-45d7b70d5321
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 539f69c33b67ad1a8a514062c5d777deaced1599
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965002"
---
# <a name="iclrmetahostrequestruntimeloadednotification-method"></a>ICLRMetaHost::RequestRuntimeLoadedNotification 메서드
CLR (공용 언어 런타임) 버전이 처음 로드 되었지만 아직 시작 되지 않은 경우 호출 되도록 보장 되는 콜백 함수를 제공 합니다. 이 메서드는 [Lockclrversion](../../../../docs/framework/unmanaged-api/hosting/lockclrversion-function.md) 함수를 대체 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT RequestRuntimeLoadedNotification (  
    [in] RuntimeLoadedCallbackFnPtr pCallbackFunction);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pCallbackFunction`  
 진행 새 런타임이 로드 될 때 호출 되는 콜백 함수입니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다.  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|메서드가 완료되었습니다.|  
|E_POINTER|`pCallbackFunction`가 null입니다.|  
  
## <a name="remarks"></a>설명  
 콜백은 다음과 같은 방식으로 작동 합니다.  
  
- 콜백은 처음으로 런타임에 로드 된 경우에만 호출 됩니다.  
  
- 콜백이 동일한 런타임의 재진입 로드에 대해 호출 되지 않습니다.  
  
- 재진입이 아닌 런타임 로드의 경우 콜백 함수에 대 한 호출이 serialize 됩니다.  
  
 콜백 함수에는 다음과 같은 프로토타입이 있습니다.  
  
```cpp  
typedef void (__stdcall *RuntimeLoadedCallbackFnPtr)(  
                     ICLRRuntimeInfo *pRuntimeInfo,  
                     CallbackThreadSetFnPtr pfnCallbackThreadSet,  
                     CallbackThreadUnsetFnPtr pfnCallbackThreadUnset);  
```  
  
 콜백 함수 프로토타입은 다음과 같습니다.  
  
- `pfnCallbackThreadSet`:  
  
    ```cpp  
    typedef HRESULT (__stdcall *CallbackThreadSetFnPtr)();  
    ```  
  
- `pfnCallbackThreadUnset`:  
  
    ```cpp  
    typedef HRESULT (__stdcall *CallbackThreadUnsetFnPtr)();  
    ```  
  
 호스트가 로드 되거나 재진입 방식 `pfnCallbackThreadSet` 으로 다른 런타임을 로드 하려는 경우 콜백 함수에 제공 된 및 `pfnCallbackThreadUnset` 매개 변수를 다음과 같은 방식으로 사용 해야 합니다.  
  
- `pfnCallbackThreadSet`는 이러한 로드를 시도 하기 전에 런타임 로드를 발생 시킬 수 있는 스레드에서 호출 해야 합니다.  
  
- `pfnCallbackThreadUnset`스레드가 더 이상 이러한 런타임 로드를 발생 시 키 게 하지 않고 초기 콜백에서 반환 되기 전에를 호출 해야 합니다.  
  
- `pfnCallbackThreadSet`및 `pfnCallbackThreadUnset` 는 모두 재진입 성이 아닙니다.  
  
> [!NOTE]
> 호스트 응용 프로그램은 `pfnCallbackThreadSet` `pCallbackFunction` 매개 변수 `pfnCallbackThreadUnset` 범위 밖에 서를 호출 해서는 안 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MetaHost.h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRMetaHost 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrmetahost-interface.md)
- [호스팅](../../../../docs/framework/unmanaged-api/hosting/index.md)
