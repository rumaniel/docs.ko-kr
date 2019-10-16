---
title: .NET 아키텍처 구성 요소
description: .NET Standard, .NET 구현, .NET 런타임 및 도구와 같은 .NET 아키텍처 구성 요소에 대해 설명합니다.
author: cartermp
ms.author: mairaw
ms.date: 08/23/2017
ms.technology: dotnet-standard
ms.openlocfilehash: f43cd61fbcb3c1c872961476449822c574f76cff
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71835276"
---
# <a name="net-architectural-components"></a>.NET 아키텍처 구성 요소

.NET 앱은 하나 이상의 *.NET 구현체*로 개발하고 이 구현체에서 동작합니다.  .NET 구현체에는 .NET Framework과 .NET Core, Mono가 있습니다. 모든 .NET 구현체에는 공통적으로 .NET Standard API 규격이 존재합니다. 이 문서에서는 이러한 개념들을 간략하게 소개합니다.

## <a name="net-standard"></a>.NET Standard

.NET Standard는 .NET 구현체의 기본 클래스 라이브러리(Base Class Library)로 구현한 API 집합입니다. 보다 공식적으로는, 코드를 컴파일할 수 있는 일정한 약속을 구성하는 .NET API 규격입니다. 이러한 약속은 모든 .NET 구현체에서 구현됩니다. 그러면 다양한 .NET 구현체 간에 코드를 효과적으로 이식하고 실행할 수 있게 됩니다.

