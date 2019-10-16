---
title: ASM_CACHE_FLAGS 열거형
ms.date: 03/30/2017
api_name:
- ASM_CACHE_FLAGS
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- ASM_CACHE_FLAGS
helpviewer_keywords:
- ASM_CACHE_FLAGS enumeration [.NET Framework fusion]
ms.assetid: 82e9a7da-321b-48b8-b239-52eaffda6be8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0e3e9da3db71d3e24b2a60ff032a631680055b88
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795279"
---
# <a name="asm_cache_flags-enumeration"></a>ASM_CACHE_FLAGS 열거형
전역 어셈블리 캐시에서 [Iassemblycacheitem](iassemblycacheitem-interface.md) 이 나타내는 어셈블리의 원본을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum {  
    ASM_CACHE_ZAP       = 0x01,  
    ASM_CACHE_GAC       = 0x02,  
    ASM_CACHE_DOWNLOAD  = 0x04,  
    ASM_CACHE_ROOT      = 0x08,  
    ASM_CACHE_ROOT_EX   = 0x80  
} ASM_CACHE_FLAGS;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`ASM_CACHE_ZAP`|Ngen.exe를 사용 하 여 미리 컴파일된 어셈블리의 캐시를 열거 합니다.|  
|`ASM_CACHE_GAC`|전역 어셈블리 캐시를 열거 합니다.|  
|`ASM_CACHE_DOWNLOAD`|요청 시 다운로드 되었거나 섀도 복사 된 어셈블리를 열거 합니다.|  
|`ASM_CACHE_ROOT`|[Getcachepath](getcachepath-function.md) 함수가 CLR (공용 언어 런타임) 버전 2.0에 대 한 전역 어셈블리 캐시에 대 한 경로를 반환 해야 함을 나타냅니다. [Getcachepath](getcachepath-function.md)호출의 컨텍스트에서만 의미가 있습니다.|  
|`ASM_CACHE_ROOT_EX`|[Getcachepath](getcachepath-function.md) 함수가 CLR 버전 4에 대 한 전역 어셈블리 캐시에 대 한 경로를 반환 해야 함을 나타냅니다. [Getcachepath](getcachepath-function.md)호출의 컨텍스트에서만 의미가 있습니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Fusion. h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [GetCachePath 함수](getcachepath-function.md)
- [IAssemblyCacheItem 인터페이스](iassemblycacheitem-interface.md)
- [Fusion 열거형](fusion-enumerations.md)
