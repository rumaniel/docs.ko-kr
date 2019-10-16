---
title: 특성(C#)
ms.date: 04/26/2018
ms.openlocfilehash: 7b78d5832c15d3d1142b80d2ccb96a72e4e20390
ms.sourcegitcommit: c70542d02736e082e8dac67dad922c19249a8893
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/05/2019
ms.locfileid: "70374377"
---
# <a name="attributes-c"></a>특성(C#)

특성은 메타데이터 또는 선언적 정보를 코드(어셈블리, 형식, 메서드, 속성 등)에 연결하는 강력한 방법을 제공합니다. 특성이 프로그램 엔터티와 연결되면 *리플렉션*이라는 기법을 사용하여 런타임에 특성이 쿼리될 수 있습니다. 자세한 내용은 [리플렉션(C#)](../reflection.md)을 참조하세요.

특성에는 다음과 같은 속성이 있습니다.

- 특성은 프로그램에 메타데이터를 추가합니다. *메타데이터*는 프로그램에 정의된 형식에 대한 정보를 의미합니다. 모든 .NET 어셈블리에는 어셈블리에 정의된 형식 및 형식 멤버를 설명하는 지정된 메타데이터 집합이 포함됩니다. 필요한 추가 정보를 지정하는 사용자 지정 특성을 추가할 수 있습니다. 자세한 내용은 [사용자 지정 특성 만들기(C#)](creating-custom-attributes.md)를 참조하세요.
- 전체 어셈블리, 모듈 또는 좀 더 작은 프로그램 요소(예: 클래스 및 속성)에 하나 이상의 특성을 적용할 수 있습니다.
- 메서드 및 속성의 경우와 같은 방식으로 특성은 인수를 수락할 수 있습니다.
- 프로그램은 리플렉션을 사용하여 자체 메타데이터 또는 다른 프로그램의 메타데이터를 검사할 수 있습니다. 자세한 내용은 [리플렉션을 사용하여 특성 액세스(C#)](accessing-attributes-by-using-reflection.md)를 참조하세요.

## <a name="using-attributes"></a>특성 사용

특정 특성은 유효한 선언 형식이 제한적일 수 있지만 거의 모든 선언에 특성을 사용할 수 있습니다. C#에서는 특성 이름을 대괄호([])로 묶어 적용하고자 하는 엔터티의 선언 위에 배치하여 특성을 지정합니다.

이 예제에서 <xref:System.SerializableAttribute> 특성은 클래스에 특정 특성을 적용하는 데 사용됩니다.

[!code-csharp[Using the serializable attribute](../../../../../samples/snippets/csharp/attributes/AttributesOverview.cs#1)]

<xref:System.Runtime.InteropServices.DllImportAttribute> 특성을 사용하는 메서드는 다음 예제와 같이 선언됩니다.

[!code-csharp[Declaring a method to import from an external library](../../../../../samples/snippets/csharp/attributes/AttributesOverview.cs#2)]

다음 예제와 같이 둘 이상의 특성을 하나의 선언에 추가할 수 있습니다.

[!code-csharp[Including the interop namespace](../../../../../samples/snippets/csharp/attributes/AttributesOverview.cs#3)]
[!code-csharp[Declaring two way marshaling for arguments](../../../../../samples/snippets/csharp/attributes/AttributesOverview.cs#4)]

지정된 엔터티에 대해 일부 특성을 두 번 이상 지정할 수 있습니다. 이러한 다용도 특성의 예로 <xref:System.Diagnostics.ConditionalAttribute>가 있습니다.

[!code-csharp[Using the conditional attribute](../../../../../samples/snippets/csharp/attributes/AttributesOverview.cs#5)]

> [!NOTE]
> 규칙에 따라 모든 특성 이름은 .NET 라이브러리의 다른 항목과 구분하기 위해 "Attribute" 단어로 끝납니다. 그러나 코드에서 특성을 사용하는 경우 특성 접미사를 지정할 필요가 없습니다. 예를 들어 `[DllImport]`는 `[DllImportAttribute]`와 같지만 `DllImportAttribute`는 .NET Framework 클래스 라이브러리에서 특성의 실제 이름입니다.

### <a name="attribute-parameters"></a>특성 매개 변수

많은 특성에는 매개 변수를 위치, 명명되지 않은 또는 명명된 상태의 매개 변수가 있을 수 있습니다. 위치 매개 변수를 특정 순서로 지정해야 하며 생략할 수는 없습니다. 명명된 매개 변수는 선택 사항이며 순서에 관계 없이 지정할 수 있습니다. 위치 매개 변수가 가장 먼저 지정됩니다. 예를 들어 다음 세 가지 특성은 동급입니다.

```csharp
[DllImport("user32.dll")]
[DllImport("user32.dll", SetLastError=false, ExactSpelling=false)]
[DllImport("user32.dll", ExactSpelling=false, SetLastError=false)]
```

첫 번째 매개 변수인 DLL 이름은 위치 매개 변수이므로 항상 맨 먼저 오고 나머지 매개 변수가 지정됩니다. 이 경우 명명된 두 매개 변수는 기본적으로 false이므로 생략할 수 있습니다. 위치 매개 변수는 특성 생성자의 매개 변수에 해당합니다. 명명된 또는 선택적 매개 변수는 특성의 속성 또는 필드에 해당합니다. 기본 매개 변수 값에 대한 자세한 내용은 개별 특성의 설명서를 참조하세요.

### <a name="attribute-targets"></a>특성 대상

특성의 *대상*은 특성이 적용되는 엔터티입니다. 예를 들어 특성은 클래스, 특정 메서드 또는 전체 어셈블리에 적용될 수 있습니다. 기본적으로 특성은 그 뒤에 오는 요소에 적용됩니다. 하지만 특성이 메서드, 해당 매개 변수 또는 해당 반환 값 중 어디에 적용될지를 명시적으로 지정할 수 있습니다.

특성 대상을 명시적으로 식별하려면 다음 구문을 사용합니다.

```csharp
[target : attribute-list]
```

가능한 `target` 값 목록은 다음 표에 나와 있습니다.

|대상 값|적용 대상|
|------------------|----------------|
|`assembly`|전체 어셈블리|
|`module`|현재 어셈블리 모듈|
|`field`|클래스 또는 구조체의 필드|
|`event`|이벤트|
|`method`|메서드 또는 `get` 및 `set` 속성 접근자|
|`param`|메서드 매개 변수 또는 `set` 속성 접근자 매개 변수|
|`property`|속성|
|`return`|메서드, 속성 인덱서 또는 `get` 속성 접근자의 반환 값|
|`type`|구조체, 클래스, 인터페이스, 열거형 또는 대리자|

[자동 구현 속성](../../../properties.md)에 대해 생성된 지원 필드에 특성을 적용하기 위해 `field` 대상 값을 지정합니다.

다음 예제에서는 어셈블리와 모듈에 특성을 적용하는 방법을 보여 줍니다. 자세한 내용은 [공통 특성(C#)](common-attributes.md)을 참조하세요.

```csharp
using System;
using System.Reflection;
[assembly: AssemblyTitleAttribute("Production assembly 4")]
[module: CLSCompliant(true)]
```

다음 예제에서는 C#에서 메서드, 메서드 매개 변수 및 메서드 반환 값에 특성을 적용하는 방법을 보여 줍니다.

[!code-csharp[Applying attributes to different code elements](../../../../../samples/snippets/csharp/attributes/AttributesOverview.cs#6)]

> [!NOTE]
> `ValidatedContract`이 정의되는 대상이 유효한지에 상관없이, 반환 값에만 적용하도록 `ValidatedContract`이 정의된 경우에도 `return` 대상을 지정해야 합니다. 즉, 컴파일러는 모호한 특성 대상을 확인하기 위해 `AttributeUsage` 정보를 사용하지 않습니다. 자세한 내용은 [AttributeUsage(C#)](attributeusage.md)를 참조하세요.

## <a name="common-uses-for-attributes"></a>특성의 일반적인 용도

다음 목록에는 코드에서 특성이 사용되는 일반적인 경우가 나와 있습니다.

- SOAP 프로토콜을 통해 메서드를 호출할 수 있음을 나타내기 위해 웹 서비스에서 `WebMethod` 특성을 사용하여 메서드에 표시. 자세한 내용은 <xref:System.Web.Services.WebMethodAttribute>을 참조하세요.
- 네이티브 코드와 상호 운용될 경우 메서드 매개 변수를 마샬링하는 방법 설명. 자세한 내용은 <xref:System.Runtime.InteropServices.MarshalAsAttribute>을 참조하세요.
- 클래스, 메서드 및 인터페이스에 대한 COM 속성 설명
- <xref:System.Runtime.InteropServices.DllImportAttribute> 클래스를 사용하는 비관리 코드 호출
- 제목, 버전, 설명 또는 상표를 기준으로 어셈블리 설명
- 지속성을 위해 serialize할 클래스의 멤버 설명
- XML serialization를 위해 클래스 멤버 및 XML 노드 간을 매핑하는 방법 설명
- 메서드에 대한 보안 요구 사항 설명
- 보안을 적용하는 데 사용되는 특징 지정
- 코드를 쉽게 디버그할 수 있도록 하기 위해 JIT(Just-In-Time) 컴파일러를 통해 최적화 제어
- 메서드 호출자에 대한 정보 얻기

## <a name="related-sections"></a>관련 단원

자세한 내용은 다음을 참조하세요.

- [사용자 지정 특성 만들기(C#)](creating-custom-attributes.md)  
- [리플렉션을 사용하여 특성 액세스(C#)](accessing-attributes-by-using-reflection.md)  
- [방법: 특성을 사용하여 C/C++ 공용 구조체 만들기(C#)](how-to-create-a-c-cpp-union-by-using-attributes.md)  
- [공통 특성(C#)](common-attributes.md)  
- [호출자 정보(C#)](../caller-information.md)  

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../../index.md)
- [리플렉션(C#)](../reflection.md)
- [특성](../../../../standard/attributes/index.md)
- [C#에서 특성 사용](../../../tutorials/attributes.md)
