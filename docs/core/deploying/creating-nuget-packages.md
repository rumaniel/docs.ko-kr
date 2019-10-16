---
title: .NET Core CLI(명령줄 인터페이스) 도구를 사용하여 NuGet 패키지 만들기
description: "'dotnet pack' 명령을 사용하여 NuGet 패키지를 만드는 방법에 관해 알아봅니다."
author: cartermp
ms.date: 06/20/2016
ms.technology: dotnet-cli
ms.custom: seodec18
ms.openlocfilehash: d36a6ee7d524933577928daa9993fba8ce62f6c7
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71116696"
---
# <a name="how-to-create-a-nuget-package-with-net-core-command-line-interface-cli-tools"></a>.NET Core CLI(명령줄 인터페이스) 도구를 사용하여 NuGet 패키지를 만드는 방법

> [!NOTE]
> 다음에서는 Unix를 사용하는 명령줄 샘플을 보여 줍니다. 여기에 표시된 `dotnet pack` 명령은 Windows에서와 동일한 방식으로 작동합니다.

.NET Standard 및 .NET Core 라이브러리는 NuGet 패키지로 배포해야 합니다. 이는 실제로 모든 .NET 표준 라이브러리가 배포되고 사용되는 방법이며, `dotnet pack` 명령을 사용하여 가장 쉽게 수행할 수 있습니다.

NuGet을 통해 배포하려는 놀라운 새 라이브러리를 작성했다고 가정해 보세요. 플랫폼 간 도구를 사용하여 NuGet 패키지를 만들면 이 작업을 정확하게 수행할 수 있습니다. 다음 예제에서는 `netstandard1.0`을 대상으로 하는 **SuperAwesomeLibrary**라는 라이브러리를 가정합니다.

전이적 종속성 즉, 다른 패키지에 종속된 프로젝트가 있는 경우 NuGet 패키지를 만들기 전에 `dotnet restore` 명령을 사용하여 전체 솔루션에 대한 패키지를 복원해야 합니다. 이렇게 복원하지 않으면 `dotnet pack` 명령이 제대로 작동하지 않습니다.

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

패키지가 복원되었는지 확인한 후 라이브러리가 있는 디렉터리로 이동할 수 있습니다.

```console
cd src/SuperAwesomeLibrary
```

그러면 명령줄에서 단일 명령만 표시됩니다.

```dotnetcli
dotnet pack
```

이제 `/bin/Debug` 폴더가 다음과 같이 표시됩니다.

```console
$ ls bin/Debug

netstandard1.0/
SuperAwesomeLibrary.1.0.0.nupkg
SuperAwesomeLibrary.1.0.0.symbols.nupkg
```

그러면 디버그할 수 있는 패키지가 생성됩니다. 릴리스 이진 파일과 함께 NuGet 패키지를 빌드하려는 경우 `--configuration`(또는 `-c`) 스위치를 추가하고 `release`를 인수로 사용하기만 하면 됩니다.

```dotnetcli
dotnet pack --configuration release
```

이제 `/bin` 폴더에 릴리스 이진 파일과 함께 NuGet 패키지를 포함하는 `release` 폴더가 있습니다.

```console
$ ls bin/release

netstandard1.0/
SuperAwesomeLibrary.1.0.0.nupkg
SuperAwesomeLibrary.1.0.0.symbols.nupkg
```

또한 NuGet 패키지를 게시하는 데 필요한 파일이 있습니다.

## <a name="dont-confuse-dotnet-pack-with-dotnet-publish"></a>`dotnet pack`을 다음과 혼동하지 마세요.`dotnet publish`

어떤 지점에서도 `dotnet publish` 명령은 관련되지 않습니다. `dotnet publish` 명령은 애플리케이션 및 모든 종속성을 동일한 번들로 배포하기 위한 것이며 NuGet을 통해 배포하고 사용할 NuGet 패키지를 생성하기 위한 것이 아닙니다.

## <a name="see-also"></a>참고 항목

- [빠른 시작: 패키지 만들기 및 게시](/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)
