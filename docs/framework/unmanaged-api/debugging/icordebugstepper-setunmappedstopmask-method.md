---
title: ICorDebugStepper::SetUnmappedStopMask 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.SetUnmappedStopMask
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::SetUnmappedStopMask
helpviewer_keywords:
- ICorDebugStepper::SetUnmappedStopMask method [.NET Framework debugging]
- SetUnmappedStopMask method [.NET Framework debugging]
ms.assetid: b1211981-e90c-4e05-8def-fa18d85ad9ab
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c0a273c54559e8e297e09740ba9c770ce12d72d1
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67760589"
---
# <a name="icordebugsteppersetunmappedstopmask-method"></a>ICorDebugStepper::SetUnmappedStopMask 메서드
매핑되지 않은 코드 실행을 중지할의 형식을 지정 하는 값을 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetUnmappedStopMask (  
    [in] CorDebugUnmappedStop   mask  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `mask`  
 [in] 디버거는 실행을 중단 하는 데는 비관리 코드의 형식을 지정 하는 CorDebugUnmappedStop 열거형의 값입니다.  
  
 기본값은 STOP_OTHER_UNMAPPED 합니다. 값 STOP_UNMANAGED interop 디버깅만 유효합니다.  
  
## <a name="remarks"></a>설명  
 비관리 코드의 해당 형식을 지정 하는 플래그를 설정한; 경우 실행 중단 디버거에서 MSIL (Microsoft intermediate language)에 해당 매핑이 없는-just-in-time (JIT) 컴파일에서 찾으면 그렇지 않으면가 계속 투명 하 게 단계별로 실행 합니다.  
  
 디버거를 사용 하지 않는 스텝 메서드를 입력 하는 경우 다음 않습니다 반드시 실행 매핑되지 않은 코드.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
