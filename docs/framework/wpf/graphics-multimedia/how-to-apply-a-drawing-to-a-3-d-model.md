---
title: '방법: 3차원 모델에 그리기 적용'
ms.date: 03/30/2017
helpviewer_keywords:
- drawings [WPF], applying to 3-D models
- 3-D models [WPF], applying drawings to
ms.assetid: 68357577-b7fc-446e-8be9-a8cc7df3a350
ms.openlocfilehash: 14470d0adeb948ea46a0720b5713c20fb7d8e6d8
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855874"
---
# <a name="how-to-apply-a-drawing-to-a-3-d-model"></a>방법: 3차원 모델에 그리기 적용

이 예제에서는을 <xref:System.Windows.Media.DrawingBrush> <xref:System.Windows.Media.Media3D.Material> 3 차원 모델에 적용 하 여를 사용 하는 방법을 보여 줍니다.

다음 코드에서는를 <xref:System.Windows.Media.DrawingGroup> <xref:System.Windows.Media.DrawingBrush>의 콘텐츠로 정의 합니다.  는 3 차원 평면에 <xref:System.Windows.Media.Media3D.DiffuseMaterial.Brush%2A> 적용 된 <xref:System.Windows.Media.Media3D.DiffuseMaterial> 의 속성으로 설정 됩니다.<xref:System.Windows.Media.DrawingBrush>

> [!NOTE]
> 코드를 다시 사용 하 고 단순화할 수 있는 리소스로 아래 드로잉과 같이 복잡 한 개체 및 값을 정의 하는 것이 좋습니다. 자세한 내용은 [XAML 리소스](../advanced/xaml-resources.md) 를 참조 하세요.

[!code-xaml[3DGallery_snip#ApplyDrawingToMaterialInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ApplyDrawingToMaterialExample.xaml#applydrawingtomaterialinline1)]

## <a name="example"></a>예제

다음 코드에는 전체 샘플을 보여 줍니다.

[!code-xaml[3DGallery_snip#ApplyDrawingToMaterialExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ApplyDrawingToMaterialExample.xaml#applydrawingtomaterialexamplewholepage)]

## <a name="see-also"></a>참고자료

- [XAML 리소스](../advanced/xaml-resources.md)
- [3차원 장면 만들기](how-to-create-a-3-d-scene.md)
- [Drawing 개체 개요](drawing-objects-overview.md)
- [3차원 그래픽 개요](3-d-graphics-overview.md)
