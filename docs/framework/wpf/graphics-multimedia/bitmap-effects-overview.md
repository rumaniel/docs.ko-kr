---
title: 비트맵 효과 개요
ms.date: 03/30/2017
helpviewer_keywords:
- bitmap effects [WPF]
ms.assetid: 23cb338e-4b59-4b52-b294-96431f9c9568
ms.openlocfilehash: f2fa42d5d63cad6a71efd259416dad3416bf2d72
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69935294"
---
# <a name="bitmap-effects-overview"></a>비트맵 효과 개요
비트맵 효과를 통해 디자이너와 개발자는 렌더링 된 Windows Presentation Foundation (WPF) 콘텐츠에 시각적 효과를 적용할 수 있습니다. 예를 들어 비트맵 효과를 사용 하면 이미지나 단추에 <xref:System.Windows.Media.Effects.DropShadowBitmapEffect> 효과 또는 흐림 효과를 쉽게 적용할 수 있습니다.  
  
> [!IMPORTANT]
> .NET Framework 4 이상 <xref:System.Windows.Media.Effects.BitmapEffect> 에서는 클래스가 사용 되지 않습니다. <xref:System.Windows.Media.Effects.BitmapEffect> 클래스를 사용 하려고 하면 사용 되지 않는 예외가 발생 합니다. 클래스에 대 한 <xref:System.Windows.Media.Effects.BitmapEffect> <xref:System.Windows.Media.Effects.Effect> 사용 되지 않는 대안은 클래스입니다. 대부분의 경우 클래스는 <xref:System.Windows.Media.Effects.Effect> 훨씬 더 빠릅니다.  

<a name="wpf_effects"></a>   
## <a name="wpf-bitmap-effects"></a>WPF 비트맵 효과  
 비트맵 효과 (<xref:System.Windows.Media.Effects.BitmapEffect> 개체)는 간단한 픽셀 처리 작업입니다. 비트맵 효과는를 <xref:System.Windows.Media.Imaging.BitmapSource> 입력으로 사용 하 고 효과를 적용 한 후 흐리게 또는 그림자와 같은 새 <xref:System.Windows.Media.Imaging.BitmapSource> 을 생성 합니다. 각 비트맵 효과는와 <xref:System.Windows.Media.Effects.BlurBitmapEffect.Radius%2A> <xref:System.Windows.Media.Effects.BlurBitmapEffect>같은 필터링 속성을 제어할 수 있는 속성을 노출 합니다.  
  
 특수 한 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]경우에는 <xref:System.Windows.Controls.Button> 또는 <xref:System.Windows.Media.Visual> <xref:System.Windows.Controls.TextBox>와 같은 라이브 개체의 속성으로 효과를 설정할 수 있습니다. 런타임에 픽셀 처리가 적용되고 렌더링됩니다. 이 경우 렌더링 <xref:System.Windows.Media.Visual> 시은 자동으로 해당으로 변환 <xref:System.Windows.Media.Imaging.BitmapSource> 되 고에 대 한 입력으로 <xref:System.Windows.Media.Effects.BitmapEffect>공급 됩니다. 출력은 개체의 <xref:System.Windows.Media.Visual> 기본 렌더링 동작을 대체 합니다. 이로 인해 <xref:System.Windows.Media.Effects.BitmapEffect> 개체는 시각적 개체를 소프트웨어 에서만 렌더링 하도록 하는 것입니다. 즉, 효과가 적용 되는 경우 시각적 개체에 대 한 하드웨어 가속이 없습니다.  
  
- <xref:System.Windows.Media.Effects.BlurBitmapEffect>포커스를 벗어난 개체를 시뮬레이션 합니다.  
  
- <xref:System.Windows.Media.Effects.OuterGlowBitmapEffect>개체의 둘레에 색의 후광을 만듭니다.  
  
- <xref:System.Windows.Media.Effects.DropShadowBitmapEffect>개체 뒤에 그림자를 만듭니다.  
  
- <xref:System.Windows.Media.Effects.BevelBitmapEffect>지정 된 곡선에 따라 이미지의 표면을 올리는 빗면을 만듭니다.  
  
