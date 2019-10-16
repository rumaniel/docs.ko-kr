---
title: '방법: 그라데이션에 감마 보정 적용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- gradient brushes [Windows Forms], gamma correction
- gradients [Windows Forms], gamma correction
ms.assetid: da4690e7-5fac-4fd2-b3f0-5cb35c165b92
ms.openlocfilehash: e812e441233c1d29a67dac639048e20a659549f0
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64753561"
---
# <a name="how-to-apply-gamma-correction-to-a-gradient"></a>방법: 그라데이션에 감마 보정 적용
브러시의을 설정 하 여 선형 그라데이션 브러시에 대 한 감마 보정을 사용할 수 있습니다 <xref:System.Drawing.Drawing2D.LinearGradientBrush.GammaCorrection%2A> 속성을 `true`입니다. 감마 보정을 사용 하지 않도록 설정 하 여 수를 <xref:System.Drawing.Drawing2D.LinearGradientBrush.GammaCorrection%2A> 속성을 `false`입니다. 감마 보정은 기본적으로 비활성화 됩니다.  
  
## <a name="example"></a>예제  

컨트롤에서 호출 되는 방법은 다음 예제에서는 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기입니다. 선형 그라데이션 브러시를 만들고 두 사각형에 맞게 해당 브러시를 사용 하는 예제입니다. 첫 번째 사각형 감마 보정 하지 않고 채워지고 감마 보정을 사용 하 여 두 번째 사각형 채워집니다.  
  
 다음 그림에서는 두 개의 채워진된 사각형을 보여 줍니다. 감마 보정 되지 않은, 맨 위 사각형 중간에 어두운 표시 됩니다. 감마 보정에는 아래 사각형 농도가 좀 더 균일에 나타납니다.  
  
 ![두 그라데이션 채워진 사각형 감마 보정 하지 않고 사용 하 여 합니다.](./media/how-to-apply-gamma-correction-to-a-gradient/two-rectangles-gamma-gradient.png)  
  
 [!code-csharp[System.Drawing.UsingaGradientBrush#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.UsingaGradientBrush#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#31)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows forms에서 사용하도록 설계되었으며 <xref:System.Windows.Forms.Control.Paint> 이벤트 처리기의 매개 변수인 <xref:System.Windows.Forms.PaintEventArgs> `e`가 필요합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Drawing2D.LinearGradientBrush?displayProperty=nameWithType>
- [그라데이션 브러시를 사용하여 도형 채우기](using-a-gradient-brush-to-fill-shapes.md)
