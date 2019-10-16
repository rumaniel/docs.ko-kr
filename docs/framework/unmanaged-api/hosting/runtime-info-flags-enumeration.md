---
title: RUNTIME_INFO_FLAGS 열거형
ms.date: 03/30/2017
api_name:
- RUNTIME_INFO_FLAGS
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- RUNTIME_INFO_FLAGS
helpviewer_keywords:
- RUNTIME_INFO_FLAGS enumeration [.NET Framework hosting]
ms.assetid: adba37be-f775-4cdb-8919-5746ce694f33
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4bf3a0507f9f7d4d622163a55fc9c45b4a4dd0a6
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781155"
---
# <a name="runtimeinfoflags-enumeration"></a>RUNTIME_INFO_FLAGS 열거형
CLR (공용 언어 런타임)에 대 한 정보를 반환할지 여부를 나타내는 값을 포함 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum {  
  
    RUNTIME_INFO_UPGRADE_VERSION             = 0x01,  
    RUNTIME_INFO_REQUEST_IA64                = 0x02,  
    RUNTIME_INFO_REQUEST_AMD64               = 0x04,  
    RUNTIME_INFO_REQUEST_X86                 = 0x08,  
    RUNTIME_INFO_DONT_RETURN_DIRECTORY       = 0x10,  
    RUNTIME_INFO_DONT_RETURN_VERSION         = 0x20,  
    RUNTIME_INFO_DONT_SHOW_ERROR_DIALOG      = 0x40,  
    RUNTIME_INFO_IGNORE_ERROR_MODE           = 0x1000  
  
} RUNTIME_INFO_FLAGS;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`RUNTIME_INFO_DONT_RETURN_DIRECTORY`|디렉터리 정보를 포함 하지 해야 함을 나타냅니다.|  
|`RUNTIME_INFO_DONT_RETURN_VERSION`|버전 정보를 포함 하지 해야 함을 나타냅니다.|  
|`RUNTIME_INFO_DONT_SHOW_ERROR_DIALOG`|실패 시 오류 대화 상자를 표시 되지 않음을 나타냅니다.|  
|`RUNTIME_INFO_IGNORE_ERROR_MODE`|나타내는 호출의 결과 [SetErrorMode](https://go.microsoft.com/fwlink/p/?LinkId=255242) SEM_FAILCRITICALERRORS 플래그를 사용 하 여 함수를 재정의 해야 합니다. 즉, 설치 대화 상자를 표시 되는 대신 실패 하면 표시 됩니다.|  
|`RUNTIME_INFO_REQUEST_AMD64`|런타임의 AMD-64-호환 되는 버전 정보에 대 한 요청을 나타냅니다.|  
|`RUNTIME_INFO_REQUEST_IA64`|런타임의 IA-64-호환 되는 버전 정보에 대 한 요청을 나타냅니다.|  
|`RUNTIME_INFO_REQUEST_X86`|런타임의 x86 호환 버전 정보에 대 한 요청을 나타냅니다.|  
|`RUNTIME_INFO_UPGRADE_VERSION`|버전 업그레이드 정보 포함 되어야 함을 나타냅니다.|  
  
## <a name="remarks"></a>설명  
 다음 플랫폼 아키텍처 플래그를 한 번에 하나만 지정된 될 수 있습니다 및 함께 사용할 수 없습니다.  
  
- RUNTIME_INFO_REQUEST_IA64  
  
- RUNTIME_INFO_REQUEST_AMD64  
  
- RUNTIME_INFO_REQUEST_X86  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [호스팅 열거형](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)
