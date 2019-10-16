---
title: DacpModuleData 구조체
ms.date: 02/01/2019
api.name:
- DacpModuleData Structure
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- DacpModuleData Structure
helpviewer.keywords:
- DacpModuleData Structure [.NET Framework debugging]
topic_type:
- apiref
author: hoyosjs
ms.author: juhoyosa
ms.openlocfilehash: 2e27082ba4c35bc10eb65139b2af6c81c10d79a6
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67739127"
---
# <a name="dacpmoduledata-structure"></a>DacpModuleData 구조체

모듈의 런타임 정보에 대 한 전송 버퍼를 정의합니다.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>구문

```cpp
struct DacpModuleData
{
    CLRDATA_ADDRESS Address;
    CLRDATA_ADDRESS File; 
    CLRDATA_ADDRESS  ilBase;
    char payLoad[132];
};
```

## <a name="members"></a>멤버

| 멤버    | 설명                                                             |
| --------- | ----------------------------------------------------------------------- |
| `Address` | 모듈 개체의 주소입니다.                                           |
| `File`    | Pe (이식 가능) 파일에 대 한 포인터입니다.                       |
| `ilBase`  | 로드 된 이미지의 주소의 기본입니다.                                 |
| `payLoad` | 런타임에서 사용 되는 추가 모듈 정보에 대 한 페이로드 버퍼입니다. |

## <a name="remarks"></a>설명

이 구조는 런타임 내에서 있으며 모든 헤더 또는 라이브러리 파일을 통해 노출 되지 않습니다. 를 사용 하려면 위에서 지정한 대로 구조를 정의 합니다.

## <a name="requirements"></a>요구 사항
**플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
**헤더:** 없음  
**라이브러리:** 없음  
**.NET Framework 버전:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>참고자료

- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
- [디버깅 구조체](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)
