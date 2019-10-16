---
title: 런타임 지시문(rd.xml) 구성 파일 참조
ms.date: 03/30/2017
ms.assetid: 8241523f-d8e1-4fb6-bf6a-b29bfe07b38a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: adfc0ae6d9bdae333daacee525c7775acd5a8029
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049133"
---
# <a name="runtime-directives-rdxml-configuration-file-reference"></a>런타임 지시문(rd.xml) 구성 파일 참조

런타임 지시문(.rd.xml) 파일은 지정된 프로그램 요소를 리플렉션에 사용할 수 있는지 여부를 지정하는 XML 구성 파일입니다. 런타임 지시문 파일의 예는 다음과 같습니다.

```xml
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">
  <Application>
    <Namespace Name="Contoso.Cloud.AppServices" Serialize="Required Public" />
    <Namespace Name="ContosoClient.ViewModels" Serialize="Required Public" />
    <Namespace Name="ContosoClient.DataModel" Serialize="Required Public" />
    <Namespace Name="Contoso.Reader.UtilityLib" Serialize="Required Public" />

    <Namespace Name="System.Collections.ObjectModel" >
      <TypeInstantiation Name="ObservableCollection"
            Arguments="ContosoClient.DataModel.ProductItem" Serialize="Public" />
      <TypeInstantiation Name="ReadOnlyObservableCollection"
            Arguments="ContosoClient.DataModel.ProductGroup" Serialize="Public" />
    </Namespace>
  </Application>
</Directives>
```

## <a name="the-structure-of-a-runtime-directives-file"></a>지시문 런타임 파일의 구조

런타임 지시문 파일은 `http://schemas.microsoft.com/netfx/2013/01/metadata` 네임스페이스를 사용합니다.

루트 요소는 [Directives](directives-element-net-native.md) 요소입니다. 이 요소는 다음 구조에 나와 있는 것처럼 [Library](library-element-net-native.md) 요소와 [Application](application-element-net-native.md) 요소를 포함하지 않을 수도 있고 포함할 수도 있습니다. [Application](application-element-net-native.md) 요소의 특성은 애플리케이션 전체 런타임 리플렉션 정책을 정의할 수도 있고 자식 요소의 컨테이너로 사용될 수도 있습니다. 반면 [Library](library-element-net-native.md) 요소는 단순한 컨테이너입니다. [Application](application-element-net-native.md) 및 [Library](library-element-net-native.md) 요소의 자식은 리플렉션에 사용할 수 있는 형식, 메서드, 필드, 속성 및 이벤트를 정의합니다.

참조 정보를 확인하려면 다음 구조체의 요소를 선택하거나 [런타임 지시문 요소](runtime-directive-elements.md)를 참조하세요. 다음 계층 구조에서 줄임표는 재귀 구조를 표시합니다. 괄호 안의 정보는 해당 요소가 필수 항목인지 선택적 항목인지와 요소가 사용되는 경우 허용되는 인스턴스 수(하나 또는 여러 개)를 나타냅니다.

