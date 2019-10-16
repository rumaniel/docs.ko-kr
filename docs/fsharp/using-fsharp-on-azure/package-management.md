---
title: Azure 용에서 F# 패키지 관리 사용
description: Paket 또는 Nuget을 사용 하 F# 여 Azure 종속성 관리
author: sylvanc
ms.date: 09/20/2016
ms.openlocfilehash: 4aa32ace91f30d0e43b9c40067f5f0f456cc4069
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71214220"
---
# <a name="package-management-for-f-azure-dependencies"></a>F# Azure 종속성에 대한 패키지 관리

패키지 관리자를 사용 하면 Azure 개발용 패키지를 쉽게 가져올 수 있습니다. 두 옵션은 [Paket](https://fsprojects.github.io/Paket/) 및 [NuGet](https://www.nuget.org/)입니다.

## <a name="using-paket"></a>Paket 사용

[Paket](https://fsprojects.github.io/Paket/) 를 종속성 관리자로 사용 하는 `paket.exe` 경우 도구를 사용 하 여 Azure 종속성을 추가할 수 있습니다. 예:

```console
> paket add nuget WindowsAzure.Storage
```

또는 플랫폼 간 .NET 개발에 [Mono](https://www.mono-project.com/) 를 사용 하는 경우:

```console
> mono paket.exe add nuget WindowsAzure.Storage
```

이렇게 하면 현재 `WindowsAzure.Storage` 디렉터리에 있는 프로젝트에 대 한 패키지 종속성 집합에 추가 되 고, `paket.dependencies` 파일을 수정 하 고, 패키지를 다운로드 합니다. 이전에 종속성을 설정 했거나 다른 개발자가 종속성을 설정한 프로젝트를 사용 하는 경우 다음과 같이 종속성을 로컬로 해결 하 고 설치할 수 있습니다.

```console
> paket install
```

또는 Mono 개발용:

```console
> mono paket.exe install
```

모든 패키지 종속성을 다음과 같은 최신 버전으로 업데이트할 수 있습니다.

```console
> paket update
```

또는 Mono 개발용:

```console
> mono paket.exe update
```

## <a name="using-nuget"></a>Nuget 사용

[NuGet](https://www.nuget.org/) 을 종속성 관리자로 사용 하는 `nuget.exe` 경우 도구를 사용 하 여 Azure 종속성을 추가할 수 있습니다. 예:

```console
> nuget install WindowsAzure.Storage -ExcludeVersion
```

또는 Mono 개발용:

```console
> mono nuget.exe install WindowsAzure.Storage -ExcludeVersion
```

이렇게 하면 현재 `WindowsAzure.Storage` 디렉터리에 있는 프로젝트에 대 한 패키지 종속성 집합에 추가 되 고 패키지가 다운로드 됩니다. 이전에 종속성을 설정 했거나 다른 개발자가 종속성을 설정한 프로젝트를 사용 하는 경우 다음과 같이 종속성을 로컬로 해결 하 고 설치할 수 있습니다.

```console
> nuget restore
```

또는 Mono 개발용:

```console
> mono nuget.exe restore
```

모든 패키지 종속성을 다음과 같은 최신 버전으로 업데이트할 수 있습니다.

```console
> nuget update
```

또는 Mono 개발용:

```console
> mono nuget.exe update
```

## <a name="referencing-assemblies"></a>어셈블리 참조

F# 스크립트에서 패키지를 사용 하려면 지시문을 `#r` 사용 하 여 패키지에 포함 된 어셈블리를 참조 해야 합니다. 예:

```fsharp
> #r "packages/WindowsAzure.Storage/lib/net40/Microsoft.WindowsAzure.Storage.dll"
```

여기에서 볼 수 있듯이 DLL에 대 한 상대 경로와 전체 DLL 이름을 지정 해야 합니다 .이 이름은 패키지 이름과 정확 하 게 일치 하지 않을 수 있습니다. 경로에는 프레임 워크 버전 및 패키지 버전 번호가 포함 됩니다. 설치 된 모든 어셈블리를 찾으려면 Windows 명령줄에서 다음과 같이 사용할 수 있습니다.

```console
> cd packages/WindowsAzure.Storage
> dir /s/b *.dll
```

또는 Unix 셸에서 다음과 같은 항목이 있습니다.

```console
> find packages/WindowsAzure.Storage -name "*.dll"
```

이렇게 하면 설치 된 어셈블리에 대 한 경로가 제공 됩니다. 여기에서 프레임 워크 버전에 대 한 올바른 경로를 선택할 수 있습니다.
