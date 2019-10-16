---
title: .NET에서 문자열 사용에 대한 모범 사례
description: .NET 애플리케이션에서 문자열을 효율적으로 사용하는 방법을 알아봅니다.
ms.date: 05/01/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- strings [.NET Framework],searching
- best practices,string comparison and sorting
- strings [.NET Framework],best practices
- strings [.NET Framework],basic string operations
- sorting strings
- strings [.NET Framework],sorting
- string comparison [.NET Framework],best practices
- string sorting
- comparing strings
- strings [.NET Framework],comparing
ms.assetid: b9f0bf53-e2de-4116-8ce9-d4f91a1df4f7
author: rpetrusha
ms.author: ronpet
ms.custom: seodec18
ms.openlocfilehash: 50127f24bfee0c2fe49da8f285e5052d2f753696
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69934933"
---
# <a name="best-practices-for-using-strings-in-net"></a>.NET에서 문자열 사용에 대한 모범 사례
<a name="top"></a> .NET에서는 지역화된 애플리케이션과 전역화된 애플리케이션을 개발하기 위한 광범위한 지원을 제공하고 문자열 정렬 및 표시와 같은 일반적인 작업을 수행할 때 현재 문화권이나 특정 문화권의 규칙을 쉽게 적용할 수 있습니다. 그러나 문자열 정렬 및 비교가 항상 문화권이 구분되는 작업은 아닙니다. 예를 들어 애플리케이션에서 내부적으로 사용되는 문자열은 대기 모든 문화권에서 동일하게 처리해야 합니다. XML 태그, HTML 태그, 사용자 이름, 파일 경로 및 시스템 개체 이름과 같이 문화권을 구분하지 않는 문자열 데이터가 문화권이 구분되는 것처럼 해석되면 애플리케이션 코드에는 감지하기 어려운 버그, 성능 저하 및 경우에 따라 보안 문제가 발생할 수 있습니다.  
  
 이 항목에서는 .NET의 문자열 정렬, 비교 및 대/소문자 구분 방법을 살펴보고, 적절한 문자열 처리 방법 선택을 위한 권장 사항을 제공하고, 문자열 처리 방법에 대한 추가 정보를 제공합니다. 또한 숫자 데이터 및 날짜/시간 데이터와 같은 형식이 지정된 데이터를 표시 및 스토리지를 위해 처리하는 방법을 살펴봅니다.  
  
 이 항목에는 다음과 같은 단원이 포함되어 있습니다.  
  
