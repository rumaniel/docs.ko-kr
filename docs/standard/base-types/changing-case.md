---
title: .NET에서 대/소문자 바꾸기
description: .NET에서 문자열의 경우 변경하는 방법을 알아봅니다.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- strings [.NET Framework], case
- case sensitivity
- ToUpper method
- ToLower method
- uppercase
- lowercase
ms.assetid: 6805f81b-e9ad-4387-9f4c-b9bdb21b87c0
author: rpetrusha
ms.author: ronpet
ms.custom: seodec18
ms.openlocfilehash: 68bce927c6426fc32cd2fe26dcc488432199612d
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69987199"
---
# <a name="changing-case-in-net"></a>.NET에서 대/소문자 바꾸기
사용자 입력을 수락하는 애플리케이션을 작성하는 경우 데이터를 입력할 때 사용하는 대/소문자를 확신할 수 없습니다. 특히 사용자 인터페이스에 표시하는 경우 문자열의 대/소문자를 일관되게 표시하려는 경우가 많습니다. 다음 표에서는 세 가지 대/소문자 변경 메서드를 설명합니다. 처음 두 메서드는 문화권을 수락하는 오버로드를 제공합니다.  
  
|메서드 이름|기능|  
|-----------------|---------|  
|<xref:System.String.ToUpper%2A?displayProperty=nameWithType>|문자열의 모든 문자를 대문자로 변환합니다.|  
|<xref:System.String.ToLower%2A?displayProperty=nameWithType>|문자열의 모든 문자를 소문자로 변환합니다.|  
|<xref:System.Globalization.TextInfo.ToTitleCase%2A?displayProperty=nameWithType>|문자열에서 단어의 첫 글자를 대문자로 변환합니다.|  
  
