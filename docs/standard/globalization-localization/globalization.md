---
title: 전역화
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- globalization [.NET Framework], about globalization
- global applications, globalization
- international applications [.NET Framework], globalization
- world-ready applications, globalization
- application development [.NET Framework], globalization
- culture, globalization
ms.assetid: 4e919934-6b19-42f2-b770-275a4fae87c9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ce2f127858305a96b358c1661b98a359ae565f57
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393124"
---
# <a name="globalization"></a>전역화

전역화는 다양한 문화권의 사용자를 위해 현지화된 인터페이스와 국가별 데이터를 지원하는 지역화 대비 응용 프로그램을 디자인하고 개발하는 작업을 수반합니다. 디자인 단계를 시작하기 전에 앱에서 지원할 문화권을 결정해야 합니다. 앱이 기본적으로 단일 문화권이나 국가를 대상으로 하더라도, 다른 문화권이나 국가의 사용자에게 쉽게 확장될 수 있도록 디자인하고 작성할 수 있습니다.

모든 개발자는 각 문화권에 의해 형성된 사용자 인터페이스와 데이터에 대해 가정하는 부분이 있습니다. 예를 들어, 미국에서 영어를 사용하는 개발자가 날짜 및 시간 데이터를 `MM/dd/yyyy hh:mm:ss` 서식의 문자열로 serialize하는 것은 매우 합당해 보입니다. 하지만 그 문자열을 다른 문화권의 시스템에서 deserialize하면 <xref:System.FormatException> 예외를 throw하거나 정확하지 않은 데이터를 생성할 수 있습니다. 전역화는 문화권별 가정을 식별하고 그것이 앱의 디자인이나 코드에 영향을 미치지 않도록 합니다.

이 문서에서는 세계화된 앱에서 고려해야 할 몇 가지 주요 문제와 문자열, 날짜, 시간 값과 숫자 값을 처리할 때 따를 수 있는 모범 사례를 설명합니다.

## <a name="strings"></a>문자열

각 문화권이나 국가는 다양한 문자 및 문자 집합을 사용하고 다양한 방식으로 문자를 정렬하기 때문에 문자와 문자열 처리는 전역화의 중심점입니다. 이 섹션에서는 전역화된 앱에서 문자열 사용에 대한 권장 사항을 제공합니다.

### <a name="use-unicode-internally"></a>내부적으로 유니코드 사용

기본적으로 .NET에서는 유니코드 문자열을 사용합니다. 유니코드 문자열은 0 또는 하나 이상의 <xref:System.Char> 개체로 구성되며, 각 개체는 UTF-16 코드 단위를 나타냅니다. 전세계에서 사용되는 모든 문자 집합의 거의 모든 문자에 대해서는 유니코드 표현이 있습니다.

Windows 운영 체제를 비롯한 많은 애플리케이션과 운영 체제는 코드 페이지를 사용하여 문자 집합을 나타낼 수도 있습니다. 일반적으로 코드 페이지는 0x00부터 0x7F까지 표준 ASCII 값을 포함하며 다른 문자를 0x80부터 0xFF까지 나머지 값에 매핑합니다. 0x80부터 0xFF까지 값에 대한 해석은 특정 코드 페이지에 따라 달라집니다. 이 때문에 전역화된 앱에서 가능하면 코드 페이지 사용을 피해야 합니다.

다음 예제는 시스템의 기본 코드 페이지가 데이터가 저장된 코드 페이지와 다른 경우 코드 페이지 데이터 해석의 위험을 보여줍니다. (이 시나리오를 시뮬레이션하기 위해, 예제에 다른 코드 페이지를 명시적으로 지정합니다.) 우선, 예제에 그리스어 알파벳의 대문자로 구성된 배열을 정의합니다. 이것을 코드 페이지 737(MS-DOS Greek이라고도 함)을 사용하여 바이트 배열로 인코딩하고 바이트 배열을 파일로 저장합니다. 파일을 가져와서 코드 페이지 737을 사용하여 바이트 배열을 디코딩하면, 원래 문자가 복원됩니다. 하지만, 파일을 가져와서 코드 페이지 1252(또는 라틴 알파벳 문자를 나타내는Windows-1252)를 사용하여 바이트 배열을 디코딩하면, 원래 문자가 손실됩니다.

