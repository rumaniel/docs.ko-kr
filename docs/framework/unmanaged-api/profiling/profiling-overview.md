---
title: 프로파일링 개요
ms.date: 03/30/2017
helpviewer_keywords:
- managed code, profiling API support
- unmanaged code, combining with managed code in profiling
- notification threads [.NET Framework profiling]
- unmanaged code, profiling
- profiling API [.NET Framework], and COM
- profiling API [.NET Framework], unmanaged code profiling
- profilers, writing
- profiling API [.NET Framework], call stacks
- code profilers, writing
- profiling API [.NET Framework], security considerations
- profiling API [.NET Framework], managed code support
- common language runtime, profiling
- profiling API [.NET Framework], notification threads
- call stacks [.NET Framework profiling]
- profiling API [.NET Framework], stack depth
- common language runtime, writing a profiler
- profiling API [.NET Framework], information retrieval interfaces
- shadow stacks [.NET Framework profiling]
- COM, using in the profiling API
- stack snapshots [.NET Framework profiling]
- profiling API [.NET Framework], supported features
- profiling API [.NET Framework], overview
- security, profiling API considerations
- stack depth [.NET Framework profiling]
ms.assetid: 864c2344-71dc-46f9-96b2-ed59fb6427a8
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6dbf36cec1bcd2ec1e96d57a889ddd9d9baef269
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663886"
---
# <a name="profiling-overview"></a>프로파일링 개요

<a name="top"></a> 프로파일러는 다른 응용 프로그램의 실행을 모니터링 하는 도구입니다. CLR(공용 언어 런타임) 프로파일러는 프로 파일링 API를 사용하여 CLR에서 메시지를 받고 보내는 함수로 구성된 DLL(동적 연결 라이브러리)입니다. 프로파일러 DLL은 런타임에 CLR에 의해 로드됩니다.

기존의 프로파일링 도구는 애플리케이션의 실행 측정에 중점을 둡니다. 즉, 각 함수에서 소요된 시간이나 시간 경과에 따른 애플리케이션의 메모리 사용량을 측정합니다. 프로파일링 API는 코드 검사 유틸리티 및 고급 디버깅 지원과 같은 광범위한 진단 도구 클래스를 대상으로 합니다. 이러한 사용은 본질적으로 모두 진단입니다. 프로파일링 API는 애플리케이션의 실행을 측정할 뿐 아니라 모니터링합니다. 이러한 이유로 프로파일링 API는 애플리케이션 자체에서 사용하면 안 되며, 애플리케이션의 실행이 프로파일러에 종속되거나 영향을 받아서도 안 됩니다.

CLR 애플리케이션을 프로파일링하려면 기존의 컴파일된 기계어 코드를 프로파일링하는 것보다 많은 지원이 필요합니다. 이는 CLR에서 애플리케이션 도메인, 가비지 컬렉션, 관리되는 예외 처리, 코드의 JIT(Just-In-Time) 컴파일(Microsoft Intermediate Language, 즉 MSIL 코드를 네이티브 기계어 코드로 변환) 및 비슷한 기능과 같은 개념을 도입하기 때문입니다. 기존의 프로파일링 메커니즘은 이러한 기능에 대한 유용한 정보를 식별하거나 제공할 수 없습니다. 프로파일링 API는 CLR 및 프로파일링된 애플리케이션의 성능에 미치는 영향을 최소화하여 이 누락된 정보를 효율적으로 제공합니다.

런타임의 JIT 컴파일은 프로파일링에 좋은 기회를 제공합니다. 프로파일링 API를 통해 프로파일러는 JIT 컴파일되기 전에 루틴에 대한 메모리 내 MSIL 코드 스트림을 변경할 수 있습니다. 이런 방식으로 프로파일러는 더 세부적인 조사가 필요한 특정 루틴에 계측 코드를 동적으로 추가할 수 있습니다. 이 접근 방식은 기존 시나리오에서도 가능하지만 프로파일링 API를 사용하여 CLR에 대해 구현하는 것이 훨씬 더 쉽습니다.

이 개요는 다음과 같은 섹션으로 구성되어 있습니다.

