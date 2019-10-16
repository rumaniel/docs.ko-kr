---
title: .NET Framework XAML 서비스에서 사용할 사용자 지정 형식 정의
ms.date: 03/30/2017
helpviewer_keywords:
- defining custom types [XAML Services]
ms.assetid: c2667cbd-2f46-4a7f-9dfc-53696e35e8e4
ms.openlocfilehash: e563c0d7e5113d55d4b942fb1d175a64f5b71abc
ms.sourcegitcommit: 30a83efb57c468da74e9e218de26cf88d3254597
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2019
ms.locfileid: "68364299"
---
# <a name="defining-custom-types-for-use-with-net-framework-xaml-services"></a>.NET Framework XAML 서비스에서 사용할 사용자 지정 형식 정의
비즈니스 개체 이거나 특정 프레임 워크에 대 한 종속성이 없는 형식인 사용자 지정 형식을 정의 하는 경우 XAML에 대 한 특정 모범 사례를 따를 수 있습니다. 이러한 연습 .NET Framework을 수행 하는 경우 XAML 서비스 및 xaml 판독기와 XAML 작성기는 사용자 형식의 XAML 특성을 검색 하 고 xaml 형식 시스템을 사용 하 여 XAML 노드 스트림에서 적절 한 표현을 제공할 수 있습니다. 이 항목에서는 형식 정의, 멤버 정의 및 형식 또는 멤버의 CLR 특성에 대 한 모범 사례를 설명 합니다.  
  
## <a name="constructor-patterns-and-type-definitions-for-xaml"></a>XAML에 대 한 생성자 패턴 및 형식 정의  
 XAML에서 개체 요소로 인스턴스화하려면 사용자 지정 클래스는 다음 요구 사항을 충족 해야 합니다.  
  
- 사용자 지정 클래스는 public 이어야 하며 매개 변수가 없는 기본 public 생성자를 노출 해야 합니다. 구조체에 대한 자세한 내용은 다음 섹션을 참조하세요.  
  
- 사용자 지정 클래스는 중첩 된 클래스가 아니어야 합니다. 전체 이름 경로에서 추가 "점"을 사용 하면 클래스 네임 스페이스 나누기가 모호해 집니다. 연결 된 속성과 같은 다른 XAML 기능을 방해 합니다.  
  
 개체를 개체 요소로 인스턴스화할 수 있는 경우 만들어진 개체는 개체를 내부 형식으로 사용 하는 속성의 속성 요소 형식을 채울 수 있습니다.  
  
 값 변환기를 사용 하는 경우 이러한 조건을 충족 하지 않는 형식에 대 한 개체 값을 계속 제공할 수 있습니다. 자세한 내용은 [Type Converters and Markup Extensions for XAML](type-converters-and-markup-extensions-for-xaml.md)합니다.  
  
### <a name="structures"></a>구조체  
 구조체는 항상 CLR 정의에 의해 XAML로 생성 될 수 있습니다. 이는 CLR 컴파일러가 구조체에 대해 매개 변수가 없는 생성자를 암시적으로 만들기 때문입니다. 이 생성자는 모든 속성 값을 기본값으로 초기화 합니다.  
  
 일부 경우에는 구조에 대 한 기본 생성 동작이 바람직하지 않습니다. 구조체는 값을 채우고 개념적으로 개념적으로 함수를 사용 하기 위한 것 이기 때문입니다. 공용 구조체로 포함 된 값에는 상호 배타적인 해석이 있을 수 있으므로 해당 속성을 설정할 수 없습니다. WPF 어휘의 <xref:System.Windows.GridLength>이러한 구조체의 예는입니다. 이러한 구조체는 구조체 값의 다른 해석 또는 모드를 만드는 문자열 규칙을 사용 하 여 값을 특성 형식으로 표현할 수 있도록 형식 변환기를 구현 해야 합니다. 또한 구조체는 매개 변수가 없는 생성자를 통해 코드 생성에 대해 비슷한 동작을 노출 해야 합니다.  
  
### <a name="interfaces"></a>인터페이스  
 인터페이스는 멤버의 기본 형식으로 사용할 수 있습니다. XAML 형식 시스템은 할당 가능한 목록을 검사 하 고 값으로 제공 된 개체를 인터페이스에 할당할 수 있어야 합니다. 관련 할당 가능한 형식이 XAML 생성 요구 사항을 지 원하는 경우 인터페이스를 XAML 형식으로 표시 하는 방법에 대 한 개념이 없습니다.  
  
### <a name="factory-methods"></a>팩터리 메서드  
 팩터리 메서드는 XAML 2009 기능입니다. 개체에 매개 변수가 없는 생성자가 있어야 하는 XAML 원칙을 수정 합니다. 팩터리 메서드는이 항목에서 설명 하지 않습니다. [X:FactoryMethod 지시문](x-factorymethod-directive.md)을 참조 하십시오.  
  