- <xref:System.Windows.Media.Effects.EmbossBitmapEffect>인공 광원의 깊이와 질감 <xref:System.Windows.Media.Visual> 을 제공 하기 위해의 범프 매핑을 만듭니다.  
  
> [!NOTE]
> [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 비트맵 효과는 소프트웨어 모드에서 렌더링됩니다. 효과를 적용하는 모든 개체도 소프트웨어에서 렌더링됩니다. 큰 시각적 개체에 비트맵 효과를 사용하거나 비트맵 효과의 속성에 애니메이션 효과를 줄 때 성능이 가장 크게 저하됩니다. 따라서 여러분도 이러한 방식으로 비트맵 효과를 사용하지 않아야 하는 것은 물론, 다른 사용자들도 바람직한 경험을 얻을 수 있도록 철저히 테스트하고 주의해야 합니다.  
  
> [!NOTE]
> [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 비트맵 효과는 부분 신뢰 실행을 지원하지 않습니다. 비트맵 효과를 사용하려면 애플리케이션에 완전 신뢰 권한이 있어야 합니다.  
  
<a name="applyeffects"></a>   
## <a name="how-to-apply-an-effect"></a>효과를 적용하는 방법  
 <xref:System.Windows.Media.Effects.BitmapEffect>는의 <xref:System.Windows.Media.Visual>속성입니다. 따라서,, <xref:System.Windows.Controls.Button> <xref:System.Windows.Media.DrawingVisual>, <xref:System.Windows.Controls.Image> 등<xref:System.Windows.UIElement>의 시각적 개체에 효과를 적용 하는 것은 속성을 설정 하는 것 만큼 쉽습니다. <xref:System.Windows.UIElement.BitmapEffect%2A>단일 <xref:System.Windows.Media.Effects.BitmapEffect> 개체로 설정 하거나, <xref:System.Windows.Media.Effects.BitmapEffectGroup> 개체를 사용 하 여 여러 효과를 연결할 수 있습니다.  
  
 다음 예제에서는에서 <xref:System.Windows.Media.Effects.BitmapEffect> [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]를 적용 하는 방법을 보여 줍니다.  
  
 [!code-xaml[EffectsGallery_snip#BlurSimpleExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/EffectsGallery_snip/CSharp/blursimpleexample.xaml#blursimpleexampleinline)]  
  
 다음 예제에서는 코드에서를 <xref:System.Windows.Media.Effects.BitmapEffect> 적용 하는 방법을 보여 줍니다.  
  
 [!code-csharp[EffectsGallery_snip#CodeBehindBlurCodeBehindExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/EffectsGallery_snip/CSharp/blurcodebehindexample.xaml.cs#codebehindblurcodebehindexampleinline)]  
  
> [!NOTE]
> <xref:System.Windows.Media.Effects.BitmapEffect> 가 <xref:System.Windows.Controls.DockPanel> 또는 와<xref:System.Windows.Controls.Canvas>같은 레이아웃 컨테이너에 적용 되는 경우 모든 자식 요소를 포함 하 여 요소 또는 시각적 개체의 시각적 트리에 효과가 적용 됩니다.  
  
<a name="customeffects"></a>   
## <a name="creating-custom-effects"></a>사용자 지정 효과 만들기  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]에서는 또한 관리되는 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 응용 프로그램에서 사용할 수 있는 사용자 지정 효과를 만들기 위한 관리되지 않는 인터페이스를 제공합니다. 사용자 지정 비트맵 효과를 만들기 위한 추가 참조 자료에 대해서는 [관리되지 않는 WPF 비트맵 효과](https://docs.microsoft.com/previous-versions/windows/desktop/wibe/-wibe-lh) 설명서를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Effects.BitmapEffectGroup>
- <xref:System.Windows.Media.Effects.BitmapEffectInput>
- <xref:System.Windows.Media.Effects.BitmapEffectCollection>
- [관리 되지 않는 WPF 비트맵 효과](https://docs.microsoft.com/previous-versions/windows/desktop/wibe/-wibe-lh)
- [이미징 개요](imaging-overview.md)
- [보안](../security-wpf.md)
- [WPF 그래픽 렌더링 개요](wpf-graphics-rendering-overview.md)
- [2차원 그래픽 및 이미징](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
