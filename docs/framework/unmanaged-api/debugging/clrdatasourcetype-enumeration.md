---
title: CLRDataSourceType 열거형
ms.date: 01/16/2019
api.name:
- CLRDataSourceType Enumeration
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- CLRDataSourceType Enumeration
helpviewer.keywords:
- CLRDataSourceType Enumeration [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 7ace405e2624f15b1cdb6d383222ae87c93289bb
ms.sourcegitcommit: 3caa92cb97e9f6c31f21769c7a3f7c4304024b39
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71274103"
---
# <a name="clrdatasourcetype-enumeration"></a>CLRDataSourceType 열거형

CLRDATA_IL_ADDRESS_MAP 구조체에서 사용 되는 값을 제공 합니다.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>구문

```cpp
typedef enum
{
    CLRDATA_SOURCE_TYPE_INVALID        = 0x00, // To indicate that nothing else applies
} CLRDataSourceType;
```

## <a name="members"></a>멤버

| 멤버                        | 설명                           |
| ----------------------------- | ------------------------------------- |
| `CLRDATA_SOURCE_TYPE_INVALID` | 다른 항목이 적용 되지 않음을 나타내려면 |

## <a name="remarks"></a>설명

이 열거형은 런타임 내부에 있고 헤더 또는 라이브러리 파일을 통해 노출 되지 않습니다. 이를 사용 하려면 코드에서 위에 정의 된 열거형을 정의 합니다. 또한 [공통 데이터 형식](../common-data-types-unmanaged-api-reference.md)에 `CLRDATA_ENUM` 설명 된 대로이 별칭을로 지정 합니다.

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
**헤더:** 없음  
**라이브러리** 없음  
**.NET Framework 버전:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>참고 항목

- [디버깅](index.md)
- [디버깅 열거형](debugging-enumerations.md)
