---
title: '방법: 시스템 글꼴 키 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- resource keys [WPF], SystemFonts class
ms.assetid: 036ebea7-5677-4f60-8ba4-56c9f9d9b8bd
ms.openlocfilehash: 7283e4225b75909322fa312583e9f1a0679762e2
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69918383"
---
# <a name="how-to-use-system-fonts-keys"></a>방법: 시스템 글꼴 키 사용
시스템 리소스는 개발자가 시스템 설정과 일관된 시각적 효과를 만들 수 있도록 몇 가지 시스템 메트릭을 리소스로 노출합니다. <xref:System.Windows.SystemFonts>는 값에 바인딩되는 시스템 글꼴 값과 시스템 글꼴 리소스 (예: <xref:System.Windows.SystemFonts.CaptionFontFamily%2A> 및 <xref:System.Windows.SystemFonts.CaptionFontFamilyKey%2A>)를 모두 포함 하는 클래스입니다.  
  
 시스템 글꼴 메트릭은 정적 리소스나 동적 리소스로 사용될 수 있습니다. 애플리케이션이 실행되는 동안 글꼴 메트릭을 자동으로 업데이트하려면 동적 리소스를 사용하고 자동으로 업데이트하지 않으려면 정적 리소스를 사용합니다.  
  
> [!NOTE]
> 동적 리소스는 키워드 *키* 를 속성 이름에 추가 합니다.  
  
 다음 예제에서는 시스템 글꼴 동적 리소스에 액세스한 후 사용하여 단추에 스타일을 지정하거나 단추를 사용자 지정하는 방법을 보여 줍니다. 이 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 예제에서는 단추에 값을 할당 <xref:System.Windows.SystemFonts> 하는 단추 스타일을 만듭니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[SystemRes_snip#FontDynamicResources](~/samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/MyApp.xaml#fontdynamicresources)]  
  
## <a name="see-also"></a>참고자료

- [시스템 브러시로 영역 그리기](../graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)
- [SystemParameters 사용](how-to-use-systemparameters.md)
- [SystemFonts 사용](how-to-use-systemfonts.md)
