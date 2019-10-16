---
title: CLI를 사용하여 .NET Core 앱 게시
description: .NET Core SDK CLI(명령줄 인터페이스) 도구를 사용하여 .NET Core 앱을 게시하는 방법을 알아봅니다.
author: thraka
ms.author: adegeo
ms.date: 01/16/2019
dev_langs:
- csharp
- vb
ms.custom: seodec18
ms.openlocfilehash: c8b4c60eb4ea09c8b10bd0b2fffc803d0a5fb6e0
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834289"
---
# <a name="publish-net-core-apps-with-the-cli"></a>CLI를 사용하여 .NET Core 앱 게시

이 문서에서는 명령줄에서 .NET Core 애플리케이션을 게시하는 방법을 보여줍니다. .NET Core는 애플리케이션을 게시하는 세 가지 방법을 제공합니다. 프레임워크 종속 배포는 로컬에 설치된 .NET Core 런타임을 사용하는 플랫폼 간 .dll 파일을 생성합니다. 프레임워크 종속 실행 파일은 로컬에 설치된 .NET Core 런타임을 사용하는 플랫폼별 실행 파일을 생성합니다. 자체 포함 실행 파일은 플랫폼별 실행 파일을 생성하고 .NET Core 런타임의 로컬 복사본을 포함합니다.

이러한 개시 모드에 대한 개요는 [.NET Core 애플리케이션 배포](index.md)를 참조하세요.

