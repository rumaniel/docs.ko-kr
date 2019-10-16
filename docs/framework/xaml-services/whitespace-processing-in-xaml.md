---
title: XAML의 공백 처리
ms.date: 03/30/2017
helpviewer_keywords:
- East Asian characters [XAML Services]
- XAML [XAML Services], white-space processing
- white-space processing in XAML [XAML Services]
- characters [XAML Services], East Asian
ms.assetid: cc9cc377-7544-4fd0-b65b-117b90bb0b23
ms.openlocfilehash: 077f19690d204d3b8f682d01c51feee9e9edbfd4
ms.sourcegitcommit: bbfcc913c275885381820be28f61efcf8e83eecc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68796817"
---
# <a name="white-space-processing-in-xaml"></a>XAML의 공백 처리
XAML에 대 한 언어 규칙에서는 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 프로세서 구현에 따라 유효 공백을 처리 해야 합니다. 이 항목에서는 이들 XAML 언어 규칙에 대해 설명합니다. 또한 serialization을 위해 xaml 프로세서 및 xaml 작성기의 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] 구현에서 정의 된 추가 공백 처리를 문서화 합니다.  
  
<a name="whitespace_definition"></a>   
## <a name="white-space-definition"></a>공백 정의  
 와 [!INCLUDE[TLA2#tla_xml](../../../includes/tla2sharptla-xml-md.md)]일치 하는의 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 공백 문자는 공백, 줄 바꿈 및 탭입니다. 이들 문자는 각각 [!INCLUDE[TLA#tla_unicode](../../../includes/tlasharptla-unicode-md.md)] 값 0020, 000A 및 0009에 해당합니다.  
  
<a name="whitespace_normalization"></a>   
## <a name="white-space-normalization"></a>공백 정규화  
 기본적으로 다음 공백 정규화는 프로세서에서 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 파일을 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 처리할 때 발생 합니다.  
  
1. 동아시아 문자 사이에서 줄 바꿈 문자가 제거됩니다. 이 용어의 정의에 대해서는 이 항목의 뒷부분에서 "동아시아 문자" 섹션을 참조하세요.  
  
2. 모든 공백 문자 (공백, 줄 바꿈, 탭)는 공백으로 변환 됩니다.  
  
3. 모든 연속 공백은 삭제되고 공백 하나로 대체됩니다.  
  
4. 시작 태그 바로 뒤의 공백은 삭제됩니다.  
  
5. 종료 태그 바로 앞의 공백은 삭제됩니다.  
  
 "기본값"은 [xml:space](xml-space-handling-in-xaml.md) 특성의 기본값으로 나타내는 상태에 해당합니다.  
  
<a name="whitespace_in_inner_text_and_string_primitives"></a>   
## <a name="white-space-in-inner-text-and-string-primitives"></a>내부 텍스트 및 문자열 기본 형식의 공백  
 이전 정규화 규칙은 XAML 요소 내에 있는 내부 텍스트에 적용됩니다. 정규화 후에 다음과 같이 XAML 프로세서에서는 모든 내부 텍스트를 적절한 형식으로 변환합니다.  
  
- 속성 형식이 컬렉션이 아니지만 직접 <xref:System.Object> 형식이 아니면 XAML 프로세서에서는 형식 변환기를 사용하여 해당 형식으로 변환하려고 합니다. 여기서 변환에 실패하면 컴파일 시간 오류가 발생합니다.  
  
- 속성 형식이 컬렉션이고 내부 텍스트가 연속(중간 요소 태그 없음)이면 내부 텍스트가 단일 <xref:System.String>으로 구문 분석됩니다. 컬렉션 형식이 <xref:System.String>을 허용할 수 없으면 이로 인해 컴파일 시간 오류가 발생합니다.  
  
- 속성 형식이 <xref:System.Object>이면 내부 텍스트가 단일 <xref:System.String>으로 구문 분석됩니다. <xref:System.Object> 형식이 단일 개체(<xref:System.String> 등)를 의미하기 때문에, 중간 요소 태그가 있으면 이로 인해 컴파일 시간 오류가 발생합니다.  
  
- 속성 형식이 컬렉션이고 내부 텍스트가 연속이 아니면 첫 번째 하위 문자열이 <xref:System.String> 으로 변환되고 컬렉션 항목으로 추가되고, 중간 요소가 컬렉션 항목으로 추가되고, 마지막으로 후행 하위 문자열(있는 경우)이 컬렉션에 세 번째 <xref:System.String> 항목으로 추가됩니다.  
  
<a name="preserving_whitespace"></a>   
## <a name="preserving-white-space"></a>공백 유지  
 최종 프레젠테이션을 위해 원본 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 에서 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 프로세서의 공백 정규화의 영향을 받지 않는 공간을 유지 하는 여러 가지 기술이 있습니다.  
  
 **xml:space="preserve"** : 공백 유지를 원하는 요소 수준에서이 특성을 지정 합니다. 이를 사용하면 코드 편집 애플리케이션에 의해 "pretty-print" 맞춤 요소에 시각적으로 바로 확인되는 중첩으로 추가될 수 있는 공백이 포함된 모든 공백이 유지됩니다. 그러나 해당 공백의 렌더링 여부는 포함하는 요소의 콘텐츠 모델에서 결정됩니다. 특성을 `xml:space="preserve"` 설정 하는 방법에 관계 없이 대부분의 개체 모델에서는 공백을 중요 한 것으로 간주 하지 않으므로 루트 수준에서를 지정 하지 마십시오. `xml:space` 를 전역으로 설정하면 일부 구현에서는 XAML 처리(특히 serialization) 성능에 영향을 미칠 수 있습니다. 문자열 내에서 공백을 렌더링 하는 요소 수준에서 구체적으로 특성을 설정 하거나 공백으로 중요 한 컬렉션을 설정 하는 것이 더 좋습니다.  
  
 **엔터티 및 줄 바꿈하지 않는 공백**: [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 에서는 텍스트 개체 모델 내에 [!INCLUDE[TLA#tla_unicode](../../../includes/tlasharptla-unicode-md.md)] 엔터티를 배치하도록 지원합니다. 줄 바꿈하지 않는 공간 (&\#160; utf-8 인코딩) 등의 전용 엔터티를 사용할 수 있습니다. 줄 바꿈하지 않는 공백 문자를 지원하는 서식 있는 텍스트 컨트롤을 사용할 수도 있습니다. 엔터티를 사용하여 들여쓰기 등의 레이아웃 특성을 시뮬레이트하는 경우 주의해야 합니다. 이는 엔터티의 런타임 출력은 패널 및 여백의 적절한 사용과 같은 일반적인 레이아웃 시스템에서 들여쓰기 결과를 생성하는 기능보다 더 많은 요소에 따라 달라지기 때문입니다. 예를 들어 엔터티는 글꼴에 매핑되고 사용자 글꼴 선택에 따라 크기가 변경될 수 있습니다.  
  
<a name="east_asian_characters"></a>   
## <a name="east-asian-characters"></a>동아시아 문자  
 "동아시아 문자"는 [!INCLUDE[TLA2#tla_unicode](../../../includes/tla2sharptla-unicode-md.md)] 문자 범위 U+20000~U+2FFFD 및 U+30000~U+3FFFD의 집합으로 정의됩니다. 이 하위 집합을 "한중일 한자"라고도 합니다. 자세한 내용은 <https://www.unicode.org>을 참조하세요.  
  
<a name="whitespace_and_text_content_models"></a>   
## <a name="white-space-and-text-content-models"></a>공백 및 텍스트 콘텐츠 모델  
 실제로 공백 유지는 모든 가능한 콘텐츠 모델의 하위 집합에만 중요 합니다. 해당 하위 집합은 몇몇 형식의 singleton <xref:System.String> 형식 또는 전용 <xref:System.String> 컬렉션을 사용하거나 <xref:System.String> 과 <xref:System.Collections.IList> 또는 <xref:System.Collections.Generic.ICollection%601> 컬렉션의 기타 형식을 혼합해서 사용할 수 있는 콘텐츠 모델로 구성됩니다.  
  
### <a name="white-space-and-text-content-models-in-wpf"></a>WPF의 공백 및 텍스트 콘텐츠 모델  
 설명하기 위해 이 섹션의 나머지 부분에서는 WPF에서 정의된 특정 형식을 참조합니다. 이 항목에 설명 된 공백 처리 기능은 일반적으로 .NET Framework XAML 서비스 및 WPF 모두와 관련이 있습니다. 작동 중인 동작을 확인하기 위해 일부 WPF XAML 태그를 실험하고, 개체 그래프에서 결과를 확인하고, 다시 태그로 serialize할 수 있습니다.  
  
 문자열을 사용할 수 있는 콘텐츠 모델의 경우에도 이러한 콘텐츠 모델 내의 기본 동작은 남아 있는 공백이 중요 한 것으로 처리 되지 않도록 하는 것입니다. 예 <xref:System.Windows.Controls.ListBox> 를 들어는 <xref:System.Collections.IList>를 사용 하지만 공백 (예: 각 <xref:System.Windows.Controls.ListBoxItem>사이의 줄 바꿈)은 유지 되지 않고 렌더링 되지 않습니다. <xref:System.Windows.Controls.ListBoxItem> 항목에 대한 문자열 사이에서 줄 바꿈을 구분 기호로 사용하려는 시도가 전혀 작동하지 않으면 줄 바꿈으로 구분된 문자열은 단일 문자열 및 단일 항목으로 처리됩니다.  
  
 공백을 중요 한 것으로 간주 하는 이러한 컬렉션은 일반적으로 유동 문서 모델의 일부입니다. 공백 유지 동작을 지 원하는 기본 컬렉션은 <xref:System.Windows.Documents.InlineCollection>입니다. 이 컬렉션 클래스는로 <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>선언 됩니다 .이 특성이 있으면 프로세서는 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 컬렉션 내의 공백을 중요 한 것으로 처리 합니다. 표시 되는 `xml:space="preserve"` 컬렉션 <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute> 내에서와 공백의 조합은 모든 공백이 유지 되 고 렌더링 됨을 의미 합니다. 내에서 와공백을`xml:space="default"` 조합 하면 앞에서 설명한 초기 공백 정규화가 수행 되어 특정 위치에 하나의 공백이 남게 되 고 해당 공백은 유지 되 고 렌더링 됩니다. <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute> 적합한 동작은 직접 결정할 수 있고 원하는 동작을 사용하려면 선택적으로 `xml:space` 를 사용해야 합니다.  
  
 또한 유동 문서 모델에서 linebreak을 바꿈을 함축 하는 특정 인라인 요소는 공백으로 중요 한 컬렉션 에서도 불필요 한 공간을 제공 해야 합니다. 예를 들어, <xref:System.Windows.Documents.LineBreak> 요소는 HTML의 \<BR/> 태그와 동일한 용도를 가지 며, 태그의 가독성을 높이기 위해 일반적 <xref:System.Windows.Documents.LineBreak> 으로는 작성 된 줄 바꿈에 의해 후속 텍스트와 구분 됩니다. 후속 줄의 선행 공백이 될 수 있으므로 줄 바꿈을 정규화하면 안 됩니다. 해당 동작을 사용 하도록 <xref:System.Windows.Documents.LineBreak> 설정 하기 위해 요소에 대 한 클래스 정의는를 <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute>적용 하며, [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 이는 프로세서에서이를 해석 하 <xref:System.Windows.Documents.LineBreak> 여 주변의 공백이 항상 트리밍 됨을 의미 합니다.  
  
## <a name="see-also"></a>참고자료

- [XAML 개요(WPF)](../wpf/advanced/xaml-overview-wpf.md)
- [XML 문자 엔터티 및 XAML](xml-character-entities-and-xaml.md)
- [xml: XAML의 공간 처리](xml-space-handling-in-xaml.md)
