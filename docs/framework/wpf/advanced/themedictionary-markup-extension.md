---
title: ThemeDictionary 태그 확장
ms.date: 03/30/2017
f1_keywords:
- ThemeDictionaryExtension
- ThemeDictionary
helpviewer_keywords:
- ThemeDictionary markup extension [WPF]
- XAML [WPF], ThemeDictionary markup extension
ms.assetid: aa75e10b-13dd-4989-972d-51bab63a05e2
ms.openlocfilehash: 7fa729d600f25b73028bae0dd6d9248b5839dd4c
ms.sourcegitcommit: 77e33b682db39955e331b8e8eda4ef1925a24e78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70133870"
---
# <a name="themedictionary-markup-extension"></a>ThemeDictionary 태그 확장
타사 컨트롤을 통합하는 사용자 지정 컨트롤 작성자 또는 애플리케이션이 컨트롤 스타일 지정에 사용할 테마별 리소스 사전을 로드하는 방법을 제공합니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xml  
<object property="{ThemeDictionary assemblyUri}" .../>  
```  
  
## <a name="xaml-object-element-usage"></a>XAML 개체 요소 사용  
  
```xml  
<object>  
  <object.property>  
    <ThemeDictionary AssemblyName="assemblyUri"/>  
  <object.property>  
<object>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|`assemblyUri`|테마 정보가 포함된 어셈블리의 [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]입니다. 일반적으로 이는 더 큰 패키지에서 어셈블리를 참조하는 Pack URI입니다. 어셈블리 리소스 및 Pack URI는 배포 문제를 완화합니다. 자세한 내용은 [WPF의 Pack URI](../app-development/pack-uris-in-wpf.md)를 참조하세요.|  
  
## <a name="remarks"></a>설명  
 이 확장은 하나의 특정 속성 값 (에 대 한 <xref:System.Windows.ResourceDictionary.Source%2A?displayProperty=nameWithType>값)만 채우도록 설계 되었습니다.  
  
 이 확장을 사용 하 여 Windows Aero 테마가 사용자 시스템에 적용 되는 경우에만 사용할 일부 스타일을 포함 하는 단일 리소스 전용 어셈블리를 지정 하 고 Luna 테마가 활성 상태인 경우에만 다른 스타일을 지정할 수 있습니다. 이 확장을 사용하면 컨트롤별 리소스 사전의 콘텐츠가 자동으로 유효성이 검사되고 필요한 경우 또 다른 테마에 관련되도록 다시 로드됩니다.  
  
 문자열 `assemblyUri` (<xref:System.Windows.ThemeDictionaryExtension.AssemblyName%2A> 속성 값)은 특정 테마에 적용 되는 사전을 식별 하는 명명 규칙의 기본을 형성 합니다. 의 <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A> [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 논리는 미리 컴파일된 리소스 어셈블리에 포함 된 특정 테마 사전 변형을 가리키는을 생성 하 여 규칙을 완료 합니다. `ThemeDictionary` 여기서는 이 규칙에 대한 설명이나 개념상 일반 컨트롤 스타일 지정 및 페이지/응용 프로그램 수준 스타일 지정과 테마의 상호 작용을 다루지 않습니다. 를 사용 하 `ThemeDictionary` 는 기본 시나리오는 응용 프로그램 <xref:System.Windows.ResourceDictionary.Source%2A> 수준에서 `ResourceDictionary` 선언 된의 속성을 지정 하는 것입니다. 직접 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]가 아닌 `ThemeDictionary`를 통해 어셈블리에 대한 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]를 제공할 경우 확장 논리는 시스템 테마가 변경될 때마다 유효성 검사 논리를 제공합니다.  
  
 특성 구문은 이러한 태그 확장에 가장 많이 사용되는 구문입니다. `ThemeDictionary` 식별자 문자열 다음에 나오는 문자열 토큰은 기본 <xref:System.Windows.ThemeDictionaryExtension.AssemblyName%2A> 확장 클래스의 <xref:System.Windows.ThemeDictionaryExtension> 값으로 할당됩니다.  
  
 `ThemeDictionary`는 개체 요소 구문에서 사용될 수도 있습니다. 이 경우 <xref:System.Windows.ThemeDictionaryExtension.AssemblyName%2A> 속성의 값을 지정 해야 합니다.  
  
 `ThemeDictionary` 속성을 다음과 같이 속성=값 쌍으로 지정하는 자세한 특성 사용 구문에도 <xref:System.Windows.Markup.StaticExtension.Member%2A>을 사용할 수 있습니다.  
  
```xml  
<object property="{ThemeDictionary AssemblyName=assemblyUri}" .../>  
```  
  
 자세한 정보 표시는 대개 설정 가능한 속성이 둘 이상이거나 일부 속성이 선택 사항인 확장의 경우에 유용합니다. `ThemeDictionary`에는 설정 가능한 속성이 하나뿐이고 이 속성은 필수적 속성이므로 자세한 정보 표시를 사용하지 않는 것이 일반적입니다.  
  
 프로세서 구현에서이 태그 <xref:System.Windows.ThemeDictionaryExtension> 확장에 대 한 처리는 클래스에 의해 정의 됩니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]  
  
 `ThemeDictionary`은 태그 확장입니다. 태그 확장은 특성 값을 리터럴 값 또는 처리기 이름이 아닌 다른 값이 되도록 이스케이프해야 하는 요구 사항이 있는 경우 일반적으로 구현되며 이러한 요구 사항은 특정 형식 또는 속성에 형식 변환기를 배치하는 것보다 더 포괄적입니다. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]의 모든 태그 확장은 특성 구문에서 { 및 } 문자를 사용합니다. 이러한 문자는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 프로세서가 태그 확장이 특성을 처리해야 함을 인식하는 데 사용되는 규칙입니다. 자세한 내용은 [태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [스타일 지정 및 템플릿](../controls/styling-and-templating.md)
- [XAML 개요(WPF)](xaml-overview-wpf.md)
- [태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)
- [WPF 응용 프로그램 리소스, 콘텐츠 및 데이터 파일](../app-development/wpf-application-resource-content-and-data-files.md)
