---
title: CorImportOptions 열거형
ms.date: 03/30/2017
api_name:
- CorImportOptions
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorImportOptions
helpviewer_keywords:
- CorImportOptions enumeration [.NET Framework metadata]
ms.assetid: 4e5d03cb-97c9-4ff4-8dbd-17d94ee374d3
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 38c0937804eb82d1c96a605b55a00784ba58fe13
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781822"
---
# <a name="corimportoptions-enumeration"></a>CorImportOptions 열거형
현재 범위를 벗어난 어셈블리를 가져오는 중의 동작을 제어하는 플래그 값을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum CorImportOptions {  
  
    MDImportOptionDefault                = 0x00000000,  
    MDImportOptionAll                    = 0xFFFFFFFF,  
    MDImportOptionAllTypeDefs            = 0x00000001,  
    MDImportOptionAllMethodDefs          = 0x00000002,  
    MDImportOptionAllFieldDefs           = 0x00000004,  
    MDImportOptionAllProperties          = 0x00000008,  
    MDImportOptionAllEvents              = 0x00000010,  
    MDImportOptionAllCustomAttributes    = 0x00000020,  
    MDImportOptionAllExportedTypes       = 0x00000040  
  
} CorImportOptions;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`MDImportOptionDefault`|삭제 된 레코드를 건너뛸 하는 기본 동작을 나타냅니다.|  
|`MDImportOptionAll`|모든 메타 데이터를 열거 해야 함을 나타냅니다.|  
|`MDImportOptionAllTypeDefs`|삭제 된 항목을 포함 하는 모든 형식 정의 열거 해야 함을 나타냅니다.|  
|`MDImportOptionAllMethodDefs`|삭제 된 항목을 포함 하는 모든 MethodDefs 열거 해야 함을 나타냅니다.|  
|`MDImportOptionAllFieldDefs`|삭제 된 항목을 포함 하 여 모든 Fielddef 열거 해야 함을 나타냅니다.|  
|`MDImportOptionAllProperties`|삭제 된 항목을 포함 하는 모든 PropertyDefs 열거 해야 함을 나타냅니다.|  
|`MDImportOptionAllEvents`|삭제 된 항목을 포함 하 여 모든 Eventdef 열거 해야 함을 나타냅니다.|  
|`MDImportOptionAllCustomAttributes`|삭제 된 항목을 포함 하 여 모든 사용자 지정 특성을 열거 해야 함을 나타냅니다.|  
|`MDImportOptionAllExportedTypes`|삭제 된 항목을 비롯 한 모든 내보낸된 형식이 열거 해야 함을 나타냅니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorHdr.h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
