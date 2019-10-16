---
title: '방법: 상태 시스템 워크플로 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3ec60e8f-fad4-493e-a426-e7962d7aee8c
ms.openlocfilehash: e93f84f0bacf7ac205294c12c55afcab8d7319b7
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70989818"
---
# <a name="how-to-create-a-state-machine-workflow"></a>방법: 상태 시스템 워크플로 만들기
기본 제공 활동뿐 아니라 사용자 지정 활동에서도 워크플로를 구성할 수 있습니다. 이 항목에서는 <xref:System.Activities.Statements.StateMachine> 활동과 같은 기본 제공 활동 및 이전 [방법의 사용자 지정 활동을 모두 사용 하는 워크플로를 만드는 과정을 단계별로 설명 합니다. 작업](how-to-create-an-activity.md) 항목을 만듭니다. 이 워크플로는 숫자 추측 게임을 모델링합니다.  
  
> [!NOTE]
> 초보자를 위한 자습서의 각 항목은 이전 항목을 바탕으로 합니다. 이 항목을 완료 하려면 먼저 다음을 수행 [해야 합니다. 활동](how-to-create-an-activity.md)을 만듭니다.  
  
> [!NOTE]
> 자습서의 전체 버전을 다운로드하려면 [Windows Workflow Foundation(WF45) - 초보자를 위한 자습서](https://go.microsoft.com/fwlink/?LinkID=248976)를 참조하세요.  
  
### <a name="to-create-the-workflow"></a>워크플로를 만들려면  
  
1. **솔루션 탐색기** 에서 **NumberGuessWorkflowActivities** 을 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 항목**을 차례로 선택 합니다.  
  
2. **설치 됨**, **공통 항목** 노드에서 **워크플로**를 선택 합니다. **워크플로** 목록에서 **작업** 을 선택 합니다.  
  
3. 이름 `StateMachineNumberGuessWorkflow` 상자에 를 입력 하 고 **추가**를 클릭 합니다.  
  
4. **도구 상자** 의 **상태 시스템** 섹션에서 **StateMachine** 활동을 끌어 워크플로 디자인 화면의 **여기에 작업 놓기** 레이블에 놓습니다.  
  
### <a name="to-create-the-workflow-variables-and-arguments"></a>워크플로 변수와 인수를 만들려면  
  
1. **솔루션 탐색기** 에서 **statemachinenumberguessworkflow.xaml** 를 두 번 클릭 하 여 디자이너에 워크플로를 표시 합니다 (아직 표시 되지 않은 경우).  
  
2. 워크플로 디자이너 왼쪽 아래에 있는 **인수** 를 클릭 하 여 **인수** 창을 표시 합니다.  
  
3. **인수 만들기**를 클릭 합니다.  
  
4. 이름 `MaxNumber` 상자에 를 입력 하 고 **방향** 드롭다운 목록 **에서 시작을 선택한 다음** **인수 형식** 드롭다운 목록에서 **Int32** 를 선택 하 고 enter 키를 눌러 인수를 저장 합니다.  
  
5. **인수 만들기**를 클릭 합니다.  
  
6. 새로 `Turns` 추가 된 인수 아래에 있는 이름 상자에를 입력 하 고 방향 드롭다운 목록에서 바깥쪽을 선택한 다음 인수 형식 드롭다운 목록에서 Int32를 선택 하 고 enter 키를 누릅니다. `MaxNumber`  
  
7. 활동 디자이너 왼쪽 아래에 있는 **인수** 를 클릭 하 여 **인수** 창을 닫습니다.  
  
8. 워크플로 디자이너 왼쪽 아래에 있는 **변수** 를 클릭 하 여 **변수** 창을 표시 합니다.  
  
9. **변수 만들기**를 클릭 합니다.  
  
    > [!TIP]
    > **변수 만들기** 상자가 표시 되지 않으면 workflow designer 화면에서 <xref:System.Activities.Statements.StateMachine> 활동을 클릭 하 여 선택 합니다.  
  
10. 이름 `Guess` 상자에 를 입력 하 고 **변수 형식** 드롭다운 목록에서 **Int32** 를 선택한 다음 enter 키를 눌러 변수를 저장 합니다.  
  
11. **변수 만들기**를 클릭 합니다.  
  
12. 이름 `Target` 상자에 를 입력 하 고 **변수 형식** 드롭다운 목록에서 **Int32** 를 선택한 다음 enter 키를 눌러 변수를 저장 합니다.  
  
13. 활동 디자이너의 왼쪽 아래에 있는 **변수** 를 클릭 하 여 **변수** 창을 닫습니다.  
  
### <a name="to-add-the-workflow-activities"></a>워크플로 활동을 추가하려면  
  
1. **State1** 을 클릭 하 여 선택 합니다. **속성 창**에서 **DisplayName** 을로 `Initialize Target`변경 합니다.  
  
    > [!TIP]
    > **속성 창이** 표시 되지 않으면 **보기** 메뉴에서 **속성 창** 을 선택 합니다.  
  
2. Workflow designer에서 새로 이름이 바뀐 **Initialize Target** 상태를 두 번 클릭 하 여 확장 합니다.  
  
3. **도구 상자** 의 **기본 형식** 섹션에서 **Assign** 활동을 끌어 상태의 **항목** 섹션에 놓습니다. To `Target` 상자에 **를** 입력 하 고  **C# 식 입력** 또는 **VB 식 입력** 상자에 다음 식을 입력 합니다.  
  
    ```vb  
    New System.Random().Next(1, MaxNumber + 1)  
    ```  
  
    ```csharp  
    new System.Random().Next(1, MaxNumber + 1)  
    ```  
  
    > [!TIP]
    > **도구 상자** 창이 표시 되지 않으면 **보기** 메뉴에서 **도구 상자** 를 선택 합니다.  
  
4. Workflow designer 위쪽의 이동 경로 표시에서 **StateMachine** 을 클릭 하 여 workflow designer의 전체 상태 시스템 뷰로 돌아갑니다.  
  
5. **도구 상자** 의 **상태 시스템** 섹션에서 **state** 활동을 workflow designer로 끌어 **Initialize Target** 상태 위로 가져갑니다. 새 상태에 있는 경우 네 개의 삼각형이 **Initialize Target** 상태 주위에 표시 됩니다. **초기화 대상** 상태 바로 아래에 있는 삼각형의 새 상태를 삭제 합니다. 그러면 새 상태가 워크플로에 추가 되 고 **Initialize Target** 상태에서 새 상태로 전환 됩니다.  
  
6. **State1** 을 클릭 하 여 선택 하 고 **DisplayName** 을 `Enter Guess`로 변경한 다음 workflow designer에서 상태를 두 번 클릭 하 여 확장 합니다.  
  
7. **도구 상자** 의 **기본 형식** 섹션에서 **WriteLine** 활동을 끌어 상태의 **항목** 섹션에 놓습니다.  
  
8. **WriteLine**의 **텍스트** 속성 상자에 다음 식을 입력 합니다.  
  
    ```vb  
    "Please enter a number between 1 and " & MaxNumber  
    ```  
  
    ```csharp  
    "Please enter a number between 1 and " + MaxNumber  
    ```  
  
9. **도구 상자** 의 **기본 형식** 섹션에서 **Assign** 활동을 끌어 상태의 **종료** 섹션에 놓습니다.  
  
10. To `Turns` 상자에 **를** 입력 하 `Turns + 1` 고  **C# 식 입력** 또는 **VB 식 입력** 상자에 입력 합니다.  
  
11. Workflow designer 위쪽의 이동 경로 표시에서 **StateMachine** 을 클릭 하 여 workflow designer의 전체 상태 시스템 뷰로 돌아갑니다.  
  
12. **도구 상자**의 **상태 시스템** 섹션 **에서 작업 상태 활동을 끌어서** **enter guess** 상태 위로 마우스를 이동 하 고 **enter guess** 상태 오른쪽에 표시 되는 삼각형에 놓으면 전환이 **Enter Guess** 와 **상태**사이에 생성 됩니다.  
  
13. 전환의 기본 이름은 **T2**입니다. Workflow designer에서 전환을 클릭 하 여 선택 하 고 **DisplayName** 을 **Guess**로 설정 합니다. 그런 다음, 선택 된 **상태**를 클릭 하 여 선택 하 고 오른쪽으로 끌어 전체 전환 이름을 표시 하는 데 사용할 공간이 두 상태 중 어느 상태에도 겹치지 않도록 합니다. 이렇게 하면 자습서의 나머지 단계를 보다 쉽게 진행할 수 있습니다.  
  
14. Workflow designer에서 새로 이름이 바뀐 **추측 올바른** 전환을 두 번 클릭 하 여 확장 합니다.  
  
15. **도구 상자** 의 **NumberGuessWorkflowActivities** 섹션에서 **readint** 활동을 끌어 전환의 **트리거** 섹션에 놓습니다.  
  
16. **Readint** 활동의 **속성 창** 에서 **BookmarkName** 속성 값 상자 `"EnterGuess"` 에 따옴표를 포함 하 여를 입력 하 고 **결과** 속성 `Guess` 값 상자에를 입력 합니다.  
  
17. **올바른** 전환의 **조건** 속성 값 상자에 다음 식을 입력 합니다.  
  
    ```vb  
    Guess = Target  
    ```  
  
    ```csharp  
    Guess == Target  
    ```  
  
18. Workflow designer 위쪽의 이동 경로 표시에서 **StateMachine** 을 클릭 하 여 workflow designer의 전체 상태 시스템 뷰로 돌아갑니다.  
  
    > [!NOTE]
    > 트리거 이벤트를 받고 <xref:System.Activities.Statements.Transition.Condition%2A>이 `True`인 경우 전환이 발생합니다. 이 전환의 경우 사용자가 `Guess` 임의로 생성 `Target`된와 일치 하는 경우 제어가 **상태** 에 전달 되 고 워크플로가 완료 됩니다.  
  
19. Guess가 정확한 지 여부에 따라 워크플로는 다른 시도에 대 한 상태 **또는 다시** **Enter 추측** 상태로 전환 되어야 합니다. 두 전환은 모두 **Readint** 활동을 통해 사용자의 추측을 수신 하기 위해 대기 하는 동일한 트리거를 공유 합니다. 이를 공유 전환이라고 합니다. 공유 전환을 만들려면 **추측 올바른** 전환의 시작을 나타내는 원을 클릭 하 고 원하는 상태로 끕니다. 이 경우 전환은 자체 전환 이므로 **추측 올바른** 전환의 시작점을 끌어서 **Enter guess** 상태의 맨 아래에 다시 놓습니다. 전환을 만든 후에는 workflow designer에서 해당 전환을 선택 하 고 **DisplayName** 속성을 **잘못 된 추측**으로 설정 합니다.  
  
    > [!NOTE]
    > 전환 디자이너의 아래쪽에 있는 **공유 트리거 전환 추가** 를 클릭 한 다음 **사용 가능한 상태에서 연결할** 대상 상태를 선택 하 여 전환 디자이너 내에서 공유 전환을 만들 수도 있습니다. 드롭다운.  
  
    > [!NOTE]
    > 전환의 <xref:System.Activities.Statements.Transition.Condition%2A>이 `false`가 되거나 모든 공유 트리거 전환 조건이 `false`가 되는 경우에는 전환이 일어나지 않으며 해당 상태로부터의 모든 전환에 대한 모든 트리거가 다시 예약됩니다. 이 자습서에서는 조건이 구성된 방식(추측이 올바른지 또는 잘못되었는지에 따라 특정 동작이 지정됨) 때문에 이러한 상황이 발생할 수 없습니다.  
  
20. Workflow designer에서 **잘못 된 Guess** 전환을 두 번 클릭 하 여 확장 합니다. **트리거** 는 **추측 올바른** 전환에 사용 된 것과 동일한 **readint** 작업으로 이미 설정 되어 있습니다.  
  
21. **조건** 속성 값 상자에 다음 식을 입력 합니다.  
  
    ```vb  
    Guess <> Target  
    ```  
  
    ```csharp  
    Guess != Target  
    ```  
  
22. **도구 상자** 의 **제어 흐름** 섹션에서 **If** 활동을 끌어 전환의 **작업** 섹션에 놓습니다.  
  
23. **If** 활동의 **Condition** 속성 값 상자에 다음 식을 입력 합니다.  
  
    ```text
    Guess < Target
    ```  
  
24. **도구 상자** 의 **기본 형식** 섹션에서 두 **WriteLine** **활동을 끌어 해당 활동의** **Then** 섹션에 있고 하나는 **Else** 섹션에 놓습니다.  
  
25. **Then** 섹션에서 **WriteLine** 활동을 클릭 하 여 선택 하 고 **텍스트** 속성 값 상자에 다음 식을 입력 합니다.  
  
    ```text
    "Your guess is too low."  
    ```  
  
26. **Else** 섹션에서 **WriteLine** 활동을 클릭 하 여 선택 하 고 **텍스트** 속성 값 상자에 다음 식을 입력 합니다.  
  
    ```text
    "Your guess is too high."  
    ```  
  
27. Workflow designer 위쪽의 이동 경로 표시에서 **StateMachine** 을 클릭 하 여 workflow designer의 전체 상태 시스템 뷰로 돌아갑니다.  
  
     다음 예제에서는 완료된 워크플로를 보여 줍니다.  
  
     ![완료 된 상태 시스템 워크플로를 보여 주는 그림입니다.](./media/how-to-create-a-state-machine-workflow/complete-state-machine-workflow.jpg)  
  
### <a name="to-build-the-workflow"></a>워크플로를 빌드하려면  
  
1. Ctrl+Shift+B를 눌러 솔루션을 빌드합니다.  
  
     워크플로를 실행 하는 방법에 대 한 지침은 다음 항목 [을 참조 하세요. 워크플로](how-to-run-a-workflow.md)를 실행 합니다. 이미 완료 [한 경우: 워크플로의 다른 스타일](how-to-run-a-workflow.md) 을 사용 하 여 워크플로 단계를 실행 하 고이 단계에서 상태 시스템 워크플로를 사용 하 여 실행 [ [하려는 경우 방법](how-to-run-a-workflow.md#BKMK_ToRunTheApplication) : 워크플로](how-to-run-a-workflow.md)를 실행 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Activities.Statements.Flowchart>
- <xref:System.Activities.Statements.FlowDecision>
- [Windows Workflow Foundation 프로그래밍](programming.md)
- [워크플로 디자인](designing-workflows.md)
- [초보자를 위한 자습서](getting-started-tutorial.md)
- [방법: 활동 만들기](how-to-create-an-activity.md)
- [방법: 워크플로 실행](how-to-run-a-workflow.md)
