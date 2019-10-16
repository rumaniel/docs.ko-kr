---
title: ICorDebugEval::CallFunction 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugEval.CallFunction
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::CallFunction
helpviewer_keywords:
- ICorDebugEval::CallFunction method [.NET Framework debugging]
- CallFunction method [.NET Framework debugging]
ms.assetid: 7f470c5c-e1c0-4d8d-aad8-830f113ae751
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 65225281fe3abaa20e69e96f4cd4d2a4b03a87ce
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65629937"
---
# <a name="icordebugevalcallfunction-method"></a>ICorDebugEval::CallFunction 메서드

지정된 된 함수에 대 한 호출을 설정합니다.

이 메서드는.NET Framework 버전 2.0에서에서 사용 되지 않습니다. 사용 하 여 [ICorDebugEval2::CallParameterizedFunction](icordebugeval2-callparameterizedfunction-method.md) 대신 합니다.

## <a name="syntax"></a>구문

```cpp
HRESULT CallFunction (
    [in] ICorDebugFunction  *pFunction,
    [in] ULONG32            nArgs,
    [in, size_is(nArgs)] ICorDebugValue *ppArgs[]
);
```

## <a name="parameters"></a>매개 변수

`pFunction`\
[in] 함수 호출 수를 지정 하는 ICorDebugFunction 개체에 대 한 포인터입니다.

`nArgs`\
[in] 함수에 대 한 인수의 수입니다.

`ppArgs`\
[in] 포인터의 배열에는 각 함수에 전달할 인수를 지정 하는 ICorDebugValue 개체를 가리킵니다.

## <a name="remarks"></a>설명

함수는 가상 경우 `CallFunction` 가상 디스패치를 수행 합니다. 함수는 다른 응용 프로그램 도메인에 있으면 모든 인수에에서도 포함 되어 해당 응용 프로그램 도메인으로 전환을 발생 합니다.

## <a name="requirements"></a>요구 사항

**플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.

**헤더:** CorDebug.idl, CorDebug.h

**라이브러리:** CorGuids.lib

**.NET framework 버전:** 1.1, 1.0

## <a name="see-also"></a>참고자료

- [CallParameterizedFunction 메서드](icordebugeval2-callparameterizedfunction-method.md)
