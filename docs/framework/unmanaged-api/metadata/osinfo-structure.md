---
title: OSINFO 구조체
ms.date: 03/30/2017
api_name:
- OSINFO
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- OSINFO
helpviewer_keywords:
- OSINFO structure [.NET Framework metadata]
ms.assetid: fac7b480-7adb-4450-a5e9-690fed81ffae
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a36cd3c5fb638799a735e4b4a1a98959500300b5
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67761604"
---
# <a name="osinfo-structure"></a>OSINFO 구조체
어셈블리 또는 모듈에 대 한 운영 체제에 대 한 정보를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef struct {  
    DWORD   dwOSPlatformId;  
    DWORD   dwOSMajorVersion;   
    DWORD   dwOSMinorVersion;   
} OSINFO;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`dwOSPlatformId`|Microsoft Windows 플랫폼 함수에 의해 정의 된 식별자 값 중 하나 `GetVersionEx`합니다. 다음 값이 지원 됩니다.<br /><br /> -VER_PLATFORM_WIN32s, 또는 0x0000, Microsoft Windows 3.1을 지정할 수 있습니다.<br />-VER_PLATFORM_WIN32_WINDOWS, 또는 0x0001, Windows 95, Windows 98 또는 운영 체제에서 나온 지정할 수 있습니다.<br />-VER_PLATFORM_WIN32_NT, 또는 0x0010, Windows NT 또는 운영 체제에서 나온 지정할 수 있습니다.|  
|`dwOSMajorVersion`|운영 체제 주 버전 또는 모든 버전을 나타내는 NULL 값입니다.|  
|`dwOSMinorVersion`|운영 체제 부 버전, 또는 모든 버전을 나타내는 NULL 값입니다.|  
  
## <a name="remarks"></a>설명  
 `OSINFO` 기반으로 합니다 `OSVERSIONINFOEX` 구조체에서 사용 되는 함수 호출에 Microsoft Windows 플랫폼 `GetVersionEx`합니다. 이 구조는 ASSEMBLYMETADATA 구조체에서 해당 운영 체제 지원을 나타내는 데 사용 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 구조체](../../../../docs/framework/unmanaged-api/metadata/metadata-structures.md)
- [IMetaDataAssemblyEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-interface.md)
