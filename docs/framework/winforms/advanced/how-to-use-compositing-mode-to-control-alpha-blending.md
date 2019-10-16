---
title: '방법: 혼합 모드를 사용하여 알파 혼합 조절'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- alpha blending [Windows Forms], compositing
- colors [Windows Forms], blending
- colors [Windows Forms], controlling transparency
ms.assetid: f331df2d-b395-4b0a-95be-24fec8c9bbb5
ms.openlocfilehash: 6863e59efa25323f80933bf8ab595316b430ef53
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65590132"
---
# <a name="how-to-use-compositing-mode-to-control-alpha-blending"></a>방법: 혼합 모드를 사용하여 알파 혼합 조절
다음 특성을 가진 오프 스크린 비트맵을 만들려고 하는 상황이 있을 수 있습니다.  
  
- 색의 알파 값을 255 보다 작은 경우  
  
- 색은 알파 비트맵을 만들 때 서로 혼합 합니다.  
  
- 완성 된 비트맵을 표시 하는 경우 비트맵 색 디스플레이 장치에서 배경 색과 혼합 된 알파가입니다.  
  
 이러한 비트맵을 만들려면 빈 생성 <xref:System.Drawing.Bitmap> 개체를 생성 한 다음는 <xref:System.Drawing.Graphics> 해당 비트맵을 기반으로 하는 개체입니다. 혼합 모드를 설정 합니다 <xref:System.Drawing.Graphics> 개체를 <xref:System.Drawing.Drawing2D.CompositingMode.SourceCopy?displayProperty=nameWithType>입니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 <xref:System.Drawing.Graphics> 기준으로 개체를 <xref:System.Drawing.Bitmap> 개체입니다. 코드를 사용 하는 <xref:System.Drawing.Graphics> 두 반투명 브러시와 함께 개체 (알파 = 160) 비트맵에 그릴 합니다. 코드는 빨간색 타원을 및 반투명 브러시를 사용 하 여 녹색 타원을 채웁니다. 녹색 타원 겹치는 빨간색 타원 있지만 때문에 녹색 빨간색 혼합 되지는 않습니다의 합성 모드를 <xref:System.Drawing.Graphics> 개체를로 <xref:System.Drawing.Drawing2D.CompositingMode.SourceCopy>합니다.  
  
 코드를 화면에 두 번 비트맵을 그립니다: 및 한 번 컬러 배경에 흰색 배경에서 한 번입니다. 타원 두 개의 포함 된 비트맵의 픽셀 160, 알파 구성 요소가 없으므로 화면의 배경 색과 혼합 되는 줄임표 합니다.  
  
 다음 그림에서는 코드 예제의 출력을 보여줍니다. 줄임표는 백그라운드와 혼합 되어 있지만 서로 혼합 하지 되는 note 합니다.  
  
 ![다이어그램 표시 줄임표 하지 서로 배경색과 혼합 됩니다.](./media/how-to-use-compositing-mode-to-control-alpha-blending/ellipses-blended-background.png)  
  
 이 문을 포함 하는 코드 예제:  
  
 [!code-csharp[System.Drawing.AlphaBlending#41](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.AlphaBlending#41](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#41)]  
  
 배경 물론 서로 혼합 수에 있는 줄임표를 하려는 경우 해당 문을 다음과 변경:  
  
 [!code-csharp[System.Drawing.AlphaBlending#42](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#42)]
 [!code-vb[System.Drawing.AlphaBlending#42](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#42)]  
  
 다음 그림에서는 수정 된 코드의 출력을 보여줍니다.  
  
 ![줄임표를 보여주는 다이어그램 배경을 사용 하 여 함께 혼합 됩니다.](./media/how-to-use-compositing-mode-to-control-alpha-blending/blend-ellipses-background.png)  
  
 [!code-csharp[System.Drawing.AlphaBlending#43](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#43)]
 [!code-vb[System.Drawing.AlphaBlending#43](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#43)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows Forms에서 사용 하도록 설계 되었으며 필요 <xref:System.Windows.Forms.PaintEventArgs> `e`의 매개 변수인 <xref:System.Windows.Forms.PaintEventHandler>합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Color.FromArgb%2A>
- [선 및 채우기 알파 혼합](alpha-blending-lines-and-fills.md)
