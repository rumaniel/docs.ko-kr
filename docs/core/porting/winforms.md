---
title: .NET Core 3.0에 Windows Forms 앱 포팅
description: Windows용 .NET Core 3.0에 .NET Framework Windows Forms 애플리케이션을 포팅하는 방법을 설명합니다.
author: Thraka
ms.author: adegeo
ms.date: 03/01/2019
ms.custom: ''
ms.openlocfilehash: 7480c86af1acd482adff5e3e24dc229f24af0e5b
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216323"
---
# <a name="how-to-port-a-windows-forms-desktop-app-to-net-core"></a>방법: .NET Core에 Windows Forms 데스크톱 앱 포팅

이 문서에서는 .NET Framework에서 .NET Core 3.0으로 Windows Forms 기반 데스크톱 앱을 포팅하는 방법을 설명합니다. .NET Core 3.0 SDK는 Windows Forms 애플리케이션을 지원합니다. Windows Forms는 Windows 전용 프레임워크이고 Windows에서만 실행됩니다. 이 예제에서는 .NET Core SDK CLI를 사용하여 프로젝트를 만들고 관리합니다.

이 문서에서는 마이그레이션에 사용되는 파일의 유형을 식별하기 위해 다양한 이름이 사용됩니다. 프로젝트를 마이그레이션할 때 파일 이름이 다르게 지정되므로 파일을 아래 나열된 파일과 대조합니다.

| 파일 | 설명 |
| ---- | ----------- |
| **MyApps.sln** | 솔루션 파일의 이름입니다. |
| **MyForms.csproj** | 포팅할 .NET Framework Windows Forms 프로젝트의 이름입니다. |
| **MyFormsCore.csproj** | 만들 새 .NET Core 프로젝트의 이름입니다. |
| **MyAppCore.exe** | .NET Core Windows Forms 앱 실행 파일입니다. |

## <a name="prerequisites"></a>전제 조건

- 수행할 디자이너 작업용 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)

  다음 Visual Studio 워크로드를 설치합니다.
  - .NET 데스크톱 개발
  - .NET 플랫폼 간 개발

