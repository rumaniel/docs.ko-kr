---
title: CorErrorIfEmitOutOfOrder 열거형
ms.date: 03/30/2017
api_name:
- CorErrorIfEmitOutOfOrder
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorErrorIfEmitOutOfOrder
helpviewer_keywords:
- CorErrorIfEmitOutOfOrder enumeration [.NET Framework metadata]
ms.assetid: 6d758aad-29a7-44fe-9481-bbff5b799a32
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 16f6d7bf6fa1730d50cfe81526817e492a453dad
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781980"
---
# <a name="corerrorifemitoutoforder-enumeration"></a>CorErrorIfEmitOutOfOrder 열거형
메타데이터를 내보내는 순서가 잘못되었을 때 오류 메시지가 생성되어야 하는 조건을 나타내는 플래그 값을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum CorErrorIfEmitOutOfOrder {  
  
    MDErrorOutOfOrderDefault    = 0x00000000,  
    MDErrorOutOfOrderNone       = 0x00000000,  
    MDErrorOutOfOrderAll        = 0xffffffff,  
    MDMethodOutOfOrder          = 0x00000001,  
    MDFieldOutOfOrder           = 0x00000002,  
    MDParamOutOfOrder           = 0x00000004,  
    MDPropertyOutOfOrder        = 0x00000008,  
    MDEventOutOfOrder           = 0x00000010  
  
} CorErrorIfEmitOutOfOrder;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`MDErrorOutOfOrderDefault`|오류 메시지를 생성 하지 않는 기본 동작을 나타냅니다.|  
|`MDErrorOutOfOrderNone`|컴파일러 오류 메시지를 생성 하지 해야 함을 나타냅니다.|  
|`MDErrorOutOfOrderAll`|필드, 속성, 이벤트, 메서드, 하는 경우 컴파일러 오류 메시지를 생성할지 또는 매개 변수 순서가 내보내집니다 나타냅니다.|  
|`MDMethodOutOfOrder`|메서드는 내보내는 순서가 잘못 되었을 때 컴파일러에서 오류 메시지를 생성 해야 함을 나타냅니다.|  
|`MDFieldOutOfOrder`|필드는 내보내는 순서가 잘못 되었을 때 컴파일러에서 오류 메시지를 생성 해야 함을 나타냅니다.|  
|`MDParamOutOfOrder`|매개 변수가 잘못 된 순서로 경우 컴파일러에서 오류 메시지를 생성 해야 함을 나타냅니다.|  
|`MDPropertyOutOfOrder`|속성은 내보내는 순서가 잘못 되었을 때 컴파일러에서 오류 메시지를 생성 해야 함을 나타냅니다.|  
|`MDEventOutOfOrder`|이벤트의 순서가 내보내집니다 때 컴파일러에서 오류 메시지를 생성 해야 함을 나타냅니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorHdr.h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
