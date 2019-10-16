---
title: ICorDebugStepper2::SetJMC 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugStepper2.SetJMC
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper2::SetJMC
helpviewer_keywords:
- ICorDebugStepper2::SetJMC method [.NET Framework debugging]
- SetJMC method [.NET Framework debugging]
ms.assetid: f5cdc135-6db4-4b32-9dd1-260ec58b774f
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5c6b53d23410dd310766dab44664c8cd865ee9ba
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67771689"
---
# <a name="icordebugstepper2setjmc-method"></a>ICorDebugStepper2::SetJMC 메서드
응용 프로그램의 개발자가 작성 된 코드를 통해서만이 ICorDebugStepper 단계 여부를 지정 하는 값을 설정 합니다. 이 프로세스는으로 내 코드만 (JMC) 디버깅 라고도 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetJMC (  
    [in] BOOL    fIsJMCStepper  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `fIsJMCStepper`  
 [in] 로 `true` 코드는 응용 프로그램의 개발자가 작성 한이 고, 그렇지로 단계별로 `false`합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
