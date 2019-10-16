---
title: ICorProfilerInfo::GetCodeInfo 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetCodeInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetCodeInfo
helpviewer_keywords:
- GetCodeInfo method [.NET Framework profiling]
- ICorProfilerInfo::GetCodeInfo method [.NET Framework profiling]
ms.assetid: 90140b0f-a926-4a7e-b6fa-23e05f703cce
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2cc587edf763a352501a0d9097bdab2c54658d98
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67762850"
---
# <a name="icorprofilerinfogetcodeinfo-method"></a>ICorProfilerInfo::GetCodeInfo 메서드
지정된 함수 ID와 연결된 네이티브 코드의 범위를 가져옵니다.  
  
 이 메서드는 사용되지 않습니다. 사용 된 [ICorProfilerInfo2::GetCodeInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getcodeinfo2-method.md) 메서드 대신 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetCodeInfo(  
    [in]  FunctionID functionId,  
    [out] LPCBYTE    *pStart,  
    [out] ULONG      *pcSize);  
```  
  
## <a name="parameters"></a>매개 변수  
 `functionId`  
 [in] 네이티브 코드가 연결된 함수의 ID입니다.  
  
 `pStart`  
 [out] 함수의 네이티브 코드를 구성하는 바이트 배열에 대한 포인터입니다.  
  
 `pcSize`  
 [out] 네이티브 코드의 크기(바이트)를 지정하는 정수에 대한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 성능을 최적화하기 위해 .NET Framework 버전 2.0의 런타임은 함수의 미리 컴파일된 네이티브 코드를 여러 영역으로 분할합니다. 결과적으로 `GetCodeInfo` 메서드는 함수의 네이티브 코드 범위를 처리할 수 없으므로 .NET Framework 2.0에서 사용되지 않습니다. 프로파일러가 보다 일반적인 `ICorProfilerInfo2::GetCodeInfo2` 메서드 사용으로 전환해야 합니다.  
  
 이 함수는 호출자 할당 버퍼를 사용합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET framework 버전:** 1.0  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerInfo 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [프로파일링](../../../../docs/framework/unmanaged-api/profiling/index.md)
