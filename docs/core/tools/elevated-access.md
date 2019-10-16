---
title: dotnet 명령에 대한 관리자 액세스 권한
description: 관리자 액세스 권한이 필요한 dotnet 명령에 대한 모범 사례를 알아봅니다.
author: wli3
ms.date: 06/26/2019
ms.openlocfilehash: cf7c93a0adcae7092a61a6fc6046cd45cf00bf58
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216309"
---
# <a name="elevated-access-for-dotnet-commands"></a>dotnet 명령에 대한 관리자 액세스 권한

소프트웨어 개발 모범 사례는 개발자에게 최소한의 권한만 요구하는 소프트웨어를 작성하도록 안내합니다. 그러나 성능 모니터링 도구와 같은 일부 소프트웨어는 운영 체제 규칙 때문에 관리자 권한이 필요합니다. 다음 지침은 이러한 소프트웨어를 .NET Core로 작성하기 위해 지원되는 시나리오를 설명합니다. 

다음 명령을 관리자 권한으로 실행할 수 있습니다.

- [dotnet 도구 설치](dotnet-tool-install.md)와 같은 `dotnet tool` 명령.
- `dotnet run --no-build`

상승된 다른 명령을 실행하지 않은 것이 좋습니다. 특히 [dotnet restore](dotnet-restore.md), [dotnet 빌드](dotnet-build.md) 및 [dotnet 실행](dotnet-run.md)과 같이 MSBuild를 사용하는 명령으로 권한 상승은 권장하지 않습니다. 기본 문제는 사용자가 dotnet 명령을 실행한 후 루트 계정과 제한된 계정 간에 앞뒤로 전환될 때 사용 권한 관리 문제입니다. 제한된 사용자로 루트 사용자가 빌드한 파일에 액세스할 수 없다는 것을 알 수 있습니다. 이 상황을 해결하는 방법이 있지만 처음부터 시작할 필요는 없습니다.

루트 계정과 제한된 계정 간에 앞뒤로 전환하지 않는 한 루트로 명령을 실행할 수 있습니다. 예를 들어 Docker 컨테이너는 기본적으로 루트로 실행되므로 이러한 특성을 갖습니다.

## <a name="global-tool-installation"></a>글로벌 도구 설치

다음 지침은 실행할 높은 권한이 필요한 .NET Core 도구를 설치, 실행 및 제거하는 권장 방법을 보여줍니다.

<!-- markdownlint-disable MD025 -->

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

### <a name="install-the-global-tool"></a>글로벌 도구 설치

`%ProgramFiles%\dotnet-tools` 폴더가 이미 있는 경우 다음을 수행하여 "사용자" 그룹에 해당 디렉터리를 쓰거나 수정할 수 있는 권한이 있는지 확인합니다.

- `%ProgramFiles%\dotnet-tools` 폴더를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **명령 속성** 대화 상자가 열립니다. 
- **보안** 탭을 선택합니다. **그룹 또는 사용자 이름**에서 “사용자” 그룹에 디렉터리를 쓰거나 수정할 수 있는 권한이 있는지 확인합니다. 
- "사용자" 그룹에 디렉터리를 쓰거나 수정할 수 있는 경우 *dotnet-tools*가 아닌 도구를 설치할 때 다른 디렉터리 이름을 사용합니다.

도구를 설치하려면 관리자 권한 프롬프트에서 다음 명령을 실행합니다. 설치 중에 *dotnet-tools* 폴더를 만듭니다.

```dotnetcli
dotnet tool install PACKAGEID --tool-path "%ProgramFiles%\dotnet-tools".
```

### <a name="run-the-global-tool"></a>글로벌 도구 실행

**옵션 1** 관리자 권한 프롬프트를 통해 전체 경로 사용:

```cmd
"%ProgramFiles%\dotnet-tools\TOOLCOMMAND"
```

**옵션 2** 새로 만든 폴더를 `%Path%`에 추가합니다. 이 작업은 한 번만 수행하면 됩니다.

```cmd
setx Path "%Path%;%ProgramFiles%\dotnet-tools\"
```

다음 항목으로 실행합니다.

```cmd
TOOLCOMMAND
```

### <a name="uninstall-the-global-tool"></a>글로벌 도구 제거

관리자 권한 프롬프트에 다음 명령을 입력합니다.

```dotnetcli
dotnet tool uninstall PACKAGEID --tool-path "%ProgramFiles%\dotnet-tools"
```

# <a name="linuxtablinux"></a>[Linux](#tab/linux)

[!INCLUDE [elevated-access-unix](../../../includes/elevated-access-unix.md)]

# <a name="macostabmacos"></a>[macOS](#tab/macos)

[!INCLUDE [elevated-access-unix](../../../includes/elevated-access-unix.md)]

---

## <a name="local-tools"></a>로컬 도구

로컬 도구는 사용자당 하위 디렉터리 트리별로 범위가 지정됩니다. 관리자 권한으로 실행되면 로컬 도구는 제한된 사용자 환경을 권한이 높은 환경에 공유합니다. Linux 및 macOS에서는 이로 인해 파일이 루트 사용자 전용 액세스로 설정됩니다. 사용자가 제한된 계정으로 전환하면 사용자는 더 이상 파일에 액세스하거나 쓸 수 없습니다. 따라서 권한 상승이 필요한 도구를 로컬 도구로 설치하는 것은 권장되지 않습니다. 대신 글로벌 도구용 `--tool-path` 옵션과 이전 지침을 사용합니다.

## <a name="elevation-during-development"></a>개발 중 권한 상승

개발하는 동안 애플리케이션을 테스트하기 위해 높은 액세스 권한이 필요할 수 있습니다. 예를 들어 이 시나리오는 일반적으로 IoT 앱에서 사용됩니다. 권한 상승 없이 애플리케이션을 빌드한 다음, 권한 상승을 통해 실행하는 것이 좋습니다. 다음과 같이 몇 가지 패턴이 있습니다.

- 생성된 실행 파일 사용(최상의 시작 성능 제공):

   ```bash
   dotnet build
   sudo ./bin/Debug/netcoreapp3.0/APPLICATIONNAME
   ```
    
- 새 이진 파일을 생성하지 않으려면 `—no-build` 플래그와 함께 [dotnet 실행](dotnet-run.md) 명령 사용:

   ```bash
   dotnet build
   sudo dotnet run --no-build
   ```

## <a name="see-also"></a>참고 항목

- [.NET Core Global Tool 개요](global-tools.md)
