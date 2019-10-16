---
title: 자동 레이아웃 사용 개요
ms.date: 03/30/2017
helpviewer_keywords:
- layout [WPF], automatic
- automatic layout [WPF]
ms.assetid: 6fed9264-18bb-4d05-8867-1fe356c6f687
ms.openlocfilehash: 2fe473da3eeabef3852e3003e61b3b9604332855
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291263"
---
# <a name="use-automatic-layout-overview"></a>자동 레이아웃 사용 개요

이 항목에서는 지역화할 수 있는 Ui (사용자 인터페이스)로 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 응용 프로그램을 작성 하는 방법에 대 한 개발자를 위한 지침을 제공 합니다 과거에는 UI를 지역화할 때 시간이 오래 걸립니다. UI에 맞게 조정 된 각 언어 마다 픽셀 조정을 통해 픽셀을 조정 해야 합니다. 오늘날 올바른 디자인 및 올바른 코딩 표준을 사용 하 여 지역화 담당자가 크기 조정 하 고 위치를 조정할 수 있도록 Ui를 생성할 수 있습니다. 보다 쉽게 크기를 조정 하 고 위치를 변경할 수 있는 응용 프로그램을 작성 하는 방법은 자동 레이아웃 이라고 하며, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램 디자인을 사용 하 여 달성할 수 있습니다.

<a name="advantages_of_autolayout"></a>

## <a name="advantages-of-using-automatic-layout"></a>자동 레이아웃 사용의 이점

@No__t-0 프레젠테이션 시스템은 강력 하 고 유연 하므로 다양 한 언어의 요구 사항에 맞게 조정할 수 있는 응용 프로그램의 요소를 레이아웃 하는 기능을 제공 합니다. 다음 목록에서는 자동 레이아웃의 몇 가지 이점을 보여 줍니다.

- UI는 모든 언어에서 잘 표시 됩니다.

- 텍스트가 변환된 후 컨트롤의 위치 및 크기를 다시 조정할 필요가 줄어듭니다.

- 창 크기를 다시 조정할 필요가 줄어듭니다.

- UI 레이아웃은 모든 언어로 적절히 렌더링 됩니다.

- 지역화를 문자열 변환 정도의 수준으로 줄일 수 있습니다.

<a name="autolayout_controls"></a>

## <a name="automatic-layout-and-controls"></a>자동 레이아웃 및 컨트롤

자동 레이아웃을 사용하면 애플리케이션에서 컨트롤의 크기를 자동으로 조정할 수 있습니다. 예를 들어 컨트롤이 문자열의 길이 맞게 변경될 수 있습니다. 이 기능을 통해 로컬라이저는 문자열을 변환할 수 있으며, 더 이상 변환된 텍스트에 맞게 컨트롤의 크기를 조정할 필요가 없습니다. 다음 예제에서는 영어 콘텐츠가 있는 단추를 만듭니다.

