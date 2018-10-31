---
title: 공백에서 XAML 처리
ms.date: 03/30/2017
helpviewer_keywords:
- East Asian characters [XAML Services]
- XAML [XAML Services], white-space processing
- white-space processing in XAML [XAML Services]
- characters [XAML Services], East Asian
ms.assetid: cc9cc377-7544-4fd0-b65b-117b90bb0b23
ms.openlocfilehash: 3eea3d6c8a28ace0cc79cbfeb7eb3a7a52c9b8ab
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50205167"
---
# <a name="white-space-processing-in-xaml"></a>공백에서 XAML 처리
XAML에 대 한 언어 규칙에 따르면 해당 유효 공백에서 처리 되어야 합니다는 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 프로세서 구현 합니다. 이 항목에서는 이들 XAML 언어 규칙에 대해 설명합니다. 정의한 추가 공백 처리도 문서화 된 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] XAML 프로세서 및 serialization에 대 한 XAML 작성기 구현의 합니다.  
  
<a name="whitespace_definition"></a>   
## <a name="white-space-definition"></a>공백 정의  
 부합 [!INCLUDE[TLA2#tla_xml](../../../includes/tla2sharptla-xml-md.md)]에 공백 문자가 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 는 공백, 줄 바꿈 및 탭 합니다. 이들 문자는 각각 [!INCLUDE[TLA#tla_unicode](../../../includes/tlasharptla-unicode-md.md)] 값 0020, 000A 및 0009에 해당합니다.  
  
<a name="whitespace_normalization"></a>   
## <a name="white-space-normalization"></a>공백 정규화  
 기본적으로 다음 공백 정규화는 발생 경우를 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 프로세서 프로세스는 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 파일:  
  
1.  동아시아 문자 사이에서 줄 바꿈 문자가 제거됩니다. 이 용어의 정의에 대해서는 이 항목의 뒷부분에서 "동아시아 문자" 섹션을 참조하세요.  
  
2.  모든 공백 문자 (공백, 줄 바꿈, 탭) 공간으로 변환 됩니다.  
  
3.  모든 연속 공백은 삭제되고 공백 하나로 대체됩니다.  
  
4.  시작 태그 바로 뒤의 공백은 삭제됩니다.  
  
5.  종료 태그 바로 앞의 공백은 삭제됩니다.  
  
 "기본값"은 [xml:space](../../../docs/framework/xaml-services/xml-space-handling-in-xaml.md) 특성의 기본값으로 나타내는 상태에 해당합니다.  
  
<a name="whitespace_in_inner_text_and_string_primitives"></a>   
## <a name="white-space-in-inner-text-and-string-primitives"></a>내부 텍스트 및 문자열 기본 형식의 공백  
 이전 정규화 규칙은 XAML 요소 내에 있는 내부 텍스트에 적용됩니다. 정규화 후에 다음과 같이 XAML 프로세서에서는 모든 내부 텍스트를 적절한 형식으로 변환합니다.  
  
-   속성 형식이 컬렉션이 아니지만 직접 <xref:System.Object> 형식이 아니면 XAML 프로세서에서는 형식 변환기를 사용하여 해당 형식으로 변환하려고 합니다. 여기서 변환에 실패하면 컴파일 시간 오류가 발생합니다.  
  
-   속성 형식이 컬렉션이고 내부 텍스트가 연속(중간 요소 태그 없음)이면 내부 텍스트가 단일 <xref:System.String>으로 구문 분석됩니다. 컬렉션 형식이 <xref:System.String>을 허용할 수 없으면 이로 인해 컴파일 시간 오류가 발생합니다.  
  
-   속성 형식이 <xref:System.Object>이면 내부 텍스트가 단일 <xref:System.String>으로 구문 분석됩니다. <xref:System.Object> 형식이 단일 개체(<xref:System.String> 등)를 의미하기 때문에, 중간 요소 태그가 있으면 이로 인해 컴파일 시간 오류가 발생합니다.  
  
-   속성 형식이 컬렉션이고 내부 텍스트가 연속이 아니면 첫 번째 하위 문자열이 <xref:System.String> 으로 변환되고 컬렉션 항목으로 추가되고, 중간 요소가 컬렉션 항목으로 추가되고, 마지막으로 후행 하위 문자열(있는 경우)이 컬렉션에 세 번째 <xref:System.String> 항목으로 추가됩니다.  
  
<a name="preserving_whitespace"></a>   
## <a name="preserving-white-space"></a>공백을 유지  
 원본에 대 한 공백을 유지 하는 것에 대 한 몇 가지 기술이 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 영향을 받지 않는 최종 표시를 위해 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 프로세서 공백 정규화 합니다.  
  
 **xml: space = "preserve"**: 공백 유지는 원할 경우 요소 수준에서이 특성을 지정 합니다. 이를 사용하면 코드 편집 응용 프로그램에 의해 "pretty-print" 맞춤 요소에 시각적으로 바로 확인되는 중첩으로 추가될 수 있는 공백이 포함된 모든 공백이 유지됩니다. 그러나 해당 공백의 렌더링 여부는 포함하는 요소의 콘텐츠 모델에서 결정됩니다. 지정 하지 않으려면 `xml:space="preserve"` 루트 수준에서 대부분의 개체 모델을 흰색 간주 해서는 안 되므로 공간 특성을 설정 하는 방법에 관계 없이 중요 한 것 처럼 합니다. `xml:space` 를 전역으로 설정하면 일부 구현에서는 XAML 처리(특히 serialization) 성능에 영향을 미칠 수 있습니다. 것만 문자열 내의 공백을 렌더링 된 공백 의미 컬렉션인 요소의 수준 특성을 설정 하는 것이 좋습니다.  
  
 **엔터티 및 줄 바꿈하지 않는 공백**: [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 에서는 텍스트 개체 모델 내에 [!INCLUDE[TLA#tla_unicode](../../../includes/tlasharptla-unicode-md.md)] 엔터티를 배치하도록 지원합니다. 줄 바꿈하지 않는 공백 같은 전용된 엔터티를 사용할 수 있습니다 (&\#160에서 u t F-8 인코딩). 줄 바꿈하지 않는 공백 문자를 지원하는 서식 있는 텍스트 컨트롤을 사용할 수도 있습니다. 엔터티를 사용하여 들여쓰기 등의 레이아웃 특성을 시뮬레이트하는 경우 주의해야 합니다. 이는 엔터티의 런타임 출력은 패널 및 여백의 적절한 사용과 같은 일반적인 레이아웃 시스템에서 들여쓰기 결과를 생성하는 기능보다 더 많은 요소에 따라 달라지기 때문입니다. 예를 들어 엔터티는 글꼴에 매핑되고 사용자 글꼴 선택에 따라 크기가 변경될 수 있습니다.  
  
<a name="east_asian_characters"></a>   
## <a name="east-asian-characters"></a>동아시아 문자  
 "동아시아 문자"는 [!INCLUDE[TLA2#tla_unicode](../../../includes/tla2sharptla-unicode-md.md)] 문자 범위 U+20000~U+2FFFD 및 U+30000~U+3FFFD의 집합으로 정의됩니다. 이 하위 집합을 "한중일 한자"라고도 합니다. 자세한 내용은 <https://www.unicode.org>을 참조하세요.  
  
<a name="whitespace_and_text_content_models"></a>   
## <a name="white-space-and-text-content-models"></a>공백 및 텍스트 콘텐츠 모델  
 실제로 공백 유지는 모든 가능한 콘텐츠 모델의 하위 집합에만 합니다. 해당 하위 집합은 몇몇 형식의 singleton <xref:System.String> 형식 또는 전용 <xref:System.String> 컬렉션을 사용하거나 <xref:System.String> 과 <xref:System.Collections.IList> 또는 <xref:System.Collections.Generic.ICollection%601> 컬렉션의 기타 형식을 혼합해서 사용할 수 있는 콘텐츠 모델로 구성됩니다.  
  
### <a name="white-space-and-text-content-models-in-wpf"></a>WPF의 공백 및 텍스트 콘텐츠 모델  
 설명하기 위해 이 섹션의 나머지 부분에서는 WPF에서 정의된 특정 형식을 참조합니다. 이 항목에 설명 된 공백 처리 기능은 일반적으로.NET Framework XAML 서비스 및 WPF 모두에 관련 수 있습니다. 작동 중인 동작을 확인하기 위해 일부 WPF XAML 태그를 실험하고, 개체 그래프에서 결과를 확인하고, 다시 태그로 serialize할 수 있습니다.  
  
 있는 경우에 문자열을 사용할 수는 이러한 콘텐츠 모델 내에서 기본 동작 남아 있는 모든 공백은 중요 한 것 처럼 처리 되지 않습니다. 예를 들어 <xref:System.Windows.Controls.ListBox> 사용을 <xref:System.Collections.IList>, 하지만 공백을 (사이의 각 줄 바꿈과 같은 <xref:System.Windows.Controls.ListBoxItem>)은 유지 되지 않고 렌더링 되지 않습니다. <xref:System.Windows.Controls.ListBoxItem> 항목에 대한 문자열 사이에서 줄 바꿈을 구분 기호로 사용하려는 시도가 전혀 작동하지 않으면 줄 바꿈으로 구분된 문자열은 단일 문자열 및 단일 항목으로 처리됩니다.  
  
 이러한 컬렉션 공백을 의미로 처리 하는 일반적으로 흐름 문서 모델의 일부입니다. 공백 유지 동작을 지 원하는 기본 컬렉션은 <xref:System.Windows.Documents.InlineCollection>합니다. 사용이 컬렉션 클래스를 선언 합니다 <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>이 특성이 발견 되 면;는 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 프로세서에서는 컬렉션 내에 있는 공백을 의미로 처리 합니다. 조합 `xml:space="preserve"` 내 및 공백은 <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute> 컬렉션은 모든 공백이 유지 되 고 렌더링을 표시 합니다. 조합 `xml:space="default"` 내 및 공백은 <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute> 초기 공백 정규화는 앞에서 설명한 남게 되 특정 위치에 하나의 공백이 고 해당 공백은 유지 되 고 렌더링 합니다. 적합한 동작은 직접 결정할 수 있고 원하는 동작을 사용하려면 선택적으로 `xml:space` 를 사용해야 합니다.  
  
 또한 흐름 문서 모델에서 줄 바꿈을 함축 하는 특정 인라인 요소는 의도적으로 공백을 추가 공백이 중요 한 컬렉션에도 합니다. 예를 들어를 <xref:System.Windows.Documents.LineBreak> 요소에 동일한 목적으로는 \<b R / > 태그 [!INCLUDE[TLA2#tla_html](../../../includes/tla2sharptla-html-md.md)], 태그의 가독성을 높이기 위해 일반적으로 <xref:System.Windows.Documents.LineBreak> 작성 된 줄 바꿈으로 후속 텍스트와에서 구분 됩니다. 후속 줄의 선행 공백이 될 수 있으므로 줄 바꿈을 정규화하면 안 됩니다. 해당 동작에 대 한 클래스 정의 사용 하도록 설정 하려면를 <xref:System.Windows.Documents.LineBreak> 요소에 적용 되는 <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute>을 해석 하 고 있는 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 주변 공백 해당 의미에 대 한 프로세서 <xref:System.Windows.Documents.LineBreak> 항상 잘립니다.  
  
## <a name="see-also"></a>참고자료  
 [XAML 개요(WPF)](../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)  
 [XML 문자 엔터티 및 XAML](../../../docs/framework/xaml-services/xml-character-entities-and-xaml.md)  
 [XAML에서 처리 하는 xml: space](../../../docs/framework/xaml-services/xml-space-handling-in-xaml.md)
