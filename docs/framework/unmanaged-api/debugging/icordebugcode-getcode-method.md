---
title: ICorDebugCode::GetCode 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugCode.GetCode
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode::GetCode
helpviewer_keywords:
- ICorDebugCode::GetCode method [.NET Framework debugging]
- GetCode method, ICorDebugCode interface [.NET Framework debugging]
ms.assetid: 7137e3d1-1dad-48d8-8c37-16ac816534d3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e18097dd380ee354e5652886544d40da074f1230
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67747630"
---
# <a name="icordebugcodegetcode-method"></a>ICorDebugCode::GetCode 메서드
디스어셈블리에 대 한 형식이 지정된 된 함수에 대 한 모든 코드를 가져옵니다. 이 메서드는.NET Framework 버전 2.0에서에서 더 이상 사용 되지 되었습니다. 사용 하 여 [ICorDebugCode2::GetCodeChunks](../../../../docs/framework/unmanaged-api/debugging/icordebugcode2-getcodechunks-method.md) 대신 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetCode (  
    [in] ULONG32     startOffset,   
    [in] ULONG32     endOffset,  
    [in] ULONG32     cBufferAlloc,  
    [out, size_is(cBufferAlloc),  
        length_is(*pcBufferSize)] BYTE buffer[],  
    [out] ULONG32    *pcBufferSize  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `startOffset`  
 [in] 오프셋은 함수의 시작 부분입니다.  
  
 `endOffset`  
 [in] 함수 끝의 오프셋입니다.  
  
 `cBufferAlloc`  
 [in] 크기는 `buffer` 에 코드가 반환 되는 배열입니다.  
  
 `buffer`  
 [out] 코드가 반환 되는 배열입니다.  
  
 `pcBufferSize`  
 [out] 반환 된 바이트 수입니다.  
  
## <a name="remarks"></a>설명  
 함수 코드에 여러 개의 청크로 나뉘어, 네이티브 오프셋을 증가 하는 순서에 연결 되며 됩니다. 명령 경계 확인 하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET framework 버전:** 1.1, 1.0  
  
## <a name="see-also"></a>참고자료

- [GetCodeChunks 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugcode2-getcodechunks-method.md)
