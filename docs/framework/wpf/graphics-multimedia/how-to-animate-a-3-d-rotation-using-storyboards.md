---
title: '방법: 스토리보드를 사용하여 3차원 회전에 애니메이션 효과 주기'
ms.date: 03/30/2017
helpviewer_keywords:
- Storyboards [WPF]
- 3-D translations [WPF], animating [WPF], with Storyboards
- animation [WPF], 3-D translations [WPF], with Storyboards
ms.assetid: 1020e44e-e21e-49a8-be53-53cbc1910e83
ms.openlocfilehash: 03b01205f1a31426a01b09533b350682c384df4b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62024757"
---
# <a name="how-to-animate-a-3-d-rotation-using-storyboards"></a>방법: 스토리보드를 사용하여 3차원 회전에 애니메이션 효과 주기
다음 예제에서는 "비틀" 애니메이션으로 회전 3D 개체를 확인 하는 방법을 보여 줍니다 합니다 <xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Angle%2A> 및 <xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Axis%2A> 의 속성을 <xref:System.Windows.Media.Media3D.AxisAngleRotation3D> 개체입니다. 이 <xref:System.Windows.Media.Media3D.AxisAngleRotation3D> 개체 3D 개체의 회전 변환을 지정 하 고 원하는 회전 효과 만듭니다 하므로 해당 속성에 애니메이션을 적용 합니다. 스토리 보드 내 <xref:System.Windows.Media.Animation.DoubleAnimation> 애니메이션을 적용 하는 데 사용 되는 <xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Angle%2A> 하는 동안 속성 <xref:System.Windows.Media.Animation.Vector3DAnimation> 애니메이션을 적용 하는 데 사용 되는 <xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Axis%2A> 속성.  
  
## <a name="example"></a>예제  
 [!code-xaml[Animation3DGallery_snip#Rotate3DUsingAxisAngleRotation3DExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/Rotat3DUsingAxisAngleRotation3DExample.xaml#rotate3dusingaxisanglerotation3dexamplewholepage)]  
  
## <a name="see-also"></a>참고자료

- [Rotation3DAnimation을 사용하여 3차원 회전에 애니메이션 효과 주기](how-to-animate-a-3-d-rotation-using-rotation3danimation.md)
- [키 프레임을 사용하여 3차원 회전에 애니메이션 효과 주기(Rotation3DAnimationUsingKeyFrames)](how-to-animate-a-3-d-rotation-using-key-frames.md)
- [3차원 그래픽 개요](3-d-graphics-overview.md)
- [Storyboard 개요](storyboards-overview.md)
