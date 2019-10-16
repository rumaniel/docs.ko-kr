---
title: WorkflowInvoker 및 WorkflowApplication 사용
ms.date: 03/30/2017
ms.assetid: cd0e583c-a3f9-4fa2-b247-c7b3368c48a7
ms.openlocfilehash: ffb8277d9b1b7369ada7add36cd833a64acbaa7d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962207"
---
# <a name="using-workflowinvoker-and-workflowapplication"></a>WorkflowInvoker 및 WorkflowApplication 사용
WF (Windows Workflow Foundation)에서는 워크플로를 호스트 하는 여러 가지 방법을 제공 합니다. <xref:System.Activities.WorkflowInvoker> 는 메서드 호출과 같은 방식으로 워크플로를 호출하기 위한 간단한 방법을 제공하며, 지속성을 사용하지 않는 워크플로에만 사용될 수 있습니다. <xref:System.Activities.WorkflowApplication>은 수명 주기 이벤트 알림, 실행 제어, 책갈피 다시 시작 및 지속성을 비롯한 다양한 워크플로 실행 모델을 제공합니다. <xref:System.ServiceModel.Activities.WorkflowServiceHost>는 메시징 활동에 대한 지원을 제공하며 주로 워크플로 서비스에 사용됩니다. 이 항목에서는 <xref:System.Activities.WorkflowInvoker> 및 <xref:System.Activities.WorkflowApplication>을 사용하는 워크플로 호스팅을 소개합니다. 에서 워크플로 <xref:System.ServiceModel.Activities.WorkflowServiceHost>를 호스트 하는 방법에 대 한 자세한 내용은 워크플로 [서비스](../wcf/feature-details/workflow-services.md) 및 [호스팅 워크플로 서비스 개요](../wcf/feature-details/hosting-workflow-services-overview.md)를 참조 하세요.  
  
