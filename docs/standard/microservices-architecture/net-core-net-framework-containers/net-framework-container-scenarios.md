---
title: Docker 컨테이너에 대해 .NET Framework를 선택하는 경우
description: 컨테이너화된 .NET 응용 프로그램용 .NET 마이크로 서비스 아키텍처 | Docker 컨테이너에 대해 .NET Framework를 선택하는 경우
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/11/2018
ms.openlocfilehash: 128801fbe49a3f7618b1cedc814b7663d57df624
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50195335"
---
# <a name="when-to-choose-net-framework-for-docker-containers"></a>Docker 컨테이너에 대해 .NET Framework를 선택하는 경우

.NET Core는 새 응용 프로그램 및 응용 프로그램 패턴에 상당한 이점을 제공하는 반면, .NET Framework는 계속해서 다양한 기존 시나리오에 적합한 선택 사양이 될 것입니다.

## <a name="migrating-existing-applications-directly-to-a-windows-server-container"></a>기존 응용 프로그램을 Windows Server 컨테이너로 직접 마이그레이션

마이크로 서비스를 만들지 않는 경우에도 Docker 컨테이너를 사용하여 배포를 단순화하려고 할 수 있습니다. 예를 들어 Docker를 사용하여 DevOps 워크플로를 향상시키려는 경우, 컨테이너를 통해 더 효율적으로 격리된 테스트 환경을 제공하고, 프로덕션 환경으로 이동할 때 종속성 누락으로 인한 배포 문제를 제거할 수 있습니다. 이러한 경우 모놀리식 응용 프로그램을 배포하더라도 현재 .NET Framework 응용 프로그램에 Docker 및 Windows 컨테이너를 사용하는 것이 좋습니다.

이 시나리오에서 대부분의 경우 기존 응용 프로그램을 .NET Core로 마이그레이션할 필요가 없습니다. 즉 기존 .NET Framework가 포함된 Docker 컨테이너를 사용하면 됩니다. 그러나 ASP.NET Core에서 새 웹 서비스를 작성하는 것과 같이 기존 응용 프로그램을 확장할 때 .NET Core를 사용하는 것이 좋습니다.

## <a name="using-third-party-net-libraries-or-nuget-packages-not-available-for-net-core"></a>.NET Core에 사용할 수 없는 타사 .NET 라이브러리 또는 NuGet 패키지 사용

