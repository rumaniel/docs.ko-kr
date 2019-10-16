---
title: '방법: 순차 워크플로 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5280e816-ae17-48c4-8de0-a1e6895dd8f0
ms.openlocfilehash: 61e3f01b1259536ff15d71526e91aef42069722e
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70989697"
---
# <a name="how-to-create-a-sequential-workflow"></a>방법: 순차 워크플로 만들기

기본 제공 활동뿐 아니라 사용자 지정 활동에서도 워크플로를 구성할 수 있습니다. 이 항목에서는 <xref:System.Activities.Statements.Sequence> 활동과 같은 기본 제공 활동 및 이전 [방법의 사용자 지정 활동을 모두 사용 하는 워크플로를 만드는 과정을 단계별로 설명 합니다. 작업](how-to-create-an-activity.md) 항목을 만듭니다. 이 워크플로는 숫자 추측 게임을 모델링합니다.

> [!NOTE]
> 초보자를 위한 자습서의 각 항목은 이전 항목을 바탕으로 합니다. 이 항목을 완료 하려면 먼저 다음을 수행 [해야 합니다. 활동](how-to-create-an-activity.md)을 만듭니다.

> [!NOTE]
> 자습서의 전체 버전을 다운로드하려면 [Windows Workflow Foundation(WF45) - 초보자를 위한 자습서](https://go.microsoft.com/fwlink/?LinkID=248976)를 참조하세요.

## <a name="to-create-the-workflow"></a>워크플로를 만들려면

1. **솔루션 탐색기** 에서 **NumberGuessWorkflowActivities** 을 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 항목**을 차례로 선택 합니다.

2. **설치 됨**, **공통 항목** 노드에서 **워크플로**를 선택 합니다. **워크플로** 목록에서 **작업** 을 선택 합니다.

3. 이름 `SequentialNumberGuessWorkflow` 상자에 를 입력 하 고 **추가**를 클릭 합니다.

4. **도구 상자** 의 **제어 흐름** 섹션에서 **Sequence** 활동을 끌어 워크플로 디자인 화면의 **여기에 작업 놓기** 레이블에 놓습니다.

## <a name="to-create-the-workflow-variables-and-arguments"></a>워크플로 변수와 인수를 만들려면

1. **솔루션 탐색기** 에서 **sequentialnumberguessworkflow.xaml** 를 두 번 클릭 하 여 디자이너에 워크플로를 표시 합니다 (아직 표시 되지 않은 경우).

2. 워크플로 디자이너 왼쪽 아래에 있는 **인수** 를 클릭 하 여 **인수** 창을 표시 합니다.

3. **인수 만들기**를 클릭 합니다.

4. 이름 `MaxNumber` 상자에 를 입력 하 고 **방향** 드롭다운 목록 **에서 시작을 선택한 다음** **인수 형식** 드롭다운 목록에서 **Int32** 를 선택 하 고 enter 키를 눌러 인수를 저장 합니다.

5. **인수 만들기**를 클릭 합니다.

6. 새로 `Turns` 추가 된 인수 아래에 있는 이름 상자에를 입력 하 고 방향 드롭다운 목록에서 바깥쪽을 선택한 다음 인수 형식 드롭다운 목록에서 Int32를 선택 하 고 enter 키를 누릅니다. `MaxNumber`

7. 활동 디자이너 왼쪽 아래에 있는 **인수** 를 클릭 하 여 **인수** 창을 닫습니다.

8. 워크플로 디자이너 왼쪽 아래에 있는 **변수** 를 클릭 하 여 **변수** 창을 표시 합니다.

9. **변수 만들기**를 클릭 합니다.

    > [!TIP]
    > **변수 만들기** 상자가 표시 되지 않으면 workflow designer 화면에서 **Sequence** 활동을 클릭 하 여 선택 합니다.

10. 이름 `Guess` 상자에 를 입력 하 고 **변수 형식** 드롭다운 목록에서 **Int32** 를 선택한 다음 enter 키를 눌러 변수를 저장 합니다.

11. **변수 만들기**를 클릭 합니다.

12. 이름 `Target` 상자에 를 입력 하 고 **변수 형식** 드롭다운 목록에서 **Int32** 를 선택한 다음 enter 키를 눌러 변수를 저장 합니다.

13. 활동 디자이너의 왼쪽 아래에 있는 **변수** 를 클릭 하 여 **변수** 창을 닫습니다.

## <a name="to-add-the-workflow-activities"></a>워크플로 활동을 추가하려면

1. **도구 상자** 의 **기본 형식** 섹션에서 **Assign** 활동을 끌어 **시퀀스** 활동에 놓습니다. To `Target` 상자에 **를** 입력 하 고  **C# 식 입력** 또는 **VB 식 입력** 상자에 다음 식을 입력 합니다.

    ```vb
    New System.Random().Next(1, MaxNumber + 1)
    ```

    ```csharp
    new System.Random().Next(1, MaxNumber + 1)
    ```

    > [!TIP]
    > **도구 상자** 창이 표시 되지 않으면 **보기** 메뉴에서 **도구 상자** 를 선택 합니다.

2. **도구 상자** 의 **제어 흐름** 섹션에서 **DoWhile** 활동을 끌어 워크플로에서 **Assign** 활동 아래에 놓습니다.

3. **DoWhile** 활동의 **Condition** 속성 값 상자에 다음 식을 입력 합니다.

    ```vb
    Guess <> Target
    ```

    ```csharp
    Guess != Target
    ```

     <xref:System.Activities.Statements.DoWhile> 활동은 자식 활동을 실행한 다음 해당 <xref:System.Activities.Statements.DoWhile.Condition%2A>을 확인합니다. <xref:System.Activities.Statements.DoWhile.Condition%2A>이 `True`로 확인되면 <xref:System.Activities.Statements.DoWhile>의 활동이 다시 실행됩니다. 이 예제에서는 사용자의 추측 값을 확인하여 추측이 올바를 때까지 <xref:System.Activities.Statements.DoWhile>이 계속됩니다.

4. **도구 상자** 의 **NumberGuessWorkflowActivities** 섹션에서 **Prompt** 활동을 끌어 이전 단계의 **DoWhile** 활동에 놓습니다.

5. **속성 창**에서 프롬프트 활동의 `"EnterGuess"` **BookmarkName** 속성 값 상자에 따옴표를 포함 하 여을 입력 합니다. 결과 `Guess` 속성 값 상자에를 입력 하 고 **텍스트** 속성 상자에 다음 식을 입력 합니다.

    ```vb
    "Please enter a number between 1 and " & MaxNumber
    ```

    ```csharp
    "Please enter a number between 1 and " + MaxNumber
    ```

    > [!TIP]
    > **속성 창이** 표시 되지 않으면 **보기** 메뉴에서 **속성 창** 을 선택 합니다.

6. **도구 상자** 의 **기본 형식** 섹션에서 **Assign** 활동을 끌어 **Prompt** 활동 뒤에 **DoWhile** 활동에 놓습니다.

    > [!NOTE]
    > **Assign** 활동을 삭제 하는 경우 workflow Designer가 **Prompt** 활동과 새로 추가 된 **Assign** 활동을 모두 포함 하도록 **Sequence** 활동을 자동으로 추가 하는 방법을 확인 합니다.

7. To `Turns` 상자에 **를** 입력 하 `Turns + 1` 고  **C# 식 입력** 또는 **VB 식 입력** 상자에 입력 합니다.

8. **도구 상자** 의 **제어 흐름** 섹션에서 **If** 활동을 끌어 새로 추가 된 **Assign** 활동 뒤에 오도록 **시퀀스** 활동에 놓습니다.

9. **If** 활동의 **Condition** 속성 값 상자에 다음 식을 입력 합니다.

    ```vb
    Guess <> Target
    ```

    ```csharp
    Guess != Target
    ```

10. **도구 상자** 의 **제어 흐름** 섹션에서 다른 **if** 활동을 끌어 첫 번째 **if** 활동의 **Then** 섹션에 놓습니다.

11. 새로 추가 된 **If** 활동의 **Condition** 속성 값 상자에 다음 식을 입력 합니다.

    ```text
    Guess < Target
    ```

12. **도구 상자** 의 **기본 형식** 섹션에서 두 **WriteLine** 활동을 끌어 새로 추가 된 **If** 활동의 **Then** 섹션에 있고, 다른 하나는 **Else** 섹션에 놓습니다.

13. **Then** 섹션에서 **WriteLine** 활동을 클릭 하 여 선택 하 고 **텍스트** 속성 값 상자에 다음 식을 입력 합니다.

    ```text
    "Your guess is too low."
    ```

14. **Else** 섹션에서 **WriteLine** 활동을 클릭 하 여 선택 하 고 **텍스트** 속성 값 상자에 다음 식을 입력 합니다.

    ```text
    "Your guess is too high."
    ```

     다음 예에서는 완료 된 워크플로를 보여 줍니다.

     ![완료 된 순차 워크플로를 보여 주는 스크린샷](./media/how-to-create-a-sequential-workflow/complete-sequential-workflow.jpg)

## <a name="to-build-the-workflow"></a>워크플로를 빌드하려면

1. Ctrl+Shift+B를 눌러 솔루션을 빌드합니다.

     워크플로를 실행 하는 방법에 대 한 지침은 다음 항목 [을 참조 하세요. 워크플로](how-to-run-a-workflow.md)를 실행 합니다. 이미 완료 [한 경우: 다른 형식의 워크플로](how-to-run-a-workflow.md) 를 사용 하 여 워크플로 단계를 실행 하 고이 단계에서 순차 워크플로를 사용 하 여 워크플로 단계를 실행 하려면 [방법: [응용 프로그램을 빌드하고 실행 하려면](how-to-run-a-workflow.md#BKMK_ToRunTheApplication) 워크플로](how-to-run-a-workflow.md)를 실행 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Activities.Statements.Flowchart>
- <xref:System.Activities.Statements.FlowDecision>
- [Windows Workflow Foundation 프로그래밍](programming.md)
- [워크플로 디자인](designing-workflows.md)
- [초보자를 위한 자습서](getting-started-tutorial.md)
- [방법: 활동 만들기](how-to-create-an-activity.md)
- [방법: 워크플로 실행](how-to-run-a-workflow.md)
