---
title: x:Static 태그 확장
ms.date: 03/30/2017
f1_keywords:
- StaticExtension
- xStatic
- x:Static
helpviewer_keywords:
- x:Static markup extension [XAML Services]
- Static markup extension in XAML [XAML Services]
- XAML [XAML Services], x:Static markup extension
ms.assetid: 056aee79-7cdd-434f-8174-dfc856cad343
ms.openlocfilehash: 9fa9e51e66af6df4d1a6b1ec94c5010651bbb21d
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68401507"
---
# <a name="xstatic-markup-extension"></a>x:Static 태그 확장
CLS (공용 언어 사양) 규격 방식으로 정의 된 모든 정적 값으로 된 코드 엔터티를 참조 합니다. 참조 되는 정적 속성은 XAML에서 속성의 값을 제공 하는 데 사용할 수 있습니다.  
  
## <a name="xaml-attribute-usage"></a>XAML 특성 사용  
  
```xaml  
<object property="{x:Static prefix:typeName.staticMemberName}" .../>  
```  
  
## <a name="xaml-values"></a>XAML 값  
  
| | |  
|-|-|  
|`prefix`|선택 사항입니다. 기본이 아닌 매핑된 XAML 네임 스페이스를 참조 하는 접두사입니다. `prefix`은 기본 XAML 네임 스페이스에서 제공 되는 정적 속성을 거의 참조 하지 않으므로 사용 시 명시적으로 표시 됩니다. 설명 부분을 참조하세요.|  
|`typeName`|필수 요소. 원하는 정적 멤버를 정의 하는 형식의 이름입니다.|  
|`staticMemberName`|필수 요소. 원하는 정적 값 멤버의 이름 (상수, 정적 속성, 필드 또는 열거형 값)입니다.|  
  
## <a name="remarks"></a>설명  

참조 되는 코드 엔터티는 다음 중 하나 여야 합니다.  
  
- 상수  
- 정적 속성  
- 필드  
- 열거형 값

비정적 속성과 같은 다른 코드 엔터티를 지정 하면 XAML이 태그 컴파일 인 경우 컴파일 시간 오류가 발생 하거나 XAML 로드 시간 구문 분석 예외가 발생 합니다.  

현재 xaml 문서 `x:Static` 에 대 한 기본 xaml 네임 스페이스에 없는 정적 필드 또는 속성에 대 한 참조를 만들 수 있지만이를 위해서는 접두사 매핑이 필요 합니다. Xaml 네임 스페이스는 거의 항상 XAML 문서의 루트 요소에 정의 되어 있습니다.  

기본 XAML 스키마 컨텍스트를 사용 하 여 실행 되는 경우 XAML 서비스 및 xaml 판독기와 XAML 작성기를 .NET Framework 하 여 정적 속성에 대 한 조회 작업을 수행할 수 있습니다. 이 XAML 스키마 컨텍스트는 CLR 리플렉션을 사용 하 여 개체 그래프 생성에 필요한 정적 값을 제공할 수 있습니다. 사용자 `typeName` 가 지정 하는는 실제로는 기본 xaml 스키마 컨텍스트를 사용할 때 또는 기존의 모든 clr 기반 xaml 구현 프레임 워크를 사용 하는 경우 동일한 이름 이지만 clr 형식 이름이 아니라 XAML 형식 이름입니다.  

속성 값의 형식이 아닌 `x:Static` 참조를 사용 하는 경우 주의 해야 합니다. XAML 처리 시퀀스에서 태그 확장의 제공 된 값은 추가 값 변환을 호출 하지 않습니다. 이는 `x:Static` 참조가 텍스트 문자열을 만드는 경우에도 마찬가지 이며 텍스트 문자열을 기반으로 하는 특성 값에 대 한 값 변환은 일반적으로 해당 특정 멤버나 반환 형식의 멤버 값에 대해 발생 합니다.  

