---
title: ICorDebugDataTarget::GetPlatform 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugDataTarget.GetPlatform Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugDataTarget::GetPlatform
helpviewer_keywords:
- GetPlatform method [.NET Framework debugging]
- ICorDebugDataTarget::GetPlatform method [.NET Framework debugging]
ms.assetid: 9ee96c9d-7a3d-4129-a6cc-7675c7f2dda4
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1065c8d710ddbd6088ee0db694a43e098564e707
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67750384"
---
# <a name="icordebugdatatargetgetplatform-method"></a>ICorDebugDataTarget::GetPlatform 메서드
프로세서 아키텍처와 대상 프로세스가 실행 되는 운영 체제를 포함 하 여 플랫폼에 대 한 정보를 제공 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetPlatform([out] CorDebugPlatform * pTargetPlatform);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pTargetPlatform`  
 [out] 에 대 한 포인터를 [CorDebugPlatformEnum](../../../../docs/framework/unmanaged-api/debugging/cordebugplatform-enumeration.md) 대상 플랫폼을 설명 하는 열거형입니다.  
  
## <a name="remarks"></a>설명  
 `CorDebugPlatformEnum` 열거형 반환 값은 사용 된 [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md) 포인터 크기, 주소 공간 레이아웃, 레지스터 집합, 명령 형식, 상황에 맞는 레이아웃 대상 프로세스의 세부 정보를 확인 하는 인터페이스 및 호출 규칙입니다.  
  
 `pTargetPlatform` 값 사용에는 실제 하드웨어를 지정 하는 대신 대상에 대해 에뮬레이트 되는 플랫폼을 참조할 수 있습니다. 예를 들어, 64 비트 버전 Windows 운영 체제의 Windows (WOW) 환경에서 Windows에서 실행 중인 프로세스를 사용 해야 합니다 `CORDB_PLATFORM_WINDOWS_X86` 의 값을 [CorDebugPlatformEnum](../../../../docs/framework/unmanaged-api/debugging/cordebugplatform-enumeration.md) 열거형입니다.  
  
 이 메서드는 성공 해야 합니다. 실패 한 경우 대상 플랫폼을 사용할 수 없는 합니다. 메서드는 다음과 같은 이유로 실패할 수 있습니다.  
  
- 대상에 대해 에뮬레이트 되는 플랫폼을 사용할 수 없는 합니다.  
  
- 대상 플랫폼에는 실제 하드웨어를 사용할 수 없습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebugDataTarget 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-interface.md)
- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
