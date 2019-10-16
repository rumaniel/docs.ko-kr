---
title: C# 식 - C# 언어 둘러보기
description: 식, 피연산자 및 연산자는 C# 언어의 블록을 빌드합니다.
ms.date: 04/25/2019
ms.assetid: 20d5eb10-7381-47b9-ad90-f1cc895aa27e
ms.openlocfilehash: 2553730d495942730c53d3646f35e80759a4d168
ms.sourcegitcommit: eaa6d5cd0f4e7189dbe0bd756e9f53508b01989e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2019
ms.locfileid: "67609325"
---
# <a name="expressions"></a>식

*식*은 *피연산자* 및 *연산자*로 생성됩니다. 식의 연산자는 피연산자에 적용할 연산을 나타냅니다. 연산자의 예로 `+`, `-`, `*`, `/` 및 `new`가 있습니다. 피연산자의 예로는 리터럴, 필드, 지역 변수 및 식이 있습니다.

식에 여러 연산자가 포함되어 있으면 연산자의 *우선 순위*에 따라 개별 연산자가 계산되는 순서가 제어됩니다. 예를 들어 `*` 연산자는 `+` 연산자보다 우선 순위가 더 높기 때문에 식 `x + y * z`는 `x + (y * z)`로 계산됩니다.

피연산자는 동일한 우선 순위를 가진 두 연산자 사이에 나올 경우 연산자의 *결합성*에 따라 연산이 수행되는 순서가 제어됩니다.

* 대입 연산자를 제외하고 모든 이항 연산자는 *왼쪽 결합성*을 갖습니다. 즉, 연산이 왼쪽에서 오른쪽으로 수행됩니다. 예를 들어, `x + y + z`는 `(x + y) + z`로 계산됩니다.
* 대입 연산자 및 조건부 연산자(`?:`)는 *오른쪽 결합성*을 갖습니다. 즉, 연산이 오른쪽에서 왼쪽으로 수행됩니다. 예를 들어, `x = y = z`는 `x = (y = z)`로 계산됩니다.

우선 순위 및 결합성은 괄호를 사용하여 제어할 수 있습니다. 예를 들어 `x + y * z`는 먼저 `y`와 `z`를 곱한 다음 그 결과를 `x`와 더하지만 `(x + y) * z`는 먼저 `x`와 `y`를 더한 다음 그 결과에 `z`를 곱합니다.

대부분의 연산자는 [*오버로드*](../language-reference/operators/operator-overloading.md)할 수 있습니다. 연산자 오버로드는 피연산자 중 하나 또는 둘 다가 사용자 정의 클래스 또는 구조체 형식인 연산에 대해 사용자 정의 연산자 구현을 지정할 수 있도록 허용합니다.

C#은 [산술](../language-reference/operators/arithmetic-operators.md), [논리](../language-reference/operators/boolean-logical-operators.md), [비트 및 시프트](../language-reference/operators/bitwise-and-shift-operators.md) 연산과 [같음](../language-reference/operators/equality-operators.md) 및 [순서](../language-reference/operators/comparison-operators.md) 비교를 수행하는 여러 연산자를 제공합니다.

우선 순위 수준에 따라 정렬된 전체 연산자 목록은 [C# 연산자](../language-reference/operators/index.md)를 참조하세요.

> [!div class="step-by-step"]
> [이전](types-and-variables.md)
> [다음](statements.md)
