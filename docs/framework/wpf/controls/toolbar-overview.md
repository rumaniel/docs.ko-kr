---
title: ToolBar 개요
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], ToolBar
- ToolBar control [WPF]
ms.assetid: a8edb32c-118d-4f31-b6e6-8899082b504b
ms.openlocfilehash: 711d55e46fb548787976a1f966c9fbf6dc7f12d8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61790855"
---
# <a name="toolbar-overview"></a>ToolBar 개요
<xref:System.Windows.Controls.ToolBar> 컨트롤은 명령 또는 해당 함수에서 일반적으로 관련이 있는 컨트롤의 그룹에 대 한 컨테이너입니다. <xref:System.Windows.Controls.ToolBar> 명령을 호출 하는 단추는 일반적으로 포함 합니다.  

<a name="ToolBarControl"></a>   
## <a name="toolbar-control"></a>ToolBar 컨트롤  
 <xref:System.Windows.Controls.ToolBar> 제어는 단일 행 또는 열에 단추나 다른 컨트롤의 막대 모양 정렬에서 해당 이름을 사용 합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.ToolBar> 크기 제한 내에서 자연스럽 게 적합 하지 않은 모든 항목을 배치 하는 오버플로 메커니즘을 제공 하는 컨트롤 <xref:System.Windows.Controls.ToolBar> 특수 오버플로 영역에 있습니다. 또한 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.ToolBar> 컨트롤은 일반적으로 사용 관련 된 <xref:System.Windows.Controls.ToolBarTray> 를 조정 하 고 컨트롤과 사용자가 시작한 지원 뿐만 아니라 특수 레이아웃 동작을 제공 하는 컨트롤입니다.  
  
<a name="Creating_ToolBars"></a>   
## <a name="specifying-the-position-of-toolbars-in-a-toolbartray"></a>ToolBarTray에서 ToolBar 위치 지정  
 사용 하 여는 <xref:System.Windows.Controls.ToolBar.Band%2A> 및 <xref:System.Windows.Controls.ToolBar.BandIndex%2A> 위치로 속성을 <xref:System.Windows.Controls.ToolBar> 에 <xref:System.Windows.Controls.ToolBarTray>. <xref:System.Windows.Controls.ToolBar.Band%2A> 위치를 나타내는 합니다 <xref:System.Windows.Controls.ToolBar> 부모 내에 배치 됩니다 <xref:System.Windows.Controls.ToolBarTray>합니다. <xref:System.Windows.Controls.ToolBar.BandIndex%2A> 순서를 나타냅니다는 <xref:System.Windows.Controls.ToolBar> band 내에 배치 됩니다. 다음 예제에서는 배치에이 속성을 사용 방법 <xref:System.Windows.Controls.ToolBar> 내부의 컨트롤을 <xref:System.Windows.Controls.ToolBarTray>입니다.  
  
 [!code-xaml[ToolBarExample#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolBarExample/CS/Pane1.xaml#2)]  
  
<a name="ToolBars_with_Overflow_Items"></a>   
## <a name="toolbars-with-overflow-items"></a>오버플로 항목이 있는 ToolBar  
 종종 <xref:System.Windows.Controls.ToolBar> 컨트롤 도구 모음의 크기에 맞출 수 있는 것 보다 많은 항목이 포함 됩니다. 이 경우는 <xref:System.Windows.Controls.ToolBar> 오버플로 단추를 표시 합니다. 오버플로 항목을 보려면 사용자가 오버플로 단추를 클릭 하 고 항목 아래 팝업 창에 표시 됩니다는 <xref:System.Windows.Controls.ToolBar>합니다. 다음 그래픽에 표시 된 <xref:System.Windows.Controls.ToolBar> 오버플로 항목이 있는:  
  
 ![오버플로 항목이 있는 도구 모음을 보여 주는 스크린샷.](./media/toolbar-overview/toolbar-overflow-items.png)  
  
 설정 하 여 도구 모음의 항목이 오버플로 패널에 배치 됩니다 때 지정할 수 있습니다 합니다 <xref:System.Windows.Controls.ToolBar.OverflowMode%2A?displayProperty=nameWithType> 연결 속성을 <xref:System.Windows.Controls.OverflowMode.Always?displayProperty=nameWithType>를 <xref:System.Windows.Controls.OverflowMode.Never?displayProperty=nameWithType>, 또는 <xref:System.Windows.Controls.OverflowMode.AsNeeded?displayProperty=nameWithType>합니다. 다음 예제에서는 도구 모음에 있는 마지막 네 개의 단추가 오버플로 패널에 항상 표시되도록 지정합니다.  
  
 [!code-xaml[ToolBarExample#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolBarExample/CS/Pane1.xaml#3)]  
  
 <xref:System.Windows.Controls.ToolBar> 사용 하는 <xref:System.Windows.Controls.Primitives.ToolBarPanel> 및 <xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel> 에서 해당 <xref:System.Windows.Controls.ControlTemplate>합니다.  <xref:System.Windows.Controls.Primitives.ToolBarPanel> 도구 모음에서 항목의 레이아웃을 담당 합니다.  합니다 <xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel> 에 맞지 않는 항목의 레이아웃을 담당 합니다 <xref:System.Windows.Controls.ToolBar>합니다. 예는 <xref:System.Windows.Controls.ControlTemplate> 에 대 한는 <xref:System.Windows.Controls.ToolBar>, 참조  
  
 [ToolBar 스타일 및 템플릿](toolbar-styles-and-templates.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Primitives.ToolBarPanel>
- <xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>
- [ToolBar 컨트롤의 스타일 지정](how-to-style-controls-on-a-toolbar.md)
- [WPF Controls Gallery Sample](https://go.microsoft.com/fwlink/?LinkID=160053)(WPF 컨트롤 갤러리 샘플)
