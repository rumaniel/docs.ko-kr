---
title: ICorDebug::CreateProcess 메서드
ms.date: 03/30/2017
api_name:
- ICorDebug.CreateProcess
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebug::CreateProcess
helpviewer_keywords:
- ICorDebug::CreateProcess method [.NET Framework debugging]
- CreateProcess method, ICorDebugProcess interface [.NET Framework debugging]
ms.assetid: b6128694-11ed-46e7-bd4e-49ea1914c46a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5d6220270634dd8e2d15787d717020b8f6f86bb9
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67738335"
---
# <a name="icordebugcreateprocess-method"></a>ICorDebug::CreateProcess 메서드
디버거의 제어 기본 스레드 및 프로세스를 시작합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CreateProcess (  
    [in]  LPCWSTR                     lpApplicationName,  
    [in]  LPWSTR                      lpCommandLine,  
    [in]  LPSECURITY_ATTRIBUTES       lpProcessAttributes,  
    [in]  LPSECURITY_ATTRIBUTES       lpThreadAttributes,  
    [in]  BOOL                        bInheritHandles,  
    [in]  DWORD                       dwCreationFlags,  
    [in]  PVOID                       lpEnvironment,  
    [in]  LPCWSTR                     lpCurrentDirectory,  
    [in]  LPSTARTUPINFOW              lpStartupInfo,  
    [in]  LPPROCESS_INFORMATION       lpProcessInformation,  
    [in]  CorDebugCreateProcessFlags  debuggingFlags,  
    [out] ICorDebugProcess            **ppProcess  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `lpApplicationName`  
 [in] 시작된 프로세스에서 실행 될 모듈을 지정 하는 null로 끝나는 문자열에 대 한 포인터입니다. 모듈 호출 프로세스의 보안 컨텍스트에서 실행 됩니다.  
  
 `lpCommandLine`  
 [in] 시작된 프로세스에서 실행할 명령줄을 지정 하는 null로 끝나는 문자열에 대 한 포인터입니다. 응용 프로그램 이름 (예: "SomeApp.exe")는 첫 번째 인수 여야 합니다.  
  
 `lpProcessAttributes`  
 [in] Win32에 대 한 포인터 `SECURITY_ATTRIBUTES` 프로세스에 대 한 보안 설명자를 지정 하는 구조입니다. 경우 `lpProcessAttributes` 가 null 인 프로세스는 기본 보안 설명자를 가져옵니다.  
  
 `lpThreadAttributes`  
 [in] Win32에 대 한 포인터 `SECURITY_ATTRIBUTES` 프로세스의 주 스레드에 대 한 보안 설명자를 지정 하는 구조입니다. 경우 `lpThreadAttributes` 가 null 이면 스레드는 기본 보안 설명자를 가져옵니다.  
  
 `bInheritHandles`  
 [in] 로 `true` 호출 프로세스에 상속할 수 있는 각 핸들 시작된 프로세스를 통해 상속 되었음을 나타내기 위해 또는 `false` 핸들이 상속 되지 않습니다 나타냅니다. 상속 된 핸들에는 원래 핸들을 동일한 값 및 액세스 권한을 갖습니다.  
  
 `dwCreationFlags`  
 [in] 비트 조합 합니다 [Win32 프로세스 생성 플래그가](https://go.microsoft.com/fwlink/?linkid=69981) 우선 순위 클래스 및 시작된 프로세스의 동작을 제어 하 합니다.  
  
 `lpEnvironment`  
 [in] 새 프로세스에 대 한 환경 블록에 대 한 포인터입니다.  
  
 `lpCurrentDirectory`  
 [in] 프로세스에 대 한 현재 디렉터리에 전체 경로 지정 하는 null로 끝나는 문자열에 대 한 포인터입니다. 이 매개 변수가 null 이면 새 프로세스 호출 프로세스와 같은 현재 드라이브 및 디렉터리 포함 됩니다.  
  
 `lpStartupInfo`  
 [in] Win32에 대 한 포인터 `STARTUPINFOW` 윈도우 스테이션, 데스크톱, 표준 핸들 및 시작된 프로세스에 대 한 주 창의 모양을 지정 하는 구조입니다.  
  
 `lpProcessInformation`  
 [in] Win32에 대 한 포인터 `PROCESS_INFORMATION` 시작 될 프로세스에 대 한 식별 정보를 지정 하는 구조입니다.  
  
 `debuggingFlags`  
 [in] 디버깅 옵션을 지정 하는 CorDebugCreateProcessFlags 열거형의 값입니다.  
  
 `ppProcess`  
 [out] 프로세스를 나타내는 ICorDebugProcess 개체의 주소에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 이 메서드의 매개 변수는 Win32의 것과 동일 `CreateProcess` 메서드.  
  
 관리 되지 않는 혼합 모드 디버깅을 사용 하려면 `dwCreationFlags` DEBUG_PROCESS를 &#124; DEBUG_ONLY_THIS_PROCESS 합니다. 관리 되는 디버깅만 사용 하려는 경우에 이러한 플래그를 설정 하지 마십시오.  
  
 디버거 및 프로세스를 디버그 (연결 된 프로세스) 하는 경우 단일 콘솔 인 공유 하는 경우 사용 되는 interop 디버깅, 콘솔 잠금을 보유 하 고 디버그 이벤트에서 중지 하는 연결 된 프로세스 수입니다. 디버거는 다음 콘솔을 사용 하려는 모든 시도 차단 합니다. 이 문제를 방지 하려면에서 CREATE_NEW_CONSOLE 플래그를 설정 합니다 `dwCreationFlags` 매개 변수입니다.  
  
 Interop 디버깅 IA-64 기반 및 AMD64 기반 플랫폼 등 Win9x 및 x86이 아닌 플랫폼에서 지원 되지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebug 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)
