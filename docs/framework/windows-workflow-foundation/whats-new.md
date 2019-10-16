---
title: Windows Workflow Foundation의 새로운 기능
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Workflow Foundation [WF], what's new
- WF [WF], what's new
ms.assetid: 11f96014-001e-41a0-bcc2-d0684a52fa43
ms.openlocfilehash: 5c08ec3f5618abc601c17cf0d32d583bf21db683
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64656105"
---
# <a name="whats-new-in-windows-workflow-foundation"></a>Windows Workflow Foundation의 새로운 기능
Windows WF (Workflow Foundation)에서 [!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)] 여러 개발 패러다임이 이전 버전에서 변경 합니다. 이제 워크플로에서 많은 새로운 기능을 보다 쉽게 작성, 실행, 유지 관리 및 구현할 수 있습니다. 마이그레이션.NET 3.0 및.NET 3.5 워크플로 응용 프로그램을 최신 버전을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [마이그레이션 지침](migration-guidance.md)합니다.  
  
## <a name="workflow-activity-model"></a>워크플로 활동 모델  
 이제 <xref:System.Workflow.Activities.SequentialWorkflowActivity> 또는 <xref:System.Workflow.Activities.StateMachineWorkflowActivity> 클래스를 사용하는 대신 활동이 워크플로를 만드는 기본 단위로 사용됩니다. <xref:System.Activities.Activity> 클래스는 워크플로 동작에 대한 기본 추상화를 제공합니다. 활동 작성자는 기본 사용자 지정 활동 기능에 대해 <xref:System.Activities.CodeActivity>를 구현하거나 다양한 런타임을 사용하는 사용자 지정 활동 기능에 대해 <xref:System.Activities.NativeActivity>를 구현할 수 있습니다. <xref:System.Activities.Activity> 활동 작성자에 의해 다른 측면에서 선언적으로 새 동작을 표현 하는 데 사용 됩니다 <xref:System.Activities.NativeActivity>, <xref:System.Activities.CodeActivity>, <xref:System.Activities.AsyncCodeActivity>, 또는 <xref:System.Activities.DynamicActivity> 개체를 사용자 지정 개발 또는에 포함 된 [기본 제공 활동 라이브러리](net-framework-4-5-built-in-activity-library.md)합니다.  
  
## <a name="rich-composite-activity-options"></a>풍부한 복합 활동 옵션  
 <xref:System.Activities.Statements.Flowchart>는 작성자가 임의 루프 및 조건 분기를 모델링할 수 있도록 하는 강력한 새 제어 흐름 활동입니다. <xref:System.Activities.Statements.Flowchart>는 이전에는 <xref:System.Workflow.Activities.StateMachineWorkflowActivity>를 사용해서만 구현 가능했던 이벤트 구동 프로그래밍 모델을 제공합니다. 절차적 워크플로에서는 <xref:System.Activities.Statements.TryCatch> 및 <xref:System.Activities.Statements.Switch%601>과 같은 기존 흐름 제어 구조를 모델링하는 새로운 흐름 제어 활동을 활용합니다.  
  
## <a name="expanded-built-in-activity-library"></a>확장된 기본 제공 활동 라이브러리  
 활동 라이브러리에는 다음과 같은 새로운 기능이 있습니다.  
  
- <xref:System.Activities.Statements.DoWhile>, <xref:System.Activities.Statements.Pick>, <xref:System.Activities.Statements.TryCatch>, <xref:System.Activities.Statements.ForEach%601>, <xref:System.Activities.Statements.Switch%601>, <xref:System.Activities.Statements.ParallelForEach%601> 등의 새 흐름 제어 활동  
  
- <xref:System.Activities.Statements.Assign> 등의 멤버 데이터 조작 활동 및 <xref:System.Activities.Statements.AddToCollection%601> 등의 컬렉션 활동  
  
- <xref:System.Activities.Statements.TransactionScope>, <xref:System.Activities.Statements.Compensate> 등의 트랜잭션 제어 활동  
  
- <xref:System.ServiceModel.Activities.SendContent>, <xref:System.ServiceModel.Activities.ReceiveReply> 등의 새로운 메시징 활동  
  
## <a name="explicit-activity-data-model"></a>명시적 활동 데이터 모델  
 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]에는 데이터 저장 또는 이동을 위한 새로운 옵션이 있습니다. <xref:System.Activities.Variable>을 사용하여 활동에 데이터를 저장할 수 있습니다. 활동 내부 또는 외부에서 데이터를 이동할 때 특수 인수 유형을 사용하여 데이터가 이동하는 방향을 결정합니다. 이러한 유형은 <xref:System.Activities.InArgument>, <xref:System.Activities.InOutArgument> 및 <xref:System.Activities.OutArgument>입니다. 자세한 내용은 [Windows Workflow Foundation 데이터 모델](data-model.md)합니다.  
  
## <a name="enhanced-hosting-persistence-and-tracking-options"></a>향상된 호스팅, 지속성 및 추적 옵션  
 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]에서는 지속성이 다음과 같이 향상되었습니다.  
  
- <xref:System.ServiceModel.Activities.WorkflowServiceHost>, <xref:System.Activities.WorkflowApplication>, <xref:System.Activities.WorkflowInvoker> 등과 같은 더 많은 워크플로 실행 옵션이 있습니다.  
  
- <xref:System.Activities.Statements.Persist> 활동을 사용하여 워크플로 상태 데이터를 명시적으로 유지할 수 있습니다.  
  
- 호스트에서 <xref:System.Activities.ActivityInstance>를 언로드하지 않고 유지할 수 있습니다.  
  
- 워크플로에서 유지할 수 없는 데이터로 작업할 때 비지속성 영역을 지정할 수 있습니다. 그러면 비지속성 영역이 있는 동안 지속성이 연기됩니다.  
  
- <xref:System.Activities.Statements.TransactionScope>를 사용하여 트랜잭션을 워크플로로 전달할 수 있습니다.  
  
- <xref:System.Activities.Tracking.TrackingParticipant>를 사용하여 보다 쉽게 추적할 수 있습니다.  
  
- <xref:System.Activities.Tracking.EtwTrackingParticipant>를 사용하여 시스템 이벤트 로그를 추적합니다.  
  
- 이제 보류 중인 워크플로 다시 시작이 <xref:System.Activities.Bookmark> 개체를 사용하여 관리됩니다.  
  
## <a name="easier-ability-to-extend-wf-designer-experience"></a>간편한 WF Designer 환경 확장 기능  
 새 WF Designer에서 Windows Presentation Foundation (WPF) 및 Visual Studio 외부에서 WF 디자이너 재호스팅 때 사용할 수 있는 간편한 모델 빌드되고 또한 사용자 지정 활동 디자이너를 만드는 간편한 메커니즘을 제공 합니다. 자세한 내용은 [워크플로 디자인 환경 사용자 지정](customizing-the-workflow-design-experience.md)합니다.
