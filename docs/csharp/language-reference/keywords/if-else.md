---
title: if-else - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- if_CSharpKeyword
- else
- else_CSharpKeyword
- if
helpviewer_keywords:
- else keyword [C#]
- if keyword [C#]
ms.assetid: d9a1d562-8cf5-4bd4-9ba7-8ad970cd25b2
ms.openlocfilehash: 18b41446eb13f4b91db86d79316a5299b0f3020a
ms.sourcegitcommit: 621a5f6df00152006160987395b93b5b55f7ffcd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66300473"
---
# <a name="if-else-c-reference"></a>if-else(C# 참조)

`if` 문은 부울 식의 값에 따라 실행할 문을 식별합니다. 다음 예제에서는 `bool` 변수 `condition` 가 `true` 로 설정된 다음 `if` 문에서 확인됩니다. 출력은 `The variable is set to true.`입니다.

[!code-csharp[csrefKeywordsSelection#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsSelection/CS/csrefKeywordsSelection.cs#1)]

콘솔 앱의 `Main` 메서드에 배치하여 이 항목의 예제를 실행할 수 있습니다.

C#의 `if` 문은 다음 예제와 같이 두 가지 형식을 사용할 수 있습니다.

```csharp
// if-else statement
if (condition)
{
    then-statement;
}
else
{
    else-statement;
}
// Next statement in the program.

// if statement without an else
if (condition)
{
    then-statement;
}
// Next statement in the program.
```

`if-else` 문에서 `condition` 이 true로 평가되는 경우 `then-statement` 가 실행됩니다. `condition` 이 false이면 `else-statement` 가 실행됩니다. `condition` 이 true인 동시에 false일 수는 없으므로 `then-statement` 문의 `else-statement` 및 `if-else` 를 둘 다 실행할 수는 없습니다. `then-statement` 또는 `else-statement` 가 실행된 후 제어가 `if` 문 뒤의 다음 문으로 전송됩니다.

`if` 문을 포함하지 않는 `else` 문에서 `condition` 이 true이면 `then-statement` 가 실행됩니다. `condition` 이 false이면 제어가 `if` 문 뒤의 다음 문으로 전송됩니다.

`then-statement` 및 `else-statement` 는 둘 다 단일 문이나 중괄호(`{}`)로 묶인 여러 문으로 구성될 수 있습니다. 단일 문의 경우 중괄호는 선택 사항이지만 권장됩니다.

`then-statement` 및 `else-statement` 의 문은 원래 `if` 문 내부에 중첩된 다른 `if` 문을 포함하여 모든 종류일 수 있습니다. 중첩된 `if` 문에서 각 `else` 절은 해당 `if` 가 없는 마지막 `else`에 속합니다. 다음 예제에서 `Result1` 및 `m > 10` 이 둘 다 true이면 `n > 20` 이 나타납니다. `m > 10` 이 true이지만 `n > 20` 이 false이면 `Result2` 가 나타납니다.

[!code-csharp[csrefKeywordsSelection#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsSelection/CS/csrefKeywordsSelection.cs#2)]

`Result2` 이 false일 때 `(m > 10)` 를 대신 표시하려는 경우 다음 예제와 같이 중괄호로 중첩된 `if` 문의 시작 및 끝을 설정하여 해당 연결을 지정할 수 있습니다.

[!code-csharp[csrefKeywordsSelection#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsSelection/CS/csrefKeywordsSelection.cs#3)]

조건 `(m > 10)`이 false이면 `Result2`가 나타납니다.

## <a name="example"></a>예제

다음 예제에서는 키보드에서 문자 하나를 입력하며, 프로그램이 중첩된 `if` 문을 사용하여 입력 문자가 영문자인지 여부를 확인합니다. 입력 문자가 영문자이면 프로그램에서 입력 문자가 소문자인지 대문자인지를 확인합니다. 각 경우에 대한 메시지가 나타납니다.

[!code-csharp[csrefKeywordsSelection#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsSelection/CS/csrefKeywordsSelection.cs#4)]

## <a name="example"></a>예제

다음 부분 코드와 같이 `if` 문을 else 블록 안에 중첩할 수도 있습니다. 예제에서는 `if` 문을 else 블록 2개와 then 블록 1개 안에 중첩합니다. 주석은 각 블록에서 true 또는 false인 조건을 지정합니다.

[!code-csharp[csrefKeywordsSelection#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsSelection/CS/csrefKeywordsSelection.cs#5)]

## <a name="example"></a>예제

다음 예제에서는 입력 문자가 소문자, 대문자 또는 숫자인지를 확인합니다. 세 가지 조건이 모두 false이면 문자는 영숫자 문자가 아닙니다. 예제에서는 각 경우에 대한 메시지가 표시됩니다.

[!code-csharp[csrefKeywordsSelection#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsSelection/CS/csrefKeywordsSelection.cs#6)]

else 블록 또는 then 블록의 문이 유효한 모든 문일 수 있는 것과 마찬가지로 유효한 모든 부울 식을 조건에 대해 사용할 수 있습니다. `!`, `&&`, `||`, `&`, `|` 및 `^`와 같은 [논리 연산자](../operators/boolean-logical-operators.md)를 사용하여 복합 조건을 만들 수 있습니다. 다음 코드는 예제를 보여 줍니다.

```csharp
// NOT
bool result = true;
if (!result)
{
    Console.WriteLine("The condition is true (result is false).");
}
else
{
    Console.WriteLine("The condition is false (result is true).");
}

// Short-circuit AND
int m = 9;
int n = 7;
int p = 5;
if (m >= n && m >= p)
{
    Console.WriteLine("Nothing is larger than m.");
}

// AND and NOT
if (m >= n && !(p > m))
{
    Console.WriteLine("Nothing is larger than m.");
}

// Short-circuit OR
if (m > n || m > p)
{
    Console.WriteLine("m isn't the smallest.");
}

// NOT and OR
m = 4;
if (!(m >= n || m >= p))
{
    Console.WriteLine("Now m is the smallest.");
}
// Output:
// The condition is false (result is true).
// Nothing is larger than m.
// Nothing is larger than m.
// m isn't the smallest.
// Now m is the smallest.
```

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [?: 연산자](../operators/conditional-operator.md)
- [if-else 문(C++)](/cpp/cpp/if-else-statement-cpp)
- [switch](switch.md)
