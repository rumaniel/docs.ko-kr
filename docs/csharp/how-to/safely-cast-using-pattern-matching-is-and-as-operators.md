---
title: '방법: 패턴 일치와 is 및 as 연산자를 사용하여 안전하게 캐스트'
description: 패턴 일치 기법을 사용하여 변수를 다른 형식으로 안전하게 캐스팅하는 방법을 알아봅니다. 패턴 일치뿐만 아니라 is 및 as 연산자를 사용하여 형식을 안전하게 변환할 수 있습니다.
ms.date: 09/05/2018
helpviewer_keywords:
- cast operators [C#], as and is operators
- as operator [C#]
- is operator [C#]
ms.openlocfilehash: d82c60374db637bb8ac879a23e2d74c39194ca18
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353731"
---
# <a name="how-to-safely-cast-by-using-pattern-matching-and-the-is-and-as-operators"></a>방법: 패턴 일치와 is 및 as 연산자를 사용하여 안전하게 캐스트

개체는 다형성이기 때문에 기본 클래스 형식의 변수에 파생 [형식](../programming-guide/types/index.md)이 포함될 수 있습니다. 파생 형식의 인스턴스 멤버에 액세스하려면 값을 파생 형식으로 다시 [캐스팅](../programming-guide/types/casting-and-type-conversions.md)해야 합니다. 그러나 캐스트는 <xref:System.InvalidCastException>이 throw될 위험을 생성합니다. C#은 성공하는 경우에만 조건부로 캐스트를 수행하는 [패턴 일치](../pattern-matching.md) 문을 제공합니다. C#은 또한 값이 특정 형식인지 테스트하기 위해 [is](../language-reference/operators/type-testing-and-cast.md#is-operator) 및 [as](../language-reference/operators/type-testing-and-cast.md#as-operator) 연산자를 제공합니다.

다음 코드에서는 패턴 일치 `is` 문을 보여 줍니다. 메서드 인수를 테스트하여 가능한 파생 형식 집합 중 하나인지 확인하는 메서드가 포함되어 있습니다.

[!code-csharp[Pattern matching is statement](../../../samples/snippets/csharp/how-to/safelycast/patternmatching/Program.cs#PatternMatchingIs)]

위의 샘플은 패턴 일치 구문의 몇 가지 기능을 보여 줍니다. `if (a is Mammal m)` 및 `if (o is Mammal m)` 문은 테스트를 초기화 할당과 결합합니다. 할당은 테스트가 성공한 경우에만 발생합니다. 변수 `m`은 할당된 `if` 문의 포함되어 있는 범위에만 있습니다. 나중에 같은 방법으로 `m`에 액세스할 수 없습니다. 대화형 창에서 시도해 보세요.

다음 샘플 코드에 표시된 대로 [nullable 값 형식](../programming-guide/nullable-types/index.md)에 값이 있는 경우 테스트할 때도 동일한 구문을 사용할 수 있습니다.

[!code-csharp[Pattern matching with nullable types](../../../samples/snippets/csharp/how-to/safelycast/nullablepatternmatching/Program.cs#PatternMatchingNullable)]

위의 샘플은 변환에 사용하기 위한 패턴 일치의 다른 기능을 보여 줍니다. 구체적으로 `null` 값을 확인하여 null 패턴에 대한 변수를 테스트할 수 있습니다. 변수의 런타임 값이 `null`일 때 형식을 확인하는 `is` 문은 항상 `false`를 반환합니다. 패턴 일치 `is` 문은 `int?` 또는 `Nullable<int>`과 같은 nullable 값 형식을 허용하지 않지만 다른 값 형식을 테스트할 수 있습니다. 앞의 예제에서 `is` 패턴은 nullable 값 형식으로 제한되지 않습니다. 이러한 패턴을 사용하여 참조 형식의 변수에 값이 있는지 또는 값이 `null`인지 테스트할 수도 있습니다.

위의 샘플도 변수가 여러 형식 중 하나일 수 있는 `switch` 문에서 패턴 일치 `is` 식을 사용하는 방법을 보여 줍니다.

변수가 지정된 형식인지 테스트하지만 새 변수에 할당하지 않으려는 경우, 참조 형식 및 nullable 형식에 대해 `is` 및 `as` 연산자를 사용할 수 있습니다. 다음 코드는 변수가 지정된 형식인지 테스트하기 위해 패턴 일치가 도입되기 전에 C# 언어의 일부인 `is` 및 `as` 문을 사용하는 방법을 보여 줍니다.

[!code-csharp[testing variable types with the is and as statements](../../../samples/snippets/csharp/how-to/safelycast/asandis/Program.cs#IsAndAs)]

이 코드를 패턴 일치 코드와 비교하여 볼 수 있듯이, 패턴 일치 구문은 테스트와 할당을 단일 명령문으로 결합함으로써 더욱 강력한 기능을 제공합니다. 가능할 때마다 패턴 일치 구문을 사용합니다.

[GitHub 리포지토리](https://github.com/dotnet/samples/tree/master/snippets/csharp/how-to/safelycast)의 코드를 확인하여 이러한 샘플을 시험해 볼 수 있습니다. 또는 샘플을 [zip 파일로](https://github.com/dotnet/samples/raw/master/snippets/csharp/how-to/safelycast.zip) 다운로드할 수 있습니다.
