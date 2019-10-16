---
title: 입력 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- commands [WPF]
- input [WPF], overview
- keyboard focus [WPF]
- keyboard input [WPF]
- touch events [WPF]
- event routing [WPF]
- touch input [WPF]
- manipulation [WPF]
- logical focus [WPF]
- stylus input [WPF]
- text input [WPF]
- input events [WPF], handling
- WPF [WPF], input overview
- manipulation events [WPF]
- mouse input [WPF]
- mouse capture [WPF]
- focus [WPF]
- mouse position [WPF]
ms.assetid: ee5258b7-6567-415a-9b1c-c0cbe46e79ef
ms.openlocfilehash: a90c74542c1a6604ed27d37f882385b67402dd92
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005024"
---
# <a name="input-overview"></a>입력 개요
<a name="introduction"></a>@No__t-1 하위 시스템은 마우스, 키보드, 터치 및 스타일러스를 비롯 한 다양 한 장치에서 입력을 얻기 위한 강력한 API를 제공 합니다. 이 항목에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]가 제공하는 서비스에 대해 설명하고 입력 시스템의 아키텍처를 살펴봅니다.

<a name="input_api"></a>
## <a name="input-api"></a>입력 API
 기본 입력 API 노출은 기본 요소 클래스인 <xref:System.Windows.UIElement>, <xref:System.Windows.ContentElement>, <xref:System.Windows.FrameworkElement> 및 <xref:System.Windows.FrameworkContentElement>에 있습니다.  기본 요소에 대한 자세한 내용은 [기본 요소 개요](base-elements-overview.md)를 참조하세요.  이러한 클래스는 키 누르기, 마우스 단추, 마우스 휠, 마우스 이동, 포커스 관리, 마우스 캡처 등과 관련된 입력 이벤트를 위한 기능을 제공합니다. 입력 아키텍처는 모든 입력 이벤트를 서비스로 처리 하는 대신 기본 요소에 배치 하 여 입력 이벤트를 UI의 특정 개체에서 소싱 하 고 둘 이상의 요소에 opp가 있는 이벤트 라우팅 체계를 지원할 수 있도록 합니다. 입력 이벤트를 처리할 수 있습니다. 대부분의 입력 이벤트에는 연결된 이벤트 쌍이 있습니다.  예를 들어 key down 이벤트는 <xref:System.Windows.Input.Keyboard.KeyDown> 및 <xref:System.Windows.Input.Keyboard.PreviewKeyDown> 이벤트와 연결 됩니다.  이벤트마다 이벤트가 대상 요소로 라우트되는 방법이 다릅니다.  미리 보기 이벤트는 요소 트리의 루트 요소에서 대상 요소로 터널링됩니다.  버블링 이벤트는 대상 요소에서 루트 요소로 버블링됩니다.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 이벤트 라우팅에 대한 자세한 내용은 이 개요 항목의 이후 단원 및 [라우트된 이벤트 개요](routed-events-overview.md)에서 자세히 설명합니다.

