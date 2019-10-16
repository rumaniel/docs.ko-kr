---
title: 소스에서 .NET Core 빌드
description: 소스 코드에서 .NET Core 및 .NET Core CLI를 빌드하는 방법을 알아봅니다.
author: bleroy
ms.date: 06/28/2017
ms.custom: seodec18
ms.openlocfilehash: dcd7c909325eec5a79db74098d7ac880000eafa1
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70105393"
---
# <a name="build-net-core-from-source"></a>소스에서 .NET Core 빌드

소스 코드에서 .NET Core를 빌드하는 기능은 여러 가지 면에서 중요합니다. .NET Core를 새 플랫폼으로 쉽게 포팅하고, 제품에 대한 기여 및 수정을 할 수 있으며, 사용자 지정 버전의 .NET을 만들 수 있습니다.
이 문서에서는 고유한 .NET Core 버전을 빌드하고 배포하려는 개발자에게 지침을 제공합니다.

## <a name="build-the-clr-from-source"></a>소스에서 CLR 빌드

.NET CoreCLR에 대한 소스 코드는 GitHub의 [dotnet/coreclr](https://github.com/dotnet/coreclr/) 리포지토리에서 확인할 수 있습니다.

현재 빌드는 다음 필수 구성 요소에 따라 달라집니다.

- [Git](https://git-scm.com/)
- [CMake](https://cmake.org/)
- [Python](https://www.python.org/)
- C++ 컴파일러

이러한 필수 구성 요소를 설치한 후 [dotnet/coreclr](https://github.com/dotnet/coreclr/) 리포지토리의 맨 아래에 있는 빌드 스크립트(Windows의 경우 `build.cmd`, Linux 및 macOS의 경우 `build.sh`)를 호출하여 CLR을 빌드할 수 있습니다.

구성 요소 설치는 OS(운영 체제)에 따라 달라집니다. 특정 OS에 대한 빌드 지침을 참조하세요.

- [Windows](https://github.com/dotnet/coreclr/blob/master/Documentation/building/windows-instructions.md)
- [Linux](https://github.com/dotnet/coreclr/blob/master/Documentation/building/linux-instructions.md)
- [macOS](https://github.com/dotnet/coreclr/blob/master/Documentation/building/osx-instructions.md)
- [FreeBSD](https://github.com/dotnet/coreclr/blob/master/Documentation/building/freebsd-instructions.md)
- [NetBSD](https://github.com/dotnet/coreclr/blob/master/Documentation/building/netbsd-instructions.md)

OS에서 교차 빌드되지 않습니다(X64에서 빌드되는 ARM의 경우에만 교차 빌드됨).  
특정 플랫폼을 빌드하려면 해당 플랫폼을 사용해야 합니다.  

빌드에는 다음과 같은 두 주요 `buildTypes`이 있습니다.

- 디버그(기본값) - 최소 최적화와 추가 런타임 검사로 런타임을 컴파일합니다(어설션). 최적화 수준의 감소와 추가 검사는 런타임 실행을 늦추지만 디버깅에는 가치가 있습니다. 이는 개발 및 테스트 환경에 권장되는 설정입니다.
- 릴리스 - 추가 런타임 검사 없이 전체 최적화를 사용하여 컴파일합니다. 런타임 성능이 더 빨라지지만 빌드하려면 약간 시간이 걸릴 수 있고 디버깅하기 어려울 수 있습니다. 이 빌드 유형을 선택하려면 `release`를 빌드 스크립트에 전달합니다.

또한 기본적으로 빌드는 런타임 실행 파일을 만들 뿐만 아니라 모든 테스트를 빌드합니다.
변경 내용을 시험하려는 경우에는 필요하지 않은 테스트가 상당히 많습니다. 이러한 테스트는 시간이 오래 걸립니다.
다음 예와 같이 빌드 스크립트에 `skiptests` 인수를 추가하여 빌드 테스트를 건너뛸 수 있습니다(Unix 컴퓨터에서는 `.\build`를 `./build.sh`로 대체).

```bat
    .\build skiptests
```

이전 예에서는 개발 시간 검사(어설션)를 사용하고 최적화를 사용하지 않는 `Debug` 버전을 빌드하는 방법을 보여 줬습니다. 릴리스(최대 속도) 버전을 빌드하려면 다음을 수행합니다.

```bat
    .\build release skiptests
```

-? 또는 -help 한정자를 사용하는 빌드와 함께 더 많은 빌드 옵션을 찾을 수 있습니다.

### <a name="using-your-build"></a>사용자의 빌드 사용

빌드는 생성된 모든 파일을 리포지토리의 맨 아래에 있는 `bin` 디렉터리 아래에 둡니다.
빌드 중 생성된 로그 파일이 들어 있는 *bin\Log* 디렉터리가 있습니다(빌드 실패 시 가장 유용함).
실제 출력 위치는 *bin\Product\Windows_NT.x64.Release* 같은 *bin\Product\[platform].[CPU architecture].[build type]* 디렉터리입니다.

빌드의 ‘원시’ 출력이 때때로 유용하지만, 사용자는 일반적으로 이전 출력 디렉터리의 `.nuget\pkg` 하위 디렉터리에 있는 NuGet 패키지에만 관심이 있습니다.

새 런타임 사용에 대한 두 가지 기본 기술은 다음과 같습니다.

 1. **dotnet.exe 및 NuGet을 사용하여 애플리케이션을 작성합니다**.
    방금 만든 NuGet 패키지 및 'dotnet' CLI(명령줄 인터페이스)를 사용하여 새 런타임을 사용하는 프로그램 작성에 대한 지침은 [사용자의 빌드 사용](https://github.com/dotnet/coreclr/blob/master/Documentation/workflow/UsingYourBuild.md)을 참조하세요. 이 기술은 비런타임 개발자가 새 런타임을 사용할 것으로 예상되는 방법입니다.

 2. **corerun.exe를 사용하여 패키지되지 않은 DLL을 사용하는 애플리케이션을 실행합니다**.
    이 리포지토리는 NuGet에서 종속성을 사용하지 않는 corerun.exe라는 간단한 호스트도 정의합니다.
    실제로 사용할 필요한 DLL을 가져올 위치를 호스트에 입력해야 하고, 수동으로 수집해야 합니다.
    이 기술은 [dotnet/coreclr](https://github.com/dotnet/coreclr) 리포지토리의 모든 테스트에 사용되며, 예비 유닛 테스트처럼 빠른 로컬 ‘edit-compile-debug’ 루프에 유용합니다.
    이 기술 사용에 대한 자세한 내용은 [Executing .NET Core Apps with CoreRun.exe](https://github.com/dotnet/coreclr/blob/master/Documentation/workflow/UsingCoreRun.md)(CoreRun.exe를 사용하여 .NET Core 앱 실행)를 참조하세요.

## <a name="build-the-cli-from-source"></a>소스에서 CLI 빌드

.NET Core CLI에 대한 소스 코드는 GitHub의 [dotnet/cli](https://github.com/dotnet/cli/) 리포지토리에서 확인할 수 있습니다.

.NET Core CLI을 빌드하려면 컴퓨터에 다음이 설치되어 있어야 합니다.

- Windows 및 Linux:
  - PATH의 git
- macOS:
  - PATH의 git
  - Xcode
  - Openssl

빌드하려면 Windows의 경우 루트에서 `build.cmd`를 실행하고, Linux 및 macOS의 경우 루트에서 `build.sh`를 실행합니다. 테스트를 실행하지 않으려면 `build.cmd -t:Compile` 또는 `./build.sh -t:Compile`을 실행합니다. macOS Sierra에서 CLI를 빌드하려면 `export DOTNET_RUNTIME_ID=osx.10.11-x64`를 실행하여 DOTNET_RUNTIME_ID 환경 변수를 설정해야 합니다.

### <a name="using-your-build"></a>사용자의 빌드 사용

*artifacts/{os}-{arch}/stage2*의 `dotnet` 실행 파일을 사용하여 새로 빌드한 CLI를 사용해 봅니다. 현재 콘솔에서 `dotnet`을 호출할 때 빌드 출력을 사용하려면 *artifacts/{os}-{arch}/stage2*를 PATH에 추가할 수도 있습니다.

## <a name="see-also"></a>참고 항목

- [.NET Core 공용 언어 런타임(CoreCLR)](https://github.com/dotnet/coreclr/blob/master/README.md)
- [.NET Core CLI 개발자 가이드](https://github.com/dotnet/cli/blob/master/Documentation/project-docs/developer-guide.md)
- [.NET Core 배포 패키징](./distribution-packaging.md)
