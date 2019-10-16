---
title: '자습서: Visual Studio 2019에서 첫 번째 WPF 응용 프로그램 만들기-.NET Framework'
ms.date: 09/06/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- getting started [WPF], WPF
- WPF [WPF], getting started
ms.assetid: b96bed40-8946-4285-8fe4-88045ab854ed
ms.topic: tutorial
ms.custom: vs-dotnet
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b2c8e36c1b8185f28a7ec20402e385f3a1ddf5ce
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991764"
---
# <a name="tutorial-create-your-first-wpf-application-in-visual-studio-2019"></a>자습서: Visual Studio 2019에서 첫 WPF 응용 프로그램 만들기

이 문서에서는 대부분의 WPF 응용 프로그램에 공통 된 요소를 포함 하는 Windows Presentation Foundation (WPF) 데스크톱 응용 프로그램을 개발 하는 방법을 보여 줍니다. XAML (Extensible Application Markup Language) 태그, 코드 숨김으로, 응용 프로그램 정의, 컨트롤, 레이아웃, 데이터 바인딩 및 스타일을 정의 합니다. 응용 프로그램을 개발 하려면 Visual Studio를 사용 합니다. 

이 자습서에서는 다음 작업을 수행하는 방법을 알아봅니다.
> [!div class="checklist"]
>
> - WPF 프로젝트를 만듭니다.
> - XAML을 사용 하 여 응용 프로그램 UI (사용자 인터페이스)의 모양을 디자인 합니다.
> - 응용 프로그램의 동작을 빌드하는 코드를 작성 합니다.
> - 응용 프로그램을 관리 하는 응용 프로그램 정의를 만듭니다.
> - 응용 프로그램 UI를 구성 하는 컨트롤을 추가 하 고 레이아웃을 만듭니다.
> - 응용 프로그램 UI 전체에 일관 된 모양의 스타일을 만듭니다.
> - Ui를 데이터에 바인딩하여 데이터에서 UI를 채우고 데이터와 UI를 동기화 된 상태로 유지 합니다.

이 자습서의 끝 부분에서는 사용자가 선택한 사용자에 대 한 경비 보고서를 볼 수 있도록 하는 독립 실행형 Windows 응용 프로그램을 빌드 했습니다. 응용 프로그램은 브라우저 스타일 창에서 호스팅되는 여러 WPF 페이지로 구성 됩니다.

> [!TIP]
> 이 자습서에서 사용 되는 샘플 코드는 Visual Basic 및 C# [자습서 WPF 앱 샘플 코드](https://github.com/Microsoft/WPF-Samples/tree/master/Getting%20Started/WalkthroughFirstWPFApp)에 모두 사용할 수 있습니다.
>
> 이 페이지 맨 위에 있는 언어 선택기를 사용 하 여 C# 및 Visual Basic 사이에 샘플 코드의 코드 언어를 전환할 수 있습니다.

## <a name="prerequisites"></a>전제 조건

- **.Net 데스크톱 개발** 워크 로드가 설치 된 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) .

   최신 버전의 Visual Studio를 설치 하는 방법에 대 한 자세한 내용은 [Visual Studio 설치](/visualstudio/install/install-visual-studio)를 참조 하세요.

## <a name="create-the-application-project"></a>응용 프로그램 프로젝트 만들기

첫 번째 단계는 응용 프로그램 정의, 페이지 2 개 및 이미지를 포함 하는 응용 프로그램 인프라를 만드는 것입니다.

1. Visual Basic 또는 시각적 개체 C# **`ExpenseIt`** 에서 새 WPF 응용 프로그램 프로젝트를 만듭니다.

   1. Visual Studio를 열고 **시작** 메뉴에서 **새 프로젝트 만들기** 를 선택 합니다.

      **새 프로젝트 만들기** 대화 상자가 열립니다.

   2. **언어** 드롭다운에서 **C#** 또는 **Visual Basic**를 선택 합니다.
      
   3. **WPF 앱 (.NET Framework)** 템플릿을 선택 하 고 **다음**을 선택 합니다. 
     
      ![새 프로젝트 만들기 대화 상자](./media/walkthrough-my-first-wpf-desktop-application/create-new-project-dialog.png)
    
      **새 프로젝트 구성** 대화 상자가 열립니다.

   4. 프로젝트 이름을 **`ExpenseIt`** 입력 하 고 **만들기**를 선택 합니다.

      ![새 프로젝트 구성 대화 상자](./media/walkthrough-my-first-wpf-desktop-application/configure-new-project-dialog.png)

      Visual Studio에서 프로젝트를 만들고 **mainwindow.xaml**이라는 기본 응용 프로그램 창에 대 한 디자이너를 엽니다.

