---
title: 예외
ms.date: 03/30/2017
ms.assetid: 065205cc-52dd-4f30-9578-b17d8d113136
ms.openlocfilehash: b08fca37e9695f57f1fcca114531e8a1e8b90c55
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64640902"
---
# <a name="exceptions"></a>예외
워크플로에서 <xref:System.Activities.Statements.TryCatch> 활동을 사용하여 워크플로 실행 중에 발생하는 예외를 처리할 수 있습니다. 이러한 예외를 처리하거나 <xref:System.Activities.Statements.Rethrow> 활동을 사용하여 다시 throw할 수 있습니다. <xref:System.Activities.Statements.TryCatch.Finally%2A> 섹션의 활동은 <xref:System.Activities.Statements.TryCatch.Try%2A> 섹션 또는 <xref:System.Activities.Statements.TryCatch.Catches%2A> 섹션이 완료되면 실행됩니다. 워크플로 호스팅하는 <xref:System.Activities.WorkflowApplication> 인스턴스를 사용할 수도 있습니다는 <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> 으로 처리 되지 않은 예외를 처리할 이벤트 처리기를 <xref:System.Activities.Statements.TryCatch> 활동입니다.  
  
## <a name="causes-of-exceptions"></a>예외의 원인  
 워크플로에서 다음과 같은 방식으로 예외가 생성될 수 있습니다.  
  
- <xref:System.Activities.Statements.TransactionScope>에서 트랜잭션의 시간 초과  
  
- <xref:System.Activities.Statements.Throw> 활동을 사용하여 워크플로에서 throw된 명시적 예외.  
  
- 활동에서 throw되는 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 예외  
  
- 워크플로에서 사용되는 라이브러리, 구성 요소 또는 서비스와 같은 외부 코드에서 throw되는 예외  
  
## <a name="handling-exceptions"></a>예외 처리  
 활동에서 예외가 throw되었지만 처리되지 않은 경우 워크플로 인스턴스를 종료하는 것이 기본 동작입니다. 사용자 지정 <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> 처리기가 있는 경우 이 기본 동작을 재정의할 수 있습니다. 워크플로 호스트 작성자는 이 처리기를 사용하여 사용자 지정 로깅, 워크플로 중단, 워크플로 취소, 워크플로 종료 등의 적절한 처리를 제공할 수 있습니다.  처리할 수 없는 예외가 워크플로에 발생한 경우 <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> 처리기가 호출됩니다. 워크플로의 최종 결과를 결정하는 <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>에서 반환된 가능한 동작에는 3가지가 있습니다.  
  
- **취소** -취소 된 워크플로 인스턴스는 분기 실행의 정상적인 종료 합니다. 취소 동작은 CancellationScope 활동을 사용하는 경우와 같이 모델링할 수 있습니다. 완료된 처리기는 취소 프로세스가 완료되면 호출됩니다. 취소된 워크플로는 Cancelled 상태입니다.  
  
- **종료** -종료 된 워크플로 인스턴스를 다시 시작 하거나 다시 시작할 수 없습니다.  이 실행에서는 종료된 이유로서 예외를 제공할 수 있는 완료된 이벤트를 트리거합니다. 종료된 처리기는 종료 프로세스가 완료되면 호출됩니다. 종료된 워크플로는 Faulted 상태입니다.  
  
- **중단** -유지 하도록 구성한 경우에 중단 된 워크플로 인스턴스를 다시 시작할 수 있습니다.  지속성이 없을 경우 워크플로는 재개할 수 없습니다.  이렇게 하면 워크플로가 중단된 경우 마지막 유지 시점 이후의 모든 작업 수행(메모리)이 손실됩니다. 중단된 워크플로의 경우 중단 프로세스가 완료된 이유로서 중단된 처리기가 예외를 통해 호출됩니다. 그러나, Cancelled 및 Terminated와 같이 Completed 처리기는 호출되지 않습니다. 중단된 워크플로가 중단된 상태인 경우입니다.  
  
 다음 예제에서는 예외를 throw하는 워크플로를 호출합니다. 이 예외는 워크플로에서 처리되지 않으며 <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> 처리기가 호출됩니다. <xref:System.Activities.WorkflowApplicationUnhandledExceptionEventArgs>를 검사하여 예외에 대한 정보를 제공하고 워크플로가 종료됩니다.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#1](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#1)]  
  