[지시문](directives-element-net-native.md) [1:1] [응용 프로그램](application-element-net-native.md) [0:1] [어셈블리](assembly-element-net-native.md) [0: m] [네임 스페이스](namespace-element-net-native.md) [0: m]. 을 선택합니다. 을 선택합니다.
[유형](type-element-net-native.md) [0: M]. 을 선택합니다. 을 선택합니다.
[Typeinstantiation](typeinstantiation-element-net-native.md) (생성 된 제네릭 형식) [0: M]. 을 선택합니다. 을 선택합니다.
[네임 스페이스](namespace-element-net-native.md) [0: M] [네임 스페이스](namespace-element-net-native.md) [0: M]. 을 선택합니다. 을 선택합니다.
[유형](type-element-net-native.md) [0: M]. 을 선택합니다. 을 선택합니다.
[Typeinstantiation](typeinstantiation-element-net-native.md) (생성 된 제네릭 형식) [0: M]. 을 선택합니다. 을 선택합니다.
[유형](type-element-net-native.md) [0: M] [하위 유형](subtypes-element-net-native.md) (포함 형식의 하위 클래스) O:1 [유형](type-element-net-native.md) [0: M]. 을 선택합니다. 을 선택합니다.
[Typeinstantiation](typeinstantiation-element-net-native.md) (생성 된 제네릭 형식) [0: M]. 을 선택합니다. 을 선택합니다.
[Attributeimplies](attributeimplies-element-net-native.md) (형식이 포함 된 특성) O:1 [GenericParameter](genericparameter-element-net-native.md) [0: M] [메서드](method-element-net-native.md) [0: M] [매개 변수](parameter-element-net-native.md) [0: M] [Typeparameter](typeparameter-element-net-native.md) [0: M] [GenericParameter](genericparameter-element-net-native.md) [0: M] [Methodinstantiation](methodinstantiation-element-net-native.md) (생성 된 제네릭 메서드) [0: M] [속성](property-element-net-native.md) [0: M] [필드](field-element-net-native.md) [0: M] [이벤트](event-element-net-native.md) [0: M] [Typeinstantiation](typeinstantiation-element-net-native.md) (생성 된 제네릭 형식) [0: M] [유형](type-element-net-native.md) [0: M]. 을 선택합니다. 을 선택합니다.
[Typeinstantiation](typeinstantiation-element-net-native.md) (생성 된 제네릭 형식) [0: M]. 을 선택합니다. 을 선택합니다.
[메서드](method-element-net-native.md) [0: M] [매개 변수](parameter-element-net-native.md) [0: M] [Typeparameter](typeparameter-element-net-native.md) [0: M] [GenericParameter](genericparameter-element-net-native.md) [0: M] [Methodinstantiation](methodinstantiation-element-net-native.md) (생성 된 제네릭 메서드) [0: M] [속성](property-element-net-native.md) [0: M] [필드](field-element-net-native.md) [0: M] [이벤트](event-element-net-native.md) [0: M] [라이브러리](library-element-net-native.md) [0: M] [어셈블리](assembly-element-net-native.md) [0: M] [네임 스페이스](namespace-element-net-native.md) [0: M]. 을 선택합니다. 을 선택합니다.
[유형](type-element-net-native.md) [0: M]. 을 선택합니다. 을 선택합니다.
[Typeinstantiation](typeinstantiation-element-net-native.md) (생성 된 제네릭 형식) [0: M]. 을 선택합니다. 을 선택합니다.
[네임 스페이스](namespace-element-net-native.md) [0: M] [네임 스페이스](namespace-element-net-native.md) [0: M]. 을 선택합니다. 을 선택합니다.
[유형](type-element-net-native.md) [0: M]. 을 선택합니다. 을 선택합니다.
[Typeinstantiation](typeinstantiation-element-net-native.md) (생성 된 제네릭 형식) [0: M]. 을 선택합니다. 을 선택합니다.
[유형](type-element-net-native.md) [0: M] [하위 유형](subtypes-element-net-native.md) (포함 형식의 하위 클래스) O:1 [유형](type-element-net-native.md) [0: M]. 을 선택합니다. 을 선택합니다.
[Typeinstantiation](typeinstantiation-element-net-native.md) (생성 된 제네릭 형식) [0: M]. 을 선택합니다. 을 선택합니다.
[Attributeimplies](attributeimplies-element-net-native.md) (형식이 포함 된 특성) O:1 [GenericParameter](genericparameter-element-net-native.md) [0: M] [메서드](method-element-net-native.md) [0: M] [Methodinstantiation](methodinstantiation-element-net-native.md) (생성 된 제네릭 메서드) [0: M] [속성](property-element-net-native.md) [0: M] [필드](field-element-net-native.md) [0: M] [이벤트](event-element-net-native.md) [0: M] [Typeinstantiation](typeinstantiation-element-net-native.md) (생성 된 제네릭 형식) [0: M] [유형](type-element-net-native.md) [0: M]. 을 선택합니다. 을 선택합니다.
[Typeinstantiation](typeinstantiation-element-net-native.md) (생성 된 제네릭 형식) [0: M]. 을 선택합니다. 을 선택합니다.
[메서드](method-element-net-native.md) [0: M] [Methodinstantiation](methodinstantiation-element-net-native.md) (생성 된 제네릭 메서드) [0: M] [속성](property-element-net-native.md) [0: M] [필드](field-element-net-native.md) [0: M] [이벤트](event-element-net-native.md) [0: M]

