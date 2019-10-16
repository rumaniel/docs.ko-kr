---
title: CorBindToRuntimeHost 함수
ms.date: 03/30/2017
api_name:
- CorBindToRuntimeHost
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- CorBindToRuntimeHost
helpviewer_keywords:
- CorBindToRuntimeHost function [.NET Framework hosting]
ms.assetid: 5c826ba3-8258-49bc-a417-78807915fcaf
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7e1965917e8a1c5ae07cf119df3664b969a979be
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69969247"
---
# <a name="corbindtoruntimehost-function"></a>CorBindToRuntimeHost 함수
호스트에서 지정 된 버전의 CLR (공용 언어 런타임)을 프로세스로 로드할 수 있도록 합니다.  
  
 이 함수는 .NET Framework 4에서 더 이상 사용 되지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CorBindToRuntimeHost (  
    [in] LPCWSTR       pwszVersion,   
    [in] LPCWSTR       pwszBuildFlavor,   
    [in] LPCWSTR       pwszHostConfigFile,   
    [in] VOID*         pReserved,   
    [in] DWORD         startupFlags,   
    [in] REFCLSID      rclsid,   
    [in] REFIID        riid,   
    [out] LPVOID FAR  *ppv  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pwszVersion`  
 진행 로드 하려는 CLR의 버전을 설명 하는 문자열입니다.  
  
 .NET Framework의 버전 번호는 마침표로 구분 된 네 부분으로 구성 되어 있습니다. 주 버전. 부 버전. *빌드. 수정 버전*. 로 `pwszVersion` 전달 된 문자열은 "v" 문자 뒤에 버전 번호의 처음 세 부분 (예: "v 1.0.1529")을 사용 하 여 시작 해야 합니다.  
  
 CLR의 이전 버전과의 호환성을 지정 하는 정책 문과 함께 일부 CLR 버전이 설치 됩니다. 기본적으로 시작 shim은 정책 문에 `pwszVersion` 대해 평가 하 고 요청 되는 버전과 호환 되는 최신 버전의 런타임을 로드 합니다. 호스트는 `startupFlags` 매개 변수에 STARTUP_LOADER_SAFEMODE 값을 전달 하 여 shim이 정책 평가를 건너뛰고에 `pwszVersion` 지정 된 정확한 버전을 로드 하도록 강제할 수 있습니다.  
  
 `pwszVersion` 가`null,` 이면 메서드는 CLR의 모든 버전을 로드 하지 않습니다. 대신 CLR_E_SHIM_RUNTIMELOAD를 반환 하며,이는 런타임을 로드 하지 못했음을 나타냅니다.  
  
 `pwszBuildFlavor`  
 진행 CLR의 워크스테이션 빌드 또는 서버를 로드할지 여부를 지정 하는 문자열입니다. 유효한 값은 `svr` 및 `wks`입니다. 서버 빌드는 가비지 컬렉션에 대해 여러 프로세서를 활용 하도록 최적화 되며 워크스테이션 빌드는 단일 프로세서 컴퓨터에서 실행 되는 클라이언트 응용 프로그램에 최적화 되어 있습니다.  
  
 가 `pwszBuildFlavor` null로 설정 된 경우 워크스테이션 빌드가 로드 됩니다. 단일 프로세서 컴퓨터에서 실행 되는 경우가로 `pwszBuildFlavor` `svr`설정 된 경우에도 워크스테이션 빌드가 항상 로드 됩니다. 그러나가로 `pwszBuildFlavor` `svr` 설정 되 고 동시 가비지 수집이 지정 된 경우 ( `startupFlags` 매개 변수에 대 한 설명 참조) 서버 빌드가 로드 됩니다.  
  
> [!NOTE]
> Intel Itanium 아키텍처 (이전의 IA-64)를 구현 하는 64 비트 시스템에서 WOW64 x86 에뮬레이터를 실행 하는 응용 프로그램에서는 동시 가비지 수집이 지원 되지 않습니다. 64 비트 Windows 시스템에서 WOW64를 사용 하는 방법에 대 한 자세한 내용은 [32 비트 응용 프로그램 실행](/windows/desktop/WinProg64/running-32-bit-applications)을 참조 하세요.  
  
 `pwszHostConfigFile`  
 진행 로드할 CLR 버전을 지정 하는 호스트 구성 파일의 이름입니다. 파일 이름에 정규화 된 경로가 포함 되어 있지 않으면 파일은 호출 하는 실행 파일과 동일한 디렉터리에 있는 것으로 간주 됩니다.  
  
 `pReserved`  
 진행 향후 확장성을 위해 예약 되었습니다.  
  
 `startupFlags`  
 진행 동시 가비지 컬렉션, 도메인 중립 코드 및 `pwszVersion` 매개 변수의 동작을 제어 하는 플래그 집합입니다. 플래그가 설정 되지 않은 경우 기본값은 단일 도메인입니다. 지원 되는 값 목록은 [STARTUP_FLAGS 열거](../../../../docs/framework/unmanaged-api/hosting/startup-flags-enumeration.md)를 참조 하세요.  
  
 `rclsid`  
 진행 [ICorRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md) 또는 [ICLRRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/iclrruntimehost-interface.md) 인터페이스를 구현 하는 coclass 의 `CLSID`입니다. 지원 되는 값은 CLSID_CorRuntimeHost 또는 CLSID_CLRRuntimeHost입니다.  
  
 `riid`  
 진행 요청 하는 인터페이스 의입니다.`IID` 지원 되는 값은 IID_ICorRuntimeHost 또는 IID_ICLRRuntimeHost입니다.  
  
 `ppv`  
 제한이 로드 된 런타임 버전에 대 한 인터페이스 포인터입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.idl  
  
 **라이브러리** MSCorEE.dll  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [CorBindToCurrentRuntime 함수](../../../../docs/framework/unmanaged-api/hosting/corbindtocurrentruntime-function.md)
- [CorBindToRuntime 함수](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntime-function.md)
- [CorBindToRuntimeByCfg 함수](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md)
- [CorBindToRuntimeEx 함수](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md)
- [ICorRuntimeHost 인터페이스](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md)
- [사용되지 않는 CLR 호스팅 함수](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
