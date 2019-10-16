---
title: 대상 프레임워크
description: .NET Core 앱 및 라이브러리의 대상 프레임워크에 대해 알아봅니다.
author: mairaw
ms.author: mairaw
ms.date: 09/23/2019
ms.custom: updateeachrelease
ms.technology: dotnet-standard
ms.openlocfilehash: b05923b293b1a5bb94a69ddd0154f8701b9326b0
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216663"
---
# <a name="target-frameworks"></a>대상 프레임워크

앱 또는 라이브러리에서 프레임워크를 대상으로 지정하면 앱 또는 라이브러리에서 사용할 수 있도록 하려는 API 집합을 지정하는 것입니다. TFM(대상 프레임워크 모니터)을 사용하여 프로젝트 파일에서 대상 프레임워크를 지정합니다.

앱 또는 라이브러리는 [.NET Standard](net-standard.md) 버전을 대상으로 지정할 수 있습니다. .NET Standard 버전은 모든 .NET 구현체에서 사용할 수 있는 표준화된 API 집합을 나타냅니다. 예를 들어 .NET Standard 1.6을 대상으로 하는 라이브러리는 동일한 코드 기반의 .NET Core 및 .NET Framework에서 동작하는 API에 액세스할 수 있습니다.

앱 또는 라이브러리는 특정 .NET 구현체을 대상으로 지정하여 구현체 관련 API에 액세스할 수도 있습니다. 예를 들어 Xamarin.iOS(예: `Xamarin.iOS10`)를 대상으로 하는 앱은 Xamarin에서 제공하는 iOS 10용 iOS API 래퍼에 액세스하고, UWP(유니버설 Windows 플랫폼, `uap10.0`)를 대상으로 하는 앱은 Windows 10이 실행되는 디바이스용으로 컴파일하는 API에 액세스할 수 있습니다.

일부 대상 프레임워크(예: .NET Framework)의 API는 프레임워크에서 시스템에 설치하는 어셈블리에 의해 정의되고 애플리케이션 프레임워크 API(예: ASP.NET)를 포함할 수 있습니다.

패키지 기반 대상 프레임워크(예: .NET Standard 및 .NET Core)에서 API는 앱이나 라이브러리에 포함된 패키지에 의해 정의됩니다. *메타패키지*는 고유한 내용은 없고 종속성(다른 패키지) 목록만 있는 NuGet 패키지입니다. NuGet 패키지 기반 대상 프레임워크는 프레임워크를 구성하는 모든 패키지를 참조하는 메타패키지를 암시적으로 지정합니다.

## <a name="latest-target-framework-versions"></a>최신 대상 프레임워크 버전

다음 표에서는 가장 일반적인 대상 프레임워크, 프레임워크가 참조되는 방법 및 프레임워크에서 구현하는 [.NET Standard](net-standard.md)의 버전을 정의합니다. 이러한 대상 프레임워크 버전은 안정적인 최신 버전입니다. 시험판 버전은 표시되지 않습니다. TFM(대상 프레임워크 모니커)은 .NET 앱 또는 라이브러리의 대상 프레임워크를 지정하기 위해 표준화된 토큰 형식입니다.

| 대상 프레임워크      | 최신 <br/> 안정적인 버전 | TFM(대상 프레임워크 모니커) | 구현된 <br/> .NET 표준 버전 |
| :-------------------: | :-------------------------: | :----------------------------: | :-------------------------------------: |
| .NET Standard         | 2.1                         | netstandard2.1                 | 해당 사항 없음                                     |
| .NET Core             | 3.0                         | netcoreapp3.0                  | 2.1                                     |
| .NET Framework        | 4.8                         | net48                          | 2.0                                     |

## <a name="supported-target-framework-versions"></a>지원되는 대상 프레임워크 버전

대상 프레임워크는 일반적으로 TFM에서 참조됩니다. 다음 표에서는 .NET Core SDK 및 NuGet 클라이언트에서 지원되는 대상 프레임워크를 보여 줍니다. 동일한 항목은 대괄호 내에 표시됩니다. 예를 들어 `win81`은 `netcore451`과 동일한 TFM입니다.

| 대상 프레임워크           | TFM |
| -------------------------- | --- |
| .NET Standard              | netstandard1.0<br>netstandard1.1<br>netstandard1.2<br>netstandard1.3<br>netstandard1.4<br>netstandard1.5<br>netstandard1.6<br>netstandard2.0<br>netstandard2.1 |
| .NET Core                  | netcoreapp1.0<br>netcoreapp1.1<br>netcoreapp2.0<br>netcoreapp2.1<br>netcoreapp2.2<br>netcoreapp3.0 |
| .NET Framework             | net11<br>net20<br>net35<br>net40<br>net403<br>net45<br>net451<br>net452<br>net46<br>net461<br>net462<br>net47<br>net471<br>net472<br>net48 |
| Windows 스토어              | netcore [netcore45]<br>netcore45 [win] [win8]<br>netcore451 [win81] |
| .NET Micro Framework       | netmf |
| Silverlight                | sl4<br>sl5 |
| Windows Phone              | wp [wp7]<br>wp7<br>wp75<br>wp8<br>wp81<br>wpa81 |
| UWP | uap [uap10.0]<br>uap10.0 [win10] [netcore50] |

