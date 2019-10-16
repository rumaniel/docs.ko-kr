---
title: '연습: WPF에서 ActiveX 컨트롤 호스팅'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ActiveX controls [WPF interoperability]
- hosting ActiveX controls [WPF]
ms.assetid: 1931d292-0dd1-434f-963c-dcda7638d75a
ms.openlocfilehash: 0181093de1c40889110ab7eae75a3847a17845a9
ms.sourcegitcommit: 83ecdf731dc1920bca31f017b1556c917aafd7a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67859943"
---
# <a name="walkthrough-hosting-an-activex-control-in-wpf"></a>연습: WPF에서 ActiveX 컨트롤 호스팅
브라우저를 사용 하 여 향상 된 상호 작용을 사용 하도록 설정 하려면 Microsoft ActiveX 컨트롤에서 사용할 수 있습니다 프로그램 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-기반 응용 프로그램입니다. 이 연습에서는 호스팅하는 방법을 보여 줍니다.는 [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] 의 컨트롤로 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 페이지입니다.

 이 연습에서 설명하는 작업은 다음과 같습니다.

- 프로젝트 만들기.

- ActiveX 컨트롤을 만드는 중입니다.

- WPF 페이지에서 ActiveX 컨트롤 호스팅.

 Microsoft ActiveX 컨트롤을 사용 하는 방법을 이해 하 게이 연습을 완료 하는 경우에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-기반 응용 프로그램입니다.

## <a name="prerequisites"></a>필수 구성 요소
 이 연습을 완료하려면 다음 구성 요소가 필요합니다.

- [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] Visual Studio를 설치한 컴퓨터에 설치 합니다.

- Visual Studio 2010

## <a name="creating-the-project"></a>프로젝트 만들기

### <a name="to-create-and-set-up-the-project"></a>프로젝트를 만들고 설정하려면

1. 이라는 WPF 응용 프로그램 프로젝트를 만듭니다 `HostingAxInWpf`합니다.

2. Windows Forms 컨트롤 라이브러리 프로젝트를 솔루션에 추가 하 고 프로젝트 이름을 `WmpAxLib`입니다.

3. WmpAxLib 프로젝트에서 wmp.dll 라고 하는 Windows Media Player 어셈블리에 대 한 참조를 추가 합니다.

4. 엽니다는 **도구 상자**합니다.

5. 마우스 오른쪽 단추로 클릭 합니다 **도구 상자**를 클릭 하 고 **선택 항목**합니다.

6. 클릭 합니다 **COM 구성 요소** 탭을 선택 합니다 **Windows Media Player** 컨트롤을 클릭 **확인**합니다.

     Windows Media Player 컨트롤이 추가 되는 **도구 상자**합니다.

7. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 **UserControl1** 파일을 선택한 다음 클릭 **이름 바꾸기**합니다.

8. 이름을 변경할 `WmpAxControl.vb` 또는 `WmpAxControl.cs`언어에 따라 합니다.

9. 모든 참조 이름을 묻는 클릭 **예**합니다.

## <a name="creating-the-activex-control"></a>ActiveX 컨트롤 만들기
 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 자동으로 생성 된 <xref:System.Windows.Forms.AxHost> 컨트롤을 디자인 화면에 추가 되 면 Microsoft ActiveX 컨트롤 래퍼 클래스입니다. 다음 절차는 AxInterop.WMPLib.dll 이라는 관리 되는 어셈블리를 만듭니다.

### <a name="to-create-the-activex-control"></a>ActiveX 컨트롤을 만들려면

1. Windows Forms 디자이너에서 WmpAxControl.vb 또는 WmpAxControl.cs를 엽니다.

2. **도구 상자**, Windows Media Player 컨트롤이 디자인 화면에 추가 합니다.

3. 속성 창에서 Windows Media Player 컨트롤의 값을 설정 <xref:System.Windows.Forms.Control.Dock%2A> 속성을 <xref:System.Windows.Forms.DockStyle.Fill>입니다.

4. WmpAxLib 컨트롤 라이브러리 프로젝트를 빌드하십시오.

## <a name="hosting-the-activex-control-on-a-wpf-page"></a>WPF 페이지에서 ActiveX 컨트롤 호스팅

### <a name="to-host-the-activex-control"></a>ActiveX 컨트롤을 호스트 하려면

1. HostingAxInWpf 프로젝트에서 생성된 된 ActiveX 상호 운용성 어셈블리에 대 한 참조를 추가 합니다.

     이 어셈블리 AxInterop.WMPLib.dll 이름이 고은 Windows Media Player 컨트롤이 가져올 때 WmpAxLib 프로젝트의 디버그 폴더에 추가 합니다.

2. WindowsFormsIntegration.dll 이라는 WindowsFormsIntegration 어셈블리에 대 한 참조를 추가 합니다.

3. 에 대 한 참조를 추가 합니다 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] System.Windows.Forms.dll 라고 하는 어셈블리입니다.

4. WPF Designer의 MainWindow.xaml을 엽니다.

5. 이름 합니다 <xref:System.Windows.Controls.Grid> 요소 `grid1`합니다.

     [!code-xaml[HostingAxInWpf#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingAxInWpf/CSharp/HostingAxInWpf/window1.xaml#1)]

6. 디자인 뷰 또는 XAML 뷰에서 선택 된 <xref:System.Windows.Window> 요소입니다.

7. 속성 창에서 클릭 합니다 **이벤트** 탭 합니다.

8. 두 번 클릭 하 여 <xref:System.Windows.FrameworkElement.Loaded> 이벤트입니다.

9. 처리 하는 다음 코드를 삽입 합니다 <xref:System.Windows.FrameworkElement.Loaded> 이벤트입니다.

     이 코드의 인스턴스를 만듭니다는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 제어 하 고 인스턴스를 추가 합니다 `AxWindowsMediaPlayer` 해당 자식 컨트롤입니다.

     [!code-csharp[HostingAxInWpf#11](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingAxInWpf/CSharp/HostingAxInWpf/window1.xaml.cs#11)]
     [!code-vb[HostingAxInWpf#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HostingAxInWpf/VisualBasic/HostingAxInWpf/window1.xaml.vb#11)]  
  
10. F5 키를 눌러 애플리케이션을 빌드하고 실행합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Visual Studio에서 XAML 디자인](/visualstudio/designers/designing-xaml-in-visual-studio)
- [연습: WPF에서 Windows Forms 복합 컨트롤 호스팅](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [연습: Windows Forms에서 WPF 복합 컨트롤 호스팅](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