특성 구문은 이러한 태그 확장에 가장 많이 사용되는 구문입니다. `x:Static` 식별자 문자열 다음에 나오는 문자열 토큰은 기본 <xref:System.Windows.Markup.StaticExtension.Member%2A> 확장 클래스의 <xref:System.Windows.Markup.StaticExtension> 값으로 할당됩니다.  

기술적으로 가능한 두 가지 XAML 사용이 있습니다. 그러나 이러한 사용은 불필요 하 게 자세한 정보를 표시 하기 때문에 더 일반적이 지 않습니다.  

1. 개체 요소 구문입니다.

    ```xaml
    <x:Static Member="prefix:typeName.staticMemberName" ... />
    ```

2. 초기화 문자열의 명시적 멤버 속성이 포함 된 특성 구문입니다.

    ```xaml
    <object property="{x:Static Member=prefix:typeName.staticMemberName}" ... />
    ```

.NET Framework XAML 서비스 구현에서이 태그 확장에 대 한 처리는 <xref:System.Windows.Markup.StaticExtension> 클래스에 의해 정의 됩니다.  

`x:Static`은 태그 확장입니다. Xaml의 모든 태그 확장은 특성 `{` 구문 `}` 에서 및 문자를 사용 합니다 .이는 xaml 프로세서가 태그 확장에서 값을 제공 해야 함을 인식 하는 데 사용 되는 규칙입니다. 태그 확장에 대한 자세한 내용은 [Markup Extensions for XAML Overview](markup-extensions-for-xaml-overview.md)를 참조하세요.  
  
## <a name="wpf-usage-notes"></a>WPF 사용 정보  
 WPF 프로그래밍에 사용 하는 기본 XAML 네임 스페이스에는 많은 유용한 정적 속성이 포함 되어 있지 않으며, 대부분의 유용한 정적 속성에는를 요구 `{x:Static}` 하지 않고 사용을 용이 하 게 하는 형식 변환기와 같은 지원이 있습니다. 정적 속성의 경우 다음 조건 중 하나에 해당 하는 경우에는 XAML 네임 스페이스에 대 한 접두사를 매핑해야 합니다.  
  
- WPF에 존재 하지만 WPF에 대 한 기본 XAML 네임 스페이스의 일부가 아닌 형식을 참조 하는 경우 ([!INCLUDE[TLA#tla_wpfxmlnsv1](../../../includes/tlasharptla-wpfxmlnsv1-md.md)]) 이는를 사용 하 `x:Static`는 매우 일반적인 시나리오입니다. 예를 들어 `x:Static` <xref:System.Environment> 클래스의 정적 속성을 참조 하기 위해 <xref:System> CLR 네임 스페이스 및 mscorlib 어셈블리에 대 한 XAML 네임 스페이스 매핑과 함께 참조를 사용할 수 있습니다.  
  
- 사용자 지정 어셈블리에서 형식을 참조 합니다.  
  
- WPF 어셈블리에 존재 하는 형식을 참조 하지만 해당 형식이 WPF 기본 XAML 네임 스페이스의 일부가 아닌 CLR 네임 스페이스 내에 있습니다. WPF의 기본 XAML 네임 스페이스에 대 한 CLR 네임 스페이스의 매핑은 다양 한 WPF 어셈블리의 정의에 의해 수행 됩니다 .이 개념에 대 한 자세한 내용은 [WPF xaml을 위한 Xaml 네임 스페이스 및 네임 스페이스 매핑](../wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)을 참조 하세요. 매핑되지 않은 CLR 네임 스페이스는 대개와 같이 일반적으로 XAML을 사용 하지 않는 대부분의 클래스 정의로 <xref:System.Windows.Threading>구성 되어 있는 경우에만 존재할 수 있습니다.  
  
 WPF에 접두사 및 XAML 네임 스페이스를 사용 하는 방법에 대 한 자세한 내용은 [WPF xaml을 위한 Xaml 네임 스페이스 및 네임 스페이스 매핑](../wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [x:Type 태그 확장](x-type-markup-extension.md)
- [WPF에서 System.Xaml로 마이그레이션된 형식](types-migrated-from-wpf-to-system-xaml.md)