- [문자열 사용에 대한 권장 사항](#recommendations_for_string_usage)  
  
- [명시적으로 문자열 비교 지정](#specifying_string_comparisons_explicitly)  
  
- [문자열 비교 세부 정보](#the_details_of_string_comparison)  
  
- [메서드 호출을 위한 StringComparison 멤버 선택](#choosing_a_stringcomparison_member_for_your_method_call)  
  
- [.NET에서 일반적인 문자열 비교 방법](#common_string_comparison_methods_in_the_net_framework)  
  
- [문자열 비교를 간접적으로 수행하는 방법](#methods_that_perform_string_comparison_indirectly)  
  
- [서식이 지정된 데이터 표시 및 유지](#Formatted)  
  
<a name="recommendations_for_string_usage"></a>   
## <a name="recommendations-for-string-usage"></a>문자열 사용에 대한 권장 사항  
 .NET으로 개발하는 경우 문자열을 사용할 때 다음과 같은 간단한 권장 사항을 따르세요.  
  
- 문자열 작업에 대한 문자열 비교 규칙을 명시적으로 지정하는 오버로드를 사용합니다. 일반적으로 이 작업은 <xref:System.StringComparison>형식 매개 변수가 포함된 메서드 오버로드를 호출하는 작업입니다.  
  
- 문화권을 구분하지 않는 문자열 일치를 위한 안전한 기본값으로 비교에 대해 <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> 또는 <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> 를 사용합니다.  
  
- 성능 향상을 위해 비교를 <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> 또는 <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> 와 함께 사용합니다.  
  
- 사용자에게 출력을 표시할 때 <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType> 에 기반을 둔 문자열 작업을 사용합니다.  
  
- 비교에 언어적 관련성이 없을 경우(예: 기호) <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> 를 기준으로 한 문자열 작업 대신 비언어적인 <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> 또는 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 값을 사용합니다.  
  
- 비교를 위해 문자열을 정교화할 경우 <xref:System.String.ToUpperInvariant%2A?displayProperty=nameWithType> 메서드 대신 <xref:System.String.ToLowerInvariant%2A?displayProperty=nameWithType> 메서드를 사용합니다.  
  
- <xref:System.String.Equals%2A?displayProperty=nameWithType> 메서드의 오버로드를 사용하여 두 문자열이 같은지를 테스트합니다.  
  
- <xref:System.String.Compare%2A?displayProperty=nameWithType> 및 <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 메서드를 사용하여 같은지 확인하는 것이 아니라 문자열을 정렬합니다.  
  
- 문화권이 구분되는 형식 지정을 사용하여 사용자 인터페이스에서 숫자 및 날짜와 같이 문자열이 아닌 데이터를 표시합니다. [고정 문화권](xref:System.Globalization.CultureInfo.InvariantCulture)과 함께 형식 지정을 사용하여 문자열 양식에서 문자열이 아닌 데이터를 유지합니다.  
  
 문자열을 사용할 때 다음 사례를 사용하지 마세요.  
  
- 문자열 작업에 대한 문자열 비교 규칙을 명시적 또는 암시적으로 지정하지 않는 오버로드를 사용하지 마세요.  
  
- 대부분 경우에 <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> 를 기준으로 한 문자열 작업을 사용하지 마세요. 몇 가지 예외의 하나는 언어적으로 의미가 있지만 문화적으로 독립적인 데이터를 유지하는 경우입니다.  
  
- <xref:System.String.Compare%2A?displayProperty=nameWithType> 또는 <xref:System.String.CompareTo%2A> 메서드의 오버로드 및 두 문자열이 같은지를 확인하기 위한 반환 값 0에 대한 테스트를 사용하지 마세요.  
  
- 문자열 양식에서 숫자 데이터나 날짜 및 시간 데이터를 유지하는 데 문화권이 구분되는 형식 지정을 사용하지 마세요.  
  
 [맨 위로 이동](#top)  
  
<a name="specifying_string_comparisons_explicitly"></a>   
## <a name="specifying-string-comparisons-explicitly"></a>명시적으로 문자열 비교 지정  
 .NET의 문자열 조작 메서드는 대부분 오버로드됩니다. 일반적으로 오버로드 하나 이상은 기본 설정을 그대로 사용하지만, 다른 오버로드는 기본값을 사용하지 않고 문자열을 비교 및 조작하는 정확한 방법을 정의합니다. 기본값을 사용하지 않는 대부분 메서드에는 문화권 및 사례별로 문자열 비교에 대한 규칙을 명시적으로 지정하는 열거형인 <xref:System.StringComparison>형식 매개 변수가 포함됩니다. 다음 표에서는 <xref:System.StringComparison> 열거형 멤버에 대해 설명합니다.  
  
|StringComparison 멤버|설명|  
|-----------------------------|-----------------|  
|<xref:System.StringComparison.CurrentCulture>|현재 문화권을 사용하여 대/소문자를 구분하는 비교를 수행합니다.|  
|<xref:System.StringComparison.CurrentCultureIgnoreCase>|현재 문화권을 사용하여 대/소문자를 구분하지 않는 비교를 수행합니다.|  
|<xref:System.StringComparison.InvariantCulture>|고정 문화권을 사용하여 대/소문자를 구분하는 비교를 수행합니다.|  
|<xref:System.StringComparison.InvariantCultureIgnoreCase>|고정 문화권을 사용하여 대/소문자를 구분하지 않는 비교를 수행합니다.|  
|<xref:System.StringComparison.Ordinal>|서수 비교를 수행합니다.|  
|<xref:System.StringComparison.OrdinalIgnoreCase>|대소문자를 구분하지 않는 서수 비교를 수행합니다.|  
  
 예를 들어 문자 또는 문자열과 일치하는 <xref:System.String.IndexOf%2A> 개체의 하위 문자열 인덱스를 반환하는 <xref:System.String> 메서드에는 다음과 같은 오버로드 9개가 포함됩니다.  
  
- <xref:System.String.IndexOf%28System.Char%29>, <xref:System.String.IndexOf%28System.Char%2CSystem.Int32%29>및 <xref:System.String.IndexOf%28System.Char%2CSystem.Int32%2CSystem.Int32%29>- 기본적으로 문자열에서 문자에 대한 서수 검색(대/소문자 구분 및 문화권을 구분하지 않음)을 수행합니다.  
  
- <xref:System.String.IndexOf%28System.String%29>, <xref:System.String.IndexOf%28System.String%2CSystem.Int32%29>및 <xref:System.String.IndexOf%28System.String%2CSystem.Int32%2CSystem.Int32%29>- 기본적으로 문자열에서 하위 문자열에 대한 대/소문자 구분 및 문화권 구분 검색을 수행합니다.  
  
- <xref:System.String.IndexOf%28System.String%2CSystem.StringComparison%29>, <xref:System.String.IndexOf%28System.String%2CSystem.Int32%2CSystem.StringComparison%29>및 <xref:System.String.IndexOf%28System.String%2CSystem.Int32%2CSystem.Int32%2CSystem.StringComparison%29>, - 비교 형식을 지정할 수 있는 <xref:System.StringComparison> 형식 매개 변수를 포함합니다.  
  
 다음 이유로 기본값을 사용하지 않는 오버로드를 선택하는 것이 좋습니다.  
  
- 기본 매개 변수가 있는 일부 오버로드(문자열 인스턴스에서 <xref:System.Char> 을 검색하는 오버로드)는 서수 비교를 수행하지만, 다른 오버로드(문자열 인스턴스에서 문자열을 검색하는 오버로드)는 문화권이 구분됩니다. 어떤 메서드가 어떤 기본값을 사용하는지 기억하기 어렵고 오버로드를 혼동하기 쉽습니다.  
  
- 메서드 호출에 대해 기본값을 사용하는 코드의 의도는 분명하지 않습니다. 기본값을 사용하는 다음 예제에서는 개발자가 실제로 두 문자열의 서수 또는 언어 비교를 의도했는지 또는 `protocol` 과 "http" 간의 대/소문자 차이로 인해 같음 테스트에서 `false`형식 매개 변수가 포함된 메서드 오버로드를 호출하는 작업입니다.  
  
     [!code-csharp[Conceptual.Strings.BestPractices#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/explicitargs1.cs#1)]
     [!code-vb[Conceptual.Strings.BestPractices#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/explicitargs1.vb#1)]  
  
 일반적으로 기본값을 사용하지 않는 메서드를 사용하면 코드의 의도가 분명해지므로 이 메서드를 호출하는 것이 좋습니다. 이 메서드를 사용하면 코드를 더 쉽게 읽을 수 있고 더 쉽게 디버그 및 유지 관리할 수도 있습니다. 다음 예제에서는 이전 예제와 관련된 질문을 해결합니다. 예제에서는 서수 비교가 사용되고 대/소문자 차이가 무시됩니다.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/explicitargs1.cs#2)]
 [!code-vb[Conceptual.Strings.BestPractices#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/explicitargs1.vb#2)]  
  
 [맨 위로 이동](#top)  
  
<a name="the_details_of_string_comparison"></a>   
## <a name="the-details-of-string-comparison"></a>문자열 비교 세부 정보  
 문자열 비교는 특히 정렬 및 같음 테스트와 같은 다양한 문자열 관련 작업의 핵심입니다. 결정된 순서로 문자열 정렬: 정렬된 문자열 목록에서 "my"가 "string" 앞에 나타나면 "my"가 "string"과 같거나 작은지 비교해야 합니다. 또한 비교는 암시적으로 같음을 정의합니다. 비교 작업은 같은 것으로 판단되는 문자열에 대해 0을 반환합니다. 다른 문자열보다 작은 문자열이 없다고 해석하는 것이 적절합니다. 문자열과 관련된 대부분 의미 있는 작업에는 다른 문자열과 비교 및 잘 정의된 정렬 작업 실행이라는 두 가지 절차가 둘 다 또는 두 가지 중 하나가 포함됩니다.  

> [!NOTE]
> Windows 운영 체제에 대한 정렬 및 비교 작업에 사용되는 문자 가중치에 대한 정보를 포함하는 텍스트 파일 집합인 [정렬 가중치 테이블](https://www.microsoft.com/download/details.aspx?id=10921) 및 Linux 및 macOS용 정렬 가중치 테이블의 최신 버전인 [기본 유니코드 데이터 정렬 요소 테이블](https://www.unicode.org/Public/UCA/latest/allkeys.txt)을 다운로드할 수 있습니다. Linux 및 macOS에서 정렬 가중치 테이블의 특정 버전은 시스템에 설치된 [International Components for Unicode](http://site.icu-project.org/) 라이브러리 버전에 따라 달라집니다. ICU 버전 및 ICU 버전이 구현하는 유니코드 버전에 대한 자세한 내용은 [ICU 다운로드](http://site.icu-project.org/download)를 참조하세요.

 그러나 두 문자열의 같음 또는 정렬 순서를 평가할 때 하나의 올바른 결과가 생성되지는 않습니다. 결과는 문자열 비교에 사용되는 기준에 따라 다릅니다. 특히 서수 문자열 비교나 현재 문화권이나 [고정 문화권](xref:System.Globalization.CultureInfo.InvariantCulture)(영어를 기준으로 로캘을 구분하지 않는 문화권)의 대/소문자 구분 및 정렬 규칙을 기준으로 한 문자열 비교에서는 다른 결과가 생성될 수 있습니다.  

또한 다른 버전의 .NET을 사용하거나 다른 운영 체제 또는 운영 체제 버전의 .NET을 사용하여 문자열을 비교하면 다른 결과가 반환될 수 있습니다. 자세한 내용은 [문자열과 유니코드 표준](xref:System.String#Unicode)을 참조하세요. 

<a name="current_culture"></a>   
### <a name="string-comparisons-that-use-the-current-culture"></a>현재 문화권을 사용하는 문자열 비교  
 문자열 비교 시 현재 문화권의 규칙을 사용하는 한 가기 기준이 포함됩니다. 현재 문화권을 기준으로 한 비교에는 스레드의 현재 문화권 또는 로캘이 사용됩니다. 사용자가 문화권을 설정하지 않으면 문화권은 기본적으로 제어판, **국가별 옵션** 창의 설정으로 지정됩니다. 데이터가 언어적으로 관련되는 경우와 문화권이 구분되는 사용자 조작을 반영하는 경우에는 항상 현재 문화권을 기준으로 한 비교를 사용해야 합니다.  
  
 그러나 문화권이 변경되면 .NET의 비교 및 대/소문자 지정 동작도 바뀝니다. 애플리케이션이 개발된 컴퓨터와 다른 문화권을 포함하는 컴퓨터에서 애플리케이션을 실행하거나 실행 스레드가 문화권을 변경할 경우 이 동작이 수행됩니다. 이 동작은 의도적이지만 대부분 개발자가 이해하기가 분명하지는 않습니다. 다음 예제에서는 미국 영어("en-US") 및 스웨덴어("sv-SE") 문화권의 정렬 순서 차이를 보여 줍니다. 정렬된 문자열 배열에서 단어 "ångström", "Windows" 및 "Visual Studio"가 다른 위치에 나타남을 알 수 있습니다.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/comparison1.cs#3)]
 [!code-vb[Conceptual.Strings.BestPractices#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/comparison1.vb#3)]  
  
 현재 문화권을 사용하는 대/소문자를 구분하지 않는 비교는 스레드의 현재 문화권에 지정된 대/소문자를 무시한다는 점을 제외하고 문화권 구분 비교와 같습니다. 이 동작은 정렬 순서에서도 나타날 수 있습니다.  
  
 현재 문화권 의미 체계를 사용하는 비교는 다음 메서드의 기본값입니다.  
  
- <xref:System.String.Compare%2A?displayProperty=nameWithType> 매개 변수를 포함하지 않는 <xref:System.StringComparison> 오버로드.  
  
- <xref:System.String.CompareTo%2A?displayProperty=nameWithType> 오버로드.  
  
- 기본 <xref:System.String.StartsWith%28System.String%29?displayProperty=nameWithType> 메서드 및 <xref:System.String.StartsWith%28System.String%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType> null `null`<xref:System.Globalization.CultureInfo> 오버로드.  
  
- 기본 <xref:System.String.EndsWith%28System.String%29?displayProperty=nameWithType> 메서드 및 <xref:System.String.EndsWith%28System.String%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType> null `null`<xref:System.Globalization.CultureInfo> 오버로드.  
  
- <xref:System.String.IndexOf%2A?displayProperty=nameWithType> 을 검색 매개 변수로 사용하고 <xref:System.String> 매개 변수를 포함하지 않는 <xref:System.StringComparison> 오버로드.  
  
- <xref:System.String.LastIndexOf%2A?displayProperty=nameWithType> 을 검색 매개 변수로 사용하고 <xref:System.String> 매개 변수를 포함하지 않는 <xref:System.StringComparison> 오버로드.  
  
 모든 경우에 메서드 호출의 의도를 분명하게 나타내도록 <xref:System.StringComparison> 매개 변수를 포함하는 오버로드를 호출하는 것이 좋습니다.  
  
 비언어적인 문자열 데이터가 언어적으로 해석되거나 특정 문화권의 문자열 데이터가 다른 문화권의 규칙을 통해 해석되면 감지하기 어려운 버그와 감지할 수 있는 버그가 발생할 수 있습니다. 대표적인 예는 Turkish-I 문제입니다.  
  
 미국 영어를 포함한 거의 모든 라틴어 알파벳에서 문자 "i"(\u0069)는 문자 "I"(\u0049)의 소문자 버전입니다. 이 대/소문자 구분 규칙은 해당 문화권에서 프로그래밍하는 사용자에게 빠르게 기본 규칙이 되었습니다. 그러나 터키어("tr-TR") 알파벳에는 "i"의 대문자 버전인 "점이 있는 I" 문자 "İ"(\u0130)가 포함됩니다. 터키어에는 대문자 버전이 "I"인 "점이 없는 i" 문자 , "ı"(\u0131)도 포함됩니다. 이 동작은 아제르바이잔어("az") 문화권에서도 발생합니다.  
  
 따라서 "i"를 대문자로 변환하거나 "I"를 소문자로 변환하는 방법에 대한 가정이 모든 문화권에서 유효한 것은 아닙니다. 문자열 비교 루틴에 대해 기본 오버로드를 사용하면 이 오버로드에는 문화권 간의 차이가 적용됩니다. 문자열 "file" 및 "FILE"의 대/소문자를 구분하지 않는 비교를 수행하는 다음 시도와 같이, 비교할 데이터가 비언어적일 경우 기본 오버로드를 사용하면 원하지 않는 결과가 생성될 수 있습니다.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/turkish1.cs#11)]
 [!code-vb[Conceptual.Strings.BestPractices#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/turkish1.vb#11)]  
  
 다음 예제와 같이 보안 관련 설정에서 문화권이 의도치 않게 사용되면 이 비교로 인해 큰 문제가 발생할 수 있습니다. `IsFileURI("file:")`와 같은 메서드 호출은 현재 문화권이 미국 영어이면 `true`를 반환하지만 현재 문화권이 터키어이면 `false`를 반환합니다. 따라서 터키어 시스템에서는 누군가 "FILE:"으로 시작하는 대/소문자를 구분하지 않는 URI에 대한 액세스를 차단하는 보안 조치를 회피할 수 있습니다.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/turkish1.cs#12)]
 [!code-vb[Conceptual.Strings.BestPractices#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/turkish1.vb#12)]  
  
 이 경우 "file:"은 비언어적, 문화권을 구분하지 않는 식별자로 해석되므로 코드를 다음 예제와 같이 작성해야 합니다.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/turkish1.cs#13)]
 [!code-vb[Conceptual.Strings.BestPractices#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/turkish1.vb#13)]  
  
### <a name="ordinal-string-operations"></a>서수 문자열 작업  
 메서드 호출에서 <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> 또는 <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> 값을 지정하는 것은 자연어의 특징이 무시되는 비언어적인 비교를 나타냅니다. 이들 <xref:System.StringComparison> 값을 사용하여 호출되는 메서드의 문자열 작업 결정은 문화권별로 매개 변수화되는 대/소문자 구분 또는 동일성 테이블이 아닌 단순 바이트 비교에 기반을 둡니다. 대부분 경우에 이 접근 방법은 의도된 문자열 해석에 가장 적합하지만 코드를 더 빠르고 더 안정적으로 만듭니다.  
  
 서수 비교는 언어적 해석 없이 각 문자열의 각 바이트가 비교되는 문자열 비교입니다. 예를 들어 "windows"는 "Windows"와 일치하지 않습니다. 이 비교는 기본적으로 C 런타임 `strcmp` 함수에 대한 호출입니다. 컨텍스트가 문자열이 정확히 일치해야 함을 나타내거나 보수적인 일치 정책을 요구할 경우 이 비교를 사용합니다. 또한 서수 비교는 결과를 결정할 때 언어 규칙을 적용하지 않으므로 가장 빠른 비교 작업입니다.  
  
 .NET의 문자열에는 포함된 null 문자가 있을 수 있습니다. 서수 비교와 문화권 구분 비교(고정 문화권을 사용하는 비교 포함) 간 가장 분명한 차이의 하나는 문자열의 포함된 null 문자 처리와 관련됩니다. <xref:System.String.Compare%2A?displayProperty=nameWithType> 및 <xref:System.String.Equals%2A?displayProperty=nameWithType> 메서드를 사용하여 문화권 구분 비교(고정 문화권을 사용하는 비교 포함)를 수행하면 이들 문자가 무시됩니다. 따라서 문화권 구분 비교에서 포함된 null 문자가 들어 있는 문자열은 해당 문자가 들어 있지 않은 문자열과 같은 것으로 간주할 수 있습니다.  
  
> [!IMPORTANT]
> 문자열 비교 메서드는 포함된 null 문자를 무시하지만 <xref:System.String.Contains%2A?displayProperty=nameWithType>, <xref:System.String.EndsWith%2A?displayProperty=nameWithType>, <xref:System.String.IndexOf%2A?displayProperty=nameWithType>, <xref:System.String.LastIndexOf%2A?displayProperty=nameWithType>및 <xref:System.String.StartsWith%2A?displayProperty=nameWithType> 와 같은 문자열 검색 메서드는 무시하지 않습니다.  
  
 다음 예제에서는 문자열 "Aa" 및 "A"와 "a" 사이에 여러 포함된 null 문자를 포함하는 비슷한 문자열의 문화권 구분 비교를 수행하고 두 문자열을 어떻게 같은 것으로 간주하는지 보여 줍니다.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/embeddednulls1.cs#19)]
 [!code-vb[Conceptual.Strings.BestPractices#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/embeddednulls1.vb#19)]  
  
 그러나 다음 예제와 같이 서수 비교를 사용할 경우 문자열을 같은 것으로 간주하지 않습니다.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/embeddednulls2.cs#20)]
 [!code-vb[Conceptual.Strings.BestPractices#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/embeddednulls2.vb#20)]  
  
 대/소문자를 구분하지 않는 서수 비교는 다음으로 가장 보수적인 접근 방법입니다. 이들 비교는 대부분 대/소문자 구분을 무시합니다. 예를 들어 "windows"는 "Windows"와 일치합니다. ASCII 문자를 처리할 때 이 정책은 사용 가능한 ASCII 대/소문자 구분을 무시한다는 점을 제외하고 <xref:System.StringComparison.Ordinal?displayProperty=nameWithType>과 같습니다. 따라서 [A, Z]\(\u0041-\u005A)의 모든 문자는 [a,z]\(\u0061-\007A)의 해당 문자와 일치합니다. ASCII 범위를 벗어난 대/소문자 구분에는 고정 문화권 테이블이 사용됩니다. 따라서 다음 비교는  
  
 [!code-csharp[Conceptual.Strings.BestPractices#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/comparison2.cs#4)]
 [!code-vb[Conceptual.Strings.BestPractices#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/comparison2.vb#4)]  
  
 다음 비교와 같지만 더 빠릅니다.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/comparison2.cs#5)]
 [!code-vb[Conceptual.Strings.BestPractices#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/comparison2.vb#5)]  
  
 이들 비교는 매우 빠릅니다.  
  
> [!NOTE]
> 파일 시스템, 레지스트리 키 및 값, 환경 변수의 문자열 동작은 <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType>로 가장 잘 표현됩니다.  
  
 <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> 및 <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> 는 둘 다 직접 이진 값을 사용하고 일치 항목 찾기에 가장 적합합니다. 사용 중인 비교 설정을 확신할 수 없으면 다음 두 값의 하나를 사용하세요. 그러나 이들 값은 바이트 단위 비교를 수행하므로 영어 사전처럼 언어 정렬 순서별로 정렬하는 것이 아니라 이진 정렬 순서별로 정렬합니다. 사용자에게 표시되는 결과가 대부분 컨텍스트에서 이상하게 표시될 수 있습니다.  
  
 서수 의미 체계는 <xref:System.String.Equals%2A?displayProperty=nameWithType> 인수(같음 연산자 포함)를 포함하지 않는 <xref:System.StringComparison> 오버로드의 기본값입니다. 모든 경우에 <xref:System.StringComparison> 매개 변수를 포함하는 오버로드를 호출하는 것이 좋습니다.  
  
### <a name="string-operations-that-use-the-invariant-culture"></a>고정 문화권을 사용하는 문자열 작업  
 고정 문화권을 사용한 비교에는 정적 <xref:System.Globalization.CultureInfo.CompareInfo%2A> 속성에서 반환되는 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 속성이 사용됩니다. 이 동작은 모든 시스템에서 동일하며, 범위 밖의 모든 문자를 동일한 고정 문화권으로 간주하는 문자로 변환합니다. 이 정책은 문화권에 걸쳐 단일 문자열 동작 집합을 유지 관리할 경우 유용하지만 예기치 않은 경과를 제공하기도 합니다.  
  
 고정 문화권을 사용한 대/소문자를 비교하지 않는 비교에는 비교 정보를 위해 정적 <xref:System.Globalization.CultureInfo.CompareInfo%2A> 속성에서 반환되는 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 속성이 사용됩니다. 모든 경우에 변환된 문자 간의 차이는 무시됩니다.  
  
 <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> 및 <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> 을 사용하는 비교는 ASCII 문자열과 똑같이 작동합니다. 그러나 <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> 는 바이트 집합으로 해석되어야 하는 문자열에 적절하지 않을 수 있는 언어적 결정을 내립니다. `CultureInfo.InvariantCulture.CompareInfo` 개체를 사용하면 <xref:System.String.Compare%2A> 메서드가 특정 문자 집합을 같은 것으로 해석합니다. 예를 들어 다음 동일성은 고정 문화권에서 유효합니다.  
  
 InvariantCulture: a + ̊ = å  
  
 LATIN SMALL LETTER A 문자 “a”(\u0061)는 COMBINING RING ABOVE 문자 “+ " ̊”(\u030a) 옆에 있을 경우 LATIN SMALL LETTER A WITH RING ABOVE 문자 “å”(\u00e5)로 해석됩니다. 다음 예제와 같이 이 동작은 서수 비교와 다릅니다.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/comparison3.cs#15)]
 [!code-vb[Conceptual.Strings.BestPractices#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/comparison3.vb#15)]  
  
 파일 이름, 쿠키 또는 "å"와 같은 조합이 나타날 수 있는 다른 항목을 해석할 때 서수 비교는 가장 투명하고 적합한 동작을 제공합니다.  
  
 모든 것을 고려해 보면 고정 문화권에는 비교에 유용할 수 있는 속성이 거의 없습니다. 고정 문화권은 완전한 기호 동일성을 보장하지 못하게 하는 언어 관련 방식으로 비교를 수행하지만 모든 문화권에서 표시하기에 적합하지 않습니다. 비교에 <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> 를 사용하는 몇 가지 이유의 하나는 서로 다른 문화에서 동일하게 표시되도록 순서가 지정된 데이터를 유지하는 것입니다. 예를 들어 표시하기 위한 정렬된 식별자 목록을 포함하는 큰 데이터 파일이 애플리케이션과 함께 제공될 경우 이 목록에 추가하려면 고정 스타일 정렬을 사용한 삽입이 필요합니다.  
  
 [맨 위로 이동](#top)  
  
<a name="choosing_a_stringcomparison_member_for_your_method_call"></a>   
## <a name="choosing-a-stringcomparison-member-for-your-method-call"></a>메서드 호출을 위한 StringComparison 멤버 선택  
 다음 표에서는 의미 체계 문자열 컨텍스트에서 <xref:System.StringComparison> 열거형 멤버로의 매핑을 간략하게 설명합니다.  
  
|데이터|동작|해당 System.StringComparison<br /><br /> 값|  
|----------|--------------|-----------------------------------------------------|  
|대/소문자 구분 내부 식별자.<br /><br /> XML 및 HTTP와 같은 표준의 대/소문자 구분 식별자.<br /><br /> 대/소문자 구분 보안 관련 설정.|바이트가 정확히 일치하는 비언어적 식별자.|<xref:System.StringComparison.Ordinal>|  
|대/소문자를 구분하지 않는 내부 식별자.<br /><br /> XML 및 HTTP와 같은 표준의 대/소문자를 구분하지 않는 식별자.<br /><br /> 파일 경로.<br /><br /> 레지스트리 키 및 값.<br /><br /> 환경 변수.<br /><br /> 리소스 식별자(예: 핸들 이름).<br /><br /> 대/소문자를 구분하지 않는 보안 관련 설정.|대/소문자가 불규칙한 비언어적 식별자, 특히 대부분 Windows 시스템 서비스에 저장된 데이터.|<xref:System.StringComparison.OrdinalIgnoreCase>|  
|일부 지속되는 언어적으로 관련된 데이터.<br /><br /> 고정 정렬 순서가 필요한 언어 데이터 표시.|언어적으로 관련된 문화권을 구분하지 않는 데이터.|<xref:System.StringComparison.InvariantCulture><br /><br /> 또는<br /><br /> <xref:System.StringComparison.InvariantCultureIgnoreCase>|  
|사용자에게 표시된 데이터.<br /><br /> 대부분 사용자 입력.|로컬 언어적 사용자 지정이 필요한 데이터.|<xref:System.StringComparison.CurrentCulture><br /><br /> 또는<br /><br /> <xref:System.StringComparison.CurrentCultureIgnoreCase>|  
  
 [맨 위로 이동](#top)  
  
<a name="common_string_comparison_methods_in_the_net_framework"></a>   
## <a name="common-string-comparison-methods-in-net"></a>.NET에서 일반적인 문자열 비교 방법  
 다음 섹션에서는 문자열 비교에 가장 일반적으로 사용되는 메서드에 대해 설명합니다.  
  
### <a name="stringcompare"></a>String.Compare  
 기본 해석: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType>.  
  
 문자열 해석의 가장 중심적인 작업으로, 이들 메서드 호출의 모든 인스턴스를 검사하여 문자열이 현재 문화권에 따라 해석되는지, 아니면 문화권과 관계가 없는지를 결정해야 합니다. 일반적으로 이는 후자이고 <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> 비교를 사용해야 합니다.  
  
 <xref:System.Globalization.CompareInfo?displayProperty=nameWithType> 속성에서 반환되는 <xref:System.Globalization.CultureInfo.CompareInfo%2A?displayProperty=nameWithType> 클래스에는 <xref:System.Globalization.CompareInfo.Compare%2A> 플래그 열거형을 통해 다양한 일치 항목 찾기 옵션(서수, 공백 무시, 가나 형식 무시 등)을 제공하는 <xref:System.Globalization.CompareOptions> 메서드가 포함됩니다.  
  
### <a name="stringcompareto"></a>String.CompareTo  
 기본 해석: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType>.  
  
 이 메서드는 현재 <xref:System.StringComparison> 형식을 지정하는 오버로드를 제공하지 않습니다. 일반적으로 이 메서드를 권장되는 <xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> 양식으로 변환할 수 있습니다.  
  
 <xref:System.IComparable> 및 <xref:System.IComparable%601> 인터페이스를 구현하는 형식이 이 메서드를 구현합니다. <xref:System.StringComparison> 매개 변수의 옵션을 제공하지 않으므로 형식 구현 시 사용자가 생성자에서 <xref:System.StringComparer>를 구현해야 할 수 있습니다. 다음 예제에서는 클래스 생성자에 `FileName` 매개 변수가 포함된 <xref:System.StringComparer> 클래스를 정의합니다. 이 <xref:System.StringComparer> 개체는 `FileName.CompareTo` 메서드에 사용됩니다.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/api1.cs#6)]
 [!code-vb[Conceptual.Strings.BestPractices#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/api1.vb#6)]  
  
### <a name="stringequals"></a>String.Equals  
 기본 해석: <xref:System.StringComparison.Ordinal?displayProperty=nameWithType>.  
  
 <xref:System.String> 클래스를 통해 정적 또는 인스턴스 <xref:System.String.Equals%2A> 메서드 오버로드를 호출하거나 정적 같음 연산자를 사용하여 같음 여부를 테스트할 수 있습니다. 오버로드 및 연산자에는 기본적으로 서수 비교가 사용됩니다. 그러나 서수 비교를 수행하려 해도 <xref:System.StringComparison> 형식을 명시적으로 지정하는 오버로드를 호출하는 것이 좋습니다. 이렇게 하면 특정 문자열 해석을 위해 코드를 더 쉽게 검색할 수 있습니다.  
  
### <a name="stringtoupper-and-stringtolower"></a>String.ToUpper 및 String.ToLower  
 기본 해석: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType>.  
  
 문자열을 대문자 또는 소문자에 적용하는 방법은 대/소문자와 관계없이 문자열 비교 시 작은 정규화로 사용되므로 이들 메서드를 사용할 때 주의해야 합니다. 이들 메서드를 사용할 경우 대/소문자를 구분하지 않는 비교를 사용하는 것이 좋습니다.  
  
 <xref:System.String.ToUpperInvariant%2A?displayProperty=nameWithType> 및 <xref:System.String.ToLowerInvariant%2A?displayProperty=nameWithType> 메서드도 사용할 수 있습니다. <xref:System.String.ToUpperInvariant%2A> 는 대/소문자를 정규화하는 표준 방법입니다. <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> 를 사용한 비교는 동작으로 두 가지 호출(두 문자열 인수에 대한 <xref:System.String.ToUpperInvariant%2A> 호출 및 <xref:System.StringComparison.Ordinal?displayProperty=nameWithType>을 사용한 비교 수행)의 컴퍼지션입니다.  
  
 문화권을 나타내는 <xref:System.Globalization.CultureInfo> 개체를 메서드에 전달하여 특정 문화권에서 대문자 및 소문자로 변환하는 데도 오버로드를 사용할 수 있습니다.  
  
### <a name="chartoupper-and-chartolower"></a>Char.ToUpper 및 Char.ToLower  
 기본 해석: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType>.  
  
 이들 메서드는 이전 섹션에서 설명된 <xref:System.String.ToUpper%2A?displayProperty=nameWithType> 및 <xref:System.String.ToLower%2A?displayProperty=nameWithType> 메서드와 비슷하게 작동합니다.  
  
### <a name="stringstartswith-and-stringendswith"></a>String.StartsWith 및 String.EndsWith  
 기본 해석: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType>.  
  
 기본적으로 이들 메서드는 둘 다 문화권 구분 비교를 수행합니다.  
  
### <a name="stringindexof-and-stringlastindexof"></a>String.IndexOf 및 String.LastIndexOf  
 기본 해석: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType>.  
  
 이들 메서드의 기본 오버로드가 비교를 수행하는 방식에는 일관성이 없습니다. <xref:System.String.IndexOf%2A?displayProperty=nameWithType> 매개 변수를 포함하는 모든 <xref:System.String.LastIndexOf%2A?displayProperty=nameWithType> 및 <xref:System.Char> 메서드는 서수 비교를 수행하지만, <xref:System.String.IndexOf%2A?displayProperty=nameWithType> 매개 변수를 포함하는 기본 <xref:System.String.LastIndexOf%2A?displayProperty=nameWithType> 및 <xref:System.String> 메서드는 문화권 구분 비교를 수행합니다.  
  
 <xref:System.String.IndexOf%28System.String%29?displayProperty=nameWithType> 또는 <xref:System.String.LastIndexOf%28System.String%29?displayProperty=nameWithType> 메서드를 호출하고 현재 인스턴스에서 찾을 문자열을 전달할 경우 <xref:System.StringComparison> 형식을 명시적으로 지정하는 오버로드를 호출하는 것이 좋습니다. <xref:System.Char> 인수를 포함하는 오버로드를 사용하면 <xref:System.StringComparison> 형식을 지정할 수 없습니다.  
  
 [맨 위로 이동](#top)  
  
<a name="methods_that_perform_string_comparison_indirectly"></a>   
## <a name="methods-that-perform-string-comparison-indirectly"></a>문자열 비교를 간접적으로 수행하는 방법  
 문자열 비교를 중심 작업으로 포함하는 일부 문자열이 아닌 메서드에는 <xref:System.StringComparer> 형식이 사용됩니다. <xref:System.StringComparer> 클래스에는 포함된 <xref:System.StringComparer> 메서드가 다음 형식의 문자열 비교를 수행하는 <xref:System.StringComparer.Compare%2A?displayProperty=nameWithType> 인스턴스를 반환하는 정적 속성 6개가 포함됩니다.  
  
- 현재 문화권을 사용한 문화권 구분 문자열 비교. 이 <xref:System.StringComparer> 개체는 <xref:System.StringComparer.CurrentCulture%2A?displayProperty=nameWithType> 속성에서 반환됩니다.  
  
- 현재 문화권을 사용한 대/소문자를 구분하지 않는 문자열 비교. 이 <xref:System.StringComparer> 개체는 <xref:System.StringComparer.CurrentCultureIgnoreCase%2A?displayProperty=nameWithType> 속성에서 반환됩니다.  
  
- 고정 문화권의 단어 비교 규칙을 사용한 대/소문자를 구분하지 않는 비교. 이 <xref:System.StringComparer> 개체는 <xref:System.StringComparer.InvariantCulture%2A?displayProperty=nameWithType> 속성에서 반환됩니다.  
  
- 고정 문화권의 단어 비교 규칙을 사용한 대/소문자를 구분하지 않고 문화권을 구분하지 않는 비교. 이 <xref:System.StringComparer> 개체는 <xref:System.StringComparer.InvariantCultureIgnoreCase%2A?displayProperty=nameWithType> 속성에서 반환됩니다.  
  
- 서수 비교. 이 <xref:System.StringComparer> 개체는 <xref:System.StringComparer.Ordinal%2A?displayProperty=nameWithType> 속성에서 반환됩니다.  
  
- 대소문자를 구분하지 않는 서수 비교. 이 <xref:System.StringComparer> 개체는 <xref:System.StringComparer.OrdinalIgnoreCase%2A?displayProperty=nameWithType> 속성에서 반환됩니다.  
  
### <a name="arraysort-and-arraybinarysearch"></a>Array.Sort 및 Array.BinarySearch  
 기본 해석: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType>.  
  
 컬렉션에 데이터를 저장하거나 영구 데이터를 파일이나 데이터베이스에서 컬렉션으로 읽을 때 현재 문화권을 전환하면 컬렉션에서 고정이 무효화될 수 있습니다. <xref:System.Array.BinarySearch%2A?displayProperty=nameWithType> 메서드는 검색할 배열의 요소가 이미 정렬되었다고 가정합니다. 배열에서 문자열 요소를 정렬하려고 <xref:System.Array.Sort%2A?displayProperty=nameWithType> 메서드는 <xref:System.String.Compare%2A?displayProperty=nameWithType> 메서드를 호출하여 개별 요소의 순서를 지정합니다. 배열이 정렬된 시간과 콘텐츠가 검색된 시간 사이에 문화권이 변경될 경우 문화권 구분 비교자 사용이 위험할 수 있습니다. 예를 들어 다음 코드에서 스토리지 및 검색은 `Thread.CurrentThread.CurrentCulture` 속성에 의해 암시적으로 제공되는 비교자에서 작동합니다. `StoreNames` 및 `DoesNameExist`에 대한 호출 사이에 문화권이 변경되고 특히 배열 콘텐츠가 두 메서드 호출 사이에 지속되면 이진 검색이 실패할 수 있습니다.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/indirect1.cs#7)]
 [!code-vb[Conceptual.Strings.BestPractices#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/indirect1.vb#7)]  
  
 배열을 정렬 및 검색할 때 둘 다 같은 서수(문화권을 구분하지 않는) 비교 메서드를 사용하는 다음 예제에서 권장되는 변형을 보여 줍니다. 변경 코드는 두 예제의 `Line A` 및 `Line B` 줄에 반영됩니다.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/indirect1.cs#8)]
 [!code-vb[Conceptual.Strings.BestPractices#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/indirect1.vb#8)]  
  
 이 데이터가 문화권에 걸쳐 지속 및 이동되고 이 데이터를 사용자에게 제공할 때 정렬을 사용할 경우 향상된 사용자 출력을 위해 언어적으로 작동하지만 문화권 변경의 영향을 받지 않는 <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType>를 사용하는 것이 좋을 수 있습니다. 다음 예제에서는 두 가지 이전 예제에서 배열 정렬 및 검색에 고정 문화권을 사용하도록 수정합니다.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/indirect1.cs#9)]
 [!code-vb[Conceptual.Strings.BestPractices#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/indirect1.vb#9)]  
  
### <a name="collections-example-hashtable-constructor"></a>컬렉션 예제: 해시 가능한 생성자  
 문자열 비교 방법이 영향을 미치는 작업의 두 번째 예로는 문자열 해시가 있습니다.  
  
 다음 예제에서는 <xref:System.Collections.Hashtable> 속성에서 반환되는 <xref:System.StringComparer> 개체를 전달하여 <xref:System.StringComparer.OrdinalIgnoreCase%2A?displayProperty=nameWithType> 개체를 인스턴스화합니다. <xref:System.StringComparer> 에서 파생된 <xref:System.StringComparer> 클래스는 <xref:System.Collections.IEqualityComparer> 인터페이스를 구현하므로 해당 <xref:System.Collections.IEqualityComparer.GetHashCode%2A> 메서드는 해시 테이블에서 문자열의 해시 코드를 컴퓨팅하는 데 사용됩니다.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/indirect2.cs#10)]
 [!code-vb[Conceptual.Strings.BestPractices#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/indirect2.vb#10)]  
  
 [맨 위로 이동](#top)  
  
<a name="Formatted"></a>   
## <a name="displaying-and-persisting-formatted-data"></a>서식이 지정된 데이터 표시 및 유지

숫자와 날짜 및 시간과 같은 문자열이 아닌 데이터를 사용자에게 표시할 때 사용자의 문화권 설정을 사용하여 형식을 지정합니다. 기본적으로 다음 항목은 모두 서식 지정 작업에서 현재 스레드 문화권을 사용합니다.

- [C#](../../csharp/language-reference/tokens/interpolated.md) 및 [Visual Basic](../../visual-basic/programming-guide/language-features/strings/interpolated-strings.md) 컴파일러에서 지원하는 보간된 문자열입니다.

- [C#](../../csharp/language-reference/operators/addition-operator.md#string-concatenation) 또는 [Visual Basic](../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md ) 연결 연산자를 사용하거나 직접 <xref:System.String.Concat%2A?displayProperty=nameWithType> 메서드를 호출하는 문자열 연결 연산자입니다.

- <xref:System.String.Format%2A?displayProperty=nameWithType> 메서드

- 숫자 형식과 날짜 및 시간 형식의 `ToString` 메서드.

지정된 문화권의 규칙 또는 [고정 문화권](xref:System.Globalization.CultureInfo.InvariantCulture)을 사용하여 문자열의 서식을 지정해야 함을 명시적으로 지정하려면 다음을 수행합니다.

- <xref:System.String.Format%2A?displayProperty=nameWithType> 및 `ToString` 메서드를 사용하는 경우 <xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType> 또는 <xref:System.DateTime.ToString%28System.IFormatProvider%29?displayProperty=nameWithType>과 같이 `provider` 매개 변수가 있는 오버로드를 호출하고 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> 속성, 원하는 문화권을 나타내는 <xref:System.Globalization.CultureInfo> 인스턴스 또는 <xref:System.Globalization.CultureInfo.InvariantCulture?displayProperty=nameWithType> 속성을 전달합니다.  

- 문자열 연결의 경우 컴파일러에서 암시적 변환을 수행하지 못하게 합니다. 대신 `provider` 매개 변수가 있는 `ToString` 오버로드를 호출하여 명시적 변환을 수행합니다. 예를 들어 컴파일러는 <xref:System.Double> 값을 다음 C# 코드의 문자열로 변환할 때 암시적으로 현재 문화권을 사용합니다.

  [!code-csharp[Implicit String Conversion](~/samples/snippets/standard/base-types/string-practices/cs/tostring.cs#1)]

  대신, 다음 C# 코드와 같이 <xref:System.Double.ToString(System.IFormatProvider)?displayProperty=nameWithType> 메서드를 호출하여 변환에 사용되는 서식 지정 규칙을 사용하는 문화권을 명시적으로 지정할 수 있습니다.

  [!code-csharp[Explicit String Conversion](~/samples/snippets/standard/base-types/string-practices/cs/tostring.cs#2)]

- 문자열 보간의 경우, 보간된 문자열을 <xref:System.String> 인스턴스에 할당하는 대신 <xref:System.FormattableString>에 할당합니다. 그런 다음, 해당 <xref:System.FormattableString.ToString?displayProperty=nameWithType> 메서드를 호출하여 현재 문화권의 규칙을 반영하는 결과 문자열을 생성하거나 <xref:System.FormattableString.ToString(System.IFormatProvider)?displayProperty=nameWithType> 메서드를 호출하여 지정된 문화권의 규칙을 반영하는 결과 문자열을 생성할 수 있습니다. 서식 지정 가능 문자열을 정적 <xref:System.FormattableString.Invariant%2A?displayProperty=nameWithType> 메서드에 전달하여 고정 문화권의 규칙을 반영하는 결과 문자열을 생성할 수도 있습니다. 다음 예제에서 이 방법을 보여 줍니다. (이 예제의 출력에는 en-US의 현재 문화권이 반영됩니다.)

  [!code-csharp[String interpolation](~/samples/snippets/standard/base-types/string-practices/cs/formattable.cs)]
  [!code-vb[String interpolation](~/samples/snippets/standard/base-types/string-practices/vb/formattable.vb)]

문자열이 아닌 데이터를 이진 데이터 또는 형식이 지정된 데이터로 유지할 수 있습니다. 서식이 지정된 데이터로 저장하는 경우 `provider` 매개 변수를 포함하는 서식 지정 메서드 오버로드를 호출하고 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 속성에 전달해야 합니다. 고정 문화권은 문화권 및 컴퓨터와 관계없는 형식이 지정된 데이터에 대해 일관된 형식을 제공합니다. 반대로 고정 문화권이 아닌 문화권을 사용하여 형식이 지정된 영구 데이터에는 많은 제한 사항이 있습니다.  
  
- 다른 문화권이 포함된 시스템에서 데이터를 검색하거나 현재 시스템의 사용자가 현재 문화권을 변경하고 데이터를 검색하려고 하면 데이터를 사용하지 못할 수 있습니다.  
  
- 특정 컴퓨터의 문화권 속성은 표준 값과 다를 수 있습니다. 언제든지 사용자가 문화권 구분 표시 설정을 사용자 지정할 수 있습니다. 이로 인해 사용자가 문화권 설정을 사용자 지정한 후에는 시스템에 저장된 형식이 지정된 데이터를 읽지 못할 수 있습니다. 컴퓨터 간에 형식이 지정된 데이터의 이식성은 훨씬 더 제한적일 수 있습니다.  
  
- 숫자 또는 날짜/시간의 형식 지정을 관리하는 국제, 지역 또는 국가 표준은 시간에 지나면서 변경되고 이들 변경은 Windows 운영 체제 업데이트에 통합됩니다. 형식 지정 규칙이 변경될 때 이전 규칙을 사용하여 형식이 지정된 데이터를 읽지 못하게 될 수 있습니다.  
  
 다음 예제에서는 문화권 구분 형식 지정을 사용하여 데이터를 유지함으로 인해 제한된 이식성을 보여 줍니다. 예제에서는 날짜 및 시간 값 배열을 파일에 저장합니다. 이들 값은 영어(미국) 문화권의 규칙을 사용하여 형식이 지정됩니다. 애플리케이션이 현재 스레드 문화권을 프랑스어(스위스)로 변경하고 나면 현재 문화권의 형식 지정 규칙을 사용하여 저장된 값을 읽으려고 합니다. 두 데이터 항목을 읽으려는 시도로 인해 <xref:System.FormatException> 예외가 throw되고 날짜 배열에는 <xref:System.DateTime.MinValue>와 같은 잘못된 두 가지 요소가 포함됩니다.  
  
 [!code-csharp[Conceptual.Strings.BestPractices#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/persistence.cs#21)]
 [!code-vb[Conceptual.Strings.BestPractices#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/persistence.vb#21)]  
  
 그러나 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> 및 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 에 대한 호출에서 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> 속성을 <xref:System.DateTime.Parse%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType>로 바꾸면 다음 출력과 같이 영구 날짜 및 시간 데이터가 성공적으로 복원됩니다.  
  
```console  
06.05.1758 21:26  
05.05.1818 07:19  
22.04.1870 23:54  
08.09.1890 06:47  
18.02.1905 15:12  
```  
  
## <a name="see-also"></a>참고 항목

- [문자열 조작](../../../docs/standard/base-types/manipulating-strings.md)
