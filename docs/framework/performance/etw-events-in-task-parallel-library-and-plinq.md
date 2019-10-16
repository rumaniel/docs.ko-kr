---
title: 작업 병렬 라이브러리 및 PLINQ의 ETW 이벤트
ms.date: 03/30/2017
helpviewer_keywords:
- tasks, ETW events
ms.assetid: 87a9cff5-d86f-4e44-a06e-d12764d0dce2
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f1926d2699357163dbb8685b7ea875e369ca29b7
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046651"
---
# <a name="etw-events-in-task-parallel-library-and-plinq"></a>작업 병렬 라이브러리 및 PLINQ의 ETW 이벤트

작업 병렬 라이브러리 및 PLINQ는 둘 다 Windows Performance Analyzer와 같은 도구를 사용하여 애플리케이션을 프로파일링하고 애플리케이션 문제를 해결하는 데 사용할 수 있는 ETW(Windows용 이벤트 추적) 이벤트를 생성합니다. 그러나 대부분의 시나리오에서 병렬 응용 프로그램 코드를 프로 파일링 하는 가장 좋은 방법은 Visual Studio에서 [동시성 시각화 도우미](/visualstudio/profiling/concurrency-visualizer) 를 사용 하는 것입니다.

## <a name="task-parallel-library-etw-events"></a>작업 병렬 라이브러리 ETW 이벤트

EVENT_HEADER 구조에서 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType>, <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.Parallel.Invoke%2A?displayProperty=nameWithType>에 의해 생성된 이벤트에 대한 ProviderId GUID는 다음과 같습니다.

`0x2e5dba47, 0xa3d2, 0x4d16, 0x8e, 0xe0, 0x66, 0x71, 0xff, 0xdc, 0xd7, 0xb5`

### <a name="parallel-loop-begin"></a>병렬 루프 시작

EVENT_DESCRIPTOR.Task = 1

EVENT_DESCRIPTOR.Id = 1

#### <a name="user-data"></a>사용자 데이터

|**이름**|**Type**|**설명**|
|--------------|--------------|---------------------|
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=nameWithType>|루프를 시작한 TaskScheduler의 ID입니다.|
|OriginatingTaskID|<xref:System.Int32?displayProperty=nameWithType>|루프를 시작한 작업의 ID입니다.|
|ForkJoinContextID|<xref:System.Int32?displayProperty=nameWithType>|분기/조인 의미 체계에 따라 이벤트에 대한 중첩 및 쌍을 나타내는 데 사용되는 고유 식별자입니다.|
|OperationType|<xref:System.Int32?displayProperty=nameWithType>|루프 형식을 나타냅니다.<br /><br /> 1 = ParallelInvoke<br /><br /> 2 = ParallelFor<br /><br /> 3 = ParallelForEach|
|InclusiveFrom|<xref:System.Int64?displayProperty=nameWithType>|루프 카운터의 시작 값입니다.|
|ExclusiveTo|<xref:System.Int64?displayProperty=nameWithType>|루프 카운터의 종료 값입니다.|

### <a name="parallel-loop-end"></a>병렬 루프 종료
 EVENT_DESCRIPTOR.Task = 2

 EVENT_DESCRIPTOR.Id = 2

#### <a name="user-data"></a>사용자 데이터

|**이름**|**Type**|**설명**|
|--------------|--------------|---------------------|
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=nameWithType>|루프를 시작한 TaskScheduler의 ID입니다.|
|OriginatingTaskID|<xref:System.Int32?displayProperty=nameWithType>|루프를 시작한 작업의 ID입니다.|
|ForkJoinContextID|<xref:System.Int32?displayProperty=nameWithType>|분기/조인 의미 체계에 따라 이벤트에 대한 중첩 및 쌍을 나타내는 데 사용되는 고유 식별자입니다.|
|totalIterations|<xref:System.Int64?displayProperty=nameWithType>|총 반복 횟수입니다.|

