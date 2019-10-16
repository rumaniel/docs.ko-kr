---
title: ICorProfilerInfo2::GetThreadStaticAddress 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetThreadStaticAddress
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetThreadStaticAddress
helpviewer_keywords:
- GetThreadStaticAddress method [.NET Framework profiling]
- ICorProfilerInfo2::GetThreadStaticAddress method [.NET Framework profiling]
ms.assetid: 8e7dbf14-98a2-4384-a950-58a7640e59df
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8f8c18935069e4162236f99c411312087ce73bdc
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782212"
---
# <a name="icorprofilerinfo2getthreadstaticaddress-method"></a>ICorProfilerInfo2::GetThreadStaticAddress 메서드
지정된 된 스레드에 범위에 있는 지정된 된 thread 정적 필드의 주소를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetThreadStaticAddress(  
    [in] ClassID     classId,  
    [in] mdFieldDef  fieldToken,  
    [in] ThreadID    threadId,  
    [out] void       **ppAddress);  
```  
  
## <a name="parameters"></a>매개 변수  
 `classId`  
 [in] 요청 된 thread 정적 필드를 포함 하는 클래스의 ID입니다.  
  
 `fieldToken`  
 [in] 요청 된 thread 정적 필드에 대 한 메타 데이터 토큰입니다.  
  
 `threadId`  
 [in] 요청 된 정적 필드에 대 한 범위는 스레드의 ID입니다.  
  
 `ppAddress`  
 [out] 지정된 된 스레드에 내에 있는 정적 필드의 주소에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 `GetThreadStaticAddress` 메서드 중 하나를 반환할 수 있습니다.  
  
- 지정 된 정적 필드에 지정 된 컨텍스트에서 주소 할당 되지 않은 경우 CORPROF_E_DATAINCOMPLETE HRESULT입니다.  
  
- 가비지 컬렉션 힙에 있을 수 있는 개체의 주소입니다. 가비지 수집 후 이러한 주소는 잘못 될 뒤 가비지 컬렉션 프로파일러는 유효한 지를 가정 하지 않아야 합니다.  
  
 클래스의 클래스 생성자 완료 되기 전에 `GetThreadStaticAddress` 정적 필드 중 일부를 초기화할 수는 이미 있지만 CORPROF_E_DATAINCOMPLETE 정적 해당 모든 필드에 대 한 반환 하 고 가비지 컬렉션 개체를 응원 하 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerInfo 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)
