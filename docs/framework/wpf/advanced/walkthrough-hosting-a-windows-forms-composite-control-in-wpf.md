---
title: '연습: WPF에서 Windows Forms 복합 컨트롤 호스팅'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hosting Windows Forms control in WPF [WPF]
- composite controls [WPF], hosting in WPF
ms.assetid: 96fcd78d-1c77-4206-8928-3a0579476ef4
ms.openlocfilehash: e4c1de17b131ee68c6e6fce0035b703eb5b489a0
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991879"
---
# <a name="walkthrough-hosting-a-windows-forms-composite-control-in-wpf"></a>연습: WPF에서 Windows Forms 복합 컨트롤 호스팅
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]에서는 응용 프로그램을 만들기 위한 다양한 환경을 제공합니다. 그러나 코드에 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 상당한 투자가 있으면 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램에서 해당 코드를 처음부터 다시 작성 하는 것 보다는 해당 코드를 다시 사용 하는 것이 더 효과적일 수 있습니다. 가장 일반적인 시나리오는 기존 Windows Forms 컨트롤이 있는 경우입니다. 경우에 따라 이러한 컨트롤에 대한 소스 코드에 액세스하지 못할 수도 있습니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)][!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램에서 이러한 컨트롤을 호스팅하기 위한 간단한 절차를 제공 합니다. 예를 들어, 특수화 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Forms.DataGridView> 된 컨트롤을 호스트 하는 동안 대부분의 프로그래밍에를 사용할 수 있습니다.  
  
 이 연습에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램에서 데이터 입력을 수행 하기 위해 Windows Forms 복합 컨트롤을 호스트 하는 응용 프로그램을 단계별로 안내 합니다. 복합 컨트롤은 DLL로 패키지됩니다. 이 일반적인 절차는 더 복잡한 애플리케이션 및 컨트롤로 확장할 수 있습니다. 이 연습은 [연습의 모양과 기능과 거의 동일 하 게 디자인 되었습니다. Windows Forms](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)에서 WPF 복합 컨트롤 호스팅 주요 차이점은 호스팅 시나리오가 반대라는 점입니다.  
  
 이 연습은 두 개의 섹션으로 구분됩니다. 첫 번째 섹션에서는 Windows Forms 복합 컨트롤의 구현을 간략하게 설명 합니다. 두 번째 섹션에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램에서 복합 컨트롤을 호스트 하 고, 컨트롤에서 이벤트를 수신 하 고, 컨트롤의 일부 속성에 액세스 하는 방법에 대해 자세히 설명 합니다.  
  
 이 연습에서 설명하는 작업은 다음과 같습니다.  
  
- Windows Forms 복합 컨트롤 구현  
  
- WPF 호스트 애플리케이션 구현  
  
 이 연습에서 설명 하는 작업의 전체 코드 목록은 [WPF에서 Windows Forms 복합 컨트롤 호스팅 샘플](https://go.microsoft.com/fwlink/?LinkID=159999)을 참조 하세요.  
  
## <a name="prerequisites"></a>전제 조건  

이 연습을 완료하려면 Visual Studio가 필요합니다.
  
## <a name="implementing-the-windows-forms-composite-control"></a>Windows Forms 복합 컨트롤 구현  
 이 예제에서 사용 되는 Windows Forms 복합 컨트롤은 간단한 데이터 입력 폼입니다. 이 폼에서는 사용자의 이름 및 주소를 사용한 다음 사용자 지정 이벤트를 사용하여 해당 정보를 호스트에 반환합니다. 다음 그림에서는 렌더링된 컨트롤을 보여 줍니다.  

 다음 이미지는 Windows Forms 복합 컨트롤을 보여 줍니다.  

 ![간단한 Windows Forms 컨트롤을 보여 주는 스크린샷](./media/walkthrough-hosting-a-windows-forms-composite-control-in-wpf/windows-forms-control.gif)  
  
### <a name="creating-the-project"></a>프로젝트 만들기  
 프로젝트를 시작하려면  
  
1. 를 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)]시작 하 고 **새 프로젝트** 대화 상자를 엽니다.  
  
