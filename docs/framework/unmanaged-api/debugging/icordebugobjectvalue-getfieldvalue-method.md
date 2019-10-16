---
title: ICorDebugObjectValue::GetFieldValue 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugObjectValue.GetFieldValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugObjectValue::GetFieldValue
helpviewer_keywords:
- ICorDebugObjectValue::GetFieldValue method [.NET Framework debugging]
- GetFieldValue method [.NET Framework debugging]
ms.assetid: c96770b0-3e09-47bb-bd29-20353b043459
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0fc65f5b55082970a0cd59a6850aaaa6779d0821
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67766414"
---
# <a name="icordebugobjectvaluegetfieldvalue-method"></a>ICorDebugObjectValue::GetFieldValue 메서드
이 개체 값에 대해 지정된 된 클래스의 지정된 된 필드의 값을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetFieldValue (  
    [in]  ICorDebugClass     *pClass,  
    [in]  mdFieldDef         fieldDef,  
    [out] ICorDebugValue     **ppValue  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pClass`  
 [in] 필드 값을 검색할 원본에 대 한 클래스를 나타내는 "ICorDebugClass" 개체에 대 한 포인터입니다.  
  
 `fieldDef`  
 [in] `mdFieldDef` 필드를 설명 하는 메타 데이터를 참조 하는 토큰입니다.  
  
 `ppValue`  
 [out] 지정된 된 필드의 값을 나타내는 "ICorDebugValue" 개체에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 에 지정 된 클래스는 `pClass` 매개 변수는 개체 값의 클래스 계층 구조에서 이어야 하며 필드에는 해당 클래스의 필드 여야 합니다.  
  
 `GetFieldValue` 메서드는 제네릭 클래스 및 제네릭 개체에 대 한 실패 하지 것입니다. 예를 들어 경우 MyDictionary\<V > 사전에서 상속\<문자열, V >, MyDictionary 형식의 개체 값 이며\<int32 > 전달 합니다 `ICorDebugClass` 사전에 대 한 개체\<K, V > 됩니다 사전의 필드를 정상적으로 가져옴\<string, int32 >.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료
