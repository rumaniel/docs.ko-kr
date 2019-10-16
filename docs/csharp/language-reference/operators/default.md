---
title: 기본 연산자 - C# 참조
ms.custom: seodec18
description: 기본 연산자를 사용하여 형식의 기본값을 생성합니다.
ms.date: 08/01/2019
helpviewer_keywords:
- default keyword [C#]
ms.openlocfilehash: 5623cb9dc3790b5bb99635c41cb3f122f4c71d8e
ms.sourcegitcommit: bbfcc913c275885381820be28f61efcf8e83eecc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68796942"
---
# <a name="default-operator-c-reference"></a>기본 연산자(C# 참조)

`default` 연산자는 형식의 [기본값](../keywords/default-values-table.md)을 생성합니다. `default` 연산자에 대한 인수는 형식 또는 형식 매개 변수의 이름이어야 합니다.

다음 예제에서는 `default` 연산자의 사용법을 보여 줍니다.

[!code-csharp-interactive[default of T](~/samples/csharp/language-reference/operators/DefaultOperator.cs#WithOperand)]

또한 `default` 키워드를 [`switch` 문](../keywords/switch.md) 내의 기본 사례 레이블로 사용할 수 있습니다.

## <a name="default-literal"></a>기본 리터럴

C# 7.1부터 `default` 리터럴을 사용하여 컴파일러가 식 형식을 유추할 수 있는 경우 형식의 기본값을 생성할 수 있습니다. `default` 리터럴 식은 `T`가 추론된 형식은 `default(T)` 식과 동일한 값을 생성합니다. 다음과 같은 경우에 `default` 리터럴 사용할 수 있습니다.

- 변수의 할당 또는 초기화에서
- 선택적 메서드 매개 변수에 대한 기본값 선언에서
- 인수 값을 제공하기 위한 메서드 호출에서
- `return` 문에서 또는 식 본문 멤버의 식으로

다음 예제에서는 `default` 리터의 사용법을 보여 줍니다.

[!code-csharp-interactive[default literal](~/samples/csharp/language-reference/operators/DefaultOperator.cs#DefaultLiteral)]

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [기본값 식](~/_csharplang/spec/expressions.md#default-value-expressions) 섹션을 참조하세요.

`default` 리터럴에 대한 자세한 내용은 [기능 제안 노트](~/_csharplang/proposals/csharp-7.1/target-typed-default.md)를 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 연산자](index.md)
- [기본값 표](../keywords/default-values-table.md)
