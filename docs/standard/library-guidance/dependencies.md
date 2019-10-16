---
title: 종속성 및 .NET 라이브러리
description: .NET 라이브러리에서 NuGet 종속성을 관리하는 모범 사례 권장 사항입니다.
author: jamesnk
ms.author: mairaw
ms.date: 10/02/2018
ms.openlocfilehash: 0cd00ff36ad52bc46769ca1793b9efd02db14da1
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65644257"
---
# <a name="dependencies"></a>종속성

.NET 라이브러리에 종속성을 추가하는 기본 방법은 NuGet 패키지를 참조하는 것입니다. NuGet 패키지 참조를 사용하면 이미 작성된 기능을 빠르게 다시 사용하고 활용할 수 있지만 .NET 개발자에게는 일반적인 마찰 소스이기도 합니다. 종속성을 올바르게 관리하는 것은 다른 .NET 라이브러리의 변경 내용으로 인한 사용자 .NET 라이브러리의 중단이나 그 반대의 경우를 방지하는 데 중요합니다.

## <a name="diamond-dependencies"></a>다이아몬드 종속성

.NET 프로젝트의 종속성 트리에 여러 버전의 패키지가 포함되는 것이 일반적인 상황입니다. 예를 들어 앱이 두 개의 NuGet 패키지에 종속되어 있고, 각 패키지는 동일한 패키지의 서로 다른 버전에 종속되어 있습니다. 이제 앱의 종속성 그래프에 다이아몬드 종속성이 있습니다.

![다이아몬드 종속성](./media/dependencies/diamond-dependency.png "다이아몬드 종속성")

빌드 시 NuGet은 종속성의 종속성을 포함하여 프로젝트가 종속된 모든 패키지를 분석합니다. 패키지의 여러 버전이 검색되면 규칙을 평가하여 하나를 선택합니다. .NET에서 동일한 애플리케이션에 있는 어셈블리의 병렬 버전을 실행하면 문제가 발생하기 때문에 패키지를 통합해야 합니다.

대부분의 다이아몬드 종속성은 쉽게 확인되지만 다음과 같은 특정 상황에서 문제가 발생할 수 있습니다.

1. **NuGet 패키지 참조가 충돌**하는 경우 패키지 복원 중에 버전이 확인되지 않습니다.
2. **버전 간에 호환성이 손상되는 변경**이 있는 경우 런타임 시 버그와 예외가 발생합니다.
3. **패키지 어셈블리에 강력한 이름이 지정**되었고, 어셈블리 버전이 변경되었으며, 앱이 .NET Framework에서 실행되고 있습니다. 어셈블리 바인딩 리디렉션이 필요합니다.

사용자 고유의 패키지와 함께 사용할 패키지를 알 수 없습니다. 다이아몬드 종속성으로 인한 라이브러리 중단 가능성을 줄이는 좋은 방법은 사용자가 종속되는 패키지 수를 최소화하는 것입니다.

**✔️** 사용자 .NET 라이브러리에서 불필요한 종속성을 검토합니다.

## <a name="nuget-dependency-version-ranges"></a>NuGet 종속성 버전 범위

패키지 참조는 허용하는 유효한 패키지 범위를 지정합니다. 일반적으로 프로젝트 파일의 패키지 참조 버전은 최소 버전이며 최댓값은 없습니다.

```xml
<!-- Accepts any version 1.0 and above. -->
<PackageReference Include="ExamplePackage" Version="1.0" />
```

NuGet에서 종속성을 확인할 때 사용하는 규칙은 [복잡](/nuget/consume-packages/dependency-resolution)하지만 NuGet은 항상 적용 가능한 가장 낮은 버전을 찾습니다. 가장 낮은 버전에서 호환성 문제가 가장 적기 때문에 NuGet은 사용 가능한 가장 높은 버전보다 적용 가능한 가장 낮은 버전을 선호합니다.

NuGet의 적용 가능한 가장 낮은 버전 규칙 때문에 최신 버전을 가져오지 않도록 패키지 참조에 상위 버전이나 정확한 범위를 배치할 필요가 없습니다. NuGet이 이미 가장 낮고, 가장 호환되는 버전을 찾으려고 시도합니다.

