---
title: ISymENCUnmanagedMethod::GetLineFromOffset 메서드
ms.date: 03/30/2017
api_name:
- ISymENCUnmanagedMethod.GetLineFromOffset
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymENCUnmanagedMethod::GetLineFromOffset
helpviewer_keywords:
- GetLineFromOffset method [.NET Framework debugging]
- ISymENCUnmanagedMethod::GetLineFromOffset method [.NET Framework debugging]
ms.assetid: cc09bad2-fb34-4d13-a521-6ec7b1a1d915
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b669921bf8d27283ba99f4ca1d97b6abc00e15db
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67776891"
---
# <a name="isymencunmanagedmethodgetlinefromoffset-method"></a>ISymENCUnmanagedMethod::GetLineFromOffset 메서드
오프셋을 사용 하 여 연결 된 줄 정보를 가져옵니다. 경우 offset 매개 변수 (`dwOffset`) 시퀀스 위치가 아닙니다.이 메서드는 이전 오프셋을 사용 하 여 연결 된 줄 정보를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetLineFromOffset(  
     [in]  ULONG32   dwOffset,  
     [out] ULONG32*  pline,  
     [out] ULONG32*  pcolumn,  
     [out] ULONG32*  pendLine,  
     [out] ULONG32*  pendColumn,  
     [out] ULONG32*  pdwStartOffset);  
```  
  
## <a name="parameters"></a>매개 변수  
 `dwOffset`  
 [in] `ULONG32` 오프셋을 포함 하는 합니다.  
  
 `pline`  
 [out] 에 대 한 포인터를 `ULONG32` 줄 받는입니다.  
  
 `pcolumn`  
 [out] 에 대 한 포인터를 `ULONG32` 을 받는 열입니다.  
  
 `pendLine`  
 [out] 에 대 한 포인터를 `ULONG32` 줄 끝을 받는입니다.  
  
 `pendColumn`  
 [out] 에 대 한 포인터를 `ULONG32` 끝 열을 받는입니다.  
  
 `pdwStartOffset`  
 [out] 에 대 한 포인터를 `ULONG32` 연결된 시퀀스 위치를 받는입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드가 성공 하면 s_ok이 고 그렇지 않으면 E_FAIL 또는 일부 다른 오류 코드입니다.  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** CorSym.idl, CorSym.h  
  
## <a name="see-also"></a>참고자료

- [ISymENCUnmanagedMethod 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymencunmanagedmethod-interface.md)
