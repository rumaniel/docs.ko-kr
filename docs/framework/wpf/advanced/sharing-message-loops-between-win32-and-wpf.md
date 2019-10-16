---
title: Win32와 WPF 간에 메시지 루프 공유
ms.date: 03/30/2017
helpviewer_keywords:
- Win32 code [WPF], sharing message loops
- message loops [WPF]
- sharing message loops [WPF]
- interoperability [WPF], Win32
ms.assetid: 39ee888c-e5ec-41c8-b11f-7b851a554442
ms.openlocfilehash: 31efc6e514682502e91487565869285dad22cab0
ms.sourcegitcommit: 83ecdf731dc1920bca31f017b1556c917aafd7a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67860018"
---
# <a name="sharing-message-loops-between-win32-and-wpf"></a>Win32와 WPF 간에 메시지 루프 공유
이 항목에서는 상호 운용성을 위한 메시지 루프를 구현 하는 방법을 설명 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], 기존를 사용 하 여 메시지에 대 한 노출을 루프 <xref:System.Windows.Threading.Dispatcher> 또는에 별도 메시지 루프를 생성 하 여를 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 측의 상호 운용 코드입니다.  
  
## <a name="componentdispatcher-and-the-message-loop"></a>ComponentDispatcher 및 메시지 루프  
 상호 운용성 및 키보드 이벤트 지원에 대 한 일반적인 시나리오를 구현 하는 것 <xref:System.Windows.Interop.IKeyboardInputSink>, 또는 이미 구현 하는 클래스에서 서브클래싱하 <xref:System.Windows.Interop.IKeyboardInputSink>와 같은 <xref:System.Windows.Interop.HwndSource> 또는 <xref:System.Windows.Interop.HwndHost>합니다. 그러나 키보드 싱크를 지 원하는 상호 운용 경계에 걸쳐 메시지를 주고받을 때 해야 하는 모든 가능한 메시지 루프 요구를 처리 하지 않습니다. 응용 프로그램 메시지 루프 아키텍처를 공식화 하는 데 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 제공 된 <xref:System.Windows.Interop.ComponentDispatcher> 수행 하는 메시지 루프에 대 한 간단한 프로토콜을 정의 하는 클래스입니다.  
  
 <xref:System.Windows.Interop.ComponentDispatcher> 여러 멤버를 노출 하는 정적 클래스입니다. 각 메서드의 범위는 호출 스레드를 암시적으로 연결 됩니다. 메시지 루프를 (다음 섹션에 정의 됨)으로 중요 한 시간에 해당 Api의 일부를 호출 해야 합니다.  
  
 <xref:System.Windows.Interop.ComponentDispatcher> 다른 구성 요소 (예: 키보드 싱크)에 대 한 수신 대기할 수 있는 이벤트를 제공 합니다. 합니다 <xref:System.Windows.Threading.Dispatcher> 적절 한 호출을 클래스 <xref:System.Windows.Interop.ComponentDispatcher> 메서드는 적절 한 순서로 합니다. 코드는 호출에 대 한 고유한 메시지 루프를 구현 하는 경우 <xref:System.Windows.Interop.ComponentDispatcher> 비슷한 방식으로 메서드.  
  
 호출 <xref:System.Windows.Interop.ComponentDispatcher> 스레드에서 메서드는 해당 스레드에서 등록 된 이벤트 처리기만 호출 됩니다.  
  
## <a name="writing-message-loops"></a>메시지 루프 작성  
 다음은 검사 목록은 <xref:System.Windows.Interop.ComponentDispatcher> 멤버가 고유한 메시지 루프를 작성 하는 경우 사용 됩니다.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.PushModal%2A>: 메시지 루프 스레드가 모달 임을 나타내려면이 호출 해야 합니다.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.PopModal%2A>:이 스레드가 모달이 되돌려 졌음을 나타내려면 메시지 루프를 호출 해야 합니다.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.RaiseIdle%2A>: 메시지 루프를 호출 해야 함을 나타내려면이 <xref:System.Windows.Interop.ComponentDispatcher> 시켜야 합니다 <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle> 이벤트입니다. <xref:System.Windows.Interop.ComponentDispatcher> 발생 하지 것입니다 <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle> 하는 경우 <xref:System.Windows.Interop.ComponentDispatcher.IsThreadModal%2A> 됩니다 `true`, 메시지 루프를 호출 하도록 선택할 수 있지만 <xref:System.Windows.Interop.ComponentDispatcher.RaiseIdle%2A> 경우에 <xref:System.Windows.Interop.ComponentDispatcher> 모달 상태에서이에 응답할 수 없습니다.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.RaiseThreadMessage%2A>: 새 메시지를 사용할 수 있음을 나타내려면이 메시지 루프를 호출 해야 합니다. 반환 값은 나타냅니다 수신기를 여부를 <xref:System.Windows.Interop.ComponentDispatcher> 이벤트 메시지를 처리 합니다. 하는 경우 <xref:System.Windows.Interop.ComponentDispatcher.RaiseThreadMessage%2A> 반환 `true` (처리) 발송자 아무 작업도 하지 않도록 추가 메시지와 함께 합니다. 반환 값이 `false`, 디스패처는 호출 하는 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 함수 `TranslateMessage`를 호출 `DispatchMessage`합니다.  
  
