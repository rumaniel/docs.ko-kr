---
title: ICorDebugAppDomain::GetName 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain.GetName
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain::GetName
helpviewer_keywords:
- ICorDebugAppDomain::GetName method [.NET Framework debugging]
- GetName method, ICorDebugAppDomain interface [.NET Framework debugging]
ms.assetid: 02c596d7-00b0-4e2c-856b-5425158fcefd
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 535d94688d02a7315529d17fae555fba457bbb86
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67737875"
---
# <a name="icordebugappdomaingetname-method"></a>ICorDebugAppDomain::GetName 메서드
응용 프로그램 도메인의 이름을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetName (  
    [in]  ULONG32           cchName,  
    [out] ULONG32           *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]   
         WCHAR              szName[]  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `cchName`  
 [in] `szName` 배열의 크기입니다. 쿼리 모드에서이 메서드를 삽입할 0으로이 값을 설정 합니다.  
  
 `pcchName`  
 [out] 이름 또는에 실제로 반환 된 문자 수의 크기에 대 한 포인터 `szName`합니다. 이 값을 버퍼의 크기를 알고 있어야 호출자에 게 사용 하면 쿼리 모드에서 이름에 할당할 수 있습니다.  
  
 `szName`  
 [out] 응용 프로그램 도메인의 이름을 저장 하는 배열입니다.  
  
## <a name="remarks"></a>설명  
 디버거를 호출 합니다 `GetName` 메서드를 한 번 이름에 필요한 버퍼의 크기를 가져옵니다. 디버거는 버퍼를 할당 하 고 메서드를 호출 하는 두 번째 시간에 버퍼를 채웁니다. 이름, 크기를 가져오는 첫 번째 호출 이라고 *쿼리 모드*합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
