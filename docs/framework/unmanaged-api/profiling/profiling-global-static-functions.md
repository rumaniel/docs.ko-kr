---
title: 프로파일링 전역 정적 함수
ms.date: 03/30/2017
helpviewer_keywords:
- global static functions [.NET Framework profiling]
- profiling global static functions [.NET Framework]
- unmanaged global static functions [.NET Framework], profiling
ms.assetid: 08a13a57-dc49-488d-b937-31e3051fda97
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3ea65c06871d9762fa6daac229a568594b4c4479
ms.sourcegitcommit: 518e7634b86d3980ec7da5f8c308cc1054daedb7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2019
ms.locfileid: "66457479"
---
# <a name="profiling-global-static-functions"></a>프로파일링 전역 정적 함수
이 섹션에서는 프로 파일링 API를 사용 하는 관리 되지 않는 API 함수를 설명 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
## <a name="net-framework-version-1-profiling-functions"></a>.NET framework 버전 1 프로 파일링 함수  
 [FunctionEnter 함수](../../../../docs/framework/unmanaged-api/profiling/functionenter-function.md)  
 컨트롤이 함수에 전달 되 고 있음을 프로파일러에 알립니다. .NET Framework 2.0에서에서 사용 되지 않습니다.  
  
 [FunctionLeave 함수](../../../../docs/framework/unmanaged-api/profiling/functionleave-function.md)  
 호출자에 게 반환 하려고 하는 함수는 프로파일러에 알립니다. .NET Framework 2.0에서에서 사용 되지 않습니다.  
  
 [FunctionTailcall 함수](../../../../docs/framework/unmanaged-api/profiling/functiontailcall-function.md)  
 현재 실행 중인 함수에 대 한 다른 함수에 대 한 마무리 호출이 수행 하는 프로파일러에 알립니다. .NET Framework 2.0에서에서 사용 되지 않습니다.  
  
## <a name="net-framework-version-2-profiling-functions"></a>.NET framework 버전 2 프로 파일링 함수  
 [FunctionIDMapper 함수](../../../../docs/framework/unmanaged-api/profiling/functionidmapper-function.md)  
 함수는 지정 된 식별자에 사용할 대체 ID를 다시 매핑할 수는 프로파일러에 알립니다. 합니다 [FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)를 [FunctionLeave2](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md), 및 [FunctionTailcall2](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md) 함수에 대 한 콜백 합니다. 프로파일러를 함수에 대 한 콜백을 받을 수 있는지 여부를 나타낼 수 있습니다.  
  
 [FunctionEnter2 함수](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)  
 제어 함수에 전달 되 고 및 프레임과 함수 인수는 스택에 대 한 정보를 제공 하는 프로파일러에 알립니다. .NET Framework 4에서에서 사용 되지 않습니다.  
  
 [FunctionLeave2 함수](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md)  
 함수에 대 한 호출자에 게 반환 하는 것을 스택 프레임 및 함수 반환 값에 대 한 정보를 제공 프로파일러에 알립니다. .NET Framework 4에서에서 사용 되지 않습니다.  
  
 [FunctionTailcall2 함수](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md)  
 현재 실행 중인 함수를 다른 함수에 대 한 마무리 호출이 수행 하려고 하는 스택 프레임에 대 한 정보를 제공 프로파일러에 알립니다. .NET Framework 4에서에서 사용 되지 않습니다.  
  
 [StackSnapshotCallback 함수](../../../../docs/framework/unmanaged-api/profiling/stacksnapshotcallback-function.md)  
 프로파일러가 시작 되는 스택 워크 중 스택의 각 관리 되는 프레임 및 관리 되지 않는 프레임의 각 실행에 대 한 정보를 제공 합니다 [ICorProfilerInfo2::DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md) 메서드.  
  
## <a name="net-framework-version-4-profiling-functions"></a>.NET framework 버전 4 프로 파일링 함수  
 [FunctionIDMapper2 함수](../../../../docs/framework/unmanaged-api/profiling/functionidmapper2-function.md)  
 함수는 지정 된 식별자에 사용할 대체 ID를 다시 매핑할 수는 프로파일러에 알립니다. 합니다 [FunctionEnter3](../../../../docs/framework/unmanaged-api/profiling/functionenter3-function.md)를 [FunctionLeave3](../../../../docs/framework/unmanaged-api/profiling/functionleave3-function.md), 및 [FunctionTailcall3](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3-function.md), 또는[FunctionEnter3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionenter3withinfo-function.md)를 [FunctionLeave3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionleave3withinfo-function.md), 및 [FunctionTailcall3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3withinfo-function.md) 해당 함수에 대 한 콜백 합니다. 프로파일러를 함수에 대 한 콜백을 받을 수 있는지 여부를 나타낼 수 있습니다.  
  
 `FunctionIDMapper2` 확장을 [FunctionIDMapper](../../../../docs/framework/unmanaged-api/profiling/functionidmapper-function.md) 함수를 `clientData` 프로파일러 런타임 중 명확히 구분 하는 데 사용할 수 있는 매개 변수입니다.  
  
 [FunctionEnter3 함수](../../../../docs/framework/unmanaged-api/profiling/functionenter3-function.md)  
 컨트롤이 함수에 전달 되 고 있음을 프로파일러에 알립니다.  
  
 [FunctionEnter3WithInfo 함수](../../../../docs/framework/unmanaged-api/profiling/functionenter3withinfo-function.md)  
 컨트롤이 함수에 전달 되 고 있음을 프로파일러에 알립니다. 및 전달할 수 있는 핸들을 제공 [ICorProfilerInfo3::GetFunctionEnter3Info](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionenter3info-method.md) 스택 프레임 및 함수 인수를 검색 하도록 합니다.  
  
 [FunctionLeave3 함수](../../../../docs/framework/unmanaged-api/profiling/functionleave3-function.md)  
 제어 함수에서 반환 되는 프로파일러에 알립니다.  
  
 [FunctionLeave3WithInfo 함수](../../../../docs/framework/unmanaged-api/profiling/functionleave3withinfo-function.md)  
 컨트롤은 함수에서 반환 되는 프로파일러에 알립니다. 및 전달할 수 있는 핸들을 제공 [ICorProfilerInfo3::GetFunctionLeave3Info](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionleave3info-method.md) 스택 프레임 및 반환 값을 검색할 수 있습니다.  
  
 [FunctionTailcall3 함수](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3-function.md)  
 현재 실행 중인 함수에 대 한 다른 함수에 대 한 마무리 호출이 수행 하는 프로파일러에 알립니다.  
  
 [FunctionTailcall3WithInfo 함수](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3withinfo-function.md)  
 현재 실행 중인 함수를 다른 함수에 대 한 마무리 호출이 수행 하려고 하는 프로파일러에 알립니다 및 전달할 수 있는 핸들을 제공 [ICorProfilerInfo3::GetFunctionTailcall3Info](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctiontailcall3info-method.md) 스택 프레임을 검색할 합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [프로파일링 개요](../../../../docs/framework/unmanaged-api/profiling/profiling-overview.md)  
  
 [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
  
 [프로파일링 열거형](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)  
  
 [프로파일링 구조체](../../../../docs/framework/unmanaged-api/profiling/profiling-structures.md)
