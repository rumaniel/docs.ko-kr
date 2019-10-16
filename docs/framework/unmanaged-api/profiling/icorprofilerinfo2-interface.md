---
title: ICorProfilerInfo2 인터페이스
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2
helpviewer_keywords:
- ICorProfilerInfo2 interface [.NET Framework profiling]
ms.assetid: 91bd49b6-4d12-494f-a8f1-2f251e8c65e3
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3476a338191a4af9cc01b7e44456f1bd20f52a10
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61796548"
---
# <a name="icorprofilerinfo2-interface"></a>ICorProfilerInfo2 인터페이스
코드 프로파일러가 CLR (공용 언어 런타임) 이벤트 모니터링을 제어 하 고 요청 정보를 사용 하 여 통신에 사용 되는 메서드를 제공 합니다. 합니다 `ICorProfilerInfo2` 인터페이스의 확장은 합니다 [ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md) 인터페이스입니다. 즉,.NET Framework 버전 2.0 이상 버전에서 지원 되는 새 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[DoStackSnapshot 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)|프로파일러에 관리 되는 호출 프레임을 보고 지정 된 스레드의 스택에 대해 설명 합니다.|  
|[EnumModuleFrozenObjects 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-enummodulefrozenobjects-method.md)|지정된 된 모듈에 고정된 된 개체를 반복할 수 있는 열거자를 가져옵니다.|  
|[GetAppDomainStaticAddress 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getappdomainstaticaddress-method.md)|지정 된 응용 프로그램 도메인의 범위 내에 있는 지정 된 응용 프로그램 도메인 정적 필드의 주소를 가져옵니다.|  
|[GetArrayObjectInfo 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getarrayobjectinfo-method.md)|배열 개체에 대 한 자세한 정보를 가져옵니다.|  
|[GetBoxClassLayout 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getboxclasslayout-method.md)|지정된 된 값 형식의 boxed는 대 한 클래스 레이아웃에 대 한 정보를 가져옵니다.|  
|[GetClassFromTokenAndTypeArgs 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclassfromtokenandtypeargs-method.md)|가져옵니다 합니다 `ClassID` 지정 된 메타 데이터 토큰을 사용 하 여 형식 및 `ClassID` 값의 형식 인수입니다.|  
|[GetClassIDInfo2 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclassidinfo2-method.md)|클래스에 대 한 메타 데이터 토큰이 지정 된 제네릭 클래스의 부모 모듈을 가져옵니다 합니다 `ClassID` , 부모 클래스의 및 `ClassID` 있는 클래스의 경우 각 형식 인수에 대 한 합니다.|  
|[GetClassLayout 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclasslayout-method.md)|지정된 클래스에서 정의된 필드의 레이아웃(메모리)에 대한 정보를 가져옵니다. 즉, 이 메서드는 클래스의 필드 오프셋을 가져옵니다.|  
|[GetCodeInfo2 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getcodeinfo2-method.md)|지정된 `FunctionID`와 연결된 네이티브 코드의 범위를 가져옵니다.|  
|[GetContextStaticAddress 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getcontextstaticaddress-method.md)|지정 된 컨텍스트의 범위 내에 있는 지정된 된 컨텍스트 정적 필드의 주소를 가져옵니다.|  
|[GetFunctionFromTokenAndTypeArgs 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctionfromtokenandtypeargs-method.md)|가져옵니다 합니다 `FunctionID` 클래스를 포함 하는 지정 된 메타 데이터 토큰을 사용 하 여 함수 및 `ClassID` 값의 형식 인수입니다.|  
|[GetFunctionInfo2 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctioninfo2-method.md)|함수의 부모 클래스, 메타데이터 토큰 및 각 형식 인수 `ClassID`(있는 경우)를 가져옵니다.|  
|[GetGenerationBounds 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getgenerationbounds-method.md)|가비지 수집 힙의 세대를 구성 하는 메모리 영역을 (힙 세그먼트)를 가져옵니다.|  
|[GetNotifiedExceptionClauseInfo 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getnotifiedexceptionclauseinfo-method.md)|예외 절에 대 한 기본 주소 및 프레임 정보를 가져옵니다 (`catch`/`finally`/`filter`) 방금 실행 되거나 실행 될는 합니다.|  
|[GetObjectGeneration 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getobjectgeneration-method.md)|지정된 된 개체를 포함 하는 힙 세그먼트를 가져옵니다.|  
|[GetRVAStaticAddress 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getrvastaticaddress-method.md)|지정 된 상대 가상 주소 (RVA)의 주소를 가져옵니다-정적 필드입니다.|  
|[GetStaticFieldInfo 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getstaticfieldinfo-method.md)|지정된 된 필드의 정적 범위를 가져옵니다.|  
|[GetStringLayout 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getstringlayout-method.md)|문자열 개체의 레이아웃 정보를 가져옵니다.|  
|[GetThreadAppDomain 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getthreadappdomain-method.md)|지정된 된 스레드에 현재 코드를 실행 하는 응용 프로그램 도메인의 ID를 가져옵니다.|  
|[GetThreadStaticAddress 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getthreadstaticaddress-method.md)|지정된 된 스레드에 범위에 있는 지정된 된 thread 정적 필드의 주소를 가져옵니다.|  
|[SetEnterLeaveFunctionHooks2 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-setenterleavefunctionhooks2-method.md)|"입력", "유지" 및 "tailcall" 후크 관리 되는 함수에서 호출 되는 프로파일러 구현 함수를 지정 합니다.|  
  
## <a name="remarks"></a>설명  
 메서드를 호출 하는 프로파일러는 `ICorProfilerInfo2` 이벤트 모니터링 및 제어 정보를 요청 하려면 CLR과 통신 하는 인터페이스입니다.  
  
 메서드는 `ICorProfilerInfo2` 인터페이스 자유 스레드 모델을 사용 하 여 CLR에 의해 구현 됩니다. 각 메서드가 HRESULT를 반환하여 성공 또는 실패를 나타냅니다. 가능한 반환 코드 목록은 CorError.h 파일을 참조하세요.  
  
 CLR 전달를 `ICorProfilerInfo2` 인터페이스의 구현을 사용 하 여 초기화 하는 동안 각 코드 프로파일러 [icorprofilercallback:: Initialize](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md)합니다. 코드 프로파일러가의 메서드를 호출할 수 있습니다는 `ICorProfilerInfo2` CLR의 제어 아래에서 실행 되는 관리 코드에 대 한 정보를 가져오는 인터페이스입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [ICorProfilerInfo 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
