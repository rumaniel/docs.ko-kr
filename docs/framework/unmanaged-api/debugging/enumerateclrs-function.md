---
title: EnumerateCLRs 함수
ms.date: 03/30/2017
api_name:
- EnumerateCLRs
api_location:
- dbgshim.dll
api_type:
- COM
f1_keywords:
- EnumerateCLRs
helpviewer_keywords:
- debugging API [Silverlight]
- Silverlight, debugging
- EnumerateCLRs function
ms.assetid: f8d50cb3-ec4f-4529-8fe3-bd61fd28e13c
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ae668a40ba1510e0e3d4f509643022ebe822a4f0
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67738944"
---
# <a name="enumerateclrs-function"></a>EnumerateCLRs 함수
프로세스의 CLR을 열거하기 위한 메커니즘을 제공합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT EnumerateCLRs (  
    [in]  DWORD      debuggeePID,  
    [out] HANDLE**   ppHandleArrayOut,  
    [out] LPWSTR**   ppStringArrayOut,  
    [out] DWORD*     pdwArrayLengthOut  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `debuggeePID`  
 [in] 로드된 CLR이 열거되는 소스 프로세스의 프로세스 식별자입니다.  
  
 `ppHandleArrayOut`  
 [out] CLR 시작을 계속하는 데 사용되는 이벤트 핸들이 포함된 배열에 대한 포인터입니다. 배열의 각 핸들이 유효한지는 보장되지 않습니다. 유효하면 핸들이 `ppStringArrayOut`의 같은 인덱스에 있는 해당 런타임에 대한 계속-시작 이벤트로 사용됩니다.  
  
 `ppStringArrayOut`  
 [out] 프로세스에 로드된 CLR의 전체 경로를 지정하는 문자열 배열에 대한 포인터입니다.  
  
 `pdwArrayLengthOut`  
 [out] 크기가 같은 `ppHandleArrayOut` 및 `pdwArrayLengthOut`의 길이가 포함된 DWORD에 대한 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
 S_OK  
 프로세스의 CLR 수가 성공적으로 확인되었으며 해당 핸들 및 경로 배열이 제대로 채워졌습니다.  
  
 E_INVALIDARG  
 `ppHandleArrayOut` 또는 `ppStringArrayOut`이 null이거나 `pdwArrayLengthOut`이 null입니다.  
  
 E_OUTOFMEMORY  
 함수에서 핸들 및 경로 배열에 충분한 메모리를 할당할 수 없습니다.  
  
 E_FAIL(또는 다른 E_ 반환 코드)  
 로드된 CLR을 열거할 수 없습니다.  
  
## <a name="remarks"></a>설명  
 `debuggeePID`로 식별되는 대상 프로세스의 경우 함수에서는 프로세스에 로드된 CLR의 경로 배열 `ppStringArrayOut`, 같은 인덱스에서 CLR에 대한 계속-시작 이벤트가 포함될 수 있는 이벤트 핸들 배열 `ppHandleArrayOut`, 로드된 CLR 수를 지정하는 배열 크기 `pdwArrayLengthOut`을 반환합니다.  
  
 Windows 운영 체제에서 `debuggeePID`는 OS 프로세스 식별자에 매핑됩니다.  
  
 `ppHandleArrayOut` 및 `ppStringArrayOut`용 메모리는 이 함수를 통해 할당됩니다. 할당 된 메모리를 확보 하기 위해 호출 해야 합니다 [CloseCLREnumeration 함수](../../../../docs/framework/unmanaged-api/debugging/closeclrenumeration-function.md)합니다.  
  
 대상 프로세스의 CLR 개수를 반환하려면 null로 설정된 두 배열 매개 변수와 함께 이 함수를 호출하면 됩니다. 이 개수에서 호출자는 만들어질 버퍼 크기를 유추할 수 있습니다. `(sizeof(HANDLE) * count) + (sizeof(LPWSTR) * count) + (sizeof(WCHAR*) * count * MAX_PATH)`.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** dbgshim.h  
  
 **라이브러리:** dbgshim.dll  
  
 **.NET framework 버전:** 3.5 SP1
