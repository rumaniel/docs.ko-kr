---
title: '방법: 순서도 워크플로 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 185d7aea-68a6-4bd8-adde-45050f33170a
ms.openlocfilehash: 0faf4d77b1ea2881ba8e029d544f2e42cf552349
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70989684"
---
# <a name="how-to-create-a-flowchart-workflow"></a>방법: 순서도 워크플로 만들기
기본 제공 활동뿐 아니라 사용자 지정 활동에서도 워크플로를 구성할 수 있습니다. 이 항목에서는 <xref:System.Activities.Statements.Flowchart> 활동과 같은 기본 제공 활동 및 이전 [방법의 사용자 지정 활동을 모두 사용 하는 워크플로를 만드는 과정을 단계별로 설명 합니다. 작업](how-to-create-an-activity.md) 항목을 만듭니다. 이 워크플로는 숫자 추측 게임을 모델링합니다.  
  
> [!NOTE]
> 초보자를 위한 자습서의 각 항목은 이전 항목을 바탕으로 합니다. 이 항목을 완료 하려면 먼저 다음을 수행 [해야 합니다. 활동](how-to-create-an-activity.md)을 만듭니다.  
  
> [!NOTE]
> 자습서의 전체 버전을 다운로드하려면 [Windows Workflow Foundation(WF45) - 초보자를 위한 자습서](https://go.microsoft.com/fwlink/?LinkID=248976)를 참조하세요.  
  
### <a name="to-create-the-workflow"></a>워크플로를 만들려면  
  
1. **솔루션 탐색기** 에서 **NumberGuessWorkflowActivities** 을 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 항목**을 차례로 선택 합니다.  
  
2. **설치 됨**, **공통 항목** 노드에서 **워크플로**를 선택 합니다. **워크플로** 목록에서 **작업** 을 선택 합니다.  
  
3. 이름 `FlowchartNumberGuessWorkflow` 상자에 를 입력 하 고 **추가**를 클릭 합니다.  
  
4. **도구 상자** 의 **순서도** 섹션에서 **순서도** 활동을 끌어 워크플로 디자인 화면의 **여기에 작업 놓기** 레이블에 놓습니다.  
  
### <a name="to-create-the-workflow-variables-and-arguments"></a>워크플로 변수와 인수를 만들려면  
  
1. **솔루션 탐색기** 에서 **flowchartnumberguessworkflow.xaml** 를 두 번 클릭 하 여 디자이너에 워크플로를 표시 합니다 (아직 표시 되지 않은 경우).  
  
2. 워크플로 디자이너 왼쪽 아래에 있는 **인수** 를 클릭 하 여 **인수** 창을 표시 합니다.  
  
3. **인수 만들기**를 클릭 합니다.  
  
4. 이름 `MaxNumber` 상자에 를 입력 하 고 **방향** 드롭다운 목록 **에서 시작을 선택한 다음** **인수 형식** 드롭다운 목록에서 **Int32** 를 선택 하 고 enter 키를 눌러 인수를 저장 합니다.  
  
5. **인수 만들기**를 클릭 합니다.  
  
6. 새로 `Turns` 추가 된 인수 아래에 있는 이름 상자에를 입력 하 고 방향 드롭다운 목록에서 바깥쪽을 선택한 다음 인수 형식 드롭다운 목록에서 Int32를 선택 하 고 enter 키를 누릅니다. `MaxNumber`  
  
7. 활동 디자이너 왼쪽 아래에 있는 **인수** 를 클릭 하 여 **인수** 창을 닫습니다.  
  
8. 워크플로 디자이너 왼쪽 아래에 있는 **변수** 를 클릭 하 여 **변수** 창을 표시 합니다.  
  
9. **변수 만들기**를 클릭 합니다.  
  
    > [!TIP]
    > **변수 만들기** 상자가 표시 되지 않으면 workflow designer 화면에서 <xref:System.Activities.Statements.Flowchart> 활동을 클릭 하 여 선택 합니다.  
  
10. 이름 `Guess` 상자에 를 입력 하 고 **변수 형식** 드롭다운 목록에서 **Int32** 를 선택한 다음 enter 키를 눌러 변수를 저장 합니다.  
  
11. **변수 만들기**를 클릭 합니다.  
  
12. 이름 `Target` 상자에 를 입력 하 고 **변수 형식** 드롭다운 목록에서 **Int32** 를 선택한 다음 enter 키를 눌러 변수를 저장 합니다.  
  
13. 활동 디자이너의 왼쪽 아래에 있는 **변수** 를 클릭 하 여 **변수** 창을 닫습니다.  
  
### <a name="to-add-the-workflow-activities"></a>워크플로 활동을 추가하려면  
  
1. **도구 상자** 의 **기본 형식** 섹션에서 **Assign** 활동을 끌어 순서도의 맨 위에 있는 **시작** 노드 위로 가져갑니다. **Assign** 활동이 **시작** 노드 위에 있으면 3 개의 삼각형이 **시작** 노드 주위에 표시 됩니다. **시작** 노드 바로 아래에 있는 삼각형에서 **Assign** 활동을 삭제 합니다. 이렇게 하면 두 항목을 함께 연결 하 고 **할당** 작업을 순서도의 첫 번째 작업으로 지정 합니다.  
  
    > [!NOTE]
    > 시작 노드에 활동을 직접 연결하여 워크플로에서 해당 활동을 시작 활동으로 나타낼 수도 있습니다. 이렇게 하려면 마우스를 **시작** 노드 위로 가져가서 마우스가 **시작** 노드 위에 있을 때 나타나는 사각형 중 하나를 클릭 하 고 연결 하는 줄을 원하는 활동으로 끌어 표시 되는 사각형 중 하나에 놓습니다. 활동을 마우스 오른쪽 단추로 클릭 하 고 **시작 노드로 설정**을 선택 하 여 활동을 시작 활동으로 지정할 수도 있습니다.  
  
2. To `Target` 상자에 **를** 입력 하 고  **C# 식 입력** 또는 **VB 식 입력** 상자에 다음 식을 입력 합니다.  
  
    ```vb  
    New System.Random().Next(1, MaxNumber + 1)  
    ```  
  
    ```csharp  
    new System.Random().Next(1, MaxNumber + 1)  
    ```  
  
    > [!TIP]
    > **도구 상자** 창이 표시 되지 않으면 **보기** 메뉴에서 **도구 상자** 를 선택 합니다.  
  
3. **도구 상자**의 **NumberGuessWorkflowActivities** 섹션에서 **prompt** 활동을 끌어 이전 단계의 **assign** 활동 아래에 놓고 **prompt** 활동을 **assign** 활동에 연결 합니다. 두 활동을 연결하는 방법에는 세 가지가 있습니다. 첫 번째 방법은 워크플로에 **프롬프트** 활동을 놓을 때 연결 하는 것입니다. **프롬프트** 활동을 워크플로로 끌어 오면 **assign** 활동 위로 마우스를 가져간 다음 **assign** 활동을 통해 **프롬프트** 활동이 있을 때 표시 되는 네 개의 삼각형 중 하나에 놓습니다. 두 번째 방법은 **프롬프트** 활동을 원하는 위치에 워크플로로 놓는 것입니다. 그런 다음 **Assign** 활동 위로 마우스를 이동 하 고 표시 되는 사각형 중 하나를 **Prompt** 활동으로 끕니다. **Assign** 활동의 연결 선이 **Prompt** 활동의 사각형 중 하나에 연결 되도록 마우스를 끌고 마우스 단추를 놓습니다. 세 번째 방법은 첫 번째 방법과 매우 유사 합니다. 단, **도구 상자**에서 **프롬프트** 활동을 끄는 대신 워크플로 디자인 화면의 해당 위치에서 끌어서 **Assign** 활동 위로 마우스를 가져간 다음 중 하나에 놓습니다. 표시 되는 삼각형입니다.  
  
4. **Prompt** 활동의 **속성 창** 에서 **BookmarkName** 속성 값 상자 `"EnterGuess"` 에 따옴표를 포함 하 여을 입력 합니다. 결과 `Guess` 속성 값 상자에를 입력 하 고 **텍스트** 속성 상자에 다음 식을 입력 합니다.  
  
    ```vb  
    "Please enter a number between 1 and " & MaxNumber  
    ```  
  
    ```csharp  
    "Please enter a number between 1 and " + MaxNumber  
    ```  
  
    > [!TIP]
    > **속성 창이** 표시 되지 않으면 **보기** 메뉴에서 **속성 창** 을 선택 합니다.  
  
5. **도구 상자** 의 **기본 형식** 섹션에서 **Assign** 활동을 끌어 **Prompt** 활동 아래에 오도록 이전 단계에서 설명한 방법 중 하나를 사용 하 여 연결 합니다.  
  
6. To `Turns` 상자에 **를** 입력 하 `Turns + 1` 고  **C# 식 입력** 또는 **VB 식 입력** 상자에 입력 합니다.  
  
7. **도구 상자** 의 **순서도** 섹션에서 **Flowdecision 결정** 을 끌어 **Assign** 활동 아래에 연결 합니다. **속성 창의** **Condition** 속성 값 상자에 다음 식을 입력 합니다.  
  
    ```vb  
    Guess = Target  
    ```  
  
    ```csharp  
    Guess == Target  
    ```  
  
8. **도구 상자** 에서 다른 **flowdecision 결정** 활동을 끌어 첫 번째 활동 아래에 놓습니다. 위쪽 **Flowdecision 결정** 활동에서 **False** 로 레이블이 지정 된 사각형에서 두 번째 **flowdecision 결정** 활동의 맨 위에 있는 사각형으로 끌어 두 활동을 연결 합니다.  
  
    > [!TIP]
    > **Flowdecision 결정**에 **True** 및 **False** 레이블이 표시 되지 않으면 **flowdecision 결정**위로 마우스를 가져갑니다.  
  
9. 두 번째 **Flowdecision 결정** 활동을 클릭 하 여 선택 합니다. **속성 창의** **Condition** 속성 값 상자에 다음 식을 입력 합니다.  
  
    ```text
    Guess < Target
    ```  
  
10. **도구 상자** 의 **기본 형식** 섹션에서 두 **WriteLine** 활동을 끌어 두 **flowdecision 결정** 활동 아래에 나란히 놓습니다. 최하위 **Flowdecision 결정** 활동의 **진정한** 동작을 가장 왼쪽의 **writeline** 활동에 연결 하 고 **False** 동작을 가장 오른쪽의 **writeline** 활동에 연결 합니다.  
  
11. 가장 왼쪽의 **WriteLine** 활동을 클릭 하 여 선택 하 고 **속성 창의** **텍스트** 속성 값 상자에 다음 식을 입력 합니다.  
  
    ```text
    "Your guess is too low."  
    ```  
  
12. **WriteLine** 을 위에 있는 **프롬프트** 활동의 왼쪽에 연결 합니다.  
  
13. 가장 오른쪽의 **WriteLine** 활동을 클릭 하 여 선택 하 고 **속성 창의** **텍스트** 속성 값 상자에 다음 식을 입력 합니다.  
  
    ```text
    "Your guess is too high."  
    ```  
  
14. 위의 **Prompt** 활동 오른쪽에 **WriteLine** 활동을 연결 합니다.  
  
     다음 예제에서는 완료된 워크플로를 보여 줍니다.  
  
     ![완료 된 Windows Workflow Foundation 순서도를 표시 하는 다이어그램입니다.](./media/how-to-create-a-flowchart-workflow/completed-windows-workflow-flowchart.png)  
  
### <a name="to-build-the-workflow"></a>워크플로를 빌드하려면  
  
1. Ctrl+Shift+B를 눌러 솔루션을 빌드합니다.  
  
     워크플로를 실행 하는 방법에 대 한 지침은 다음 항목 [을 참조 하세요. 워크플로](how-to-run-a-workflow.md)를 실행 합니다. 이미 완료 [한 경우: 워크플로의 다른 스타일](how-to-run-a-workflow.md) 을 사용 하 여 워크플로 단계를 실행 하 고이 단계에서 순서도 워크플로를 사용 하 여 실행 하려면 [방법: [응용 프로그램을 빌드하고 실행](how-to-run-a-workflow.md#BKMK_ToRunTheApplication) 하는 방법에 대 한 다음 섹션으로 건너뜁니다. 워크플로](how-to-run-a-workflow.md)를 실행 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Activities.Statements.Flowchart>
- <xref:System.Activities.Statements.FlowDecision>
- [Windows Workflow Foundation 프로그래밍](programming.md)
- [워크플로 디자인](designing-workflows.md)
- [초보자를 위한 자습서](getting-started-tutorial.md)
- [방법: 활동 만들기](how-to-create-an-activity.md)
- [방법: 워크플로 실행](how-to-run-a-workflow.md)
