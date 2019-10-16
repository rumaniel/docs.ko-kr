---
title: EClrOperation 열거형
ms.date: 03/30/2017
api_name:
- EClrOperation
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EClrOperation
helpviewer_keywords:
- EClrOperation enumeration [.NET Framework hosting]
ms.assetid: 5aef6808-5aac-4b2f-a2c7-fee1575c55ed
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 01b000ed3d75ddb6a7882cb8f03ff2cec64fb9fe
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67767882"
---
# <a name="eclroperation-enumeration"></a>EClrOperation 열거형
호스트 정책 작업을 적용할 수 있는 작업 집합을 설명 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum {  
    OPR_ThreadAbort,  
    OPR_ThreadRudeAbortInNonCriticalRegion,  
    OPR_ThreadRudeAbortInCriticalRegion,  
    OPR_AppDomainUnload,  
    OPR_AppDomainRudeUnload,  
    OPR_ProcessExit,  
    OPR_FinalizerRun  
} EClrOperation;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`OPR_AppDomainRudeUnload`|호스트 정책 작업을 수행할 때 지정할 수는 <xref:System.AppDomain> 정상적이 지 않은 (강제) 방식으로 언로드되는 합니다.|  
|`OPR_AppDomainUnload`|호스트 정책 작업을 수행할 때 지정할 수는 <xref:System.AppDomain> 언로드됩니다.|  
|`OPR_FinalizerRun`|호스트 종료 자가 실행 시 수행 될 정책 작업을 지정할 수 있습니다.|  
|`OPR_ProcessExit`|호스트는 프로세스가 종료 시 수행 될 정책 작업을 지정할 수 있습니다.|  
|`OPR_ThreadAbort`|호스트 정책 스레드가 중단 될 때 수행할 작업을 지정할 수 있습니다.|  
|`OPR_ThreadRudeAbortInCriticalRegion`|호스트 정책 코드의 중요 영역에서 강제 스레드 중단이 발생할 경우 수행할 작업을 지정할 수 있습니다.|  
|`OPR_ThreadRudeAbortInNonCriticalRegion`|호스트 코드는 중요 하지 않은 영역에서 강제 스레드 중단이 발생할 경우 되려면 정책 작업을 지정할 수 있습니다.|  
  
## <a name="remarks"></a>설명  
 공용 언어 런타임 (CLR) 안정성 인프라 중단 되 고 리소스 간에 코드 및 코드의 중요 하지 않은 지역에서 발생 하는 중요 한 영역에서 발생 하는 할당 오류를 구분 합니다. 이 차이 호스트 코드에서 오류가 발생 하는 위치에 따라 다양 한 정책을 설정할 수 있도록 설계 되었습니다.  
  
 A *중요 한 코드 영역* CLR에서 해당 작업을 중단 또는 리소스에는 현재 태스크에만 영향이 대 한 요청을 완료 하지 못함을 줄 수 없는 공간이 있습니다. 예를 들어 작업 잠금을 보유 하는 메모리 할당 요청 시 오류를 나타내는 hresult가 하는 경우 충분 하지 않기 위해 해당 작업의 안정성을 중단 합니다 <xref:System.AppDomain>이므로 <xref:System.AppDomain> 다른 포함 될 수 있습니다 동일한 잠금을 대기 하는 태스크입니다. 중단할 현재 작업 응답을 중지 하도록 다른 작업이 발생할 수 있습니다. 이런 경우 호스트 해야 전체를 언로드할 수 <xref:System.AppDomain> 위험 잠재적 불안정 하는 대신 합니다.  
  
 A *중요 하지 않은 코드 영역의*, 다른 한편으로 여기서 CLR 중단 또는 실패는 오류가 발생 하는 작업에만 영향이 보장할 수 영역입니다.  
  
 또한 CLR 정상적이 고 정상 되지 않은 (강제) 중단을 구분합니다. 일반적으로 정상적으로 중단 하기 위해 모든 노력 강제 중단은 이러한 보증도 하지 않습니다 하는 동안 작업을 중단 하기 전에 예외 처리 루틴 및 종료자를 실행 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [EClrFailure 열거형](../../../../docs/framework/unmanaged-api/hosting/eclrfailure-enumeration.md)
- [EPolicyAction 열거형](../../../../docs/framework/unmanaged-api/hosting/epolicyaction-enumeration.md)
- [ICLRPolicyManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-interface.md)
- [IHostPolicyManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostpolicymanager-interface.md)
- [호스팅 열거형](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
