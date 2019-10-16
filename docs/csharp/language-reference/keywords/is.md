---
title: is - C# 참조
ms.custom: seodec18
ms.date: 06/21/2019
f1_keywords:
- is_CSharpKeyword
- is
helpviewer_keywords:
- is keyword [C#]
ms.assetid: bc62316a-d41f-4f90-8300-c6f4f0556e43
ms.openlocfilehash: a04105137fad7cd3a25b869c3aa7fcbe91ed20ab
ms.sourcegitcommit: 29a9b29d8b7d07b9c59d46628da754a8bff57fa4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2019
ms.locfileid: "69566315"
---
# <a name="is-c-reference"></a>is(C# 참조)

`is` 연산자는 식의 결과가 지정된 형식과 호환되는지 확인하거나, (C# 7.0부터) 패턴에 대해 식을 테스트합니다. 형식 테스트 `is` 연산자에 대한 자세한 내용은 [형식 테스트 및 캐스트 연산자](../operators/type-testing-and-cast.md) 문서의 [is 연산자](../operators/type-testing-and-cast.md#is-operator) 섹션을 참조하세요.

## <a name="pattern-matching-with-is"></a>`is`를 사용한 패턴 일치

C# 7.0부터는 `is` 및 [switch](switch.md) 문에서 패턴 일치를 지원합니다. `is` 키워드는 다음과 같은 패턴을 지원합니다.

- [형식 패턴](#type-pattern) - 식을 지정된 형식으로 변환할 수 있는지를 테스트하고, 변환할 수 있으면 해당 형식의 변수로 캐스트합니다.

- [상수 패턴](#constant-pattern) - 식이 지정된 상수 값으로 평가되는지 여부를 테스트합니다.

- [var 패턴](#var-pattern) - 항상 성공하고 식의 값을 새 로컬 변수에 바인딩하는 일치입니다.

### <a name="type-pattern"></a>형식 패턴

형식 패턴을 사용하여 패턴 일치를 수행하는 경우 `is`는 식을 지정된 형식으로 변환할 수 있는지 여부를 테스트하고, 변환할 수 있으면 해당 형식의 변수로 캐스트합니다. 간결한 형식 평가 및 변환을 사용하는 `is` 문의 간단한 확장입니다. `is` 형식 패턴의 일반적인 형식은 다음과 같습니다.

```csharp
   expr is type varname
```

여기서 *expr*은 일부 형식의 인스턴스로 평가되는 식이고 *type*은 *expr*의 결과가 변환될 형식의 이름이며 *varname*은 `is` 테스트가 `true`인 경우 *expr*의 결과가 변환되는 개체입니다. 

*expr*이 `null`이 아니고 다음 중 하나가 true일 경우 `is` 식은 `true`입니다.

- *expr*이 *type*과 동일한 형식의 인스턴스입니다.

- *expr*이 *type*에서 파생된 형식의 인스턴스입니다. 즉, *expr*의 결과를 *type*의 인스턴스로 업캐스트할 수 있습니다.

- *expr*의 컴파일 시간 형식은 *type*의 기본 클래스이고 *expr*의 런타임 형식은 *type*이거나 *type*에서 파생됩니다. 변수의 *컴파일 시간 형식*은 해당 선언에 정의된 변수의 형식입니다. 변수의 *런타임 형식*은 해당 변수에 할당된 인스턴스의 형식입니다.

- *expr*이 *type* 인터페이스를 구현하는 형식의 인스턴스입니다.

C# 7.1부터 *expr*은 제네릭 형식 매개 변수 및 해당 제약 조건을 통해 컴파일 시간 형식을 정의할 수 있습니다.

*expr*이 `true`이고 `is`가 `if` 문에서 사용되는 경우 *varname*이 `if` 문 내에서만 할당됩니다. *varname*의 범위는 `is` 식에서부터 `if` 문을 닫는 블록의 끝까지입니다. 다른 위치에서 *varname*을 사용하여 할당되지 않은 변수 사용에 대한 컴파일 시간 오류를 생성합니다.

다음 예제에서는 `is` 형식 패턴을 사용하여 형식의 <xref:System.IComparable.CompareTo(System.Object)?displayProperty=nameWithType> 메서드 구현을 제공합니다.

[!code-csharp[is#5](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern5.cs#5)]

패턴 일치를 사용하지 않을 경우 이 코드를 다음과 같이 작성할 수 있습니다. 형식 패턴 일치를 사용하면 변환 결과가 `null`인지 여부를 테스트할 필요가 없으므로 보다 간결하고 읽기 쉬운 코드가 생성됩니다.  

[!code-csharp[is#6](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern6.cs#6)]

또한 `is` 형식 패턴은 값 형식의 형식을 확인할 때 보다 간결한 코드를 생성합니다. 다음 예제에서는 `is` 형식 패턴을 사용하여 개체가 `Person` 인스턴스인지 `Dog` 인스턴스인지를 확인한 후 적절한 속성의 값을 표시합니다.

[!code-csharp[is#9](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern9.cs#9)]

패턴 일치를 사용하지 않는 동일한 코드에는 명시적 캐스트를 포함하는 별도의 할당이 필요합니다.

[!code-csharp[is#10](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern10.cs#10)]

### <a name="constant-pattern"></a>상수 패턴

상수 패턴을 사용한 패턴 일치를 수행하는 경우 `is`는 식이 지정된 상수와 같은지 여부를 테스트합니다. C# 6 이전 버전에서는 상수 패턴이 [switch](switch.md) 문에서 지원됩니다. C# 7.0부터는 `is` 문에서도 지원됩니다. 사용되는 구문은 다음과 같습니다.

```csharp
   expr is constant
```

여기서 *expr*은 평가할 식이고 *constant*는 테스트할 값입니다. *constant*는 다음 상수 식 중 하나가 될 수 있습니다.

- 리터럴 값.

- 선언된 `const` 변수의 이름.

- 열거형 상수.

상수 식은 다음과 같이 계산됩니다.

- *expr* 및 *constant*가 정수 형식인 경우 C# 같음 연산자는 식에서 `true`를 반환하는지 여부 즉, `expr == constant`인지 여부를 확인합니다.

- 정수 형식이 아닌 경우 정적 [Object.Equals(expr, constant)](xref:System.Object.Equals(System.Object,System.Object)) 메서드 호출을 통해 식의 값이 결정됩니다.  

다음 예제에서는 형식 패턴과 상수 패턴을 결합하여 개체가 `Dice` 인스턴스인지 여부를 테스트하고, 그럴 경우 주사위 굴리기 값이 6인지 여부를 확인합니다.

[!code-csharp[is#7](../../../../samples/snippets/csharp/language-reference/keywords/is/is-const-pattern7.cs#7)]

상수 패턴을 사용하여 `null`을 검사할 수 있습니다. `null` 키워드는 `is` 문에서 지원됩니다. 사용되는 구문은 다음과 같습니다.

```csharp
   expr is null
```

다음 예제는 `null` 검사의 비교를 보여 줍니다.

[!code-csharp[is#11](../../../../samples/snippets/csharp/language-reference/keywords/is/is-const-pattern11.cs#11)]

### <a name="var-pattern"></a>var 패턴

`var` 패턴은 모든 형식 또는 값에 대해 catch-all입니다. *expr*의 값은 항상 *expr*의 컴파일 시간 형식과 동일한 형식의 지역 변수에 할당됩니다. `is` 식의 결과는 항상 `true`입니다. 사용되는 구문은 다음과 같습니다.

```csharp
   expr is var varname
```

다음 예제에서는 var 패턴을 사용하여 `obj`라는 변수에 식을 할당합니다. 그런 다음 `obj`의 값과 형식을 표시합니다.

[!code-csharp[is#8](../../../../samples/snippets/csharp/language-reference/keywords/is/is-var-pattern8.cs#8)]

## <a name="c-language-specification"></a>C# 언어 사양
  
자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [s 연산자](~/_csharplang/spec/expressions.md#the-is-operator) 섹션과 다음 C# 언어 제안을 참조하세요.

- [패턴 일치](~/_csharplang/proposals/csharp-7.0/pattern-matching.md)
- [제네릭과 일치하는 패턴](~/_csharplang/proposals/csharp-7.1/generics-pattern-match.md)
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 키워드](index.md)
- [형식 테스트 및 캐스트 연산자](../operators/type-testing-and-cast.md)
