---
title: '방법: PathGeometry 내에 다중 하위 경로 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- multiple subpaths [WPF]
- graphics [WPF], subpaths
- subpaths [WPF]
ms.assetid: 104a862c-dde2-4e62-ac87-80660dd1681c
ms.openlocfilehash: 286075448cd6a343f8a7b15b2b5005f840f68e1d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61904724"
---
# <a name="how-to-create-multiple-subpaths-within-a-pathgeometry"></a>방법: PathGeometry 내에 다중 하위 경로 만들기
이 예제에서 여러 하위 경로를 만드는 방법을 보여 줍니다는 <xref:System.Windows.Media.PathGeometry>합니다. 다중 하위 경로 만들려면, 한 <xref:System.Windows.Media.PathFigure> 각 하위 경로 대 한 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 두 개의 하위 경로 각 삼각형을 만듭니다.  
  
 [!code-xaml[GeometrySample#38](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#38)]  
  
 다음 예제에 사용 하 여 다중 하위 경로 만드는 방법을 보여 줍니다는 <xref:System.Windows.Shapes.Path> 고 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 특성 구문입니다. 각 `M` 예제에서는 각각 삼각형을 그리는 두 개의 하위 경로 만들 수 있도록 새 하위 경로 만듭니다.  
  
 [!code-xaml[GeometrySample#58](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/geometryattributesyntaxexample.xaml#58)]  
  
 (이 특성 구문은 실제로 만들어지는 참고를 <xref:System.Windows.Media.StreamGeometry>, 가벼운 버전의는 <xref:System.Windows.Media.PathGeometry>합니다. 자세한 내용은 [경로 태그 구문](path-markup-syntax.md) 페이지를 참조하세요.)  
  
## <a name="see-also"></a>참고자료

- [Geometry 개요](geometry-overview.md)
