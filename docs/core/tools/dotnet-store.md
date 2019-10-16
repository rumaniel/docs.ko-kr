---
title: dotnet store 명령
description: "'dotnet store' 명령은 지정된 어셈블리를 런타임 패키지 저장소에 저장합니다."
author: bleroy
ms.date: 05/29/2018
ms.custom: seodec18
ms.openlocfilehash: 58889039d117a2231cda693e4aca7790f018d1b5
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54606753"
---
# <a name="dotnet-store"></a>dotnet store

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-2plus.md)]

## <a name="name"></a>name

`dotnet store` - 지정된 어셈블리를 [런타임 패키지 저장소](../deploying/runtime-store.md)에 저장합니다.

## <a name="synopsis"></a>개요

`dotnet store -m|--manifest -f|--framework -r|--runtime  [--framework-version] [-h|--help] [--output] [--skip-optimization] [--skip-symbols] [-v|--verbosity] [--working-dir]`

## <a name="description"></a>설명

`dotnet store`는 지정된 어셈블리를 [런타임 패키지 저장소](../deploying/runtime-store.md)에 저장합니다. 기본적으로 어셈블리는 대상 런타임 및 프레임워크에 최적화됩니다. 자세한 내용은 [런타임 패키지 저장소](../deploying/runtime-store.md) 항목을 참조하세요.

## <a name="required-options"></a>필수 옵션

`-f|--framework <FRAMEWORK>`

[대상 프레임워크](../../standard/frameworks.md)를 지정합니다.

`-m|--manifest <PATH_TO_MANIFEST_FILE>`

*패키지 저장소 매니페스트 파일*은 저장할 패키지 목록이 포함된 XML 파일입니다. 매니페스트 파일 형식은 SDK 스타일 프로젝트 형식과 호환됩니다. 따라서 원하는 패키지를 참조하는 프로젝트 파일을 `-m|--manifest` 옵션과 함께 사용하여 런타임 패키지 저장소에 어셈블리를 저장할 수 있습니다. 여러 매니페스트 파일을 지정하려면 각 파일에 대해 옵션 및 경로를 반복합니다. 예: `--manifest packages1.csproj --manifest packages2.csproj`

`-r|--runtime <RUNTIME_IDENTIFIER>`

대상으로 지정할 [런타임 식별자](../rid-catalog.md)입니다.

## <a name="optional-options"></a>선택적 옵션

`--framework-version <FRAMEWORK_VERSION>`

.NET Core SDK 버전을 지정합니다. 이 옵션을 사용하여 `-f|--framework` 옵션을 통해 지정된 프레임워크가 아닌 특정 프레임워크 버전을 선택할 수 있습니다.

`-h|--help`

도움말 정보를 표시합니다.

`-o|--output <OUTPUT_DIRECTORY>`

런타임 패키지 저장소의 경로를 지정합니다. 지정하지 않으면 기본적으로 사용자 프로필 .NET Core 설치 디렉터리의 *store* 하위 디렉터리가 사용됩니다.

`--skip-optimization`

최적화 단계를 건너뜁니다.

`--skip-symbols`

기호 생성을 건너뜁니다. 현재 Windows 및 Linux에서만 기호를 생성합니다.

`-v|--verbosity <LEVEL>`

명령의 세부 정보 표시 수준을 설정합니다. 허용되는 값은 `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, `diag[nostic]`입니다.

`-w|--working-dir <INTERMEDIATE_WORKING_DIRECTORY>`

명령에서 사용되는 작업 디렉터리입니다. 지정하지 않으면 현재 디렉터리의 *obj* 하위 디렉터리가 사용됩니다.

## <a name="examples"></a>예제

지정된 패키지를 .NET Core 2.0.0에 대한 *packages.csproj* 프로젝트 파일에 저장합니다.

`dotnet store --manifest packages.csproj --framework-version 2.0.0`

지정된 패키지를 최적화 없이 *packages.csproj*에 저장합니다.

`dotnet store --manifest packages.csproj --skip-optimization`

## <a name="see-also"></a>참고 항목

- [런타임 패키지 저장소](../deploying/runtime-store.md)
