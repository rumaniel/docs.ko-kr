---
title: in 매개 변수 한정자 - C# 참조
ms.custom: seodec18
ms.date: 03/26/2019
helpviewer_keywords:
- parameters [C#], in
- in parameters [C#]
ms.openlocfilehash: e39d470308ed5a2b2ed82ade0faf8ba925228c2c
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59112647"
---
# <a name="in-parameter-modifier-c-reference"></a>in 매개 변수 한정자(C# 참조)

`in` 키워드를 사용하면 참조를 통해 인수를 전달할 수 있습니다. 이 키워드는 정식 매개 변수를 변수여야 하는 인수의 별칭으로 설정합니다. 즉, 매개 변수에 대한 모든 작업이 인수에서 수행됩니다. 이 키워드는 호출된 메서드에서 `in` 인수를 수정할 수 없다는 점을 제외하고 [ref](ref.md) 또는 [out](out-parameter-modifier.md) 키워드와 유사합니다. `ref` 인수는 수정할 수 있지만 `out` 인수는 호출된 메서드가 수정해야 하며, 해당 수정 사항은 호출 컨텍스트에서 식별 가능합니다.

[!code-csharp-interactive[cs-in-keyword](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/InParameterModifier.cs#1)]  

앞의 예제는 호출 사이트에서 일반적으로 `in` 한정자가 필요하지 않다는 것을 설명합니다. 메서드 선언에만 필요합니다.

> [!NOTE] 
> `in` 키워드는 `foreach` 명령문의 일부 또는 LINQ 쿼리에서 `join` 절의 일부로 형식 매개 변수가 반공변(contravariant)임을 지정하도록 제네릭 형식 매개 변수와 함께 사용될 수도 있습니다. 이러한 컨텍스트에서 `in` 키워드의 사용에 대한 자세한 내용은 모든 해당 사용에 대한 링크를 제공하는 [in](in.md)을 참조하세요.
  
`in` 인수로 전달되는 변수는 메서드 호출에서 전달되기 전에 초기화되어야 합니다. 그러나 호출된 메서드는 값을 할당하거나 인수를 수정하지 않을 수 있습니다.  

`in` 매개 변수 한정자는 C# 7.2 이상에서 사용 가능합니다. 이전 버전은 컴파일러 오류 `CS8107`(“C# 7.0에서는 ’읽기 전용 참조’ 기능을 사용할 수 없습니다. 언어 버전 7.2 이상을 사용하세요.”)을 생성합니다. 컴파일러 언어 버전을 구성하려면 [C# 언어 버전 선택](../configure-language-version.md)을 참조하세요.

`in`, `ref` 및 `out` 키워드는 오버로드 해결을 위한 메서드 시그니처의 일부로 간주되지 않습니다. 따라서 메서드 하나는 `ref` 또는 `in` 인수를 사용하고 다른 하나는 `out` 인수를 사용한다는 것 외에는 차이점이 없으면 메서드를 오버로드할 수 없습니다. 예를 들어 다음 코드는 컴파일되지 않습니다.  
  
```csharp
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded 
    // methods that differ only on in, ref and out".
    public void SampleMethod(in int i) { }
    public void SampleMethod(ref int i) { }
}
```
  
`in`의 존재에 기반한 오버로딩이 허용됩니다.  
  
```csharp
class InOverloads
{
    public void SampleMethod(in int i) { }
    public void SampleMethod(int i) { }
}
```

## <a name="overload-resolution-rules"></a>오버로드 해결 규칙

`in` 인수에 대한 동기를 이해하여 값과 `in` 인수로 메서드의 오버로드 해결 규칙을 이해할 수 있습니다. `in` 매개 변수를 사용하여 메서드를 정의하면 잠재적인 성능 최적화가 이루어집니다. 일부 `struct` 형식 인수는 크기가 클 수 있으며 긴밀한 루프 또는 중요한 코드 경로에서 메서드를 호출할 때 해당 구조를 복사하는 비용이 중요합니다. 메서드는 호출된 메서드가 인수의 상태를 수정하지 않으므로 `in` 매개 변수를 선언하여 해당 인수가 참조로 안전하게 전달될 수 있음을 지정합니다. 이러한 인수를 참조로 전달하면 (잠재적으로) 비용이 많이 드는 복사본을 방지할 수 있습니다. 

호출 사이트의 인수에 `in`을 지정하는 것은 일반적으로 선택 사항입니다. 값으로 인수를 전달하고 `in` 한정자를 사용하여 인수를 전달하는 것 사이에는 의미 체계상 차이가 없습니다. 호출 사이트의 `in` 한정자는 인수 값이 변경될 수 있음을 나타내지 않아도 되므로 선택 사항입니다. 호출 사이트에서 `in` 한정자를 명시적으로 추가하여 인수가 값이 아닌 참조로 전달되도록 합니다. 명시적으로 `in`을 사용하는 경우 다음과 같은 두 가지 효과가 있습니다.

먼저 호출 사이트에서 `in`을 지정하면 컴파일러가 일치하는 `in` 매개 변수로 정의된 메서드를 선택하게 됩니다. 그렇지 않으면 두 메서드가 `in`이 있을 때만 다른 경우 by 값 오버로드가 더 적합합니다.

둘째, `in`을 지정하면 참조로 인수를 전달할 의사가 있음을 선언하는 것입니다. `in`에 사용된 인수는 직접 참조할 수 있는 위치를 나타내야 합니다. `out` 및 `ref` 인수에는 동일한 일반 규칙이 적용됩니다. 상수, 일반 속성 또는 값을 생성하는 다른 식은 사용할 수 없습니다. 그렇지 않으면 호출 사이트에서 `in`을 생략할 경우 메서드에 대한 읽기 전용 참조로 전달할 임시 변수를 만들 수 있도록 컴파일러에 알립니다. 컴파일러는 `in` 인수를 사용하여 몇 가지 제한 사항을 해결하기 위해 임시 변수를 만듭니다.

- 임시 변수는 컴파일 시간 상수를 `in` 매개 변수로 허용합니다.
- 임시 변수는 속성 또는 `in` 매개 변수에 대한 다른 식을 허용합니다.
- 임시 변수는 인수 형식에서 매개 변수 형식으로의 암시적 변환이 있는 경우 인수를 허용합니다.

앞의 모든 인스턴스에서 컴파일러는 상수, 속성 또는 다른 식의 값을 저장하는 임시 변수를 만듭니다.

다음 코드에서는 이러한 규칙을 보여줍니다.

```csharp
static void Method(in int argument)
{
    // implementation removed
}

Method(5); // OK, temporary variable created.
Method(5L); // CS1503: no implicit conversion from long to int
short s = 0;
Method(s); // OK, temporary int created with the value 0
Method(in s); // CS1503: cannot convert from in short to in int
int i = 42;
Method(i); // passed by readonly reference
Method(in i); // passed by readonly reference, explicitly using `in`
```

이제 by 값 인수를 사용하는 다른 메서드를 사용할 수 있다고 가정하겠습니다. 결과는 다음 코드와 같이 변경됩니다.

```csharp
static void Method(int argument)
{
    // implementation removed
}

static void Method(in int argument)
{
    // implementation removed
}

Method(5); // Calls overload passed by value
Method(5L); // CS1503: no implicit conversion from long to int
short s = 0;
Method(s); // Calls overload passed by value.
Method(in s); // CS1503: cannot convert from in short to in int
int i = 42;
Method(i); // Calls overload passed by value
Method(in i); // passed by readonly reference, explicitly using `in`
```

인수가 참조로 전달되는 유일한 메서드 호출이 마지막입니다.

> [!NOTE]
> 앞의 코드는 단순화를 위해 인수 형식으로 `int`를 사용합니다. `int`는 대부분의 최신 컴퓨터에서 참조보다 크지 않기 때문에 단일 `int`를 읽기 전용 참조로 전달하면 아무런 이점이 없습니다. 

## <a name="limitations-on-in-parameters"></a>`in` 매개 변수에 대한 제한 사항

다음과 같은 종류의 메서드에는 `in`, `ref` 및 `out` 키워드를 사용할 수 없습니다.  
  
- [async](async.md) 한정자를 사용하여 정의하는 비동기 메서드  
- [yield return](yield.md) 또는 `yield break` 문을 포함하는 반복기 메서드  

## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [메서드 매개 변수](method-parameters.md)
- [안전하고 효율적인 코드 작성](../../write-safe-efficient-code.md)
