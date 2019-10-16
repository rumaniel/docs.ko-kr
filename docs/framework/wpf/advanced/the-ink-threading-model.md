---
title: 잉크 스레딩 모델
ms.date: 03/30/2017
helpviewer_keywords:
- application user interface thread [WPF]
- stylus plug-in
- ink threading model [WPF]
- ink [WPF], rendering
- pen thread [WPF]
- threading model [WPF]
- rendering ink [WPF]
- dynamic rendering thread [WPF]
- ink collection plug-in
- plug-ins [WPF], for ink
ms.assetid: c85fcad1-cb50-4431-847c-ac4145a35c89
ms.openlocfilehash: b753fcffbdaa1cc9ba960a774077457dd0263e0a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64621367"
---
# <a name="the-ink-threading-model"></a>잉크 스레딩 모델
Tablet pc 잉크의 이점 중 하나는 마치 많은 쓰기와 같은 일반 펜과 종이 사용 하 여 것입니다.  태블릿 펜이를 위해 마우스 않으며 사용자가 쓸 때 잉크를 렌더링 하는 보다 훨씬 빠른 속도로 입력된 데이터를 수집 합니다.  차단 될 수 있으므로 응용 프로그램의 사용자 인터페이스 (UI) 스레드에서 펜 데이터와 렌더링 잉크를 수집 하기 위한 충분 하지 않습니다.  이 해결 하는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 사용자 잉크를 쓸 때 응용 프로그램에서는 두 개의 추가 스레드를 사용 합니다.  
  
 다음 목록은 수집 하 고 디지털 잉크를 렌더링에 참여 하는 스레드를 보여 줍니다.  
  
- 펜 스레드-스레드 스타일러스에서 입력입니다.  (실제로 스레드 풀 이지만이 항목에서는 펜 스레드는이를 나타냅니다.)  
  
- 응용 프로그램 사용자 인터페이스 스레드 응용 프로그램의 사용자 인터페이스를 제어 하는 스레드입니다.  
  
- 동적 렌더링 스레드-사용자 동안 잉크를 렌더링 하는 스레드는 스트로크를 그립니다. Window Presentation Foundation에서 설명 했 듯이 동적 렌더링 스레드는 응용 프로그램의 다른 UI 요소를 렌더링 하는 스레드가 아닌 다른 [스레딩 모델](threading-model.md)합니다.  
  
 잉크 입력 기능 모델이 동일 응용 프로그램을 사용 합니다 <xref:System.Windows.Controls.InkCanvas> 또는 사용자 지정 컨트롤에서 비슷하게 [잉크 입력 컨트롤 만들기](creating-an-ink-input-control.md)합니다.  이 항목에서는 설명의 측면에서 스레딩 있지만 <xref:System.Windows.Controls.InkCanvas>, 사용자 지정 컨트롤을 만들 때 동일한 개념이 적용 합니다.  
  
## <a name="threading-overview"></a>스레딩 개요  
 다음 다이어그램에서는 사용자가 스트로크를 그릴 때 스레딩 모델을 보여 줍니다.  
  
 ![스트로크를 그리는 동안 스레딩 모델입니다. ](./media/inkthreading-drawingink.png "InkThreading_DrawingInk")  
  
1. 사용자가 스트로크를 그리는 동안 발생 하는 작업  
  
    1. 사용자가 스트로크를 그릴, 펜 스레드에서 스타일러스 지점을 제공 합니다.  스타일러스 플러그 인을 포함 하는 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>와 펜 스레드에서 스타일러스 지점을 적용 하기 전에 수정 하 게는 <xref:System.Windows.Controls.InkCanvas> 를 수신 합니다.  
  
    2. <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 스타일러스 지점을 동적 렌더링 스레드에서 렌더링 합니다. 이전 단계와 동시에 발생합니다.  
  
    3. <xref:System.Windows.Controls.InkCanvas> 스타일러스 포인트 UI 스레드를 수신 합니다.  
  
2. 사용자가 스트로크를 종료 한 후 발생 하는 작업  
  
    1. 사용자가 스트로크를 그리는 마치면 합니다 <xref:System.Windows.Controls.InkCanvas> 만듭니다를 <xref:System.Windows.Ink.Stroke> 개체에 추가 합니다는 <xref:System.Windows.Controls.InkPresenter>를 정적으로 렌더링 하는 합니다.  
  
    2. UI 스레드 경고는 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 스트로크를 정적으로 렌더링 하는 하므로 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 스트로크의 시각적 표시를 제거 합니다.  
  
