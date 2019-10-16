---
title: ICorProfilerInfo::SetILFunctionBody 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.SetILFunctionBody
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::SetILFunctionBody
helpviewer_keywords:
- ICorProfilerInfo::SetILFunctionBody method [.NET Framework profiling]
- SetILFunctionBody method [.NET Framework profiling]
ms.assetid: b159c712-00f4-4fc7-a990-40bf9f642e8f
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: abe0a0fc177c9ec89f4621e7defb5330c911034b
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67778614"
---
# <a name="icorprofilerinfosetilfunctionbody-method"></a>ICorProfilerInfo::SetILFunctionBody 메서드
지정된 된 모듈에 지정 된 함수의 본문을 바꿉니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetILFunctionBody(  
    [in] ModuleID    moduleId,  
    [in] mdMethodDef methodid,  
    [in] LPCBYTE     pbNewILMethodHeader);  
```  
  
## <a name="parameters"></a>매개 변수  
 `moduleId`  
 [in] 함수가 상주 하는 모듈의 ID입니다.  
  
 `methodid`  
 [in] 함수 본문을 대체 하는 토큰입니다.  
  
 `pbNewILMethodHeader`  
 [in] 함수에 대 한 새 헤더입니다.  
  
## <a name="remarks"></a>설명  
 `SetILFunctionBody` 메서드는 새 함수 본문 요소를 내부 데이터 구조를 필요에 따라 조정 되도록 메타 데이터 함수의 상대 가상 주소를 바꿉니다.  
  
 `SetILFunctionBody` 되지 시간 (JIT) 컴파일러에 의해 컴파일된 함수만에서 메서드를 호출할 수 있습니다.  
  
 사용 된 [icorprofilerinfo:: Getilfunctionbodyallocator](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getilfunctionbodyallocator-method.md) 버퍼 호환 되는지 확인 하려면 새 메서드에 대 한 공간을 할당 하는 방법입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerInfo 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
