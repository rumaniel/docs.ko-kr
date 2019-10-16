---
title: 버전 관리 및 .NET 라이브러리
description: .NET 라이브러리의 버전을 관리하는 모범 사례 권장 사항입니다.
author: jamesnk
ms.author: mairaw
ms.date: 12/10/2018
ms.openlocfilehash: 9250e48707c0ea72cdf8bef9663f5a3516309b86
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70969016"
---
# <a name="versioning"></a>버전 관리

소프트웨어 라이브러리가 버전 1.0에서 완성되는 경우는 거의 없습니다. 훌륭한 라이브러리는 시간이 지남에 따라 발전하며, 기능을 추가하고, 버그를 수정하고, 성능을 개선합니다. 기존 사용자를 중단하지 않고 각 버전에서 추가 가치를 제공하여 .NET 라이브러리의 새 버전을 릴리스하는 것이 중요합니다.

## <a name="breaking-changes"></a>호환성이 손상되는 변경

버전 간의 호환성이 손상되는 변경 처리에 대한 자세한 내용은 [호환성이 손상되는 변경](./breaking-changes.md)을 참조하세요.

## <a name="version-numbers"></a>버전 번호

.NET 라이브러리에는 버전을 지정하는 여러 가지 방법이 있습니다. 가장 중요한 버전은 다음과 같습니다.

### <a name="nuget-package-version"></a>NuGet 패키지 버전

[NuGet 패키지 버전](/nuget/reference/package-versioning)은 Visual Studio NuGet 패키지 관리자인 NuGet.org에 표시되고 패키지를 사용할 때 소스 코드에 추가됩니다. NuGet 패키지 버전은 사용자에게 일반적으로 표시되는 버전 번호이며, 사용 중인 라이브러리 버전을 말할 때는 이 버전을 가리킵니다. NuGet 패키지 버전은 NuGet에서 사용되며 런타임 동작에는 영향을 미치지 않습니다.

```xml
<PackageVersion>1.0.0-alpha1</PackageVersion>
```

