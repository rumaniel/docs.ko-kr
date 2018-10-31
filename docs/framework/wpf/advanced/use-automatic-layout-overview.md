---
title: 자동 레이아웃 사용 개요
ms.date: 03/30/2017
helpviewer_keywords:
- layout [WPF], automatic
- automatic layout [WPF]
ms.assetid: 6fed9264-18bb-4d05-8867-1fe356c6f687
ms.openlocfilehash: d6ed0da9be32a4a4de4111acfb2d347b7bd5096d
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50201558"
---
# <a name="use-automatic-layout-overview"></a>자동 레이아웃 사용 개요
이 항목에서는 개발자가 작성 하는 방법에 대 한 지침을 소개 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 응용 프로그램을 지역화할 수 있는 [!INCLUDE[TLA#tla_ui#plural](../../../../includes/tlasharptla-uisharpplural-md.md)]합니다. 과거에는 UI의 지역화는 시간이 오래 걸리는 프로세스 였습니다. 에 대 한 UI를 조정 하는 각 언어는 픽셀 단위 조정이 필요 합니다. 적합 한 설계 및 코딩 표준을 사용 하 여 오늘 [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] 는 작은 크기 조정 및 위치 조정 작업을 생성할 수 있습니다. 보다 쉽게 크기 및 위치가 변경 될 수 있는 응용 프로그램을 작성 하는 방법을 자동 레이아웃 이라고 하며 사용 하 여 구현할 수 있습니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램 디자인.  

<a name="advantages_of_autolayout"></a>   
## <a name="advantages-of-using-automatic-layout"></a>자동 레이아웃 사용의 이점  
 때문에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 프레젠테이션 시스템은 강력 하 고 유연한, 다른 언어의 요구 사항에 맞게 조정할 수 있는 응용 프로그램에서 레이아웃 요소 기능을 제공 합니다. 다음 목록에서는 자동 레이아웃의 몇 가지 이점을 보여 줍니다.  

-   UI는 모든 언어에서 잘 표시 됩니다.  

-   텍스트가 변환된 후 컨트롤의 위치 및 크기를 다시 조정할 필요가 줄어듭니다.  
  
-   창 크기를 다시 조정할 필요가 줄어듭니다.  

-   UI 레이아웃이 모든 언어에서 제대로 렌더링 됩니다.  

-   지역화를 문자열 변환 정도의 수준으로 줄일 수 있습니다.  
  
<a name="autolayout_controls"></a>   
## <a name="automatic-layout-and-controls"></a>자동 레이아웃 및 컨트롤  
 자동 레이아웃을 사용하면 응용 프로그램에서 컨트롤의 크기를 자동으로 조정할 수 있습니다. 예를 들어 컨트롤이 문자열의 길이 맞게 변경될 수 있습니다. 이 기능을 통해 로컬라이저는 문자열을 변환할 수 있으며, 더 이상 변환된 텍스트에 맞게 컨트롤의 크기를 조정할 필요가 없습니다. 다음 예제에서는 영어 콘텐츠가 있는 단추를 만듭니다.  
  
 [!code-xaml[LocalizationBtn_snip#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn_snip/CS/Pane1.xaml#1)]  
  
 이 예제에서 스페인어 단추를 만들려면 텍스트만 변경하면 됩니다. 예를 들면 다음과 같습니다.  
  
 [!code-xaml[LocalizationBtn#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn/CS/Pane1.xaml#1)]  
  
 다음 그림에서는 코드 샘플의 출력을 보여 줍니다.  
  
 ![서로 다른 언어로 텍스트는 동일한 단추](../../../../docs/framework/wpf/advanced/media/globalizationbutton.png "GlobalizationButton")  
자동 크기 조정 단추  
  
<a name="autolayout_coding"></a>   
## <a name="automatic-layout-and-coding-standards"></a>자동 레이아웃 및 코딩 표준  
 자동 레이아웃 방식을 사용 하 여 코딩 및 디자인 표준 및 완전히 지역화할 수 있는 UI를 생성 하는 규칙 집합이 필요 합니다. 다음은 자동 레이아웃 코딩에 도움이 되는 지침입니다.  

**절대 위치를 사용 하지 마세요**

- 사용 하지 않는 <xref:System.Windows.Controls.Canvas> 요소를 절대 위치에 배치 하기 때문에 있습니다.

- 사용 하 여 <xref:System.Windows.Controls.DockPanel>, <xref:System.Windows.Controls.StackPanel>, 및 <xref:System.Windows.Controls.Grid> 컨트롤의 위치입니다.

다양 한 패널 유형에 대 한 자세한 내용은 참조 하세요. [Panel 개요](../../../../docs/framework/wpf/controls/panels-overview.md)합니다.

**창에 대 한 고정된 크기를 설정 하지**

- <xref:System.Windows.Window.SizeToContent%2A?displayProperty=nameWithType>을 사용하세요. 예를 들어:

   [!code-xaml[LocalizationGrid#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#2)]

**추가 <xref:System.Windows.FrameworkElement.FlowDirection%2A>**

- 추가 된 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 응용 프로그램의 루트 요소입니다.

   WPF는 편리 하 게 지원 가로, 양방향 및 세로 레이아웃을 제공 합니다. 프레젠테이션 프레임 워크에서는 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 레이아웃을 정의 하려면 속성을 사용할 수 있습니다. 흐름 방향 패턴은 다음과 같습니다.
   
     - <xref:System.Windows.FlowDirection.LeftToRight?displayProperty=nameWithType> (LrTb) — 라틴어, 동아시아, 등을 위한 가로 레이아웃.
     
     - <xref:System.Windows.FlowDirection.RightToLeft?displayProperty=nameWithType> (RlTb) — 아랍어, 히브리어 등을 위한 양방향.

**실제 글꼴 대신 합성 글꼴을 사용 합니다.**

- 합성 글꼴을 사용 합니다 <xref:System.Windows.Controls.Control.FontFamily%2A> 속성 지역화할 필요가 없습니다.

- 개발자는 다음 글꼴 중 하나를 사용하거나 직접 만들 수 있습니다.

   - 전역 사용자 인터페이스
   - 전역 San Serif
   - 전역 Serif

**Xml: lang를 추가 합니다.**

- 추가 된 `xml:lang` 하면 UI의 루트 요소와 같은 특성 `xml:lang="en-US"` 영어 응용 프로그램에 대 한 합니다.

- 합성 글꼴을 사용 하므로 `xml:lang` 글꼴을 사용 하 여 결정할 다국어 시나리오를 지원 하도록이 속성을 설정 합니다.

<a name="autolay_grids"></a>   
## <a name="automatic-layout-and-grids"></a>자동 레이아웃 및 그리드  
 <xref:System.Windows.Controls.Grid> 요소는 요소의 위치를 개발자 수 있기 때문에 자동 레이아웃에 유용 합니다. <xref:System.Windows.Controls.Grid> 컨트롤은 열 및 행 정렬을 사용 하 여 해당 자식 요소 간에 사용 가능한 공간을 배포 합니다. UI 요소에는 여러 셀에 걸쳐 있을 수 있으며 그리드 내에 그리드를 가질 수 것. 표를 만들고 복잡 한 UI를 배치할 수 있도록 하므로 유용 합니다. 다음 예제에서는 그리드를 사용하여 몇 가지 단추 및 텍스트 위치를 지정하는 것을 보여 줍니다. 셀의 너비와 높이가 설정 된 알림 <xref:System.Windows.GridUnitType.Auto>따라서 이미지가 있는 단추가 포함 된 셀이 이미지에 맞게 조정 합니다.  

 [!code-xaml[LocalizationGrid#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#1)]  
  
 다음 그래픽에서는 이전 코드로 생성된 그리드를 보여 줍니다.  
  
 ![그리드 예제](../../../../docs/framework/wpf/advanced/media/glob-grid.png "glob_grid")  
표  
  
<a name="autolay_grids_issharedsizescope"></a>   
## <a name="automatic-layout-and-grids-using-the-issharedsizescope-property"></a>IsSharedSizeScope 속성을 사용하는 자동 레이아웃 및 그리드  
 <xref:System.Windows.Controls.Grid> 요소 내용에 맞게 조정 되는 컨트롤을 만들려면 지역화 가능 응용 프로그램에 유용 합니다. 그러나 경우에 따라 콘텐츠에 관계없이 컨트롤을 특정 크기로 유지하려고 할 수 있습니다. 예를 들어 "확인", "취소" 및 "찾아보기" 단추가 있는 경우 콘텐츠에 맞게 단추 크기를 조정하지 않을 수 있습니다. 이 경우에 <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A?displayProperty=nameWithType> 연결 된 속성은 여러 그리드 요소 간에 동일한 크기 조정을 공유 하는 데 유용 합니다. 다음 예제에서는 열 및 행 크기 조정 여러 간에 데이터를 공유 하는 방법에 설명 <xref:System.Windows.Controls.Grid> 요소입니다.  
  
 [!code-xaml[gridIssharedsizescopeProp#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#2)]  
  
 **참고** 전체 코드 샘플을 보려면 [그리드 간 공유 크기 조정 속성](../../../../docs/framework/wpf/controls/how-to-share-sizing-properties-between-grids.md)  
  
## <a name="see-also"></a>참고 항목  
 [WPF의 전역화](../../../../docs/framework/wpf/advanced/globalization-for-wpf.md)  
 [자동 레이아웃을 사용하여 단추 만들기](../../../../docs/framework/wpf/advanced/how-to-use-automatic-layout-to-create-a-button.md)  
 [자동 레이아웃에 그리드 사용](../../../../docs/framework/wpf/advanced/how-to-use-a-grid-for-automatic-layout.md)
