---
title: 문화권을 구분하지 않는 문자열 비교 수행
ms.date: 08/22/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- String.CompareTo method
- String.Compare method
- string comparison [.NET Framework], culture-insensitive
- strings [.NET Framework], comparing
- culture-insensitive string operations, comparisons
- culture parameter
ms.assetid: abae50ef-32f7-4a50-a540-fd256fd1aed0
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7b68d079413168b042412a67e8732e8afed66ffa
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69915874"
---
# <a name="performing-culture-insensitive-string-comparisons"></a>문화권을 구분하지 않는 문자열 비교 수행
기본적으로 <xref:System.String.Compare%2A?displayProperty=nameWithType> 메서드는 문화권 구분 및 대/소문자 구분 비교 작업을 수행합니다. 이 메서드에는 사용할 문화권을 지정할 수 있는 `culture` 매개 변수와 사용할 비교 규칙을 지정할 수 있는 `comparisonType` 매개 변수를 제공하는 몇 가지 오버로드도 포함되어 있습니다. 기본 오버로드 대신 이러한 메서드를 호출하면 특정 메서드 호출에서 사용되는 규칙에 대한 모든 모호성이 제거되고 특정 비교가 문화권을 구분하는지 여부가 명확히 나타납니다.  
  
> [!NOTE]
> <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 메서드의 두 오버로드는 문화권 구분 비교와 대/소문자 구분 비교를 수행합니다. 이 메서드를 사용하여 문화권을 구분하지 않는 비교를 수행할 수 없습니다. 코드의 명확성을 위해 <xref:System.String.Compare%2A?displayProperty=nameWithType> 메서드를 대신 사용하는 것이 좋습니다.  
  
 문화권 구분 작업의 경우 <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType> 또는 <xref:System.StringComparison.CurrentCultureIgnoreCase?displayProperty=nameWithType> 열거형 값을 `comparisonType` 매개 변수로 지정합니다. 현재 문화권이 아닌 지정된 문화권을 사용하여 문화권 구분 비교를 수행하려면 해당 문화권을 나타내는 <xref:System.Globalization.CultureInfo> 개체를 `culture` 매개 변수로 지정합니다.  
  
 <xref:System.String.Compare%2A?displayProperty=nameWithType> 메서드에서 지원하는 문화권을 구분하지 않는 문자열 비교는 언어적(고정 문화권의 정렬 규칙 기반)이거나 비언어적(문자열에 있는 문자의 서수 값 기반)입니다. 대부분의 문화권을 구분하지 않는 문자열 비교는 비언어적입니다. 이러한 비교의 경우 <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> 또는 <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> 열거형 값을 `comparisonType` 매개 변수로 지정합니다. 예를 들어 사용자 이름 또는 암호 비교와 같은 보안 결정이 문자열 비교의 결과를 기반으로 하는 경우 결과가 특정 문화권 또는 언어 규칙의 영향을 받지 않도록 작업이 문화권을 구분하지 않고 비언어적이어야 합니다.  
  
 여러 문화권의 언어적으로 관련된 문자열을 일관성 있게 처리하려면 문화권을 구분하지 않는 언어적 문자열 비교를 사용합니다. 예를 들어 애플리케이션에서 목록 상자에 여러 문자 집합을 사용하는 단어를 표시하는 경우 현재 문화권에 관계없이 동일한 순서로 단어를 표시하려고 할 수 있습니다. 문화권을 구분하지 않는 언어적 비교의 경우 .NET Framework에서는 영어의 언어적 규칙을 기반으로 하는 고정 문화권을 정의합니다. 문화권을 구분하지 않는 언어적 비교를 수행하려면 <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> 또는 <xref:System.StringComparison.InvariantCultureIgnoreCase?displayProperty=nameWithType>를 `comparisonType` 매개 변수로 지정합니다.  
  
 다음 예제에서는 문화권을 구분하지 않는 비언어적 문자열 비교를 두 가지 수행합니다. 첫 번째 비교는 대/소문자를 구분하지만 두 번째 비교는 대/소문자를 구분하지 않습니다.  
  
 [!code-csharp[Conceptual.Strings.CultureInsensitiveComparison#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.cultureinsensitivecomparison/cs/cultureinsensitive1.cs#1)]
 [!code-vb[Conceptual.Strings.CultureInsensitiveComparison#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.cultureinsensitivecomparison/vb/cultureinsensitive1.vb#1)]  

Windows 운영 체제에 대한 정렬 및 비교 작업에 사용되는 문자 가중치에 대한 정보를 포함하는 텍스트 파일의 집합, [가중치 테이블 정렬](https://www.microsoft.com/download/details.aspx?id=10921) 및 Linux 및 macOS의 정렬 가중치 테이블 [기본 유니코드 데이터 정렬 요소 테이블](https://www.unicode.org/Public/UCA/latest/allkeys.txt)을 다운로드할 수 있습니다.

## <a name="see-also"></a>참고 항목

- <xref:System.String.Compare%2A?displayProperty=nameWithType>
- <xref:System.String.CompareTo%2A?displayProperty=nameWithType>
- [Culture의 영향을 받지 않는 문자열 작업 수행](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations.md)
- [문자열 사용에 대한 모범 사례](../../../docs/standard/base-types/best-practices-strings.md)