2. 창 범주에서 **Windows Forms 컨트롤 라이브러리** 템플릿을 선택 합니다.  
  
3. 새 프로젝트의 이름을 `MyControls`로 지정합니다.  
  
4. 위치에 대해와 같이 편리 하 게 `WpfHostingWindowsFormsControl`명명 된 최상위 폴더를 지정 합니다. 나중에 이 폴더에 호스트 애플리케이션을 넣습니다.  
  
5. **확인**을 클릭해 프로젝트를 만듭니다. 기본 프로젝트에는 라는 `UserControl1`단일 컨트롤이 포함 되어 있습니다.  
  
6. 솔루션 탐색기에서로 `MyControl1`이름을 `UserControl1` 바꿉니다.  
  
 프로젝트에는 다음과 같은 시스템 DLL에 대한 참조가 있어야 합니다. 이러한 DLL이 기본적으로 포함되지 않은 경우 프로젝트에 추가합니다.  
  
- 시스템  
  
- System.Data  
  
- System.Drawing  
  
- System.Windows.Forms  
  
- System.Xml  
  
### <a name="adding-controls-to-the-form"></a>폼에 컨트롤 추가  
 폼에 컨트롤을 추가하려면  
  
- 디자이너 `MyControl1` 에서를 엽니다.  
  
 앞의 <xref:System.Windows.Forms.Label> 그림과 같이 폼에 <xref:System.Windows.Forms.TextBox> 5 개의 컨트롤과 해당 컨트롤을 추가 합니다. 이 예제에서 컨트롤의 <xref:System.Windows.Forms.TextBox> 이름은 다음과 같습니다.  
  
- `txtName`  
  
- `txtAddress`  
  
- `txtCity`  
  
- `txtState`  
  
- `txtZip`  
  
 확인 및 <xref:System.Windows.Forms.Button> **취소**라는 두 개의 컨트롤 **을** 추가 합니다. 이 예제에서 단추 이름은 `btnOK` 각각 및 `btnCancel`입니다.  
  
