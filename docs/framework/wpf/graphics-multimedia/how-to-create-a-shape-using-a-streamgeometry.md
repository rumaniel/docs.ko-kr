---
title: '방법: StreamGeometry를 사용하여 도형 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], shapes
- shapes [WPF], creating with StreamGeometry class
ms.assetid: 08f7c8ce-074b-49cd-9aba-cc9592d4ee51
ms.openlocfilehash: ce2097568349ad376540163f5fe05d6a3e5b0643
ms.sourcegitcommit: 127343afce8422bfa944c8b0c4ecc8f79f653255
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67348023"
---
# <a name="how-to-create-a-shape-using-a-streamgeometry"></a>방법: StreamGeometry를 사용하여 도형 만들기
<xref:System.Windows.Media.StreamGeometry> 경량 대체는 <xref:System.Windows.Media.PathGeometry> 기 하 도형 만들기에 대 한 합니다. 사용 하 여는 <xref:System.Windows.Media.StreamGeometry> 복잡 한 기 하 도형을 설명 해야 하지만 데이터 바인딩, 애니메이션 또는 수정을 지원 오버 헤드를 원하지 않는 합니다. 예를 들어는 효율성으로 인해는 <xref:System.Windows.Media.StreamGeometry> 클래스는 표시기 (adorner)를 설명 하는 데 적합 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 특성 구문을 사용 하 여 삼각형을 만드는 <xref:System.Windows.Media.StreamGeometry> 에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]합니다.  
  
 [!code-xaml[GeometriesMiscSnippets_snip#StreamGeometryTriangleExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/GeometriesMiscSnippets_snip/XAML/StreamGeometryExample.xaml#streamgeometrytriangleexamplewholepage)]  
  
 에 대 한 자세한 내용은 <xref:System.Windows.Media.StreamGeometry> 특성 구문, 참조는 [경로 태그 구문](path-markup-syntax.md) 페이지입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Windows.Media.StreamGeometry> 코드에서 삼각형을 정의 합니다. 첫째,이 예에서는 만듭니다는 <xref:System.Windows.Media.StreamGeometry>을 구합니다를 <xref:System.Windows.Media.StreamGeometryContext> 삼각형을 설명 하는 데 사용 합니다.  
  
 [!code-csharp[GeometriesMiscSnippets_procedural_snip#StreamGeometryTriangleExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/CSharp/StreamGeometryTriangleExample.cs#streamgeometrytriangleexamplewholepage)]
 [!code-vb[GeometriesMiscSnippets_procedural_snip#StreamGeometryTriangleExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/visualbasic/streamgeometrytriangleexample.vb#streamgeometrytriangleexamplewholepage)]  
  
## <a name="example"></a>예제  
 다음 예제를 사용 하는 메서드를 만듭니다는 <xref:System.Windows.Media.StreamGeometry> 및 <xref:System.Windows.Media.StreamGeometryContext> 에 지정 된 매개 변수를 기반으로 도형을 정의 합니다.  
  
 [!code-csharp[GeometriesMiscSnippets_procedural_snip#StreamGeometryExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/CSharp/StreamGeometryExample.cs#streamgeometryexamplewholepage)]
 [!code-vb[GeometriesMiscSnippets_procedural_snip#StreamGeometryExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/visualbasic/streamgeometryexample.vb#streamgeometryexamplewholepage)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.PathGeometry>
- <xref:System.Windows.Media.StreamGeometry>
- <xref:System.Windows.Media.StreamGeometryContext>
- [PathGeometry를 사용하여 도형 만들기](how-to-create-a-shape-by-using-a-pathgeometry.md)
- [Geometry 개요](geometry-overview.md)
