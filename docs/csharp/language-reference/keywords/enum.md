---
title: enum 키워드 - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- enum
- enum_CSharpKeyword
helpviewer_keywords:
- enum keyword [C#]
ms.assetid: bbeb9a0f-e9b3-41ab-b0a6-c41b1a08974c
ms.openlocfilehash: fb11fb1a81b8407e2585e32d4217e08a75ea19b0
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69605826"
---
# <a name="enum-c-reference"></a>enum(C# 참조)

`enum` 키워드는 열거자 목록이라고 하는 명명된 상수 집합으로 구성된 고유 형식인 열거형을 선언하는 데 사용됩니다.

대개 네임스페이스의 모든 클래스가 같은 수준으로 열거형에 액세스할 수 있도록 네임스페이스 내에서 직접 열거형을 정의하는 것이 좋습니다. 하지만 특정 클래스나 구조체 내에 열거형이 중첩될 수도 있습니다.

기본적으로 첫 번째 열거자 값은 0이며 그 이후의 열거자 값은 순서대로 1씩 증가됩니다. 예를 들어 다음 열거형에서 `Sat` 은 `0`, `Sun` 은 `1`, `Mon` 은 `2`등입니다.

```csharp
enum Day {Sat, Sun, Mon, Tue, Wed, Thu, Fri};
```

다음 예제와 같이 열거자는 이니셜라이저를 사용하여 기본값을 재정의할 수 있습니다.

```csharp
enum Day {Sat=1, Sun, Mon, Tue, Wed, Thu, Fri};
```

이 열거형에서 요소의 순서는 `1` 대신 `0`부터 시작합니다. 그러나 값이 0인 상수를 포함하는 것이 좋습니다. 자세한 내용은 [열거형 형식](../../programming-guide/enumeration-types.md)을 참조하세요.

모든 열거형 형식에는 기본 형식이 있으며, 해당 형식은 [정수 숫자 형식](../builtin-types/integral-numeric-types.md)일 수 있습니다. [char](char.md) 형식은 열거형의 기본 형식일 수 없습니다. 열거형 요소의 기본적인 기본 형식은 i [int](../builtin-types/integral-numeric-types.md)입니다. [바이트](../builtin-types/integral-numeric-types.md)와 같은 다른 정수 형식의 열거형을 선언하려면 다음 예제에서와 같이 콜론을 사용하여 identifier 다음에 형식을 사용합니다.

```csharp
enum Day : byte {Sat=1, Sun, Mon, Tue, Wed, Thu, Fri};
```

열거형 형식의 변수에는 명명된 상수뿐 아니라 기본 형식의 범위에 있는 모든 값을 할당할 수 있습니다.

`enum E` 의 기본값은 식 `(E)0`으로 계산된 값입니다.

> [!NOTE]
> 열거자의 이름에는 공백이 포함될 수 없습니다.

기본 형식은 각 열거자에 할당될 스토리지 크기를 지정합니다. 그러나 `enum` 형식에서 정수 계열 형식으로 변환하려면 명시적 캐스트가 필요합니다. 예를 들어 다음 문은 `Sun` 을 [로 변환하는 캐스트를 사용하여 열거자](../builtin-types/integral-numeric-types.md) 을 `enum` int `int`형식 변수에 대입합니다.

```csharp
int x = (int)Day.Sun;
```

일부 요소가 비트 <xref:System.FlagsAttribute?displayProperty=nameWithType> 연산으로 결합될 수 있는 열거형에 `OR` 를 적용하면 일부 도구에서 이 열거형을 사용할 때 해당 특성이 `enum` 의 동작에 영향을 줍니다. <xref:System.Console> 클래스 메서드 및 식 계산기 등의 도구를 사용할 때 이러한 변경 사항을 확인할 수 있습니다. 세 번째 예제를 참조하세요.

## <a name="robust-programming"></a>강력한 프로그래밍

다른 상수와 마찬가지로, 컴파일 시간에 열거형의 개별 값에 대한 모든 참조는 숫자 리터럴로 변환됩니다. 따라서 [상수](../../programming-guide/classes-and-structs/constants.md)에서 설명하는 버전 문제가 발생할 가능성이 있습니다.

새 버전의 열거형에 값을 추가로 할당하거나 새 버전의 열거형 멤버 값을 변경하면 종속된 소스 코드에 문제가 발생할 수 있습니다. [switch](switch.md) 문에서 열거형 값이 사용되는 경우가 많습니다. `enum` 형식에 요소가 추가되었으면 switch 문의 기본 섹션을 예기치 않게 선택할 수 있습니다.

다른 개발자가 코드를 사용할 경우 `enum` 형식에 새 요소가 추가된다면 해당 코드에서 이를 적절히 처리할 수 있도록 지침을 제공해야 합니다.

## <a name="example"></a>예

다음 예제에서는 열거형 `Day`를 선언합니다. 두 개의 열거자를 명시적으로 정수로 변환하여 정수 변수에 대입합니다.

[!code-csharp[csrefKeywordsTypes#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#10)]

## <a name="example"></a>예

다음 예제에서는 base-type 옵션을 사용하여 멤버가 `enum` 형식인 `long`을 선언합니다. 열거형의 기본 형식이 `long`인 경우에도 캐스트를 사용하여 열거형 멤버를 `long` 형식으로 명시적으로 변환해야 합니다.

[!code-csharp[csrefKeywordsTypes#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#11)]

## <a name="example"></a>예

다음 코드 예제에서는 <xref:System.FlagsAttribute?displayProperty=nameWithType> 선언에 `enum` 특성을 사용하는 방법과 그 결과를 보여 줍니다.

[!code-csharp[csrefKeywordsTypes#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#12)]

## <a name="comments"></a>설명

`Flags`를 제거하면 예에 다음 값이 표시됩니다.

`5`

`5`

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [열거형 형식](../../programming-guide/enumeration-types.md)
- [C# 키워드](index.md)
- [정수 형식](../builtin-types/integral-numeric-types.md)
- [기본 제공 형식 표](built-in-types-table.md)
- [암시적 숫자 변환 표](implicit-numeric-conversions-table.md)
- [명시적 숫자 변환 표](explicit-numeric-conversions-table.md)
- [열거형 명명 규칙](../../../standard/design-guidelines/names-of-classes-structs-and-interfaces.md#naming-enumerations)