## <a name="enumerations"></a>열거형  
 열거형에는 XAML 네이티브 형식 변환 동작이 있습니다. XAML로 지정 된 열거형 상수 이름은 기본 열거형 형식에 대해 확인 되 고 열거형 값을 XAML 개체 작성기로 반환 합니다.  
  
 XAML은 적용 된 <xref:System.FlagsAttribute> 열거형의 플래그 스타일 사용을 지원 합니다. 자세한 내용은 [XAML 구문 정보](../wpf/advanced/xaml-syntax-in-detail.md)를 참조 하세요. [Xaml 구문](../wpf/advanced/xaml-syntax-in-detail.md) 에 대 한 자세한 내용은 WPF 대상에 맞게 작성 되었지만 해당 항목의 대부분의 정보는 특정 구현 프레임 워크와 관련이 없는 xaml과 관련이 있습니다.  
  
## <a name="member-definitions"></a>멤버 정의  
 형식은 XAML 사용에 대 한 멤버를 정의할 수 있습니다. 특정 형식이 XAML을 사용할 수 없는 경우에도 XAML을 사용할 수 있는 멤버를 정의 하는 형식에 대해 가능 합니다. 이는 CLR 상속 때문에 가능 합니다. 멤버를 상속 하는 일부 형식이 XAML 사용을 형식으로 지원 하 고 멤버가 내부 형식에 대 한 XAML 사용을 지원 하거나 네이티브 XAML 구문을 사용할 수 있는 경우 해당 멤버는 XAML을 사용할 수 있습니다.  
  
### <a name="properties"></a>속성  
 일반적인 clr `get` 및 `set` 접근자 패턴 및 언어에 적합 한 단어를 사용 하 여 속성을 공용 clr 속성으로 정의 하는 경우 XAML 형식 시스템은에 대해 제공 된 적절 한 정보를 사용 하 여 속성을 멤버로 보고할 수 있습니다. 속성 (예: <xref:System.Xaml.XamlMember.IsWritePublic%2A>및) <xref:System.Xaml.XamlMember.IsReadPublic%2A> <xref:System.Xaml.XamlMember>  
  
 특정 속성은를 적용 <xref:System.ComponentModel.TypeConverterAttribute>하 여 텍스트 구문을 사용 하도록 설정할 수 있습니다. 자세한 내용은 [Type Converters and Markup Extensions for XAML](type-converters-and-markup-extensions-for-xaml.md)합니다.  
  
 텍스트 구문이 나 네이티브 XAML 변환이 없고 태그 확장 사용과 같은 추가 간접 참조가 없으면 속성의 형식 (<xref:System.Xaml.XamlMember.TargetType%2A> xaml 형식 시스템)은 t를 처리 하 여 xaml 개체 작성기에 인스턴스를 반환할 수 있어야 합니다. arget 형식을 CLR 형식으로 입력 합니다.  
  
 XAML 2009를 사용 하는 경우 앞의 고려 사항이 충족 되지 않는 경우에는 [X:reference 태그 확장](x-reference-markup-extension.md) 을 사용 하 여 값을 제공할 수 있습니다. 그러나이는 형식 정의 문제 보다 더 많은 사용 문제가 있습니다.  
  
### <a name="events"></a>이벤트  
 이벤트를 공용 CLR 이벤트로 정의 하면 XAML 형식 시스템에서로 이벤트를 멤버로 <xref:System.Xaml.XamlMember.IsEvent%2A> `true`보고할 수 있습니다. 이벤트 처리기가 .NET Framework XAML 서비스 기능 범위 내에 없습니다. 이는 특정 프레임 워크 및 구현으로 유지 됩니다.  
  
### <a name="methods"></a>메서드  
 메서드에 대 한 인라인 코드는 기본 XAML 기능이 아닙니다. 대부분의 경우 XAML에서 메서드 멤버를 직접 참조 하지 않으며 XAML의 메서드 역할은 특정 XAML 패턴에 대 한 지원도 제공 합니다. [X:FactoryMethod 지시문](x-factorymethod-directive.md) 은 예외입니다.  
  
### <a name="fields"></a>필드  
 CLR 디자인 지침은 비정적 필드를 억제 합니다. 정적 필드의 경우 [X:Static 태그 확장](x-static-markup-extension.md)을 통해서만 정적 필드 값에 액세스할 수 있습니다. 이 경우 [x:Static](x-static-markup-extension.md) 사용에 대 한 필드를 노출 하기 위해 CLR 정의에서 특별 한 작업을 수행 하지 않습니다.  
  
