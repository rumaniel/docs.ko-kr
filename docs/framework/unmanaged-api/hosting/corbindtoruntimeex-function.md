---
title: CorBindToRuntimeEx 함수
ms.date: 03/30/2017
api_name:
- CorBindToRuntimeEx
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- CorBindToRuntimeEx
helpviewer_keywords:
- CorBindToRuntimeEx function [.NET Framework hosting]
ms.assetid: aae9fb17-5d01-41da-9773-1b5b5b642d81
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 88f31ae29efee9b353c2dcc679724db73da5444e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69969423"
---
# <a name="corbindtoruntimeex-function"></a>CorBindToRuntimeEx 함수
관리 되지 않는 호스트에서 CLR (공용 언어 런타임)을 프로세스로 로드할 수 있도록 합니다. [CorBindToRuntime](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntime-function.md) 및 `CorBindToRuntimeEx` 함수는 동일한 `CorBindToRuntimeEx` 작업을 수행 하지만 함수를 사용 하 여 CLR의 동작을 지정 하는 플래그를 설정할 수 있습니다.  
  
 이 함수는 .NET Framework 4에서 더 이상 사용 되지 않습니다.  
  
 이 함수는 호스트에서 다음 작업을 수행할 수 있도록 하는 매개 변수 집합을 사용 합니다.  
  
- 로드할 런타임 버전을 지정 합니다.  
  
- 서버 또는 워크스테이션 빌드를 로드할지 여부를 나타냅니다.  
  
- 동시 가비지 수집 또는 비 동시 가비지 수집 수행 여부를 제어 합니다.  
  
> [!NOTE]
> Intel Itanium 아키텍처 (이전의 IA-64)를 구현 하는 64 비트 시스템에서 WOW64 x86 에뮬레이터를 실행 하는 응용 프로그램에서는 동시 가비지 수집이 지원 되지 않습니다. 64 비트 Windows 시스템에서 WOW64를 사용 하는 방법에 대 한 자세한 내용은 [32 비트 응용 프로그램 실행](/windows/desktop/WinProg64/running-32-bit-applications)을 참조 하세요.  
  
- 어셈블리가 도메인 중립적으로 로드 되는지 여부를 제어 합니다.  
  
