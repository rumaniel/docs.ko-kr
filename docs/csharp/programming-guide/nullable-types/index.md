---
title: nullable 값 형식 - C# 프로그래밍 가이드
ms.custom: seodec18
description: C# nullable 값 형식 및 사용 방법 알아보기
ms.date: 09/26/2019
helpviewer_keywords:
- nullable value types [C#]
ms.assetid: e473cb01-28ca-42be-9cea-f717055d72c6
ms.openlocfilehash: b8b52e7fb34adf65d5c76d59811ea6dd0ab16a98
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396224"
---
# <a name="nullable-value-types-c-programming-guide"></a>nullable 값 형식(C# 프로그래밍 가이드)

nullable 값 형식은 <xref:System.Nullable%601?displayProperty=nameWithType> 구조체의 인스턴스입니다. nullable 값 형식은 기본 형식 `T`의 모든 값과 추가 [null](../../language-reference/keywords/null.md) 값을 나타낼 수 있습니다. 기본 형식 `T`는 nullable이 아닌 [값 형식](../../language-reference/keywords/value-types.md)일 수 있습니다. `T`는 참조 형식이 아닙니다.

> [!NOTE]
> C# 8.0에서는 nullable 참조 형식 기능을 소개합니다. 자세한 내용은 [nullable 참조 형식](../../nullable-references.md)을 참조하세요. nullable 값 형식은 C# 2부터 사용할 수 있습니다.

예를 들어 <xref:System.Int32.MinValue?displayProperty=nameWithType>부터 <xref:System.Int32.MaxValue?displayProperty=nameWithType>까지의 `null` 또는 정수 값을 `Nullable<int>`에 할당하고, [true](../../language-reference/keywords/true-literal.md), [false](../../language-reference/keywords/false-literal.md) 또는 `null`을 `Nullable<bool>`에 할당할 수 있습니다

기본 형식의 정의되지 않은 값을 표시해야 하는 경우 nullable 값 형식을 사용합니다. 부울 변수에는 두 개의 값(`true` 및 `false`)만 있을 수 있습니다. "정의되지 않은" 값이 없습니다. 많은 프로그래밍 애플리케이션(특히, 데이터베이스 상호 작용)에서 변수는 정의되지 않거나 누락될 수 있습니다. 예를 들어 데이터베이스의 필드는 true 또는 false 값을 포함하거나 값을 전혀 포함하지 않을 수 있습니다. 해당 경우에 `Nullable<bool>` 형식을 사용합니다.

nullable 값 형식은 다음 특성을 갖습니다.

- nullable 값 형식은 `null` 값이 할당될 수 있는 값-형식 변수를 나타냅니다.

- `T?` 구문은 `Nullable<T>`의 축약형입니다. 두 가지 형태는 동일하게 사용할 수 있습니다.

- 일반 값 형식의 경우처럼 nullable 값 형식에 값을 할당합니다(`int? x = 10;` 또는 `double? d = 4.108;`). `null` 값을 할당할 수도 있습니다(`int? x = null;`).

- 다음 예제와 같이 <xref:System.Nullable%601.HasValue%2A?displayProperty=nameWithType> 및 <xref:System.Nullable%601.Value%2A?displayProperty=nameWithType> 읽기 전용 속성을 사용하여 null인지 테스트하고 값을 검색합니다. `if (x.HasValue) y = x.Value;`

  - <xref:System.Nullable%601.HasValue%2A> 속성은 변수에 값이 있으면 `true`를 반환하고, `null`이면 `false`를 반환합니다.

  - <xref:System.Nullable%601.Value%2A> 속성은 <xref:System.Nullable%601.HasValue%2A>가 `true`를 반환하는 경우 값을 반환합니다. 그렇지 않으면 <xref:System.InvalidOperationException>이 throw됩니다.

- 다음 예제와 같이 nullable 값 형식에서 `==` 및 `!=` 연산자를 사용할 수도 있습니다. `if (x != null) y = x.Value;` `a` 및 `b`가 둘 다 null인 경우 `a == b`는 `true`로 평가합니다.

- C# 7.0부터는 [패턴 일치](../../pattern-matching.md#the-is-type-pattern-expression)를 사용하여 nullable 형식의 값을 검사하고 가져올 수 있습니다(`if (x is int valueOfX) y = valueOfX;`).

- 기본값인 `T?`는 <xref:System.Nullable%601.HasValue%2A> 속성이 `false`를 반환하는 인스턴스입니다.

- nullable 형식 값이 `null`인 경우 <xref:System.Nullable%601.GetValueOrDefault> 메서드를 사용하여 할당된 값 또는 기본 값 형식의 [기본값](../../language-reference/keywords/default-values-table.md) 중 하나를 반환합니다.

- nullable 형식 값이 `null`인 경우 <xref:System.Nullable%601.GetValueOrDefault(%600)> 메서드를 사용하여 할당된 값 또는 제공된 기본값 중 하나를 반환합니다.

- [null 결합 연산자](../../language-reference/operators/null-coalescing-operator.md)인 `??`을(를) 사용하여 nullable 형식 값(`int? x = null; int y = x ?? -1;`)을 기반으로 하는 기본 값 형식의 변수에 값을 할당합니다. 예제에서 `x`이(가) `null`이므로 결과 값인 `y`은(는) `-1`입니다.

- 두 값 형식에 사용자 정의 변환이 정의된 경우 해당 nullable 형식에도 같은 변환을 사용할 수 있습니다.

- 중첩된 nullable 값 형식은 허용되지 않습니다. 다음 줄은 컴파일되지 않습니다. `Nullable<Nullable<int>> n;`

자세한 내용은 [nullable 값 형식 사용](using-nullable-types.md) 및 [방법: nullable 값 형식 식별](how-to-identify-a-nullable-type.md) 항목을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [?? 연산자](../../language-reference/operators/null-coalescing-operator.md)
- [Nullable 값 형식(Visual Basic)](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)
- <xref:System.Nullable%601?displayProperty=nameWithType>
- <xref:System.Nullable?displayProperty=nameWithType>
