---
title: ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain3.GetCachedWinRTTypesForIIDs
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs
helpviewer_keywords:
- ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs method, [.NET Framework debugging]
- GetCachedWinRTTypesForIIDs method, ICorDebugAppDomain3 interface [.NET Framework debugging]
ms.assetid: 23682ca0-1bcf-48e6-996e-69f7ba337682
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6ef8d1c47275d3cbd69c1516b788b950f8535513
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67737722"
---
# <a name="icordebugappdomain3getcachedwinrttypesforiids-method"></a>ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs 메서드
해당 인터페이스 식별자에 따라 응용 프로그램 도메인에서 캐시 된 Windows 런타임 형식에 대 한 열거자를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetCachedWinRTTypesForIIDs (   
    [in]  ULONG32            cReqTypes,  
    [in]  GUID                *iidsToResolve,  
    [out] ICorDebugTypeEnum   **ppTypesEnum  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `cReqTypes`  
 [in] 필요한 형식의 수입니다.  
  
 `iidsToResolve`  
 [in] 검색할 Windows 런타임 형식의 관리 되는 표현에 해당 하는 인터페이스 식별자를 포함 하는 배열에 대 한 포인터입니다.  
  
 `ppTypesEnum`  
 [out] Windows 런타임 형식의 관리 되는 캐시 된 표현을 열거형을 허용 하는 "ICorDebugTypeEnum" 인터페이스 개체의 주소에 대 한 포인터를 기반으로 검색의 인터페이스 식별자 `iidsToResolve`합니다.  
  
## <a name="remarks"></a>설명  
 메서드를 특정 인터페이스 식별자에 대 한 정보를 검색 하지 못하는 경우 "ICorDebugTypeEnum" 컬렉션의 해당 항목은 형식이 `ELEMENT_TYPE_END` 데이터 검색 문제로 인해 오류 또는 `ELEMENT_TYPE_VOID` 알 수 없는 인터페이스에 대 한 식별자입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** Windows 런타임  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebugAppDomain3 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain3-interface.md)
