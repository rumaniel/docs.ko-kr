---
title: char 키워드 - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- char
- char_CSharpKeyword
helpviewer_keywords:
- char data type [C#]
ms.assetid: b51cf4fb-124c-4067-af48-afbac122b228
ms.openlocfilehash: 63f8871926e8c279678c59a2256bef46b2ff514e
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698784"
---
# <a name="char-c-reference"></a>char(C# 참조)

`char` 키워드는 .NET Framework에서 유니코드 문자를 표현하는 데 사용하는 <xref:System.Char?displayProperty=nameWithType> 구조체의 인스턴스를 선언하는 데 사용됩니다. `Char` 개체의 값은 16비트 숫자(서수) 값입니다.

 유니코드 문자는 전 세계에서 대부분의 문자 체계를 표현하는 데 사용됩니다.

|형식|범위|크기|.NET 형식|
|----------|-----------|----------|-------------------------|
|`char`|U+0000~U+FFFF|유니코드 16비트 문자|<xref:System.Char?displayProperty=nameWithType>|

## <a name="literals"></a>리터럴

`char` 형식의 상수는 문자 리터럴, 16진수 이스케이프 시퀀스 또는 유니코드 표현으로 기록될 수 있습니다. 정수 문자 코드를 캐스트할 수도 있습니다. 다음 예제에서는 `char` 배열의 네 요소가 같은 문자 `X`로 초기화됩니다.

[!code-csharp[csrefKeywordsTypes#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#19)]

## <a name="conversions"></a>변환

`char`는 [ushort](../builtin-types/integral-numeric-types.md), [int](../builtin-types/integral-numeric-types.md), [uint](../builtin-types/integral-numeric-types.md), [double](../builtin-types/floating-point-numeric-types.md) 또는 [decimal](../builtin-types/floating-point-numeric-types.md)로 암시적으로 변환될 수 있습니다. 그러나 기타 형식에서 `char` 형식으로의 암시적 변환은 없습니다.

<xref:System.Char?displayProperty=nameWithType> 형식은 `char` 값 작업을 위한 몇 가지 정적 메서드를 제공합니다.

## <a name="c-language-specification"></a>C# 언어 사양  

자세한 내용은 [C# 언어 사양](../language-specification/index.md)의 [정수 형식](~/_csharplang/spec/types.md#integral-types)을 참조하세요. 언어 사양은 C# 구문 및 사용법에 대 한 신뢰할 수 있는 소스 됩니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Char>
- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](./index.md)
- [정수 형식](../builtin-types/integral-numeric-types.md)
- [기본 제공 형식 표](./built-in-types-table.md)
- [암시적 숫자 변환 표](./implicit-numeric-conversions-table.md)
- [명시적 숫자 변환 표](./explicit-numeric-conversions-table.md)
- [문자열](../../programming-guide/strings/index.md)
