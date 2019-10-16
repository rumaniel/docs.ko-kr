---
title: '방법: 선 그리기'
ms.date: 03/30/2017
helpviewer_keywords:
- drawing [WPF], lines
- graphics [WPF], lines
- lines [WPF], drawing
ms.assetid: 0513ee01-6b27-4bb3-85f3-3a3e6710d80e
ms.openlocfilehash: c11dfb9523834ec2e622cb2e62bd6982a1a78fd4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61947656"
---
# <a name="how-to-draw-a-line"></a>방법: 선 그리기
이 예제에서는 사용 하 여 선을 그리는 방법을 보여 줍니다.는 <xref:System.Windows.Shapes.Line> 요소입니다.  
  
 선을 그리는 만들려면는 <xref:System.Windows.Shapes.Line> 요소입니다. 사용 하 여 해당 <xref:System.Windows.Shapes.Line.X1%2A> 하 고 <xref:System.Windows.Shapes.Line.Y1%2A> 시작점;를 사용 하 여 속성 해당 <xref:System.Windows.Shapes.Line.X2%2A> 및 <xref:System.Windows.Shapes.Line.Y2%2A> 끝점을 설정 하는 속성입니다. 마지막으로 설정 하는 <xref:System.Windows.Shapes.Shape.Stroke%2A> 및 <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> 스트로크 없는 줄에 표시 되지 않으므로 합니다.  
  
 설정 된 <xref:System.Windows.Shapes.Shape.Fill%2A> 요소 줄에 대 한 영향을 주지 않습니다, 줄 없는 내부에 있으므로.  
  
 다음 예제에서는 세 줄을 그립니다는 <xref:System.Windows.Controls.Canvas> 요소입니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[drawingwithshapeelements#LineExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/lineexample.xaml#lineexample1)]  
  
 이 예제는 더 큰 샘플;의 일부 전체 샘플을 참조 하세요 [도형 요소 샘플](https://go.microsoft.com/fwlink/?LinkID=160037)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Shapes.Line>
- [도형 요소 샘플](https://go.microsoft.com/fwlink/?LinkID=160037)
