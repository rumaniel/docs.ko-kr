---
title: '방법: 키 프레임을 사용하여 매트릭스에 애니메이션 효과 주기'
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], Matrix properties with key frames
- Matrix properties [WPF], animating with key frames
- key frames [WPF], animating Matrix properties with
ms.assetid: b851a4c7-ecb1-420e-9203-83e7afd037fd
ms.openlocfilehash: 6aa3e27cdfda7597c9b6acbf2980a2774f2b667b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963034"
---
# <a name="how-to-animate-a-matrix-by-using-key-frames"></a>방법: 키 프레임을 사용하여 매트릭스에 애니메이션 효과 주기
이 예제에서는 키 프레임을 사용 <xref:System.Windows.Media.MatrixTransform.Matrix%2A> 하 <xref:System.Windows.Media.MatrixTransform> 여의 속성에 애니메이션 효과를 주는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Windows.Media.Animation.MatrixAnimationUsingKeyFrames> 클래스를 사용 하 여의 <xref:System.Windows.Media.MatrixTransform.Matrix%2A> <xref:System.Windows.Media.MatrixTransform>속성에 애니메이션 효과를 적용 합니다. 이 예제에서는 <xref:System.Windows.Media.MatrixTransform> 개체를 사용 하 여 <xref:System.Windows.Controls.Button>의 모양과 위치를 변환 합니다.  
  
 이 애니메이션은 <xref:System.Windows.Media.Animation.DiscreteMatrixKeyFrame> 클래스를 사용 하 여 두 개의 키 프레임을 만들고이를 사용 하 여 다음 작업을 수행 합니다.  
  
1. 처음 0.2 초 <xref:System.Windows.Media.Matrix> 동안 처음에 애니메이션 효과를 적용 합니다. 이 예제에서는의 <xref:System.Windows.Media.Matrix.M11%2A> <xref:System.Windows.Media.Matrix.M12%2A>및속성 을 변경 합니다 <xref:System.Windows.Media.Matrix>. 이렇게 변경 하면 단추가 늘어나거나 왜곡 됩니다. 또한이 예제에서는 단추가 <xref:System.Windows.Media.Matrix.OffsetX%2A> 위치 <xref:System.Windows.Media.Matrix.OffsetY%2A> 를 변경 하도록 및 속성을 변경 합니다.  
  
2. 초 <xref:System.Windows.Media.Matrix> (1.0 초)에 애니메이션 효과를 적용 합니다. 단추가 더 이상 기울어짐 또는 스트레치 되지 않은 상태에서 단추가 다른 위치로 이동 합니다.  
  
3. 애니메이션을 무기한 반복 합니다.  
  
> [!NOTE]
> <xref:System.Windows.Media.Animation.DiscreteMatrixKeyFrame> 개체에서 파생 되는 키 프레임은 값 간에 급격 한 점프가 생성 됩니다. 즉, 애니메이션의 이동이 jerky 됩니다.  
  
 [!code-xaml[keyframes_snip#MatrixAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/MatrixAnimationUsingKeyFramesExample.xaml#matrixanimationusingkeyframeswholepage)]  
  
 전체 샘플을 보려면 [키 프레임 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=160012)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.MatrixTransform.Matrix%2A>
- <xref:System.Windows.Media.MatrixTransform>
- [키 프레임 애니메이션 개요](key-frame-animations-overview.md)
- [키 프레임 방법 항목](key-frame-animation-how-to-topics.md)
