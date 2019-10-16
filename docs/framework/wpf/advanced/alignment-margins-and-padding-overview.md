---
title: 맞춤, 여백 및 안쪽 여백 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- margins [WPF]
- padding [WPF]
- aligning [WPF]
ms.assetid: 9c6a2009-9b86-4e40-8605-0a2664dc3973
ms.openlocfilehash: bf351b6df972dc992f214ddfe899bfa808d0cd53
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963644"
---
# <a name="alignment-margins-and-padding-overview"></a>맞춤, 여백 및 안쪽 여백 개요
클래스 <xref:System.Windows.FrameworkElement> 는 자식 요소를 정확 하 게 배치 하는 데 사용 되는 여러 속성을 노출 합니다. 이 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>항목에서는 <xref:System.Windows.FrameworkElement.Margin%2A> ,<xref:System.Windows.Controls.Border.Padding%2A>, 및<xref:System.Windows.FrameworkElement.VerticalAlignment%2A>의 가장 중요 한 속성 중 4 가지를 설명 합니다. [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 응용 프로그램에서의 요소 위치를 제어하기 위한 기반을 제공하기 때문에 이 속성의 결과를 이해하는 것이 중요합니다.  

<a name="wcpsdk_layout_amp_introduction"></a>   
## <a name="introduction-to-element-positioning"></a>요소 위치 지정 소개  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]를 사용하여 요소를 배치하는 방법은 여러 가지가 있습니다. 그러나 이상적인 레이아웃을 달성 하는 것은 단순히 올바른 <xref:System.Windows.Controls.Panel> 요소를 선택 하는 것 이상으로 진행 됩니다. <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>위치 지정 <xref:System.Windows.FrameworkElement.Margin%2A> 을세밀하게<xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 제어 하려면, ,및속성을이해해야합니다.<xref:System.Windows.Controls.Border.Padding%2A>  
  
 다음 그림에서는 여러 위치 지정 속성을 사용하는 레이아웃 시나리오를 보여줍니다.  
  
 ![WPF 위치 지정 속성 샘플](./media/layout-margins-padding-alignment-graphic1.PNG "layout_margins_padding_alignment_graphic1")  
  
 처음에는이 그림 <xref:System.Windows.Controls.Button> 의 요소가 무작위로 배치 된 것 처럼 보일 수 있습니다. 그러나 해당 위치는 여백, 맞춤 및 안쪽 여백의 조합을 사용하여 실제로 정확하게 제어됩니다.  
  
 다음 예제에서는 앞의 그림에서 레이아웃을 만드는 방법을 설명합니다. 요소 <xref:System.Windows.Controls.Border> 는 <xref:System.Windows.Controls.Border.Padding%2A> 값이 15 <xref:System.Windows.Controls.StackPanel>인 장치 독립적 픽셀을 사용 하 여 부모를 캡슐화 합니다. 이는 자식을 <xref:System.Windows.Controls.StackPanel>둘러싸는 좁은 <xref:System.Windows.Media.Brushes.LightBlue%2A> 대역에 대 한 계정입니다. 의 자식 요소는 <xref:System.Windows.Controls.StackPanel> 이 항목에서 자세히 설명 하는 다양 한 위치 지정 속성을 설명 하는 데 사용 됩니다. <xref:System.Windows.FrameworkElement.Margin%2A> <xref:System.Windows.Controls.Button> 및<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 속성을 모두 보여 주기 위해 세 가지 요소가 사용 됩니다.  
  
 [!code-csharp[MPALayoutSampleIntro#1](~/samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutSampleIntro/CSharp/MPA_Layout_Sample_Intro.cs#1)]
 [!code-vb[MPALayoutSampleIntro#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutSampleIntro/VisualBasic/MPALayoutIntro.vb#1)]  
  
 다음 다이어그램은 이전 샘플에서 사용되는 다양한 위치 지정 속성의 자세히 보기를 제공합니다. 이 항목의 후속 섹션에서는 각 위치 지정 속성을 사용하는 방법을 자세히 설명합니다.  
  
 ![화면 호출을 사용하여 속성 위치 지정](./media/layout-margins-padding-alignment-graphic2.PNG "layout_margins_padding_alignment_graphic2")  
  
<a name="wcpsdk_layout_amp_alignment_properties"></a>   
## <a name="understanding-alignment-properties"></a>맞춤 속성 이해  
 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 및<xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 속성은 부모 요소의 할당 된 레이아웃 공간 내에 자식 요소를 배치 하는 방법을 설명 합니다. 이러한 속성을 함께 사용하여 자식 요소를 정확하게 배치할 수 있습니다. 예를 들어의 자식 요소는 <xref:System.Windows.Controls.DockPanel> , <xref:System.Windows.HorizontalAlignment.Right>또는 <xref:System.Windows.HorizontalAlignment.Center> <xref:System.Windows.HorizontalAlignment.Stretch> 의 4 가지 가로 맞춤 <xref:System.Windows.HorizontalAlignment.Left>을 지정 하 여 사용 가능한 공간을 채울 수 있습니다. 비슷한 값을 세로 위치 지정에 사용할 수 있습니다.  
  
> [!NOTE]
> 요소의 명시적 설정 <xref:System.Windows.FrameworkElement.Height%2A> 및 <xref:System.Windows.FrameworkElement.Width%2A> 속성은 <xref:System.Windows.HorizontalAlignment.Stretch> 속성 값 보다 우선 합니다. , <xref:System.Windows.FrameworkElement.Height%2A> 및<xref:System.Windows.FrameworkElement.Width%2A>값 을설정<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 하려고 하면 요청이`Stretch`무시됩니다. `Stretch`  
  
<a name="wcpsdk_layout_amp_horizontalalignment_properties"></a>   
### <a name="horizontalalignment-property"></a>HorizontalAlignment 속성  
 속성 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 은 자식 요소에 적용할 가로 맞춤 특성을 선언 합니다. 다음 표에서는 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 속성의 가능한 각 값을 보여 줍니다.  
  
|멤버|설명|  
|------------|-----------------|  
|<xref:System.Windows.HorizontalAlignment.Left>|자식 요소는 부모 요소의 할당된 레이아웃 공간의 왼쪽에 정렬됩니다.|  
|<xref:System.Windows.HorizontalAlignment.Center>|자식 요소는 부모 요소의 할당된 레이아웃 공간의 중앙에 정렬됩니다.|  
|<xref:System.Windows.HorizontalAlignment.Right>|자식 요소는 부모 요소의 할당된 레이아웃 공간의 오른쪽에 정렬됩니다.|  
|<xref:System.Windows.HorizontalAlignment.Stretch>기본|자식 요소는 부모 요소의 할당된 레이아웃 공간을 채우도록 확장됩니다. 명시적 <xref:System.Windows.FrameworkElement.Width%2A> 및<xref:System.Windows.FrameworkElement.Height%2A> 값이 우선적으로 적용 됩니다.|  
  
 다음 예제에서는 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 속성을 요소에 <xref:System.Windows.Controls.Button> 적용 하는 방법을 보여 줍니다. 다양한 렌더링 동작의 이해를 돕기 위해 각 특성 값이 표시됩니다.  
  
 [!code-csharp[MPALayoutHorizontalAlignment#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutHorizontalAlignment/CSharp/MPA_Layout_HorizontalAlignment.cs#2)]
 [!code-vb[MPALayoutHorizontalAlignment#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutHorizontalAlignment/VisualBasic/MPA_Layout_HorizontalAlignment.vb#2)]  
  
 앞의 코드는 다음 이미지와 비슷한 레이아웃을 만듭니다. 각 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 값의 위치 지정 효과는 그림에 표시 됩니다.  
  
 ![HorizontalAlignment 샘플](./media/layout-horizontal-alignment-graphic.PNG "layout_horizontal_alignment_graphic")  
  
<a name="wcpsdk_layout_amp_verticalalignment_properties"></a>   
### <a name="verticalalignment-property"></a>VerticalAlignment 속성  
 속성 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 은 자식 요소에 적용할 세로 맞춤 특성을 설명 합니다. 다음 표에서는 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 속성에 사용할 수 있는 각 값을 보여 줍니다.  
  
|멤버|설명|  
|------------|-----------------|  
|<xref:System.Windows.VerticalAlignment.Top>|자식 요소는 부모 요소의 할당된 레이아웃 공간의 위에 정렬됩니다.|  
|<xref:System.Windows.VerticalAlignment.Center>|자식 요소는 부모 요소의 할당된 레이아웃 공간의 중앙에 정렬됩니다.|  
|<xref:System.Windows.VerticalAlignment.Bottom>|자식 요소는 부모 요소의 할당된 레이아웃 공간의 아래에 정렬됩니다.|  
|<xref:System.Windows.VerticalAlignment.Stretch>기본|자식 요소는 부모 요소의 할당된 레이아웃 공간을 채우도록 확장됩니다. 명시적 <xref:System.Windows.FrameworkElement.Width%2A> 및<xref:System.Windows.FrameworkElement.Height%2A> 값이 우선적으로 적용 됩니다.|  
  
 다음 예제에서는 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 속성을 요소에 <xref:System.Windows.Controls.Button> 적용 하는 방법을 보여 줍니다. 다양한 렌더링 동작의 이해를 돕기 위해 각 특성 값이 표시됩니다. 이 샘플 <xref:System.Windows.Controls.Grid> 의 목적을 위해 눈금선이 표시 된 요소가 각 속성 값의 레이아웃 동작을 보다 잘 보여 주기 위해 부모로 사용 됩니다.  
  
 [!code-csharp[MPALayoutVerticalAlignment#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutVerticalAlignment/CSharp/MPA_Layout_VerticalAlignment.cs#2)]
 [!code-vb[MPALayoutVerticalAlignment#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutVerticalAlignment/VisualBasic/MPA_Layout_VerticalAlignment.vb#2)]
 [!code-xaml[MPALayoutVerticalAlignment#2](~/samples/snippets/xaml/VS_Snippets_Wpf/MPALayoutVerticalAlignment/XAML/default.xaml#2)]  
  
 앞의 코드는 다음 이미지와 비슷한 레이아웃을 만듭니다. 각 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 값의 위치 지정 효과는 그림에 표시 됩니다.  
  
 ![VerticalAlignment 속성 샘플](./media/layout-vertical-alignment-graphic.PNG "layout_vertical_alignment_graphic")  
  
<a name="wcpsdk_layout_amp_margin_properties"></a>   
## <a name="understanding-margin-properties"></a>여백 속성 이해  
 속성 <xref:System.Windows.FrameworkElement.Margin%2A> 은 요소와 자식 또는 피어 간의 거리를 설명 합니다. <xref:System.Windows.FrameworkElement.Margin%2A>와 같은 `Margin="20"`구문을 사용 하 여 값을 균일 하 게 지정할 수 있습니다. 이 구문을 사용 하 여 요소 <xref:System.Windows.FrameworkElement.Margin%2A> 에 장치 독립적 픽셀의 균일 픽셀을 적용 합니다. <xref:System.Windows.FrameworkElement.Margin%2A>값은 4 개의 고유 값 형식으로 사용할 수 있습니다. 각 값은와 같이 `Margin="0,10,5,25"`왼쪽, 위쪽, 오른쪽 및 아래쪽 (순서 대로)에 적용할 고유한 여백을 설명 하는 값입니다. <xref:System.Windows.FrameworkElement.Margin%2A> 속성을 적절 하 게 사용 하면 요소의 렌더링 위치와 해당 인접 요소 및 자식의 렌더링 위치를 매우 세밀 하 게 제어할 수 있습니다.  
  
> [!NOTE]
> 0이 아닌 여백은 요소의 <xref:System.Windows.FrameworkElement.ActualWidth%2A> 및 <xref:System.Windows.FrameworkElement.ActualHeight%2A>외부에 공간을 적용 합니다.  
  
 다음 예제에서는 <xref:System.Windows.Controls.Button> 요소 그룹 주위에 균일 한 여백을 적용 하는 방법을 보여 줍니다. 각 방향에서 10 픽셀의 여백 버퍼와 함께 요소가균등하게배치됩니다.<xref:System.Windows.Controls.Button>  
  
 [!code-cpp[MarginPaddingAlignmentSample#1](~/samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#1)]
 [!code-csharp[MarginPaddingAlignmentSample#1](~/samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#1)]
 [!code-vb[MarginPaddingAlignmentSample#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#1)]
 [!code-xaml[MarginPaddingAlignmentSample#1](~/samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#1)]  
  
 대부분의 경우 균일한 여백이 적합하지 않습니다. 이러한 경우, 균일하지 않은 여백을 적용할 수 있습니다. 다음 예제에서는 자식 요소에 균일하지 않은 여백을 적용하는 방법을 보여 줍니다. 여백은 왼쪽, 위, 오른쪽, 아래의 순서로 설명됩니다.  
  
 [!code-cpp[MarginPaddingAlignmentSample#2](~/samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#2)]
 [!code-csharp[MarginPaddingAlignmentSample#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#2)]
 [!code-vb[MarginPaddingAlignmentSample#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#2)]
 [!code-xaml[MarginPaddingAlignmentSample#2](~/samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#2)]  
  
<a name="wcpsdk_layout_amp_padding_properties"></a>   
## <a name="understanding-the-padding-property"></a>안쪽 여백 속성 이해  
 안쪽 여백은 대부분 <xref:System.Windows.FrameworkElement.Margin%2A> 의 측면에서와 비슷합니다. 패딩 속성은 몇 가지 <xref:System.Windows.Documents.Block>클래스 (주로 편의상 <xref:System.Windows.Controls.Border> <xref:System.Windows.Controls.Control>,,, 및 <xref:System.Windows.Controls.TextBlock> 는 패딩 속성을 노출 하는 클래스의 샘플)에만 노출 됩니다. 속성 <xref:System.Windows.Controls.Border.Padding%2A> 은 지정 <xref:System.Windows.Thickness> 된 값을 기준으로 자식 요소의 유효 크기를 확대 합니다.  
  
 다음 예제에서는 부모 <xref:System.Windows.Controls.Border.Padding%2A> <xref:System.Windows.Controls.Border> 요소에를 적용 하는 방법을 보여 줍니다.  
  
 [!code-cpp[MarginPaddingAlignmentSample#3](~/samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#3)]
 [!code-csharp[MarginPaddingAlignmentSample#3](~/samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#3)]
 [!code-vb[MarginPaddingAlignmentSample#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#3)]
 [!code-xaml[MarginPaddingAlignmentSample#3](~/samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#3)]  
  
<a name="wcpsdk_layout_amp_summary"></a>   
## <a name="using-alignment-margins-and-padding-in-an-application"></a>애플리케이션에서 맞춤, 여백 및 안쪽 여백 사용  
 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>, <xref:System.Windows.FrameworkElement.Margin%2A>, 및<xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 는 복잡[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]한를 만드는 데 필요한 위치 지정 컨트롤을 제공 합니다. <xref:System.Windows.Controls.Border.Padding%2A> 각 속성의 결과를 사용하여 자식 요소 위치를 변경하면 동적 애플리케이션과 사용자 환경을 만드는 유연성을 사용할 수 있습니다.  
  
 다음 예제에서는 이 항목에 설명된 각 개념을 보여 줍니다. 이 항목의 첫 번째 샘플에서 볼 수 있는 인프라를 기반으로 하는이 <xref:System.Windows.Controls.Grid> 예제에서는 첫 번째 샘플 <xref:System.Windows.Controls.Border> 에서 요소를의 자식으로 추가 합니다. <xref:System.Windows.Controls.Border.Padding%2A>부모 <xref:System.Windows.Controls.Border> 요소에 적용 됩니다. 는 <xref:System.Windows.Controls.Grid> 세 개의 자식 <xref:System.Windows.Controls.StackPanel> 요소 간에 공간을 분할 하는 데 사용 됩니다. <xref:System.Windows.Controls.Button>요소는 및 <xref:System.Windows.FrameworkElement.Margin%2A> <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>의 다양 한 효과를 표시 하는 데 다시 사용 됩니다. <xref:System.Windows.Controls.TextBlock>각 열의 <xref:System.Windows.Controls.Button> 요소에 적용 <xref:System.Windows.Controls.ColumnDefinition> 되는 다양 한 속성을 더 잘 정의 하기 위해 요소를 각각에 추가 합니다.  
  
 [!code-cpp[MarginPaddingAlignmentSample#4](~/samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#4)]
 [!code-csharp[MarginPaddingAlignmentSample#4](~/samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#4)]
 [!code-vb[MarginPaddingAlignmentSample#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#4)]
 [!code-xaml[MarginPaddingAlignmentSample#4](~/samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#4)]  
  
 컴파일 시, 이전 애플리케이션은 다음 그림과 유사한 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]를 생성합니다. 다양 한 속성 값의 효과는 요소 사이의 간격에서 명확 하 게 표시 되 고 각 열의 요소에 대 한 중요 한 속성 값 <xref:System.Windows.Controls.TextBlock> 이 요소 내에 표시 됩니다.  
  
 ![한 응용 프로그램에서 여러 개의 위치 지정 속성](./media/layout-margins-padding-aligment-graphic3.PNG "layout_margins_padding_aligment_graphic3")  
  
<a name="wcpsdk_layout_amp_alignment_whatsnext"></a>   
## <a name="whats-next"></a>새로운 기능  
 <xref:System.Windows.FrameworkElement> 클래스에서 정의 된 위치 지정 속성을 사용 하면 응용 프로그램 내 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 에서 요소 배치를 세부적으로 제어할 수 있습니다. 이제 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]를 사용하여 요소 배치에 사용할 수 있는 여러 기술을 사용할 수 있습니다.  
  
 자세하게 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 레이아웃을 설명하는 추가 리소스를 사용할 수 있습니다. [패널 개요](../controls/panels-overview.md) 항목에는 다양 <xref:System.Windows.Controls.Panel> 한 요소에 대 한 자세한 정보가 포함 되어 있습니다. 연습 항목 [: 내 첫 번째 WPF 데스크톱](../getting-started/walkthrough-my-first-wpf-desktop-application.md) 응용 프로그램은 레이아웃 요소를 사용 하 여 구성 요소를 배치 하 고 해당 작업을 데이터 소스에 바인딩하는 고급 기술을 소개 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.FrameworkElement>
- <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>
- <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>
- <xref:System.Windows.FrameworkElement.Margin%2A>
- [패널 개요](../controls/panels-overview.md)
- [레이아웃](layout.md)
- [WPF 레이아웃 갤러리 샘플](https://go.microsoft.com/fwlink/?LinkID=160054)
