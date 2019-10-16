---
title: .NET Core 자체 포함 앱 배포에 대한 런타임 롤포워드입니다.
description: 자체 포함된 배포에 대한 dotnet 게시 변경 내용에 대해 알아봅니다.
author: KathleenDollard
ms.date: 05/31/2018
ms.custom: seodec18
ms.openlocfilehash: 9af1454ede03b277f9b1a10e1d99a997e38809ea
ms.sourcegitcommit: 3d0c29b878f00caec288dfecb3a5c959de5aa629
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53656299"
---
# <a name="self-contained-deployment-runtime-roll-forward"></a>자체 포함된 배포 런타임 롤포워드

.NET Core [자체 포함된 애플리케이션 배포](index.md)에는 .NET Core 라이브러리와 .NET Core 런타임이 모두 포함됩니다. .NET Core 2.1 SDK(버전 2.1.300)부터 자체 포함 애플리케이션 배포가 [사용자 머신에 가장 높은 패치 런타임을 게시합니다](https://github.com/dotnet/designs/pull/36). 기본적으로 자체 포함된 배포에 대한 [`dotnet publish`](../tools/dotnet-publish.md)는 게시 컴퓨터에서 SDK의 일부로 설치된 최신 버전을 선택합니다. 이렇게 하면 보안 수정 사항(및 기타 수정 사항)과 함께 실행할 배포된 애플리케이션을 `publish` 중에 사용할 수 있습니다. 새 패치를 얻으려면 애플리케이션을 다시 게시해야 합니다. 자체 포함 애플리케이션은 `dotnet publish` 명령에서 `-r <RID>`를 지정하거나 프로젝트 파일(csproj/vbproj) 또는 명령줄에서 [RID(런타임 식별자)](../rid-catalog.md)를 지정하여 만듭니다.

## <a name="patch-version-roll-forward-overview"></a>패치 버전 롤포워드 개요

[`restore`](../tools/dotnet-restore.md), [`build`](../tools/dotnet-build.md) 및 [`publish`](../tools/dotnet-publish.md)는 별도로 실행할 수 있는 `dotnet` 명령입니다. 런타임 선택 사항은 `restore` 작업의 일부이며 `publish` 또는 `build`가 아닙니다. `publish`를 호출하면, 최신 버전의 패치가 선택됩니다. `--no-restore` 인수와 함께 `publish`를 호출하면, 이전의 `restore`가 새로운 자체 포함된 애플리케이션 게시 정책으로 실행되지 않았기 때문에 원하는 패치 버전을 얻을 수 없습니다. 이 경우 다음과 비슷한 텍스트와 함께 빌드 오류가 생성됩니다.

  "Microsoft.NETCore.App 버전 2.0.0을 사용하여 프로젝트가 복원되었지만 현재 설정으로는 버전 2.0.6이 대신 사용됩니다. 이 문제를 해결하려면 복원 및 빌드 또는 게시와 같은 후속 작업에 대해 동일한 설정을 사용해야 합니다. 일반적으로 복원 중이 아닌, 빌드 또는 게시 중에 RuntimeIdentifier 속성이 설정된 경우 이 문제가 발생할 수 있습니다."

> [!NOTE]
> `restore` 및 `build`를 `publish`와 같은 다른 명령의 일부로 암시적으로 실행할 수 있습니다. 다른 명령의 일부로 암시적으로 실행할 때는 적절한 아티팩트가 생성되도록 추가 컨텍스트와 함께 제공됩니다. 런타임과 함께 `publish`하는 경우(예를 들어 `dotnet publish -r linux-x64`), 암시적 `restore`로 linux-x64 런타임에 대한 패키지가 복원됩니다. 명시적으로 `restore`를 호출하는 경우, 해당 컨텍스트를 포함하지 않으므로 기본적으로 런타임 패키지를 복원하지 않습니다.

## <a name="how-to-avoid-restore-during-publish"></a>게시하는 동안 복원을 피하는 방법

`publish` 작업의 일부로 `restore`를 실행하는 것은 사용자 시나리오에 적합하지 않을 수 있습니다. 자체 포함된 애플리케이션을 만드는 동안 `publish` 중에 `restore`되지 않도록 다음을 수행합니다.

* `RuntimeIdentifiers` 속성을 게시할 모든 [RID](../rid-catalog.md)의 세미콜론으로 구분된 목록으로 설정합니다.
* `TargetLatestRuntimePatch` 속성을 `true`으로 설정합니다.

## <a name="no-restore-argument-with-dotnet-publish-options"></a>dotnet 게시 옵션으로 복원 안 함 인수

동일한 프로젝트 파일로 자체 포함된 애플리케이션과 [프레임워크 종속 애플리케이션](index.md)을 모두 만드는 경우 `--no-restore` 인수를 `dotnet publish`와 함께 사용하려면 다음 중 하나를 선택합니다.

1. 프레임워크 종속 동작을 선호합니다. 애플리케이션이 프레임워크 종속인 경우 이것이 기본 동작입니다. 애플리케이션이 자체 포함되고 패치가 적용되지 않은 2.1.0 로컬 런타임을 사용할 수 있는 경우 프로젝트 파일에서 `TargetLatestRuntimePatch`를 `false`로 설정합니다.

2. 자체 포함된 동작을 선호합니다. 애플리케이션이 자체 포함된 경우 이것이 기본 동작입니다. 애플리케이션이 프레임워크 종속이고 최신 패치를 설치해야 하는 경우 프로젝트 파일에서 `TargetLatestRuntimePatch`를 `true`로 설정합니다.

3. 프로젝트 파일에서 `RuntimeFrameworkVersion`을 특정 패치 버전으로 설정하여 런타임 프레임워크 버전을 명시적으로 제어합니다.
