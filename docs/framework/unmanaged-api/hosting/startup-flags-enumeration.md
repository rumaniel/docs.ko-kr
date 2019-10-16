---
title: STARTUP_FLAGS 열거형
ms.date: 03/30/2017
api_name:
- STARTUP_FLAGS
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- STARTUP_FLAGS
helpviewer_keywords:
- STARTUP_FLAGS enumeration [.NET Framework hosting]
ms.assetid: 4f043594-0c45-4bc6-988e-a6793f0d8d06
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f39608b39be7d5c25b916fb20877aa73d6e5a8bc
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916227"
---
# <a name="startup_flags-enumeration"></a>STARTUP_FLAGS 열거형
CLR (공용 언어 런타임)의 시작 동작을 나타내는 값을 포함 합니다. 기본적으로 가비지 수집은 비 동시 이며 기본 클래스 라이브러리만 도메인 중립적 영역에 로드 됩니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum {  
    STARTUP_CONCURRENT_GC                         = 0x1,  
    STARTUP_LOADER_OPTIMIZATION_MASK              = 0x3<<1,  
    STARTUP_LOADER_OPTIMIZATION_SINGLE_DOMAIN     = 0x1<<1,  
    STARTUP_LOADER_OPTIMIZATION_MULTI_DOMAIN      = 0x2<<1,  
    STARTUP_LOADER_OPTIMIZATION_MULTI_DOMAIN_HOST = 0x3<<1,  
  
    STARTUP_LOADER_SAFEMODE                       = 0x10,  
    STARTUP_LOADER_SETPREFERENCE                  = 0x100,  
  
    STARTUP_SERVER_GC                             = 0x1000,  
    STARTUP_HOARD_GC_VM                           = 0x2000,  
  
    STARTUP_SINGLE_VERSION_HOSTING_INTERFACE      = 0x4000,  
    STARTUP_LEGACY_IMPERSONATION                  = 0x10000,  
    STARTUP_DISABLE_COMMITTHREADSTACK             = 0x20000,  
    STARTUP_ALWAYSFLOW_IMPERSONATION              = 0x40000,  
    STARTUP_TRIM_GC_COMMIT                        = 0x80000,  
  
    STARTUP_ETW                                   = 0x100000,  
    STARTUP_ARM                                   = 0x400000  
} STARTUP_FLAGS;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`STARTUP_CONCURRENT_GC`|동시 가비지 수집을 사용 하도록 지정 합니다. 호출자가 단일 프로세서 컴퓨터에서 서버 빌드 및 동시 가비지 수집을 요청 하면 워크스테이션 빌드 및 비 동시 가비지 수집이 대신 실행 됩니다. **참고:**  Intel Itanium 아키텍처 (이전의 IA-64)를 구현 하는 64 비트 시스템에서 WOW64 x86 에뮬레이터를 실행 하는 응용 프로그램에서는 동시 가비지 수집이 지원 되지 않습니다. 64 비트 Windows 시스템에서 WOW64를 사용 하는 방법에 대 한 자세한 내용은 [32 비트 응용 프로그램 실행](/windows/desktop/WinProg64/running-32-bit-applications)을 참조 하세요.|  
|`STARTUP_LOADER_OPTIMIZATION_MASK`|로더 최적화를 수행 하도록 지정 합니다.|  
|`STARTUP_LOADER_OPTIMIZATION_SINGLE_DOMAIN`|어셈블리를 도메인 중립적으로 로드 하지 않도록 지정 합니다.|  
|`STARTUP_LOADER_OPTIMIZATION_MULTI_DOMAIN`|모든 어셈블리를 도메인 중립적으로 로드 하도록 지정 합니다.|  
|`STARTUP_LOADER_OPTIMIZATION_MULTI_DOMAIN_HOST`|모든 강력한 이름의 어셈블리를 도메인 중립적으로 로드 하도록 지정 합니다.|  
|`STARTUP_LOADER_SAFEMODE`|전달 된 버전에 CLR 버전 정책이 적용 되지 않도록 지정 합니다. CLR에 지정 된 정확한 버전이 로드 됩니다. Shim은 정책을 평가 하 여 호환 되는 최신 버전을 확인 하지 않습니다.|  
|`STARTUP_LOADER_SETPREFERENCE`|기본 런타임을 설정 하지만 실제로 시작 하지 않도록 지정 합니다.|  
|`STARTUP_SERVER_GC`|서버 가비지 수집을 사용 하도록 지정 합니다.|  
|`STARTUP_HOARD_GC_VM`|가비지 수집에서 사용 되는 가상 주소를 유지 하도록 지정 합니다.|  
|`STARTUP_SINGLE_VERSION_HOSTING_INTERFACE`|호스팅 인터페이스를 혼합 하 여 사용할 수 없도록 지정 합니다.|  
|`STARTUP_LEGACY_IMPERSONATION`|기본적으로 가장이 비동기 요소 간에 이동 하지 않도록 지정 합니다.|  
|`STARTUP_DISABLE_COMMITTHREADSTACK`|스레드의 실행이 시작 될 때 전체 스레드 스택을 커밋하지 않도록 지정 합니다.|  
|`STARTUP_ALWAYSFLOW_IMPERSONATION`|플랫폼 호출을 통해 달성 된 관리 되는 가장 및 가장가 비동기 요소를 통해 전달 되도록 지정 합니다. 기본적으로 관리 되는 가장는 비동기 요소를 통해 전달 됩니다.|  
|`STARTUP_TRIM_GC_COMMIT`|시스템 메모리가 부족할 때 가비지 수집에서 커밋된 공간을 적게 사용 하도록 지정 합니다. `gcTrimCommitOnLowMemory` [공유 웹 호스팅을 위한 최적화](../../../standard/garbage-collection/optimization-for-shared-web-hosting.md)에서을 참조 하세요.|  
|`STARTUP_ETW`|공용 언어 런타임 이벤트에 대해 ETW (Windows 용 이벤트 추적)를 사용 하도록 지정 합니다. Windows Vista 부터는 이벤트 추적이 항상 사용 되도록 설정 되므로이 플래그는 영향을 주지 않습니다. [.NET Framework 로깅 제어](../../../../docs/framework/performance/controlling-logging.md)를 참조 하세요.|  
|`STARTUP_ARM`|응용 프로그램 도메인 리소스 모니터링을 사용 하도록 지정 합니다. Property 및 <xref:System.AppDomain.MonitoringIsEnabled%2A?displayProperty=nameWithType> [ appDomainResourceMonitoring>요소를참조하세요.\<](../../../../docs/framework/configure-apps/file-schema/runtime/appdomainresourcemonitoring-element.md)|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리** MSCorEE.dll  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [호스팅 열거형](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
