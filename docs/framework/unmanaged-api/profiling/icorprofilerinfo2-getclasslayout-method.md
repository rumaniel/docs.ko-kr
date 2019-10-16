---
title: ICorProfilerInfo2::GetClassLayout 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetClassLayout
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetClassLayout
helpviewer_keywords:
- ICorProfilerInfo2::GetClassLayout method [.NET Framework profiling]
- GetClassLayout method, ICorProfilerInfo2 interface [.NET Framework profiling]
ms.assetid: a3a36987-5666-4e2f-95b5-d0cb246502ec
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b5cec1022c9d4a2c96e4216aa09d4c0f7795b4f8
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67751817"
---
# <a name="icorprofilerinfo2getclasslayout-method"></a>ICorProfilerInfo2::GetClassLayout 메서드
지정된 클래스에서 정의된 필드의 레이아웃(메모리)에 대한 정보를 가져옵니다. 즉, 이 메서드는 클래스의 필드 오프셋을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetClassLayout(  
    [in]  ClassID classID,  
    [in, out] COR_FIELD_OFFSET rFieldOffset[],  
    [in]  ULONG cFieldOffset,  
    [out] ULONG *pcFieldOffset,  
    [out] ULONG *pulClassSize);  
```  
  
## <a name="parameters"></a>매개 변수  
 `classID`  
 [in] 레이아웃이 검색되는 클래스의 ID입니다.  
  
 `rFieldOffset`  
 [out에서] 배열을 [COR_FIELD_OFFSET](../../../../docs/framework/unmanaged-api/metadata/cor-field-offset-structure.md) 구조, 각 토큰을 클래스의 필드의 오프셋을 포함 합니다.  
  
 `cFieldOffset`  
 [in] `rFieldOffset` 배열의 크기입니다.  
  
 `pcFieldOffset`  
 [out] 사용 가능한 요소의 총수에 대한 포인터입니다. `cFieldOffset`이 0인 경우 이 값은 필요한 요소 수를 나타냅니다.  
  
 `pulClassSize`  
 [out] 클래스의 크기(바이트)를 포함하는 위치에 대한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 `GetClassLayout` 메서드는 클래스 자체에서 정의된 필드만 반환합니다. 클래스의 부모 클래스에도 정의된 필드가 있는 경우 프로파일러가 부모 클래스에 대해 `GetClassLayout`을 호출하여 해당 필드를 가져와야 합니다.  
  
 문자열 클래스와 함께 `GetClassLayout`을 사용하는 경우 메서드가 E_INVALIDARG 오류 코드로 실패합니다. 사용 하 여 [ICorProfilerInfo2::GetStringLayout](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getstringlayout-method.md) 문자열의 레이아웃 정보를 가져옵니다. 배열 클래스를 사용하여 호출된 경우 `GetClassLayout`도 실패합니다.  
  
 `GetClassLayout`이 반환된 후 `rFieldOffset` 버퍼가 사용 가능한 모든 `COR_FIELD_OFFSET` 구조체를 포함하기에 충분히 큰지 확인해야 합니다. 이렇게 하려면 `pcFieldOffset`이 가리키는 값을 `rFieldOffset`의 크기를 `COR_FIELD_OFFSET` 구조체의 크기로 나눈 값과 비교합니다. `rFieldOffset`이 충분히 크지 않은 경우 더 큰 `rFieldOffset` 버퍼를 할당하고 `cFieldOffset`을 더 큰 새 크기로 업데이트한 후 `GetClassLayout`을 다시 호출합니다.  
  
 또는 길이가 0인 `rFieldOffset` 버퍼로 `GetClassLayout`를 먼저 호출하여 올바른 버퍼 크기를 구합니다. 그런 다음 버퍼 크기를 `pcFieldOffset`에 반환된 값으로 설정하고 `GetClassLayout`을 다시 호출합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerInfo 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)
- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [프로파일링](../../../../docs/framework/unmanaged-api/profiling/index.md)
