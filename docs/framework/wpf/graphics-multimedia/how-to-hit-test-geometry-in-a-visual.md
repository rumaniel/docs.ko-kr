---
title: '방법: 시각적 개체의 기하 도형 적중 테스트'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hit tests [WPF], on visual objects comprising Geometry objects [WPF]
- visual objects [WPF], hit tests on
- Geometry objects [WPF], visual objects comprising
ms.assetid: 8bf2643f-d7f9-4cb4-9ea6-5b893c23200d
ms.openlocfilehash: 52b9b99b0af38d797e4a3c98dc0979211c930c1f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923373"
---
# <a name="how-to-hit-test-geometry-in-a-visual"></a>방법: 시각적 개체의 기하 도형 적중 테스트
이 예제에서는 하나 <xref:System.Windows.Media.Geometry> 이상의 개체로 구성 된 시각적 개체에 대해 적중 테스트를 수행 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 메서드를 <xref:System.Windows.Media.DrawingGroup> <xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A> 사용 하는 시각적 개체에서를 검색 하는 방법을 보여 줍니다. 적중 테스트는 적중 된 기 <xref:System.Windows.Media.DrawingGroup> 하 도형을 확인 하기 위해에서 각 드로잉의 렌더링 된 콘텐츠에 대해 수행 됩니다.  
  
> [!NOTE]
> 대부분의 경우 <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> 메서드를 사용 하 여 요소가 시각적 개체의 렌더링 된 콘텐츠와 교차 하는지 여부를 확인 합니다.  
  
 [!code-csharp[VisualsOverview#VisualsOverviewSnippet4](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml.cs#visualsoverviewsnippet4)]
 [!code-vb[VisualsOverview#VisualsOverviewSnippet4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsOverview/visualbasic/window1.xaml.vb#visualsoverviewsnippet4)]  
  
 메서드는 지정 <xref:System.Windows.Point> 된 또는 <xref:System.Windows.Media.Geometry>를 사용 하 여 적중 테스트를 수행할 수 있도록 하는 오버 로드 된 메서드입니다. <xref:System.Windows.Media.Geometry.FillContains%2A> 기하 도형에 스트로크를 적용할 경우 스트로크가 채우기 경계 밖으로 확장될 수 있습니다. 이 경우 <xref:System.Windows.Media.Geometry.StrokeContains%2A> <xref:System.Windows.Media.Geometry.FillContains%2A>외에도를 호출 하는 것이 좋습니다.  
  
 또한 베 지 어 평면화 <xref:System.Windows.Media.ToleranceType> 의 목적으로 사용 되는를 제공할 수 있습니다.  
  
> [!NOTE]
> 이 샘플에서는 기하 도형에 적용될 수 있는 변환 또는 클리핑을 고려하지 않습니다. 또한 이 샘플은 직접 연결된 그림이 없으므로 스타일이 적용된 컨트롤에서 작동하지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [시각적 계층에서 적중 테스트](hit-testing-in-the-visual-layer.md)
- [기하 도형을 매개 변수로 사용하여 적중 테스트](how-to-hit-test-using-geometry-as-a-parameter.md)
