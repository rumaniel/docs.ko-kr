---
title: '방법: 선형 그라데이션으로 영역 칠하기'
ms.date: 03/30/2017
helpviewer_keywords:
- linear gradients [WPF], painting with
- brushes [WPF], painting with linear gradients
- painting [WPF], with linear gradients
ms.assetid: 00e0cd04-48c0-4ec5-850e-d321beb37a34
ms.openlocfilehash: 92c9ccd846dbbce043d13e6ba82b9fa8e72fa8b5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916173"
---
# <a name="how-to-paint-an-area-with-a-linear-gradient"></a>방법: 선형 그라데이션으로 영역 칠하기
이 예제에서는 <xref:System.Windows.Media.LinearGradientBrush> 클래스를 사용 하 여 선형 그라데이션으로 영역을 그리는 방법을 보여 줍니다. 다음 예제에서의는 <xref:System.Windows.Shapes.Shape.Fill%2A> 노란색에서 빨강으로, <xref:System.Windows.Shapes.Rectangle> 녹색에서 파랑으로 전환 되는 대각선 선형 그라데이션으로 그려집니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[GradientBrushExamples_snip#DiagonalGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#diagonalgradient1xaml)]  
  
 [!code-csharp[GradientBrushExamples_snip#DiagonalGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#diagonalgradient1csharp)]  
  
 다음 그림은 이전 예제에서 만든 그라데이션을 보여 줍니다.  
  
 ![대각선 선형 그라데이션](./media/graphicsmm-diagonallgb.jpg "graphicsmm_DiagonalLGB")  
  
 가로 선형 그라데이션을 만들려면의 <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> <xref:System.Windows.Media.LinearGradientBrush> 및 <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> 을 (0, 0.5) 및 (1, 0.5)로 변경 합니다. 다음 예제에서는 가로 선형 그라데이션을 <xref:System.Windows.Shapes.Rectangle> 사용 하 여을 그립니다.  
  
 [!code-xaml[GradientBrushExamples_snip#HorizontalGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#horizontalgradient1xaml)]  
  
 [!code-csharp[GradientBrushExamples_snip#HorizontalGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#horizontalgradient1csharp)]  
  
 다음 그림은 이전 예제에서 만든 그라데이션을 보여 줍니다.  
  
 ![가로 선형 그라데이션](./media/graphicsmm-horizontallgb.jpg "graphicsmm_HorizontalLGB")  
  
 세로 선형 그라데이션을 만들려면의 <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> <xref:System.Windows.Media.LinearGradientBrush> 및 <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> 을 (0.5, 0) 및 (0.5, 1)로 변경 합니다. 다음 예제에서는 세로 선형 그라데이션을 <xref:System.Windows.Shapes.Rectangle> 사용 하 여을 그립니다.  
  
 [!code-xaml[GradientBrushExamples_snip#VerticalGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#verticalgradient1xaml)]  
  
 [!code-csharp[GradientBrushExamples_snip#VerticalGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#verticalgradient1csharp)]  
  
 다음 그림은 이전 예제에서 만든 그라데이션을 보여 줍니다.  
  
 ![세로 선형 그라데이션](./media/graphicsmm-verticallgb.jpg "graphicsmm_VerticalLGB")  
  
> [!NOTE]
> 이 항목의 예에서는 기본 좌표계를 사용 하 여 시작점 및 끝점을 설정 합니다. 기본 좌표계는 경계 상자를 기준으로 합니다. 0은 경계 상자의 0%를 나타내고 1은 경계 상자의 100%를 나타냅니다. <xref:System.Windows.Media.GradientBrush.MappingMode%2A> 속성을 값 <xref:System.Windows.Media.BrushMappingMode.Absolute?displayProperty=nameWithType>으로 설정 하 여이 좌표계를 변경할 수 있습니다. 절대 좌표계는 경계 상자를 기준으로 하지 않습니다. 값은 로컬 공간에서 직접 해석됩니다.  
  
 추가 예제는 [브러시 샘플](https://go.microsoft.com/fwlink/?LinkID=159973)을 참조 하세요. 그라데이션 및 기타 브러시 형식에 대 한 자세한 내용은 [단색 및 그라데이션을 사용한 그리기 개요](painting-with-solid-colors-and-gradients-overview.md)를 참조 하세요.
