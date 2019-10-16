---
title: const 키워드 - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- const_CSharpKeyword
- const
helpviewer_keywords:
- const keyword [C#]
ms.assetid: 79eb447c-117b-4418-933f-97c50aa472db
ms.openlocfilehash: 2a2e4bb45d21708ea3971d2f5b784280b9d13d0d
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69605889"
---
# <a name="const-c-reference"></a>const(C# 참조)

상수 필드 또는 지역 상수를 선언할 때는 `const` 키워드를 사용합니다. 상수 필드 및 지역 상수는 변수가 아니며 수정할 수 없습니다. 상수는 숫자, 부울 값, 문자열 또는 null 참조일 수 있습니다. 언제든지 변경될 수 있는 정보를 나타낼 때는 상수를 만들지 마세요. 예를 들어, 상수 필드를 사용하여 서비스의 가격, 제품 버전 번호 또는 회사의 브랜드 이름을 저장하지 마세요. 이러한 값은 시간이 지남에 따라 변경될 수 있으며, 컴파일러는 상수를 전파하므로 변경 내용을 보기 위해서는 라이브러리를 사용하여 컴파일된 다른 코드를 다시 컴파일해야 합니다. [readonly](./readonly.md) 키워드를 참조하세요. 예:

```csharp
const int X = 0;
public const double GravitationalConstant = 6.673e-11;
private const string ProductName = "Visual C#";
```

## <a name="remarks"></a>설명

상수 선언 형식은 선언에서 제공하는 멤버의 형식을 지정합니다. 지역 상수 또는 상수 필드의 이니셜라이저는 대상 형식으로 암시적으로 변환될 수 있는 상수 식이어야 합니다.

상수 식은 컴파일 시간에 완전히 계산될 수 있는 식입니다. 따라서 참조 형식의 상수에 대해 가능한 값은 `string` 및 null 참조뿐입니다.

상수 선언에서는 다음과 같이 여러 상수를 선언할 수 있습니다.

```csharp
public const double X = 1.0, Y = 2.0, Z = 3.0;
```

`static` 한정자는 상수 선언에는 허용되지 않습니다.

상수는 다음과 같이 상수 식에 참여할 수 있습니다.

```csharp
public const int C1 = 5;
public const int C2 = C1 + 100;
```

> [!NOTE]
> [readonly](./readonly.md) 키워드는 `const` 키워드와 다릅니다. `const` 필드는 필드 선언에서만 초기화될 수 있습니다. `readonly` 필드는 선언이나 생성자에서 초기화될 수 있습니다. 따라서 `readonly` 필드는 사용된 생성자에 따라 다른 값을 가질 수 있습니다. 또한 `const` 필드가 컴파일 시간 상수라고 하더라도 `readonly` 필드는 다음 줄에서와 같이 런타임 상수에 사용될 수 있습니다. `public static readonly uint l1 = (uint)DateTime.Now.Ticks;`

## <a name="example"></a>예

[!code-csharp[csrefKeywordsModifiers#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#5)]

## <a name="example"></a>예

이 예제에서는 상수를 지역 변수로 사용하는 방법을 보여 줍니다.

[!code-csharp[csrefKeywordsModifiers#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#6)]

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](./index.md)
- [한정자](./modifiers.md)
- [readonly](./readonly.md)
