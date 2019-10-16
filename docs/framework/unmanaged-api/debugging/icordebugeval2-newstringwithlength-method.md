---
title: ICorDebugEval2::NewStringWithLength 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugEval2.NewStringWithLength
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval2::NewStringWithLength
helpviewer_keywords:
- NewStringWithLength method [.NET Framework debugging]
- ICorDebugEval2::NewStringWithLength method [.NET Framework debugging]
ms.assetid: d5f54a34-6335-4708-b407-a756ec70fab4
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a90f0a0319d88654d0310530749ef35b7095e0fb
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67754432"
---
# <a name="icordebugeval2newstringwithlength-method"></a>ICorDebugEval2::NewStringWithLength 메서드
지정된 된 콘텐츠를 사용 하 여 지정 된 길이의 문자열을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT NewStringWithLength (  
    [in] LPCWSTR               string,  
    [in] UINT                  uiLength  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `string`  
 [in] 문자열 값에 대 한 포인터입니다.  
  
 `uiLength`  
 [in] 문자열의 길이입니다.  
  
## <a name="remarks"></a>설명  
 경우 문자열의 후행 null 문자 이어야 하는데 관리 되는 문자열에서 호출자는 `NewStringWithLength` 메서드 문자열 길이 후행 null 문자를 포함 해야 합니다.  
  
 스레드가 현재 실행 중인 응용 프로그램 도메인에서 문자열 항상 만들어집니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