## <a name="using-workflowinvoker"></a>WorkflowInvoker 사용  
 <xref:System.Activities.WorkflowInvoker>는 워크플로를 메서드 호출처럼 실행하는 방법을 제공합니다. <xref:System.Activities.WorkflowInvoker>를 사용하여 워크플로를 호출하려면 <xref:System.Activities.WorkflowInvoker.Invoke%2A> 메서드를 호출하고 호출할 워크플로의 워크플로 정의를 전달합니다. 이 예제에서는 <xref:System.Activities.Statements.WriteLine>를 사용하여 <xref:System.Activities.WorkflowInvoker> 활동을 호출합니다.  
  
 [!code-csharp[CFX_WorkflowInvokerExample#1](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#1)]  
  
 <xref:System.Activities.WorkflowInvoker>를 사용하여 워크플로를 호출하면 호출 스레드에서 워크플로가 실행되고 유휴 시간을 포함하여 워크플로가 완료될 때까지 <xref:System.Activities.WorkflowInvoker.Invoke%2A> 메서드가 차단됩니다. 워크플로가 완료되어야 하는 시간 제한 간격을 구성하려면 <xref:System.Activities.WorkflowInvoker.Invoke%2A> 매개 변수를 취하는 <xref:System.TimeSpan> 오버로드 중 하나를 사용합니다. 이 예제에서는 서로 다른 두 가지 시간 제한 간격으로 워크플로를 두 번 호출합니다. 첫 번째 워크플로는 완료되지만 두 번째 워크플로는 완료되지 않습니다.  
  
 [!code-csharp[CFX_WorkflowInvokerExample#50](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#50)]  
  
> [!NOTE]
> <xref:System.TimeoutException>은 시간 제한 간격이 경과하고 실행 시 워크플로가 유휴 상태가 되는 경우에만 throw됩니다. 완료하는 데 지정한 시간 제한 간격보다 오래 걸리는 워크플로는 해당 워크플로가 유효 상태가 되지 않는 경우에 성공적으로 완료됩니다.  
  
 <xref:System.Activities.WorkflowInvoker>는 호출 메서드의 비동기 버전도 제공합니다. 자세한 내용은 <xref:System.Activities.WorkflowInvoker.InvokeAsync%2A> 및 <xref:System.Activities.WorkflowInvoker.BeginInvoke%2A>를 참조하세요.  
  
### <a name="setting-input-arguments-of-a-workflow"></a>워크플로의 입력 인수 설정  
 워크플로의 입력 인수에 매핑되는 인수 이름으로 키가 지정된 입력 매개 변수 사전을 사용하여 워크플로에 데이터를 전달할 수 있습니다. 이 예제에서는 <xref:System.Activities.Statements.WriteLine>을 호출하고 입력 매개 변수 사전을 사용하여 해당 <xref:System.Activities.Statements.WriteLine.Text%2A> 인수의 값을 지정합니다.  
  
 [!code-csharp[CFX_WorkflowInvokerExample#3](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#3)]  
  
### <a name="retrieving-output-arguments-of-a-workflow"></a>워크플로의 출력 인수 검색  
 <xref:System.Activities.WorkflowInvoker.Invoke%2A> 호출에서 반환되는 출력 사전을 사용하여 워크플로의 출력 매개 변수를 가져올 수 있습니다 다음 예제에서는 두 개의 입력 인수와 두 개의 출력 인수를 포함하는 단일 `Divide` 활동으로 구성된 워크플로를 호출합니다. 워크플로가 호출되면 각 입력 인수의 값이 인수 이름으로 키가 지정되어 포함된 `arguments` 사전이 전달됩니다. `Invoke`에 대한 호출이 반환되면 각 출력 인수가 `outputs` 사전에 반환됩니다. 이렇게 반환되는 인수에는 인수 이름이 키로 지정됩니다.  
  
 [!code-csharp[CFX_WorkflowInvokerExample#120](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#120)]  
  
 [!code-csharp[CFX_WorkflowInvokerExample#20](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#20)]  
  
 워크플로가 <xref:System.Activities.ActivityWithResult> 또는 `CodeActivity<TResult>` 같은 `Activity<TResult>`에서 파생되는 경우 잘 정의된 <xref:System.Activities.Activity%601.Result%2A> 출력 인수 외의 출력 인수가 있으면 `Invoke`의 비제네릭 오버로드를 사용해야 추가 인수를 검색할 수 있습니다. 이렇게 하려면 `Invoke`로 전달된 워크플로 정의가 <xref:System.Activities.Activity> 형식이어야 합니다. 이 예제에서 `Divide` 활동은 `CodeActivity<int>`에서 파생되지만 단일 반환 값 대신 인수 사전을 반환하는 <xref:System.Activities.Activity>의 비제네릭 오버로드를 사용하도록 `Invoke`로 선언됩니다.  
  
 [!code-csharp[CFX_WorkflowInvokerExample#121](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#121)]  
  
 [!code-csharp[CFX_WorkflowInvokerExample#21](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#21)]  
  
## <a name="using-workflowapplication"></a>WorkflowApplication 사용  
 <xref:System.Activities.WorkflowApplication>은 워크플로 인스턴스 관리를 위한 다양한 기능 집합을 제공합니다. <xref:System.Activities.WorkflowApplication>은 런타임을 캡슐화하는 실제 <xref:System.Activities.Hosting.WorkflowInstance>에 대해 스레드로부터 안전한 프록시로 작용하며 워크플로 인스턴스 만들기 및 로드, 일시 중지 및 다시 시작, 종료 및 수명 주기 이벤트 알림을 위한 메서드를 제공합니다. <xref:System.Activities.WorkflowApplication>을 사용하여 워크플로를 실행하려면 <xref:System.Activities.WorkflowApplication>을 만들고 원하는 수명 주기 이벤트에 알림을 신청한 다음 워크플로를 시작하고 워크플로가 완료될 때까지 기다립니다. 이 예제에서는 <xref:System.Activities.Statements.WriteLine> 활동으로 구성된 워크플로 정의를 만들고 지정된 워크플로 정의를 사용하여 <xref:System.Activities.WorkflowApplication>을 만듭니다. 워크플로가 완료되면 호스트가 알림을 받도록 <xref:System.Activities.WorkflowApplication.Completed%2A>가 처리되고, <xref:System.Activities.WorkflowApplication.Run%2A>을 호출하면 워크플로가 시작되며, 호스트는 워크플로가 완료되기를 기다립니다. 다음 예와 같이, 워크플로가 완료되면 <xref:System.Threading.AutoResetEvent>가 설정되고 호스트 애플리케이션이 실행을 다시 시작할 수 있습니다.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#31](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#31)]  
  
### <a name="workflowapplication-lifecycle-events"></a>WorkflowApplication 수명 주기 이벤트  
 <xref:System.Activities.WorkflowApplication.Completed%2A> 외에도 워크플로가 언로드되거나(<xref:System.Activities.WorkflowApplication.Unloaded%2A>), 중단되거나(<xref:System.Activities.WorkflowApplication.Aborted%2A>), 유휴 상태가 되거나(<xref:System.Activities.WorkflowApplication.Idle%2A> 및 <xref:System.Activities.WorkflowApplication.PersistableIdle%2A>), 처리되지 않은 예외가 발생하면(<xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>) 호스트 작성자에게 알릴 수 있습니다. 다음 예와 같이 워크플로 애플리케이션 개발자는 이 알림을 처리하고 적절한 작업을 수행할 수 있습니다.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#32](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#32)]  
  
### <a name="setting-input-arguments-of-a-workflow"></a>워크플로의 입력 인수 설정  
 <xref:System.Activities.WorkflowInvoker>를 사용할 때 데이터가 전달되는 것과 비슷한 방법으로 매개 변수 사전을 사용하여 워크플로가 시작될 때 워크플로에 데이터를 전달할 수 있습니다. 사전의 각 항목은 지정된 워크플로의 입력 인수에 매핑됩니다. 이 예제에서는 <xref:System.Activities.Statements.WriteLine> 활동으로 구성된 워크플로를 호출하고 입력 매개 변수 사전을 사용하여 <xref:System.Activities.Statements.WriteLine.Text%2A> 인수를 지정합니다.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#30](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#30)]  
  
### <a name="retrieving-output-arguments-of-a-workflow"></a>워크플로의 출력 인수 검색  
 워크플로가 완료되면 <xref:System.Activities.WorkflowApplication.Completed%2A> 사전에 액세스하여 <xref:System.Activities.WorkflowApplicationCompletedEventArgs.Outputs%2A?displayProperty=nameWithType> 처리기에서 출력 매개 변수를 검색할 수 있습니다. 다음 예제에서는 <xref:System.Activities.WorkflowApplication>을 사용하여 워크플로를 호스트합니다. 인스턴스 <xref:System.Activities.WorkflowApplication> 는 단일 `DiceRoll` 활동으로 구성 된 워크플로 정의를 사용 하 여 생성 됩니다. `DiceRoll` 활동에는 주사위 굴리기 작업의 결과를 나타내는 두 개의 출력 인수가 있습니다. 워크플로가 완료되면 <xref:System.Activities.WorkflowApplication.Completed%2A> 처리기에서 출력이 검색됩니다.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#130](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#130)]  
  
 [!code-csharp[CFX_WorkflowApplicationExample#21](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#21)]  
  
> [!NOTE]
> <xref:System.Activities.WorkflowApplication> 및 <xref:System.Activities.WorkflowInvoker>는 입력 인수의 사전을 취하여 `out` 인수 사전을 반환합니다. 이 사전 매개 변수, 속성 및 반환 값은 `IDictionary<string, object>` 형식입니다. 전달되는 사전 클래스의 실제 인스턴스는 `IDictionary<string, object>`를 구현하는 클래스일 수 있습니다. 이 예제에서는 `Dictionary<string, object>`를 사용합니다. 사전에 대 한 자세한 내용은 및 <xref:System.Collections.Generic.IDictionary%602> <xref:System.Collections.Generic.Dictionary%602>을 참조 하십시오.  
  
### <a name="passing-data-into-a-running-workflow-using-bookmarks"></a>책갈피를 사용하여 실행 중인 워크플로에 데이터 전달  
 책갈피는 활동이 다시 시작되기를 수동적으로 대기하는 메커니즘이자 실행 중인 워크플로 인스턴스에 데이터를 전달하기 위한 메커니즘입니다. 다음 예와 같이 활동이 데이터를 대기 중인 경우 <xref:System.Activities.Bookmark>를 만들고 <xref:System.Activities.Bookmark>를 다시 시작할 때 호출할 콜백 메서드를 등록할 수 있습니다.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#15](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#15)]  
  
 `ReadLine` 활동이 실행되면 <xref:System.Activities.Bookmark>를 만들고 콜백을 등록한 다음 <xref:System.Activities.Bookmark>가 다시 시작될 때까지 기다립니다. 책갈피가 다시 시작되면 `ReadLine` 활동은 <xref:System.Activities.Bookmark>와 함께 전달된 데이터를 해당 <xref:System.Activities.Activity%601.Result%2A> 인수에 할당합니다. 이 예제에서는 `ReadLine` 활동을 사용하여 사용자 이름을 수집하고 콘솔 창에 표시하는 워크플로를 만듭니다.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#22](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#22)]  
  
 `ReadLine` 활동이 실행되면 <xref:System.Activities.Bookmark>이라는 `UserName`를 만든 다음 책갈피가 다시 시작될 때까지 기다립니다. 호스트는 원하는 데이터를 수집한 다음 <xref:System.Activities.Bookmark>를 다시 시작합니다. 워크플로가 다시 시작되고 이름을 표시한 다음 완료됩니다.  
  
 호스트 애플리케이션에서 활성 책갈피가 있는지 여부를 확인하기 위해 워크플로를 조사할 수 있습니다. 이를 위해 <xref:System.Activities.WorkflowApplication.GetBookmarks%2A> 인스턴스의 <xref:System.Activities.WorkflowApplication> 메서드를 호출하거나 <xref:System.Activities.WorkflowApplicationIdleEventArgs> 처리기에서 <xref:System.Activities.WorkflowApplication.Idle%2A>를 조사할 수 있습니다.  
  
 다음 코드 예제는 책갈피를 다시 시작하기 전에 활성 책갈피를 열거한다는 점을 제외하고 앞의 예제와 유사합니다. 워크플로가 시작된 다음 <xref:System.Activities.Bookmark>가 만들어지고 워크플로가 유휴 상태가 되면 <xref:System.Activities.WorkflowApplication.GetBookmarks%2A>가 호출됩니다. 워크플로가 완료되면 다음 출력이 콘솔에 표시됩니다.  
  
 **이름이 뭐에요?**  
**BookmarkName 사용자 이름-소유자 Displayname: ReadLine**   
**Steve**   
**안녕하세요, Steve**

[!code-csharp[CFX_WorkflowApplicationExample#14](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#14)]  
  
 다음 코드 예제에서는 <xref:System.Activities.WorkflowApplicationIdleEventArgs> 인스턴스의 <xref:System.Activities.WorkflowApplication.Idle%2A> 처리기로 전달된 <xref:System.Activities.WorkflowApplication>를 검사합니다. 이 예제에서는 유휴 상태로 전환되는 워크플로에 이름이 <xref:System.Activities.Bookmark>이고 `EnterGuess` 활동이 소유하는 `ReadInt` 한 개가 있습니다. 이 코드 예제는 다음을 수행 [하는 방법을 기반으로 합니다. [시작 자습서](getting-started-tutorial.md)의](how-to-run-a-workflow.md)일부인 워크플로를 실행 합니다. 이 단계에서 <xref:System.Activities.WorkflowApplication.Idle%2A> 처리기가 이 예제 코드를 포함하도록 수정되면 다음과 같은 출력이 표시됩니다.  
  
 **BookmarkName 이름 추측-소유자 displayname: ReadInt**
 
 [!code-csharp[CFX_WorkflowApplicationExample#2](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#2)]  
  
## <a name="summary"></a>요약  
 <xref:System.Activities.WorkflowInvoker>는 워크플로를 호출하는 간단한 방법과 워크플로를 시작할 때 데이터를 전달하고 완료된 워크플로에서 데이터를 추출하는 메서드를 제공하지만, <xref:System.Activities.WorkflowApplication>을 사용할 수 있는 복잡한 시나리오는 제공하지 않습니다.
