---
title: '방법: 요소의 높이 속성 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- height properties [WPF]
- Panel control [WPF], height properties of elements
ms.assetid: 5ab9e781-dbb8-469a-a3c8-cf38ce312647
ms.openlocfilehash: fb655630336c3b69afdc726a2e3c5a2cb8838667
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62024419"
---
# <a name="how-to-set-the-height-properties-of-an-element"></a>방법: 요소의 높이 속성 설정
## <a name="example"></a>예제  
 이 예제에서는 시각적으로 렌더링 동작의 네 가지 높이 관련 속성 간의 차이점을 보여 줍니다 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]합니다.  
  
 <xref:System.Windows.FrameworkElement> 클래스는 요소의 높이 특성을 설명 하는 네 가지 속성을 표시 합니다. 이러한 네 가지 속성 충돌할 수 있습니다 하 고 그럴 경우 우선적으로 적용 하는 값을 다음과 같이 결정 됩니다:는 <xref:System.Windows.FrameworkElement.MinHeight%2A> 값 보다 우선 합니다 <xref:System.Windows.FrameworkElement.MaxHeight%2A> 에 우선 하는 값은 <xref:System.Windows.FrameworkElement.Height%2A> 값. 네 번째 속성인 <xref:System.Windows.FrameworkElement.ActualHeight%2A>, 읽기 전용 이며 레이아웃 프로세스와의 상호 작용에 의해 결정 된 실제 높이 보고 합니다.  
  
 다음 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 예제 그리기는 <xref:System.Windows.Shapes.Rectangle> 요소 (`rect1`)의 자식으로 <xref:System.Windows.Controls.Canvas>입니다. 높이 속성을 변경할 수는 <xref:System.Windows.Shapes.Rectangle> 일련의를 사용 하 여 <xref:System.Windows.Controls.ListBox> 의 속성 값을 나타내는 요소 <xref:System.Windows.FrameworkElement.MinHeight%2A>, <xref:System.Windows.FrameworkElement.MaxHeight%2A>, 및 <xref:System.Windows.FrameworkElement.Height%2A>. 이런 방식으로 각 속성의 우선 순위를 시각적으로 표시 됩니다.  
  
 [!code-xaml[HeightMinHeightMaxHeight#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HeightMinHeightMaxHeight/CSharp/Window1.xaml#1)]  
[!code-xaml[HeightMinHeightMaxHeight#2](~/samples/snippets/csharp/VS_Snippets_Wpf/HeightMinHeightMaxHeight/CSharp/Window1.xaml#2)]  
  
 다음 코드 숨김 예제에서는 이벤트를 처리 하는 <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> 이벤트를 발생 시킵니다. 각 처리기에서 입력을 가져와 합니다 <xref:System.Windows.Controls.ListBox>, 값을 구문 분석을 <xref:System.Double>, 지정한 높이 관련 된 속성에 값을 적용 하 고 합니다. 높이 값 또한 문자열로 변환 되 고 다양 한 쓸 <xref:System.Windows.Controls.TextBlock> 요소 (해당 요소의 정의 선택한 XAML에는 표시 되지 않습니다).  
  
 [!code-csharp[HeightMinHeightMaxHeight#3](~/samples/snippets/csharp/VS_Snippets_Wpf/HeightMinHeightMaxHeight/CSharp/Window1.xaml.cs#3)]
 [!code-vb[HeightMinHeightMaxHeight#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HeightMinHeightMaxHeight/VisualBasic/Window1.xaml.vb#3)]  
  
 전체 샘플을 참조 하세요 [높이 속성 샘플](https://go.microsoft.com/fwlink/?LinkID=159993)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.FrameworkElement>
- <xref:System.Windows.Controls.ListBox>
- <xref:System.Windows.FrameworkElement.ActualHeight%2A>
- <xref:System.Windows.FrameworkElement.MaxHeight%2A>
- <xref:System.Windows.FrameworkElement.MinHeight%2A>
- <xref:System.Windows.FrameworkElement.Height%2A>
- [요소의 너비 속성 설정](how-to-set-the-width-properties-of-an-element.md)
- [패널 개요](panels-overview.md)
- [높이 속성 샘플](https://go.microsoft.com/fwlink/?LinkID=159993)
