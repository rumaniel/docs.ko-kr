---
title: '방법: 타원형 원호 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [WPF], elliptical arcs
- elliptical arcs [WPF], creating
- arcs [WPF], elliptical
ms.assetid: 3dcfe502-3485-45de-99fb-d53a1367c484
ms.openlocfilehash: aae304b9963f3a8e5833b4d8ba0a54777a750225
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62003368"
---
# <a name="how-to-create-an-elliptical-arc"></a>방법: 타원형 원호 만들기
이 예제에서는 타원형 호를 그리는 방법을 보여 줍니다. 타원형 호를 만들려면 사용 합니다 <xref:System.Windows.Media.PathGeometry>, <xref:System.Windows.Media.PathFigure>, 및 <xref:System.Windows.Media.ArcSegment> 클래스입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 타원형 호가 그려집니다 (10100)에서 (200100). 호에는 <xref:System.Windows.Media.ArcSegment.Size%2A> 50에서 100 장치 독립적 픽셀을 <xref:System.Windows.Media.ArcSegment.RotationAngle%2A> 45도의 <xref:System.Windows.Media.ArcSegment.IsLargeArc%2A> 설정 `true`, 및 <xref:System.Windows.Media.ArcSegment.SweepDirection%2A> 의 <xref:System.Windows.Media.SweepDirection.Counterclockwise>합니다.  
  
 [xaml]  
  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], 경로를 설명할 특성 구문을 사용할 수 있습니다.  
  
 [!code-xaml[GeometrySample#56](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/geometryattributesyntaxexample.xaml#56)]  
  
 [xaml]  
  
 (이 특성 구문은 실제로 만들어지는 참고를 <xref:System.Windows.Media.StreamGeometry>, 가벼운 버전의는 <xref:System.Windows.Media.PathGeometry>합니다. 자세한 내용은 [경로 태그 구문](path-markup-syntax.md) 페이지를 참조하세요.)  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]를 명시적으로 object 태그를 사용 하 여 타원형 호를 그릴 수도 있습니다. 다음은 위의 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 태그입니다.  
  
 [!code-xaml[GeometrySample#36](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#36)]  
  
 이 예제는 더 큰 샘플의 일부입니다. 전체 샘플을 참조 하세요. 합니다 [기 하 도형 샘플](https://go.microsoft.com/fwlink/?LinkID=159989)합니다.  
  
## <a name="see-also"></a>참고자료

- [정방형 3차원 곡선 만들기](how-to-create-a-quadratic-bezier-curve.md)
- [입방형 3차원 곡선 만들기](how-to-create-a-cubic-bezier-curve.md)
