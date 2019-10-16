---
title: CloseCLREnumeration 함수
ms.date: 03/30/2017
api_name:
- CloseCLREnumeration
api_location:
- dbgshim.dll
api_type:
- COM
f1_keywords:
- CloseCLREnumeration
helpviewer_keywords:
- debugging API [Silverlight]
- Silverlight, debugging
- CloseCLR Enumeration function
ms.assetid: 5e3c3958-80bb-43b1-a96b-dd3e6dbd9cd7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3a05a779d4a56eb8f881da1824d5ffaa363b5a01
ms.sourcegitcommit: 3caa92cb97e9f6c31f21769c7a3f7c4304024b39
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71274277"
---
# <a name="closeclrenumeration-function"></a>CloseCLREnumeration 함수
[EnumerateCLRs 함수](enumerateclrs-function.md)에서 반환 된 핸들 배열에 있는 모든 유효한 CLR (공용 언어 런타임) 계속 시작 이벤트를 닫고 핸들 및 문자열 경로 배열에 대 한 메모리를 해제 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CloseCLREnumeration (  
    [in]  DWORD      pHandleArray,  
    [in]  LPWSTR**   pStringArray,  
    [in]  DWORD*     dwArrayLength  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pHandleArray`  
 진행 [EnumerateCLRs 함수](enumerateclrs-function.md)에서 반환 된 이벤트 핸들 배열에 대 한 포인터입니다.  
  
 `pStringArray`  
 진행 [EnumerateCLRs 함수](enumerateclrs-function.md)에서 반환 된 CLR 문자열 경로 배열에 대 한 포인터입니다.  
  
 `dwArrayLength`  
 [in] `pHandleArray` 또는 `pStringArray`의 크기(길이)를 포함하는 DWORD입니다(동일).  
  
## <a name="return-value"></a>반환 값  
 S_OK  
 [EnumerateCLRs 함수](enumerateclrs-function.md) 에 의해 열린 핸들이 닫히고 핸들 및 문자열 배열에 할당 된 메모리가 해제 됩니다.  
  
 E_INVALIDARG  
 `pHandleArray`의 길이가 `dwArrayLength`에 전달된 길이와 일치하지 않습니다.  
  
 E_FAIL(또는 다른 E_ 반환 코드)  
 함수가 `pHandleArray` 및 `pStringArray`에 대한 메모리를 해제할 수 없습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** dbgshim.dll  
  
 **라이브러리:** dbgshim.dll  
  
 **.NET Framework 버전:** 3.5 SP1
