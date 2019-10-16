---
title: 고품질 .NET 라이브러리 만들기 시작
description: .NET 라이브러리 빌드를 시작합니다.
author: jamesnk
ms.author: mairaw
ms.date: 10/02/2018
ms.openlocfilehash: 980f0edcee07688935f6d08f3ce1ed812159695e
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65640740"
---
# <a name="get-started"></a>시작

## <a name="cross-platform-targetingcross-platform-targetingmd"></a>[플랫폼 간 대상 지정](./cross-platform-targeting.md)

.NET Standard 및 멀티 타기팅을 사용하여 플랫폼 간 라이브러리를 만드는 방법입니다. .NET은 많은 장소에서 실행되며, 좋은 .NET 라이브러리는 가능한 한 많은 플랫폼과 개발자를 지원하려고 해야 합니다.

## <a name="strong-namingstrong-namingmd"></a>[강력한 이름 지정](./strong-naming.md)

강력한 이름 지정과 장점 및 단점에 대해 알아봅니다. .NET 라이브러리에 강력한 이름을 지정하면 대부분의 개발자가 라이브러리를 사용할 수 있으므로 권장되는 모범 사례입니다.

## <a name="nuget-and-open-source-librariesnugetmd"></a>[NuGet 및 오픈 소스 라이브러리](./nuget.md)

NuGet.org에 공개적으로 게시된 모든 패키지에 대한 권장 메타데이터를 포함하여 오픈 소스 .NET 라이브러리용 NuGet 패키지를 만드는 최상의 방법입니다.

### <a name="dependenciesdependenciesmd"></a>[종속성](./dependencies.md)

NuGet을 사용하면 .NET 라이브러리를 빌드할 때 기존 패키지를 쉽게 이용할 수 있습니다. NuGet 종속성의 일반적인 마찰 소스와 이를 방지하는 방법을 알아봅니다.

### <a name="source-linksourcelinkmd"></a>[소스 링크](./sourcelink.md)

소스 링크는 .NET 라이브러리의 사용자가 디버그하는 동안 해당 소스 코드를 한 단계씩 실행할 수 있게 해주는 훌륭한 도구입니다. 이 문서는 소스 링크란 무엇이고 왜 사용해야 하는지에 대한 개요입니다.

### <a name="publishingpublish-nuget-packagemd"></a>[게시](./publish-nuget-package.md)

NuGet.org가 가장 널리 알려지고 사용되는 리포지토리지만, NuGet 패키지는 여러 장소에 게시할 수 있습니다. 사용할 수 있는 다양한 NuGet 패키지 리포지토리와 .NET 라이브러리 게시에 대한 보안 모범 사례를 알아봅니다.

## <a name="versioningversioningmd"></a>[버전 관리](./versioning.md)

훌륭한 .NET 라이브러리는 시간이 지남에 따라 발전하며, 이후 릴리스에서 기능을 추가하고, 버그를 수정하고, 성능을 개선합니다. 다양한 버전 번호와 개발자에게 호환성이 손상되는 변경 사항을 전달하는 방법을 알아봅니다.

### <a name="breaking-changesbreaking-changesmd"></a>[주요 변경 사항](./breaking-changes.md)

.NET 라이브러리에서 기존 사용자를 위한 안정성과 미래를 위한 혁신 간에 균형을 맞추는 것이 중요합니다. 이전 버전과의 호환성을 유지하면서 새로운 기능을 추가하기 위한, 여러 종류의 호환성이 손상되는 변경 및 전략에 대해 알아봅니다.

>[!div class="step-by-step"]
>[이전](index.md)
>[다음](cross-platform-targeting.md)
