---
title: EPolicyAction 열거형
ms.date: 03/30/2017
api_name:
- EPolicyAction
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EPolicyAction
helpviewer_keywords:
- EPolicyAction enumeration [.NET Framework hosting]
ms.assetid: 72dd76ba-239e-45ac-9ded-318fb07d6c6d
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 404cd5513a1cbd353faed41030a80ec2abef235f
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67774203"
---
# <a name="epolicyaction-enumeration"></a>EPolicyAction 열거형
호스트에서 설명 하는 작업에 대해 설정할 정책 작업을 설명 [EClrOperation](../../../../docs/framework/unmanaged-api/hosting/eclroperation-enumeration.md) 에 정의 된 오류 [EClrFailure](../../../../docs/framework/unmanaged-api/hosting/eclrfailure-enumeration.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum {  
    eNoAction,  
    eThrowException,  
    eAbortThread,  
    eRudeAbortThread,  
    eUnloadAppDomain,  
    eRudeUnloadAppDomain,  
    eExitProcess,  
    eFastExitProcess,  
    eRudeExitProcess,  
    eDisableRuntime  
} EPolicyAction;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`eAbortThread`|CLR (공용 언어 런타임) 스레드를 정상적으로 중단 하도록 지정 합니다. 모든 실행 하려는 시도 포함 하는 정상적인 중단 `finally` 차단 된 `catch` 스레드 중단 및 종료자와 관련 된 블록입니다.|  
|`eDisableRuntime`|CLR 사용 안 함된 상태를 시작 해야를 지정 합니다. 더 이상 영향을 받는 프로세스에서 관리 되는 코드를 실행할 수 있습니다 하 고 clr에서 스레드가 차단 됩니다.|  
|`eExitProcess`|CLR 종료자 실행 등 정리 및 로깅 작업을 수행 하는 프로세스의 정상 종료 하면을 지정 합니다.|  
|`eFastExitProcess`|CLR 프로세스를 종료 하도록 즉시 종료자를 실행 하거나 정리 및 로깅 작업을 수행 하지 않고 지정 합니다. 그러나 디버거에 알림이 전송 됩니다.|  
|`eNoAction`|조치가 취해야 합니다를 지정 합니다.|  
|`eRudeAbortThread`|CLR 강제 스레드 중단을 수행 해야 한다고 지정 합니다. 경우에 `catch` 하 고 `finally` 블록으로 표시 된 <xref:System.EnterpriseServices.MustRunInClientContextAttribute> 실행 됩니다.|  
|`eRudeExitProcess`|CLR 종료자를 실행 하거나 작업을 기록 하지 않고 프로세스를 종료 하도록 지정 합니다.|  
|`eRudeUnloadAppDomain`|CLR의 잘못 된 언로드를 수행 하도록 지정 된 <xref:System.AppDomain>합니다. 로 표시만 종료자 <xref:System.EnterpriseServices.MustRunInClientContextAttribute> 실행 됩니다. 마찬가지로, 모든 스레드가이 사용 하 여 <xref:System.AppDomain> 해당 스택 수신를 `ThreadAbortException`, 하지만 경우에 `catch` 하 고 `finally` 블록으로 표시 <xref:System.EnterpriseServices.MustRunInClientContextAttribute> 실행 됩니다.|  
|`eThrowException`|메모리, 버퍼 오버플로 등과 같은 조건에 적합 한 예외를 throw 해야를 지정 합니다.|  
|`eUnloadAppDomain`|지정 된 <xref:System.AppDomain> 로드 해야 합니다. CLR은 종료자를 실행 하려고 시도 합니다.|  
  
## <a name="remarks"></a>설명  
 호스트의 메서드를 호출 하 여 정책을 실행 하도록 설정 하는 [ICLRPolicyManager](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-interface.md) 인터페이스입니다. 강제 하 고 정상적으로 중단에 대 한 내용은 참조는 [EClrOperation](../../../../docs/framework/unmanaged-api/hosting/eclroperation-enumeration.md) 열거형입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [EClrFailure 열거형](../../../../docs/framework/unmanaged-api/hosting/eclrfailure-enumeration.md)
- [ICLRPolicyManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-interface.md)
- [IHostPolicyManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostpolicymanager-interface.md)
- [호스팅 열거형](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