## <a name="attachable-members"></a>연결 가능한 멤버  
 연결 가능한 멤버는 정의 형식에 대 한 접근자 메서드 패턴을 통해 XAML로 노출 됩니다. 정의 형식 자체는 개체로 XAML을 사용할 필요가 없습니다. 실제로 패턴은 연결할 수 있는 멤버를 소유 하 고 관련 된 동작을 구현 하는 역할을 하는 서비스 클래스를 선언 하는 것입니다. 그러나 UI 표현과 같은 다른 함수는 제공 하지 않습니다. 다음 섹션에서 자리 표시자 *PropertyName* 은 연결 가능한 멤버의 이름을 나타냅니다. 이 이름은 [XamlName 문법](xamlname-grammar.md)에서 유효 해야 합니다.  
  
 이러한 패턴과 형식의 다른 메서드 간 이름 충돌을 주의 해야 합니다. 패턴 중 하 나와 일치 하는 멤버가 있는 경우 의도 하지 않은 경우에도 XAML 프로세서에서 연결 가능한 멤버 사용 경로로 해석 될 수 있습니다.  
  
#### <a name="the-getpropertyname-accessor"></a>GetPropertyName 접근자  
 `Get`*PropertyName* 접근자에 대한 서명은 다음과 같아야 합니다.  
  
 `public static object Get`*PropertyName* `(object`  `target` `)`  
  
- 구현에서 보다 구체적인 형식으로 `target` 개체를 지정할 수 있습니다. 이를 사용 하 여 연결 가능한 멤버를 사용 하는 범위를 지정할 수 있습니다. 의도 된 범위를 벗어나는 사용량은 XAML 구문 분석 오류로 표시 되는 잘못 된 캐스팅 예외를 throw 합니다. 매개 변수 이름은 `target` 요구 사항이 아니지만 대부분의 구현에서 `target` 규칙에 따라 이름이 지정 됩니다.  
  
- 구현에서 보다 구체적인 형식으로 반환 값을 지정할 수 있습니다.  
  
 연결 가능한 멤버 <xref:System.ComponentModel.TypeConverter> 의 특성 사용에 대해 활성화 된 텍스트 구문을 지원 하려면 *PropertyName* 접근자에 `Get`을 적용 <xref:System.ComponentModel.TypeConverterAttribute> 합니다. `get` 대신`set` 에를 적용 하면 nonintuitive 보일 수 있습니다. 그러나이 규칙은 serialize 할 수 있는 읽기 전용 연결 가능 멤버의 개념을 지원할 수 있습니다 .이는 디자이너 시나리오에서 유용 합니다.  
  
#### <a name="the-setpropertyname-accessor"></a>SetPropertyName 접근자  
 Set*PropertyName* 접근자에 대 한 시그니처는 다음과 같아야 합니다.  
  
 `public static void Set` *PropertyName* `(object`  `target` `, object`  `value` `)`  
  
- 이전 `target` 섹션에서 설명한 것과 동일한 논리와 결과를 사용 하 여 구현에서 개체를 더 구체적인 형식으로 지정할 수 있습니다.  
  
- 구현에서 보다 구체적인 형식으로 `value` 개체를 지정할 수 있습니다.  
  
 이 메서드의 값은 일반적으로 특성 형식의 XAML 사용에서 들어오는 입력입니다. 특성 형식에서 텍스트 구문에 대 한 값 변환기를 지원 해야 하며 *PropertyName* 접근자에 대 한 `Get`특성을 설정 해야 합니다.  
  
### <a name="attachable-member-stores"></a>연결 가능한 멤버 저장소  
 일반적으로 접근자 메서드는 개체 그래프에 연결할 수 있는 멤버 값을 배치할 수단을 제공 하거나 개체 그래프에서 값을 검색 하 고 올바르게 serialize 할 수 있는 수단을 제공 하기에 충분 하지 않습니다. 이 기능을 제공 하기 위해 `target` 이전 접근자 시그니처의 개체는 값을 저장할 수 있어야 합니다. 연결 가능한 멤버가 멤버 목록에 없는 대상에 연결할 수 있는 연결 가능한 멤버와 저장소 메커니즘이 일치 해야 합니다. .NET Framework XAML 서비스는 api <xref:System.Xaml.IAttachedPropertyStore> 및 <xref:System.Xaml.AttachablePropertyServices>를 통해 연결 가능한 멤버 저장소에 대 한 구현 기술을 제공 합니다. <xref:System.Xaml.IAttachedPropertyStore>는 XAML 작성기에서 저장소 구현을 검색 하는 데 사용 되며 접근자 `target` 의 인 형식에 대해 구현 되어야 합니다. 정적 <xref:System.Xaml.AttachablePropertyServices> api는 접근자의 본문 내에서 사용 되며 <xref:System.Xaml.AttachableMemberIdentifier>에서 연결 가능한 멤버를 참조 합니다.  
  
