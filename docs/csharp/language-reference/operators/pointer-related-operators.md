---
title: 포인터 관련 연산자 - C# 참조
description: 포인터로 작업할 때 사용할 수 있는 C# 연산자에 대해 알아봅니다.
ms.date: 05/20/2019
author: pkulikov
f1_keywords:
- ->_CSharpKeyword
helpviewer_keywords:
- pointer related operators [C#]
- address-of operator [C#]
- '& operator [C#]'
- pointer indirection operator [C#]
- dereference operator [C#]
- '* operator [C#]'
- pointer member access operator [C#]
- -> operator [C#]
- pointer element access [C#]
- '[] operator [C#]'
- pointer arithmetic [C#]
- pointer increment [C#]
- pointer decrement [C#]
- pointer comparison [C#]
ms.openlocfilehash: 830aef8546191df3df4a70e350ba561367a9e474
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68512348"
---
# <a name="pointer-related-operators-c-reference"></a>포인터 관련 연산자(C# 참조)

다음 연산자를 사용하여 포인터로 작업할 수 있습니다.

- 단항 [`&`(address-of)](#address-of-operator-) 연산자: 변수의 주소를 가져오려면
- 단항 [`*`(포인터 간접 참조)](#pointer-indirection-operator-) 연산자: 포인터가 가리키는 변수를 가져오려면
- [`->`(멤버 액세스)](#pointer-member-access-operator--) 및 [`[]`(요소 액세스)](#pointer-element-access-operator-) 연산자
- 산술 연산자 [`+`, `-`, `++` 및 `--`](#pointer-arithmetic-operators)
- 비교 연산자 [`==`, `!=`, `<`, `>`, `<=` 및 `>=`](#pointer-comparison-operators)

포인터 형식에 대한 내용은 [포인터 형식](../../programming-guide/unsafe-code-pointers/pointer-types.md)을 참조하세요.

> [!NOTE]
> 포인터를 사용한 작업에는 [안전하지 않은](../keywords/unsafe.md) 컨텍스트가 필요합니다. 안전하지 않은 블록을 포함하는 코드는 [`-unsafe`](../compiler-options/unsafe-compiler-option.md) 컴파일러 옵션으로 컴파일해야 합니다.

## <a name="address-of-operator-"></a> Address-of 연산자 &amp;

단항 `&` 연산자는 해당 피연산자의 주소를 반환합니다.

[!code-csharp[address of local](~/samples/csharp/language-reference/operators/PointerOperators.cs#AddressOf)]

`&` 연산자의 피연산자는 고정 변수여야 합니다. *고정* 변수는 [가비지 수집기](../../../standard/garbage-collection/index.md)의 작동에 영향을 받지 않는 스토리지 위치에 있는 변수입니다. 앞의 예제에서 로컬 변수 `number`는 스택에 있으므로 고정 변수입니다. 가비지 수집기에 의해 영향을 받을 수 있는 스토리지 위치에 상주하는 변수(예: 재배치됨)를 *이동 가능한* 변수라고 합니다. 개체 필드 및 배열 요소는 이동 가능한 변수의 예입니다. [고정](../keywords/fixed-statement.md) 문으로 "fix" 또는 "pin"으로 할 경우 이동 가능한 변수의 주소를 가져올 수 있습니다. 가져온 주소는 `fixed` 문 블록의 기간 동안에만 유효합니다. 다음 예제에서는 `fixed` 문과 `&` 연산자를 사용하는 방법을 보여줍니다.

[!code-csharp[address of fixed](~/samples/csharp/language-reference/operators/PointerOperators.cs#AddressOfFixed)]

상수 또는 값의 주소를 가져올 수 없습니다.

고정 및 이동 가능한 변수에 대한 자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [고정 및 이동 가능 변수](~/_csharplang/spec/unsafe-code.md#fixed-and-moveable-variables) 섹션을 참조하세요.

이진 `&` 연산자는 해당 부울 피연산자의 [논리 AND](boolean-logical-operators.md#logical-and-operator-) 또는 해당 정수 피연산자의 [비트 논리 AND](bitwise-and-shift-operators.md#logical-and-operator-)를 컴퓨팅합니다.

## <a name="pointer-indirection-operator-"></a>포인터 간접 참조 연산자 *

단항 포인터 간접 참조 연산자 `*`는 피연산자가 가리키는 변수를 가져옵니다. 역참조 연산자라고도 합니다. `*` 연산자의 피연산자는 포인터 형식이여야 합니다.

[!code-csharp[pointer indirection](~/samples/csharp/language-reference/operators/PointerOperators.cs#PointerIndirection)]

`*` 연산자를 `void*` 유형의 식에 적용할 수 없습니다.

이진 `*` 연산자는 해당 숫자 피연산자의 [곱](arithmetic-operators.md#multiplication-operator-)을 컴퓨팅합니다.

## <a name="pointer-member-access-operator--"></a>포인터 멤버 액세스 연산자 ->

`->` 연산자는 포인터 [간접 참조](#pointer-indirection-operator-)와 [멤버 액세스](member-access-operators.md#member-access-operator-)를 결합합니다. 즉, `x`가 `T*` 형식의 포인터이고 `y`가 `T`의 액세스 가능한 멤버인 경우 양식의 식은

```csharp
x->y
```

위의 식은 아래의 식과 동일합니다.

```csharp
(*x).y
```

다음 예제에서는 `->` 연산자의 사용법을 보여 줍니다.

[!code-csharp[pointer member access](~/samples/csharp/language-reference/operators/PointerOperators.cs#MemberAccess)]

`->` 연산자를 `void*` 유형의 식에 적용할 수 없습니다.

## <a name="pointer-element-access-operator-"></a>포인터 요소 액세스 연산자 []

포인터 형식의 식 `p`의 경우 `p[n]` 양식의 포인터 요소 액세스는 `*(p + n)`으로 평가됩니다. 여기서 `n`은 암시적으로 `int`, `uint`, `long` 또는 `ulong`으로 전환할 수 있는 형식이어야 합니다. 포인터가 있는 `+` 연산자의 동작에 대한 자세한 내용은 [포인터에 또는 포인터에서 정수 값 더하기 또는 빼기](#addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer) 섹션을 참조하세요.

다음 예제에서는 포인터 및 `[]` 연산자를 사용하여 배열 요소에 액세스하는 방법을 보여 줍니다.

[!code-csharp[pointer element access](~/samples/csharp/language-reference/operators/PointerOperators.cs#ElementAccess)]

이 예제에서는 [`stackalloc` 연산자](stackalloc.md)를 사용하여 스택의 메모리 블록을 할당합니다.

> [!NOTE]
> 포인터 요소 액세스 연산자는 범위 이탈 오류를 검사하지 않습니다.

`void*` 형식의 식으로 포인터 요소 액세스에 `[]`(을)를 사용할 수 없습니다.

[배열 요소 또는 인덱서 액세스](member-access-operators.md#indexer-operator-)에 대해 `[]` 연산자를 사용할 수도 있습니다.

## <a name="pointer-arithmetic-operators"></a>포인터 산술 연산자

포인터를 사용하여 다음과 같은 산술 연산을 수행할 수 있습니다.

- 포인터로 또는 포인터에서 정수 값 추가 또는 빼기
- 두 포인터 빼기
- 포인터 증가 또는 감소

`void*` 형식의 포인터를 사용하여 이러한 작업을 수행할 수 없습니다.

숫자 형식으로 지원되는 산술 연산에 대한 내용은 [산술 연산자](arithmetic-operators.md)를 참조하세요.

### <a name="addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer"></a>포인터로 또는 포인터에서 정수 값 더하기 또는 빼기

`T*` 형식의 포인터 `p` 및 `int`, `uint`, `long` 또는 `ulong`으로 암시적으로 변환할 수 있는 형식의 `n` 식에 대한 더하기와 빼기가 다음과 같이 정의됩니다.

- `p + n` 및 `n + p` 식 모두 `p`에서 지정한 주소에 `n * sizeof(T)`를 추가한 결과 `T*` 유형의 포인터를 생성합니다.
- `p - n` 식은 `p`에 의해 지정된 주소에서 `n * sizeof(T)`를 뺀 결과 `T*` 유형의 포인터를 생성합니다.

[`sizeof` 연산자](sizeof.md)는 바이트 단위의 형식 크기를 가져옵니다.

다음 예제에서는 포인터로 `+` 연산자를 사용하는 방법을 보여줍니다.

[!code-csharp[pointer addition](~/samples/csharp/language-reference/operators/PointerOperators.cs#AddNumber)]

### <a name="pointer-subtraction"></a>포인터 빼기

`T*` 형식의 두 가지 포인터 `p1` 및 `p2`에 대해 `p1 - p2` 식은 `p1`과 `p2`에 의해 지정된 주소 간의 차이를 `sizeof(T)`로 나누어 생성합니다. 결과의 형식은 `long`입니다. 즉, `p1 - p2`는 `((long)(p1) - (long)(p2)) / sizeof(T)`로 계산됩니다.

다음 예제에서는 포인터 빼기를 보여줍니다.

[!code-csharp[pointer subtraction](~/samples/csharp/language-reference/operators/PointerOperators.cs#SubtractPointers)]

### <a name="pointer-increment-and-decrement"></a>포인터 증가 및 감소

`++` 증가 연산자는 포인터 피연산자에 1을 [추가](#addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer)합니다. `--` 감소 연산자는 포인터 피연산자에서 1을 [뺍니다](#addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer).

두 연산자는 접미사(`p++` 및 `p--`)와 접두사(`++p` 및 `--p`)의 두 가지 형태로 지원됩니다. `p++` 및 `p--`의 결과는 작업 `p` *전*의 값입니다. `++p` 및 `--p`의 결과는 작업 `p` *후*의 값입니다.

다음 예제에서는 접미사 및 접두사 증가 연산자의 동작을 보여줍니다.

[!code-csharp[pointer increment](~/samples/csharp/language-reference/operators/PointerOperators.cs#Increment)]

## <a name="pointer-comparison-operators"></a>포인터 비교 연산자

`==`, `!=`, `<`, `>`, `<=` 및 `>=` 연산자를 사용하여 `void*`를 포함한 모든 포인터 형식의 피연산자를 비교할 수 있습니다. 이러한 연산자는 두 피연산자가 지정한 주소를 부호 없는 정수인 것처럼 비교합니다.

다른 형식의 피연산자에 대한 해당 연산자의 동작에 대한 정보는 [항등 연산자](equality-operators.md) 및 [비교 연산자](comparison-operators.md) 문서를 참조하세요.

## <a name="operator-precedence"></a>연산자 우선 순위

다음 목록에서는 포인터 관련 연산자를 가장 높은 우선순위부터 가장 낮은 것으로 정렬합니다.

- 접미사 증가 `x++` 및 감소 `x--` 연산자와 `->` 및 `[]` 연산자
- 접두사 증가 `++x` 및 감소 `--x` 연산자와 `&` 및 `*` 연산자
- 가감 `+` 및 `-` 연산자
- 비교 `<`, `>`, `<=` 및 `>=` 연산자
- 같음 `==` 및 `!=` 연산자

괄호(`()`)를 사용하여 연산자 우선순위에 따라 주어진 평가 순서를 변경합니다.

우선 순위 수준에 따라 정렬된 전체 연산자 목록은 [C# 연산자](index.md)를 참조하세요.

## <a name="operator-overloadability"></a>연산자 오버로드 가능성

사용자 정의 형식은 포인터 관련 연산자 `&`, `*`, `->` 및 `[]`(을)를 오버로드할 수 없습니다.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 다음 섹션을 참조하세요.

- [고정 및 고정되지 않은 변수](~/_csharplang/spec/unsafe-code.md#fixed-and-moveable-variables)
- [address-of 연산자](~/_csharplang/spec/unsafe-code.md#the-address-of-operator)
- [포인터 간접 참조](~/_csharplang/spec/unsafe-code.md#pointer-indirection)
- [포인터 멤버 액세스](~/_csharplang/spec/unsafe-code.md#pointer-member-access)
- [포인터 요소 액세스](~/_csharplang/spec/unsafe-code.md#pointer-element-access)
- [포인터 산술 연산](~/_csharplang/spec/unsafe-code.md#pointer-arithmetic)
- [포인터 증가 및 감소](~/_csharplang/spec/unsafe-code.md#pointer-increment-and-decrement)
- [포인터 비교](~/_csharplang/spec/unsafe-code.md#pointer-comparison)

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 연산자](index.md)
- [포인터 형식](../../programming-guide/unsafe-code-pointers/pointer-types.md)
- [unsafe 키워드](../keywords/unsafe.md)
- [fixed 키워드](../keywords/fixed-statement.md)
- [stackalloc 연산자](stackalloc.md)
- [sizeof 연산자](sizeof.md)
