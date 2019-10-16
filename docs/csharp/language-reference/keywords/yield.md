---
title: yield 상황별 키워드 - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- yield
- yield_CSharpKeyword
helpviewer_keywords:
- yield keyword [C#]
ms.assetid: 1089194f-9e53-46a2-8642-53ccbe9d414d
ms.openlocfilehash: 0d2c3f67715b9b2161a6c908576ac9f964ff13d6
ms.sourcegitcommit: 30a83efb57c468da74e9e218de26cf88d3254597
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2019
ms.locfileid: "68363120"
---
# <a name="yield-c-reference"></a>yield(C# 참조)

문에 `yield` [상황별 키워드](index.md#contextual-keywords)를 사용하는 경우 해당 메서드, 연산자, 또는 이 키워드가 나타나는 `get` 접근자가 반복기임을 나타냅니다. `yield`를 사용하여 반복기를 정의할 경우 사용자 지정 컬렉션 형식에 <xref:System.Collections.Generic.IEnumerator%601> 및 <xref:System.Collections.IEnumerable> 패턴을 구현하면 명시적 추가 클래스(열거형의 상태를 보관하는 클래스, 예제는 <xref:System.Collections.IEnumerator> 참조)를 사용하지 않아도 됩니다.

다음 예제에서는 두 가지 형태의 `yield` 문을 보여줍니다.

```csharp
yield return <expression>;
yield break;
```

## <a name="remarks"></a>설명

`yield return` 문을 사용하여 각 요소를 따로따로 반환할 수 있습니다.

반복기 메서드에서 반환된 시퀀스는 [foreach](foreach-in.md) 문 또는 LINQ 쿼리를 통해 사용할 수 있습니다. 각각의 `foreach` 루프의 반복이 반복기 메서드를 호출합니다. `yield return` 문이 반복기 메서드에 도달하면 `expression` 이 반환되고 코드에서 현재 위치는 유지됩니다. 다음에 반복기 함수가 호출되면 해당 위치에서 실행이 다시 시작됩니다.

`yield break` 문을 사용하여 반복기를 종료할 수 있습니다.

반복기에 대한 자세한 내용은 [반복기](../../iterators.md)를 참조하세요.

## <a name="iterator-methods-and-get-accessors"></a>반복기 메서드 및 Get 접근자

반복기 선언은 다음과 같은 요구 사항을 충족해야 합니다.

- 반환 형식은 <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator>, 또는 <xref:System.Collections.Generic.IEnumerator%601>여야 합니다.

- 선언에 [in](in-parameter-modifier.md) [ref](ref.md) 또는 [out](out-parameter-modifier.md) 매개 변수가 허용되지 않습니다.

`yield` 또는 <xref:System.Collections.IEnumerable>를 반환하는 반복기의 <xref:System.Collections.IEnumerator> 형식은 `object`입니다.  반복기가 <xref:System.Collections.Generic.IEnumerable%601> 또는 <xref:System.Collections.Generic.IEnumerator%601>를 반환할 경우 `yield return` 문의 식 형식에서 제네릭 형식 매개 변수로 암시적 변환이 있어야 합니다.

`yield return` 또는 `yield break` 식을

- [람다 식](../../programming-guide/statements-expressions-operators/lambda-expressions.md) 및 [무명 메서드](../operators/delegate-operator.md)에 포함할 수 없습니다.

- 안전하지 않은 블록을 포함하는 메서드 자세한 내용은 [unsafe](unsafe.md)를 참조하세요.

## <a name="exception-handling"></a>예외 처리

`yield return` 문은 try-catch 블록에서 찾을 수 없습니다. `yield return` 문은 try-finally 문의 try 블록에서 찾을 수 있습니다.

`yield break` 문은 try 블록이나 catch 블록에서 찾을 수 있지만 finally 블록에서는 찾을 수 없습니다.

`foreach` 본문(반복기 메서드 외부)에서 예외를 throw한 경우, 반복기 메서드의 `finally` 블록이 실행됩니다.

## <a name="technical-implementation"></a>기술 구현

다음 코드는 반복기 메서드에서 `IEnumerable<string>`을 반환하고 해당 요소를 반복합니다.

```csharp
IEnumerable<string> elements = MyIteratorMethod();
foreach (string element in elements)
{
   ...
}
```

`MyIteratorMethod` 호출은 메서드의 본문을 실행하지 않습니다. 대신에 `IEnumerable<string>` 변수에 `elements`을 반환합니다.

`foreach` 루프 반복에서 <xref:System.Collections.IEnumerator.MoveNext%2A>에 대한 `elements` 메서드가 호출됩니다. 이 호출은 다음 `MyIteratorMethod` 문에 도달할 때까지 `yield return` 본문을 실행합니다. `yield return` 문에서 반환하는 식은 루프 본문에서 사용하는 `element` 변수 값뿐만 아니라 `IEnumerable<string>`인 `elements`의 <xref:System.Collections.Generic.IEnumerator%601.Current%2A> 속성도 결정합니다.

이후에 `foreach` 루프가 반복될 때마다 중지되었던 위치에서 반복기 본문 실행이 계속되고 `yield return` 문에 도달하면 다시 중지됩니다. `foreach` 루프는 반복기 메서드가 종료되거나 `yield break` 문에 도달하면 완료됩니다.

## <a name="example"></a>예

다음 예제에는 `yield return` 루프 내에 `for` 문이 있습니다. `Main` 메서드에서 `foreach` 문의 본문을 반복할 때마다 `Power` 반복기 함수에 대한 호출이 생성됩니다. 반복기 함수를 호출할 때마다 다음에 `yield return` 루프를 반복하는 도중에 `for` 문이 실행됩니다.

반복기 메서드의 반환 형식은 반복기 인터페이스 형식인 <xref:System.Collections.IEnumerable>입니다. 반복기 메서드가 호출되면 숫자의 거듭제곱이 들어 있는 열거형 개체를 반환합니다.

[!code-csharp[csrefKeywordsContextual#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsContextual/CS/csrefKeywordsContextual.cs#5)]

## <a name="example"></a>예

다음 예제는 반복기인 `get` 접근자에 대해 설명합니다. 이 예제에서는 각 `yield return` 문이 사용자 정의 클래스의 인스턴스를 반환합니다.

[!code-csharp[csrefKeywordsContextual#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsContextual/CS/csrefKeywordsContextual.cs#21)]

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../../language-reference/index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [foreach, in](foreach-in.md)
- [반복기](../../iterators.md)