또한 .NET Standard는 [대상 프레임워크](glossary.md#target-framework)입니다. .NET Standard 버전을 대상으로 하는 코드는 해당 .NET Standard 버전을 지원하는 모든 .NET 구현체에서 실행할 수 있습니다.

.NET Standard와 대상 지정 방법의 자세한 내용은 [.NET Standard](net-standard.md) 항목을 참조하세요.

## <a name="net-implementations"></a>.NET 구현체

.NET의 각 구현체에는 다음 구성 요소가 포함됩니다.

- 하나 이상의 런타임. 예: .NET Framework용 CLR과 .NET Core용 CoreCLR, CoreRT.
- .NET Standard와 추가 API를 구현할 수 있는 클래스 라이브러리. 예: .NET Framework 기본 클래스 라이브러리, .NET Core 기본 클래스 라이브러리.
- 필요에 따라 하나 이상의 애플리케이션 프레임워크. 예: [ASP.NET](https://www.asp.net/), [Windows Forms](../framework/winforms/windows-forms-overview.md) 및 [WPF(Windows Presentation Foundation)](../framework/wpf/index.md)가 .NET Framework 및 .NET Core에 포함됩니다.
- 필요에 따라 개발 도구. 일부 개발 도구는 여러 구현체에서 공통적으로 사용할 수 있음.

Microsoft에서 적극적으로 개발 및 유지 보수하는 네 가지 기본 .NET 구현체는 .NET Core와 .NET Framework, Mono, UWP입니다.

### <a name="net-core"></a>.NET Core

.NET Core는 다양한 .NET 플랫폼에서 사용할 수 있는 구현체로, 대규모 서버 및 클라우드 워크로드를 처리하도록 설계되었습니다. Windows와 macOS, Linux에서 실행됩니다. .NET Core는 .NET Standard를 구현하므로 .NET Standard를 대상으로 하는 코드는 .NET Core에서 실행할 수 있습니다. [ASP.NET Core](https://dotnet.microsoft.com/learn/aspnet/what-is-aspnet-core), [Windows Forms](../framework/winforms/windows-forms-overview.md) 및 [WPF(Windows Presentation Foundation)](../framework/wpf/index.md)는 모두 .NET Core에서 실행됩니다.

.NET Core의 자세한 내용은 [.NET Core 가이드](../core/index.md)와 [서버 앱에 대해 .NET Core와 .NET Framework 중에 선택](choosing-core-framework-server.md)을 참조하세요.

### <a name="net-framework"></a>.NET Framework

.NET Framework는 2002년부터 있었던 원래 .NET 구현입니다. 기존 .NET 개발자가 항상 사용해 온 것과 동일한 .NET Framework입니다. 버전 4.5 이상은 .NET Standard를 구현하므로 .NET Standard를 대상으로 하는 코드는 .NET Framework의 해당 버전에서 실행할 수 있습니다. Windows Forms 및 WPF를 사용하는 Windows 데스크톱 개발용 API와 같이 Windows 관련 추가 API가 포함되어 있습니다. .NET Framework는 Windows 데스크톱 애플리케이션을 구축을 위해 최적화되어 있습니다.

.NET Framework의 자세한 내용은 [.NET Framework 가이드](../framework/index.md)를 참조하세요.

### <a name="mono"></a>Mono

Mono는 작은 런타임이 필요할 때 주로 사용되는 .NET 구현체입니다. 이는 Android와 Mac, iOS, tvOS, watchOS에서 Xamarin 애플리케이션을 구동하는 런타임으로, 주로 적은 공간을 점유하는데 중점을 두고 있습니다. 또한 Mono에서는 Unity 엔진으로 만든 게임이 동작합니다.

Mono는 현재 게시된 .NET Standard 버전을 모두 지원합니다.

지금까지 Mono는 .NET Framework의 방대한 API를 구현하고 Unix에서 가장 인기 있는 기능의 일부를 따라서 만들었습니다. 경우에 따라 Unix에서 해당 기능을 사용하는 .NET 애플리케이션을 실행하는 데도 사용됩니다.

일반적으로 Mono는 Just-In-Time 컴파일러에서 사용되지만 iOS 같은 플랫폼에 사용되는 전체 정적 컴파일러(Ahead-Of-Time 컴파일) 기능도 제공합니다.

Mono의 자세한 내용은 [Mono 설명서](https://www.mono-project.com/docs/)를 참조하세요.

### <a name="universal-windows-platform-uwp"></a>UWP(유니버설 Windows 플랫폼)

UWP는 IoT(사물 인터넷)에 대한 최신 터치 가능 Windows 애플리케이션 및 소프트웨어를 작성하는 데 사용되는 .NET의 구현입니다. PC와 태블릿, 패블릿, 휴대폰, Xbox 등을 포함하여 대상이 될 수 있는 다양한 종류의 디바이스를 통합하기 위해 설계되었습니다. UWP는 중앙 집중식 앱 스토어, 실행 환경(AppContainer), Win32를 대체할 Windows API(WinRT) 등 많은 서비스를 제공합니다. 앱은 C++과 C#, VB.NET, JavaScript로 작성할 수 있습니다. C#과 VB.NET을 사용할 경우 .NET API는 .NET Core에서 제공됩니다.

UWP의 자세한 내용은 [유니버설 Windows 플랫폼 소개](/windows/uwp/get-started/universal-application-platform-guide)를 참조하세요.

## <a name="net-runtimes"></a>.NET 런타임

런타임은 관리되는 프로그램에 대한 실행 환경입니다. OS는 런타임 환경의 일부이지만 .NET 런타임의 일부는 아닙니다. 다음은 .NET 런타임의 몇 가지 예입니다.

- .NET Framework에 대한 CLR(공용 언어 런타임)
- .NET Core에 대한 CoreCLR(Core 공용 언어 런타임)
- 유니버설 Windows 플랫폼용 .NET 네이티브 
- Xamarin.iOS와 Xamarin.Android, Xamarin.Mac, Mono 데스크톱 프레임워크에 대한 Mono 런타임

## <a name="net-tooling-and-common-infrastructure"></a>.NET 도구 및 공통 인프라

모든 .NET 구현체에서 동작하는 다양한 도구와 인프라 구성 요소를 사용할 수 있습니다. 여기에는 다음 항목들이 포함되며 이 항목들이 전부는 아닙니다.

- .NET 언어 및 해당 컴파일러
- .NET 프로젝트 시스템( *.csproj*, *.vbproj* 및 *.fsproj* 파일 기반)
- 프로젝트를 빌드하는 데 사용하는 빌드 엔진 [MSBuild](/visualstudio/msbuild/msbuild)
- .NET에 대한 Microsoft의 패키지 관리자 [NuGet](/nuget/)
- [CAKE](https://cakebuild.net/) 및 [FAKE](https://fake.build/) 등의 오픈 소스 빌드 오케스트레이션 도구

## <a name="applicable-standards"></a>적용 가능한 표준

C# 언어 및 CLI(공용 언어 인프라) 사양은 [Ecma International® ](https://www.ecma-international.org/)을 통해 표준화됩니다. 이러한 표준의 첫 번째 버전은 2001년 12월에 Ecma에서 게시했습니다.

표준에 대한 후속 수정 사항은 프로그래밍 언어 기술 위원회([TC49](https://www.ecma-international.org/memento/tc49.htm)) 내에서 TC49-TG2(C#) 및 TC49-TG3(CLI) 작업 그룹을 통해 개발되었고 이후에는 Ecma General Assembly가, 그 이후에는 ISO/IEC JTC 1이 ISO Fast-Track 프로세스를 통해 도입했습니다.

### <a name="latest-standards"></a>최신 표준

다음과 같은 공식 Ecma 문서는 [C#](http://www.ecma-international.org/publications/standards/Ecma-334.htm) 및 [CLI](http://www.ecma-international.org/publications/standards/Ecma-335.htm)([TR-84](http://www.ecma-international.org/publications/techreports/E-TR-084.htm))에서 사용할 수 있습니다.

- **C# 언어 표준(버전 5.0)** : [ECMA-334.pdf](https://www.ecma-international.org/publications/files/ECMA-ST/ECMA-334.pdf)
- **CLI(공용 언어 인프라)** : [pdf](https://www.ecma-international.org/publications/files/ECMA-ST/ECMA-335.pdf) 양식 및 [zip](https://www.ecma-international.org/publications/files/ECMA-ST/ECMA-335.zip) 양식으로 제공됩니다.
- **파티션 IV XML 파일에서 파생된 정보**: [pdf](https://www.ecma-international.org/publications/files/ECMA-TR/ECMA%20TR-084.pdf) 및 [zip](https://www.ecma-international.org/publications/files/ECMA-TR/TR-084.zip) 양식으로 제공됩니다.
 
공식 ISO/IEC 문서는 ISO/IEC [공개적으로 사용할 수 있는 표준](https://standards.iso.org/ittf/PubliclyAvailableStandards/) 페이지에서 사용할 수 있습니다. 이러한 링크는 해당 페이지에서 직접 제공됩니다.

- **정보 기술 - 프로그래밍 언어- C#** : [ISO/IEC 23270:2018](https://standards.iso.org/ittf/PubliclyAvailableStandards/c075178_ISO_IEC_23270_2018.zip)
- **정보 기술 - CLI(공용 언어 인프라) 파티션 I ~ VI**: [ISO/IEC 23271:2012](https://standards.iso.org/ittf/PubliclyAvailableStandards/c058046_ISO_IEC_23271_2012(E).zip)
- **정보 기술 - CLI (공용 언어 인프라) - 파티션 IV XML 파일에서 파생된 정보에 대한 기술 보고서**: [ISO/IEC TR 23272:2011](https://standards.iso.org/ittf/PubliclyAvailableStandards/c057955_ISO_IEC_TR_23272_2011.zip)

## <a name="see-also"></a>참고 항목

- [서버 앱에 대해 .NET Core와 .NET Framework 중에 선택](choosing-core-framework-server.md)
- [.NET Standard](net-standard.md)
- [.NET Core 가이드](../core/index.md)
- [.NET Framework 가이드](../framework/index.md)
- [C# 가이드](../csharp/index.md)
- [F# 가이드](../fsharp/index.md)
- [VB.NET 가이드](../visual-basic/index.md)
