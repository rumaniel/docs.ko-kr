---
title: CorValidatorModuleType 열거형
ms.date: 03/30/2017
api_name:
- CorValidatorModuleType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorValidatorModuleType
helpviewer_keywords:
- CorValidatorModuleType enumeration [.NET Framework metadata]
ms.assetid: 748f1ab2-fbcb-4f55-89ec-8d23d81ebc80
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 04bed418d96658e29328cf2ce6bba445639b437f
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67750752"
---
# <a name="corvalidatormoduletype-enumeration"></a>CorValidatorModuleType 열거형
모듈의 형식을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum  
{  
    ValidatorModuleTypeInvalid  = 0x0,  
    ValidatorModuleTypeMin      = 0x00000001,  
    ValidatorModuleTypePE       = 0x00000001,  
    ValidatorModuleTypeObj      = 0x00000002,  
    ValidatorModuleTypeEnc      = 0x00000003,  
    ValidatorModuleTypeIncr     = 0x00000004,  
    ValidatorModuleTypeMax      = 0x00000004  
} CorValidatorModuleType;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`ValidatorModuleTypeInvalid`|모듈에는 잘못 된 형식입니다.|  
|`ValidatorModuleTypeMin`|최소값을 `CorValidatorModuleType` 열거형입니다.|  
|`ValidatorModuleTypePE`|모듈에는 pe (이식 가능) 파일입니다.|  
|`ValidatorModuleTypeObj`|모듈에는.obj 파일입니다.|  
|`ValidatorModuleTypeEnc`|모듈은 편집 및 계속 디버거 세션을 합니다.|  
|`ValidatorModuleTypeIncr`|모듈은 증분 방식으로 빌드된입니다.|  
|`ValidatorModuleTypeMax`|최대값을 `CorValidatorModuleType` 열거형입니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
