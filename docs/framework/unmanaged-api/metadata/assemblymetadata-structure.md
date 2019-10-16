---
title: ASSEMBLYMETADATA 구조체
ms.date: 03/30/2017
api_name:
- ASSEMBLYMETADATA
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ASSEMBLYMETADATA
helpviewer_keywords:
- ASSEMBLYMETADATA structure [.NET Framework metadata]
ms.assetid: 1af98e57-9145-4d35-bb78-77d1da7c91a5
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a5039117c649943a1f05a91ecccf22eb4230e5e7
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67776384"
---
# <a name="assemblymetadata-structure"></a>ASSEMBLYMETADATA 구조체
해당 버전 및 해당 수준의 로캘, 프로세서 및 운영 체제에 대 한 지원 포함 한 참조 된 어셈블리에 대 한 정보를 포함 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef struct {  
    USHORT  usMajorVersion;  
    USHORT  usMinorVersion;  
    USHORT  usBuildNumber;  
    USHORT  usRevisionNumber;  
    LPWSTR  szLocale;  
    ULONG   cbLocale;  
    DWORD*  rdwProcessor[];  
    ULONG   ulProcessor  
    OSINFO* rOS[];  
    ULONG   ulOS;  
} ASSEMBLYMETADATA;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`usMajorVersion`|참조 된 어셈블리의 주 버전 번호입니다. 이 값은 0 일 수 없습니다. 하는 경우의 모든 비트가 `usMajorVersion` 주요 버전을 지정 하지 않으면 설정 됩니다.|  
|`usMinorVersion`|참조 된 어셈블리의 부 버전 번호입니다. 이 값은 0 일 수 없습니다. 하는 경우의 모든 비트가 `usMinorVersion` 부 버전을 지정 하지 않으면 설정 됩니다.|  
|`usBuildNumber`|참조 된 어셈블리의 빌드 번호입니다. 이 값은 0 일 수 없습니다. 하는 경우의 모든 비트가 `usBuildNumber` 빌드 번호를 지정 하지 않으면 설정 됩니다.|  
|`usRevisionNumber`|참조 된 어셈블리의 수정 번호입니다. 이 값은 0 일 수 없습니다. 하는 경우의 모든 비트가 `usRevisionNumber` 수정 번호를 지정 하지 않으면 설정 됩니다.|  
|`szLocale`|목록에 참조 된 어셈블리에서 지원 되는 로캘을 지정 세미콜론으로 구분 된 RFC1766 사양에 맞는 로캘 이름입니다. Null 값에는 로캘과 관련이 없음을 나타냅니다. **참고:**  .NET framework 버전 1.0 둘 이상의 로캘을 지정할 수 없습니다.|  
|`cbLocale`|와이드 문자에서 크기 `szLocale`합니다.|  
|`rdwProcessor`|참조 된 어셈블리에서 지원 되는 프로세서 유형에 대 한 Winnt.h에 정의 된 식별자의 배열입니다. NULL 값에는 프로세서 관련이 없음을 나타냅니다.|  
|`ulProcessor`|길이 `rdwProcessor` 배열입니다.|  
|`rOS`|배열을 [OSINFO](../../../../docs/framework/unmanaged-api/metadata/osinfo-structure.md) 참조 된 어셈블리에서 지원 되는 운영 체제를 지정 하는 인스턴스. NULL 값에는 운영 체제 관련이 없음을 나타냅니다.|  
|`ulOS`|길이 `rOS` 배열입니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 구조체](../../../../docs/framework/unmanaged-api/metadata/metadata-structures.md)
- [IMetaDataAssemblyEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-interface.md)
- [OSINFO 구조체](../../../../docs/framework/unmanaged-api/metadata/osinfo-structure.md)
