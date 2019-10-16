---
title: '방법: String.Split(C# Guide)를 사용하여 문자열 구문 분석'
description: String.Split은 구분 기호 집합에서 분리된 문자열 배열을 반환합니다. 문자열을 구문 분석하는 쉬운 방법입니다.
ms.date: 01/03/2018
helpviewer_keywords:
- splitting strings [C#]
- Split method [C#]
- strings [C#], splitting
- parse strings
ms.assetid: 729c2923-4169-41c6-9c90-ef176c1e2953
ms.custom: mvc
ms.openlocfilehash: a8cb3a62497379f60e9cc6dec3d342192361f865
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54603723"
---
# <a name="how-to-parse-strings-using-stringsplit-c-guide"></a>방법: String.Split(C# Guide)를 사용하여 문자열 구문 분석

<xref:System.String.Split%2A?displayProperty=nameWithType> 메서드는 하나 이상의 구분 기호를 기준으로 입력 문자열을 분할하여 부분 문자열 배열을 만듭니다. 종종 단어 경계에서 문자열을 분리하는 가장 쉬운 방법입니다. 다른 특정 문자 또는 문자열에서 문자열을 분할하는 데도 사용됩니다.

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

다음 코드는 공통 어구를 각 단어에 대한 문자열의 배열로 나눕니다.

[!code-csharp-interactive[split strings on word boundaries](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#1)]

구분 문자의 모든 인스턴스는 반환된 배열에 값을 생성합니다. 연속된 구분 문자는 반환된 배열의 값으로 빈 문자열을 생성합니다.  다음 예제에서 공백을 구분 기호로 사용하여 내용을 확인할 수 있습니다.

[!code-csharp-interactive[split strings with repeated separators](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#2)]

이 동작은 표 형식 데이터를 나타내는 쉼표로 구분된 값(CSV) 파일과 같은 형식을 더 쉽게 만듭니다. 연속된 쉼표는 빈 열을 나타냅니다.

반환된 배열에 빈 문자열을 제외하기 위해 선택적인 <xref:System.StringSplitOptions.RemoveEmptyEntries?displayProperty=nameWithType> 매개 변수를 전달할 수 있습니다. 반환된 컬렉션의 더 복잡한 처리를 위해 [LINQ](../programming-guide/concepts/linq/index.md)를 사용하여 결과 시퀀스를 조작할 수 있습니다.

<xref:System.String.Split%2A?displayProperty=nameWithType>은 다중 구분 문자를 사용할 수 있습니다.
다음 예제에서는 공백, 쉼표, 마침표, 콜론 및 탭을 사용하며, 모두 이러한 구분 문자를 포함하는 배열에서 <xref:System.String.Split%2A>로 전달됩니다.
코드 맨 아래의 루프는 반환된 배열의 각 단어를 표시합니다.  

[!code-csharp-interactive[split strings using multiple separators](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#3)]

연속되는 모든 구분 기호의 인스턴스는 출력 배열에 빈 문자열을 생성합니다.

[!code-csharp-interactive[split strings using multiple consecutive separators](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#4)]

<xref:System.String.Split%2A?displayProperty=nameWithType>은 문자열 배열(단일 문자 대신 대상 문자열을 구문 분석하는 구분 기호 역할을 하는 문자 시퀀스)을 사용할 수 있습니다.  
  
[!code-csharp-interactive[split strings using strings as separators](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#5)]

[GitHub 리포지토리](https://github.com/dotnet/samples/tree/master/snippets/csharp/how-to/strings)의 코드를 확인하여 이러한 샘플을 시험해 볼 수 있습니다. 또는 샘플을 [zip 파일로](https://github.com/dotnet/samples/raw/master/snippets/csharp/how-to/strings.zip) 다운로드할 수 있습니다.

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../programming-guide/index.md)
- [문자열](../programming-guide/strings/index.md)
- [.NET 정규식](../../standard/base-types/regular-expressions.md)
