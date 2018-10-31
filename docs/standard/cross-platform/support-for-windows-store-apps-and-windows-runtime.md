---
title: Windows 스토어 앱 및 Windows 런타임에 대한 .NET Framework 지원
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- Windows Store apps, .NET Framework support for
- Windows Runtime, .NET Framework support for
- .NET for Windows Store apps
- .NET Framework, and Windows Store apps
- .NET Framework, and Windows Runtime
ms.assetid: 6fa7d044-ae12-4c54-b8ee-50915607a565
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 0476fe7ed731dbb2c6b86cff3255673ecee6f98d
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50198460"
---
# <a name="net-framework-support-for-windows-store-apps-and-windows-runtime"></a>Windows 스토어 앱 및 Windows 런타임에 대한 .NET Framework 지원
[!INCLUDE[net_v45](../../../includes/net-v45-md.md)]는 [!INCLUDE[wrt](../../../includes/wrt-md.md)]와 함께 다양한 소프트웨어 개발 시나리오를 지원합니다. 이러한 시나리오는 다음 세 가지 범주로 구분됩니다.

-   개발 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 에 설명 된 대로 XAML 컨트롤을 사용 하 여 앱 [Windows 스토어 앱 용 로드맵 C# 또는 Visual Basic을 사용 하 여](https://docs.microsoft.com/previous-versions/windows/apps/br229583(v=win.10)), [하는 방법 (XAML) tos](https://docs.microsoft.com/previous-versions/windows/apps/br229566(v=win.10)), 및 [.NET Windows 스토어 용 앱 개요 ](https://msdn.microsoft.com/library/windows/apps/br230302%28v=VS.110%29.aspx).

-   .NET Framework로 만든 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램에서 사용할 클래스 라이브러리 개발.

-   [!INCLUDE[wrt](../../../includes/wrt-md.md)]를 지원하는 모든 프로그래밍 언어에서 사용할 수 있는 .WinMD 파일에서 패키지된 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소 개발. 예를 들어, 참조 [Creating Windows Runtime Components in C# 및 Visual Basic](/windows/uwp/winrt-components/creating-windows-runtime-components-in-csharp-and-visual-basic)합니다.

 이 항목에서는 .NET Framework에서 모든 세 가지 범주에 대해 제공하는 지원을 간략하게 설명하고 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소에 대한 시나리오를 설명합니다. 첫 번째 섹션에서는 .NET Framework와 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 사이의 관계에 대한 기본 정보가 포함되어 있으며 도움말 시스템 및 IDE에서 발생할 수 있는 일부 의문 사항을 설명합니다. 합니다 [섹션을 두 번째](#WindowsRuntimeComponents) 개발 하기 위한 시나리오에 설명 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소입니다.

## <a name="the-basics"></a>기본 사항
 .NET Framework는 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]을 제공하고 [!INCLUDE[wrt](../../../includes/wrt-md.md)]를 자체 지원하여 앞부분에서 설명한 세 가지 개발 시나리오를 지원합니다.

-   [Windows 스토어 앱 용.NET](https://msdn.microsoft.com/library/windows/apps/br230232(v=vs.110).aspx) .NET Framework 클래스 라이브러리의 간결한 뷰를 제공 하 고는 형식 및 멤버를 만드는 데 사용할 수 있습니다 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱 및 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소입니다.

    -   Visual Studio (Visual Studio 2012 이상 버전) 개발에 사용 하는 경우는 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱 또는 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소 참조 어셈블리 집합으로 관련 형식 및 멤버만 표시 되도록 합니다.

    -   이 간소화된 API 집합은 .NET Framework 내에서 복제되었거나 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 기능을 복제하는 기능을 제거하여 더욱 단순화되었습니다. 예를 들어, 컬렉션 형식의 제네릭 버전만 포함하고, XML 문서 개체 모델은 [!INCLUDE[wrt](../../../includes/wrt-md.md)] XML API 집합을 위해 제거됩니다.

    -   [!INCLUDE[wrt](../../../includes/wrt-md.md)]를 관리 코드에서 쉽게 호출할 수 있기 때문에 단순히 운영 체제 API를 래핑하는 기능 또한 제거됩니다.

     에 대 한 자세한 합니다 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]를 참조 합니다 [.NET Windows 스토어 용 앱 개요](https://msdn.microsoft.com/library/windows/apps/br230302(v=VS.110).aspx). API 선택 프로세스에 대 한 자세한 내용은 참조는 [Metro 스타일 앱 용.NET](https://blogs.msdn.microsoft.com/dotnet/2012/04/17/net-for-metro-style-apps/) .NET 블로그의 항목입니다.

-   [Windows 런타임](/uwp/api/) 건물에 대 한 사용자 인터페이스 요소를 제공 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램, 운영 체제 기능에 대 한 액세스를 제공 합니다. .NET Framework와 같이 [!INCLUDE[wrt](../../../includes/wrt-md.md)]에 있는 메타데이터를 사용하여 C# 및 Visual Basic 컴파일러를 통해 .NET Framework 클래스 라이브러리를 사용하는 방식과 같이 [!INCLUDE[wrt](../../../includes/wrt-md.md)]를 사용할 수 있습니다. .NET Framework에서는 다음과 같이 일부 차이점을 숨겨 [!INCLUDE[wrt](../../../includes/wrt-md.md)]를 좀 더 쉽게 사용할 수 있습니다.

    -   .NET Framework 및 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 사이의 프로그래밍 패턴(예: 이벤트 처리기를 추가 및 제거하기 위한 패턴)의 일부 차이점이 숨겨져 있습니다. .NET Framework 패턴을 그대로 사용하면 됩니다.

    -   자주 사용되는 형식(예: 기본 형식 및 컬렉션)의 일부 차이점이 숨겨져 있습니다. 에 설명 된 대로 단순히.NET Framework 형식에 사용할 [차이점 표시 되는 IDE에서](#DifferencesVisibleInIDE)이 문서의 뒷부분에 나오는.

 대부분의 경우 [!INCLUDE[wrt](../../../includes/wrt-md.md)]에 대한 .NET Framework 지원이 명백합니다. 다음 섹션에서는 관리 코드와 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 사이의 일부 명백한 차이점을 설명합니다.

<a name="AboutReferenceDocumentation"></a>
### <a name="the-net-framework-and-the-includewrtincludeswrt-mdmd-reference-documentation"></a>.NET Framework 및 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 참조 설명서
 Windows 런타임 및.NET Framework 설명서 집합 구분 됩니다. 형식이나 멤버에 도움말을 표시하기 위해 F1 키를 누르면, 적절한 집합의 참조 설명서가 표시됩니다. 그러나 탐색할 경우 합니다 [Windows 런타임 참조](/uwp/api/) 같이 난해해 보이는 예제를 발생할 수 있습니다.

-   와 같은 항목을 <xref:Windows.Foundation.Collections.IIterable%601> 인터페이스는 Visual Basic 또는 C# 용 선언 구문이 없는 합니다. 구문 섹션 위에 메모가 표시 하는 대신 (이 경우 ".NET:이 인터페이스 System.Collections.Generic.IEnumerable 요소로\<T >"). 이는 .NET Framework와 [!INCLUDE[wrt](../../../includes/wrt-md.md)]가 서로 다른 인터페이스로 비슷한 기능을 제공하기 때문입니다. 게다가 동작의 차이점도 있습니다. 예를 들면 `IIterable`은 `First` 메서드 대신에 <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 메서드를 사용하여 열거자를 반환합니다. 일반적인 작업을 수행하는 다른 방법을 배우도록 강요하는 대신, .NET Framework는 관리 코드가 익숙한 형식을 사용하는 것처럼 보이게 하여 [!INCLUDE[wrt](../../../includes/wrt-md.md)]를 지원합니다. IDE에서 `IIterable` 인터페이스를 볼 수 없으므로 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 참조 문서에서 확인할 수 있는 유일한 방법은 해당 문서를 직접 살펴보는 것입니다.

-   <xref:Windows.Web.Syndication.SyndicationFeed.%23ctor(System.String,System.String,Windows.Foundation.Uri)> 설명서는 밀접 하 게 관련 된 문제를 보여 줍니다: 해당 매개 변수 형식이 언어 마다 다를 수 표시 합니다. C# 및 Visual Basic의 경우 매개 변수 형식은 <xref:System.String?displayProperty=nameWithType> 및 <xref:System.Uri?displayProperty=nameWithType>입니다. 즉, .NET Framework에 자체 `String` 및 `Uri` 형식이 있고, 이같이 자주 사용되는 형식에 대해 다른 작업 방식을 배우도록 .NET Framework 사용자를 강요하는 것이 적합하지 않기 때문입니다. IDE에서 .NET Framework는 해당 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 형식을 숨깁니다.

-   몇 가지 경우에 같은 <xref:Windows.UI.Xaml.GridLength> 구조를.NET Framework 이름은 같지만 더 많은 기능을 사용 하 여 형식을 제공 합니다. 예를 들어, 생성자 및 속성 항목 집합은 `GridLength`와 연관되어 있지만, 멤버를 관리 코드에서만 사용할 수 있기 때문에 Visual Basic 및 C#용 구문 블록만 있습니다. [!INCLUDE[wrt](../../../includes/wrt-md.md)]에서 구조체는 필드만 가지고 있습니다. 합니다 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구조체에 도우미 클래스인 필요 <xref:Windows.UI.Xaml.GridLengthHelper>, 해당 기능을 제공 합니다. 관리 코드를 작성할 때 IDE에서 도우미 클래스를 볼 수 없습니다.

-   IDE에서 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 형식은 <xref:System.Object?displayProperty=nameWithType>에서 파생되어 나타납니다. <xref:System.Object>과 같은 <xref:System.Object.ToString%2A?displayProperty=nameWithType>에서 상속된 멤버를 가진 것으로 나타납니다. 이러한 멤버는 형식이 실제로 <xref:System.Object>에서 상속된 것처럼 작동하고, [!INCLUDE[wrt](../../../includes/wrt-md.md)] 형식을 <xref:System.Object>로 캐스팅할 수 있습니다. 이 기능은 [!INCLUDE[wrt](../../../includes/wrt-md.md)]에 대해 .NET Framework가 제공하는 지원의 일부입니다. 그러나 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 참조 문서에서 형식을 볼 경우 이러한 멤버는 표시되지 않습니다. 이 상속된 명백한 멤버에 대한 문서는 <xref:System.Object?displayProperty=nameWithType> 참조 문서에서 제공합니다.

<a name="DifferencesVisibleInIDE"></a>
### <a name="differences-that-are-visible-in-the-ide"></a>IDE에서 표시되는 차이점
 더 많은 고급 프로그래밍 시나리오(예: JavaScript를 사용하여 Windows용으로 빌드된 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 앱에 대해 응용 프로그램 논리를 제공하는 데 C#에서 작성된 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 구성 요소 사용)에서 이러한 차이점은 IDE와 문서 모두에서 명백합니다. 구성 요소가 `IDictionary<int, string>`을 JavaScript로 반환하고 이를 JavaScript 디버거에서 살펴보면, JavaScript가 `IMap<int, string>` 형식을 사용하므로 [!INCLUDE[wrt](../../../includes/wrt-md.md)]의 메서드를 볼 수 있습니다. 두 언어에서 다르게 나타나는 일반적으로 사용되는 컬렉션 형식의 일부는 다음 표에 표시됩니다.

|[!INCLUDE[wrt](../../../includes/wrt-md.md)] 형식|해당 .NET Framework 형식|
|--------------------------------------------------------------|---------------------------------------|
|`IIterable<T>`|`IEnumerable<T>`|
|`IIterator<T>`|`IEnumerator<T>`|
|`IVector<T>`|`IList<T>`|
|`IVectorView<T>`|`IReadOnlyList<T>`|
|`IMap<K, V>`|`IDictionary<TKey, TValue>`|
|`IMapView<K, V>`|`IReadOnlyDictionary<TKey, TValue>`|
|`IBindableIterable`|`IEnumerable`|
|`IBindableVector`|`IList`|
|`Windows.UI.Xaml.Data.INotifyPropertyChanged`|`System.ComponentModel.INotifyPropertyChanged`|
|`Windows.UI.Xaml.Data.PropertyChangedEventHandler`|`System.ComponentModel.PropertyChangedEventHandler`|
|`Windows.UI.Xaml.Data.PropertyChangedEventArgs`|`System.ComponentModel.PropertyChangedEventArgs`|

 [!INCLUDE[wrt](../../../includes/wrt-md.md)]에서 `IMap<K, V>` 및 `IMapView<K, V>`는 `IKeyValuePair`를 사용하며 반복됩니다. 관리 코드에 전달되면 이들은 `IDictionary<TKey, TValue>` 및 `IReadOnlyDictionary<TKey, TValue>`로 표시되므로 당연히 `System.Collections.Generic.KeyValuePair<TKey, TValue>`를 사용하여 열거해야 합니다.

 인터페이스가 관리 코드에 표시되는 방식은 이러한 인터페이스를 구현하는 형식이 표시되는 방식에 영향을 미칩니다. 예를 들어 `PropertySet` 클래스는 관리되는 코드에 `IDictionary<TKey, TValue>`로 나타나는 `IMap<K, V>`를 구현합니다. `PropertySet`에서 `IMap<K, V>` 대신 `IDictionary<TKey, TValue>`가 구현된 것으로 나타나므로 관리되는 코드에서는 .NET Framework 사전의 `Add` 메서드처럼 동작하는 `Add` 메서드가 있는 것으로 나타납니다. 이 클래스는 `Insert` 메서드를 가지고 있는 것으로 보이지 않습니다.

 만들려면.NET Framework를 사용 하는 방법에 대 한 자세한 내용은 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소 및 JavaScript를 사용 하 여 이러한 구성 요소를 사용 하는 방법을 보여 주는 연습 [Creating Windows Runtime Components in C# 및 Visual Basic](/windows/uwp/winrt-components/creating-windows-runtime-components-in-csharp-and-visual-basic)합니다.

### <a name="primitive-types"></a>기본 형식
 관리 코드에서 [!INCLUDE[wrt](../../../includes/wrt-md.md)]를 자연스럽게 사용할 수 있도록 코드에서 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 기본 형식 대신 .NET Framework 기본 형식이 나타납니다. .NET Framework에서 `Int32` 구조체와 같은 기본 형식은 많은 유용한 속성 및 메서드(예: `Int32.TryParse` 메서드)를 갖고 있습니다. 반면에 [!INCLUDE[wrt](../../../includes/wrt-md.md)]의 기본 형식과 구조체에는 필드만 포함되어 있습니다. 관리 코드에서 기본 형식을 사용할 때 .NET Framework 형식으로 표시되고, 평소와 같이 .NET Framework 형식의 속성 및 메서드를 사용할 수 있습니다. 다음 목록은 요약을 제공합니다.

-   [!INCLUDE[wrt](../../../includes/wrt-md.md)] 기본 형식인 `Int32`, `Int64`, `Single`, `Double`, `Boolean`, `String`(변경할 수 없는 유니코드 문자 컬렉션), `Enum`, `UInt32`, `UInt64` 및 `Guid`의 경우 `System` 네임스페이스에 있는 동일한 이름의 형식을 사용합니다.

-   `UInt8`에 대해 `System.Byte`를 사용합니다.

-   `Char16`에 대해 `System.Char`를 사용합니다.

-   `IInspectable` 인터페이스에 대해 `System.Object`를 사용합니다.

-   `HRESULT`에 대해 하나의 `System.Int32` 멤버가 있는 구조체를 사용합니다.

 인터페이스 형식에서처럼, .NET Framework 프로젝트가 JavaScript를 사용하여 빌드된 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 앱에서 사용하는 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 구성 요소일 때에만 이 표현의 증거를 볼 수 있습니다.

 관리 코드에 해당 .NET Framework 형식으로 표시되는 일반적으로 사용되는 다른 기본 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 형식에는 `Windows.Foundation.DateTime` 구조체(관리 코드에 <xref:System.DateTimeOffset?displayProperty=nameWithType> 구조체로 표시됨) 및 `Windows.Foundation.TimeSpan` 구조체(<xref:System.TimeSpan?displayProperty=nameWithType> 구조체로 표시됨)가 포함됩니다.

### <a name="other-differences"></a>기타 차이점
 일부의 경우 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 형식 대신 .NET Framework 형식이 코드에 나타나는 사실로 보아 사용자가 수행해야 할 작업이 있습니다. 예를 들어 합니다 <xref:Windows.Foundation.Uri?displayProperty=nameWithType> 으로 표시 되는 클래스 <xref:System.Uri?displayProperty=nameWithType> .NET Framework 코드에서. <xref:System.Uri?displayProperty=nameWithType> 상대 URI를 사용할 수 있지만 <xref:Windows.Foundation.Uri?displayProperty=nameWithType> 는 절대 URI가 필요 합니다. 따라서 URI를 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 메서드로 전달할 때 URI가 절대적인지 확인해야 합니다. (참조 [Windows 런타임에 URI 전달](../../../docs/standard/cross-platform/passing-a-uri-to-the-windows-runtime.md).)

<a name="WindowsRuntimeComponents"></a>
## <a name="scenarios-for-developing-windows-runtime-components"></a>Windows 런타임 구성 요소를 개발하기 위한 시나리오
 관리 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소에 대해 지원되는 시나리오는 다음 일반 원칙에 따라 다릅니다.

-   .NET Framework를 사용하여 빌드된 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소는 다른 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 라이브러리와 명백한 차이점이 없습니다. 예를 들어 관리 코드를 사용하여 네이티브 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소를 다시 구현하는 경우, 두 구성 요소는 외부적으로 구별할 수 없습니다. 코드 그 자체가 관리 코드이더라도 구성 요소가 관리 코드로 작성되었다는 사실은 그것을 사용하는 코드에 표시되지 않습니다. 그러나 내부적으로 구성 요소는 실제 관리 코드이며 CLR(공용 언어 런타임)에서 실행됩니다.

-   구성 요소는 응용 프로그램 논리, [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] UI 컨트롤 또는 둘 모두를 구현하는 형식을 포함할 수 있습니다.

    > [!NOTE]
    >  UI 요소를 응용 프로그램 논리에서 분리하는 것이 좋습니다. 또한 JavaScript 및 HTML을 사용하여 Windows용으로 빌드된 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱에서 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] UI 컨트롤을 사용할 수 없습니다.

-   구성 요소는 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱을 위한 Visual Studio 솔루션 내의 프로젝트이거나 여러 솔루션에 추가할 수 있는 재사용 가능한 구성 요소일 수 있습니다.

    > [!NOTE]
    >  구성 요소가 C# 또는 Visual Basic에서만 사용될 경우 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소로 만들 필요가 없습니다. 대신 일반적인 .NET Framework 클래스 라이브러리로 만들 경우 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 형식에 대해 공용 API 화면을 제한할 필요가 없습니다.

-   사용 하 여 다양 한 재사용 가능한 구성 요소를 해제할 수 있습니다 합니다 [!INCLUDE[wrt](../../../includes/wrt-md.md)] <xref:Windows.Foundation.Metadata.VersionAttribute> 형식 (및 형식 내 멤버)를 식별 하기 위한 특성 서로 다른 버전에 추가 되었습니다.

-   구성 요소의 형식은 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 형식에서 파생될 수 있습니다. 컨트롤의 기본 컨트롤 형식에서 파생 될 수 있습니다 합니다 <xref:Windows.UI.Xaml.Controls.Primitives> 네임 스페이스 또는 좀 더 완료 된 컨트롤 같은 <xref:Windows.UI.Xaml.Controls.Button>합니다.

    > [!IMPORTANT]
    >  [!INCLUDE[win8](../../../includes/win8-md.md)] 및 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]부터 관리 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소의 모든 공용 형식은 봉인되어야 합니다. 여기서 다른 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소의 형식은 파생될 수 없습니다. 구성 요소에서 다형 동작을 제공하려면 인터페이스를 만들어 다형 형식에서 구현할 수 있습니다.

-   구성 요소에서 공용 형식에 대한 모든 매개 변수 및 반환 형식은 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 형식(구성 요소가 정의하는 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 형식 포함)이어야 합니다.

 다음 섹션에서는 일반적인 시나리오의 예제를 제공합니다.

### <a name="application-logic-for-a-includewin8appnamelongincludeswin8-appname-long-mdmd-app-with-javascript"></a>JavaScript을 사용한 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱에 대한 응용 프로그램 논리
 JavaScript를 사용하여 Windows용으로 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱을 개발할 때 관리 코드에서 응용 프로그램 논리의 일부가 더 잘 수행되거나 개발하기 더 쉬울 수도 있습니다. JavaScript는 .NET Framework 클래스 라이브러리를 직접 사용할 수 없지만, 이 클래스 라이브러리를 .WinMD 파일로 만들 수 있습니다. 이 시나리오에서 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소는 앱의 핵심 부분이므로 버전 특성을 제공하는 것은 바람직하지 않습니다.

### <a name="reusable-includewin8appnamelongincludeswin8-appname-long-mdmd-ui-controls"></a>다시 사용 가능한 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] UI 컨트롤
 관련된 UI 컨트롤 집합을 재사용 가능한 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소에 패키지할 수 있습니다. 구성 요소는 직접 시장에 출시하거나 사용자가 만든 앱의 요소로서 사용할 수 있습니다. 이 시나리오에서 사용 하는 것이 있도록를 [!INCLUDE[wrt](../../../includes/wrt-md.md)] <xref:Windows.Foundation.Metadata.VersionAttribute> 호환성을 개선 하기 위해 특성입니다.

### <a name="reusable-application-logic-from-existing-net-framework-apps"></a>기존 .NET Framework 앱의 재사용 가능한 응용 프로그램 논리
 관리 코드를 기존 데스크톱 앱에서 독립 실행형 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소로 패키지할 수 있습니다. 따라서 C++ 또는 JavaScript를 사용하여 빌드한 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱 및 C# 또는 Visual Basic을 사용하여 빌드한 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱 모두에서 구성 요소를 사용할 수 있습니다. 코드를 재사용하는 시나리오가 여러 개일 경우 버전 관리는 옵션입니다.

## <a name="related-topics"></a>관련 항목

|제목|설명|
|-----------|-----------------|
|[Windows 스토어 앱용 .NET 개요](https://msdn.microsoft.com/library/windows/apps/br230302(v=VS.110).aspx)|[!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱 및 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소를 만드는 데 사용할 수 있는 .NET Framework 형식 및 멤버를 설명합니다. (Windows 개발자 센터)|
|[C# 또는 Visual Basic을 사용 하 여 Windows 스토어 앱 용 로드맵](https://docs.microsoft.com/previous-versions/windows/apps/br229583(v=win.10))|C# 또는 Visual Basic을 사용하여 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱을 개발하기 시작할 때 도움을 주기 위해 다양한 퀵 스타트 항목, 지침 및 모범 사례를 포함한 주요 리소스를 제공합니다. (Windows 개발자 센터)|
|[방법 tos (XAML)](https://docs.microsoft.com/previous-versions/windows/apps/br229566(v=win.10))|C# 또는 Visual Basic을 사용하여 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱을 개발하기 시작할 때 도움을 주기 위해 다양한 퀵 스타트 항목, 지침 및 모범 사례를 포함한 주요 리소스를 제공합니다. (Windows 개발자 센터)|
|[C# 및 Visual Basic으로 Windows 런타임 구성 요소 만들기](/windows/uwp/winrt-components/creating-windows-runtime-components-in-csharp-and-visual-basic)|.NET Framework를 사용하여 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 구성 요소를 만드는 방법, JavaScript를 사용하여 Windows용으로 빌드한 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱의 일부로 사용하는 방법 및 Visual Studio로 조합을 디버깅하는 방법을 설명합니다. (Windows 개발자 센터)|
|[Windows 런타임 참조](/uwp/api/)|[!INCLUDE[wrt](../../../includes/wrt-md.md)]에 대한 참조 문서입니다. (Windows 개발자 센터)|
|[Windows 런타임에 URI 전달](../../../docs/standard/cross-platform/passing-a-uri-to-the-windows-runtime.md)|관리 코드에서 URI를 [!INCLUDE[wrt](../../../includes/wrt-md.md)]로 전달할 때 발생할 수 있는 문제 및 이러한 문제를 방지하는 방법을 설명합니다.|
