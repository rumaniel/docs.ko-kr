---
title: C# switch 문
ms.date: 04/09/2019
f1_keywords:
- switch_CSharpKeyword
- switch
- case
- case_CSharpKeyword
helpviewer_keywords:
- switch statement [C#]
- switch keyword [C#]
- case statement [C#]
- default keyword [C#]
ms.assetid: 44bae8b8-8841-4d85-826b-8a94277daecb
ms.openlocfilehash: 5257d1d677246cdd6d826cd71ed3ffe116d2a4a6
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67424119"
---
# <a name="switch-c-reference"></a>switch(C# 참조)

`switch`는 *일치 식*을 사용한 패턴 일치를 기반으로 하여 후보 목록에서 실행할 *switch 섹션* 하나를 선택하는 선택 문입니다.

[!code-csharp[switch#1](~/samples/snippets/csharp/language-reference/keywords/switch/switch1.cs#1)]

단일 식을 3개 이상의 조건에 대해 테스트하는 경우 `switch` 문이 [if-else](if-else.md) 구문 대신 사용되는 경우가 많습니다. 예를 들어 다음 `switch` 문은 `Color` 형식의 변수에 다음 세 가지 값 중 하나가 있는지 여부를 확인합니다.

[!code-csharp[switch#3](~/samples/snippets/csharp/language-reference/keywords/switch/switch3.cs#1)]

이 문은 `if`-`else` 구문을 사용하는 다음 예제와 같습니다.

[!code-csharp[switch#3a](~/samples/snippets/csharp/language-reference/keywords/switch/switch3a.cs#1)]

## <a name="the-match-expression"></a>일치 식

일치 식은 `case` 레이블의 패턴과 일치시킬 값을 제공합니다. 사용되는 구문은 다음과 같습니다.

```csharp
   switch (expr)
```

C# 6 이하에서 일치 식은 다음 형식의 값을 반환하는 식이어야 합니다.

- [char](char.md)
- [string](string.md)
- [bool](bool.md)
- [int](../builtin-types/integral-numeric-types.md) 또는 [long](../builtin-types/integral-numeric-types.md)과 같은 정수 계열 값
- [enum](enum.md) 값

C# 7.0부터 일치 식은 null이 아닌 모든 식일 수 있습니다.

## <a name="the-switch-section"></a>switch 섹션

`switch` 문에는 스위치 섹션이 하나 이상 포함됩니다. 각 switch 섹션에는 하나 이상의 *case 레이블*(사례 또는 기본 레이블) 및 하나 이상의 명령문이 있습니다. `switch` 문은 switch 섹션에 있는 기본 레이블이 하나만 포함될 수 있습니다. 다음 예제에서는 각각 두 개의 명령문을 포함하는 세 개의 switch 섹션이 있는 간단한 `switch` 문을 보여 줍니다. 두 번째 switch 섹션에는 `case 2:` 및 `case 3:` 레이블이 포함되어 있습니다.

`switch` 문에 포함할 수 있는 switch 섹션 수에는 제한이 없으며 각 섹션에 하나 이상의 case 레이블을 포함할 수 있습니다(다음 예제 참조). 하지만 두 case 레이블에 동일한 식을 포함할 수는 없습니다.

[!code-csharp[switch#2](~/samples/snippets/csharp/language-reference/keywords/switch/switch2.cs#1)]

switch 문에서 하나의 switch 섹션만 실행됩니다. C#은 한 switch 섹션에서 다음 switch 섹션으로 계속 실행하도록 허용하지 않습니다. 이로 인해 다음 코드는 다음과 같은 컴파일러 오류를 생성합니다. CS0163: "한 case 레이블(\<case label>)에서 다른 case 레이블로 제어를 이동할 수 없습니다."

```csharp
switch (caseSwitch)
{
    // The following switch section causes an error.
    case 1:
        Console.WriteLine("Case 1...");
        // Add a break or other jump statement here.
    case 2:
        Console.WriteLine("... and/or Case 2");
        break;
}
```

이 요구 사항은 일반적으로 [break](break.md), [goto](goto.md) 또는 [return](return.md) 문을 통해 switch 섹션을 명시적으로 종료하여 충족됩니다. 그러나 다음 코드는 프로그램 제어가 `default` switch 섹션으로 이동할 수 없도록 하기 때문에 유효합니다.

[!code-csharp[switch#4](~/samples/snippets/csharp/language-reference/keywords/switch/switch4.cs#1)]

case 레이블이 일치 식과 일치하는 switch 섹션에서 문 목록의 실행은 첫 번째 문으로 시작하고 일반적으로 `break`, `goto case`, `goto label`, `return` 또는 `throw` 같은 점프 문에 도달할 때까지 문 목록 전체를 진행합니다. 이 경우 `switch` 문 외부 또는 다른 case 레이블로 제어를 보냅니다. 사용되는 경우 `goto` 문은 constant 레이블에 컨트롤을 전달해야 합니다. 이 제한 사항이 필요합니다. constant가 아닌 레이블에 컨트롤을 전달하려고 하면 코드의 의도치 않은 위치에 컨트롤을 전달하거나 무한 루프를 만드는 것과 같은 원치 않는 부작용이 발생할 수 있기 때문입니다.

## <a name="case-labels"></a>case 레이블

각 case 레이블은 일치 식과 비교할 패턴(이전 예제의 `caseSwitch` 변수)을 지정합니다. 일치하는 경우 제어가 일치하는 **첫 번째** case 레이블을 포함하는 switch 섹션으로 전송됩니다. 일치 식과 일치하는 case 레이블 패턴이 없는 경우 제어가 `default` case 레이블을 포함하는 섹션으로 전송됩니다(있는 경우). `default` case가 없는 경우 switch 섹션의 문이 실행되지 않으며, 제어가 `switch` 문 외부로 전송됩니다.

`switch` 문과 패턴 일치에 대한 자세한 내용은 [`switch` 문을 사용한 패턴 일치](#pattern) 섹션을 참조하세요.

C# 6에서 상수 패턴만 지원하고 상수 값의 반복을 허용하지 않는 경우 case 레이블은 상호 배타적인 값을 정의하며 하나의 패턴만 일치 식과 일치할 수 있습니다. 따라서 `case` 문이 표시되는 순서는 중요하지 않습니다.

그러나 C# 7.0에서는 다른 패턴도 지원되므로 case 레이블에서 상호 배타적인 값을 정의할 필요가 없으며 여러 패턴이 일치 식과 일치할 수 있습니다. 일치 패턴을 포함하는 첫 번째 switch 섹션의 문만 실행되기 때문에 이제 `case` 문이 나타나는 순서가 중요합니다. C#에서 case 문이 이전 문과 같거나 이전 문의 하위 집합인 switch 섹션을 검색할 경우 컴파일러 오류, CS8120, "Switch case가 이전 case에서 이미 처리되었습니다."를 생성합니다.

다음 예제에서는 상호 배타적이 아닌 다양한 패턴을 사용하는 `switch` 문을 보여 줍니다. 더 이상 `switch` 문의 첫 번째 섹션이 아니도록 `case 0:` switch 섹션을 이동하는 경우 해당 값이 0인 정수는 `case int val` 문에 정의된 패턴인 모든 정수의 하위 집합이므로 C#에서 컴파일러 오류를 생성합니다.

[!code-csharp[switch#5](~/samples/snippets/csharp/language-reference/keywords/switch/switch5.cs#1)]

이 문제를 해결하고 다음 두 가지 방법 중 하나로 컴파일러 경고를 제거할 수 있습니다.

- switch 섹션의 순서 변경

- `case` 레이블에서 [when 절](#when) 사용

## <a name="the-default-case"></a>`default` case

`default` case는 일치 식이 다른 `case` 레이블과 일치하지 않는 경우 실행할 switch 섹션을 지정합니다. `default` case가 없고 일치 식이 다른 `case` 레이블과 일치하지 않는 경우 프로그램 흐름이 `switch` 문으로 이동합니다.

`default` case는 `switch` 문에 임의 순서로 표시될 수 있습니다. 소스 코드에서 해당 순서와 관계없이 항상 모든 `case` 레이블이 평가된 후 마지막에 평가됩니다.

## <a name="a-namepattern--pattern-matching-with-the-switch-statement"></a>`switch` 문을 사용한 <a name="pattern" /> 패턴 일치

각 `case` 문은 일치 식과 일치할 경우 포함하는 switch 섹션이 실행되는 패턴을 정의합니다. 상수 패턴은 모든 버전의 C#에서 지원됩니다. 나머지 패턴은 C# 7.0부터 지원됩니다.

### <a name="constant-pattern"></a>상수 패턴

상수 패턴은 일치 식이 지정된 상수와 같은지 여부를 테스트합니다. 사용되는 구문은 다음과 같습니다.

```csharp
   case constant:
```

여기서 *constant*는 테스트할 값입니다. *constant*는 다음 상수 식 중 하나가 될 수 있습니다.

- [bool](bool.md) 리터럴(`true` 또는 `false`)
- [int](../builtin-types/integral-numeric-types.md), [long](../builtin-types/integral-numeric-types.md) 또는 [byte](../builtin-types/integral-numeric-types.md)와 같은 모든 정수 계열 상수
- 선언된 `const` 변수의 이름
- 열거형 상수
- [char](char.md) 리터럴
- [string](string.md) 리터럴

상수 식은 다음과 같이 계산됩니다.

- *expr* 및 *constant*가 정수 형식인 경우 C# 같음 연산자는 식에서 `true`를 반환하는지 여부 즉, `expr == constant`인지 여부를 확인합니다.

- 정수 형식이 아니면 static [Object.Equals(expr, constant)](xref:System.Object.Equals(System.Object,System.Object)) 메서드 호출을 통해 식의 값이 결정됩니다.

다음 예제에서는 상수 패턴을 사용하여 특정 날짜가 주말인지, 작업 주의 첫째 날인지, 작업 주의 마지막 날인지 또는 작업 주의 중간인지를 확인합니다. 현재 날짜의 <xref:System.DateTime.DayOfWeek?displayProperty=nameWithType> 속성을 <xref:System.DayOfWeek> 열거형의 멤버와 비교해서 평가합니다.

[!code-csharp[switch#7](~/samples/snippets/csharp/language-reference/keywords/switch/const-pattern.cs#1)]

다음 예제에서는 상수 패턴을 사용하여 자동 커피 머신을 시뮬레이트하는 콘솔 애플리케이션의 사용자 입력을 처리합니다.

[!code-csharp[switch#6](~/samples/snippets/csharp/language-reference/keywords/switch/switch6.cs)]

### <a name="type-pattern"></a>형식 패턴

형식 패턴은 간결한 형식 평가 및 변환을 사용하도록 설정합니다. `switch` 문과 함께 사용하여 패턴 일치를 수행하는 경우 식을 지정된 형식으로 변환할 수 있는지 여부를 테스트하고, 변환할 수 있으면 해당 형식의 변수로 캐스팅합니다. 사용되는 구문은 다음과 같습니다.

```csharp
   case type varname
```

여기서 *type*은 *expr*의 결과가 변환되는 형식의 이름이고, *varname*은 일치에 성공할 경우 *expr*의 결과가 변환되는 개체입니다. *expr*의 컴파일 시간 형식은 C# 7.1부터 제네릭 형식 매개 변수일 수 있습니다.

다음 중 하나가 true일 경우 `case` 식은 `true`입니다.

- *expr*이 *type*과 동일한 형식의 인스턴스입니다.

- *expr*이 *type*에서 파생된 형식의 인스턴스입니다. 즉, *expr*의 결과를 *type*의 인스턴스로 업캐스트할 수 있습니다.

- *expr*의 컴파일 시간 형식은 *type*의 기본 클래스이고 *expr*의 런타임 형식은 *type*이거나 *type*에서 파생됩니다. 변수의 *컴파일 시간 형식*은 해당 형식 선언에 정의된 변수의 형식입니다. 변수의 *런타임 형식*은 해당 변수에 할당된 인스턴스의 형식입니다.

- *expr*이 *type* 인터페이스를 구현하는 형식의 인스턴스입니다.

case 식이 true이면 *varname*이 한정적으로 할당되고 switch 섹션 내의 로컬 범위만 갖습니다.

`null`은 형식과 일치하지 않습니다. `null`과 일치하려면 다음 `case` 레이블을 사용합니다.

```csharp
case null:
```

다음 예제에서는 형식 패턴을 사용하여 다양한 종류의 컬렉션 형식에 대한 정보를 제공합니다.

[!code-csharp[type-pattern#1](~/samples/snippets/csharp/language-reference/keywords/switch/type-pattern.cs#1)]

`object` 대신, 다음 코드와 같이 컬렉션 형식을 형식 매개 변수로 사용하여 제네릭 메서드를 만들 수 있습니다.

[!code-csharp[type-pattern#3](~/samples/snippets/csharp/language-reference/keywords/switch/type-pattern3.cs#1)]

제네릭 버전은 두 가지 측면에서 첫 번째 샘플과 다릅니다. 먼저 `null` case를 사용할 수 없습니다. 컴파일러가 임의 형식 `T`를 `object` 이외의 형식으로 변환할 수 없으므로 constant case를 사용할 수 없습니다. `default` case였던 항목이 이제 Null이 아닌 `object`에 대해 테스트됩니다. 즉, `default` case는 `null`에 대해서만 테스트됩니다.

패턴 일치를 사용하지 않을 경우 이 코드를 다음과 같이 작성할 수 있습니다. 형식 패턴 일치를 사용하면 변환 결과가 `null`인지 여부를 테스트하거나 반복된 캐스트를 수행할 필요가 없으므로 더욱 단순하고 읽기 쉬운 코드가 생성됩니다.

[!code-csharp[type-pattern2#1](~/samples/snippets/csharp/language-reference/keywords/switch/type-pattern2.cs#1)]

## <a name="a-namewhen--the-case-statement-and-the-when-clause"></a><a name="when" /> `case` 문 및 `when` 절

C# 7.0부터 case 문이 상호 배타적일 필요가 없으므로 `when` 절을 추가하여 case 문이 true로 평가되기 위해 충족해야 하는 추가 조건을 지정할 수 있습니다. `when` 절은 부울 값을 반환하는 모든 식일 수 있습니다.

다음 예제에서는 기본 `Shape` 클래스, `Shape`에서 파생된 `Rectangle` 클래스 및 `Rectangle`에서 파생된 `Square` 클래스를 정의합니다. `when` 절을 사용하여 `ShowShapeInfo`에서 `Square` 개체로 인스턴스화되지 않은 경우에도 동일한 길이 및 너비가 할당된 `Rectangle` 개체를 `Square`로 처리하도록 합니다. 이 메서드는 `null`인 개체나 면적이 0인 도형에 대한 정보를 표시하지 않습니다.

[!code-csharp[when-clause#1](~/samples/snippets/csharp/language-reference/keywords/switch/when-clause.cs#1)]

`Shape` 개체가 `null`인지 여부를 테스트하는 예제의 `when` 절은 실행되지 않습니다. `null`인지 테스트하는 올바른 형식 패턴은 `case null:`입니다.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](../language-specification/index.md)의 [switch 문](~/_csharplang/spec/statements.md#the-switch-statement)을 참조하세요. 언어 사양은 C# 구문 및 사용법에 대 한 신뢰할 수 있는 소스 됩니다.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [if-else](if-else.md)
- [패턴 일치](../../pattern-matching.md)
