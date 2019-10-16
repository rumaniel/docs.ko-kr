---
title: ML.NET CLI(명령줄 인터페이스) 도구를 설치하는 방법
description: ML.NET CLI(명령줄 인터페이스) 도구 개요 및 설치
ms.date: 04/16/2019
ms.custom: ''
ms.openlocfilehash: baced9bbcc72153458d42d4b6d8206921bf187b8
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117998"
---
# <a name="how-to-install-the-mlnet-command-line-interface-cli-tool"></a>ML.NET CLI(명령줄 인터페이스) 도구를 설치하는 방법

모든 명령 프롬프트(Windows, Mac 또는 Linux)에서 ML.NET CLI를 실행하여 제공한 학습 데이터 세트를 기초로 품질 높은 ML.NET 모델과 소스 코드를 생성할 수 있습니다.

> [!NOTE]
> 이 항목은 현재 미리 보기로 제공되는 ML.NET CLI 및 ML.NET AutoML을 참조하며, 자료는 변경될 수 있습니다.

## <a name="pre-requisites"></a>필수 구성 요소

- [.NET Core 2.2 SDK](https://dotnet.microsoft.com/download/dotnet-core/2.2)

- (선택 사항) [Visual Studio 2017 또는 2019](https://visualstudio.microsoft.com/vs/)

생성된 C# 코드 프로젝트를 Visual Studio F5 또는 `dotnet run`(.NET Core CLI)으로 실행할 수 있습니다.

참고: [.NET Core 2.2 SDK](https://dotnet.microsoft.com/download/dotnet-core/2.2) 설치 후 `dotnet tool` 명령이 작동하지 않는 경우 Windows에서 로그아웃했다가 다시 로그인합니다.

## <a name="install"></a>설치

ML.NET CLI는 다른 DotNet Global Tool처럼 설치됩니다. `dotnet tool install` .NET Core CLI 명령을 사용합니다. 

다음 예제에서는 기본 NuGet 피드 위치에 ML.NET CLI를 설치하는 방법을 보여 줍니다.

```dotnetcli
dotnet tool install -g mlnet
```

도구를 설치할 수 없는 경우(즉 기본 NuGet 피드에서 사용할 수 없는 경우) 오류 메시지가 표시됩니다. 예상한 피드가 확인되고 있는지 검사합니다.

설치에 성공하면 다음 예와 같이 도구와 설치된 버전을 호출하는 데 사용되는 명령을 보여 주는 메시지가 표시됩니다.

```console
You can invoke the tool using the following command: mlnet
Tool 'mlnet' (version 'X.X.X') was successfully installed.
```

다음 명령을 입력하여 설치가 완료되었는지 확인할 수 있습니다.

```console
mlnet
```

'auto-train' 명령처럼 mlnet 도구에 대해 사용 가능한 명령의 도움말을 참조해야 합니다.

## <a name="install-a-specific-release-version"></a>특정 릴리스 버전 설치

이전 릴리스 버전 또는 특정 버전의 도구를 설치하려는 경우 다음 형식을 사용하여 [프레임워크](../../standard/frameworks.md)를 지정할 수 있습니다.

```dotnetcli
dotnet tool install -g mlnet --framework <FRAMEWORK>
```

다음 명령을 입력하여 패키지가 올바르게 설치되었는지 확인할 수도 있습니다.

```dotnetcli
dotnet tool list -g
```

## <a name="uninstall-the-cli-package"></a>CLI 패키지 제거

로컬 컴퓨터에서 패키지를 제거하려면 다음 명령을 입력합니다.

```dotnetcli
dotnet tool uninstall mlnet -g
```

## <a name="update-the-cli-package"></a>CLI 패키지 업데이트

로컬 컴퓨터에서 패키지를 업데이트하려면 다음 명령을 입력합니다.

```dotnetcli
dotnet tool update -g mlnet
```

## <a name="set-up-cli-suggestions-tab-based-auto-completion"></a>CLI 제안(탭 기반 자동 완성) 설정

ML.NET CLI는 `System.CommandLine`을 기반으로 하므로 탭 완성을 기본 제공으로 지원합니다.

탭 자동 완성이 작동하는 예제는 다음 애니메이션에 표시됩니다.

![이미지](./media/cli-tab-completion.gif)

'탭 기반 자동 완성'(매개 변수 제안)은 *Windows PowerShell* 및 *macOS/Linux bash*에서 실행되나 *Windows CMD*에서는 작동하지 않습니다.

현재 미리 보기 버전에서 이를 사용하려면 최종 사용자가 아래에서 설명한 대로 셸마다 한 번씩 몇 가지 단계를 수행해야 합니다. 이 후에는 ML.NET CLI처럼 `System.CommandLine`을 사용하여 작성된 모든 앱에 완성이 적용됩니다.

완성을 사용하려는 컴퓨터에서 다음 두 가지를 수행해야 합니다.

1. 다음 명령을 실행하여 `dotnet-suggest` 글로벌 도구를 설치합니다.

    ```dotnetcli
    dotnet tool install dotnet-suggest -g
    ```

2. 셸 프로필에 적합한 Shim 스크립트를 추가합니다. 셸 프로필 파일을 만들어야 할 수 있습니다. Shim 스크립트는 셸의 완성 요청을 `dotnet-suggest` 도구로 전달하며 적합한 `System.CommandLine` 기반 앱에 위임됩니다.

    - Bash의 경우 [dotnet-suggest-shim.bash](https://github.com/dotnet/System.CommandLine/blob/master/src/System.CommandLine.Suggest/dotnet-suggest-shim.bash)의 콘텐츠를 `~/.bash_profile`에 추가합니다.

    - PowerShell의 경우 [dotnet-suggest-shim.ps1](https://github.com/dotnet/System.CommandLine/blob/master/src/System.CommandLine.Suggest/dotnet-suggest-shim.ps1)의 콘텐츠를 PowerShell 프로필에 추가합니다. 콘솔에서 다음 명령을 실행하여 PowerShell 프로필의 예상 경로를 찾을 수 있습니다.

    ```console
    echo $profile
    ``` 

(다른 셸의 경우 [검색](https://github.com/dotnet/System.CommandLine/issues?q=is%3Aissue+is%3Aopen+label%3A%22shell+suggestion%22) 또는 [문제](https://github.com/dotnet/System.CommandLine/issues) 열기)

## <a name="installation-directory"></a>설치 디렉터리

ML.NET CLI는 기본 디렉터리 또는 특정 위치에 설치할 수 있습니다. 기본 디렉터리는 다음과 같습니다.

| OS          | 경로                          |
|-------------|-------------------------------|
| Linux/macOS | `$HOME/.dotnet/tools`         |
| Windows     | `%USERPROFILE%\.dotnet\tools` |

이러한 위치는 SDK를 처음 실행할 때 사용자 경로에 추가되므로 설치된 Global Tool을 직접 호출할 수 있습니다.

참고: Global Tool은 컴퓨터 전체가 아닌 사용자 특정입니다. 사용자별 도구라는 것은 컴퓨터의 모든 사용자가 사용할 수 있는 Global Tool을 설치할 수 없음을 의미합니다. 이 도구는 도구가 설치된 각 사용자 프로필에서만 사용할 수 있습니다.

Global Tool을 특정 디렉터리에 설치할 수도 있습니다. 특정 디렉터리에 설치된 경우 사용자는 경로에 해당 디렉터리를 포함하거나, 지정된 디렉터리로 명령을 호출하거나, 지정된 디렉터리 내에서 도구를 호출하여 명령을 사용할 수 있는지 확인해야 합니다.
이 경우 .NET Core CLI는 이 위치를 PATH 환경 변수에 자동으로 추가하지 않습니다.

## <a name="see-also"></a>참고 항목

- [‘ML.NET CLI 도구 시작' 자습서](../tutorials/mlnet-cli.md)
- [ML.NET CLI 도구를 사용하여 자동으로 모델을 학습하는 방법](../automate-training-with-cli.md)
- [ML.NET CLI auto-train 명령 참조 가이드](../reference/ml-net-cli-reference.md) 
- [ML.NET CLI의 원격 분석](../resources/ml-net-cli-telemetry.md)