- [프로 파일링 API](#profiling_api)

- [지원 되는 기능](#support)

- [알림 스레드](#notification_threads)

- [보안](#security)

- [결합 코드와 비관리 코드 Profiler에서 코드](#combining_managed_unmanaged)

- [비관리 코드 프로 파일링](#unmanaged)

- [COM을 사용 하 여](#com)

- [호출 스택](#call_stacks)

- [콜백 및 스택 수준](#callbacks)

- [관련 항목](#related_topics)

<a name="profiling_api"></a>

## <a name="the-profiling-api"></a>프로파일링 API

프로 파일링 API를 쓰는 데 사용 되는 일반적으로 *코드 프로파일러*, 관리 되는 응용 프로그램의 실행을 모니터링 하는 프로그램인 합니다.

프로파일링 API는 프로파일링되는 애플리케이션과 동일한 프로세스에 로드된 프로파일러 DLL에서 사용됩니다. 콜백 인터페이스를 구현 하는 프로파일러 DLL ([ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) .NET framework 버전 1.0 및 1.1 [ICorProfilerCallback2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md) 2.0 이상 버전에서). CLR은 해당 인터페이스의 메서드를 호출하여 프로파일링된 프로세스의 이벤트를 프로파일러에 알립니다. 프로파일러 콜백할 수 있는 런타임에서에서 메서드를 사용 하는 [ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md) 및 [ICorProfilerInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md) 프로 파일링 된 응용 프로그램의 상태에 대 한 정보를 가져오는 인터페이스입니다.

> [!NOTE]
> 프로파일러 솔루션의 데이터 수집 부분만 프로파일링된 애플리케이션과 동일한 프로세스에서 실행되어야 합니다. 모든 사용자 인터페이스 및 데이터 분석은 별도 프로세스에서 수행되어야 합니다.

다음 그림에서는 프로파일러 DLL이 프로파일링되는 애플리케이션 및 CLR과 상호 작용하는 방법을 보여 줍니다.

![프로 파일링 아키텍처를 보여 주는 스크린샷.](./media/profiling-overview/profiling-architecture.png)

### <a name="the-notification-interfaces"></a>알림 인터페이스

[ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md) 하 고 [ICorProfilerCallback2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md) 알림 인터페이스로 간주 될 수 있습니다. 이러한 인터페이스와 같은 메서드의 구성 [ClassLoadStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-classloadstarted-method.md)를 [ClassLoadFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-classloadfinished-method.md), 및 [JITCompilationStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationstarted-method.md)합니다. CLR은 클래스를 로드 또는 언로드하고 함수를 컴파일할 때마다 프로파일러의 `ICorProfilerCallback` 또는 `ICorProfilerCallback2` 인터페이스에서 해당 메서드를 호출합니다.

예를 들어 프로파일러는 두 알림 함수를 통해 코드 성능을 측정할 수 있습니다. [FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md) 하 고 [FunctionLeave2](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md)합니다. 단순히 각 알림에 타임스탬프를 지정하고, 결과를 누적한 다음 애플리케이션 실행 중에 가장 많은 CPU 또는 벽시계 시간을 사용한 함수를 나타내는 목록을 출력합니다.

### <a name="the-information-retrieval-interfaces"></a>정보 검색 인터페이스

다른 주요 인터페이스 프로 파일링에 관련 된 됩니다 [ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md) 하 고 [ICorProfilerInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)합니다. 프로파일러는 필요에 따라 이러한 인터페이스를 호출하여 분석에 도움이 되는 자세한 정보를 가져옵니다. CLR이 호출 될 때마다 예를 들어 합니다 [FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md) 함수 함수 식별자를 제공 합니다. 프로파일러를 호출 하 여 해당 함수에 대 한 자세한 정보를 얻을 수는 [ICorProfilerInfo2::GetFunctionInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctioninfo2-method.md) 함수의 부모 클래스, 이름 및 등을 검색 하는 방법입니다.

[맨 위로 이동](#top)

<a name="support"></a>

## <a name="supported-features"></a>지원되는 기능

프로파일링 API는 공용 언어 런타임에서 발생하는 다양한 이벤트와 작업에 대한 정보를 제공합니다. 이 정보를 사용하여 프로세스의 내부 작업을 모니터링하고 .NET Framework 애플리케이션의 성능을 분석할 수 있습니다.

프로파일링 API는 CLR에서 발생하는 다음 작업 및 이벤트에 대한 정보를 검색합니다.

- CLR 시작 및 종료 이벤트

- 애플리케이션 도메인 생성 및 종료 이벤트

- 어셈블리 로드 및 언로드 이벤트

- 모듈 로드 및 언로드 이벤트

- COM vtable 생성 및 소멸 이벤트

- JIT(Just-In-Time) 컴파일 및 코드 피칭 이벤트

- 클래스 로드 및 언로드 이벤트

- 스레드 생성 및 소멸 이벤트

- 함수 진입 및 종료 이벤트

- 예외

- 관리 코드와 비관리 코드 실행 간의 전환

- 다양한 런타임 컨텍스트 간의 전환

- 런타임 일시 중단에 대한 정보

- 런타임 메모리 힙 및 가비지 수집 작업에 대한 정보

모든(관리되지 않는) COM 호환 언어에서 프로파일링 API를 호출할 수 있습니다.

이 API는 CPU 및 메모리 사용과 관련해서 효율적입니다. 프로파일링에서는 프로파일링된 애플리케이션에 대해 잘못된 결과를 일으킬 만큼 중요한 변경 작업을 수행하지 않습니다.

프로파일링 API는 샘플링 및 비샘플링 프로파일러 둘 다에 유용합니다. A *샘플링 프로파일러* 는 프로 파일을 검사 일반 클록 틱 예를 들어 5 밀리초 간격입니다. A *비 샘플링 프로파일러* 는 이벤트를 발생 시키는 스레드에서 동기적으로 이벤트의 알림을 받습니다.

### <a name="unsupported-functionality"></a>지원되지 않는 기능

프로파일링 API에서는 다음 기능을 지원하지 않습니다.

- 기존의 Win32 메서드를 통해 프로파일링해야 하는 비관리 코드. 그러나 CLR 프로파일러에는 관리 코드와 비관리 코드 간의 경계를 결정하는 전환 이벤트가 포함됩니다.

- 관점 지향 프로그래밍과 같은 목적을 위해 해당 코드를 수정하는 자체 수정 애플리케이션

- 범위 검사. 프로파일링 API에서 이 정보를 제공하지 않기 때문입니다. CLR은 모든 관리 코드의 범위 검사를 기본적으로 지원합니다.

- 원격 프로파일링. 다음과 같은 이유로 지원되지 않습니다.

  - 원격 프로파일링은 실행 시간을 연장합니다. 프로파일링 인터페이스를 사용하는 경우 프로파일링 결과가 과도한 영향을 받지 않도록 실행 시간을 최소화해야 합니다. 이는 실행 성능을 모니터링하는 경우 특히 중요합니다. 그러나 원격 프로파일링은 프로파일링 인터페이스를 사용하여 메모리 사용량을 모니터링하거나 스택 프레임, 개체 등에 대한 런타임 정보를 가져올 때 제한 사항이 아닙니다.

  - CLR 코드 프로파일러는 프로파일링된 애플리케이션이 실행되고 있는 로컬 컴퓨터에서 런타임에 하나 이상의 콜백 인터페이스를 등록해야 합니다. 이로 인해 원격 코드 프로파일러를 만드는 기능이 제한됩니다.

- 고가용성 요구 사항이 있는 프로덕션 환경의 프로파일링. 프로파일링 API는 개발 시 진단을 지원하기 위해 만들어졌습니다. 프로덕션 환경을 지원하는 데 필요한 엄격한 테스트를 받지 않았습니다.

[맨 위로 이동](#top)

<a name="notification_threads"></a>

## <a name="notification-threads"></a>알림 스레드

대부분의 경우 이벤트를 생성하는 스레드도 알림을 실행합니다. 이러한 알림 (예를 들어 [FunctionEnter](../../../../docs/framework/unmanaged-api/profiling/functionenter-function.md) 하 고 [FunctionLeave](../../../../docs/framework/unmanaged-api/profiling/functionleave-function.md)) 명시적 제공할 필요가 없습니다 `ThreadID`합니다. 또한 프로파일러는 영향을 받는 스레드의 `ThreadID`에 따라, 전역 스토리지의 분석 블록을 인덱싱하는 대신 스레드 로컬 스토리지를 사용하여 분석 블록을 저장 및 업데이트할 수 있습니다.

이러한 콜백은 직렬화되지 않습니다. 사용자는 스레드로부터 안전한 데이터 구조를 만들고 여러 스레드에서의 병렬 액세스를 방지하기 위해 필요에 따라 프로파일러 코드를 잠가 코드를 보호해야 합니다. 따라서 특정 경우에서는 사용자가 평소와 다른 콜백 시퀀스를 받을 수 있습니다. 예를 들어 관리되는 애플리케이션이 동일한 코드를 실행하는 두 스레드를 생성한다고 가정합니다. 받을 수 있습니다이 예제의 경우를 [icorprofilercallback:: Jitcompilationstarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationstarted-method.md) 한 스레드에서 일부 함수에 대 한 이벤트 및 `FunctionEnter` 콜백을 받기 전에 다른 스레드에서 [ Icorprofilercallback:: Jitcompilationfinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationfinished-method.md) 콜백 합니다. 이 경우에는 사용자가 아직 완전히 JIT(Just-In-Time) 컴파일되지 않았을 수 있는 함수에 대해 `FunctionEnter` 콜백을 받는 것입니다.

[맨 위로 이동](#top)

<a name="security"></a>

## <a name="security"></a>보안

프로파일러 DLL은 공용 언어 런타임 실행 엔진의 일부로 실행되는 관리되지 않는 DLL입니다. 따라서 프로파일러 DLL의 코드에 관리 코드 액세스 보안의 제한이 적용되지 않습니다. 프로파일러 DLL에 대한 유일한 제한 사항은 운영 체제에서 프로파일링된 애플리케이션을 실행하는 사용자에 대해 적용하는 제한입니다.

프로파일러 작성자는 보안 관련 문제를 방지하기 위해 적절한 예방 조치를 취해야 합니다. 예를 들어 악의적인 사용자가 수정할 수 없도록 설치 중에 프로파일러 DLL을 ACL(액세스 제어 목록)에 추가해야 합니다.

[맨 위로 이동](#top)

<a name="combining_managed_unmanaged"></a>

## <a name="combining-managed-and-unmanaged-code-in-a-code-profiler"></a>코드 프로파일러에서 관리 코드와 비관리 코드 결합

잘못 작성된 프로파일러는 자체 순환 참조를 생성하여 예기치 않은 동작이 발생할 수 있습니다.

CLR 프로파일링 API를 검토하면 COM interop 또는 간접 호출을 통해 서로 호출하는 관리되는 구성 요소와 관리되지 않는 구성 요소를 포함하는 프로파일러를 작성할 수 있다는 인상을 받을 수 있습니다.

디자인 관점에서는 가능하지만 프로파일링 API는 관리되는 구성 요소를 지원하지 않습니다. CLR 프로파일러는 완전히 관리되지 않아야 합니다. CLR 프로파일러에서 관리 코드와 비관리 코드를 결합하려고 하면 액세스 위반, 프로그램 오류 또는 교착 상태가 발생할 수 있습니다. 프로파일러의 관리되는 구성 요소는 관리되지 않는 해당 구성 요소로 다시 이벤트를 발생시키고, 이후에 이 구성 요소가 관리되는 구성 요소를 다시 호출하여 순환 참조가 발생합니다.

CLR 프로파일러가 관리 코드를 안전하게 호출할 수 있는 유일한 위치는 메서드의 MSIL(Microsoft Intermediate Language) 본문입니다. MSIL 본문을 수정 하는 것에 대 한 권장 되는 방법에서 JIT 재컴파일 메서드를 사용 하는 것은 [ICorProfilerCallback4](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md) 인터페이스입니다.

오래된 계측 메서드를 사용하여 MSIL을 수정할 수도 있습니다. 프로파일러는 메서드 및 다음 JIT 컴파일되나요 MSIL 본문에 관리 되는 호출을 삽입할 수 함수의 time (JIT) 컴파일이 완료 되기 전에 해당 (참조를 [icorprofilerinfo:: Getilfunctionbody](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getilfunctionbody-method.md) 메서드). 이 기술은 관리 코드의 선택적 계측이나 JIT에 대한 통계 및 성능 데이터 수집을 위해 성공적으로 사용할 수 있습니다.

또는 코드 프로파일러가 비관리 코드를 호출하는 모든 관리되는 함수의 MSIL 본문에 네이티브 후크를 삽입할 수 있습니다. 이 기술은 계측 및 검사에 사용할 수 있습니다. 예를 들어 코드 프로파일러가 모든 MSIL 블록 뒤에 계측 후크를 삽입하여 블록이 실행되었는지 확인할 수 있습니다. 메서드의 MSIL 본문 수정은 매우 정교한 작업이며 여러 가지 요인을 고려해야 합니다.

[맨 위로 이동](#top)

<a name="unmanaged"></a>

## <a name="profiling-unmanaged-code"></a>비관리 코드 프로파일링

CLR(공용 언어 런타임) 프로파일링 API는 비관리 코드 프로파일링에 대해 최소한의 지원을 제공합니다. 다음 기능이 제공됩니다.

- 스택 체인 열거형. 이 기능을 통해 코드 프로파일러는 관리 코드와 비관리 코드 사이의 경계를 결정할 수 있습니다.

- 스택 체인이 관리 코드에 해당하는지 또는 네이티브 코드에 해당하는지를 결정합니다.

.NET Framework 버전 1.0 및 1.1에서는 CLR 디버깅 API의 in-process 하위 집합을 통해 이러한 메서드를 사용할 수 있습니다. CorDebug.idl 파일에서 정의됩니다.

.NET Framework 2.0 이상 버전에서는 사용할 수는 [ICorProfilerInfo2::DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md) 이 기능에 대 한 메서드.

[맨 위로 이동](#top)

<a name="com"></a>

## <a name="using-com"></a>COM 사용

프로파일링 인터페이스는 COM 인터페이스로 정의되지만 CLR(공용 언어 런타임)에서 실제로 이러한 인터페이스를 사용하도록 COM를 초기화하지는 않습니다. 이유는을 사용 하 여 스레딩 모델을 설정 하지 않도록 하는 [CoInitialize](/windows/desktop/api/objbase/nf-objbase-coinitialize) 관리 되는 응용 프로그램에 필요한 해당 스레딩 모델을 지정 하기 전에 함수. 마찬가지로, 프로파일러 자체는 프로파일링되는 애플리케이션과 호환되지 않는 스레딩 모델을 선택하여 애플리케이션이 실패하게 만들 수 있으므로 `CoInitialize`를 호출하면 안 됩니다.

[맨 위로 이동](#top)

<a name="call_stacks"></a>

## <a name="call-stacks"></a>호출 스택

프로파일링 API는 호출 스택을 가져오는 두 가지 방법을 제공합니다. 스택 스냅샷 메서드는 호출 스택의 스파스 수집을 가능하게 하고 섀도 스택 메서드는 모든 순간에 호출 스택을 추적합니다.

### <a name="stack-snapshot"></a>스택 스냅샷

스택 스냅샷은 한 순간의 스레드 스택 추적입니다. 프로파일링 API는 스택에서 관리되는 함수의 추적을 지원하지만 관리되지 않는 함수의 추적은 프로파일러의 자체 스택 워크에 맡깁니다.

관리 되는 스택 워크에 프로파일러를 프로그래밍 하는 방법에 대 한 자세한 내용은 참조는 [ICorProfilerInfo2::DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md) 이 설명서의 메서드 및 [Profiler Stack Walking.NET Framework 2.0 in에서: Basics and Beyond](https://go.microsoft.com/fwlink/?LinkId=73638)합니다.

### <a name="shadow-stack"></a>섀도 스택

스냅샷 메서드를 너무 자주 사용하면 성능 문제가 빠르게 발생할 수 있습니다. 프로파일러를 사용 하 여 섀도 스택을 빌드 대신 해야 스택 추적을 자주 수행 하려는 경우는 [FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md), [FunctionLeave2](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md)합니다 [FunctionTailcall2](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md), 및 [ICorProfilerCallback2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md) 예외 콜백을 합니다. 섀도 스택은 항상 최신 상태이며 스택 스냅샷이 필요할 때마다 스토리지로 빠르게 복사될 수 있습니다.

섀도 스택은 함수 인수, 반환 값 및 제네릭 인스턴스화에 대한 정보를 얻을 수 있습니다. 이 정보는 섀도 스택을 통해서만 제공되며 컨트롤이 함수에 전달될 때 얻을 수 있습니다. 그러나 나중에 함수 실행 중에는 이 정보는 사용할 수 없습니다.

[맨 위로 이동](#top)

<a name="callbacks"></a>

## <a name="callbacks-and-stack-depth"></a>콜백 및 스택 수준

프로파일러 콜백은 스택이 매우 제한된 환경에서 실행할 수 있으며, 프로파일러 콜백의 스택 오버플로로 인해 즉시 프로세스가 종료됩니다. 프로파일러는 콜백에 대한 응답으로 가능한 한 적은 스택을 사용해야 합니다. 프로파일러가 스택 오버플로에 대해 강력한 프로세스에 사용하기 위한 것이면 프로파일러 자체에서 스택 오버플로 트리거도 피해야 합니다.

[맨 위로 이동](#top)

<a name="related_topics"></a>

## <a name="related-topics"></a>관련 항목

|제목|설명|
|-----------|-----------------|
|[프로파일링 환경 설정](../../../../docs/framework/unmanaged-api/profiling/setting-up-a-profiling-environment.md)|프로파일러를 초기화하고, 이벤트 알림을 설정하고, Windows 서비스를 프로파일링하는 방법을 설명합니다.|
|[프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)|프로파일링 API에서 사용하는 관리되지 않는 인터페이스를 설명합니다.|
|[프로파일링 전역 정적 함수](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)|프로파일링 API에서 사용하는 관리되지 않는 전역 정적 함수를 설명합니다.|
|[프로파일링 열거형](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)|프로파일링 API에서 사용하는 관리되지 않는 열거형을 설명합니다.|
|[프로파일링 구조체](../../../../docs/framework/unmanaged-api/profiling/profiling-structures.md)|프로파일링 API에서 사용하는 관리되지 않는 구조체를 설명합니다.|
