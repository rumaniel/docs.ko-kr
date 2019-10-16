---
title: = 연산자 - C# 참조
ms.custom: seodec18
ms.date: 09/10/2019
f1_keywords:
- =_CSharpKeyword
helpviewer_keywords:
- = operator [C#]
ms.assetid: d802a6d5-32f0-42b8-b180-12f5a081bfc1
ms.openlocfilehash: a450a55524f33f4f06ed077aba864e8f641a458d
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70924653"
---
# <a name="-operator-c-reference"></a>= 연산자(C# 참조)

대입 연산자 `=`은 오른쪽 피연산자의 값을 왼쪽 피연산자가 제공하는 변수, [속성](../../programming-guide/classes-and-structs/properties.md) 또는 [인덱서](../../programming-guide/indexers/index.md) 요소에 할당합니다. 대입식의 결과는 왼쪽 피연산자에 할당된 값입니다. 오른쪽 피연산자의 형식은 왼쪽 피연산자의 형식과 동일하거나 왼쪽 피연산자의 형식으로 암시적으로 변환할 수 있어야 합니다.

대입 연산자는 오른쪽 결합성입니다. 즉, 다음 형식의 식을 가정해 보세요.

```csharp
a = b = c
```

이 식은 다음과 같이 계산됩니다.

```csharp
a = (b = c)
```

다음 예제에서는 로컬 변수, 속성 및 인덱서 요소를 왼쪽 피연산자로 포함해서 대입 연산자를 사용하는 방법을 보여 줍니다.

[!code-csharp-interactive[simple assignment](~/samples/csharp/language-reference/operators/AssignmentOperator.cs#Simple)]

## <a name="ref-assignment-operator"></a>ref 대입 연산자

C# 7.3부터 ref 대입 연산자 `= ref`를 사용하여 [ref 지역](../keywords/ref.md#ref-locals) 또는 [ref readonly 지역](../keywords/ref.md#ref-readonly-locals) 변수를 다시 할당할 수 있습니다. 다음 예제에서는 ref 대입 연산자의 사용법을 보여 줍니다.

[!code-csharp[ref assignment operator](~/samples/csharp/language-reference/operators/AssignmentOperator.cs#RefAssignment)]

ref 대입 연산자의 경우 양쪽 피연산자의 형식이 같아야 합니다.

자세한 내용은 [기능 제안 노트](~/_csharplang/proposals/csharp-7.3/ref-local-reassignment.md)를 참조하세요.

## <a name="compound-assignment"></a>복합 할당

이진 연산자(`op`)의 경우 양식의 복합 할당 식

```csharp
x op= y
```

위의 식은 아래의 식과 동일합니다.

```csharp
x = x op y
```

단, `x`가 한 번만 계산됩니다.

복합 할당은 [산술](arithmetic-operators.md#compound-assignment), [부울 논리](boolean-logical-operators.md#compound-assignment), [비트 논리 및 시프트](bitwise-and-shift-operators.md#compound-assignment) 연산자를 통해 지원됩니다.

## <a name="null-coalescing-assignment"></a>null 병합 할당

C# 8.0부터 null 병합 할당 연산자 `??=`를 사용하여 왼쪽 피연산자가 `null`로 계산되는 경우에만 오른쪽 피연산자의 값을 왼쪽 피연산자에 대입할 수 있습니다. 자세한 내용은 [?? 및 ??= 연산자](null-coalescing-operator.md) 문서를 참조하세요.

## <a name="operator-overloadability"></a>연산자 오버로드 가능성

사용자 정의 형식은 대입 연산자를 오버로드할 수 없습니다. 그러나 사용자 정의 형식은 다른 형식으로 암시적 변환을 정의할 수 있습니다. 이렇게 하면 사용자 정의 형식의 값을 다른 형식의 변수, 속성 또는 인덱서 요소에 할당할 수 있습니다. 자세한 내용은 [사용자 정의 변환 연산자](user-defined-conversion-operators.md)를 참조하세요.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](../language-specification/index.md)의 [대입 연산자](~/_csharplang/spec/expressions.md#assignment-operators) 섹션을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 연산자](index.md)
- [ref 키워드](../keywords/ref.md)
