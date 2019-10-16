---
title: 워크플로의 취소 동작 모델링
ms.date: 03/30/2017
ms.assetid: d48f6cf3-cdde-4dd3-8265-a665acf32a03
ms.openlocfilehash: ec0cf810693e2eda01a4c489b6eb938538719228
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965946"
---
# <a name="modeling-cancellation-behavior-in-workflows"></a>워크플로의 취소 동작 모델링
워크플로 내에서 활동을 취소할 수도 있고(예: <xref:System.Activities.Statements.Parallel>의 평가 결과가 <xref:System.Activities.Statements.Parallel.CompletionCondition%2A>일 때 완료되지 않은 분기를 `true` 활동을 사용하여 취소하는 경우), 호스트가  <xref:System.Activities.WorkflowApplication.Cancel%2A>을 호출하는 경우에는 워크플로 외부에서 활동을 취소할 수도 있습니다. 취소 처리를 위해 워크플로 작성자는 <xref:System.Activities.Statements.CancellationScope> 활동 또는 <xref:System.Activities.Statements.CompensableActivity> 활동을 사용하거나 취소 논리를 제공하는 사용자 지정 활동을 만들 수 있습니다. 이 항목에서는 워크플로의 취소에 대해 간략하게 설명합니다.  
  
## <a name="cancellation-compensation-and-transactions"></a>취소, 보정 및 트랜잭션  
 애플리케이션에 트랜잭션을 사용하면 트랜잭션 프로세스의 일부에서 오류가 발생하는 경우 트랜잭션 내에서 실행된 모든 변경 내용을 중단(롤백)할 수 있습니다. 그러나 취소하거나 실행을 취소해야 하는 작업 중에는 장기 실행 작업이나 트랜잭션 리소스가 관련되지 않은 작업처럼 트랜잭션에 적합하지 않은 작업도 있습니다. 보정은 워크플로에서 오류가 발생할 경우 이전에 완료된 비트랜잭션 작업의 실행을 취소하는 모델을 제공합니다. 취소는 워크플로 및 활동 작성자가 완료되지 않은 비트랜잭션 작업을 처리하는 모델을 제공합니다. 활동의 실행이 완료되지 않은 상태에서 활동을 취소한 경우 적용 가능한 취소 논리가 있으면 해당 논리가 호출됩니다.  
  
> [!NOTE]
> 트랜잭션 및 보정에 대 한 자세한 내용은 [트랜잭션](workflow-transactions.md) 및 [보정](compensation.md)을 참조 하세요.  
  
## <a name="using-cancellationscope"></a>CancellationScope 사용  
 <xref:System.Activities.Statements.CancellationScope> 활동에는 자식 활동을 포함할 수 있는 <xref:System.Activities.Statements.CancellationScope.Body%2A>와 <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>라는 두 개의 섹션이 있습니다. <xref:System.Activities.Statements.CancellationScope.Body%2A>는 활동의 논리를 구성하는 자식 활동이 포함되는 위치이며, <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>는 활동에 대한 취소 논리를 제공하는 자식 활동이 포함되는 위치입니다. 활동은 완료되지 않은 경우에만 취소할 수 있습니다. <xref:System.Activities.Statements.CancellationScope> 활동의 경우 완료란 <xref:System.Activities.Statements.CancellationScope.Body%2A>에 포함된 활동이 완료되었음을 의미합니다. 취소 요청이 예약되어 있고 <xref:System.Activities.Statements.CancellationScope.Body%2A>의 활동이 완료되지 않은 경우 <xref:System.Activities.Statements.CancellationScope>가 <xref:System.Activities.ActivityInstanceState.Canceled>로 표시되고 <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> 활동이 실행됩니다.  
  
### <a name="canceling-a-workflow-from-the-host"></a>호스트에서 워크플로 취소  
 워크플로를 호스트하는 <xref:System.Activities.WorkflowApplication.Cancel%2A> 인스턴스의 <xref:System.Activities.WorkflowApplication> 메서드를 호출하여 호스트에서 워크플로를 취소할 수 있습니다. 다음 예제에서는 <xref:System.Activities.Statements.CancellationScope>가 있는 워크플로를 만듭니다. 이 워크플로가 호출되면 호스트에서 <xref:System.Activities.WorkflowApplication.Cancel%2A>을 호출합니다. 그 결과로 워크플로의 주 실행이 중지되고 <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>의 <xref:System.Activities.Statements.CancellationScope>가 호출된 다음 워크플로가 <xref:System.Activities.ActivityInstanceState.Canceled> 상태로 완료됩니다.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#35](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#35)]  
  
 이 워크플로가 호출되면 다음 출력이 콘솔에 표시됩니다.  
  
 **워크플로를 시작 합니다.**  
