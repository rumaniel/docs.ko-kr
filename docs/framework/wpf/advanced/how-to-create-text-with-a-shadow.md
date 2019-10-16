---
title: '방법: 그림자가 적용된 텍스트 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- typography [WPF], shadow effects
- shadow effects in text [WPF]
- text [WPF], shadowed
ms.assetid: 6ab9c754-6001-4708-b479-5367f2fd1a35
ms.openlocfilehash: 0fe64e4e9e7aadbd30a38743647251f9fa49ba95
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69960436"
---
# <a name="how-to-create-text-with-a-shadow"></a>방법: 그림자가 적용된 텍스트 만들기
이 단원의 예제에서는 표시된 텍스트에 대해 그림자 효과를 만드는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 개체 <xref:System.Windows.Media.Effects.DropShadowEffect> 를 사용 하 여 개체에 대 한 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 그림자 효과를 다양 하 게 만들 수 있습니다. 다음 예제에서는 그림자 효과가 적용된 텍스트를 보여 줍니다. 이 경우 그림자는 그림자 색깔이 흐린, 부드러운 그림자입니다.  
  
 ![부드러움 &#61; 0.25이 있는 텍스트 그림자](./media/how-to-create-text-with-a-shadow/drop-shadow-text-effect.jpg) 
  
 속성을 <xref:System.Windows.Media.Effects.DropShadowEffect.ShadowDepth%2A> 설정 하 여 그림자의 너비를 제어할 수 있습니다. 값은 그림자 `4.0` 너비 (4 픽셀)를 나타냅니다. 속성을 <xref:System.Windows.Media.Effects.DropShadowEffect.BlurRadius%2A> 수정 하 여 그림자의 부드러움 또는 흐림 효과를 제어할 수 있습니다. 값 `0.0` 이 이면 흐리게 표시 되지 않습니다. 다음 코드 예제에서는 부드러운 그림자를 만드는 방법을 보여 줍니다.  
  
 [!code-xaml[TextShadowSnippets#TextShadowSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/SingleShadows.xaml#textshadowsnippet1)]  
  
> [!NOTE]
> 이러한 그림자 효과는 텍스트 렌더링 파이프라인을 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 통해 이동 하지 않습니다. 따라서 이러한 효과를 사용할 때 ClearType이 사용하지 않도록 설정됩니다.  
  
 다음 예제에서는 진한 그림자 효과가 적용된 텍스트를 보여 줍니다. 이 경우 그림자가 흐려지지 않습니다.  
  
 ![부드러움 &#61; 0이 있는 텍스트 그림자](./media/how-to-create-text-with-a-shadow/text-shadow-softness.jpg) 
  
 <xref:System.Windows.Media.Effects.DropShadowEffect.BlurRadius%2A> 속성을로 `0.0`설정 하 여 하드 그림자를 만들 수 있습니다 .이는 흐리게가 사용 되지 않음을 나타냅니다. 속성을 <xref:System.Windows.Media.Effects.DropShadowEffect.Direction%2A> 수정 하 여 그림자의 방향을 제어할 수 있습니다. 이 속성의 방향 값을와 `0` `360`사이의 수준으로 설정 합니다. 다음 그림에서는 <xref:System.Windows.Media.Effects.DropShadowEffect.Direction%2A> 속성 설정의 방향 값을 보여 줍니다.  
  
 ![그림자의 DropShadow 정도 설정](./media/how-to-create-text-with-a-shadow/drop-shadow-degree-setting.png)
  
 다음 코드 예제에서는 진한 그림자를 만드는 방법을 보여 줍니다.  
  
 [!code-xaml[TextShadowSnippets#TextShadowSnippet2](~/samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/SingleShadows.xaml#textshadowsnippet2)]  
  
## <a name="using-a-blur-effect"></a>흐림 효과 사용  
 는 <xref:System.Windows.Media.Effects.BlurBitmapEffect> 텍스트 개체 뒤에 배치할 수 있는 그림자와 같은 효과를 만드는 데 사용할 수 있습니다. 텍스트에 적용된 흐림 비트맵 효과는 모든 방향에서 균등하게 텍스트를 흐리게 만듭니다.  
  
 다음 예제에서는 흐림 효과가 적용된 텍스트를 보여 줍니다.  
  
 ![BlurBitmapEffect를 사용한 텍스트 그림자](./media/how-to-create-text-with-a-shadow/text-shadow-blur-effect.jpg)  
  
 다음 코드 예제에는 흐린 효과를 만드는 방법을 보여 줍니다.  
  
 [!code-xaml[TextShadowSnippets#TextShadowSnippet6](~/samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/BlurShadows.xaml#textshadowsnippet6)]  
  
## <a name="using-a-translate-transform"></a>좌표 이동 변환 사용  
 는 <xref:System.Windows.Media.TranslateTransform> 텍스트 개체 뒤에 배치할 수 있는 그림자와 같은 효과를 만드는 데 사용할 수 있습니다.  
  
 다음 코드 예제에서는를 사용 <xref:System.Windows.Media.TranslateTransform> 하 여 텍스트를 오프셋 합니다. 이 예제에서 기본 텍스트 아래에 있는 약간 오프셋된 텍스트 복사본이 그림자 효과를 만듭니다.  
  
 ![TranslateTransform을 사용한 텍스트 그림자](./media/how-to-create-text-with-a-shadow/text-transform-shadow-effect.jpg)    
  
 다음 코드 예제에서는 그림자 효과에 변환을 만드는 방법을 보여 줍니다.  
  
 [!code-xaml[TextShadowSnippets#TextShadowSnippet7](~/samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/TransformShadows.xaml#textshadowsnippet7)]