## <a name="ink-collection-and-stylus-plug-ins"></a>잉크 수집 및 스타일러스 플러그 인  
 각 <xref:System.Windows.UIElement> 에 <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection>합니다.  합니다 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 개체는 <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection> 받고 펜 스레드에서 스타일러스 지점을 수정할 수 있습니다. 합니다 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 개체에서 해당 순서에 따라 스타일러스 지점이 수신는 <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection>합니다.  
  
 다음 다이어그램에서는 가상의 상황 위치는 <xref:System.Windows.UIElement.StylusPlugIns%2A> 의 컬렉션을 <xref:System.Windows.UIElement> 포함 `stylusPlugin1`, <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>, 및 `stylusPlugin2`해당 순서.  
  
 ![스타일러스 플러그 인 순서가 출력을 영향을 줍니다. ](./media/inkthreading-pluginorder.png "InkThreading_PluginOrder")  
  
 이전 다이어그램에서 다음과 같은 동작이 수행 됩니다.  
  
1. `StylusPlugin1` x에 대 한 값을 수정 하 고 y입니다.  
  
2. <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 수정 된 스타일러스 지점을 받고 동적 렌더링 스레드에서 렌더링 합니다.  
  
3. `StylusPlugin2` 수정된 된 스타일러스 포인트를 수신 하 고 추가 x에 대 한 값을 수정 하 고 y입니다.  
  
4. 응용 프로그램 스타일러스 지점을 수집 하 고 사용자가 스트로크를 끝내는 정적으로 스트로크를 렌더링 합니다.  
  
 가정 `stylusPlugin1` 스타일러스 지점이 사각형에 제한 및 `stylusPlugin2` 오른쪽으로 스타일러스 포인트를 변환 합니다.  앞의 시나리오에는 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 제한 스타일러스 포인트를 받지만 번역 된 스타일러스 지점이 없습니다.  사용자가 스트로크를 그리면 사각형의 경계 내 스트로크 렌더링 되지만 사용자가 펜을 뗄 때까지 변환할 스트로크 표시 되지 않습니다.  
  
### <a name="performing-operations-with-a-stylus-plug-in-on-the-ui-thread"></a>UI 스레드에서 플러그 스타일러스를 사용 하 여 작업을 수행합니다.  
 펜 스레드에서 정확한 적중 테스트를 수행할 수 없으므로, 일부 요소가 다른 요소에 대 한 스타일러스 입력을 받는 경우도 합니다. 입력이 작업을 수행 하기 전에 올바르게 라우트 되도록 해야 하는 경우 등록 하 고 작업을 수행 합니다 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn.OnStylusDownProcessed%2A>, <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn.OnStylusMoveProcessed%2A>, 또는 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn.OnStylusUpProcessed%2A> 메서드. 이러한 메서드는 정확한 적중 테스트가 수행 된 후 응용 프로그램 스레드에 의해 호출 됩니다. 를 구독 하려면 이러한 메서드 호출을 <xref:System.Windows.Input.StylusPlugIns.RawStylusInput.NotifyWhenProcessed%2A> 펜 스레드에서 발생 하는 방법에 대 한 메서드.  
  
 다음 다이어그램은 펜 스레드 및 스타일러스 이벤트를 기준으로 UI 스레드 간의 관계를 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>입니다.  
  
 ![잉크 스레딩 모델 &#40;UI 및 펜&#41;](./media/inkthreading-plugincallbacks.png "InkThreading_PluginCallbacks")  
  
## <a name="rendering-ink"></a>잉크 렌더링  
 사용자가 스트로크를 그릴 때 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 잉크가 "흘러나오는" 펜에서 UI 스레드가 사용 중인 경우에 표시 되도록 별도 스레드에서 잉크를 렌더링 합니다.  <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 시각적 트리를 기반으로 동적 렌더링 스레드 스타일러스 포인트를 수집 합니다.  사용자가 스트로크를 끝내는 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 응용 프로그램이 다음 렌더링 과정을 수행 하는 경우 알려 주도록 요청 합니다.  응용 프로그램에는 다음 렌더링 과정을 완료 된 후의 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 시각적 트리를 정리 합니다.  다음 다이어그램에서는이 프로세스를 보여 줍니다.  
  
 ![잉크 스레딩 다이어그램](./media/inkthreading-visualtree.png "InkThreading_VisualTree")  
  
1. 사용자가 스트로크를 시작 합니다.  
  
    1. <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 시각적 트리를 만듭니다.  
  
2. 사용자가 스트로크를 그리고 있습니다.  
  
    1. <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 시각적 트리를 만듭니다.  
  
3. 사용자가 스트로크를 종료 합니다.  
  
    1. <xref:System.Windows.Controls.InkPresenter> 스트로크 해당 시각적 트리를 추가 합니다.  
  
    2. 미디어 통합 계층 (MIL) 스트로크를 정적으로 렌더링합니다.  
  
    3. <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 시각적 개체를 정리 합니다.
