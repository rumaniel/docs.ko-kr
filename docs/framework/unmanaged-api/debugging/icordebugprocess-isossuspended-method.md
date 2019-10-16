---
title: ICorDebugProcess::IsOSSuspended 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.IsOSSuspended
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::IsOSSuspended
helpviewer_keywords:
- IsOSSuspended method [.NET Framework debugging]
- ICorDebugProcess::IsOSSuspended method [.NET Framework debugging]
ms.assetid: 83406cb2-5797-4402-872d-89c9516aefec
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 275f62c8211f71f067d310dd4b3af2ddb11e93d7
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67755465"
---
# <a name="icordebugprocessisossuspended-method"></a>ICorDebugProcess::IsOSSuspended 메서드
이 프로세스를 중지 하는 디버거 결과로 지정 된 스레드가 일시 중단 된 여부를 나타내는 값을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT IsOSSuspended(  
    [in]  DWORD threadID,  
    [out] BOOL  *pbSuspended);  
```  
  
## <a name="parameters"></a>매개 변수  
 `threadID`  
 [in] 해당 스레드의 ID입니다.  
  
 `pbSuspended`  
 [out] 부울 값에 대 한 포인터 `true` 지정된 된 스레드의 일시 중단 된 그렇지 않은 경우 *`pbSuspended` 는 `false`합니다.  
  
## <a name="remarks"></a>설명  
 지정 된 스레드의 Win32 일시 중단 횟수가 지정된 된 스레드에으로 일시 중단 된 결과로 디버거가이 프로세스를 중지 하는 경우 1 씩 증가 합니다. 디버거 사용자 인터페이스 (UI) 운영 체제를 표시 하는 경우 계정에이 정보를 사용 하려고 합니다. (OS) 사용자에 게 스레드 개수를 일시 중단 합니다.  
  
 `IsOSSuspended` 메서드가 관리 되지 않는 디버깅의 경우에만 적합 합니다. 관리 되는 디버깅 하는 동안 스레드는 협조적으로 일시 중단 된 것이 아니라 OS 일시 중단 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