[!code-csharp[Conceptual.Globalization#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/codepages1.cs#1)]
[!code-vb[Conceptual.Globalization#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/codepages1.vb#1)]

유니코드를 사용하면 동일한 코드 단위가 항상 동일한 문자에 매핑되고, 동일한 문자가 항상 동일한 바이트 배열에 매핑되도록 할 수 있습니다.

### <a name="use-resource-files"></a>리소스 파일 사용

단일 문화권이나 국가를 대상하는 하는 앱을 개발하더라도 사용자 인터페이스로 표시되는 문자열 및 기타 리소스를 저장하는 리소스 파일을 사용해야 합니다. 이러한 리소스는 절대로 코드에 직접 추가하지 말아야 합니다. 리소스 파일을 사용하면 많은 장점이 있습니다.

- 모든 문자열이 단일 위치에 존재합니다. 특정 언어나 문화권에 대해 수정하기 위해 문자열을 식별하려고 소스 코드 전체를 검색할 필요가 없습니다.

- 문자열을 중복할 필요가 없습니다. 리소스 파일을 자주 사용하지 않는 개발자는 동일한 문자열을 여러 소스 코드 파일에 정의하곤 합니다. 이렇게 중복하면 문자열을 수정할 때 하나 이상의 인스턴스를 간과할 가능성이 높아집니다.

- 이미지 또는 이진 데이터와 같이 문자열이 아닌 리소스를 별도의 독립 실행형 파일 대신 리소스 파일에 포함시키면 쉽게 가져올 수 있습니다.

리소스 파일을 사용하면 특히 현지화된 앱을 만드는 경우에 장점이 있습니다. 위성 어셈블리로 리소스를 배포하는 경우, 공용 언어 런타임은 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> 속성에 의해 정의된 사용자의 현재 UI 문화권을 기반으로 적절한 문화권의 리소스를 자동으로 선택합니다. 문화권별로 적절한 리소스를 제공하고 <xref:System.Resources.ResourceManager> 개체를 제대로 인스턴스화하거나 강력한 형식 리소스 클래스를 사용하기만 한다면, 런타임에서 적절한 리소스를 가져오는 세부 정보를 처리합니다.

리소스 파일을 만드는 방법에 대한 자세한 내용은 [리소스 파일 만들기](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md)를 참조하세요. 위성 어셈블리를 만들고 배포하는 방법에 대한 자세한 내용은 [위성 어셈블리 만들기](../../../docs/framework/resources/creating-satellite-assemblies-for-desktop-apps.md) 및 [리소스 패키징 및 배포](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md)를 참조하세요.

### <a name="search-and-compare-strings"></a>문자열 검색 및 비교

가능하면 문자열을 일련의 개별 문자로 처리하는 대신 전체 문자열로 처리합니다. 이것은 부분 문자열을 정렬하거나 검색하는 경우, 결합된 문자의 구문 분석과 관련된 문제를 방지하는 데 특히 중요합니다.

> [!TIP]
> 문자열의 개별 문자 보다는 텍스트 요소에 <xref:System.Globalization.StringInfo> 클래스를 사용할 수 있습니다.

문자열 검색 및 비교 시 일반적인 실수는 문자열을 각각 <xref:System.Char> 개체로 표시되는 문자의 컬렉션으로 다루는 것입니다. 실제, 단일 문자는 하나, 둘, 또는 그 이상의 <xref:System.Char> 개체로 형성될 수 있습니다. 이러한 문자는 알파벳이 유니코드 기본 라틴 문자의 범위(U+0021 ~ U+007E)에 속하지 않는 문자로 구성된 문화권의 문자열에서 가장 빈번하게 나타납니다. 다음 예제는 문자열에서 LATIN CAPITAL LETTER A WITH GRAVE 문자(U+00C0)의 인덱스를 찾으려고 합니다. 하지만 이 문자는 단일 코드 단위(U+00C0) 또는 복합 문자(두 코드 단위: U+0021 및 U+007E)처럼 두 가지 다른 방법으로 나타낼 수 있습니다. 이런 경우, 문자는 2개의 <xref:System.Char> 개체 즉, U+0021 및 U+007E를 통해 문자열 인스턴스로 표현됩니다. 예제 코드는 문자열 인스턴스 내에서 이 문자의 위치를 찾기 위해 <xref:System.String.IndexOf%28System.Char%29?displayProperty=nameWithType> 및 <xref:System.String.IndexOf%28System.String%29?displayProperty=nameWithType> 오버로드를 호출하지만 이것은 다른 결과를 반환합니다. 첫 번째 메서드 호출에는 <xref:System.Char> 인수가 있고, 이것이 서수 비교를 수행하기 때문에 일치하는 값을 찾을 수 없습니다. 두 번째 호출에는 <xref:System.String> 인수가 있고, 이것은 문화권구분 비교를 수행하기 때문에 일치하는 값을 찾습니다.

[!code-csharp[Conceptual.Globalization#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/search1.cs#18)]
[!code-vb[Conceptual.Globalization#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/search1.vb#18)]

<xref:System.String.IndexOf%28System.String%2CSystem.StringComparison%29?displayProperty=nameWithType> 또는 <xref:System.String.LastIndexOf%28System.String%2CSystem.StringComparison%29?displayProperty=nameWithType> 메서드와 같이 <xref:System.StringComparison> 매개 변수를 포함하는 오버로드를 호출하면 이 예제(다른 결과를 반환하는 메서드의 두 가지 유사한 오버로드에 대한 호출)의 모호성을 피할 수 있습니다.

하지만 검색에 항상 문화권을 구분하지는 않습니다. 검색의 목적이 보안 결정을 내리거나 리소스에 대한 액세스를 허용하거나 허용하지 않는 것이라면, 비교는 다음 섹션의 설명처럼 서수여야 합니다.

### <a name="test-strings-for-equality"></a>문자열이 같은지 테스트

두 개 문자열의 정렬 순서를 비교하는 방법을 결정하는 게 아니라 문자열 두 개가 같은지를 테스트하려면 <xref:System.String.Compare%2A?displayProperty=nameWithType> 또는 <xref:System.Globalization.CompareInfo.Compare%2A?displayProperty=nameWithType>와 같은 문자열 비교 메서드 대신 <xref:System.String.Equals%2A?displayProperty=nameWithType> 메서드를 사용합니다.

같음 비교는 조건부로 일부 리소스에 액세스하기 위해 수행됩니다. 예를 들어, 암호를 확인하거나 파일이 있는지 확인하기 위해 같음 비교를 수행합니다. 이러한 비언어적인 비교는 문화권을 구분하지 않고 항상 서수여야 합니다. 일반적으로 암호와 같은 문자열에 대해서는 <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> 값으로, 파일 이름 또는 URI와 같은 문자열에 대해서는 <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> 값으로, 인스턴스 <xref:System.String.Equals%28System.String%2CSystem.StringComparison%29?displayProperty=nameWithType> 메서드 또는 정적 <xref:System.String.Equals%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> 메서드를 호출해야 합니다.

같음 비교에 <xref:System.String.Equals%2A?displayProperty=nameWithType> 메서드에 대한 호출이 아닌 검색 또는 부분 문자열 비교를 수반하는 경우가 있습니다. 경우에 따라, 부분 문자열이 다른 문자열과 같은지를 판단하기 위해 부분 문자열 검색을 사용할 수 있습니다. 비교의 목적이 비언어적인 경우, 검색은 문화권 구분이 아닌 서수여야 합니다.

다음 예제는 비언어적인 데이터에 대한 문화권 구분 검색의 위험을 설명합니다. `AccessesFileSystem` 메서드는 "FILE"이라는 부분 문자열로 시작되는 URI에 대한 파일 시스템 액세스를 금지하도록 설계되었습니다. 이를 위해, URI의 시작 부분을 "FILE"이라는 문자열과 문화권을 구분하고 대/소문자를 구분하지 않는 비교를 수행합니다. 파일 시스템에 액세스하는 URI는 “FILE:” 또는 “file:”로 시작되기 때문에 “i”(U+0069)는 언제나 “I”(U+0049)에 해당하는 소문자라는 암묵적인 가정이 있습니다. 하지만 터키어 및 아제르바이잔어에서 "i"의 대문자 버전은 "İ"(U+0130)입니다. 이러한 불일치로 인해, 문화권 구분 비교는 파일 시스템 액세스를 금지해야 하는 경우에 액세스를 허용합니다.

[!code-csharp[Conceptual.Globalization#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/equals1.cs#12)]
[!code-vb[Conceptual.Globalization#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/equals1.vb#12)]

다음 예제와 같은 대/소문자를 무시하는 서수 비교를 수행하여 이러한 문제를 방지할 수 있습니다.

[!code-csharp[Conceptual.Globalization#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/equals2.cs#13)]
[!code-vb[Conceptual.Globalization#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/equals2.vb#13)]

### <a name="order-and-sort-strings"></a>문자열 순서 및 정렬

일반적으로 사용자 인터페이스로 표시되는 순서가 지정된 문자열은 문화권을 기반으로 정렬되어야 합니다. 대부분의 경우, 이러한 문자열 비교는 <xref:System.Array.Sort%2A?displayProperty=nameWithType> 또는 <xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=nameWithType>와 같이 문자열을 정렬하는 메서드를 호출할 때 .NET에 의해 암시적으로 처리됩니다. 기본적으로 문자열은 현재 문화권의 정렬 규칙을 사용하여 정렬됩니다. 다음 예제는 문자열 배열이 영어(미국) 문화권과 스웨덴어(스웨덴) 문화권의 규칙을 사용하여 정렬되는 경우 차이점을 설명합니다.

[!code-csharp[Conceptual.Globalization#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/sort1.cs#14)]
[!code-vb[Conceptual.Globalization#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/sort1.vb#14)]

문화권 구분 문자열 비교는 <xref:System.Globalization.CompareInfo> 개체로 정의되며, 이것은 각 문화권의 <xref:System.Globalization.CultureInfo.CompareInfo%2A?displayProperty=nameWithType> 속성에 의해 반환됩니다. <xref:System.String.Compare%2A?displayProperty=nameWithType> 메서드 오버로드를 사용하는 문화권 구분 문자열 비교는 <xref:System.Globalization.CompareInfo> 개체도 사용합니다.

.NET에서는 테이블을 사용하여 문자열 데이터에 대해 문화권 구분 정렬을 수행합니다. 이러한 테이블의 내용에는 정렬 가중치 및 문자열 정규화에 대한 데이터가 포함되며, 이것은 특정한 .NET 버전에서 구현되는 유니코드 표준 버전에 의해 결정됩니다. 다음 테이블에는 지정된 .NET Framework 버전 및 .NET Core로 구현되는 유니코드 버전이 나열되어 있습니다. 지원되는 유니코드 버전 목록은 문자 비교 및 정렬에만 적용되며 범주에 따른 유니코드 문자의 분류에는 적용되지 않습니다. 자세한 내용은 <xref:System.String> 항목의 “문자열과 유니코드 표준” 섹션을 참조하세요.

|.NET Framework 버전|운영 체제|유니코드 버전|
|----------------------------|----------------------|---------------------|
|.NET Framework 2.0|모든 운영 체제|Unicode 4.1|
|.NET Framework 3.0|모든 운영 체제|Unicode 4.1|
|.NET Framework 3.5|모든 운영 체제|Unicode 4.1|
|.NET Framework 4|모든 운영 체제|Unicode 5.0|
|Windows 7의 .NET Framework 4.5 이상|Unicode 5.0|
|Windows 8 이상 운영 체제의 .NET Framework 4.5 이상|유니코드 6.3.0|
|.NET Core(모든 버전)|기본 운영 체제에서 지원되는 유니코드 표준의 버전에 따라 달라집니다.|

.NET Framework 4.5 이상 및 모든 버전의 .NET Core에서 문자열 비교 및 정렬은 운영 체제에 따라 달라집니다. Windows 7에서 실행되는 .NET Framework 4.5 이상은 Unicode 5.0을 구현하는 자체 테이블의 데이터를 검색합니다. Windows 8 이상에서 실행되는 .NET Framework 4.5 이상은 Unicode 6.3을 구현하는 운영 체제 테이블의 데이터를 검색합니다. .NET Core에서 지원되는 유니코드의 버전은 기본 운영 체제에 따라 달라집니다. 문화권 구분 정렬 데이터를 직렬화하면 <xref:System.Globalization.SortVersion> 클래스를 사용하여 직렬화된 데이터가 .NET 및 운영 체제의 정렬 순서와 일치하도록 정렬되어야 하는 시기를 결정할 수 있습니다. 예제는 <xref:System.Globalization.SortVersion> 클래스 항목을 참조하세요.

앱에서 문자열 데이터의 광범위한 문화권별 정렬을 수행하는 경우, <xref:System.Globalization.SortKey> 클래스를 사용하여 문자열을 비교합니다. 정렬 키는 알파벳, 대/소문자, 특정 문자열의 분음 부호 가중치를 비롯한 문화권별 정렬 가중치를 반영합니다. 정렬 키를 사용한 비교는 이진이기 때문에 암시적 또는 명시적으로 <xref:System.Globalization.CompareInfo> 개체를 사용하는 비교보다 빠릅니다. 문자열을 <xref:System.Globalization.CompareInfo.GetSortKey%2A?displayProperty=nameWithType> 메서드에 전달하여 특정 문자열에 대한 문화권별 정렬 키를 만듭니다.

다음 예제는 이전 예제와 유사합니다. 하지만 <xref:System.Globalization.CompareInfo.Compare%2A?displayProperty=nameWithType> 메서드를 암시적으로 호출하는 <xref:System.Array.Sort%28System.Array%29?displayProperty=nameWithType> 메서드를 호출하는 대신, 정렬 키를 비교하는 <xref:System.Collections.Generic.IComparer%601?displayProperty=nameWithType> 구현을 정의하고, 인스턴스화하여 <xref:System.Array.Sort%60%601%28%60%600%5B%5D%2CSystem.Collections.Generic.IComparer%7B%60%600%7D%29?displayProperty=nameWithType> 메서드에 전달합니다.

[!code-csharp[Conceptual.Globalization#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/sortkey1.cs#15)]
[!code-vb[Conceptual.Globalization#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/sortkey1.vb#15)]

### <a name="avoid-string-concatenation"></a>문자열 연결 사용하지 않기

만약 가능하다면, 연결된 구에서 런타임에 작성된 복합 문자열을 사용하지 마십시오. 복합 문자열은 다른 현지화된 언어에 적용되지 않는 앱의 원래 언어로 문법적인 순서를 가정하는 경우가 많기 때문에 현지화하기 어렵습니다.

## <a name="handle-dates-and-times"></a>날짜 및 시간 처리

날짜 및 시간 값을 처리하는 방법은 사용자 인터페이스로 표시되거나 지속되는 여부에 따라 다릅니다. 이 섹션은 두 가지 사용법 모두를 검토합니다. 날짜 및 시간을 작업할 때 표준 시간대 차이 및 산술 연산을 처리하는 방법도 설명합니다.

### <a name="display-dates-and-times"></a>날짜 및 시간 표시

일반적으로 날짜 및 시간이 사용자 인터페이스로 표시되는 경우, 사용자 문화권의 서식 규칙을 사용해야 합니다. 이것은 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> 속성 및 `CultureInfo.CurrentCulture.DateTimeFormat` 속성에 의해 반환되는 <xref:System.Globalization.DateTimeFormatInfo> 개체에 의해 정의됩니다. 현재 문화권의 서식 규칙은 다음 메서드 중 하나를 사용하여 날짜의 서식을 지정할 때 자동으로 사용됩니다.

- 매개 변수가 없는 <xref:System.DateTime.ToString?displayProperty=nameWithType> 메서드

- 서식 문자열을 포함하는 <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> 메서드

- 매개 변수가 없는 <xref:System.DateTimeOffset.ToString?displayProperty=nameWithType> 메서드

- 서식 문자열을 포함하는 <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=nameWithType>

- 날짜에 사용되는 경우, [복합 서식 지정](../../../docs/standard/base-types/composite-formatting.md) 기능

다음 예제는 2012년 10월 11일에 대한 일출 및 일몰 데이터를 두 번 표시합니다. 처음에는 현재 문화권을 크로아티아어(크로아티아)로 설정하고 다음에는 영어(영국)로 설정합니다. 각각의 경우, 날짜 및 시간이 해당 문화권에 적절한 서식으로 표시됩니다.

[!code-csharp[Conceptual.Globalization#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates1.cs#2)]
[!code-vb[Conceptual.Globalization#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates1.vb#2)]

### <a name="persist-dates-and-times"></a>날짜 및 시간 유지

문화권에 따라 달라질 수 있는 서식으로 날짜 및 시간 데이터를 유지하지 말아야 합니다. 이것은 일반적인 프로그래밍 오류이며, 손상된 데이터 또는 런타임 예외를 발생시킵니다. 다음 예제는 2013년 1월 9일 및 2013년 8월 18일이라는 두 개의 날짜를 영어(미국) 문화권의 서식 규칙을 사용하여 문자열로 serialize합니다. 영어(미국) 문화권의 형식을 사용하여 데이터를 가져와서 구문을 분석하면, 성공적으로 복원됩니다. 하지만, 영어(영국) 문화권의 규칙을 사용하여 데이터를 가져와서 구문을 분석하면, 첫 번째 날짜는 9월 1일로 잘못 해석되고 두 번째는 일반 달력에 18번째 달이 없기 때문에 구문 분석에 실패합니다.

[!code-csharp[Conceptual.Globalization#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates2.cs#3)]
[!code-vb[Conceptual.Globalization#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates2.vb#3)]

세 가지 방법 중 하나를 통해 이러한 문제를 피할 수 있습니다.

- 날짜 및 시간을 문자열이 아닌 이진 형식으로 serialize합니다.

- 사용자의 문화권과 상관없이 동일한 사용자 지정 서식 문자열을 사용하여 날짜와 시간의 문자열 표현을 저장하고 구문 분석합니다.

- 고정 문화권의 서식 규칙을 사용하여 문자열을 저장합니다.

다음 예제에서 마지막 방법을 보여 줍니다. 정적 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 속성에 의해 반환되는 고정 문화권의 서식 규칙을 사용합니다.

[!code-csharp[Conceptual.Globalization#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates3.cs#4)]
[!code-vb[Conceptual.Globalization#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates3.vb#4)]

### <a name="serialization-and-time-zone-awareness"></a>Serialization 및 표준 시간대 인식

날짜 및 시간 값은 일반 시간("매장은 2013년 1월 2일 오전 9:00에 개장합니다.")에서 특정한 순간("생년월일: 2013년 1월 2일 오전 6:32:00")에 이르기까지 다수의 해석이 있을 수 있습니다. 시간 값이 특정한 순간을 나타내는 경우 serialize된 값으로부터 복원하며, 사용자의 지리적 위치 또는 표준 시간대와 상관없이 동일한 순간을 나타내도록 해야 합니다.

다음 예제에서는 이 문제를 보여 줍니다. 단일 지역 날짜 및 시간 값을 세 가지 [표준 서식](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)(“G”는 일반 날짜 자세한 시간, “s”는 정렬 가능한 날짜/시간, “o”는 날짜/시간 값 라운드트립)은 물론 이진 형식의 문자열로 저장합니다.

[!code-csharp[Conceptual.Globalization#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates4.cs#10)]
[!code-vb[Conceptual.Globalization#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates4.vb#10)]

데이터가 serialize된 시스템과 표준 시간대가 같은 시스템에서 데이터가 복원되면, deserialize된 날짜 및 시간 값이 원래 값을 정확하게 반영하고 다음과 같이 출력됩니다.

```console
'3/30/2013 6:00:00 PM' --> 3/30/2013 6:00:00 PM Unspecified
'2013-03-30T18:00:00' --> 3/30/2013 6:00:00 PM Unspecified
'2013-03-30T18:00:00.0000000-07:00' --> 3/30/2013 6:00:00 PM Local

3/30/2013 6:00:00 PM Local
```

하지만, 표준 시간대가 다른 시스템에서 데이터를 복원하면, "o"(라운드트립) 표준 서식 문자열로 서식이 지정된 날짜 및 시간 값만 표준 시간대 정보를 유지하기 때문에 동일한 시점을 나타냅니다. 날짜 및 시간 데이터를 로망스 표준 시간대 시스템에서 복원하면 다음과 같이 출력됩니다.

```console
'3/30/2013 6:00:00 PM' --> 3/30/2013 6:00:00 PM Unspecified
'2013-03-30T18:00:00' --> 3/30/2013 6:00:00 PM Unspecified
'2013-03-30T18:00:00.0000000-07:00' --> 3/31/2013 3:00:00 AM Local

3/30/2013 6:00:00 PM Local
```

데이터가 deserialize된 시스템의 표준 시간대와 상관없이 단일 순간을 나타내는 날짜 및 시간 값을 정확하게 반영하려면 다음 중 하나를 수행합니다.

- "o"(라운드트립) 표준 서식 문자열을 사용하여 값을 문자열로 저장합니다. 그런 다음 대상 시스템에서 값을 deserialize합니다.

- 값을 UTC로 변환하고 "r"(RFC1123) 표준 서식 문자열을 사용하여 문자열로 저장합니다. 그런 다음 대상 시스템에서 값을 deserialize하고 현지 시간으로 변환합니다.

- 값을 UTC로 변환하고 "u"(정렬 가능한 유니버설) 표준 서식 문자열을 사용하여 문자열로 저장합니다. 그런 다음 대상 시스템에서 값을 deserialize하고 현지 시간으로 변환합니다.

- 값을 UTC로 변환하고 이진 형식으로 저장합니다. 그런 다음 대상 시스템에서 값을 deserialize하고 현지 시간으로 변환합니다.

다음 예제는 각 방법을 보여 줍니다.

[!code-csharp[Conceptual.Globalization#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates8.cs#11)]
[!code-vb[Conceptual.Globalization#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates8.vb#11)]

데이터가 태평양 표준 시간대 시스템에서 serialize되고 로망스 표준 시간대 시스템에서 deserialize되는 경우에, 예제는 다음과 같이 출력됩니다.

```console
'2013-03-30T18:00:00.0000000-07:00' --> 3/31/2013 3:00:00 AM Local
'Sun, 31 Mar 2013 01:00:00 GMT' --> 3/31/2013 3:00:00 AM Local
'2013-03-31 01:00:00Z' --> 3/31/2013 3:00:00 AM Local

3/31/2013 3:00:00 AM Local
```

자세한 내용은 [표준 시간대 간에 시간 변환](../../../docs/standard/datetime/converting-between-time-zones.md)을 참조하세요.

### <a name="perform-date-and-time-arithmetic"></a>날짜 및 시간 연산 수행

<xref:System.DateTime> 및 <xref:System.DateTimeOffset> 형식 모두 산술 연산을 지원합니다. 두 날짜 값 사이의 차이를 계산하거나 날짜 값에서 특정한 시간 간격을 빼거나 더할 수 있습니다. 하지만 날짜 및 시간 값에 대한 산술 연산은 표준 시간대 및 표준 시간대 조정 규칙을 감안하지 않습니다. 이 때문에, 순간을 나타내는 값에 대한 날짜 및 시간 연산은 부정확한 결과를 반환할 수 있습니다.

예를 들어, 태평양 표준시는 3월 둘째 주 일요일 즉, 2013년 3월 10일에 태평양 일광 절약 시간으로 전환됩니다. 다음 예제에 나와 있듯이 태평양 표준 시간대의 시스템상 시간인 2013년 3월 9일 오전 10시 30분의 48시간 이후인 날짜 및 시간을 계산하면 그 결과가 2013년 3월 11일 오전 10시 30분으로, 중간의 시간대 조정이 고려되지 않습니다.

[!code-csharp[Conceptual.Globalization#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates5.cs#8)]
[!code-vb[Conceptual.Globalization#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates5.vb#8)]

날짜 및 시간 값에 대한 산술 연산이 정확한 결과를 생성하도록 보장하려면 다음 단계를 수행합니다.

1. 소스 표준 시간대의 시간을 UTC로 변환합니다.

2. 산술 연산을 수행합니다.

3. 결과가 날짜 및 시간 값이면, UTC에서 소스 표준 시간대의 시간으로 변환합니다.

다음 예제는 2013년 3월 9일 오전 10시 30분에 48시간을 제대로 더하기 위하여 이러한 세 가지 단계를 수행한 것을 제외하면 이전 예제와 유사합니다.

[!code-csharp[Conceptual.Globalization#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/dates6.cs#9)]
[!code-vb[Conceptual.Globalization#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/dates6.vb#9)]

자세한 내용은 [날짜 및 시간에 대한 산술 연산 수행](../../../docs/standard/datetime/performing-arithmetic-operations.md)을 참조하세요.

### <a name="use-culture-sensitive-names-for-date-elements"></a>날짜 요소에서 문화권 구분 이름 사용

앱에 월 이름 또는 요일을 표시해야 하는 경우가 있습니다. 이를 위해서는, 다음과 같은 코드가 일반적입니다.

[!code-csharp[Conceptual.Globalization#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/monthname1.cs#19)]
[!code-vb[Conceptual.Globalization#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/monthname1.vb#19)]

하지만 이 코드는 요일의 이름을 항상 영어로 반환합니다. 월 이름을 추출하는 코드는 훨씬 더 유연한 경우가 많습니다. 특정 언어에 월 이름과 12개월 달력이 있을 것으로 가정하는 경우가 많습니다.

다음 예제에서 볼 수 있듯이, [사용자 지정 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/custom-date-and-time-format-strings.md) 또는 <xref:System.Globalization.DateTimeFormatInfo> 개체의 속성을 사용하면 사용자 문화권의 월 또는 요일 이름을 반영하는 문자열을 쉽게 추출할 수 있습니다. 현재 문화권을 프랑스어(프랑스)로 변경하고 2013년 7월 1일에 대한 월 이름과 요일 이름을 나타냅니다.

[!code-csharp[Conceptual.Globalization#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/monthname2.cs#20)]
[!code-vb[Conceptual.Globalization#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/monthname2.vb#20)]

## <a name="numeric-values"></a>숫자 값

숫자 처리는 숫자가 사용자 인터페이스로 표시되거나 지속되는 여부에 따라 달라집니다. 이 섹션은 두 가지 사용법 모두를 검토합니다.

> [!NOTE]
> 구문 분석 및 서식 지정 작업에서 .NET은 0에서 9까지(U+0030 ~ U+0039)의 기본 라틴 문자를 숫자로만 인식합니다.

### <a name="display-numeric-values"></a>숫자 값 표시

일반적으로 숫자가 사용자 인터페이스로 표시되는 경우, 사용자 문화권의 서식 규칙을 사용해야 합니다. 이것은 <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> 속성 및 `CultureInfo.CurrentCulture.NumberFormat` 속성에 의해 반환되는 <xref:System.Globalization.NumberFormatInfo> 개체에 의해 정의됩니다. 현재 문화권의 서식 규칙은 다음 메서드 중 하나를 사용하여 날짜의 서식을 지정할 때 자동으로 사용됩니다.

- 숫자 형식의 매개 변수가 없는 `ToString` 메서드

- 서식 문자열을 인수로 포함하는, 숫자 형식의 `ToString(String)` 메서드

- 숫자 값에 사용되는 경우, [복합 서식 지정](../../../docs/standard/base-types/composite-formatting.md) 기능

다음 예제는 프랑스 파일의 월별 평균 온도를 나타냅니다. 우선 데이터를 표시하기 전에 현재 문화권을 프랑스어(프랑스)로 설정하고 그 다음 영어(미국)로 설정합니다. 각각의 경우, 월 이름 및 온도가 해당 문화권에 적합한 서식으로 표시됩니다. 두 문화권을 온도 값에 다른 소수 구분 기호를 사용합니다. 또한, 월 이름 전체를 표시하기 위해 "MMMM" 사용자 지정 날짜 및 시간 서식 문자열이 예제에 사용되었고, 이를 통해 <xref:System.Globalization.DateTimeFormatInfo.MonthNames%2A?displayProperty=nameWithType> 배열에서 가장 긴 월 이름의 길이를 판단하여 결과 문자열에 월 이름을 나타내기에 적합한 공간이 할당됩니다.

[!code-csharp[Conceptual.Globalization#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/numbers1.cs#5)]
[!code-vb[Conceptual.Globalization#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/numbers1.vb#5)]

### <a name="persist-numeric-values"></a>숫자 값 유지

숫자 데이터를 문화권별 서식으로 유지하지 말아야 합니다. 이것은 일반적인 프로그래밍 오류이며, 손상된 데이터 또는 런타임 예외를 발생시킵니다. 다음 예제는 10개의 부동 소수점 난수를 생성한 다음 영어(미국) 문화권의 서식 규칙을 사용하여 문자열로 serialize합니다. 영어(미국) 문화권의 형식을 사용하여 데이터를 가져와서 구문을 분석하면, 성공적으로 복원됩니다. 하지만, 이것을 가져와서 프랑스어(프랑스) 문화권 규칙을 사용하여 구문 분석을 수행하면, 이 문화권에서 다른 소수 구분 기호를 사용하기 때문에 숫자를 구문 분석할 수 없습니다.

[!code-csharp[Conceptual.Globalization#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/numbers2.cs#6)]
[!code-vb[Conceptual.Globalization#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/numbers2.vb#6)]

이 문제를 피하려면, 다음 방법 중 하나를 사용합니다.

- 사용자의 문화권과 상관없이 동일한 사용자 지정 서식 문자열을 사용하여 숫자의 문자열 표현을 저장하고 구문 분석합니다.

- <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 속성에 의해 반환되는 고정 문화권의 서식 규칙을 사용하여 숫자를 문자열로 저장합니다.

- 숫자를 이진 형식이 아닌 문자열 형식으로 serialize합니다.

다음 예제에서 마지막 방법을 보여 줍니다. <xref:System.Double> 값의 배열을 serialize한 다음 deserialize하고 영어(미국) 및 프랑스어(프랑스) 문화권의 서식 규칙을 사용하여 나타냅니다.

[!code-csharp[Conceptual.Globalization#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/numbers3.cs#7)]
[!code-vb[Conceptual.Globalization#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/numbers3.vb#7)]

통화 값 serialize는 특별한 경우입니다. 통화 값은 값이 표현되는 통화의 단위에 따라 달라지므로, 이것을 독립적인 숫자 값으로 처리하는 것은 합당하지 않습니다. 하지만, 통화 값을 통화 기호를 포함하는 서식이 지정된 문자열로 저장하면, 다음 예제에서 볼 수 있듯이, 다른 통화 기호를 사용하는 기본 문화권의 시스템에서 deserialize될 수 없습니다.

[!code-csharp[Conceptual.Globalization#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/currency1.cs#16)]
[!code-vb[Conceptual.Globalization#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/currency1.vb#16)]

대신, 값과 그에 대한 통화 기호가 현재 문화권과 관계 없이 deserialize될 수 있도록, 숫자 값을 문화권 정보(예: 문화권의 이름)와 함께 serialize해야 합니다. 다음 예제에서는 두 가지 멤버 즉, <xref:System.Decimal> 값과 그 값이 속하는 문화권의 이름으로 `CurrencyValue` 구조를 정의하여 이것을 구현합니다.

[!code-csharp[Conceptual.Globalization#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.globalization/cs/currency2.cs#17)]
[!code-vb[Conceptual.Globalization#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.globalization/vb/currency2.vb#17)]

## <a name="work-with-culture-specific-settings"></a>문화권별 설정 작업

.NET에서 <xref:System.Globalization.CultureInfo> 클래스는 특정 문화권 또는 국가를 나타냅니다. 이들 속성 중 일부는 문화의 일부 측면에 대한 구체적인 정보를 제공하는 개체를 반환합니다.

- <xref:System.Globalization.CultureInfo.CompareInfo%2A?displayProperty=nameWithType> 속성은 문화권에서 문자열을 비교하고 정렬하는 방법에 대한 정보를 포함하는 <xref:System.Globalization.CompareInfo> 개체를 반환합니다.

- <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=nameWithType> 속성은 날짜 및 시간 데이터의 서식 지정에 사용되는 문화권별 정보를 제공하는 <xref:System.Globalization.DateTimeFormatInfo> 개체를 반환합니다.

- <xref:System.Globalization.CultureInfo.NumberFormat%2A?displayProperty=nameWithType> 속성은 숫자 데이터의 서식 지정에 사용되는 문화권별 정보를 제공하는 <xref:System.Globalization.NumberFormatInfo> 개체를 반환합니다.

- <xref:System.Globalization.CultureInfo.TextInfo%2A?displayProperty=nameWithType> 속성은 문화권의 쓰기 시스템에 대한 정보를 제공하는 <xref:System.Globalization.TextInfo> 개체를 반환합니다.

일반적으로 특정한 <xref:System.Globalization.CultureInfo> 속성의 값 및 그와 관련된 개체에 대한 가정을 하지 말아야 합니다. 대신, 문화권별 데이터를 변경의 대상으로 봐야 합니다. 그 이유는 다음과 같습니다.

- 개별적인 속성 값은 데이터가 수정되거나, 더 나은 데이터를 사용할 수 있게 되거나, 문화권별 규칙이 변경되면서, 시간이 지남에 따라 변경 및 개정될 수 있습니다.

- 개별적인 속성 값은 .NET 버전 또는 운영 체제 버전에 따라 달라질 수 있습니다.

- .NET은 대체 문화권을 지원합니다. 이 때문에 기존의 표준 문화권을 보완하거나 완전히 대체하는 새로운 사용자 지정 문화권을 정의하는 것이 가능합니다.

- Windows 시스템에서 사용자는 제어판의 **국가 및 언어** 앱을 사용하여 문화권별 설정을 사용자 지정할 수 있습니다. <xref:System.Globalization.CultureInfo> 개체를 인스턴스화할 때, <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=nameWithType> 생성자를 호출하여 사용자 지정을 반영할지 여부를 결정할 수 있습니다. 일반적으로 최종 사용자 앱에 대해서는 사용자가 예상하는 서식으로 사용자에게 데이터가 표시되도록 사용자 기본 설정을 고려해야 합니다.

## <a name="see-also"></a>참고 항목

- [전역화 및 지역화](../../../docs/standard/globalization-localization/index.md)
- [문자열 사용에 대한 모범 사례](../../../docs/standard/base-types/best-practices-strings.md)
