---
title: .NET 아키텍처 구성 요소
description: .NET Standard, .NET 구현, .NET 런타임 및 도구와 같은 .NET 아키텍처 구성 요소에 대해 설명합니다.
author: cartermp
ms.author: mairaw
ms.date: 08/23/2017
ms.technology: dotnet-standard
ms.openlocfilehash: b98095cd6afd408331ab8c8f6bb15e7741d3073a
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50189695"
---
# <a name="net-architectural-components"></a>.NET 아키텍처 구성 요소

.NET 앱은 하나 이상의 *.NET 구현*에 대해 개발되고 이 구현에서 실행됩니다.  .NET 구현에는 .NET Framework, .NET Core 및 Mono가 포함됩니다. .NET Standard라는 모든 .NET 구현에 공통된 API 사양이 있습니다. 이 문서에서는 이러한 각 개념에 대해 간략하게 소개합니다.

## <a name="net-standard"></a>.NET Standard

.NET Standard는 .NET 구현의 기본 클래스 라이브러리에서 구현하는 API 집합입니다. 공식적으로 말하자면 코드를 컴파일할 균일한 계약 집합을 구성하는 .NET API 사양입니다. 이러한 계약은 각 .NET 구현에서 구현됩니다. 그러면 코드가 어디서든 실행될 수 있도록 여러 .NET 구현 간에 이식할 수 있습니다.

