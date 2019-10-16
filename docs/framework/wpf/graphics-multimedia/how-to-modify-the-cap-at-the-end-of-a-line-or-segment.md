---
title: '방법: 줄 또는 세그먼트의 끝 모양 수정'
ms.date: 03/30/2017
helpviewer_keywords:
- Shape elements [WPF], ends
- Shape elements [WPF], caps
- graphics [WPF], Shape caps
ms.assetid: f4bf3416-b3d8-4568-b98e-3eda8f6dbf7a
ms.openlocfilehash: 53487417636dae8d855fe70b7b9255351a2dfb1e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916127"
---
# <a name="how-to-modify-the-cap-at-the-end-of-a-line-or-segment"></a>방법: 줄 또는 세그먼트의 끝 모양 수정
이 예제에서는 열린 <xref:System.Windows.Shapes.Shape> 요소의 시작 또는 끝에서 셰이프를 수정 하는 방법을 보여 줍니다. 열린 <xref:System.Windows.Shapes.Shape>의 시작 부분에 있는 캡을 변경 하려면 해당 <xref:System.Windows.Shapes.Shape.StrokeStartLineCap%2A> 속성을 사용 합니다. 열린 <xref:System.Windows.Shapes.Shape>의 끝에 있는 캡을 변경 하려면 해당 <xref:System.Windows.Shapes.Shape.StrokeEndLineCap%2A> 속성을 사용 합니다. 사용 가능한 선 끝 모양을 보려면 <xref:System.Windows.Media.PenLineCap> 열거를 참조 하세요.  
  
> [!NOTE]
> 이 속성은 <xref:System.Windows.Shapes.Line> <xref:System.Windows.Shapes.Polyline>, 또는 열린 <xref:System.Windows.Shapes.Path> 요소와 같은 열린 도형에만 영향을 줍니다.  
  
 다음 예제에서는 4 개의 <xref:System.Windows.Shapes.Polyline> 요소를 그린 다음 각의 끝에 서로 다른 모양 집합을 사용 합니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[drawingwithshapeelements#ShapeLineCaps1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/linecapsandjoinsexample.xaml#shapelinecaps1)]  
  
 이 예제는 더 큰 샘플의 일부입니다. 전체 샘플은 [셰이프 요소 샘플](https://go.microsoft.com/fwlink/?LinkID=160037)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Shapes.Polyline>
- <xref:System.Windows.Media.PenLineCap>
