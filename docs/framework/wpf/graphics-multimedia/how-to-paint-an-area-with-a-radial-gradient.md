---
title: '방법: 방사형 그라데이션으로 영역 칠하기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], painting with radial gradients
- radial gradients [WPF], painting with
- painting [WPF], with radial gradients
ms.assetid: b5d0fc8a-8986-4796-b003-a75b41a48928
ms.openlocfilehash: 5762ef1a1526ba6f004917c8a947e35ce731c86d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916094"
---
# <a name="how-to-paint-an-area-with-a-radial-gradient"></a>방법: 방사형 그라데이션으로 영역 칠하기
이 예제에서는 <xref:System.Windows.Media.RadialGradientBrush> 클래스를 사용 하 여 방사형 그라데이션으로 영역을 그리는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는를 <xref:System.Windows.Media.RadialGradientBrush> 사용 하 여 노랑에서 빨강, 파랑, 녹색으로 전환 되는 방사형 그라데이션으로 사각형을 그립니다.  
  
 [!code-csharp[BrushesIntroduction_snip#SimpleRadialGradientExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/RadialGradientBrushSnippet.cs#simpleradialgradientexamplewholepage)]
 [!code-vb[BrushesIntroduction_snip#SimpleRadialGradientExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/radialgradientbrushsnippet.vb#simpleradialgradientexamplewholepage)]
 [!code-xaml[BrushesIntroduction_snip#SimpleRadialGradientExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/RadialGradientBrushSnippet.xaml#simpleradialgradientexamplewholepage)]  
  
 다음 그림에서는 이전 예제의 그라데이션을 보여 줍니다. 그라데이션 중지점이 강조 표시 되었습니다.  
  
 ![방사형 그라데이션의 그라데이션 중지점](./media/wcpsdk-graphicsmm-4gradientstops-rg.png "wcpsdk_graphicsmm_4gradientstops")  
  
> [!NOTE]
> 이 항목의 예제에서는 기본 좌표계를 사용 하 여 컨트롤 요소를 설정 합니다. 기본 좌표계는 경계 상자를 기준으로 합니다. 0은 경계 상자의 0%를 나타내고 1은 경계 상자의 100%를 나타냅니다. <xref:System.Windows.Media.GradientBrush.MappingMode%2A> 속성을 값 <xref:System.Windows.Media.BrushMappingMode.Absolute>으로 설정 하 여이 좌표계를 변경할 수 있습니다. 절대 좌표계는 경계 상자를 기준으로 하지 않습니다. 값은 로컬 공간에서 직접 해석됩니다.  
  
 추가 <xref:System.Windows.Media.RadialGradientBrush> 예제는 [브러시 샘플](https://go.microsoft.com/fwlink/?LinkID=159973)을 참조 하세요. 그라데이션 및 기타 브러시 형식에 대 한 자세한 내용은 [단색 및 그라데이션을 사용한 그리기 개요](painting-with-solid-colors-and-gradients-overview.md)를 참조 하세요.
