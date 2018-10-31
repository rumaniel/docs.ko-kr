---
title: short(C# 참조)
ms.date: 03/14/2017
f1_keywords:
- short
- short_CSharpKeyword
helpviewer_keywords:
- short keyword [C#]
ms.assetid: 04c10688-e51a-4a87-bfec-83f7fb42ff11
ms.openlocfilehash: 0d90f31da49b94eee490e95f0cdf1d582bb0b059
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50184155"
---
# <a name="short-c-reference"></a>short(C# 참조)

`short`는 다음 표에 나와 있는 크기와 범위에 따라 값을 저장하는 정수 데이터 형식을 나타냅니다.

|형식|범위|크기|.NET 형식|
|----------|-----------|----------|-------------------------|
|`short`|–32,768 ~ 32,767|부호 있는 16비트 정수|<xref:System.Int16?displayProperty=nameWithType>|

## <a name="literals"></a>리터럴

10진수 리터럴, 16진수 리터럴 또는 (C# 7.0부터) 이진 리터럴을 할당하여 `short` 변수를 선언하고 초기화할 수 있습니다.  정수 리터럴이 `short` 범위를 벗어나는 경우(즉 <xref:System.Int16.MinValue?displayProperty=nameWithType>보다 작거나 <xref:System.Int16.MaxValue?displayProperty=nameWithType>보다 큰 경우) 컴파일 오류가 발생합니다.

다음 예제에서는 10진수, 16진수 및 이진 리터럴로 표현된 1,034와 같은 정수가 [int](int.md)에서 `short` 값으로 암시적으로 변환됩니다.

[!code-csharp[Short](~/samples/snippets/csharp/language-reference/keywords/numeric-literals.cs#Short)]

> [!NOTE]
> `0x` 또는 `0X` 접두사를 사용하여 16진수 리터럴을 나타내고, `0b` 또는 `0B` 접두사를 사용하여 이진 리터럴을 나타냅니다. 10진수 리터럴에는 접두사가 없습니다.

C# 7.0부터 가독성 향상을 위해 몇 가지 기능이 추가됐습니다.

- C# 7.0은 숫자 구분 기호로 밑줄 문자 `_`를 사용할 수 있습니다.
- C# 7.2는 접두사 뒤에 이진 또는 16진수 리터럴에 대한 자리 구분 기호로 `_`을 사용할 수 있습니다. 10진수 리터럴에 선행 밑줄이 있는 것이 허용되지 않습니다.

일부 예제는 다음과 같습니다.

[!code-csharp[Short](~/samples/snippets/csharp/language-reference/keywords/numeric-literals.cs#ShortS)]

## <a name="compiler-overload-resolution"></a>컴파일러 오버로드 확인

오버로드된 메서드를 호출할 때 캐스트를 사용해야 합니다. 예를 들어 `short` 및 [int](int.md) 매개 변수를 사용하는 다음의 오버로드된 메서드를 살펴보세요.

```csharp
public static void SampleMethod(int i) {}
public static void SampleMethod(short s) {}
```

`short` 캐스트를 사용하면 올바른 형식이 호출됩니다. 예를 들면 다음과 같습니다.

```csharp
SampleMethod(5);         // Calling the method with the int parameter
SampleMethod((short)5);  // Calling the method with the short parameter
```

## <a name="conversions"></a>변환

`short`에서 [int](int.md), [long](long.md), [float](float.md), [double](double.md) 또는 [decimal](decimal.md)로 미리 정의된 암시적 변환이 있습니다.

더 큰 저장소 크기의 비리터럴 숫자 형식을 `short`로 암시적으로 변환할 수는 없습니다(정수 형식의 저장소 크기는 [정수 형식 표](integral-types-table.md) 참조). 예를 들어 다음 두 가지 `short` 변수 `x` 및 `y`를 고려해 보세요.

```csharp
short x = 5, y = 12;
```

다음 대입문은 대입 연산자의 오른쪽에 있는 산술 식이 기본적으로 [int](int.md)로 계산되므로 컴파일 오류를 생성합니다.

```csharp
short z  = x + y;        // Compiler error CS0266: no conversion from int to short
```

이 문제를 해결하려면 다음 캐스트를 사용합니다.

```csharp
short z  = (short)(x + y);   // Explicit conversion
```

대상 변수에 동일한 저장소 크기 또는 더 큰 저장소 크기가 있는 다음 문을 사용할 수도 있습니다.

```csharp
int m = x + y;
long n = x + y;
```

부동 소수점 형식에서 `short`로의 암시적 변환은 없습니다. 예를 들어 명시적 캐스트를 사용하지 않는 경우 다음 문은 컴파일러 오류를 일으킵니다.

```csharp
short x = 3.0;          // Error: no implicit conversion from double
short y = (short)3.0;   // OK: explicit conversion
```

부동 소수점 형식 및 정수 형식이 혼합된 산술 식에 대한 자세한 내용은 [float](float.md) 및 [double](double.md)을 참조하세요.

암시적 숫자 변환 규칙에 대한 자세한 내용은 [암시적 숫자 변환 표](implicit-numeric-conversions-table.md)를 참조하세요.

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- <xref:System.Int16>
- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [정수 계열 형식 표](integral-types-table.md)
- [기본 제공 형식 표](built-in-types-table.md)
- [암시적 숫자 변환 표](implicit-numeric-conversions-table.md)
- [명시적 숫자 변환 표](explicit-numeric-conversions-table.md)