[!code-xaml[LocalizationBtn_snip#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn_snip/CS/Pane1.xaml#1)]

이 예제에서 스페인어 단추를 만들려면 텍스트만 변경하면 됩니다. 예를 들면 다음과 같습니다.

[!code-xaml[LocalizationBtn#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn/CS/Pane1.xaml#1)]

다음 그림은 코드 샘플의 출력을 보여 줍니다.

![텍스트가 여러 언어로 표시되는 동일한 단추](./media/use-automatic-layout-overview/auto-resizable-button.png)

<a name="autolayout_coding"></a>

## <a name="automatic-layout-and-coding-standards"></a>자동 레이아웃 및 코딩 표준

자동 레이아웃 방법을 사용 하려면 코딩 및 디자인 표준 및 규칙 집합을 사용 하 여 완전히 지역화 가능한 UI를 생성 해야 합니다. 다음은 자동 레이아웃 코딩에 도움이 되는 지침입니다.

**절대 위치 사용 안 함**

- 요소를 절대적으로 배치 하므로 <xref:System.Windows.Controls.Canvas>을 사용 하지 마십시오.

- @No__t-0, <xref:System.Windows.Controls.StackPanel>, <xref:System.Windows.Controls.Grid>를 사용 하 여 컨트롤을 배치 합니다.

다양 한 패널 형식에 대 한 자세한 내용은 [패널 개요](../controls/panels-overview.md)를 참조 하세요.

**창에 고정 크기를 설정 하지 않습니다.**

- 대신 <xref:System.Windows.Window.SizeToContent%2A?displayProperty=nameWithType>를 예를 들어 다음과 같은 가치를 제공해야 합니다.

  [!code-xaml[LocalizationGrid#2](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#2)]

**@No__t 추가-1**

- 응용 프로그램의 루트 요소에 <xref:System.Windows.FrameworkElement.FlowDirection%2A>을 추가 합니다.

  WPF는 가로, 양방향 및 세로 레이아웃을 지 원하는 편리한 방법을 제공 합니다. 프레젠테이션 프레임 워크에서 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 속성은 레이아웃을 정의 하는 데 사용할 수 있습니다. 흐름 방향 패턴은 다음과 같습니다.

  - <xref:System.Windows.FlowDirection.LeftToRight?displayProperty=nameWithType> (LrTb)-라틴어, 동아시아 등의 가로 레이아웃.

  - <xref:System.Windows.FlowDirection.RightToLeft?displayProperty=nameWithType> (RlTb)-아랍어, 히브리어 등의 경우 양방향입니다.

**실제 글꼴 대신 복합 글꼴 사용**

- 복합 글꼴을 사용 하는 경우 <xref:System.Windows.Controls.Control.FontFamily%2A> 속성을 지역화할 필요가 없습니다.

- 개발자는 다음 글꼴 중 하나를 사용하거나 직접 만들 수 있습니다.

  - 전역 사용자 인터페이스
  - 전역 San Serif
  - 전역 Serif

**Xml 추가: lang**

- UI의 루트 요소에 `xml:lang` 특성을 추가 합니다 (예: 영어 응용 프로그램의 경우 `xml:lang="en-US"`).

- 합성 글꼴은 `xml:lang`을 사용 하 여 사용할 글꼴을 결정 하므로 다국어 시나리오를 지원 하도록이 속성을 설정 합니다.

<a name="autolay_grids"></a>

## <a name="automatic-layout-and-grids"></a>자동 레이아웃 및 그리드

@No__t-0 요소는 개발자가 요소를 배치할 수 있도록 자동 레이아웃에 유용 합니다. @No__t-0 컨트롤은 열 및 행 정렬을 사용 하 여 사용 가능한 공간을 자식 요소 간에 배포할 수 있습니다. UI 요소는 여러 셀에 걸쳐 있을 수 있으며 그리드 내에 표가 있을 수 있습니다. 표를 사용 하면 복잡 한 UI를 만들고 배치할 수 있으므로 유용 합니다. 다음 예제에서는 그리드를 사용하여 몇 가지 단추 및 텍스트 위치를 지정하는 것을 보여 줍니다. 셀의 높이와 너비가 <xref:System.Windows.GridUnitType.Auto>으로 설정 되어 있는지 확인 합니다. 따라서 이미지가 포함 된 단추가 포함 된 셀은 이미지에 맞게 조정 됩니다.

[!code-xaml[LocalizationGrid#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#1)]

다음 그래픽에서는 이전 코드로 생성된 그리드를 보여 줍니다.

![표 형태 예](./media/glob-grid.png "glob_grid") grid

<a name="autolay_grids_issharedsizescope"></a>

## <a name="automatic-layout-and-grids-using-the-issharedsizescope-property"></a>IsSharedSizeScope 속성을 사용하는 자동 레이아웃 및 그리드

@No__t-0 요소는 지역화할 수 있는 응용 프로그램에서 내용에 맞게 조정 되는 컨트롤을 만드는 데 유용 합니다. 그러나 경우에 따라 콘텐츠에 관계없이 컨트롤을 특정 크기로 유지하려고 할 수 있습니다. 예를 들어 "확인", "취소" 및 "찾아보기" 단추가 있는 경우 콘텐츠에 맞게 단추 크기를 조정하지 않을 수 있습니다. 이 경우 <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A?displayProperty=nameWithType>에 연결 된 속성은 여러 grid 요소에서 동일한 크기 조정을 공유 하는 데 유용 합니다. 다음 예에서는 여러 <xref:System.Windows.Controls.Grid> 요소 사이에서 열 및 행 크기 조정 데이터를 공유 하는 방법을 보여 줍니다.

[!code-xaml[gridIssharedsizescopeProp#2](~/samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#2)]

> [!NOTE]
> 전체 코드 샘플을 보려면 [모눈 간 크기 조정 속성 공유](../controls/how-to-share-sizing-properties-between-grids.md)를 참조 하세요.

## <a name="see-also"></a>참조

- [WPF의 전역화](globalization-for-wpf.md)
- [자동 레이아웃을 사용하여 단추 만들기](how-to-use-automatic-layout-to-create-a-button.md)
- [자동 레이아웃에 그리드 사용](how-to-use-a-grid-for-automatic-layout.md)
