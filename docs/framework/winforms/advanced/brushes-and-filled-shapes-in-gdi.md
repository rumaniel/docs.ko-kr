---
title: GDI+의 브러시 및 채워진 도형
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [Windows Forms], GDI+
- filled shapes [Windows Forms], GDI+
- shapes [Windows Forms], GDI+
- GDI+, brushes
- GDI+, filled shapes
- gradient brushes
- brushes [Windows Forms], gradient
ms.assetid: e863e2a7-0294-4130-99b6-f1ea3201e7cd
ms.openlocfilehash: 45ef0b5920e43300e047d363149ea10a7833477b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69912224"
---
# <a name="brushes-and-filled-shapes-in-gdi"></a>GDI+의 브러시 및 채워진 도형
사각형 또는 타원과 같은 닫힌 도형은 윤곽선과 내부로 구성 됩니다. 펜을 사용 하 여 윤곽선을 그리고 내부가 브러시로 채워집니다. Gdi +는 <xref:System.Drawing.SolidBrush>닫힌 셰이프의 내부를 채우기 위한 몇 가지 브러시 클래스 <xref:System.Drawing.TextureBrush>, <xref:System.Drawing.Drawing2D.HatchBrush> <xref:System.Drawing.Drawing2D.LinearGradientBrush>,, 및 <xref:System.Drawing.Drawing2D.PathGradientBrush>를 제공 합니다. 이러한 클래스는 모두 <xref:System.Drawing.Brush> 클래스에서 상속 됩니다. 다음 그림에서는 단색 브러시와 빗살 무늬 브러시로 채워진 사각형을 보여 줍니다.  
  
 ![채워진 도형](./media/aboutgdip02-art17.gif "Aboutgdip02_art17")  
  
## <a name="solid-brushes"></a>단색 브러시  
 폐쇄형 셰이프를 채우려면 <xref:System.Drawing.Graphics> 클래스 <xref:System.Drawing.Brush>및의 인스턴스가 필요 합니다. <xref:System.Drawing.Graphics> 클래스의 인스턴스는 및 <xref:System.Drawing.Graphics.FillEllipse%2A>와 <xref:System.Drawing.Graphics.FillRectangle%2A> 같은 메서드를 제공 하 고 <xref:System.Drawing.Brush> , 색 및 패턴과 같은 채우기의 특성을 저장 합니다. 는 <xref:System.Drawing.Brush> fill 메서드에 대 한 인수 중 하나로 전달 됩니다. 다음 코드 예제에서는 빨강 빨강 색으로 타원을 채우는 방법을 보여 줍니다.  
  
 [!code-csharp[LinesCurvesAndShapes#121](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#121)]
 [!code-vb[LinesCurvesAndShapes#121](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#121)]  
  
> [!NOTE]
> 앞의 예제에서 브러시는에서 <xref:System.Drawing.SolidBrush> <xref:System.Drawing.Brush>상속 되는 형식입니다.  
  
## <a name="hatch-brushes"></a>빗살 무늬 브러시  
 빗살 무늬 브러시를 사용 하 여 도형을 채울 때 전경색, 배경색 및 빗살 무늬 스타일을 지정 합니다. 전경색은 해칭 색입니다.  
  
 [!code-csharp[LinesCurvesAndShapes#122](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#122)]
 [!code-vb[LinesCurvesAndShapes#122](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#122)]  
  
 GDI +는 50 이상의 빗살 무늬 스타일을 제공 합니다. 다음 그림 <xref:System.Drawing.Drawing2D.HatchStyle.Horizontal>에 표시 된 세 가지 스타일은, <xref:System.Drawing.Drawing2D.HatchStyle.ForwardDiagonal>및 <xref:System.Drawing.Drawing2D.HatchStyle.Cross>입니다.  
  
 ![채워진 도형](./media/aboutgdip02-art18.gif "Aboutgdip02_art18")  
  
## <a name="texture-brushes"></a>질감 브러시  
 질감 브러시를 사용 하 여 비트맵에 저장 된 패턴으로 셰이프를 채울 수 있습니다. 예를 들어 다음 그림은 라는 `MyTexture.bmp`디스크 파일에 저장 되어 있다고 가정 합니다.  
  
 ![채워진 도형](./media/aboutgdip02-art19.gif "Aboutgdip02_Art19")  
  
 다음 코드 예제에서는에 `MyTexture.bmp`저장 된 그림을 반복 하 여 타원을 채우는 방법을 보여 줍니다.  
  
 [!code-csharp[LinesCurvesAndShapes#123](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#123)]
 [!code-vb[LinesCurvesAndShapes#123](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#123)]  
  
 다음 그림에서는 채워진 타원을 보여 줍니다.  
  
 ![채워진 도형](./media/aboutgdip02-art20.gif "AboutGdip02_Art20")  
  
## <a name="gradient-brushes"></a>그라데이션 브러시  
 GDI +는 두 가지 종류의 그라데이션 브러시 (선형 및 경로)를 제공 합니다. 선형 그라데이션 브러시를 사용 하 여 도형을 가로, 세로 또는 대각선 방향으로 이동할 때 점차적으로 변하는 색으로 셰이프를 채울 수 있습니다. 다음 코드 예제에서는 타원의 왼쪽 가장자리에서 오른쪽 가장자리로 이동할 때 파란색에서 녹색으로 변경 되는 가로 그라데이션 브러시를 사용 하 여 타원을 채우는 방법을 보여 줍니다.  
  
 [!code-csharp[LinesCurvesAndShapes#124](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#124)]
 [!code-vb[LinesCurvesAndShapes#124](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#124)]  
  
 다음 그림에서는 채워진 타원을 보여 줍니다.  
  
 ![채워진 도형](./media/aboutgdip02-art21.gif "AboutGdip02_Art21")  
  
 셰이프 중심에서 가장자리로 이동할 때 색을 변경 하도록 경로 그라데이션 브러시를 구성할 수 있습니다.  
  
 ![채워진 도형](./media/aboutgdip02-art22.gif "AboutGdip02_Art22")  
  
 경로 그라데이션 브러시는 매우 유연 합니다. 다음 그림에서 삼각형을 채우는 데 사용 되는 그라데이션 브러시는 중앙의 빨간색에서 꼭 짓 점에 있는 세 가지 색으로 점차 변합니다.  
  
 ![채워진 도형](./media/aboutgdip02-art23.gif "AboutGdip02_Art23")  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.SolidBrush?displayProperty=nameWithType>
- <xref:System.Drawing.Drawing2D.HatchBrush?displayProperty=nameWithType>
- <xref:System.Drawing.TextureBrush?displayProperty=nameWithType>
- <xref:System.Drawing.Drawing2D.LinearGradientBrush?displayProperty=nameWithType>
- [선, 곡선 및 도형](lines-curves-and-shapes.md)
- [방법: Windows Form에 채워진 사각형 그리기](how-to-draw-a-filled-rectangle-on-a-windows-form.md)
- [방법: Windows Form에 채워진 타원 그리기](how-to-draw-a-filled-ellipse-on-a-windows-form.md)