## <a name="using-componentdispatcher-and-existing-message-handling"></a>ComponentDispatcher를 사용 하 고 기존 메시지 처리  
 다음은의 검사 목록 <xref:System.Windows.Interop.ComponentDispatcher> 멤버에는 내재 된 사용 하는 경우 사용할 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 메시지 루프입니다.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.IsThreadModal%2A>: 응용 프로그램 모달 상태가 있는지 여부를 반환 합니다 (예를 들어 모달 메시지 루프를 푸시 되었습니다). <xref:System.Windows.Interop.ComponentDispatcher> 클래스의 개수를 유지 하기 때문에이 상태를 추적할 수 있습니다 <xref:System.Windows.Interop.ComponentDispatcher.PushModal%2A> 고 <xref:System.Windows.Interop.ComponentDispatcher.PopModal%2A> 메시지 루프에서 호출 합니다.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage> 및 <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> 이벤트 대리자 호출에 대 한 표준 규칙을 따릅니다. 대리자는 지정 되지 않은 순서로 호출 됩니다 및 처리 된 것으로 첫 번째 메시지를 표시 하는 경우에 모든 대리자가 호출 됩니다.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle>: 유휴 상태를 처리 하는 적절 하 고 효율적인 시간을 나타냅니다 (다른 스레드에 대 한 보류 중인 메시지가 없는 함). <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle> 스레드가 모달이면 되지 발생 합니다.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage>: 메시지 펌프를 처리 하는 모든 메시지에서 발생 합니다.  
  
- <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage>: 발생 하는 동안 처리 되지 않은 모든 메시지에 대해 <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage>합니다.  
  
 메시지로 간주 됩니다 후 처리 된 경우에는 <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage> 이벤트 또는 <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> 이벤트를 `handled` 이벤트 데이터에서 참조로 전달 된 매개 변수가 `true`합니다. 이벤트 처리기가 메시지를 무시 해야 `handled` 는 `true`이므로 즉, 다른 처리기에서 메시지를 먼저 처리 합니다. 두 이벤트에 이벤트 처리기는 메시지를 수정할 수 있습니다. 수정된 된 메시지를 원래 변경 되지 않은 메시지가 아니라 발송자 발송 해야 합니다. <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> 모든 수신기 있지만 아키텍처 의도에 게 전달 되는 대상 메시지는 메시지에 대 한 응답에서 코드를 호출 해야 하는 HWND를 포함 하는 최상위 창을 합니다.  
  
## <a name="how-hwndsource-treats-componentdispatcher-events"></a>HwndSource는 ComponentDispatcher 이벤트를 처리 하는 방법  
 경우는 <xref:System.Windows.Interop.HwndSource> 최상위 창 (부모가 HWND)에 등록 됩니다 <xref:System.Windows.Interop.ComponentDispatcher>합니다. 하는 경우 <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> 발생 메시지에 사용 되 고는 <xref:System.Windows.Interop.HwndSource> 또는 자식 창 <xref:System.Windows.Interop.HwndSource> 호출 해당 <xref:System.Windows.Interop.HwndSource.System%23Windows%23Interop%23IKeyboardInputSink%23TranslateAccelerator%2A>를 <xref:System.Windows.Interop.IKeyboardInputSink.TranslateChar%2A>, <xref:System.Windows.Interop.IKeyboardInputSink.OnMnemonic%2A> 키보드 싱크 시퀀스입니다.  
  
 경우는 <xref:System.Windows.Interop.HwndSource> 최상위 창이 아닙니다 (부모가 HWND)을 처리 하지 않아도 됩니다. 최상위 창만는 처리를 수행 하 고 있는 모든 상호 운용 시나리오의 일부로 키보드 싱크를 지 원하는 사용 하 여 최상위 창으로 예상 됩니다.  
  
 하는 경우 <xref:System.Windows.Interop.HwndHost.WndProc%2A> 에 <xref:System.Windows.Interop.HwndSource> 라고 먼저 호출 되는 적절 한 키보드 싱크 메서드에 없이 응용 프로그램이 받을 더 높은 수준의 키보드 이벤트와 같은 <xref:System.Windows.UIElement.KeyDown>합니다. 그러나 키보드 싱크 메서드가 호출 될 대 한 액세스 키 지원과 같은 바람직하지 키보드 입력된 모델 기능을 우회 하는 합니다. 이 메시지 루프 관련 스레드 시 제대로 알리지 않음 않은 때문에 발생할 수 있습니다는 <xref:System.Windows.Interop.ComponentDispatcher>, 없거나 부모 HWND를 호출 하지 않는 적절 한 키보드 싱크 응답 합니다.  
  
 사용 하 여 해당 메시지에 대 한 후크를 추가한 경우 키보드 싱크를 이동 하는 메시지 HWND에 전송 되지 않을 수 있습니다는 <xref:System.Windows.Interop.HwndSource.AddHook%2A> 메서드. 메시지가 아니라 직접 전송할 메시지 펌프 수준에서 처리 될 수 있습니다는 `DispatchMessage` 함수입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Interop.ComponentDispatcher>
- <xref:System.Windows.Interop.IKeyboardInputSink>
- [WPF 및 Win32 상호 운용성](wpf-and-win32-interoperation.md)
- [스레딩 모델](threading-model.md)
- [입력 개요](input-overview.md)
