---
title: TPL 및 일반적인 .NET Framework 비동기 프로그래밍
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, with other asynchronous models
ms.assetid: e7b31170-a156-433f-9f26-b1fc7cd1776f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 57f274d55ba5723ce8e0b51a7a39e98e95855e28
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64653922"
---
# <a name="tpl-and-traditional-net-framework-asynchronous-programming"></a>TPL 및 일반적인 .NET Framework 비동기 프로그래밍
.NET Framework에서는 I/O에 바인딩된 비동기 작업과 계산에 바인딩된 비동기 작업을 수행하도록 다음 표준 패턴 두 개를 제공합니다.  
  
- APM(비동기 프로그래밍 모델) - <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType> 및 <xref:System.IO.Stream.EndRead%2A?displayProperty=nameWithType>와 같은 Begin/End 메서드 쌍으로 비동기 작업을 표현합니다.  
  
- EAP(이벤트 기반 비동기 패턴) - <xref:System.Net.WebClient.DownloadStringAsync%2A?displayProperty=nameWithType> 및 <xref:System.Net.WebClient.DownloadStringCompleted?displayProperty=nameWithType>와 같이 *OperationName*Async 및 *OperationName*Completed라는 메서드/이벤트 쌍으로 비동기 작업을 표현합니다. EAP는 .NET Framework 버전 2.0에 도입되었습니다.  
  
 TPL(작업 병렬 라이브러리)을 비동기 패턴의 하나와 함께 다양한 방법으로 사용할 수 있습니다. APM 및 EAP 작업을 둘 다 라이브러리 소비자에 대한 작업으로 노출하거나, APM 패턴을 노출하지만 작업 개체를 사용하여 내부적으로 구현할 수 있습니다. 두 시나리오에서 모두 작업 개체를 사용하여 코드를 간소화하고 다음 유용한 기능을 활용할 수 있습니다.  
  
- 작업이 시작되고 나서 언제든지 작업 연속 형태로 콜백을 등록합니다.  
  
- <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A>와 <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAny%2A> 메서드를 사용하거나 <xref:System.Threading.Tasks.Task.WaitAll%2A> 메서드 또는 <xref:System.Threading.Tasks.Task.WaitAny%2A> 메서드를 사용하여 `Begin_` 메서드에 대한 응답으로 실행되는 여러 작업을 조정합니다.  
  
- I/O에 바인딩된 비동기 작업과 계산에 바인딩된 비동기 작업을 같은 작업 개체로 캡슐화합니다.  
  
- 작업 개체 상태를 모니터링합니다.  
  
- <xref:System.Threading.Tasks.TaskCompletionSource%601>을 사용하여 작업 상태를 작업 개체에 마샬링합니다.  
  
