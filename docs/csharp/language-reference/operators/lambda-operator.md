---
title: '>= 연산자 - C# 참조'
ms.custom: seodec18
ms.date: 01/22/2019
f1_keywords:
- =>_CSharpKeyword
helpviewer_keywords:
- lambda operator [C#]
- => operator [C#]
- lambda expressions [C#], => operator
ms.openlocfilehash: 3b3a5c2e96e92271da66cbd8f1039a9ec97544fa
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68971227"
---
# <a name="-operator-c-reference"></a>=> 연산자(C# 참조)

`=>` 토큰은 람다 연산자와 식 본문 정의의 멤버 이름과 멤버 구현의 구분자라는 두 가지 형식으로 지원됩니다.

## <a name="lambda-operator"></a>람다 연산자

[람다 식](../../programming-guide/statements-expressions-operators/lambda-expressions.md)에서 람다 연산자 `=>`은 왼쪽의 입력 변수를 오른쪽의 람다 본문과 구분합니다.

다음 예제에서는 메서드 구문이 포함된 [LINQ](../../programming-guide/concepts/linq/index.md) 기능을 사용하여 람다 식의 사용법을 보여줍니다.

[!code-csharp-interactive[infer types of input variables](~/samples/csharp/language-reference/operators/LambdaOperator.cs#InferredTypes)]

람다 식의 입력 변수는 컴파일 시 강력한 형식을 지정합니다. 위의 예제와 같이 컴파일러가 입력 변수의 형식을 추론하는 경우, 형식 선언을 생략할 수 있습니다. 입력 변수의 형식을 지정해야 하는 경우 다음 예제와 같이 각 변수에 대해 입력 변수를 지정해야 합니다.

[!code-csharp-interactive[specify types of input variables](~/samples/csharp/language-reference/operators/LambdaOperator.cs#ExplicitTypes)]

다음 예제에서는 입력 변수 없이 람다 식을 정의하는 방법을 보여줍니다.

[!code-csharp-interactive[without input variables](~/samples/csharp/language-reference/operators/LambdaOperator.cs#WithoutInput)]

자세한 내용은 [람다 식](../../programming-guide/statements-expressions-operators/lambda-expressions.md)을 참조하세요.

## <a name="expression-body-definition"></a>식 본문 정의

식 본문 정의의 일반 구문은 다음과 같습니다.

```csharp
member => expression;
```

여기서 `expression`은(는) 유효한 식입니다. `expression`의 반환 형식은 구성원의 반환 형식으로 암시적으로 변환할 수 있어야 합니다. 구성원의 반환 형식이 `void`(이)거나 구성원이 생성자, 종료자 또는 속성 `set` 접근자인 경우 `expression`은(는) [*statement 식*](~/_csharplang/spec/statements.md#expression-statements)이어야 하며 모든 형식을 사용할 수 있습니다.

다음 예제에서는 `Person.ToString` 메서드에 대한 식 본문 정의를 보여줍니다.

```csharp
public override string ToString() => $"{fname} {lname}".Trim();
```

다음과 같은 메서드 정의의 약식 버전입니다.

```csharp
public override string ToString()
{
   return $"{fname} {lname}".Trim();
}
```

메서드 및 읽기 전용 속성에 대한 식 본문 정의는 C# 6부터 지원됩니다. 생성자, 종료자, 속성 접근자 및 인덱서에 대한 식 본문 정의는 C# 7.0부터 지원됩니다.

자세한 내용은 [식 본문 멤버](../../programming-guide/statements-expressions-operators/expression-bodied-members.md)를 참조하세요.

## <a name="operator-overloadability"></a>연산자 오버로드 가능성

`=>` 연산자를 오버로드할 수 없습니다.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](../language-specification/index.md)의 [익명 함수 식](~/_csharplang/spec/expressions.md#anonymous-function-expressions) 섹션을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 연산자](index.md)
- [람다 식](../../programming-guide/statements-expressions-operators/lambda-expressions.md)
- [식 본문 멤버](../../programming-guide/statements-expressions-operators/expression-bodied-members.md)
