---
title: ICorDebugType::GetStaticFieldValue 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugType.GetStaticFieldValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::GetStaticFieldValue
helpviewer_keywords:
- GetStaticFieldValue method, ICorDebugType interface [.NET Framework debugging]
- ICorDebugType::GetStaticFieldValue method [.NET Framework debugging]
ms.assetid: 62eb5d55-53ee-4fb3-8d47-7b6c96808f9e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1054c7c977a487bb5a4bbf464322a65bcc039608
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67755741"
---
# <a name="icordebugtypegetstaticfieldvalue-method"></a>ICorDebugType::GetStaticFieldValue 메서드
지정한 스택 프레임이 토큰 지정 된 필드에서 참조 하는 정적 필드의 값이 포함 된 ICorDebugValue 개체 인터페이스 포인터를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetStaticFieldValue (  
    [in]  mdFieldDef        fieldDef,  
    [in]  ICorDebugFrame    *pFrame,  
    [out] ICorDebugValue    **ppValue  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `fieldDef`  
 [in] `mdFieldDef` 정적 필드를 지정 하는 토큰입니다.  
  
 `pFrame`  
 [in] 스택 프레임을 나타내는 ICorDebugFrame 포인터입니다.  
  
 `ppValue`  
 [out] 주소에 대 한 포인터는 `ICorDebugValue` 정적 필드의 값이 들어 있는입니다.  
  
## <a name="remarks"></a>설명  
 합니다 `GetStaticFieldValue` 메서드에 사용할 수 형식이 ELEMENT_TYPE_CLASS 또는 ELEMENT_TYPE_VALUETYPE, 경우에 표시 된 대로 합니다 [icordebugtype:: Gettype](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-gettype-method.md) 메서드.  
  
 제네릭이 아닌 형식에 대 한 작업을 수행 하 여 `GetStaticFieldValue` 호출과 동일 [icordebugclass:: Getstaticfieldvalue](../../../../docs/framework/unmanaged-api/debugging/icordebugclass-getstaticfieldvalue-method.md) 반환한 ICorDebugClass 개체에서 [icordebugtype:: Getclass](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-getclass-method.md).  
  
 제네릭 형식의 정적 필드 값을 특정 인스턴스화를 상대적으로 지정 됩니다. 또한 정적 필드 스레드, 컨텍스트 또는 응용 프로그램 도메인을 기준으로 될 수, 하는 경우 다음 스택 프레임 데 도움이 됩니다 적절 한 값을 결정 하는 디버거.  
  
## <a name="remarks"></a>설명  
 `GetStaticFieldValue` 호출할 때에 사용할 수 있습니다 `ICorDebugType::GetType` ELEMENT_TYPE_CLASS 또는 ELEMENT_TYPE_VALUETYPE 값을 반환 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
