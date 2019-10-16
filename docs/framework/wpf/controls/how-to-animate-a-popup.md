---
title: '방법: 팝업에 애니메이션 효과 주기'
ms.date: 03/30/2017
helpviewer_keywords:
- Popup control [WPF], animating
- animation [WPF], Popup controls
ms.assetid: acaa2a0a-6137-4efd-9cd1-75ece222e390
ms.openlocfilehash: b70d9c4cb1bca26a6c77d3a7c50add517ca8ef92
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61911289"
---
# <a name="how-to-animate-a-popup"></a>방법: 팝업에 애니메이션 효과 주기
두 가지 방법으로 애니메이션 효과를 보여 주는이 예제는 <xref:System.Windows.Controls.Primitives.Popup> 제어 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 합니다 <xref:System.Windows.Controls.Primitives.PopupAnimation> 속성의 값을 <xref:System.Windows.Controls.Primitives.PopupAnimation.Slide>, 있어는 <xref:System.Windows.Controls.Primitives.Popup> "슬라이드-in"으로 표시 되는 경우.  
  
 순환 하려면를 <xref:System.Windows.Controls.Primitives.Popup>, 지정 하는이 예제는 <xref:System.Windows.Media.RotateTransform> 에 <xref:System.Windows.UIElement.RenderTransform%2A> 속성을는 <xref:System.Windows.Controls.Canvas>의 자식 요소는는 <xref:System.Windows.Controls.Primitives.Popup>.  
  
 제대로 작동 하려면 변환에 대 한 예제 설정 해야 합니다 <xref:System.Windows.Controls.Primitives.Popup.AllowsTransparency%2A> 속성을 `true`입니다. 또한를 <xref:System.Windows.FrameworkElement.Margin%2A> 에 <xref:System.Windows.Controls.Canvas> 내용에 대 한 충분 한 공간을 지정 해야 합니다는 <xref:System.Windows.Controls.Primitives.Popup> 회전 하 합니다.  
  
 [!code-xaml[AnimatedPopup#RotateTransform2](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimatedPopup/CS/Window1.xaml#rotatetransform2)]  
  
 다음 예제에서는 어떻게를 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 발생 하는 이벤트 때를 <xref:System.Windows.Controls.Button> 를 클릭 하면 트리거는 <xref:System.Windows.Media.Animation.Storyboard> 애니메이션을 시작 하는.  
  
 [!code-xaml[AnimatedPopup#RotateTransform1](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimatedPopup/CS/Window1.xaml#rotatetransform1)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.UIElement.RenderTransform%2A>
- <xref:System.Windows.Controls.Primitives.BulletDecorator>
- <xref:System.Windows.Media.RotateTransform>
- <xref:System.Windows.Media.Animation.Storyboard>
- <xref:System.Windows.Controls.Primitives.Popup>
- [방법 항목](popup-how-to-topics.md)
- [팝업 개요](popup-overview.md)
