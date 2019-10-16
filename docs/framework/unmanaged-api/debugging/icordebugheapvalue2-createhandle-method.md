---
title: ICorDebugHeapValue2::CreateHandle 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugHeapValue2.CreateHandle
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapValue2::CreateHandle
helpviewer_keywords:
- CreateHandle method [.NET Framework debugging]
- ICorDebugHeapValue2::CreateHandle method [.NET Framework debugging]
ms.assetid: fbc418e8-fa22-420d-84ec-e0e1800db041
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: da5c5a12df5689f113857045ba4bcda696bda8f5
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67756722"
---
# <a name="icordebugheapvalue2createhandle-method"></a>ICorDebugHeapValue2::CreateHandle 메서드
이 ICorDebugHeapValue2 개체로 표현 되는 힙 값에 대 한 지정 된 형식의 핸들을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CreateHandle (  
    [in] CorDebugHandleType      type,   
    [out] ICorDebugHandleValue   **ppHandle  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `type`  
 [in] 만들려는 핸들의 형식을 지정 하는 CorDebugHandleType 열거형의 값입니다.  
  
 `ppHandle`  
 [out] 이 힙 값에 대 한 새 핸들을 나타내는 ICorDebugHandleValue 개체의 주소에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 핸들 힙 값을 사용 하 여 연결 된 응용 프로그램 도메인에서 만들어지고 응용 프로그램 도메인이 언로드된 경우 유효 하지 않게 됩니다.  
  
 같은 힙 값에 대 한이 함수를 여러 번 호출을 여러 핸들을 만듭니다. 가비지 수집의 성능에 영향을 주는 처리 하기 때문에 디버거에서 상대적으로 적은 수의 한 번에 활성 상태인 처리 (약 256) 자체를 제한 해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
