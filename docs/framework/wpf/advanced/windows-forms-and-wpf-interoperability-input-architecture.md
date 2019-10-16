---
title: Windows Forms 및 WPF 상호 운용성 입력 아키텍처
ms.date: 03/30/2017
helpviewer_keywords:
- input architecture [WPF interoperability]
- messages [WPF]
- Windows Forms [WPF], interoperability with
- Windows Forms [WPF], WPF interoperation
- interoperability [WPF], Windows Forms
- modeless forms [WPF]
- ElementHost keyboard and messages [WPF]
- keyboard interoperation [WPF]
- WindowsFormsHost keyboard and messages [WPF]
- modeless dialog boxes [WPF]
ms.assetid: 0eb6f137-f088-4c5e-9e37-f96afd28f235
ms.openlocfilehash: 10c3ced3bc69f12c107b8d49139f829fab4e312a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662217"
---
# <a name="windows-forms-and-wpf-interoperability-input-architecture"></a>Windows Forms 및 WPF 상호 운용성 입력 아키텍처
간에 상호 운용 합니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 및 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 두 기술 모두에서 해당 하는 키보드 입력된 처리 해야 합니다. 이 항목에서는 이러한 기술을 키보드 및 하이브리드 응용 프로그램에 원활한 상호 운용성을 사용 하도록 설정 하기 위해 메시지 처리를 구현 하는 방법을 설명 합니다.  
  
 이 항목에는 다음과 같은 하위 단원이 포함되어 있습니다.  
  
- 모덜리스 폼 및 대화 상자  
  
- WindowsFormsHost 키보드 및 메시지 처리  
  
- ElementHost 키보드 및 메시지 처리  
  
## <a name="modeless-forms-and-dialog-boxes"></a>모덜리스 폼 및 대화 상자  
 호출을 <xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A> 메서드를 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 에서 모덜리스 폼 또는 대화 상자를 열려면 요소를 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-기반 응용 프로그램입니다.  
  
 호출을 <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A> 메서드를 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤을 모덜리스를 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 페이지에서 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]-기반 응용 프로그램.  
  
## <a name="windowsformshost-keyboard-and-message-processing"></a>WindowsFormsHost 키보드 및 메시지 처리  
 호스팅되는 경우는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-기반 응용 프로그램에서 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 키보드 및 메시지 처리는 다음으로 이루어집니다.  
  
- <xref:System.Windows.Forms.Integration.WindowsFormsHost> 에서 메시지를 획득 하는 클래스를 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 에서 구현 하는 메시지 루프에는 <xref:System.Windows.Interop.ComponentDispatcher> 클래스.  
  
- 합니다 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 서로게이트 클래스를 만듭니다 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 일반 되도록 메시지 루프 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 키보드 처리가 발생 합니다.  
  
- 합니다 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 클래스가 구현 하는 <xref:System.Windows.Interop.IKeyboardInputSink> 인터페이스를 사용 하 여 포커스 관리 조정 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]합니다.  
  
- <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤 자체를 등록 하 고 해당 메시지 루프를 시작 합니다.  
  
 다음 섹션에서는 이러한 부분 과정을 자세히 설명합니다.  
  
### <a name="acquiring-messages-from-the-wpf-message-loop"></a>WPF 메시지 루프에서 메시지를 획득합니다.  
 합니다 <xref:System.Windows.Interop.ComponentDispatcher> 클래스 구현에 대 한 메시지 루프 관리자 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]합니다. 합니다 <xref:System.Windows.Interop.ComponentDispatcher> 클래스를 제공 하기 전에 메시지를 필터링 하려면 외부 클라이언트를 사용 하도록 설정 하려면 후크 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 처리 합니다.  
  
 상호 운용성 구현 처리 합니다 <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType> 수 있도록 하는 경우 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 하기 전에 메시지를 처리 하는 컨트롤 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤입니다.  
  
### <a name="surrogate-windows-forms-message-loop"></a>서로게이트 Windows Forms 메시지 루프  
 기본적으로 <xref:System.Windows.Forms.Application?displayProperty=nameWithType> 에 대 한 기본 메시지 루프를 포함 하는 클래스 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 응용 프로그램입니다. 상호 운용성을 하는 동안는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 메시지 루프는 메시지를 처리 하지 않습니다. 따라서이 논리를 재현해 야 합니다. 에 대 한 처리기를 <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType> 이벤트에는 다음 단계를 수행 합니다.  
  