```xml
<!-- Accepts 1.0 up to 1.x, but not 2.0 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.0,2.0)" />

<!-- Accepts exactly 1.0. -->
<PackageReference Include="ExamplePackage" Version="[1.0]" />
```

충돌이 있을 경우 상위 버전 제한으로 인해 NuGet이 실패합니다. 예를 들어 한 라이브러리는 정확히 1.0을 허용하는 반면, 다른 라이브러리에는 2.0 이상이 필요합니다. 버전 2.0에서 호환성이 손상되는 변경이 도입되었을 수도 있지만, 엄격한 버전 종속성 또는 상한 버전 종속성이 적용되어 오류가 발생합니다.

![다이아몬드 종속성 충돌](./media/dependencies/diamond-dependency-conflict.png "다이아몬드 종속성 충돌")

**❌** 최소 버전이 없는 NuGet 패키지 참조를 사용하지 않습니다.

**❌ 회피** 정확한 버전을 요구하는 NuGet 패키지 참조입니다.

**❌** 버전 상한이 있는 NuGet 패키지 참조를 사용하지 않습니다.

## <a name="nuget-shared-source-packages"></a>NuGet 공유 소스 패키지

외부 NuGet 패키지 종속성을 줄이는 한 가지 방법은 공유 소스 패키지를 참조하는 것입니다. 공유 소스 패키지에는 참조 시 프로젝트에 포함되는 [소스 코드 파일](/nuget/reference/nuspec#including-content-files)이 들어 있습니다. 프로젝트의 나머지 부분과 함께 컴파일되는 소스 코드 파일만 포함하기 때문에 외부 종속성 및 충돌 가능성이 없습니다.

공유 소스 패키지는 작은 기능 집합을 포함하는 데 유용합니다. HTTP 호출을 수행하기 위한 도우미 메서드의 공유 소스 패키지를 예로 들 수 있습니다.

![공유 소스 패키지](./media/dependencies/shared-source-package.png "공유 소스 패키지")

```xml
<PackageReference Include="Microsoft.Extensions.Buffers.Testing.Sources" PrivateAssets="All" Version="1.0" />
```

![공유 소스 프로젝트](./media/dependencies/shared-source-project.png "공유 소스 프로젝트")

공유 소스 패키지에는 몇 가지 제한 사항이 있습니다. `PackageReference`에서만 참조할 수 있으므로, 이전 `packages.config` 프로젝트는 제외됩니다. 또한 공유 소스 패키지는 동일한 언어 형식의 프로젝트에서만 사용할 수 있습니다. 이러한 제한 사항 때문에 공유 소스 패키지는 오픈 소스 프로젝트 내에서 기능을 공유하는 데 가장 좋습니다.

**✔️** 작은 내부 기능 집합을 위해 공유 소스 패키지를 참조합니다.

**✔️** 작은 내부 기능 집합을 제공하는 경우 사용자 패키지를 공유 소스 패키지로 설정합니다.

**✔️** `PrivateAssets="All"`을 사용하여 공유 소스 패키지를 참조합니다.

> 이 설정은 개발할 때만 패키지를 사용하고 공용 종속성으로 노출하지 않도록 NuGet에 지시합니다.

**❌** 공용 API에 공유 소스 패키지 형식을 포함하지 않습니다.

> 공유 소스 형식은 참조 어셈블리로 컴파일되며 어셈블리 경계를 넘어 교환할 수 없습니다. 예를 들어 한 프로젝트에 있는 공유 소스 `IRepository` 형식은 다른 프로젝트에 있는 동일한 공유 소스 `IRepository`와 별개의 형식입니다. 공유 소스 패키지의 형식에 `internal` 가시성이 있어야 합니다.

**❌** 공유 소스 패키지를 NuGet.org에 게시하지 마세요.

> 공유 소스 패키지에는 소스 코드가 들어 있으며 동일한 언어 형식의 프로젝트에서만 사용할 수 있습니다. 예를 들어 C# 공유 소스 패키지는 F# 애플리케이션에서 사용할 수 없습니다.
>
> 공유 소스 패키지를 [로컬 피드 또는 MyGet](./publish-nuget-package.md)에 게시하여 프로젝트 내에서 내부적으로 사용합니다.

>[!div class="step-by-step"]
>[이전](nuget.md)
>[다음](sourcelink.md)
