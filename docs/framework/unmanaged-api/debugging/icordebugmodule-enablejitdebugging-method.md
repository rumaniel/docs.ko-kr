---
title: ICorDebugModule::EnableJITDebugging 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugModule.EnableJITDebugging
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule::EnableJITDebugging
helpviewer_keywords:
- ICorDebugModule::EnableJITDebugging method [.NET Framework debugging]
- EnableJITDebugging method [.NET Framework debugging]
ms.assetid: 0a65e2a4-5bb6-496c-ae6f-40474426b5a6
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8aeb6ed448539db2720fee0d42cfcc344fd3bbf7
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67762768"
---
# <a name="icordebugmoduleenablejitdebugging-method"></a>ICorDebugModule::EnableJITDebugging 메서드
Just-in-time (JIT) 컴파일러가이 모듈 내에서 메서드에 대 한 디버깅 정보를 유지할지 여부를 제어 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT EnableJITDebugging(  
    [in] BOOL bTrackJITInfo,  
    [in] BOOL bAllowJitOpts  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `bTrackJITInfo`  
 [in] 이 값을 설정 `true` 는 MSIL (intermediate language) 버전의 Microsoft 및이 모듈에서 각 메서드의 JIT 컴파일된 버전 간의 매핑 정보를 유지 하기 위해 JIT 컴파일러를 사용 하도록 설정 합니다.  
  
 `bAllowJitOpts`  
 [in] 이 값을 설정 `true` 디버깅에 대 한 특정 관련 JIT 최적화를 사용 하 여 코드를 생성 하는 JIT 컴파일러를 사용 하도록 설정 합니다.  
  
## <a name="remarks"></a>설명  
 JIT 디버깅이 디버거가 활성 상태일 때 로드 되는 모든 모듈에 대해 기본적으로 사용 됩니다. 프로그래밍 방식으로 사용 하도록 설정 하거나 사용 하지 않도록 설정 된 전역 설정을 재정의 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
