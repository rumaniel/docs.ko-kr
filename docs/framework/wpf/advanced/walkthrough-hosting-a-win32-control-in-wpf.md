---
title: '연습: WPF에서 Win32 컨트롤 호스팅'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hosting Win32 control in WPF [WPF]
- Win32 code [WPF], WPF interoperation
ms.assetid: a676b1eb-fc55-4355-93ab-df840c41cea0
ms.openlocfilehash: cc27189afd2185d5f0a1eeacccf4c537dd3d9c2e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69917538"
---
# <a name="walkthrough-hosting-a-win32-control-in-wpf"></a>연습: WPF에서 Win32 컨트롤 호스팅
WPF (Windows Presentation Foundation)는 응용 프로그램을 만들기 위한 다양 한 환경을 제공 합니다. 그러나 Win32 코드에 상당한 투자를 한 경우 WPF 응용 프로그램에서 해당 코드를 완전히 다시 작성 하는 것 보다 최소한의 코드를 다시 사용 하는 것이 더 효과적일 수 있습니다. Wpf는 WPF 페이지에서 Win32 창을 호스팅하기 위한 간단한 메커니즘을 제공 합니다.  
  
 이 항목에서는 Win32 목록 상자 컨트롤을 호스트 하는 [WPF 샘플에서 Win32 ListBox 컨트롤](https://github.com/Microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/WPFHostingWin32Control)을 호스트 하는 응용 프로그램을 안내 합니다. 이 일반적인 절차를 확장 하 여 모든 Win32 창을 호스트할 수 있습니다.  

<a name="requirements"></a>   
## <a name="requirements"></a>요구 사항  
 이 항목에서는 WPF 및 Windows API 프로그래밍에 대 한 기본적인 지식이 있다고 가정 합니다. WPF 프로그래밍에 대 한 기본적인 소개는 [시작](../getting-started/index.md)을 참조 하세요. Windows API 프로그래밍에 대 한 소개는 주제에 대 한 다양 한 서적, 특히 Charles Petzold의 *프로그래밍 창* 을 참조 하세요.  
  
 이 항목과 함께 제공 되는 샘플은에서 C#구현 되었으므로 PInvoke (플랫폼 호출 서비스)를 사용 하 여 Windows API에 액세스 합니다. PInvoke를 사용 하는 데 도움이 되지만 반드시 필요한 것은 아닙니다.  
  
> [!NOTE]
> 이 항목에는 관련 샘플의 많은 코드 예제가 포함되어 있습니다. 그러나 가독성을 위해 전체 샘플 코드를 포함하지는 않습니다. [WPF 샘플에서 Win32 ListBox 컨트롤 호스팅](https://github.com/Microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/WPFHostingWin32Control)에서 전체 코드를 가져오거나 볼 수 있습니다.  
  
<a name="basic_procedure"></a>   
## <a name="the-basic-procedure"></a>기본 절차  
 이 섹션에서는 WPF 페이지에서 Win32 창을 호스트 하는 기본 절차를 간략하게 설명 합니다. 나머지 섹션에서는 각 단계를 자세히 설명합니다.  
  
 기본 호스팅 절차는 다음과 같습니다.  
  
1. 창을 호스트 하는 WPF 페이지를 구현 합니다. 한 가지 방법은 호스트 된 창 <xref:System.Windows.Controls.Border> 에 대 한 페이지의 섹션을 예약 하는 요소를 만드는 것입니다.  
  
2. 에서 <xref:System.Windows.Interop.HwndHost>상속 되는 컨트롤을 호스트 하는 클래스를 구현 합니다.  
  
3. 해당 클래스에서 <xref:System.Windows.Interop.HwndHost> 클래스 멤버 <xref:System.Windows.Interop.HwndHost.BuildWindowCore%2A>를 재정의 합니다.  
  
4. 호스팅된 창을 WPF 페이지가 포함 된 창의 자식으로 만듭니다. 기존 WPF 프로그래밍은 명시적으로 사용할 필요가 없지만 호스팅 페이지는 핸들 (HWND)이 포함 된 창입니다. <xref:System.Windows.Interop.HwndHost.BuildWindowCore%2A> 메서드의 매개 변수를 `hwndParent` 통해 페이지 HWND를 수신 합니다. 호스트된 창은 이 HWND의 자식으로 만들어야 합니다.  
  
5. 호스트 창을 만들었으면 호스트된 창의 HWND를 반환합니다. 하나 이상의 Win32 컨트롤을 호스트 하려는 경우 일반적으로 호스트 창을 HWND의 자식으로 만들고 컨트롤을 해당 호스트 창의 자식으로 만듭니다. 호스트 창에서 컨트롤을 래핑하여 WPF 페이지가 컨트롤에서 알림을 받을 수 있는 간단한 방법을 제공 하 고,이를 통해 HWND 경계에서 알림과 관련 된 몇 가지 특정 Win32 문제를 처리 합니다.  
  
6. 자식 컨트롤의 알림과 같이 호스트 창으로 전송되는 선택한 메시지를 처리합니다. 그런 경우 두 가지 방법이 있습니다.  
  
    - 호스팅 클래스에서 메시지를 처리 하려는 경우 <xref:System.Windows.Interop.HwndHost.WndProc%2A> <xref:System.Windows.Interop.HwndHost> 클래스의 메서드를 재정의 합니다.  
  
    - WPF에서 메시지를 처리 하도록 하려는 경우 코드 숨김으로 <xref:System.Windows.Interop.HwndHost> 클래스 <xref:System.Windows.Interop.HwndHost.MessageHook> 이벤트를 처리 합니다. 이 이벤트는 호스트된 창에서 받은 모든 메시지에 대해 발생합니다. 이 옵션을 선택 하는 경우에도를 <xref:System.Windows.Interop.HwndHost.WndProc%2A>재정의 해야 하지만 최소한의 구현만 필요 합니다.  
  
7. 의 <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A> <xref:System.Windows.Interop.HwndHost.WndProc%2A> 및 메서드를재정의합니다.<xref:System.Windows.Interop.HwndHost> 이러한 메서드를 재정의 하 여 <xref:System.Windows.Interop.HwndHost> 계약을 충족 해야 하지만 최소한의 구현만 제공 하면 됩니다.  
  
8. 코드를 작성 하는 파일에서 컨트롤 호스팅 클래스의 인스턴스를 만들고이를 창을 호스트 하기 위한 <xref:System.Windows.Controls.Border> 요소의 자식으로 만듭니다.  
  
9. 컨트롤에서 보내는 알림과 같이 자식 창에서 [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] 메시지를 보내고 처리 하 여 호스팅된 창과 통신 합니다.  
  
<a name="page_layout"></a>   
## <a name="implement-the-page-layout"></a>페이지 레이아웃 구현  
 ListBox 컨트롤을 호스트 하는 WPF 페이지의 레이아웃은 두 개의 영역으로 구성 됩니다. 페이지의 왼쪽은 Win32 컨트롤을 조작할 수 있는를 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 제공 하는 몇 가지 WPF 컨트롤을 호스팅합니다. 페이지의 오른쪽 위에는 호스트된 ListBox 컨트롤에 대한 사각형 영역이 있습니다.  
  
 이 레이아웃을 구현 하는 코드는 매우 간단 합니다. Root 요소 <xref:System.Windows.Controls.DockPanel> 는 두 개의 자식 요소가 있는입니다. 첫 번째 <xref:System.Windows.Controls.Border> 는 ListBox 컨트롤을 호스트 하는 요소입니다. 이 요소는 페이지의 오른쪽 위에 있는 200x200 정사각형을 사용합니다. 두 번째는 정보 <xref:System.Windows.Controls.StackPanel> 를 표시 하 고 노출 된 상호 운용성 속성을 설정 하 여 ListBox 컨트롤을 조작할 수 있도록 하는 WPF 컨트롤 집합을 포함 하는 요소입니다. 의 <xref:System.Windows.Controls.StackPanel>자식인 각 요소에 대 한 참조 자료는 아래 예제 코드에 나열 되어 있지만 여기서는 설명 하지 않습니다 (기본 항목을 참조 하세요.) .이 요소에 대 한 자세한 내용은 상호 운용 모델에는 이러한 모델이 필요 하지 않으며 샘플에 일부 상호 작용을 추가 하기 위해 제공 됩니다.  
  
 [!code-xaml[WPFHostingWin32Control#WPFUI](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/Page1.xaml#wpfui)]  
  
<a name="host_class"></a>   
## <a name="implement-a-class-to-host-the-microsoft-win32-control"></a>Microsoft Win32 컨트롤을 호스트하는 클래스 구현  
 이 샘플의 핵심은 ControlHost.cs 컨트롤을 실제로 호스트하는 클래스입니다. <xref:System.Windows.Interop.HwndHost>에서 상속받습니다. 생성자는 ListBox 컨트롤을 호스트 하는 <xref:System.Windows.Controls.Border> 요소의 높이 및 너비에 해당 하는 두 개의 매개 변수인 height 및 width를 사용 합니다. 이러한 값은 나중에 컨트롤의 크기가 <xref:System.Windows.Controls.Border> 요소와 일치 하는지 확인 하는 데 사용 됩니다.  
  
 [!code-csharp[WPFHostingWin32Control#ControlHostClass](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#controlhostclass)]
 [!code-vb[WPFHostingWin32Control#ControlHostClass](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#controlhostclass)]  
  
 또한 상수 집합도 있습니다. 이러한 상수는 주로 Winuser.h에서 가져오며 Win32 함수를 호출할 때 기본 이름을 사용할 수 있습니다.  
  
 [!code-csharp[WPFHostingWin32Control#ControlHostConstants](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#controlhostconstants)]
 [!code-vb[WPFHostingWin32Control#ControlHostConstants](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#controlhostconstants)]  
  
<a name="buildwindowcore"></a>   
### <a name="override-buildwindowcore-to-create-the-microsoft-win32-window"></a>BuildWindowCore를 재정의하여 Microsoft Win32 창 만들기  
 이 메서드를 재정의 하 여 페이지에서 호스트 되는 Win32 창을 만들고 창과 페이지 간에 연결을 설정 합니다. 이 샘플에서는 ListBox 컨트롤을 호스트하므로 두 개의 창을 만듭니다. 첫 번째는 WPF 페이지에서 실제로 호스팅하는 창입니다. ListBox 컨트롤은 해당 창의 자식으로 만듭니다.  
  
 이 방법은 컨트롤에서 알림을 받는 프로세스를 간소화하기 위해서 사용합니다. <xref:System.Windows.Interop.HwndHost> 클래스를 사용 하면 호스트 하는 창으로 전송 된 메시지를 처리할 수 있습니다. Win32 컨트롤을 직접 호스트 하는 경우 컨트롤의 내부 메시지 루프로 전송 되는 메시지를 받습니다. 컨트롤을 표시하고 메시지를 전송할 수 있지만 컨트롤이 해당 부모 창으로 전송된다는 알림은 받지 않습니다. 즉, 사용자가 컨트롤과 상호 작용하는 경우를 검색할 방법이 없습니다. 대신 호스트 창을 만들고 컨트롤을 해당 창의 자식으로 설정합니다. 이렇게 하면 컨트롤에서 전송한 알림을 포함하여 호스트 창에 대한 메시지를 처리할 수 있습니다. 호스트 창은 컨트롤에 대한 간단한 래퍼에 불과하므로 편의상 패키지를 ListBox 컨트롤이라고 합니다.  
  
<a name="create_the_window_and_listbox"></a>   
#### <a name="create-the-host-window-and-listbox-control"></a>호스트 창 및 ListBox 컨트롤 만들기  
 PInvoke를 사용 하 여 창 클래스를 만들고 등록 하는 등의 방법으로 컨트롤에 대 한 호스트 창을 만들 수 있습니다. 그러나 미리 정의된 "정적" 창 클래스를 사용하여 창을 만드는 방법이 훨씬 더 간단합니다. 이 방법은 컨트롤에서 알림을 받기 위해 필요한 창 프로시저를 제공하며 최소한의 코딩이 필요합니다.  
  
 컨트롤의 HWND는 읽기 전용 속성을 통해 노출되므로 호스트 페이지에서 컨트롤로 메시지를 전송하는 데 사용할 수 있습니다.  
  
 [!code-csharp[WPFHostingWin32Control#IntPtrProperty](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#intptrproperty)]
 [!code-vb[WPFHostingWin32Control#IntPtrProperty](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#intptrproperty)]  
  
 ListBox 컨트롤은 호스트 창의 자식으로 만듭니다. 두 창의 너비와 높이는 위에서 설명한 대로 생성자에 전달된 값으로 설정됩니다. 이렇게 하면 호스트 창과 컨트롤의 크기가 페이지에서 예약된 영역과 동일해집니다.  Windows를 만든 후 샘플은 호스트 창의 HWND를 <xref:System.Runtime.InteropServices.HandleRef> 포함 하는 개체를 반환 합니다.  
  
 [!code-csharp[WPFHostingWin32Control#BuildWindowCore](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#buildwindowcore)]
 [!code-vb[WPFHostingWin32Control#BuildWindowCore](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#buildwindowcore)]  
  
 [!code-csharp[WPFHostingWin32Control#BuildWindowCoreHelper](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#buildwindowcorehelper)]
 [!code-vb[WPFHostingWin32Control#BuildWindowCoreHelper](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#buildwindowcorehelper)]  
  
<a name="destroywindow_wndproc"></a>   
### <a name="implement-destroywindow-and-wndproc"></a>DestroyWindow 및 WndProc 구현  
 이외 <xref:System.Windows.Interop.HwndHost.BuildWindowCore%2A>에도의 <xref:System.Windows.Interop.HwndHost.WndProc%2A> <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A>및메서드 를 재정의 해야 합니다. <xref:System.Windows.Interop.HwndHost> 이 예제에서는 컨트롤에 대 한 메시지가 <xref:System.Windows.Interop.HwndHost.MessageHook> 처리기에 의해 처리 되므로 및 <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A> 의 <xref:System.Windows.Interop.HwndHost.WndProc%2A> 구현은 최소화 됩니다. 의 <xref:System.Windows.Interop.HwndHost.WndProc%2A>경우 메시지를 처리 하지 않고 `false` 0을 반환 함을 나타내려면를로 설정 `handled` 합니다. 의 <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A>경우 창을 제거 하기만 하면 됩니다.  
  
 [!code-csharp[WPFHostingWin32Control#WndProcDestroy](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#wndprocdestroy)]
 [!code-vb[WPFHostingWin32Control#WndProcDestroy](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#wndprocdestroy)]  
  
 [!code-csharp[WPFHostingWin32Control#WndProcDestroyHelper](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#wndprocdestroyhelper)]
 [!code-vb[WPFHostingWin32Control#WndProcDestroyHelper](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#wndprocdestroyhelper)]  
  
<a name="host_the_control"></a>   
## <a name="host-the-control-on-the-page"></a>페이지에서 컨트롤 호스트  
 페이지에서 컨트롤을 호스트 하려면 먼저 `ControlHost` 클래스의 새 인스턴스를 만듭니다. 컨트롤 (`ControlHostElement`)이 포함 된 border 요소의 높이와 너비를 `ControlHost` 생성자에 전달 합니다. 이렇게 하면 ListBox 크기가 정확하게 조정됩니다. 그런 다음 호스트 `ControlHost` <xref:System.Windows.Controls.Decorator.Child%2A> 의<xref:System.Windows.Controls.Border>속성에 개체를 할당 하 여 페이지에서 컨트롤을 호스팅합니다.  
  
 이 샘플은 컨트롤에서 메시지를 <xref:System.Windows.Interop.HwndHost.MessageHook> 수신 `ControlHost` 하는 처리기를의 이벤트에 연결 합니다. 이 이벤트는 호스트된 창으로 전송된 모든 메시지에 대해 발생됩니다. 이 경우 컨트롤의 알림을 포함하여 실제 ListBox 컨트롤을 래핑하는 창에 전송된 메시지입니다. 샘플에서는 SendMessage를 호출하여 컨트롤에서 정보를 가져오고 해당 내용을 수정합니다. 페이지가 컨트롤과 통신하는 방법에 대한 자세한 내용은 다음 섹션에서 설명합니다.  
  
> [!NOTE]
> SendMessage에 대 한 두 개의 PInvoke 선언이 있습니다. 이는 `wParam` 매개 변수를 사용 하 여 문자열을 전달 하 고 다른 하나는 정수를 전달 하기 때문에 필요 합니다. 데이터가 올바르게 마샬링되도록 하려면 각 시그니처에 대해 별도의 선언이 필요합니다.  
  
 [!code-csharp[WPFHostingWin32Control#HostWindowClass](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/Page1.xaml.cs#hostwindowclass)]
 [!code-vb[WPFHostingWin32Control#HostWindowClass](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/Page1.xaml.vb#hostwindowclass)]  
  
 [!code-csharp[WPFHostingWin32Control#ControlMsgFilterSendMessage](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/Page1.xaml.cs#controlmsgfiltersendmessage)]
 [!code-vb[WPFHostingWin32Control#ControlMsgFilterSendMessage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/Page1.xaml.vb#controlmsgfiltersendmessage)]  
  
<a name="communication"></a>   
## <a name="implement-communication-between-the-control-and-the-page"></a>컨트롤과 페이지 간의 통신 구현  
 Windows 메시지를 전송 하 여 컨트롤을 조작 합니다. 컨트롤은 사용자가 호스트 창에 알림을 보내 상호 작용할 때 알려 줍니다. [WPF에서 Win32 ListBox 컨트롤 호스팅](https://github.com/Microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/WPFHostingWin32Control) 샘플에는이 기능이 작동 하는 방법에 대 한 몇 가지 예제를 제공 하는 UI가 포함 되어 있습니다.  
  
- 목록에 항목을 추가합니다.  
  
- 선택한 항목을 목록에서 삭제합니다.  
  
- 현재 선택한 항목의 텍스트를 표시합니다.  
  
- 목록의 항목 수를 표시합니다.  
  
 또한 사용자는 기존 Win32 응용 프로그램과 마찬가지로 목록 상자에서 항목을 클릭 하 여 선택할 수 있습니다. 표시된 데이터는 사용자가 항목을 선택 또는 추가하여 목록 상자의 상태를 변경할 때마다 업데이트됩니다.  
  
 항목을 추가 하려면 목록 상자 [ `LB_ADDSTRING` 에 메시지](/windows/desktop/Controls/lb-addstring)를 보냅니다. 항목을 삭제 하려면를 [`LB_GETCURSEL`](/windows/desktop/Controls/lb-getcursel) 전송 하 여 현재 선택 항목의 인덱스를 가져온 [`LB_DELETESTRING`](/windows/desktop/Controls/lb-deletestring) 다음 항목을 삭제 합니다. 또한이 샘플은 [`LB_GETCOUNT`](/windows/desktop/Controls/lb-getcount)를 보내고 반환 된 값을 사용 하 여 항목 수를 표시 하는 표시를 업데이트 합니다. 이러한 두 인스턴스 [`SendMessage`](/windows/desktop/api/winuser/nf-winuser-sendmessage) 는 모두 이전 섹션에서 설명한 PInvoke 선언 중 하나를 사용 합니다.  
  
 [!code-csharp[WPFHostingWin32Control#AppendDeleteText](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/Page1.xaml.cs#appenddeletetext)]
 [!code-vb[WPFHostingWin32Control#AppendDeleteText](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/Page1.xaml.vb#appenddeletetext)]  
  
 사용자가 항목을 선택 하거나 선택 항목을 변경 하면 컨트롤은 페이지에 대 한 <xref:System.Windows.Interop.HwndHost.MessageHook> 이벤트를 발생 시키는 [ `WM_COMMAND` 메시지](/windows/desktop/menurc/wm-command)를 전송 하 여 호스트 창에 알립니다. 처리기는 호스트 창의 주 창 프로시저와 같은 정보를 수신합니다. 또한 부울 값 `handled`에 대 한 참조를 전달 합니다. 메시지를 `handled` 처리 `true` 했으며 추가 처리가 필요 하지 않음을 나타내려면를로 설정 합니다.  
  
 [`WM_COMMAND`](/windows/desktop/menurc/wm-command)은 다양 한 이유로 전송 되므로 알림 ID를 검사 하 여 처리할 이벤트 인지 여부를 확인 해야 합니다. ID는 `wParam` 매개 변수의 상위 단어에 포함 되어 있습니다. 이 샘플에서는 비트 연산자를 사용 하 여 ID를 추출 합니다. 사용자가 선택을 변경 하거나 변경 하는 경우 ID [`LBN_SELCHANGE`](/windows/desktop/Controls/lbn-selchange)는가 됩니다.  
  
 이 [`LBN_SELCHANGE`](/windows/desktop/Controls/lbn-selchange) 수신 되 면 샘플은 [ `LB_GETCURSEL` ](/windows/desktop/Controls/lb-getcursel)컨트롤에 메시지를 전송 하 여 선택한 항목의 인덱스를 가져옵니다. 텍스트를 가져오려면 먼저를 <xref:System.Text.StringBuilder>만듭니다. 그런 다음 컨트롤 [ `LB_GETTEXT` 을 메시지](/windows/desktop/Controls/lb-gettext)에 보냅니다. 빈 <xref:System.Text.StringBuilder> 개체`wParam` 를 매개 변수로 전달 합니다. 가 [`SendMessage`](/windows/desktop/api/winuser/nf-winuser-sendmessage) 반환 되 면 <xref:System.Text.StringBuilder> 에는 선택한 항목의 텍스트가 포함 됩니다. 이를 [`SendMessage`](/windows/desktop/api/winuser/nf-winuser-sendmessage) 사용 하려면 아직 또 다른 PInvoke 선언이 필요 합니다.  
  
 마지막으로를 `handled` `true` 로 설정 하 여 메시지가 처리 되었음을 표시 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Interop.HwndHost>
- [WPF 및 Win32 상호 운용성](wpf-and-win32-interoperation.md)
- [연습: 내 첫 WPF 데스크톱 애플리케이션](../getting-started/walkthrough-my-first-wpf-desktop-application.md)
