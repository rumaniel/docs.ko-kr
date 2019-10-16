---
title: COR_PRF_MODULE_FLAGS 열거형
ms.date: 03/30/2017
api_name:
- COR_PRF_MODULE_FLAGS
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_MODULE_FLAGS
helpviewer_keywords:
- COR_PRF_MODULE_FLAGS enumeration [.NET Framework profiling]
ms.assetid: 7bc3a938-0df1-4739-9ff1-89cff454b704
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f94867db6908f0999604511d9782b6f5abfb5e77
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67752041"
---
# <a name="corprfmoduleflags-enumeration"></a>COR_PRF_MODULE_FLAGS 열거형
모듈의 속성을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum  
{  
    COR_PRF_MODULE_DISK             = 0x00000001,  
    COR_PRF_MODULE_NGEN             = 0x00000002,  
    COR_PRF_MODULE_DYNAMIC          = 0x00000004,  
    COR_PRF_MODULE_COLLECTIBLE      = 0x00000008,  
    COR_PRF_MODULE_RESOURCE         = 0x00000010,  
    COR_PRF_MODULE_FLAT_LAYOUT      = 0x00000020,  
    COR_PRF_MODULE_WINDOWS_RUNTIME  = 0x00000040  
}   COR_PRF_MODULE_FLAGS;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|설명|  
|------------|-----------------|  
|COR_PRF_MODULE_DISK|모듈은 디스크에서 로드 되었습니다.|  
|COR_PRF_MODULE_NGEN|모듈 네이티브 이미지 생성기 (Ngen.exe)에서 생성 되었습니다.|  
|COR_PRF_MODULE_DYNAMIC|모듈의 메서드에 의해 만들어진는 <xref:System.Reflection.Emit?displayProperty=nameWithType> 네임 스페이스입니다.|  
|COR_PRF_MODULE_COLLECTIBLE|모듈의 수명 동안 가비지 수집기에 의해 관리 됩니다.|  
|COR_PRF_MODULE_RESOURCE|모듈 메타 데이터를 포함 하 고 리소스로 엄격 하 게 사용 됩니다. 이 비트에 해당 하는 관리 되는 <xref:System.Reflection.Module.IsResource%2A?displayProperty=nameWithType> 메서드.|  
|COR_PRF_MODULE_FLAT_LAYOUT|메모리에서 모듈의 레이아웃은 플랫 매핑되지 않습니다. 모듈에이 비트는 설정, 프로파일러는 이식 가능한 실행 파일 (PE) 파일 헤더 로부터 직접 정보가 가상 Rva (상대 주소)에서 헤더를 해석할 때 주의 해야 합니다. 읽기.|  
|COR_PRF_MODULE_WINDOWS_RUNTIME|Windows 런타임 콘텐츠 형식 플래그는이 모듈의이 어셈블리에 대 한 메타 데이터에서 설정 됩니다. 이 경우 모든 Windows 메타 데이터 (.winmd) 모듈에 대 한 합니다.|  
  
## <a name="remarks"></a>설명  
 COR_PRF_MODULE_FLAGS에서 비트에서 프로파일러에 반환 되는 `pdwModuleFlags` 의 출력 매개 변수를 [ICorProfilerInfo3::GetModuleInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getmoduleinfo2-method.md) 메서드. 두 개 이상의 플래그의 일부 조합이 가능 하지만 일부 조합은 가능 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [프로파일링 열거형](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)
