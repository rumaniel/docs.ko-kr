---
title: 순서도 워크플로
ms.date: 03/30/2017
ms.assetid: b0a3475c-d22f-49eb-8912-973c960aebf5
ms.openlocfilehash: 1840f677929509e4902498c5aa8920f49cb13496
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61773596"
---
# <a name="flowchart-workflows"></a>순서도 워크플로

순서도는 잘 알려진 프로그램 설계용 패러다임입니다. Flowchart 활동은 일반적으로 순차적이 아닌 워크플로를 구현하는 데 사용하지만, `FlowDecision` 노드를 사용하지 않는 경우 순차적 워크플로에도 사용할 수 있습니다.

## <a name="flowchart-workflow-structure"></a>순서도 워크플로 구조

 Flowchart 활동은 에서 실행되는 활동의 컬렉션을 포함하는 활동입니다.  순서도에는 변수 값에 따라 포함된 활동 사이의 실행을 연결하는 <xref:System.Activities.Statements.FlowDecision> 및 <xref:System.Activities.Statements.FlowSwitch%601> 같은 흐름 제어 요소도 포함되어 있습니다.

## <a name="types-of-flow-nodes"></a>흐름 노드 형식

 요소가 실행될 때 필요한 흐름 제어 형식에 따라 다양한 형식의 요소가 사용됩니다. 다음과 같은 순서도 요소 형식이 있습니다.

- `FlowStep` - 순서도에서 실행의 한 단계를 모델링합니다.

- `FlowDecision` - <xref:System.Activities.Statements.If>와 유사한 부울 조건을 기반으로 실행을 분기합니다.

- `FlowSwitch` – <xref:System.Activities.Statements.Switch%601>과 유사한 전용 스위치를 기반으로 실행을 분기합니다.

각 링크에는 자식 활동을 실행하는 데 사용할 수 있는 `Action`을 정의하는 <xref:System.Activities.ActivityAction> 속성과 요소 실행이 완료되었을 때 실행할 현재 요소를 정의하는 하나 이상의 `Next` 속성이 있습니다.

### <a name="creating-a-basic-activity-sequence-with-a-flowstep-node"></a>FlowStep 노드로 기본 활동 시퀀스 만들기

두 활동이 차례로 실행되는 기본 시퀀스를 모델링하려면 `FlowStep` 요소를 사용합니다. 다음 예에서는 두 `FlowStep` 요소를 사용하여 두 활동을 순서대로 실행합니다.

```xml
<Flowchart>
  <FlowStep>
    <Assign DisplayName="Get Name">
      <Assign.To>
        <OutArgument x:TypeArguments="x:String">[result]</OutArgument>
      </Assign.To>
      <Assign.Value>
        <InArgument x:TypeArguments="x:String">["User"]</InArgument>
      </Assign.Value>
    </Assign>
    <FlowStep.Next>
      <FlowStep>
        <WriteLine Text="["Hello, " & result]"/>
      </FlowStep>
    </FlowStep.Next>
  </FlowStep>
</Flowchart>
```

### <a name="creating-a-conditional-flowchart-with-a-flowdecision-node"></a>FlowDecision 노드로 조건부 순서도 만들기

순서도 워크플로에서 조건부 흐름 노드를 모델링하려면(즉, 기존 순서도의 결정 기호 역할을 하는 링크를 만들려면) <xref:System.Activities.Statements.FlowDecision> 노드를 사용합니다. 노드의 <xref:System.Activities.Statements.FlowDecision.Condition%2A> 속성은 조건을 정의하는 식으로 설정되고, <xref:System.Activities.Statements.FlowDecision.True%2A> 및 <xref:System.Activities.Statements.FlowDecision.False%2A> 속성은 식이 <xref:System.Activities.Statements.FlowNode> 또는 `true`로 평가될 경우 실행할 `false` 인스턴스로 설정됩니다. 다음 예에서는 <xref:System.Activities.Statements.FlowDecision> 노드를 사용하는 순서도를 정의하는 방법을 보여 줍니다.

```xml
<Flowchart>
  <FlowStep>
    <Read Result="[s]"/>
    <FlowStep.Next>
      <FlowDecision>
        <IsEmpty Input="[s]" />
        <FlowDecision.True>
          <FlowStep>
            <Write Text="Empty"/>
          </FlowStep>
        </FlowDecision.True>
        <FlowDecision.False>
          <FlowStep>
            <Write Text="Non-Empty"/>
          </FlowStep>
        </FlowDecision.False>
      </FlowDecision>
    </FlowStep.Next>
  </FlowStep>
</Flowchart>
```

### <a name="creating-an-exclusive-switch-with-a-flowswitch-node"></a>FlowSwitch 노드로 전용 스위치 만들기

일치하는 값에 따라 전용 경로 하나를 선택하는 순서도를 모델링하려면 <xref:System.Activities.Statements.FlowSwitch%601> 노드를 사용합니다. <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 속성은 선택 항목과 비교할 값을 정의하는 <xref:System.Activities.Activity%601>의 형식 매개 변수를 사용하여 <xref:System.Object>로 설정됩니다. <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 속성은 조건식과 비교할 키 및 <xref:System.Activities.Statements.FlowNode> 개체의 사전을 정의하며, 지정된 case가 조건식과 일치하는 경우 실행의 흐름을 정의하는 <xref:System.Activities.Statements.FlowNode> 개체 집합을 정의합니다. <xref:System.Activities.Statements.FlowSwitch%601>도 조건식과 일치하는 case가 없을 때의 실행 흐름을 정의하는 <xref:System.Activities.Statements.FlowSwitch%601.Default%2A> 속성을 정의합니다. 다음 예에서는 <xref:System.Activities.Statements.FlowSwitch%601> 요소를 사용하는 워크플로를 정의하는 방법을 보여 줍니다.

```xml
<Flowchart>
  <FlowSwitch>
    <FlowStep x:Key="Red">
      <WriteRed/>
    </FlowStep>
    <FlowStep x:Key="Blue">
      <WriteBlue/>
    </FlowStep>
    <FlowStep x:Key="Green">
      <WriteGreen/>
    </FlowStep>
  </FlowSwitch>
</Flowchart>
```
