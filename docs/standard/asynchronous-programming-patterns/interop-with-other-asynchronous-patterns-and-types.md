---
title: 다른 비동기 패턴 및 형식과의 Interop
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- .NET Framework, and TAP
- asynchronous design patterns, .NET Framework
- TAP, .NET Framework support for
- Task-based Asynchronous Pattern, .NET Framework support for
- .NET Framework, asynchronous design patterns
ms.assetid: f120a5d9-933b-4d1d-acb6-f034a57c3749
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 05b53016712f75e45636979d77bfd27116ce8e14
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48850663"
---
# <a name="interop-with-other-asynchronous-patterns-and-types"></a>다른 비동기 패턴 및 형식과의 Interop
.NET Framework 1.0에서는 <xref:System.IAsyncResult> 또는 [Begin/End](../../../docs/standard/asynchronous-programming-patterns/asynchronous-programming-model-apm.md)패턴이라고도 하는 `Begin/End` 패턴이 도입되었습니다.  .NET Framework 2.0에서는 [Event-based Asynchronous Pattern (EAP)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)이 추가되었습니다.  .NET Framework 4부터 [Task-based Asynchronous Pattern (TAP)](../../../docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md) 이 APM과 EAP를 둘 다 대체하지만 이전 패턴에서 마이그레이션 루틴을 쉽게 빌드할 수 있는 기능을 제공합니다.  
  
 항목 내용:  
  
