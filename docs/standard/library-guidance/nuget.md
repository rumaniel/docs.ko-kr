---
title: NuGet 및 .NET 라이브러리
description: .NET 라이브러리용 NuGet을 사용하여 패키지하는 모범 사례 권장 사항입니다.
author: jamesnk
ms.author: mairaw
ms.date: 01/15/2019
ms.openlocfilehash: 9cf30fa41af2d31e416bae1d75d8880ece7dde3e
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70895203"
---
# <a name="nuget"></a>NuGet

NuGet은 .NET 에코시스템의 패키지 관리자이며, 개발자가 .NET 오픈 소스 라이브러리를 검색하고 획득할 수 있는 기본 방법입니다. NuGet 패키지를 호스트하기 위해 Microsoft에서 제공하는 무료 서비스인 [NuGet.org](https://www.nuget.org/)가 공용 NuGet 패키지의 기본 호스트지만, [MyGet](https://www.myget.org/) 및 [Azure Artifacts](https://azure.microsoft.com/services/devops/artifacts/)와 같은 사용자 지정 NuGet 서비스에 게시할 수도 있습니다.

![NuGet](./media/nuget/nuget-logo.png "NuGet")

## <a name="create-a-nuget-package"></a>NuGet 패키지 만들기

NuGet 패키지(`*.nupkg`)는 .NET 어셈블리 및 관련 메타데이터를 포함하는 zip 파일입니다.

NuGet 패키지를 만드는 방법에는 크게 두 가지가 있습니다. 최신 및 권장되는 방법은 SDK 스타일 프로젝트(콘텐츠가 `<Project Sdk="Microsoft.NET.Sdk">`로 시작하는 프로젝트 파일)에서 패키지를 만드는 것입니다. 어셈블리 및 대상은 패키지에 자동으로 추가되고, 패키지 이름 및 버전 번호와 같은 나머지 메타데이터는 MSBuild 파일에 추가됩니다. [`dotnet pack`](../../core/tools/dotnet-pack.md) 명령을 사용하여 컴파일하면 어셈블리 대신 `*.nupkg` 파일이 출력됩니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <AssemblyName>Contoso.Api</AssemblyName>
    <PackageVersion>1.1.0</PackageVersion>
    <Authors>John Doe</Authors>
  </PropertyGroup>
</Project>
```

NuGet 패키지를 만드는 이전 방법은 `*.nuspec` 파일 및 `nuget.exe` 명령줄 도구를 사용하는 것입니다. nuspec 파일을 사용하면 제어 기능이 향상되지만 최종 NuGet 패키지에 포함할 어셈블리 및 대상을 신중하게 지정해야 합니다. 실수하거나, 다른 사람이 변경할 때 nuspec 업데이트를 잊어버리기 쉽습니다. nuspec의 장점은 아직 SDK 스타일 프로젝트 파일을 지원하지 않는 프레임워크에 대한 NuGet 패키지를 만드는 데 사용할 수 있다는 것입니다.

**✔** SDK 스타일 프로젝트 파일을 사용하여 NuGet 패키지를 만드세요.

## <a name="package-dependencies"></a>패키지 종속성

NuGet 패키지 종속성은 [종속성](./dependencies.md) 문서에서 자세히 다룹니다.

## <a name="important-nuget-package-metadata"></a>중요 NuGet 패키지 메타데이터

NuGet 패키지는 많은 [메타데이터 속성](/nuget/reference/nuspec)을 지원합니다. 다음 표에는 모든 NuGet.org의 패키지에서 제공해야 하는 핵심 메타데이터가 나와 있습니다.

| MSBuild 속성 이름              | Nuspec 이름              | 설명  |
| ---------------------------------- | ------------------------ | ------------ |
| `PackageId`                        | `id`                       | 패키지 식별자입니다. [조건](/nuget/reference/id-prefix-reservation)을 충족하는 경우 식별자의 접두사를 예약할 수 있습니다. |
| `PackageVersion`                   | `version`                  | NuGet 패키지 버전입니다. 자세한 내용은 [NuGet 패키지 버전](./versioning.md#nuget-package-version)을 참조하세요.             |
| `Title`                            | `title`                    | 패키지의 제목입니다. 기본값은 `PackageId`입니다.             |
| `Description`                      | `description`              | UI에 표시되는, 패키지에 대한 자세한 설명입니다.             |
| `Authors`                          | `authors`                  | nuget.org의 프로필 이름과 일치하는 패키지 작성자의 쉼표로 구분된 목록입니다.             |
| `PackageTags`                      | `tags`                     | 패키지를 설명하는 태그 및 키워드의 공백으로 구분된 목록입니다. 태그는 패키지를 검색할 때 사용됩니다.             |
| `PackageIconUrl`                   | `iconUrl`                  | 패키지의 아이콘으로 사용할 이미지의 URL입니다. URL은 HTTPS여야 하며, 이미지는 64x64이고 투명한 배경을 사용해야 합니다.             |
| `PackageProjectUrl`                | `projectUrl`               | 프로젝트 홈페이지 또는 소스 리포지토리의 URL입니다.             |
| `PackageLicenseExpression`         | `license`                  | 프로젝트 라이선스의 [SPDX 식별자](https://spdx.org/licenses/)입니다. OSI 및 FSF 승인 라이선스만 식별자를 사용할 수 있습니다. 다른 라이선스는 `PackageLicenseFile`을 사용해야 합니다. [`license` 메타데이터](/nuget/reference/nuspec#license)에 대해 자세히 알아봅니다. |

> [!IMPORTANT]
> 라이선스가 없는 프로젝트의 기본값은 [배타적 저작권](https://choosealicense.com/no-permission/)으로 설정되므로 다른 사용자는 합법적으로 사용할 수 없습니다.

**✔️** NuGet의 접두사 예약 [조건](/nuget/reference/id-prefix-reservation)을 충족하는 접두사를 가진 NuGet 패키지 이름을 선택합니다.

**✔️** 패키지 아이콘에 대한 HTTPS href를 사용합니다.

> HTTPS를 사용하여 실행되고 HTTPS가 아닌 이미지를 표시하는 NuGet.org 등의 사이트는 혼합 콘텐츠 경고를 만듭니다.

**✔️** 보기 결과를 최적화하기 위해 64x64이고 투명한 배경을 가진 패키지 아이콘 이미지를 사용합니다.

**✔️** [소스 링크](./sourcelink.md)를 설정하여 어셈블리 및 NuGet 패키지에 소스 제어 메타데이터를 추가하세요.

> 소스 링크는 `RepositoryUrl` 및 `RepositoryType` 메타데이터를 NuGet 패키지에 자동으로 추가합니다. 소스 링크는 패키지가 빌드된 정확한 소스 코드에 대한 정보도 추가합니다. 예를 들어 Git 리포지토리에서 만든 패키지에는 메타데이터로 추가된 커밋 해시가 있습니다.

## <a name="pre-release-packages"></a>시험판 패키지

버전 접미사가 있는 NuGet 패키지는 [시험판](/nuget/create-packages/prerelease-packages)으로 간주됩니다. 기본적으로 NuGet 패키지 관리자 UI는 사용자가 시험판 패키지를 옵트인하지 않는 한 안정적인 릴리스를 표시하므로, 시험판 패키지는 제한된 사용자 테스트에 적합합니다.

```xml
<PackageVersion>1.0.1-beta1</PackageVersion>
```

> [!NOTE]
> 안정적인 패키지는 시험판 패키지에 종속될 수 없습니다. 사용자 고유의 패키지를 시험판으로 설정하거나 이전의 안정적인 버전에 종속되도록 설정해야 합니다.

![NuGet 시험판 패키지 종속성](./media/nuget/nuget-prerelease-package.png "NuGet 시험판 패키지 종속성")

**✔️** 테스트, 미리 보기 또는 실험 시에는 시험판 패키지를 게시합니다.

**✔️** 준비가 되면 안정적인 패키지를 게시하여 다른 안정적인 패키지가 참조할 수 있도록 합니다.

## <a name="symbol-packages"></a>기호 패키지

기호 파일(`*.pdb`)은 어셈블리와 함께 .NET 컴파일러에서 생성됩니다. 기호 파일은 실행 위치를 원래 소스 코드에 매핑하므로, 디버거를 사용하여 실행 중인 소스 코드를 한 단계씩 실행할 수 있습니다. NuGet은 .NET 어셈블리를 포함하는 주 패키지와 함께 기호 파일을 포함하는 [별도의 기호 패키지(`*.snupkg`) 생성](/nuget/create-packages/symbol-packages-snupkg)을 지원합니다. 기호 패키지는 기호 서버에서 호스트되며 요청 시 Visual Studio와 같은 도구에서만 다운로드되도록 설계되었습니다.

NuGet.org는 자체 [기호 서버 리포지토리](/nuget/create-packages/symbol-packages-snupkg#nugetorg-symbol-server)를 호스팅합니다. 개발자는 해당 [Visual Studio의 심볼 소스](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)에 `https://symbols.nuget.org/download/symbols`를 추가하여 NuGet.org 기호 서버에 게시된 기호를 사용할 수 있습니다.

> [!IMPORTANT]
> NuGet.org 기호 서버는 SDK 스타일 프로젝트에서 생성한 새 [이식 가능한 기호 파일](https://github.com/dotnet/core/blob/master/Documentation/diagnostics/portable_pdb.md)(`*.pdb`)만 지원합니다.
>
> .NET 라이브러리를 디버그할 때 NuGet.org 기호 서버를 사용하려면 개발자에게 Visual Studio 2017 15.9 이상이 있어야 합니다.

기호 패키지를 만드는 대신 기본 NuGet 패키지에 기호 파일을 포함시킬 수 있습니다. 기본 NuGet 패키지는 더 클 것이지만 포함된 기호 파일은 개발자가 NuGet.org 기호 서버를 구성할 필요가 없음을 의미합니다. SDK 스타일 프로젝트를 사용하여 NuGet 패키지를 빌드하는 경우 `AllowedOutputExtensionsInPackageBuildOutputFolder` 속성을 설정하여 기호 파일을 포함시킬 수 있습니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">
 <PropertyGroup>
    <!-- Include symbol files (*.pdb) in the built .nupkg -->
    <AllowedOutputExtensionsInPackageBuildOutputFolder>$(AllowedOutputExtensionsInPackageBuildOutputFolder);.pdb</AllowedOutputExtensionsInPackageBuildOutputFolder>
  </PropertyGroup>
</Project>
```

포함된 기호 파일의 단점은 SDK 스타일 프로젝트를 사용하여 컴파일된 .NET 라이브러리의 패키지 크기가 약 30% 증가한다는 것입니다. 패키지 크기가 중요한 경우 기호 패키지에 기호를 게시해야 합니다.

**✔️ CONSIDER** NuGet.org에 기호 패키지(`*.snupkg`)로 기호 게시

> 기호 패키지(`*.snupkg`)는 주 패키지 크기를 블로트하지 않고 NuGet 패키지를 디버그할 의도가 없는 개발자에게 복원 성능에 영향을 주지 않으면서 개발자에게 좋은 주문형 디버깅 환경을 제공합니다.
>
> 중요한 점은 기호 파일을 가져오기 위해 사용자가 해당 IDE에서 NuGet 기호 서버를 찾아(한 번 설정으로) 구성해야 한다는 것입니다. Visual Studio 2019 버전 16.1은 기본 기호 서버 목록에 NuGet.org의 기호 서버를 추가했습니다.

>[!div class="step-by-step"]
>[이전](strong-naming.md)
>[다음](dependencies.md)
