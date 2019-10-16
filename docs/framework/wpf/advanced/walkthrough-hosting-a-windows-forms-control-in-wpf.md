---
title: '연습: WPF에서 Windows Forms 컨트롤 호스팅'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hosting Windows Forms control in WPF [WPF]
ms.assetid: 9cb88415-39b0-4c46-80c4-ff325b674286
ms.openlocfilehash: af5a0d58e789e609a25aa828493a3b0722cc83e1
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64605468"
---
# <a name="walkthrough-hosting-a-windows-forms-control-in-wpf"></a>연습: WPF에서 Windows Forms 컨트롤 호스팅

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 풍부한 기능 집합이 있는 많은 컨트롤을 제공합니다. 그러나 사용 하려는 경우에 따라 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 페이지입니다. 예를 들어, 기존에 상당한 투자를 해야 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤 또는 있습니다 있을 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 고유한 기능을 제공 하는 컨트롤입니다.

이 연습에서는 호스트 하는 방법을 보여 줍니다.는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] <xref:System.Windows.Forms.MaskedTextBox?displayProperty=nameWithType> 컨트롤을 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 코드를 사용 하 여 페이지입니다.

이 연습에 나와 있는 작업의 전체 코드 목록은 참조 하세요 [WPF 샘플에서 Windows Forms 컨트롤 호스팅](https://go.microsoft.com/fwlink/?LinkID=160057)합니다.

## <a name="prerequisites"></a>전제 조건

이 연습을 완료하려면 Visual Studio가 필요합니다.

## <a name="hosting-the-windows-forms-control"></a>Windows Forms 컨트롤 호스팅

### <a name="to-host-the-maskedtextbox-control"></a>MaskedTextBox 컨트롤을 호스트하려면

1. 이라는 WPF 응용 프로그램 프로젝트를 만듭니다 `HostingWfInWpf`합니다.

2. 다음 어셈블리에 대한 참조를 추가합니다.

    - WindowsFormsIntegration

    - System.Windows.Forms

3. MainWindow.xaml을 엽니다는 [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]합니다.

4. 이름 합니다 <xref:System.Windows.Controls.Grid> 요소 `grid1`합니다.

     [!code-xaml[HostingWfInWPF#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWfInWPF/CSharp/HostingWfInWPF/Window1.xaml#1)]

5. 디자인 뷰 또는 XAML 뷰에서 선택 된 <xref:System.Windows.Window> 요소입니다.

6. 속성 창에서 클릭 합니다 **이벤트** 탭 합니다.

7. 두 번 클릭 하 여 <xref:System.Windows.FrameworkElement.Loaded> 이벤트입니다.

8. 처리 하는 다음 코드를 삽입 합니다 <xref:System.Windows.FrameworkElement.Loaded> 이벤트입니다.

     [!code-csharp[HostingWfInWPF#10](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWfInWPF/CSharp/HostingWfInWPF/Window1.xaml.cs#10)]
     [!code-vb[HostingWfInWPF#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWfInWPF/VisualBasic/HostingWfInWpf/Window1.xaml.vb#10)]

9. 파일의 맨 위에 있는 다음 코드를 추가 `Imports` 또는 `using` 문입니다.

     [!code-csharp[HostingWfInWPF#11](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWfInWPF/CSharp/HostingWfInWPF/Window1.xaml.cs#11)]
     [!code-vb[HostingWfInWPF#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWfInWPF/VisualBasic/HostingWfInWpf/Window1.xaml.vb#11)]

10. **F5** 키를 눌러 응용 프로그램을 빌드하고 실행합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Visual Studio에서 XAML 디자인](/visualstudio/designers/designing-xaml-in-visual-studio)
- [연습: XAML을 사용 하 여 WPF에서 Windows Forms 컨트롤 호스팅](walkthrough-hosting-a-windows-forms-control-in-wpf-by-using-xaml.md)
- [연습: WPF에서 Windows Forms 복합 컨트롤 호스팅](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [연습: Windows Forms에서 WPF 복합 컨트롤 호스팅](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
- [Windows Forms 컨트롤 및 해당 WPF 컨트롤](windows-forms-controls-and-equivalent-wpf-controls.md)
- [WPF에서 Windows Forms 컨트롤 호스팅 샘플](https://go.microsoft.com/fwlink/?LinkID=160057)
