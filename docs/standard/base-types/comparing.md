---
title: .NET에서 문자열 비교
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- value comparisons of strings
- LastIndexOf method
- CompareTo method
- IndexOf method
- Compare method
- strings [.NET Framework], comparing
- CompareOrdinal method
- EndsWith method
- Equals method
- StartsWith method
ms.assetid: 977dc094-fe19-4955-98ec-d2294d04a4ba
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: dd5ec18147c074400457581618bacba11d9ee40a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963414"
---
# <a name="comparing-strings-in-net"></a>.NET에서 문자열 비교
.NET에서는 문자열의 값을 비교하는 여러 가지 메서드를 제공합니다. 다음 표에서는 값 비교 메서드를 나열하고 설명합니다.  
  
|메서드 이름|기능|  
|-----------------|---------|  
|<xref:System.String.Compare%2A?displayProperty=nameWithType>|두 문자열의 값을 비교합니다. 정수 값을 반환합니다.|  
|<xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType>|로컬 문화권에 관계없이 두 문자열을 비교합니다. 정수 값을 반환합니다.|  
|<xref:System.String.CompareTo%2A?displayProperty=nameWithType>|현재 문자열 개체를 다른 문자열과 비교합니다. 정수 값을 반환합니다.|  
|<xref:System.String.StartsWith%2A?displayProperty=nameWithType>|문자열이 전달된 문자열로 시작하는지 여부를 확인합니다. 부울 값을 반환합니다.|  
|<xref:System.String.EndsWith%2A?displayProperty=nameWithType>|문자열이 전달된 문자열로 끝나는지 여부를 확인합니다. 부울 값을 반환합니다.|  
|<xref:System.String.Equals%2A?displayProperty=nameWithType>|두 문자열이 같은지 여부를 확인합니다. 부울 값을 반환합니다.|  
|<xref:System.String.IndexOf%2A?displayProperty=nameWithType>|검사 중인 문자열의 처음부터 시작하여 문자 또는 문자열의 인덱스 위치를 반환합니다. 정수 값을 반환합니다.|  
|<xref:System.String.LastIndexOf%2A?displayProperty=nameWithType>|검사 중인 문자열의 끝부터 시작하여 문자 또는 문자열의 인덱스 위치를 반환합니다. 정수 값을 반환합니다.|  
  
## <a name="compare"></a>비교  
 정적 <xref:System.String.Compare%2A?displayProperty=nameWithType> 메서드는 두 문자열을 비교하는 철저한 방법을 제공합니다. 이 메서드는 문화권을 인식합니다. 이 함수를 사용하여 두 문자열 또는 두 문자열의 부분 문자열을 비교할 수 있습니다. 또한 대/소문자와 문화권 차이를 반영하거나 무시하는 오버로드가 제공됩니다. 다음 표에서는 이 메서드가 반환할 수 있는 세 가지 정수 값을 보여 줍니다.  
  
|반환 값|조건|  
|------------------|---------------|  
|음의 정수|정렬 순서에서 첫 번째 문자열이 두 번째 문자열 앞에 옵니다.<br /><br /> 또는<br /><br /> 첫 번째 문자열이 `null`입니다.|  
|0|첫 번째 문자열과 두 번째 문자열이 같습니다.<br /><br /> 또는<br /><br /> 두 문자열이 모두 `null`입니다.|  
|양의 정수<br /><br /> 또는<br /><br /> 1|정렬 순서에서 첫 번째 문자열이 두 번째 문자열 뒤에 옵니다.<br /><br /> 또는<br /><br /> 두 번째 문자열이 `null`입니다.|  
  