타사 라이브러리는 [.NET 표준](../../net-standard.md)을 빠르게 수용하여 .NET Core를 포함한 모든 .NET 계열에서 코드 공유를 사용할 수 있게 합니다. .NET Standard 라이브러리 2.0 이상에서는 서로 다른 프레임워크 간의 API 표면 호환성이 상당히 증가하였으며, .NET Core 2.x에서는 응용 프로그램이 기존 .NET Framework 라이브러리를 직접 참조할 수도 있습니다([호환 shim](https://github.com/dotnet/standard/blob/master/docs/netstandard-20/README.md#net-framework-461-supporting-net-standard-20) 참조).

또한 Windows의 .NET Standard 2.0에 사용할 수 있는 API 노출을 확장하기 위해 2017년 11월에 [Windows 호환성 팩](../../../core/porting/windows-compat-pack.md)이 릴리스되었습니다. 이 팩을 사용하면 수정 사항이 거의 없거나 전혀 없이 Windows에서 실행하도록 대부분의 기존 코드를 .NET Standard 2.x에 다시 컴파일할 수 있습니다.

그러나 .NET Standard 2.0 및 .NET Core 2.1 이후의 뛰어난 발전에도 불구하고 특정 NuGet 패키지에서 Windows를 실행해야 하고 .NET Core를 지원하지 않는 경우가 있을 수도 있습니다. 이러한 패키지가 응용 프로그램에 매우 중요한 경우 Windows 컨테이너에서 .NET Framework를 사용해야 합니다.

## <a name="using-net-technologies-not-available-for-net-core"></a>.NET Core에 사용할 수 없는 .NET 기술 사용 

일부 .NET Framework 기술은 현재 버전의 .NET Core(이 문서를 작성한 시점 이후 버전 2.1)에서 사용할 수 없습니다. 그 중 일부는 이후 .NET Core 릴리스(.NET Core 2.x)에서 사용할 수 있지만, 다른 일부는 .NET Core에서 대상으로 하는 새 응용 프로그램 패턴에 적용되지 않으며 사용하지 못할 수도 있습니다.

다음 목록에서는 .NET Core 2.x에서 사용할 수 없는 대부분의 기술을 보여 줍니다.

-   ASP.NET Web Forms. 이 기술은 .NET Framework에서만 사용할 수 있습니다. 현재 .NET Core에 ASP.NET Web Forms를 적용할 계획은 없습니다.

-   WCF 서비스. .NET Core에서 WCF 서비스를 사용할 수 있는 [WCF-클라이언트 라이브러리](https://github.com/dotnet/wcf)가 있더라도(2017년 중순 기준) WCF 서버 구현은 .NET Framework에서만 사용할 수 있습니다. 이 시나리오는 .NET Core의 향후 릴리스에 대해 고려할 수 있으며, 이 경우 [Windows 호환성 팩](../../../core/porting/windows-compat-pack.md)에 일부 API를 포함하도록 고려되고 있습니다.

-   워크플로 관련 서비스. Windows WF(Workflow Foundation), 워크플로 서비스(단일 서비스의 WCF + WF) 및 WCF Data Services(이전의 ADO.NET Data Services)는 .NET Framework에서만 사용할 수 있습니다. 현재 .NET Core로 가져올 계획은 없습니다.

공식 [.NET Core 로드맵](https://github.com/aspnet/Home/wiki/Roadmap)에 나열된 기술 외에도 다른 기능이 .NET Core에 이식될 수도 있습니다. 전체 목록은 CoreFX GitHub 사이트에서 [port-to-core](https://github.com/dotnet/corefx/issues?q=is%3Aopen+is%3Aissue+label%3Aport-to-core) 태그로 지정된 항목을 살펴보세요. 이 목록은 이러한 구성 요소를 .NET Core로 가져오는 Microsoft의 약속을 나타내지는 않으며, 항목은 단순히 커뮤니티의 요청만 캡처합니다. 위에 나열된 구성 요소 중 하나에 관심이 있는 경우 자신의 의견에 대해 답변을 받을 수 있도록 GitHub의 토론에 참여해 보세요. 누락된 내용이 있다고 생각이 들면 [CoreFX 리포지토리에 새로운 문제를 등록](https://github.com/dotnet/corefx/issues/new)하세요.

.NET Core 3(이 쓰기가 진행 중일 때)가 기존 .NET Framework API에 대한 지원을 포함하더라도, 이는 데스크톱 지향이므로 현재 컨테이너에서 사용하고 있지 않습니다.

## <a name="using-a-platform-or-api-that-does-not-support-net-core"></a>.NET Core를 지원하지 않는 플랫폼 또는 API 사용

일부 Microsoft 또는 타사 플랫폼은 .NET Core를 지원하지 않습니다. 예를 들어 일부 Azure 서비스는 .NET Core에서 아직 사용할 수 없는 SDK를 제공합니다. 모든 Azure 서비스에서 결국에는 .NET Core를 사용할 것이므로 이는 일시적인 현상입니다. 예를 들어 [.NET Core용 Azure DocumentDB SDK](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/1.2.1)는 2016년 11월 16일에 미리 보기로 릴리스되었지만 이제는 안정적인 GA(일반 공급) 버전으로 사용할 수 있습니다.

그동안 Azure의 플랫폼 또는 서비스에서 여전히 클라이언트 API를 통해 .NET Core를 지원하지 않는 경우에는 Azure 서비스 또는 .NET Framework의 클라이언트 SDK에서 동등한 REST API를 사용할 수 있습니다.

### <a name="additional-resources"></a>추가 자료

-   **.NET Core 가이드**  
    [https://docs.microsoft.com/dotnet/core/index](../../../core/index.md)

-   **.NET Framework에서 .NET Core로 이식**  
    [https://docs.microsoft.com/dotnet/core/porting/index](../../../core/porting/index.md)

-   **Docker 가이드의 .NET Framework**  
    [https://docs.microsoft.com/dotnet/framework/docker/](../../../framework/docker/index.md)

-   **.NET 구성 요소 개요**  
    [https://docs.microsoft.com/dotnet/standard/components](../../components.md)




>[!div class="step-by-step"]
[이전](net-core-container-scenarios.md)
[다음](container-framework-choice-factors.md)
