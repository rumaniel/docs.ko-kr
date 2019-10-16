---
title: ICorDebugClass2::GetParameterizedType 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugClass2.GetParameterizedType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugClass2::GetParameterizedType
helpviewer_keywords:
- GetParameterizedType method [.NET Framework debugging]
- ICorDebugClass2::GetParameterizedType method [.NET Framework debugging]
ms.assetid: 94b591c4-9302-4af2-a510-089496afb036
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1bfc503bfc2b278d7a7344b94cb089cd8e019890
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67747769"
---
# <a name="icordebugclass2getparameterizedtype-method"></a>ICorDebugClass2::GetParameterizedType 메서드
이 클래스에 대 한 형식 선언을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetParameterizedType (  
    [in] CorElementType                      elementType,  
    [in] ULONG32                             nTypeArgs,  
    [in, size_is(nTypeArgs)] ICorDebugType  *ppTypeArgs[],  
    [out] ICorDebugType                    **ppType  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `elementType`  
 [in] CorElementType 열거형이 클래스에 대 한 요소 유형을 지정 하는 값입니다. 이 ICorDebugClass2 값 형식을 나타내면 ELEMENT_TYPE_VALUETYPE로이 값을 설정 합니다. 이 경우이 값 ELEMENT_TYPE_CLASS로 `ICorDebugClass2` 복합 유형을 나타냅니다.  
  
 `nTypeArgs`  
 [in] 형식이 제네릭인 경우 형식 매개 변수의 수입니다. 형식 매개 변수 (있는 경우)의 수에는 클래스에 필요한 번호와 일치 해야 합니다.  
  
 `ppTypeArgs`  
 [in] 형식 매개 변수를 나타내는 ICorDebugType 개체를 가리키는 각각 포인터의 배열입니다. 클래스의 제네릭이 아닌 경우이 값은 null입니다.  
  
 `ppType`  
 [out] 주소에 대 한 포인터는 `ICorDebugType` 형식 선언을 나타내는 개체입니다. 이 개체는 해당 하는 <xref:System.Type> 관리 되는 코드의 개체입니다.  
  
## <a name="remarks"></a>설명  
 클래스는 제네릭이 아닌 즉, 형식 매개 변수가 없는 있으면 경우 `GetParameterizedType` 단순히 클래스에 해당 하는 런타임 형식 개체를 가져옵니다. `elementType` 클래스에 대 한 올바른 요소 형식으로 매개 변수를 설정 해야 합니다. 클래스는 값 형식; 변수 그렇지 않으면 ELEMENT_TYPE_CLASS 합니다.  
  
 클래스 형식 매개 변수를 허용 하는 경우 (예를 들어 `ArrayList<T>`)를 사용할 수 있습니다 `GetParameterizedType` 과 같은 인스턴스화된 형식에 대 한 형식 개체를 생성 하 `ArrayList<int>`합니다.  
  
## <a name="background-information"></a>배경 정보  
 .NET Framework 버전 1.0 및 1.1에서는 메타 데이터의 형식은 모두 실행 중인 프로세스의 형식으로 직접 매핑할 수 없습니다. 따라서 메타 데이터 형식 및 런타임 형식에서 실행 중인 프로세스를 단일 표현을 했습니다. 그러나 메타 데이터에서 제네릭 형식 하나는 많은 여러 인스턴스에서 실행 중인 프로세스의 형식에 매핑할 수 있습니다. 예를 들어, 메타 데이터 형식 `SortedList<K,V>` 매핑할 수 있습니다 `SortedList<String, EmployeeRecord>`를 `SortedList<Int32, String>`, `SortedList<String,Array<Int32>>`등입니다. 따라서 형식 인스턴스화를 처리 하는 방법을 해야 합니다.  
  
 .NET Framework 버전 2.0에 도입 된 `ICorDebugType` 인터페이스입니다. 제네릭 형식에 대 한는 `ICorDebugClass` 하거나 `ICorDebugClass2` 개체가 인스턴스화되지 않은 형식을 나타내는 (`SortedList<K,V>`), 및 `ICorDebugType` 개체는 다양 한 인스턴스화된 형식을 나타냅니다. 지정 된는 `ICorDebugClass` 또는 `ICorDebugClass2` 개체를 만들 수 있습니다는 `ICorDebugType` 호출 하 여 모든 인스턴스화에 대 한 개체는 `ICorDebugClass2::GetParameterizedType` 메서드. 만들 수도 있습니다는 `ICorDebugType` Int32 등의 단순 형식 또는 제네릭이 아닌 형식에 대 한 개체입니다.  
  
 도입 된 `ICorDebugType` 형식의 런타임 개념을 나타내는 개체를 API 전반에 걸쳐 파급 효과가 있습니다. 이전에 함수는 `ICorDebugClass` 또는 `ICorDebugClass2` 개체 또는 심지어는 `CorElementType` 값이 사용 하도록 일반화 되었습니다는 `ICorDebugType` 개체입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
