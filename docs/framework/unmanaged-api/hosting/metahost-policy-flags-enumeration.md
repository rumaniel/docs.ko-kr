---
title: METAHOST_POLICY_FLAGS 열거형
ms.date: 03/30/2017
api_name:
- METAHOST_POLICY_FLAGS
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- METAHOST_POLICY_FLAGS
helpviewer_keywords:
- METAHOST_POLICY_FLAGS enumeration [.NET Framework hosting]
ms.assetid: 3bb4b526-0118-42e2-ba59-c95648528ce9
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1d35bd5f8aaa2dc0df0044671414a5a936fed24d
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781063"
---
# <a name="metahostpolicyflags-enumeration"></a>METAHOST_POLICY_FLAGS 열거형
대부분의 런타임 호스트에 공통 되는 바인딩 정책을 제공 합니다. 이 열거형은에서 사용 된 [iclrmetahostpolicy:: Getrequestedruntime](../../../../docs/framework/unmanaged-api/hosting/iclrmetahostpolicy-getrequestedruntime-method.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum {  
    METAHOST_POLICY_HIGHCOMPAT              = 0x00,  
    METAHOST_POLICY_APPLY_UPGRADE_POLICY    = 0x08,  
    METAHOST_POLICY_EMULATE_EXE_LAUNCH      = 0x10,  
    METAHOST_POLICY_SHOW_ERROR_DIALOG       = 0x20,  
    METAHOST_POLICY_USE_PROCESS_IMAGE_PATH  = 0x40,  
    METAHOST_POLICY_ENSURE_SKU_SUPPORTED    = 0x80,  
    METAHOST_POLICY_IGNORE_ERROR_MODE       = 0x1000  
  
} METAHOST_POLICY_FLAGS;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|설명|  
|------------|-----------------|  
|`METAHOST_POLICY_HIGHCOMPAT`|현재 프로세스에 로드 되는 모든 공용 언어 런타임 (CLR)를 고려 하지 않는 높은 호환성 정책을 정의 합니다. 고려 합니다만 설치 된 Clr 및 구성 요소의 기본 자체 어셈블리 파일는 선언 된 빌드 대상 버전 또는 구성 파일에서 파생 된 합니다.|  
|`METAHOST_POLICY_APPLY_UPGRADE_POLICY`|정확히 일치 하는 없는 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft의 내용을 기반으로 하는 경우 업그레이드 정책 버전 바인딩 결과에 적용\\합니다. NETFramework\Policy\Upgrades 합니다. 것과 동일한 효과가 [RUNTIME_INFO_UPGRADE_VERSION](../../../../docs/framework/unmanaged-api/hosting/runtime-info-flags-enumeration.md)합니다.|  
|`METAHOST_POLICY_EMULATE_EXE_LAUNCH`|호출에 제공 된 이미지는 새 프로세스에서 실행 된 것 처럼 바인딩 결과가 반환 됩니다. 현재 `GetRequestedRuntime` 로드할 런타임 집합을 무시 하 고 설치 된 런타임 집합에 대해 바인딩합니다. 이 플래그는 호스트를를 시작할 때 EXE를 바인딩할 런타임을 확인할 수 있습니다.|  
|`METAHOST_POLICY_SHOW_ERROR_DIALOG`|경우에 오류 대화 상자가 표시 됩니다 `GetRequestedRuntime` 입력된 매개 변수를 사용 하 여 호환 되는 런타임을 찾을 수 없습니다. 이 오류 대화 상자는.NET Framework 4.5부터, 사용자는 적절 한 기능을 사용 하도록 설정 하는지 여부를 묻는 Windows 기능 대화 상자 형식의 걸릴 수 있습니다.|  
|`METAHOST_POLICY_USE_PROCESS_IMAGE_PATH`|`GetRequestedRuntime` 바인딩 프로세스에 대 한 추가 입력으로 프로세스 이미지 (및 모든 해당 구성 파일)를 사용합니다. 기본적으로 `GetRequestedRuntime` 프로세스 이미지 경로 (일반적으로 프로세스를 시작 하는 데 사용 된 EXE)으로 대체 되지 않습니다 바인딩할 런타임에 결정 합니다.|  
|`METAHOST_POLICY_ENSURE_SKU_SUPPORTED`|`GetRequestedRuntime` 구성 파일에 정보가 없는 경우 해당 SKU에 설치 되어 있는지 확인 해야 합니다. 이 구성 파일을.NET Framework의 기본 설치 보다 작은 Sku에서 정상적으로 실패 하지 않은 응용 프로그램이 있습니다. 기본적으로 `GetRequestedRuntime` 구성 파일에서 SKU 특성을 지정 하지 않으면 해당 SKU에 설치 되어 있는지 확인 하지 않습니다 `<supportedRuntime />` 요소입니다.|  
|`METAHOST_POLICY_IGNORE_ERROR_MODE`|`GetRequestedRuntime` SEM_FAILCRITICALERRORS를 무시 해야 (호출 하 여 설정 됩니다는 [SetErrorMode](https://go.microsoft.com/fwlink/p/?LinkId=255242) 함수), 오류 대화 상자를 표시 합니다. 기본적으로 SEM_FAILCRITICALERRORS를 오류 대화 상자를 표시 하지 않습니다. 다른 프로세스에서 상속 된 된 및 자동 오류 시나리오에서 적합할 수 있습니다.|  
  
## <a name="remarks"></a>설명  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Metahost.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [호스팅 열거형](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
- [GetRequestedRuntime 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrmetahostpolicy-getrequestedruntime-method.md)
