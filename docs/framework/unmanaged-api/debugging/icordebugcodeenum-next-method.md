---
title: ICorDebugCodeEnum::Next 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugCodeEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCodeEnum::Next
helpviewer_keywords:
- ICorDebugCodeEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugEnum interface [.NET Framework debugging]
ms.assetid: 644ece86-384d-4c63-9fba-52c789616ff7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 076b5d628dfe83decdbbe2f5e74c50e08262c580
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700689"
---
# <a name="icordebugcodeenumnext-method"></a>ICorDebugCodeEnum::Next 메서드

현재 위치에서 시작 하 여 열거형에서 지정 된 수의 "ICorDebugCode" 인스턴스를 가져옵니다.

## <a name="syntax"></a>구문

```cpp
HRESULT Next (
    [in] ULONG  celt,
    [out, size_is(celt), length_is(*pceltFetched)]
        ICorDebugCode *values[],
    [out] ULONG *pceltFetched
);
```

## <a name="parameters"></a>매개 변수

 `celt`  
 진행 검색할 `ICorDebugCode` 인스턴스 수입니다.

 `values`  
 제한이 각각 `ICorDebugCode` 개체를 가리키는 포인터의 배열입니다.

 `pceltFetched`  
 제한이 실제로 반환 된 @no__t 인스턴스 수에 대 한 포인터입니다. @No__t-0이 1 이면이 값은 null 일 수 있습니다.

## <a name="requirements"></a>요구 사항

 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

 **헤더:** CorDebug.idl, CorDebug.h

 **라이브러리** CorGuids.lib

 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
 