2. *응용 프로그램 .xaml* (Visual Basic *) 또는 app.xaml* (C#)을 엽니다.

    이 XAML 파일은 WPF 응용 프로그램 및 모든 응용 프로그램 리소스를 정의 합니다. 또한이 파일을 사용 하 여 UI를 지정 합니다 .이 경우에는 응용 프로그램이 시작 될 때 자동으로 표시 되는 UI (이 경우 *mainwindow.xaml*)를 지정 합니다.

    XAML은 Visual Basic에서 다음과 같이 표시 됩니다.

    [!code-xaml[ExpenseIt#1_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/Application.xaml#1_a)]

    그리고에서 C#다음과 같이 합니다.

    [!code-xaml[ExpenseIt#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/App.xaml#1)]

3. *Mainwindow.xaml*를 엽니다.

    이 XAML 파일은 응용 프로그램의 주 창이 며 페이지에서 만든 콘텐츠를 표시 합니다. 클래스 <xref:System.Windows.Window> 는 창 속성 (예: 제목, 크기 또는 아이콘)을 정의 하 고 닫기 또는 숨기기와 같은 이벤트를 처리 합니다.

4. 다음 XAML과 같이 <xref:System.Windows.Navigation.NavigationWindow> 요소를로변경합니다.<xref:System.Windows.Window>

   ```xaml
   <NavigationWindow x:Class="ExpenseIt.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        ...
   </NavigationWindow>
   ```

   이 앱은 사용자 입력에 따라 다른 콘텐츠를 탐색 합니다. 이렇게 하면 main <xref:System.Windows.Window> 을 <xref:System.Windows.Navigation.NavigationWindow>로 변경 해야 합니다. <xref:System.Windows.Navigation.NavigationWindow>의 <xref:System.Windows.Window>모든 속성을 상속 합니다. XAML <xref:System.Windows.Navigation.NavigationWindow> 파일의 요소는 <xref:System.Windows.Navigation.NavigationWindow> 클래스의 인스턴스를 만듭니다. 자세한 내용은 [탐색 개요](../app-development/navigation-overview.md)를 참조 하세요.

5. 태그 사이에서 요소를 <xref:System.Windows.Controls.Grid> 제거 합니다. <xref:System.Windows.Navigation.NavigationWindow>

6. <xref:System.Windows.Navigation.NavigationWindow> 요소에 대 한 XAML 코드에서 다음 속성을 변경 합니다.

    - 속성을 "`ExpenseIt`"로 설정 합니다. <xref:System.Windows.Window.Title%2A>

    - <xref:System.Windows.FrameworkElement.Height%2A> 속성을 350 픽셀로 설정 합니다.

    - <xref:System.Windows.FrameworkElement.Width%2A> 속성을 500 픽셀로 설정 합니다.

    XAML은 Visual Basic에 대해 다음과 같이 표시 되어야 합니다.

    [!code-xaml[ExpenseIt#2_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt/MainWindow.xaml#2_a)]

    그리고 다음과 같이 합니다 C#.

    [!code-xaml[ExpenseIt#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/MainWindow.xaml#2)]

7. *Mainwindow.xaml* 또는 *MainWindow.xaml.cs*를 엽니다.

    이 파일은 *mainwindow.xaml*에 선언 된 이벤트를 처리 하는 코드를 포함 하는 코드를 포함 하는 파일입니다. 이 파일에는 XAML에 정의된 창의 부분 클래스가 포함되어 있습니다.

8. 를 사용 C#하는 `MainWindow` 경우에서 <xref:System.Windows.Navigation.NavigationWindow>파생 되도록 클래스를 변경 합니다. Visual Basic XAML에서 창을 변경할 때 자동으로 발생 합니다. 이제 C# 코드는 다음과 같습니다.

   [!code-csharp[ExpenseIt#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/MainWindow.xaml.cs?highlight=21)]

## <a name="add-files-to-the-application"></a>응용 프로그램에 파일 추가

이 섹션에서는 애플리케이션에 두 페이지와 이미지를 추가합니다.

1. 프로젝트에 새 페이지를 추가 하 고 이름을 *`ExpenseItHome.xaml`* 로 추가 합니다.

   1. **솔루션 탐색기** **`ExpenseIt`** 에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 **추가** > **페이지**를 선택 합니다.

   1. **새 항목 추가** 대화 상자에서 **페이지 (WPF)** 템플릿이 이미 선택 되어 있습니다. 이름을 **`ExpenseItHome`** 입력 하 고 **추가**를 선택 합니다.

    이 페이지는 응용 프로그램이 시작 될 때 표시 되는 첫 번째 페이지입니다. 에 대 한 경비 보고서를 표시 하기 위해 선택할 사용자의 목록이 표시 됩니다.

1. 를 *`ExpenseItHome.xaml`* 엽니다.

1. <xref:System.Windows.Controls.Page.Title%2A> 을"`ExpenseIt - Home`"로 설정 합니다.

1. 를 350 픽셀로 설정 하 `DesignWidth` 고을 500 픽셀로 설정 합니다. `DesignHeight`

    이제 XAML이 Visual Basic에 대해 다음과 같이 표시 됩니다.

    [!code-xaml[ExpenseIt#6_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseItHome.xaml#6_a)]

    그리고 다음과 같이 합니다 C#.

    [!code-xaml[ExpenseIt#6](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt2/ExpenseItHome.xaml#6)]

1. *Mainwindow.xaml*를 엽니다.

1. 요소에 속성을 <xref:System.Windows.Navigation.NavigationWindow.Source%2A> 추가 하 고 "`ExpenseItHome.xaml`"로 설정 합니다. <xref:System.Windows.Navigation.NavigationWindow>

    이는 *`ExpenseItHome.xaml`* 응용 프로그램이 시작 될 때 열리는 첫 페이지로 설정 됩니다. 

    Visual Basic의 XAML 예제는 다음과 같습니다.

    [!code-xaml[ExpenseIt#7_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/MainWindow.xaml#7_a)]

    및 C#:

    [!code-xaml[ExpenseIt#7](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt2/MainWindow.xaml#7)]

   > [!TIP]
   > **속성** 창의 **기타** 범주에서 **원본** 속성을 설정할 수도 있습니다.
   >
   > ![속성 창의 원본 속성](./media/properties-source.png)

1. 프로젝트에 다른 새 WPF 페이지를 추가 하 고 이름을 *expensereportpage.xaml*::

   1. **솔루션 탐색기** **`ExpenseIt`** 에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 **추가** > **페이지**를 선택 합니다.

   1. **새 항목 추가** 대화 상자에서 **페이지 (WPF)** 템플릿을 선택 합니다. **Expensereportpage.xaml**이름을 입력 한 다음 **추가**를 선택 합니다.

    이 페이지에서는 **`ExpenseItHome`** 페이지에서 선택한 사용자에 대 한 경비 보고서를 표시 합니다.

1. *ExpenseReportPage.xaml*을 엽니다.

1. <xref:System.Windows.Controls.Page.Title%2A> 을"`ExpenseIt - View Expense`"로 설정 합니다.

1. 를 350 픽셀로 설정 하 `DesignWidth` 고을 500 픽셀로 설정 합니다. `DesignHeight` 

    *Expensereportpage.xaml* 는 Visual Basic에서 다음과 같이 표시 됩니다.

    [!code-xaml[ExpenseIt#4_A](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseReportPage.xaml#4_a)]

    그리고에서 C#다음과 같이 합니다.

    [!code-xaml[ExpenseIt#4](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/ExpenseReportPage.xaml#4)]

1. *Expenseithome.xaml* 및 *expensereportpage.xaml*, *ExpenseItHome.xaml.cs* 및 *ExpenseReportPage.xaml.cs*를 엽니다.

    새 페이지 파일을 만드는 경우 Visual Studio에서 자동으로 해당 *코드 숨김으로* 파일을 만듭니다. 이러한 코드 숨김 파일은 사용자 입력에 응답하기 위한 논리를 처리합니다.

    코드는 **`ExpenseItHome`** 다음과 같습니다.

    [!code-csharp[ExpenseIt#2_5](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt2/ExpenseItHome.xaml.cs#2_5)]

    [!code-vb[ExpenseIt#2_5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseItHome.xaml.vb#2_5)]

    **Expensereportpage.xaml**에 대해 다음과 같이 합니다.

    [!code-csharp[ExpenseIt#5](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/ExpenseReportPage.xaml.cs#5)]

    [!code-vb[ExpenseIt#5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseReportPage.xaml.vb#5)]

1. *워터 마크 .png* 라는 이미지를 프로젝트에 추가 합니다. 사용자 고유의 이미지를 만들거나 샘플 코드에서 파일을 복사 하거나 [microsoft/WPF 샘플](https://raw.githubusercontent.com/microsoft/WPF-Samples/master/Getting%20Started/WalkthroughFirstWPFApp/csharp/watermark.png) GitHub 리포지토리에서 가져올 수 있습니다.

    1. 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고**기존 항목** **추가** > 를 선택 하거나 **Shift**+**Alt**+**A**를 누릅니다.

    2. **기존 항목 추가** 대화 상자에서 파일 필터를 **모든 파일** 또는 **이미지 파일**로 설정 하 고 사용 하려는 이미지 파일을 찾은 다음 **추가**를 선택 합니다.

## <a name="build-and-run-the-application"></a>응용 프로그램 빌드 및 실행

1. 응용 프로그램을 빌드하고 실행 하려면 **F5** 키를 누르거나 **디버그** 메뉴에서 **디버깅 시작** 을 선택 합니다.

    다음 그림에서는 <xref:System.Windows.Navigation.NavigationWindow> 단추가 있는 응용 프로그램을 보여 줍니다.

    ![응용 프로그램을 빌드하고 실행 한 후](./media/walkthrough-my-first-wpf-desktop-application/build-run-application.png)

2. Visual Studio로 돌아가려면 응용 프로그램을 닫습니다.

## <a name="create-the-layout"></a>레이아웃 만들기

레이아웃은 UI 요소를 배치 하는 순서가 지정 된 방법을 제공 하며 UI 크기를 조정할 때 해당 요소의 크기와 위치도 관리 합니다. 일반적으로 다음 레이아웃 컨트롤 중 하나를 사용하여 레이아웃을 만듭니다.

- <xref:System.Windows.Controls.Canvas>-캔버스 영역에 상대적인 좌표를 사용 하 여 자식 요소의 위치를 명시적으로 지정할 수 있는 영역을 정의 합니다.
- <xref:System.Windows.Controls.DockPanel>-자식 요소를 서로 상대적인 가로 또는 세로로 정렬할 수 있는 영역을 정의 합니다.
- <xref:System.Windows.Controls.Grid>-열과 행으로 구성 되는 유연한 그리드 영역을 정의 합니다.
- <xref:System.Windows.Controls.StackPanel>-가로 또는 세로 방향으로 사용할 수 있는 한 줄로 자식 요소를 정렬 합니다.
- <xref:System.Windows.Controls.VirtualizingStackPanel>-가로 또는 세로 방향으로 한 줄로 콘텐츠를 정렬 하 고 가상화 합니다.
- <xref:System.Windows.Controls.WrapPanel>-콘텐츠를 포함 하는 상자의 가장자리에 있는 다음 줄로 줄 바꿈 하는 왼쪽에서 오른쪽으로 자식 요소를 배치 합니다. 이후 정렬은 방향 속성의 값에 따라 위쪽에서 아래쪽으로 또는 오른쪽에서 왼쪽으로 순차적으로 발생 합니다.

이러한 각 레이아웃 컨트롤은 자식 요소에 대해 특정 형식의 레이아웃을 지원 합니다. `ExpenseIt`페이지 크기를 조정할 수 있으며, 각 페이지에는 다른 요소와 함께 가로 및 세로 방향으로 정렬 되는 요소가 있습니다. 이 예제에서는 <xref:System.Windows.Controls.Grid> 응용 프로그램에 대 한 레이아웃 요소로 사용 됩니다.

> [!TIP]
> 요소에 대 한 <xref:System.Windows.Controls.Panel> 자세한 내용은 [패널 개요](../controls/panels-overview.md)를 참조 하세요. 레이아웃에 대 한 자세한 내용은 [레이아웃](../advanced/layout.md)을 참조 하세요.

이 섹션에서는 <xref:System.Windows.Controls.Grid> 의 *`ExpenseItHome.xaml`* 에 열 및 행 정의를 추가 하 여 세 개의 행과 10 픽셀 여백으로 단일 열 테이블을 만듭니다.

1. 에서 *`ExpenseItHome.xaml`* 요소의<xref:System.Windows.Controls.Grid> 속성을 <xref:System.Windows.FrameworkElement.Margin%2A> 왼쪽, 위쪽, 오른쪽 및 아래쪽 여백에 해당 하는 "10, 0, 10, 10"으로 설정 합니다.

   ```xaml
   <Grid Margin="10,0,10,10">
   ```

   > [!TIP]
   > **속성** 창의 **레이아웃** 범주에서 **여백** 값을 설정할 수도 있습니다.
   >
   > ![속성 창 여백 값](./media/properties-margin.png)

2. <xref:System.Windows.Controls.Grid> 태그 사이에 다음 XAML을 추가 하 여 행 및 열 정의를 만듭니다.

    [!code-xaml[ExpenseIt#8](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt3/ExpenseItHome.xaml#8)]

    두 <xref:System.Windows.Controls.RowDefinition.Height%2A> 행의는로 <xref:System.Windows.GridLength.Auto%2A>설정 됩니다. 즉, 행의 내용에 따라 행의 크기가 조정 됩니다. 기본값 <xref:System.Windows.Controls.RowDefinition.Height%2A> 은 크기 <xref:System.Windows.GridUnitType.Star> 조정입니다. 즉, 행 높이가 사용 가능한 공간의 가중치가 적용 된 비율입니다. 예를 들어 각 <xref:System.Windows.Controls.RowDefinition.Height%2A> 행에 "*"가 있는 경우 각각은 사용 가능한 공간의 절반 인 높이가 있습니다.

    이제 <xref:System.Windows.Controls.Grid> 에 다음 XAML이 포함 됩니다.

    [!code-xaml[ExpenseIt#9](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt3/ExpenseItHome.xaml#9)]

## <a name="add-controls"></a>컨트롤 추가

이 섹션에서는 홈 페이지 UI를 업데이트 하 여 경비 보고서를 표시 하는 사람을 선택할 수 있는 사람 목록을 표시 합니다. 컨트롤은 사용자가 애플리케이션과 상호 작용할 수 있게 하는 UI 개체입니다. 자세한 내용은 [컨트롤](../controls/index.md)을 참조하세요.

이 UI를 만들려면 다음 요소를에 *`ExpenseItHome.xaml`* 추가 합니다.

- <xref:System.Windows.Controls.ListBox> 사용자의 목록에 대 한입니다.
- <xref:System.Windows.Controls.Label> 목록 헤더의입니다.
- <xref:System.Windows.Controls.Button> 목록에서 선택한 사용자에 대 한 경비 보고서를 보려면 클릭 합니다.

각 컨트롤은 연결 된 속성을 <xref:System.Windows.Controls.Grid> <xref:System.Windows.Controls.Grid.Row%2A?displayProperty=nameWithType> 설정 하 여의 행에 배치 됩니다. 연결 된 속성에 대 한 자세한 내용은 [연결 된 속성 개요](../advanced/attached-properties-overview.md)를 참조 하세요.

1. 에서 *`ExpenseItHome.xaml`* 태그<xref:System.Windows.Controls.Grid> 사이에 다음 XAML을 추가 합니다.

   [!code-xaml[ExpenseIt#10](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt4/ExpenseItHome.xaml#10)]

   > [!TIP]
   > **도구 상자** 창에서 디자인 창으로 끌어 오고 **속성** 창에서 속성을 설정 하 여 컨트롤을 만들 수도 있습니다.

2. 응용 프로그램을 빌드 및 실행합니다.

    다음 그림에서는 사용자가 만든 컨트롤을 보여 줍니다.

![이름 목록을 표시 하는 ExpenseIt 샘플 스크린샷](./media/walkthrough-my-first-wpf-desktop-application/add-application-controls.png)

## <a name="add-an-image-and-a-title"></a>이미지 및 제목 추가

이 섹션에서는 이미지와 페이지 제목으로 홈 페이지 UI를 업데이트 합니다.

1. 에서 *`ExpenseItHome.xaml`* <xref:System.Windows.Controls.Grid.ColumnDefinitions%2A> 고정 230<xref:System.Windows.Controls.ColumnDefinition.Width%2A> 픽셀을 사용 하 여에 다른 열을 추가 합니다.

    [!code-xaml[ExpenseIt#11](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseItHome.xaml?highlight=52-55)]

2. 에 다른 행 <xref:System.Windows.Controls.Grid.RowDefinitions%2A>을 추가 하 여 총 4 개 행을 만듭니다.

    [!code-xaml[ExpenseIt#11b](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseItHome.xaml?highlight=57-62)]

3. 세 가지 컨트롤 (테두리, ListBox 및 단추) <xref:System.Windows.Controls.Grid.Column%2A?displayProperty=nameWithType> 각각의 속성을 1로 설정 하 여 컨트롤을 두 번째 열로 이동 합니다.

4. 3 개의 컨트롤 (테두리, ListBox 및 단추 <xref:System.Windows.Controls.Grid.Row%2A?displayProperty=nameWithType> )과 border 요소 각각에 대해 해당 값을 1 씩 증가 하 여 각 컨트롤을 한 행 아래로 이동 합니다.

   이제 세 가지 컨트롤에 대 한 XAML은 다음과 같습니다.

    [!code-xaml[ExpenseIt#12](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#12)]

5. `<Grid>` 태그와 <xref:System.Windows.Controls.Panel.Background%2A?displayProperty=nameWithType> 태그`</Grid>` 사이에 다음 XAML을 추가 하 여 속성을 *워터 마크 .png* 이미지 파일로 설정 합니다.

    [!code-xaml[ExpenseIt#14](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#14)]

6. 요소 앞에 "경비 보고서 <xref:System.Windows.Controls.Label> 보기" 내용이 포함 된를 추가 합니다. <xref:System.Windows.Controls.Border> 이 레이블은 페이지의 제목입니다.

    [!code-xaml[ExpenseIt#13](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#13)]

7. 응용 프로그램을 빌드 및 실행합니다.

다음 그림에서는 방금 추가한 항목의 결과를 보여 줍니다.

![새 이미지 배경과 페이지 제목을 보여 주는 ExpenseIt 샘플 스크린샷](./media/walkthrough-my-first-wpf-desktop-application/add-application-image-title.png)

## <a name="add-code-to-handle-events"></a>이벤트를 처리 하는 코드 추가

1. 에서 *`ExpenseItHome.xaml`* 요소<xref:System.Windows.Controls.Button> 에 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트 처리기를 추가 합니다. 자세한 내용은 [방법: 간단한 이벤트 처리기](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/bb675300(v=vs.100))를 만듭니다.

    [!code-xaml[ExpenseIt#15](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt6/ExpenseItHome.xaml#15)]

2. *`ExpenseItHome.xaml.vb`* *또는`ExpenseItHome.xaml.cs`* 를 엽니다.

3. `ExpenseItHome` 클래스에 다음 코드를 추가 하 여 단추 클릭 이벤트 처리기를 추가 합니다. 이벤트 처리기가 **expensereportpage.xaml** 페이지를 엽니다.

    [!code-csharp[ExpenseIt#16](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt6/ExpenseItHome.xaml.cs#16)]
    [!code-vb[ExpenseIt#16](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt6/ExpenseItHome.xaml.vb#16)]

## <a name="create-the-ui-for-expensereportpage"></a>Expensereportpage.xaml에 대 한 UI 만들기

*Expensereportpage.xaml* 는 **`ExpenseItHome`** 페이지에서 선택한 사용자에 대 한 경비 보고서를 표시 합니다. 이 섹션에서는 **expensereportpage.xaml**에 대 한 UI를 만듭니다. 또한 다양 한 UI 요소에 배경 및 채우기 색을 추가 합니다.

1. *ExpenseReportPage.xaml*을 엽니다.

2. <xref:System.Windows.Controls.Grid> 태그 사이에 다음 XAML을 추가 합니다.

    [!code-xaml[ExpenseIt#17](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt6/ExpenseReportPage.xaml#17)]

    이 UI는와 유사 *`ExpenseItHome.xaml`* <xref:System.Windows.Controls.DataGrid>합니다. 단, 보고서 데이터는에 표시 됩니다.

3. 응용 프로그램을 빌드 및 실행합니다.

4. **보기** 단추를 선택 합니다.

    경비 보고서 페이지가 나타납니다. 또한 뒤로 탐색 단추를 사용할 수 있습니다.

다음 그림에서는 *expensereportpage.xaml*에 추가 된 UI 요소를 보여 줍니다.

![Expensereportpage.xaml에 대해 만든 UI를 보여 주는 ExpenseIt 샘플 스크린샷](./media/walkthrough-my-first-wpf-desktop-application/create-application-ui.png)

## <a name="style-controls"></a>스타일 컨트롤

UI에서 같은 형식의 모든 요소에 대해 다양 한 요소의 모양이 동일 하 게 표시 되는 경우가 많습니다. UI는 [스타일](../controls/styling-and-templating.md) 을 사용 하 여 여러 요소에서 모양을 다시 사용할 수 있도록 합니다. 스타일의 재사용은 XAML 생성 및 관리를 간소화 하는 데 도움이 됩니다. 이 섹션에서는 이전 단계에서 정의된 요소별 특성을 스타일로 바꿉니다.

1. *응용 프로그램 .xaml* *또는 app.xaml을 엽니다*.

2. <xref:System.Windows.Application.Resources%2A?displayProperty=nameWithType> 태그 사이에 다음 XAML을 추가 합니다.

    [!code-xaml[ExpenseIt#18](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt7/App.xaml#18)]

    이 XAML은 다음 스타일을 추가합니다.

    - `headerTextStyle`: 페이지 제목 <xref:System.Windows.Controls.Label>에 서식을 지정 합니다.

    - `labelStyle`: 컨트롤의 <xref:System.Windows.Controls.Label> 형식을 지정 합니다.

    - `columnHeaderStyle`: 의 <xref:System.Windows.Controls.Primitives.DataGridColumnHeader>형식을 지정 합니다.

    - `listHeaderStyle`: 목록 헤더 <xref:System.Windows.Controls.Border> 컨트롤의 형식을 지정 합니다.

    - `listHeaderTextStyle`: 목록 헤더 <xref:System.Windows.Controls.Label>의 형식을 지정 합니다.

    - `buttonStyle`: 의 형식을 지정 <xref:System.Windows.Controls.Button> `ExpenseItHome.xaml`하려면입니다.

    스타일은 <xref:System.Windows.Application.Resources%2A?displayProperty=nameWithType> 속성 요소의 리소스 및 자식입니다. 이 위치에서 스타일은 애플리케이션의 모든 요소에 적용됩니다. .NET 앱에서 리소스를 사용 하는 방법에 대 한 예제는 [응용 프로그램 리소스 사용](../advanced/how-to-use-application-resources.md)을 참조 하세요.

3. 에서 *`ExpenseItHome.xaml`* 요소<xref:System.Windows.Controls.Grid> 사이에 있는 모든 항목을 다음 XAML로 바꿉니다.

    [!code-xaml[ExpenseIt#19](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt7/ExpenseItHome.xaml#19)]

    스타일을 적용하면 각 컨트롤의 모양을 정의하는 <xref:System.Windows.VerticalAlignment> 및 <xref:System.Windows.Media.FontFamily> 와 같은 속성이 제거되고 바뀝니다. 예를 들어는 `headerTextStyle` "경비 보고서 보기" <xref:System.Windows.Controls.Label>에 적용 됩니다.

4. *ExpenseReportPage.xaml*을 엽니다.

5. <xref:System.Windows.Controls.Grid> 요소 사이에 있는 모든 항목을 다음 XAML로 바꿉니다.

    [!code-xaml[ExpenseIt#20](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt7/ExpenseReportPage.xaml#20)]

    이 XAML은 <xref:System.Windows.Controls.Label> 및 <xref:System.Windows.Controls.Border> 요소에 스타일을 추가 합니다.

6. 응용 프로그램을 빌드 및 실행합니다. 창 모양은 이전과 동일 합니다.

    ![마지막 섹션과 동일한 모양의 샘플 스크린샷 ExpenseIt.](./media/walkthrough-my-first-wpf-desktop-application/create-application-ui.png)

7. Visual Studio로 돌아가려면 응용 프로그램을 닫습니다.

## <a name="bind-data-to-a-control"></a>컨트롤에 데이터 바인딩

이 섹션에서는 다양 한 컨트롤에 바인딩되는 XML 데이터를 만듭니다.

1. 에서 *`ExpenseItHome.xaml`* <xref:System.Windows.Data.XmlDataProvider> 열린 <xref:System.Windows.Controls.Grid> 요소 뒤에 다음 XAML을 추가 하 여 각 사용자에 대 한 데이터를 포함 하는를 만듭니다.

    [!code-xaml[ExpenseIt#23](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml?range=13,16-40,49)]

    데이터는 <xref:System.Windows.Controls.Grid> 리소스로 생성 됩니다. 일반적으로이 데이터는 파일로 로드 되지만 편의상 데이터가 인라인으로 추가 됩니다.

2. 요소 내 <xref:System.Windows.Controls.ListBox>에서 요소`<XmlDataProvider>` 뒤에 데이터 `<xref:System.Windows.DataTemplate>` 를 표시 하는 방법을 정의 하는 다음 요소를 추가 합니다. `<Grid.Resources>`

    [!code-xaml[ExpenseIt#24](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml?range=13,43-46,49)]

    데이터 템플릿에 대 한 자세한 내용은 [데이터 템플릿 개요](../data/data-templating-overview.md)를 참조 하세요.

3. 기존 <xref:System.Windows.Controls.ListBox> 를 다음 XAML로 바꿉니다.

    [!code-xaml[ExpenseIt#25](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml#25)]

    이 XAML은 <xref:System.Windows.Controls.ListBox> 의 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 속성을 데이터 소스에 바인딩하고 데이터 템플릿을로 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>적용 합니다.

## <a name="connect-data-to-controls"></a>컨트롤에 데이터 연결

다음으로는 **`ExpenseItHome`** 페이지에서 선택한 이름을 검색 하 고 **expensereportpage.xaml**의 생성자에 전달 하는 코드를 추가 합니다. **Expensereportpage.xaml** 는 *expensereportpage.xaml* 에 정의 된 컨트롤이 바인딩되는 전달 된 항목으로 데이터 컨텍스트를 설정 합니다.

1. *ExpenseReportPage.xaml.vb* 또는 *ExpenseReportPage.xaml.cs*를 엽니다.

2. 선택한 사람의 비용 보고서 데이터를 전달할 수 있도록 개체를 사용하는 생성자를 추가합니다.

    [!code-csharp[ExpenseIt#26](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseReportPage.xaml.cs#26)]
    [!code-vb[ExpenseIt#26](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt8/ExpenseReportPage.xaml.vb#26)]

3. *`ExpenseItHome.xaml.vb`* *또는`ExpenseItHome.xaml.cs`* 를 엽니다.

4. 선택한 사람의 비용 보고서 데이터를 전달 하는 새 생성자를 호출 하도록 이벤트처리기를변경합니다.<xref:System.Windows.Controls.Primitives.ButtonBase.Click>

    [!code-csharp[ExpenseIt#27](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml.cs#27)]
    [!code-vb[ExpenseIt#27](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt8/ExpenseItHome.xaml.vb#27)]

## <a name="style-data-with-data-templates"></a>데이터 템플릿을 사용 하 여 데이터 스타일

이 섹션에서는 데이터 템플릿을 사용 하 여 데이터 바인딩된 목록의 각 항목에 대 한 UI를 업데이트 합니다.

1. *ExpenseReportPage.xaml*을 엽니다.

2. "Name" 및 "학과" <xref:System.Windows.Controls.Label> 요소의 내용을 적절 한 데이터 원본 속성에 바인딩합니다. 데이터 바인딩에 대 한 자세한 내용은 [데이터 바인딩 개요](../data/data-binding-overview.md)를 참조 하세요.

    [!code-xaml[ExpenseIt#31](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseReportPage.xaml#31)]

3. <xref:System.Windows.Controls.Grid> 시작 요소 뒤에 경비 보고서 데이터를 표시 하는 방법을 정의 하는 다음 데이터 템플릿을 추가 합니다.

    [!code-xaml[ExpenseIt#30](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseReportPage.xaml#30)]

4. 요소를 요소<xref:System.Windows.Controls.DataGrid> 아래의 <xref:System.Windows.Controls.DataGridTemplateColumn> 로 바꾸고 템플릿을 적용 합니다. <xref:System.Windows.Controls.DataGridTextColumn>

    [!code-xaml[ExpenseIt#32](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseReportPage.xaml#32)]

5. 애플리케이션을 빌드 및 실행합니다.

6. 사용자를 선택한 다음 **보기** 단추를 선택 합니다.

다음 그림에서는 컨트롤, 레이아웃, 스타일 `ExpenseIt` , 데이터 바인딩 및 데이터 템플릿이 적용 된 응용 프로그램의 두 페이지를 모두 보여 줍니다.

![응용 프로그램의 두 페이지 모두 이름 목록과 경비 보고서를 표시 합니다.](./media/walkthrough-my-first-wpf-desktop-application/application-data-templates.png)

> [!NOTE]
> 이 샘플은 WPF의 특정 기능을 보여 주며 보안, 지역화 및 접근성과 같은 항목에 대 한 모든 모범 사례를 따르지 않습니다. WPF 및 .NET 앱 개발 모범 사례에 대 한 포괄적인 적용 범위는 다음 항목을 참조 하세요.
>
> - [액세스 가능성](../../ui-automation/accessibility-best-practices.md)
> - [보안](../security-wpf.md)
> - [WPF 전역화 및 지역화](../advanced/wpf-globalization-and-localization-overview.md)
> - [WPF 성능](../advanced/optimizing-wpf-application-performance.md)

## <a name="next-steps"></a>다음 단계

이 연습에서는 Windows Presentation Foundation (WPF)를 사용 하 여 UI를 만들기 위한 다양 한 기술을 배웠습니다. 이제 데이터 바인딩된 .NET 앱의 구성 요소를 기본적으로 이해 하 고 있어야 합니다. WPF 아키텍처 및 프로그래밍 모델에 대한 자세한 내용은 다음 항목을 참조하세요.

- [WPF 아키텍처](../advanced/wpf-architecture.md)
- [XAML 개요(WPF)](../advanced/xaml-overview-wpf.md)
- [종속성 속성 개요](../advanced/dependency-properties-overview.md)
- [레이아웃](../advanced/layout.md)

애플리케이션을 만드는 방법에 대한 자세한 내용은 다음 항목을 참조하세요.

- [응용 프로그램 개발](../app-development/index.md)
- [컨트롤](../controls/index.md)
- [데이터 바인딩 개요](../data/data-binding-overview.md)
- [그래픽 및 멀티미디어](../graphics-multimedia/index.md)
- [WPF의 문서](../advanced/documents-in-wpf.md)

## <a name="see-also"></a>참고 항목

- [패널 개요](../controls/panels-overview.md)
- [데이터 템플릿 개요](../data/data-templating-overview.md)
- [WPF 응용 프로그램 빌드](../app-development/building-a-wpf-application-wpf.md)
- [스타일 및 템플릿](../controls/styles-and-templates.md)
