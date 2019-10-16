---
title: ASSEMBLY_INFO 구조체
ms.date: 03/30/2017
api_name:
- ASSEMBLY_INFO
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- ASSEMBLY_INFO
helpviewer_keywords:
- ASSEMBLY_INFO structure [.NET Framework fusion]
ms.assetid: b3cbb47c-457f-4083-8895-49562ca99ab8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 390ab4881396bbc01337d087f05b6066153bfed1
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795493"
---
# <a name="assembly_info-structure"></a>ASSEMBLY_INFO 구조체
전역 어셈블리 캐시에 등록 된 어셈블리에 대 한 정보를 포함 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef struct _ASSEMBLY_INFO {  
    ULONG           cbAssemblyInfo;  
    DWORD           dwAssemblyFlags;  
    ULARGE_INTEGER  uliAssemblySizeInKB;  
    LPWSTR          pszCurrentAssemblyPathBuf;  
    ULONG           cchBuf;  
} ASSEMBLY_INFO;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|설명|  
|------------|-----------------|  
|`cbAssemblyInfo`|구조체의 크기 (바이트)입니다. 이 필드는 나중에 확장할 수 있도록 예약 되어 있습니다.|  
|`dwAssemblyFlags`|어셈블리에 대 한 설치 세부 정보를 나타내는 플래그입니다. 다음 값이 지원 됩니다.<br /><br /> -어셈블리가 설치 되었음을 나타내는 ASSEMBLYINFO_FLAG_INSTALLED 값입니다. .NET Framework의 현재 버전은 항상이 값 `dwAssemblyFlags` 으로 설정 됩니다.<br />-어셈블리가 페이로드가 있음을 나타내는 ASSEMBLYINFO_FLAG_PAYLOADRESIDENT 값입니다. .NET Framework의 현재 버전은이 값으로 `dwAssemblyFlags` 설정 되지 않습니다.|  
|`uliAssemblySizeInKB`|어셈블리에 포함 된 파일의 총 크기 (kb)입니다.|  
|`pszCurrentAssemblyPathBuf`|매니페스트 파일의 현재 경로를 포함 하는 문자열 버퍼에 대 한 포인터입니다. 경로는 null 문자로 끝나야 합니다.|  
|`cchBuf`|을 포함 하는 null 종결자를 포함 하 `pszCurrentAssemblyPathBuf` 는 와이드 문자 수입니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Fusion. h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [Fusion 구조체](fusion-structures.md)
- [전역 어셈블리 캐시](../../app-domains/gac.md)
