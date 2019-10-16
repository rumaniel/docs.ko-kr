---
title: CreateVersionStringFromModule 함수
ms.date: 03/30/2017
api_name:
- CreateVersionStringFromModule
api_location:
- dbgshim.dll
api_type:
- COM
f1_keywords:
- CreateVersionStringFromModule
helpviewer_keywords:
- debugging API [Silverlight]
- Silverlight, debugging
- CreateVersionStringFromModule function
ms.assetid: 3d2fe9bd-75ef-4364-84a6-da1e1994ac1a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b68624b962ed610dbeecd3e4cead769ab1400f4a
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67739215"
---
# <a name="createversionstringfrommodule-function"></a>CreateVersionStringFromModule 함수
대상 프로세스의 CLR(공용 언어 런타임) 경로에서 버전 문자열을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CreateVersionStringFromModule (  
    [in]  DWORD      pidDebuggee,  
    [in]  LPCWSTR    szModuleName,  
    [out, size_is(cchBuffer),  
          length_is(*pdwLength)] LPWSTR Buffer,  
    [in]  DWORD      cchBuffer,  
    [out] DWORD*     pdwLength  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pidDebuggee`  
 [in] 대상 CLR이 로드되는 프로세스의 식별자입니다.  
  
 `szModuleName`  
 [in] 프로세스에서 로드된 대상 CLR의 전체 경로 또는 상대 경로입니다.  
  
 `pBuffer`  
 [out] 대상 CLR에 대한 버전 문자열을 저장하기 위한 버퍼를 반환합니다.  
  
 `cchBuffer`  
 [in] `pBuffer`의 크기입니다.  
  
 `pdwLength`  
 [out] `pBuffer`에서 반환된 버전 문자열의 길이입니다.  
  
## <a name="return-value"></a>반환 값  
 S_OK  
 `pBuffer`에 반환된 대상 CLR에 대한 버전 문자열입니다.  
  
 E_INVALIDARG  
 `szModuleName`이 null이거나 `pBuffer` 또는 `cchBuffer`가 null입니다. `pBuffer` 및 `cchBuffer`는 둘 다 null이거나 null이 아니어야 합니다.  
  
 HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)  
 `pdwLength`가 `cchBuffer`보다 큰 경우 이는 `pBuffer` 및 `cchBuffer` 둘 다에 대해 null을 전달하고 `pdwLength`를 사용하여 필요한 버퍼 크기를 쿼리한 경우의 예상 결과일 수 있습니다.  
  
 HRESULT_FROM_WIN32(ERROR_MOD_NOT_FOUND)  
 `szModuleName`이 대상 프로세스의 유효한 CLR에 대한 경로를 포함하지 않습니다.  
  
 E_FAIL(또는 다른 E_ 반환 코드)  
 `pidDebuggee`가 유효한 프로세스 또는 다른 실패를 참조하지 않습니다.  
  
## <a name="remarks"></a>설명  
 이 함수는 `pidDebuggee`로 식별된 CLR 프로세스 및 `szModuleName`으로 지정된 문자열 경로를 수락합니다. `pBuffer`가 가리키는 버퍼에 버전 문자열이 반환됩니다. 이 문자열은 함수 사용자에게 불투명합니다. 즉, 버전 문자열 자체에는 내포된 의미가 없습니다. 이 함수의 컨텍스트에서 되 고 [CreateDebuggingInterfaceFromVersion 함수](../../../../docs/framework/unmanaged-api/debugging/createdebugginginterfacefromversion-function-for-silverlight.md)합니다.  
  
 이 함수는 두 번 호출해야 합니다. 처음 호출할 때는 `pBuffer` 및 `cchBuffer` 둘 다에 대해 null을 전달합니다. 이렇게 하면 `pBuffer`에 필요한 버퍼의 크기가 `pdwLength`에 반환됩니다. 그런 다음 두 번째로 함수를 호출하고 버퍼에 `pBuffer`에, 해당 크기를 `cchBuffer`에 전달할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** dbgshim.h  
  
 **라이브러리:** dbgshim.dll  
  
 **.NET framework 버전:** 3.5 SP1