### <a name="parallel-invoke-begin"></a>병렬 호출 시작
 EVENT_DESCRIPTOR.Task = 3

 EVENT_DESCRIPTOR.Id = 3

#### <a name="user-data"></a>사용자 데이터

|**이름**|**Type**|**설명**|
|--------------|--------------|---------------------|
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=nameWithType>|루프를 시작한 TaskScheduler의 ID입니다.|
|OriginatingTaskID|<xref:System.Int32?displayProperty=nameWithType>|루프를 시작한 작업의 ID입니다.|
|ForkJoinContextID|<xref:System.Int32?displayProperty=nameWithType>|분기/조인 의미 체계에 따라 이벤트에 대한 중첩 및 쌍을 나타내는 데 사용되는 고유 식별자입니다.|
|totalIterations|<xref:System.Int64?displayProperty=nameWithType>|총 반복 횟수입니다.|
|operationType|<xref:System.Int32?displayProperty=nameWithType>|루프 형식을 나타냅니다.<br /><br /> 1 = ParallelInvoke<br /><br /> 2 = ParallelFor<br /><br /> 3 = ParallelForEach|
|ActionCount|<xref:System.Int32?displayProperty=nameWithType>|병렬 호출에서 실행될 작업 수입니다.|

### <a name="parallel-invoke-end"></a>병렬 호출 종료
 EVENT_DESCRIPTOR.Task = 4

 EVENT_DESCRIPTOR.Id = 4

#### <a name="user-data"></a>사용자 데이터

|**이름**|**Type**|**설명**|
|--------------|--------------|---------------------|
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=nameWithType>|루프를 시작한 TaskScheduler의 ID입니다.|
|OriginatingTaskID|<xref:System.Int32?displayProperty=nameWithType>|루프를 시작한 작업의 ID입니다.|
|ForkJoinContextID|<xref:System.Int32?displayProperty=nameWithType>|분기/조인 의미 체계에 따라 이벤트에 대한 중첩 및 쌍을 나타내는 데 사용되는 고유 식별자입니다.|

## <a name="plinq-etw-events"></a>PLINQ ETW 이벤트
 PLINQ에 대한 EVENT_HEADER.ProviderId GUID는 다음과 같습니다.

`0x159eeeec, 0x4a14, 0x4418, 0xa8, 0xfe, 0xfa, 0xab, 0xcd, 0x98, 0x78, 0x87`

### <a name="parallel-query-begin"></a>병렬 쿼리 시작
 EVENT_DESCRIPTOR.Task = 1

 EVENT_DESCRIPTOR.Id = 1

#### <a name="user-data"></a>사용자 데이터

|**이름**|**Type**|**설명**|
|--------------|--------------|---------------------|
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=nameWithType>|루프를 시작한 TaskScheduler의 ID입니다.|
|OriginatingTaskID|<xref:System.Int32?displayProperty=nameWithType>|루프를 시작한 작업의 ID입니다.|
|QueryID|<xref:System.Int32?displayProperty=nameWithType>|고유 쿼리 식별자입니다.|

### <a name="parallel-query-end"></a>병렬 쿼리 종료
 EVENT_DESCRIPTOR.Task = 2

 EVENT_DESCRIPTOR.Id = 2

#### <a name="user-data"></a>사용자 데이터

|**이름**|**Type**|**설명**|
|--------------|--------------|---------------------|
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=nameWithType>|루프를 시작한 TaskScheduler의 ID입니다.|
|OriginatingTaskID|<xref:System.Int32?displayProperty=nameWithType>|루프를 시작한 작업의 ID입니다.|
|QueryID|<xref:System.Int32?displayProperty=nameWithType>|고유 쿼리 식별자입니다.|

## <a name="see-also"></a>참고자료

- [.NET Framework의 ETW 이벤트](etw-events.md)
- [TPL(작업 병렬 라이브러리)](../../standard/parallel-programming/task-parallel-library-tpl.md)
- [PLINQ(병렬 LINQ)](../../standard/parallel-programming/parallel-linq-plinq.md)