### <a name="implementing-the-supporting-code"></a>지원 코드 구현  
 코드 보기에서 폼을 엽니다. 컨트롤은 사용자 지정 `OnButtonClick` 이벤트를 발생 시켜 해당 호스트에 수집 된 데이터를 반환 합니다. 데이터는 이벤트 인수 개체에 포함되어 있습니다. 다음 코드에서는 이벤트 및 대리자 선언을 보여 줍니다.  
  
 `MyControl1` 클래스에 다음 코드를 추가합니다.  
  
 [!code-csharp[WpfHostingWindowsFormsControl#2](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/MyControls/MyControl1.cs#2)]
 [!code-vb[WpfHostingWindowsFormsControl#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/MyControls/MyControl1.vb#2)]

 클래스 `MyControlEventArgs` 에는 호스트에 반환 되는 정보가 포함 되어 있습니다.

 다음 클래스를 폼에 추가합니다.

 [!code-csharp[WpfHostingWindowsFormsControl#3](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/MyControls/MyControl1.cs#3)]
 [!code-vb[WpfHostingWindowsFormsControl#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/MyControls/MyControl1.vb#3)]

 사용자가 **확인** 또는 **취소** <xref:System.Windows.Forms.Control.Click> 단추를 클릭 하면 이벤트 처리기가 데이터를 포함 `MyControlEventArgs` 하는 개체를 만들고 이벤트를 `OnButtonClick` 발생 시킵니다. 두 처리기의 유일한 차이점은 이벤트 인수의 `IsOK` 속성입니다. 이 속성을 통해 호스트는 클릭한 단추를 확인할 수 있습니다. `true` **확인** 단추 와`false` **취소** 단추의 경우로 설정 됩니다. 다음 코드에서는 두 개의 단추 처리기를 보여 줍니다.

 `MyControl1` 클래스에 다음 코드를 추가합니다.

 [!code-csharp[WpfHostingWindowsFormsControl#4](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/MyControls/MyControl1.cs#4)]
 [!code-vb[WpfHostingWindowsFormsControl#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/MyControls/MyControl1.vb#4)]

### <a name="giving-the-assembly-a-strong-name-and-building-the-assembly"></a>어셈블리에 강력한 이름을 지정하고 어셈블리 빌드
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램에서이 어셈블리를 참조 하려면 강력한 이름을 포함 해야 합니다. 강력한 이름을 만들려면 Sn.exe를 사용 하 여 키 파일을 만들고 프로젝트에 추가 합니다.

1. [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 명령 프롬프트를 엽니다. 이렇게 하려면 **시작** 메뉴를 클릭 한 다음 **모든 프로그램/Microsoft Visual Studio 2010/Visual Studio Tools/Visual Studio 명령 프롬프트**를 선택 합니다. 그러면 사용자 지정된 환경 변수가 있는 콘솔 창이 시작됩니다.

2. 명령 프롬프트에서 `cd` 명령을 사용 하 여 프로젝트 폴더로 이동 합니다.

3. 다음 명령을 실행하여 MyControls.snk라는 키 파일을 생성합니다.

    ```console
    Sn.exe -k MyControls.snk
    ```

4. 프로젝트에 키 파일을 포함 하려면 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다. 프로젝트 디자이너에서 **서명** 탭을 클릭 하 고 **어셈블리 서명** 확인란을 선택한 다음 키 파일을 찾습니다.

5. 솔루션을 빌드합니다. 빌드하면 MyControls.dll이라는 DLL이 생성됩니다.

## <a name="implementing-the-wpf-host-application"></a>WPF 호스트 애플리케이션 구현
 호스트 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램은 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤을 사용 하 `MyControl1`여를 호스팅합니다. 응용 프로그램은 `OnButtonClick` 이벤트를 처리 하 여 컨트롤에서 데이터를 수신 합니다. 또한 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램에서 컨트롤의 일부 속성을 변경할 수 있는 옵션 단추 모음이 있습니다. 다음 그림에서는 완료된 애플리케이션을 보여 줍니다.

다음 이미지는 WPF 응용 프로그램에 포함 된 컨트롤을 포함 하 여 전체 응용 프로그램을 보여 줍니다.

 ![WPF 페이지에 포함 된 컨트롤을 보여 주는 스크린샷](./media/walkthrough-hosting-a-windows-forms-composite-control-in-wpf/windows-presentation-foundation-page-control.gif)

### <a name="creating-the-project"></a>프로젝트 만들기
 프로젝트를 시작하려면

1. 를 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)]열고 **새 프로젝트**를 선택 합니다.

2. 창 범주에서 **WPF 응용 프로그램** 템플릿을 선택 합니다.

3. 새 프로젝트의 이름을 `WpfHost`로 지정합니다.

4. 위치에는 MyControls 프로젝트를 포함하는 동일한 최상위 폴더를 지정합니다.

5. **확인**을 클릭해 프로젝트를 만듭니다.

 또한 및 기타 어셈블리를 포함 `MyControl1` 하는 DLL에 대 한 참조를 추가 해야 합니다.

1. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 **참조 추가**를 선택 합니다.

2. **찾아보기** 탭을 클릭 하 고 MyControls이 포함 된 폴더를 찾습니다. 이 연습에서 이 폴더는 MyControls\bin\Debug입니다.

3. MyControls를 선택 하 고 **확인**을 클릭 합니다.

4. Windows양식 통합 어셈블리에 참조를 추가 합니다 .이 어셈블리에는 Windows Integration .dll 이라는 이름이 지정 됩니다.

### <a name="implementing-the-basic-layout"></a>기본 레이아웃 구현
 호스트 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 응용 프로그램의는 mainwindow.xaml에서 구현 됩니다. 이 파일에 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 는 레이아웃을 정의 하 고 Windows Forms 컨트롤을 호스트 하는 태그가 포함 되어 있습니다. 애플리케이션은 세 가지 영역으로 구분됩니다.

- **컨트롤 속성** 패널-호스트 된 컨트롤의 다양 한 속성을 수정 하는 데 사용할 수 있는 옵션 단추 모음이 포함 되어 있습니다.

- 호스팅된 컨트롤에서 반환 된 데이터를 표시 하 <xref:System.Windows.Controls.TextBlock> 는 여러 요소가 포함 된 **제어판의 데이터** 입니다.

- 호스트된 컨트롤 자체.

 기본 레이아웃은 다음과 같은 XAML로 표시됩니다. 호스트 `MyControl1` 하는 데 필요한 태그는이 예제에서 생략 되었지만 나중에 설명 하겠습니다.

 MainWindow.xaml의 XAML을 다음 코드로 바꿉니다. Visual Basic를 사용 하는 경우 클래스를로 `x:Class="MainWindow"`변경 합니다.

 [!code-xaml[WpfHostingWindowsFormsControl#100](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml#100)]

 첫 번째 <xref:System.Windows.Controls.StackPanel> 요소에는 호스트 된 <xref:System.Windows.Controls.RadioButton> 컨트롤의 다양 한 기본 속성을 수정할 수 있도록 하는 여러 컨트롤 집합이 포함 되어 있습니다. 그런 다음 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 를 호스팅하 `MyControl1`는 요소입니다. Final <xref:System.Windows.Controls.StackPanel> 요소에는 호스팅된 <xref:System.Windows.Controls.TextBlock> 컨트롤에서 반환 하는 데이터를 표시 하는 여러 요소가 포함 됩니다. 요소와 <xref:System.Windows.Controls.DockPanel.Dock%2A> 및 <xref:System.Windows.FrameworkElement.Height%2A> 특성 설정의 순서는 호스트 된 컨트롤을 간격이 나 왜곡 없이 창에 포함 합니다.

#### <a name="hosting-the-control"></a>컨트롤 호스팅
 이전 XAML의 편집 된 다음 버전은를 호스트 `MyControl1`하는 데 필요한 요소를 중점적으로 다룹니다.

 [!code-xaml[WpfHostingWindowsFormsControl#101](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml#101)]
[!code-xaml[WpfHostingWindowsFormsControl#102](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml#102)]

 네임 `xmlns` 스페이스 매핑 특성은 호스팅된 컨트롤을 포함 `MyControls` 하는 네임 스페이스에 대 한 참조를 만듭니다. 이 매핑을 사용 하면를 `MyControl1` [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 로 `<mcl:MyControl1>`나타낼 수 있습니다.

 XAML의 두 요소가 호스팅을 처리합니다.

- `WindowsFormsHost`응용[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 프로그램 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 에서 Windows Forms 컨트롤을 호스트 하는 데 사용할 수 있는 요소를 나타냅니다.

- `mcl:MyControl1`가 나타내는 `MyControl1`는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소의 자식 컬렉션에 추가 됩니다. 결과적으로이 Windows Forms 컨트롤은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 창의 일부로 렌더링 되며 응용 프로그램에서 컨트롤과 통신할 수 있습니다.

### <a name="implementing-the-code-behind-file"></a>코드 숨김 파일 구현
 코드 숨김이 파일 mainwindow.xaml 또는 MainWindow.xaml.cs에는 이전 섹션에서 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 설명한의 기능을 구현 하는 절차 코드가 포함 되어 있습니다. 기본 작업은 다음과 같습니다.

- 이벤트 처리기를의 `MyControl1` `OnButtonClick` 이벤트에 연결 합니다.

- 옵션 단추의 컬렉션을 `MyControl1`설정 하는 방법에 따라의 다양 한 속성을 수정 합니다.

- 컨트롤에서 수집한 데이터 표시.

#### <a name="initializing-the-application"></a>애플리케이션 초기화
 초기화 코드는 창의 <xref:System.Windows.FrameworkElement.Loaded> 이벤트에 대 한 이벤트 처리기에 포함 되 고 컨트롤의 `OnButtonClick` 이벤트에 이벤트 처리기를 연결 합니다.

 Mainwindow.xaml 또는 MainWindow.xaml.cs에서 다음 코드를 `MainWindow` 클래스에 추가 합니다.

 [!code-csharp[WpfHostingWindowsFormsControl#11](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml.cs#11)]
 [!code-vb[WpfHostingWindowsFormsControl#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/WpfHost/Page1.xaml.vb#11)]

 앞에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 설명한가 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소의 `MyControl1` `MyControl1` 자식요소<xref:System.Windows.Forms.Integration.WindowsFormsHost.Child%2A> 컬렉션에 추가 되었기 때문에에 대 한 참조를 가져오기 위해 요소의를캐스팅할수있습니다.<xref:System.Windows.Forms.Integration.WindowsFormsHost> 그런 다음 해당 참조를 사용 하 여에 `OnButtonClick`이벤트 처리기를 연결할 수 있습니다.

 컨트롤 자체에 대 한 참조를 제공 하는 것 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 외에도는 응용 프로그램에서 조작할 수 있는 다양 한 컨트롤 속성을 노출 합니다. 초기화 코드는 나중에 애플리케이션에서 사용할 수 있도록 private 전역 변수에 해당 값을 할당합니다.

 `MyControls` DLL의 형식에 쉽게 액세스할 수 있도록 파일의 맨 위에 다음 `Imports` 또는 `using` 문을 추가 합니다.

```vb
Imports MyControls
```

```csharp
using MyControls;
```

#### <a name="handling-the-onbuttonclick-event"></a>OnButtonClick 이벤트 처리
 `MyControl1`사용자가 `OnButtonClick` 컨트롤의 단추 중 하나를 클릭 하면 이벤트를 발생 시킵니다.

 `MainWindow` 클래스에 다음 코드를 추가합니다.

 [!code-csharp[WpfHostingWindowsFormsControl#12](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml.cs#12)]
 [!code-vb[WpfHostingWindowsFormsControl#12](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/WpfHost/Page1.xaml.vb#12)]

 텍스트 상자의 데이터는 `MyControlEventArgs` 개체에 압축 됩니다. 사용자가 **확인** 단추를 클릭 하면 이벤트 처리기가 데이터를 추출 하 여 아래 `MyControl1`패널에 표시 합니다.

#### <a name="modifying-the-controls-properties"></a>컨트롤의 속성 수정
 요소 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 는 호스트 된 컨트롤의 몇 가지 기본 속성을 노출 합니다. 결과적으로 애플리케이션의 스타일과 더 가깝게 일치하도록 컨트롤의 모양을 변경할 수 있습니다. 왼쪽 패널의 옵션 단추 집합을 사용하여 사용자는 여러 가지 색 및 글꼴 속성을 수정할 수 있습니다. 각 단추 집합에는 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트에 대 한 처리기가 있으며 사용자의 옵션 단추 선택 항목을 검색 하 고 컨트롤의 해당 속성을 변경 합니다.

 `MainWindow` 클래스에 다음 코드를 추가합니다.

 [!code-csharp[WpfHostingWindowsFormsControl#13](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml.cs#13)]
 [!code-vb[WpfHostingWindowsFormsControl#13](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/WpfHost/Page1.xaml.vb#13)]  
  
 애플리케이션을 빌드 및 실행합니다. Windows Forms 복합 컨트롤에 일부 텍스트를 추가한 다음 **확인**을 클릭 합니다. 텍스트가 레이블에 나타납니다. 컨트롤에 대한 효과를 확인하려면 다른 라디오 단추를 클릭합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Visual Studio에서 XAML 디자인](/visualstudio/designers/designing-xaml-in-visual-studio)
- [연습: WPF에서 Windows Forms 컨트롤 호스팅](walkthrough-hosting-a-windows-forms-control-in-wpf.md)
- [연습: Windows Forms에서 WPF 복합 컨트롤 호스팅](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
