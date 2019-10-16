---
title: .NET Framework 및 .NET Core용 프로젝트 구성
description: .NET Framework 및 .NET Core에 대해 솔루션을 나란히 컴파일하려는 프로젝트 소유자를 위한 도움말입니다.
author: conniey
ms.date: 12/07/2018
ms.custom: seodec18
ms.openlocfilehash: 1e120e1aee60e88ea33a8290f3bf36eb93bfc91c
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698928"
---
# <a name="organize-your-project-to-support-both-net-framework-and-net-core"></a>.NET Framework 및 .NET Core를 둘 다 지원하도록 프로젝트 구성

.NET Framework와 .NET Core 둘 다에 대해 나란히 컴파일되는 솔루션을 만드는 방법을 알아봅니다. 이러한 목표를 달성할 수 있도록 프로젝트를 구성하는 여러 가지 옵션을 참조하세요. .NET Core를 사용하여 프로젝트 레이아웃을 설정하는 방법을 결정할 때 고려해야 할 몇 가지 일반적인 시나리오는 다음과 같습니다. 여기에서 모든 것을 다루지는 못할 수 있습니다. 프로젝트 요구에 따라 우선 순위를 정하세요.

* [**기존 프로젝트와 .NET Core 프로젝트를 단일 프로젝트로 결합**](#replace-existing-projects-with-a-multi-targeted-net-core-project)

  *좋은 점:*
  * 각각 다른 .NET Framework 버전 또는 플랫폼을 대상으로 하는 여러 프로젝트를 컴파일하는 것이 아니라 단일 프로젝트를 컴파일함으로써 빌드 프로세스를 간소화합니다.
  * 단일 프로젝트 파일을 관리해야 하므로 멀티 타기팅 프로젝트에 대한 소스 파일 관리를 간소화합니다. 소스 파일을 추가/제거할 때 대체 방법에서는 이를 다른 프로젝트와 수동으로 동기화해야 합니다.
  * 사용할 NuGet 패키지를 쉽게 생성합니다.
  * 컴파일러 지시문을 사용하여 라이브러리에서 특정 .NET Framework 버전에 대한 코드를 작성할 수 있습니다.

  *지원되지 않는 시나리오:*
  * 개발자가 기존 프로젝트를 열려면 Visual Studio 2017을 사용해야 합니다. Visual Studio의 이전 버전을 지원하려면 [프로젝트 파일을 서로 다른 폴더에 유지](#support-vs)하는 것이 더 낫습니다.

* <a name="support-vs"></a>[**기존 프로젝트와 새로운 .NET Core 프로젝트를 별도로 유지**](#keep-existing-projects-and-create-a-net-core-project)

  *좋은 점:*
  * Visual Studio 2017이 없는 개발자/참가자의 경우 업그레이드하지 않고 기존 프로젝트에 대한 개발을 계속 지원할 수 있습니다.
  * 기존 프로젝트에서 코드 변동이 필요하지 않으므로 새 버그가 발생할 가능성이 줄어듭니다.

## <a name="example"></a>예

아래 리포지토리를 고려하세요.

![기존 프로젝트](./media/project-structure/existing-project-structure.png)

[**소스 코드**](https://github.com/dotnet/samples/tree/master/framework/libraries/migrate-library/)

아래에서는 기존 프로젝트의 제약 조건 및 복잡성에 따라 이 리포지토리에 대한 .NET Core 지원을 추가하는 여러 가지 방법을 설명합니다.

## <a name="replace-existing-projects-with-a-multi-targeted-net-core-project"></a>기존 프로젝트를 멀티 타기팅 .NET Core 프로젝트로 교체

기존 *\*.csproj* 파일을 제거하고 여러 프레임워크를 대상으로 하는 단일 *\*.csproj* 파일을 만들도록 리포지토리를 재구성합니다. 서로 다른 프레임워크에 대해 단일 프로젝트를 컴파일할 수 있으므로 이는 좋은 옵션입니다. 대상 프레임워크별로 서로 다른 컴파일 옵션 및 종속성을 처리할 수도 있습니다.

![여러 프레임워크를 대상으로 하는 csproj 만들기](./media/project-structure/multi-targeted-project.png)

[**소스 코드**](https://github.com/dotnet/samples/tree/master/framework/libraries/migrate-library-csproj/)

주목할 변경 사항은 다음과 같습니다.

* *packages.config* 및 *\*.csproj*가 새로운 [.NET Core *\*.csproj*](https://github.com/dotnet/samples/tree/master/framework/libraries/migrate-library-csproj/src/Car/Car.csproj)로 바뀌었습니다. NuGet 패키지가 `<PackageReference> ItemGroup`을 사용하여 지정됩니다.

## <a name="keep-existing-projects-and-create-a-net-core-project"></a>기존 프로젝트를 유지하고 .NET Core 프로젝트 만들기

이전 프레임워크를 대상으로 하는 기존 프로젝트가 있는 경우, 이러한 프로젝트는 그대로 두고 이후 프레임워크를 대상으로 하는 .NET Core를 사용할 수 있습니다.

![다른 폴더에 기존 프로젝트가 있는 .NET Core 프로젝트](./media/project-structure/separate-projects-same-source.png)

[**소스 코드**](https://github.com/dotnet/samples/tree/master/framework/libraries/migrate-library-csproj-keep-existing/)

주목할 변경 사항은 다음과 같습니다.

* .NET Core와 기존 프로젝트가 별도의 폴더에 유지됩니다.
  * 프로젝트를 별도의 폴더에 유지하면 Visual Studio 2017이 없어도 됩니다. 이전 프로젝트만 여는 별도 솔루션을 만들 수 있습니다.

## <a name="see-also"></a>참고 항목

- [.NET Core 이식 설명서](index.md)
