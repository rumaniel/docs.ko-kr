---
title: '방법: 문자열 비교 - C# 가이드'
description: 문화권별 순서 지정 여부나 대/소문자와 상관없이 문자열 값을 비교하고 정렬하는 방법에 대해 알아봅니다.
ms.date: 10/03/2018
helpviewer_keywords:
- strings [C#], comparison
- comparing strings [C#]
ms.openlocfilehash: bce234ca3a86f057ec35e1c53d22169ee29b7b94
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58759874"
---
# <a name="how-to-compare-strings-in-c"></a>C\#에서 문자열을 비교하는 방법

문자열을 비교하여 다음 두 가지 질문 중 하나를 해결할 수 있습니다. "이 두 문자열이 같나요?" 또는 "정렬할 때 이 문자열을 어떤 순서로 정렬해야 하는가?"

이러한 두 가지 질문은 문자열 비교에 영향을 주는 요소에 의해 복잡해 집니다.

- 서수 또는 언어 비교를 선택할 수 있습니다.
- 대/소문자를 구분할지 여부를 선택할 수 있습니다.
- 문화권별 비교를 선택할 수 있습니다.
- 언어적 비교는 문화권 및 플랫폼에 따라 다릅니다.

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

문자열을 비교할 때 순서를 정의합니다. 비교는 문자열 시퀀스를 정렬하는 데 사용됩니다. 시퀀스가 알려진 순서대로 되면 소프트웨어와 사람 모두를 검색하는 것이 더 쉽습니다. 다른 비교로 문자열이 같은지 확인할 수 있습니다. 이러한 동일성 검사는 동등 여부와 유사하지만 대/소문자 차이 같은 일부 차이점은 무시할 수 있습니다.

## <a name="default-ordinal-comparisons"></a>기본 서수 비교

가장 일반적인 작업인

- <xref:System.String.CompareTo%2A?displayProperty=nameWithType>
- <xref:System.String.Equals%2A?displayProperty=nameWithType>
- <xref:System.String.op_Equality%2A?displayProperty=nameWithType> 

은(는) 서수 비교, 대/소문자 구분 비교를 사용하고 현재 문화권을 사용합니다. 결과는 다음 예제에서 확인할 수 있습니다.

[!code-csharp-interactive[Comparing strings using an ordinal comparison](../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs#1)]

기본 서수 비교는 문자열을 비교할 때 언어 규칙을 고려하지 않습니다. 두 문자열에서 각 <xref:System.Char> 개체의 이진값을 비교합니다. 결과적으로, 기본 서수 비교도 대/소문자를 구분합니다. 

<xref:System.String.Equals%2A?displayProperty=nameWithType> 및 <xref:System.String.op_Equality%2A?displayProperty=nameWithType>의 같음에 대한 테스트는 <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 및 <xref:System.String.Compare(System.String,System.String)?displayProperty=nameWithType)> 메서드를 사용한 문자열 비교와 다릅니다. 같음에 대한 테스트가 대/소문자 구분 서수 비교를 수행하는 동안 비교 메서드는 현재 문화권을 사용하여 대/소문자 구분하고 문화권 구분 비교를 수행합니다. 기본 비교 메서드는 종종 다양한 유형의 비교를 수행하기 때문에 수행할 비교 형식을 명시적으로 지정하는 오버로드를 호출하여 코드의 의도를 항상 명확히 하는 것이 좋습니다.

## <a name="case-insensitive-ordinal-comparisons"></a>대/소문자를 구분하지 않는 서수 비교

<xref:System.String.Equals(System.String,System.StringComparison)?displayProperty=nameWithType> 메서드를 사용하면 <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType>의 <xref:System.StringComparison> 값을 지정하여
대/소문자를 구분하지 않는 서수 비교. <xref:System.StringComparison> 인수에 대해 <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> 값을 지정하는 경우 대/소문자를 구분 하지 않는 서수 비교를 수행하는 정적 <xref:System.String.Compare(System.String,System.String,System.StringComparison)?displayProperty=nameWithType> 메서드도 있습니다. 이는 다음 코드에서 확인할 수 있습니다.

[!code-csharp-interactive[Comparing strings ignoring case](../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs#2)]

대/소문자를 구분하지 않는 서수 비교를 수행하는 경우 이러한 메서드는 [고정 문화권](xref:System.Globalization.CultureInfo.InvariantCulture)의 대/소문자 규칙을 사용합니다.

## <a name="linguistic-comparisons"></a>언어 비교

또한 현재 문화권에 대한 언어 규칙을 사용하여 문자열을 정렬할 수 있습니다.
이를 종종 "단어 정렬 순서"라고 합니다. 언어 비교를 수행할 때 일부 영숫자가 아닌 유니코드 문자에 특별한 가중치가 할당될 수 있습니다. 예를 들어, 하이픈 "-"는 매우 작은 가중치가 할당될 수 있으므로 "co-op" 및 "coop"는 정렬 순서에 나란히 표시됩니다. 또한 일부 유니코드 문자는 <xref:System.Char> 인스턴스의 시퀀스와 동일할 수 있습니다. 다음 예에서는 "ss" 및 'ß'를 사용하여 독일어로 독일어에서는 "ss"(U+0073 U+0073)가 한 문자열에 있고 'ß'(U+00DF)가 다른 문자열에 있습니다. 언어적으로(Windows의 경우) "ss"는 "en-US" 및 "de-DE" 문화권에서 독일어 Esszet: 'ß' 문자와 같습니다.

[!code-csharp-interactive[Comparing strings using linguistic rules](../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs#3)]

이 샘플에서는 운영 체제별 언어 비교 특성을 보여줍니다. 대화형 창 호스트는 Linux 호스트입니다. 언어 및 서수 비교는 동일한 결과를 생성합니다. 이 샘플을 Windows 호스트에서 실행한 경우 다음과 같은 출력을 볼 수 있습니다.

```console
<coop> is less than <co-op> using invariant culture
<coop> is greater than <co-op> using ordinal comparison
<coop> is less than <cop> using invariant culture
<coop> is less than <cop> using ordinal comparison
<co-op> is less than <cop> using invariant culture
<co-op> is less than <cop> using ordinal comparison
```

Windows에서 언어 비교를 서수 비교로 변경하면 "cop", "coop" 및 "co-op"의 정렬 순서가 변경됩니다. 두 개의 독일어 문장도 서로 다른 비교 형식을 사용하여 다르게 비교됩니다.

## <a name="comparisons-using-specific-cultures"></a>특정 문화권을 사용한 비교

이 샘플은 en-US 및 de-DE 문화권에 대한 <xref:System.Globalization.CultureInfo> 개체를 저장합니다.
비교는 문화권별 비교를 보장하기 위해 <xref:System.Globalization.CultureInfo> 개체를 사용하여 수행됩니다.

사용된 문화권은 언어 비교에 영향을 줍니다. 다음 예에서는 "en-US" 문화권과 "de-DE" 문화권을 사용하여 두 개의 독일어 문장을 비교한 결과를 보여줍니다.

[!code-csharp-interactive[Comparing strings across cultures](../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs#4)]

문화권별 비교는 일반적으로 사용자가 입력한 문자열을 사용자가 입력한 다른 문자열과 비교하여 정렬하는 데 사용됩니다. 이러한 문자열의 문자 및 정렬 규칙은 사용자 컴퓨터의 로캘에 따라 달라질 수 있습니다. 똑같은 문자가 포함된 문자열이라도 현재 스레드의 문화권에 따라 다르게 정렬될 수 있습니다. 또한 이 샘플 코드를 Windows 컴퓨터에서 로컬로 시도하면 다음과 같은 결과가 나타납니다.

```console
<coop> is less than <co-op> using en-US culture
<coop> is greater than <co-op> using ordinal comparison
<coop> is less than <cop> using en-US culture
<coop> is less than <cop> using ordinal comparison
<co-op> is less than <cop> using en-US culture
<co-op> is less than <cop> using ordinal comparison
```

언어 비교는 현재 문화권에 따라 달라지며 OS에 종속됩니다. 문자열 비교 작업을 할 때 이 점을 고려해야 합니다.

## <a name="linguistic-sorting-and-searching-strings-in-arrays"></a>배열의 언어적 정렬 및 문자열 검색

다음 예에서는 현재 문화권에 따라 언어 비교를 사용하여 배열에서 문자열을 정렬하고 검색하는 방법을 보여줍니다. <xref:System.StringComparer?displayProperty=nameWithType> 매개 변수를 사용하는 정적 <xref:System.Array> 메서드를 사용합니다.

이 예에서는 현재 문화권을 사용하여 문자열 배열을 정렬하는 방법을 보여줍니다.

[!code-csharp-interactive[Sorting an array of strings](../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs#5)]

배열이 정렬되면 이진 검색을 사용하여 항목을 검색할 수 있습니다. 이진 검색은 컬렉션의 중간에서 시작하여 컬렉션의 절반에서 검색 문자열이 포함되어 있는지 확인합니다. 이후의 각 비교는 컬렉션의 나머지 부분을 절반으로 세분합니다.  배열은 <xref:System.StringComparer.CurrentCulture?displayProperty=nameWithType>을 사용하여 정렬됩니다. 로컬 함수 `ShowWhere`는 문자열이 발견된 위치에 대한 정보를 표시합니다. 문자열을 찾을 수 없는 경우 반환된 값은 발견된 그 위치를 나타냅니다. 

[!code-csharp-interactive[Searching in a sorted array](../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs#6)]

## <a name="ordinal-sorting-and-searching-in-collections"></a>컬렉션의 서수 정렬 및 검색

다음 코드에서는 <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> 컬렉션 클래스를 사용하여 문자열을 저장합니다. 문자열은 <xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=nameWithType> 메서드를 사용하여 정렬됩니다. 이 메서드에는 두 문자열을 비교하고 정렬하는 대리자가 필요합니다. <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 메서드는 비교 함수를 제공합니다. 이 샘플을 실행하고 순서를 관찰합니다. 이 정렬 작업은 서수 대/소문자 구분 정렬을 사용합니다. 정적 <xref:System.String.Compare%2A?displayProperty=nameWithType> 메서드를 사용하여 여러 비교 규칙을 지정합니다.

[!code-csharp-interactive[Sorting a list of strings](../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs#7)]

정렬된 후에는 이진 검색을 사용하여 문자열 목록을 검색할 수 있습니다. 다음 샘플에서는 동일한 비교 함수를 사용하여 정렬된 목록을 검색하는 방법을 보여줍니다. 로컬 함수 `ShowWhere`는 검색된 텍스트가 어디에 있는지를 보여줍니다.

[!code-csharp-interactive[csProgGuideStrings#11](../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs#8)]

정렬 및 검색 시 항상 동일한 형식의 비교를 사용하도록 하세요. 정렬 및 검색에 대해 서로 다른 비교 형식을 사용하면 예기치 않은 결과가 발생합니다.

<xref:System.Collections.Hashtable?displayProperty=nameWithType>, <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType>, <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> 등의 컬렉션 클래스는 요소 또는 키의 형식이 `string`인 경우 <xref:System.StringComparer?displayProperty=nameWithType> 매개 변수를 사용하는 생성자를 포함합니다. 일반적으로 가능하면 이러한 생성자를 사용하고 <xref:System.StringComparer.Ordinal?displayProperty=nameWithType> 또는 <xref:System.StringComparer.OrdinalIgnoreCase?displayProperty=nameWithType>를 지정해야 합니다.

## <a name="reference-equality-and-string-interning"></a>참조 동일성과 문자열 인터닝

샘플 중에 <xref:System.Object.ReferenceEquals%2A>를 사용한 것은 없습니다. 이 메서드는 두 문자열이 동일한 개체인지 확인합니다. 이로 인해 문자열 비교 시 일관성 없는 결과가 발생할 수 있습니다. 다음 예에서는 C#의 *문자열 인터닝* 기능을 보여줍니다. 프로그램이 두 개 이상의 동일 문자열 변수를 선언할 경우 컴파일러는 변수를 모두 같은 위치에 저장합니다. <xref:System.Object.ReferenceEquals%2A> 메서드를 호출하여 두 문자열이 실제로 메모리에서 같은 개체를 참조하는지 확인할 수 있습니다. 인터닝을 방지하려면 <xref:System.String.Copy%2A?displayProperty=nameWithType> 메서드를 사용합니다. 복사본이 생성된 후 두 개의 문자열은 동일한 값을 가지더라도 스토리지 위치가 다릅니다. `a` 및 `b`가 *인터닝*되었음을, 즉 동일한 스토리지를 공유한다는 것을 보여주는 다음 샘플을 실행합니다. 문자열 `a`와 `c`는 그렇지 않습니다.

[!code-csharp-interactive[Demonstrating string interning](../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs#9)]

> [!NOTE]
> 문자열의 동일성을 테스트할 때, 어떤 유형의 비교를 수행할지 명시적으로 지정하는 메서드를 사용해야 합니다. 코드를 훨씬 더 쉽게 유지 관리하고 읽을 수 있습니다. <xref:System.StringComparison> 열거형 매개 변수를 사용하는 <xref:System.String?displayProperty=nameWithType> 및 <xref:System.Array?displayProperty=nameWithType> 클래스의 메서드 오버로드를 사용합니다. 수행할 비교 형식을 지정합니다. 동일성을 테스트할 때 `==` 및 `!=` 연산자를 사용하지 않습니다. <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 인스턴스 메서드는 항상 서수 대/소문자 구분 비교를 수행합니다. 주로 알파벳순으로 문자열을 정렬하는 데 적합합니다.

<xref:System.String.Intern%2A?displayProperty=nameWithType> 메서드를 호출하여 문자열을 인터트하거나 기존의 인턴된 문자열에 대한 참조를 검색할 수 있습니다. 문자열이 인턴트되었는지 확인하려면 <xref:System.String.IsInterned%2A?displayProperty=nameWithType> 메서드를 호출합니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Globalization.CultureInfo?displayProperty=nameWithType>
- <xref:System.StringComparer?displayProperty=nameWithType>
- [문자열](../programming-guide/strings/index.md)
- [문자열 비교](../../standard/base-types/comparing.md)
- [애플리케이션 전역화 및 지역화](/visualstudio/ide/globalizing-and-localizing-applications)
