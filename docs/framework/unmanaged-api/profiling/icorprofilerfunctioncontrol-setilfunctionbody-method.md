---
title: ICorProfilerFunctionControl::SetILFunctionBody 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionControl.SetILFunctionBody
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionControl::SetILFunctionBody
helpviewer_keywords:
- ICorProfilerFunctionControl::SetILFunctionBody method [.NET Framework profiling]
- SetILFunctionBody method, ICorProfilerFunctionControl interface [.NET Framework profiling]
ms.assetid: 2c33f0f7-75b2-4c19-b2c7-c94b54997576
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d831dd7a63c06327bb0f373b3be254401c6e2ee9
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67780361"
---
# <a name="icorprofilerfunctioncontrolsetilfunctionbody-method"></a>ICorProfilerFunctionControl::SetILFunctionBody 메서드
메서드의 공용 중간 언어(CIL) 본문을 바꿉니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetILFunctionBody(  
    [in]  ULONG   cbNewILMethodHeader,  
    [in, size_is(cbNewILMethodHeader)] LPCBYTE pbNewILMethodHeader);  
```  
  
## <a name="parameters"></a>매개 변수  
 `cbNewILMethodHeader`  
 [in] 헤더와 본문 다음에 오는 모든 구조를 포함한 새 CIL의 총 크기입니다.  
  
 `pbNewILMethodHeader`  
 [in] 새 CIL 헤더에 대한 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT를 반환합니다.  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|바꾸기에 성공했습니다.|  
  
## <a name="remarks"></a>설명  
 달리 합니다 [icorprofilerinfo:: Setilfunctionbody](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilfunctionbody-method.md) 메서드를 `SetILFunctionBody` 메서드는 새 CIL 본문에 필요한 메모리를 관리 합니다. 즉, 프로파일러에서 제공 하는 CIL 본문에 없는지를 사용 하 여 할당 되는 [IMethodMalloc](../../../../docs/framework/unmanaged-api/profiling/imethodmalloc-interface.md) 인터페이스 또는 특정 범위 내에 할당 합니다. 어떤 힙에든 할당할 수 있습니다. 프로파일러 후 CIL 본문에 사용 된 메모리를 확보할 수 `SetILFunctionBody` 반환 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerFunctionControl 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerfunctioncontrol-interface.md)
