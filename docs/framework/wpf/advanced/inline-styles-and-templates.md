---
title: 인라인 스타일 및 템플릿
ms.date: 03/30/2017
helpviewer_keywords:
- inline templates [WPF]
- styles [WPF], inline
- templates [WPF], inline
- inline styles [WPF]
ms.assetid: 69a1a3f9-acb5-4e2c-9c43-2e376c055ac4
ms.openlocfilehash: b566e157e2d4a9e9be21a678541bf5d5341a898c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62051015"
---
# <a name="inline-styles-and-templates"></a>인라인 스타일 및 템플릿
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 제공 <xref:System.Windows.Style> 개체 및 템플릿은 개체 (<xref:System.Windows.FrameworkTemplate> 서브 클래스) 리소스에서 요소의 시각적 모양을 정의 하는 방법,으로 사용할 수 있도록 여러 번입니다. 따라서 특성 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 형식을 사용 하 <xref:System.Windows.Style> 고 <xref:System.Windows.FrameworkTemplate> 거의 항상 리소스 참조를 기존 스타일 및 템플릿 사용 하지 않고 새로 인라인을 정의 합니다.  
  
## <a name="limitations-of-inline-styles-and-templates"></a>인라인 스타일 및 템플릿의 제한 사항  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], 스타일 및 템플릿 속성 기술적으로 두 가지 방법 중 하나로 설정할 수 있습니다. 예를 들어 리소스 내에서 정의 된 스타일을 참조할 특성 구문을 사용할 수 있습니다 `<` *개체*`Style="{StaticResource`*myResourceKey*`}" .../>`합니다. 또는 예를 들어 인라인 스타일을 정의 하려면 속성 요소 구문을 사용할 수 있습니다.  
  
 `<` *개체* `>`  
  
 `<` *개체* `.Style>`  
  
 `<` `Style`  `.../>`  
  
 `</` *개체* `.Style>`  
  
 `</` *개체* `>`  
  
 특성을 사용 하는 것이 훨씬 더 일반적입니다. 인라인으로 정의 및에서는 정의 되지 않은 리소스는 스타일을 포함 하는 요소에만 범위가 지정 이므로 사용할 수 없습니다 다시 쉽게 없는 리소스 키를 있기 때문입니다. 일반적 리소스 정의 스타일을 유용 하 게 이며 더 일반적인 부합 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 프로그래밍 모델 원칙 태그에는 디자인에서 코드의 프로그램 논리를 분리 합니다.  
  
 일반적으로 해당 위치에 해당 스타일이 나 템플릿을 사용 하려는 경우에 스타일 또는 템플릿이 인라인을 설정할 필요가 없습니다 있습니다. 스타일이 나 템플릿을 사용할 수 있는 대부분의 요소는 또한 콘텐츠 속성 및 콘텐츠 모델을 지원 합니다. 어떤 논리 트리만 사용 하는 경우 만든 스타일이 나 템플릿을 통해 한 번,는 것이 더욱 쉽게 직접 태그에서 해당 자식 요소를 사용 하 여 해당 콘텐츠 속성을 채우는 것입니다. 이 스타일 및 템플릿 메커니즘은 완전히 바이패스 됩니다.  
  
 개체를 반환 하는 태그 확장으로 사용 하도록 설정 하는 다른 구문 스타일 및 템플릿을 사용할 수도 있습니다. 이러한 두 확장 가능한 시나리오에 포함할 [TemplateBinding](templatebinding-markup-extension.md) 고 <xref:System.Windows.Data.Binding>입니다.  
  
## <a name="see-also"></a>참고자료

- [스타일 지정 및 템플릿](../controls/styling-and-templating.md)