### <a name="handling-exceptions-with-the-trycatch-activity"></a>TryCatch 활동을 사용하여 예외 처리  
 워크플로 내부의 예외 처리는 <xref:System.Activities.Statements.TryCatch> 활동을 통해 수행됩니다. <xref:System.Activities.Statements.TryCatch> 활동에는 특정 <xref:System.Activities.Statements.TryCatch.Catches%2A> 형식에 각각 연결되는 <xref:System.Activities.Statements.Catch> 활동의 <xref:System.Exception> 컬렉션이 있습니다. <xref:System.Activities.Statements.TryCatch.Try%2A> 활동의 <xref:System.Activities.Statements.TryCatch> 섹션에 포함된 활동에 의해 throw된 예외가 <xref:System.Activities.Statements.Catch%601> 컬렉션의 <xref:System.Activities.Statements.TryCatch.Catches%2A> 활동의 예외와 일치하면 예외가 처리됩니다. 예외가 명시적으로 다시 throw되거나 새 예외가 throw될 경우 이 예외는 부모 활동에 전달됩니다. 다음 코드 예제에서는 <xref:System.Activities.Statements.TryCatch> 섹션에서 <xref:System.ApplicationException> 활동에 의해 throw되는 <xref:System.Activities.Statements.TryCatch.Try%2A>을 처리하는 <xref:System.Activities.Statements.Throw> 활동을 보여 줍니다. 예외 메시지는 <xref:System.Activities.Statements.Catch%601> 활동에 의해 콘솔에 기록된 다음 <xref:System.Activities.Statements.TryCatch.Finally%2A> 섹션에서 콘솔에 기록됩니다.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#33](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#33)]  
  
 <xref:System.Activities.Statements.TryCatch.Finally%2A> 섹션의 활동은 <xref:System.Activities.Statements.TryCatch.Try%2A> 섹션 또는 <xref:System.Activities.Statements.TryCatch.Catches%2A> 섹션이 성공적으로 완료되면 실행됩니다. <xref:System.Activities.Statements.TryCatch.Try%2A> 단원은 예외가 throw되면 성공적으로 완료되고 예외가 throw되거나 다시 throw되지 않으면 <xref:System.Activities.Statements.TryCatch.Catches%2A> 단원이 성공적으로 완료됩니다. 예외가 <xref:System.Activities.Statements.TryCatch.Try%2A>의 <xref:System.Activities.Statements.TryCatch> 단원에서 throw되고 <xref:System.Activities.Statements.Catch%601> 단원에서 <xref:System.Activities.Statements.TryCatch.Catches%2A>에 의해 처리되지 않거나 <xref:System.Activities.Statements.TryCatch.Catches%2A>에서 다시 throw되면 <xref:System.Activities.Statements.TryCatch.Finally%2A>의 모든 활동은 다음 중 하나가 발생하지 않는 한 실행되지 않습니다.  
  
- 더 높은 수준의 <xref:System.Activities.Statements.TryCatch>에서 예외가 다시 throw되는지 여부에 관계 없이 워크플로에서 더 높은 수준의 <xref:System.Activities.Statements.TryCatch> 활동에 의해 예외가 catch됩니다.  
  
- 예외는 더 높은 수준의 <xref:System.Activities.Statements.TryCatch>에서 처리되며 워크플로 루트를 이스케이프하며 워크플로는 종료하거나 중단하는 대신 취소하도록 구성됩니다. <xref:System.Activities.WorkflowApplication>을 사용하여 호스트된 워크플로는 <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>을 처리하고 <xref:System.Activities.UnhandledExceptionAction.Cancel>을 반환하여 구성할 수 있습니다. <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>의 처리 예제는 이 항목에 이전에 제공된 것입니다. <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior>을 워크플로 서비스는 사용하고 <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction.Cancel>을 지정하여 구성할 수 있습니다. 구성의 예 <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior>를 참조 하세요 [워크플로 서비스 호스트 확장성](../wcf/feature-details/workflow-service-host-extensibility.md)합니다.  
  
## <a name="exception-handling-versus-compensation"></a>예외 처리와 보정 비교  
 예외 처리와 보정의 차이점은 예외 처리는 활동 실행 중에 발생하고, 보정은 활동이 완료된 이후에 발생한다는 점입니다. 예외 처리를 사용하면 활동에서 예외가 발생한 이후에 정리 작업이 가능하고, 보정을 사용하면 이전에 성공적으로 완료된 활동을 실행 취소할 수 있습니다. 자세한 내용은 [보정](compensation.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Activities.Statements.TryCatch>
- <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>
- <xref:System.Activities.Statements.CompensableActivity>
