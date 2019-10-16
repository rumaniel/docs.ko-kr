---
title: '방법: 여러 문자열 연결(C# 가이드)'
description: C#에서 문자열을 연결하는 데는 여러 방법이 있습니다. 서로 다른 선택의 옵션과 이유에 대해 알아보세요.
ms.date: 02/20/2018
helpviewer_keywords:
- joining strings [C#]
- concatenating strings [C#]
- strings [C#], concatenation
ms.assetid: 8e16736f-4096-4f3f-be0f-9d4c3ff63520
ms.openlocfilehash: da83a79f58c236692e284a7920c7b98c3520e5d6
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54710419"
---
# <a name="how-to-concatenate-multiple-strings-c-guide"></a>방법: 여러 문자열 연결(C# 가이드)

*연결*은 한 문자열을 다른 문자열의 끝에 추가하는 프로세스입니다. `+` 연산자를 사용하여 문자열을 연결합니다. 문자열 리터럴 및 문자열 상수의 경우 연결 시 컴파일이 발생하며, 런타임 연결은 발생하지 않습니다. 문자열 변수의 경우 연결은 런타임에서만 발생합니다.

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

다음 예제에서는 소스 코드의 가독성을 향상하기 위해 긴 문자열 리터럴을 작은 문자열로 분할하기 위해 연결을 사용합니다. 분할된 문자열은 컴파일 시간에 단일 문자열로 연결됩니다. 이 경우 처리되는 문자열 수가 런타임 성능에 미치는 영향은 없습니다.  
  
 [!code-csharp-interactive[Combining strings at compile time](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#1)]  

문자열 변수를 연결하려면 `+` 또는 `+=` 연산자, [문자열 보간](../language-reference/tokens/interpolated.md) 또는 <xref:System.String.Format%2A?displayProperty=nameWithType>, <xref:System.String.Concat%2A?displayProperty=nameWithType>, <xref:System.String.Join%2A?displayProperty=nameWithType> 또는 <xref:System.Text.StringBuilder.Append%2A?displayProperty=nameWithType> 메서드를 사용할 수 있습니다. `+` 연산자는 사용하기 쉽고 직관적인 코드를 만듭니다. 하나의 문에서 여러 `+` 연산자를 사용해도 문자열 콘텐츠는 한 번만 복사됩니다. 다음 코드는 `+` 및 `+=` 연산자를 사용하여 문자열을 연결하는 예제를 보여줍니다.

[!code-csharp-interactive[combining strings using +](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#2)]  

일부 식에서는 다음 코드와 같이 문자열 보간을 사용하여 문자열을 연결하는 것이 더 쉽습니다.
  
[!code-csharp-interactive[building strings using string interpolation](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#3)]  
  
> [!NOTE]
> 문자열 연결 연산에서 C # 컴파일러는 null 문자열을 빈 문자열과 동일하게 처리합니다.

문자열을 연결하는 다른 메서드는 <xref:System.String.Format%2A?displayProperty=nameWithType>입니다. 이 메서드는 작은 수의 구성 요소 문자열에서 문자열을 빌드할 때 잘 작동합니다.

다른 경우는 결합하는 문자열의 개수를 모르는 루프에서 문자열을 결합할 수 있으며, 소스 문자열의 실제 개수는 매우 클 수 있습니다. <xref:System.Text.StringBuilder> 클래스는 이러한 시나리오를 위해 설계되었습니다. 다음 코드는 <xref:System.Text.StringBuilder> 클래스의 <xref:System.Text.StringBuilder.Append%2A> 메서드를 사용하여 문자열을 연결합니다.  
  
[!code-csharp-interactive[string concatenation using string builder](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#4)]  

[문자열 연결 또는 `StringBuilder` 클래스를 선택하는 이유](xref:System.Text.StringBuilder#StringAndSB)에 대해 자세히 읽을 수 있습니다.

컬렉션의 문자열을 조인하는 또 다른 옵션은 <xref:System.String.Concat%2A?displayProperty=nameWithType> 메서드를 사용하는 것입니다. 원본 문자열을 구분 기호로 구분해야 하는 경우 <xref:System.String.Join%2A?displayProperty=nameWithType> 메서드를 사용합니다. 다음 코드는 두 메서드 모두를 사용하여 단어 배열을 결합합니다.

[!code-csharp-interactive[concatenation of string collection](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#5)]

마지막으로 [LINQ](../programming-guide/concepts/linq/index.md)와 <xref:System.Linq.Enumerable.Aggregate%2A?displayProperty=nameWithType> 메서드를 사용하여 컬렉션의 문자열을 조인할 수 있습니다. 이 메서드는 람다 식을 사용하여 소스 문자열을 결합합니다. 람다 식은 각 문자열을 기존의 누적 문자열에 추가하는 작업을 수행합니다. 다음 예에서는 배열의 각 단어 사이에 공백을 추가하여 단어 배열을 결합합니다.

[!code-csharp-interactive[string concatenation using LINQ expressions](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#6)]  

[GitHub 리포지토리](https://github.com/dotnet/samples/tree/master/snippets/csharp/how-to/strings)의 코드를 확인하여 이러한 샘플을 시험해 볼 수 있습니다. 또는 샘플을 [zip 파일로](https://github.com/dotnet/samples/raw/master/snippets/csharp/how-to/strings.zip) 다운로드할 수 있습니다.

## <a name="see-also"></a>참고 항목

- <xref:System.String>
- <xref:System.Text.StringBuilder>
- [C# 프로그래밍 가이드](../programming-guide/index.md)
- [문자열](../programming-guide/strings/index.md)
