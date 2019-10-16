---
title: '방법: PathGeometry를 사용하여 도형 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- shapes [WPF], creating with PathGeometry class
- graphics [WPF], shapes
ms.assetid: 49a4a8b7-e738-45be-8dac-b54a6d8f5b21
ms.openlocfilehash: b0ab703596612524881ab892a1095b0f49cd1551
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61904317"
---
# <a name="how-to-create-a-shape-by-using-a-pathgeometry"></a>방법: PathGeometry를 사용하여 도형 만들기
사용 하 여 도형을 만드는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.PathGeometry> 클래스입니다. <xref:System.Windows.Media.PathGeometry> 개체는 하나 이상의 구성 됩니다 <xref:System.Windows.Media.PathFigure> 객체; 각 <xref:System.Windows.Media.PathFigure> 다른 "그림" 또는 도형을 나타냅니다. 각 <xref:System.Windows.Media.PathFigure> 자체는 하나 이상의 구성 <xref:System.Windows.Media.PathSegment> 각각이 그림 또는 도형의 연결 된 부분을 나타내는 개체입니다. 세그먼트 형식 포함 <xref:System.Windows.Media.LineSegment>, <xref:System.Windows.Media.ArcSegment>, 및 <xref:System.Windows.Media.BezierSegment>합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Windows.Media.PathGeometry> 삼각형이 생성 됩니다. 합니다 <xref:System.Windows.Media.PathGeometry> 를 사용 하 여 표시 되는 <xref:System.Windows.Shapes.Path> 요소입니다.  
  
 [!code-xaml[GeometrySample#49](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#49)]  
  
 다음 그림은 이전 예제에서 만든 도형을 보여 줍니다.  
  
 ![PathGeometry](./media/wcpsdk-graphicsmm-pathgeometry-triangle.gif "wcpsdk_graphicsmm_pathgeometry_triangle")  
PathGeometry를 사용 하 여 만든 삼각형  
  
 이전 예제에는 비교적 간단한 도형을, 삼각형을 만드는 방법을 보여 주었습니다. <xref:System.Windows.Media.PathGeometry> 호와 곡선을 포함 하 여 더 복잡 한 도형을 만들고를 사용할 수도 있습니다. 예제를 보려면 [타원형 원호 만들기](how-to-create-an-elliptical-arc.md)를 [입방 형 3 차원 곡선을 만듭니다](how-to-create-a-cubic-bezier-curve.md), 및 [정방형 베 지 어 곡선 만들기](how-to-create-a-quadratic-bezier-curve.md)합니다.  
  
 이 예제는 더 큰 샘플에 속합니다. 전체 샘플을 보려면 [기하 도형 샘플](https://go.microsoft.com/fwlink/?LinkID=159989)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Shapes.Path>
- <xref:System.Windows.Media.GeometryDrawing>
- [Geometry 개요](geometry-overview.md)
- [기 하 도형 샘플](https://go.microsoft.com/fwlink/?LinkID=159989)
