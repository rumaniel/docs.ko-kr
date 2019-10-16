---
title: '자습서: Win32 애플리케이션에서 시각적 개체 호스팅'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- visual objects in Win32 code [WPF]
- Win32 code [WPF], visual objects in
- hosting [WPF], visual objects in Win32 code
ms.assetid: f0e1600c-3217-43d5-875d-1864fa7fe628
ms.openlocfilehash: c8baefbf01467a65626a77f300f34a145d5c7281
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962870"
---
# <a name="tutorial-hosting-visual-objects-in-a-win32-application"></a>자습서: Win32 애플리케이션에서 시각적 개체 호스팅
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]에서는 응용 프로그램을 만들기 위한 다양한 환경을 제공합니다. 그러나 코드에 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 상당한 투자를 한 경우 코드를 다시 작성 하는 대신 응용 프로그램에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 기능을 추가 하는 것이 더 효과적일 수 있습니다. 응용 프로그램에서 동시 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 사용 되는 및 그래픽 하위 시스템에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 대 한 지원을 제공 하기 위해에서는 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창에서 개체를 호스트 하기 위한 메커니즘을 제공 합니다.  
  
 이 자습서에서는 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창에서 시각적 [개체를 호스트](https://go.microsoft.com/fwlink/?LinkID=159995) [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 하는 샘플 응용 프로그램을 작성 하는 방법을 설명 합니다.  

<a name="requirements"></a>   
## <a name="requirements"></a>요구 사항  
 이 자습서에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 및 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 프로그래밍에 대한 기본 지식이 있다고 가정합니다. 프로그래밍에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 대 한 기본적인 소개를 보려면 [연습: 내 첫 번째 WPF 데스크톱](../getting-started/walkthrough-my-first-wpf-desktop-application.md)응용 프로그램입니다. 프로그래밍에 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 대 한 소개는 주제에 대 한 다양 한 서적, 특히 Charles Petzold의 *프로그래밍 창* 을 참조 하세요.  
  
> [!NOTE]
> 이 자습서에는 관련 샘플의 많은 코드 예제가 포함되어 있습니다. 그러나 가독성을 위해 전체 샘플 코드를 포함하지는 않습니다. 전체 샘플 코드는 [Win32 상호 운용을 사용한 적중 테스트 샘플](https://go.microsoft.com/fwlink/?LinkID=159995)을 참조 하세요.  
  
<a name="creating_the_host_win32_window"></a>   
## <a name="creating-the-host-win32-window"></a>호스트 Win32 창 만들기  
 창 에서개체[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 를 호스트 하는 열쇠는 클래스입니다.<xref:System.Windows.Interop.HwndSource> [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 이 클래스는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창에 개체를 래핑하여에 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 자식 창으로 통합 될 수 있도록 합니다.  
  
 다음 예제에서는 개체를 <xref:System.Windows.Interop.HwndSource> 시각적 개체에 대 한 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 컨테이너 창으로 만드는 코드를 보여 줍니다. 창에 대 한 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창 스타일, 위치 및 기타 매개 변수를 설정 하려면 <xref:System.Windows.Interop.HwndSourceParameters> 개체를 사용 합니다.  
  
 [!code-csharp[VisualsHitTesting#101](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#101)]
 [!code-vb[VisualsHitTesting#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#101)]  
  
> [!NOTE]
> <xref:System.Windows.Interop.HwndSourceParameters.ExtendedWindowStyle%2A> 속성의 값을 WS_EX_TRANSPARENT로 설정할 수 없습니다. 즉, 호스트 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창은 투명 할 수 없습니다. 이러한 이유로 호스트 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창의 배경색은 부모 창과 동일한 배경색으로 설정 됩니다.  
  
<a name="adding_visual_objects_to_the_host_win32_window"></a>   
## <a name="adding-visual-objects-to-the-host-win32-window"></a>호스트 Win32 창에 시각적 개체 추가  
 시각적 개체에 대 한 호스트 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 컨테이너 창을 만든 후에는 시각적 개체를 추가할 수 있습니다. 애니메이션 등의 시각적 개체에 대 한 변환이 호스트 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창의 경계 사각형 범위를 벗어나 확장 되지 않도록 하려고 합니다.  
  
 다음 예제에서는 <xref:System.Windows.Interop.HwndSource> 개체를 만들고이 개체에 시각적 개체를 추가 하는 코드를 보여 줍니다.  
  
> [!NOTE]
> 개체의 속성은 호스트 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창에 추가 된 첫 번째 시각적 개체로 설정 됩니다. <xref:System.Windows.Interop.HwndSource.RootVisual%2A> <xref:System.Windows.Interop.HwndSource> 루트 시각적 개체는 시각적 개체 트리의 최상위 노드를 정의합니다. 호스트 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창에 추가 된 모든 후속 시각적 개체는 자식 개체로 추가 됩니다.  
  
 [!code-csharp[VisualsHitTesting#100](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#100)]
 [!code-vb[VisualsHitTesting#100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#100)]  
  
<a name="implementing_the_win32_message_filter"></a>   
## <a name="implementing-the-win32-message-filter"></a>Win32 메시지 필터 구현  
 시각적 개체 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 에 대 한 호스트 창에는 응용 프로그램 큐에서 창으로 전송 된 메시지를 처리 하기 위한 창 메시지 필터 프로시저가 필요 합니다. 창 프로시저는 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 시스템에서 메시지를 받습니다. 이러한 메시지를 입력 메시지이거나 창 관리 메시지일 수 있습니다. 필요에 따라 창 절차에서 메시지를 처리하거나 기본 처리를 위해 메시지를 시스템으로 전달할 수 있습니다.  
  
 시각적 <xref:System.Windows.Interop.HwndSource> 개체에 대 한 부모로 정의 된 개체는 사용자가 제공 하는 창 메시지 필터 프로시저를 참조 해야 합니다. <xref:System.Windows.Interop.HwndSource> 개체를 만들 때 창 프로시저를 참조 <xref:System.Windows.Interop.HwndSourceParameters.HwndSourceHook%2A> 하도록 속성을 설정 합니다.  
  
 [!code-csharp[VisualsHitTesting#102](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#102)]
 [!code-vb[VisualsHitTesting#102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#102)]  
  
 다음 예제에서는 왼쪽 및 오른쪽 마우스 단추 잠금 메시지를 처리하기 위한 코드를 보여 줍니다. 마우스 적중 위치의 좌표 값은 `lParam` 매개 변수 값에 포함 됩니다.  
  
 [!code-csharp[VisualsHitTesting#103](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#103)]
 [!code-vb[VisualsHitTesting#103](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#103)]  
  
<a name="processing_the_win32_messages"></a>   
## <a name="processing-the-win32-messages"></a>Win32 메시지 처리  
 다음 예제의 코드는 호스트 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창에 포함 된 시각적 개체의 계층 구조에 대해 적중 테스트를 수행 하는 방법을 보여 줍니다. <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> 메서드를 사용 하 여 적중 테스트에 대 한 루트 시각적 개체 및 좌표 값을 지정 하 여 요소가 시각적 개체의 기 하 도형 내에 있는지 여부를 식별할 수 있습니다. 이 경우 루트 시각적 개체는 <xref:System.Windows.Interop.HwndSource.RootVisual%2A> <xref:System.Windows.Interop.HwndSource> 개체의 속성 값입니다.  
  
 [!code-csharp[VisualsHitTesting#104](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyCircle.cs#104)]
 [!code-vb[VisualsHitTesting#104](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyCircle.vb#104)]  
  
 시각적 개체에 대 한 적중 테스트에 대 한 자세한 내용은 [시각적 계층의 적중 테스트](hit-testing-in-the-visual-layer.md)를 참조 하십시오.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Interop.HwndSource>
- [Win32 상호 운용성 샘플로 적중 테스트](https://go.microsoft.com/fwlink/?LinkID=159995)
- [시각적 계층에서 적중 테스트](hit-testing-in-the-visual-layer.md)
