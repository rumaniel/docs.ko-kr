---
title: 패턴 일치 - C# 가이드
description: C#의 패턴 일치 식에 대한 자세한 정보
ms.date: 04/10/2019
ms.assetid: 1e575c32-2e2b-4425-9dca-7d118f3ed15b
ms.openlocfilehash: 5ace3c4552184b848b90dee3516d549ca8fd5806
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61652028"
---
# <a name="pattern-matching"></a>패턴 일치

패턴은 값에 특정 *모양*이 있는지 테스트하고 모양이 일치하는 경우 값에서 정보를 *추출*할 수 있습니다. 패턴 일치는 이미 사용하고 있는 알고리즘에 대해 더 간결한 구문을 제공합니다. 이미 기존 구문을 사용하여 패턴 일치 알고리즘을 만듭니다. 값을 테스트하는 `if` 또는 `switch` 문을 작성합니다. 그런 다음 이러한 문이 일치할 경우 해당 값에서 정보를 추출하고 사용합니다. 새 구문 요소는 이미 친숙한 `is` 및 `switch` 문에 대한 확장입니다. 이러한 새 확장은 값 테스트와 해당 정보 추출을 결합합니다.

이 문서에서는 읽을 수 있고 간결한 코드를 사용하는 방법을 보여 주는 새로운 구문을 살펴보겠습니다. 패턴 일치를 통해 데이터와 데이터를 조작하는 메서드가 긴밀하게 연결된 개체 지향 디자인과 달리 데이터와 코드가 구분된 구문을 사용할 수 있습니다.

