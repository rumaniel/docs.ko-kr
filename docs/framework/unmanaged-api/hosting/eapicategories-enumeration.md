---
title: EApiCategories 열거형
ms.date: 03/30/2017
api_name:
- EApiCategories
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EApiCategories
helpviewer_keywords:
- EApiCategories enumeration [.NET Framework hosting]
ms.assetid: 3c4a8a5a-8a46-4ac9-947f-4959bc9d6ac6
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 41513d9b6f98743bfad95e4d9606cfb4927369e6
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67769784"
---
# <a name="eapicategories-enumeration"></a>EApiCategories 열거형
부분적으로 신뢰할 수 있는 코드에서 실행 되는 호스트를 차단할 수 있는 기능의 범주를 설명 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum {  
    eNoCategory               = 0,  
    eSynchronization          = 0x1,  
    eSharedState              = 0x2,  
    eExternalProcessMgmt      = 0x4,  
    eSelfAffectingProcessMgmt = 0x8,  
    eExternalThreading        = 0x10,  
    eSelfAffectingThreading   = 0x20,  
    eSecurityInfrastructure   = 0x40,  
    eUI                       = 0x80,  
    eMayLeakOnAbort           = 0x100,  
    eAll                      = 0x1ff  
} EHostProtectionCategories;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`eAll`|관리 되는 모든 클래스 및 기타 적용 되는 멤버 지정 `EApiCategories` 필드에서 부분적으로 신뢰할 수 있는 코드 실행에서 차단 합니다.|  
|`eExternalProcessMgmt`|관리 되는 클래스 및 멤버를 생성, 조작 및 외부 프로세스의 소멸을 사용 하면 부분적으로 신뢰할 수 있는 코드에서 실행 차단 수를 지정 합니다.|  
|`eExternalThreading`|관리 되는 클래스 및 멤버를 생성, 조작 및 외부 스레드 소멸을 사용 하면 부분적으로 신뢰할 수 있는 코드에서 실행 차단 수를 지정 합니다.|  
|`eMayLeakOnAbort`|부분적으로 신뢰할 수 있는 코드에서 실행 중단 시 메모리 누수가 발생할 수 있는 관리 되는 형식 및 멤버는 차단 수를 지정 합니다.|  
|`eNoCategory`|관리 코드 범주가 수 부분적으로 신뢰할 수 있는 코드에서 실행 되는 지정 합니다.|  
|`eSecurityInfrastructure`|공용 언어 런타임 (CLR) 보안 인프라에서 부분적으로 신뢰할 수 있는 코드에서 사용 하 고 차단를 지정 합니다.|  
|`eSelfAffectingProcessMgmt`|관리 되는 클래스 및 멤버 호스팅된 프로세스 영향을 줄 수 있는 기능이 부분적으로 신뢰할 수 있는 코드에서 실행 차단 수를 지정 합니다.|  
|`eSelfAffectingThreading`|관리 되는 클래스 및 멤버 호스트 프로세스의 스레드 영향을 줄 수 있는 기능이 부분적으로 신뢰할 수 있는 코드에서 실행 차단 수를 지정 합니다.|  
|`eSharedState`|공유 상태를 노출 하는 관리 되는 클래스와 멤버 부분적으로 신뢰할 수 있는 코드에서 실행 차단 수를 지정 합니다.|  
|`eSynchronization`|공용 언어 런타임 클래스 및 멤버를 잠금을 유지 하기 위해 사용자 코드를 사용 하면 부분적으로 신뢰할 수 있는 코드에서 실행 차단 수를 지정 합니다.|  
|`eUI`|관리 되는 클래스 및 멤버 허용 하거나 사용자 상호 작용을 필요로 하는 부분적으로 신뢰할 수 있는 코드에서 실행 차단 수를 지정 합니다.|  
  
## <a name="remarks"></a>설명  
 합니다 [iclrhostprotectionmanager:: Setprotectedcategories](../../../../docs/framework/unmanaged-api/hosting/iclrhostprotectionmanager-setprotectedcategories-method.md) 형식의 매개 변수를 사용 하는 메서드 `EApiCategories`합니다.  
  
 `EApiCategories` 열거형 및 `SetProtectedCategories` 메서드 직접적으로 관련 된 관리 되는 <xref:System.Security.Permissions.HostProtectionAttribute?displayProperty=nameWithType> 클래스. 관리 되는 클래스를 사용 합니다 <xref:System.Security.Permissions.HostProtectionResource?displayProperty=nameWithType> 열거형 값에 직접적으로 해당 합니다 `EApiCategories` 에 설명 된 범주에 해당 하는 기능을 제공 하는 관리 되는 형식 및 멤버를 표시 하려면 값을 `EApiCategories`입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRHostProtectionManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrhostprotectionmanager-interface.md)
- [호스팅 열거형](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