**CancellationHandler가 호출 되었습니다.**    
**워크플로 b30ebb30-df46-4d90-a211-e31c38d8db3c가 취소 되었습니다.**    
> [!NOTE]
> <xref:System.Activities.Statements.CancellationScope> 활동이 취소되고 <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>가 호출되는 경우 적절한 취소 논리를 제공하기 위해서는 해당 활동을 취소하기 전에 취소 대상 활동이 얼마나 진행되었는지 워크플로 작성자가 직접 확인해야 합니다. <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>에서는 취소된 활동의 진행률에 대한 어떠한 정보도 제공하지 않습니다.  
  
 워크플로의 루트를 지난 뒤에 처리되지 않은 예외가 버블링되고 <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> 처리기가 <xref:System.Activities.UnhandledExceptionAction.Cancel>을 반환하는 경우에도 호스트에서 워크플로를 취소할 수 있습니다. 이 예제에서는 워크플로가 시작된 후 <xref:System.ApplicationException>을 throw합니다. 이 예외는 워크플로에서 처리되지 않으므로 <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> 처리기가 호출됩니다. 이 처리기는 워크플로를 취소하도록 런타임에 지시를 내리고, 현재 실행 중인 <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> 활동의 <xref:System.Activities.Statements.CancellationScope>가 호출됩니다.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#36](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#36)]  
  
 이 워크플로가 호출되면 다음 출력이 콘솔에 표시됩니다.  
  
 **워크플로를 시작 합니다.**  
**OnUnhandledException in Workflow 6bb2d5d6-f49a-4c6d-a988-478afb86dbe9**   
**ApplicationException이 throw 되었습니다.**    
**CancellationHandler가 호출 되었습니다.**    
**워크플로 6bb2d5d6-f49a-4c6d-a988-478afb86dbe9가 취소 되었습니다.**    
### <a name="canceling-an-activity-from-inside-a-workflow"></a>워크플로 내에서 활동 취소  
 활동의 부모를 사용하여 활동을 취소할 수도 있습니다. 예를 들어 <xref:System.Activities.Statements.Parallel> 활동에 여러 개의 실행 분기가 있고 해당 <xref:System.Activities.Statements.Parallel.CompletionCondition%2A>이 `true`인 경우 완료되지 않은 분기는 취소됩니다. 이 예제에서는 분기가 두 개인 <xref:System.Activities.Statements.Parallel> 활동을 만듭니다. 이 활동의 <xref:System.Activities.Statements.Parallel.CompletionCondition%2A>이 `true`로 설정되므로 해당 분기 중 하나를 완료하는 즉시 <xref:System.Activities.Statements.Parallel>이 완료됩니다. 이 예제에서는 분기 2가 완료되므로 분기 1이 취소됩니다.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#37](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#37)]  
  
 이 워크플로가 호출되면 다음 출력이 콘솔에 표시됩니다.  
  
 **분기 1부터 시작 합니다.**  
**분기 2가 완료 되었습니다.**    
**분기 1이 취소 되었습니다.**    
**워크플로 e0685e24-18ef-4a47-acf3-5c638732f3be 완료 되었습니다.**  활동의 루트를 지난 뒤에 예외가 버블링되었지만 워크플로의 더 높은 수준에서 해당 예외를 처리하는 경우에도 활동이 취소됩니다. 이 예제에서 워크플로의 주 논리는 <xref:System.Activities.Statements.Sequence> 활동으로 구성되어 있습니다. <xref:System.Activities.Statements.Sequence>는 <xref:System.Activities.Statements.CancellationScope.Body%2A> 활동에 포함된 <xref:System.Activities.Statements.CancellationScope> 활동의 <xref:System.Activities.Statements.TryCatch>로 지정됩니다. <xref:System.Activities.Statements.Sequence>의 본문에서 예외가 throw되면 부모 <xref:System.Activities.Statements.TryCatch> 활동을 통해 해당 예외가 처리되고 <xref:System.Activities.Statements.Sequence>가 취소됩니다.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#39](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#39)]  
  
 이 워크플로가 호출되면 다음 출력이 콘솔에 표시됩니다.  
  
 **시퀀스를 시작 합니다.**  
