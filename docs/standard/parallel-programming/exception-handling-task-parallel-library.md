---
title: 예외 처리(작업 병렬 라이브러리)
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, exceptions
ms.assetid: beb51e50-9061-4d3d-908c-56a4f7c2e8c1
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a3e602057bfd2dea15887daee9058b12f26992f2
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65639039"
---
# <a name="exception-handling-task-parallel-library"></a>예외 처리(작업 병렬 라이브러리)

작업 내에서 실행되는 사용자 코드에 의해 throw된 처리되지 않은 예외는 이 항목의 뒷부분에서 설명하는 특정 시나리오를 제외하고는 호출 스레드로 다시 전파됩니다. 정적 또는 인스턴스 <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType> 메서드 중 하나를 사용할 때 예외가 전파되며 `try`/`catch` 문에 호출을 포함하여 예외를 처리할 수 있습니다. 어떤 작업이 연결된 자식 작업의 부모인 경우 또는 여러 작업에서 대기 중인 경우, 여러 개의 예외가 throw될 수 있습니다.

모든 예외를 호출 스레드로 다시 전파하기 위해 작업 인프라가 이러한 예외를 <xref:System.AggregateException> 인스턴스에서 래핑합니다. <xref:System.AggregateException> 예외에는 <xref:System.AggregateException.InnerExceptions%2A> 속성이 있으며 이 속성을 열거하면 throw된 모든 원래 예외를 확인하고 각 예외를 개별적으로 처리하거나 처리하지 않을 수 있습니다. 또한 <xref:System.AggregateException.Handle%2A?displayProperty=nameWithType> 메서드를 사용하여 원래 예외를 처리할 수도 있습니다.

하나의 예외만 throw된 경우 다음 예제와 같이 <xref:System.AggregateException> 예외에서 여전히 래핑됩니다.

