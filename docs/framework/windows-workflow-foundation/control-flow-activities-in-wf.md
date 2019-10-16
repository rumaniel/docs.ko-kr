---
title: WF의 흐름 제어 활동
ms.date: 03/30/2017
ms.assetid: 6892885b-f7c5-4aea-8f5e-28863fb4ae75
ms.openlocfilehash: bcbb12210af2d0172977dca6f81355031baa043a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61945914"
---
# <a name="control-flow-activities-in-wf"></a>WF의 흐름 제어 활동
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]에서는 워크플로 내의 실행 흐름 제어를 위한 다양한 활동을 제공합니다. 이러한 작업 중 일부 (같은 `Switch` 및 `If`) 프로그래밍 시각적 개체와 같은 환경에서와 비슷한 흐름 제어 구조를 구현 C#, 하지만 (같은 `Pick`) 새 프로그래밍 구조를 모델링 합니다.  
  
 `Parallel` 및 `ParallelForEach`와 같은 활동은 동시에 실행할 여러 자식 활동을 예약하지만, 스레드는 워크플로별로 하나씩만 사용됩니다. 이러한 활동의 각 자식 활동은 순차적으로 실행되며 이전 활동이 완료되거나 유휴 상태로 전환될 때까지는 다음 활동이 실행되지 않습니다. 따라서 이러한 활동은 다른 활동을 차단하는 여러 활동을 인터리브하게 실행해야 하는 애플리케이션에 매우 유용합니다. 이러한 활동의 자식 활동이 유휴 상태로 전환되지 않는 경우에는 `Parallel` 활동은 `Sequence` 활동처럼 실행되고 `ParallelForEach` 활동은 `ForEach` 활동처럼 실행됩니다. 하지만 비동기 활동(예: <xref:System.Activities.AsyncCodeActivity>에서 파생된 활동) 또는 메시징 활동이 사용되는 경우에는 자식 활동이 메시지를 받거나 비동기 작업을 완료할 때가지 기다리는 동안 제어가 다음 분기로 전달됩니다.  
  
## <a name="flow-control-activities"></a>흐름 제어 활동  
  
|활동|설명|  
|--------------|-----------------|  
|<xref:System.Activities.Statements.DoWhile>|포함된 활동을 한 번 실행하면 조건이 `true`인 동안 계속 실행됩니다.|  
|<xref:System.Activities.Statements.ForEach%601>|컬렉션의 각 요소에 대한 포함 문을 직렬로 실행합니다. <xref:System.Activities.Statements.ForEach%601>는 키워드 `foreach`와 유사하지만 언어 문이 아니라 작업으로 구현됩니다.|  
|<xref:System.Activities.Statements.If>|조건이 `true`이면 포함된 활동을 실행하고, 조건이 <xref:System.Activities.Statements.If.Else%2A>이면 `false` 속성에 포함된 활동을 실행할 수 있습니다.|  
|<xref:System.Activities.Statements.Parallel>|포함된 활동을 병렬로 실행합니다.|  
|<xref:System.Activities.Statements.ParallelForEach%601>|컬렉션의 각 요소에 대한 포함 문을 병렬로 실행합니다.|  
|<xref:System.Activities.Statements.Pick>|이벤트 기반 제어 흐름 모델링을 제공합니다.|  
|<xref:System.Activities.Statements.PickBranch>|<xref:System.Activities.Statements.Pick> 활동의 잠재적 실행 경로를 나타냅니다.|  
|<xref:System.Activities.Statements.Sequence>|포함된 활동을 차례로 실행합니다.|  
|<xref:System.Activities.Statements.Switch%601>|지정된 식의 값을 기준으로 많은 활동 중에서 실행할 활동 하나를 선택합니다.|  
|<xref:System.Activities.Statements.While>|조건이 `true`이면 포함된 활동을 실행합니다.|