.NET Standard는 또한 [대상 프레임워크](glossary.md#target-framework)입니다. 코드가 .NET Standard의 버전을 대상으로 하는 경우 해당 버전의 .NET Standard를 지원하는 모든 .NET 구현에서 실행할 수 있습니다.

.NET Standard 및 대상으로 지정하는 방법에 대한 자세한 내용은 [.NET Standard](net-standard.md) 항목을 참조하세요.

## <a name="net-implementations"></a>.NET 구현

.NET의 각 구현에는 다음과 같은 구성 요소가 포함됩니다.

- 하나 이상의 런타임. 예를 들어 .NET Framework용 CLR, CoreCLR 및 .NET Core용 CoreRT가 있습니다.
- .NET Standard를 구현하고 추가 API를 구현할 수 있는 클래스 라이브러리. 예를 들어 .NET Framework 기본 클래스 라이브러리, .NET Core 기본 클래스 라이브러리가 있습니다.
- 필요에 따라 하나 이상의 응용 프로그램 프레임워크. 예를 들어 [ASP.NET](https://www.asp.net/), [Windows Forms](../framework/winforms/windows-forms-overview.md) 및 [WPF(Windows Presentation Foundation)](../framework/wpf/index.md)가 .NET Framework에 포함됩니다.
- 필요에 따라 개발 도구. 일부 개발 도구는 여러 구현에서 공유됩니다.

Microsoft에서 적극적으로 개발하고 유지 관리하는 네 가지 기본 .NET 구현은 .NET Core, .NET Framework, Mono 및 UWP입니다.

### <a name="net-core"></a>.NET Core

.NET Core는 .NET의 플랫폼 간 구현으로, 대규모 서버 및 클라우드 워크로드를 처리하도록 설계되었습니다. Windows, macOS 및 Linux에서 실행됩니다. .NET Core는 .NET Standard를 구현하므로 .NET Standard를 대상으로 하는 코드는 .NET Core에서 실행할 수 있습니다. ASP.NET Core는 .NET Core에서 실행됩니다. 

.NET Core에 대한 자세한 내용은 [.NET Core 가이드](../core/index.md) 및 [서버 앱에 대해 .NET Core와 .NET Framework 중에 선택](choosing-core-framework-server.md)을 참조하세요.

### <a name="net-framework"></a>.NET Framework

.NET Framework는 2002년부터 있었던 원래 .NET 구현입니다. 기존 .NET 개발자가 항상 사용해 온 것과 동일한 .NET Framework입니다. 버전 4.5 이상은 .NET Standard를 구현하므로 .NET Standard를 대상으로 하는 코드는 .NET Framework의 해당 버전에서 실행할 수 있습니다. Windows Forms 및 WPF를 사용하는 Windows 데스크톱 개발용 API와 같이 Windows 관련 추가 API가 포함되어 있습니다. .NET Framework는 Windows 데스크톱 응용 프로그램을 구축을 위해 최적화되어 있습니다.

.NET Framework에 대한 자세한 내용은 [.NET Framework 가이드](../framework/index.md)를 참조하세요.

### <a name="mono"></a>Mono

Mono는 작은 런타임이 필요할 때 주로 사용되는 .NET 구현입니다. 이는 Android, Mac, iOS, tvOS 및 watchOS에서 Xamarin 응용 프로그램의 성능을 향상하는 런타임으로, 주로 작은 사용 공간에 초점을 맞춥니다. 또한 Mono는 Unity 엔진을 사용하여 빌드된 게임을 제공합니다.

Mono는 현재 게시된 .NET Standard 버전을 모두 지원합니다.

지금까지 Mono는 .NET Framework의 더 큰 API를 구현하고 Unix에서 가장 인기 있는 기능 중 일부를 에뮬레이트했습니다. 경우에 따라 Unix에서 해당 기능을 사용하는 .NET 응용 프로그램을 실행하는 데도 사용됩니다.

일반적으로 Mono는 Just-In-Time 컴파일러에서 사용되지만 iOS 같은 플랫폼에 사용되는 전체 정적 컴파일러(Ahead-Of-Time 컴파일) 기능도 제공합니다.

Mono에 대한 자세한 내용은 [Mono 설명서](https://www.mono-project.com/docs/)를 참조하세요.

### <a name="universal-windows-platform-uwp"></a>UWP(유니버설 Windows 플랫폼)

UWP는 IoT(사물 인터넷)에 대한 최신 터치 가능 Windows 응용 프로그램 및 소프트웨어를 작성하는 데 사용되는 .NET의 구현입니다. PC, 태블릿, 패블릿, 휴대폰, Xbox 등 대상으로 지정할 수 있는 다양한 종류의 장치를 통합하도록 설계되었습니다. UWP는 중앙 집중식 앱 스토어, 실행 환경(AppContainer), Win32 대신 사용할 Windows API 집합(WinRT) 등 많은 서비스를 제공합니다. 앱은 C++, C#, VB.NET 및 JavaScript로 작성할 수 있습니다. C# 및 VB.NET을 사용할 경우 .NET API는 .NET Core에서 제공됩니다.

UWP에 대한 자세한 내용은 [유니버설 Windows 플랫폼 소개](/windows/uwp/get-started/universal-application-platform-guide)를 참조하세요.

## <a name="net-runtimes"></a>.NET 런타임

런타임은 관리되는 프로그램에 대한 실행 환경입니다. OS는 런타임 환경의 일부이지만 .NET 런타임의 일부는 아닙니다. 다음은 .NET 런타임의 몇 가지 예입니다.

- .NET Framework에 대한 CLR(공용 언어 런타임)
- .NET Core에 대한 CoreCLR(Core 공용 언어 런타임)
- 유니버설 Windows 플랫폼용 .NET 네이티브 
- Xamarin.iOS, Xamarin.Android, Xamarin.Mac 및 Mono 데스크톱 프레임워크에 대한 Mono 런타임

## <a name="net-tooling-and-common-infrastructure"></a>.NET 도구 및 공통 인프라

모든 .NET 구현에서 작동하는 광범위한 도구 및 인프라 구성 요소 집합에 액세스할 수 있습니다. 여기에는 다음이 포함되지만 다음으로 제한되지는 않습니다.

- .NET 언어 및 해당 컴파일러
- .NET 프로젝트 시스템(*.csproj*, *.vbproj* 및 *.fsproj* 파일 기반)
- 프로젝트를 빌드하는 데 사용하는 빌드 엔진 [MSBuild](/visualstudio/msbuild/msbuild)
- .NET에 대한 Microsoft의 패키지 관리자 [NuGet](/nuget/)
- [CAKE](https://cakebuild.net/) 및 [FAKE](https://fake.build/) 등의 오픈 소스 빌드 오케스트레이션 도구

## <a name="see-also"></a>참고 항목

- [서버 앱에 대해 .NET Core와 .NET Framework 중에 선택](choosing-core-framework-server.md)   
- [.NET Standard](net-standard.md)  
- [.NET Core 가이드](../core/index.md)  
- [.NET Framework 가이드](../framework/index.md)  
- [C# 가이드](../csharp/index.md)  
- [F# 가이드](../fsharp/index.md)  
- [VB.NET 가이드](../visual-basic/index.md)  
