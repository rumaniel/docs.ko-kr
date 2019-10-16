---
title: CeeSectionRelocType 열거형
ms.date: 03/30/2017
api_name:
- CeeSectionRelocType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CeeSectionRelocType
helpviewer_keywords:
- CeeSectionRelocType enumeration [.NET Framework metadata]
ms.assetid: 124656f6-0dad-4ceb-9043-d3869ab65cde
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1218ee76a3b7a2f501f87adf1e0bc8133d5329b5
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781344"
---
# <a name="ceesectionreloctype-enumeration"></a>CeeSectionRelocType 열거형
값의 형식에 영향을 줄을 제공 `reloc` 명령에 대 한 호출에서 내보낸 [iceegen:: Addsectionreloc](../../../../docs/framework/unmanaged-api/metadata/iceegen-addsectionreloc-method.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum  {  
    srRelocAbsolute,  
    srRelocHighLow          = 3,  
    srRelocHighAdj,       
    srRelocMapToken,  
    srRelocRelative,  
    srRelocFilePos,  
    srRelocCodeRelative,  
    srRelocIA64Imm64,  
    srRelocDir64,  
    srRelocIA64PcRel25,  
    srRelocIA64PcRel64,    srRelocAbsoluteTagged,    srRelocSentinel,    srNoBaseReloc       = 0x4000,  
    srRelocPtr          = 0x8000,  
    srRelocAbsolutePtr      = srRelocPtr + srRelocAbsolute,  
    srRelocHighLowPtr       = srRelocPtr + srRelocHighLow,  
    srRelocRelativePtr      = srRelocPtr + srRelocRelative,  
    srRelocIA64Imm64Ptr     = srRelocPtr + srRelocIA64Imm64,  
    srRelocDir64Ptr         = srRelocPtr + srRelocDir64  
    } CeeSectionRelocType;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`srRelocAbsolute`|섹션 상대만 생성 `reloc`.reloc 섹션에 아무 것도 합니다.|  
|`srRelocHighLow`|생성 된 `reloc` 포인터 크기의 위치에 대 한 합니다. 플랫폼에 따라 BASED_HIGHLOW 또는 BASED_DIR64로 변환 됩니다.|  
|`srRelocHighAdj`|생성 된 `reloc` 상위 하위 16 비트.reloc 표에 다음 단어에 포함 된 있는 32 비트 숫자의 16 비트에 대 한 합니다.|  
|`srRelocMapToken`|Nothing.reloc 섹션으로 전송 된 토큰 맵을 재배치를 생성 합니다.|  
|`srRelocRelative`|값이 상대 주소 픽스업의 임을 나타냅니다.|  
|`srRelocFilePos`|섹션 상대만 생성 `reloc`.reloc 섹션에 아무 것도 합니다. 이 `reloc` 없습니다 섹션의 가상 주소 섹션의 파일 위치에 상대적입니다.|  
|`srRelocCodeRelative`|픽스업 코드 상대 주소를 지정합니다.|  
|`srRelocIA64Imm64`|생성 된 `reloc` ia64에서 64 비트 주소에 대 한 `movl` 명령입니다.|  
|`srRelocDir64`|생성 된 `reloc` 64 비트 주소에 대 한 합니다.|  
|`srRelocIA64PcRel25`|생성 된 `reloc` ia64에서 25 비트 PC 상대 주소에 대 한 `br.call` 명령입니다.|  
|`srRelocIA64PcRel64`|생성 된 `reloc` ia64에서 64 비트 PC 상대 주소에 대 한 `brl.call` 명령입니다.|  
|`srRelocAbsoluteTagged`|30 비트 섹션 관련 생성 `reloc`태그가 지정 된 포인터 값에 사용 되는 합니다.|  
|`srRelocSentinel`|이 열거형에 대 한 추가 확인 하는 데 센티널 값 내부에 반영 됩니다 `reloc` 이름 배열입니다.|  
|`srNoBaseReloc`|자료를 내보낼 필요가 지정 `reloc`합니다.|  
|`srRelocPtr`|픽스업 전 메모리의 내용이 섹션을이 아닌 포인터를 나타내는 값을 오프셋 합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
- [ICeeGen 인터페이스](../../../../docs/framework/unmanaged-api/metadata/iceegen-interface.md)
- [AddSectionReloc 메서드](../../../../docs/framework/unmanaged-api/metadata/iceegen-addsectionreloc-method.md)
