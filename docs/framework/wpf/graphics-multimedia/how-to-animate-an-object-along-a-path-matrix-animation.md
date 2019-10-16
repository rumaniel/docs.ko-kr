---
title: '방법: 경로를 따라 개체에 애니메이션 효과 주기(Matrix 애니메이션)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], objects along paths (matrix animation)
- matrix animation [WPF]
ms.assetid: 7000e697-1414-468c-b915-cf66062fc49e
ms.openlocfilehash: 3c90d20cac60004aa9876d9fe8d213d33c5a6883
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64651431"
---
# <a name="how-to-animate-an-object-along-a-path-matrix-animation"></a>방법: 경로를 따라 개체에 애니메이션 효과 주기(Matrix 애니메이션)
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> 클래스에서 정의 된 경로 따라 개체에 애니메이션 효과를 <xref:System.Windows.Media.PathGeometry>합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 다음을 수행하여 경로를 따라 개체에 애니메이션 효과를 줍니다.  
  
- 적용 되는 <xref:System.Windows.Media.MatrixTransform> 이동 하기 위해 개체입니다.  
  
- 경로 사용 하 여 정의 된 <xref:System.Windows.Media.PathGeometry>합니다.  
  
- 만듭니다는 <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> 애니메이션을 적용 하는 데 사용 합니다 <xref:System.Windows.Media.Matrix> 의 속성을 <xref:System.Windows.Media.MatrixTransform>. <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> 사용 합니다 <xref:System.Windows.Media.PathGeometry> 생성 하는 데 사용 하 고 <xref:System.Windows.Media.Matrix> 값.  
  
 [!code-xaml[PathAnimationGallery_snippet#MatrixAnimationUsingPathWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/matrixanimationusingpathexample.xaml#matrixanimationusingpathwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/MatrixAnimationUsingPathExample.cs#matrixanimationusingpathwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/MatrixAnimationUsingPathExample.vb#matrixanimationusingpathwholepage)]  
  
 전체 샘플을 참조 하세요 [경로 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=160028)합니다. 기하학적 경로 대 한 자세한 내용은 참조는 [기 하 도형 개요](geometry-overview.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [애니메이션 개요](animation-overview.md)
- [경로 애니메이션 샘플](https://go.microsoft.com/fwlink/?LinkID=160028)
- [경로 애니메이션 방법 항목](path-animation-how-to-topics.md)