## <a name="wrapping-apm-operations-in-a-task"></a>작업으로 APM 작업 래핑  
 <xref:System.Threading.Tasks.TaskFactory?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.TaskFactory%601?displayProperty=nameWithType> 클래스는 둘 다 APM Begin/End 메서드 쌍을 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601> 인스턴스 하나로 캡슐화하도록 하는 <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.TaskFactory%601.FromAsync%2A?displayProperty=nameWithType> 메서드의 여러 가지 오버로드를 제공합니다. 다양한 오버로드가 입력 매개 변수 수가 0~3개인 Begin/End 메서드 쌍을 수용합니다.  
  
 값(Visual Basic의 `Function`)을 반환하는 `End` 메서드가 있는 쌍의 경우 <xref:System.Threading.Tasks.TaskFactory%601>에서 <xref:System.Threading.Tasks.Task%601>을 만드는 메서드를 사용합니다. void(Visual Basic의 `Sub`)를 반환하는 `End` 메서드의 경우 <xref:System.Threading.Tasks.TaskFactory>에서 <xref:System.Threading.Tasks.Task>를 만드는 메서드를 사용합니다.  
  
 `Begin` 메서드에 매개 변수가 4개 이상 포함되거나 `ref` 또는 `out` 매개 변수가 포함되는 경우에는 `End` 메서드만 캡슐화하는 추가 `FromAsync` 오버로드가 제공됩니다.  
  
 다음 예제에서는 <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType> 및 <xref:System.IO.FileStream.EndRead%2A?displayProperty=nameWithType> 메서드와 일치하는 `FromAsync` 오버로드에 대한 서명을 보여 줍니다. 이 오버로드는 다음과 같이 입력 매개 변수 세 개를 사용합니다.  
  
 [!code-csharp[FromAsync#01](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#01)]
 [!code-vb[FromAsync#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#01)]  
  
 첫 번째 매개 변수는 <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType> 메서드의 서명과 일치하는 <xref:System.Func%606> 대리자입니다. 두 번째 매개 변수는 <xref:System.IAsyncResult>를 사용하고 `TResult`를 반환하는 <xref:System.Func%602> 대리자입니다. <xref:System.IO.FileStream.EndRead%2A>는 정수를 반환하므로 컴파일러에서는 `TResult` 형식을 <xref:System.Int32>로 유추하고 작업 형식을 <xref:System.Threading.Tasks.Task>로 유추합니다. 마지막 매개 변수 4개는 <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType> 메서드의 매개 변수와 동일합니다.  
  
- 파일 데이터를 저장할 버퍼입니다.  
  
- 데이터 쓰기를 시작할 버퍼의 오프셋입니다.  
  
- 파일에서 읽을 최대 데이터 양입니다.  
  
- 콜백에 전달할 사용자 정의 상태 데이터를 저장하는 선택적 개체입니다.  
  
### <a name="using-continuewith-for-the-callback-functionality"></a>콜백 기능에 ContinueWith 사용  
 단순한 바이트 수와는 달리 파일의 데이터에 대한 액세스 권한이 필요할 경우에는 <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A> 메서드로는 충분하지 않습니다. 대신에 파일 데이터가 들어 있는 `Result` 속성이 포함된 <xref:System.Threading.Tasks.Task>를 사용하세요. 이 작업을 하려면 원래 작업에 연속을 추가합니다. 연속은 일반적으로 <xref:System.AsyncCallback> 대리자에서 수행하는 작업을 수행합니다. 연속은 선행이 완료되고 데이터 버퍼가 채워졌을 때 호출됩니다. 돌아가기 전에 <xref:System.IO.FileStream> 개체를 닫아야 합니다.  
  
 다음 예제에서는 <xref:System.IO.FileStream> 클래스의 BeginRead/EndRead 쌍을 캡슐화하는 <xref:System.Threading.Tasks.Task>를 반환하는 방법을 보여 줍니다.  
  
 [!code-csharp[FromAsync#03](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#03)]
 [!code-vb[FromAsync#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#03)]  
  
 그리고 나서 다음과 같이 메서드를 호출할 수 있습니다.  
  
 [!code-csharp[FromAsync#04](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#04)]
 [!code-vb[FromAsync#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#04)]  
  
### <a name="providing-custom-state-data"></a>사용자 지정 상태 데이터 제공  
 일반적인 <xref:System.IAsyncResult> 작업에서 <xref:System.AsyncCallback> 대리자에 사용자 지정 상태 데이터가 필요하면 `Begin` 메서드의 마지막 매개 변수를 통해 데이터를 전달해야 하므로, 데이터를 <xref:System.IAsyncResult> 개체로 데이터를 패키지하고 나서 최종적으로 콜백 메서드에 전달할 수 있습니다. 일반적으로 `FromAsync` 메서드를 사용할 때 이 기능이 필요합니다. 사용자 지정 데이터가 연속에 알려지면 연속 대리자에서 직접 캡슐화될 수 있습니다. 다음 예제는 이전 예제와 비슷하지만 선행의 `Result` 속성을 검사하지 않고 연속의 사용자 대리자에 직접 액세스할 수 있는 사용자 지정 상태 데이터를 연속에서 검사합니다.  
  
 [!code-csharp[FromAsync#05](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#05)]
 [!code-vb[FromAsync#05](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#05)]  
  
### <a name="synchronizing-multiple-fromasync-tasks"></a>여러 FromAsync 작업 동기화  
 정적 <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A> 및 <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAny%2A> 메서드는 `FromAsync` 메서드와 함께 사용될 때 더 큰 유연성을 제공합니다. 다음 예제에서는 여러 비동기 I/O 작업을 시작하고 연속을 실행하기 전에 모든 작업이 완료될 때까지 기다리는 방법을 보여 줍니다.  
  
 [!code-csharp[FromAsync#06](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#06)]
 [!code-vb[FromAsync#06](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#06)]  
  
### <a name="fromasync-tasks-for-only-the-end-method"></a>End 메서드 전용 FromAsync 작업  
 `Begin` 메서드에 입력 매개 변수가 4개 이상 필요하거나 `ref` 또는 `out` 매개 변수가 있는 경우 `End` 메서드만 표현하는 `FromAsync` 오버로드(예: <xref:System.Threading.Tasks.TaskFactory%601.FromAsync%28System.IAsyncResult%2CSystem.Func%7BSystem.IAsyncResult%2C%600%7D%29?displayProperty=nameWithType>)를 사용할 수 있습니다. <xref:System.IAsyncResult>를 전달하고 이를 작업으로 캡슐화하려는 시나리오에서 이들 메서드를 사용할 수도 있습니다.  
  
 [!code-csharp[FromAsync#07](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#07)]
 [!code-vb[FromAsync#07](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#07)]  
  
### <a name="starting-and-canceling-fromasync-tasks"></a>FromAsync 작업 시작 및 취소  
 `FromAsync` 메서드에서 반환된 작업의 상태는 WaitingForActivation 상태이고 이 작업은 작업이 만들어지고 나서 시스템에 의해 시작됩니다. 해당 작업에서 시작을 호출하려고 하면 예외가 발생합니다.  
  
 기본 .NET Framework API에서는 현재 파일 또는 네트워크 I/O의 진행 중 취소를 지원하지 않으므로 `FromAsync` 작업을 취소할 수 없습니다. `FromAsync` 호출을 캡슐화하는 메서드에 취소 기능을 추가할 수 있지만, `FromAsync`가 호출되기 전이나 완료된 후(예: 연속 작업에서)에만 취소에 응답할 수 있습니다.  
  
 <xref:System.Net.WebClient>와 같이 EAP를 지원하는 몇몇 클래스는 취소를 지원하며 취소 토큰을 사용하여 해당 네이티브 취소 기능을 통합할 수 있습니다.  
  
## <a name="exposing-complex-eap-operations-as-tasks"></a>복잡한 EAP 작업을 작업으로 노출  
 TPL은 메서드의 `FromAsync` 패밀리가 <xref:System.IAsyncResult> 패턴을 래핑하는 것과 같은 방법으로 이벤트 기반 비동기 작업을 캡슐화하도록 특수 디자인된 메서드를 제공하지 않습니다. 그러나 TPL은 임의 작업 집합을 <xref:System.Threading.Tasks.Task%601>로 표현하는 데 사용할 수 있는 <xref:System.Threading.Tasks.TaskCompletionSource%601?displayProperty=nameWithType> 클래스를 제공합니다. 작업은 동기 또는 비동기 작업일 수 있고 I/O에 바인딩되거나 계산에 바인딩된 작업이거나 두 작업에 모두 해당할 수 있습니다.  
  
 다음 예제에서는 a <xref:System.Threading.Tasks.TaskCompletionSource%601>을 사용하여 비동기 <xref:System.Net.WebClient> 작업 집합을 클라이언트 코드에 기본 <xref:System.Threading.Tasks.Task%601>로 노출하는 방법을 보여 줍니다. 메서드를 통해 웹 URL 배열과 검색할 용어 또는 이름을 입력할 수 있고, 그리고 나서 각 사이트에서 검색 용어가 발생하는 횟수가 반환됩니다.  
  
 [!code-csharp[FromAsync#10](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/snippet10.cs#10)]
 [!code-vb[FromAsync#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/snippet10.vb#10)]  
  
 추가적인 예외 처리가 포함되고 클라이언트 코드에서 메서드를 호출하는 방법을 보여주는 더 자세한 예제는 [방법: 작업에서 EAP 패턴 래핑](../../../docs/standard/parallel-programming/how-to-wrap-eap-patterns-in-a-task.md)을 참조하세요.  
  
 <xref:System.Threading.Tasks.TaskCompletionSource%601>에서 만들어진 작업은 TaskCompletionSource에 의해 시작되므로 사용자 코드는 해당 작업에서 Start 메서드를 호출하지 않아야 합니다.  
  
## <a name="implementing-the-apm-pattern-by-using-tasks"></a>작업을 사용하여 APM 패턴 구현  
 몇몇 시나리오에서는 API에서 Begin/End 메서드 쌍을 사용하여 <xref:System.IAsyncResult> 패턴을 직접 노출하는 것이 좋을 수 있습니다. 예를 들어 기존 API와 일관성을 유지하려고 하거나 이 패턴이 필요한 자동화된 도구가 있을 수 있습니다. 이 경우 작업을 사용하여 APM 패턴을 내부적으로 구현하는 방법을 간소화할 수 있습니다.  
  
 다음 예제에서는 작업을 사용하여 계산에 바인딩된 장기 실행 메서드에 대한 APM Begin/End 메서드 쌍을 구현하는 방법을 보여 줍니다.  
  
 [!code-csharp[FromAsync#09](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#09)]
 [!code-vb[FromAsync#09](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#09)]  
  
## <a name="using-the-streamextensions-sample-code"></a>StreamExtensions 샘플 코드 사용  
 [Samples for Parallel Programming with the .NET Framework 4](https://code.msdn.microsoft.com/ParExtSamples)(.NET Framework 4를 사용한 병렬 프로그래밍 샘플)에서 제공되는 Streamextensions.cs 파일에는 비동기 파일 및 네트워크 I/O에 Task 개체를 사용하는 몇 가지 참조 구현이 포함되어 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [TPL(작업 병렬 라이브러리)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)
