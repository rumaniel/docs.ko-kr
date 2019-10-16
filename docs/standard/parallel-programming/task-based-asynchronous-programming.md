---
title: 작업 기반 비동기 프로그래밍 - .NET
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallelism, task
ms.assetid: 458b5e69-5210-45e5-bc44-3888f86abd6f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ab754da005dcc16fc71c3a59728e4ff6848fbbb1
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666312"
---
# <a name="task-based-asynchronous-programming"></a>작업 기반 비동기 프로그래밍

TPL(작업 병렬 라이브러리)은 *작업*이란 개념을 기반으로 하며 비동기 작업을 나타냅니다. 몇 가지 점에서 작업은 스레드 또는 <xref:System.Threading.ThreadPool> 작업 항목과 비슷하지만 추상화 수준은 더 높습니다. *작업 병렬 처리*는 동시에 실행되는 하나 이상의 독립적인 작업을 의미합니다. 작업을 사용할 때의 주된 이점 두 가지는 다음과 같습니다.

- 시스템 리소스를 더 효율적이고 확장 가능한 방식으로 사용할 수 있습니다.

     내부적으로 작업은 <xref:System.Threading.ThreadPool>의 큐에 대기됩니다. 이 ThreadPool은 스레드 수를 파악하여 이에 맞게 조정하고, 처리량을 최대화하는 부하 분산을 제공하는 알고리즘을 사용하여 기능이 향상되었습니다. 이로써 작업이 비교적 단순해지며, 여러 개의 작업을 만들어 세부적인 병렬 처리를 사용할 수 있습니다.

- 프로그래밍 방식 제어 수준이 스레드 또는 작업 항목을 사용할 때보다 높아집니다.

     작업과 작업을 기반으로 만들어진 프레임워크는 대기, 취소, 연속, 강력한 예외 처리, 세부 상태, 사용자 지정 예약 등을 지원하는 강력한 API 집합을 제공합니다.

이 두 가지 이유 때문에 .NET Framework에서는 다중 스레드, 비동기 및 병렬 코드를 작성하는 API로 TPL이 선호됩니다.

## <a name="creating-and-running-tasks-implicitly"></a>암시적으로 작업 만들기 및 실행

<xref:System.Threading.Tasks.Parallel.Invoke%2A?displayProperty=nameWithType> 메서드를 사용하면 개수에 관계없이 여러 개의 임의 문을 간편하게 동시에 실행할 수 있습니다. 작업의 각 항목에 대한 <xref:System.Action> 대리자를 전달하기만 하면 됩니다. 이러한 대리자를 만드는 가장 쉬운 방법은 람다 식을 사용하는 것입니다. 람다 식은 명명된 메서드를 호출하거나 코드를 인라인으로 제공합니다. 다음 예제에서는 동시에 실행되는 두 개의 작업을 만들고 시작하는 기본적인 <xref:System.Threading.Tasks.Parallel.Invoke%2A> 호출을 보여 줍니다.call that creates and starts two tasks that run concurrently. 이름이 `DoSomeWork`인 메서드를 호출하는 람다 식에서 첫 번째 작업을 표시하며 이름이 `DoSomeOtherWork`인 메서드를 호출하는 람다 식에서 두 번째 작업을 표시합니다.

> [!NOTE]
> 이 문서에서는 람다 식을 사용하여 TPL에 대리자를 정의합니다. C# 또는 Visual Basic의 람다 식을 잘 모르는 경우 [PLINQ 및 TPL의 람다 식](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)을 참조하세요.

