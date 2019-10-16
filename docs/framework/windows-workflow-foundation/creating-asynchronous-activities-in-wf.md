---
title: WF에서 비동기 활동 만들기
ms.date: 03/30/2017
ms.assetid: 497e81ed-5eef-460c-ba55-fae73c05824f
ms.openlocfilehash: b990631d6efdb4644274c8a4606af07495b1979c
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65592968"
---
# <a name="creating-asynchronous-activities-in-wf"></a>WF에서 비동기 활동 만들기
<xref:System.Activities.AsyncCodeActivity>는 활동 작성자가 파생 활동에서 비동기 실행 논리를 구현하는 데 사용할 수 있는 기본 클래스를 제공합니다. 이 기능은 워크플로 스케줄러 스레드를 유지하지 않고 병렬로 실행 가능한 활동을 차단하지 않으면서 비동기 작업을 수행해야 하는 사용자 지정 활동에 유용합니다. 이 항목에서는 <xref:System.Activities.AsyncCodeActivity>를 사용하여 사용자 지정 비동기 활동을 만드는 방법을 간략하게 설명합니다.  
  
## <a name="using-asynccodeactivity"></a>AsyncCodeActivity 사용  
 <xref:System.Activities?displayProperty=nameWithType>는 사용자 지정 활동 작성자에게 활동 작성 요구 사항별로 다른 기본 클래스를 제공합니다. 각 클래스는 특정 체계를 따르고 워크플로 작성자 및 활동 런타임에 해당 계약을 제공합니다. <xref:System.Activities.AsyncCodeActivity> 기반 활동은 스케줄러 스레드를 기준으로 비동기 작업을 수행하고 실행 논리가 관리 코드에 표시되는 활동입니다. 비동기 처리로 인해 <xref:System.Activities.AsyncCodeActivity>에서 실행 중에 유휴 지점이 발생할 수 있습니다. 비동기 작업의 일시적 특성으로 인해 <xref:System.Activities.AsyncCodeActivity>는 활동 실행 기간 동안 항상 비지속성 블록을 만듭니다. 따라서 비동기 작업 중에 워크플로 런타임에 워크플로 인스턴스가 유지되지 않을 뿐만 아니라 비동기 코드를 실행하는 동안 워크플로 인스턴스가 언로드되지 않습니다.  
  
