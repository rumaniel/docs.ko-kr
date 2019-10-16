---
title: 패키지, 메타패키지 및 프레임워크 - .NET Core
description: 패키지, 메타패키지 및 프레임워크 용어에 관해 알아봅니다.
author: richlander
ms.date: 06/20/2016
ms.custom: seodec18
ms.openlocfilehash: 7b019686df195a8cebdce126f7a0b2d22548dc0e
ms.sourcegitcommit: 992f80328b51b165051c42ff5330788627abe973
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72275759"
---
# <a name="packages-metapackages-and-frameworks"></a>패키지, 메타패키지 및 프레임워크

.NET Core는 NuGet 패키지로 구성된 플랫폼입니다. 일부 제품은 정교하게 정의된 패키지로 구성되는 반면 다른 제품은 다소 거칠게 정의된 패키지로 구성됩니다. 이러한 이중성을 수용하기 위해 이 제품은 세분화된 패키지 집합으로 배포되고 비공식적으로 [메타패키지](#metapackages)라고 하는 패키지 형식의 거친 덩어리 상태입니다.

각 .NET Core 패키지는 프레임워크라고 하는 여러 .NET 구현에서의 실행을 지원합니다. 그러한 프레임워크 중 일부는 `net46`처럼 .NET Framework를 나타내는 기존의 프레임워크입니다. 또 다른 집합은 "패키지 기반 프레임워크"로 간주할 수 있는 새로운 프레임워크로, 프레임워크를 정의하기 위한 새 모델을 설정합니다. 이러한 패키지 기반 프레임워크는 패키지로서 완전히 구성 및 정의되어, 패키지와 프레임워크 간에 강력한 관계를 형성합니다.

## <a name="packages"></a>패키지

.NET Core는 기본 형식, 더 높은 수준의 데이터 형식, 앱 구성 형식 및 공통 유틸리티를 제공하는 패키지 집합으로 나누어집니다. 이러한 각 패키지는 동일한 이름의 단일 어셈블리를 나타냅니다. 예를 들어 [System.Runtime](https://www.nuget.org/packages/System.Runtime)은 System.Runtime.dll을 포함합니다. 

세분화된 방식으로 패키지를 정의하는 데 따른 이점이 있습니다.

- 세분화된 패키지는 비교적 제한적으로 타 패키지를 테스트하며 자체 일정으로 출시될 수 있습니다.
- 세분화된 패키지는 다른 OS 및 CPU 지원을 제공할 수 있습니다.
- 세분화된 패키지는 하나의 라이브러리에 대한 종속성을 가질 수 있습니다.
- 참조되지 않은 패키지는 앱 배포에 포함되지 않으므로 앱의 크기가 더 작습니다.

이러한 혜택 중 일부는 특정 상황에서만 사용됩니다. 예를 들어 .NET Core 패키지는 일반적으로 동일한 플랫폼 지원과 함께 동일한 일정으로 출시됩니다. 서비스의 경우 수정은 작은 단일 패키지 업데이트로서 배포 및 설치될 수 있습니다. 변경 범위가 좁기 때문에 수정을 준비하는 시간과 유효성 검사는 단일 라이브러리에 필요한 것으로 제한됩니다.

다음은 .NET Core용 핵심 NuGet 패키지의 목록입니다.

- [System.Runtime](https://www.nuget.org/packages/System.Runtime) - 가장 기본적인 .NET Core 패키지로, <xref:System.Object>, <xref:System.String>, <xref:System.Array>, <xref:System.Action> 및 <xref:System.Collections.Generic.IList%601>를 포함합니다.
- [System.Collections](https://www.nuget.org/packages/System.Collections) - 주로 제네릭 컬렉션 집합으로, <xref:System.Collections.Generic.List%601> 및 <xref:System.Collections.Generic.Dictionary%602>를 포함합니다.
- [System.Net.Http](https://www.nuget.org/packages/System.Net.Http) - HTTP 네트워크 통신에 대한 형식의 집합으로, <xref:System.Net.Http.HttpClient> 및 <xref:System.Net.Http.HttpResponseMessage>를 포함합니다.
- [System.IO.FileSystem](https://www.nuget.org/packages/System.IO.FileSystem) - 로컬 또는 네트워크 디스크 기반 스토리지에 대한 읽기 및 쓰기를 위한 형식 집합으로, <xref:System.IO.File> 및 <xref:System.IO.Directory>를 포함합니다.
- [System.Linq](https://www.nuget.org/packages/System.Linq) - 개체 쿼리를 위한 형식 집합으로, `Enumerable` 및 <xref:System.Linq.ILookup%602>를 포함합니다.
- [System.Reflection](https://www.nuget.org/packages/System.Reflection) - 형식의 로드, 검사 및 활성화를 위한 형식의 집합으로, <xref:System.Reflection.Assembly>, <xref:System.Reflection.TypeInfo> 및 <xref:System.Reflection.MethodInfo>를 포함합니다.

일반적으로 각 패키지를 포함하는 것보다 [메타패키지](#metapackages)를 포함하기가 좀 더 쉽고 강력합니다. 그러나 단일 패키지가 필요한 경우 [System.Runtime](https://www.nuget.org/packages/System.Runtime/) 패키지를 참조하는 다음 예제에서처럼 포함할 수 있습니다. 

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard1.6</TargetFramework>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="System.Runtime" Version="4.3.0" />
  </ItemGroup>
</Project>
```

## <a name="metapackages"></a>메타패키지

메타패키지는 서로 의미가 있는 패키지 집합을 기술하기 위한 NuGet 패키지 규칙입니다. 메타패키지는 종속성을 설정함으로써 이러한 패키지 집합을 나타냅니다. 선택적으로, 프레임워크를 지정하여 이 패키지 집합에 대한 프레임워크를 설정할 수 있습니다. 

이전 버전의 .NET Core 도구(project.json 및 csproj 기반 도구)는 기본적으로 프레임워크와 메타패키지를 모두 지정했습니다. 그러나 현재 메타패키지는 암시적으로 대상 프레임워크에서 참조하므로 각 메타패키지는 대상 프레임워크에 연결됩니다. 예를 들어 `netstandard1.6` 프레임워크는 NetStandard.Library 버전 1.6.0 메타패키지를 참조합니다. 마찬가지로 `netcoreapp2.1` 프레임워크는 Microsoft.NETCore.App 버전 2.1.0 메타패키지를 참조합니다. 자세한 내용은 [Implicit metapackage package reference in the .NET Core SDK](https://github.com/dotnet/core/blob/master/release-notes/1.0/sdk/1.0-rc3-implicit-package-refs.md)(.NET Core SDK에서 암시적인 메타패키지 패키지 참조)를 참조하세요.

프레임워크 대상을 지정하고 메타패키지를 암시적으로 참조함으로써 각각의 종속된 패키지에 단일 제스처로서 참조를 추가하게 됩니다. 즉, IntelliSense(또는 유사한 환경) 및 앱 게시에 대해 해당 패키지의 모든 라이브러리를 사용할 수 있습니다.  

메타패키지 사용에 따른 이점이 있습니다.

- 세분화된 패키지의 큰 집합을 참조하기 위한 편리한 사용자 환경을 제공합니다. 
- 테스트되고 함께 잘 작동하는 패키지 집합을 정의합니다(특정 버전 포함).

.NET 표준 메타패키지:

- [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library) - ".NET 표준"에 포함된 라이브러리를 설명합니다. .NET 표준을 지원하는 모든 .NET 구현(예: .NET Framework, .NET Core 및 Mono)에 적용됩니다. 'netstandard' 프레임워크를 설정합니다.

주요 .NET Core 메타패키지:

- [Microsoft.NETCore.App](https://www.nuget.org/packages/Microsoft.NETCore.App) - .NET Core 배포에 포함된 라이브러리를 설명합니다. [`.NETCoreApp` 프레임워크를 설정합니다](https://github.com/dotnet/core-setup/blob/release/1.1.0/pkg/projects/Microsoft.NETCore.App/Microsoft.NETCore.App.pkgproj). 더 작은 `NETStandard.Library`에 종속됩니다.
- [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App) - 타사 종속성을 포함하는 패키지를 제외하고 ASP.NET Core 및 Entity Framework Core의 모든 지원되는 패키지를 포함합니다. 자세한 내용은 [ASP.NET Core에 대한 Microsoft.AspNetCore.App 메타패키지](/aspnet/core/fundamentals/metapackage-app)를 참조하세요.
- [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) - ASP.NET Core, Entity Framework Core 및 ASP.NET Core와 Entity Framework Core에서 사용되는 내부/타사 종속성의 모든 지원되는 패키지를 포함합니다. 자세한 내용은 [ASP.NET Core 2.x에 대한 Microsoft.AspNetCore.All 메타패키지](/aspnet/core/fundamentals/metapackage)를 참조하세요.
- [Microsoft.NETCore.Portable.Compatibility](https://www.nuget.org/packages/Microsoft.NETCore.Portable.Compatibility) - .NET Core에서 실행되는 mscorlib 기반 PCL(이식 가능한 클래스 라이브러리)을 사용하도록 설정하는 호환성 외관의 집합입니다.

## <a name="frameworks"></a>프레임워크

각 .NET Core 패키지는 런타임 프레임워크 집합을 지원합니다. 프레임워크는 사용 가능한 API 집합(및 기타 가능한 특성)을 설명하며, 이러한 집합은 특정 프레임워크를 대상으로 할 때 사용할 수 있습니다. 새 API가 추가될 때 버전이 지정됩니다.

예를 들어 [System.IO.FileSystem](https://www.nuget.org/packages/System.IO.FileSystem)은 다음 프레임워크를 지원합니다.

- .NETFramework,Version=4.6
- .NETStandard,Version=1.3
- 6개 Xamarin 플랫폼(예: xamarinios10)

처음 두 프레임워크는 프레임워크를 정의하는 두 가지 방법의 예를 보여주므로 대조해보면 유용합니다.

`.NETFramework,Version=4.6` 프레임워크는 .NET Framework 4.6의 사용 가능한 API를 나타냅니다. .NET Framework 4.6 참조 어셈블리로 컴파일된 라이브러리를 생성하고 net46 lib 폴더의 NuGet 패키지에 배포할 수 있습니다. 이는 .NET Framework 4.6을 대상으로 하거나 이와 호환되는 앱에 사용됩니다. 모든 프레임워크는 지금까지 이러한 방식으로 작동했습니다.

`.NETStandard,Version=1.3` 프레임워크는 패키지 기반 프레임워크로서, API를 정의하고 노출하는 프레임워크를 대상으로 하는 패키지에 의존합니다.

## <a name="package-based-frameworks"></a>패키지 기반 프레임워크

프레임워크와 패키지 간에 양방향 관계가 있습니다. 첫 번째 부분은 특정 프레임워크(예: `netstandard1.3`)에 사용 가능한 API를 정의하는 것입니다. `netstandard1.3`(또는 `netstandard1.0`과 같은 호환되는 프레임워크)을 대상으로 하는 패키지는 `netstandard1.3`에 사용 가능한 API를 정의합니다. 순환 정의처럼 들릴 수 있지만 그렇지 않습니다. "패키지 기반" 덕분에 프레임워크의 API 정의는 패키지에서 옵니다. 프레임워크 자체는 API를 정의하지 않습니다.

관계의 두 번째 부분은 자산 선택입니다. 패키지는 여러 프레임워크에 대한 자산을 포함할 수 있습니다. 패키지 및/또는 메타패키지 집합에 대한 참조를 고려하여, 프레임워크는 어떤 자산을 선택할지를 결정해야 합니다(예: `net46` 또는 `netstandard1.3`). 올바른 자산을 선택하는 것이 중요합니다. 예를 들어 한 `net46` 자산은 .NET Framework 4.0 또는 .NET Core 1.0과 호환될 것 같지 않습니다.

다음 이미지에서 이 관계를 볼 수 있습니다. *API*는 *프레임워크*를 대상으로 하고 정의합니다. *프레임워크*는 *자산 선택*에 사용됩니다. *자산*은 API를 제공합니다.

![패키지 기반 프레임워크 구성](./media/packages/package-framework.png)

.NET Core와 사용되는 두 가지 기본 패키지 기반 프레임워크는 다음과 같습니다.

- `netstandard`
- `netcoreapp`

### <a name="net-standard"></a>.NET Standard

.NET Standard([대상 프레임워크 모니커](../standard/frameworks.md): `netstandard`) 프레임워크는 [.NET Standard](../standard/net-standard.md)에 의해 정의되고 그 위에 빌드되는 API를 나타냅니다. 여러 런타임에서 실행되도록 만들어진 라이브러리는 이 프레임워크를 대상으로 하며, .NET Core, .NET Framework 및 Mono/Xamarin 같은 .NET 표준 호환 런타임에서 지원됩니다. 이러한 각 런타임은 구현하는 API에 따라 .NET 표준 버전 집합을 지원합니다.

`netstandard` 프레임워크는 [`NETStandard.Library`](https://www.nuget.org/packages/NETStandard.Library) 메타패키지를 암시적으로 참조합니다. 예를 들어 다음 MSBuild 프로젝트 파일은 프로젝트가 [`NETStandard.Library` 버전 1.6](https://www.nuget.org/packages/NETStandard.Library/1.6.0) 메타패키지를 참조하는 `netstandard1.6`을 대상으로 지정함을 나타냅니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard1.6</TargetFramework>
  </PropertyGroup>
</Project>
```

그러나 프로젝트 파일의 프레임워크 및 메타패키지 참조는 일치할 필요가 없으며, 프로젝트 파일에서 `<NetStandardImplicitPackageVersion>` 요소를 사용하여 메타패키지 버전보다 낮은 프레임워크 버전을 지정할 수 있습니다. 예를 들어, 다음 프로젝트 파일은 유효합니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard1.3</TargetFramework>
    <NetStandardImplicitPackageVersion>1.6.0</NetStandardImplicitPackageVersion>
  </PropertyGroup>
</Project>
```

`netstandard1.3`을 대상으로 하지만 `NETStandard.Library`의 1.6.0 버전을 사용하는 것이 이상하게 보일 수 있습니다. 메타패키지가 이전 `netstandard` 버전에 대한 지원을 유지하므로 이는 유효한 사용 사례입니다. 메타패키지의 1.6.0 버전에서 표준화하고 모든 라이브러리에 사용하여 다양한 `netstandard` 버전을 대상으로 하는 사례일 수 있습니다. 이 방법을 통해 `NETStandard.Library` 1.6.0만을 복원할 수 있으며 그 이전 버전은 복원할 수 없습니다. 

`NETStandard.Library`의 1.3.0 버전으로 `netstandard1.6`를 대상으로 하는 반대의 경우는 유효하지 않습니다. 더 낮은 메타패키지로 더 높은 프레임워크를 대상으로 할 수 없습니다. 더 낮은 버전의 메타패키지는 더 높은 프레임워크의 자산을 노출하지 않기 때문입니다. 메타패키지의 버전 관리 체계는 메타패키지가 프레임워크의 최고 버전과 일치해야 한다고 주장합니다. 버전 관리 체계 덕분에, `netstandard1.6` 자산을 포함하는 경우 `NETStandard.Library`의 첫 번째 버전은 v1.6.0입니다. 위의 예제에는 v1.3.0이 사용되지만(위 예제와 대칭을 위해), 실제로 존재하지는 않습니다.

### <a name="net-core-application"></a>.NET Core 애플리케이션

.NET Core([대상 프레임워크 모니커](../standard/frameworks.md): `netcoreapp`) 프레임워크는 .NET Core 배포와 함께 제공되는 패키지 및 관련 API, 그리고 콘솔 애플리케이션 모델을 나타냅니다. .NET Core 앱은 콘솔 애플리케이션 모델을 대상으로 하기 때문에 이 프레임워크를 사용해야 하며, .NET Core에서만 실행되도록 만들어진 라이브러리도 마찬가지입니다. 이 프레임워크를 사용하면 앱과 라이브러리의 실행이 .NET Core로만 제한됩니다. 

`Microsoft.NETCore.App` 메타패키지는 `netcoreapp` 프레임워크를 대상으로 합니다. 최대 60개 라이브러리, `NETStandard.Library` 패키지에서 제공하는 최대 40개 및 추가 20개에 대한 액세스를 제공합니다. 추가 API에 대한 액세스 권한을 얻기 위해 `netcoreapp` 또는 호환 프레임워크(예: `netstandard`)를 대상으로 하는 추가 라이브러리를 참조할 수 있습니다. 

다른 `netstandard` 라이브러리에서 종속성을 충족하는 경우 `Microsoft.NETCore.App`에서 제공하는 추가 라이브러리 대부분은 또한 `netstandard`를 대상으로 합니다. 즉, `netstandard` 라이브러리 역시 해당 패키지를 종속성으로 참조할 수 있습니다. 
