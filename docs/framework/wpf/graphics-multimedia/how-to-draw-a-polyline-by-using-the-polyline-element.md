---
title: '방법: Polyline 요소를 사용하여 폴리라인 그리기'
ms.date: 03/30/2017
helpviewer_keywords:
- connected lines [WPF]
- polylines [WPF], drawing
- graphics [WPF], polylines
- lines [WPF], connected (see polylines)
- drawing [WPF], polylines
ms.assetid: 65db8935-d047-4295-87c4-b427ff3ad293
ms.openlocfilehash: fb5220082989a9d0a22c4998bb79c0a196067e7e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69934958"
---
# <a name="how-to-draw-a-polyline-by-using-the-polyline-element"></a>방법: Polyline 요소를 사용하여 폴리라인 그리기
이 예제에서는 <xref:System.Windows.Shapes.Polyline> 요소를 사용 하 여 일련의 연결 된 선 인 다중선을 그리는 방법을 보여 줍니다.  
  
 다중선을 그리려면 요소를 <xref:System.Windows.Shapes.Polyline> 만든 다음 해당 <xref:System.Windows.Shapes.Polyline.Points%2A> 속성을 사용 하 여 도형 꼭 짓 점을 지정 합니다. 마지막으로 스트로크가 없는 <xref:System.Windows.Shapes.Shape.Stroke%2A> 선이 <xref:System.Windows.Shapes.Shape.StrokeThickness%2A> 보이지 않기 때문에 및 속성을 사용 하 여 다중선 윤곽선을 설명 합니다.  
  
> [!NOTE]
> 요소가 닫힌 모양이 아니기 때문에 속성은 <xref:System.Windows.Shapes.Shape.Fill%2A> 모양 윤곽선을 의도적으로 닫는 경우에도 영향을 주지 않습니다. <xref:System.Windows.Shapes.Polyline> 을 사용 하 여 <xref:System.Windows.Shapes.Shape.Fill%2A>닫힌 도형을 만들려면 요소를 <xref:System.Windows.Shapes.Polygon> 사용 합니다.  
  
 다음 예제에서는 내에 <xref:System.Windows.Shapes.Polyline> 두 개의 요소 <xref:System.Windows.Controls.Canvas>를 그립니다.  
  
## <a name="example"></a>예제  
 에서 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]점의 유효한 구문은 쉼표로 구분 된 x 및 y 좌표 쌍의 공백으로 구분 된 목록입니다.  
  
 [!code-xaml[drawingwithshapeelements#PolylineExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/polylineexample.xaml#polylineexample1)]  
  
 이 예제에서는를 <xref:System.Windows.Controls.Canvas> 사용 하 여 폴리라인을 포함 하지만, 텍스트가 아닌 콘텐츠를 지 원하는 <xref:System.Windows.Controls.Panel> 또는 <xref:System.Windows.Controls.Control> 와 함께 폴리라인 요소 (및 다른 모든 셰이프 요소)를 사용할 수 있습니다.  
  
 이 예제는 더 큰 샘플의 일부입니다. 전체 샘플은 [셰이프 요소 샘플](https://go.microsoft.com/fwlink/?LinkID=160037)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Shapes.Polyline>
- <xref:System.Windows.Shapes.Polygon>
- <xref:System.Windows.Shapes.Shape>
- [셰이프 요소 샘플](https://go.microsoft.com/fwlink/?LinkID=160037)
- [WPF에서 Shape 및 기본 그리기 개요](shapes-and-basic-drawing-in-wpf-overview.md)
