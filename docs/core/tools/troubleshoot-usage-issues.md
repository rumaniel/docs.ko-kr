---
title: .NET Core 도구 사용 문제 해결
description: .NET Core 도구를 실행할 때 발생하는 일반적인 문제와 가능한 해결 방법을 검색합니다.
author: kdollard
ms.date: 09/23/2019
ms.openlocfilehash: eb769550493e5a25d4380cd543a3bbec880b38e9
ms.sourcegitcommit: 8b8dd14dde727026fd0b6ead1ec1df2e9d747a48
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71332952"
---
# <a name="troubleshoot-net-core-tool-usage-issues"></a>.NET Core 도구 사용 문제 해결

전역 도구 또는 로컬 도구일 수 있는 .NET Core 도구를 설치하거나 실행할 때 문제가 발생할 수 있습니다. 이 문서에서는 일반적인 근본 원인과 몇 가지 가능한 해결 방법을 설명합니다.

## <a name="installed-net-core-tool-fails-to-run"></a>설치된 .NET Core 도구가 실행되지 않음

.NET Core 도구가 실행되지 않는 경우, 다음 문제 중 하나가 발생했을 가능성이 큽니다.

* 도구의 실행 파일을 찾을 수 없습니다.
* 올바른 버전의 .NET Core 런타임을 찾을 수 없습니다. 

### <a name="executable-file-not-found"></a>실행 파일을 찾을 수 없음

실행 파일을 찾을 수 없는 경우 다음과 유사한 메시지가 표시됩니다.

```
Could not execute because the specified command or file was not found.
Possible reasons for this include:
  * You misspelled a built-in dotnet command.
  * You intended to execute a .NET Core program, but dotnet-xyz does not exist.
  * You intended to run a global tool, but a dotnet-prefixed executable with this name could not be found on the PATH.
```

실행 파일 이름에 따라 도구 호출 방법이 결정됩니다. 다음 표에서는 형식을 설명합니다.

| 실행 파일 이름 형식  | 호출 형식   |
|-------------------------|---------------------|
| `dotnet-<toolName>.exe` | `dotnet <toolName>` |
| `<toolName>.exe`        | `<toolName>`        |

* 전역 도구

    전역 도구는 기본 디렉터리 또는 특정 위치에 설치할 수 있습니다. 기본 디렉터리는 다음과 같습니다.

    | OS          | 경로                          |
    |-------------|-------------------------------|
    | Linux/macOS | `$HOME/.dotnet/tools`         |
    | Windows     | `%USERPROFILE%\.dotnet\tools` |

    전역 도구를 실행하려는 경우, 머신의 `PATH` 환경 변수에 전역 도구를 설치한 경로가 포함되어 있고 실행 파일이 해당 경로에 있는지 확인합니다.

    .NET Core CLI는 처음 사용 시 PATH 환경 변수에 기본 위치를 추가하려고 시도합니다. 그러나 위치가 PATH에 자동으로 추가되지 않는 몇 가지 시나리오가 있으므로, 다음과 같은 경우 PATH를 편집하여 위치를 구성해야 합니다.

  * Linux를 사용 중이고, apt-get 또는 rpm이 아닌 *.tar.gz* 파일을 사용하여 .NET Core SDK를 설치한 경우
  * macOS10.15 “Catalina” 이상 버전을 사용하는 경우
  * macOS10.14 “Mojave” 또는 이전 버전을 사용 중이고, *.pkg*가 아닌 *.tar.gz* 파일을 사용하여 .NET Core SDK를 설치한 경우
  * .NET Core 3.0 SDK를 설치했으며 `DOTNET_ADD_GLOBAL_TOOLS_TO_PATH` 환경 변수를 `false`로 설정한 경우
  * .NET Core 2.2 SDK 또는 이전 버전을 설치했으며 `DOTNET_SKIP_FIRST_TIME_EXPERIENCE` 환경 변수를 `true`로 설정한 경우
  
  전역 도구에 대한 자세한 내용은 [.NET Core 전역 도구 개요](global-tools.md)를 참조하세요.

