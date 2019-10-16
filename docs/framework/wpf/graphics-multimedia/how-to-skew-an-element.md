---
title: '방법: 요소 기울이기'
ms.date: 03/30/2017
helpviewer_keywords:
- skewing elements [WPF]
- graphics [WPF], skewing elements
- classes [WPF], SkewTransform
ms.assetid: 56b65f2f-dc6e-4238-923f-ca44ec53c52f
ms.openlocfilehash: cf770a284238826852e788e27f3b3f329ed0269f
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67664079"
---
# <a name="how-to-skew-an-element"></a>방법: 요소 기울이기
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.SkewTransform> 요소 기울이기 하 합니다. 전단이라고도 하는 기울이기는 일관되지 않은 방식으로 좌표 공간을 늘리는 변환입니다. 일반적인 한 가지 용도 <xref:System.Windows.Media.SkewTransform> 를 2 차원 개체에 3 차원 깊이 시뮬레이트하는 것입니다.  
  
 사용 하 여는 <xref:System.Windows.Media.SkewTransform.CenterX%2A> 및 <xref:System.Windows.Media.SkewTransform.CenterY%2A> 가운데를 지정 하는 속성의 가리킨는 <xref:System.Windows.Media.SkewTransform>합니다.  
  
 사용 된 <xref:System.Windows.Media.SkewTransform.AngleX%2A> 및 <xref:System.Windows.Media.SkewTransform.AngleY%2A> 속성 x 축 및 y 축 기울기 각도 지정 하 고 이러한 축 따라 현재 좌표계를 기울입니다.  
  
 기울이기 변환 효과 예측 하는 것이 좋습니다 <xref:System.Windows.Media.SkewTransform.AngleX%2A> 는 원래 좌표계를 기준으로 x 축 값을 기울입니다. 따라서는 <xref:System.Windows.Media.SkewTransform.AngleX%2A> 30 y 축은 원점을 30도 회전 및 값 x-해당 원점에서 30도 만큼 기울어집니다. 마찬가지로,는 <xref:System.Windows.Media.SkewTransform.AngleY%2A> 30 도형의 y 값 원점에서 30도 만큼 기울어집니다. 이것은 좌표 시스템을 x 또는 y축으로 30도만큼 변환(이동)하는 것과 같지 않습니다.  
  
 다음 예에서는 45도의 가로 기울이기를 적용을 <xref:System.Windows.Shapes.Rectangle> (0, 0)의 중심점에서.  
  
## <a name="example"></a>예제  
 [!code-xaml[transformsSample#41](~/samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/SkewTransformExample.xaml#41)]  
  
 다음 예에서는 45도의 가로 기울이기를 적용을 <xref:System.Windows.Shapes.Rectangle> (25, 25)의 중심점에서.  
  
 [!code-xaml[transformsSample#42](~/samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/SkewTransformExample.xaml#42)]  
  
 다음 예에서는 45도의 세로 기울이기를 적용을 <xref:System.Windows.Shapes.Rectangle> (25, 25)의 중심점에서.  
  
 [!code-xaml[transformsSample#43](~/samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/SkewTransformExample.xaml#43)]  
  
 다음 그림에서는 이 예제에서 사용되는 다양한 기울이기를 보여 줍니다.  
  
 ![SkewTransform 예제](./media/img-wcpsdk-graphicsmm-skewtransformexample.gif "img_wcpsdk_graphicsmm_skewtransformexample")  
세 개의 SkewTransform 예제 그림  
  
 전체 샘플을 보려면 [2차원 변환 샘플](https://go.microsoft.com/fwlink/?LinkID=158252)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Transform>
- <xref:System.Windows.Media.SkewTransform>
- [Transform 개요](transforms-overview.md)
- [방법 항목](transformations-how-to-topics.md)