### <a name="keyboard-and-mouse-classes"></a>키보드 및 마우스 클래스
 기본 요소 클래스의 입력 API 외에도 <xref:System.Windows.Input.Keyboard> 클래스 및 <xref:System.Windows.Input.Mouse> 클래스는 키보드 및 마우스 입력 작업을 위한 추가 API를 제공 합니다.

 @No__t-0 클래스에 대 한 입력 API의 예로는 <xref:System.Windows.Input.Keyboard.Modifiers%2A> 속성이 있습니다 .이 속성은 현재 누른 <xref:System.Windows.Input.ModifierKeys>를 반환 하 고 지정 된 키를 눌렀는지 여부를 결정 하는 <xref:System.Windows.Input.Keyboard.IsKeyDown%2A> 메서드를 반환 합니다.

 다음 예제에서는 <xref:System.Windows.Input.Keyboard.GetKeyStates%2A> 메서드를 사용 하 여 <xref:System.Windows.Input.Key>이 눌러져 있는지 여부를 확인 합니다.

 [!code-csharp[keyargssnippetsample#KeyEventArgsKeyBoardGetKeyStates](~/samples/snippets/csharp/VS_Snippets_Wpf/KeyArgsSnippetSample/CSharp/Window1.xaml.cs#keyeventargskeyboardgetkeystates)]
 [!code-vb[keyargssnippetsample#KeyEventArgsKeyBoardGetKeyStates](~/samples/snippets/visualbasic/VS_Snippets_Wpf/KeyArgsSnippetSample/visualbasic/window1.xaml.vb#keyeventargskeyboardgetkeystates)]

 @No__t-0 클래스에 대 한 입력 API의 예로는 마우스 가운데 단추의 상태를 가져오는-1이 @no__t, 마우스 포인터가 현재 있는 요소를 가져오는 <xref:System.Windows.Input.Mouse.DirectlyOver%2A>가 있습니다.

 다음 예에서는 마우스의 <xref:System.Windows.Input.Mouse.LeftButton%2A>이 <xref:System.Windows.Input.MouseButtonState.Pressed> 상태 인지 여부를 확인 합니다.

 [!code-csharp[mouserelatedsnippets#MouseRelatedSnippetsGetLeftButtonMouse](~/samples/snippets/csharp/VS_Snippets_Wpf/MouseRelatedSnippets/CSharp/Window1.xaml.cs#mouserelatedsnippetsgetleftbuttonmouse)]
 [!code-vb[mouserelatedsnippets#MouseRelatedSnippetsGetLeftButtonMouse](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MouseRelatedSnippets/visualbasic/window1.xaml.vb#mouserelatedsnippetsgetleftbuttonmouse)]

 @No__t-0 및 <xref:System.Windows.Input.Keyboard> 클래스는이 개요에서 자세히 설명 합니다.

### <a name="stylus-input"></a>스타일러스 입력
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]은 <xref:System.Windows.Input.Stylus>에 대 한 통합 지원을 제공 합니다.  @No__t-0은 태블릿 PC에서 널리 사용 되는 펜 입력입니다.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램은 마우스 API를 사용 하 여 스타일러스를 마우스로 처리할 수 있지만 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]은 키보드 및 마우스와 유사한 모델을 사용 하는 스타일러스 장치 추상화도 노출 합니다.  모든 스타일러스 관련 Api는 "스타일러스" 라는 단어를 포함 합니다.

 스타일러스는 마우스처럼 동작할 수 있으므로 마우스 입력만 지원하는 애플리케이션도 약간의 스타일러스 지원을 자동으로 받을 수 있습니다. 이러한 방식으로 스타일러스를 사용하는 경우 애플리케이션은 알맞은 스타일러스 이벤트를 처리한 다음 해당 마우스 이벤트를 처리할 수 있게 됩니다. 뿐만 아니라 스타일러스 디바이스 추상화를 통해 잉크 입력과 같은 높은 수준의 서비스도 사용할 수 있습니다.  잉크 입력에 대한 자세한 내용은 [잉크 시작](getting-started-with-ink.md)을 참조하세요.

<a name="event_routing"></a>
## <a name="event-routing"></a>이벤트 라우팅
 @No__t-0은 요소 트리를 형성 하는 다른 요소를 콘텐츠 모델의 자식 요소로 포함할 수 있습니다.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 부모 요소는 이벤트를 처리하여 해당 자식 요소 또는 다른 하위 요소를 대상으로 하는 입력에 참가할 수 있습니다. 이는 특히 더 작은 컨트롤에서 컨트롤을 빌드하는 “컨트롤 컴퍼지션” 또는 “합치기”라고 하는 프로세스에 유용합니다. 요소 트리 및 요소 트리와 이벤트 경로가 서로 어떻게 관련되는지에 대한 자세한 내용은 [WPF의 트리](trees-in-wpf.md)를 참조하세요.

 이벤트 라우팅은 이벤트를 여러 요소로 전달함으로써 경로 상의 특정 개체나 요소가 다른 요소에서 발생시킨 이벤트에 대해 이벤트 처리를 통해 의미 있는 응답을 제공할 수 있도록 하는 프로세스입니다.  라우트된 이벤트는 직접, 버블링, 터널링이라는 세 가지 라우팅 메커니즘 중 하나를 사용합니다.  직접 라우팅에서는 소스 요소만 이벤트에 대한 알림을 받으며 이벤트가 다른 요소로 라우트되지 않습니다. 그러나 직접 라우트된 이벤트는 표준 CLR 이벤트와는 달리 라우트된 이벤트에 대해서만 제공 되는 몇 가지 추가 기능을 제공 합니다. 버블링은 먼저 이벤트에 대해 이벤트를 발생시킨 요소에 알린 다음 부모 요소 등에 알리는 순서로 요소 트리의 위쪽으로 작동합니다.  터널링은 요소 트리의 루트에서 시작하여 아래로 이동한 다음 원래 소스 요소에서 끝납니다.  라우트된 이벤트에 대한 자세한 내용은 [라우트된 이벤트 개요](routed-events-overview.md)를 참조하세요.

 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 입력 이벤트는 일반적으로 터널링 이벤트와 버블링 이벤트의 쌍으로 구성되어 제공됩니다.  터널링 이벤트는 “Preview” 접두사가 있다는 점에서 버블링 이벤트와 다릅니다.  예를 들어 <xref:System.Windows.Input.Mouse.PreviewMouseMove>은 마우스 이동 이벤트의 터널링 버전 이며 <xref:System.Windows.Input.Mouse.MouseMove>은이 이벤트의 버블링 버전입니다. 이 이벤트 쌍은 요소 수준에서 구현되는 규칙이며 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 이벤트 시스템의 본질적인 기능은 아닙니다. 자세한 내용은 [라우트된 이벤트 개요](routed-events-overview.md)의 WPF 입력 이벤트 섹션을 참조하세요.

<a name="handling_input_events"></a>
## <a name="handling-input-events"></a>입력 이벤트 처리
 요소에서 입력을 받으려면 특정 이벤트에 이벤트 처리기를 연결해야 합니다.  [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에서는 이 작업이 매우 간단합니다. 이 이벤트를 수신할 요소의 특성으로 이벤트 이름을 참조합니다.  그런 다음 대리자에 따라 정의하는 이벤트 처리기의 이름으로 특성 값을 설정하기만 하면 됩니다.  이벤트 처리기는와 C# 같은 코드에 작성 해야 하며 코드 숨김이 포함 된 파일에 포함 될 수 있습니다.

 키보드 이벤트는 키보드 포커스가 요소에 있는 동안 발생하는 키 동작을 운영 체제에서 보고할 때 발생합니다. 마우스 및 스타일러스 이벤트는 각각 요소를 기준으로 포인터 위치의 변경을 보고하는 이벤트와 디바이스 단추의 상태 변경을 보고하는 이벤트의 두 범주로 나뉩니다.

### <a name="keyboard-input-event-example"></a>키보드 입력 이벤트 예제
 다음 예제에서는 왼쪽 화살표 키 누르기를 수신합니다.  @No__t-1 인 <xref:System.Windows.Controls.StackPanel>이 생성 됩니다.  왼쪽 화살표 키 누름을 수신 대기 하는 이벤트 처리기는 <xref:System.Windows.Controls.Button> 인스턴스에 연결 됩니다.

 이 예제의 첫 번째 섹션에서는 <xref:System.Windows.Controls.StackPanel> 및 <xref:System.Windows.Controls.Button>을 만들고 <xref:System.Windows.UIElement.KeyDown>에 대 한 이벤트 처리기를 연결 합니다.

 [!code-xaml[InputOvw#Input_OvwKeyboardExampleXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/InputOvw/CSharp/Page1.xaml#input_ovwkeyboardexamplexaml)]

 [!code-csharp[InputOvw#Input_OvwKeyboardExampleUICodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/InputOvw/CSharp/Page1.xaml.cs#input_ovwkeyboardexampleuicodebehind)]
 [!code-vb[InputOvw#Input_OvwKeyboardExampleUICodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/InputOvw/VisualBasic/Page1.xaml.vb#input_ovwkeyboardexampleuicodebehind)]

 코드로 작성된 두 번째 섹션은 이벤트 처리기를 정의합니다.  왼쪽 화살표 키를 누르면 <xref:System.Windows.Controls.Button>에 키보드 포커스가 있는 경우 처리기가 실행 되 고 <xref:System.Windows.Controls.Button>의 @no__t 1 색이 변경 됩니다.  키를 누른 상태에서 왼쪽 화살표 키가 아닌 경우에는 <xref:System.Windows.Controls.Button>의 <xref:System.Windows.Controls.Control.Background%2A> 색이 다시 시작 색으로 변경 됩니다.

 [!code-csharp[InputOvw#Input_OvwKeyboardExampleHandlerCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/InputOvw/CSharp/Page1.xaml.cs#input_ovwkeyboardexamplehandlercodebehind)]
 [!code-vb[InputOvw#Input_OvwKeyboardExampleHandlerCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/InputOvw/VisualBasic/Page1.xaml.vb#input_ovwkeyboardexamplehandlercodebehind)]

### <a name="mouse-input-event-example"></a>마우스 입력 이벤트 예제
 다음 예제에서는 마우스 포인터가 <xref:System.Windows.Controls.Button>로 들어가면 <xref:System.Windows.Controls.Button>의 <xref:System.Windows.Controls.Control.Background%2A> 색이 변경 됩니다.  @No__t-0 색은 마우스가 <xref:System.Windows.Controls.Button>을 벗어날 때 복원 됩니다.

 이 예제의 첫 번째 섹션에서는 <xref:System.Windows.Controls.StackPanel> 및 <xref:System.Windows.Controls.Button> 컨트롤을 만들고 <xref:System.Windows.UIElement.MouseEnter> 및 <xref:System.Windows.UIElement.MouseLeave> 이벤트의 이벤트 처리기를 <xref:System.Windows.Controls.Button>에 연결 합니다.

 [!code-xaml[InputOvw#Input_OvwMouseExampleXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/InputOvw/CSharp/Page1.xaml#input_ovwmouseexamplexaml)]

 [!code-csharp[InputOvw#Input_OvwMouseExampleUICodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/InputOvw/CSharp/Page1.xaml.cs#input_ovwmouseexampleuicodebehind)]
 [!code-vb[InputOvw#Input_OvwMouseExampleUICodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/InputOvw/VisualBasic/Page1.xaml.vb#input_ovwmouseexampleuicodebehind)]

 예제에서 코드로 작성된 두 번째 섹션은 이벤트 처리기를 정의합니다.  마우스가 <xref:System.Windows.Controls.Button>에 들어가면 <xref:System.Windows.Controls.Button>의 @no__t 1 색이 <xref:System.Windows.Media.Brushes.SlateGray%2A>으로 변경 됩니다.  마우스가 <xref:System.Windows.Controls.Button>을 벗어나면 <xref:System.Windows.Controls.Button>의 @no__t 1 색이 다시 <xref:System.Windows.Media.Brushes.AliceBlue%2A>으로 변경 됩니다.

 [!code-csharp[InputOvw#Input_OvwMouseExampleEneterHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/InputOvw/CSharp/Page1.xaml.cs#input_ovwmouseexampleeneterhandler)]
 [!code-vb[InputOvw#Input_OvwMouseExampleEneterHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/InputOvw/VisualBasic/Page1.xaml.vb#input_ovwmouseexampleeneterhandler)]

 [!code-csharp[InputOvw#Input_OvwMouseExampleLeaveHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/InputOvw/CSharp/Page1.xaml.cs#input_ovwmouseexampleleavehandler)]
 [!code-vb[InputOvw#Input_OvwMouseExampleLeaveHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/InputOvw/VisualBasic/Page1.xaml.vb#input_ovwmouseexampleleavehandler)]

<a name="text_input"></a>
## <a name="text-input"></a>텍스트 입력
 @No__t-0 이벤트를 사용 하면 장치 독립적 방식으로 텍스트 입력을 수신할 수 있습니다. 텍스트 입력에는 주로 키보드를 사용하지만 음성, 필기 및 기타 입력 디바이스를 통해서도 텍스트 입력을 생성할 수 있습니다.

 키보드 입력의 경우 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]은 먼저 적절 한 <xref:System.Windows.ContentElement.KeyDown> @ no__t @ no__t 이벤트를 보냅니다. 이러한 이벤트가 처리 되지 않고 키가 방향 화살표 또는 기능 키와 같은 컨트롤 키가 아닌 텍스트 이면 <xref:System.Windows.ContentElement.TextInput> 이벤트가 발생 합니다.  여러 번의 키 입력으로 텍스트 입력의 단일 문자를 생성할 수 있고 단일 키 입력이 여러 문자로 된 문자열을 생성할 수 있기 때문에 <xref:System.Windows.ContentElement.KeyDown> @ no__t @ no__t-2 및 <xref:System.Windows.ContentElement.TextInput> 이벤트 사이에는 간단한 일대일 매핑이 항상 발생 하지는 않습니다.  이는 Ime (입력기)를 사용 하 여 해당 하는 알파벳에서 수천 개의 문자를 생성 하는 중국어, 일본어, 한국어 등의 언어에서 특히 그렇습니다.

 @No__t-0이 <xref:System.Windows.ContentElement.KeyUp> @ no__t @ no__t 이벤트 @no__t를 보내는 경우에는 키 입력이 @no__t 이벤트의 일부가 될 수 있는 경우 (예: ALT + S를 누른 경우)-5 @no__t로 설정 됩니다. 이를 통해 <xref:System.Windows.ContentElement.KeyDown> 이벤트 처리기의 코드에서 <xref:System.Windows.Input.Key.System?displayProperty=nameWithType>을 확인 하 고, 검색 된 경우 이후에 발생 한 <xref:System.Windows.ContentElement.TextInput> 이벤트의 처리기에 대 한 처리를 유지할 수 있습니다. 이 경우 <xref:System.Windows.Input.TextCompositionEventArgs> 인수의 다양 한 속성을 사용 하 여 원래 키 입력을 확인할 수 있습니다. 마찬가지로 IME가 활성화 되어 있는 경우 <xref:System.Windows.Input.Key>의 값은 <xref:System.Windows.Input.Key.ImeProcessed?displayProperty=nameWithType>이 고, <xref:System.Windows.Input.KeyEventArgs.ImeProcessedKey%2A>는 원래 키 입력 또는 키 입력을 제공 합니다.

 다음 예제에서는 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트에 대 한 처리기 및 <xref:System.Windows.UIElement.KeyDown> 이벤트에 대 한 처리기를 정의 합니다.

 코드 또는 태그의 첫 번째 세그먼트에서는 사용자 인터페이스를 만듭니다.

 [!code-xaml[InputOvw#Input_OvwTextInputXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/InputOvw/CSharp/Page1.xaml#input_ovwtextinputxaml)]

 [!code-csharp[InputOvw#Input_OvwTextInputUICodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/InputOvw/CSharp/Page1.xaml.cs#input_ovwtextinputuicodebehind)]
 [!code-vb[InputOvw#Input_OvwTextInputUICodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/InputOvw/VisualBasic/Page1.xaml.vb#input_ovwtextinputuicodebehind)]

 코드의 두 번째 세그먼트에는 이벤트 처리기가 포함되어 있습니다.

 [!code-csharp[InputOvw#Input_OvwTextInputHandlersCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/InputOvw/CSharp/Page1.xaml.cs#input_ovwtextinputhandlerscodebehind)]
 [!code-vb[InputOvw#Input_OvwTextInputHandlersCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/InputOvw/VisualBasic/Page1.xaml.vb#input_ovwtextinputhandlerscodebehind)]

 입력 이벤트는 이벤트 경로를 버블링 하기 때문에 <xref:System.Windows.Controls.StackPanel>은 키보드 포커스가 있는 요소에 관계 없이 입력을 받습니다. @No__t-0 컨트롤에는 먼저 알림이 표시 되 고 `OnTextInputKeyDown` 처리기는 <xref:System.Windows.Controls.TextBox>가 입력을 처리 하지 않은 경우에만 호출 됩니다. @No__t-1 이벤트 대신 <xref:System.Windows.UIElement.PreviewKeyDown> 이벤트를 사용 하는 경우 `OnTextInputKeyDown` 처리기가 먼저 호출 됩니다.

 이 예제에서 처리 논리는 Ctrl+O에 대해 한 번, 그리고 단추의 클릭 이벤트에 대해 한 번으로 총 두 번 작성되었습니다. 입력 이벤트를 직접 처리하는 대신 명령을 사용하면 이를 간편하게 처리할 수 있습니다.  명령에 대해서는 이 개요 항목과 [명령 개요](commanding-overview.md)에서 설명합니다.

<a name="touch_and_manipulation"></a>
## <a name="touch-and-manipulation"></a>터치 및 조작
 Windows 7 운영 체제의 새로운 하드웨어 및 API를 사용하면 애플리케이션이 여러 터치에서 동시에 입력을 수신할 수 있습니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]를 사용하면 애플리케이션에서 터치가 발생할 때 이벤트를 발생시킴으로써 마우스나 키보드와 같은 다른 입력에 응답하는 것과 유사한 방식으로 터치를 감지하고 이에 응답할 수 있습니다.

 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 터치가 발생할 때 두 가지 형식의 이벤트, 즉 터치 이벤트와 조작 이벤트를 노출합니다. 터치 이벤트는 터치 스크린의 각 손가락과 그 이동에 대한 원시 데이터를 제공합니다. 조작 이벤트는 특정 작업으로 입력을 해석합니다. 이 섹션에서는 두 가지 형식의 이벤트에 대해 모두 설명합니다.

### <a name="prerequisites"></a>사전 요구 사항
 터치에 응답하는 애플리케이션을 개발하려면 다음 구성 요소가 필요합니다.

- Visual Studio 2010

- Windows 7.

- Windows Touch를 지원하는 터치 스크린과 같은 디바이스

### <a name="terminology"></a>용어
 터치에 대해 설명할 때 다음 용어가 사용됩니다.

- **터치**는 Windows 7에서 인식되는 사용자 입력 형식입니다. 일반적으로 터치 스크린에 손가락을 대면 터치가 시작됩니다. 랩톱 컴퓨터에서 일반적으로 사용되는 터치 패드와 같은 디바이스는 디바이스가 손가락의 위치와 움직임을 마우스 입력으로 단순히 변환하는 경우 터치를 지원하지 않습니다.

- **멀티 터치**는 둘 이상의 지점에서 동시에 발생하는 터치입니다. Windows 7 및 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 멀티 터치를 지원합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에 대한 설명서에서 터치를 설명할 때마다 이 개념이 멀티 터치에 적용됩니다.

- 터치가 개체에 적용되는 물리적 액션으로 해석되면 **조작**이 발생합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 조작 이벤트는 입력을 변환, 확장 또는 회전 조작으로 해석합니다.

- `touch device`는 터치 스크린에서 한 손가락과 같은 터치식 입력을 생성하는 디바이스를 나타냅니다.

### <a name="controls-that-respond-to-touch"></a>터치에 반응하는 컨트롤
 보기에서 스크롤된 콘텐츠가 있는 경우 컨트롤에서 손가락을 드래그하여 다음 컨트롤을 스크롤할 수 있습니다.

- <xref:System.Windows.Controls.ComboBox>

- <xref:System.Windows.Controls.ContextMenu>

- <xref:System.Windows.Controls.DataGrid>

- <xref:System.Windows.Controls.ListBox>

- <xref:System.Windows.Controls.ListView>

- <xref:System.Windows.Controls.MenuItem>

- <xref:System.Windows.Controls.TextBox>

- <xref:System.Windows.Controls.ToolBar>

- <xref:System.Windows.Controls.TreeView>

 @No__t-0 @no__t 연결 된 속성을 정의 합니다 .이 속성을 사용 하면 터치식 이동을 가로, 세로, 둘 다 또는 둘 다로 사용할지 여부를 지정할 수 있습니다. @No__t-0 속성은 사용자가 터치 스크린에서 손가락을 뗄 때 스크롤이 느려지는 속도를 지정 합니다. @No__t-0 연결 된 속성은 조작 오프셋을 변환할 스크롤 오프셋의 비율을 지정 합니다.

### <a name="touch-events"></a>터치 이벤트
 기본 클래스 <xref:System.Windows.UIElement>, <xref:System.Windows.UIElement3D>, <xref:System.Windows.ContentElement>는 응용 프로그램에서 터치에 응답할 수 있도록 구독할 수 있는 이벤트를 정의 합니다. 터치 이벤트는 애플리케이션이 터치를 개체 조작이 아닌 다른 것으로 해석할 때 유용합니다. 예를 들어 사용자가 하나 이상의 손가락으로 그릴 수 있는 애플리케이션은 터치 이벤트를 구독합니다.

 세 클래스 모두 다음과 같은 이벤트를 정의합니다. 이 이벤트는 정의 클래스에 관계없이 유사하게 동작합니다.

- <xref:System.Windows.UIElement.TouchDown>

- <xref:System.Windows.UIElement.TouchMove>

- <xref:System.Windows.UIElement.TouchUp>

- <xref:System.Windows.UIElement.TouchEnter>

- <xref:System.Windows.UIElement.TouchLeave>

- <xref:System.Windows.UIElement.PreviewTouchDown>

- <xref:System.Windows.UIElement.PreviewTouchMove>

- <xref:System.Windows.UIElement.PreviewTouchUp>

- <xref:System.Windows.UIElement.GotTouchCapture>

- <xref:System.Windows.UIElement.LostTouchCapture>

 키보드 및 마우스 이벤트와 마찬가지로 터치 이벤트는 라우트된 이벤트입니다. `Preview`로 시작하는 이벤트는 터널링 이벤트이고 `Touch`로 시작하는 이벤트는 버블링 이벤트입니다. 라우트된 이벤트에 대한 자세한 내용은 [라우트된 이벤트 개요](routed-events-overview.md)를 참조하세요. 이러한 이벤트를 처리할 때 <xref:System.Windows.Input.TouchEventArgs.GetTouchPoint%2A> 또는 <xref:System.Windows.Input.TouchEventArgs.GetIntermediateTouchPoints%2A> 메서드를 호출 하 여 모든 요소를 기준으로 하는 입력의 위치를 가져올 수 있습니다.

 터치 이벤트 간의 상호 작용을 이해하려면 사용자가 한 손가락을 요소 위에 놓고 손가락을 요소에서 움직인 다음 요소에서 손가락을 들어 올리는 시나리오를 고려해 보세요. 다음 그림에서는 버블링 이벤트를 실행하는 것을 보여 줍니다(단순하게 하기 위해 터널링 이벤트는 생략됨).

 ![터치 이벤트의 시퀀스입니다.](./media/ndp-touchevents.png "NDP_TouchEvents") 터치 이벤트

 다음 목록은 앞의 그림에서 이벤트 시퀀스를 설명합니다.

1. @No__t-0 이벤트는 사용자가 요소에 손가락을 놓을 때 한 번 발생 합니다.

2. @No__t-0 이벤트는 한 번 발생 합니다.

3. 사용자가 요소 내에서 손가락을 움직이면 <xref:System.Windows.UIElement.TouchMove> 이벤트가 여러 번 발생 합니다.

4. @No__t-0 이벤트는 사용자가 요소에서 손가락을 뗄 때 한 번 발생 합니다.

5. @No__t-0 이벤트는 한 번 발생 합니다.

 3개 이상의 손가락이 사용되면 각 손가락마다 이벤트가 발생합니다.

### <a name="manipulation-events"></a>조작 이벤트
 응용 프로그램에서 사용자가 개체를 조작할 수 있도록 하는 경우 <xref:System.Windows.UIElement> 클래스는 조작 이벤트를 정의 합니다. 터치 위치를 단순히 보고하는 터치 이벤트와 달리 조작 이벤트는 입력을 해석할 수 있는 방법을 보고합니다. 변환, 확장 및 회전이라는 세 가지 형식의 조작이 있습니다. 다음 목록은 세 가지 형식의 조작을 호출하는 방법을 설명합니다.

- 개체에 손가락을 대고 터치 스크린에서 손가락을 움직이면 변환 조작을 호출합니다. 그러면 일반적으로 개체를 이동합니다.

- 개체 위에 두 개의 손가락을 놓고 손가락을 서로 더 가깝게 또는 멀리 움직여 확장 조작을 호출합니다. 그러면 일반적으로 개체의 크기를 조정합니다.

- 개체에 두 손가락을 놓고 손가락을 서로 회전하면 회전 조작을 호출합니다. 그러면 일반적으로 개체를 회전합니다.

 둘 이상의 조작 형식이 동시에 발생할 수 있습니다.

 개체가 조작에 응답하게 하면 개체에 관성이 있는 것처럼 보일 수 있습니다. 그러면 개체가 실제 세계를 시뮬레이트하게 만들 수 있습니다. 예를 들어 테이블에서 책을 밀 때 충분히 세게 밀면 책을 놓은 후에도 책이 계속 움직입니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]을 사용하면 사용자가 손가락을 개체에서 뗀 후 조작 이벤트를 발생시켜 이 동작을 시뮬레이트할 수 있습니다.

 사용자가 개체를 이동 하 고 크기를 조정 하 고 회전 하는 데 사용할 수 있는 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 [ 연습: 첫 번째 Touch 응용 프로그램 만들기 @ no__t-0.

 @No__t-0은 다음 조작 이벤트를 정의 합니다.

- <xref:System.Windows.UIElement.ManipulationStarting>

- <xref:System.Windows.UIElement.ManipulationStarted>

- <xref:System.Windows.UIElement.ManipulationDelta>

- <xref:System.Windows.UIElement.ManipulationInertiaStarting>

- <xref:System.Windows.UIElement.ManipulationCompleted>

- <xref:System.Windows.UIElement.ManipulationBoundaryFeedback>

 기본적으로 <xref:System.Windows.UIElement>은 이러한 조작 이벤트를 수신 하지 않습니다. @No__t-0에서 조작 이벤트를 수신 하려면 <xref:System.Windows.UIElement.IsManipulationEnabled%2A?displayProperty=nameWithType>을 `true`로 설정 합니다.

#### <a name="the-execution-path-of-manipulation-events"></a>조작 이벤트 실행 경로
 사용자가 개체를 “throw”하는 시나리오를 고려해 보겠습니다. 사용자가 개체 위에 손가락을 놓고 터치 스크린에서 짧은 거리만큼 손가락을 이동한 다음 개체가 움직이는 동안 손가락을 뗍니다. 그 결과 사용자가 손가락을 뗀 후에도 개체가 사용자의 손가락 아래에서 계속 움직입니다.

 다음 그림에서는 조작 이벤트의 실행 경로 및 각 이벤트에 대한 중요한 정보를 보여 줍니다.

 ![조작 이벤트의 시퀀스입니다.](./media/ndp-manipulationevents.png "NDP_ManipulationEvents") 조작 이벤트

 다음 목록은 앞의 그림에서 이벤트 시퀀스를 설명합니다.

1. @No__t-0 이벤트는 사용자가 개체에 손가락을 놓을 때 발생 합니다. 무엇 보다도이 이벤트를 사용 하 여 <xref:System.Windows.Input.ManipulationStartingEventArgs.ManipulationContainer%2A> 속성을 설정할 수 있습니다. 이후 이벤트에서 조작의 위치는 <xref:System.Windows.Input.ManipulationStartingEventArgs.ManipulationContainer%2A>에 상대적입니다. @No__t-0이 아닌 이벤트에서이 속성은 읽기 전용 이므로이 속성을 설정할 수 있는 유일한 시간 (<xref:System.Windows.UIElement.ManipulationStarting>) 이벤트입니다.

2. @No__t-0 이벤트는 다음에 발생 합니다. 이 이벤트는 조작의 출처를 보고합니다.

3. 사용자가 터치 스크린에서 손가락을 움직이면 <xref:System.Windows.UIElement.ManipulationDelta> 이벤트가 여러 번 발생 합니다. @No__t-1 클래스의 <xref:System.Windows.Input.ManipulationDeltaEventArgs.DeltaManipulation%2A> 속성은 조작이 이동, 확장 또는 변환으로 해석 되는지 여부를 보고 합니다. 바로 여기서 개체 조작 작업의 대부분이 수행됩니다.

4. @No__t-0 이벤트는 사용자의 손가락이 개체와의 연결이 끊어질 때 발생 합니다. 이 이벤트를 사용하면 관성이 발생하는 동안 수행되는 조작의 감속을 지정할 수 있습니다. 따라서 사용자가 선택한 여러 가지 실제 공간 또는 특성을 개체가 에뮬레이트할 수 있습니다. 예를 들어 애플리케이션에 실제 세계의 항목을 나타내는 개체가 두 개 있고 한 개체가 다른 개체보다 무거운 경우를 가정해 봅니다. 이 경우 무거운 개체가 가벼운 개체보다 더 빠르게 감속되도록 할 수 있습니다.

5. @No__t-0 이벤트는 관성이 발생할 때 여러 번 발생 합니다. 이 이벤트는 사용자가 터치 스크린에서 손가락을 이동하고 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 관성을 시뮬레이트하는 경우에 발생합니다. 즉, <xref:System.Windows.UIElement.ManipulationDelta>은 <xref:System.Windows.UIElement.ManipulationInertiaStarting> 이벤트 전후에 발생 합니다. @No__t-0 속성은 관성 중에 <xref:System.Windows.UIElement.ManipulationDelta> 이벤트가 발생 하는지 여부를 보고 하므로 해당 속성을 확인 하 고 해당 값에 따라 다른 작업을 수행할 수 있습니다.

6. @No__t-0 이벤트는 조작과 모든 관성이 종료 될 때 발생 합니다. 즉, 모든 <xref:System.Windows.UIElement.ManipulationDelta> 이벤트가 발생 한 후에는 @no__t 1 이벤트가 발생 하 여 조작이 완료 되었음을 신호로 알립니다.

 @No__t-0은 또한 <xref:System.Windows.UIElement.ManipulationBoundaryFeedback> 이벤트를 정의 합니다. 이 이벤트는 <xref:System.Windows.UIElement.ManipulationDelta> 이벤트에서 <xref:System.Windows.Input.ManipulationDeltaEventArgs.ReportBoundaryFeedback%2A> 메서드가 호출 될 때 발생 합니다. @No__t-0 이벤트를 사용 하면 개체가 경계에 도달할 때 응용 프로그램 또는 구성 요소가 시각적 피드백을 제공할 수 있습니다. 예를 들어 <xref:System.Windows.Window> 클래스는 <xref:System.Windows.UIElement.ManipulationBoundaryFeedback> 이벤트를 처리 하 여 가장자리가 나타날 때 창이 약간 이동 되도록 합니다.

 @No__t-1 이벤트를 제외한 모든 조작 이벤트의 이벤트 인수에서 <xref:System.Windows.Input.ManipulationStartingEventArgs.Cancel%2A> 메서드를 호출 하 여 조작을 취소할 수 있습니다. @No__t-0을 호출 하면 조작 이벤트가 더 이상 발생 하지 않고 터치를 위해 마우스 이벤트가 발생 합니다. 다음 표에서는 조작이 취소되는 시점과 발생하는 마우스 이벤트 간의 관계에 대해 설명합니다.

|Cancel이 호출되는 이벤트|이미 발생한 입력에 대해 발생하는 마우스 이벤트|
|----------------------------------------|-----------------------------------------------------------------|
|<xref:System.Windows.UIElement.ManipulationStarting> 및 <xref:System.Windows.UIElement.ManipulationStarted>|마우스 누름 이벤트|
|<xref:System.Windows.UIElement.ManipulationDelta>|마우스 누름 및 마우스 이동 이벤트|
|<xref:System.Windows.UIElement.ManipulationInertiaStarting> 및 <xref:System.Windows.UIElement.ManipulationCompleted>|마우스 누름, 마우스 이동 및 마우스 놓기 이벤트|

 조작이 관성에 있을 때 <xref:System.Windows.Input.ManipulationStartingEventArgs.Cancel%2A>을 호출 하는 경우 메서드는 `false`을 반환 하 고 입력은 마우스 이벤트를 발생 시 키 지 않습니다.

### <a name="the-relationship-between-touch-and-manipulation-events"></a>터치 이벤트와 조작 이벤트의 관계
 @No__t-0은 항상 터치 이벤트를 받을 수 있습니다. @No__t-0 속성이 `true`로 설정 된 경우 <xref:System.Windows.UIElement>는 터치 이벤트와 조작 이벤트를 모두 받을 수 있습니다.  @No__t-0 이벤트가 처리 되지 않은 경우 (즉, <xref:System.Windows.RoutedEventArgs.Handled%2A> 속성이 `false` 인 경우) 조작 논리는 요소에 터치를 캡처하고 조작 이벤트를 생성 합니다. @No__t-2 이벤트에서 <xref:System.Windows.RoutedEventArgs.Handled%2A> 속성이 `true`로 설정 된 경우 조작 논리는 조작 이벤트를 생성 하지 않습니다. 다음 그림에서는 터치 이벤트와 조작 이벤트의 관계를 보여 줍니다.

 터치 이벤트와 조작 이벤트(./media/ndp-touchmanipulateevents.png "NDP_TouchManipulateEvents") 터치 및 조작 이벤트 ![간의 관계]

 다음 목록에서는 앞의 그림에 나와 있는 터치 이벤트와 조작 이벤트의 관계에 대해 설명합니다.

- 첫 번째 터치 장치가 <xref:System.Windows.UIElement>에서 <xref:System.Windows.UIElement.TouchDown> 이벤트를 생성 하는 경우 조작 논리는 <xref:System.Windows.UIElement.GotTouchCapture> 이벤트를 생성 하는 <xref:System.Windows.UIElement.CaptureTouch%2A> 메서드를 호출 합니다.

- @No__t-0이 발생 하면 조작 논리는 <xref:System.Windows.Input.Manipulation.AddManipulator%2A?displayProperty=nameWithType> 메서드를 호출 하 여 <xref:System.Windows.UIElement.ManipulationStarting> 이벤트를 생성 합니다.

- @No__t-0 이벤트가 발생 하는 경우 조작 논리는 <xref:System.Windows.UIElement.ManipulationInertiaStarting> 이벤트 이전에 발생 하는 @no__t 1 이벤트를 생성 합니다.

- 요소의 마지막 터치 장치가 <xref:System.Windows.UIElement.TouchUp> 이벤트를 발생 시키면 조작 논리는 <xref:System.Windows.UIElement.ManipulationInertiaStarting> 이벤트를 생성 합니다.

<a name="focus"></a>
## <a name="focus"></a>포커스
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에는 포커스와 관련된 두 가지 주요 개념인 키보드 포커스와 논리 포커스가 있습니다.

### <a name="keyboard-focus"></a>키보드 포커스
 키보드 포커스는 키보드 입력을 받고 있는 요소를 말합니다.  키보드 포커스가 있는 전체 데스크탑에는 요소가 하나뿐이어야 합니다.  @No__t-0에서 키보드 포커스가 있는 요소는 <xref:System.Windows.IInputElement.IsKeyboardFocused%2A>이 `true`로 설정 됩니다.  정적 <xref:System.Windows.Input.Keyboard> 메서드 <xref:System.Windows.Input.Keyboard.FocusedElement%2A>은 현재 키보드 포커스가 있는 요소를 반환 합니다.

 요소에 대 한 탭을 이동 하거나 특정 요소 (예: <xref:System.Windows.Controls.TextBox>)에서 마우스를 클릭 하 여 키보드 포커스를 가져올 수 있습니다.  @No__t-1 클래스에서 <xref:System.Windows.Input.Keyboard.Focus%2A> 메서드를 사용 하 여 프로그래밍 방식으로 키보드 포커스를 가져올 수도 있습니다.  <xref:System.Windows.Input.Keyboard.Focus%2A>은 지정 된 요소에 키보드 포커스를 지정 하려고 시도 합니다.  @No__t-0에서 반환 된 요소는 현재 키보드 포커스가 있는 요소입니다.

 요소가 키보드 포커스를 가져오도록 하려면 <xref:System.Windows.UIElement.Focusable%2A> 속성을 지정 하 고 <xref:System.Windows.UIElement.IsVisible%2A> 속성을 **true**로 설정 해야 합니다.  @No__t-0과 같은 일부 클래스에는 기본적으로 <xref:System.Windows.UIElement.Focusable%2A>이 `false`로 설정 되어 있습니다. 따라서 해당 요소에서 포커스를 얻을 수 있도록 하려면이 속성을 `true`으로 설정 해야 할 수 있습니다.

 다음 예제에서는 <xref:System.Windows.Input.Keyboard.Focus%2A>을 사용 하 여 <xref:System.Windows.Controls.Button>에 키보드 포커스를 설정 합니다.  응용 프로그램에서 초기 포커스를 설정 하는 데 권장 되는 위치가 <xref:System.Windows.FrameworkElement.Loaded> 이벤트 처리기에 있습니다.

 [!code-csharp[focussample#FocusSampleSetFocus](~/samples/snippets/csharp/VS_Snippets_Wpf/FocusSample/CSharp/Window1.xaml.cs#focussamplesetfocus)]
 [!code-vb[focussample#FocusSampleSetFocus](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FocusSample/visualbasic/window1.xaml.vb#focussamplesetfocus)]

 키보드 포커스에 대한 자세한 내용은 [포커스 개요](focus-overview.md)를 참조하세요.

### <a name="logical-focus"></a>논리 포커스
 논리적 포커스는 포커스 범위의 <xref:System.Windows.Input.FocusManager.FocusedElement%2A?displayProperty=nameWithType>을 참조 합니다.  애플리케이션에 논리 포커스가 있는 요소는 여러 개일 수 있지만, 특정 포커스 범위에 논리 포커스가 있는 요소는 하나뿐일 수 있습니다.

 포커스 범위는 추적 하는 컨테이너 요소는 <xref:System.Windows.Input.FocusManager.FocusedElement%2A> 해당 범위 내에서.  포커스가 포커스 범위를 벗어나면 포커스가 있는 요소에서 키보드 포커스를 잃지만 논리 포커스는 유지합니다.  포커스가 포커스 범위로 돌아오면 포커스가 있는 요소가 키보드 포커스를 갖습니다.  이렇게 하면 여러 포커스 범위 사이에서 키보드 포커스가 변경되더라도 포커스 범위 내에서 포커스가 있는 요소는 포커스가 다시 돌아올 때 포커스가 있는 상태로 유지됩니다.

 @No__t-1 연결 된 속성 <xref:System.Windows.Input.FocusManager.IsFocusScope%2A>를 `true`으로 설정 하거나 코드에서 <xref:System.Windows.Input.FocusManager.SetIsFocusScope%2A> 메서드를 사용 하 여 연결 된 속성을 설정 하 여 @no__t에서 요소를 포커스 범위로 설정할 수 있습니다.

 다음 예제에서는 <xref:System.Windows.Input.FocusManager.IsFocusScope%2A> 연결 된 속성을 설정 하 여 <xref:System.Windows.Controls.StackPanel>을 포커스 범위로 설정 합니다.

 [!code-xaml[MarkupSnippets#MarkupIsFocusScopeXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/MarkupSnippets/CSharp/Window1.xaml#markupisfocusscopexaml)]

 [!code-csharp[FocusSnippets#FocusSetIsFocusScope](~/samples/snippets/csharp/VS_Snippets_Wpf/FocusSnippets/CSharp/Window1.xaml.cs#focussetisfocusscope)]
 [!code-vb[FocusSnippets#FocusSetIsFocusScope](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FocusSnippets/visualbasic/window1.xaml.vb#focussetisfocusscope)]

 기본적으로 포커스 범위에 해당 하는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]의 클래스는 <xref:System.Windows.Window>, <xref:System.Windows.Controls.Menu>, <xref:System.Windows.Controls.ToolBar> 및 <xref:System.Windows.Controls.ContextMenu>입니다.

 키보드 포커스가 있는 요소에는 자신이 속한 포커스 범위에 대 한 논리 포커스가 있습니다. 따라서 <xref:System.Windows.Input.Keyboard> 클래스 또는 기본 요소 클래스에서 <xref:System.Windows.Input.Keyboard.Focus%2A> 메서드를 사용 하 여 요소에 포커스를 설정 하면 요소에 키보드 포커스와 논리 포커스를 제공 하려고 시도 합니다.

 포커스 범위에서 포커스가 있는 요소를 확인 하려면 <xref:System.Windows.Input.FocusManager.GetFocusedElement%2A>을 사용 합니다. 포커스 범위에 대 한 포커스가 있는 요소를 변경 하려면 <xref:System.Windows.Input.FocusManager.SetFocusedElement%2A>을 사용 합니다.

 논리 포커스에 대한 자세한 내용은 [포커스 개요](focus-overview.md)를 참조하세요.

<a name="mouse_position"></a>
## <a name="mouse-position"></a>마우스 위치
 @No__t-0 입력 API는 좌표 공간과 관련 된 유용한 정보를 제공 합니다.  예를 들어 좌표 `(0,0)`은 좌표의 왼쪽 위를 나타냅니다. 그러나 트리에서 어떤 요소의 왼쪽 위인가요? 즉, 좌표가 나타내는 요소가 입력 대상인지 이벤트 처리기를 연결한 요소인지 또는 다른 요소인지 알 수 없습니다. 혼동을 피하기 위해 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 입력 API를 사용 하려면 마우스를 통해 가져온 좌표를 사용할 때 참조 프레임을 지정 해야 합니다. @No__t-0 메서드는 지정 된 요소를 기준으로 마우스 포인터의 좌표를 반환 합니다.

<a name="mouse_capture"></a>
## <a name="mouse-capture"></a>마우스 캡처
 마우스 디바이스에는 마우스 캡처라고 하는 모달 특성이 있습니다. 마우스 캡처는 끌어서 놓기 작업이 시작될 때 전환되는 입력 상태를 유지함으로써 마우스 포인터의 명목상 화면 위치와 관련된 다른 작업이 발생할 필요가 없도록 하기 위해 사용됩니다. 마우스를 끄는 동안 끌어서 놓기 작업을 중단하지 않고는 클릭할 수 없으므로 끌기 원점에서 마우스 캡처를 보유하는 동안에는 대부분의 마우스 이동 동작이 적절하지 않게 됩니다. 입력 시스템은 마우스 캡처 상태를 확인할 수 있는 Api 뿐만 아니라 특정 요소에 마우스 캡처를 적용 하거나 마우스 캡처 상태를 지울 수 있는 api를 노출 합니다. 끌어서 놓기 작업에 대한 자세한 내용은 [끌어서 놓기 개요](drag-and-drop-overview.md)를 참조하세요.

<a name="commands"></a>
## <a name="commands"></a>명령
 명령을 사용하면 디바이스 입력에 비해 보다 의미적 수준에서 입력을 처리할 수 있습니다.  명령은 `Cut`, `Copy`, `Paste` 또는 `Open`과 같은 단순한 지시문입니다.  명령은 명령 논리를 중앙 집중화하는 데 유용합니다.  동일한 명령은 <xref:System.Windows.Controls.Menu>, <xref:System.Windows.Controls.ToolBar> 또는 바로 가기 키를 통해 액세스할 수 있습니다. 또한 명령은 명령을 사용할 수 없을 때 컨트롤을 비활성화하는 메커니즘도 제공합니다.

 <xref:System.Windows.Input.RoutedCommand>은 <xref:System.Windows.Input.ICommand>의 @no__t 1 구현입니다.  @No__t-0을 실행 하면 명령 대상에서 <xref:System.Windows.Input.CommandManager.PreviewExecuted>과 <xref:System.Windows.Input.CommandManager.Executed> 이벤트가 발생 합니다 .이 이벤트는 다른 입력과 마찬가지로 요소 트리를 통해 터널링 및 버블링 합니다.  명령 대상이 설정되어 있지 않으면 키보드 포커스가 있는 요소가 명령 대상이 됩니다.  명령을 수행 하는 논리는 <xref:System.Windows.Input.CommandBinding>에 연결 됩니다.  @No__t-0 이벤트가 특정 명령에 대해 <xref:System.Windows.Input.CommandBinding>에 도달 하면 <xref:System.Windows.Input.CommandBinding>의 <xref:System.Windows.Input.ExecutedRoutedEventHandler>가 호출 됩니다.  이 처리기는 명령의 작업을 수행합니다.

 명령에 대한 자세한 내용은 [명령 개요](commanding-overview.md)를 참조하세요.

 <xref:System.Windows.Input.ApplicationCommands> , <xref:System.Windows.Input.MediaCommands>, <xref:System.Windows.Input.ComponentCommands>, <xref:System.Windows.Input.NavigationCommands> 및 <xref:System.Windows.Documents.EditingCommands>로 구성 된 일반적인 명령 라이브러리를 제공 하거나 사용자가 직접 정의할 수 있습니다.

 다음 예에서는 <xref:System.Windows.Controls.MenuItem>을 설정 하는 방법을 보여 줍니다. 클릭 하면 <xref:System.Windows.Controls.TextBox>에 키보드 포커스가 있는 것으로 가정 하 여 <xref:System.Windows.Controls.TextBox>에서 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 명령을 호출 합니다.

 [!code-xaml[CommandingOverviewSnippets#CommandingOverviewSimpleCommand](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewsimplecommand)]

 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCommandTargetCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcommandtargetcodebehind)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCommandTargetCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcommandtargetcodebehind)]

 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 명령에 대한 자세한 내용은 [명령 개요](commanding-overview.md)를 참조하세요.

<a name="the_input_system_and_base_elements"></a>
## <a name="the-input-system-and-base-elements"></a>입력 시스템 및 기본 요소
 @No__t-0, <xref:System.Windows.Input.Keyboard> 및 @no__t 클래스에 의해 정의 된 연결 된 이벤트와 같은 입력 이벤트는 입력 시스템에 의해 발생 하 고 런타임에 시각적 트리의 적중 테스트를 기반으로 개체 모델의 특정 위치에 삽입 됩니다.

 @No__t, <xref:System.Windows.Input.Keyboard> 및 <xref:System.Windows.Input.Stylus>가 연결 된 이벤트로 정의 하는 각 이벤트는 기본 요소 클래스 <xref:System.Windows.UIElement> 및 <xref:System.Windows.ContentElement>에서 새로운 라우트된 이벤트로도 다시 노출 됩니다. 기본 요소의 라우트된 이벤트는 원래 연결된 이벤트를 처리하고 이벤트 데이터를 다시 사용하는 클래스를 통해 생성됩니다.

 입력 이벤트가 해당 기본 요소 입력 이벤트 구현을 통해 특정 소스 요소와 연결되는 경우 이 입력 이벤트는 논리적 트리 개체 및 시각적 트리 개체의 조합을 기반으로 하는 이벤트 경로의 나머지 부분을 통해 전송할 수 있으며 애플리케이션 코드에서 처리할 수 있습니다.  일반적으로 <xref:System.Windows.UIElement> 및 <xref:System.Windows.ContentElement>에서 라우트된 이벤트를 사용 하 여 이러한 장치 관련 입력 이벤트를 처리 하는 것이 더 편리 합니다. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]와 코드에서 보다 직관적인 이벤트 처리기 구문을 사용할 수 있기 때문입니다. 대신 프로세스를 시작한 연결된 이벤트를 처리할 수도 있지만 이 경우 몇 가지 문제에 직면할 수 있습니다. 예를 들어 기본 요소 클래스 처리를 통해 연결된 이벤트가 처리된 것으로 표시될 수 있습니다. 또한 연결된 이벤트에 대한 처리기를 연결하기 위해 실제 이벤트 구문 대신 접근자 메서드를 사용해야 합니다.

<a name="whats_next"></a>
## <a name="whats-next"></a>새로운 기능
 이제 보다 다양한 기술로 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 입력을 처리할 수 있게 되었습니다.  따라서 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서 사용하는 라우트된 이벤트 메커니즘 및 다양한 형식의 입력 이벤트에 대해 보다 잘 이해하고 있어야 합니다.

 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 프레임워크 요소 및 이벤트 라우팅에 대해 보다 자세히 설명하는 추가 리소스가 있습니다. 자세한 내용은 [명령 개요](commanding-overview.md), [포커스 개요](focus-overview.md), [기본 요소 개요](base-elements-overview.md),[WPF의 트리](trees-in-wpf.md) 및 [라우트된 이벤트 개요](routed-events-overview.md)와 같은 개요를 참조하세요.

## <a name="see-also"></a>참조

- [포커스 개요](focus-overview.md)
- [명령 개요](commanding-overview.md)
- [라우트된 이벤트 개요](routed-events-overview.md)
- [기본 요소 개요](base-elements-overview.md)
- [Properties](properties-wpf.md)