1. 사용 하 여 메시지 필터는 <xref:System.Windows.Forms.IMessageFilter> 인터페이스입니다.  
  
2. <xref:System.Windows.Forms.Control.PreProcessMessage%2A?displayProperty=nameWithType> 메서드를 호출합니다.  
  
3. 변환 하 고 필요한 경우 메시지를 디스패치합니다.  
  
4. 메시지를 처리 하는 다른 컨트롤이 없는 경우에 호스팅 컨트롤에 메시지를 전달 합니다.  
  
### <a name="ikeyboardinputsink-implementation"></a>IKeyboardInputSink 구현  
 서로게이트 메시지 루프 바로 관리를 처리합니다. 따라서 합니다 <xref:System.Windows.Interop.IKeyboardInputSink.TabInto%2A?displayProperty=nameWithType> 메서드는 유일한 <xref:System.Windows.Interop.IKeyboardInputSink> 에서 구현 되어야 하는 멤버를 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 클래스입니다.  
  
 기본적으로 <xref:System.Windows.Interop.HwndHost> 반환 클래스 `false` 에 대 한 해당 <xref:System.Windows.Interop.HwndHost.System%23Windows%23Interop%23IKeyboardInputSink%23TabInto%2A> 구현 합니다. 탭을 사용 하는 것이 이렇게를 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤을 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 제어 합니다.  
  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 구현의 <xref:System.Windows.Interop.IKeyboardInputSink.TabInto%2A?displayProperty=nameWithType> 메서드는 다음 단계를 수행 합니다.  
  
1. 찾은 첫 번째 또는 마지막 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤에 포함 되는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤과 포커스를 받을 수 있습니다. 컨트롤 선택 통과 정보에 따라 달라 집니다.  
  
2. 컨트롤에 포커스를 설정 하 고 반환 `true`합니다.  
  
3. 컨트롤이 포커스를 받을 수 있습니다 하는 경우 반환 `false`합니다.  
  
### <a name="windowsformshost-registration"></a>WindowsFormsHost 등록  
 에 대 한 창 핸들을 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤을 만든를 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 제어 메시지 루프에 대 한 존재 여부에 따라 등록 하는 내부 정적 메서드를 호출 합니다.  
  
 등록 하는 동안는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 제어 메시지 루프를 검사 합니다. 메시지 루프 시작 되지 않은 경우는 <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType> 이벤트 처리기가 만들어집니다. 메시지 루프 때 중인 것으로 간주 되는 <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType> 이벤트 처리기가 연결 합니다.  
  
 창 핸들을 소멸 될 때를 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 컨트롤 등록에서 자신을 제거 합니다.  
  
## <a name="elementhost-keyboard-and-message-processing"></a>ElementHost 키보드 및 메시지 처리  
 호스팅되는 경우는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 응용 프로그램을 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 키보드 및 메시지 처리는 다음으로 이루어집니다.  
  
- <xref:System.Windows.Interop.HwndSource>하십시오 <xref:System.Windows.Interop.IKeyboardInputSink>, 및 <xref:System.Windows.Interop.IKeyboardInputSite> 인터페이스 구현.  
  
- Tab 키와 화살표 키입니다.  
  
- 명령 키 및 대화 상자 키입니다.  
  
- [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 액셀러레이터 처리 합니다.  
  
 다음 섹션에서는 이러한 부분을 자세히 설명합니다.  
  
### <a name="interface-implementations"></a>인터페이스 구현  
 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)], 키보드 메시지를 포커스가 있는 컨트롤의 창 핸들에 라우팅됩니다. <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤 호스팅된 요소에 이러한 메시지가 라우팅됩니다. 이 수행 하는 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤은 제공는 <xref:System.Windows.Interop.HwndSource> 인스턴스. 경우는 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤에 포커스가 합니다 <xref:System.Windows.Interop.HwndSource> 인스턴스 경로 입력 하 여 처리할 수 있도록 하는 대부분의 키보드를 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.InputManager> 클래스입니다.  
  
 합니다 <xref:System.Windows.Interop.HwndSource> 클래스가 구현 하는 <xref:System.Windows.Interop.IKeyboardInputSink> 및 <xref:System.Windows.Interop.IKeyboardInputSite> 인터페이스입니다.  
  
 키보드 상호 운용 구현에서는 <xref:System.Windows.Interop.IKeyboardInputSite.OnNoMoreTabStops%2A> 방법 핸들 TAB 키와 화살표 키 호스 티 드 요소에서 포커스를 이동 하는 입력 합니다.  
  