- 문제없이 빌드 및 실행되는 솔루션의 작업 Windows Forms 프로젝트.
- 프로젝트는 C#으로 코딩되어야 합니다. 
- 최신 [.NET Core 3.0](https://aka.ms/netcore3download) 미리 보기를 설치합니다.

>[!NOTE]
>**Visual Studio 2017**은 .NET Core 3.0 프로젝트를 지원하지 않습니다. **Visual Studio 2019**는 .NET Core 3.0 프로젝트를 지원하지만, .NET Core 3.0 Windows Forms 프로젝트의 비주얼 디자이너는 아직 지원하지 않습니다. 비주얼 디자이너를 사용하려면 .NET Core 프로젝트와 양식 파일을 공유하는 .NET Windows Forms 프로젝트가 솔루션에 있어야 합니다.

### <a name="consider"></a>Consider

.NET Framework Windows Forms 애플리케이션을 포팅할 때 몇 가지 항목을 고려해야 합니다.

01. 애플리케이션이 마이그레이션에 적합한 후보인지 확인합니다.

    [.NET 이식성 분석기](../../standard/analyzers/portability-analyzer.md)를 사용하여 프로젝트가 .NET Core 3.0으로 마이그레이션되는지 확인합니다. 프로젝트에 .NET Core 3.0 관련 문제가 있는 경우 분석기는 해당 문제를 식별하는 데 도움이 됩니다.

01. 다른 버전의 Windows Forms를 사용 중입니다.

    .NET Core 3.0 미리 보기 1이 릴리스될 때 Windows Forms가 GitHub에서 오픈 소스로 전환되었습니다. .NET Core Windows Forms의 코드는 .NET Framework Windows Forms 코드베이스의 포크입니다. 몇 가지 차이가 있을 수 있고 앱은 포팅되지 않습니다.

01. [Windows 호환성 팩][compat-pack]이 마이그레이션하는 데 도움이 될 수 있습니다.

    .NET Framework에서 사용할 수 있는 일부 API는 .NET Core 3.0에서 사용할 수 없습니다. [Windows 호환성 팩][compat-pack]은 이와 같은 다양한 API를 추가하며, Windows Forms 앱이 .NET Core와 호환되도록 도와줍니다.

01. 프로젝트에서 사용되는 NuGet 패키지를 업데이트합니다.

    마이그레이션하기 전에 항상 NuGet 패키지의 최신 버전을 사용하는 것이 좋습니다. 애플리케이션이 NuGet 패키지를 참조하는 경우 최신 버전으로 업데이트합니다. 애플리케이션이 성공적으로 빌드되었는지 확인합니다. 업그레이드한 후 패키지 오류가 있는 경우에는 코드를 중단하지 않는 최신 버전으로 패키지를 다운그레이드합니다.

01. Visual Studio 2019는 .NET Core 3.0용 Forms 디자이너를 아직 지원하지 않습니다.

    현재 Visual Studio에서 Forms 디자이너를 사용하려면 기존 .NET Framework Windows Forms 프로젝트 파일을 유지해야 합니다.

## <a name="create-a-new-sdk-project"></a>새 SDK 프로젝트 만들기

만들려는 새 .NET Core 3.0 프로젝트는 .NET Framework 프로젝트와 다른 디렉터리에 있어야 합니다. 둘 다 동일한 디렉터리에 있는 경우 **obj** 디렉터리에서 생성된 파일과 충돌할 수 있습니다. 이 예제에서는 **SolutionFolder** 디렉터리에 **MyFormsAppCore**라는 디렉터리를 만듭니다.

```
SolutionFolder
├───MyApps.sln
├───MyFormsApp
│   └───MyForms.csproj
└───MyFormsAppCore      <--- New folder for core project
```

그런 다음, **MyFormsAppCore** 디렉터리에 **MyFormsCore.csproj** 프로젝트를 만들어야 합니다. 선택한 텍스트 편집기를 사용하여 이 파일을 수동으로 만들 수 있습니다. 다음 XML에 붙여넣습니다.

```xml
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>netcoreapp3.0</TargetFramework>
    <UseWindowsForms>true</UseWindowsForms>
  </PropertyGroup>

</Project>
```

프로젝트 파일을 수동으로 만들지 않으려면 Visual Studio 또는 .NET Core SDK를 사용하여 프로젝트를 생성하면 됩니다. 그러나 프로젝트 파일을 제외하고 프로젝트 템플릿에서 생성된 다른 모든 파일을 삭제해야 합니다. SDK를 사용하려면 **SolutionFolder** 디렉터리에서 다음 명령을 실행합니다.

```dotnetcli
dotnet new winforms -o MyFormsAppCore -n MyFormsCore
```

**MyFormsCore.csproj**를 만든 후 디렉터리 구조는 다음과 같이 표시되어야 합니다.

```
SolutionFolder
├───MyApps.sln
├───MyFormsApp
│   └───MyForms.csproj
└───MyFormsAppCore
    └───MyFormsCore.csproj
```

**SolutionFolder** 디렉터리에서 Visual Studio 또는 .NET Core CLI를 사용하여 **MyFormsCore.csproj** 프로젝트를 **MyApps.sln**에 추가하려고 합니다.

```dotnetcli
dotnet sln add .\MyFormsAppCore\MyFormsCore.csproj
```

## <a name="fix-assembly-info-generation"></a>어셈블리 정보 생성 수정

.NET Framework로 만든 Windows Forms 프로젝트에는 생성할 어셈블리 버전과 같은 어셈블리 특성을 포함하는 `AssemblyInfo.cs` 파일이 포함됩니다. SDK 스타일 프로젝트는 SDK 프로젝트 파일을 기반으로 이 정보를 자동으로 생성합니다. 두 유형의 “어셈블리 정보”가 모두 있으면 충돌이 발생합니다. 자동 생성을 비활성화하여 이 문제를 해결합니다. 그러면 프로젝트가 기존 `AssemblyInfo.cs` 파일을 강제로 사용합니다.

기본 `<PropertyGroup>` 노드에 추가할 세 가지 설정이 있습니다. 

- **GenerateAssemblyInfo**\
이 속성을 `false`로 설정하면 어셈블리 특성이 생성되지 않습니다. 따라서 .NET Framework 프로젝트의 기존 `AssemblyInfo.cs` 파일과 충돌하지 않습니다.

- **AssemblyName**\
이 속성 값은 컴파일할 때 생성되는 출력 이진입니다. 이름에 확장명을 추가할 필요가 없습니다. 예를 들어 `MyCoreApp`을 사용하면 `MyCoreApp.exe`가 생성됩니다.

- **RootNamespace**\
프로젝트에서 사용되는 기본 네임스페이스입니다. 이 네임스페이스는 .NET Framework 프로젝트의 기본 네임스페이스와 일치해야 합니다.

`MyFormsCore.csproj` 파일의 `<PropertyGroup>` 노드에 다음 세 개의 요소를 추가합니다.

```xml
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>netcoreapp3.0</TargetFramework>
    <UseWindowsForms>true</UseWindowsForms>

    <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
    <AssemblyName>MyCoreApp</AssemblyName>
    <RootNamespace>WindowsFormsApp1</RootNamespace>
  </PropertyGroup>

</Project>
```

## <a name="add-source-code"></a>소스 코드 추가

현재는 **MyFormsCore.csproj** 프로젝트가 코드를 컴파일하지 않습니다. 기본적으로 .NET Core 프로젝트는 현재 디렉터리 및 자식 디렉터리에 있는 모든 소스 코드를 자동으로 포함합니다. 상대 경로를 사용하여 .NET Framework 프로젝트의 코드를 포함하도록 프로젝트를 구성해야 합니다. .NET Framework 프로젝트가 양식의 아이콘과 리소스에 **.resx** 파일을 사용한 경우 해당 파일도 포함해야 합니다. 

다음 `<ItemGroup>` 노드를 프로젝트에 추가합니다. 각 문에는 자식 디렉터리를 포함하는 파일 GLOB 패턴이 포함됩니다.

```xml
  <ItemGroup>
    <Compile Include="..\MyFormsApp\**\*.cs" />
    <EmbeddedResource Include="..\MyFormsApp\**\*.resx" />
  </ItemGroup>
```

또는 .NET Framework 프로젝트의 각 파일에 대해 `<Compile>` 또는 `<EmbeddedResource>` 항목을 만들 수 있습니다.

## <a name="add-nuget-packages"></a>NuGet 패키지 추가

.NET Framework 프로젝트에서 참조하는 각 NuGet 패키지를 .NET Core 프로젝트에 추가합니다. 

대부분의 경우 .NET Framework Windows Forms 앱에는 프로젝트에서 참조하는 모든 NuGet 패키지의 목록을 포함하는 **packages.config** 파일이 있습니다. 이 목록을 보고 .NET Core 프로젝트에 추가할 NuGet 패키지를 결정할 수 있습니다. 예를 들어 .NET Framework 프로젝트가 `MetroFramework`, `MetroFramework.Design` 및 `MetroFramework.Fonts` NuGet 패키지를 참조한 경우 Visual Studio를 사용하거나 **SolutionFolder** 디렉터리에서 .NET Core CLI를 사용하여 프로젝트에 각 NuGet 패키지를 추가합니다.

```dotnetcli
dotnet add .\MyFormsAppCore\MyFormsCore.csproj package MetroFramework
dotnet add .\MyFormsAppCore\MyFormsCore.csproj package MetroFramework.Design
dotnet add .\MyFormsAppCore\MyFormsCore.csproj package MetroFramework.Fonts
```

이전 명령은 **MyFormsCore.csproj** 프로젝트에 다음 NuGet 참조를 추가합니다.

```xml
  <ItemGroup>
    <PackageReference Include="MetroFramework" Version="1.2.0.3" />
    <PackageReference Include="MetroFramework.Design" Version="1.2.0.3" />
    <PackageReference Include="MetroFramework.Fonts" Version="1.2.0.3" />
  </ItemGroup>
```

## <a name="port-control-libraries"></a>컨트롤 라이브러리 포팅

포팅할 Windows Forms 컨트롤 라이브러리 프로젝트가 있는 경우 일부 설정을 제외하고 지침은 .NET Framework Windows Forms 앱 프로젝트를 포팅하는 것과 같습니다. 또한 실행 파일로 컴파일하는 대신 라이브러리로 컴파일합니다. 소스 코드를 포함하는 파일 GLOB 경로 외에 실행 가능 프로젝트와 라이브러리 프로젝트 간 차이는 최소화됩니다.

이전 단계의 예제를 사용하여 작업 중인 프로젝트 및 파일을 확장해 보겠습니다.

| 파일 | 설명 |
| ---- | ----------- |
| **MyApps.sln** | 솔루션 파일의 이름입니다. |
| **MyControls.csproj** | 포팅할 .NET Framework Windows Forms 컨트롤 프로젝트의 이름입니다. |
| **MyControlsCore.csproj** | 만들려는 새 .NET Core 라이브러리 프로젝트의 이름입니다. |
| **MyCoreControls.dll** | .NET Core Windows Forms 컨트롤 라이브러리입니다. |

```
SolutionFolder
├───MyApps.sln
├───MyFormsApp
│   └───MyForms.csproj
├───MyFormsAppCore
│   └───MyFormsCore.csproj
│
├───MyFormsControls
│   └───MyControls.csproj
└───MyFormsControlsCore
    └───MyControlsCore.csproj   <--- New project for core controls
```

`MyControlsCore.csproj` 프로젝트와 이전에 만든 `MyFormsCore.csproj` 프로젝트 간 차이를 고려합니다.

```diff
 <Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">

   <PropertyGroup>
-    <OutputType>WinExe</OutputType>
     <TargetFramework>netcoreapp3.0</TargetFramework>
     <UseWindowsForms>true</UseWindowsForms>

     <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
-    <AssemblyName>MyCoreApp</AssemblyName>
-    <RootNamespace>WindowsFormsApp1</RootNamespace>
+    <AssemblyName>MyControlsCore</AssemblyName>
+    <RootNamespace>WindowsFormsControlLibrary1</RootNamespace>
   </PropertyGroup>

   <ItemGroup>
-    <Compile Include="..\MyFormsApp\**\*.cs" />
-    <EmbeddedResource Include="..\MyFormsApp\**\*.resx" />
+    <Compile Include="..\MyFormsControls\**\*.cs" />
+    <EmbeddedResource Include="..\MyFormsControls\**\*.resx" />
   </ItemGroup>

 </Project>
```

.NET Core Windows Forms 컨트롤 라이브러리 프로젝트 파일이 표시되는 예는 다음과 같습니다.

```xml
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">

  <PropertyGroup>
    
    <TargetFramework>netcoreapp3.0</TargetFramework>
    <UseWindowsForms>true</UseWindowsForms>

    <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
    <AssemblyName>MyCoreControls</AssemblyName>
    <RootNamespace>WindowsFormsControlLibrary1</RootNamespace>
  </PropertyGroup>
  
  <ItemGroup>
    <Compile Include="..\MyFormsControls\**\*.cs" />
    <EmbeddedResource Include="..\MyFormsControls\**\*.resx" />
  </ItemGroup>
  
</Project>
```

확인한 것처럼 `<OutputType>` 노드가 제거되어 기본적으로 컴파일러가 실행 파일 대신 라이브러리를 생성합니다. `<AssemblyName>` 및 `<RootNamespace>`가 변경되었습니다. 특히 `<RootNamespace>`는 포팅할 Windows Forms 컨트롤 라이브러리의 네임스페이스와 일치해야 합니다. 마지막으로 `<Compile>` 및 `<EmbeddedResource>` 노드는 포팅할 Windows Forms 컨트롤 라이브러리의 폴더를 가리키도록 조정되었습니다.

다음으로, 기본 .NET Core **MyFormsCore.csproj** 프로젝트에서 새 .NET Core Windows Forms 컨트롤 라이브러리에 참조를 추가합니다. Visual Studio를 사용하거나 **SolutionFolder** 디렉터리에서 .NET Core CLI를 사용하여 참조를 추가합니다.

```dotnetcli
dotnet add .\MyFormsAppCore\MyFormsCore.csproj reference .\MyFormsControlsCore\MyControlsCore.csproj
```

이전 명령은 **MyFormsCore.csproj** 프로젝트에 다음을 추가합니다.

```xml
  <ItemGroup>
    <ProjectReference Include="..\MyFormsControlsCore\MyControlsCore.csproj" />
  </ItemGroup>
```

## <a name="problems-compiling"></a>컴파일 문제

프로젝트를 컴파일하는 데 문제가 있는 경우 .NET Framework에서 사용할 수 있지만 .NET Core에서는 사용할 수 없는 일부 Windows 전용 API를 사용하고 있는 것일 수 있습니다. [Windows 호환성 팩][compat-pack] NuGet 패키지를 프로젝트에 추가해 볼 수 있습니다. 이 패키지는 Windows에서만 실행되고 .NET Core 및 .NET Standard 프로젝트에 20,000개 정도의 Windows API를 추가합니다.

```dotnetcli
dotnet add .\MyFormsAppCore\MyFormsCore.csproj package Microsoft.Windows.Compatibility
```

이전 명령은 **MyFormsCore.csproj** 프로젝트에 다음을 추가합니다.

```xml
  <ItemGroup>
    <PackageReference Include="Microsoft.Windows.Compatibility" Version="2.0.1" />
  </ItemGroup>
```

## <a name="windows-forms-designer"></a>Windows Forms 디자이너

이 문서에 설명된 대로, Visual Studio 2019만 .NET Framework 프로젝트의 Forms 디자이너를 지원합니다. 동시에 .NET Core 프로젝트를 만들면 .NET Framework 프로젝트를 사용하여 양식을 디자인하는 동안 .NET Core를 사용하여 프로젝트를 테스트할 수 있습니다. 솔루션 파일에는 .NET Framework 및 .NET Core 프로젝트가 모두 포함됩니다. .NET Framework 프로젝트에서 양식과 컨트롤을 추가 및 디자인합니다. 그러면 .NET Core 프로젝트에 추가한 파일 GLOB 패턴을 기반으로 새 파일이나 변경된 파일이 자동으로 .NET Core 프로젝트에 포함됩니다.

Visual Studio 2019가 Windows Forms 디자이너를 지원하면 .NET Core 프로젝트 파일의 콘텐츠를 .NET Framework 프로젝트 파일로 복사하여 붙여넣을 수 있습니다. 그런 다음, `<Source>` 및 `<EmbeddedResource>` 항목과 함께 추가된 파일 GLOB 패턴을 삭제합니다. 앱에서 사용하는 프로젝트 참조의 경로를 수정합니다. 이렇게 하면 .NET Framework 프로젝트가 .NET Core 프로젝트로 효과적으로 업그레이드됩니다.
 
## <a name="next-steps"></a>다음 단계

- [Windows 호환성 팩][compat-pack]에 대해 자세히 알아봅니다.
- .NET Framework Windows Forms 프로젝트를 .NET Core에 [포팅하는 방법에 관한 동영상](https://www.youtube.com/watch?v=upVQEUc_KwU)을 봅니다.

[compat-pack]: windows-compat-pack.md
