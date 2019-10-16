---
title: '방법: 3차원 개체의 앞뒤에 재질 적용'
ms.date: 03/30/2017
helpviewer_keywords:
- 3-D objects [WPF], applying Material class
- Material class [WPF], applying to both sides of 3-D object
- classes [WPF], Material
ms.assetid: d93c8ad6-4939-4d29-9544-4d16d98093c1
ms.openlocfilehash: 1d3f6a0622b5e0ccccf14af99782bb78dfe87ccb
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61698970"
---
# <a name="how-to-apply-material-to-the-front-and-back-of-a-3-d-object"></a>방법: 3차원 개체의 앞뒤에 재질 적용
다음 예제에 적용 하는 방법을 보여 줍니다는 <xref:System.Windows.Media.Media3D.Material> 전면 및 후면 3 차원 개체 및 개체의 양쪽에 표시할 개체에 애니메이션을 적용 합니다. <xref:System.Windows.Media.Media3D.GeometryModel3D.Material%2A> 의 속성을 <xref:System.Windows.Media.Media3D.GeometryModel3D> 빨간색을 적용 하는 데 사용 됩니다 <xref:System.Windows.Media.Brush> 개체의 전면에 및 <xref:System.Windows.Media.Media3D.GeometryModel3D.BackMaterial%2A> 속성의는 <xref:System.Windows.Media.Media3D.GeometryModel3D> 파란색을 적용 하는 데 사용 됩니다 <xref:System.Windows.Media.Brush> 개체의 뒷면에. 아래 코드에서는 개체에 대 한 자료의 응용 프로그램을 보여 줍니다.  
  
 [!code-xaml[Animation3DGallery_snip#BackMaterialAnimationExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/BackMaterialAnimationExample.xaml#backmaterialanimationexampleinline1)]  
  
## <a name="example"></a>예제  
 다음 코드에는 전체 샘플을 보여 줍니다.  
  
 [!code-xaml[Animation3DGallery_snip#BackMaterialAnimationExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/BackMaterialAnimationExample.xaml#backmaterialanimationexamplewholepage)]  
  
## <a name="see-also"></a>참고자료

- [3차원 장면 만들기](how-to-create-a-3-d-scene.md)
- [3차원 그래픽 개요](3-d-graphics-overview.md)
- [3차원 장면의 Material 속성에 애니메이션 효과 주기](how-to-animate-material-properties-in-a-3-d-scene.md)
- [3차원 개체에 EmissiveMaterial 적용](how-to-apply-emissive-material-to-a-3-d-object.md)