**시퀀스가 취소 되었습니다.**    
**예외가 catch 되었습니다.**    
**워크플로 e3c18939-121e-4c43-af1c-ba1ce977ce55 완료 되었습니다.**   
### <a name="throwing-exceptions-from-a-cancellationhandler"></a>CancellationHandler에서 예외 throw  
 <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>의 <xref:System.Activities.Statements.CancellationScope>에서 throw되는 예외는 워크플로에 치명적인 영향을 줍니다. <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>에서 예외가 이스케이프될 가능성이 있으면 <xref:System.Activities.Statements.TryCatch>에 <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>를 사용하여 해당 예외를 catch 및 처리해야 합니다.  
  
### <a name="cancellation-using-compensableactivity"></a>CompensableActivity를 사용한 취소  
 <xref:System.Activities.Statements.CancellationScope> 활동과 마찬가지로 <xref:System.Activities.Statements.CompensableActivity>에도 <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>가 있습니다. <xref:System.Activities.Statements.CompensableActivity>를 취소하면 해당 <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>의 모든 활동이 호출됩니다. 이는 보정 가능하며 부분적으로 완료된 작업을 실행 취소하는 데 유용할 수 있습니다. 보정 및 취소에를 사용 <xref:System.Activities.Statements.CompensableActivity> 하는 방법에 대 한 자세한 내용은 [보정](compensation.md)을 참조 하세요.  
  
## <a name="cancellation-using-custom-activities"></a>사용자 지정 활동을 사용한 취소  
 사용자 지정 활동 작성자는 각기 다른 여러 가지 방법으로 사용자 지정 활동에 취소 논리를 구현할 수 있습니다. <xref:System.Activities.Activity>에서 파생되는 사용자 지정 활동은 <xref:System.Activities.Statements.CancellationScope> 또는 활동 본문에 취소 논리를 포함하는 다른 사용자 지정 활동을 배치하여 취소 논리를 구현할 수 있습니다. <xref:System.Activities.AsyncCodeActivity> 및 <xref:System.Activities.NativeActivity> 파생 활동은 해당 <xref:System.Activities.NativeActivity.Cancel%2A> 메서드를 재정의하고 취소 논리를 제공할 수 있습니다. <xref:System.Activities.CodeActivity> 파생 활동은 런타임에서 <xref:System.Activities.CodeActivity.Execute%2A> 메서드를 호출할 때 한 번 실행으로 모든 작업을 수행하기 때문에 취소를 위한 수단을 제공하지 않습니다. 실행 메서드가 아직 호출되지 않은 상태에서 <xref:System.Activities.CodeActivity> 기반 활동이 취소되는 경우 활동이 <xref:System.Activities.ActivityInstanceState.Canceled> 상태로 닫히고 <xref:System.Activities.CodeActivity.Execute%2A> 메서드는 호출되지 않습니다.  
  
