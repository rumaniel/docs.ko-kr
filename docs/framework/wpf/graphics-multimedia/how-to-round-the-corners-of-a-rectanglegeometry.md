---
title: '방법: RectangleGeometry의 모서리 둥글게 하기'
ms.date: 03/30/2017
helpviewer_keywords:
- corners [WPF], rounding
- RectangleGeometry class [WPF], rounding corners
- graphics [WPF], rounding corners of RectangleGeometry objects [WPF]
- rounding corners of RectangleGeometry objects [WPF]
ms.assetid: 926644bc-1357-4c0b-ac81-694bd090ae87
ms.openlocfilehash: eb2f173bedb903e12b2795264c684524cfa09825
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61651395"
---
# <a name="how-to-round-the-corners-of-a-rectanglegeometry"></a>방법: RectangleGeometry의 모서리 둥글게 하기
모퉁이 둥글게 하는 <xref:System.Windows.Media.RectangleGeometry>설정, 해당 <xref:System.Windows.Media.RectangleGeometry.RadiusX%2A> 및 <xref:System.Windows.Media.RectangleGeometry.RadiusY%2A> 0 보다 큰 값으로 속성입니다. 이 값이 클수록 더 둥글게 사각형의 모퉁이입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 몇 가지 <xref:System.Windows.Media.RectangleGeometry> 다른 개체 <xref:System.Windows.Media.RectangleGeometry.RadiusX%2A> 고 <xref:System.Windows.Media.RectangleGeometry.RadiusY%2A> 설정 합니다. 합니다 <xref:System.Windows.Media.RectangleGeometry> 개체를 사용 하 여 표시 됩니다 <xref:System.Windows.Shapes.Path> 요소입니다.  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMRoundedRectangleGeometryExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/RectangleGeometryRoundedCornerExample.xaml#graphicsmmroundedrectanglegeometryexamplewholepage)]  
  
 ![여러 RadiusX 사각형&#47;RadiusY 설정을](./media/graphicsmm-rounded.png "graphicsmm_rounded")  
모퉁이가 둥근 사각형  
  
## <a name="see-also"></a>참고자료

- [Geometry 개요](geometry-overview.md)
- [복합 도형 만들기](how-to-create-a-composite-shape.md)
- [PathGeometry를 사용하여 도형 만들기](how-to-create-a-shape-by-using-a-pathgeometry.md)