### <a name="asynccodeactivity-methods"></a>AsyncCodeActivity 메서드  
 <xref:System.Activities.AsyncCodeActivity>에서 파생되는 활동은 사용자 지정 코드로 <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> 및 <xref:System.Activities.AsyncCodeActivity.EndExecute%2A> 메서드를 재정의하여 비동기 실행 논리를 만들 수 있습니다. 런타임에 의해 호출되면 이러한 메서드가 <xref:System.Activities.AsyncCodeActivityContext>에 전달됩니다. <xref:System.Activities.AsyncCodeActivityContext> 활동 작성자 통해 공유 상태를 제공할 수 있습니다 <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> /  <xref:System.Activities.AsyncCodeActivity.EndExecute%2A> 컨텍스트에서 <xref:System.Activities.AsyncCodeActivityContext.UserState%2A> 속성입니다. 다음 예제에서 `GenerateRandom` 활동은 난수를 비동기적으로 생성합니다.  
  
 [!code-csharp[CFX_ActivityExample#8](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#8)]  
  
 이전 예제 활동은 <xref:System.Activities.AsyncCodeActivity%601>에서 파생되며 `OutArgument<int>`라는 높은 `Result`를 갖습니다. `GetRandom` 메서드에 의해 반환되는 값은 <xref:System.Activities.AsyncCodeActivity%601.EndExecute%2A> 재정의를 통해 추출되어 반환되며, 이 값이 `Result` 값으로 설정됩니다. 결과를 반환하지 않는 비동기 활동은 <xref:System.Activities.AsyncCodeActivity>에서 파생되어야 합니다. 다음 예제에서는 `DisplayRandom`에서 파생되는 <xref:System.Activities.AsyncCodeActivity> 활동을 정의합니다. 이 활동은 `GetRandom` 활동과 비슷하지만 결과를 반환하는 대신 콘솔에 메시지를 표시합니다.  
  
 [!code-csharp[CFX_ActivityExample#11](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#11)]  
  
 반환 값이 없으므로 `DisplayRandom`은 <xref:System.Action> 대신 <xref:System.Func%602>을 사용하여 대리자를 호출하고 대리자는 아무 값도 반환하지 않습니다.  
  
 또한 <xref:System.Activities.AsyncCodeActivity>는 <xref:System.Activities.AsyncCodeActivity.Cancel%2A> 재정의를 제공합니다. <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> 및 <xref:System.Activities.AsyncCodeActivity.EndExecute%2A>는 재정의가 필요하지만, <xref:System.Activities.AsyncCodeActivity.Cancel%2A>은 선택 사항이며, 활동에서 처리 중인 비동기 상태를 취소하거나 중단할 때 비동기 상태를 정리할 수 있도록 재정의할 수 있습니다. 정리할 수 있고 `AsyncCodeActivity.ExecutingActivityInstance.IsCancellationRequested`가 `true`이면 활동에서 <xref:System.Activities.AsyncCodeActivityContext.MarkCanceled%2A>를 호출해야 합니다. 이 메서드에서 throw되는 예외는 워크플로 인스턴스에 치명적입니다.  
  
 [!code-csharp[CFX_ActivityExample#10](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#10)]  
  
### <a name="invoking-asynchronous-methods-on-a-class"></a>클래스에 대한 비동기 메서드 호출  
 다양 한.NET Framework의 클래스는 비동기 기능을 제공이 기능을 사용 하 여 비동기적으로 호출할 수 있습니다는 <xref:System.Activities.AsyncCodeActivity> 활동을 기반으로 합니다. 다음 예제에서는 활동 만들어집니다 비동기적으로 파일을 사용 하 여 만드는 <xref:System.IO.FileStream> 클래스입니다.  
  
 [!code-csharp[CFX_ActivityExample#12](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#12)]  
  
### <a name="sharing-state-between-the-beginexecute-and-endexecute-methods"></a>BeginExecute 및 EndExecute 메서드 간에 상태 공유  
 앞의 예제에서 <xref:System.IO.FileStream>에서 만든 <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> 개체는 <xref:System.Activities.AsyncCodeActivity.EndExecute%2A>에서 액세스합니다. 이는 `file` 변수가 <xref:System.Activities.AsyncCodeActivityContext.UserState%2A?displayProperty=nameWithType>에서 <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> 속성에 전달되기 때문입니다. 이는 <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A>와 <xref:System.Activities.AsyncCodeActivity.EndExecute%2A> 간의 상태 공유에 올바른 메서드입니다. 파생 클래스(`FileWriter` in this case)에서 멤버 변수를 사용하여 <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A>와 <xref:System.Activities.AsyncCodeActivity.EndExecute%2A>간에 상태를 공유하는 것은 활동 개체가 여러 활동 인스턴스에서 참조될 수 있으므로 잘못된 것입니다. 멤버 변수를 사용하여 상태를 공유하려고 시도한 경우 어떤 <xref:System.Activities.ActivityInstance>의 값이 다른 <xref:System.Activities.ActivityInstance>의 값을 덮어쓰거나 사용하게 될 수 있습니다.  
  
### <a name="accessing-argument-values"></a>인수 값 액세스  
 <xref:System.Activities.AsyncCodeActivity> 환경은 활동에 정의된 인수들로 구성됩니다. 이 인수에서 액세스할 수 있습니다 합니다 <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> / <xref:System.Activities.AsyncCodeActivity.EndExecute%2A> 사용 하 여 재정의 <xref:System.Activities.AsyncCodeActivityContext> 매개 변수입니다. 대리자에서는 인수에 액세스할 수 없지만 해당 매개 변수를 사용하여 인수 값 또는 원하는 다른 데이터를 대리자에 전달할 수 있습니다. 다음 예제에서는 `Max` 인수에서 상한(포함)을 가져오는 난수 생성 활동을 정의합니다. 대리자를 호출하면 인수 값이 비동기 코드에 전달됩니다.  
  
 [!code-csharp[CFX_ActivityExample#9](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#9)]  
  
### <a name="scheduling-actions-or-child-activities-using-asynccodeactivity"></a>AsyncCodeActivity를 사용하여 작업 또는 자식 활동 예약  
 <xref:System.Activities.AsyncCodeActivity> 파생 사용자 지정 활동은 워크플로 스레드와 관련하여 작업을 비동기식으로 수행하는 메서드를 제공하지만 자식 활동이나 작업을 예약하는 기능은 제공하지 않습니다. 단 비동기식 동작은 구성을 통해 자식 활동의 예약으로 통합할 수 있습니다. 비동기 작업을 만든 다음 <xref:System.Activities.Activity> 또는 <xref:System.Activities.NativeActivity> 파생 작업을 통해 구성하여 비동기식 동작을 제공하고 자식 활동 또는 작업을 예약할 수 있습니다. 예를 들어 <xref:System.Activities.Activity>에서 파생되고, 활동의 논리를 구현하는 다른 활동뿐만 아니라 비동기 활동을 포함하는 <xref:System.Activities.Statements.Sequence> 구현으로 포함되도록 활동을 만들 수 있습니다. 에 대 한 자세한 예제를 사용 하 여 활동 작성 <xref:System.Activities.Activity> 하 고 <xref:System.Activities.NativeActivity>를 참조 [방법: 활동을 만드는](how-to-create-an-activity.md) 하 고 [활동 제작 옵션](activity-authoring-options-in-wf.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Action>
- <xref:System.Func%602>