NuGet 패키지 식별자와 NuGet 패키지 버전을 결합하여 NuGet에서 패키지를 식별합니다. 예: `Newtonsoft.Json` + `11.0.2`. 접미사가 있는 패키지는 시험판 패키지이며, 테스트에 적합하게 하는 특수 동작이 있습니다. 자세한 내용은 [시험판 패키지](./nuget.md#pre-release-packages)를 참조하세요.

NuGet 패키지 버전은 개발자가 가장 보기 쉬운 버전이므로 [SemVer(유의적 버전)](https://semver.org/)를 사용하여 업데이트하는 것이 좋습니다. SemVer는 릴리스 간 변경 내용의 중요도를 나타내며, 개발자가 사용할 버전을 선택할 때 정확하고 합리적으로 결정할 수 있도록 지원합니다. 예를 들어 `1.0`에서 `2.0`으로 이동하는 경우 호환성이 손상되는 변경이 있을 수 있습니다.

**✔️ 고려** [SemVer 2.0.0](https://semver.org/)을 사용하여 NuGet 패키지 버전을 관리합니다.

**✔️** 사용자에게 일반적으로 표시되는 버전 번호인 NuGet 패키지 버전을 공용 문서에서 사용합니다.

**✔️** 불안정한 패키지를 릴리스할 때는 시험판 접미사를 포함합니다.

> 사용자는 시험판 패키지를 가져오기 위해 옵트인해야 하므로 패키지가 불완전함을 알 수 있습니다.

### <a name="assembly-version"></a>어셈블리 버전

어셈블리 버전은 CLR에서 런타임 시 로드할 어셈블리 버전을 선택하는 데 사용하는 버전입니다. 버전 관리를 사용한 어셈블리 선택은 강력한 이름의 어셈블리에만 적용됩니다.

```xml
<AssemblyVersion>1.0.0.0</AssemblyVersion>
```

Windows .NET Framework CLR에서는 정확히 일치해야 강력한 이름의 어셈블리를 로드할 수 있습니다. 예를 들어 `Libary1, Version=1.0.0.0`은 `Newtonsoft.Json, Version=11.0.0.0`을 참조하여 컴파일되었습니다. .NET Framework는 정확한 버전인 `11.0.0.0`만 로드합니다. 런타임 시 다른 버전을 로드하려면 .NET 애플리케이션의 구성 파일에 바인딩 리디렉션을 추가해야 합니다.

강력한 이름 지정과 어셈블리 버전을 결합하면 [엄격한 어셈블리 버전 로드](../assembly/versioning.md)를 사용할 수 있습니다. 라이브러리에 강력한 이름을 지정하면 여러 가지 혜택이 있지만, 어셈블리를 찾을 수 없는 런타임 예외가 자주 발생하며 `app.config`/`web.config`의 [바인딩 리디렉션](../../framework/configure-apps/redirect-assembly-versions.md)을 수정해야 합니다. .NET Core 어셈블리 로드가 완화되었으며, .NET Core CLR이 런타임에 상위 버전의 어셈블리를 자동으로 로드합니다.

**✔️** AssemblyVersion에 주 버전만 포함합니다.

> 예: 라이브러리 1.0 및 라이브러리 1.0.1의 AssemblyVersion은 둘 다 `1.0.0.0`인 반면, 라이브러리 2.0의 AssemblyVersion은 `2.0.0.0`입니다. 어셈블리 버전의 변경 빈도가 낮으면 바인딩 리디렉션이 줄어듭니다.

**✔️** AssemblyVersion의 주 버전 번호와 NuGet 패키지 버전을 동기화 상태로 유지합니다.

> AssemblyVersion은 사용자에게 표시되는 일부 정보 메시지(예: 예외 메시지의 어셈블리 이름 및 어셈블리 한정 형식 이름)에 포함됩니다. 버전 간의 관계를 유지 관리하면 사용 중인 버전에 대한 자세한 정보가 개발자에게 제공됩니다.

**❌** 고정된 AssemblyVersion을 사용하지 않습니다.

> AssemblyVersion이 변경되지 않는 경우 바인딩 리디렉션이 필요하지 않지만, 단일 어셈블리 버전만 GAC(전역 어셈블리 캐시)에 설치할 수 있습니다. 또한 다른 애플리케이션이 GAC 어셈블리를 호환성이 손상되는 변경으로 업데이트하는 경우 GAC에 있는 어셈블리를 참조하는 애플리케이션이 손상됩니다.

### <a name="assembly-file-version"></a>어셈블리 파일 버전

어셈블리 파일 버전은 Windows에서 파일 버전을 표시하는 데 사용되며 런타임 동작에는 영향을 미치지 않습니다. 이 버전 설정은 선택 사항입니다. Windows 탐색기의 파일 속성 대화 상자에 표시됩니다.

```xml
<FileVersion>11.0.2.21924</FileVersion>
```

![Windows 탐색기](./media/versioning/win-properties.png "Windows 탐색기")

**✔️** 연속 통합 빌드 번호를 AssemblyFileVersion 수정으로 포함합니다.

> 예를 들어 프로젝트 버전 1.0.0을 빌드 중이며 연속 통합 빌드 번호가 99인 경우 AssemblyFileVersion은 1.0.0.99입니다.

**✔️ DO(수행하세요)** 는 파일 버전에 대해 `Major.Minor.Build.Revision` 형식을 사용합니다.

> .NET에서는 파일 버전을 사용하지 않지만 [Windows에서는 파일 버전](/windows/desktop/menurc/versioninfo-resource)이 `Major.Minor.Build.Revision` 형식이어야 합니다. 버전이 이 형식을 따르지 않으면 경고가 발생합니다.

### <a name="assembly-informational-version"></a>어셈블리 정보 버전

어셈블리 정보 버전은 추가 버전 정보를 기록하는 데 사용되며 런타임 동작에는 영향을 미치지 않습니다. 이 버전 설정은 선택 사항입니다. 소스 링크를 사용하는 경우 이 버전은 NuGet 패키지 버전과 소스 제어 버전을 사용하여 빌드에서 설정됩니다. 예를 들어 `1.0.0-beta1+204ff0a`는 어셈블리 빌드에 사용된 소스 코드의 커밋 해시를 포함합니다. 자세한 내용은 [소스 링크](./sourcelink.md)를 참조하세요.

```xml
<AssemblyInformationalVersion>The quick brown fox jumped over the lazy dog.</AssemblyInformationalVersion>
```

> [!NOTE]
> 이 버전이 `Major.Minor.Build.Revision` 형식을 따르지 않으면 이전 버전의 Visual Studio에서는 빌드 경고가 발생합니다. 경고는 무시해도 됩니다.

**❌** 어셈블리 정보 버전을 직접 설정하지 않습니다.

> SourceLink에서 NuGet 및 소스 제어 메타데이터가 포함된 버전을 자동으로 생성하도록 허용합니다.

>[!div class="step-by-step"]
>[이전](publish-nuget-package.md)
>[다음](breaking-changes.md)
