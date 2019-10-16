---
title: '작업 2: 워크플로 디자이너 호스트'
ms.date: 03/30/2017
ms.assetid: 0a29b138-270d-4846-b78e-2b875e34e501
ms.openlocfilehash: 15657ad79632812d3802e4da22b9ef297d08f932
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72180256"
---
# <a name="task-2-host-the-workflow-designer"></a>작업 2: 워크플로 디자이너 호스트

이 항목에서는 Windows Presentation Foundation (WPF) 응용 프로그램에서 [!INCLUDE[wfd1](../../../includes/wfd1-md.md)]의 인스턴스를 호스트 하는 절차에 대해 설명 합니다.

프로시저는 디자이너가 포함 된 **Grid** 컨트롤을 구성 하 고, 기본 @no__t 작업을 포함 하는 <xref:System.Activities.Presentation.WorkflowDesigner>의 인스턴스를 프로그래밍 방식으로 만들고, 디자이너 메타 데이터를 등록 하 여 모든 기본 제공에 대 한 디자이너 지원을 제공 합니다. 작업 및는 WPF 응용 프로그램의 [!INCLUDE[wfd2](../../../includes/wfd2-md.md)]을 호스팅합니다.

## <a name="to-host-the-workflow-designer"></a>워크플로 디자이너를 호스트하려면

1. @No__t-0Task 1에서 만든 HostingApplication 프로젝트를 엽니다. 새 Windows Presentation Foundation 응용 프로그램 @ no__t-0을 만듭니다.

2. [!INCLUDE[wfd2](../../../includes/wfd2-md.md)]를 쉽게 사용할 수 있도록 창의 크기를 조정합니다. 이렇게 하려면 디자이너에서 **mainwindow.xaml** 를 선택 하 고 F4 키를 눌러 **속성** 창을 표시 한 후 **레이아웃** 섹션에서 **너비** 를 600로 설정 하 고 **높이** 를 350 값으로 설정 합니다.

3. 디자이너에서 **그리드** 패널을 선택 하 고 ( **mainwindow.xaml**안쪽 상자 클릭) **속성** 창 맨 위에 있는 **name** 속성을 "grid1"로 설정 하 여 그리드 이름을 설정 합니다.

4. **속성** 창에서 `ColumnDefinitions` 속성 옆에 있는 줄임표 ( **...** )를 클릭 하 여 **컬렉션 편집기** 대화 상자를 엽니다.

5. **컬렉션 편집기** 대화 상자에서 **추가** 단추를 세 번 클릭 하 여 레이아웃에 세 개의 열을 삽입 합니다. 첫 번째 열에는 **도구 상자가**포함 되 고 두 번째 열은 [!INCLUDE[wfd2](../../../includes/wfd2-md.md)]을 호스팅하고, 세 번째 열은 속성 검사자에 사용 됩니다.

6. 가운데 열의 `Width` 속성을 값 "4 *"로 설정 합니다.

7. **확인** 을 클릭하여 변경 내용을 저장합니다. 다음 XAML이 *mainwindow.xaml* 파일에 추가 됩니다.

    ```xaml
    <Grid Name="grid1">
        <Grid.ColumnDefinitions>
            <ColumnDefinition />
            <ColumnDefinition Width="4*" />
            <ColumnDefinition />
        </Grid.ColumnDefinitions>
    </Grid>
    ```

8. **솔루션 탐색기**에서 *mainwindow.xaml* 를 마우스 오른쪽 단추로 클릭 하 고 **코드 보기**를 선택 합니다. 다음 단계에 따라 코드를 수정합니다.

    1. 다음 네임스페이스를 추가합니다.

        ```csharp
        using System.Activities;
        using System.Activities.Core.Presentation;
        using System.Activities.Presentation;
        using System.Activities.Presentation.Metadata;
        using System.Activities.Presentation.Toolbox;
        using System.Activities.Statements;
        using System.ComponentModel;
        ```

    2. @No__t 인스턴스를 포함 하도록 전용 멤버 필드를 선언 하려면 `MainWindow` 클래스에 다음 코드를 추가 합니다.

        ```csharp
        public partial class MainWindow : Window
        {
            private WorkflowDesigner wd;

            public MainWindow()
            {
                InitializeComponent();
            }
        }
        ```

    3. 다음 `AddDesigner` 메서드를 `MainWindow` 클래스에 추가합니다. 구현은 <xref:System.Activities.Presentation.WorkflowDesigner>의 인스턴스를 만들고, @no__t 1 활동을 추가 하 고, grid1 **Grid**의 중간 열에 배치 합니다.

        ```csharp
        private void AddDesigner()
        {
            // Create an instance of WorkflowDesigner class.
            this.wd = new WorkflowDesigner();

            // Place the designer canvas in the middle column of the grid.
            Grid.SetColumn(this.wd.View, 1);

            // Load a new Sequence as default.
            this.wd.Load(new Sequence());

            // Add the designer canvas to the grid.
            grid1.Children.Add(this.wd.View);
        }
        ```

    4. 디자이너 메타데이터를 등록하여 모든 기본 제공 활동에 대한 디자이너 지원을 추가합니다. 그러면 도구 상자의 활동을 <xref:System.Activities.Statements.Sequence>의 원래 [!INCLUDE[wfd2](../../../includes/wfd2-md.md)] 활동으로 끌어 놓을 수 있습니다. 이렇게 하려면 `RegisterMetadata` 메서드를 `MainWindow` 클래스에 추가 합니다.

        ```csharp
        private void RegisterMetadata()
        {
            var dm = new DesignerMetadata();
            dm.Register();
        }
        ```

        활동 디자이너를 등록 하는 방법에 대 한 자세한 내용은 [How to: 사용자 지정 활동 디자이너 @ no__t-0을 만듭니다.

    5. `MainWindow` 클래스 생성자에서 앞에서 선언한 메서드에 호출을 추가하여 디자이너 지원을 위한 메타데이터를 등록하고 <xref:System.Activities.Presentation.WorkflowDesigner>를 만듭니다.

        ```csharp
        public MainWindow()
        {
            InitializeComponent();

            // Register the metadata.
            RegisterMetadata();

            // Add the WFF Designer.
            AddDesigner();
        }
        ```

        > [!NOTE]
        > `RegisterMetadata` 메서드는 <xref:System.Activities.Statements.Sequence> 활동을 포함한 기본 제공 활동의 디자이너 메타데이터를 등록합니다. `AddDesigner` 메서드는 <xref:System.Activities.Statements.Sequence> 활동을 사용하기 때문에 `RegisterMetadata` 메서드를 먼저 호출해야 합니다.

9. <kbd>F5</kbd> 키를 눌러 솔루션을 빌드하고 실행 합니다.

10. @No__t-0Task 3: 도구 상자 및 PropertyGrid Panes @ no__t-0을 만들어 다시 호스트 된 워크플로 디자이너에 **도구 상자** 및 **PropertyGrid** 지원을 추가 하는 방법을 알아봅니다.

## <a name="see-also"></a>참조

- [워크플로 디자이너 재호스트](rehosting-the-workflow-designer.md)
- [ 작업 1: 새 Windows Presentation Foundation 응용 프로그램 만들기 @ no__t-0
- [Task 작업 3: 도구 상자 및 PropertyGrid 창 만들기 @ no__t-0
