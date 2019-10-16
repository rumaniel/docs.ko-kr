---
title: CREATE_ASM_NAME_OBJ_FLAGS 열거형
ms.date: 03/30/2017
api_name:
- CREATE_ASM_NAME_OBJ_FLAGS
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- CREATE_ASM_NAME_OBJ_FLAGS
helpviewer_keywords:
- CREATE_ASM_NAME_OBJ_FLAGS enumeration [.NET Framework fusion]
ms.assetid: a5ed2fd0-c7d2-4603-aaca-5d0caad92675
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9897e396424b9076da8f30c61b5a14cfa9539690
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795428"
---
# <a name="create_asm_name_obj_flags-enumeration"></a>CREATE_ASM_NAME_OBJ_FLAGS 열거형
[Createassemblynameobject](createassemblynameobject-function.md) 함수에 의해 생성 되는 경우 [IAssemblyName Interface](iassemblyname-interface.md) 개체의 특성을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum {  
  
    CANOF_PARSE_DISPLAY_NAME            = 0x1,  
    CANOF_SET_DEFAULT_VALUES            = 0x2,  
    CANOF_VERIFY_FRIEND_ASSEMBLYNAME    = 0x4,  
    CANOF_PARSE_FRIEND_DISPLAY_NAME     =   
        CANOF_PARSE_DISPLAY_NAME | CANOF_VERIFY_FRIEND_ASSEMBLYNAME  
  
} CREATE_ASM_NAME_OBJ_FLAGS;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`CANOF_PARSE_DISPLAY_NAME`|전달 된 매개 변수가 텍스트 id 임을 나타냅니다.|  
|`CANOF_SET_DEFAULT_VALUES`|몇 가지 기본값을 설정 합니다.|  
|`CANOF_VERIFY_FRIEND_ASSEMBLYNAME`|Friend 어셈블리 규칙 (이름 및 공개 키만)을 확인 합니다. 이 멤버는 내부용 으로만 사용 됩니다.|  
|`CANOF_PARSE_FRIEND_DISPLAY_NAME`|`CANOF_PARSE_DISPLAY_NAME` 및`CANOF_VERIFY_FRIEND_ASSEMBLYNAME` 플래그의 조합입니다. 이 멤버는 내부용 으로만 사용 됩니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Fusion. h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IAssemblyName 인터페이스](iassemblyname-interface.md)
- [CreateAssemblyNameObject 함수](createassemblynameobject-function.md)
- [Fusion 열거형](fusion-enumerations.md)
