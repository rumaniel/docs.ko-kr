---
title: '방법: 글꼴 메트릭 가져오기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- fonts [Windows Forms], obtaining metrics
- font metrics [Windows Forms], obtaining
ms.assetid: ff7c0616-67f7-4fa2-84ee-b8d642f2b09b
ms.openlocfilehash: 7d7ad92199bb8a8f01290066f8ae023a14c2f9ce
ms.sourcegitcommit: a970268118ea61ce14207e0916e17243546a491f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2019
ms.locfileid: "67307432"
---
# <a name="how-to-obtain-font-metrics"></a>방법: 글꼴 메트릭 가져오기
<xref:System.Drawing.FontFamily> 클래스는 특정 제품군/스타일 조합에 대 한 다양 한 메트릭을 검색 하는 메서드를 제공 합니다.  
  
- <xref:System.Drawing.FontFamily.GetEmHeight%2A>(FontStyle)  
  
- <xref:System.Drawing.FontFamily.GetCellAscent%2A>(FontStyle)  
  
- <xref:System.Drawing.FontFamily.GetCellDescent%2A>(FontStyle)  
  
- <xref:System.Drawing.FontFamily.GetLineSpacing%2A>(FontStyle)  
  
 이러한 메서드에서 반환 된 값은 글꼴 디자인 단위로 크기 및 특정 단위의 독립 되므로 <xref:System.Drawing.Font> 개체입니다.  
  
 다음 그림에는 다양 한 메트릭을 보여 줍니다.
  
 ![글꼴 메트릭 보여 줍니다: ascent, 하강 및 줄 간격.](./media/how-to-obtain-font-metrics/various-font-metrics.png)  
  
## <a name="example"></a>예제  
 다음 예제에서는 Arial 글꼴 패밀리의 일반 스타일에 대 한 메트릭을 표시합니다. 코드는 또한 만듭니다는 <xref:System.Drawing.Font> 16 픽셀 크기 및 표시 (픽셀 단위)는 특정 메트릭 사용 하 여 개체 (Arial 패밀리에 따라) <xref:System.Drawing.Font> 개체입니다.  
  
 다음 그림에서는 예제 코드의 출력을 보여 줍니다.
  
 ![예제 코드의 출력 Arial 글꼴 메트릭입니다.](./media/how-to-obtain-font-metrics/example-output-code-arial-font.png)  
  
 앞의 그림에서 출력의 처음 두 줄을 note 합니다. <xref:System.Drawing.Font> 개체의 크기가 16 반환 하며 <xref:System.Drawing.FontFamily> 2,048는 em 높이 반환 하는 개체입니다. 이러한 두 값 (16 및 2,048)는 키 글꼴 디자인 단위로 및 단위 (이 예제의 경우 픽셀)의 사이 변환로 <xref:System.Drawing.Font> 개체입니다.  
  
 예를 들어, 변환할 수 있습니다 어센더 디자인 단위로에서 픽셀을 다음과 같습니다.  
  
 ![표시 픽셀 디자인 단위로 변환 하는 수식](./media/how-to-obtain-font-metrics/convert-font-units-example.png)  
  
 다음 코드는 텍스트를 세로로 배치 설정 하 여 합니다 <xref:System.Drawing.PointF.Y%2A> 의 데이터 멤버는 <xref:System.Drawing.PointF> 개체입니다. 에 대 한 y-좌표 증분됩니다 `font.Height` 각 새 텍스트 줄에 대 한 합니다. 합니다 <xref:System.Drawing.Font.Height%2A> 의 속성을 <xref:System.Drawing.Font> 개체는 특정 줄 간격 (픽셀)를 반환 합니다. <xref:System.Drawing.Font> 개체입니다. 이 예제에서는 반환 되는 수 여 <xref:System.Drawing.Font.Height%2A> 은 19입니다. 이 줄 간격 메트릭 픽셀로 변환 하 여 얻은 (정수로 반올림) 수와 동일 하 게 note 합니다.  
  
 Em 높이 (크기나 em 크기 라고도 함)는 기준선 위와의 합계가 아닙니다 note 합니다. 위와 어센더 합계 셀 높이 이라고 합니다. 내부 앞에 오는 빼기 셀 높이 em 높이 같습니다. 셀 높이 외부 앞에 오는 줄 간격으로 같습니다.  
  
 [!code-csharp[System.Drawing.FontsAndText#71](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#71)]
 [!code-vb[System.Drawing.FontsAndText#71](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#71)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 앞의 예제는 Windows Forms에서 사용 하도록 설계 되었으며 필요 <xref:System.Windows.Forms.PaintEventArgs> `e`의 매개 변수인 <xref:System.Windows.Forms.PaintEventHandler>합니다.  
  
## <a name="see-also"></a>참고자료

- [Windows Forms의 그래픽 및 그리기](graphics-and-drawing-in-windows-forms.md)
- [글꼴 및 텍스트 사용](using-fonts-and-text.md)
