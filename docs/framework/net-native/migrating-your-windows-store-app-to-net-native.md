---
title: Windows 스토어 앱을 .NET 네이티브로 마이그레이션
ms.date: 03/30/2017
ms.assetid: 4153aa18-6f56-4a0a-865b-d3da743a1d05
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: fdff7aa92e4c1c357c83b625a6daadbf0a8d556b
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049510"
---
# <a name="migrating-your-windows-store-app-to-net-native"></a>Windows 스토어 앱을 .NET 네이티브로 마이그레이션

.NET 네이티브는 Windows 스토어 또는 개발자 컴퓨터에서 앱을 정적으로 컴파일하는 기능을 제공 합니다. 이 기능은 디바이스의 [네이티브 이미지 생성기(Ngen.exe)](../tools/ngen-exe-native-image-generator.md) 또는 JIT(Just-In-Time) 컴파일러가 Windows 스토어 앱에 대해 수행하는 동적 컴파일과는 다릅니다. 차이점에도 불구 하 고 .NET 네이티브는 [Windows 스토어 앱 용 .net과의](https://docs.microsoft.com/previous-versions/windows/apps/br230302%28v=vs.140%29)호환성을 유지 하려고 합니다. 대부분의 경우 Windows 스토어 앱 용 .NET에서 작동 하는 작업은 .NET 네이티브 에서도 작동 합니다.  그러나 동작이 변경되는 경우도 있습니다. 이 문서에서는 다음과 같은 영역에서 Windows 스토어 앱 용 표준 .NET과 .NET 네이티브 간의 이러한 차이점에 대해 설명 합니다.

- [일반 런타임 차이점](#Runtime)

- [동적 프로그래밍 차이점](#Dynamic)

- [기타 리플렉션 관련 차이점](#Reflection)

- [지원되지 않는 시나리오 및 API](#Unsupported)

- [Visual Studio의 차이점](#VS)

<a name="Runtime"></a>

## <a name="general-runtime-differences"></a>일반 런타임 차이점

- 앱이 CLR ( <xref:System.TypeLoadException>공용 언어 런타임)에서 실행 될 때 JIT 컴파일러에서 throw 되는와 같은 예외는 일반적으로 .NET 네이티브에서 처리 될 때 컴파일 시간 오류가 발생 합니다.

- 앱 UI 스레드에서 <xref:System.GC.WaitForPendingFinalizers%2A?displayProperty=nameWithType> 메서드를 호출해서는 안 됩니다. 이로 인해 .NET 네이티브에 교착 상태가 발생할 수 있습니다.

- 정적 클래스 생성자 호출 순서를 따라서는 안 됩니다. .NET 네이티브 호출 순서는 표준 런타임의 순서와 다릅니다. 표준 런타임을 사용하는 경우에도 정적 클래스 생성자 실행 순서를 따라서는 안 됩니다.

- 스레드에서 호출을 하지 않고 무한 루프(예: `while(true);`)를 사용하면 앱이 중지될 수 있습니다. 마찬가지로 대기 시간이 길어지거나 무한히 계속되어도 앱이 중지될 수 있습니다.

- 특정 제네릭 초기화 주기는 .NET 네이티브에서 예외를 throw 하지 않습니다. 예를 들어 다음 코드는 표준 CLR에서는 <xref:System.TypeLoadException> 예외를 throw하지만 .NET 네이티브는 그렇지 않습니다.

  [!code-csharp[ProjectN#8](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat1.cs#8)]

- 경우에 따라 .NET 네이티브는 .NET Framework 클래스 라이브러리의 다른 구현을 제공 합니다. 메서드에서 반환된 개체는 항상 반환된 형식의 멤버를 구현합니다. 그러나 지원 구현이 다르므로 기타 .NET Framework 플랫폼에서와 같이 해당 개체를 동일한 형식 집합으로 캐스팅하지 못할 수도 있습니다. 예를 들어 <xref:System.Collections.Generic.IEnumerable%601> , <xref:System.Reflection.TypeInfo.DeclaredMembers%2A?displayProperty=nameWithType> 등의 메서드가 반환한 <xref:System.Reflection.TypeInfo.DeclaredProperties%2A?displayProperty=nameWithType> 인터페이스 개체는 `T[]`로 캐스팅할 수 없습니다.

- WinInet 캐시는 Windows 스토어 앱 용 .NET에서는 기본적으로 사용 하도록 설정 되어 있지 않지만 .NET 네이티브에 있습니다. 이로 인해 성능은 향상되지만 작업 집합이 영향을 받습니다. 개발자가 작업을 수행할 필요는 없습니다.

<a name="Dynamic"></a>

## <a name="dynamic-programming-differences"></a>동적 프로그래밍 차이점

.NET Framework 코드의 정적 링크를 .NET 네이티브 하 여 최대 성능을 위해 코드를 로컬 코드로 만듭니다. 그러나 이진 크기를 작게 유지해야 하므로 전체 .NET Framework의 코드를 가져올 수는 없습니다. .NET 네이티브 컴파일러는 사용 되지 않는 코드에 대 한 참조를 제거 하는 종속성 리 듀 서을 사용 하 여이 제한을 해결 합니다. 그러나 컴파일 타임에 정적으로 정보를 유추할 수 없지만 런타임에 동적으로 검색 하는 경우에는 .NET 네이티브에서 일부 형식 정보와 코드를 유지 관리 하거나 생성할 수 없습니다.

.NET 네이티브은 리플렉션 및 동적 프로그래밍을 사용 하도록 설정 합니다. 그러나 이로 인해 생성되는 코드 크기가 너무 커지며 특히 .NET Framework에서는 공용 API에 대한 리플렉션이 지원되지 않기 때문에 일부 형식만 리플렉션하도록 표시할 수 있습니다. .NET 네이티브 컴파일러는 리플렉션을 지원 해야 하는 형식을 현명 하 게 선택 하 고 메타 데이터를 유지 하 고 해당 형식에 대 한 코드만 생성 합니다.

예를 들어 데이터 바인딩을 사용하려면 앱이 속성 이름을 함수에 매핑할 수 있어야 합니다. Windows 스토어 앱용 .NET에서는 공용 언어 런타임이 리플렉션을 자동으로 사용하여 관리되는 형식 및 공개적으로 사용 가능한 네이티브 형식에 대해 이 기능을 제공합니다. .NET 네이티브에서 컴파일러는 데이터를 바인딩할 형식에 대 한 메타 데이터를 자동으로 포함 합니다.

.NET 네이티브 컴파일러는 힌트 또는 지시문을 요구 하지 않고 작동 하 <xref:System.Collections.Generic.List%601> 는 <xref:System.Collections.Generic.Dictionary%602>및와 같은 일반적으로 사용 되는 제네릭 형식을 처리할 수도 있습니다. [동적](../../csharp/language-reference/keywords/dynamic.md) 키워드도 일정한 제한 내에서 지원됩니다.

> [!NOTE]
> 앱을 .NET 네이티브로 이식할 때 모든 동적 코드 경로를 철저 하 게 테스트 해야 합니다.

.NET 네이티브에 대 한 기본 구성은 대부분의 개발자에 게 충분 하지만, 일부 개발자는 런타임 지시문 (system.xml) 파일을 사용 하 여 구성을 미세 조정할 수 있습니다. 또한 경우에 따라 .NET 네이티브 컴파일러는 리플렉션에 사용할 수 있어야 하는 메타 데이터를 확인할 수 없으며, 특히 다음과 같은 경우에 힌트를 사용 해야 합니다.

- <xref:System.Type.MakeGenericType%2A?displayProperty=nameWithType> , <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A?displayProperty=nameWithType> 등의 일부 구문은 정적으로 확인할 수 없습니다.

- 컴파일러는 인스턴스화를 확인할 수 없으므로 런타임 지시문을 사용하여 리플렉션을 수행하려는 제네릭 형식을 지정해야 합니다. 이는 단순히 모든 코드를 포함해야 하기 때문이 아니라, 제네릭 형식에 대해 리플렉션을 수행하면 무한 주기가 생성될 수 있기 때문입니다(예: 제네릭 형식에 대해 제네릭 메서드를 호출하는 경우).

> [!NOTE]
> 런타임 지시문은 런타임 지시문(.rd.xml) 파일에서 정의합니다. 이 파일의 사용 방법에 대한 일반 정보는 [시작](getting-started-with-net-native.md)을 참조하세요. 런타임 지시문에 대한 자세한 내용은 [Runtime Directives (rd.xml) Configuration File Reference](runtime-directives-rd-xml-configuration-file-reference.md)를 참조하세요.

또한 .NET 네이티브에는 개발자가 기본 집합 외부에서 리플렉션을 지원 해야 하는 형식을 결정 하는 데 도움이 되는 프로 파일링 도구도 포함 되어 있습니다.

<a name="Reflection"></a>

## <a name="other-reflection-related-differences"></a>기타 리플렉션 관련 차이점

Windows 스토어 앱 용 .NET과 .NET 네이티브 간의 동작에는 다양 한 개별 리플렉션 관련 차이점이 있습니다.

.NET 네이티브:

- .NET Framework 클래스 라이브러리의 형식 및 멤버에 대한 개인 리플렉션은 지원되지 않습니다. 그러나 고유한 개인 형식과 멤버 및 타사 라이브러리의 형식과 멤버에 대해서는 리플렉션을 수행할 수 있습니다.

- <xref:System.Reflection.ParameterInfo.HasDefaultValue%2A?displayProperty=nameWithType> 속성은 반환 값을 나타내는 `false` 개체에 대해 <xref:System.Reflection.ParameterInfo>를 올바르게 반환합니다. 그러나 Windows 스토어 앱용 .NET에서는 `true`가 반환됩니다. IL(중간 언어)은 이러한 반환을 직접 지원하지 않으며 해석은 언어에 따라 달라집니다.

- <xref:System.RuntimeFieldHandle> 및 <xref:System.RuntimeMethodHandle> 구조체에서는 public 멤버를 사용할 수 없습니다. 이러한 형식은 LINQ, 식 트리 및 정적 배열 초기화에서만 지원됩니다.

- <xref:System.Reflection.RuntimeReflectionExtensions.GetRuntimeProperties%2A?displayProperty=nameWithType> 및 <xref:System.Reflection.RuntimeReflectionExtensions.GetRuntimeEvents%2A?displayProperty=nameWithType> 의 기본 클래스는 숨겨진 멤버를 포함하므로 명시적으로 재정의하지 않아도 재정의될 수 있습니다. 이는 다른 [RuntimeReflectionExtensions.GetRuntime*](xref:System.Reflection.RuntimeReflectionExtensions) 메서드에서도 마찬가지입니다.

- byref 배열과 같은 특정 조합을 만들 때<xref:System.Type.MakeArrayType%2A?displayProperty=nameWithType> 및 <xref:System.Type.MakeByRefType%2A?displayProperty=nameWithType> 에서 오류가 발생하지 않습니다.

- 리플렉션을 사용하여 포인터 매개 변수가 있는 멤버를 호출할 수는 없습니다.

- 리플렉션을 사용하여 포인터 필드를 가져오거나 설정할 수는 없습니다.

- 인수 개수가 잘못 되 고 인수 중 하나의 형식이 잘못 된 경우 .NET 네이티브는 <xref:System.ArgumentException> <xref:System.Reflection.TargetParameterCountException>대신을 throw 합니다.

- 예외의 이진 serialization은 일반적으로 지원되지 않습니다. 그러므로 serialize할 수 없는 개체를 <xref:System.Exception.Data%2A?displayProperty=nameWithType> 사전에 추가할 수 있습니다.

<a name="Unsupported"></a>

## <a name="unsupported-scenarios-and-apis"></a>지원되지 않는 시나리오 및 API

다음 섹션에서는 일반 개발, interop 및 HTTPClient, WCF(Windows Communication Foundation) 등의 기술에 대해 지원되지 않는 시나리오와 API에 대해 설명합니다.

- [일반 개발](#General)

- [HttpClient](#HttpClient)

- [Interop](#Interop)

- [지원되지 않는 API](#APIs)

<a name="General"></a>

### <a name="general-development-differences"></a>일반 개발 관련 차이점

**값 형식**

- 값 형식에 대해 <xref:System.ValueType.Equals%2A?displayProperty=nameWithType> 및 <xref:System.ValueType.GetHashCode%2A?displayProperty=nameWithType> 메서드를 재정의하는 경우 기본 클래스 구현을 호출하지 마세요. Windows 스토어 앱용 .NET에서 이러한 메서드는 리플렉션을 사용합니다. 컴파일 시간에 .NET 네이티브는 런타임 리플렉션을 사용 하지 않는 구현을 생성 합니다. 즉, 이러한 두 메서드를 재정의 하지 않으면 .NET 네이티브 컴파일 시간에 구현을 생성 하기 때문에 예상 대로 작동 합니다. 그러나 이러한 메서드를 재정의하고 기본 클래스 구현을 호출하면 예외가 발생합니다.

- 1MB보다 큰 값 형식은 지원되지 않습니다.

- 값 형식은 .NET 네이티브에서 매개 변수가 없는 생성자를 가질 수 없습니다. C# 및 Visual Basic 값 형식에 대해 매개 변수가 없는 생성자를 금지 합니다. IL에서는 기본 생성자를 만들 수 있습니다.

**배열**

- 하한이 0이 아닌 배열은 지원되지 않습니다. 이러한 배열은 대개 <xref:System.Array.CreateInstance%28System.Type%2CSystem.Int32%5B%5D%2CSystem.Int32%5B%5D%29?displayProperty=nameWithType> 오버로드를 호출하여 만듭니다.

- 동적으로 다차원 배열을 만들 수 없습니다. 이러한 배열은 대개 <xref:System.Array.CreateInstance%2A?displayProperty=nameWithType> 매개 변수를 포함하는 `lengths` 메서드의 오버로드 또는 <xref:System.Type.MakeArrayType%28System.Int32%29?displayProperty=nameWithType> 메서드를 호출하여 만듭니다.

- 차원이 4개 이상(해당 <xref:System.Array.Rank%2A?displayProperty=nameWithType> 속성 값이 4 이상)인 다차원 배열은 지원되지 않습니다. 이러한 경우에는 [가변 배열](../../csharp/programming-guide/arrays/jagged-arrays.md) (배열의 배열)을 대신 사용합니다. 예를 들어 `array[x,y,z]` 는 유효하지 않지만 `array[x][y][z]` 는 유효합니다.

- 다차원 배열에는 가변성(variance)이 지원되지 않으며, 가변성(variance)을 적용하는 경우 런타임에 <xref:System.InvalidCastException> 예외가 발생합니다.

**제네릭**

- 무한 제네릭 형식을 확장하면 컴파일러 오류가 발생합니다. 예를 들어 다음 코드는 컴파일되지 않습니다.

  [!code-csharp[ProjectN#9](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat2.cs#9)]

**포인터**

- 포인터 배열은 지원되지 않습니다.

- 리플렉션을 사용하여 포인터 필드를 가져오거나 설정할 수는 없습니다.

**serialization**

<xref:System.Runtime.Serialization.KnownTypeAttribute.%23ctor%28System.String%29> 특성은 지원되지 않습니다. 대신 <xref:System.Runtime.Serialization.KnownTypeAttribute.%23ctor%28System.Type%29> 특성을 사용하세요.

**리소스**

<xref:System.Diagnostics.Tracing.EventSource> 클래스에는 지역화된 리소스를 사용할 수 없습니다. <xref:System.Diagnostics.Tracing.EventSourceAttribute.LocalizationResources%2A?displayProperty=nameWithType> 속성은 지역화된 리소스를 정의하지 않습니다.

**대리자**

`Delegate.BeginInvoke` 및 `Delegate.EndInvoke` 는 지원되지 않습니다.

**기타 API**

- 특성이 형식에 <xref:System.PlatformNotSupportedException>적용 되지 않으면<xref:System.Runtime.InteropServices.GuidAttribute> [TypeInfo.GUID](xref:System.Type.GUID) 속성이 예외를 throw 합니다. GUID는 주로 COM 지원을 위해 사용됩니다.

- 메서드 <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> 는 .NET 네이티브에서 짧은 날짜를 포함 하는 문자열을 올바르게 구문 분석 합니다. 그러나 Microsoft 기술 자료 문서 [KB2803771](https://support.microsoft.com/kb/2803771) 및 [KB2803755](https://support.microsoft.com/kb/2803755)에서 설명하는 날짜 및 시간 구문 분석 변경 내용과의 호환성은 유지되지 않습니다.

- <xref:System.Numerics.BigInteger.ToString%2A?displayProperty=nameWithType>`("E")` .NET 네이티브에서 올바르게 반올림 됩니다. 일부 CLR 버전에서는 결과 문자열이 반올림되는 대신 잘립니다.

<a name="HttpClient"></a>

### <a name="httpclient-differences"></a>HttpClient의 차이점

.NET 네이티브에서 클래스는 <xref:System.Net.Http.HttpClientHandler> Windows 스토어 앱 용 표준 .net에서 <xref:Windows.Web.Http.Filters.HttpBaseProtocolFilter> 사용 되는 <xref:System.Net.WebRequest> 및 <xref:System.Net.WebResponse> 클래스 대신 클래스를 통해 내부적으로 WinINet을 사용 합니다.  WinINet은 <xref:System.Net.Http.HttpClientHandler> 클래스에서 지원하는 구성 옵션 중 일부만 지원합니다.  그 결과는 다음과 같습니다.

- 의 일부 기능 속성 <xref:System.Net.Http.HttpClientHandler> 은 .NET 네이티브에서 반환 `false` 하는 반면 Windows 스토어 `true` 앱 용 표준 .net에서는를 반환 합니다.

- 일부 구성 속성 `get` 접근자는 Windows 스토어 앱 용 .net의 기본 구성 가능한 값과 다른 .NET 네이티브의 고정 값을 항상 반환 합니다.

다음 하위 섹션에서 몇 가지 추가적인 동작 차이점에 대해 설명합니다.

**프록시**

클래스 <xref:Windows.Web.Http.Filters.HttpBaseProtocolFilter> 는 요청 별로 프록시 구성 또는 재정의를 지원 하지 않습니다.  즉, .NET 네이티브의 모든 요청은 <xref:System.Net.Http.HttpClientHandler.UseProxy%2A?displayProperty=nameWithType> 속성의 값에 따라 시스템에서 구성 된 프록시 서버를 사용 하거나 프록시 서버를 사용 하지 않습니다.  Windows 스토어 앱용 .NET에서는 <xref:System.Net.Http.HttpClientHandler.Proxy%2A?displayProperty=nameWithType> 속성을 통해 프록시 서버가 정의됩니다.  .NET 네이티브에서를 이외의 값 <xref:System.Net.Http.HttpClientHandler.Proxy%2A?displayProperty=nameWithType> `null` 으로 설정 하면 <xref:System.PlatformNotSupportedException> 예외가 throw 됩니다.  속성 <xref:System.Net.Http.HttpClientHandler.SupportsProxy%2A?displayProperty=nameWithType> 은 .NET 네이티브 `false` 에 대해를 반환 하는 `true` 반면 Windows 스토어 앱에 대 한 표준 .NET Framework을 반환 합니다.

**자동 리디렉션**

클래스 <xref:Windows.Web.Http.Filters.HttpBaseProtocolFilter> 는 최대 자동 리디렉션 수를 구성할 수 없습니다.  Windows 스토어 앱용 표준 .NET에서는 <xref:System.Net.Http.HttpClientHandler.MaxAutomaticRedirections%2A?displayProperty=nameWithType> 속성의 기본값이 50이며, 이 값은 수정 가능합니다. .NET 네이티브에서이 속성의 값은 10이 고 수정 하려고 하면 <xref:System.PlatformNotSupportedException> 예외가 throw 됩니다.  속성 <xref:System.Net.Http.HttpClientHandler.SupportsRedirectConfiguration%2A?displayProperty=nameWithType> 은 .NET 네이티브 `false` 에 대해를 반환 하는 `true` 반면 Windows 스토어 앱 용 .net에서는를 반환 합니다.

**자동 압축 풀기**

Windows 스토어 앱용 .NET에서는 <xref:System.Net.Http.HttpClientHandler.AutomaticDecompression%2A?displayProperty=nameWithType> 속성을 <xref:System.Net.DecompressionMethods.Deflate>또는 <xref:System.Net.DecompressionMethods.GZip>중 하나로 설정하거나, <xref:System.Net.DecompressionMethods.Deflate> 및 <xref:System.Net.DecompressionMethods.GZip>둘 다로 설정하거나, <xref:System.Net.DecompressionMethods.None>으로 설정할 수 있습니다.  .NET 네이티브는, <xref:System.Net.DecompressionMethods.Deflate> 또는 <xref:System.Net.DecompressionMethods.None>와 <xref:System.Net.DecompressionMethods.GZip>함께 지원 됩니다.  <xref:System.Net.Http.HttpClientHandler.AutomaticDecompression%2A> 속성을 <xref:System.Net.DecompressionMethods.Deflate> 또는 <xref:System.Net.DecompressionMethods.GZip> 중 하나만으로 설정하면 <xref:System.Net.DecompressionMethods.Deflate> 및 <xref:System.Net.DecompressionMethods.GZip>둘 다로 자동 설정됩니다.

**쿠키**

쿠키 처리는 <xref:System.Net.Http.HttpClient> 및 WinINet에서 동시에 수행됩니다.  <xref:System.Net.CookieContainer> 의 쿠키는 WinINet 쿠키 캐시의 쿠키와 결합됩니다.  <xref:System.Net.CookieContainer> 에서 쿠키를 제거하면 <xref:System.Net.Http.HttpClient> 가 쿠키를 보낼 수 없습니다. 그러나 WinINet에서 쿠키를 이미 확인했으며 사용자가 쿠키를 삭제하지 않은 경우에는 WinINet이 쿠키를 보냅니다.  <xref:System.Net.Http.HttpClient>, <xref:System.Net.Http.HttpClientHandler>또는 <xref:System.Net.CookieContainer> API를 사용하여 WinINet에서 프로그래밍 방식으로 쿠키를 제거할 수는 없습니다.  <xref:System.Net.Http.HttpClientHandler.UseCookies%2A?displayProperty=nameWithType> 속성을 `false` 로 설정하면 <xref:System.Net.Http.HttpClient> 만 쿠키 보내기를 중지하며 WinINet은 요청에 쿠키를 계속 포함할 수 있습니다.

**자격 증명**

Windows 스토어 앱용 .NET에서는 <xref:System.Net.Http.HttpClientHandler.UseDefaultCredentials%2A?displayProperty=nameWithType> 및 <xref:System.Net.Http.HttpClientHandler.Credentials%2A?displayProperty=nameWithType> 속성이 독립적으로 작동합니다.  또한 <xref:System.Net.Http.HttpClientHandler.Credentials%2A> 속성은 <xref:System.Net.ICredentials> 인터페이스를 구현하는 모든 개체를 수락합니다.  .NET 네이티브에서 <xref:System.Net.Http.HttpClientHandler.UseDefaultCredentials%2A> 속성을로 `true` <xref:System.Net.Http.HttpClientHandler.Credentials%2A> 설정 하면 속성이 `null`로 설정 됩니다.  또한 <xref:System.Net.Http.HttpClientHandler.Credentials%2A> 속성은 `null`, <xref:System.Net.CredentialCache.DefaultCredentials%2A>또는 <xref:System.Net.NetworkCredential>형식 개체로만 설정할 수 있습니다.  다른 <xref:System.Net.ICredentials> 개체(가장 널리 사용되는 항목은 <xref:System.Net.CredentialCache>)를 <xref:System.Net.Http.HttpClientHandler.Credentials%2A> 속성에 할당하면 <xref:System.PlatformNotSupportedException>이 throw됩니다.

**기타 지원되지 않거나 구성할 수 없는 기능**

.NET 네이티브:

- <xref:System.Net.Http.HttpClientHandler.ClientCertificateOptions%2A?displayProperty=nameWithType> 속성의 값은 항상 <xref:System.Net.Http.ClientCertificateOption.Automatic>입니다.  Windows 스토어 앱용 .NET에서는 기본값이 <xref:System.Net.Http.ClientCertificateOption.Manual>입니다.

- <xref:System.Net.Http.HttpClientHandler.MaxRequestContentBufferSize%2A?displayProperty=nameWithType> 속성은 구성할 수 없습니다.

- <xref:System.Net.Http.HttpClientHandler.PreAuthenticate%2A?displayProperty=nameWithType> 속성은 항상 `true`입니다.  Windows 스토어 앱용 .NET에서는 기본값이 `false`입니다.

- 응답의 `SetCookie2` 헤더는 사용되지 않는 항목으로 간주되어 무시됩니다.

<a name="Interop"></a>
### <a name="interop-differences"></a>interop 차이점
 **사용되지 않는 API**

 관리되는 코드와의 상호 운용성을 위해 제공되었던 사용 빈도가 낮은 여러 API가 더 이상 사용되지 않습니다. .NET 네이티브와 함께 사용 하는 경우 이러한 api는 <xref:System.NotImplementedException> 또는 <xref:System.PlatformNotSupportedException> 예외를 throw 하거나 컴파일러 오류가 발생할 수 있습니다. Windows 스토어 앱용 .NET에서는 이러한 API가 사용되지 않는 것으로 표시되지만 호출해도 컴파일러 오류가 아닌 컴파일러 경고가 생성됩니다.

 마샬링에 `VARIANT` 사용 되지 않는 api는 다음과 같습니다.

- <xref:System.Runtime.InteropServices.BStrWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.CurrencyWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.DispatchWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.ErrorWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.UnknownWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.VariantWrapper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.UnmanagedType.IDispatch?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.UnmanagedType.SafeArray?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.VarEnum?displayProperty=nameWithType>

 <xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=nameWithType> 가 지원되기는 하지만 [IDispatch](https://docs.microsoft.com/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) 또는 byref 변형에서 사용하는 경우와 같은 일부 시나리오에서는 예외가 발생됩니다.

 [IDispatch](https://docs.microsoft.com/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) 지원에 대해 사용 되지 않는 api는 다음과 같습니다.

- <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDispatch?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDual?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.ComDefaultInterfaceAttribute?displayProperty=nameWithType>

기존 COM 이벤트에 대해 사용 되지 않는 Api는 다음과 같습니다.

- <xref:System.Runtime.InteropServices.ComEventsHelper?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>

.NET 네이티브에서 지원 되지 <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=nameWithType> 않는 인터페이스에서 사용 되지 않는 api는 다음과 같습니다.

- <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=nameWithType>(모든 멤버)
- <xref:System.Runtime.InteropServices.CustomQueryInterfaceMode?displayProperty=nameWithType>(모든 멤버)
- <xref:System.Runtime.InteropServices.CustomQueryInterfaceResult?displayProperty=nameWithType>(모든 멤버)
- <xref:System.Runtime.InteropServices.Marshal.GetComInterfaceForObject%28System.Object%2CSystem.Type%2CSystem.Runtime.InteropServices.CustomQueryInterfaceMode%29?displayProperty=fullName>

기타 지원 되지 않는 interop 기능은 다음과 같습니다.

- <xref:System.Runtime.InteropServices.ICustomAdapter?displayProperty=nameWithType>(모든 멤버)
- <xref:System.Runtime.InteropServices.SafeBuffer?displayProperty=nameWithType>(모든 멤버)
- <xref:System.Runtime.InteropServices.UnmanagedType.Currency?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.UnmanagedType.VBByRefStr?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.UnmanagedType.AnsiBStr?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.UnmanagedType.AsAny?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.UnmanagedType.CustomMarshaler?displayProperty=fullName>

 거의 사용 되지 않는 마샬링 Api:

- <xref:System.Runtime.InteropServices.Marshal.ReadByte%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.ReadInt16%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.ReadInt32%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.ReadInt64%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.ReadIntPtr%28System.Object%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteByte%28System.Object%2CSystem.Int32%2CSystem.Byte%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteInt16%28System.Object%2CSystem.Int32%2CSystem.Int16%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteInt32%28System.Object%2CSystem.Int32%2CSystem.Int32%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteInt64%28System.Object%2CSystem.Int32%2CSystem.Int64%29?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.Marshal.WriteIntPtr%28System.Object%2CSystem.Int32%2CSystem.IntPtr%29?displayProperty=fullName>

 **플랫폼 호출 및 COM interop 호환성**

 대부분의 플랫폼 호출 및 COM interop 시나리오는 .NET 네이티브에서 계속 지원 됩니다. 특히 WinRT(Windows 런타임) API와의 모든 상호 운용성 및 Windows 런타임에 필요한 모든 마샬링은 지원됩니다. 여기에는 다음에 대한 마샬링 지원이 포함됩니다.

- 배열(<xref:System.Runtime.InteropServices.UnmanagedType.ByValArray?displayProperty=nameWithType> 포함)

- `BStr`

- 대리자

- 문자열(유니코드, ANSI 및 HSTRING)

- 구조체(`byref` 및 `byval`)

- Unions

- Win32 핸들

- 모든 WinRT 구문

- Variant 형식 마샬링에 대한 부분 지원. 지원되는 형식은 다음과 같습니다.

  - <xref:System.Boolean>

  - <xref:System.Byte>

  - <xref:System.Decimal>

  - <xref:System.Double>

  - <xref:System.Int16>

  - <xref:System.Int32>

  - <xref:System.Int64>

  - <xref:System.SByte>

  - <xref:System.Single>

  - <xref:System.UInt16>

  - <xref:System.UInt32>

  - <xref:System.UInt64>

  - `BStr`

  - [IUnknown](/windows/desktop/api/unknwn/nn-unknwn-iunknown)

그러나 .NET 네이티브는 다음을 지원 하지 않습니다.

- 기본 COM 이벤트 사용

- 관리되는 형식에서 <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=nameWithType> 인터페이스 구현

- [특성을 통해 관리되는 형식에서](https://docs.microsoft.com/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) IDispatch <xref:System.Runtime.InteropServices.ComDefaultInterfaceAttribute?displayProperty=nameWithType> 인터페이스 구현. 그러나 `IDispatch`를 통해 COM 개체를 호출할 수는 없으며 관리되는 개체는 `IDispatch`를 구현할 수 없습니다.

리플렉션을 사용하여 플랫폼 호출 메서드를 호출할 수는 없습니다. 대신 다른 메서드에서 메서드 호출을 래핑하고 리플렉션을 사용해 래퍼를 호출하여 이 제한을 해결할 수 있습니다.

<a name="APIs"></a>

### <a name="other-differences-from-net-apis-for-windows-store-apps"></a>Windows 스토어 앱용 .NET API의 기타 차이점

이 섹션에서는 .NET 네이티브에서 지원 되지 않는 나머지 Api를 나열 합니다. 지원되지 않는 API의 대부분은 WCF(Windows Communication Foundation) API입니다.

**DataAnnotations(System.ComponentModel.DataAnnotations)**

<xref:System.ComponentModel.DataAnnotations> 및<xref:System.ComponentModel.DataAnnotations.Schema> 네임 스페이스의 형식은 .NET 네이티브에서 지원 되지 않습니다. 여기에는 windows 8 용 Windows 스토어 앱 용 .NET에서 제공 되는 다음과 같은 형식이 포함 됩니다.

- <xref:System.ComponentModel.DataAnnotations.AssociationAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ConcurrencyCheckAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.CustomValidationAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DataType?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DataTypeAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DisplayAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DisplayColumnAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.DisplayFormatAttribute>
- <xref:System.ComponentModel.DataAnnotations.EditableAttribute>
- <xref:System.ComponentModel.DataAnnotations.EnumDataTypeAttribute>
- <xref:System.ComponentModel.DataAnnotations.FilterUIHintAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.KeyAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.RangeAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.RegularExpressionAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.RequiredAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.StringLengthAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.TimestampAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.UIHintAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationContext?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationException?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationResult?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.Validator?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedOption?displayProperty=nameWithType>

 **Visual Basic**

Visual Basic 현재 .NET 네이티브에서 지원 되지 않습니다. <xref:Microsoft.VisualBasic> 및<xref:Microsoft.VisualBasic.CompilerServices> 네임 스페이스의 다음 형식은 .NET 네이티브 사용할 수 없습니다.

- <xref:Microsoft.VisualBasic.CallType?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Constants?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.HideModuleNameAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Strings?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.Conversions?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.DesignerGeneratedAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.IncompleteInitialization?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.NewLateBinding?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.ObjectFlowControl?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.ObjectFlowControl.ForLoopControl?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.Operators?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.OptionCompareAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.OptionTextAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.ProjectData?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.StandardModuleAttribute?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.StaticLocalInitFlag?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.CompilerServices.Utils?displayProperty=nameWithType>

**리플렉션 컨텍스트(System.Reflection.Context 네임스페이스)**

클래스 <xref:System.Reflection.Context.CustomReflectionContext?displayProperty=nameWithType> 는 .NET 네이티브에서 지원 되지 않습니다.

**RTC(System.Net.Http.Rtc)**

클래스 `System.Net.Http.RtcRequestFactory` 는 .NET 네이티브에서 지원 되지 않습니다.

**Windows Communication Foundation (WCF) (System.ServiceModel.\*)**

[System.servicemodel. * 네임 스페이스](xref:System.ServiceModel) 의 형식은 .NET 네이티브 지원 되지 않습니다. 여기에는 다음과 같은 형식이 포함됩니다.

- <xref:System.ServiceModel.ActionNotSupportedException?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpBinding?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpMessageCredentialType?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpSecurity?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpSecurityMode?displayProperty=nameWithType>
- <xref:System.ServiceModel.CallbackBehaviorAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType>
- <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.BeginOperationDelegate?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.ChannelBase%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.EndOperationDelegate?displayProperty=nameWithType>
- <xref:System.ServiceModel.ClientBase%601.InvokeAsyncCompletedEventArgs?displayProperty=nameWithType>
- <xref:System.ServiceModel.CommunicationException?displayProperty=nameWithType>
- <xref:System.ServiceModel.CommunicationObjectAbortedException?displayProperty=nameWithType>
- <xref:System.ServiceModel.CommunicationObjectFaultedException?displayProperty=nameWithType>
- <xref:System.ServiceModel.CommunicationState?displayProperty=nameWithType>
- <xref:System.ServiceModel.DataContractFormatAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.DnsEndpointIdentity?displayProperty=nameWithType>
- <xref:System.ServiceModel.DuplexChannelFactory%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.DuplexClientBase%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.EndpointAddress?displayProperty=nameWithType>
- <xref:System.ServiceModel.EndpointAddressBuilder?displayProperty=nameWithType>
- <xref:System.ServiceModel.EndpointIdentity?displayProperty=nameWithType>
- <xref:System.ServiceModel.EndpointNotFoundException?displayProperty=nameWithType>
- <xref:System.ServiceModel.EnvelopeVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.ExceptionDetail?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultCode?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultException?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultReason?displayProperty=nameWithType>
- <xref:System.ServiceModel.FaultReasonText?displayProperty=nameWithType>
- <xref:System.ServiceModel.HttpBindingBase?displayProperty=nameWithType>
- <xref:System.ServiceModel.HttpClientCredentialType?displayProperty=nameWithType>
- <xref:System.ServiceModel.HttpTransportSecurity?displayProperty=nameWithType>
- <xref:System.ServiceModel.IClientChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.ICommunicationObject?displayProperty=nameWithType>
- <xref:System.ServiceModel.IContextChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.IDefaultCommunicationTimeouts?displayProperty=nameWithType>
- <xref:System.ServiceModel.IExtensibleObject%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.IExtension%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.IExtensionCollection%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.InstanceContext?displayProperty=nameWithType>
- <xref:System.ServiceModel.InvalidMessageContractException?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageBodyMemberAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageContractMemberAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageCredentialType?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageHeader%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageHeaderException?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageParameterAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageSecurityOverTcp?displayProperty=nameWithType>
- <xref:System.ServiceModel.MessageSecurityVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.NetHttpBinding?displayProperty=nameWithType>
- <xref:System.ServiceModel.NetHttpMessageEncoding?displayProperty=nameWithType>
- <xref:System.ServiceModel.NetTcpBinding?displayProperty=nameWithType>
- <xref:System.ServiceModel.NetTcpSecurity?displayProperty=nameWithType>
- <xref:System.ServiceModel.OperationContext?displayProperty=nameWithType>
- <xref:System.ServiceModel.OperationContextScope?displayProperty=nameWithType>
- <xref:System.ServiceModel.OperationContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.OperationFormatStyle?displayProperty=nameWithType>
- <xref:System.ServiceModel.ProtocolException?displayProperty=nameWithType>
- <xref:System.ServiceModel.QuotaExceededException?displayProperty=nameWithType>
- <xref:System.ServiceModel.SecurityMode?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServerTooBusyException?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServiceActivationException?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServiceContractAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.ServiceKnownTypeAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.SpnEndpointIdentity?displayProperty=nameWithType>
- <xref:System.ServiceModel.TcpClientCredentialType?displayProperty=nameWithType>
- <xref:System.ServiceModel.TcpTransportSecurity?displayProperty=nameWithType>
- <xref:System.ServiceModel.TransferMode?displayProperty=nameWithType>
- <xref:System.ServiceModel.UnknownMessageReceivedEventArgs?displayProperty=nameWithType>
- <xref:System.ServiceModel.UpnEndpointIdentity?displayProperty=nameWithType>
- <xref:System.ServiceModel.XmlSerializerFormatAttribute?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.AddressHeader?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.AddressHeaderCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.AddressingVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ChannelManagerBase?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ChannelParameterCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.CommunicationObject?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.CompressionFormat?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.FaultConverter?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.HttpRequestMessageProperty?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.HttpResponseMessageProperty?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.HttpsTransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.HttpTransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IChannelFactory?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IChannelFactory%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IDuplexChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IDuplexSession?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IDuplexSessionChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IHttpCookieContainerManager?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IInputChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IInputSession?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IInputSessionChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IMessageProperty?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IOutputChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IOutputSession?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IOutputSessionChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IRequestChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.IRequestSessionChannel?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ISession?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.ISessionChannel%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.LocalClientSecuritySettings?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.Message?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageBuffer?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageEncoder?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageEncoderFactory?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageEncodingBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageFault?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageHeader?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageHeaderInfo?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageHeaders?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageProperties?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageState?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.MessageVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.RequestContext?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.SecurityBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.SecurityHeaderLayout?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TcpConnectionPoolSettings?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TcpTransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TransportBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.TransportSecurityBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.WebSocketTransportSettings?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.WebSocketTransportUsage?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.ClientCredentials?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.ContractDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.FaultDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.FaultDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageBodyDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageDirection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageHeaderDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessageHeaderDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessagePartDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessagePartDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessagePropertyDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.MessagePropertyDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.OperationDescription?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.OperationDescriptionCollection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.ClientOperation?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.ClientRuntime?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.DispatchOperation?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.DispatchRuntime?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.EndpointDispatcher?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IClientOperationSelector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.BasicSecurityProfileVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.HttpDigestClientCredential?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.MessageSecurityException?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.SecureConversationVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.SecurityAccessDeniedException?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.SecurityPolicyVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.SecurityVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.TrustVersion?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.UserNamePasswordClientCredential?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.WindowsClientCredential?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.Tokens.SupportingTokenParameters?displayProperty=nameWithType>
- <xref:System.ServiceModel.Security.Tokens.UserNameSecurityTokenParameters?displayProperty=nameWithType>

### <a name="differences-in-serializers"></a>serializer의 차이점

<xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>및 <xref:System.Xml.Serialization.XmlSerializer> 클래스의 serialization 및 deserialization에는 다음과 같은 차이점이 있습니다.

- .NET 네이티브 <xref:System.Runtime.Serialization.DataContractSerializer> 에서 및 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 는 해당 형식이 루트 serialization 형식이 아닌 기본 클래스 멤버를 포함 하는 파생 클래스를 serialize 또는 deserialize 할 수 없습니다. 예를 들어 다음 코드에서 `Y` 를 serialize 또는 deserialize하려고 하면 오류가 발생합니다.

  [!code-csharp[ProjectN#10](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat3.cs#10)]

  기본 클래스의 멤버가 serialization 중에 트래버스되지 않으므로 serializer가 `InnerType` 형식을 인식하지 못합니다.

- <xref:System.Runtime.Serialization.DataContractSerializer> 및 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 가 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스를 구현하는 클래스나 구조체를 serialize하지 못합니다. 예를 들어 다음과 같은 형식은 serialize 또는 deserialize할 수 없습니다.

- <xref:System.Xml.Serialization.XmlSerializer> 가 다음 개체 값을 serialize하지 못합니다. serialize할 정확한 개체 형식을 알 수 없기 때문입니다.

- <xref:System.Xml.Serialization.XmlSerializer> 는 serialize된 개체의 형식이 <xref:System.Xml.XmlQualifiedName>이면 해당 개체를 serialize 또는 deserialize할 수 없습니다.

- 모든 serializer(<xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>및 <xref:System.Xml.Serialization.XmlSerializer>)는 <xref:System.Xml.Linq.XElement?displayProperty=nameWithType> 를 포함하는 형식 또는 <xref:System.Xml.Linq.XElement>형식에 대해 serialization 코드를 생성하지 못하며, 대신 빌드 시간 오류가 표시됩니다.

- serialization 형식의 다음 생성자에 대해서는 정상적인 작동이 보장되지 않습니다.

  - <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Runtime.Serialization.DataContractSerializerSettings%29?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.String%2CSystem.String%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Xml.XmlDictionaryString%2CSystem.Xml.XmlDictionaryString%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor%28System.Type%2CSystem.Runtime.Serialization.Json.DataContractJsonSerializerSettings%29?displayProperty=nameWithType>

  - <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor%28System.Type%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=nameWithType>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.String%29?displayProperty=nameWithType>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Type%5B%5D%29?displayProperty=nameWithType>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlAttributeOverrides%29?displayProperty=nameWithType>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlRootAttribute%29?displayProperty=nameWithType>

  - <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlAttributeOverrides%2CSystem.Type%5B%5D%2CSystem.Xml.Serialization.XmlRootAttribute%2CSystem.String%29?displayProperty=nameWithType>

- <xref:System.Xml.Serialization.XmlSerializer> 는 메서드에 다음 특성이 포함된 형식에 대해 코드를 생성하지 못합니다.

  - <xref:System.Runtime.Serialization.OnSerializingAttribute>

  - <xref:System.Runtime.Serialization.OnSerializedAttribute>

  - <xref:System.Runtime.Serialization.OnDeserializingAttribute>

  - <xref:System.Runtime.Serialization.OnDeserializedAttribute>

- <xref:System.Xml.Serialization.XmlSerializer> 는 <xref:System.Xml.Serialization.IXmlSerializable> 사용자 지정 serialization 인터페이스를 따르지 않습니다. 이 인터페이스를 구현하는 클래스가 있는 경우 <xref:System.Xml.Serialization.XmlSerializer> 는 해당 형식을 POCO(Plain Old CLR 개체) 형식으로 간주하여 public 속성만 serialize합니다.

- 일반 <xref:System.Exception> 개체 직렬화는 및 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>에서 <xref:System.Runtime.Serialization.DataContractSerializer> 잘 작동 하지 않습니다.

<a name="VS"></a>

## <a name="visual-studio-differences"></a>Visual Studio의 차이점

**예외 및 디버깅**

디버거에서 .NET 네이티브를 사용 하 여 컴파일된 응용 프로그램을 실행 하는 경우 다음 예외 형식에 대해 첫 번째 예외를 사용할 수 있습니다.

- <xref:System.MemberAccessException>

- <xref:System.TypeAccessException>

**앱 빌드**

Visual Studio에서 기본적으로 사용되는 x86 빌드 도구를 사용합니다. C:\Program Files (x86)\MSBuild\12.0\bin\amd64에 있는 AMD64 MSBuild 도구를 사용하는 경우 빌드 문제가 발생할 수 있으므로 사용하지 않는 것이 좋습니다.

**프로파일러**

- Visual Studio CPU 프로파일러 및 XAML 메모리 프로파일러에 내 코드만 옵션이 올바르게 표시되지 않습니다.

- XAML 메모리 프로파일러에 관리되는 힙 데이터가 정확하게 표시되지 않습니다.

- CPU 프로파일러가 모듈을 올바르게 식별하지 않으며 접두사가 붙은 함수 이름을 표시합니다.

**단위 테스트 라이브러리 프로젝트**

Windows 스토어 앱 프로젝트에 대 한 단위 테스트 라이브러리에서 .NET 네이티브를 사용 하도록 설정 하는 것은 지원 되지 않으며 프로젝트 빌드에 실패 합니다.

## <a name="see-also"></a>참고자료

- [시작](getting-started-with-net-native.md)
- [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)
- [Windows 스토어 앱 용 .NET 개요](https://docs.microsoft.com/previous-versions/windows/apps/br230302%28v=vs.140%29)
- [Windows 스토어 앱 및 Windows 런타임에 대한 .NET Framework 지원](../../standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)
