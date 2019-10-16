---
title: EClrFailure 열거형
ms.date: 03/30/2017
api_name:
- EClrFailure
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EClrFailure
helpviewer_keywords:
- EClrFailure enumeration [.NET Framework hosting]
ms.assetid: 37b95cce-9bfb-4ecf-a00b-33dcba782c67
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5f3e39d94996f14f1ae6593b9adaa5db3ef674c5
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67769657"
---
# <a name="eclrfailure-enumeration"></a>EClrFailure 열거형
호스트 정책 작업 설정할 수 있는 오류를 설명 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum {  
    FAIL_NonCriticalResource,  
    FAIL_CriticalResource,  
    FAIL_FatalRuntime,  
    FAIL_OrphanedLock  
    FAIL_StackOverflow  
    FAIL_AccessViolation  
    FAIL_CodeContract  
} EClrFailure;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|설명|  
|------------|-----------------|  
|`FAIL_NonCriticalResource`|중요 하지 않은 코드 영역 (예: 스레드, 메모리, 블록 또는 잠금을) 리소스를 할당 하는 동안 오류가 발생 했습니다.|  
|`FAIL_CriticalResource`|코드의 중요 영역 (예: 스레드, 메모리, 블록 또는 잠금을) 리소스를 할당 하는 동안 오류가 발생 했습니다.|  
|`FAIL_FatalRuntime`|CLR (공용 언어 런타임)이 더 이상 프로세스에서 관리 되는 코드를 실행 수 없습니다. 예측이 모든 호스팅 함수를 호출 하는 HOST_E_CLRNOTAVAILABLE의 HRESULT 값을 반환합니다.|  
|`FAIL_OrphanedLock`|반환 시 잠금 해제 하지 못했습니다 스레드는 <xref:System.AppDomain> 개체입니다. 호스트에는이 오류는 스레드가 중단 되도록를 설정할 수 없습니다.|  
|`FAIL_StackOverflow`|스택 오버플로가 발생 했습니다.|  
|`FAIL_AccessViolation`|보호 된 메모리를 쓰거나 읽을 하려고 했습니다. .NET Framework 4에서 지원 되지 않습니다.|  
|`FAIL_CodeContract`|코드 계약 실패가 했습니다. 참조 [계약 코드](../../../../docs/framework/debug-trace-profile/code-contracts.md)합니다.|  
  
## <a name="remarks"></a>설명  
 참조를 [iclrpolicymanager:: Setactiononfailure](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-setactiononfailure-method.md) 메서드 목록은 [EPolicyAction](../../../../docs/framework/unmanaged-api/hosting/epolicyaction-enumeration.md) 값 호스트 사용 오류 조건에 대 한 정책 작업을 지정할 수 있습니다. 코드의 중요 한 및 중요 하지 않은 지역에 대 한 자세한 내용은 참조 [EClrOperation](../../../../docs/framework/unmanaged-api/hosting/eclroperation-enumeration.md)합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRPolicyManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-interface.md)
- [SetActionOnFailure 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-setactiononfailure-method.md)
- [IHostPolicyManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostpolicymanager-interface.md)
- [호스팅 열거형](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
