---
title: '방법: 결합된 기하 도형 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- combining geometries [WPF]
- graphics [WPF], combining geometries
- geometries [WPF], combining
ms.assetid: 54c3277c-6b6e-4b25-91be-fda0bbc706b4
ms.openlocfilehash: c5ebe87abd4c2cf70f8fa17f1fcc773293f3ad27
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910098"
---
# <a name="how-to-create-a-combined-geometry"></a>방법: 결합된 기하 도형 만들기
이 예제에는 기 하 도형을 결합 하는 방법을 보여 줍니다. 사용 하 여 두 기 하 도형을 결합 하는 <xref:System.Windows.Media.CombinedGeometry> 개체입니다. 설정 해당 <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> 및 <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> 결합 하 여 설정 하는 두 기 하 도형 사용 하 여 속성을 <xref:System.Windows.Media.CombinedGeometry.GeometryCombineMode%2A> 기 하 도형을 함께 결합할 수는 어떻게 결정을 하는 속성을 `Union`, `Intersect`, `Exclude`, 또는 `Xor`.  
  
 복합 기 하 도형을 둘 이상의 기 하 도형에서를 만들려면 사용을 <xref:System.Windows.Media.GeometryGroup>입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Windows.Media.CombinedGeometry> 의 기 하 도형 결합 모드를 사용 하 여 정의 `Exclude`합니다.  둘 다 <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> 하며 <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> 50 여 원 동일한 반지름의 원이지만 중심 오프셋으로 정의 됩니다.  
  
 [!code-xaml[GeometrySample#21](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#21)]  
  
 ![결과 Exclude 결합 모드](./media/mil-task-combined-geometry-exclude.PNG "mil_task_combined_geometry_exclude")  
결합 된 기 하 도형 제외  
  
 다음 태그에서를 <xref:System.Windows.Media.CombinedGeometry> 결합 모드를 사용 하 여 정의 `Intersect`합니다.  둘 다 <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> 하며 <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> 50 여 원 동일한 반지름의 원이지만 중심 오프셋으로 정의 됩니다.  
  
 [!code-xaml[GeometrySample#22](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#22)]  
  
 ![결과 Intersect 결합 모드](./media/mil-task-combined-geometry-intersect.PNG "mil_task_combined_geometry_intersect")  
Intersect 결합 된 기 하 도형  
  
 다음 태그에서를 <xref:System.Windows.Media.CombinedGeometry> 결합 모드를 사용 하 여 정의 `Union`합니다.  둘 다 <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> 하며 <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> 50 여 원 동일한 반지름의 원이지만 중심 오프셋으로 정의 됩니다.  
  
 [!code-xaml[GeometrySample#23](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#23)]  
  
 ![Union 결합 모드의 결과](./media/mil-task-combined-geometry-union.PNG "mil_task_combined_geometry_union")  
결합 된 Geometry 합집합  
  
 다음 태그에서를 <xref:System.Windows.Media.CombinedGeometry> 결합 모드를 사용 하 여 정의 `Xor`합니다.  둘 다 <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> 하며 <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> 50 여 원 동일한 반지름의 원이지만 중심 오프셋으로 정의 됩니다.  
  
 [!code-xaml[GeometrySample#24](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#24)]  
  
 ![Xor 결합 모드의 결과](./media/mil-task-combined-geometry-xor.PNG "mil_task_combined_geometry_union")  
Xor 결합 된 기 하 도형
