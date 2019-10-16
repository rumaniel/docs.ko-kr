---
title: '연습: Windows Forms에서 WPF 복합 컨트롤 호스팅'
ms.date: 03/30/2017
helpviewer_keywords:
- hosting WPF content in Windows Forms [WPF]
ms.assetid: 0ac41286-4c1b-4b17-9196-d985cb844ce1
ms.openlocfilehash: a062095885e6c1fc8816a78847968b1c250eabf8
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991455"
---
# <a name="walkthrough-hosting-a-wpf-composite-control-in-windows-forms"></a>연습: Windows Forms에서 WPF 복합 컨트롤 호스팅
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]에서는 응용 프로그램을 만들기 위한 다양한 환경을 제공합니다. 그러나 코드에 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 상당한 투자를 한 경우 처음부터 다시 작성 하지 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 않고 기존 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 응용 프로그램을 확장 하는 것이 더 효과적일 수 있습니다. 일반적인 시나리오는 Windows Forms 응용 프로그램 내에서로 구현 된 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 하나 이상의 컨트롤을 포함 하려는 경우입니다. WPF 컨트롤을 사용자 지정 하는 방법에 대 한 자세한 내용은 [컨트롤 사용자 지정](../controls/control-customization.md)을 참조 하세요.  
  
 이 연습에서는 Windows Forms 응용 프로그램에서 데이터 입력을 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 수행 하기 위해 복합 컨트롤을 호스트 하는 응용 프로그램을 단계별로 안내 합니다. 복합 컨트롤은 DLL로 패키지됩니다. 이 일반적인 절차는 더 복잡한 애플리케이션 및 컨트롤로 확장할 수 있습니다. 이 연습은 [연습의 모양과 기능과 거의 동일 하 게 디자인 되었습니다. WPF](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)에서 Windows Forms 복합 컨트롤 호스팅 주요 차이점은 호스팅 시나리오가 반대라는 점입니다.  
  
 이 연습은 두 개의 섹션으로 구분됩니다. 첫 번째 섹션에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 복합 컨트롤의 구현을 간략하게 설명 합니다. 두 번째 섹션에서는 Windows Forms 응용 프로그램에서 복합 컨트롤을 호스트 하 고, 컨트롤에서 이벤트를 수신 하 고, 컨트롤의 일부 속성에 액세스 하는 방법에 대해 자세히 설명 합니다.  
  
 이 연습에서 설명하는 작업은 다음과 같습니다.  
  
- WPF 복합 컨트롤 구현  
  
- Windows Forms 호스트 애플리케이션 구현  
  
 이 연습에서 설명 하는 작업의 전체 코드 목록은 [Windows Forms 샘플에서 WPF 복합 컨트롤 호스팅](https://github.com/microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/WindowsFormsHostingWpfControl)을 참조 하세요.  
  
## <a name="prerequisites"></a>전제 조건  

이 연습을 완료하려면 Visual Studio가 필요합니다.  
  
## <a name="implementing-the-wpf-composite-control"></a>WPF 복합 컨트롤 구현  
 이 예제에서 사용 되는 복합컨트롤은사용자의이름과주소를사용하는간단한데이터입력폼입니다.[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 사용자가 작업이 완료되었음을 나타내는 두 개의 단추 중 하나를 클릭하면 컨트롤에서 사용자 지정 이벤트가 발생하여 해당 정보가 호스트에 반환됩니다. 다음 그림에서는 렌더링된 컨트롤을 보여 줍니다. 

 다음 이미지는 WPF 복합 컨트롤을 보여 줍니다. 

 ![간단한 WPF 컨트롤을 보여 주는 스크린샷](./media/walkthrough-hosting-a-wpf-composite-control-in-windows-forms/windows-presentation-foundation-composite-control.png)  
  
### <a name="creating-the-project"></a>프로젝트 만들기  
 프로젝트를 시작하려면  
  
1. 를 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)]시작 하 고 **새 프로젝트** 대화 상자를 엽니다.  
  
2. Visual C# 및 Windows 범주에서 **WPF 사용자 정의 컨트롤 라이브러리** 템플릿을 선택 합니다.  
  
3. 새 프로젝트의 이름을 `MyControls`로 지정합니다.  
  
4. 위치에 대해와 같이 편리 하 게 `WindowsFormsHostingWpfControl`명명 된 최상위 폴더를 지정 합니다. 나중에 이 폴더에 호스트 애플리케이션을 넣습니다.  
  
