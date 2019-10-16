---
title: ICorDebugNativeFrame::GetIP 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.GetIP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::GetIP
helpviewer_keywords:
- GetIP method, ICorDebugNativeFrame interface [.NET Framework debugging]
- ICorDebugNativeFrame::GetIP method [.NET Framework debugging]
ms.assetid: 99f693f3-d3b9-4fd8-9d09-b8efd03f7b67
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 71e9149bafc866f89253c4318ac69f2705431e48
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67765298"
---
# <a name="icordebugnativeframegetip-method"></a>ICorDebugNativeFrame::GetIP 메서드
가져옵니다 네이티브 코드 명령 포인터를 현재 설정 된 위치를 오프셋입니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetIP (  
    [out] ULONG32           *pnOffset  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pnOffset`  
 [out] 네이티브 코드 내의 오프셋된 위치에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 이 "ICorDebugNativeFrame"으로 표시 되는 스택 프레임을 활성 상태인 경우 오프셋 실행할 다음 명령의 주소입니다. 이 스택 프레임이 활성 상태인 경우 오프셋은 스택 프레임을 다시 활성화 될 때 실행할 다음 명령의 주소입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료
