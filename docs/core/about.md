---
title: .NET Core 정보
description: .NET Core에 대한 자세히 알아봅니다.
ms.date: 09/17/2019
ms.openlocfilehash: 1baad9d6611a4c4340012b9a467d3499ad9ab834
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71181921"
---
# <a name="about-net-core"></a>.NET Core 정보

.NET Core에는 다음과 같은 특징이 있습니다.

- **플랫폼 간:** Windows, macOS 및 Linux [운영 체제](https://github.com/dotnet/core/blob/master/os-lifecycle-policy.md)에서 실행됩니다.
- **아키텍처 간에 일관됨:** x64, x86 및 ARM을 비롯한 여러 아키텍처에서 동일한 동작을 사용하여 코드를 실행합니다.
- **명령줄 도구:**  로컬 개발 및 연속 통합 시나리오에서 사용할 수 있는 편리한 명령줄 도구를 포함합니다.
- **유연한 배포:** 앱이나 설치된 side-by-side(사용자 또는 시스템 수준 설치)에 포함할 수 있습니다. [Docker 컨테이너](docker/index.md)에서 사용될 수 있습니다.
- **호환 가능:** .NET Core는 [.NET Standard](../standard/net-standard.md)를 통해 .NET Framework, Xamarin 및 Mono와 호환됩니다.
- **오픈 소스:** .NET Core 플랫폼은 MIT 및 Apache 2 라이선스를 사용하는 오픈 소스입니다. .NET Core는 [.NET Foundation](https://dotnetfoundation.org/) 프로젝트입니다.
- **Microsoft에서 지원됨:** .NET Core는 [.NET Core 지원](https://dotnet.microsoft.com/platform/support/policy)에 따라 Microsoft에서 지원됩니다.

## <a name="languages"></a>언어

C#, Visual Basic 및 F# 언어를 사용하여 .NET Core에 대한 애플리케이션 및 라이브러리를 작성할 수 있습니다. 이러한 언어는 즐겨 찾는 텍스트 편집기나 다음과 같은 IDE(통합 개발 환경)에서 사용할 수 있습니다.

- [Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)
- [Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)
- Sublime 텍스트
- Vim
 
[OmniSharp](https://www.omnisharp.net/) 및 [Ionide](http://ionide.io) 프로젝트의 참가자가 이 통합의 일부를 제공합니다.

## <a name="apis"></a>API

.NET Core는 다음과 같은 여러 시나리오에서 API를 노출합니다.

- [bool](../csharp/language-reference/keywords/bool.md) 및 [int](../csharp/language-reference/builtin-types/integral-numeric-types.md)와 같은 기본 형식
- <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> 및 <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType>과 같은 컬렉션
- <xref:System.Net.Http.HttpClient?displayProperty=nameWithType> 및 <xref:System.IO.FileStream?displayProperty=nameWithType>과 같은 유틸리티 형식
- <xref:System.Data.DataSet?displayProperty=nameWithType> 및 [DbSet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore/)과 같은 데이터 형식
- <xref:System.Numerics.Vector?displayProperty=nameWithType> 및 [Pipelines](https://devblogs.microsoft.com/dotnet/system-io-pipelines-high-performance-io-in-net/)와 같은 고성능 형식

.NET Core는 [.NET Standard](../standard/net-standard.md) 사양을 구현하여 .NET Framework 및 Mono API에서 호환성을 제공합니다.

## <a name="frameworks"></a>프레임워크

여러 프레임워크가 .NET Core를 기반으로 빌드되었습니다.

- [ASP.NET Core](/aspnet/core/)
- [Windows 10 UWP(유니버설 Windows 플랫폼)](https://developer.microsoft.com/windows)
- [Tizen](https://developer.tizen.org/development/training/.net-application)

## <a name="composition"></a>컴퍼지션

.NET Core는 다음과 같은 부분으로 구성됩니다.

- [.NET Core 런타임](https://github.com/dotnet/coreclr)은 형식 시스템, 어셈블리 로드, 가비지 수집기, 네이티브 interop, 기타 기본 서비스를 제공합니다. [.NET Core 프레임워크 라이브러리](https://github.com/dotnet/corefx)는 기본 데이터 형식, 앱 컴퍼지션 형식, 기본 유틸리티를 제공합니다.
- [ASP.NET 런타임](https://github.com/aspnet/home)은 웹앱, IoT 앱, 모바일 백 엔드 등의 최신 클라우드 기반 인터넷 연결 애플리케이션을 빌드하기 위한 프레임워크를 제공합니다.
- .NET Core 개발자 환경을 사용할 수 있도록 하는 [.NET Core CLI 도구](https://github.com/dotnet/cli) 및 언어 컴파일러([Roslyn](https://github.com/dotnet/roslyn) 및 [F#](https://github.com/microsoft/visualfsharp))입니다.
- [dotnet 도구](https://github.com/dotnet/core-setup)는 .NET Core 앱 및 CLI 도구를 시작하는 데 사용됩니다. 런타임을 선택 및 호스트하고, 어셈블리 로드 정책을 제공하며, 앱과 도구를 시작합니다.

이러한 구성 요소는 다음과 같은 방법으로 배포됩니다.

- [.NET Core 런타임](https://dotnet.microsoft.com/download) - .NET Core 런타임 및 프레임워크 라이브러리가 포함되어 있습니다.
- [ASP.NET Core 런타임](https://dotnet.microsoft.com/download) - ASP.NET Core 및 .NET Core 런타임 및 프레임워크 라이브러리가 포함되어 있습니다.
- [.NET Core SDK](https://dotnet.microsoft.com/download) - .NET CLI 도구, ASP.NET Core 런타임 및 .NET Core 런타임 및 프레임워크가 포함되어 있습니다.

### <a name="open-source"></a>소스 열기

[.NET Core](https://github.com/dotnet/core)는 오픈 소스([MIT 라이선스](https://github.com/dotnet/core/blob/master/LICENSE.TXT))이며 2014년 Microsoft에 의해 [.NET Foundation](https://dotnetfoundation.org)에 제공되었습니다. 현재 가장 많이 사용되는 .NET Foundation 프로젝트 중 하나입니다. 개인, 교육 또는 상업용으로 개인 및 회사에서 사용할 수 있습니다. 여러 회사에서 앱, 도구, 새 플랫폼, 호스팅 서비스의 일부로 .NET Core를 사용합니다. 이러한 회사 중 일부는 GitHub에서 .NET Core에 대한 중요한 정보를 제공하고 [.NET Foundation Technical Steering Group(.NET Foundation 기술 방향 설정 그룹)](https://dotnetfoundation.org/blog/tsg-welcome)의 일부로 제품 판매에 대한 지침을 제공합니다.

### <a name="designed-for-adaptability"></a>뛰어난 적응성

.NET Core는 다른 .NET 제품과 매우 유사하지만 고유한 제품으로 빌드되었습니다. 새 플랫폼과 워크로드에 광범위하게 적응되도록 설계되었으며, 사용 가능한 여러 OS 및 CPU 포트가 있고 더 많은 포트로 포팅될 수도 있습니다.

제품은 여러 조각으로 구분되어 다양한 시점에 다양한 부품을 새 플랫폼에 적용할 수 있습니다. 런타임 및 플랫폼별 기본 라이브러리는 하나의 단위로 이식해야 합니다. 플랫폼 제약 없는 라이브러리는 구성에 따라 모든 플랫폼에서 있는 그대로 작동합니다. 개발자 효율성을 높이기 위해 플랫폼별 구현을 줄이려는 프로젝트 성향이 있으므로, 가능한 경우 항상 플랫폼 중립 C# 코드를 사용하여 알고리즘이나 API를 전체 또는 부분적으로 구현합니다.

일반적으로 사용자는 여러 운영 체제를 지원하기 위해 .NET Core를 구현하는 방법을 질문합니다. 또한 별도의 구현이 있는지 또는 [조건부 컴파일](https://en.wikipedia.org/wiki/Conditional_compilation)이 사용되는지에 대해서도 질문합니다. 둘 다 조건부 컴파일에 대한 강력한 편견이 있습니다.

대부분의 [CoreFX](https://github.com/dotnet/corefx)가 모든 플랫폼에서 공유되는 플랫폼 중립 코드임을 다음 차트에서 확인할 수 있습니다. 플랫폼 중립 코드는 모든 플랫폼에서 사용할 수 있는 이식 가능한 단일 어셈블리로 구현할 수 있습니다.

![CoreFX: 플랫폼별 코드 줄](../images/corefx-platforms-loc.png)

Windows 및 Unix 구현은 크기가 비슷합니다. CoreFX에서 [Microsoft.Win32.Registry](https://github.com/dotnet/corefx/tree/master/src/Microsoft.Win32.Registry)와 같은 일부 Windows 전용 기능만 구현하고 Unix 전용 개념은 많이 구현하지 않으므로, Windows 구현이 더 큽니다. Linux 및 macOS 특정 구현은 크기가 거의 비슷하지만, 대부분의 Linux 및 macOS 구현이 Unix 구현에서 공유된다는 것도 확인할 수 있습니다.

.NET Core에는 플랫폼별 라이브러리와 플랫폼 중립 라이브러리가 혼합되어 있습니다. 몇 가지 예제에서 패턴을 확인할 수 있습니다.

- [CoreCLR](https://github.com/dotnet/coreclr)는 플랫폼별이며, 메모리 관리자 및 스레드 스케줄러와 같은 OS 하위 시스템을 기반으로 빌드합니다.
- 스토리지 및 암호화 API가 각 OS에서 다르기 때문에 [System.IO](https://github.com/dotnet/corefx/tree/master/src/System.IO) 및 [System.Security.Cryptography.Algorithms](https://github.com/dotnet/corefx/tree/master/src/System.Security.Cryptography.Algorithms)는 플랫폼별입니다.
- [System.Collections](https://github.com/dotnet/corefx/tree/master/src/System.Collections) 및 [System.Linq](https://github.com/dotnet/corefx/tree/master/src/System.Linq)는 데이터 구조를 통해 만들고 작동하기 때문에 플랫폼 중립입니다.

## <a name="comparisons-to-other-net-implementations"></a>다른 .NET 구현과 비교

기존 .NET 구현과 비교하면 .NET Core의 크기와 모양을 더 쉽게 파악할 수 있습니다.

### <a name="comparison-with-net-framework"></a>.NET Framework와 비교

.NET은 Microsoft가 2000년에 처음 발표한 후 발전해 왔습니다. .NET Framework는 Microsoft에서 거의 20년 가까이 만들어낸 기본 .NET 구현입니다.

.NET Core와 .NET Framework 간의 주요 차이점은 다음과 같습니다.

- **앱 모델** - .NET Core는 일부 .NET Framework 앱 모델을 지원하지 않습니다. 특히, ASP.NET Web Forms 및 ASP.NET MVC는 지원하지 않지만 ASP.NET Core MVC는 지원합니다. .NET Core 3.0부터 .NET Core는 Windows에서만 WPF와 Windows Forms도 지원합니다.
- **API** - .NET Core에는 팩터링이 다른 .NET Framework 기본 클래스 라이브러리의 대량 하위 집합이 포함됩니다(핵심 사례에서 어셈블리 이름이 다르고, 형식에서 노출된 멤버가 다름). 이러한 차이로 인해 소스를 .NET Core로 포팅하도록 변경해야 하는 경우도 있습니다. 자세한 내용은 [.NET 이식성 분석기](../standard/analyzers/portability-analyzer.md)를 참조하세요. .NET Core는 [.NET Standard](../standard/net-standard.md) API 사양을 구현합니다.
- **하위 시스템** -- .Net Core는 더 간단한 구현 및 프로그래밍 모델 구축을 위해 .NET Framework에 하위 시스템의 하위 집합을 구현합니다. 예를 들어 리플렉션은 지원되지만 CAS(코드 액세스 보안)는 지원되지 않습니다.
- **플랫폼** -- .NET Framework는 Windows와 Windows Server를 지원하는 반면 .NET Core는 macOS 및 Linux도 지원합니다.
- **오픈 소스** -- .NET Core는 오픈 소스이며, [.NET Framework의 읽기 전용 하위 집합](https://github.com/microsoft/referencesource)은 오픈 소스입니다.

.NET Core는 고유하며 .NET Framework 및 기타 .NET 구현과 현저한 차이가 있지만, 소스 또는 이진 공유 기술을 사용하여 이러한 구현 간에 코드를 간단하게 공유할 수 있습니다.

.NET Core는 side-by-side 설치를 지원하고 그 런타임은 .NET Framework와 완전히 독립적이므로 .NET Framework가 설치된 머신에 아무 문제 없이 설치할 수 있습니다.

### <a name="comparison-with-mono"></a>Mono와 비교

[Mono](https://www.mono-project.com/)는 원본 플랫폼 간 .NET입니다. .NET Framework의 [오픈 소스]([open-source](https://github.com/mono/mono)) 대안으로 시작되었으며, iOS 및 Android 디바이스가 보편화되면서 모바일 디바이스 대상 프로그램으로 전환되었습니다. .NET Framework의 커뮤니티 복제본으로 생각할 수 있습니다. Mono 프로젝트 팀은 호환되는 구현을 제공하기 위해 Microsoft에서 게시한 오픈 [.NET 표준](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/dotnet-standards.md)(특히 ECMA 335)을 사용했습니다.

.NET Core와 Mono 간의 주요 차이점은 다음과 같습니다.

- **앱 모델** - Mono는 Xamarin 제품을 통해 .NET Framework 앱 모델의 하위 집합(예: Windows Forms)과 모바일 개발을 위한 몇 가지 추가 모델(예: [Xamarin.iOS](https://www.xamarin.com/platform))을 지원합니다. .NET Core는 Xamarin을 지원하지 않습니다.
- **API** -- Mono는 .NET Framework API의 [큰 하위 집합](http://docs.go-mono.com/?link=root%3a%2fclasslib)을 지원하며, 동일한 어셈블리 이름 및 팩터링을 사용합니다.
- **플랫폼** -- Mono는 여러 플랫폼 및 CPU를 지원합니다.
- **오픈 소스** -- Mono와 .NET Core 둘 다 MIT 라이선스를 사용하며 .NET Foundation 프로젝트입니다.
- **포커스** -- 최근 몇 년 간 Mono의 주요 포커스는 모바일 플랫폼인 반면, .NET Core의 포커스는 클라우드 및 데스크톱 워크로드입니다.

## <a name="the-future"></a>미래

.NET Core의 다음 릴리스인 .NET 5는 플랫폼 통합을 나타낸다고 발표되었습니다. 이 프로젝트는 다음과 같은 몇 가지 주요 방법으로 .NET을 개선하려고 합니다.

- 어디서나 사용할 수 있고 일관성 있는 런타임 동작 및 개발자 환경을 제공하는 단일 .NET 런타임 및 프레임워크를 생성합니다.
- .NET Core, .NET Framework, Xamarin, Mono를 활용하여 .NET의 기능을 확장합니다.
- 개발자(Microsoft 및 커뮤니티)가 함께 작업하고 확장할 수 있으며 모든 시나리오를 개선하는 단일 코드 베이스에서 해당 제품을 빌드합니다.

.NET 5와 관련된 계획에 대한 자세한 내용은 [.NET 5 소개](https://devblogs.microsoft.com/dotnet/introducing-net-5/)를 참조하세요.
