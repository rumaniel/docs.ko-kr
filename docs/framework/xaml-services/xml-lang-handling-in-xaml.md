---
title: XAML의 xml:lang 처리
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], xml:lang attribute
- xml:lang attribute [XAML Services]
- RFC 3066 standard [XAML Services]
- standards [XAML Services], RFC 3066
ms.assetid: 7aac0078-a1c5-41f8-b8b0-975510d9dca0
ms.openlocfilehash: 6495e980beea8731c47a774589919f160b4551ca
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62053602"
---
# <a name="xmllang-handling-in-xaml"></a>XAML의 xml:lang 처리
`xml:lang` 특성은 요소에 대해 언어 및 문화권 정보를 XML 형식으로 선언하는 [!INCLUDE[TLA2#tla_xml](../../../includes/tla2sharptla-xml-md.md)]에서 정의된 특성입니다. XAML을 사용해도 특성의 의미가 동일하게 유지되지만, 일부 추가적인 고려 사항이 적용됩니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xaml  
<object xml:lang="rfc3066lang" />  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
|||  
|-|-|  
|*rfc3066lang*|[RFC 3066](https://go.microsoft.com/fwlink/?LinkId=132454) 표준에서 파생되고 언어 또는 언어 영역을 식별하는 문자열입니다. 후자의 경우, 언어 및 지역이 단일 하이픈으로 구분됩니다. 값 및 형식에 대한 자세한 내용은 <xref:System.Windows.Markup.XmlLanguage> 를 참조하세요.|  
  
## <a name="remarks"></a>설명  
 `xml:lang` 에서 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 특성에 대한 정의는 `xml:lang` 에 대해 [!INCLUDE[TLA#tla_w3c](../../../includes/tlasharptla-w3c-md.md)] 가 “특수 특성"으로 정의한 대로 [!INCLUDE[TLA2#tla_xml](../../../includes/tla2sharptla-xml-md.md)]에서 파생됩니다. 언어 및 문화권 정보는 구현에 따라 요소에서 다양한 방법으로 처리될 수 있습니다. 하지만 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 특성의 기본 `xml:lang` 처리는 없습니다.  
  
 `xml:lang` 특성의 기본값은 이 특성 수준의 빈 문자열입니다.  
  
 `xml:lang` 특성 효과 및 특성의 값은 일반적으로 `xml:lang` 값에 영향을 주는 시스템에서 해석될 때 자식 요소에 지속됩니다.  
  
 .NET Framework XAML 서비스의 XAML 작성기로 해석되면 `xml:lang` 값은 <xref:System.Windows.Markup.XmlLanguage> 또는 <xref:System.Globalization.CultureInfo> 개체를 기본 개체 표현으로 생성할 수 있습니다. 하지만 이 동작은 `xml:lang` 에 지정된 값이 이러한 클래스에 대해 유효한 생성인지에 따라 다릅니다.  
  
 프레임워크는 `xml:lang` 를 속성에 적용하여 프레임워크에서 정의된 속성과 <xref:System.Windows.Markup.XmlLangPropertyAttribute> 의 의미 사이에 연결을 XML 형식으로 만들 수 있습니다.  
  
## <a name="wpf-usage-nodes"></a>WPF 사용 노드  
 <xref:System.Windows.FrameworkElement> 또는 <xref:System.Windows.FrameworkContentElement>의 파생 클래스인 요소의 경우, <xref:System.Windows.FrameworkElement.Language%2A> 특성의 해당되는 `xml:lang` 종속성 속성을 사용할 수 있습니다. 기본적으로, <xref:System.Windows.FrameworkElement.Language%2A> 속성은 이 속성 또는 `xml:lang` 특성 처리를 통해 달리 설정되지 않은 경우 "en-US"를 사용합니다.  
  
## <a name="see-also"></a>참고자료

- [WPF의 전역화](../wpf/advanced/globalization-for-wpf.md)
