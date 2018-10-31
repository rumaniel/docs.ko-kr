---
title: string(C# 참조)
ms.date: 07/20/2015
f1_keywords:
- string
- string_CSharpKeyword
helpviewer_keywords:
- strings [C#], reference
- '@ string literal'
- string literals [C#]
- string keyword [C#]
ms.assetid: 3037e558-fb22-494d-bca1-a15ade11b11a
ms.openlocfilehash: ab2e69c60872aed19d46450f17becc918ffe2a38
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50181462"
---
# <a name="string-c-reference"></a>string(C# 참조)

`string` 형식은 0자 이상의 유니코드 문자 시퀀스를 나타냅니다. `string`는 .NET에서 <xref:System.String>의 별칭입니다.

`string`은 참조 형식이지만 같음 연산자(`==` 및 `!=`)는 참조가 아니라 `string` 개체의 값을 비교하도록 정의됩니다. 이 때문에 좀 더 직관적으로 문자열이 같은지 테스트할 수 있습니다. 예:

```csharp
string a = "hello";
string b = "h";
// Append to contents of 'b'
b += "ello";
Console.WriteLine(a == b);
Console.WriteLine((object)a == (object)b);
```

이 코드는 "True"를 표시한 다음 "False"를 표시하며, 이는 문자열의 내용이 동일하지만 `a`와 `b`는 동일한 문자열 인스턴스를 가리키지 않기 때문입니다.

+ 연산자는 문자열을 연결합니다.

```csharp
string a = "good " + "morning";
```

이 경우 "good morning"이 포함된 문자열 개체가 생성됩니다.

문자열은 *변경할 수 없습니다*. 구문상 가능한 것처럼 보여도 개체를 만든 후에는 문자열 개체의 내용을 변경할 수 없습니다. 예를 들어 이 코드를 작성하면 컴파일러에서 실제로 새 문자 시퀀스가 포함될 새 문자열 개체를 만들고, 새 개체가 b에 할당됩니다. 그런 다음 문자열 "h"는 가비지 수집 대상이 됩니다.

```csharp
string b = "h";
b += "ello";
```

`string`의 개별 문자에 대한 읽기 전용 액세스를 위해 [] 연산자를 사용할 수 있습니다.

```csharp
string str = "test";
char x = str[2];  // x = 's';
```

문자열 리터럴은 `string` 형식이며, quoted 및 @-quoted의 두 가지 형태로 작성될 수 있습니다. 따옴표가 있는 문자열 리터럴은 큰따옴표(")로 묶여 있습니다.

```csharp
"good morning"  // a string literal
```

문자열 리터럴에는 모든 문자 리터럴이 포함될 수 있습니다. 이스케이프 시퀀스가 포함됩니다. 다음 예제에서는 이스케이프 시퀀스 `\\`를 백슬래시에 사용하고, `\u0066`을 f에 사용하고, `\n`을 줄 바꿈에 사용합니다.

```csharp
string a = "\\\u0066\n";
Console.WriteLine(a);
```

> [!NOTE]
> 이스케이프 코드 `\udddd`(여기서 `dddd`는 4자리 숫자)는 유니코드 문자 U+`dddd`를 나타냅니다. 8자리 유니코드 이스케이프 코드 `\Udddddddd`도 인식됩니다.

축자 문자열 리터럴은 `@`로 시작하며 큰따옴표로 묶여 있습니다. 예:

```csharp
@"good morning"  // a string literal
```

축자 문자열의 장점은 이스케이프 시퀀스가 처리되지 *않으므로*, 정규화된 파일 이름 등을 쉽게 쓸 수 있다는 것입니다.

```csharp
@"c:\Docs\Source\a.txt"  // rather than "c:\\Docs\\Source\\a.txt"
```

@-quoted 문자열에 큰따옴표를 포함하려면 큰따옴표로 묶습니다.

```csharp
@"""Ahoy!"" cried the captain." // "Ahoy!" cried the captain.
```

`@` 특수 문자의 다른 용도는 [@ - 축자 식별자](../tokens/verbatim.md)를 참조하세요.

C#의 문자열에 대한 자세한 내용은 [문자열](../../programming-guide/strings/index.md)을 참조하세요.

## <a name="example"></a>예

[!code-csharp[csrefKeywordsTypes#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#17)]  

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [문자열 사용에 대한 모범 사례](../../../standard/base-types/best-practices-strings.md)
- [C# 키워드](index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [참조 형식](reference-types.md)
- [값 형식](value-types.md)
- [기본적인 문자열 작업](../../../standard/base-types/basic-string-operations.md)
- [새 문자열 만들기](../../../standard/base-types/creating-new.md)
- [숫자 결과 형식 지정 표](formatting-numeric-results-table.md)