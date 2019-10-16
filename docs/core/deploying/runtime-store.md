---
title: 런타임 패키지 저장소
description: 런타임 패키지 저장소를 사용하여 .NET Core에서 사용되는 매니페스트를 대상으로 지정하는 방법을 알아봅니다.
author: bleroy
ms.date: 08/12/2017
ms.custom: seodec18
ms.openlocfilehash: 8a8d2d3298f144347c36c640700a1e578dc14715
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71116541"
---
# <a name="runtime-package-store"></a>런타임 패키지 저장소

.NET Core 2.0부터는 대상 환경의 알려진 패키지 집합을 대상으로 앱을 패키지하고 배포할 수 있습니다. 경우에 따라 더 빠르게 배포하고, 디스크 공간을 더 적게 사용하고, 시작 성능이 향상되는 이점이 있습니다.

이 기능은 패키지가 저장된 디스크의 디렉터리(일반적으로 macOS/Linux의 */usr/local/share/dotnet/store* 및 Windows의 *C:/Program Files/dotnet/store*)에 해당하는 *런타임 패키지 저장소*로 구현됩니다. 이 디렉터리 아래에는 아키텍처 및 [대상 프레임워크](../../standard/frameworks.md)의 하위 디렉터리가 있습니다. 파일 레이아웃은 [NuGet 자산이 디스크에 배치](/nuget/create-packages/supporting-multiple-target-frameworks#framework-version-folder-structure)되는 방식과 비슷합니다.

```
\dotnet
    \store
        \x64
            \netcoreapp2.0
                \microsoft.applicationinsights
                \microsoft.aspnetcore
                ...
        \x86
            \netcoreapp2.0
                \microsoft.applicationinsights
                \microsoft.aspnetcore
                ...
```

*대상 매니페스트* 파일에는 런타임 패키지 저장소의 패키지가 나열됩니다. 개발자는 앱을 게시할 때 이 매니페스트를 대상으로 지정할 수 있습니다. 일반적으로 대상 프로덕션 환경의 소유자가 대상 매니페스트를 제공합니다.

## <a name="preparing-a-runtime-environment"></a>런타임 환경 준비

런타임 환경의 관리자는 런타임 패키지 저장소 및 해당하는 대상 매니페스트를 빌드하여 더 빠르게 배포하고 디스크 공간을 더 적게 사용하도록 앱을 최적화할 수 있습니다.

첫 번째 단계는 런타임 패키지 저장소를 작성하는 패키지가 나열되는 *패키지 저장소 매니페스트*를 만드는 것입니다. 이 파일 형식은 프로젝트 파일 형식(*csproj*)과 호환됩니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <ItemGroup>
    <PackageReference Include="<NUGET_PACKAGE>" Version="<VERSION>" />
    <!-- Include additional packages here -->
  </ItemGroup>
</Project>
```

**예제**

다음 패키지 저장소 매니페스트(*packages.csproj*) 예제는 [`Newtonsoft.Json`](https://www.nuget.org/packages/Newtonsoft.Json/) 및 [`Moq`](https://www.nuget.org/packages/moq/)를 런타임 패키지 저장소에 추가하는 데 사용됩니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
    <PackageReference Include="Moq" Version="4.7.63" />
  </ItemGroup>
</Project>
```

패키지 저장소 매니페스트, 런타임 및 프레임워크에서 `dotnet store`를 실행하여 런타임 패키지 저장소를 프로비전합니다.

```dotnetcli
dotnet store --manifest <PATH_TO_MANIFEST_FILE> --runtime <RUNTIME_IDENTIFIER> --framework <FRAMEWORK>
```

**예제**

```dotnetcli
dotnet store --manifest packages.csproj --runtime win10-x64 --framework netcoreapp2.0 --framework-version 2.0.0
```

명령에서 옵션과 경로를 반복해서 단일 [`dotnet store`](../tools/dotnet-store.md) 명령에 여러 대상 패키지 저장소 매니페스트의 경로를 전달할 수 있습니다.

기본적으로 명령의 출력은 사용자 프로필의 *.dotnet/store* 하위 디렉터리 아래에 있는 패키지 저장소입니다. `--output <OUTPUT_DIRECTORY>` 옵션을 사용하여 다른 위치를 지정할 수 있습니다. 저장소의 루트 디렉터리에는 대상 매니페스트 *artifact.xml* 파일이 있습니다. 게시할 때 이 저장소를 대상으로 지정하고자 하는 앱 작성자가 이 파일을 다운로드하도록 제공하고 사용할 수 있습니다.

**예제**

이전 예제를 실행한 후 다음 *artifact.xml* 파일이 생성됩니다. [`Castle.Core`](https://www.nuget.org/packages/Castle.Core/)는 `Moq`의 종속성이므로 *artifacts.xml* 매니페스트 파일에 자동으로 포함되고 표시됩니다.

```xml
<StoreArtifacts>
  <Package Id="Newtonsoft.Json" Version="10.0.3" />
  <Package Id="Castle.Core" Version="4.1.0" />
  <Package Id="Moq" Version="4.7.63" />
</StoreArtifacts>
```

## <a name="publishing-an-app-against-a-target-manifest"></a>대상 매니페스트에 앱 게시

디스크에 대상 매니페스트 파일이 있는 경우 앱을 게시할 때 [`dotnet publish`](../tools/dotnet-publish.md) 명령을 사용하여 파일 경로를 지정합니다.

```dotnetcli
dotnet publish --manifest <PATH_TO_MANIFEST_FILE>
```

**예제**

```dotnetcli
dotnet publish --manifest manifest.xml
```

대상 매니페스트에 설명된 패키지가 있는 환경에 게시된 결과 앱을 배포합니다. 배포하지 못하면 앱이 시작되지 않습니다.

앱을 게시할 때 옵션과 경로를 반복하여 여러 대상 매니페스트를 지정합니다(예: `--manifest manifest1.xml --manifest manifest2.xml`). 이렇게 하면 명령에 제공되는 대상 매니페스트 파일에 지정된 패키지의 합집합을 기준으로 앱이 트리밍됩니다.

## <a name="specifying-target-manifests-in-the-project-file"></a>프로젝트 파일에서 대상 매니페스트 지정

[`dotnet publish`](../tools/dotnet-publish.md) 명령을 사용하여 대상 매니페스트를 지정하는 대신, 프로젝트 파일에서 **\<TargetManifestFiles>** 태그 아래에 세미콜론으로 구분된 경로 목록으로 대상 매니페스트를 지정할 수 있습니다.

```xml
<PropertyGroup>
  <TargetManifestFiles>manifest1.xml;manifest2.xml</TargetManifestFiles>
</PropertyGroup>
```

.NET Core 프로젝트와 같이 앱의 대상 환경이 잘 알려진 경우에만 프로젝트 파일에서 대상 매니페스트를 지정합니다. 오픈 소스 프로젝트에는 이 방법을 사용할 수 없습니다. 오픈 소스 프로젝트의 사용자는 일반적으로 앱을 다양한 프로덕션 환경에 배포합니다. 이러한 프로덕션 환경에는 대개 여러 가지 패키지 집합이 미리 설치되어 있습니다. 이런 환경에서는 대상 매니페스트에 대한 가정을 세울 수 없으므로 [`dotnet publish`](../tools/dotnet-publish.md)의 `--manifest` 옵션을 사용해야 합니다.

## <a name="aspnet-core-implicit-store"></a>ASP.NET Core 암시적 저장소

ASP.NET Core 암시적 저장소는 ASP.NET Core 2.0에만 적용됩니다. 암시적 저장소를 사용하지 **않는** ASP.NET Core 2.1 이상을 사용하는 애플리케이션을 강력히 권장합니다. ASP.NET Core 2.1 이상에서는 공유 프레임워크를 사용합니다.

런타임 패키지 저장소 기능은 앱이 [FDD(프레임워크 종속 배포)](index.md#framework-dependent-deployments-fdd) 앱으로 배포될 경우 ASP.NET Core 앱에서 암시적으로 사용됩니다. [`Microsoft.NET.Sdk.Web`](https://github.com/aspnet/websdk)의 대상에는 대상 시스템의 암시적 패키지 저장소를 참조하는 매니페스트가 포함됩니다. 또한 `Microsoft.AspNetCore.All` 패키지를 사용하는 FDD 앱은 앱과 자산만 포함되고 `Microsoft.AspNetCore.All` 메타패키지에 나열된 패키지가 포함되지 않은 게시된 앱이 됩니다. 해당 패키지는 대상 시스템에 있는 것으로 가정합니다.

런타임 패키지 저장소는 .NET Core SDK가 설치될 때 호스트에 설치됩니다. 다른 설치 관리자에서는 .NET Core SDK, `apt-get`, Red Hat Yum, .NET Core Windows Server 호스팅 번들의 Zip/tarball 설치와 수동 런타임 패키지 저장소 설치를 포함한 런타임 패키지 저장소를 제공할 수 있습니다.

[FDD(프레임워크 종속 배포)](index.md#framework-dependent-deployments-fdd) 앱을 배포할 경우 대상 환경에 .NET Core SDK가 설치되어 있는지 확인합니다. ASP.NET Core가 포함되지 않은 환경에 앱을 배포할 경우 다음 예제와 같이 프로젝트 파일에서 **\<PublishWithAspNetCoreTargetManifest>** 를 `false`로 지정하여 암시적 저장소를 옵트아웃(opt out)할 수 있습니다.

```xml
<PropertyGroup>
  <PublishWithAspNetCoreTargetManifest>false</PublishWithAspNetCoreTargetManifest>
</PropertyGroup>
```

> [!NOTE]
> [SCD(자체 포함된 배포)](index.md#self-contained-deployments-scd) 앱의 경우 대상 시스템에 필수 매니페스트 패키지가 없어도 되는 것으로 가정합니다. 따라서 SCD 앱의 경우 **\<PublishWithAspNetCoreTargetManifest>** 는 `true`로 설정될 수 없습니다.

배포에 포함되지 않은 매니페스트 종속성을 사용하여 애플리케이션을 배포할 경우(어셈블리가 *bin* 폴더에 있음) 해당 어셈블리의 호스트에서 런타임 패키지 저장소가 *사용되지 않습니다*. *bin* 폴더 어셈블리는 호스트의 런타임 패키지 저장소에 어셈블리가 있는지에 관계없이 사용됩니다.

매니페스트에 지정된 종속성 버전은 런타임 패키지 저장소의 종속성 버전과 일치해야 합니다. 대상 매니페스트의 종속성과 런타임 패키지 저장소에 있는 버전 간에 버전이 일치하지 않고 앱 배포에 필수 패키지 버전이 없는 경우에는 앱이 시작되지 않습니다. 런타임 패키지 저장소 어셈블리에 대해 호출되는 대상 매니페스트의 이름은 예외에 포함되므로 불일치 문제를 해결하는 데 도움이 됩니다.

게시할 때 배포가 *트리밍*될 경우에는 게시된 출력에서 지정한 매니페스트 패키지의 특정 버전만 보류됩니다. 앱을 시작하려면 지정된 버전의 패키지가 호스트에 있어야 합니다.

## <a name="see-also"></a>참고 항목

- [dotnet-publish](../tools/dotnet-publish.md)
- [dotnet-store](../tools/dotnet-store.md)