5. **확인**을 클릭해 프로젝트를 만듭니다. 기본 프로젝트에는 라는 `UserControl1`단일 컨트롤이 포함 되어 있습니다.  
  
6. 솔루션 탐색기에서로 `MyControl1`이름을 `UserControl1` 바꿉니다.  
  
 프로젝트에는 다음과 같은 시스템 DLL에 대한 참조가 있어야 합니다. 이러한 DLL이 기본적으로 포함되지 않은 경우 프로젝트에 추가합니다.  
  
- PresentationCore  
  
- PresentationFramework  
  
- 시스템  
  
- WindowsBase  
  
### <a name="creating-the-user-interface"></a>사용자 인터페이스 만들기  
 복합 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 컨트롤의는를 사용 하 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]여 구현 됩니다. 복합 컨트롤 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 은 5 개의 <xref:System.Windows.Controls.TextBox> 요소로 구성 됩니다. 각 <xref:System.Windows.Controls.TextBox> 요소에는 레이블로 <xref:System.Windows.Controls.TextBlock> 사용 되는 연결 된 요소가 있습니다. 아래쪽에는 <xref:System.Windows.Controls.Button> 두 개의 요소, 즉 **확인** 및 **취소가**있습니다. 사용자가 이 단추 중 하나를 클릭하면 컨트롤에서 사용자 지정 이벤트가 발생하여 호스트에 정보가 반환됩니다.  
  
