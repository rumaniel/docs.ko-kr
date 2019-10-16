---
title: GetRequestedRuntimeInfo 함수
ms.date: 03/30/2017
api_name:
- GetRequestedRuntimeInfo
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- GetRequestedRuntimeInfo
helpviewer_keywords:
- GetRequestedRuntimeInfo function [.NET Framework hosting]
ms.assetid: 0dfd7cdc-c116-4e25-b56a-ac7b0378c942
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 62a6f6d6e73ce42c8c86d4e458322e5bd361f412
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67778133"
---
# <a name="getrequestedruntimeinfo-function"></a>GetRequestedRuntimeInfo 함수
버전 및 디렉터리는 CLR (공용 언어 런타임) 응용 프로그램에서 요청한 정보를 가져옵니다.  
  
 .NET Framework 4에서이 함수에 사용 되지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetRequestedRuntimeInfo (  
    [in]  LPCWSTR  pExe,   
    [in]  LPCWSTR  pwszVersion,   
    [in]  LPCWSTR  pConfigurationFile,   
    [in]  DWORD    startupFlags,   
    [in]  DWORD    runtimeInfoFlags,   
    [out] LPWSTR   pDirectory,   
    [in]  DWORD    dwDirectory,   
    [out] DWORD   *dwDirectoryLength,   
    [out] LPWSTR   pVersion,   
    [in]  DWORD    cchBuffer,   
    [out] DWORD   *dwlength  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pExe`  
 [in] 응용 프로그램의 이름입니다.  
  
 `pwszVersion`  
 [in] 런타임의 버전 번호를 지정 하는 문자열입니다.  
  
 `pConfigurationFile`  
 [in] 연결 된 구성 파일의 이름을 `pExe`입니다.  
  
 `startupFlags`  
 [in] 하나 이상의 합니다 [STARTUP_FLAGS](../../../../docs/framework/unmanaged-api/hosting/startup-flags-enumeration.md) 열거형 값입니다.  
  
 `runtimeInfoFlags`  
 [in] 하나 이상의 합니다 [RUNTIME_INFO_FLAGS](../../../../docs/framework/unmanaged-api/hosting/runtime-info-flags-enumeration.md) 열거형 값입니다.  
  
 `pDirectory`  
 [out] 완료 되 면 런타임에 대 한 디렉터리 경로 포함 하는 버퍼입니다.  
  
 `dwDirectory`  
 [in] Directory 버퍼의 길이입니다.  
  
 `dwDirectoryLength`  
 [out] 디렉터리 경로 문자열의 길이에 대 한 포인터입니다.  
  
 `pVersion`  
 [out] 성공적으로 완료 되는 런타임의 버전 번호를 포함 하는 버퍼입니다.  
  
 `cchBuffer`  
 [in] 버전 문자열 버퍼의 길이입니다.  
  
 `dwlength`  
 [out] 버전 문자열의 길이에 대 한 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음 값 외에도 WinError.h에 정의 된 대로 표준 구성 요소 개체 모델 (COM) 오류 코드를 반환 합니다.  
  
|반환 코드|Description|  
|-----------------|-----------------|  
|S_OK|메서드가 완료되었습니다.|  
|ERROR_INSUFFICIENT_BUFFER|디렉터리 버퍼가 디렉터리 경로 저장 하기에 충분 하지 않습니다.<br /><br /> -또는-<br /><br /> 버전 버퍼의 버전 문자열을 저장할 만큼 크지 않습니다.|  
  
## <a name="remarks"></a>설명  
 `GetRequestedRuntimeInfo` 메서드 최신 컴퓨터에 설치할 필요가 없는 프로세스에 로드 된 버전에 대 한 런타임 정보를 반환 합니다.  
  
 .NET framework 버전 2.0에서 사용 하 여 최신 버전에 대 한 정보를 얻을 수는 `GetRequestedRuntimeInfo` 같이 메서드:  
  
- 지정 된 `pExe`, `pwszVersion`, 및 `pConfigurationFile` 매개 변수를 null로 합니다.  
  
- RUNTIME_INFO_UPGRADE_VERSION 플래그를 지정 합니다 `RUNTIME_INFO_FLAGS` 열거형을 `runtimeInfoFlags` 매개 변수.  
  
 `GetRequestedRuntimeInfo` 메서드는 다음과 같은 상황에서 최신 CLR 버전을 반환 하지 않습니다.  
  
- 특정 CLR 버전을 로드 하도록 지정 하는 응용 프로그램 구성 파일에 있습니다. .NET Framework를 사용 하 여 구성 파일에 대 한 null을 지정 하는 경우에는 `pConfigurationFile` 매개 변수입니다.  
  
- 합니다 [CorBindToRuntimeEx](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md) 이전 버전의 CLR 지정 메서드가 호출 되었습니다.  
  
- 이전 버전의 CLR에 대해 컴파일된 응용 프로그램 실행 중입니다.  
  
 에 대 한 합니다 `runtimeInfoFlags` 매개 변수를 지정할 수 있습니다만 아키텍처 상수 중 하나는 `RUNTIME_INFO_FLAGS` 번 열거형:  
  
- RUNTIME_INFO_REQUEST_IA64  
  
- RUNTIME_INFO_REQUEST_AMD64  
  
- RUNTIME_INFO_REQUEST_X86  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [GetRequestedRuntimeVersion 함수](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeversion-function.md)
- [GetVersionFromProcess 함수](../../../../docs/framework/unmanaged-api/hosting/getversionfromprocess-function.md)
- [사용되지 않는 CLR 호스팅 함수](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