- CLR 인스턴스를 시작 하기 전에 구성 하기 위한 추가 옵션을 설정 하는 데 사용할 수 있는 [ICorRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md) 에 대 한 인터페이스 포인터를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CorBindToRuntimeEx (  
    [in]  LPCWSTR      pwszVersion,   
    [in]  LPCWSTR      pwszBuildFlavor,   
    [in]  DWORD        startupFlags,   
    [in]  REFCLSID     rclsid,   
    [in]  REFIID       riid,   
    [out] LPVOID FAR  *ppv  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pwszVersion`  
 진행 로드 하려는 CLR의 버전을 설명 하는 문자열입니다.  
  
 .NET Framework의 버전 번호는 마침표로 구분 된 네 부분으로 구성 되어 있습니다. 주 버전. 부 버전. *빌드. 수정 버전*. 로 `pwszVersion` 전달 된 문자열은 "v" 문자 뒤에 버전 번호의 처음 세 부분 (예: "v 1.0.1529")을 사용 하 여 시작 해야 합니다.  
  
 CLR의 이전 버전과의 호환성을 지정 하는 정책 문과 함께 일부 CLR 버전이 설치 됩니다. 기본적으로 시작 shim은 정책 문에 `pwszVersion` 대해 평가 하 고 요청 되는 버전과 호환 되는 최신 버전의 런타임을 로드 합니다. 호스트는 아래에 설명 된 `pwszVersion` `startupFlags` 대로 매개 변수에 `STARTUP_LOADER_SAFEMODE` 대 한 값을 전달 하 여 shim이 정책 평가를 건너뛰고에 지정 된 정확한 버전을 로드 하도록 강제 설정할 수 있습니다.  
  
 호출자가에 대해 `pwszVersion` `CorBindToRuntimeEx` null을 지정 하는 경우는 버전 번호가 .NET Framework 4 런타임 보다 낮은 설치 된 런타임 집합을 식별 하 고 해당 집합에서 최신 버전의 런타임을 로드 합니다. .NET Framework 4 이상을 로드 하지 않으며, 이전 버전이 설치 되어 있지 않으면 실패 합니다. Null을 전달 하면 로드 되는 런타임 버전을 호스트에서 제어할 수 없습니다. 이 방법은 일부 시나리오에서 적합할 수 있지만 호스트에서 로드할 특정 버전을 제공 하는 것이 좋습니다.  
  
 `pwszBuildFlavor`  
 진행 CLR의 워크스테이션 빌드 또는 서버를 로드할지 여부를 지정 하는 문자열입니다. 유효한 값은 `svr` 및 `wks`입니다. 서버 빌드는 가비지 컬렉션에 대해 여러 프로세서를 활용 하도록 최적화 되며 워크스테이션 빌드는 단일 프로세서 컴퓨터에서 실행 되는 클라이언트 응용 프로그램에 최적화 되어 있습니다.  
  
 가 `pwszBuildFlavor` null로 설정 된 경우 워크스테이션 빌드가 로드 됩니다. 단일 프로세서 컴퓨터에서 실행 되는 경우가로 `pwszBuildFlavor` `svr`설정 된 경우에도 워크스테이션 빌드가 항상 로드 됩니다. 그러나가로 `pwszBuildFlavor` `svr` 설정 되 고 동시 가비지 수집이 지정 된 경우 ( `startupFlags` 매개 변수에 대 한 설명 참조) 서버 빌드가 로드 됩니다.  
  
 `startupFlags`  
 진행 [STARTUP_FLAGS](../../../../docs/framework/unmanaged-api/hosting/startup-flags-enumeration.md) 열거형 값의 조합입니다. 이러한 플래그는 동시 가비지 컬렉션, 도메인 중립 코드 및 `pwszVersion` 매개 변수의 동작을 제어 합니다. 플래그가 설정 되지 않은 경우 기본값은 단일 도메인입니다. 유효한 값은 다음과 같습니다.  
  
- `STARTUP_CONCURRENT_GC`  
  
- `STARTUP_LOADER_OPTIMIZATION_SINGLE_DOMAIN`  
  
- `STARTUP_LOADER_OPTIMIZATION_MULTI_DOMAIN`  
  
- `STARTUP_LOADER_OPTIMIZATION_MULTI_DOMAIN_HOST`  
  
- `STARTUP_LOADER_SAFEMODE`  
  
- `STARTUP_LEGACY_IMPERSONATION`  
  
- `STARTUP_LOADER_SETPREFERENCE`  
  
- `STARTUP_SERVER_GC`  
  
- `STARTUP_HOARD_GC_VM`  
  
- `STARTUP_SINGLE_VERSION_HOSTING_INTERFACE`  
  
- `STARTUP_LEGACY_IMPERSONATION`  
  
- `STARTUP_DISABLE_COMMITTHREADSTACK`  
  
- `STARTUP_ALWAYSFLOW_IMPERSONATION`  
  
 이러한 플래그에 대 한 설명은 [STARTUP_FLAGS](../../../../docs/framework/unmanaged-api/hosting/startup-flags-enumeration.md) 열거를 참조 하세요.  
  
 `rclsid`  
 진행 [ICorRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md) 또는 [ICLRRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/iclrruntimehost-interface.md) 인터페이스를 구현 하는 coclass 의 `CLSID`입니다. 지원 되는 값은 CLSID_CorRuntimeHost 또는 CLSID_CLRRuntimeHost입니다.  
  
 `riid`  
 진행 `IID` 에서`rclsid`요청 된 인터페이스의입니다. 지원 되는 값은 IID_ICorRuntimeHost 또는 IID_ICLRRuntimeHost입니다.  
  
 `ppv`  
 제한이 에 `riid`대해 반환 된 인터페이스 포인터입니다.  
  
## <a name="remarks"></a>설명  
 가 `pwszVersion` 존재 하지 않는 런타임 버전을 지정 하는 `CorBindToRuntimeEx` 경우 CLR_E_SHIM_RUNTIMELOAD의 HRESULT 값을 반환 합니다.  
  
## <a name="execution-context-and-flow-of-windows-identity"></a>Windows Id의 실행 컨텍스트 및 흐름  
 CLR 버전 1에서 개체는 <xref:System.Security.Principal.WindowsIdentity> 새 스레드, 스레드 풀 또는 타이머 콜백과 같은 비동기 요소를 통해 전달 되지 않습니다. CLR 버전 2.0에서 개체는 <xref:System.Threading.ExecutionContext> 현재 실행 중인 스레드에 대 한 일부 정보를 래핑하고 응용 프로그램 도메인 경계를 넘어 전달 합니다. 마찬가지로, <xref:System.Security.Principal.WindowsIdentity> 개체도 모든 비동기 지점에서 흐릅니다. 따라서 스레드의 현재 가장 (있는 경우)는 흐름이 너무 많습니다.  
  
 흐름은 다음 두 가지 방법으로 변경할 수 있습니다.  
  
1. 스레드 단위로 흐름 <xref:System.Threading.ExecutionContext> 을 표시 하지 않도록 설정 수정 ( <xref:System.Threading.ExecutionContext.SuppressFlow%2A>, <xref:System.Security.SecurityContext.SuppressFlow%2A>및 <xref:System.Security.SecurityContext.SuppressFlowWindowsIdentity%2A> 메서드 참조)  
  
2. 프로세스 기본 모드를 버전 1 호환성 모드로 <xref:System.Security.Principal.WindowsIdentity> 변경 하 여 현재 스레드의 <xref:System.Threading.ExecutionContext> 설정에 관계 없이 개체가 비동기 지점에서 이동 하지 않습니다. 기본 모드를 변경 하는 방법은 관리 되는 실행 파일 또는 관리 되지 않는 호스팅 인터페이스를 사용 하 여 CLR을 로드 하는지 여부에 따라 달라 집니다.  
  
    1. 관리 되는 실행 파일의 경우 `enabled` [ \<legacyImpersonationPolicy >](../../../../docs/framework/configure-apps/file-schema/runtime/legacyimpersonationpolicy-element.md) 요소의 특성을로 `true`설정 해야 합니다.  
  
    2. 관리 되지 않는 호스팅 인터페이스의 경우 `STARTUP_LEGACY_IMPERSONATION` `CorBindToRuntimeEx` 함수를 호출할 `startupFlags` 때 매개 변수에서 플래그를 설정 합니다.  
  
     버전 1 호환성 모드는 전체 프로세스와 프로세스의 모든 응용 프로그램 도메인에 적용 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리** MSCorEE.dll  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [CorBindToCurrentRuntime 함수](../../../../docs/framework/unmanaged-api/hosting/corbindtocurrentruntime-function.md)
- [CorBindToRuntime 함수](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntime-function.md)
- [CorBindToRuntimeByCfg 함수](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md)
- [CorBindToRuntimeHost 함수](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimehost-function.md)
- [ICorRuntimeHost 인터페이스](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md)
- [사용되지 않는 CLR 호스팅 함수](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
