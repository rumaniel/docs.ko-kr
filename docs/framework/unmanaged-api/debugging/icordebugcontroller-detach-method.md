---
title: ICorDebugController::Detach 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugController.Detach
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::Detach
helpviewer_keywords:
- Detach method, ICorDebugController interface [.NET Framework debugging]
- ICorDebugController::Detach method [.NET Framework debugging]
ms.assetid: 06fae364-f2c6-4a50-aa7e-3da9f2684dc3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f687e48413cb227ad715720e24bd645065309553
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67748850"
---
# <a name="icordebugcontrollerdetach-method"></a>ICorDebugController::Detach 메서드
프로세스 또는 응용 프로그램 도메인에서 디버거를 분리합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT Detach ();  
```  
  
## <a name="remarks"></a>설명  
 프로세스 또는 응용 프로그램 도메인 실행을 일반적으로 계속 하지만 "ICorDebugProcess" 또는 "ICorDebugAppDomain" 개체를 더 이상 유효 하 고 없습니다 추가 콜백이 발생 합니다.  
  
 .NET framework 버전 2.0에서 관리 되지 않는 디버깅을 사용 하도록 설정 하는 경우 운영 체제 제한으로 인해이 메서드가 실패 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료
