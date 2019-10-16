---
title: XAML의 제네릭
ms.date: 03/30/2017
helpviewer_keywords:
- generics [XAML Services]
ms.assetid: 835bfed7-585c-4216-ae67-b674edab8b92
ms.openlocfilehash: 6ca7986513d1a6cbe160ca1a0af6699c323aac7e
ms.sourcegitcommit: d8ebe0ee198f5d38387a80ba50f395386779334f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66690646"
---
# <a name="generics-in-xaml"></a>XAML의 제네릭
System.Xaml에서 구현 될 때.NET Framework XAML 서비스 일반 CLR 형식을 사용 하 여에 대 한 지원을 제공 합니다. 이 지원은 포함 형식 인수로 제네릭의 제약 조건을 지정 하 고 적절 한 호출 하 여 제약 조건을 적용 `Add` 제네릭 컬렉션의 경우에 대 한 메서드. 이 항목에서는 사용 하 고 XAML의 제네릭 형식 참조의 측면을 설명 합니다.  
  
## <a name="xtypearguments"></a>x:TypeArguments  
 `x:TypeArguments` 지시문은 XAML 언어에서 정의 됩니다. 제네릭 형식에서 지 원하는 XAML 형식의 멤버로 사용할 `x:TypeArguments` 제한 전달 백업 생성자에 제네릭 인수를 입력 합니다. .NET Framework XAML 서비스에 관련 된 참조 구문이 사용 `x:TypeArguments`구문 예제를 포함 하는, 참조 [X:typearguments Directive](x-typearguments-directive.md)합니다.  
  
 때문에 `x:TypeArguments` 문자열을 사용 및 형식 변환기 백업의 경우에 일반적으로 특성으로 XAML 사용에 선언 된 것입니다.  
  
 XAML 노드 스트림의 정보를 선언 하 여 `x:TypeArguments` 에서 가져올 수 있습니다 <xref:System.Xaml.XamlType.TypeArguments%2A?displayProperty=nameWithType> 에 `StartObject` 노드 스트림 내의 위치입니다. 반환 값 <xref:System.Xaml.XamlType.TypeArguments%2A?displayProperty=nameWithType> 목록은 <xref:System.Xaml.XamlType> 값입니다. XAML 형식을 제네릭 형식을 나타내는지 여부를 결정을 호출 하 여 가능 <xref:System.Xaml.XamlType.IsGeneric%2A?displayProperty=nameWithType>합니다.  
  
## <a name="rules-and-syntax-conventions-for-generics-in-xaml"></a>규칙 및 XAML의 제네릭에 대 한 구문 표기 규칙  
 XAML을에서 제네릭 형식은 항상 표시 되어야 합니다 제약 조건이 지정 된 제네릭; 제네릭은은 XAML 노드 스트림의 XAML 형식 시스템에 있는 되지 및 XAML 태그에 나타낼 수 없습니다. 제네릭 중첩된 형식 제약 조건에서 참조 하 고 일반 하는 경우에 대 한 XAML 특성 구문 내에서 참조할 수 있습니다 `x:TypeArguments`, 또는 경우에는 `x:Type` 제네릭 형식에 대 한 CLR 형식 참조를 제공 합니다. 이 통해 지원 되는 <xref:System.Xaml.Schema.XamlTypeTypeConverter> .NET Framework XAML 서비스에 정의 된 클래스입니다.  
  
 XAML 특성으로 사용 하도록 설정 하는 구문 형식 <xref:System.Xaml.Schema.XamlTypeTypeConverter> 일반적인 MSIL 변경 각도 사용 하는 CLR 구문 규칙 형식 및 제네릭, 제약 조건에 대 한 괄호와 제약 조건 컨테이너에 대 한 괄호를 대신 합니다. 예를 들어 참조 [X:typearguments Directive](x-typearguments-directive.md)합니다.  
  
## <a name="generics-and-xaml-2009-features"></a>제네릭 및 XAML 2009 기능  
 XAML 2009를 사용 하는 경우 CLR 대신 기본 공용 언어 기본 형식에 대 한 XAML 형식을 가져올 형식, 사용할 수 있습니다 [기본 제공 형식 XAML 2009](built-in-types-for-common-xaml-language-primitives.md) 의 정보 항목으로 `x:TypeArguments`입니다. 예를 들어, 다음에 선언할 수 있습니다 (접두사 매핑이 표시 되지 않지만 `x` XAML 2009에 대 한 XAML 언어 XAML 네임 스페이스):  
  
```xaml  
<my:BusinessObject x:TypeArguments="x:String,x:Int32"/>  
```  
  
## <a name="generics-support-in-wpf-and-other-v35-frameworks"></a>WPF 및 다른 v3.5 프레임 워크에서 제네릭 지원  
 구체적으로 WPF를 대상으로 할 때 XAML 2006 사용량에 대 한 [X:class](x-class-directive.md) 와 동일한 요소에도 제공 해야 `x:TypeArguments`, 해당 요소는 XAML 문서의 루트 요소 여야 합니다. 루트 요소는 하나 이상의 형식 인수가 있는 제네릭 형식에 매핑되어야 합니다. 예제입니다. <xref:System.Windows.Navigation.PageFunction%601>  
  
 제네릭 사용을 지원 하기 위해 가능한 해결 방법이 포함 제네릭 형식을 반환할 수 있는 사용자 지정 태그 확장을 정의 하거나 래핑 제공 클래스는 제네릭 형식에서 파생 되지만 평면화는 자체 클래스 정의에서 제네릭 제약 조건을 정의 합니다.  
  
 WPF 및.NET Framework 4를 대상으로 하에서 함께 XAML 2009 기능을 사용할 수 있습니다 `x:TypeArguments`, 느슨한 XAML (태그 컴파일되지 않은 XAML)에 대해서만 합니다. WPF에 대한 태그로 컴파일된 XAML 및 BAML 형식의 XAML은 현재 XAML 2009 키워드 및 기능을 지원하지 않습니다.  
  
 .NET Framework 3.5 용 Windows Workflow Foundation에서 사용자 지정 워크플로 일반 XAML 사용을 지원 하지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [x:TypeArguments 지시문](x-typearguments-directive.md)
- [x:Class 지시문](x-class-directive.md)
- [공용 XAML 언어 기본 형식에 대한 기본 제공 형식](built-in-types-for-common-xaml-language-primitives.md)
