---
title: '방법: 불투명 및 반투명 브러시를 사용하여 그리기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- semi-transparent shapes [Windows Forms], drawing
- transparency [Windows Forms], semi-transparent shapes
- alpha blending [Windows Forms], brush
- brushes [Windows Forms], using semi-transparent
ms.assetid: a4f6f6b8-3bc8-440a-84af-d62ef0f8ff40
ms.openlocfilehash: 1be3fd2ce10f6681e531559a6e9594fe3d021f5f
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65582587"
---
# <a name="how-to-draw-with-opaque-and-semitransparent-brushes"></a>방법: 불투명 및 반투명 브러시를 사용하여 그리기
셰이프를 채울 때 <xref:System.Drawing.Brush> 개체를 <xref:System.Drawing.Graphics> 클래스의 채우기 메서드 중 하나에 전달해야 합니다. <xref:System.Drawing.SolidBrush.%23ctor%2A> 생성자의 매개 변수 중 하나는 <xref:System.Drawing.Color> 개체입니다. 불투명 셰이프를 채우려면 색의 알파 구성 요소를 255로 설정합니다. 반투명 셰이프를 채우려면 알파 구성 요소를 1에서 254 사이의 임의 값으로 설정합니다.  
  
 반투명 셰이프를 채우면 셰이프 색이 배경색과 혼합됩니다. 알파 구성 요소는 셰이프 색과 배경색을 혼합하는 방법을 지정합니다. 알파 값이 0에 가까우면 배경색에 더 많은 가중치가 적용되고 알파 값이 255에 가까우면 셰이프 색에 더 많은 가중치가 적용됩니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 비트맵을 그린 다음 이 비트맵과 겹치는 세 개의 타원을 채웁니다. 첫 번째 타원은 알파 구성 요소 255를 사용하므로 불투명합니다. 두 번째 및 세 번째 타원은 알파 구성 요소 128을 사용하므로 반투명합니다. 타원을 통과하는 배경 이미지를 볼 수 있습니다. <xref:System.Drawing.Graphics.CompositingQuality%2A> 속성을 설정하는 호출은 감마 보정과 함께 세 번째 타원에 대한 혼합이 수행되도록 합니다.  

 [!code-csharp[System.Drawing.AlphaBlending#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.AlphaBlending#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#31)]  

 다음 그림에서는 다음 코드의 출력을 보여 줍니다. 
  
 ![불투명 및 반투명 출력을 보여 주는 그림입니다.](./media/how-to-draw-with-opaque-and-semitransparent-brushes/compositingquality-ellipse-semitransparent.png)  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows Forms에서 사용 하도록 설계 되었으며 필요 <xref:System.Windows.Forms.PaintEventArgs> `e`의 매개 변수인 <xref:System.Windows.Forms.PaintEventHandler>합니다.  
  
## <a name="see-also"></a>참고자료

- [Windows Forms의 그래픽 및 그리기](graphics-and-drawing-in-windows-forms.md)
- [선 및 채우기 알파 혼합](alpha-blending-lines-and-fills.md)
- [방법: 컨트롤에 투명 한 배경을 제공합니다](../controls/how-to-give-your-control-a-transparent-background.md)
- [방법: 불투명 및 반투명 선 그리기](how-to-draw-opaque-and-semitransparent-lines.md)
