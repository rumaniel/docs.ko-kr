---
title: .NET Core 2.0의 새로운 기능
description: .NET Core에서 볼 수 있는 새로운 기능에 대해 알아봅니다.
author: rpetrusha
ms.author: ronpet
ms.date: 08/13/2017
ms.openlocfilehash: c208f565bebedc06e244de1f6554129f21c77b8c
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70849941"
---
# <a name="whats-new-in-net-core-20"></a>.NET Core 2.0의 새로운 기능

.NET Core 2.0은 다음 영역에서 향상된 기능 및 새로운 기능을 포함합니다.

- [도구](#tooling)
- [언어 지원](#language-support)
- [플랫폼 개선](#platform-improvements)
- [API 변경 내용](#api-changes-and-library-support)
- [Visual Studio 통합](#visual-studio-integration)
- [설명서 개선](#documentation-improvements)

## <a name="tooling"></a>도구

### <a name="dotnet-restore-runs-implicitly"></a>dotnet restore runs implicitly

이전 버전의 .NET Core에서 [dotnet new](../tools/dotnet-new.md) 명령을 사용하여 새 프로젝트를 만든 이후뿐만 아니라 프로젝트에 새 종속성을 추가할 때마다 [dotnet restore](../tools/dotnet-restore.md) 명령을 실행하여 즉시 종속성을 다운로드합니다.

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

`--no-restore` 스위치를 `new`, `run`, `build`, `publish`, `pack` 및 `test` 명령으로 전달하여 `dotnet restore` 자동 호출을 사용하지 않도록 설정할 수 있습니다.

### <a name="retargeting-to-net-core-20"></a>.NET Core 2.0로 대상 다시 지정

.NET Core 2.0 SDK가 설치되면 .NET Core 1.x을 대상으로 지정하는 프로젝트는 .NET Core 2.0의 대상으로 다시 지정될 수 있습니다.

.NET Core 2.0을 대상으로 지정하려면 1.x에서 2.0까지 `<TargetFramework>` 요소(또는 프로젝트 파일에서 대상이 둘 이상 있는 경우 `<TargetFrameworks>` 요소)의 값을 변경하여 프로젝트 파일을 편집합니다.

```xml
<PropertyGroup>
    <TargetFramework>netcoreapp2.0</TargetFramework>
 </PropertyGroup>
```

또한 같은 방식으로 .NET 표준 2.0으로 .NET 표준 라이브러리의 대상을 다시 지정할 수 있습니다.

```xml
<PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
 </PropertyGroup>
```

프로젝트를 .NET Core 2.0으로 마이그레이션하는 방법에 대한 자세한 정보는 [ASP.NET Core 1.x에서 ASP.NET Core 2.0으로 마이그레이션](/aspnet/core/migration/1x-to-2x/index)을 참조하세요.

## <a name="language-support"></a>언어 지원

C# 및 F#를 지원할 뿐만 아니라 .NET Core 2.0도 Visual Basic을 지원합니다.

### <a name="visual-basic"></a>Visual Basic

이제 버전 2.0,.NET Core는 Visual Basic 2017을 지원합니다. Visual Basic을 사용하여 다음과 같은 프로젝트 형식을 만들 수 있습니다.

- .NET Core 콘솔 앱
- .NET Core 클래스 라이브러리
- .NET 표준 클래스 라이브러리
- .NET Core 단위 테스트 프로젝트
- .NET Core xUnit 테스트 프로젝트

예를 들어 Visual Basic "Hello World" 애플리케이션을 만들려면 명령줄에서 다음 단계를 수행합니다.

1. 콘솔 창을 열고 프로젝트에 대한 디렉터리를 만들고 현재 디렉터리로 설정합니다.

1. `dotnet new console -lang vb` 명령을 입력합니다.

   이 명령은 *Program.vb*라는 Visual Basic 소스 코드와 함께 `.vbproj` 파일 확장인 프로젝트 파일을 만듭니다. 이 파일은 문자열 "Hello World!"를 작성하는 소스 코드를 포함합니다. 콘솔 창에 표시합니다.

1. `dotnet run` 명령을 입력합니다. [.NET Core CLI](../tools/index.md)는 "Hello World!" 메시지를 표시하는 애플리케이션을 자동으로 컴파일하고 실행합니다. 콘솔 창에 표시합니다.

### <a name="support-for-c-71"></a>C# 7.1에 대한 지원

.NET Core 2.0은 다음을 비롯하여 다양하고 새로운 기능을 추가하는 C# 7.1을 지원합니다.

- 애플리케이션 진입점인 `Main` 메서드는 [비동기](../../csharp/language-reference/keywords/async.md) 키워드로 표시될 수 있습니다.
- 유추된 튜플 이름입니다.
- 기본 식입니다.

<!-- For more information see [link to C# what's new](url). -->

## <a name="platform-improvements"></a>플랫폼 개선

.NET Core 2.0은 .NET Core를 쉽게 설치하고 지원되는 운영 체제에서 사용할 수 있는 다양한 기능을 포함합니다.

### <a name="net-core-for-linux-is-a-single-implementation"></a>Linux용 .NET core는 단일 구현입니다.

.NET Core 2.0은 여러 Linux 배포에서 작동하는 단일 Linux 구현을 제공합니다. .NET Core 1.x은 배포 관련 Linux 구현을 다운로드하는 데 필요합니다.

또한 단일 운영 체제로 Linux를 대상으로 하는 앱을 개발할 수 있습니다. .NET Core 1.x는 별도로 각 Linux 배포를 대상으로 하는 데 필요합니다.

### <a name="support-for-the-apple-cryptographic-libraries"></a>Apple 암호화 라이브러리에 대한 지원

.NET Core 1.x는 OpenSSL 도구 키트의 암호화 라이브러리에 필요합니다. .NET Core 2.0은 Apple 암호화 라이브러리를 사용하고 OpenSSL을 필요로 하지 않으므로 더 이상 설치할 필요가 없습니다.

## <a name="api-changes-and-library-support"></a>API 변경 내용 및 라이브러리 지원

### <a name="support-for-net-standard-20"></a>.NET 표준 2.0에 대한 지원

.NET 표준은 해당 버전의 표준에 부합하는 .NET 구현에서 사용할 수 있어야 하는 버전이 지정된 API 집합을 정의합니다. .NET 표준은 라이브러리 개발자에서 대상으로 지정됩니다. 각 .NET 구현에 .NET 표준의 버전을 대상으로 지정하는 라이브러리에 사용할 수 있는 기능을 보장하려고 합니다. .NET Core 1.x는 .NET 표준 버전 1.6을 지원하고 .NET Core 2.0은 최신 버전인 .NET 표준 2.0을 지원합니다. 자세한 내용은 [.NET 표준](../../standard/net-standard.md)을 참조하세요.

.NET 표준 2.0에는 .NET 표준 1.6에서 사용할 수 있었던 20,000개가 넘는 API가 포함됩니다. 이 확장된 노출 영역 중 상당 부분은 .NET Framework 및 Xamarin에 공통되는 API를 .NET 표준에 통합한 결과입니다.

.NET 표준 2.0 클래스 라이브러리는 .NET Framework 클래스 라이브러리를 참조할 수도 있고 .NET 표준 2.0에서 표시되는 API를 호출하도록 제공됩니다. .NET Framework 라이브러리를 다시 컴파일하지 않아도 됩니다.

마지막 버전인 .NET 표준 1.6 이후 .NET 표준에 추가된 API 목록은 [.NET 표준 2.0 및 1.6](https://raw.githubusercontent.com/dotnet/standard/master/docs/versions/netstandard2.0_diff.md)을 참조하세요.

### <a name="expanded-surface-area"></a>확장된 노출 영역

.NET Core 2.0에서는 사용할 수 있는 API의 총수는 .NET Core 1.1에 비교하여 두 배 이상 증가했습니다.

그리고 [Windows 호환 기능 팩](../porting/windows-compat-pack.md) 덕분에 .NET Framework에서 이식하는 작업이 훨씬 더 간편해졌습니다.

### <a name="support-for-net-framework-libraries"></a>.NET Framework 라이브러리에 대한 지원

.NET Core 코드는 기존 NuGet 패키지를 비롯한 기존 .NET Framework 라이브러리를 참조할 수 있습니다. 라이브러리는 표준.NET에서 발견되는 API를 사용해야 합니다.

## <a name="visual-studio-integration"></a>Visual Studio 통합

Visual Studio 2017 버전 15.3 및 경우에 따라 Mac용 Visual Studio는 .NET Core 개발자를 위해 다양한 주요 기능 향상을 제공합니다.

### <a name="retargeting-net-core-apps-and-net-standard-libraries"></a>.NET Core 앱 및 .NET 표준 라이브러리를 대상으로 다시 지정

.NET Core 2.0 SDK가 설치되는 경우 .NET Core 1.x 프로젝트를 .NET Core 2.0으로, .NET 표준 1.x 라이브러리를 .NET 표준 2.0으로 대상을 변경할 수 있습니다.

Visual Studio에서 프로젝트의 대상을 변경하려면 프로젝트 속성 대화 상자의 **애플리케이션** 탭을 열고 **대상 프레임 워크** 값을 **.NET Core 2.0** 또는 **.NET 표준 2.0**으로 변경합니다. 또한 프로젝트를 마우스 오른쪽 단추로 클릭하고 **\*.csproj 파일 편집** 옵션을 선택하여 변경할 수 있습니다. 자세한 내용은 이 항목 앞 부분의 [도구](#tooling) 섹션을 참조하세요.

### <a name="live-unit-testing-support-for-net-core"></a>.NET Core에 대한 Live Unit Testing 지원

Live Unit Testing이 코드를 수정하려면 언제든지 자동으로 백그라운드에서 영향을 받는 단위 테스트를 실행하고 Visual Studio 환경에서 결과 및 코드 검사 라이브를 표시합니다. 이제 .NET Core 2.0은 Live Unit Testing을 지원합니다. 이전에 Live Unit Testing은 .NET Framework 애플리케이션에만 사용할 수 있었습니다.

자세한 내용은 [Visual Studio 2017에서 Live Unit Testing](/visualstudio/test/live-unit-testing) 및 [Live Unit Testing FAQ](/visualstudio/test/live-unit-testing-faq)를 참조하세요.

### <a name="better-support-for-multiple-target-frameworks"></a>다양한 대상 프레임워크에 대한 지원 향상

다양한 대상 프레임워크에 대한 프로젝트를 빌드하는 경우 이제 최상위 메뉴에서 대상 플랫폼을 선택할 수 있습니다. 다음 그림에서 SCD1이라는 프로젝트는 64비트 macOS X 10.11(`osx.10.11-x64`) 및 64비트 Windows 10/Windows Server 2016(`win10-x64`)을 대상으로 지정합니다. 디버그 빌드를 실행하는 경우에 프로젝트 단추를 선택하기 전에 대상 프레임워크를 선택할 수 있습니다.

![프로젝트를 빌드할 때 대상 프레임워크 선택 영역을 보여주는 스크린샷](./media/dotnet-core-2-0/target-framework-selection.png)

### <a name="side-by-side-support-for-net-core-sdks"></a>.NET Core SDK에 대한 병렬 지원

이제 Visual Studio와 독립적으로 .NET Core SDK를 설치할 수 있습니다. 따라서 단일 버전의 Visual Studio에서 다른 버전의 .NET Core를 대상으로 지정하는 프로젝트를 빌드할 수 있습니다. 이전에 Visual Studio 및 .NET Core SDK는 밀접하게 연결되어 있었습니다. 특정 버전의 SDK는 특정 버전의 Visual Studio와 함께 제공되었습니다.

## <a name="documentation-improvements"></a>설명서 개선

### <a name="net-application-architecture"></a>.NET 애플리케이션 아키텍처

빌드하는 데 .NET을 사용하는 경우 [.NET 애플리케이션 아키텍처](https://dotnet.microsoft.com/learn/dotnet/architecture-guides)는 지침, 모범 사례 및 애플리케이션 예제를 제공하는 eBook 집합에 액세스 권한을 부여합니다.

- [마이크로 서비스 및 Docker 컨테이너](../../architecture/microservices/index.md)
- [ASP.NET을 사용하여 개발한 웹 애플리케이션](../../architecture/modern-web-apps-azure/index.md)
- [Xamarin을 사용하는 모바일 애플리케이션](/xamarin/xamarin-forms/enterprise-application-patterns/index)
- [Azure에서 클라우드에 배포되는 애플리케이션](/azure/architecture/reference-architectures/index)

## <a name="see-also"></a>참고 항목

- [ASP.NET Core 2.0의 새로운 기능](/aspnet/core/aspnetcore-2.0)