#### <a name="basic-layout"></a>기본 레이아웃  
 여러 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 요소는 <xref:System.Windows.Controls.Grid> 요소에 포함 되어 있습니다. HTML에서 요소 <xref:System.Windows.Controls.Grid> 를 `Table` 사용 하는 것과 거의 동일한 방식으로를 사용 하 여 복합 컨트롤의 콘텐츠를 정렬할 수 있습니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에는 <xref:System.Windows.Documents.Table> 요소도 있지만 <xref:System.Windows.Controls.Grid> 간단한 레이아웃 작업에는 더 간단 하 고 더 적합 합니다.  
  
 다음 XAML에서는 기본 레이아웃을 보여 줍니다. 이 XAML은 <xref:System.Windows.Controls.Grid> 요소의 열 및 행 수를 지정 하 여 컨트롤의 전체 구조를 정의 합니다.  
  
 MyControl1.xaml에서 기존 XAML을 다음 XAML로 바꿉니다.  
  
 [!code-xaml[WindowsFormsHostingWpfControl#101](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml#101)]  
[!code-xaml[WindowsFormsHostingWpfControl#102](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml#102)]  
  
#### <a name="adding-textblock-and-textbox-elements-to-the-grid"></a>그리드에 TextBlock 및 TextBox 요소 추가  
 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 요소의 및 특성<xref:System.Windows.Controls.Grid.ColumnProperty> 을 적절 한 행 및 열 번호로 설정 하 여 표에 요소를 놓습니다 <xref:System.Windows.Controls.Grid.RowProperty> . 행 및 열 번호는 0부터 시작해야 합니다. <xref:System.Windows.Controls.Grid.ColumnSpanProperty> 특성을 설정 하 여 요소가 여러 열에 걸쳐 있을 수 있습니다. 요소에 대 한 <xref:System.Windows.Controls.Grid> 자세한 내용은 [Grid 요소 만들기](../controls/how-to-create-a-grid-element.md)를 참조 하세요.  
  
 다음 XAML은 <xref:System.Windows.Controls.TextBox> <xref:System.Windows.Controls.Grid.RowProperty> 및 <xref:System.Windows.Controls.TextBlock> 특성이<xref:System.Windows.Controls.Grid.ColumnProperty> 있는 복합 컨트롤의 및 요소를 보여 줍니다 .이 요소는 그리드에서 요소를 올바르게 삽입 하도록 설정 됩니다.  
  
 Mycontrol1.xaml에서 <xref:System.Windows.Controls.Grid> 요소 내에 다음 xaml을 추가 합니다.  
  
 [!code-xaml[WindowsFormsHostingWpfControl#103](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml#103)]  
  
#### <a name="styling-the-ui-elements"></a>UI 요소 스타일 지정  
 데이터 입력 폼의 요소는 대부분 모양이 비슷합니다. 즉, 이러한 요소의 여러 속성 설정이 동일합니다. 이전 XAML은 각 요소의 특성을 별도로 설정 하는 대신 요소 <xref:System.Windows.Style> 를 사용 하 여 요소의 클래스에 대 한 표준 속성 설정을 정의 합니다. 이 방법을 사용하면 컨트롤의 복잡도를 줄이고 하나의 스타일 특성을 통해 여러 요소의 모양을 변경할 수 있습니다.  
  
 요소 <xref:System.Windows.Style> 는 <xref:System.Windows.Controls.Grid> 요소의 속성에포함되어있으므로컨트롤의모든요소에서사용할수있습니다.<xref:System.Windows.FrameworkElement.Resources%2A> 스타일의 이름을 지정 하는 경우 스타일 이름에 <xref:System.Windows.Style> 요소 집합을 추가 하 여 요소에 적용 합니다. 이름이 지정되지 않은 스타일은 요소의 기본 스타일이 됩니다. 스타일에 대 한 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 자세한 내용은 스타일 지정 [및 템플릿](../controls/styling-and-templating.md)을 참조 하세요.  
  
 다음 XAML에서는 복합 컨트롤 <xref:System.Windows.Style> 의 요소를 보여 줍니다. 스타일이 요소에 어떻게 적용되는지 확인하려면 앞의 XAML을 참조하세요. 예를 들어 마지막 <xref:System.Windows.Controls.TextBlock> 요소 `inlineText` 는 스타일을 사용 하 고 마지막 <xref:System.Windows.Controls.TextBox> 요소는 기본 스타일을 사용 합니다.  
  
 Mycontrol1.xaml에서 <xref:System.Windows.Controls.Grid> 시작 요소 바로 뒤에 다음 xaml을 추가 합니다.  
  
 [!code-xaml[WindowsFormsHostingWpfControl#104](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml#104)]  
  
#### <a name="adding-the-ok-and-cancel-buttons"></a>확인 및 취소 단추 추가  
 복합 컨트롤의 마지막 요소는의 마지막 행 <xref:System.Windows.Controls.Grid>에 있는 처음 두 개의 열을 차지 하는 **OK** 및 **Cancel** <xref:System.Windows.Controls.Button> 요소입니다. 이러한 요소는 공용 이벤트 처리기, `ButtonClicked`및 이전 XAML에 정의 된 기본 <xref:System.Windows.Controls.Button> 스타일을 사용 합니다.  
  
 Mycontrol1.xaml에서 마지막 <xref:System.Windows.Controls.TextBox> 요소 뒤에 다음 xaml을 추가 합니다. 이제 복합 컨트롤의 일부가완료되었습니다.[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]  
  
 [!code-xaml[WindowsFormsHostingWpfControl#105](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml#105)]  
  
### <a name="implementing-the-code-behind-file"></a>코드 숨김 파일 구현  
 코드 숨김이 MyControl1.xaml.cs는 세 가지 필수 작업을 구현 합니다.
  
1. 사용자가 단추 중 하나를 클릭할 때 발생하는 이벤트를 처리합니다.  
  
2. <xref:System.Windows.Controls.TextBox> 요소에서 데이터를 검색 하 여 사용자 지정 이벤트 인수 개체에 패키지 합니다.  
  
3. 사용자 지정 `OnButtonClick` 이벤트를 발생 시킵니다 .이 이벤트는 사용자가 완료 했음을 호스트에 알리고 데이터를 다시 호스트에 전달 합니다.  
  
 또한 컨트롤에서는 모양을 변경하는 데 사용할 수 있는 많은 수의 색 및 글꼴 속성을 노출합니다. Windows Forms 컨트롤을 호스트 하는 데 사용 되는 <xref:System.Windows.Forms.Integration.ElementHost> <xref:System.Windows.Controls.Panel.Background%2A> 클래스와달리클래스는컨트롤의<xref:System.Windows.Forms.Integration.WindowsFormsHost> 속성만 노출 합니다. 이 코드 예제와 연습에 [설명 된 예제 간의 유사성을 유지 하려면 다음을 수행 합니다. WPF](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)에서 Windows Forms 복합 컨트롤을 호스트 하는 경우 컨트롤은 나머지 속성을 직접 노출 합니다.  
  
#### <a name="the-basic-structure-of-the-code-behind-file"></a>코드 숨김 파일의 기본 구조  
 코드 숨겨진 파일은 단일 네임 스페이스로 구성 되며, `MyControls`이 네임 스페이스에는 `MyControl1` 및 `MyControlEventArgs`라는 두 개의 클래스가 포함 됩니다.  
  
```csharp  
namespace MyControls  
{  
  public partial class MyControl1 : Grid  
  {  
    //...  
  }  
  public class MyControlEventArgs : EventArgs  
  {  
    //...  
  }  
}  
```  
  
 첫 번째 클래스 `MyControl1`는 mycontrol1.xaml에 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 정의 된의 기능을 구현 하는 코드를 포함 하는 partial 클래스입니다. Mycontrol1.xaml이 구문 분석 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 되 면이 동일한 partial 클래스로 변환 되 고 두 partial 클래스가 병합 되어 컴파일된 컨트롤을 형성 합니다. 따라서 코드 숨김 파일의 클래스 이름이 MyControl1.xaml에 할당된 클래스 이름과 일치해야 하며 컨트롤의 루트 요소에서 상속되어야 합니다. 두 번째 클래스인 `MyControlEventArgs`는 호스트에 데이터를 다시 보내는 데 사용 되는 이벤트 인수 클래스입니다.  
  
 MyControl1.xaml.cs를 엽니다. 다음 이름을 포함 하 고에서 <xref:System.Windows.Controls.Grid>상속 하도록 기존 클래스 선언을 변경 합니다.  
  
 [!code-csharp[WindowsFormsHostingWpfControl#21](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml.cs#21)]  
  
#### <a name="initializing-the-control"></a>컨트롤 초기화  
 다음 코드에서는 다음과 같은 몇 가지 기본 작업을 구현합니다.  
  
- Private 이벤트 `OnButtonClick`, 및 연결 된 `MyControlEventHandler`대리자를 선언 합니다.  
  
- 사용자 데이터를 저장하는 여러 private 전역 변수를 만듭니다. 이 데이터는 해당 속성을 통해 노출됩니다.  
  
- 컨트롤의 `Init` <xref:System.Windows.FrameworkElement.Loaded> 이벤트에 대 한 처리기를 구현 합니다. 이 처리기에서는 MyControl1.xaml에 정의된 값을 할당하여 전역 변수를 초기화합니다. 이렇게 하기 위해이 메서드는 일반적인 <xref:System.Windows.FrameworkElement.Name%2A> <xref:System.Windows.Controls.TextBlock> 요소인 `nameLabel`에 할당 된를 사용 하 여 해당 요소의 속성 설정에 액세스 합니다.  
  
 기존 생성자를 삭제 하 고 `MyControl1` 클래스에 다음 코드를 추가 합니다.  
  
 [!code-csharp[WindowsFormsHostingWpfControl#11](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml.cs#11)]  
  
#### <a name="handling-the-buttons-click-events"></a>단추의 클릭 이벤트 처리  
 사용자는 **확인** 단추나 **취소** 단추를 클릭 하 여 데이터 입력 작업을 완료 했음을 나타냅니다. 두 단추 모두 동일한 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트 처리기를 `ButtonClicked`사용 합니다. 두 단추 모두에는 `btnOK` `sender` 인수 값 `btnCancel`을 검사 하 여 처리기가 클릭 한 단추를 확인할 수 있는 이름 또는가 있습니다. 처리기에서는 다음 작업을 수행합니다.  
  
- 요소의<xref:System.Windows.Controls.TextBox> 데이터 `MyControlEventArgs` 를 포함 하는 개체를 만듭니다.  
  
- 사용자가 **취소** 단추를 클릭 한 경우 `MyControlEventArgs` 개체의 `IsOK` 속성을로 `false`설정 합니다.  
  
- 사용자가 완료 되었음을 호스트에 알리기 위해 이벤트를발생시키고수집된데이터를다시전달합니다.`OnButtonClick`  
  
 `MyControl1` 클래스의 `Init` 메서드 뒤에 다음 코드를 추가 합니다.  
  
 [!code-csharp[WindowsFormsHostingWpfControl#12](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml.cs#12)]  
  
#### <a name="creating-properties"></a>속성 만들기  
 클래스의 나머지 부분에서는 위에서 설명한 전역 변수에 해당하는 속성을 노출하기만 합니다. 속성이 변경되면 set 접근자가 해당 요소 속성을 변경하고 기본 전역 변수를 업데이트하여 컨트롤 모양을 수정합니다.  
  
 `MyControl1` 클래스에 다음 코드를 추가 합니다.  
  
 [!code-csharp[WindowsFormsHostingWpfControl#13](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml.cs#13)]  
  
#### <a name="sending-the-data-back-to-the-host"></a>데이터를 다시 호스트에 보내기  
 파일의 마지막 구성 요소는 수집 된 `MyControlEventArgs` 데이터를 호스트에 다시 보내는 데 사용 되는 클래스입니다.  
  
 `MyControls` 네임 스페이스에 다음 코드를 추가 합니다. 구현 방법은 간단하므로 자세히 설명하지 않습니다.  
  
 [!code-csharp[WindowsFormsHostingWpfControl#14](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml.cs#14)]  
  
 솔루션을 빌드합니다. 빌드하면 MyControls.dll이라는 DLL이 생성됩니다.  
  
<a name="winforms_host_section"></a>   
## <a name="implementing-the-windows-forms-host-application"></a>Windows Forms 호스트 애플리케이션 구현  
 Windows Forms 호스트 응용 프로그램은 <xref:System.Windows.Forms.Integration.ElementHost> 개체를 사용 하 여 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 복합 컨트롤을 호스팅합니다. 응용 프로그램은 `OnButtonClick` 이벤트를 처리 하 여 복합 컨트롤에서 데이터를 수신 합니다. 또한 애플리케이션은 컨트롤 모양을 수정하는 데 사용할 수 있는 옵션 단추 집합도 포함합니다. 다음 그림에서는 애플리케이션을 보여 줍니다.  

다음 이미지는 Windows Forms 응용 프로그램에서 호스트 되는 WPF 복합 컨트롤을 보여 줍니다. "  

 ![Avalon 컨트롤을 호스트 하는 Windows Form을 표시 하는 Scteenshot입니다.](./media/walkthrough-hosting-a-wpf-composite-control-in-windows-forms/windows-form-hosting-avalon-control.png)  
  
### <a name="creating-the-project"></a>프로젝트 만들기  
 프로젝트를 시작하려면  
  
1. 를 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)]시작 하 고 **새 프로젝트** 대화 상자를 엽니다.  
  
2. Visual C# 및 Windows 범주에서 **Windows Forms 응용 프로그램** 템플릿을 선택 합니다.  
  
3. 새 프로젝트의 이름을 `WFHost`로 지정합니다.  
  
4. 위치에는 MyControls 프로젝트를 포함하는 동일한 최상위 폴더를 지정합니다.  
  
5. **확인**을 클릭해 프로젝트를 만듭니다.  
  
 또한 및 기타 어셈블리를 포함 `MyControl1` 하는 DLL에 대 한 참조를 추가 해야 합니다.  
  
1. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 **참조 추가**를 선택 합니다.  
  
2. **찾아보기** 탭을 클릭 하 고 MyControls이 포함 된 폴더를 찾습니다. 이 연습에서 이 폴더는 MyControls\bin\Debug입니다.  
  
3. MyControls를 선택 하 고 **확인**을 클릭 합니다.  
  
4. 다음 어셈블리에 대한 참조를 추가합니다.  
  
    - PresentationCore  
  
    - PresentationFramework  
  
    - System.Xaml  
  
    - WindowsBase  
  
    - WindowsFormsIntegration  
  
### <a name="implementing-the-user-interface-for-the-application"></a>애플리케이션에 대한 사용자 인터페이스 구현  
 Windows Form 애플리케이션의 UI에는 WPF 복합 컨트롤과 상호 작용하는 여러 컨트롤이 포함되어 있습니다.  
  
1. Windows Form 디자이너에서 Form1을 엽니다.  
  
2. 컨트롤 크기에 맞게 폼을 확장합니다.  
  
3. 폼의 오른쪽 위 모퉁이에 <xref:System.Windows.Forms.Panel?displayProperty=nameWithType> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 복합 컨트롤을 포함할 컨트롤을 추가 합니다.  
  
4. 폼에 다음 <xref:System.Windows.Forms.GroupBox?displayProperty=nameWithType> 컨트롤을 추가 합니다.  
  
    |이름|텍스트|  
    |----------|----------|  
    |groupBox1|배경색|  
    |groupBox2|전경색|  
    |groupBox3|글꼴 크기|  
    |groupBox4|글꼴 패밀리|  
    |groupBox5|글꼴 스타일|  
    |groupBox6|글꼴 두께|  
    |groupBox7|컨트롤의 데이터|  
  
5. 컨트롤에 다음 <xref:System.Windows.Forms.RadioButton?displayProperty=nameWithType> 컨트롤을 추가 합니다. <xref:System.Windows.Forms.GroupBox?displayProperty=nameWithType>  
  
    |GroupBox|이름|텍스트|  
    |--------------|----------|----------|  
    |groupBox1|radioBackgroundOriginal|원래 색|  
    |groupBox1|radioBackgroundLightGreen|LightGreen|  
    |groupBox1|radioBackgroundLightSalmon|LightSalmon|  
    |groupBox2|radioForegroundOriginal|원래 색|  
    |groupBox2|radioForegroundRed|빨강|  
    |groupBox2|radioForegroundYellow|노랑|  
    |groupBox3|radioSizeOriginal|원래 색|  
    |groupBox3|radioSizeTen|10|  
    |groupBox3|radioSizeTwelve|12|  
    |groupBox4|radioFamilyOriginal|원래 색|  
    |groupBox4|radioFamilyTimes|궁서|  
    |groupBox4|radioFamilyWingDings|WingDings|  
    |groupBox5|radioStyleOriginal|보통|  
    |groupBox5|radioStyleItalic|기울임꼴|  
    |groupBox6|radioWeightOriginal|원래 색|  
    |groupBox6|radioWeightBold|Bold|  
  
6. 다음 <xref:System.Windows.Forms.Label?displayProperty=nameWithType> 컨트롤을 마지막 <xref:System.Windows.Forms.GroupBox?displayProperty=nameWithType>에 추가 합니다. 이러한 컨트롤은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 복합 컨트롤에서 반환 된 데이터를 표시 합니다.  
  
    |GroupBox|이름|텍스트|  
    |--------------|----------|----------|  
    |groupBox7|lblName|이름:|  
    |groupBox7|lblAddress|구/군/시:|  
    |groupBox7|lblCity|시/도:|  
    |groupBox7|lblState|상태:|  
    |groupBox7|lblZip|우편 번호:|  
  
### <a name="initializing-the-form"></a>폼 초기화  
 일반적으로 폼의 <xref:System.Windows.Forms.Form.Load> 이벤트 처리기에서 호스팅 코드를 구현 합니다. 다음 코드에서는 <xref:System.Windows.Forms.Form.Load> 이벤트 처리기, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 복합 컨트롤의 <xref:System.Windows.FrameworkElement.Loaded> 이벤트에 대 한 처리기 및 나중에 사용 되는 여러 전역 변수에 대 한 선언을 보여 줍니다.  
  
 Windows Forms 디자이너에서 폼을 두 번 클릭 하 여 <xref:System.Windows.Forms.Form.Load> 이벤트 처리기를 만듭니다. Form1.cs의 맨 위에 다음 `using` 문을 추가 합니다.  
  
 [!code-csharp[WindowsFormsHostingWpfControl#10](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/WFHost/Form1.cs#10)]  
  
 기존 `Form1` 클래스의 내용을 다음 코드로 바꿉니다.  
  
 [!code-csharp[WindowsFormsHostingWpfControl#2](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/WFHost/Form1.cs#2)]  
  
 이전 `Form1_Load` 코드의 메서드는 컨트롤을 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 호스트 하는 일반적인 절차를 보여 줍니다.  
  
1. 새 <xref:System.Windows.Forms.Integration.ElementHost> 개체를 만듭니다.  
  
2. 컨트롤의 <xref:System.Windows.Forms.Control.Dock%2A> 속성을로 <xref:System.Windows.Forms.DockStyle.Fill?displayProperty=nameWithType>설정 합니다.  
  
3. 컨트롤을 <xref:System.Windows.Forms.Panel> 컨트롤 의<xref:System.Windows.Forms.Control.Controls%2A> 컬렉션에 추가 합니다. <xref:System.Windows.Forms.Integration.ElementHost>  
  
4. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤의 인스턴스를 만듭니다.  
  
5. 컨트롤을 <xref:System.Windows.Forms.Integration.ElementHost> <xref:System.Windows.Forms.Integration.ElementHost.Child%2A> 컨트롤의 속성에 할당 하 여 폼에 복합 컨트롤을 호스팅합니다.  
  
 `Form1_Load` 메서드의 나머지 두 줄은 처리기를 두 개의 컨트롤 이벤트에 연결 합니다.  
  
- `OnButtonClick`사용자가 **확인** 또는 **취소** 단추를 클릭할 때 복합 컨트롤에서 발생 하는 사용자 지정 이벤트입니다. 이 이벤트를 처리하여 사용자의 응답을 수신하고 사용자가 지정한 데이터를 수집합니다.  
  
- <xref:System.Windows.FrameworkElement.Loaded>는 컨트롤이 완전히 로드 될 때 컨트롤에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 의해 발생 하는 표준 이벤트입니다. 이 예제에서는 컨트롤의 속성을 사용하여 여러 전역 변수를 초기화해야 하기 때문에 이 이벤트가 사용됩니다. 폼의 <xref:System.Windows.Forms.Form.Load> 이벤트가 발생할 때 컨트롤이 완전히 로드 되지 않고 해당 값이로 `null`설정 됩니다. 이러한 속성에 액세스 하기 전에 컨트롤의 <xref:System.Windows.FrameworkElement.Loaded> 이벤트가 발생할 때까지 기다려야 합니다.  
  
 <xref:System.Windows.FrameworkElement.Loaded> 이벤트 처리기는 위의 코드에 나와 있습니다. `OnButtonClick` 처리기는 다음 섹션에서 설명 합니다.  
  
### <a name="handling-onbuttonclick"></a>OnButtonClick 처리  
 이 `OnButtonClick` 이벤트는 사용자가 **확인** 또는 **취소** 단추를 클릭할 때 발생 합니다.  
  
 이벤트 처리기는 이벤트 인수의 `IsOK` 필드를 확인 하 여 클릭 한 단추를 확인 합니다. `lbl` 데이터<xref:System.Windows.Forms.Label> 변수는 앞에서 설명한 컨트롤에 해당 합니다. 사용자가 **확인** 단추를 클릭 하면 컨트롤의 <xref:System.Windows.Controls.TextBox> 컨트롤에 있는 데이터가 해당 <xref:System.Windows.Forms.Label> 컨트롤에 할당 됩니다. 사용자가 **취소**를 <xref:System.Windows.Forms.Label.Text%2A> 클릭 하면 값이 기본 문자열로 설정 됩니다.  
  
 다음 단추 클릭 이벤트 처리기 코드를 `Form1` 클래스에 추가 합니다.  
  
 [!code-csharp[WindowsFormsHostingWpfControl#3](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/WFHost/Form1.cs#3)]  
  
 애플리케이션을 빌드 및 실행합니다. WPF 복합 컨트롤에 일부 텍스트를 추가한 다음 **확인을**클릭 합니다. 텍스트가 레이블에 나타납니다. 현재는 라디오 단추를 처리하는 코드가 추가되지 않았습니다.  
  
### <a name="modifying-the-appearance-of-the-control"></a>컨트롤의 모양 수정  
 폼의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤을 사용 하면 사용자가 복합 컨트롤의 전경색 및 배경색 뿐만 아니라 여러 글꼴 속성을 변경할 수 있습니다. <xref:System.Windows.Forms.RadioButton> 배경색은 <xref:System.Windows.Forms.Integration.ElementHost> 개체에 의해 노출 됩니다. 나머지 속성은 컨트롤의 사용자 지정 속성으로 노출됩니다.  
  
 폼에서 각 <xref:System.Windows.Forms.RadioButton> 컨트롤을 두 번 클릭 하 여 <xref:System.Windows.Forms.RadioButton.CheckedChanged> 이벤트 처리기를 만듭니다. 이벤트 처리기 <xref:System.Windows.Forms.RadioButton.CheckedChanged> 를 다음 코드로 바꿉니다.  
  
 [!code-csharp[WindowsFormsHostingWpfControl#4](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/WFHost/Form1.cs#4)]  
  
 애플리케이션을 빌드 및 실행합니다. WPF 복합 컨트롤에 대한 효과를 확인하려면 다른 라디오 단추를 클릭합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Visual Studio에서 XAML 디자인](/visualstudio/designers/designing-xaml-in-visual-studio)
- [연습: WPF에서 Windows Forms 복합 컨트롤 호스팅](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [연습: Windows Forms에서 3 차원 WPF 복합 컨트롤 호스팅](walkthrough-hosting-a-3-d-wpf-composite-control-in-windows-forms.md)
