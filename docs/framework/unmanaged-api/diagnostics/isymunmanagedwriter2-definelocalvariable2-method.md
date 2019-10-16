---
title: ISymUnmanagedWriter2::DefineLocalVariable2 메서드
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter2.DefineLocalVariable2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter2::DefineLocalVariable2
helpviewer_keywords:
- ISymUnmanagedWriter2::DefineLocalVariable2 method [.NET Framework debugging]
- DefineLocalVariable2 method [.NET Framework debugging]
ms.assetid: e774eefe-858c-4362-8d2d-28ebf2ba1a24
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8fa385805d3e2dca8fef3e1490b2c67dd0583373
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67755059"
---
# <a name="isymunmanagedwriter2definelocalvariable2-method"></a>ISymUnmanagedWriter2::DefineLocalVariable2 메서드
현재 어휘 범위에 단일 변수를 정의합니다. 이 메서드는 다중 홈을 범위에 걸쳐 있는 동일한 이름의 변수에 대 한 여러 번 호출할 수 있습니다. 그러나이 경우,:의 값을 `startOffset` 및 `endOffset` 매개 변수는 겹치지 않아야 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT DefineLocalVariable2(  
    [in] const WCHAR  *name,  
    [in] ULONG32      attributes,  
    [in] mdSignature  sigToken,  
    [in] ULONG32      addrKind,  
    [in] ULONG32      addr1,  
    [in] ULONG32      addr2,  
    [in] ULONG32      addr3,  
    [in] ULONG32      startOffset,  
    [in] ULONG32      endOffset);  
```  
  
## <a name="parameters"></a>매개 변수  
 `name`  
 [in] 로컬 변수 이름입니다.  
  
 `attributes`  
 [in] 로컬 변수 특성입니다.  
  
 `sigToken`  
 [in] 서명의 메타 데이터 토큰입니다.  
  
 `addrKind`  
 [in] 주소 유형입니다.  
  
 `addr1`  
 [in] 매개 변수 사양에 대 한 첫 번째 주소입니다.  
  
 `addr2`  
 [in] 매개 변수 사양에 대 한 두 번째 주소입니다.  
  
 `addr3`  
 [in] 매개 변수 사양의 세 번째 주소입니다.  
  
 `startOffset`  
 [in] 변수의 시작 오프셋입니다. 이 매개 변수는 선택 사항입니다. 0 인 경우이 매개 변수가 무시 되 고 변수가 전체 범위에서 정의 됩니다. 0이 아닌 값 이면 현재 범위의 오프셋 내에 변수가 포함 됩니다.  
  
 `endOffset`  
 [in] 변수의 끝 오프셋입니다. 이 매개 변수는 선택 사항입니다. 0 인 경우이 매개 변수가 무시 되 고 변수가 전체 범위에서 정의 됩니다. 0이 아닌 값 이면 현재 범위의 오프셋 내에 변수가 포함 됩니다.  
  
## <a name="return-value"></a>반환 값  
 메서드가 성공 하면 s_ok이 고 그렇지 않으면 E_FAIL 또는 일부 다른 오류 코드입니다.  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** CorSym.idl  
  
## <a name="see-also"></a>참고자료

- [ISymUnmanagedWriter2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter2-interface.md)
- [DefineLocalVariable 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-definelocalvariable-method.md)
