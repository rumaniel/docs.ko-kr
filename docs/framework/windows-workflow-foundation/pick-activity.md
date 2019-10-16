---
title: 선택 활동
ms.date: 03/30/2017
ms.assetid: b3e49b7f-0285-4720-8c09-11ae18f0d53e
ms.openlocfilehash: b9ee6c06377760d27bc54d39c1d1f3ecf67ea0d8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61909426"
---
# <a name="pick-activity"></a>선택 활동
<xref:System.Activities.Statements.Pick> 활동은 해당 처리기 앞에 있는 이벤트 트리거 집합의 모델링을 단순화합니다.  <xref:System.Activities.Statements.Pick> 활동은 <xref:System.Activities.Statements.PickBranch> 활동 컬렉션을 포함합니다. 여기서 각 <xref:System.Activities.Statements.PickBranch>는 <xref:System.Activities.Statements.PickBranch.Trigger%2A> 활동과 <xref:System.Activities.Statements.PickBranch.Action%2A> 활동의 쌍입니다.  실행 시간에 모든 분기에 대한 트리거가 병렬로 실행됩니다.  트리거 하나가 완료되면 그에 상응하는 작업이 실행되고 다른 모든 트리거가 취소됩니다.  [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]<xref:System.Activities.Statements.Pick> 활동의 동작은 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]<xref:System.Workflow.Activities.ListenActivity> 활동과 유사합니다.  
  
 다음 [Pick 활동 사용](./samples/using-the-pick-activity.md) SDK 샘플 스크린샷에서는 분기가 두 개 있는 Pick 활동을 보여 줍니다.  한 분기에는 명령줄에서 입력을 읽는 사용자 지정 활동인 **Read input**이라는 트리거가 있습니다. 두 번째 분기에는 <xref:System.Activities.Statements.Delay> 활동 트리거가 있습니다. 경우는 **Read input** 작업 하기 전에 데이터를 받을 합니다 <xref:System.Activities.Statements.Delay> 활동이 완료 되 면 <xref:System.Activities.Statements.Delay> 지연이 취소 되 고 인사말이 콘솔에 기록 됩니다.  할당된 시간 안에 **Read input** 활동에 데이터가 수신되지 않으면 활동이 취소되고 시간 제한 메시지가 콘솔에 기록됩니다.  이것은 모든 작업에 제한 시간을 추가하는 데 사용되는 일반적인 패턴입니다.  
  
 ![선택 활동](./media/pick-activity/pick-activity-two-branches.jpg)  
  
## <a name="best-practices"></a>최선의 구현 방법  
 Pick을 사용할 때 실행되는 분기는 트리거가 먼저 완료되는 분기입니다.  개념상 모든 트리거는 병렬로 실행되며 다른 트리거가 완료되어 해당 트리거가 취소되기 전에 한 트리거가 대부분의 논리를 실행할 수 있습니다.  이 점을 염두에 두고 Pick 활동을 사용할 때 따라야 할 일반적인 지침은 트리거를 단일 이벤트를 나타내는 것으로 처리하고 가능한 한 작은 논리를 입력하는 것입니다.  이상적으로는 트리거가 이벤트를 받을 만큼 충분한 논리를 포함해야 하며 해당 이벤트의 모든 처리가 분기 작업으로 이동해야 합니다.  이 메서드는 트리거 실행 간에 겹치는 양을 최소화합니다.  예를 들어, 트리거 두 개를 사용하는 <xref:System.Activities.Statements.Pick>을 살펴봅니다. 이 경우 각 트리거는 <xref:System.ServiceModel.Activities.Receive> 활동과 추가 논리를 포함합니다.  추가 논리로 유휴 지점이 도입되는 경우 두 <xref:System.ServiceModel.Activities.Receive> 활동이 성공적으로 완료될 가능성이 있습니다.  한 트리거는 완전히 완료되는 반면, 다른 트리거는 부분적으로 완료됩니다.  일부 시나리오에서는 메시지를 허용한 다음 메시지 처리를 부분적으로 완료하는 방법이 허용되지 않습니다.  따라서 <xref:System.ServiceModel.Activities.Receive>가 트리거에서 일반적으로 사용되는 동안 <xref:System.ServiceModel.Activities.SendReply> 및 <xref:System.ServiceModel.Activities.Receive>와 같은 WF 기본 제공 메시징 활동을 사용할 때는 가능한 경우 항상 <xref:System.ServiceModel.Activities.SendReply> 및 기타 논리를 작업에 입력해야 합니다.  
  
## <a name="using-the-pick-activity-in-the-designer"></a>디자이너에서 Pick 활동 사용  
 디자이너에서 Pick을 사용하려면 도구 상자에서 **Pick** 및 **PickBranch**를 찾습니다.  **Pick**를 끌어 캔버스에 놓습니다.  기본적으로 디자이너의 새 **Pick** 활동은 분기 두 개를 포함합니다.  분기를 더 추가하려면 **PickBranch** 활동을 끌어서 기존 분기 옆에 놓습니다. **Pick** 활동의 **Trigger** 영역 또는 **PickBranch**의 **Action** 영역에 활동을 놓을 수 있습니다.  
  
## <a name="using-the-pick-activity-in-code"></a>코드에서 Pick 활동 사용  
 <xref:System.Activities.Statements.Pick> 컬렉션에 <xref:System.Activities.Statements.Pick.Branches%2A> 활동을 채워서 <xref:System.Activities.Statements.PickBranch> 활동을 사용합니다. 각 <xref:System.Activities.Statements.PickBranch> 활동에는 <xref:System.Activities.Statements.PickBranch.Trigger%2A> 형식의 <xref:System.Activities.Activity> 속성이 있습니다. 지정된 활동의 실행이 완료되면 <xref:System.Activities.Statements.PickBranch.Action%2A>이 실행됩니다.  
  
 다음 코드 예에서는 <xref:System.Activities.Statements.Pick> 활동을 사용하여 콘솔 행 읽기 활동에 대해 제한 시간을 지정하는 방법을 보여 줍니다.  
  
```csharp  
Sequence body = new Sequence()  
{  
    Variables = { name },  
    Activities =   
   {  
       new System.Activities.Statements.Pick  
        {  
           Branches =   
           {  
               new PickBranch  
               {  
                   Trigger = new ReadLine  
                   {  
                      Result = name,  
                      BookmarkName = "name"  
                   },  
                   Action = new WriteLine   
                   {   
                       Text = ExpressionServices.Convert<string>(ctx => "Hello " +   
                           name.Get(ctx))   
                   }  
               },  
               new PickBranch  
               {  
                   Trigger = new Delay  
                   {  
                      Duration = new TimeSpan(0, 0, 5)  
                   },  
                   Action = new WriteLine  
                   {  
                      Text = "Time is up."  
                   }  
               }  
           }  
       }  
   }  
};  
```  
  
```xaml  
<Sequence xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <Sequence.Variables>  
    <Variable x:TypeArguments="x:String" Name="username" />  
  </Sequence.Variables>  
  <Pick>  
    <PickBranch>  
      <PickBranch.Trigger>  
        <ReadLine BookmarkName="name" Result="username" />  
      </PickBranch.Trigger>  
      <WriteLine>[String.Concat("Hello ", username)]</WriteLine>  
    </PickBranch>  
    <PickBranch>  
      <PickBranch.Trigger>  
        <Delay>00:00:05</Delay>  
      </PickBranch.Trigger>  
      <WriteLine>Time is up.</WriteLine>  
    </PickBranch>  
  </Pick>  
</Sequence>  
```
