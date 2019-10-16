---
title: '방법: 3차원 개체에 발광 재질 적용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- EmissiveMaterial [WPF], applying to 3-D objects
- 3-D objects [WPF], applying EmissiveMaterial
ms.assetid: fd442cc2-5adc-487a-ba70-e45ed54bb3b4
ms.openlocfilehash: b898148fa07950e3ad1eddcaf9206f7d6a837241
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61698982"
---
# <a name="how-to-apply-emissive-material-to-a-3-d-object"></a>방법: 3차원 개체에 발광 재질 적용
다음 예제에서는 사용 하는 방법을 보여 줍니다 <xref:System.Windows.Media.Media3D.EmissiveMaterial> 색 EmissiveMaterial의 브러시의 색 같음는 기존 자료에 추가 합니다. 아래 코드 <xref:System.Windows.Media.Media3D.DiffuseMaterial> 고 <xref:System.Windows.Media.Media3D.EmissiveMaterial> 파란색 DiffuseMaterial의 모양을 추가할 조합에 적용 합니다.  
  
 [!code-xaml[3DGallery_snip#EmmisiveMaterialAnimationExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/EmissiveMaterialExample.xaml#emmisivematerialanimationexampleinline1)]  
  
 프로시저 코드  
  
 [!code-csharp[3DGallery_procedural_snip#EmissiveMaterialCodeExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_procedural_snip/CSharp/EmissiveMaterialExample.cs#emissivematerialcodeexampleinline1)]
 [!code-vb[3DGallery_procedural_snip#EmissiveMaterialCodeExampleInline1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DGallery_procedural_snip/visualbasic/emissivematerialexample.vb#emissivematerialcodeexampleinline1)]  
  
## <a name="example"></a>예제  
 다음 코드는 XAML에서 전체 샘플을 보여줍니다.  
  
 [!code-xaml[3DGallery_snip#EmissiveMaterialExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/EmissiveMaterialExample.xaml#emissivematerialexamplewholepage)]  
  
## <a name="example"></a>예제  
 프로시저 코드에서 전체 샘플을 다음과 같습니다.  
  
 [!code-csharp[3DGallery_procedural_snip#EmissiveMaterialCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_procedural_snip/CSharp/EmissiveMaterialExample.cs#emissivematerialcodeexamplewholepage)]
 [!code-vb[3DGallery_procedural_snip#EmissiveMaterialCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DGallery_procedural_snip/visualbasic/emissivematerialexample.vb#emissivematerialcodeexamplewholepage)]  
  
## <a name="see-also"></a>참고자료

- [3차원 장면 만들기](how-to-create-a-3-d-scene.md)
- [3차원 그래픽 개요](3-d-graphics-overview.md)
- [3차원 장면의 Material 속성에 애니메이션 효과 주기](how-to-animate-material-properties-in-a-3-d-scene.md)
- [3차원 개체의 앞과 뒤에 Material 적용](how-to-apply-material-to-the-front-and-back-of-a-3-d-object.md)