> [!WARNING]
> 문자열을 비교하거나 같은지 테스트하기 위해 <xref:System.String.ToUpper%2A?displayProperty=nameWithType> 및 <xref:System.String.ToLower%2A?displayProperty=nameWithType> 메서드를 사용하여 문자열을 변환하면 안 됩니다. 자세한 내용은 [대/소문자가 혼합된 문자열 비교](#Comparing) 섹션을 참조하세요.  
  
<a name="Comparing"></a>   
## <a name="comparing-strings-of-mixed-case"></a>대/소문자가 혼합된 문자열 비교  
 대/소문자가 혼합된 문자열을 비교하여 순서를 확인하려면 <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 메서드의 오버로드 중 하나를 `comparisonType` 매개 변수와 함께 호출하고 `comparisonType` 인수에 대해 <xref:System.StringComparison.CurrentCultureIgnoreCase?displayProperty=nameWithType>, <xref:System.StringComparison.InvariantCultureIgnoreCase?displayProperty=nameWithType> 또는 <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> 값을 제공합니다. 현재 문화권이 아닌 특정 문화권을 사용하여 비교하려면 <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 메서드의 오버로드를 `culture` 및 `options` 매개 변수 둘 다와 함께 호출하고 `options` 인수로 <xref:System.Globalization.CompareOptions.IgnoreCase?displayProperty=nameWithType> 값을 제공합니다.  
  
 대/소문자가 혼합된 문자열을 비교하여 같은지 확인하려면 <xref:System.String.Equals%2A?displayProperty=nameWithType> 메서드의 오버로드 중 하나를 `comparisonType` 매개 변수와 함께 호출하고 `comparisonType` 인수에 대해 <xref:System.StringComparison.CurrentCultureIgnoreCase?displayProperty=nameWithType>, <xref:System.StringComparison.InvariantCultureIgnoreCase?displayProperty=nameWithType> 또는 <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> 값을 제공합니다.  
  
 자세한 내용은 [문자열 사용에 대한 모범 사례](../../../docs/standard/base-types/best-practices-strings.md)를 참조하세요.  
  
## <a name="toupper"></a>ToUpper  
 <xref:System.String.ToUpper%2A?displayProperty=nameWithType> 메서드는 문자열의 모든 문자를 대문자로 변경합니다. 다음 예제에서는 "Hello World!" 문자열을 대/소문자 혼합에서 대문자로 변환합니다.  
  
 [!code-csharp[Strings.ChangingCase#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.ChangingCase/cs/Example.cs#1)]
 [!code-vb[Strings.ChangingCase#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.ChangingCase/vb/Example.vb#1)]  
  
 앞의 예제는 기본적으로 문화권을 구분합니다. 기본적으로 현재 문화권의 대/소문자 규칙을 적용합니다. 문화권을 구분하지 않는 대/소문자 변경을 수행하거나 특정 문화권의 대/소문자 규칙을 적용하려면 <xref:System.String.ToUpper%28System.Globalization.CultureInfo%29?displayProperty=nameWithType> 메서드 오버로드를 사용하고 지정된 문화권을 나타내는 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 값 또는 <xref:System.Globalization.CultureInfo?displayProperty=nameWithType> 개체를 *culture* 매개 변수에 제공합니다. <xref:System.String.ToUpper%2A> 메서드를 사용하여 문화권을 구분하지 않는 대/소문자 변경을 수행하는 방법을 보여주는 예제는 [문화권을 구분하지 않는 대/소문자 변경 수행](../../../docs/standard/globalization-localization/performing-culture-insensitive-case-changes.md)을 참조하세요.  
  
## <a name="tolower"></a>ToLower  
 <xref:System.String.ToLower%2A?displayProperty=nameWithType> 메서드는 이전 메서드와 비슷하지만 대신 문자열의 모든 문자를 소문자로 변환합니다. 다음 예제에서는 "Hello World!" 문자열을 소문자로 변환합니다.  
  
 [!code-csharp[Strings.ChangingCase#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.ChangingCase/cs/Example.cs#2)]
 [!code-vb[Strings.ChangingCase#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.ChangingCase/vb/Example.vb#2)]  
  
 앞의 예제는 기본적으로 문화권을 구분합니다. 기본적으로 현재 문화권의 대/소문자 규칙을 적용합니다. 문화권을 구분하지 않는 대/소문자 변경을 수행하거나 특정 문화권의 대/소문자 규칙을 적용하려면 <xref:System.String.ToLower%28System.Globalization.CultureInfo%29?displayProperty=nameWithType> 메서드 오버로드를 사용하고 지정된 문화권을 나타내는 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 값 또는 <xref:System.Globalization.CultureInfo?displayProperty=nameWithType> 개체를 *culture* 매개 변수에 제공합니다. <xref:System.String.ToLower%28System.Globalization.CultureInfo%29> 메서드를 사용하여 문화권을 구분하지 않는 대/소문자 변경을 수행하는 방법을 보여주는 예제는 [문화권을 구분하지 않는 대/소문자 변경 수행](../../../docs/standard/globalization-localization/performing-culture-insensitive-case-changes.md)을 참조하세요.  
  
## <a name="totitlecase"></a>ToTitleCase  
 <xref:System.Globalization.TextInfo.ToTitleCase%2A?displayProperty=nameWithType>는 각 문자의 첫 문자를 대문자로 변환하고 나머지 문자를 소문자로 변환합니다. 그러나 전체적으로 대문자인 단어는 머리글자어로 간주되며 변환되지 않습니다.  
  
 <xref:System.Globalization.TextInfo.ToTitleCase%2A?displayProperty=nameWithType> 메서드는 문화권을 구분합니다. 즉, 특정 문화권의 대/소문자 규칙을 사용합니다. 메서드를 호출하려면 먼저 특정 문화권의 <xref:System.Globalization.CultureInfo.TextInfo%2A?displayProperty=nameWithType> 속성에서 특정 문화권의 대/소문자 규칙을 나타내는 <xref:System.Globalization.TextInfo> 개체를 검색합니다.  
  
 다음 예제에서는 배열의 각 문자열을 <xref:System.Globalization.TextInfo.ToTitleCase%2A?displayProperty=nameWithType> 메서드에 전달합니다.  문자열에는 적절한 제목 문자열과 머리글자어가 포함됩니다. 영어(미국) 문화권의 대/소문자 규칙을 사용하여 문자열에서 단어의 첫 글자가 대문자로 변환됩니다.  
  
 [!code-csharp[System.Globalization.TextInfo.ToTitleCase#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.globalization.textinfo.totitlecase/cs/totitlecase2.cs#1)]
 [!code-vb[System.Globalization.TextInfo.ToTitleCase#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.globalization.textinfo.totitlecase/vb/totitlecase2.vb#1)]  
  
 문화권을 구분하지만 <xref:System.Globalization.TextInfo.ToTitleCase%2A?displayProperty=nameWithType> 메서드는 언어학적으로 올바른 대/소문자 규칙을 제공하지 않습니다. 예를 들어 앞의 예제에서 메서드는 "a tale of two cities"를 "A Tale Of Two Cities"로 변환합니다. 그러나 en-US 문화권에서 언어적으로 올바른 단어의 첫 글자를 대문자로 변환은 "A Tale of Two Cities"입니다.  
  
## <a name="see-also"></a>참고 항목

- [기본적인 문자열 작업](../../../docs/standard/base-types/basic-string-operations.md)
- [Culture의 영향을 받지 않는 문자열 작업 수행](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations.md)