### <a name="cancellation-using-nativeactivity"></a>NativeActivity를 사용한 취소  
 <xref:System.Activities.NativeActivity> 파생 활동에서는 <xref:System.Activities.NativeActivity.Cancel%2A> 메서드를 재정의하여 사용자 지정 취소 논리를 제공할 수 있습니다. 이 메서드를 재정의하지 않으면 기본 워크플로 취소 논리가 적용됩니다. 기본 취소는 <xref:System.Activities.NativeActivity> 메서드를 <xref:System.Activities.NativeActivity.Cancel%2A> 재정의 하지 않거나 <xref:System.Activities.NativeActivity.Cancel%2A> 해당 메서드가 기본 <xref:System.Activities.NativeActivity> <xref:System.Activities.NativeActivity.Cancel%2A> 메서드를 호출 하는에 대해 발생 하는 프로세스입니다. 활동을 취소하면 런타임에 취소 대상 활동에 대한 플래그가 설정되고 특정 정리 작업이 자동으로 처리됩니다. 활동에서 처리 중인 책갈피만 있으면 책갈피가 제거되고 활동이 <xref:System.Activities.ActivityInstanceState.Canceled>로 표시됩니다. 취소된 활동에서 처리 중인 자식 활동이 있으면 자식 활동이 차례로 취소됩니다. 자식 활동을 추가로 예약하려는 시도가 있으면 해당 시도가 무시되고 활동이 <xref:System.Activities.ActivityInstanceState.Canceled>로 표시됩니다. 처리 중이던 자식 활동이 <xref:System.Activities.ActivityInstanceState.Canceled> 또는 <xref:System.Activities.ActivityInstanceState.Faulted> 상태로 완료되면 활동이 <xref:System.Activities.ActivityInstanceState.Canceled>로 표시됩니다. 취소 요청은 무시할 수 없습니다. 활동에서 처리 중인 책갈피나 실행 중인 자식 활동이 전혀 없고 취소 플래그가 설정된 후에 작업 항목을 추가로 예약하지도 않는다면 활동이 성공적으로 완료됩니다. 대부분의 시나리오에는 이와 같은 기본 취소 프로세스로도 충분합니다. 그러나 취소 논리가 추가로 필요한 경우에는 기본 제공 취소 활동이나 사용자 지정 활동을 사용할 수 있습니다.  
  
 다음 예제에서는 <xref:System.Activities.NativeActivity.Cancel%2A>의 <xref:System.Activities.NativeActivity> 재정의를 기반으로 하는 사용자 지정 `ParallelForEach` 활동을 정의합니다. 활동을 취소하면 이 재정의를 통해 활동의 취소 논리가 처리됩니다. 이 예제는 [제네릭이 아닌 ParallelForEach](./samples/non-generic-parallelforeach.md) 샘플의 일부입니다.  
  
```csharp  
protected override void Cancel(NativeActivityContext context)  
{  
    // If we do not have a completion condition then we can just  
    // use default logic.  
    if (this.CompletionCondition == null)  
    {  
        base.Cancel(context);  
    }  
    else  
    {  
        context.CancelChildren();  
    }  
}  
```  
  
 <xref:System.Activities.NativeActivity> 파생 활동의 경우 <xref:System.Activities.NativeActivityContext.IsCancellationRequested%2A> 속성을 조사하여 취소가 요청되었는지 여부를 확인하고 <xref:System.Activities.NativeActivityContext.MarkCanceled%2A> 메서드를 호출하여 자신을 취소된 활동으로 표시할 수 있습니다. <xref:System.Activities.NativeActivityContext.MarkCanceled%2A>를 호출한다고 해서 활동이 즉시 완료되지는 않습니다. 일반적으로 런타임에서 더 이상 처리 중인 작업이 없을 때 활동이 완료되지만, <xref:System.Activities.NativeActivityContext.MarkCanceled%2A>를 호출한 경우에는 최종 상태가 <xref:System.Activities.ActivityInstanceState.Canceled> 대신 <xref:System.Activities.ActivityInstanceState.Closed>가 됩니다.  
  
### <a name="cancellation-using-asynccodeactivity"></a>AsyncCodeActivity를 사용한 취소  
 <xref:System.Activities.AsyncCodeActivity> 기반 활동에서도 <xref:System.Activities.AsyncCodeActivity.Cancel%2A> 메서드를 재정의하여 사용자 지정 취소 논리를 제공할 수 있습니다. 이 메서드를 재정의하지 않은 경우 활동이 취소되지 않으면 취소 처리도 수행되지 않습니다. 다음 예제에서는 <xref:System.Activities.AsyncCodeActivity.Cancel%2A>의 <xref:System.Activities.AsyncCodeActivity> 재정의를 기반으로 하는 사용자 지정 `ExecutePowerShell` 활동을 정의합니다. 활동을 취소하면 필요한 취소 동작이 수행됩니다.
  
 [!code-csharp[CFX_WorkflowApplicationExample#1020](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#1020)]  
  
 <xref:System.Activities.AsyncCodeActivity> 파생 활동의 경우 <xref:System.Activities.AsyncCodeActivityContext.IsCancellationRequested%2A> 속성을 조사하여 취소가 요청되었는지 여부를 확인하고 <xref:System.Activities.AsyncCodeActivityContext.MarkCanceled%2A> 메서드를 호출하여 자신을 취소된 활동으로 표시할 수 있습니다.
