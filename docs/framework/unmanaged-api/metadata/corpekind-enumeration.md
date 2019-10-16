---
title: CorPEKind 열거형
ms.date: 03/30/2017
api_name:
- CorPEKind
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorPEKind
helpviewer_keywords:
- CorPEKind enumeration [.NET Framework metadata]
ms.assetid: 22dc6dea-b1b9-4982-a730-a022d586b117
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 0bfe30567bcd8e22a82d401e00b0a6ee50407def
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781665"
---
# <a name="corpekind-enumeration"></a>CorPEKind 열거형
에 대 한 호출에서 반환 된 pe (이식 가능) 파일을 설명 하는 값을 포함 [IMetaDataImport2::GetPEKind](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-getpekind-method.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum CorPEKind {  
  
    peNot           = 0x00000000,  
    peILonly        = 0x00000001,  
    pe32BitRequired = 0x00000002,  
    pe32Plus        = 0x00000004,  
    pe32Unmanaged   = 0x00000008,  
    pe32BitPreferred= 0x00000010  
  
} CorPEKind;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`peNot`|PE 파일 아님을 나타냅니다.|  
|`peILOnly`|이 PE 파일에 코드를 관리 되는 포함 되어 있음을 나타냅니다.|  
|`pe32BitRequired`|PE 파일이 Win32 호출을 나타냅니다.|  
|`pe32Plus`|64 비트 플랫폼에서이 PE 파일을 실행 함을 나타냅니다.|  
|`pe32Unmanaged`|PE 파일을 네이티브 코드를 나타냅니다.|  
|pe32BitPreferred|PE 파일에이 플랫폼 중립적 선호 하는 32 비트 환경에서 로드할 수 있음을 나타냅니다.|  
  
## <a name="remarks"></a>설명  
 이러한 값의 비트 조합을 사용할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorHdr.h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