### <a name="tabbing-and-arrow-keys"></a>Tabbing 및 화살표 키  
 합니다 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 선택 논리에 매핑되는 <xref:System.Windows.Interop.HwndSource.System%23Windows%23Interop%23IKeyboardInputSink%23TabInto%2A> 및 <xref:System.Windows.Interop.IKeyboardInputSite.OnNoMoreTabStops%2A> 탭 및 화살표를 구현 하는 방법을 탐색 키입니다. 재정의 <xref:System.Windows.Forms.Integration.ElementHost.Select%2A> 메서드가이 매핑을 수행 합니다.  
  
### <a name="command-keys-and-dialog-box-keys"></a>키와 대화 상자 키 명령  
 부여할 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 명령 키 및 대화 상자 키를 처리 하는 데 첫 번째 기회 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 에 연결 된 명령 전처리는 <xref:System.Windows.Interop.IKeyboardInputSink.TranslateAccelerator%2A> 메서드. 재정의 <xref:System.Windows.Forms.Control.ProcessCmdKey%2A?displayProperty=nameWithType> 메서드는 두 기술을 연결 합니다.  
  
 사용 하 여는 <xref:System.Windows.Interop.IKeyboardInputSink.TranslateAccelerator%2A> 메서드를 호스 티 드 요소 WM_KEYDOWN, WM_KEYUP, WM_SYSKEYDOWN, WM_SYSKEYUP, 탭, ENTER, ESC 키를 및 화살표 키와 같은 명령 키를 포함 하 여 등의 모든 키 메시지를 처리할 수 있습니다. 키 메시지를 처리 되지 않은 경우 보내는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 처리에 대 한 상위 계층입니다.  
  
### <a name="accelerator-processing"></a>액셀러레이터 키 처리  
 가속기를 올바르게 처리 하는 데 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 액셀러레이터 처리에 연결 해야 합니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.AccessKeyManager> 클래스입니다. 또한 모든 WM_CHAR 메시지 요소를 호스트 올바르게 라우팅할 수 있어야 합니다.  
  
 때문에 기본값 <xref:System.Windows.Interop.HwndSource> 구현의 합니다 <xref:System.Windows.Interop.IKeyboardInputSink.TranslateChar%2A> 메서드가 반환 되는 `false`, WM_CHAR 메시지를 다음 논리를 사용 하 여 처리:  
  
- <xref:System.Windows.Forms.Control.IsInputChar%2A?displayProperty=nameWithType> 모든 WM_CHAR 메시지는 호스트 된 요소에 전달 되도록 확인 메서드를 재정의 합니다.  
  
- ALT 키를 누르는 경우 메시지 WM_SYSCHAR입니다. [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 통해이 메시지를 전처리 하지 않고 않습니다는 <xref:System.Windows.Forms.Control.IsInputChar%2A> 메서드. 따라서 합니다 <xref:System.Windows.Forms.Control.ProcessMnemonic%2A> 메서드를 재정의 쿼리에 합니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.AccessKeyManager> 등록된 된 액셀러레이터 키에 대 한 합니다. 등록된 된 액셀러레이터 키가 있으면 <xref:System.Windows.Input.AccessKeyManager> 처리 합니다.  
  
- ALT 키를 누르지 경우 합니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.InputManager> 클래스 처리 되지 않은 입력을 처리 합니다. 입력이 액셀러레이터는 <xref:System.Windows.Input.AccessKeyManager> 처리 합니다. <xref:System.Windows.Input.InputManager.PostProcessInput> 처리 되지 않은 WM_CHAR 메시지에 대 한 이벤트를 처리 합니다.  
  
 사용자가 ALT 키를 누르면 accelerator에 대 한 시각적 정보 전체 폼에 표시 됩니다. 이 동작을 지 원하는 모든 <xref:System.Windows.Forms.Integration.ElementHost> 활성 폼에서 컨트롤에 관계 없이 컨트롤에 포커스가 WM_SYSKEYDOWN 메시지를 수신 합니다.  
  
 메시지에만 보내집니다 <xref:System.Windows.Forms.Integration.ElementHost> 활성 폼에서 컨트롤입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A>
- <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A>
- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [연습: WPF에서 Windows Forms 복합 컨트롤 호스팅](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [연습: Windows Forms에서 WPF 복합 컨트롤 호스팅](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
- [WPF 및 Win32 상호 운용성](wpf-and-win32-interoperation.md)
