---
title: '방법: 키 프레임을 사용하여 카메라 위치 및 방향에 애니메이션 효과 주기'
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], camera direction with key frames
- key frames [WPF], animating camera direction
- animation [WPF], camera position with key frames
- camera position [WPF], animating with key frames
- key frames [WPF], animating camera position
- camera direction [WPF], animating with key frames
ms.assetid: 5753024e-0057-454d-947f-43ea686879c7
ms.openlocfilehash: 44464cc314d649516998338e36c1b523101ac4e2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61651339"
---
# <a name="how-to-animate-camera-position-and-direction-using-key-frames"></a>방법: 키 프레임을 사용하여 카메라 위치 및 방향에 애니메이션 효과 주기
다음 예에서 <xref:System.Windows.Media.Animation.Point3DAnimationUsingKeyFrames> 위치에 애니메이션을 적용 하는 데 사용 되는 <xref:System.Windows.Media.Media3D.PerspectiveCamera> 3D 장면에서. 또한 <xref:System.Windows.Media.Animation.Vector3DAnimationUsingKeyFrames> 3D 장면에서 카메라 가리키고 방향에 애니메이션을 적용 하는 데 사용 됩니다. 이러한 애니메이션은 둘 다 다양 한 애니메이션 효과 만드는 몇 가지 키 프레임을 사용 합니다.  
  
1. <xref:System.Windows.Media.Animation.LinearPoint3DKeyFrame> 및 <xref:System.Windows.Media.Animation.LinearVector3DKeyFrame> 값 사이 매끄러운 선형 보간을 만드는 데 사용 됩니다.  
  
2. <xref:System.Windows.Media.Animation.DiscretePoint3DKeyFrame> 및 <xref:System.Windows.Media.Animation.DiscreteVector3DKeyFrame> "사이 갑작스러운" 값 (보간 없음)를 만드는 데 사용 됩니다.  
  
3. <xref:System.Windows.Media.Animation.SplinePoint3DKeyFrame> 및 <xref:System.Windows.Media.Animation.SplineVector3DKeyFrame> 에 따라 값 사이 가변 전환을 만드는 데 사용 되는 <xref:System.Windows.Media.Animation.SplinePoint3DKeyFrame.KeySpline%2A> 속성입니다. 아래 예제에서는 애니메이션이 서서히 하지만 시간 세그먼트의 끝에 다가가 시작, 면 기하급수적으로 빨라집니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[Animation3DGallery_snip#PointVector3DAnimationUsingKeyFramesExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/PointVector3DAnimationUsingKeyFramesExample.xaml#pointvector3danimationusingkeyframesexamplewholepage)]  
  
## <a name="see-also"></a>참고자료

- [3차원 장면에서 카메라 위치 및 방향에 애니메이션 효과 주기](how-to-animate-camera-position-and-direction-in-a-3d-scene.md)
- [3차원 그래픽 개요](3-d-graphics-overview.md)
