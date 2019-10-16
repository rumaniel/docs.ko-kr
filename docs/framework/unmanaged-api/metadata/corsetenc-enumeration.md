---
title: CorSetENC 열거형
ms.date: 03/30/2017
api_name:
- CorSetENC
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorSetENC
helpviewer_keywords:
- CorSetENC enumeration [.NET Framework metadata]
ms.assetid: fe4150e8-071d-43fb-8e06-c3c616dbeed2
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2796be32154275387da891683cc5053095f534af
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67772319"
---
# <a name="corsetenc-enumeration"></a>CorSetENC 열거형
메타데이터 생성 중의 동작에 영향을 주는 데 사용되는 값을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum CorSetENC {  
  
    MDSetENCOn                  = 0x00000001,  
    MDSetENCOff                 = 0x00000002,  
  
    MDUpdateENC                 = 0x00000001,  
    MDUpdateFull                = 0x00000002,  
    MDUpdateExtension           = 0x00000003,  
    MDUpdateIncremental         = 0x00000004,  
    MDUpdateDelta               = 0x00000005,  
    MDUpdateMask                = 0x00000007  
  
} CorSetENC;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`MDSetENCOn`|더 이상 사용되지 않습니다.|  
|`MDSetENCOff`|더 이상 사용되지 않습니다.|  
|`MDUpdateENC`|메타 데이터를 업데이트할 수 있지만 토큰은 이동할 수 없음을 나타냅니다.|  
|`MDUpdateFull`|업데이트 하는 동안 토큰을 이동할 수 있는지를 나타냅니다.|  
|`MDUpdateExtension`|업데이트 추가 이루어진 수를 나타냅니다. 토큰을 이동할 수 없습니다.|  
|`MDUpdateIncremental`|증분 컴파일을 나타냅니다.|  
|`MDUpdateDelta`|해당만 변경 된 메타 데이터를 저장할 것을 나타냅니다.|  
|`MDUpdateMask`|포함 `MDUpdateENC`하십시오 `MDUpdateFull` 및 `MDUpdateIncremental`합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorHdr.h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
