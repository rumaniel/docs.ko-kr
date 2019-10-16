---
title: unsafe 키워드 - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- unsafe_CSharpKeyword
- unsafe
helpviewer_keywords:
- unsafe keyword [C#]
ms.assetid: 7e818009-1c6e-4b9e-b769-3728a01586a0
ms.openlocfilehash: bca12c1dd8c79a5ae17e4a9b7b75d3c7b302fb89
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2019
ms.locfileid: "65875870"
---
# <a name="unsafe-c-reference"></a>unsafe(C# 참조)

`unsafe` 키워드는 포인터와 관련된 모든 작업에 필요한 안전하지 않은 컨텍스트를 나타냅니다. 자세한 내용은 [안전하지 않은 코드 및 포인터](../../programming-guide/unsafe-code-pointers/index.md)를 참조하세요.

형식 또는 멤버 선언에서 `unsafe` 한정자를 사용할 수 있습니다. 따라서 형식 또는 멤버의 전체 텍스트 범위가 안전하지 않은 컨텍스트로 간주됩니다. 예를 들어 다음은 `unsafe` 한정자를 사용하여 선언된 메서드입니다.

```csharp
unsafe static void FastCopy(byte[] src, byte[] dst, int count)
{
    // Unsafe context: can use pointers here.
}
```

안전하지 않은 컨텍스트의 범위는 매개 변수 목록에서 메서드의 끝까지 확장되므로 매개 변수 목록에 포인터를 사용할 수도 있습니다.

```csharp
unsafe static void FastCopy ( byte* ps, byte* pd, int count ) {...}
```

안전하지 않은 블록을 통해 이 블록 내에서 안전하지 않은 코드를 사용할 수도 있습니다. 예:

```csharp
unsafe
{
    // Unsafe context: can use pointers here.
}
```

안전하지 않은 코드를 컴파일하려면 [`-unsafe`](../compiler-options/unsafe-compiler-option.md) 컴파일러 옵션을 지정해야 합니다. 안전하지 않은 코드는 공용 언어 런타임에서 확인할 수 없습니다.

## <a name="example"></a>예제

[!code-csharp[csrefKeywordsModifiers#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#22)]

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](../language-specification/index.md)의 [안전하지 않은 코드](~/_csharplang/spec/unsafe-code.md)를 참조하세요. 언어 사양은 C# 구문 및 사용법에 대 한 신뢰할 수 있는 소스 됩니다.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [fixed 문](fixed-statement.md)
- [안전하지 않은 코드 및 포인터](../../programming-guide/unsafe-code-pointers/index.md)
- [고정 크기 버퍼](../../programming-guide/unsafe-code-pointers/fixed-size-buffers.md)
