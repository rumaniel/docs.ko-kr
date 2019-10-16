---
title: ICorDebugEval::NewArray 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugEval.NewArray
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::NewArray
helpviewer_keywords:
- NewArray method [.NET Framework debugging]
- ICorDebugEval::NewArray method [.NET Framework debugging]
ms.assetid: cc79a67d-5368-434d-a943-209db90491b9
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9597d05e46c2d41ab1f24a073c028561e944fb59
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67753036"
---
# <a name="icordebugevalnewarray-method"></a>ICorDebugEval::NewArray 메서드
지정 된 요소 형식 및 차원에는 새 배열을 할당합니다.  
  
 이 메서드는.NET Framework 버전 2.0에서에서 사용 되지 않습니다. 사용 하 여 [ICorDebugEval2::NewParameterizedArray](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-newparameterizedarray-method.md) 대신 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT NewArray (  
    [in] CorElementType     elementType,  
    [in] ICorDebugClass     *pElementClass,  
    [in] ULONG32            rank,  
    [in, size_is(rank)] ULONG32 dims[],  
    [in, size_is(rank)] ULONG32 lowBounds[]  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `elementType`  
 [in] 배열의 요소 형식을 지정 하는 CorElementType 열거형의 값입니다.  
  
 `pElementClass`  
 [in] 요소의 클래스를 지정 하는 ICorDebugClass 개체에 대 한 포인터입니다. 이 값 요소 형식이 기본 형식인 경우에 null 일 수 있습니다.  
  
 `rank`  
 [in] 배열의 차원 수입니다. .NET Framework 2.0에서는이 값에는 1 이어야 합니다.  
  
 `dims`  
 [in] 바이트 배열의 각 차원 크기입니다.  
  
 `lowBounds`  
 [in] 선택적 항목으로, 배열의 각 차원 하 한. 이 값을 생략 하는 경우에 각 차원에 대 한 하한값 0으로 간주 됩니다.  
  
## <a name="remarks"></a>설명  
 스레드가 현재 실행 중인 응용 프로그램 도메인에서 배열 항상 만들어집니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET framework 버전:** 1.1, 1.0
