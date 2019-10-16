---
title: '방법: 요소의 너비 속성 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- width properties [WPF]
- Panel control [WPF], width properties of elements
ms.assetid: 6ee04a9d-63f0-4f5b-a406-0a8cd4c35729
ms.openlocfilehash: a5ed67ba20176398a863a1e9826b1eab71b182f2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62052042"
---
# <a name="how-to-set-the-width-properties-of-an-element"></a>방법: 요소의 너비 속성 설정
## <a name="example"></a>예제  
 이 예제에서는 시각적으로 렌더링의 너비와 관련 된 네 가지 속성 간의 동작 차이 보여 줍니다 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]합니다.  
  
 <xref:System.Windows.FrameworkElement> 클래스는 요소의 너비 특성을 설명 하는 네 가지 속성을 노출 합니다. 이러한 네 가지 속성 충돌할 수 있습니다 하 고 그럴 경우 우선적으로 적용 하는 값을 다음과 같이 결정 됩니다:는 <xref:System.Windows.FrameworkElement.MinWidth%2A> 값 보다 우선 합니다 <xref:System.Windows.FrameworkElement.MaxWidth%2A> 에 우선 하는 값은 <xref:System.Windows.FrameworkElement.Width%2A> 값. 네 번째 속성인 <xref:System.Windows.FrameworkElement.ActualWidth%2A>, 읽기 전용 이며 레이아웃 프로세스와의 상호 작용에 의해 결정 된 실제 너비를 보고 합니다.  
  
 다음 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 예제 그리기는 <xref:System.Windows.Shapes.Rectangle> 요소 (`rect1`)의 자식으로 <xref:System.Windows.Controls.Canvas>입니다. 너비 속성을 변경할 수 있습니다는 <xref:System.Windows.Shapes.Rectangle> 일련의를 사용 하 여 <xref:System.Windows.Controls.ListBox> 의 속성 값을 나타내는 요소 <xref:System.Windows.FrameworkElement.MinWidth%2A>를 <xref:System.Windows.FrameworkElement.MaxWidth%2A>, 및 <xref:System.Windows.FrameworkElement.Width%2A>합니다. 이런 방식으로 각 속성의 우선 순위를 시각적으로 표시 됩니다.  
  
 [!code-xaml[WidthMinWidthMaxWidth#1](~/samples/snippets/csharp/VS_Snippets_Wpf/WidthMinWidthMaxWidth/CSharp/Window1.xaml#1)]  
[!code-xaml[WidthMinWidthMaxWidth#2](~/samples/snippets/csharp/VS_Snippets_Wpf/WidthMinWidthMaxWidth/CSharp/Window1.xaml#2)]  
  
 다음 코드 숨김 예제에서는 이벤트를 처리 하는 <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> 이벤트를 발생 시킵니다. 입력을 사용 하는 각 사용자 지정 메서드를 <xref:System.Windows.Controls.ListBox>, 값을 구문 분석를 <xref:System.Double>, 지정된 된 너비와 관련 된 속성에 값을 적용 합니다. 너비 값 또한 문자열로 변환 되 고 다양 한 쓸 <xref:System.Windows.Controls.TextBlock> 요소 (해당 요소의 정의 선택한 XAML에는 표시 되지 않습니다).  
  
 [!code-csharp[WidthMinWidthMaxWidth#3](~/samples/snippets/csharp/VS_Snippets_Wpf/WidthMinWidthMaxWidth/CSharp/Window1.xaml.cs#3)]
 [!code-vb[WidthMinWidthMaxWidth#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WidthMinWidthMaxWidth/VisualBasic/Window1.xaml.vb#3)]  
  
 전체 샘플을 참조 하세요 [너비 속성 비교 샘플](https://go.microsoft.com/fwlink/?LinkID=160050)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.ListBox>
- <xref:System.Windows.FrameworkElement>
- <xref:System.Windows.FrameworkElement.ActualWidth%2A>
- <xref:System.Windows.FrameworkElement.MaxWidth%2A>
- <xref:System.Windows.FrameworkElement.MinWidth%2A>
- <xref:System.Windows.FrameworkElement.Width%2A>
- [패널 개요](panels-overview.md)
- [요소의 높이 속성 설정](how-to-set-the-height-properties-of-an-element.md)
- [너비 속성 비교 샘플](https://go.microsoft.com/fwlink/?LinkID=160050)