CLI 사용에 대한 빠른 도움말을 찾나요? 다음 표는 앱을 게시하는 방법의 몇 가지 예를 보여줍니다. `-f <TFM>` 매개 변수를 사용하거나 프로젝트 파일을 편집하여 대상 프레임워크를 지정할 수 있습니다. 자세한 내용은 [기본 사항 게시](#publishing-basics)를 참조하세요.

| 게시 모드 | SDK 버전 | 명령 |
| ------------ | ----------- | ------- |
| 프레임워크 종속 배포 | 2.x | `dotnet publish -c Release` |
| 프레임워크 종속 실행 파일 | 2.2 | `dotnet publish -c Release -r <RID> --self-contained false` |
|                                | 3.0 | `dotnet publish -c Release -r <RID> --self-contained false` |
|                                | 3.0* | `dotnet publish -c Release` |
| 자체 포함 배포      | 2.1 | `dotnet publish -c Release -r <RID> --self-contained true` |
|                                | 2.2 | `dotnet publish -c Release -r <RID> --self-contained true` |
|                                | 3.0 | `dotnet publish -c Release -r <RID> --self-contained true` |

\*SDK 버전 3.0을 사용할 경우 프레임워크 종속 실행 파일은 기본 `dotnet publish` 명령을 실행할 때 기본 게시 모드입니다. 이 내용은 **.NET Core 2.1** 또는 **.NET Core 3.0**을 대상으로 하는 프로젝트에만 적용됩니다.

## <a name="publishing-basics"></a>게시 기본 사항

프로젝트 파일의 `<TargetFramework>` 설정은 앱을 게시할 때 기본 대상 프레임워크를 지정합니다. 대상 프레임워크를 유효한 [TFM(대상 프레임워크 모니커)](../../standard/frameworks.md)으로 변경할 수 있습니다. 예를 들어 프로젝트에서 `<TargetFramework>netcoreapp2.2</TargetFramework>`를 사용하는 경우 .NET Core 2.2를 대상으로 하는 이진 파일이 생성됩니다. 이 설정에 지정된 TFM은 [`dotnet publish`](../tools/dotnet-publish.md) 명령에서 사용되는 기본 대상입니다.

둘 이상의 프레임워크를 대상으로 하려는 경우 `<TargetFrameworks>` 설정을 세미콜론으로 구분된 둘 이상의 TFM 값으로 설정할 수 있습니다. `dotnet publish -f <TFM>` 명령을 사용하여 프레임워크 중 하나를 게시할 수 있습니다. 예를 들어 `<TargetFrameworks>netcoreapp2.1;netcoreapp2.2</TargetFrameworks>`가 있고 `dotnet publish -f netcoreapp2.1`을 실행하는 경우 .NET Core 2.1을 대상으로 하는 이진 파일이 생성됩니다.

달리 설정하지 않으면 [`dotnet publish`](../tools/dotnet-publish.md) 명령의 출력 디렉터리는 `./bin/<BUILD-CONFIGURATION>/<TFM>/publish/`입니다. `-c` 매개 변수를 사용하여 변경하지 않는 한 기본 **BUILD-CONFIGURATION** 모드는 **디버그**입니다. 예를 들어 `dotnet publish -c Release -f netcoreapp2.1`은 `myfolder/bin/Release/netcoreapp2.1/publish/`에 게시합니다.

.NET Core SDK 3.0을 사용하는 경우 .NET Core 버전 2.1, 2.2 또는 3.0을 대상으로 하는 앱의 기본 게시 모드는 프레임워크 종속 실행 파일입니다.

.NET Core SDK 2.1을 사용하는 경우 .NET Core 버전 2.1, 2.2를 대상으로 하는 앱의 기본 게시 모드는 프레임워크 종속 배포입니다.

### <a name="native-dependencies"></a>네이티브 종속성

앱에 네이티브 종속성이 있는 경우 다른 운영 체제에서 실행되지 않을 수 있습니다. 예를 들어 앱이 네이티브 Windows API를 사용하는 경우 macOS 또는 Linux에서 실행되지 않습니다. 플랫폼별 코드를 제공하고 각 플랫폼에 대해 실행 파일을 컴파일해야 합니다.

또한 참조한 라이브러리에 네이티브 종속성이 있는 경우 모든 플랫폼에서 앱이 실행되지 않을 수 있습니다. 그러나 참조하는 NuGet 패키지에 플랫폼별 버전이 포함되어 있어 사용자의 필수 네이티브 종속성을 처리할 수 있습니다.

네이티브 종속성이 있는 앱을 배포할 때 `dotnet publish -r <RID>` 스위치를 사용하여 게시할 대상 플랫폼을 지정해야 할 수 있습니다. 런타임 식별자 목록은 [런타임 식별자(RID) 카탈로그](../rid-catalog.md)를 참조하세요.

플랫폼별 이진 파일에 대한 자세한 내용은 [프레임워크 종속 실행 파일](#framework-dependent-executable) 및 [자체 포함 배포](#self-contained-deployment) 섹션을 참조하세요.

## <a name="sample-app"></a>샘플 앱

다음 앱을 사용하여 게시 명령을 살펴볼 수 있습니다. 이 앱은 터미널에서 다음 명령을 실행하여 만듭니다.

```dotnetcli
mkdir apptest1
cd apptest1
dotnet new console
dotnet add package Figgle
```

콘솔 템플릿에 의해 생성된 `Program.cs` 또는 `Program.vb` 파일을 다음과 같이 변경해야 합니다.

```csharp
using System;

namespace apptest1
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine(Figgle.FiggleFonts.Standard.Render("Hello, World!"));
        }
    }
}
```

```vb
Imports System

Module Program
    Sub Main(args As String())
        Console.WriteLine(Figgle.FiggleFonts.Standard.Render("Hello, World!"))
    End Sub
End Module
```

앱([`dotnet run`](../tools/dotnet-run.md))을 실행하면 다음 출력이 표시됩니다.

```terminal
  _   _      _ _         __        __         _     _ _
 | | | | ___| | | ___    \ \      / /__  _ __| | __| | |
 | |_| |/ _ \ | |/ _ \    \ \ /\ / / _ \| '__| |/ _` | |
 |  _  |  __/ | | (_) |    \ V  V / (_) | |  | | (_| |_|
 |_| |_|\___|_|_|\___( )    \_/\_/ \___/|_|  |_|\__,_(_)
                     |/
```

## <a name="framework-dependent-deployment"></a>프레임워크 종속 배포

.NET Core SDK 2.x CLI의 경우 FDD(프레임워크 종속 배포)가 기본 `dotnet publish` 명령의 기본 모드입니다.

앱을 FDD로 게시하면 `<PROJECT-NAME>.dll` 파일이 `./bin/<BUILD-CONFIGURATION>/<TFM>/publish/` 폴더에 생성됩니다. 앱을 실행하려면 출력 폴더로 이동하여 `dotnet <PROJECT-NAME>.dll` 명령을 사용합니다.

앱이 특정 버전의 .NET Core를 대상으로 구성됩니다. 대상으로 하는 .NET Core 런타임은 앱을 실행하려는 머신에 있어야 합니다. 예를 들어 앱이 .NET Core 2.2를 대상으로 하는 경우, 앱이 실행 되는 모든 머신에 .NET Core 2.2 런타임이 설치되어 있어야 합니다. [기본 사항 게시](#publishing-basics) 섹션에서 설명된 대로 프로젝트 파일을 편집하여 기본 대상 프레임워크를 변경하거나 둘 이상의 프레임워크를 대상으로 할 수 있습니다.

FDD를 게시하면 앱을 실행하는 시스템에서 사용할 수 있는 최신 .NET Core 보안 패치로 자동으로 롤포워드하는 앱이 만들어집니다. 컴파일 시 버전 바인딩에 대한 자세한 내용은 [사용할 .NET Core 버전 선택](../versions/selection.md#framework-dependent-apps-roll-forward)을 참조하세요.

## <a name="framework-dependent-executable"></a>프레임워크 종속 실행 파일

.NET Core SDK 3.x CLI의 경우 FDE(프레임워크 종속 실행 파일)가 기본 `dotnet publish` 명령의 기본 모드입니다. 현재 운영 체제를 대상으로 하는 한 다른 매개 변수를 지정할 필요가 없습니다.

이 모드에서는 플랫폼별 실행 파일 호스트가 만들어져 플랫폼 간 앱을 호스트합니다. 이 모드는 FDD에 `dotnet` 명령 형식의 호스트가 필요함으로 FDD와 유사합니다. 호스트 실행 파일 이름은 플랫폼마다 다르며 `<PROJECT-FILE>.exe`와 유사한 이름이 지정됩니다. `dotnet <PROJECT-FILE>.dll`을 호출하는 대신 이 실행 파일을 직접 실행하여 앱을 실행할 수 있습니다.

앱이 특정 버전의 .NET Core를 대상으로 구성됩니다. 대상으로 하는 .NET Core 런타임은 앱을 실행하려는 머신에 있어야 합니다. 예를 들어 앱이 .NET Core 2.2를 대상으로 하는 경우, 앱이 실행 되는 모든 머신에 .NET Core 2.2 런타임이 설치되어 있어야 합니다. [기본 사항 게시](#publishing-basics) 섹션에서 설명된 대로 프로젝트 파일을 편집하여 기본 대상 프레임워크를 변경하거나 둘 이상의 프레임워크를 대상으로 할 수 있습니다.

FDE를 게시하면 앱을 실행하는 시스템에서 사용할 수 있는 최신 .NET Core 보안 패치로 자동으로 롤포워드하는 앱이 만들어집니다. 컴파일 시 버전 바인딩에 대한 자세한 내용은 [사용할 .NET Core 버전 선택](../versions/selection.md#framework-dependent-apps-roll-forward)을 참조하세요.

현재 플랫폼을 대상으로 할 때는 .NET Core 3.x를 제외하고 `dotnet publish` 명령과 함께 다음 스위치를 사용하여 FDE를 게시해야 합니다.

- `-r <RID>` 이 스위치는 식별자(RID)를 사용하여 대상 플랫폼을 지정합니다. 런타임 식별자 목록은 [런타임 식별자(RID) 카탈로그](../rid-catalog.md)를 참조하세요.

- `--self-contained false` 이 스위치는 .NET Core SDK에 실행 파일을 FDE로 생성하도록 지시합니다.

`-r` 스위치를 사용할 때마다 출력 폴더 경로가 `./bin/<BUILD-CONFIGURATION>/<TFM>/<RID>/publish/`로 변경됩니다.

[예제 앱](#sample-app)을 사용하는 경우 `dotnet publish -f netcoreapp2.2 -r win10-x64 --self-contained false`를 실행합니다. 이 명령은 `./bin/Debug/netcoreapp2.2/win10-x64/publish/apptest1.exe` 실행 파일을 만듭니다.

> [!NOTE]
> **세계화 고정 모드**를 사용하여 배포의 전체 크기를 줄일 수 있습니다. 이 모드는 전역적으로 인식되지 않는 서식 지정 규칙, 대/소문자 규칙 및 문자열 비교와 [고정 문화권](xref:System.Globalization.CultureInfo.InvariantCulture)의 정렬 순서를 사용할 수 있는 애플리케이션에 유용합니다. **세계화 고정 모드**와 이 모드를 사용하는 방법에 대한 자세한 내용은 [.NET Core 세계화 고정 모드](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/globalization-invariant-mode.md)를 참조하세요.

## <a name="self-contained-deployment"></a>자체 포함 배포

SCD(자체 포함 배포)를 게시하면 .NET Core SDK는 플랫폼별 실행 파일을 만듭니다. SCD 게시에는 앱을 실행하는 데 필요한 모든 .NET Core 파일이 포함되지만, [.NET Core의 네이티브 종속성](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md)은 포함되지 않습니다. 이러한 종속성은 앱을 실행하기 전에 시스템에 있어야 합니다.

SCD를 게시하면 사용 가능한 최신 .NET Core 보안 패치로 롤포워드되지 않는 앱이 만들어집니다. 컴파일 시 버전 바인딩에 대한 자세한 내용은 [사용할 .NET Core 버전 선택](../versions/selection.md#self-contained-deployments-include-the-selected-runtime)을 참조하세요.

SCD를 게시하려면 `dotnet publish` 명령과 함께 다음 스위치를 사용해야 합니다.

- `-r <RID>` 이 스위치는 식별자(RID)를 사용하여 대상 플랫폼을 지정합니다. 런타임 식별자 목록은 [런타임 식별자(RID) 카탈로그](../rid-catalog.md)를 참조하세요.

- `--self-contained true` 이 스위치는 .NET Core SDK에 실행 파일을 SCD로 생성하도록 지시합니다.

> [!NOTE]
> **세계화 고정 모드**를 사용하여 배포의 전체 크기를 줄일 수 있습니다. 이 모드는 전역적으로 인식되지 않는 서식 지정 규칙, 대/소문자 규칙 및 문자열 비교와 [고정 문화권](xref:System.Globalization.CultureInfo.InvariantCulture)의 정렬 순서를 사용할 수 있는 애플리케이션에 유용합니다. **세계화 고정 모드**와 이 모드를 사용하는 방법에 대한 자세한 내용은 [.NET Core 세계화 고정 모드](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/globalization-invariant-mode.md)를 참조하세요.

## <a name="see-also"></a>참고 항목

- [.NET Core 애플리케이션 배포 개요](index.md)
- [.NET Core RID(런타임 식별자) 카탈로그](../rid-catalog.md)
