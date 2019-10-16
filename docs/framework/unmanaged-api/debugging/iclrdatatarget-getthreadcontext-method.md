---
title: ICLRDataTarget::GetThreadContext 메서드
ms.date: 03/30/2017
api_name:
- ICLRDataTarget.GetThreadContext
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget::GetThreadContext
helpviewer_keywords:
- ICLRDataTarget::GetThreadContext method [.NET Framework debugging]
- GetThreadContext method, ICLRDataTarget interface [.NET Framework debugging]
ms.assetid: b9d8c3b5-3a2e-4225-95d4-dd052c4532c3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1492c6d72d68a95a79925d7789a710b5b5ed14b1
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67738711"
---
# <a name="iclrdatatargetgetthreadcontext-method"></a>ICLRDataTarget::GetThreadContext 메서드
대상 프로세스에서 지정 된 스레드에 대해 현재 실행 컨텍스트를 가져옵니다. 이 메서드는 공용 언어 런타임 데이터 액세스 서비스에서 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetThreadContext (  
    [in] ULONG32            threadID,  
    [in] ULONG32            contextFlags,  
    [in] ULONG32            contextSize,  
    [out, size_is(contextSize)]   
        BYTE                *context  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `threadID`  
 [in] 대상 프로세스에서 스레드의 운영 체제 식별자입니다.  
  
 `contextFlags`  
 [in] 반환할 컨텍스트 부분을 지정 하는 플래그입니다. 구현은 컨텍스트 최소한 이러한 부분을 반환 합니다.  
  
 `contextSize`  
 [in] 컨텍스트 크기입니다.  
  
 `context`  
 [out] 컨텍스트를 버퍼에 대 한 포인터입니다.  
  
 데이터를 `context` 버퍼 Win32의 형식 이어야 합니다 `CONTEXT` 구조입니다. 컨텍스트 프로세서별 등록 데이터를 지정 하므로 Win32 정의 `CONTEXT` 구조는 프로세서 아키텍처에 따라 달라 집니다. Win32의 정의 대 한 WinNT.h 헤더 파일 참조 `CONTEXT` 구조입니다.  
  
## <a name="remarks"></a>설명  
 이 메서드는 디버깅 애플리케이션의 작성자가 구현합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** ClrData.idl, ClrData.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRDataTarget 인터페이스](../../../../docs/framework/unmanaged-api/debugging/iclrdatatarget-interface.md)