[Application](application-element-net-native.md) 요소는 특성을 포함할 수 없거나 [런타임 지시문 및 정책 섹션](#Directives)에서 설명하는 정책 특성을 포함할 수 있습니다.

[Library](library-element-net-native.md) 요소는 파일 이름 확장명을 포함하지 않는 라이브러리나 어셈블리의 이름을 지정하는 단일 특성(`Name`)을 포함합니다. 예를 들어 다음 [Library](library-element-net-native.md) 요소는 Extensions.dll 어셈블리에 적용되는 요소입니다.

```xml
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">
  <Application>
     <!-- Child elements go here -->
  </Application>
  <Library Name="Extensions">
     <!-- Child elements go here -->
  </Library>
</Directives>
```

<a name="Directives"></a>

## <a name="runtime-directives-and-policy"></a>런타임 지시문 및 정책

[Application](application-element-net-native.md) 요소 자체와 [Library](library-element-net-native.md) 및 [Application](application-element-net-native.md) 요소의 자식 요소는 정책을 표현합니다. 즉, 앱이 프로그램 요소에 리플렉션을 적용할 수 있는 방식을 정의합니다. 정책 형식은 요소의 특성에 의해 정의됩니다(예: `Serialize`). 정책 값은 특성의 값으로 정의됩니다(예: `Serialize="Required"`).

요소의 특성으로 지정된 정책은 해당 정책에 대해 값을 지정하지 않는 모든 자식 요소에 적용됩니다. 예를 들어 정책이 [Type](type-element-net-native.md) 요소로 지정된 경우 정책이 명시적으로 지정되지 않은 모든 포함된 형식 및 멤버에 해당 정책이 적용됩니다.

[Application](application-element-net-native.md), [Assembly](assembly-element-net-native.md), [AttributeImplies](attributeimplies-element-net-native.md), [Namespace](namespace-element-net-native.md), [Subtypes](subtypes-element-net-native.md) 및 [Type](type-element-net-native.md) 요소로 표현할 수 있는 정책은 [Method](method-element-net-native.md), [Property](property-element-net-native.md), [Field](field-element-net-native.md) 및 [Event](event-element-net-native.md) 요소로 개별 멤버에 대해 표현할 수 있는 정책과는 다릅니다.

### <a name="specifying-policy-for-assemblies-namespaces-and-types"></a>어셈블리, 네임스페이스 및 형식에 대한 정책 지정

[Application](application-element-net-native.md), [Assembly](assembly-element-net-native.md), [AttributeImplies](attributeimplies-element-net-native.md), [Namespace](namespace-element-net-native.md), [Subtypes](subtypes-element-net-native.md) 및 [Type](type-element-net-native.md) 요소는 다음 정책 형식을 지원합니다.

- `Activate`. 인스턴스를 활성화할 수 있도록 생성자에 대한 런타임 액세스를 제어합니다.

- `Browse`. 프로그램 요소에 대한 정보 쿼리를 제어하지만 런타임 액세스를 사용하도록 설정하지는 않습니다.

- `Dynamic`. 동적 프로그래밍을 수행할 수 있도록 생성자, 메서드, 필드, 속성 및 이벤트를 비롯한 모든 형식 멤버에 대한 런타임 액세스를 제어합니다.

- `Serialize`. Newtonsoft JSON serializer 등의 타사 라이브러리를 통해 형식 인스턴스를 serialize 및 deserialize할 수 있도록 생성자, 필드 및 속성에 대한 런타임 액세스를 제어합니다.

- `DataContractSerializer`. <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> 클래스를 사용하는 serialization에 대한 정책을 제어합니다.

- `DataContractJsonSerializer`. <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> 클래스를 사용하는 JSON serialization에 대한 정책을 제어합니다.

- `XmlSerializer`. <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> 클래스를 사용하는 XML serialization에 대한 정책을 제어합니다.

- `MarshalObject`. WinRT 및 COM에 대한 참조 형식을 마샬링하는 정책을 제어합니다.

- `MarshalDelegate`. 네이티브 코드에 대한 함수 포인터로 대리자 형식을 마샬링하는 정책을 제어합니다.

- `MarshalStructure` . 구조체를 네이티브 코드로 마샬링하는 정책을 제어합니다.

이러한 정책 형식과 연관된 설정은 다음과 같습니다.

- `All`. 도구 체인에서 제거하지 않는 모든 형식과 멤버에 대해 정책을 사용하도록 설정합니다.

- `Auto`. 기본 동작을 사용합니다. 정책을 지정하지 않는 것은 부모 요소에 의해 정책이 재정의되는 등의 경우를 제외하면 해당 정책을 `Auto`로 설정하는 것과 같습니다.

- `Excluded`. 프로그램 요소에 대한 정책을 사용하지 않도록 설정합니다.

- `Public`. 도구 체인이 멤버를 불필요한 것으로 결정하여 제거하는 경우가 아니면 public 형식 또는 멤버에 대해서는 정책을 사용하도록 설정합니다. 멤버가 제거되는 경우에는 `Required Public`을 사용하여 멤버를 유지하고 리플렉션 기능이 포함되도록 해야 합니다.

- `PublicAndInternal`. 도구 체인에서 제거하지 않는 public 및 내부 형식이나 멤버에 대해 정책을 사용하도록 설정합니다.

- `Required Public`. 사용 여부에 관계없이 도구 체인이 public 형식과 멤버를 유지해야 하도록 지정하고 해당 형식과 멤버에 대해 정책을 사용하도록 설정합니다.

- `Required PublicAndInternal`. 사용 여부에 관계없이 도구 체인이 public 및 내부 형식과 멤버를 모두 유지해야 하도록 지정하고 해당 형식과 멤버에 대해 정책을 사용하도록 설정합니다.

- `Required All`. 사용 여부에 관계없이 도구 체인이 모든 형식과 멤버를 유지해야 하도록 지정하고 해당 형식과 멤버에 대해 정책을 사용하도록 설정합니다.

예를 들어 다음 런타임 지시문 파일은 DataClasses.dll 어셈블리의 모든 형식과 멤버에 대한 정책을 정의합니다. 이 정책은 모든 public 속성의 serialization에 대해 리플렉션을 사용하도록 설정하고, 모든 형식 및 형식 멤버를 검색할 수 있도록 설정하고, `Dynamic` 특성을 통해 모든 형식을 활성화할 수 있도록 설정하고, 모든 public 형식 및 멤버에 대해 리플렉션을 사용하도록 설정합니다.

```xml
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">
   <Application>
      <Assembly Name="DataClasses" Serialize="Required Public"
                Browse="All" Activate="PublicAndInternal"
                Dynamic="Public"  />
   </Application>
   <Library Name="UtilityLibrary">
     <!-- Child elements go here -->
   </Library>
</Directives>
```

### <a name="specifying-policy-for-members"></a>멤버에 대한 정책 지정

[Property](property-element-net-native.md) 및 [Field](field-element-net-native.md) 요소는 다음 정책 형식을 지원합니다.

- `Browse` - 이 멤버에 대한 정보 쿼리는 제어하지만 런타임 액세스를 사용하도록 설정하지는 않습니다.

- `Dynamic` - 동적 프로그래밍을 수행할 수 있도록 생성자, 메서드, 필드, 속성 및 이벤트를 비롯한 모든 형식 멤버에 대한 런타임 액세스를 제어합니다. 또한 포함 형식에 대한 정보 쿼리도 제어합니다.

- `Serialize` - Newtonsoft JSON serializer 등의 라이브러리를 통해 형식 인스턴스를 serialize 및 deserialize할 수 있도록 멤버에 대한 런타임 액세스를 제어합니다. 이 정책은 생성자, 필드 및 속성에 적용할 수 있습니다.

[Method](method-element-net-native.md) 및 [Event](event-element-net-native.md) 요소는 다음 정책 형식을 지원합니다.

- `Browse` - 이 멤버에 대한 정보 쿼리는 제어하지만 런타임 액세스를 사용하도록 설정하지는 않습니다.

- `Dynamic` - 동적 프로그래밍을 수행할 수 있도록 생성자, 메서드, 필드, 속성 및 이벤트를 비롯한 모든 형식 멤버에 대한 런타임 액세스를 제어합니다. 또한 포함 형식에 대한 정보 쿼리도 제어합니다.

 이러한 정책 형식과 연관된 설정은 다음과 같습니다.

- `Auto` - 기본 동작을 사용합니다. 특정 요소가 정책을 재정의하는 경우를 제외하면 정책을 지정하지 않는 것은 정책을 `Auto`로 설정하는 것과 같습니다.

- `Excluded` - 멤버에 대한 메타데이터를 포함하지 않습니다.

- `Included` - 출력에 부모 형식이 있으면 정책을 사용하도록 설정합니다.

- `Required` - 특정 멤버가 사용되지 않는 것으로 확인되더라도 도구 체인이 해당 멤버를 유지해야 하도록 지정하고 해당 멤버에 대해 정책을 사용하도록 설정합니다.

## <a name="runtime-directives-file-semantics"></a>런타임 지시문 파일 의미

상위 및 하위 요소 둘 다에 대해 정책을 동시에 정의할 수 있습니다. 예를 들어 어셈블리 및 해당 어셈블리에 포함된 일부 형식에 대한 정책을 정의할 수 있습니다. 표시되지 않는 특정 하위 요소는 부모의 정책을 상속합니다. 예를 들어 `Assembly` 요소는 있는데 `Type` 요소는 없으면 `Assembly` 요소에 지정된 정책이 어셈블리의 각 형식에 적용됩니다. 또한 여러 요소가 같은 프로그램 요소에 정책을 적용할 수도 있습니다. 예를 들어 개별 [Assembly](assembly-element-net-native.md) 요소가 같은 어셈블리에 대해 같은 정책 요소를 각기 다르게 정의할 수 있습니다. 다음 섹션에서는 이러한 경우 특정 형식에 대한 정책을 확인하는 방법을 설명합니다.

제네릭 형식이나 메서드의 [Type](type-element-net-native.md) 또는 [Method](method-element-net-native.md) 요소는 자체 정책을 포함하지 않는 모든 인스턴스화에 해당 정책을 적용합니다. 예를 들어 `Type`에 대해 정책을 지정하는 <xref:System.Collections.Generic.List%601> 요소는 해당 제네릭 형식의 생성된 모든 인스턴스에 적용됩니다. 단, `List<Int32>` 요소가 `TypeInstantiation`와 같은 생성된 특정 제네릭 형식에 대해 정책을 재정의하는 경우는 예외입니다. 이러한 경우가 아니면 요소는 명명된 프로그램 요소에 대해 정책을 정의합니다.

요소가 모호한 경우 엔진은 일치하는 항목을 찾으며 정확히 일치하는 항목이 발견되면 해당 항목을 사용합니다. 일치하는 항목이 여러 개이면 경고나 오류가 표시됩니다.

### <a name="if-two-directives-apply-policy-to-the-same-program-element"></a>두 지시문이 같은 프로그램 요소에 정책을 적용하는 경우

서로 다른 런타임 지시문 파일의 두 요소가 어셈블리나 형식 등의 같은 프로그램 요소에 대한 동일 정책 형식을 각기 다른 값으로 설정하려는 경우에는 다음과 같은 방법으로 충돌을 해결합니다.

1. `Excluded` 요소가 있으면 우선적으로 적용됩니다.

2. `Required`인 항목이 `Required`가 아닌 항목보다 우선적으로 적용됩니다.

3. `All`, `PublicAndInternal`, `Public`이 순서대로 적용됩니다.

4. 명시적 설정이 `Auto`보다 우선적으로 적용됩니다.

예를 들어 프로젝트 하나에 다음과 같은 두 런타임 지시문 파일이 포함되어 있으면 DataClasses.dll의 serialization 정책이 `Required Public` 및 `All` 둘 다로 설정됩니다. 이 경우 serialization 정책은 `Required All`로 확인됩니다.

```xml
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">
   <Application>
      <Assembly Name="DataClasses" Serialize="Required Public"/>
   </Application>
   <Library Name="DataClasses">
      <!-- any other elements -->
   </Library>
</Directives>
```

```xml
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">
   <Application>
      <Assembly Name="DataClasses" Serialize="All" />
   </Application>
   <Library Name="DataClasses">
      <!-- any other elements -->
   </Library>
</Directives>
```

그러나 단일 런타임 지시문 파일의 두 지시문이 같은 프로그램 요소에 대해 같은 정책 형식을 설정하려고 하면 XML 스키마 정의 도구에 오류 메시지가 표시됩니다.

### <a name="if-child-and-parent-elements-apply-the-same-policy-type"></a>자식 및 부모 요소가 같은 정책 형식을 적용하는 경우

자식 요소는 `Excluded` 설정을 포함하여 부모 요소를 재정의합니다. 대개 이러한 재정의로 인해 `Auto`를 지정하게 됩니다.

다음 예에서는 `DataClasses`에 포함되어 있지 않은 `DataClasses.ViewModels`의 모든 항목에 대한 serialization 정책 설정은 `Required Public`이 되고 `DataClasses` 및 `DataClasses.ViewModels`에 모두 포함되어 있는 모든 항목에 대한 serialization 정책 설정은 `All`이 됩니다.

```xml
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">
   <Application>
      <Assembly Name="DataClasses" Serialize="Required Public" >
         <Namespace Name="DataClasses.ViewModels" Serialize="All" />
      </Assembly>
   </Application>
   <Library Name="DataClasses">
      <!-- any other elements -->
   </Library>
</Directives>
```

### <a name="if-open-generics-and-instantiated-elements-apply-the-same-policy-type"></a>개방형 제네릭 및 인스턴스화된 요소 형식이 같은 정책을 적용하는 경우

다음 예제에서는 엔진이 다른 이유로 인해 `Dictionary<int,int>` 정책을 적용해야 하는 경우에만 `Browse`에 `Browse` 정책이 할당됩니다(그렇지 않으면 이 정책이 기본 동작임). <xref:System.Collections.Generic.Dictionary%602>의 다른 모든 인스턴스화에서는 모든 구성원을 검색할 수 있습니다.

```xml
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">
   <Application>
      <Assembly Name="DataClasses" Serialize="Required Public" >
         <Namespace Name="DataClasses.ViewModels" Serialize="All" />
      </Assembly>
      <Namespace Name="DataClasses.Generics" />
      <Type Name="Dictionary" Browse="All" />
      <TypeInstantiation Name="Dictionary"
                         Arguments="System.Int32,System.Int32" Browse="Auto" />
   </Application>
   <Library Name="DataClasses">
      <!-- any other elements -->
   </Library>
</Directives>
```

### <a name="how-policy-is-inferred"></a>정책을 유추하는 방법

각 정책 형식에는 해당 정책 형식의 유무가 다른 구문에 주는 영향을 결정하는 여러 규칙 집합이 있습니다.

#### <a name="the-effect-of-browse-policy"></a>Browse 정책의 영향

형식에 `Browse` 정책을 적용하면 정책이 다음과 같이 변경됩니다.

- 해당 형식의 기본 형식이 `Browse` 정책으로 표시됩니다.

- 형식이 인스턴스화된 제네릭인 경우 인스턴스화되지 않은 형식 버전이 `Browse` 정책으로 표시됩니다.

- 형식이 대리자인 경우에는 형식의 `Invoke` 메서드가 `Dynamic` 정책으로 표시됩니다.

- 형식의 각 인터페이스가 `Browse` 정책으로 표시됩니다.

- 형식에 적용된 각 특성의 형식이 `Browse` 정책으로 표시됩니다.

- 형식이 제네릭인 경우 각 제약 조건 형식이 `Browse` 정책으로 표시됩니다.

- 형식이 제네릭이면 해당 형식이 인스턴스화되는 형식이 `Browse` 정책으로 표시됩니다.

메서드에 `Browse` 정책을 적용하면 정책이 다음과 같이 변경됩니다.

- 메서드의 각 매개 변수 형식이 `Browse` 정책으로 표시됩니다.

- 해당 메서드의 반환 형식이 `Browse` 정책으로 표시됩니다.

- 해당 메서드의 포함 형식이 `Browse` 정책으로 표시됩니다.

- 메서드가 인스턴스화된 제네릭 메서드인 경우 인스턴스화되지 않은 제네릭 메서드가 `Browse` 정책으로 표시됩니다.

- 메서드에 적용된 각 특성의 형식이 `Browse` 정책으로 표시됩니다.

- 메서드가 제네릭인 경우 각 제약 조건 형식이 `Browse` 정책으로 표시됩니다.

- 메서드가 제네릭이면 해당 메서드가 인스턴스화되는 형식이 `Browse` 정책으로 표시됩니다.

필드에 `Browse` 정책을 적용하면 정책이 다음과 같이 변경됩니다.

- 필드에 적용된 각 특성의 형식이 `Browse` 정책으로 표시됩니다.

- 필드의 형식이 `Browse` 정책으로 표시됩니다.

- 필드가 속하는 형식이 `Browse` 정책으로 표시됩니다.

#### <a name="the-effect-of-dynamic-policy"></a>Dynamic 정책의 영향

형식에 `Dynamic` 정책을 적용하면 정책이 다음과 같이 변경됩니다.

- 해당 형식의 기본 형식이 `Dynamic` 정책으로 표시됩니다.

- 형식이 인스턴스화된 제네릭인 경우 인스턴스화되지 않은 형식 버전이 `Dynamic` 정책으로 표시됩니다.

- 형식이 대리자 형식인 경우에는 형식의 `Invoke` 메서드가 `Dynamic` 정책으로 표시됩니다.

- 형식의 각 인터페이스가 `Browse` 정책으로 표시됩니다.

- 형식에 적용된 각 특성의 형식이 `Browse` 정책으로 표시됩니다.

- 형식이 제네릭인 경우 각 제약 조건 형식이 `Browse` 정책으로 표시됩니다.

- 형식이 제네릭이면 해당 형식이 인스턴스화되는 형식이 `Browse` 정책으로 표시됩니다.

메서드에 `Dynamic` 정책을 적용하면 정책이 다음과 같이 변경됩니다.

- 메서드의 각 매개 변수 형식이 `Browse` 정책으로 표시됩니다.

- 해당 메서드의 반환 형식이 `Dynamic` 정책으로 표시됩니다.

- 해당 메서드의 포함 형식이 `Dynamic` 정책으로 표시됩니다.

- 메서드가 인스턴스화된 제네릭 메서드인 경우 인스턴스화되지 않은 제네릭 메서드가 `Browse` 정책으로 표시됩니다.

- 메서드에 적용된 각 특성의 형식이 `Browse` 정책으로 표시됩니다.

- 메서드가 제네릭인 경우 각 제약 조건 형식이 `Browse` 정책으로 표시됩니다.

- 메서드가 제네릭이면 해당 메서드가 인스턴스화되는 형식이 `Browse` 정책으로 표시됩니다.

- `MethodInfo.Invoke`를 통해 메서드를 호출할 수 있으며 <xref:System.Reflection.MethodInfo.CreateDelegate%2A?displayProperty=nameWithType>를 통해 대리자를 만들 수 있습니다.

필드에 `Dynamic` 정책을 적용하면 정책이 다음과 같이 변경됩니다.

- 필드에 적용된 각 특성의 형식이 `Browse` 정책으로 표시됩니다.

- 필드의 형식이 `Dynamic` 정책으로 표시됩니다.

- 필드가 속하는 형식이 `Dynamic` 정책으로 표시됩니다.

#### <a name="the-effect-of-activation-policy"></a>Activation 정책의 영향

형식에 Activation 정책을 적용하면 정책이 다음과 같이 변경됩니다.

- 형식이 인스턴스화된 제네릭인 경우 인스턴스화되지 않은 형식 버전이 `Browse` 정책으로 표시됩니다.

- 형식이 대리자 형식인 경우에는 형식의 `Invoke` 메서드가 `Dynamic` 정책으로 표시됩니다.

- 형식의 생성자가 `Activation` 정책으로 표시됩니다.

메서드에 `Activation` 정책을 적용하면 정책이 다음과 같이 변경됩니다.

- <xref:System.Reflection.ConstructorInfo.Invoke%2A?displayProperty=nameWithType> 및 <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType> 메서드를 통해 생성자를 호출할 수 있습니다. 메서드의 경우에는 `Activation` 정책이 생성자에만 적용됩니다.

필드에는 `Activation` 정책을 적용해도 아무런 영향이 없습니다.

#### <a name="the-effect-of-serialize-policy"></a>Serialize 정책의 영향

`Serialize` 정책을 적용하면 일반적인 리플렉션 기반 serializer를 사용할 수 있습니다. 그러나 Microsoft는 타사 serializer의 정확한 리플렉션 액세스 패턴을 확인할 수 없으므로 이 정책이 완전히 적용되지 않을 수도 있습니다.

형식에 `Serialize` 정책을 적용하면 정책이 다음과 같이 변경됩니다.

- 해당 형식의 기본 형식이 `Serialize` 정책으로 표시됩니다.

- 형식이 인스턴스화된 제네릭인 경우 인스턴스화되지 않은 형식 버전이 `Browse` 정책으로 표시됩니다.

- 형식이 대리자 형식인 경우에는 형식의 `Invoke` 메서드가 `Dynamic` 정책으로 표시됩니다.

- 형식이 열거형이면 해당 형식의 배열이 `Serialize` 정책으로 표시됩니다.

- 형식이 <xref:System.Collections.Generic.IEnumerable%601>를 구현하는 경우 `T`가 `Serialize` 정책으로 표시됩니다.

- 형식이 <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.Generic.IList%601>, <xref:System.Collections.Generic.ICollection%601>, <xref:System.Collections.Generic.IReadOnlyCollection%601> 또는 <xref:System.Collections.Generic.IReadOnlyList%601>이면 `T[]` 및 <xref:System.Collections.Generic.List%601>는 `Serialize` 정책으로 표시되지만 인터페이스 형식의 멤버는 `Serialize` 정책으로 표시되지 않습니다.

- 형식이 <xref:System.Collections.Generic.List%601>이면 형식의 멤버는 `Serialize` 정책으로 표시되지 않습니다.

- 형식이 <xref:System.Collections.Generic.IDictionary%602>이면 <xref:System.Collections.Generic.Dictionary%602>가 `Serialize` 정책으로 표시됩니다. 그러나 형식의 멤버는 `Serialize` 정책으로 표시되지 않습니다.

- 형식이 <xref:System.Collections.Generic.Dictionary%602>이면 형식의 멤버는 `Serialize` 정책으로 표시되지 않습니다.

- 형식이 <xref:System.Collections.Generic.IDictionary%602>를 구현하는 경우 `TKey` 및 `TValue`는 `Serialize` 정책으로 표시됩니다.

- 각 생성자, 각 속성 접근자 및 각 필드가 `Serialize` 정책으로 표시됩니다.

메서드에 `Serialize` 정책을 적용하면 정책이 다음과 같이 변경됩니다.

- 포함 형식이 `Serialize` 정책으로 표시됩니다.

- 해당 메서드의 반환 형식이 `Serialize` 정책으로 표시됩니다.

필드에 `Serialize` 정책을 적용하면 정책이 다음과 같이 변경됩니다.

- 포함 형식이 `Serialize` 정책으로 표시됩니다.

- 필드의 형식이 `Serialize` 정책으로 표시됩니다.

#### <a name="the-effect-of-xmlserializer-datacontractserializer-and-datacontractjsonserializer-policies"></a>XmlSerializer, DataContractSerializer 및 DataContractJsonSerializer 정책의 영향

리플렉션 기반 serializer <xref:System.Xml.Serialization.XmlSerializer>에 사용 되는 <xref:System.Runtime.Serialization.DataContractSerializer> <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> `Serialize` 정책과 달리, 및 정책은 .NET 네이티브 도구 체인에 알려진 일련의 직렬 변환기를 사용 하도록 설정 하는 데 사용 됩니다. 이러한 serializer는 리플렉션을 사용하여 구현되지 않으며 런타임에 serialize할 수 있는 형식 집합은 리플렉션 가능한 형식과 비슷한 방식으로 결정됩니다.

이러한 정책 중 하나를 형식에 적용하면 일치하는 serializer를 사용하여 형식을 serialize할 수 있습니다. 또한 serialization 엔진이 serialization을 수행해야 한다고 정적으로 확인할 수 있는 모든 형식도 serialize할 수 있습니다.

이러한 정책은 메서드 또는 필드에는 영향을 주지 않습니다.

자세한 내용은 [Windows 스토어 앱을 .NET 네이티브로 마이그레이션](migrating-your-windows-store-app-to-net-native.md)에서 “직렬 변환기의 차이점” 섹션을 참조하세요.

## <a name="see-also"></a>참고자료

- [런타임 지시문 요소](runtime-directive-elements.md)
- [리플렉션 및 .NET 네이티브](reflection-and-net-native.md)