[!code-csharp[TPL#21](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl/cs/tpl.cs#21)]
[!code-vb[TPL#21](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl/vb/tpl_vb.vb#21)]

> [!NOTE]
> <xref:System.Threading.Tasks.Task>에 의해 자동으로 만들어지는 <xref:System.Threading.Tasks.Parallel.Invoke%2A> 인스턴스의 수는 제공되는 대리자의 수와 같지 않을 수도 있습니다. TPL에서는 대리자 수가 많은 경우 등에 다양한 최적화 기능을 사용할 수 있기 때문입니다.

자세한 내용은 [방법: Parallel.Invoke를 사용하여 병렬 작업 실행](../../../docs/standard/parallel-programming/how-to-use-parallel-invoke-to-execute-parallel-operations.md)을 참조하세요.

작업 실행을 더 구체적으로 제어하거나 작업을 통해 값을 반환하려면 <xref:System.Threading.Tasks.Task> 개체를 더 명시적으로 사용해야 합니다.

## <a name="creating-and-running-tasks-explicitly"></a>명시적으로 작업 만들기 및 실행

<xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 클래스로 표현되는 값을 반환하지 않는 작업입니다. 값을 반환하는 작업은 <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType>에서 상속하는 <xref:System.Threading.Tasks.Task> 클래스로 표현됩니다. 작업 개체는 인프라 세부 사항을 처리하고, 작업의 수명 내내 호출 스레드에서 액세스할 수 있는 메서드 및 속성을 제공합니다. 예를 들어 언제든지 작업의 <xref:System.Threading.Tasks.Task.Status%2A> 속성에 액세스하여 작업이 실행되기 시작했는지, 이미 실행되어 완료되었는지, 취소되었는지, 또는 예외를 throw했는지를 확인할 수 있습니다. 이러한 상태는 <xref:System.Threading.Tasks.TaskStatus> 열거형으로 표현됩니다.

작업을 만들 때는 해당 작업에서 실행할 코드를 캡슐화하는 사용자 대리자를 지정합니다. 대리자는 명명된 대리자, 익명 메서드 또는 람다 식으로 표현할 수 있습니다. 람다 식에는 다음 예제에서처럼 명명된 메서드에 대한 호출을 포함할 수 있습니다. 예제에는 콘솔 모드 애플리케이션이 종료되기 전에 작업 실행이 완료되도록 <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType> 메서드에 대한 호출이 포함됩니다.

[!code-csharp[TPL_TaskIntro#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_taskintro/cs/lambda1.cs#1)]
[!code-vb[TPL_TaskIntro#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_taskintro/vb/lambda1.vb#1)]

<xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType> 메서드를 사용하여 한 번에 작업을 만들고 시작할 수도 있습니다. 작업을 관리하기 위해 <xref:System.Threading.Tasks.Task.Run%2A> 메서드는 기본 작업 스케줄러를 사용합니다. 이 경우 작업 스케줄러가 현재 스레드와 연결되었는지 여부는 관계없습니다. <xref:System.Threading.Tasks.Task.Run%2A> 메서드는 작업을 만들고 작업 일정을 예약할 때 더 자세히 제어할 필요가 없는 경우 작업을 만들고 시작하는 데 가장 많이 사용되는 방법입니다.

[!code-csharp[TPL_TaskIntro#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_taskintro/cs/run1.cs#2)]
[!code-vb[TPL_TaskIntro#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_taskintro/vb/run1.vb#2)]

<xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=nameWithType> 메서드를 사용하여 한 번에 작업을 만들고 시작할 수도 있습니다. 생성 및 일정 예약을 구분할 필요가 없고 추가 작업 생성 옵션이나 특정 스케줄러를 사용할 필요가 있는 경우 또는 다음 예제와 같이 <xref:System.Threading.Tasks.Task.AsyncState%2A?displayProperty=nameWithType> 속성을 통해 검색할 수 있는 작업에 추가 상태를 전달해야 하는 경우 이 메서드를 사용합니다.

[!code-csharp[TPL_TaskIntro#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_taskintro/cs/asyncstate.cs#23)]
[!code-vb[TPL_TaskIntro#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_taskintro/vb/asyncstate.vb#23)]

<xref:System.Threading.Tasks.Task> 및 <xref:System.Threading.Tasks.Task%601>는 각각 <xref:System.Threading.Tasks.Task.Factory%2A>의 기본 인스턴스를 반환하는 정적 <xref:System.Threading.Tasks.TaskFactory> 속성을 노출하므로 메서드를 `Task.Factory.StartNew()`로 호출할 수 있습니다. 또한 다음 예제에서 작업은 <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> 형식이므로 계산 결과가 들어 있는 공용 <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=nameWithType> 속성이 각 작업에 포함됩니다. 작업은 비동기적으로 실행되며 완료 순서에는 제한이 없습니다. 계산이 완료되기 전에 <xref:System.Threading.Tasks.Task%601.Result%2A> 속성에 액세스할 경우 이 속성이 값을 사용할 수 있을 때까지 호출 스레드를 차단합니다.

[!code-csharp[TPL_TaskIntro#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_taskintro/cs/result1.cs#4)]
[!code-vb[TPL_TaskIntro#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_taskintro/vb/result1.vb#4)]

자세한 내용은 [방법: 작업에서 값 반환](../../../docs/standard/parallel-programming/how-to-return-a-value-from-a-task.md)을 참조하세요.

람다 식을 사용하여 대리자를 만드는 경우 소스 코드의 해당 지점에서 표시되는 모든 변수에 액세스할 수 있습니다. 그러나 특히 루프 내에서 람다가 기대한 대로 변수를 캡처하지 않는 경우가 있습니다. 이 경우 람다는 각 반복 후에 변경할 때 값이 아닌 최종 값만 capture합니다. 다음 예제에서 이 문제를 보여 줍니다. `CustomData` 개체를 인스턴스화하고 루프 카운터를 개체 식별자로 사용하는 람다 식에 루프 카운터를 전달합니다. 이 예제의 출력에서 표시되는 것처럼 각 `CustomData` 개체에는 동일한 식별자가 있습니다.

[!code-csharp[TPL_TaskIntro#22](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_taskintro/cs/iteration1b.cs#22)]
[!code-vb[TPL_TaskIntro#22](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_taskintro/vb/iteration1b.vb#22)]

생성자를 통해 작업에 상태 개체를 제공하여 각 반복의 값에 액세스할 수 있습니다. 다음 예제에서는 `CustomData` 개체를 만들 때 루프 카운터를 사용하여 이전 예제를 수정하여 람다 식에 전달되도록 합니다.  예제 출력에서 보듯이 각 `CustomData` 개체는 이제 개체를 인스턴스화한 시간에 루프 카운터의 값을 기반으로 한 고유 식별자가 있습니다.

[!code-csharp[TPL_TaskIntro#21](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_taskintro/cs/iteration1a.cs#21)]
[!code-vb[TPL_TaskIntro#21](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_taskintro/vb/iteration1a.vb#21)]

이 상태는 작업 대리자에 인수로 전달되며 작업 개체에서 <xref:System.Threading.Tasks.Task.AsyncState%2A?displayProperty=nameWithType> 속성을 사용하여 액세스할 수 있습니다.  다음 예제는 이전 예제를 약간 변형한 예제입니다. <xref:System.Threading.Tasks.Task.AsyncState%2A> 속성을 사용하여 람다 식에 전달된 `CustomData` 개체에 대한 정보를 표시합니다.

[!code-csharp[TPL_TaskIntro#23](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_taskintro/cs/asyncstate.cs#23)]
[!code-vb[TPL_TaskIntro#23](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_taskintro/vb/asyncstate.vb#23)]

## <a name="task-id"></a>작업 ID

모든 작업은 애플리케이션 도메인에서 작업을 고유하게 식별하는 정수 ID를 받으며, 이 ID는 <xref:System.Threading.Tasks.Task.Id%2A?displayProperty=nameWithType> 속성을 사용하여 액세스할 수 있습니다. ID는 Visual Studio 디버거의 **병렬 스택** 및 **작업** 창에서 작업 정보를 보는 데 유용합니다. ID는 나중에 만들어집니다. 즉, 요청될 때까지는 ID가 만들어지지 않으므로 프로그램이 실행될 때마다 작업 ID가 달라질 수 있습니다. 디버거에서 작업 ID를 보는 방법에 대한 자세한 내용은 [작업 창 사용](/visualstudio/debugger/using-the-tasks-window) 및 [병렬 스택 창 사용](/visualstudio/debugger/using-the-parallel-stacks-window)을 참조하세요.

## <a name="task-creation-options"></a>작업 생성 옵션

작업을 만드는 대부분의 API는 <xref:System.Threading.Tasks.TaskCreationOptions> 매개 변수를 사용하는 오버로드를 제공합니다. 이러한 옵션 중 하나를 지정하여 스레드 풀에서 작업을 예약하는 방법을 작업 스케줄러에 지시할 수 있습니다. 다음 표에서는 다양한 작업 생성 옵션을 보여 줍니다.

|<xref:System.Threading.Tasks.TaskCreationOptions> 매개 변수 값|설명|
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
|<xref:System.Threading.Tasks.TaskCreationOptions.None>|옵션을 지정하지 않을 경우의 기본값입니다. 스케줄러에서는 스케줄러의 기본 휴리스틱을 사용하여 작업을 예약합니다.|
|<xref:System.Threading.Tasks.TaskCreationOptions.PreferFairness>|먼저 만들어진 작업은 먼저 실행될 가능성이 높고 나중에 만들어진 작업은 나중에 실행될 가능성이 높게 작업이 예약되도록 지정합니다.|
|<xref:System.Threading.Tasks.TaskCreationOptions.LongRunning>|작업이 장기 실행 작업을 나타냄을 지정합니다.|
|<xref:System.Threading.Tasks.TaskCreationOptions.AttachedToParent>|작업을 현재 작업(있는 경우)의 연결된 자식 작업으로 만들어야 함을 지정합니다. 자세한 내용은 [연결된 자식 작업과 분리된 자식 작업](../../../docs/standard/parallel-programming/attached-and-detached-child-tasks.md)을 참조하세요.|
|<xref:System.Threading.Tasks.TaskCreationOptions.DenyChildAttach>|내부 작업이 `AttachedToParent` 옵션을 지정할 경우 해당 작업이 연결된 자식 작업이 되지 않도록 지정합니다.|
|<xref:System.Threading.Tasks.TaskCreationOptions.HideScheduler>|특정 작업 내에서 <xref:System.Threading.Tasks.TaskFactory.StartNew%2A?displayProperty=nameWithType> 또는 <xref:System.Threading.Tasks.Task%601.ContinueWith%2A?displayProperty=nameWithType> 같은 메서드를 호출하여 만든 작업을 위한 작업 스케줄러가 이 작업이 실행 중인 스케줄러 대신 기본 스케줄러임을 지정합니다.|

이러한 옵션과 비트 **OR** 연산을 함께 사용할 수 있습니다. 다음 예제에서는 <xref:System.Threading.Tasks.TaskCreationOptions.LongRunning> 및 <xref:System.Threading.Tasks.TaskContinuationOptions.PreferFairness> 옵션이 있는 작업을 보여 줍니다.

[!code-csharp[TPL_TaskIntro#03](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_taskintro/cs/taskintro.cs#03)]
[!code-vb[TPL_TaskIntro#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_taskintro/vb/tpl_intro.vb#03)]

## <a name="tasks-threads-and-culture"></a>작업, 스레드 및 문화권

각 스레드에는 각각 <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Thread.CurrentUICulture%2A?displayProperty=nameWithType> 속성으로 정의된 관련 문화권 및 UI 문화권이 있습니다. 스레드의 문화권은 형식 지정, 구문 분석, 정렬 및 문자열 비교와 같은 작업에서 사용됩니다. 스레드의 UI 문화권은 리소스 조회에서 사용됩니다. 일반적으로, <xref:System.Globalization.CultureInfo.DefaultThreadCurrentCulture%2A?displayProperty=nameWithType> 및 <xref:System.Globalization.CultureInfo.DefaultThreadCurrentUICulture%2A?displayProperty=nameWithType> 속성을 사용하여 애플리케이션 도메인의 모든 스레드에 대한 기본 문화권을 지정하지 않는 한 스레드의 기본 문화권 및 UI 문화권은 시스템 문화권에 의해 정의됩니다. 스레드의 문화권을 명시적으로 설정하고 새 스레드를 시작하는 경우 새 스레드는 호출 스레드의 문화권을 상속하지 않습니다. 대신, 해당 문화권은 기본 시스템 문화권입니다. .NET Framework 4.6 이전의 .NET Framework 버전을 대상으로 하는 앱에 대한 작업 기반 프로그래밍 모델은 이 관행을 준수합니다.

> [!IMPORTANT]
> 작업 컨텍스트의 일부인 호출 스레드의 문화권은 .NET Framework 4.6 *아래에서 실행*되는 앱이 아니라 .NET Framework 4.6을 *대상으로 하는* 앱에 적용됩니다. Visual Studio에서 **새 프로젝트** 대화 상자 위쪽의 드롭다운 목록에서 버전을 선택하여 프로젝트를 만들 때 특정 버전의 .NET Framework를 대상으로 지정할 수 있으며, Visual Studio 외부에서는 <xref:System.Runtime.Versioning.TargetFrameworkAttribute> 특성을 사용할 수 있습니다. .NET Framework 4.6 이전의 .NET Framework 버전을 대상으로 하거나 특정 버전의 .NET Framework를 대상으로 하는 앱의 경우 작업의 문화권은 작업이 실행되는 스레드의 문화권에 의해 계속 결정됩니다.

.NET Framework 4.6을 대상으로 하는 앱부터 작업이 스레드 풀 스레드에서 비동기적으로 실행되는 경우에도 호출 스레드의 문화권이 각 작업에 상속됩니다.

다음 예제에서는 간단한 설명을 제공합니다. <xref:System.Runtime.Versioning.TargetFrameworkAttribute> 특성을 사용하여 .NET Framework 4.6을를 대상으로 지정하고 앱의 현재 문화권을 프랑스어(프랑스) 또는 프랑스어(프랑스)가 이미 현재 문화권인 경우 영어(미국)로 변경합니다. 그런 다음 새 문화권의 통화 값으로 형식이 지정된 일부 숫자를 반환하는 `formatDelegate`라는 대리자를 호출합니다. 호출 스레드의 문화권이 비동기 작업에 상속되므로 작업으로서 대리자가 동기적 또는 비동기적인지에 관계없이 예상 결과를 반환합니다.

[!code-csharp[System.Globalization.CultureInfo.Class.Async#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.globalization.cultureinfo.class.async/cs/asyncculture1.cs#5)]
[!code-vb[System.Globalization.CultureInfo.Class.Async#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.globalization.cultureinfo.class.async/vb/asyncculture1.vb#5)]

Visual Studio를 사용할 경우 <xref:System.Runtime.Versioning.TargetFrameworkAttribute> 특성을 생략하고 **새 프로젝트** 대화 상자에서 프로젝트를 만들 때 대신 .NET Framework 4.6을 대상으로 선택할 수 있습니다.

.NET Framework 4.6 이전의 .NET Framework 버전을 대상으로 하는 앱의 동작을 반영하는 출력의 경우 소스 코드에서 <xref:System.Runtime.Versioning.TargetFrameworkAttribute> 특성을 제거합니다. 출력은 호출 스레드의 문화권이 아닌 기본 시스템 문화권의 형식 지정 규칙을 반영합니다.

비동기 작업 및 문화권에 대한 자세한 내용은 <xref:System.Globalization.CultureInfo> 항목의 "문화권 및 비동기 작업 기반 작업" 섹션을 참조하세요.

## <a name="creating-task-continuations"></a>작업 연속 만들기

<xref:System.Threading.Tasks.Task.ContinueWith%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.Task%601.ContinueWith%2A?displayProperty=nameWithType> 메서드를 사용하면 ‘선행 작업’이 완료될 때 시작할 작업을 지정할 수 있습니다.  연속 작업의 대리자가 선행 작업으로 참조를 전달하여 <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=nameWithType> 속성의 값을 검색하여 선행 작업의 상태를 검사할 수 있으며 선행 작업의 출력을 연속 작업의 입력으로 사용할 수 있습니다.

다음 예제에서는 `getData` 작업이 <xref:System.Threading.Tasks.TaskFactory.StartNew%60%601%28System.Func%7B%60%600%7D%29?displayProperty=nameWithType> 메서드에 대한 호출로 시작됩니다. `processData`작업은 `getData`가 완료되면 자동으로 시작되고 `displayData`는 `processData`가 완료되면 시작됩니다. `getData`는 `processData` 작업의 `getData` 속성을 통해 <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=nameWithType> 작업에 액세스할 수 있는 정수 배열을 생성합니다. `processData` 작업은 해당 배열을 처리하고 <xref:System.Threading.Tasks.Task%601.ContinueWith%60%601%28System.Func%7BSystem.Threading.Tasks.Task%7B%600%7D%2C%60%600%7D%29?displayProperty=nameWithType> 메서드로 전달된 람다 식의 반환 형식에서 유추한 형식을 갖는 결과를 반환합니다. `displayData` 작업은 `processData`가 완료되면 자동으로 실행되며 <xref:System.Tuple%603> 람다 식에서 반환한 `processData` 개체는 `displayData` 작업의 `processData` 속성을 통해 <xref:System.Threading.Tasks.Task%601.Result%2A?displayProperty=nameWithType> 작업에 액세스할 수 있습니다. `displayData` 작업은 `processData` 작업의 결과를 사용해서 해당 형식이 비슷한 방식으로 유추되고 <xref:System.Threading.Tasks.Task%601.Result%2A> 속성의 프로그램에서 사용할 수 있는 결과를 생성합니다.

[!code-csharp[TPL_TaskIntro#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_taskintro/cs/continuations1.cs#5)]
[!code-vb[TPL_TaskIntro#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_taskintro/vb/continuations1.vb#5)]

<xref:System.Threading.Tasks.Task.ContinueWith%2A?displayProperty=nameWithType>는 인스턴스 메서드이므로 각 선행 작업에 대해 <xref:System.Threading.Tasks.Task%601> 개체를 인스턴스화하는 대신 메서드를 연속 호출할 수 있습니다. 다음 예제는 <xref:System.Threading.Tasks.Task.ContinueWith%2A?displayProperty=nameWithType> 메서드에 대한 호출도 함께 연결된다는 점을 제외하고 이전 예제와 기능적으로 동일합니다. 일련의 메서드 호출에서 반환되는 <xref:System.Threading.Tasks.Task%601> 개체는 최종 연속 작업입니다.

[!code-csharp[TPL_TaskIntro#24](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_taskintro/cs/continuations2.cs#24)]
[!code-vb[TPL_TaskIntro#24](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_taskintro/vb/continuations2.vb#24)]

<xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A> 및 <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAny%2A> 메서드를 사용하면 여러 작업을 연속적으로 수행할 수 있습니다.

자세한 내용은 [연속 작업을 사용하여 작업 연결](../../../docs/standard/parallel-programming/chaining-tasks-by-using-continuation-tasks.md)을 참조하세요.

## <a name="creating-detached-child-tasks"></a>분리된 자식 작업 만들기

작업에서 실행되는 사용자 코드를 통해 새 작업이 만들어지지만 <xref:System.Threading.Tasks.TaskCreationOptions.AttachedToParent> 옵션은 지정되지 않을 경우 새 작업은 어떤 특수한 방법으로도 부모 작업과 동기화되지 않습니다. 이 유형의 동기화되지 않은 작업을 *분리된 중첩 작업* 또는 *분리된 자식 작업*이라고 부릅니다. 다음 예제에서는 분리된 상태의 자식 작업을 하나 만드는 작업을 보여 줍니다.

[!code-csharp[TPL_TaskIntro#07](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_taskintro/cs/taskintro.cs#07)]
[!code-vb[TPL_TaskIntro#07](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_taskintro/vb/tpl_intro.vb#07)]

부모 작업은 분리된 자식 작업이 완료될 때까지 대기하지 않습니다.

## <a name="creating-child-tasks"></a>자식 작업 만들기

작업에서 실행되는 사용자 코드를 통해 <xref:System.Threading.Tasks.TaskCreationOptions.AttachedToParent> 옵션을 사용해서 작업을 만들 경우, 새 작업은 부모 작업의 ‘연결된 자식 작업’으로 알려집니다.  <xref:System.Threading.Tasks.TaskCreationOptions.AttachedToParent> 옵션을 사용하면 부모 작업은 암시적으로 모든 연결된 자식 작업이 완료될 때까지 대기하게 되므로 이 옵션을 사용하여 구조적 작업 병렬 처리를 표현할 수 있습니다. 다음 예제에서는 10개의 연결된 자식 작업을 만드는 부모 작업을 보여 줍니다. 예제는 부모 작업이 완료되기를 기다리도록 <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType> 메서드를 호출하지만 첨부된 자식 작업이 완료되기를 명시적으로 기다릴 필요가 없습니다.

[!code-csharp[TPL_TaskIntro#8](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_taskintro/cs/child1.cs#8)]
[!code-vb[TPL_TaskIntro#8](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_taskintro/vb/child1.vb#8)]

부모 작업은 <xref:System.Threading.Tasks.TaskCreationOptions.DenyChildAttach?displayProperty=nameWithType> 옵션을 사용하여 부모 작업에 다른 작업이 첨부되지 않도록 할 수 있습니다. 자세한 내용은 [연결된 자식 작업과 분리된 자식 작업](../../../docs/standard/parallel-programming/attached-and-detached-child-tasks.md)을 참조하세요.

## <a name="waiting-for-tasks-to-finish"></a>작업 완료 시까지 대기

<xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> 형식은 작업이 완료될 때까지 대기할 수 있게 해주는 <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType> 메서드의 몇 가지 오버로드를 제공합니다. 또한 정적 <xref:System.Threading.Tasks.Task.WaitAll%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Tasks.Task.WaitAny%2A?displayProperty=nameWithType> 메서드의 오버로드를 사용하면 작업 배열의 일부 또는 모두가 완료될 때까지 대기할 수 있습니다.

일반적으로 다음과 같은 경우에 작업을 대기시킵니다.

- 주 스레드에서 작업에 의해 계산된 최종 결과를 사용해야 하는 경우

- 작업에서 throw될 수 있는 예외를 처리해야 하는 경우

- 애플리케이션은 모든 작업이 실행을 완료하기 전에 종료할 수 있습니다. 예를 들어, 콘솔 애플리케이션은 `Main`(애플리케이션 진입점)의 모든 동기 코드가 실행되는 즉시 종료됩니다.

다음 예제에서는 예외 처리가 포함되지 않은 기본적인 패턴을 보여 줍니다.

[!code-csharp[TPL_TaskIntro#06](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_taskintro/cs/taskintro.cs#06)]
[!code-vb[TPL_TaskIntro#06](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_taskintro/vb/tpl_intro.vb#06)]

예외 처리를 보여 주는 예제는 [예외 처리](../../../docs/standard/parallel-programming/exception-handling-task-parallel-library.md)를 참조하세요.

일부 오버로드에서는 제한 시간을 지정할 수 있으며, 다른 오버로드에서는 프로그래밍 방식으로 또는 사용자 입력에 대한 응답으로 대기 자체를 취소할 수 있도록 추가 <xref:System.Threading.CancellationToken>을 입력 매개 변수로 사용합니다.

작업을 대기할 때는 암시적으로 <xref:System.Threading.Tasks.TaskCreationOptions.AttachedToParent?displayProperty=nameWithType> 옵션의 사용으로 생성된 해당 작업의 모든 자식 작업을 대기합니다. <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType>는 작업이 이미 완료되었는지 여부를 즉시 반환합니다. 작업에서 발생한 예외는 모두 <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType> 메서드에 의해 throw됩니다. 이는 <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType> 메서드가 작업 완료 후 호출된 경우에도 해당됩니다.

## <a name="composing-tasks"></a>작업 작성

<xref:System.Threading.Tasks.Task> 및 <xref:System.Threading.Tasks.Task%601> 클래스는 공통 패턴을 구현하고 C#, Visual Basic 및 F#에서 제공하는 비동기 언어 기능을 더욱 효율적으로 사용하도록 여러 작업을 구성할 수 있는 여러 메서드를 제공합니다. 이 단원에서는 <xref:System.Threading.Tasks.Task.WhenAll%2A>, <xref:System.Threading.Tasks.Task.WhenAny%2A>, <xref:System.Threading.Tasks.Task.Delay%2A> 및 <xref:System.Threading.Tasks.Task.FromResult%2A> 메서드에 대해 설명합니다.

### <a name="taskwhenall"></a>Task.WhenAll

<xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 메서드는 여러 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601> 개체가 완료될 때까지 비동기적으로 대기합니다. 균일하지 않은 작업 집합에 대해 대기할 수 있는 오버로드된 버전을 제공합니다. 예를 들어, 여러 <xref:System.Threading.Tasks.Task> 및 <xref:System.Threading.Tasks.Task%601> 개체가 한 메서드 호출에서 완료되기를 기다릴 수 있습니다.

### <a name="taskwhenany"></a>Task.WhenAny

<xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType> 메서드는 여러 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601> 개체 중 하나가 완료될 때까지 비동기적으로 대기합니다. <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 메서드에서와 마찬가지로 이 메서드는 균일하지 않은 작업 집합에 대해 대기할 수 있는 오버로드된 버전을 제공합니다. <xref:System.Threading.Tasks.Task.WhenAny%2A> 메서드는 다음과 같은 시나리오에서 특히 유용합니다.

- 중복 작업입니다. 알고리즘 또는 여러 방법으로 수행할 수 있는 작업을 고려합니다. <xref:System.Threading.Tasks.Task.WhenAny%2A> 메서드를 사용하여 먼저 완료되는 작업을 선택한 다음 나머지 작업을 취소할 수 있습니다.

- 인터리브 작업입니다. 모두 완료되어야 하는 여러 작업을 시작하고 <xref:System.Threading.Tasks.Task.WhenAny%2A> 메서드를 사용하여 각 작업이 완료되면 결과를 처리할 수 있습니다. 하나의 작업이 완료되면 하나 이상의 추가 작업을 시작할 수 있습니다.

- 제한된 작업입니다. <xref:System.Threading.Tasks.Task.WhenAny%2A> 메서드를 사용하여 동시 작업 수를 제한하여 이전 시나리오를 확장할 수 있습니다.

- 만료된 작업입니다. <xref:System.Threading.Tasks.Task.WhenAny%2A> 메서드를 사용하여 <xref:System.Threading.Tasks.Task.Delay%2A> 메서드에서 반환되는 작업처럼 특정 시간 이후에 완료되는 하나 이상의 작업 중에서 선택할 수 있습니다. <xref:System.Threading.Tasks.Task.Delay%2A> 메서드는 다음 단원에서 설명됩니다.

### <a name="taskdelay"></a>Task.Delay

<xref:System.Threading.Tasks.Task.Delay%2A?displayProperty=nameWithType> 메서드는 지정된 시간 이후에 완료되는 <xref:System.Threading.Tasks.Task> 개체를 생성합니다. 이 메서드를 사용하여 때때로 데이터를 폴링하는 루프를 빌드하고, 제한 시간을 소개하고, 미리 지정된 시간 동안에 사용자의 입력 처리를 지연하는 데 사용할 수 있습니다.

### <a name="tasktfromresult"></a>Task(T).FromResult

<xref:System.Threading.Tasks.Task.FromResult%2A?displayProperty=nameWithType> 메서드를 사용하면 미리 계산된 결과를 갖는 <xref:System.Threading.Tasks.Task%601> 개체를 만들 수 있습니다. 이 메서드는 <xref:System.Threading.Tasks.Task%601> 개체가 반환되는 비동기 작업을 수행하고 해당 <xref:System.Threading.Tasks.Task%601> 개체의 결과가 계산되어 있을 때 유용합니다. <xref:System.Threading.Tasks.Task.FromResult%2A>를 사용하여 캐시에 저장된 비동기 다운로드 작업 결과를 검색하는 예제는 [방법: 미리 계산된 작업 만들기](../../../docs/standard/parallel-programming/how-to-create-pre-computed-tasks.md)를 참조하세요.

## <a name="handling-exceptions-in-tasks"></a>작업의 예외 처리

작업이 하나 이상의 예외를 throw하면 해당 예외가 <xref:System.AggregateException> 예외에 래핑됩니다. 이 예외는 작업과 조인하는 스레드에 다시 전파됩니다. 이 스레드는 일반적으로 작업이 완료될 때까지 기다리는 스레드이거나 <xref:System.Threading.Tasks.Task%601.Result%2A> 속성에 액세스하는 스레드입니다. 이 동작을 통해 처리되지 않은 예외가 발생할 때마다 기본적으로 프로세스를 종료하도록 하는 .NET Framework 정책을 적용할 수 있습니다. 호출 코드는 다음 `try`/`catch` 블록을 사용하여 예외를 처리할 수 있습니다.

- <xref:System.Threading.Tasks.Task.Wait%2A> 메서드

- <xref:System.Threading.Tasks.Task.WaitAll%2A> 메서드

- <xref:System.Threading.Tasks.Task.WaitAny%2A> 메서드

- <xref:System.Threading.Tasks.Task%601.Result%2A> 속성

또한 조인하는 스레드에서는 작업이 가비지 수집되기 전에 <xref:System.Threading.Tasks.Task.Exception%2A> 속성에 액세스하여 예외를 처리할 수 있습니다. 이 속성에 액세스하면 처리되지 않은 예외로 인해 개체가 종료될 때 프로세스를 종료하는 예외 전파 동작이 트리거되는 것을 방지할 수 있습니다.

예외 및 작업에 대한 자세한 내용은 [예외 처리](../../../docs/standard/parallel-programming/exception-handling-task-parallel-library.md)를 참조하세요.

## <a name="canceling-tasks"></a>작업 취소

<xref:System.Threading.Tasks.Task> 클래스는 협조적 취소를 지원하며 .NET Framework 4에 소개된 <xref:System.Threading.CancellationTokenSource?displayProperty=nameWithType> 및 <xref:System.Threading.CancellationToken?displayProperty=nameWithType> 클래스와 완전히 통합됩니다. <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 클래스의 많은 생성자는 <xref:System.Threading.CancellationToken> 개체를 입력 매개 변수로 사용합니다. 대부분의 <xref:System.Threading.Tasks.TaskFactory.StartNew%2A> 및 <xref:System.Threading.Tasks.Task.Run%2A> 오버로드는 <xref:System.Threading.CancellationToken> 매개 변수를 포함합니다.

이 토큰을 만든 다음 나중에 <xref:System.Threading.CancellationTokenSource> 클래스를 사용하여 취소 요청을 실행할 수 있습니다. 이 토큰을 <xref:System.Threading.Tasks.Task>에 인수로 전달하고, 취소 요청에 대한 응답 작업을 수행하는 사용자 대리자에서도 동일한 토큰을 참조합니다.

자세한 내용은 [작업 취소](../../../docs/standard/parallel-programming/task-cancellation.md) 및 [방법: 작업 및 해당 자식 취소](../../../docs/standard/parallel-programming/how-to-cancel-a-task-and-its-children.md)를 참조하세요.

## <a name="the-taskfactory-class"></a>TaskFactory 클래스

<xref:System.Threading.Tasks.TaskFactory> 클래스에서는 작업 및 연속 작업을 만들고 시작하기 위한 몇 가지 일반적인 패턴을 캡슐화하는 정적 메서드를 제공합니다.

- 가장 일반적인 패턴은 하나의 문으로 작업을 만들고 시작하는 <xref:System.Threading.Tasks.TaskFactory.StartNew%2A>입니다.

- 여러 선행 작업에서 연속 작업을 만들 때는 <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAll%2A> 메서드나 <xref:System.Threading.Tasks.TaskFactory.ContinueWhenAny%2A> 메서드 또는 <xref:System.Threading.Tasks.Task%601> 클래스에서 이에 해당하는 메서드를 사용합니다. 자세한 내용은 [연속 작업을 사용하여 작업 연결](../../../docs/standard/parallel-programming/chaining-tasks-by-using-continuation-tasks.md)을 참조하세요.

- 비동기 프로그래밍 모델인 `BeginX` 및 `EndX` 메서드를 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601> 인스턴스에 캡슐화하려면 <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A> 메서드를 사용합니다. 자세한 내용은 [TPL 및 일반적인 .NET 비동기 프로그래밍](../../../docs/standard/parallel-programming/tpl-and-traditional-async-programming.md)을 참조하세요.

기본 <xref:System.Threading.Tasks.TaskFactory>는 <xref:System.Threading.Tasks.Task> 클래스 또는 <xref:System.Threading.Tasks.Task%601> 클래스에서 정적 속성으로 액세스될 수 있습니다. <xref:System.Threading.Tasks.TaskFactory>를 직접 인스턴스화하고 <xref:System.Threading.CancellationToken>, <xref:System.Threading.Tasks.TaskCreationOptions> 옵션, <xref:System.Threading.Tasks.TaskContinuationOptions> 옵션 또는 <xref:System.Threading.Tasks.TaskScheduler>를 포함한 다양한 옵션을 지정할 수도 있습니다. 작업 팩터리를 만들 때 어떤 옵션을 지정하든 작업 팩터리에서 만드는 모든 작업에 해당 옵션이 적용됩니다. 단, <xref:System.Threading.Tasks.Task> 열거형을 사용하여 <xref:System.Threading.Tasks.TaskCreationOptions>을 만드는 경우는 제외되며, 이때는 해당 작업의 옵션이 작업 팩터리의 옵션을 재정의합니다.

## <a name="tasks-without-delegates"></a>대리자가 없는 작업

일부 경우에는 <xref:System.Threading.Tasks.Task>를 사용하여 사용자 대리자 대신 외부 구성 요소에서 수행되는 비동기 작업을 캡슐화할 수 있습니다. 이 작업이 비동기 프로그래밍 모델인 Begin/End 패턴을 기반으로 하는 경우에는 <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A> 메서드를 사용할 수 있습니다. 그러지 않은 경우에는 <xref:System.Threading.Tasks.TaskCompletionSource%601> 개체를 사용하여 작업에서 수행할 비동기 작업을 래핑하고 이를 통해 예외 전파 및 연속에 대한 지원과 같은 <xref:System.Threading.Tasks.Task> 프로그래밍 기능의 몇 가지 이점을 얻을 수 있습니다. 자세한 내용은 <xref:System.Threading.Tasks.TaskCompletionSource%601>을 참조하세요.

## <a name="custom-schedulers"></a>사용자 지정 스케줄러

대부분의 애플리케이션 또는 라이브러리 개발자는 작업이 실행되는 프로세서, 작업과 다른 작업이 동기화되는 방식 또는 <xref:System.Threading.ThreadPool?displayProperty=nameWithType>에서 작업이 예약되는 방식에는 크게 신경 쓰지 않고, 단지 작업이 호스트 컴퓨터에서 가능한 한 효율적으로 실행되기만을 바랍니다. 예약 세부 사항을 보다 세부적으로 제어해야 하는 경우 작업 병렬 라이브러리를 사용하면 기본 작업 스케줄러의 일부 설정을 구성할 수 있으며 사용자 지정 스케줄러를 지정할 수도 있습니다. 자세한 내용은 <xref:System.Threading.Tasks.TaskScheduler>을 참조하세요.

## <a name="related-data-structures"></a>관련 데이터 구조

TPL에는 병렬 시나리오와 순차 시나리오 모두에 유용한 새로운 공용 형식이 몇 가지 포함되어 있습니다. 여기에는 스레드로부터 안전하며 속도 및 확장성이 우수한 <xref:System.Collections.Concurrent?displayProperty=nameWithType> 네임스페이스의 몇 가지 컬렉션 클래스뿐 아니라 특정 종류의 작업 부하에 대해 이전보다 높은 효율성을 제공하는 <xref:System.Threading.Semaphore?displayProperty=nameWithType> 및 <xref:System.Threading.ManualResetEventSlim?displayProperty=nameWithType> 등의 새로운 몇 가지 동기화 형식도 포함됩니다. .NET Framework 4에 새로 추가된 <xref:System.Threading.Barrier?displayProperty=nameWithType> 및 <xref:System.Threading.SpinLock?displayProperty=nameWithType> 등의 다른 형식은 이전 릴리스에서는 사용할 수 없었던 기능을 제공합니다. 자세한 내용은 [병렬 프로그래밍의 데이터 구조](../../../docs/standard/parallel-programming/data-structures-for-parallel-programming.md)를 참조하세요.

## <a name="custom-task-types"></a>사용자 지정 작업 형식

<xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 또는 <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType>에서 상속하지 않는 것이 좋습니다. 대신 <xref:System.Threading.Tasks.Task.AsyncState%2A> 속성을 사용하여 추가 데이터 또는 상태를 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601> 개체에 연결하는 것이 좋습니다. 확장 메서드를 사용하여 <xref:System.Threading.Tasks.Task> 및 <xref:System.Threading.Tasks.Task%601> 클래스의 기능을 확장할 수도 있습니다. 확장 메서드에 대한 자세한 내용은 [확장 메서드](../../csharp/programming-guide/classes-and-structs/extension-methods.md) 및 [확장 메서드](../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)를 참조하세요.

<xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601>에서 상속해야 하는 경우에는 <xref:System.Threading.Tasks.Task.Run%2A>, <xref:System.Threading.Tasks.Task.Run%2A> 또는 <xref:System.Threading.Tasks.TaskFactory?displayProperty=nameWithType>, <xref:System.Threading.Tasks.TaskFactory%601?displayProperty=nameWithType> 또는 <xref:System.Threading.Tasks.TaskCompletionSource%601?displayProperty=nameWithType> 클래스를 사용하여 사용자 지정 작업 형식의 인스턴스를 만들 수 없습니다. 이러한 메커니즘은 <xref:System.Threading.Tasks.Task> 및 <xref:System.Threading.Tasks.Task%601> 개체만 만들기 때문입니다. 또한 <xref:System.Threading.Tasks.Task>, <xref:System.Threading.Tasks.Task%601>, <xref:System.Threading.Tasks.TaskFactory> 및 <xref:System.Threading.Tasks.TaskFactory%601>에서 제공하는 작업 연속 메커니즘을 사용하여 사용자 지정 작업의 인스턴스를 만들 수 없습니다. 이 메커니즘에서도 mechanisms also create only <xref:System.Threading.Tasks.Task> 및 <xref:System.Threading.Tasks.Task%601> 개체만 만들기 때문입니다.

## <a name="related-topics"></a>관련 항목

|제목|설명|
|-|-|
|[연속 작업을 사용하여 작업 연결](../../../docs/standard/parallel-programming/chaining-tasks-by-using-continuation-tasks.md)|연속 작업이 실행되는 방식을 설명합니다.|
|[연결된 자식 작업 및 분리된 자식 작업](../../../docs/standard/parallel-programming/attached-and-detached-child-tasks.md)|연결된 자식 작업과 분리된 자식 작업의 차이점을 설명합니다.|
|[작업 취소](../../../docs/standard/parallel-programming/task-cancellation.md)|<xref:System.Threading.Tasks.Task> 개체에 기본 제공되는 취소 지원에 대해 설명합니다.|
|[예외 처리](../../../docs/standard/parallel-programming/exception-handling-task-parallel-library.md)|동시 스레드에 대한 예외를 처리하는 방법을 설명합니다.|
|[방법: Parallel.Invoke를 사용하여 병렬 작업 실행](../../../docs/standard/parallel-programming/how-to-use-parallel-invoke-to-execute-parallel-operations.md)|<xref:System.Threading.Tasks.Parallel.Invoke%2A>를 사용하는 방법을 설명합니다.|
|[방법: 작업에서 값 반환](../../../docs/standard/parallel-programming/how-to-return-a-value-from-a-task.md)|작업을 통해 값을 반환하는 방법을 설명합니다.|
|[방법: 작업 및 해당 자식 취소](../../../docs/standard/parallel-programming/how-to-cancel-a-task-and-its-children.md)|작업을 취소하는 방법을 설명합니다.|
|[방법: 미리 계산된 작업 만들기](../../../docs/standard/parallel-programming/how-to-create-pre-computed-tasks.md)|<xref:System.Threading.Tasks.Task.FromResult%2A?displayProperty=nameWithType> 메서드를 사용하여 캐시에 저장된 비동기 다운로드 작업 결과를 검색하는 방법을 설명합니다.|
|[방법: 병렬 작업을 사용하여 이진 트리 트래버스](../../../docs/standard/parallel-programming/how-to-traverse-a-binary-tree-with-parallel-tasks.md)|작업을 사용하여 이진 트리를 따라 이동하는 방법을 설명합니다.|
|[방법: 중첩된 작업 래핑 취소](../../../docs/standard/parallel-programming/how-to-unwrap-a-nested-task.md)|<xref:System.Threading.Tasks.TaskExtensions.Unwrap%2A> 확장 메서드를 사용하는 방법을 보여 줍니다.|
|[데이터 병렬 처리](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)|<xref:System.Threading.Tasks.Parallel.For%2A> 및 <xref:System.Threading.Tasks.Parallel.ForEach%2A>를 사용하여 데이터에 대한 병렬 루프를 만드는 방법을 설명합니다.|
|[병렬 프로그래밍](../../../docs/standard/parallel-programming/index.md)|.NET Framework 병렬 프로그래밍의 최상위 노드입니다.|

## <a name="see-also"></a>참고 항목

- [병렬 프로그래밍](../../../docs/standard/parallel-programming/index.md)
- [NET Framework를 사용한 병렬 프로그래밍 샘플](https://code.msdn.microsoft.com/Samples-for-Parallel-b4b76364)
