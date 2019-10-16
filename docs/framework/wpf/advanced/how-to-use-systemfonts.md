---
title: '방법: SystemFonts 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- system fonts [WPF]
- fonts [WPF], system fonts
- classes [WPF], SystemFonts
ms.assetid: 3f46a4ec-2225-408a-8123-8838a8f7057a
ms.openlocfilehash: 7438705a82faee464649b5f6f577627a379e9a8c
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69918358"
---
# <a name="how-to-use-systemfonts"></a>방법: SystemFonts 사용
이 예제에서는 <xref:System.Windows.SystemFonts> 클래스의 정적 리소스를 사용 하 여 단추에 스타일을 지정 하거나 사용자 지정 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 시스템 설정과 일관된 시각적 효과를 만들도록 지원하기 위해 시스템 리소스는 몇 가지 시스템이 결정하는 값을 리소스와 속성 모두로 노출합니다. <xref:System.Windows.SystemFonts>는 시스템 글꼴 값을 정적 속성으로 포함 하는 클래스이 고, 런타임에 이러한 값에 동적으로 액세스 하는 데 사용할 수 있는 리소스 키를 참조 하는 속성입니다. 예 <xref:System.Windows.SystemFonts.CaptionFontFamily%2A> 를 들어 <xref:System.Windows.SystemFonts> 은 값이 고 <xref:System.Windows.SystemFonts.CaptionFontFamilyKey%2A> 은 해당 리소스 키입니다.  
  
 에서는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 의<xref:System.Windows.SystemFonts> 멤버를 정적 속성 또는 동적 리소스 참조 (정적 속성 값을 키로 사용 하는)로 사용할 수 있습니다. 애플리케이션이 실행되는 동안 글꼴 메트릭을 자동으로 업데이트하려면 동적 리소스 참조를 사용하고 자동으로 업데이트하지 않으려면 정적 값 참조를 사용합니다.  
  
> [!NOTE]
> 리소스 키의 경우 속성 이름 뒤에 “Key”라는 접미사가 붙습니다.  
  
 다음 예제에서는 단추에 스타일을 지정 하거나 사용자 지정 하기 <xref:System.Windows.SystemFonts> 위해의 속성을 정적 값으로 액세스 하 고 사용 하는 방법을 보여 줍니다. 이 태그 예제에서는 <xref:System.Windows.SystemFonts> 단추에 값을 할당 합니다.  
  
 [!code-xaml[SystemRes_snip#FontStaticResources](~/samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml#fontstaticresources)]  
  
 코드에서의 <xref:System.Windows.SystemFonts> 값을 사용 하려면 정적 값 또는 동적 리소스 참조를 사용할 필요가 없습니다. 대신 <xref:System.Windows.SystemFonts> 클래스의 키가 아닌 속성을 사용 합니다. 키가 아닌 속성이 정적 속성으로 정의 된 경우에도 시스템에서 호스팅되는의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 런타임 동작은 속성을 실시간으로 다시 평가 하 고 시스템 값에 대 한 사용자 기반 변경을 적절 하 게 고려 합니다. 다음 예제에서는 단추의 글꼴 설정을 지정하는 방법을 보여 줍니다.  
  
 [!code-csharp[SystemRes_snip#FontResourcesCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml.cs#fontresourcescode)]
 [!code-vb[SystemRes_snip#FontResourcesCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SystemRes_snip/VisualBasic/Pane1.xaml.vb#fontresourcescode)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.SystemFonts>
- [시스템 브러시로 영역 그리기](../graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)
- [SystemParameters 사용](how-to-use-systemparameters.md)
- [시스템 글꼴 키 사용](how-to-use-system-fonts-keys.md)
- [방법 항목](resources-how-to-topics.md)
- [x:Static 태그 확장](../../xaml-services/x-static-markup-extension.md)
- [XAML 리소스](xaml-resources.md)
- [DynamicResource 태그 확장](dynamicresource-markup-extension.md)
