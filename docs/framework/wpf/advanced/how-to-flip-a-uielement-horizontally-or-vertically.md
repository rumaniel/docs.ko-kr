---
title: '방법: 가로 또는 세로로 UIElement 대칭 이동'
ms.date: 03/30/2017
helpviewer_keywords:
- flipping UIElements [WPF]
- UIElements [WPF], flipping
ms.assetid: 02c6730f-65c0-40d5-a553-4cb663721882
ms.openlocfilehash: 6b3da322493d17e4f8e36a35b9a0e40fdc9dc685
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61767055"
---
# <a name="how-to-flip-a-uielement-horizontally-or-vertically"></a>방법: 가로 또는 세로로 UIElement 대칭 이동
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.ScaleTransform> 대칭으로 배열할지를 <xref:System.Windows.UIElement> 가로나 세로 방향으로 합니다. 이 예제에서는 <xref:System.Windows.Controls.Button> 컨트롤 (유형의 <xref:System.Windows.UIElement>) 적용 하 여 대칭 이동를 <xref:System.Windows.Media.ScaleTransform> 에 해당 <xref:System.Windows.UIElement.RenderTransform%2A> 속성입니다.  
  
## <a name="example"></a>예제  
 다음 그림에서는 대칭 이동 하려면 단추를 보여 줍니다.  
  
 ![변형이 없는 단추](./media/graphicsmm-buttonflipbeforeflip.gif "graphicsmm_buttonflipbeforeflip")  
UIElement 대칭 이동  
  
 다음 단추를 만드는 코드를 보여줍니다.  
  
 [!code-xaml[Transforms_snip#GraphicsMMButtonWithoutFlip](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmbuttonwithoutflip)]  
  
## <a name="example"></a>예제  
 만들기 단추를 가로로 대칭 이동 하는 <xref:System.Windows.Media.ScaleTransform> 설정 및 해당 <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> 속성을-1입니다. 적용 된 <xref:System.Windows.Media.ScaleTransform> 단추를 <xref:System.Windows.UIElement.RenderTransform%2A> 속성입니다.  
  
 [!code-xaml[Transforms_snip#GraphicsMMFlipButtonExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmflipbuttonexample1)]  
  
 ![단추에 대 한 가로 대칭 이동 된 &#40;0, 0&#41;](./media/graphicsmm-buttonfliphorizontalflip-displaced.gif "graphicsmm_buttonfliphorizontalflip_displaced")  
ScaleTransform을 적용 한 후 단추  
  
## <a name="example"></a>예제  
 위의 그림에서 보듯이 단추 대칭 되는 이동 되었습니다. 단추를 왼쪽된 위 모서리에서 대칭 때문입니다. 적용 하려는 곳에서 단추를 뒤집고,는 <xref:System.Windows.Media.ScaleTransform> 해당 센터로 구석에 해당 되지 않습니다. 적용 하는 쉬운 방법을 합니다 <xref:System.Windows.Media.ScaleTransform> 단추를 가운데 단추를 설정 하는 <xref:System.Windows.UIElement.RenderTransformOrigin%2A> 속성을 0.5, 0.5입니다.  
  
 [!code-xaml[Transforms_snip#GraphicsMMFlipButtonExample2](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmflipbuttonexample2)]  
  
 ![가운데를 중심으로 가로 대칭 이동 된 단추](./media/graphicsmm-buttonfliphorizontalflip-inplace.gif "graphicsmm_buttonfliphorizontalflip_inplace")  
RenderTransformOrigin 0.5를 사용 하 여 단추 0.5  
  
## <a name="example"></a>예제  
 상하 대칭 이동 단추를 설정 합니다 <xref:System.Windows.Media.ScaleTransform> 개체의 <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> 속성 대신 해당 <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> 속성입니다.  
  
 [!code-xaml[Transforms_snip#GraphicsMMVerticalFlipButtonExample2](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/FlipExample.xaml#graphicsmmverticalflipbuttonexample2)]  
  
 ![가운데를 중심으로 세로 대칭 이동 된 단추](./media/graphicsmm-buttonflipverticalflip-inplace.gif "graphicsmm_buttonflipverticalflip_inplace")  
수직 대칭 이동 된 단추  
  
## <a name="see-also"></a>참고자료

- [Transform 개요](../graphics-multimedia/transforms-overview.md)