## <a name="xaml-related-clr-attributes"></a>XAML 관련 CLR 특성  
 Xaml 서비스를 .NET Framework 하는 XAML 형식 시스템 정보를 보고 하려면 형식, 멤버 및 어셈블리의 특성을 올바르게 입력 해야 합니다. 이는 .NET Framework XAML 서비스 XAML 판독기와 XAML 작성기를 기반으로 하는 XAML 시스템에서 사용 하려는 경우 또는 이러한 XAML 판독기와 XAML 작성기를 기반으로 하는 XAML 활용 프레임 워크를 정의 하거나 사용 하려는 경우에 적합 합니다.  
  
 사용자 지정 형식의 XAML 지원과 관련 된 각 XAML 관련 특성의 목록은 [사용자 지정 형식 및 라이브러리에 대 한 Xaml 관련 CLR 특성](xaml-related-clr-attributes-for-custom-types-and-libraries.md)을 참조 하세요.  
  
## <a name="usage"></a>사용  
 사용자 지정 형식을 사용 하려면 태그 작성자가 어셈블리 및 사용자 지정 형식이 포함 된 CLR 네임 스페이스에 대 한 접두사를 매핑해야 합니다. 이 절차는이 항목에서 설명 하지 않습니다.  
  
## <a name="access-level"></a>액세스 수준  
 XAML은 `internal` 액세스 수준이 있는 형식을 로드 하 고 인스턴스화하는 방법을 제공 합니다. 사용자 코드에서 고유한 형식을 정의한 다음 동일한 사용자 코드 범위의 일부인 태그에서 해당 클래스를 인스턴스화할 수 있도록이 기능이 제공 됩니다.  
  
 WPF의 한 가지 예는 사용자 코드에서 UI <xref:System.Windows.Controls.UserControl> 동작을 리팩터링 하는 방법으로 사용 되지만 액세스 수준으로 `public` 지원 클래스를 선언 하 여 암시 될 수 있는 확장 메커니즘의 일부가 아닌를 정의할 때마다입니다. 지원 코드 <xref:System.Windows.Controls.UserControl> 를 XAML 형식으로 `internal` 참조 되는 것과 동일한 어셈블리로 컴파일하면 액세스를 사용 하 여 이러한을 선언할 수 있습니다.  
  
 완전 신뢰 및 사용 <xref:System.Xaml.XamlObjectWriter>중인 XAML을 로드 하는 응용 프로그램의 경우 액세스 수준을 사용 하 여 `internal` 클래스를 로드 하는 것은 항상 활성화 됩니다.  
  
 부분 신뢰에서 XAML을 로드 하는 응용 프로그램의 경우 API를 <xref:System.Xaml.Permissions.XamlAccessLevel> 사용 하 여 액세스 수준 특성을 제어할 수 있습니다. 또한 지연 메커니즘 (예: WPF 템플릿 시스템)은 액세스 수준 권한을 전파 하 고 최종 실행 시간 평가를 위해 유지할 수 있어야 합니다. 이는 정보를 <xref:System.Xaml.Permissions.XamlAccessLevel> 전달 하 여 내부적으로 처리 됩니다.  
  
### <a name="wpf-implementation"></a>WPF 구현  
 WPF XAML은 부분 신뢰 액세스 모델을 사용 합니다. 여기서 baml이 부분 신뢰로 로드 되 면 baml 소스인 <xref:System.Xaml.Permissions.XamlAccessLevel.AssemblyAccessTo%2A> 어셈블리에 대 한 액세스가로 제한 됩니다. 지연의 경우 WPF는 <xref:System.Xaml.IXamlObjectWriterFactory.GetParentSettings%2A?displayProperty=nameWithType> 액세스 수준 정보를 전달 하기 위한 메커니즘으로를 사용 합니다.  
  
 WPF XAML 용어에서 *내부 형식은* 참조 XAML도 포함 하는 동일한 어셈블리에 의해 정의 되는 형식입니다. 이러한 형식은 어셈블리를 의도적으로 생략 하는 XAML 네임 스페이스 (예: `xmlns:local="clr-namespace:WPFApplication1"`)를 통해 매핑될 수 있습니다.  BAML이 내부 형식을 참조 하 고 해당 형식 `internal` 에 액세스 수준이 있는 경우 어셈블리에 대 한 `GeneratedInternalTypeHelper` 클래스가 생성 됩니다. 이를 방지 `GeneratedInternalTypeHelper`하려면 액세스 수준을 사용 `public` 해야 합니다. 또는 관련 클래스의 수준을 별도의 어셈블리로 지정 하 고 해당 어셈블리를 종속 된 것으로 설정 해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [사용자 지정 형식 및 라이브러리에 대한 XAML 관련 CLR 특성](xaml-related-clr-attributes-for-custom-types-and-libraries.md)
- [XAML 서비스](index.md)
