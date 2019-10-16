---
title: 특성
description: 특성을 F# 사용 하 여 프로그래밍 구문에 메타 데이터를 적용 하는 방법을 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 17822891109b8e8eaa10044f82f0b872ce9d30b5
ms.sourcegitcommit: 878ca7550b653114c3968ef8906da2b3e60e3c7a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2019
ms.locfileid: "71736806"
---
# <a name="attributes"></a>특성

특성을 사용 하면 프로그래밍 구문에 메타 데이터를 적용할 수 있습니다.

## <a name="syntax"></a>구문

```fsharp
[<target:attribute-name(arguments)>]
```

## <a name="remarks"></a>설명

이전 구문에서 *대상은* 선택 사항이 며, 있는 경우 특성이 적용 되는 프로그램 엔터티의 종류를 지정 합니다. *대상* 에 유효한 값은이 문서의 뒷부분에 나오는 표에 표시 됩니다.

*특성 이름* 은 특성 형식 이름에 일반적으로 사용 되는 접미사 `Attribute` 를 사용 하거나 사용 하지 않고 유효한 특성 형식의 이름 (네임 스페이스로 한정 될 수 있음)을 참조 합니다. 예를 들어이 컨텍스트에서 `ObsoleteAttribute` 만 `Obsolete` 형식이 줄어들 수 있습니다.

*인수* 는 특성 형식의 생성자에 대 한 인수입니다. 특성에 매개 변수가 없는 생성자가 있는 경우 인수 목록과 괄호를 생략할 수 있습니다. 특성은 위치 인수와 명명 된 인수를 모두 지원 합니다. *위치 인수* 는 표시 되는 순서 대로 사용 되는 인수입니다. 특성에 public 속성이 있는 경우 명명 된 인수를 사용할 수 있습니다. 인수 목록에서 다음 구문을 사용 하 여이를 설정할 수 있습니다.

```fsharp
property-name = property-value
```

이러한 속성 초기화는 순서에 제한이 없지만 위치 인수를 따라야 합니다. 다음은 위치 인수 및 속성 초기화를 사용 하는 특성의 예입니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6202.fs)]

이 예제에서 특성은 축약 된 `DllImportAttribute`형식으로 사용 됩니다. 첫 번째 인수는 위치 매개 변수이 고, 두 번째 인수는 속성입니다.

특성은 *특성* 으로 알려진 개체가 형식 또는 다른 프로그램 요소와 연결 될 수 있도록 하는 .net 프로그래밍 구문입니다. 특성이 적용 되는 program 요소를 *특성 대상*이라고 합니다. 특성은 일반적으로 대상에 대 한 메타 데이터를 포함 합니다. 이 컨텍스트에서 메타 데이터는 필드 및 멤버 이외의 형식에 대 한 모든 데이터가 될 수 있습니다.

의 F# 특성은 함수, 메서드, 어셈블리, 모듈, 형식 (클래스, 레코드, 구조체, 인터페이스, 대리자, 열거형, 공용 구조체 등), 생성자, 속성, 필드와 같은 프로그래밍 구문에 적용 될 수 있습니다. 매개 변수, 형식 매개 변수 및 반환 값을 반환 합니다. 클래스, 식 또는 워크플로 `let` 식 내의 바인딩에는 특성을 사용할 수 없습니다.

일반적으로 특성 선언은 특성 대상의 선언 바로 앞에 표시 됩니다. 다음과 같이 여러 특성 선언을 함께 사용할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6603.fs)]

.NET 리플렉션을 사용 하 여 런타임에 특성을 쿼리할 수 있습니다.

앞의 코드 예제와 같이 여러 특성을 개별적으로 선언 하거나, 세미콜론을 사용 하 여 개별 특성 및 생성자를 구분 하는 경우 한 개의 대괄호 집합에서 다음과 같이 여러 특성을 선언할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6604.fs)]

`Obsolete` 일반적으로 특성, 보안 고려 사항에 대 한 특성, COM 지원에 대 한 특성, 코드의 소유권과 관련 된 특성, 형식을 serialize 할 수 있는지 여부를 나타내는 특성 등이 있습니다. 다음 예제에서는 `Obsolete` 특성을 사용 하는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6605.fs)]

특성 대상 `assembly` 및 `module`의 경우 어셈블리의 최상위 `do` 바인딩에 특성을 적용 합니다. 다음과 같이 특성 선언에 `assembly` 또는 `module` 이라는 단어를 포함할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6606.fs)]

`do` 바인딩에 적용 된 특성에 대 한 특성 대상을 생략 하면 컴파일러는 F# 해당 특성에 적합 한 특성 대상을 확인 하려고 합니다. 많은 특성 클래스에는 해당 특성에 `System.AttributeUsageAttribute` 대해 지원 되는 가능한 대상에 대 한 정보를 포함 하는 형식의 특성이 있습니다. 이 특성이 함수를 대상으로 지원함을 나타내는경우에는해당특성이프로그램의주진입점에적용됩니다.`System.AttributeUsageAttribute` 이 특성이 어셈블리를 대상으로 지원 함을나타내면컴파일러가어셈블리에적용할특성을사용합니다.`System.AttributeUsageAttribute` 대부분의 특성은 함수 및 어셈블리에 모두 적용 되지 않지만, 이러한 특성을 사용 하는 경우에는 프로그램의 main 함수에 특성을 적용 하는 데 사용 됩니다. 특성 대상이 명시적으로 지정 된 경우 특성이 지정 된 대상에 적용 됩니다.

일반적으로 특성 대상을 명시적으로 지정할 필요는 없지만 특성의 *target* 에 대 한 유효한 값을 사용 예제와 함께 사용 하는 방법은 다음과 같습니다.

<table>
  <tr>
    <th>특성 대상</td>
    <th>예제</td> 
  </tr>
  <tr>
    <td>어셈블리(assembly)</td>
    <td><pre lang="fsharp"><code>[&lt;assembly: AssemblyVersionAttribute("1.0.0.0")&gt;]</code></pre></td> 
  </tr>
  <tr>
    <td>반환값(return)</td>
    <td><pre lang="fsharp"><code>let function1 x : [&lt;return: Obsolete&gt;] int = x + 1</code></pre></td> 
  </tr>
  <tr>
    <td>필드</td>
    <td><pre lang="fsharp"><code>[&lt;field: DefaultValue&gt;] val mutable x: int</code></pre></td> 
  </tr>
  <tr>
    <td>속성</td>
    <td><pre lang="fsharp"><code>[&lt;property: Obsolete&gt;] this.MyProperty = x</code></pre></td> 
  </tr>
  <tr>
    <td>매개변수(param)</td>
    <td><pre lang="fsharp"><code>member this.MyMethod([&lt;param: Out&gt;] x : ref&lt;int&gt;) = x := 10</code></pre></td> 
  </tr>
  <tr>
    <td>type</td>
    <td>
        <pre lang="fsharp"><code>
[&lt;type: StructLayout(Sequential)&gt;] 
type MyStruct = 
struct 
x : byte
y : int
end</code></pre>
    </td>
  </tr>
</table>

## <a name="see-also"></a>참조

- [F# 언어 참조](index.md)
