---
title: EMemoryAvailable 열거형
ms.date: 03/30/2017
api_name:
- EMemoryAvailable
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EMemoryAvailable
helpviewer_keywords:
- EMemoryAvailable enumeration [.NET Framework hosting]
ms.assetid: 38e72a06-dbed-473b-a59b-7e0b3ea4f2af
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 76fc5f578e6da731ffd6406344d00cda8b57f493
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67772402"
---
# <a name="ememoryavailable-enumeration"></a>EMemoryAvailable 열거형
컴퓨터의 사용 가능한 실제 메모리의 크기를 나타내는 값을 포함 합니다. 이러한 값을 이벤트에 메모리에서 반환 하는 상위 및 하위 논리적으로 매핑할는 `CreateMemoryResourceNotification` Windows api에서 함수입니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum {  
    eMemoryAvailableLow     = 1,  
    eMemoryAvailableNeutral = 2,  
    eMemoryAvailableHigh    = 3   
} EMemoryAvailable;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`eMemoryAvailableHigh`|다양 한 실제 메모리를 사용할 수 있습니다.|  
|`eMemoryAvailableLow`|매우 작은 실제 메모리를 사용할 수 있습니다.|  
|`eMemoryAvailableNeutral`|사용 가능한 실제 메모리를 보통 수준입니다.|  
  
## <a name="remarks"></a>설명  
 에 대 한 호출을 사용 하는 CLR (공용 언어 런타임)에서 호스트에서이 값은 전달 된 [iclrmemorynotificationcallback:: Onmemorynotification](../../../../docs/framework/unmanaged-api/hosting/iclrmemorynotificationcallback-onmemorynotification-method.md) 메서드.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [호스팅 열거형](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
