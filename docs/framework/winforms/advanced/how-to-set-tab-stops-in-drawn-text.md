---
title: '방법: 그린 텍스트에 탭 정지 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text [Windows Forms], drawing with tab stops
- tabs [Windows Forms], drawn text
ms.assetid: 64878f98-39ba-4303-b63f-0859ab682eeb
ms.openlocfilehash: 8821f6170b8ba588e3197ef54eab14c2719a6cc3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69947828"
---
# <a name="how-to-set-tab-stops-in-drawn-text"></a>방법: 그린 텍스트에 탭 정지 설정
<xref:System.Drawing.StringFormat.SetTabStops%2A> <xref:System.Drawing.StringFormat> <xref:System.Drawing.Graphics.DrawString%2A> 개체의 메서드를 호출 하 고 해당 개체를 <xref:System.Drawing.Graphics> 클래스의 메서드에 전달 하 여 텍스트에 대 한 탭 정지를 설정할 수 있습니다. <xref:System.Drawing.StringFormat>  
  
> [!NOTE]
> 합니다 <xref:System.Windows.Forms.TextRenderer?displayProperty=nameWithType> 사용을 중지할 기존 탭을 확장할 수 있지만 그린된 텍스트에 탭 정지를 추가 하는 지원 하지 않습니다는 <xref:System.Windows.Forms.TextFormatFlags.ExpandTabs?displayProperty=nameWithType> 플래그입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 150, 250 및 350에서 탭 정지를 설정 합니다. 그런 다음 코드에서 이름 및 테스트 점수의 탭 목록을 표시 합니다.  
  
 다음 그림에서는 탭 텍스트를 보여 줍니다.  
  
 ![이름 및 점수의 탭 목록을 보여 주는 스크린샷](./media/how-to-set-tab-stops-in-drawn-text/tab-list-names-test-scores.png)  
  
 다음 코드는 <xref:System.Drawing.StringFormat.SetTabStops%2A> 메서드에 두 개의 인수를 전달 합니다. 두 번째 인수는 탭 오프셋을 포함 하는 배열입니다. 에 <xref:System.Drawing.StringFormat.SetTabStops%2A> 전달 되는 첫 번째 인수는 0 이며,이는 배열의 첫 번째 오프셋이 경계 사각형의 왼쪽 가장자리 위치 0에서 측정 됨을 나타냅니다.  
  
 [!code-csharp[System.Drawing.FontsAndText#41](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.FontsAndText#41](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#41)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
- 위의 예제는 Windows Forms와 함께 사용 하도록 설계 되었으며의 <xref:System.Windows.Forms.PaintEventArgs> <xref:System.Windows.Forms.PaintEventHandler>매개 변수인가 필요 `e`합니다.  
  
## <a name="see-also"></a>참고자료

- [글꼴 및 텍스트 사용](using-fonts-and-text.md)
- [방법: GDI를 사용 하 여 텍스트 그리기](how-to-draw-text-with-gdi.md)
