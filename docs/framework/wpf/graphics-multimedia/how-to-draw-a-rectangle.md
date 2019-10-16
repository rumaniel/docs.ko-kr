---
title: '방법: 사각형 그리기'
ms.date: 03/30/2017
helpviewer_keywords:
- drawing [WPF], rectangles
- graphics [WPF], rectangles
- rectangles [WPF], drawing
ms.assetid: beeb57ef-fab5-4446-a38a-1588f97b4c2f
ms.openlocfilehash: 261026b994b432565928b38ff1657115ff7cbe4e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61947630"
---
# <a name="how-to-draw-a-rectangle"></a>방법: 사각형 그리기
사용 하 여 사각형을 그리는 방법을 보여 주는이 예제는 <xref:System.Windows.Shapes.Rectangle> 요소입니다.  
  
 사각형을 그리려면 만들려면를 <xref:System.Windows.Shapes.Rectangle> 요소를 지정 하 고 해당 <xref:System.Windows.FrameworkElement.Width%2A> 및 <xref:System.Windows.FrameworkElement.Height%2A>합니다. 사각형의 내부 그릴 설정 해당 <xref:System.Windows.Shapes.Shape.Fill%2A>합니다. 사각형 윤곽선을 제공 하려면 사용 하 여 해당 <xref:System.Windows.Shapes.Shape.Stroke%2A> 고 <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> 속성입니다.  
  
 모서리가 둥근 사각형, 선택적으로 지정할 <xref:System.Windows.Shapes.Rectangle.RadiusX%2A> 고 <xref:System.Windows.Shapes.Rectangle.RadiusY%2A> 속성입니다. 합니다 <xref:System.Windows.Shapes.Rectangle.RadiusX%2A> 및 <xref:System.Windows.Shapes.Rectangle.RadiusY%2A> 속성 사각형의 모퉁이 둥글게 하는 데 사용 되는 타원의 x 축과 y 반지름을 설정 합니다.  
  
 다음 예제에서는 두 개의 <xref:System.Windows.Shapes.Rectangle> 요소를 그립니다는 <xref:System.Windows.Controls.Canvas>합니다. 첫 번째 사각형에는 <xref:System.Windows.Media.Brushes.Blue%2A> 내부. 두 번째 사각형에는 <xref:System.Windows.Media.Brushes.Blue%2A> 내부에 <xref:System.Windows.Media.Brushes.Black%2A> 윤곽선 및 모서리가 둥근된 합니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[drawingwithshapeelements#Rectangle1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/rectangleexample.xaml#rectangle1)]  
  
 이 예제에서는 한 <xref:System.Windows.Controls.Canvas> 사각형을 포함 하려면 사용할 수 있습니다 사각형 요소 (및 다른 모든 도형 요소)와 <xref:System.Windows.Controls.Panel> 또는 <xref:System.Windows.Controls.Control> 텍스트가 아닌 콘텐츠를 지 원하는 합니다. 사각형의 일부에 대 한 배경을 제공 하는 데 특히 유용은 사실 <xref:System.Windows.Controls.Grid> 패널입니다. 예를 들어 참조 된 [테이블 개요](../advanced/table-overview.md)합니다.  
  
 이 예제는 더 큰 샘플;의 일부 전체 샘플을 참조 하세요 [도형 요소 샘플](https://go.microsoft.com/fwlink/?LinkID=160037)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Shapes.Rectangle>
- [도형 요소 샘플](https://go.microsoft.com/fwlink/?LinkID=160037)
- [WPF에서 Shape 및 기본 그리기 개요](shapes-and-basic-drawing-in-wpf-overview.md)
- [테이블 개요](../advanced/table-overview.md)
