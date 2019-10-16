---
title: ICorDebugCode2::GetCodeChunks 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugCode2.GetCodeChunks
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode2::GetCodeChunks
helpviewer_keywords:
- GetCodeChunks method [.NET Framework debugging]
- ICorDebugCode2::GetCodeChunks method [.NET Framework debugging]
ms.assetid: 210a2f02-2678-4555-bc4a-78a0408764c8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1bdaf6391ca5c19f073708d6258ad5775bec9824
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700723"
---
# <a name="icordebugcode2getcodechunks-method"></a>ICorDebugCode2::GetCodeChunks 메서드

이 코드 개체가 구성 된 코드의 청크를 가져옵니다.

## <a name="syntax"></a>구문

```cpp
HRESULT GetCodeChunks (
    [in]  ULONG32     cbufSize,
    [out] ULONG32     *pcnumChunks,
    [out, size_is(cbufSize), length_is(*pcnumChunks)]
        CodeChunkInfo chunks[]
);
```

## <a name="parameters"></a>매개 변수

 `cbufSize`  
 진행 @No__t-0 배열의 크기입니다.

 `pcnumChunks`  
 제한이 @No__t-0 배열에서 반환 된 청크의 수입니다.

 `chunks`  
 제한이 각각 단일 코드 청크를 나타내는 "CodeChunkInfo" 구조체의 배열입니다. @No__t-0의 값이 0 이면이 매개 변수는 null 일 수 있습니다.

## <a name="remarks"></a>설명

 코드 청크가 겹치면 안 되며, [ICorDebugCode:: GetCode](icordebugcode-getcode-method.md)에 의해 연결 된 순서를 따릅니다. .NET Framework 버전 2.0의 MSIL (Microsoft 중간 언어) 코드 개체는 단일 코드 청크로 구성 됩니다.

## <a name="requirements"></a>요구 사항

 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

 **헤더:** CorDebug.idl, CorDebug.h

 **라이브러리** CorGuids.lib

 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
 
