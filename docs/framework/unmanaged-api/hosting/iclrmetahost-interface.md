---
title: ICLRMetaHost 인터페이스
ms.date: 03/30/2017
api_name:
- ICLRMetaHost
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMetaHost
helpviewer_keywords:
- ICLRMetaHost interface [.NET Framework hosting]
ms.assetid: c627fcdd-fc4f-4b1c-8e91-df8536f627d8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 45089d1b64264e000c07603808f0c5fb1263b042
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67776578"
---
# <a name="iclrmetahost-interface"></a>ICLRMetaHost 인터페이스
해당 버전 번호를 기준으로 CLR (공용 언어 런타임)의 특정 버전을 반환, 모든 설치 된 Clr list, 지정된 된 프로세스에 로드 되는 모든 런타임 목록, 어셈블리로 컴파일, 프로세스를 종료 하는 데 CLR 버전을 검색 하는 메서드를 제공 합니다. 깨끗 한 런타임이 종료 및 레거시 API 바인딩을 쿼리 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[EnumerateInstalledRuntimes 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrmetahost-enumerateinstalledruntimes-method.md)|유효한 포함 하는 열거자를 반환 합니다 [ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md) 컴퓨터에 설치 되어 있는 각 CLR 버전에 대 한 인터페이스 포인터입니다.|  
|[EnumerateLoadedRuntimes 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrmetahost-enumerateloadedruntimes-method.md)|유효한 포함 하는 열거자를 반환 합니다 [ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md) 주어진된 프로세스에서 로드 되는 각 CLR에 대 한 인터페이스 포인터입니다. 이 메서드를 대체 [GetVersionFromProcess](../../../../docs/framework/unmanaged-api/hosting/getversionfromprocess-function.md)합니다.|  
|[ExitProcess 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrmetahost-exitprocess-method.md)|로드 된 모든 런타임을 정상적으로 종료 하 고 프로세스를 종료 합니다. 대체는 [CorExitProcess](../../../../docs/framework/unmanaged-api/hosting/corexitprocess-function.md) 함수입니다.|  
|[GetRuntime 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrmetahost-getruntime-method.md)|가져옵니다 합니다 [ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md) 특정 CLR 버전에 해당 하는 인터페이스입니다. 이 메서드를 대체 합니다 [CorBindToRuntimeEx](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md) 함수를 사용 합니다 [STARTUP_LOADER_SAFEMODE](../../../../docs/framework/unmanaged-api/hosting/startup-flags-enumeration.md) 플래그입니다.|  
|[GetVersionFromFile 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrmetahost-getversionfromfile-method.md)|파일 경로가 지정 된 어셈블리의 원래.net 컴파일 버전을 (메타 데이터에 저장 됨)을 가져옵니다. 이 메서드를 대체 [GetFileVersion](../../../../docs/framework/unmanaged-api/hosting/getfileversion-function.md)합니다.|  
|[QueryLegacyV2RuntimeBinding 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrmetahost-querylegacyv2runtimebinding-method.md)|레거시 활성화 정책이 바인딩된, 예를 들어 사용 하 여 런타임을 나타내는 인터페이스를 반환 합니다 `useLegacyV2RuntimeActivationPolicy` 특성을 합니다 [ \<시작 > 요소](../../../../docs/framework/configure-apps/file-schema/startup/startup-element.md) 직접 사용 하 여 구성 파일 항목 호출 하거나 레거시 활성화 Api는 [ICLRRuntimeInfo::BindAsLegacyV2Runtime](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-bindaslegacyv2runtime-method.md) 메서드.|  
|[RequestRuntimeLoadedNotification 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrmetahost-requestruntimeloadednotification-method.md)|CLR 버전을 처음 로드 되었지만 아직 시작 하지 않은 경우 지정 된 함수 포인터에 대 한 콜백의 보장 합니다. 이 메서드를 대체 [LockClrVersion](../../../../docs/framework/unmanaged-api/hosting/lockclrversion-function.md)|  
  
## <a name="remarks"></a>설명  
 호출 하 여이 인터페이스의 인스턴스를 가져올 유일한 방법은는 [CLRCreateInstance](../../../../docs/framework/unmanaged-api/hosting/clrcreateinstance-function.md) 같이 함수:  
  
```cpp  
ICLRMetaHost *pMetaHost = NULL;  
HRESULT hr = CLRCreateInstance(CLSID_CLRMetaHost,  
                   IID_ICLRMetaHost, (LPVOID*)&pMetaHost);  
```  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MetaHost.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
- [호스팅](../../../../docs/framework/unmanaged-api/hosting/index.md)
