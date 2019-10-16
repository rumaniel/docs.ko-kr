---
title: throw - C# 참조
ms.custom: seodec18
ms.date: 03/02/2015
f1_keywords:
- throw
- throw_CSharpKeyword
helpviewer_keywords:
- throw statement [C#]
- throw expression [C#]
- throw keyword [C#]
ms.assetid: 5ac4feef-4b1a-4c61-aeb4-61d549e5dd42
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1e3f9ff82bdc4f35232c4ea1162050e216a9cc21
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353423"
---
# <a name="throw-c-reference"></a>throw(C# 참조)

프로그램 실행 중 예외 발생 신호를 보냅니다.  
  
## <a name="remarks"></a>설명

`throw`의 구문은 다음과 같습니다.

```csharp
throw [e];
```

여기서 `e`는 <xref:System.Exception?displayProperty=nameWithType>에서 파생된 클래스의 인스턴스입니다. 다음 예제에서는 `throw` 문을 사용하여 `GetNumber`라는 메서드에 전달된 인수가 내부 배열의 유효한 인덱스에 해당하지 않는 경우  <xref:System.IndexOutOfRangeException> 을 throw합니다.

[!code-csharp[csrefKeyword#1](~/samples/snippets/csharp/language-reference/keywords/throw/throw-1.cs#1)]

그러면 메서드 호출자가 `try-catch` 또는 `try-catch-finally` 블록을 사용하여 throw된 예외를 처리합니다. 다음 예제에서는 `GetNumber` 메서드에 의해 throw된 예외를 처리합니다.

[!code-csharp[csrefKeyword#2](~/samples/snippets/csharp/language-reference/keywords/throw/throw-1.cs#2)]

## <a name="re-throwing-an-exception"></a>예외 다시 throw

`catch` 블록에서 `throw`를 사용하여 `catch` 블록에서 처리된 예외를 다시 throw할 수도 있습니다.  이 경우 `throw`는 예외 피연산자를 사용하지 않습니다. 이는 메서드가 호출자의 인수를 다른 일부 라이브러리 메서드에 전달하고 라이브러리 메서드가 호출자에게 전달되어야 하는 예외를 throw하는 경우에 가장 유용합니다. 예를 들어 다음 예제에서는 초기화되지 않은 문자열의 첫 번째 문자를 검색하려고 할 때 throw되는 <xref:System.NullReferenceException>을 다시 throw합니다.

[!code-csharp[csrefKeyword#3](~/samples/snippets/csharp/language-reference/keywords/throw/throw-3.cs#3)]

> [!IMPORTANT]
> `catch` 블록의 `throw e` 구문을 사용하여 호출자에게 전달하는 새 예외를 인스턴스화할 수도 있습니다. 이 경우 <xref:System.Exception.StackTrace> 속성에서 제공되는 원래 예외의 스택 추적이 유지되지 않습니다.

## <a name="the-throw-expression"></a>`throw` 식

C# 7.0부터 `throw`를 명령문뿐만 아니라 식으로도 사용할 수 있습니다. 이렇게 하면 이전에 지원되지 않은 상황에서 예외를 throw할 수 있습니다. 여기에는 다음이 포함됩니다.

- [조건 연산자](../operators/conditional-operator.md). 다음 예제에서는 `throw` 식을 사용하여 메서드에 빈 문자열 배열이 전달된 경우 <xref:System.ArgumentException>을 throw합니다. C# 7.0 이전에는 이 논리가 `if`/`else` 문에 표시되어야 합니다.

   [!code-csharp[csrefKeyword#4](~/samples/snippets/csharp/language-reference/keywords/throw/conditional.cs#1)]

- [Null 병합 연산자](../operators/null-coalescing-operator.md). 다음 예제에서는 `throw` 식에 Null 병합 연산자를 사용하여 `Name` 속성에 할당된 문자열이 `null`인 경우 예외를 throw합니다.

   [!code-csharp[csrefKeyword#5](~/samples/snippets/csharp/language-reference/keywords/throw/coalescing.cs#1)]

- 식 본문 [람다](../../programming-guide/statements-expressions-operators/lambda-expressions.md) 또는 메서드. 다음 예제에서는 <xref:System.DateTime> 값으로 변환이 지원되지 않기 때문에 <xref:System.InvalidCastException>을 throw하는 식 본문 메서드를 보여 줍니다.

   [!code-csharp[csrefKeyword#6](~/samples/snippets/csharp/language-reference/keywords/throw/exp-bodied.cs#1)]

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [try-catch](try-catch.md)
- [C# 키워드](index.md)
- [방법: 명시적으로 예외 Throw](../../../standard/exceptions/how-to-explicitly-throw-exceptions.md)
