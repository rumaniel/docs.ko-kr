---
title: ISymUnmanagedWriter::SetScopeRange 메서드
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.SetScopeRange
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::SetScopeRange
helpviewer_keywords:
- SetScopeRange method [.NET Framework debugging]
- ISymUnmanagedWriter::SetScopeRange method [.NET Framework debugging]
ms.assetid: d4d98676-444b-46ca-bfe6-0d827385cd22
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c13eb7ca16cdb7c70f3fef0dd4efcb9362cd3d87
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67776588"
---
# <a name="isymunmanagedwritersetscoperange-method"></a>ISymUnmanagedWriter::SetScopeRange 메서드
지정된 어휘 범위에 대한 오프셋 범위를 정의합니다. 범위는 현재 범위가 새 하 고 범위 스택에 푸시됩니다. 범위 계층 구조를 형성 해야 합니다. 형제 겹칠 수 없습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT OpenScope(  
    [in] ULONG32  scopeID,  
    [in] ULONG32  startOffset,  
    [in] ULONG32  endOffset);  
```  
  
## <a name="parameters"></a>매개 변수  
 `scopeId`  
 [in] 범위에 대 한 범위 식별자입니다.  
  
 `startOffset`  
 [in] 메서드의 시작 부분에서 어휘 범위에서 첫 번째 명령의 바이트 오프셋입니다.  
  
 `endOffset`  
 [in] 메서드의 시작 부분에서 어휘 범위에서 마지막 명령의 바이트 오프셋입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드가 성공 하면 s_ok이 고 그렇지 않으면 E_FAIL 또는 일부 다른 오류 코드입니다.  
  
## <a name="remarks"></a>설명  
 [Isymunmanagedwriter:: Openscope](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-openscope-method.md) 사용 하 여 사용할 수 있는 불투명 한 범위 식별자를 반환 합니다 `ISymUnmanagedWriter::SetScopeRange` 범위를 정의 하의 시작과 끝 이후에 오프셋입니다. 이 경우에 전달 된 오프셋 `ISymUnmanagedWriter::OpenScope` 하 고 [isymunmanagedwriter:: Closescope](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-closescope-method.md) 무시 됩니다. 범위 식별자 현재 메서드에서만에서 유효합니다.  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** CorSym.idl, CorSym.h  
  
## <a name="see-also"></a>참고자료

- [ISymUnmanagedWriter 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-interface.md)