[!code-csharp[TPL_Exceptions#21](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/handling21.cs#21)]
[!code-vb[TPL_Exceptions#21](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/handling21.vb#21)]

<xref:System.AggregateException> 을 catch하고 내부 예외를 관찰하지 않으면 처리되지 않은 예외를 방지할 수 있습니다. 하지만 이 방법은 기본 <xref:System.Exception> 유형을 비병렬 시나리오에서 catch하는 것과 유사하기 때문에 사용하지 않는 것이 좋습니다. 복구하기 위한 특정 작업을 수행하지 않고 예외를 catch하려면 프로그램을 결정할 수 없는 상태 그대로 두면 됩니다.

<xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType> 메서드를 호출하여 작업의 완료를 기다리는 것을 원하지 않는 경우 다음 예제가 보여주는 것처럼 작업의 <xref:System.Threading.Tasks.Task.Exception%2A> 속성에서 <xref:System.AggregateException> 예외를 검색할 수도 있습니다. 자세한 내용은 이 문서의 [Task.Exception 속성을 사용하여 예외 관찰](#observing-exceptions-by-using-the-taskexception-property) 섹션을 참조하세요.

[!code-csharp[TPL_Exceptions#29](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/handling22.cs#29)]
[!code-vb[TPL_Exceptions#29](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/handling22.vb#29)]

예외를 전파하는 작업을 기다리지 않거나 해당 <xref:System.Threading.Tasks.Task.Exception%2A> 속성에 액세스하는 경우 작업이 가비지 수집될 때 .NET 예외 정책에 따라 예외가 에스컬레이션됩니다.

예외가 가입된 스레드로 다시 버블 업될 수 있는 경우 예외가 발생한 후에도 작업에서 일부 항목을 계속 처리할 수 있습니다.

> [!NOTE]
> “내 코드만”이 사용하도록 설정된 경우 Visual Studio가 예외를 발생시키는 줄에서 중단하고 "예외가 사용자 코드에서 처리되지 않았다"는 오류 메시지를 표시합니다. 이 오류는 심각하지는 않습니다. F5 키를 눌러 계속하고 이러한 예제에 설명된 예외 처리 동작을 확인할 수 있습니다. 맨 처음 오류 지점에서 Visual Studio가 실행을 중단하지 않도록 하려면 **도구, 옵션, 디버깅, 일반** 을 차례로 선택하고 **내 코드만 사용**확인란의 선택을 취소하기만 하면 됩니다.

## <a name="attached-child-tasks-and-nested-aggregateexceptions"></a>연결된 자식 작업 및 중첩된 AggregateExceptions

작업에 예외를 throw하는 연결된 자식 작업이 있는 경우 해당 예외가 <xref:System.AggregateException> 에서 래핑된 다음 상위 작업으로 전파되고, 이 상위 작업은 해당 예외를 자체 <xref:System.AggregateException> 에서 래핑한 다음 호출 스레드로 다시 전파합니다. 이러한 경우 <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType>, <xref:System.Threading.Tasks.Task.WaitAny%2A> 또는 <xref:System.Threading.Tasks.Task.WaitAll%2A> 메서드에서 catch된 <xref:System.AggregateException> 예외의 <xref:System.AggregateException.InnerExceptions%2A> 속성에는 오류를 발생시킨 원래 예외가 아니라 하나 이상의 <xref:System.AggregateException> 인스턴스가 포함됩니다. 중첩된 <xref:System.AggregateException> 예외를 반복할 필요가 없도록 하려면 <xref:System.AggregateException.InnerExceptions%2A?displayProperty=nameWithType> 속성에 원래 예외가 포함되도록 <xref:System.AggregateException.Flatten%2A> 메서드를 사용하여 중첩된 모든 <xref:System.AggregateException> 예외를 제거합니다. 다음 예제에서는 중첩된 <xref:System.AggregateException> 인스턴스가 하나의 루프에서 결합되고 처리됩니다.

[!code-csharp[TPL_Exceptions#22](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/flatten2.cs#22)]
[!code-vb[TPL_Exceptions#22](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/flatten2.vb#22)]

또한 다음 예제가 보여주는 것처럼 <xref:System.AggregateException.Flatten%2A?displayProperty=nameWithType> 메서드를 사용하여 단일 <xref:System.AggregateException> 인스턴스에서 여러 작업에 의해 throw된 여러 <xref:System.AggregateException> 인스턴스의 내부 예외를 다시 throw할 수 있습니다.

[!code-csharp[TPL_Exceptions#13](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/taskexceptions2.cs#13)]
[!code-vb[TPL_Exceptions#13](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/taskexceptions2.vb#13)]

## <a name="exceptions-from-detached-child-tasks"></a>분리된 자식 작업의 예외

기본적으로 자식 작업은 분리된 작업으로 만들어집니다. 분리된 작업에서 throw된 예외는 직계 부모 작업에서 처리되거나 다시 throw되어야 하지만, 연결된 자식 작업이 다시 전파되는 것과 동일한 방식으로 호출 스레드에 다시 전파되지는 않습니다. 최상위 부모는 분리된 자식의 예외를 수동으로 다시 throw하여 <xref:System.AggregateException> 에서 래핑하고 호출 스레드로 다시 전파할 수 있습니다.

[!code-csharp[TPL_Exceptions#23](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/detached21.cs#23)]
[!code-vb[TPL_Exceptions#23](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/detached21.vb#23)]

연속을 사용하여 자식 작업에서 예외를 계속 관찰하는 경우에도 해당 예외는 여전히 부모 작업에서 관찰해야 합니다.

## <a name="exceptions-that-indicate-cooperative-cancellation"></a>협조적 취소를 나타내는 예외

작업의 사용자 코드가 취소 요청에 응답하는 경우, 올바른 절차는 요청을 통신한 취소 토큰을 전달하는 <xref:System.OperationCanceledException> 을 throw하는 것입니다. 예외를 전파하려고 시도하기 전에 작업 인스턴스가 요청이 만들어졌을 때 요청에 전달된 토큰과 예외의 토큰을 비교합니다. 두 토큰이 동일한 경우 작업은 <xref:System.Threading.Tasks.TaskCanceledException> 에서 래핑된 <xref:System.AggregateException>을 전파하며 이는 내부 예외를 검사할 때 확인할 수 있습니다. 그러나 호출 스레드가 작업을 기다리지 않는 경우 이 특정 예외는 전파되지 않습니다. 자세한 내용은 [작업 취소](../../../docs/standard/parallel-programming/task-cancellation.md)를 참조하세요.

[!code-csharp[TPL_Exceptions#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/exceptions.cs#4)]
[!code-vb[TPL_Exceptions#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/tpl_exceptions.vb#4)]

## <a name="using-the-handle-method-to-filter-inner-exceptions"></a>핸들 메서드를 사용하여 내부 예외 필터링

<xref:System.AggregateException.Handle%2A?displayProperty=nameWithType> 메서드를 사용하여 추가 논리를 사용하지 않고 “처리됨”으로 처리할 수 있는 예외를 필터링할 수 있습니다. <xref:System.AggregateException.Handle%28System.Func%7BSystem.Exception%2CSystem.Boolean%7D%29?displayProperty=nameWithType> 메서드에 제공되는 사용자 대리자에서 예외 형식, 해당 예외의 <xref:System.Exception.Message%2A> 속성 또는 예외가 무해한지 여부를 결정할 수 있는 정보를 검사할 수 있습니다. 이 대리자가 `false`를 반환하는 모든 예외는 <xref:System.AggregateException.Handle%2A?displayProperty=nameWithType> 메서드에서 반환한 직후 새 <xref:System.AggregateException> 인스턴스에서 다시 throw됩니다.

다음 예제에서는 <xref:System.AggregateException.InnerExceptions%2A?displayProperty=nameWithType> 컬렉션에서 각 예외를 검사하는 이 항목의 첫 번째 예제와 기능적으로 같습니다.  대신 이 예외 처리기는 각 예외에 대해 <xref:System.AggregateException.Handle%2A?displayProperty=nameWithType> 메서드 개체를 호출하고 `CustomException` 인스턴스가 아닌 예외만 다시 throw합니다.

[!code-csharp[TPL_Exceptions#26](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/handlemethod21.cs#26)]
[!code-vb[TPL_Exceptions#26](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/handlemethod21.vb#26)]

다음은 보다 자세한 예제로, 파일을 열거할 때 <xref:System.AggregateException.Handle%2A?displayProperty=nameWithType> 예외에 특수 처리를 제공하기 위해 <xref:System.UnauthorizedAccessException> 메서드를 사용합니다.

[!code-csharp[TPL_Exceptions#12](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/taskexceptions.cs#12)]
[!code-vb[TPL_Exceptions#12](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/taskexceptions.vb#12)]

## <a name="observing-exceptions-by-using-the-taskexception-property"></a>Task.Exception 속성을 사용하여 예외 관찰

작업이 <xref:System.Threading.Tasks.TaskStatus.Faulted?displayProperty=nameWithType> 상태에서 완료된 경우 <xref:System.Threading.Tasks.Task.Exception%2A> 속성을 검사하여 오류를 발생시킨 특정 예외를 검색할 수 있습니다. <xref:System.Threading.Tasks.Task.Exception%2A> 속성을 관찰하는 좋은 방법은 다음 예제에 나와 있는 것처럼 선행 작업에서 오류가 발생할 경우에만 실행되는 연속을 사용하는 것입니다.

[!code-csharp[TPL_Exceptions#27](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/exceptionprop21.cs#27)]
[!code-vb[TPL_Exceptions#27](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/exceptionprop21.vb#27)]

실제 애플리케이션에서 연속 대리자는 예외에 대한 자세한 정보를 기록하고 새 작업을 생성하여 예외에서 복구할 수도 있습니다.

## <a name="unobservedtaskexception-event"></a>UnobservedTaskException 이벤트

일부 시나리오에서는 예를 들어 신뢰할 수 없는 플러그인을 호스트할 때 무해한 예외가 자주 발생할 수 있으며 그 모든 예외를 수동으로 관찰하는 것은 어려울 수 있습니다. 이러한 경우 <xref:System.Threading.Tasks.TaskScheduler.UnobservedTaskException?displayProperty=nameWithType> 이벤트를 처리할 수 있습니다. 처리기로 전달되는 <xref:System.Threading.Tasks.UnobservedTaskExceptionEventArgs?displayProperty=nameWithType> 인스턴스를 사용하면 관찰되지 않은 예외가 가입된 스레드로 다시 전파되는 것을 방지할 수 있습니다.

## <a name="see-also"></a>참고 항목

- [TPL(작업 병렬 라이브러리)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)
