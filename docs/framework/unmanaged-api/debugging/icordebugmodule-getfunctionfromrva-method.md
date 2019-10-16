---
title: ICorDebugModule::GetFunctionFromRVA 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugModule.GetFunctionFromRVA
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule::GetFunctionFromRVA
helpviewer_keywords:
- GetFunctionFromRVA method [.NET Framework debugging]
- ICorDebugModule::GetFunctionFromRVA method [.NET Framework debugging]
ms.assetid: f5a34517-2422-484f-be89-2ce0b4bce195
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0ab8d56a457db0a70b47293684f0de73ce9ff5f4
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67763366"
---
# <a name="icordebugmodulegetfunctionfromrva-method"></a>ICorDebugModule::GetFunctionFromRVA 메서드
이 메서드는 현재 버전의.NET Framework에서 구현 되지에.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetFunctionFromRVA(  
    [in]  CORDB_ADDRESS      rva,  
    [out] ICorDebugFunction  **ppFunction  
);  
```  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** CorDebug.idl, CorDebug.h  
  
## <a name="see-also"></a>참고자료