## <a name="how-to-specify-target-frameworks"></a>대상 프레임워크를 지정하는 방법

대상 프레임워크는 프로젝트 파일에서 지정합니다. 단일 대상 프레임워크를 지정하는 경우 **TargetFramework** 요소를 사용합니다. 다음 콘솔 앱 프로젝트 파일에서는 .NET Core 3.0을 대상 프레임워크로 지정하는 방법을 보여 줍니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.0</TargetFramework>
  </PropertyGroup>

</Project>
```

여러 대상 프레임워크를 지정하는 경우 각 대상 프레임워크에 대한 어셈블리를 조건에 따라 참조할 수 있습니다. 코드에서는 *if-then-else* 로직에 전처리기 기호를 사용하여 해당 어셈블리를 조건에 따라 컴파일할 수 있습니다.

다음 라이브러리 프로젝트 파일은 .NET Standard(`netstandard1.4`)의 API 및 .NET Framework(`net40` 및 `net45`)의 API를 대상으로 합니다. 여러 대상 프레임워크에는 복수형 **TargetFrameworks** 요소를 사용합니다. 라이브러리를 두 개의 .NET Framework TFM에 대해 컴파일하려면 `Condition` 특성에 구현체 관련 패키지를 포함합니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard1.4;net40;net45</TargetFrameworks>
  </PropertyGroup>

  <!-- Conditionally obtain references for the .NET Framework 4.0 target -->
  <ItemGroup Condition=" '$(TargetFramework)' == 'net40' ">
    <Reference Include="System.Net" />
  </ItemGroup>

  <!-- Conditionally obtain references for the .NET Framework 4.5 target -->
  <ItemGroup Condition=" '$(TargetFramework)' == 'net45' ">
    <Reference Include="System.Net.Http" />
    <Reference Include="System.Threading.Tasks" />
  </ItemGroup>

</Project>
```

라이브러리나 앱에서, 조건에 따라 각 대상 프레임워크에 대해 컴파일하는 코드를 작성합니다.

```csharp
public class MyClass
{
    static void Main()
    {
#if NET40
        Console.WriteLine("Target framework: .NET Framework 4.0");
#elif NET45  
        Console.WriteLine("Target framework: .NET Framework 4.5");
#else
        Console.WriteLine("Target framework: .NET Standard 1.4");
#endif
    }
}
```

빌드 시스템은 [지원되는 대상 프레임워크 버전](#supported-target-framework-versions) 표에 표시된 대상 프레임워크를 나타내는 전처리기 기호를 인식합니다. .NET Standard 또는 .NET Core TFM을 나타내는 기호를 사용할 경우 점을 밑줄로 바꾸고 소문자를 대문자로 변경합니다. 예를 들어 `netstandard1.4`에 대한 기호는 `NETSTANDARD1_4`입니다.

다음은 .NET Core 대상 프레임워크에 대한 전체 전처리기 기호 목록입니다.

[!INCLUDE [Preprocessor symbols](../../includes/preprocessor-symbols.md)]

## <a name="deprecated-target-frameworks"></a>사용되지 않는 대상 프레임워크

다음 대상 프레임워크는 사용되지 않습니다. 이러한 대상 프레임워크를 대상으로 하는 패키지는 지정된 대체 항목으로 마이그레이션되어야 합니다.

| 사용되지 않는 TFM                                                                             | Replacement |
| ------------------------------------------------------------------------------------------ | ----------- |
| aspnet50<br>aspnetcore50<br>dnxcore50<br>dnx<br>dnx45<br>dnx451<br>dnx452                  | netcoreapp  |
| dotnet<br>dotnet50<br>dotnet51<br>dotnet52<br>dotnet53<br>dotnet54<br>dotnet55<br>dotnet56 | netstandard |
| netcore50                                                                                  | uap10.0     |
| win                                                                                        | netcore45   |
| win8                                                                                       | netcore45   |
| win81                                                                                      | netcore451  |
| win10                                                                                      | uap10.0     |
| winrt                                                                                      | netcore45   |

## <a name="see-also"></a>참고 항목

- [패키지, 메타패키지 및 프레임워크](../core/packages.md)
- [여러 플랫폼에서 사용할 수 있는 도구로 라이브러리 개발](../core/tutorials/libraries.md)
- [.NET Standard](net-standard.md)
- [.NET Core 버전 관리](../core/versions/index.md)
- [dotnet/standard GitHub repository](https://github.com/dotnet/standard)(dotnet/표준 GitHub 리포지토리)
- [NuGet Tools GitHub Repository](https://github.com/joelverhagen/NuGetTools)(NuGet 도구 GitHub 리포지토리)
- [Framework Profiles in .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html)(.NET의 프레임워크 프로필)
