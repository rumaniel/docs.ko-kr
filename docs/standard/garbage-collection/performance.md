---
title: 가비지 컬렉션 및 성능
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- garbage collection, troubleshooting
- garbage collection, performance
ms.assetid: c203467b-e95c-4ccf-b30b-953eb3463134
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a0d21ab8af3669575a451644deb2b3572fdb7651
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71354034"
---
# <a name="garbage-collection-and-performance"></a>가비지 컬렉션 및 성능

<a name="top"></a> 이 항목에서는 가비지 컬렉션 및 메모리 사용과 관련된 문제를 설명합니다. 관리되는 힙과 관련된 문제를 해결하고 애플리케이션에 미치는 가비지 컬렉션의 영향을 최소화하는 방법을 설명합니다. 각 문제에는 문제를 조사하는 데 사용할 수 있는 절차 링크가 있습니다.

이 항목에는 다음과 같은 단원이 포함되어 있습니다.

- [성능 분석 도구](#performance_analysis_tools)

- [성능 문제 해결](#troubleshooting_performance_issues)

- [문제 해결 지침](#troubleshooting_guidelines)

- [성능 검사 절차](#performance_check_procedures)

<a name="performance_analysis_tools"></a>

## <a name="performance-analysis-tools"></a>성능 분석 도구

다음 섹션에서는 메모리 사용 및 가비지 컬렉션 문제를 조사하는 데 사용할 수 있는 도구를 설명합니다. 이 항목의 뒷부분에 제공된 [절차](#performance_check_procedures)에서는 이러한 도구를 참조합니다.

<a name="perf_counters"></a>

### <a name="memory-performance-counters"></a>메모리 성능 카운터

성능 카운터를 사용하여 성능 데이터를 수집할 수 있습니다. 자세한 내용은 [런타임 프로파일링](../../../docs/framework/debug-trace-profile/runtime-profiling.md)을 참조하세요. [.NET Framework의 성능 카운터](../../../docs/framework/debug-trace-profile/performance-counters.md)에 설명된 대로 성능 카운터의 .NET CLR 메모리 범주는 가비지 수집기에 대한 정보를 제공합니다.

<a name="sos"></a>

### <a name="debugging-with-sos"></a>SOS를 사용한 디버깅

[Windows 디버거(WinDbg)](/windows-hardware/drivers/debugger/index)를 사용하여 관리되는 힙의 개체를 검사할 수 있습니다.

WinDbg를 설치하려면 [Debugging Tools for Windows 다운로드](/windows-hardware/drivers/debugger/debugger-download-tools) 페이지에서 Debugging Tools for Windows를 설치합니다.

<a name="etw"></a>

### <a name="garbage-collection-etw-events"></a>가비지 컬렉션 ETW 이벤트

ETW(Windows용 이벤트 추적)는 .NET Framework에서 제공하는 프로파일링 및 디버깅 지원을 보완하는 추적 시스템입니다. .NET Framework 4부터 [가비지 수집 ETW 이벤트](../../../docs/framework/performance/garbage-collection-etw-events.md)는 통계 관점에서 관리되는 힙을 분석하는 데 유용한 정보를 캡처합니다. 예를 들어 가비지 수집이 수행되려고 할 때 발생하는 `GCStart_V1` 이벤트는 다음과 같은 정보를 제공합니다.

- 수집되는 개체 세대

- 가비지 수집 트리거

- 가비지 수집 유형(동시 수집 또는 비동시 수집)

ETW 이벤트 로깅은 효율적이며 가비지 수집과 관련된 성능 문제를 숨기지 않습니다. 프로세스에서 ETW 이벤트와 함께 고유한 이벤트를 제공할 수 있습니다. 기록된 경우 애플리케이션 이벤트와 가비지 수집 이벤트를 서로 연결하여 힙 문제가 발생하는 방법 및 시기를 확인할 수 있습니다. 예를 들어 서버 애플리케이션은 클라이언트 요청이 시작되고 끝날 때 이벤트를 제공할 수 있습니다.

<a name="profiling_api"></a>

### <a name="the-profiling-api"></a>프로파일링 API

CLR(공용 언어 런타임) 프로파일링 인터페이스는 가비지 수집 중에 영향을 받은 개체에 대한 자세한 정보를 제공합니다. 가비지 수집이 시작되고 끝날 때 프로파일러에 알릴 수 있습니다. 각 세대의 개체 ID를 포함하여 관리되는 힙의 개체에 대한 보고서를 제공할 수 있습니다. 자세한 내용은 [프로파일링 개요](../../../docs/framework/unmanaged-api/profiling/profiling-overview.md)를 참조하세요.

프로파일러는 포괄적인 정보를 제공할 수 있습니다. 그러나 복잡한 프로파일러는 애플리케이션의 동작을 수정할 가능성이 있습니다.

### <a name="application-domain-resource-monitoring"></a>애플리케이션 도메인 리소스 모니터링

.NET Framework 4부터 ARM(애플리케이션 도메인 리소스 모니터링)을 통해 호스트가 애플리케이션 도메인별로 CPU 및 메모리 사용량을 모니터링할 수 있습니다. 자세한 내용은 [애플리케이션 도메인 리소스 모니터링](../../../docs/standard/garbage-collection/app-domain-resource-monitoring.md)을 참조하세요.

[맨 위로 이동](#top)

<a name="troubleshooting_performance_issues"></a>

## <a name="troubleshooting-performance-issues"></a>성능 문제 해결

첫 번째 단계에서는 [문제가 실제로 가비지 컬렉션인지 여부를 확인](#IsGC)합니다. 확인되었으면 다음 목록에서 선택하여 문제를 해결합니다.

- [메모리 부족 예외가 발생합니다.](#Issue_OOM)

- [프로세스에서 메모리를 너무 많이 사용합니다.](#Issue_TooMuchMemory)

- [가비지 수집기가 개체를 충분히 빠르게 회수하지 않습니다.](#Issue_NotFastEnough)

- [관리되는 힙이 너무 조각화되었습니다.](#Issue_Fragmentation)

- [가비지 컬렉션 일시 중지가 너무 깁니다.](#Issue_LongPauses)

- [0세대가 너무 큽니다.](#Issue_Gen0)

- [가비지 컬렉션 중 CPU 사용량이 너무 많습니다.](#Issue_HighCPU)

<a name="Issue_OOM"></a>

### <a name="issue-an-out-of-memory-exception-is-thrown"></a>문제: 메모리 부족 예외가 발생합니다.

관리되는 <xref:System.OutOfMemoryException>이 발생하는 다음 두 가지 정당한 경우가 있습니다.

- 가상 메모리 부족.

  가비지 수집기는 미리 결정된 크기의 세그먼트로 시스템의 메모리를 할당합니다. 할당에 추가 세그먼트가 필요하지만 프로세스의 가상 메모리 공간에 연속된 여유 블록이 남지 않은 경우 관리되는 힙에 대한 할당이 실패합니다.

- 할당할 실제 메모리 부족

|성능 검사|
|------------------------|
|[메모리 부족 예외가 관리되는지 여부를 확인합니다.](#OOMIsManaged)<br /><br /> [예약할 수 있는 가상 메모리 양을 확인합니다.](#GetVM)<br /><br /> [실제 메모리가 충분한지 확인합니다.](#Physical)|

예외가 정당하지 않다고 확인되면 다음 정보와 함께 Microsoft 고객 지원 담당자에게 문의하세요.

- 관리되는 메모리 부족 예외가 발생한 스택

- 전체 메모리 덤프

- 가상 메모리 또는 실제 메모리가 문제가 아님을 보여 주는 데이터를 포함하여 정당한 메모리 부족 예외가 아님을 입증하는 데이터

<a name="Issue_TooMuchMemory"></a>

### <a name="issue-the-process-uses-too-much-memory"></a>문제: 프로세스에서 메모리를 너무 많이 사용합니다.

일반적인 가정은 Windows 작업 관리자 **성능** 탭의 메모리 사용량 표시에서 메모리가 너무 많이 사용되는 경우를 나타낼 수 있다는 것입니다. 그러나 해당 표시는 작업 집합과 관련이 있고 가상 메모리 사용량에 대한 정보는 제공하지 않습니다.

문제가 관리되는 힙에서 발생한 것이면 시간별로 관리되는 힙을 측정하여 패턴을 확인합니다.

문제가 관리되는 힙에서 발생한 것이 아니면 네이티브 디버깅을 사용해야 합니다.

|성능 검사|
|------------------------|
|[예약할 수 있는 가상 메모리 양을 확인합니다.](#GetVM)<br /><br /> [관리되는 힙이 커밋 중인 메모리 양을 확인합니다.](#ManagedHeapCommit)<br /><br /> [관리되는 힙이 예약하는 메모리 양을 확인합니다.](#ManagedHeapReserve)<br /><br /> [2세대의 대형 개체를 확인합니다.](#ExamineGen2)<br /><br /> [개체에 대한 참조를 확인합니다.](#ObjRef)|

<a name="Issue_NotFastEnough"></a>

### <a name="issue-the-garbage-collector-does-not-reclaim-objects-fast-enough"></a>문제: 가비지 수집기가 개체를 충분히 빠르게 회수하지 않습니다.

개체가 가비지 수집에 예상되는 대로 회수되지 않는 것처럼 보이면 해당 개체에 대한 강력한 참조가 있는지 확인해야 합니다.

비활성 개체를 포함하는 세대에 대한 가비지 수집이 없어 비활성 개체에 대한 종료자가 실행되지 않았음을 나타내는 경우 이 문제가 발생할 수도 있습니다. 예를 들어 STA(단일 스레드 아파트) 애플리케이션을 실행 중이며 종료자 큐를 서비스하는 스레드가 큐를 호출할 수 없는 경우에 발생할 수 있습니다.

|성능 검사|
|------------------------|
|[개체에 대한 참조를 확인합니다.](#ObjRef)<br /><br /> [종료자가 실행되었는지 여부를 확인합니다.](#Induce)<br /><br /> [종료 대기 중인 개체가 있는지 여부를 확인합니다.](#Finalize)|

<a name="Issue_Fragmentation"></a>

### <a name="issue-the-managed-heap-is-too-fragmented"></a>문제: 관리되는 힙이 너무 조각화되었습니다.

조각화 수준은 세대에 할당된 총 메모리에 대한 여유 공간의 비율로 계산됩니다. 2세대에 적절한 조각화 수준은 20% 이하입니다. 2세대는 매우 커질 수 있으므로 절대값보다 조각화 비율이 더 중요합니다.

새 개체가 할당되는 세대이므로 0세대에 여유 공간이 많은 것은 문제가 되지 않습니다.

조각화는 항상 대형 개체 힙이 압축되지 않아서 발생합니다. 대형 개체 할당 요청을 충족하기 위해 인접한 여유 개체가 자연스럽게 단일 공간으로 축소됩니다.

조각화는 1세대와 2세대에서 문제가 될 수 있습니다. 가비지 수집 후에 이러한 세대에 대량의 여유 공간이 있을 경우 애플리케이션의 개체 사용을 수정해야 할 수 있으며 장기 개체의 수명을 다시 평가하는 것이 좋습니다.

개체를 과도하게 고정하면 조각화가 증가할 수 있습니다. 조각화가 높을 경우 너무 많은 개체가 고정되었을 수 있습니다.

가상 메모리의 조각화로 인해 가비지 수집기에서 세그먼트를 추가할 수 없는 경우 원인은 다음 중 하나일 수 있습니다.

- 다수의 작은 어셈블리를 자주 로드 및 언로드

- 비관리 코드와 상호 운용할 때 COM 개체에 대한 참조를 너무 많이 보유

- 대형 임시 개체를 만들어 대형 개체 힙이 힙 세그먼트를 자주 할당 및 해제

  CLR을 호스트하는 경우 애플리케이션에서 가비지 수집기가 해당 세그먼트를 유지하도록 요청할 수 있습니다. 이 경우 세그먼트 할당 빈도가 감소합니다. 이 작업을 수행하려면 [STARTUP_FLAGS 열거형](../../../docs/framework/unmanaged-api/hosting/startup-flags-enumeration.md)의 STARTUP_HOARD_GC_VM 플래그를 사용합니다.

|성능 검사|
|------------------------|
|[관리되는 힙의 여유 공간 크기를 확인합니다.](#Fragmented)<br /><br /> [고정된 개체 수를 확인합니다.](#Pinned)|

조각화에 대한 정당한 원인이 없다고 생각하는 경우 Microsoft 고객 지원 담당자에게 문의하세요.

<a name="Issue_LongPauses"></a>

### <a name="issue-garbage-collection-pauses-are-too-long"></a>문제: 가비지 수집 일시 중지가 너무 깁니다.

가비지 수집은 소프트 실시간으로 작동하므로 애플리케이션에서 약간의 일시 중지를 허용할 수 있어야 합니다. 소프트 실시간의 기준은 작업의 95%가 시간 내에 완료되어야 한다는 것입니다.

동시 가비지 수집에서는 수집 중에 관리되는 스레드를 실행할 수 있으므로 일시 중지가 최소화됩니다.

단기 가비지 수집(0세대 및 1세대)은 몇 밀리초 동안만 지속되므로 일시 중지를 줄이는 것이 일반적으로 불가능합니다. 그러나 애플리케이션에 의한 할당 요청 패턴을 변경하면 2세대 컬렉션의 일시 중지를 줄일 수 있습니다.

보다 정확한 다른 방법은 [가비지 컬렉션 ETW 이벤트](../../../docs/framework/performance/garbage-collection-etw-events.md)를 사용하는 것입니다. 이벤트 시퀀스에 대한 타임스탬프 차이를 추가하여 컬렉션 타이밍을 찾을 수 있습니다. 전체 컬렉션 시퀀스에는 실행 엔진 일시 중단, 가비지 컬렉션 자체 및 실행 엔진 다시 시작이 포함됩니다.

[가비지 컬렉션 알림](../../../docs/standard/garbage-collection/notifications.md)을 사용하여 서버가 2세대 컬렉션을 수행할지 여부 및 요청을 다른 서버로 다시 라우팅할 경우 일시 중지 문제를 줄일 수 있는지 여부를 확인할 수 있습니다.

|성능 검사|
|------------------------|
|[가비지 컬렉션 기간을 확인합니다.](#TimeInGC)<br /><br /> [가비지 컬렉션이 발생한 이유를 확인합니다.](#Triggered)|

<a name="Issue_Gen0"></a>

### <a name="issue-generation-0-is-too-big"></a>문제: 0세대가 너무 큽니다.

0세대는 워크스테이션 가비지 수집 대신 서버 가비지 수집을 사용하는 경우 특히 64비트 시스템에서 다수의 개체를 포함할 가능성이 큽니다. 이러한 환경에서는 0세대 가비지 수집을 트리거하는 임계값이 더 높으며 0세대 수집이 훨씬 더 커질 수 있기 때문입니다. 가비지 수집이 트리거되기 전에 애플리케이션이 더 많은 메모리를 할당하면 성능이 향상됩니다.

<a name="Issue_HighCPU"></a>

### <a name="issue-cpu-usage-during-a-garbage-collection-is-too-high"></a>문제: 가비지 수집 중 CPU 사용량이 너무 많습니다.

가비지 수집 중 CPU 사용량이 너무 많습니다. 상당한 양의 처리 시간이 가비지 수집에 소요되는 경우 수집 횟수가 너무 빈번하거나 수집이 너무 오래 지속되는 것입니다. 관리되는 힙에서 개체의 할당 비율이 증가하면 가비지 수집이 더 자주 발생합니다. 할당 비율을 낮추면 가비지 수집 빈도가 감소합니다.

`Allocated Bytes/second` 성능 카운터를 사용하여 할당 비율을 모니터링할 수 있습니다. 자세한 내용은 [.NET Framework의 성능 카운터](../../../docs/framework/debug-trace-profile/performance-counters.md)를 참조하세요.

컬렉션 기간은 주로 할당 후 남아 있는 개체 수의 비율입니다. 수집할 많은 개체가 남아 있으면 가비지 수집기가 많은 양의 메모리를 처리해야 합니다. 남은 개체를 압축하는 작업은 오랜 시간이 소요됩니다. 수집 중 처리된 개체 수를 확인하려면 디버거에서 지정된 세대에 대한 가비지 수집의 끝에 중단점을 설정합니다.

|성능 검사|
|------------------------|
|[높은 CPU 사용량이 가비지 컬렉션에 의해 발생한 것인지 여부를 확인합니다.](#HighCPU)<br /><br /> [가비지 컬렉션의 끝에 중단점을 설정합니다.](#GenBreak)|

[맨 위로 이동](#top)

<a name="troubleshooting_guidelines"></a>

## <a name="troubleshooting-guidelines"></a>문제 해결 지침

이 섹션에서는 조사를 시작할 때 고려해야 할 지침을 설명합니다.

### <a name="workstation-or-server-garbage-collection"></a>워크스테이션 또는 서버 가비지 수집

올바른 유형의 가비지 수집을 사용 중인지 확인합니다. 애플리케이션에서 여러 스레드 및 개체 인스턴스를 사용하는 경우 워크스테이션 가비지 수집 대신 서버 가비지 수집을 사용합니다. 서버 가비지 수집은 여러 스레드에서 작동하는 반면, 워크스테이션 가비지 수집에서는 애플리케이션의 여러 인스턴스가 고유한 가비지 수집 스레드를 실행하고 CPU 시간을 경합해야 합니다.

부하가 낮고 백그라운드에서 자주 작업을 수행하지 않는 서비스와 같은 애플리케이션은 동시 가비지 수집을 사용하지 않도록 설정하여 워크스테이션 가비지 수집을 사용할 수 있습니다.

### <a name="when-to-measure-the-managed-heap-size"></a>관리되는 힙 크기를 측정하는 시기

프로파일러를 사용하지 않는 한 효과적으로 성능 문제를 진단하려면 일관된 측정 패턴을 설정해야 합니다. 일정을 설정하려면 다음 사항을 고려합니다.

- 2세대 가비지 수집 후에 측정하는 경우 전체 관리되는 힙의 가비지(비활성 개체)가 제거됩니다.

- 0세대 가비지 수집 직후에 측정하는 경우 1세대 및 2세대의 개체는 아직 수집되지 않습니다.

- 가비지 수집 직전에 측정하는 경우 가비지 수집이 시작되기 전에 가능한 한 많은 할당을 측정합니다.

- 가비지 수집기 데이터 구조는 순회에 유효한 상태가 아니며 완전한 결과를 제공할 수 없으므로 가비지 수집 중에 측정하는 것은 문제가 됩니다. 이것은 의도적인 것입니다.

- 동시 가비지 수집과 함께 워크스테이션 가비지 수집을 사용하는 경우 회수된 개체가 압축되지 않으므로 힙 크기가 동일하거나 더 클 수 있습니다(조각화로 인해 더 크게 보일 수 있음).

- 실제 메모리 부하가 너무 높으면 2세대의 동시 가비지 수집이 지연됩니다.

다음 절차에서는 관리되는 힙을 측정할 수 있도록 중단점을 설정하는 방법을 설명합니다.

<a name="GenBreak"></a>

#### <a name="to-set-a-breakpoint-at-the-end-of-garbage-collection"></a>가비지 수집의 끝에 중단점을 설정하려면

- SOS 디버거 확장이 로드된 WinDbg에서 다음 명령을 입력합니다.

  **bp mscorwks!WKS::GCHeap::RestartEE "j (dwo(mscorwks!WKS::GCHeap::GcCondemnedGeneration)==2) 'kb';'g'"**

  여기서 **GcCondemnedGeneration**은 원하는 세대로 설정됩니다. 이 명령에는 전용 기호가 필요합니다.

  이 명령은 가비지 컬렉션을 위해 2세대 개체가 회수된 후 **RestartEE**가 실행되는 경우 강제로 중단합니다.

  서버 가비지 컬렉션에서는 하나의 스레드만 **RestartEE**를 호출하므로 2세대 가비지 컬렉션 중 한 번만 중단점이 발생합니다.

[맨 위로 이동](#top)

<a name="performance_check_procedures"></a>

## <a name="performance-check-procedures"></a>성능 검사 절차

이 섹션에서는 성능 문제의 원인을 격리시키는 다음 절차를 설명합니다.

- [문제가 가비지 컬렉션에 의해 발생한 것인지 여부를 확인합니다.](#IsGC)

- [메모리 부족 예외가 관리되는지 여부를 확인합니다.](#OOMIsManaged)

- [예약할 수 있는 가상 메모리 양을 확인합니다.](#GetVM)

- [실제 메모리가 충분한지 확인합니다.](#Physical)

- [관리되는 힙이 커밋 중인 메모리 양을 확인합니다.](#ManagedHeapCommit)

- [관리되는 힙이 예약하는 메모리 양을 확인합니다.](#ManagedHeapReserve)

- [2세대의 대형 개체를 확인합니다.](#ExamineGen2)

- [개체에 대한 참조를 확인합니다.](#ObjRef)

- [종료자가 실행되었는지 여부를 확인합니다.](#Induce)

- [종료 대기 중인 개체가 있는지 여부를 확인합니다.](#Finalize)

- [관리되는 힙의 여유 공간 크기를 확인합니다.](#Fragmented)

- [고정된 개체 수를 확인합니다.](#Pinned)

- [가비지 컬렉션 기간을 확인합니다.](#TimeInGC)

- [가비지 컬렉션 트리거를 확인합니다.](#Triggered)

- [높은 CPU 사용량이 가비지 컬렉션에 의해 발생한 것인지 여부를 확인합니다.](#HighCPU)

<a name="IsGC"></a>

### <a name="to-determine-whether-the-problem-is-caused-by-garbage-collection"></a>문제가 가비지 컬렉션에 의해 발생한 것인지 여부를 확인하려면

- 다음 두 개의 메모리 성능 카운터를 검사합니다.

  - **% Time in GC**. 마지막 가비지 컬렉션 주기 이후 가비지 컬렉션을 수행하는 데 소요된 경과 시간의 백분율을 표시합니다. 이 카운터를 사용하여 가비지 수집기가 관리되는 힙 공간을 사용할 수 있도록 하는 데 너무 많은 시간을 소비하고 있는지 여부를 확인할 수 있습니다. 가비지 수집에 소요된 시간이 비교적 적은 경우 관리되는 힙 외부의 리소스 문제를 나타낼 수 있습니다. 이 카운터는 동시 또는 백그라운드 가비지 컬렉션이 관련된 경우 정확하지 않을 수 있습니다.

  - **# Total committed Bytes**. 가비지 컬렉션기에서 현재 커밋한 가상 메모리 크기를 표시합니다. 이 카운터를 사용하여 가비지 수집기에서 사용되는 메모리가 애플리케이션에서 사용되는 메모리에 비해 과도하게 많은지 여부를 확인할 수 있습니다.

  대부분의 메모리 성능 카운터는 각 가비지 수집이 끝날 때 업데이트됩니다. 따라서 정보를 확인하려는 현재 상태가 반영되지 않을 수 있습니다.

<a name="OOMIsManaged"></a>

### <a name="to-determine-whether-the-out-of-memory-exception-is-managed"></a>메모리 부족 예외가 관리되는지 여부를 확인하려면

1. SOS 디버거 확장이 로드된 WinDbg 또는 Visual Studio 디버거에서 예외 인쇄(**pe**) 명령을 입력합니다.

    **!pe**

    예외가 관리되는 경우 다음 예제와 같이 <xref:System.OutOfMemoryException>이 예외 형식으로 표시됩니다.

    ```console
    Exception object: 39594518
    Exception type: System.OutOfMemoryException
    Message: <none>
    InnerException: <none>
    StackTrace (generated):
    ```

2. 출력에서 예외를 지정하지 않는 경우 메모리 부족 예외가 발생한 스레드를 확인해야 합니다. 디버거에서 다음 명령을 입력하여 호출 스택과 함께 모든 스레드를 표시합니다.

    **~\*kb**

    예외 호출이 포함된 스택이 있는 스레드는 `RaiseTheException` 인수로 표시됩니다. 이는 관리되는 예외 개체입니다.

    ```console
    28adfb44 7923918f 5b61f2b4 00000000 5b61f2b4 mscorwks!RaiseTheException+0xa0
    ```

3. 다음 명령을 사용하여 중첩된 예외를 덤프할 수 있습니다.

    **!pe -nested**

    예외를 찾을 수 없는 경우 메모리 부족 예외가 비관리 코드에서 발생한 것입니다.

<a name="GetVM"></a>

### <a name="to-determine-how-much-virtual-memory-can-be-reserved"></a>예약할 수 있는 가상 메모리 양을 확인하려면

- SOS 디버거 확장이 로드된 WinDbg에서 다음 명령을 입력하여 최대 여유 영역을 가져옵니다.

  **!address -summary**

  다음 출력과 같이 최대 여유 영역이 표시됩니다.

  ```console
  Largest free region: Base 54000000 - Size 0003A980
  ```

  이 예제에서 최대 여유 영역의 크기는 약 24000KB(16진수로 3A980)입니다. 이 영역은 가비지 수집기에서 세그먼트에 필요한 크기보다 훨씬 작습니다.

  또는

- 다음 **vmstat** 명령을 사용합니다.

  **!vmstat**

  다음 출력과 같이 최대 여유 영역은 MAXIMUM 열에서 가장 큰 값입니다.

  ```console
  TYPE        MINIMUM   MAXIMUM     AVERAGE   BLK COUNT   TOTAL
  ~~~~        ~~~~~~~   ~~~~~~~     ~~~~~~~   ~~~~~~~~~~  ~~~~
  Free:
  Small       8K        64K         46K       36          1,671K
  Medium      80K       864K        349K      3           1,047K
  Large       1,384K    1,278,848K  151,834K  12          1,822,015K
  Summary     8K        1,278,848K  35,779K   51          1,824,735K
  ```

<a name="Physical"></a>

### <a name="to-determine-whether-there-is-enough-physical-memory"></a>실제 메모리가 충분한지 확인하려면

1. Windows 작업 관리자를 시작합니다.

2. **성능** 탭에서 커밋된 값을 확인합니다. Windows 7에서는 **시스템 그룹**의 **커밋(KB)** 을 확인합니다.

    **합계**가 **제한**에 가까우면 실제 메모리가 부족한 것입니다.

<a name="ManagedHeapCommit"></a>

### <a name="to-determine-how-much-memory-the-managed-heap-is-committing"></a>관리되는 힙이 커밋 중인 메모리 양을 확인하려면

- `# Total committed bytes` 메모리 성능 카운터를 사용하여 관리되는 힙에서 커밋 중인 바이트 수를 가져올 수 있습니다. 가비지 수집기는 동시에 모두 커밋하지 않고 필요에 따라 세그먼트의 청크를 커밋합니다.

  > [!NOTE]
  > `# Bytes in all Heaps` 성능 카운터는 관리되는 힙의 실제 메모리 사용량을 나타내지 않으므로 사용하지 마세요. 세대 크기가 이 값에 포함되며 실제로 해당 임계값 크기, 즉 세대가 개체로 채워진 경우 가비지 수집을 실행하는 크기입니다. 따라서 이 값은 일반적으로 0입니다.

<a name="ManagedHeapReserve"></a>

### <a name="to-determine-how-much-memory-the-managed-heap-reserves"></a>관리되는 힙이 예약하는 메모리 양을 확인하려면

- `# Total reserved bytes` 메모리 성능 카운터를 사용합니다.

  가비지 수집기는 세그먼트의 메모리를 예약하고, **eeheap** 명령을 사용하여 세그먼트가 시작되는 위치를 확인할 수 있습니다.

  > [!IMPORTANT]
  > 가비지 수집기가 각 세그먼트에 대해 할당하는 메모리 양은 확인할 수 있지만 세그먼트 크기는 구현마다 다르며 정기 업데이트를 포함하여 언제든지 변경될 수 있습니다. 앱에서 특정 세그먼트 크기를 가정하거나 의존해서는 안 되며, 세그먼트 할당에 사용할 수 있는 메모리 크기를 구성하려고 해서도 안 됩니다.

- SOS 디버거 확장이 로드된 WinDbg 또는 Visual Studio 디버거에서 다음 명령을 입력합니다.

  **!eeheap -gc**

  결과는 다음과 같습니다.

  ```console
  Number of GC Heaps: 2
  ------------------------------
  Heap 0 (002db550)
  generation 0 starts at 0x02abe29c
  generation 1 starts at 0x02abdd08
  generation 2 starts at 0x02ab0038
  ephemeral segment allocation context: none
    segment    begin allocated     size
  02ab0000 02ab0038  02aceff4 0x0001efbc(126908)
  Large object heap starts at 0x0aab0038
    segment    begin allocated     size
  0aab0000 0aab0038  0aab2278 0x00002240(8768)
  Heap Size   0x211fc(135676)
  ------------------------------
  Heap 1 (002dc958)
  generation 0 starts at 0x06ab1bd8
  generation 1 starts at 0x06ab1bcc
  generation 2 starts at 0x06ab0038
  ephemeral segment allocation context: none
    segment    begin allocated     size
  06ab0000 06ab0038  06ab3be4 0x00003bac(15276)
  Large object heap starts at 0x0cab0038
    segment    begin allocated     size
  0cab0000 0cab0038  0cab0048 0x00000010(16)
  Heap Size    0x3bbc(15292)
  ------------------------------
  GC Heap Size   0x24db8(150968)
  ```

  "segment"로 표시된 주소는 세그먼트의 시작 주소입니다.

<a name="ExamineGen2"></a>

### <a name="to-determine-large-objects-in-generation-2"></a>2세대의 대형 개체를 확인하려면

- SOS 디버거 확장이 로드된 WinDbg 또는 Visual Studio 디버거에서 다음 명령을 입력합니다.

  **!dumpheap –stat**

  관리되는 힙이 크면 **dumpheap**을 완료하는 데 오랜 시간이 걸릴 수 있습니다.

  가장 많은 공간을 사용하는 개체를 나열하는 출력의 마지막 몇 줄에서 분석을 시작하는 것이 좋습니다. 예:

  ```console
  2c6108d4   173712     14591808 DevExpress.XtraGrid.Views.Grid.ViewInfo.GridCellInfo
  00155f80      533     15216804      Free
  7a747c78   791070     15821400 System.Collections.Specialized.ListDictionary+DictionaryNode
  7a747bac   700930     19626040 System.Collections.Specialized.ListDictionary
  2c64e36c    78644     20762016 DevExpress.XtraEditors.ViewInfo.TextEditViewInfo
  79124228   121143     29064120 System.Object[]
  035f0ee4    81626     35588936 Toolkit.TlkOrder
  00fcae40     6193     44911636 WaveBasedStrategy.Tick_Snap[]
  791242ec    40182     90664128 System.Collections.Hashtable+bucket[]
  790fa3e0  3154024    137881448 System.String
  Total 8454945 objects
  ```

  마지막에 나열된 개체는 문자열이며 가장 많은 공간을 사용합니다. 애플리케이션을 검사하여 문자열 개체를 최적화할 수 있는 방법을 확인할 수 있습니다. 150바이트에서 200바이트 사이의 문자열을 확인하려면 다음을 입력합니다.

  **!dumpheap -type System.String -min 150 -max 200**

  결과의 예는 다음과 같습니다.

  ```console
  Address  MT           Size  Gen
  1875d2c0 790fa3e0      152    2 System.String HighlightNullStyle_Blotter_PendingOrder-11_Blotter_PendingOrder-11
  …
  ```

  ID 문자열 대신 정수를 사용하면 더 효율적일 수 있습니다. 같은 문자열이 수천 번 반복되는 경우 문자열 인터닝을 고려합니다. 문자열 인터닝에 대한 자세한 내용은 <xref:System.String.Intern%2A?displayProperty=nameWithType> 메서드에 대한 참조 항목을 참조하세요.

<a name="ObjRef"></a>

### <a name="to-determine-references-to-objects"></a>개체에 대한 참조를 확인하려면

- SOS 디버거 확장이 로드된 WinDbg에서 다음 명령을 입력하여 개체에 대한 참조를 나열합니다.

  **!gcroot**

  `-or-`

- 특정 개체에 대한 참조를 확인하려면 다음과 같이 주소를 포함합니다.

  **!gcroot 1c37b2ac**

  스택에서 발견된 루트는 가양성(false positive)일 수 있습니다. 자세한 내용을 보려면 `!help gcroot` 명령을 사용하세요.

  ```console
  ebx:Root:19011c5c(System.Windows.Forms.Application+ThreadContext)->
  19010b78(DemoApp.FormDemoApp)->
  19011158(System.Windows.Forms.PropertyStore)->
  … [omitted]
  1c3745ec(System.Data.DataTable)->
  1c3747a8(System.Data.DataColumnCollection)->
  1c3747f8(System.Collections.Hashtable)->
  1c376590(System.Collections.Hashtable+bucket[])->
  1c376c98(System.Data.DataColumn)->
  1c37b270(System.Data.Common.DoubleStorage)->
  1c37b2ac(System.Double[])
  Scan Thread 0 OSTHread 99c
  Scan Thread 6 OSTHread 484
  ```

  **gcroot** 명령을 완료하는 데 오랜 시간이 걸릴 수 있습니다. 가비지 컬렉션에 의해 회수되지 않은 개체는 모두 라이브 개체입니다. 이는 일부 루트가 직접 또는 간접적으로 개체에 연결되어 있으므로 **gcroot**에서 개체의 경로 정보가 반환되어야 함을 의미합니다. 반환된 그래프를 검사하고 이러한 개체가 여전히 참조되는 이유를 확인해야 합니다.

<a name="Induce"></a>

### <a name="to-determine-whether-a-finalizer-has-been-run"></a>종료자가 실행되었는지 여부를 확인하려면

- 다음 코드가 포함된 테스트 프로그램을 실행합니다.

  ```csharp
  GC.Collect();
  GC.WaitForPendingFinalizers();
  GC.Collect();
  ```

  테스트에서 문제가 해결되는 경우 이는 해당 개체에 대한 종료자가 일시 중단되어 가비지 수집기가 개체를 회수하지 못했음을 의미합니다. <xref:System.GC.WaitForPendingFinalizers%2A?displayProperty=nameWithType> 메서드는 종료자가 해당 작업을 완료할 수 있도록 하며 문제를 해결합니다.

<a name="Finalize"></a>

### <a name="to-determine-whether-there-are-objects-waiting-to-be-finalized"></a>종료 대기 중인 개체가 있는지 여부를 확인하려면

1. SOS 디버거 확장이 로드된 WinDbg 또는 Visual Studio 디버거에서 다음 명령을 입력합니다.

    **!finalizequeue**

    종료 준비가 된 개체 수를 확인합니다. 개수가 많을 경우 이러한 종료자가 전혀 처리할 수 없거나 충분히 빨리 처리할 수 없는 이유를 검사해야 합니다.

2. 스레드의 출력을 가져오려면 다음 명령을 입력합니다.

    **threads -special**

    이 명령은 다음과 같은 출력을 제공합니다.

    ```console
       OSID     Special thread type
    2    cd0    DbgHelper
    3    c18    Finalizer
    4    df0    GC SuspendEE
    ```

    종료자 스레드는 현재 실행 중인 종료자(있는 경우)를 나타냅니다. 종료자 스레드가 종료자를 실행하지 않는 경우 해당 작업을 수행하도록 지시할 이벤트를 기다리고 있습니다. 종료자 스레드는 THREAD_HIGHEST_PRIORITY에서 실행되고 종료자(있는 경우) 실행을 매우 빠르게 완료하기 때문에 대부분의 경우 이 상태의 종료자 스레드가 표시됩니다.

<a name="Fragmented"></a>

### <a name="to-determine-the-amount-of-free-space-in-the-managed-heap"></a>관리되는 힙의 여유 공간 크기를 확인하려면

- SOS 디버거 확장이 로드된 WinDbg 또는 Visual Studio 디버거에서 다음 명령을 입력합니다.

  **!dumpheap -type Free -stat**

  이 명령은 다음 예제와 같이 관리되는 힙에서 사용 가능한 모든 개체의 전체 크기를 표시합니다.

  ```console
  total 230 objects
  Statistics:
        MT    Count    TotalSize Class Name
  00152b18      230     40958584      Free
  Total 230 objects
  ```

- 0세대의 여유 공간을 확인하려면 세대별 메모리 소비 정보를 위해 다음 명령을 입력합니다.

  **!eeheap -gc**

  이 명령은 다음과 유사한 출력을 표시합니다. 마지막 줄은 단기 세그먼트를 보여 줍니다.

  ```console
  Heap 0 (0015ad08)
  generation 0 starts at 0x49521f8c
  generation 1 starts at 0x494d7f64
  generation 2 starts at 0x007f0038
  ephemeral segment allocation context: none
  segment  begin     allocated  size
  00178250 7a80d84c  7a82f1cc   0x00021980(137600)
  00161918 78c50e40  78c7056c   0x0001f72c(128812)
  007f0000 007f0038  047eed28   0x03ffecf0(67103984)
  3a120000 3a120038  3a3e84f8   0x002c84c0(2917568)
  46120000 46120038  49e05d04   0x03ce5ccc(63855820)
  ```

- 0세대에서 사용되는 공간을 계산합니다.

  **? 49e05d04-0x49521f8c**

  결과는 다음과 같습니다. 0세대는 약 9MB입니다.

  ```console
  Evaluate expression: 9321848 = 008e3d78
  ```

- 다음 명령은 0세대 범위 내의 여유 공간을 덤프합니다.

  **!dumpheap -type Free -stat 0x49521f8c 49e05d04**

  결과는 다음과 같습니다.

  ```console
  ------------------------------
  Heap 0
  total 409 objects
  ------------------------------
  Heap 1
  total 0 objects
  ------------------------------
  Heap 2
  total 0 objects
  ------------------------------
  Heap 3
  total 0 objects
  ------------------------------
  total 409 objects
  Statistics:
        MT    Count TotalSize Class Name
  0015a498      409   7296540      Free
  Total 409 objects
  ```

  이 출력은 힙의 0세대 부분에서 개체에 9MB 공간을 사용하고 있으며 여유 공간이 7MB임을 보여 줍니다. 이 분석은 0세대가 조각화에 기여하는 정도를 보여 줍니다. 장기 개체에 의한 조각화의 원인으로 계산된 전체 크기에서 이 힙 사용량을 차감해야 합니다.

<a name="Pinned"></a>

### <a name="to-determine-the-number-of-pinned-objects"></a>고정된 개체 수를 확인하려면

- SOS 디버거 확장이 로드된 WinDbg 또는 Visual Studio 디버거에서 다음 명령을 입력합니다.

  **!gchandles**

  다음 예제와 같이 표시된 통계는 고정된 핸들 수를 포함합니다.

  ```console
  GC Handle Statistics:
  Strong Handles:      29
  Pinned Handles:      10
  ```

<a name="TimeInGC"></a>

### <a name="to-determine-the-length-of-time-in-a-garbage-collection"></a>가비지 수집 기간을 확인하려면

- `% Time in GC` 메모리 성능 카운터를 검사합니다.

  값은 샘플 간격 시간을 사용하여 계산됩니다. 각 가비지 수집이 끝날 때 카운터가 업데이트되므로 간격 중에 수집이 발생하지 않은 경우 현재 샘플은 이전 샘플과 동일한 값을 갖습니다.

  수집 시간은 샘플 간격 시간에 백분율 값을 곱하여 구합니다.

  다음 데이터는 8초 연구를 위해 2초 샘플링 간격 4개를 보여 줍니다. `Gen0`, `Gen1` 및 `Gen2` 열은 해당 세대에 대해 해당 간격 중에 발생한 가비지 수집 횟수를 보여 줍니다.

  ```console
  Interval    Gen0    Gen1    Gen2    % Time in GC
          1       9       3       1              10
          2      10       3       1               1
          3      11       3       1               3
          4      11       3       1               3
  ```

  이 정보는 가비지 수집이 발생한 시간을 표시하지 않지만 시간 간격에서 발생한 가비지 수집 횟수를 확인할 수 있습니다. 최악의 경우를 가정하여 2번째 간격이 시작될 때 10번째 0세대 가비지 수집이 완료되었으며 5번째 간격이 끝날 때 11번째 0세대 가비지 수집이 완료되었습니다. 10번째 가비지 수집의 끝과 11번째 가비지 수집의 끝 사이의 시간은 약 2초이며, 성능 카운터에 3%가 표시되므로 11번째 0세대 가비지 수집 기간은 (2초 * 3% = 60ms)입니다.

  이 예제에서는 5개 기간이 있습니다.

  ```console
  Interval    Gen0    Gen1    Gen2     % Time in GC
          1       9       3       1                3
          2      10       3       1                1
          3      11       4       2                1
          4      11       4       2                1
          5      11       4       2               20
  ```

  2번째 2세대 가비지 수집은 3번째 간격 중에 시작되고 5번째 간격에 완료되었습니다. 최악의 경우를 가정하여 0세대에 대한 마지막 수집은 2번째 간격이 시작될 때 완료된 수집이었으며 5번째 간격이 끝날 때 2세대 가비지 수집이 완료되었습니다. 따라서 0세대 가비지 수집의 끝과 2세대 가비지 수집의 끝 사이의 시간은 4초입니다. `% Time in GC` 카운터는 20%이므로 2세대 가비지 수집에 소요되었을 수 있는 최대 시간은 (4초 * 20% = 800ms)입니다.

- 또는 [가비지 컬렉션 ETW 이벤트](../../../docs/framework/performance/garbage-collection-etw-events.md)를 사용하여 가비지 컬렉션 길이를 결정하고 정보를 분석하여 가비지 컬렉션 기간을 확인할 수 있습니다.

  예를 들어 다음 데이터는 비 동시 가비지 컬렉션 중에 발생한 이벤트 시퀀스를 보여 줍니다.

  ```console
  Timestamp    Event name
  513052        GCSuspendEEBegin_V1
  513078        GCSuspendEEEnd
  513090        GCStart_V1
  517890        GCEnd_V1
  517894        GCHeapStats
  517897        GCRestartEEBegin
  517918        GCRestartEEEnd
  ```

  관리되는 스레드를 일시 중단하는 데 26us(`GCSuspendEEEnd` – `GCSuspendEEBegin_V1`) 걸렸습니다.

  실제 가비지 수집에 4.8ms(`GCEnd_V1` – `GCStart_V1`) 걸렸습니다.

  관리되는 스레드를 다시 시작하는 데 21us(`GCRestartEEEnd` – `GCRestartEEBegin`) 걸렸습니다.

  다음 출력은 백그라운드 가비지 수집에 대한 예제를 제공하며 프로세스, 스레드 및 이벤트 필드를 포함합니다. 일부 데이터만 표시됩니다.

  ```console
  timestamp(us)    event name            process    thread    event field
  42504385        GCSuspendEEBegin_V1    Test.exe    4372             1
  42504648        GCSuspendEEEnd         Test.exe    4372
  42504816        GCStart_V1             Test.exe    4372        102019
  42504907        GCStart_V1             Test.exe    4372        102020
  42514170        GCEnd_V1               Test.exe    4372
  42514204        GCHeapStats            Test.exe    4372        102020
  42832052        GCRestartEEBegin       Test.exe    4372
  42832136        GCRestartEEEnd         Test.exe    4372
  63685394        GCSuspendEEBegin_V1    Test.exe    4744             6
  63686347        GCSuspendEEEnd         Test.exe    4744
  63784294        GCRestartEEBegin       Test.exe    4744
  63784407        GCRestartEEEnd         Test.exe    4744
  89931423        GCEnd_V1               Test.exe    4372        102019
  89931464        GCHeapStats            Test.exe    4372
  ```

  42504816의 `GCStart_V1` 이벤트는 마지막 필드가 `1`이므로 백그라운드 가비지 수집임을 나타냅니다. 가비지 수집 번호 102019가 됩니다.

  `GCStart` 이벤트는 백그라운드 가비지 수집을 시작하기 전에 단기 가비지 수집이 필요한 경우에 발생합니다. 가비지 수집 번호 102020이 됩니다.

  42514170에서 가비지 수집 번호 102020이 완료됩니다. 이 지점에서 관리되는 스레드가 다시 시작됩니다. 이 수집은 이 백그라운드 가비지 수집을 트리거한 스레드 4372에서 완료됩니다.

  스레드 4744에서 일시 중단이 발생합니다. 백그라운드 가비지 수집이 관리되는 스레드를 일시 중단해야 하는 경우는 이때뿐입니다. 이 기간은 약 99ms((63784407-63685394)/1000)입니다.

  백그라운드 가비지 수집에 대한 `GCEnd` 이벤트는 89931423에 있습니다. 이는 백그라운드 가비지 수집이 약 47초((89931423-42504816)/1000) 동안 지속되었음을 의미합니다.

  관리되는 스레드가 실행되는 동안 개수에 관계없이 발생하는 단기 가비지 수집을 확인할 수 있습니다.

<a name="Triggered"></a>

### <a name="to-determine-what-triggered-a-garbage-collection"></a>가비지 수집 트리거를 확인하려면

- SOS 디버거 확장이 로드된 WinDbg 또는 Visual Studio 디버거에서 다음 명령을 입력하여 호출 스택과 함께 모든 스레드를 표시합니다.

  **~\*kb**

  이 명령은 다음과 유사한 출력을 표시합니다.

  ```console
  0012f3b0 79ff0bf8 mscorwks!WKS::GCHeap::GarbageCollect
  0012f454 30002894 mscorwks!GCInterface::CollectGeneration+0xa4
  0012f490 79fa22bd fragment_ni!request.Main(System.String[])+0x48
  ```

  가비지 수집이 운영 체제의 메모리 부족 알림으로 인해 발생한 경우 스레드가 종료자 스레드라는 것을 제외하면 호출 스택이 비슷합니다. 종료자 스레드는 비동기 메모리 부족 알림을 가져오고 가비지 수집을 실행합니다.

  가비지 수집이 메모리 할당에 의해 발생한 경우 스택이 다음과 같이 나타납니다.

  ```console
  0012f230 7a07c551 mscorwks!WKS::GCHeap::GarbageCollectGeneration
  0012f2b8 7a07cba8 mscorwks!WKS::gc_heap::try_allocate_more_space+0x1a1
  0012f2d4 7a07cefb mscorwks!WKS::gc_heap::allocate_more_space+0x18
  0012f2f4 7a02a51b mscorwks!WKS::GCHeap::Alloc+0x4b
  0012f310 7a02ae4c mscorwks!Alloc+0x60
  0012f364 7a030e46 mscorwks!FastAllocatePrimitiveArray+0xbd
  0012f424 300027f4 mscorwks!JIT_NewArr1+0x148
  000af70f 3000299f fragment_ni!request..ctor(Int32, Single)+0x20c
  0000002a 79fa22bd fragment_ni!request.Main(System.String[])+0x153
  ```

  결국 Just-In-Time 도우미(`JIT_New*`)가 `GCHeap::GarbageCollectGeneration`을 호출합니다. 2세대 가비지 수집이 할당에 의해 발생한 경우 2세대 가비지 수집에서 수집된 개체와 이를 방지하는 방법을 확인해야 합니다. 즉, 2세대 가비지 수집의 시작과 끝 사이의 차이 및 2세대 수집을 발생시킨 개체를 확인하려고 합니다.

  예를 들어 디버거에서 다음 명령을 입력하여 2세대 컬렉션의 시작을 표시합니다.

  **!dumpheap –stat**

  예제 출력(가장 많은 공간을 사용하는 개체를 표시하기 위해 요약됨):

  ```console
  79124228    31857      9862328 System.Object[]
  035f0384    25668     11601936 Toolkit.TlkPosition
  00155f80    21248     12256296      Free
  79103b6c   297003     13068132 System.Threading.ReaderWriterLock
  7a747ad4   708732     14174640 System.Collections.Specialized.HybridDictionary
  7a747c78   786498     15729960 System.Collections.Specialized.ListDictionary+DictionaryNode
  7a747bac   700298     19608344 System.Collections.Specialized.ListDictionary
  035f0ee4    89192     38887712 Toolkit.TlkOrder
  00fcae40     6193     44911636 WaveBasedStrategy.Tick_Snap[]
  7912c444    91616     71887080 System.Double[]
  791242ec    32451     82462728 System.Collections.Hashtable+bucket[]
  790fa3e0  2459154    112128436 System.String
  Total 6471774 objects
  ```

  2세대의 끝에서 명령을 반복합니다.

  **!dumpheap –stat**

  예제 출력(가장 많은 공간을 사용하는 개체를 표시하기 위해 요약됨):

  ```console
  79124228    26648      9314256 System.Object[]
  035f0384    25668     11601936 Toolkit.TlkPosition
  79103b6c   296770     13057880 System.Threading.ReaderWriterLock
  7a747ad4   708730     14174600 System.Collections.Specialized.HybridDictionary
  7a747c78   786497     15729940 System.Collections.Specialized.ListDictionary+DictionaryNode
  7a747bac   700298     19608344 System.Collections.Specialized.ListDictionary
  00155f80    13806     34007212      Free
  035f0ee4    89187     38885532 Toolkit.TlkOrder
  00fcae40     6193     44911636 WaveBasedStrategy.Tick_Snap[]
  791242ec    32370     82359768 System.Collections.Hashtable+bucket[]
  790fa3e0  2440020    111341808 System.String
  Total 6417525 objects
  ```

  `double[]` 개체가 출력의 끝에서 사라졌으며, 이는 수집되었음을 의미합니다. 이러한 개체가 약 70MB를 차지합니다. 나머지 개체는 많이 변경되지 않았습니다. 따라서 이러한 `double[]` 개체가 이 2세대 가비지 수집이 발생한 이유입니다. 다음 단계에서는 `double[]` 개체가 있는 이유 및 작동하지 않는 이유를 확인합니다. 이러한 개체가 어디서 온 것인지 코드 개발자에게 묻거나 **gcroot** 명령을 사용할 수 있습니다.

<a name="HighCPU"></a>

### <a name="to-determine-whether-high-cpu-usage-is-caused-by-garbage-collection"></a>높은 CPU 사용량이 가비지 컬렉션에 의해 발생한 것인지 여부를 확인하려면

- `% Time in GC` 메모리 성능 카운터 값을 프로세스 시간과 상호 연결합니다.

  `% Time in GC` 값이 프로세스 시간과 동시에 급증하는 경우 가비지 수집으로 인해 CPU 사용량이 증가한 것입니다. 그러지 않으면 애플리케이션을 프로파일링하여 높은 사용량이 발생하는 위치를 찾습니다.

## <a name="see-also"></a>참고 항목

- [가비지 수집](../../../docs/standard/garbage-collection/index.md)