-   [작업 및 APM](#APM) ([APM에서 TAP로](#ApmToTap) 또는 [TAP에서 APM으로](#TapToApm))  
  
-   [작업 및 EAP](#EAP)  
  
-   [작업 및 대기 핸들](#WaitHandles) ([대기 핸들에서 TAP로](#WHToTap) 또는 [TAP에서 대기 핸들로](#TapToWH))  
  
<a name="APM"></a>   
## <a name="tasks-and-the-asynchronous-programming-model-apm"></a>작업 및 APM(비동기 프로그래밍 모델)  
  
<a name="ApmToTap"></a>   
### <a name="from-apm-to-tap"></a>APM에서 TAP로  
 [Asynchronous Programming Model (APM)](../../../docs/standard/asynchronous-programming-patterns/asynchronous-programming-model-apm.md) 패턴은 매우 구조적이므로 APM 구현을 TAP 구현으로 노출하는 래퍼를 쉽게 빌드할 수 있습니다. 사실상, [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]부터 .NET Framework에 이 변환을 제공하는 도우미 루틴이 <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A> 메서드 오버로드의 형태로 포함되었습니다.  
  
 동기 <xref:System.IO.Stream> 메서드에 해당하는 APM 항목을 나타내는 <xref:System.IO.Stream.BeginRead%2A> 클래스와 해당 <xref:System.IO.Stream.EndRead%2A> 및 <xref:System.IO.Stream.Read%2A> 메서드를 고려합니다.  
  
 [!code-csharp[Conceptual.AsyncInterop#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Stream1.cs#1)]
 [!code-vb[Conceptual.AsyncInterop#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/stream1.vb#1)]  
[!code-csharp[Conceptual.AsyncInterop#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Stream1.cs#2)]
[!code-vb[Conceptual.AsyncInterop#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/stream1.vb#2)]  
[!code-csharp[Conceptual.AsyncInterop#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Stream1.cs#3)]
[!code-vb[Conceptual.AsyncInterop#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/stream1.vb#3)]  
  
 <xref:System.Threading.Tasks.TaskFactory%601.FromAsync%2A?displayProperty=nameWithType> 메서드를 사용하여 다음과 같이 이 작업에 대한 TAP 래퍼를 구현할 수 있습니다.  
  
 [!code-csharp[Conceptual.AsyncInterop#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Wrap1.cs#4)]
 [!code-vb[Conceptual.AsyncInterop#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Wrap1.vb#4)]  
  
 구현은 다음과 유사합니다.  
  
 [!code-csharp[Conceptual.AsyncInterop#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Wrap2.cs#5)]
 [!code-vb[Conceptual.AsyncInterop#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Wrap2.vb#5)]  
  
<a name="TapToApm"></a>   
### <a name="from-tap-to-apm"></a>TAP에서 APM으로  
 기존 인프라에 APM 패턴이 필요한 경우 TAP 구현을 가져와 APM 구현이 필요한 곳에서 사용할 수도 있습니다.  작업이 구성되고 <xref:System.Threading.Tasks.Task> 클래스가 <xref:System.IAsyncResult>를 구현하기 때문에 간단한 도우미 함수를 사용하여 이 작업을 수행합니다. 다음 코드에서는 <xref:System.Threading.Tasks.Task%601> 클래스 확장을 사용하지만 제네릭이 아닌 작업에 대해 거의 동일한 함수를 사용할 수 있습니다.  
  
 [!code-csharp[Conceptual.AsyncInterop#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM1.cs#6)]
 [!code-vb[Conceptual.AsyncInterop#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM1.vb#6)]  
  
 이제 다음 TAP 구현이 있는 경우를 고려해 보세요.  
  
 [!code-csharp[Conceptual.AsyncInterop#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM2.cs#7)]
 [!code-vb[Conceptual.AsyncInterop#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM2.vb#7)]  
  
 다음 APM 구현을 제공하려고 합니다.  
  
 [!code-csharp[Conceptual.AsyncInterop#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM2.cs#8)]
 [!code-vb[Conceptual.AsyncInterop#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM2.vb#8)]  
[!code-csharp[Conceptual.AsyncInterop#9](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM2.cs#9)]
[!code-vb[Conceptual.AsyncInterop#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM2.vb#9)]  
  
 다음 예제에서는 APM으로 마이그레이션을 보여 줍니다.  
  
 [!code-csharp[Conceptual.AsyncInterop#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM2.cs#10)]
 [!code-vb[Conceptual.AsyncInterop#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM2.vb#10)]  
  
<a name="EAP"></a>   
## <a name="tasks-and-the-event-based-asynchronous-pattern-eap"></a>작업 및 EAP(이벤트 기반 비동기 패턴)  
 EAP 패턴에는 APM 패턴보다 더 많은 변형과 더 적은 구조가 있기 때문에 [Event-based Asynchronous Pattern (EAP)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md) 구현 래핑이 APM 패턴 래핑보다 훨씬 복잡합니다.  이를 보여 주기 위해 다음 코드에서는 `DownloadStringAsync` 메서드를 래핑합니다.  `DownloadStringAsync` 는 URI를 수락하고 진행 중인 여러 통계를 보고하기 위해 다운로드하는 동안 `DownloadProgressChanged` 이벤트를 발생시키며 완료되면 `DownloadStringCompleted` 이벤트를 발생시킵니다.  최종 결과는 지정된 URI에 있는 페이지의 내용이 포함된 문자열입니다.  
  
 [!code-csharp[Conceptual.AsyncInterop#11](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/EAP1.cs#11)]
 [!code-vb[Conceptual.AsyncInterop#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/EAP1.vb#11)]  
  
<a name="WaitHandles"></a>   
## <a name="tasks-and-wait-handles"></a>작업 및 대기 핸들  
  
<a name="WHToTap"></a>   
### <a name="from-wait-handles-to-tap"></a>대기 핸들에서 TAP로  
 대기 핸들은 비동기 패턴을 구현하지 않지만 대기 핸들이 설정된 경우 고급 개발자는 <xref:System.Threading.WaitHandle> 클래스 및 <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A?displayProperty=nameWithType> 메서드를 비동기 알림에 사용할 수 있습니다.  <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A> 메서드를 래핑하여 대기 핸들의 동기 대기에 대해 작업 기반 대체 항목을 사용하도록 설정할 수 있습니다.  
  
 [!code-csharp[Conceptual.AsyncInterop#12](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Wait1.cs#12)]
 [!code-vb[Conceptual.AsyncInterop#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Wait1.vb#12)]  
  
 이 메서드를 통해 비동기 메서드에서 기존 <xref:System.Threading.WaitHandle> 구현을 사용할 수 있습니다.  예를 들어 특정 시간에 실행되는 비동기 작업 수를 제한하려는 경우 세마포( <xref:System.Threading.SemaphoreSlim?displayProperty=nameWithType> 개체)를 활용할 수 있습니다.  세마포 개수를 *N* 으로 초기화하고, 작업을 수행하려는 시간 동안 세마포에서 대기한 다음 작업이 완료되면 세마포를 해제하여 동시에 실행되는 작업 수를 *N*개로 제한할 수 있습니다.  
  
 [!code-csharp[Conceptual.AsyncInterop#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Semaphore1.cs#13)]
 [!code-vb[Conceptual.AsyncInterop#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Semaphore1.vb#13)]  
  
 대기 핸들에 의존하지 않고 완전히 작업으로 작동하는 비동기 세마포를 빌드할 수도 있습니다. 이렇게 하려면 [Consuming the Task-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md) 에 설명된 <xref:System.Threading.Tasks.Task>이 추가되었습니다.  
  
<a name="TapToWH"></a>   
### <a name="from-tap-to-wait-handles"></a>TAP에서 대기 핸들로  
 앞에서 설명한 대로 <xref:System.Threading.Tasks.Task> 클래스는 <xref:System.IAsyncResult>를 구현하고, 해당 구현에서 <xref:System.Threading.Tasks.Task.System%23IAsyncResult%23AsyncWaitHandle%2A> 가 완료될 때 설정되는 대기 핸들을 반환하는 <xref:System.Threading.Tasks.Task> 속성을 노출합니다.  다음과 같이 <xref:System.Threading.WaitHandle> 에 대한 <xref:System.Threading.Tasks.Task> 을 가져올 수 있습니다.  
  
 [!code-csharp[Conceptual.AsyncInterop#14](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Wait1.cs#14)]
 [!code-vb[Conceptual.AsyncInterop#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Wait1.vb#14)]  
  
## <a name="see-also"></a>참고 항목

- [TAP(작업 기반 비동기 패턴)](../../../docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)  
- [작업 기반 비동기 패턴 구현](../../../docs/standard/asynchronous-programming-patterns/implementing-the-task-based-asynchronous-pattern.md)  
- [Consuming the Task-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md)