이러한 새 구문을 보여 주기 위해 패턴 일치 문을 사용하여 도형을 나타내는 구조체를 살펴보겠습니다. 클래스 계층 구조를 작성하고 [가상 메서드 및 재정의된 메서드](methods.md#inherited)를 만들어 개체의 런타임 형식에 따라 개체 동작을 사용자 지정하는 작업에 대해 이미 잘 알고 있을 것입니다.

이러한 기술은 클래스 계층 구조로 구성되지 않은 데이터에는 사용할 수 없습니다. 데이터와 메서드가 분리된 경우 다른 도구가 필요합니다. 새 *패턴 일치* 구문에서는 더 명확한 구문으로 데이터를 검사하고 해당 데이터의 조건에 따라 제어 흐름을 조작할 수 있습니다. 이미 변수 값을 테스트하는 `if` 및 `switch` 문을 작성합니다. 변수 형식을 테스트하는 `is` 문을 작성합니다. *패턴 일치*는 이러한 문에 새로운 기능을 추가합니다.

이 문서에서는 여러 도형의 면적을 계산하는 메서드를 작성합니다. 그러나 이 작업을 위해 개체 지향 기술을 사용하여 다양한 셰이프에 대한 클래스 계층 구조를 작성하지 않습니다.
대신 *패턴 일치*를 사용합니다.
이 샘플을 진행하면서 이 코드를 개체 계층 구조로 구성된 방식과 대조합니다. 쿼리 및 조작해야 하는 데이터가 클래스 계층 구조가 아닌 경우 패턴 일치를 통해 세련된 디자인을 사용할 수 있습니다.

추상 셰이프 정의로 시작하고 다른 특정 셰이프 클래스를 추가하는 대신 각 도형에 대한 간단한 데이터 전용 정의로 시작하겠습니다.

[!code-csharp[ShapeDefinitions](../../samples/csharp/PatternMatching/Shapes.cs#01_ShapeDefinitions "Shape definitions")]

이러한 구조체에서 일부 셰이프의 면적을 계산하는 메서드를 작성하겠습니다.

## <a name="the-is-type-pattern-expression"></a>`is` 형식 패턴 식

C# 7.0 이전에는 일련의 `if` 및 `is` 문에서 각 형식을 테스트해야 했습니다.

[!code-csharp[ClassicIsExpression](../../samples/csharp/PatternMatching/GeometricUtilities.cs#02_ClassicIsExpression "Classic type pattern using is")]

위의 코드는 ‘형식 패턴’의 클래식 식입니다. 변수를 테스트하여 해당 형식을 확인하고 해당 형식에 따라 다른 작업을 수행합니다.

`is` 식에 대한 확장을 사용하여 테스트에 성공할 경우 변수를 할당하면 이 코드가 더 간단해집니다.

[!code-csharp[IsPatternExpression](../../samples/csharp/PatternMatching/GeometricUtilities.cs#03_IsPatternExpression "is pattern expression")]

이 업데이트된 버전에서 `is` 식은 변수를 테스트하고 적절한 형식의 새로운 변수에 할당합니다. 또한 이 버전에는 `struct`인 `Rectangle` 형식이 포함되어 있습니다. 새 `is` 식은 참조 형식뿐 아니라 값 형식에서도 작동합니다.

패턴 일치 식에 대한 언어 규칙은 일치 식의 결과를 잘못 사용하는 경우를 방지하는 데 도움이 됩니다. 위의 예제에서 `s`, `c` 및 `r` 변수는 범위 내에만 있고 해당 패턴 일치 식에 `true` 결과가 있는 경우 무기한 할당됩니다. 다른 위치에 있는 변수 중 하나를 사용하려는 경우 코드에서 컴파일러 오류를 생성합니다.

범위부터 시작하여 해당 규칙을 자세히 살펴보겠습니다. `c` 변수는 첫 번째 `if` 문의 `else` 분기에서만 범위 내에 있습니다. `s` 변수는 `ComputeAreaModernIs` 메서드에서 범위 내에 있습니다. 이는 `if` 문의 각 분기가 변수에 대해 별도 범위를 설정하기 때문입니다. 그러나 `if` 문 자체는 별도 범위를 설정하지 않습니다. 즉, `if` 문에서 선언된 변수는 `if` 문(이 경우 메서드)과 동일한 범위에 있습니다. 이 동작은 패턴 일치와 관련은 없지만 변수 범위와 `if` 및 `else` 문에 대해 정의된 동작입니다.

`c` 및 `s` 변수는 한정적으로 할당된 true 시 메커니즘 때문에 해당 `if` 문이 true일 때 할당됩니다.

> [!TIP]
> 이 항목의 샘플에서는 패턴 일치 `is` 식이 `if` 문의 `true` 분기에 있는 일치 변수를 한정적으로 할당하는 권장 구문을 사용합니다.
> `if (!(shape is Square s))` 및 `s` 변수가 `false` 분기에서만 한정적으로 할당된다고 지정하면 논리를 반전시킬 수 있습니다. 이 논리는 C#에서 유효하지만 논리를 따르는 것이 더 혼동되기 때문에 따르지 않는 것이 좋습니다.

이 규칙은 해당 패턴이 충족되지 않은 경우 패턴 일치 식의 결과에 실수로 액세스할 가능성이 없음을 의미합니다.

## <a name="using-pattern-matching-switch-statements"></a>패턴 일치 `switch` 문 사용

시간이 흐르면서 다른 셰이프 형식을 지원해야 할 수도 있습니다. 테스트하는 조건 수가 증가함에 따라 `is` 패턴 일치 식 사용이 불편해질 수 있습니다. 확인하려는 각 형식에 대한 `if` 문이 필요할 뿐 아니라 `is` 식은 입력이 단일 형식과 일치하는지 여부의 테스트로 제한됩니다. 이 경우 `switch` 패턴 일치 식을 선택하는 것이 더 나을 수 있습니다. 

기존의 `switch` 문은 패턴 식이었으며 상수 패턴을 지원했습니다.
`case` 문에서 사용된 상수와 변수를 비교할 수 있습니다.

[!code-csharp[ClassicSwitch](../../samples/csharp/PatternMatching/GeometricUtilities.cs#04_ClassicSwitch "Classic switch statement")]

`switch` 문이 지원하는 패턴은 상수 패턴뿐이었습니다. 숫자 형식과 `string` 형식으로 더욱 제한되었습니다.
이러한 제한 사항이 제거되었으며, 이제 형식 패턴을 사용하여 `switch` 문을 작성할 수 있습니다.

[!code-csharp[Switch Type Pattern](../../samples/csharp/PatternMatching/GeometricUtilities.cs#05_SwitchTypePattern "Compute with `switch` expression")]

패턴 일치 `switch` 문은 기존의 C 스타일 `switch` 문을 사용한 개발자에게 친숙한 구문을 사용합니다. 각 `case`가 평가되고, 입력 변수와 일치하는 조건 아래에 있는 코드가 실행됩니다. 코드 실행은 case 식 간에 “이동”할 수 없습니다. `case` 문의 구문에서는 각 `case`가 `break`, `return` 또는 `goto`로 끝나야 합니다.

> [!NOTE]
> 다른 레이블로 이동하는 `goto` 문은 클래식 switch 문인 상수 패턴에만 유효합니다.

`switch` 문을 제어하는 중요한 새 규칙이 있습니다. `switch` 식의 변수 형식에 대한 제한 사항이 제거되었습니다.
이 예제의 `object`와 같은 모든 형식을 사용할 수 있습니다. case 식이 더 이상 상수 값으로 제한되지 않습니다. 이러한 제한이 제거되면서 `switch` 섹션을 다시 정렬할 경우 프로그램의 동작이 변경될 수 있습니다.

상수 값으로 제한될 경우 최대 한 개의 `case` 레이블만 `switch` 식과 일치할 수 있습니다. 모든 `switch` 섹션이 다음 섹션으로 이동해서는 안 되는 규칙과 결합되어 동작에 영향을 주지 않고 `switch` 섹션을 임의 순서로 다시 정렬할 수 있습니다.
이제 보다 일반화된 `switch` 식을 사용하므로 각 섹션의 순서가 중요합니다. `switch` 식은 텍스트 순서로 계산됩니다. `switch` 식과 일치하는 첫 번째 `switch` 레이블로 실행이 전송됩니다.  
`default` case는 일치하는 다른 case 레이블이 없는 경우에만 실행됩니다. `default` 사례는 텍스트 순서에 관계없이 마지막으로 평가됩니다. `default` case가 없고 일치하는 다른 `case` 문이 없는 경우 `switch` 문 뒤의 문에서 실행이 계속됩니다. `case` 레이블 코드는 실행되지 않습니다.

## <a name="when-clauses-in-case-expressions"></a>`case` 식의 `when` 절

`case` 레이블에 `when` 절을 사용하여 면적이 0인 해당 셰이프에 대한 특수 사례를 만들 수 있습니다. 측면 길이가 0인 사각형 또는 반지름이 0인 원은 면적이 0입니다. `case` 레이블에 `when` 절을 사용하여 해당 조건을 지정할 수 있습니다.  

[!code-csharp[ComputeDegenerateShapes](../../samples/csharp/PatternMatching/GeometricUtilities.cs#07_ComputeDegenerateShapes "Compute shapes with 0 area")]

이 변경 내용은 새 구문에 대한 몇 가지 중요한 사항을 보여 줍니다. 첫째, 여러 `case` 레이블을 하나의 `switch` 섹션에 적용할 수 있습니다. 문 블록은 이러한 레이블이 `true`인 경우에 실행됩니다. 이 인스턴스에서 `switch` 식이 면적이 0인 원 또는 사각형인 경우 메서드가 상수 0을 반환합니다.

이 예제에서는 첫 번째 `switch` 블록에 대한 두 개의 `case` 레이블에 있는 두 개의 변수를 소개합니다. 이 `switch` 블록의 문은 `c`(원) 또는 `s`(사각형) 변수를 사용하지 않습니다.
이러한 변수는 이 `switch` 블록에서 한정적으로 할당되지 않습니다.
이 사례 중 하나가 일치하면 변수 중 하나가 명확하게 할당된 것입니다.
그러나 case 중 하나가 런타임에 일치할 수 있기 때문에 컴파일 시간에 어떤 사례가 할당되었는지 알 수 없습니다. 이런 이유로 동일한 블록에 여러 `case` 레이블을 사용하는 경우 대부분 `case` 문에서 새 변수를 도입하지 않거나 `when` 절에서만 변수를 사용합니다.

면적이 0인 셰이프를 추가한 경우 사각형과 삼각형인 셰이프 유형 두 개를 더 추가하겠습니다.

[!code-csharp[AddRectangleAndTriangle](../../samples/csharp/PatternMatching/GeometricUtilities.cs#09_AddRectangleAndTriangle "Add rectangle and triangle")]

 이 변경 내용 집합은 degenerate 사례에 대한 `case` 레이블과 새로운 각 셰이프에 대한 레이블 및 블록을 추가합니다. 

마지막으로, `null` case를 추가하여 인수가 `null`이 아닌지 확인할 수 있습니다.

[!code-csharp[NullCase](../../samples/csharp/PatternMatching/GeometricUtilities.cs#10_NullCase "Add null case")]

`null` 패턴의 특수 동작은 패턴에서 형식이 없는 `null` 상수를 모든 참조 형식 또는 nullable 형식으로 변환할 수 있기 때문에 흥미롭습니다. `null`을 임의 형식으로 변환하는 대신, 언어에서 `null` 값은 변수의 컴파일 시간 형식과 관계없이 어떠한 형식 패턴과도 일치하지 않는다고 정의합니다. 이 동작을 통해 새 `switch` 기반 형식 패턴이 `is` 문과 일치하게 됩니다. `is` 문은 확인되는 값이 `null`일 경우 항상 `false`를 반환합니다. 더 간단하기도 합니다. 형식을 확인한 후에는 추가 null 검사가 필요하지 않습니다. 위 샘플의 case 블록에 null 검사가 없다는 사실에서 이를 확인할 수 있습니다. 형식 패턴 일치를 통해 null이 아닌 값이 보장되므로 null 검사가 필요하지 않습니다.

## <a name="var-declarations-in-case-expressions"></a>`case` 식의 `var` 선언

match 식 중 하나인 `var`이 소개되면서 패턴 일치에 대한 새 규칙이 도입됩니다.

첫 번째 규칙은 `var` 선언이 일반 형식 유추 규칙을 따른다는 것입니다. 형식은 switch 식의 정적 형식으로 유추됩니다. 이 규칙에 따라 형식이 항상 일치합니다.

두 번째 규칙은 `var` 선언에 다른 형식 패턴 식이 포함하는 null 검사가 없다는 것입니다. 즉, 변수가 null일 수 있고 이 경우 null 검사가 필요합니다.

이러한 두 규칙은 여러 인스턴스에서 `case` 식의 `var` 선언이 `default` 식과 동일한 조건과 일치함을 의미합니다.
`default` 사례보다 기본값이 아닌 사례가 선호되므로 `default` 사례는 실행되지 않습니다.

> [!NOTE]
> 컴파일러는 `default` 사례가 작성되었지만 실행되지 않을 경우에 경고를 표시하지 않습니다. 이것은 모든 가능한 사례가 나열된 현재 `switch` 문 동작과 일치합니다.

세 번째 규칙은 `var` 사례가 유용할 수 있는 사용법을 소개합니다. 입력이 문자열이고 알려진 명령 값을 검색하는 패턴 일치를 수행한다고 가정해 봅니다. 다음과 같이 작성할 수 있습니다.

[!code-csharp[VarCaseExpression](../../samples/csharp/PatternMatching/Program.cs#VarCaseExpression "use a var case expression to filter white space")]

`var` 사례는 `null`, 빈 문자열, 또는 공백만 포함하는 문자열과 일치합니다. 앞의 코드에서는 `?.` 연산자를 사용하여 실수로 <xref:System.NullReferenceException>을 throw하지 않도록 합니다. `default` case는 이 명령 파서에서 인식되지 않는 기타 문자열 값을 처리합니다.

이는 `default` 식과 구별되는 `var` 사례 식을 고려할 수 있는 하나의 예제입니다.

## <a name="conclusions"></a>결론

‘패턴 일치 구문’을 사용하면 상속 계층 구조와 관련이 없는 다양한 변수 및 형식 간의 제어 흐름을 쉽게 관리할 수 있습니다. 논리를 제어하여 변수에 테스트하는 조건을 사용할 수도 있습니다. 데이터 및 해당 데이터를 조작하는 메서드가 별개인 더욱 분산된 애플리케이션을 빌드하는 경우 더 자주 필요한 패턴과 구문을 사용할 수 있습니다. 이 샘플에 사용된 셰이프 구조체에는 메서드가 없고 읽기 전용 속성만 있습니다.
패턴 일치는 모든 데이터 형식에서 작동합니다. 개체를 검사하는 식을 작성하고 해당 조건에 따라 제어 흐름 결정을 내립니다.

추상 `Shape` 및 각각 고유한 가상 메서드 구현으로 면적을 계산하는 특정 파생 셰이프에 대한 클래스 계층 구조를 만들어 수행하는 디자인과 이 샘플의 코드를 비교합니다. 데이터로 작업하고 데이터 스토리지 문제와 동작 문제를 구분하려는 경우 패턴 일치 식은 매우 유용한 도구일 수 있습니다.
