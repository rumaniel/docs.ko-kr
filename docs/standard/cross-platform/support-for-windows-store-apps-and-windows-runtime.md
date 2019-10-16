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
ms.openlocfilehash: 2f46d21123ecfda4bd336edbbd79fabf01e002a4
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71835335"
---
# <a name="net-framework-support-for-windows-store-apps-and-windows-runtime"></a>Windows 스토어 앱 및 Windows 런타임에 대한 .NET Framework 지원

.NET Framework 4.5는 Windows 런타임를 사용 하 여 다양 한 소프트웨어 개발 시나리오를 지원 합니다. 이러한 시나리오는 다음 세 가지 범주로 구분됩니다.

- [또는 Visual Basic를 사용 하 C# 는 windows 스토어 앱 용 로드맵](https://docs.microsoft.com/previous-versions/windows/apps/br229583(v=win.10)), how [To (xaml)](https://docs.microsoft.com/previous-versions/windows/apps/br229566(v=win.10))및 [windows 스토어 앱 용 .net 개요](https://docs.microsoft.com/previous-versions/windows/apps/br230302(v=vs.140))에 설명 된 대로 xaml 컨트롤을 사용 하 여 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱을 개발 합니다.

- .NET Framework로 만든 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램에서 사용할 클래스 라이브러리 개발.

- 에서 패키지 Windows 런타임 구성 요소를 개발 합니다. Windows 런타임를 지 원하는 모든 프로그래밍 언어에서 사용할 수 있는 WinMD 파일. 예를 들어 [및 Visual Basic에서 C# Windows 런타임 구성 요소 만들기](/windows/uwp/winrt-components/creating-windows-runtime-components-in-csharp-and-visual-basic)를 참조 하세요.

이 항목에서는 모든 세 가지 범주에 대해 .NET Framework에서 제공 하는 지원에 대해 간략하게 설명 하 고 Windows 런타임 구성 요소에 대 한 시나리오를 설명 합니다. 첫 번째 섹션에는 .NET Framework와 Windows 런타임 간의 관계에 대 한 기본 정보가 포함 되어 있으며 도움말 시스템과 IDE에서 발생할 수 있는 몇 가지 oddities 설명 합니다. [두 번째 섹션](#WindowsRuntimeComponents) 에서는 Windows 런타임 구성 요소를 개발 하는 시나리오에 대해 설명 합니다.

## <a name="the-basics"></a>기본 사항

.NET Framework는 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]을 제공 하 고 Windows 런타임 자체를 지원 하 여 앞에서 설명한 세 가지 개발 시나리오를 지원 합니다.

- [.NET Framework 및 Windows 런타임 네임 스페이스](https://docs.microsoft.com/previous-versions/windows/apps/br230302(v=vs.140)#net-framework-and-windows-runtime-namespaces) 는 .NET Framework 클래스 라이브러리를 간소화 된 뷰로 제공 하며 @no__t 1 앱 및 Windows 런타임 구성 요소를 만드는 데 사용할 수 있는 형식과 멤버만 포함 합니다.

  - Visual Studio (Visual Studio 2012 이상)를 사용 하 여 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱 또는 Windows 런타임 구성 요소를 개발 하는 경우 참조 어셈블리 집합은 관련 형식 및 멤버만 볼 수 있도록 합니다.

  - 이 간소화 된 API 집합은 .NET Framework 내에서 중복 되거나 Windows 런타임 기능이 중복 되는 기능을 제거 하 여 더욱 간소화 됩니다. 예를 들어, 컬렉션 형식의 제네릭 버전만 포함 하 고 XML 문서 개체 모델은 Windows 런타임 XML API 집합을 위해 제거 됩니다.

  - Windows 런타임는 관리 코드에서 쉽게 호출할 수 있으므로 단순히 운영 체제 API를 래핑하는 기능도 제거 됩니다.

  @No__t에 대 한 자세한 내용은 [Windows 스토어 앱 용 .net 개요](https://docs.microsoft.com/previous-versions/windows/apps/br230302(v=vs.140))를 참조 하세요. API 선택 프로세스에 대 한 자세한 내용은 .NET 블로그에서 [Metro 스타일 앱 용 .net](https://devblogs.microsoft.com/dotnet/net-for-metro-style-apps/) 항목을 참조 하세요.

- [Windows 런타임](/uwp/api/) 은 @no__t 1 앱을 빌드하기 위한 사용자 인터페이스 요소를 제공 하 고 운영 체제 기능에 대 한 액세스를 제공 합니다. .NET Framework와 마찬가지로 Windows 런타임에는 C# 및 Visual Basic 컴파일러가 .NET Framework 클래스 라이브러리를 사용 하는 방식으로 Windows 런타임를 사용할 수 있도록 하는 메타 데이터가 있습니다. .NET Framework를 사용 하면 몇 가지 차이점을 숨겨 Windows 런타임를 더 쉽게 사용할 수 있습니다.

  - 이벤트 처리기를 추가 및 제거 하는 패턴과 같은 .NET Framework와 Windows 런타임 간의 프로그래밍 패턴 차이는 숨겨집니다. .NET Framework 패턴을 그대로 사용하면 됩니다.

  - 자주 사용되는 형식(예: 기본 형식 및 컬렉션)의 일부 차이점이 숨겨져 있습니다. 이 문서의 뒷부분에 나오는 [IDE에 표시](#DifferencesVisibleInIDE)되는 차이점에 설명 된 대로 .NET Framework 형식을 사용 하기만 하면 됩니다.

대부분의 경우 Windows 런타임에 대 한 .NET Framework 지원은 투명 합니다. 다음 섹션에서는 관리 코드와 Windows 런타임의 몇 가지 명백한 차이점에 대해 설명 합니다.

<a name="AboutReferenceDocumentation"></a>

### <a name="the-net-framework-and-the-windows-runtime-reference-documentation"></a>.NET Framework 및 Windows 런타임 참조 설명서

Windows 런타임 및 .NET Framework 설명서 집합은 별도입니다. 형식이나 멤버에 도움말을 표시하기 위해 F1 키를 누르면, 적절한 집합의 참조 설명서가 표시됩니다. 그러나 [Windows 런타임 참조](/uwp/api/) 를 탐색 하는 경우에는 난해해 보이는 예제가 발생할 수 있습니다.

- @No__t-0 인터페이스와 같은 항목에는 Visual Basic 또는 C#에 대 한 선언 구문이 없습니다. 대신 구문 섹션 위에 노트가 표시 됩니다 (이 경우 ".NET: 이 인터페이스는 no__t-0T > ")로 표시 됩니다. .NET Framework 및 Windows 런타임는 다른 인터페이스와 유사한 기능을 제공 하기 때문입니다. 게다가 동작의 차이점도 있습니다. 예를 들면 `IIterable`은 `First` 메서드 대신에 <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 메서드를 사용하여 열거자를 반환합니다. 일반적인 작업을 수행 하는 다른 방법을 배울 수 있도록 하는 대신, .NET Framework는 사용자가 익숙한 형식을 사용 하기 위해 관리 코드를 표시 하 여 Windows 런타임를 지원 합니다. IDE에 `IIterable` 인터페이스가 표시 되지 않으므로 Windows 런타임 참조 설명서에서 해당 설명서를 직접 탐색 하는 방법에 대해서만 설명 합니다.

- @No__t-0 설명서는 밀접 하 게 관련 된 문제를 보여 줍니다. 해당 매개 변수 형식이 언어 마다 다르게 표시 됩니다. C# 및 Visual Basic의 경우 매개 변수 형식은 <xref:System.String?displayProperty=nameWithType> 및 <xref:System.Uri?displayProperty=nameWithType>입니다. 즉, .NET Framework에 자체 `String` 및 `Uri` 형식이 있고, 이같이 자주 사용되는 형식에 대해 다른 작업 방식을 배우도록 .NET Framework 사용자를 강요하는 것이 적합하지 않기 때문입니다. IDE에서 .NET Framework 해당 하는 Windows 런타임 형식을 숨깁니다.

- @No__t-0 구조와 같은 일부 경우에는 .NET Framework에서 이름이 같지만 기능이 더 많은 형식을 제공 합니다. 예를 들어, 생성자 및 속성 항목 집합은 `GridLength`와 연관되어 있지만, 멤버를 관리 코드에서만 사용할 수 있기 때문에 Visual Basic 및 C#용 구문 블록만 있습니다. Windows 런타임 구조에는 필드만 있습니다. Windows 런타임 구조체에는 동일한 기능을 제공 하기 위해-0 @no__t 도우미 클래스가 필요 합니다. 관리 코드를 작성할 때 IDE에서 도우미 클래스를 볼 수 없습니다.

- IDE에서는 Windows 런타임 형식이 <xref:System.Object?displayProperty=nameWithType>에서 파생 된 것으로 나타납니다. <xref:System.Object>과 같은 <xref:System.Object.ToString%2A?displayProperty=nameWithType>에서 상속된 멤버를 가진 것으로 나타납니다. 이러한 멤버는 <xref:System.Object>에서 실제로 상속 된 형식 및 Windows 런타임 형식을 <xref:System.Object>로 캐스팅할 수 있는 경우 처럼 작동 합니다. 이 기능은 .NET Framework에서 Windows 런타임에 대해 제공 하는 지원의 일부입니다. 그러나 Windows 런타임 참조 설명서에서 형식을 보면 해당 멤버가 표시 되지 않습니다. 이 상속된 명백한 멤버에 대한 문서는 <xref:System.Object?displayProperty=nameWithType> 참조 문서에서 제공합니다.

<a name="DifferencesVisibleInIDE"></a>

### <a name="differences-that-are-visible-in-the-ide"></a>IDE에서 표시되는 차이점

JavaScript를 사용 하 여 Windows 용으로 빌드된 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱에 C# 대 한 응용 프로그램 논리를 제공 하기 위해에서 작성 된 Windows 런타임 구성 요소를 사용 하는 등의 고급 프로그래밍 시나리오에서는 IDE와 설명서에서 이러한 차이가 명확해 집니다. 구성 요소가 javascript에 대 한 `IDictionary<int, string>`을 반환 하 고 javascript 디버거에서이를 확인 하는 경우 JavaScript는 Windows 런타임 형식을 사용 하기 때문에 `IMap<int, string>`의 메서드를 볼 수 있습니다. 두 언어에서 다르게 나타나는 일반적으로 사용되는 컬렉션 형식의 일부는 다음 표에 표시됩니다.

|Windows 런타임 형식|해당 .NET Framework 형식|
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

Windows 런타임에서 `IMap<K, V>` 및 `IMapView<K, V>`은 `IKeyValuePair`를 사용 하 여 반복 됩니다. 관리 코드에 전달되면 이들은 `IDictionary<TKey, TValue>` 및 `IReadOnlyDictionary<TKey, TValue>`로 표시되므로 당연히 `System.Collections.Generic.KeyValuePair<TKey, TValue>`를 사용하여 열거해야 합니다.

인터페이스가 관리 코드에 나타나는 방법은 이러한 인터페이스를 구현한 형식이 나타나는 방법에 영향을 줍니다. 예를 들어 `PropertySet` 클래스는 관리되는 코드에 `IDictionary<TKey, TValue>`로 나타나는 `IMap<K, V>`를 구현합니다. `PropertySet`에서 `IMap<K, V>` 대신 `IDictionary<TKey, TValue>`가 구현된 것으로 나타나므로 관리되는 코드에서는 .NET Framework 사전의 `Add` 메서드처럼 동작하는 `Add` 메서드가 있는 것으로 나타납니다. 이 클래스는 `Insert` 메서드를 가지고 있는 것으로 보이지 않습니다.

.NET Framework를 사용 하 여 Windows 런타임 구성 요소를 만드는 방법 및 JavaScript와 함께 이러한 구성 요소를 사용 하는 방법을 보여 주는 연습은 [및 Visual Basic에서 C# Windows 런타임 구성 요소 만들기](/windows/uwp/winrt-components/creating-windows-runtime-components-in-csharp-and-visual-basic)를 참조 하세요.

### <a name="primitive-types"></a>기본 형식

관리 코드에서 Windows 런타임를 자연스럽 게 사용할 수 있도록 하기 위해 코드에 기본 형식 Windows 런타임 대신 .NET Framework 기본 형식이 표시 됩니다. .NET Framework에서 `Int32` 구조체와 같은 기본 형식에는 `Int32.TryParse` 메서드 등 유용한 속성 및 메서드가 많이 포함되어 있습니다. 이와 대조적으로 Windows 런타임의 기본 형식과 구조체에는 필드만 있습니다. 관리 코드에서 기본 형식을 사용할 때 .NET Framework 형식으로 표시되고, 평소와 같이 .NET Framework 형식의 속성 및 메서드를 사용할 수 있습니다. 다음 목록은 요약을 제공합니다.

- Windows 런타임 기본 형식 `Int32`, `Int64`, `Single`, `Double`, `Boolean`, `String` (유니코드 문자의 변경할 수 없는 컬렉션), `Enum`, `UInt32`, `UInt64` 및 `Guid`의 경우 0 네임 스페이스에 있는 동일한 이름의 형식을 사용 합니다.

- `UInt8`에 대해 `System.Byte`를 사용합니다.

- `Char16`에 대해 `System.Char`를 사용합니다.

- `IInspectable` 인터페이스에 대해 `System.Object`를 사용합니다.

- `HRESULT`에 대해 하나의 `System.Int32` 멤버가 있는 구조체를 사용합니다.

인터페이스 형식과 마찬가지로, .NET Framework 프로젝트가 JavaScript를 사용 하 여 빌드된 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱에서 사용 하는 Windows 런타임 구성 요소인 경우에만이 표현의 증거가 표시 될 수 있습니다.

관리 코드에 해당 하는 것으로 표시 되는 다른 기본, 일반적으로 사용 되는 Windows 런타임 형식 .NET Framework으로는 관리 코드에 <xref:System.DateTimeOffset?displayProperty=nameWithType> 구조로 표시 되는 `Windows.Foundation.DateTime` 구조와 <xref:System.TimeSpan?displayProperty=nameWithType>으로 표시 되는 `Windows.Foundation.TimeSpan` 구조가 있습니다. 구조체나.

### <a name="other-differences"></a>기타 차이점

일부 경우에는 Windows 런타임 형식 대신 .NET Framework 형식이 코드에 표시 되기 때문에 사용자가 작업을 수행 해야 합니다. 예를 들어 <xref:Windows.Foundation.Uri?displayProperty=nameWithType> 클래스는 .NET Framework 코드에서 <xref:System.Uri?displayProperty=nameWithType>로 표시 됩니다. <xref:System.Uri?displayProperty=nameWithType>은 상대 URI를 허용 하지만 <xref:Windows.Foundation.Uri?displayProperty=nameWithType>에는 절대 URI가 필요 합니다. 따라서 Windows 런타임 메서드에 URI를 전달 하는 경우 절대 URI 인지 확인 해야 합니다. [Windows 런타임에 URI 전달을](../../../docs/standard/cross-platform/passing-a-uri-to-the-windows-runtime.md)참조 하세요.

<a name="WindowsRuntimeComponents"></a>

## <a name="scenarios-for-developing-windows-runtime-components"></a>Windows 런타임 구성 요소를 개발하기 위한 시나리오

관리 되는 Windows 런타임 구성 요소에 대해 지원 되는 시나리오는 다음과 같은 일반적인 원칙에 따라 다릅니다.

- .NET Framework를 사용 하 여 빌드된 Windows 런타임 구성 요소는 다른 Windows Runtimelibraries와 뚜렷한 차이점이 없습니다. 예를 들어 관리 코드를 사용 하 여 네이티브 Windows 런타임 구성 요소를 다시 구현 하는 경우 두 구성 요소는 outwardly 구분할 수 없습니다. 코드 그 자체가 관리 코드이더라도 구성 요소가 관리 코드로 작성되었다는 사실은 그것을 사용하는 코드에 표시되지 않습니다. 그러나 내부적으로 구성 요소는 실제 관리 코드이며 CLR(공용 언어 런타임)에서 실행됩니다.

- 구성 요소는 애플리케이션 논리, [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] UI 컨트롤 또는 둘 모두를 구현하는 형식을 포함할 수 있습니다.

  > [!NOTE]
  > UI 요소를 애플리케이션 논리에서 분리하는 것이 좋습니다. 또한 JavaScript 및 HTML을 사용하여 Windows용으로 빌드된 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱에서 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] UI 컨트롤을 사용할 수 없습니다.

- 구성 요소는 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱을 위한 Visual Studio 솔루션 내의 프로젝트이거나 여러 솔루션에 추가할 수 있는 재사용 가능한 구성 요소일 수 있습니다.

  > [!NOTE]
  > 구성 요소가 C# 또는 Visual Basic 에서만 사용 되는 경우에는 Windows 런타임 구성 요소로 만들 이유가 없습니다. 대신 일반 .NET Framework 클래스 라이브러리로 지정 하는 경우 공용 API 화면을 Windows 런타임 형식으로 제한할 필요가 없습니다.

- 여러 버전에 추가 된 형식 (및 형식 내 멤버)을 식별 하기 위해 Windows 런타임 <xref:Windows.Foundation.Metadata.VersionAttribute> 특성을 사용 하 여 다시 사용할 수 있는 구성 요소 버전을 해제할 수 있습니다.

- 구성 요소의 형식은 Windows 런타임 형식에서 파생 될 수 있습니다. 컨트롤은 <xref:Windows.UI.Xaml.Controls.Primitives> 네임 스페이스의 기본 컨트롤 형식이 나 <xref:Windows.UI.Xaml.Controls.Button>과 같은 완성 된 컨트롤에서 파생할 수 있습니다.

  > [!IMPORTANT]
  > @No__t-0 및 .NET Framework 4.5부터 관리 되는 Windows 런타임 구성 요소의 모든 public 형식이 sealed 여야 합니다. 다른 Windows 런타임 구성 요소의 형식은 해당 형식에서 파생 될 수 없습니다. 구성 요소에서 다형 동작을 제공하려면 인터페이스를 만들어 다형 형식에서 구현할 수 있습니다.

- 구성 요소의 공용 형식에 대 한 모든 매개 변수 및 반환 형식은 구성 요소에서 정의 하는 Windows 런타임 형식을 포함 하 여 Windows 런타임 형식 이어야 합니다.

다음 섹션에서는 일반적인 시나리오의 예제를 제공합니다.

### <a name="application-logic-for-a-includewin8_appname_longincludeswin8-appname-long-mdmd-app-with-javascript"></a>JavaScript을 사용한 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱에 대한 애플리케이션 논리

JavaScript를 사용하여 Windows용으로 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱을 개발할 때 관리 코드에서 애플리케이션 논리의 일부가 더 잘 수행되거나 개발하기 더 쉬울 수도 있습니다. JavaScript는 .NET Framework 클래스 라이브러리를 직접 사용할 수 없지만, 이 클래스 라이브러리를 .WinMD 파일로 만들 수 있습니다. 이 시나리오에서 Windows 런타임 구성 요소는 앱의 필수적인 부분 이므로 버전 특성을 제공 하는 것은 적합 하지 않습니다.

### <a name="reusable-includewin8_appname_longincludeswin8-appname-long-mdmd-ui-controls"></a>다시 사용 가능한 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] UI 컨트롤

재사용 가능한 Windows 런타임 구성 요소에서 관련 된 UI 컨트롤 집합을 패키지할 수 있습니다. 구성 요소는 직접 시장에 출시하거나 사용자가 만든 앱의 요소로서 사용할 수 있습니다. 이 시나리오에서는 Windows 런타임 <xref:Windows.Foundation.Metadata.VersionAttribute> 특성을 사용 하 여 호환성을 향상 시키는 것이 좋습니다.

### <a name="reusable-application-logic-from-existing-net-framework-apps"></a>기존 .NET Framework 앱의 재사용 가능한 애플리케이션 논리

기존 데스크톱 앱에서 관리 코드를 독립 실행형 Windows 런타임 구성 요소로 패키지할 수 있습니다. 따라서 C++ 또는 JavaScript를 사용하여 빌드한 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱 및 C# 또는 Visual Basic을 사용하여 빌드한 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱 모두에서 구성 요소를 사용할 수 있습니다. 코드를 재사용하는 시나리오가 여러 개일 경우 버전 관리는 옵션입니다.

## <a name="related-topics"></a>관련 항목

|제목|설명|
|-----------|-----------------|
|[Windows 스토어 앱용 .NET 개요](https://docs.microsoft.com/previous-versions/windows/apps/br230302(v=vs.140))|@No__t-0 앱 및 Windows RuntimeComponents을 만드는 데 사용할 수 있는 .NET Framework 형식 및 멤버에 대해 설명 합니다. (Windows 개발자 센터)|
|[또는 Visual Basic를 사용 하 C# 는 Windows 스토어 앱 용 로드맵](https://docs.microsoft.com/previous-versions/windows/apps/br229583(v=win.10))|C# 또는 Visual Basic을 사용하여 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱을 개발하기 시작할 때 도움을 주기 위해 다양한 퀵 스타트 항목, 지침 및 모범 사례를 포함한 주요 리소스를 제공합니다. (Windows 개발자 센터)|
|[방법 (XAML)](https://docs.microsoft.com/previous-versions/windows/apps/br229566(v=win.10))|C# 또는 Visual Basic을 사용하여 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱을 개발하기 시작할 때 도움을 주기 위해 다양한 퀵 스타트 항목, 지침 및 모범 사례를 포함한 주요 리소스를 제공합니다. (Windows 개발자 센터)|
|[C# 및 Visual Basic에서 Windows 런타임 구성 요소 만들기](/windows/uwp/winrt-components/creating-windows-runtime-components-in-csharp-and-visual-basic)|.NET Framework를 사용 하 여 Windows 런타임 구성 요소를 만드는 방법 및 JavaScript를 사용 하 여 Windows 용으로 빌드된 @no__t 0 앱의 일부로 사용 하는 방법을 설명 하 고 Visual Studio와의 조합을 디버그 하는 방법을 설명 합니다. (Windows 개발자 센터)|
|[Windows 런타임 참조](/uwp/api/)|Windows 런타임에 대 한 참조 설명서입니다. (Windows 개발자 센터)|
|[Windows 런타임에 URI 전달](../../../docs/standard/cross-platform/passing-a-uri-to-the-windows-runtime.md)|관리 코드에서 Windows 런타임 URI를 전달 하는 경우 발생할 수 있는 문제와이를 방지 하는 방법을 설명 합니다.|