* 로컬 도구

  로컬 도구를 실행하려는 경우, 현재 디렉터리 또는 부모 디렉터리 중 하나에 *dotnet-tools.json*이라는 매니페스트 파일이 있는지 확인합니다. 이 파일은 루트 폴더 대신, 프로젝트 폴더 계층 구조에서 *.config*라는 임의 폴더 아래에 있을 수도 있습니다. *dotnet-tools.json*이 있으면 파일을 열고 실행하려는 도구를 확인합니다. 파일에 `"isRoot": true` 항목이 없을 경우 파일 계층 구조 위로 추가 도구 매니페스트 파일이 있는지도 확인합니다.

    지정된 경로를 사용하여 설치된 .NET Core 도구를 실행하려는 경우, 도구를 사용할 때 해당 경로를 포함해야 합니다. 도구 경로를 사용하여 설치된 도구의 사용 예제는 다음과 같습니다.

   ```console
   ..\<toolDirectory>\dotnet-<toolName>
    ```

### <a name="runtime-not-found"></a>런타임을 찾을 수 없음

전역 도구는 [프레임워크 종속 애플리케이션](../deploying/index.md#framework-dependent-deployments-fdd)이므로, 머신에 설치된 .NET Core 런타임을 사용합니다. 필요한 런타임을 찾을 수 없는 경우, 다음과 같은 일반적인 .NET Core 런타임 롤포워드 규칙을 따릅니다.

* 애플리케이션은 지정된 주 및 부 버전의 가장 높은 패치 릴리스로 롤포워드합니다.
* 일치하는 주 버전 및 부 버전 번호를 가진, 일치하는 런타임이 없으면 다음으로 높은 부 버전이 사용됩니다.
* 런타임의 미리 보기 버전 간 또는 미리 보기 버전과 릴리스 버전 간에는 롤포워드가 발생하지 않습니다. 따라서 미리 보기 버전을 사용하여 만든 .NET Core 도구는 작성자가 다시 빌드하여 다시 게시한 후에 다시 설치해야 합니다.

다음 두 가지 일반적인 시나리오에서는 롤포워드가 기본적으로 발생하지 않습니다.

* 하위 버전의 런타임만 사용할 수 있는 경우. 롤포워드는 이후 버전의 런타임만 선택합니다.
* 상위 주 버전의 런타임만 사용할 수 있는 경우. 롤포워드는 주 버전 경계를 넘지 않습니다.

애플리케이션이 적절한 런타임을 찾을 수 없는 경우 애플리케이션이 실행되지 않고 오류가 보고됩니다.

다음 명령 중 하나를 사용하여 머신에 설치된 .NET Core 런타임을 확인할 수 있습니다.

```dotnetcli
dotnet --list-runtimes
dotnet --info
```

도구가 현재 설치된 런타임 버전을 지원해야 한다고 생각되는 경우, 도구 작성자에게 버전 번호 또는 다중 대상의 업데이트가 가능한지 문의할 수 있습니다. 작성자가 업데이트된 버전 번호로 도구 패키지를 다시 컴파일하고 NuGet에 다시 게시하면 복사본을 업데이트할 수 있습니다. 업데이트가 가능할 때까지 가장 빠른 해결 방법은 실행하려는 도구에서 작동하는 런타임 버전을 설치하는 것입니다. 특정 .NET Core 런타임 버전을 다운로드하려면 [.NET Core 다운로드 페이지](https://dotnet.microsoft.com/download/dotnet-core)로 이동합니다.

기본 위치가 아닌 다른 위치에 .NET Core SDK를 설치하는 경우, 환경 변수 `DOTNET_ROOT`를 `dotnet` 실행 파일이 있는 디렉터리로 설정해야 합니다.

## <a name="net-core-tool-installation-fails"></a>.NET Core 도구 설치 실패

.NET Core 전역 또는 로컬 도구의 설치에 실패할 수 있는 원인에는 여러 가지가 있습니다. 도구 설치에 실패하면 다음과 유사한 메시지가 표시됩니다.

```
Tool '{0}' failed to install. This failure may have been caused by:

* You are attempting to install a preview release and did not use the --version option to specify the version.
* A package by this name was found, but it was not a .NET Core tool.
* The required NuGet feed cannot be accessed, perhaps because of an Internet connection problem.
* You mistyped the name of the tool.

For more reasons, including package naming enforcement, visit https://aka.ms/failure-installing-tool
```

실패 진단을 지원하기 위해 이전 메시지와 함께 NuGet 메시지가 사용자에게 직접 표시됩니다. NuGet 메시지는 문제를 확인하는 데 도움이 될 수 있습니다.

### <a name="package-naming-enforcement"></a>패키지 명명 적용

Microsoft에서 도구의 패키지 ID 지침이 변경되어, 예상 이름으로 찾을 수 없는 도구가 많습니다. 새 지침에 따라 모든 Microsoft 도구 앞에 “Microsoft”가 접두사로 추가됩니다. 이 접두사는 예약되었으며, Microsoft 공인 인증서로 서명된 패키지에만 사용할 수 있습니다.

전환 중에 일부 Microsoft 도구는 이전 형식의 패키지 ID를 사용하고 다른 도구는 새 형식을 사용하게 됩니다.

```dotnetcli
dotnet tool install -g Microsoft.<toolName>
dotnet tool install -g <toolName>
```

패키지 ID가 업데이트될 경우, 최신 업데이트를 가져오려면 새 패키지 ID로 변경해야 합니다. 간소화된 도구 이름을 가진 패키지는 사용되지 않습니다.

### <a name="preview-releases"></a>미리 보기 릴리스

* 미리 보기 릴리스를 설치하려고 하며, `--version` 옵션을 통해 버전을 지정하지 않았습니다.

미리 보기로 제공되는 .NET Core 도구는 미리 보기 상태임을 나타내는 이름 부분으로 지정해야 합니다. 전체 미리 보기를 포함할 필요는 없습니다. 버전 번호가 올바른 형식이라고 가정하면, 다음 예제와 같이 사용할 수 있습니다.

```dotnetcli
dotnet tool install -g --version 1.1.0-pre <toolName>
```

> [!NOTE]
> .NET Core CLI 팀은 이 작업이 더 용이하도록, 향후 릴리스에서 `--preview` 스위치를 추가할 계획입니다.

### <a name="package-isnt-a-net-core-tool"></a>패키지가 .NET Core 도구가 아님

* 이 이름을 가진 NuGet 패키지는 있지만 .NET Core 도구가 아닙니다.

.NET Core 도구가 아닌 일반 NuGet 패키지인 NuGet 패키지를 설치하려고 하면 다음과 유사한 오류가 표시됩니다.

`NU1212: Invalid project-package combination for `<ToolName>`. DotnetToolReference project style can only contain references of the DotnetTool type.`

### <a name="nuget-feed-cant-be-accessed"></a>NuGet 피드에 액세스할 수 없음

* 인터넷 연결 문제 등의 이유로, 필요한 NuGet 피드에 액세스할 수 없습니다.

도구를 설치하려면 도구 패키지가 포함된 NuGet 피드에 액세스할 수 있어야 합니다. 피드를 사용할 수 없는 경우 설치에 실패합니다. `nuget.config`를 사용하여 피드를 변경하거나, 특정 `nuget.config` 파일을 요청하거나, `--add-source` 스위치를 사용하여 추가 피드를 지정할 수 있습니다. 기본적으로 NuGet은 연결할 수 없는 모든 피드에 대해 오류를 throw합니다. `--ignore-failed-sources` 플래그는 연결할 수 없는 이러한 소스를 건너뛸 수 있습니다.

### <a name="package-id-incorrect"></a>패키지 ID가 올바르지 않음

* 도구 이름을 잘못 입력했습니다.

일반적인 실패 원인은 잘못된 도구 이름입니다. 잘못 입력했을 수도 있고, 도구가 이동되었거나 사용 중단되었을 수도 있습니다. NuGet.org 도구의 경우 올바른 이름을 입력하는 한 가지 방법은 NuGet.org에서 도구를 검색하여 설치 명령을 복사하는 것입니다.

## <a name="see-also"></a>참고 항목
* [.NET Core Global Tool 개요](global-tools.md)