> [!IMPORTANT]
> <xref:System.String.Compare%2A?displayProperty=nameWithType> 메서드는 주로 문자열의 순서를 지정하거나 정렬할 때 사용됩니다. <xref:System.String.Compare%2A?displayProperty=nameWithType> 메서드를 통해 같은지 여부를 테스트하면 안 됩니다(즉, 한 문자열이 다른 문자열보다 작거나 큰지에 관계없이 반환 값 0을 명시적으로 찾기 위해 사용하면 안 됨). 대신, 두 문자열이 같은지 여부를 확인하려면 <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> 메서드를 사용합니다.  
  
 다음 예제에서는 <xref:System.String.Compare%2A?displayProperty=nameWithType> 메서드를 사용하여 두 문자열의 상대 값을 확인합니다.  
  
 [!code-cpp[Conceptual.String.BasicOps#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#6)]
 [!code-csharp[Conceptual.String.BasicOps#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#6)]
 [!code-vb[Conceptual.String.BasicOps#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#6)]  
  
 이 예제에서는 콘솔에 `-1` 를 표시합니다.  
  
 앞의 예제는 기본적으로 문화권을 구분합니다. 문화권을 구분하지 않는 문자열 비교를 수행하려면 <xref:System.String.Compare%2A?displayProperty=nameWithType> culture *매개 변수를 제공하여 사용할 문화권을 지정할 수 있게 해주는* 메서드의 오버로드를 사용합니다. <xref:System.String.Compare%2A?displayProperty=nameWithType> 메서드를 사용하여 문화권을 구분하지 않는 비교를 수행하는 방법을 보여 주는 예제는 [문화권을 구분하지 않는 문자열 비교 수행](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-comparisons.md)을 참조하세요.  
  
## <a name="compareordinal"></a>CompareOrdinal  
 <xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType> 메서드는 로컬 문화권을 고려하지 않고 두 문자열 개체를 비교합니다. 이 메서드의 반환 값은 앞의 표에서 **Compare** 메서드가 반환하는 값과 동일합니다.  
  
> [!IMPORTANT]
> <xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType> 메서드는 주로 문자열의 순서를 지정하거나 정렬할 때 사용됩니다. <xref:System.String.CompareOrdinal%2A?displayProperty=nameWithType> 메서드를 통해 같은지 여부를 테스트하면 안 됩니다(즉, 한 문자열이 다른 문자열보다 작거나 큰지에 관계없이 반환 값 0을 명시적으로 찾기 위해 사용하면 안 됨). 대신, 두 문자열이 같은지 여부를 확인하려면 <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> 메서드를 사용합니다.  
  
 다음 예제에서는 **CompareOrdinal** 메서드를 사용하여 두 문자열의 값을 비교합니다.  
  
 [!code-cpp[Conceptual.String.BasicOps#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#7)]
 [!code-csharp[Conceptual.String.BasicOps#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#7)]
 [!code-vb[Conceptual.String.BasicOps#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#7)]  
  
 이 예제에서는 콘솔에 `-32` 를 표시합니다.  
  
## <a name="compareto"></a>CompareTo  
 <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 메서드는 현재 문자열 개체가 캡슐화하는 문자열을 다른 문자열 또는 개체와 비교합니다. 이 메서드의 반환 값은 앞의 표에서 <xref:System.String.Compare%2A?displayProperty=nameWithType> 메서드가 반환하는 값과 동일합니다.  
  
> [!IMPORTANT]
> <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 메서드는 주로 문자열의 순서를 지정하거나 정렬할 때 사용됩니다. <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 메서드를 통해 같은지 여부를 테스트하면 안 됩니다(즉, 한 문자열이 다른 문자열보다 작거나 큰지에 관계없이 반환 값 0을 명시적으로 찾기 위해 사용하면 안 됨). 대신, 두 문자열이 같은지 여부를 확인하려면 <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> 메서드를 사용합니다.  
  
 다음 예제에서는 <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 메서드를 사용하여 `string1` 개체를 `string2` 개체와 비교합니다.  
  
 [!code-cpp[Conceptual.String.BasicOps#8](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#8)]
 [!code-csharp[Conceptual.String.BasicOps#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#8)]
 [!code-vb[Conceptual.String.BasicOps#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#8)]  
  
 이 예제에서는 콘솔에 `-1` 를 표시합니다.  
  
 <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 메서드의 모든 오버로드는 기본적으로 문화권 구분 및 대/소문자 구분 비교 작업을 수행합니다. 문화권을 구분하지 않는 비교를 수행할 수 있는 이 메서드의 오버로드는 제공되지 않습니다. 코드를 이해하기 쉽도록 문화권 구분 작업에는 **를 지정하고 문화권을 구분하지 않는 작업에는** 를 지정하여 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> String.Compare <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 메서드를 대신하는 것이 좋습니다. **String.Compare** 메서드를 사용하여 문화권 구분 비교와 문화권을 구분하지 않는 비교를 둘 다 수행하는 방법을 보여 주는 예제는 [문화권을 구분하지 않는 문자열 비교 수행](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-comparisons.md)을 참조하세요.  
  
## <a name="equals"></a>같음  
 **String.Equals** 메서드는 두 문자열이 같은지 여부를 쉽게 확인할 수 있습니다. 대/소문자 구분 메서드는 **true** 또는 **false** 부울 값을 반환합니다. 다음 예제와 같이 기존 클래스에서 사용할 수 있습니다. 다음 예제에서는 **Equals** 메서드를 사용하여 문자열 개체에 "Hello World"라는 구가 포함되어 있는지 여부를 확인합니다.  
  
 [!code-cpp[Conceptual.String.BasicOps#9](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#9)]
 [!code-csharp[Conceptual.String.BasicOps#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#9)]
 [!code-vb[Conceptual.String.BasicOps#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#9)]  
  
 이 예제에서는 콘솔에 `True` 를 표시합니다.  
  
 이 메서드는 정적 메서드로 사용될 수도 있습니다. 다음 예제에서는 정적 메서드를 사용하여 두 문자열 개체를 비교합니다.  
  
 [!code-cpp[Conceptual.String.BasicOps#10](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#10)]
 [!code-csharp[Conceptual.String.BasicOps#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#10)]
 [!code-vb[Conceptual.String.BasicOps#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#10)]  
  
 이 예제에서는 콘솔에 `True` 를 표시합니다.  
  
## <a name="startswith-and-endswith"></a>StartsWith 및 EndsWith  
 **String.StartsWith** 메서드를 사용하여 문자열 개체가 다른 문자열을 포함하는 동일한 문자로 시작하는지 여부를 확인합니다. 이 대/소문자 구분 메서드는 현재 문자열 개체가 전달된 문자열로 시작하는 경우 **true** 를 반환하고, 그러지 않은 경우 **false** 를 반환합니다. 다음 예제에서는 이 메서드를 사용하여 문자열 개체가 "Hello"로 시작하는지 여부를 확인합니다.  
  
 [!code-cpp[Conceptual.String.BasicOps#11](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#11)]
 [!code-csharp[Conceptual.String.BasicOps#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#11)]
 [!code-vb[Conceptual.String.BasicOps#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#11)]  
  
 이 예제에서는 콘솔에 `True` 를 표시합니다.  
  
 **String.EndsWith** 메서드는 전달된 문자열을 현재 문자열 개체의 끝에 있는 문자와 비교합니다. 역시 부울 값을 반환합니다. 다음 예제에서는 **EndsWith** 메서드를 사용하여 문자열의 끝을 검사합니다.  
  
 [!code-cpp[Conceptual.String.BasicOps#12](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#12)]
 [!code-csharp[Conceptual.String.BasicOps#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#12)]
 [!code-vb[Conceptual.String.BasicOps#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#12)]  
  
 이 예제에서는 콘솔에 `False` 를 표시합니다.  
  
## <a name="indexof-and-lastindexof"></a>IndexOf 및 LastIndexOf  
 **String.IndexOf** 메서드를 사용하여 문자열 내에서 특정 문자의 첫 번째 발생 위치를 확인합니다. 이 대/소문자 구분 메서드는 문자열의 시작 부분에서 계산을 시작하고 0부터 시작하는 인덱스를 사용하여 전달된 문자의 위치를 반환합니다. 문자를 찾을 수 없는 경우 -1 값이 반환됩니다.  
  
 다음 예제에서는 **IndexOf** 메서드를 사용하여 문자열에서 '`l`' 문자의 첫 번째 발생을 검색합니다.  
  
 [!code-cpp[Conceptual.String.BasicOps#13](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#13)]
 [!code-csharp[Conceptual.String.BasicOps#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#13)]
 [!code-vb[Conceptual.String.BasicOps#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#13)]  
  
 이 예제에서는 콘솔에 `2` 를 표시합니다.  
  
 **String.LastIndexOf** 메서드는 문자열 내에서 특정 문자의 마지막 발생 위치를 반환한다는 점을 제외하고 **String.IndexOf** 메서드와 비슷합니다. 대/소문자를 구분하며 0부터 시작하는 인덱스를 사용합니다.  
  
 다음 예제에서는 **LastIndexOf** 메서드를 사용하여 문자열에서 '`l`' 문자의 마지막 발생을 검색합니다.  
  
 [!code-cpp[Conceptual.String.BasicOps#14](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/compare.cpp#14)]
 [!code-csharp[Conceptual.String.BasicOps#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/compare.cs#14)]
 [!code-vb[Conceptual.String.BasicOps#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/compare.vb#14)]  
  
 이 예제에서는 콘솔에 `9` 를 표시합니다.  
  
 두 메서드는 모두 **String.Remove** 메서드와 함께 사용할 때 유용합니다. 문자 또는 해당 문자로 시작하는 단어를 제거하기 위해 **IndexOf** 또는 **LastIndexOf** 메서드 중 하나를 사용하여 문자의 위치를 검색한 다음 해당 위치를 **Remove** 메서드에 제공할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [기본적인 문자열 작업](../../../docs/standard/base-types/basic-string-operations.md)
- [Culture의 영향을 받지 않는 문자열 작업 수행](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations.md)
- [정렬 가중치 테이블(Windows의 .NET용)](https://www.microsoft.com/download/details.aspx?id=10921)
- [기본 유니코드 데이터 정렬 요소 테이블(Linux 및 macOS의 .NET Core용)](https://www.unicode.org/Public/UCA/latest/allkeys.txt)
