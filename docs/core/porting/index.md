---
title: .NET Framework에서 .NET Core로 코드 포팅
description: 이식 프로세스를 이해하고 .NET Framework 프로젝트를 .NET Core로 이식할 때 유용한 도구에 관해 알아보세요.
author: cartermp
ms.date: 09/13/2019
ms.custom: seodec18
ms.openlocfilehash: b6c02932b5d9c7ccc2743dd38dddf2904f9c24e4
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71039656"
---
# <a name="port-your-code-from-net-framework-to-net-core"></a>.NET Framework에서 .NET Core로 코드 포팅

.NET Framework에서 실행되는 코드를 사용한 적이 있다면 .NET Core에서 코드를 실행하는 것에도 관심이 있을 수 있습니다. 여기서는 포팅 프로세스 및 코드를 .NET Core로 포팅할 때 유용할 수 있는 도구 목록을 간략하게 설명합니다.

## <a name="overview-of-the-porting-process"></a>포팅 프로세스 개요

프로젝트를 .NET Core로 포팅할 때 권장되는 프로세스입니다. 프로세스의 각 단계는 향후 문서에서 자세히 설명합니다.

1. 타사 종속성을 식별하고 확인합니다.

   이 단계에서는 타사 종속성의 개념, 사용 방법, .NET Core에서도 실행되는지 확인하는 방법 및 실행되지 않을 경우 수행할 수 있는 단계를 파악해야 합니다. .NET Core에 사용되는 [PackageReference](/nuget/consume-packages/package-references-in-project-files) 형식으로 종속성을 마이그레이션하는 방법에 대해서도 설명합니다.

2. 포팅하려는 모든 프로젝트의 대상을 .NET Framework 4.7.2 이상으로 다시 지정합니다.

   이 단계에서는 .NET Core에서 특정 API를 지원하지 않는 경우 .NET Framework 특정 대상에 대한 API 대안을 사용할 수 있도록 합니다.

3. [.NET Portability Analyzer](../../standard/analyzers/portability-analyzer.md)를 사용하여 어셈블리를 분석하고 결과에 따라 이식 계획을 수립합니다.

   API 이식성 분석기 도구는 컴파일된 어셈블리를 분석하고 개괄적인 이식성 요약 및 대상 .NET Core 플랫폼 공개 화면에서 사용할 수 없는 사용 중인 각 API에 대한 분석 결과를 보여 주는 보고서를 생성합니다. 코드베이스에 대한 분석과 함께 이 보고서를 사용하여 코드를 이식할 방법에 대한 계획을 개발할 수 있습니다.

4. 프로젝트 파일을 대상 .NET Core 버전으로 변환하면 Roslyn 기반 [.NET API 분석기](../../standard/analyzers/api-analyzer.md)를 사용하여 일부 플랫폼에서 throw하는 API <xref:System.PlatformNotSupportedException> 및 일부 다른 잠재적인 호환성 문제를 식별할 수 있습니다.

5. 테스트 코드를 이식합니다.

   .NET Core로 포팅하면 코드베이스가 많이 변경되기 때문에 코드를 포팅할 때 테스트를 실행할 수 있도록 테스트를 포팅하는 것이 좋습니다. MSTest, xUnit 및 NUnit는 모두 .NET Core를 지원합니다.

6. 이식에 대한 계획을 실행합니다.

다음 목록은 포팅 프로세스 중에 사용하면 도움이 되는 도구를 보여 줍니다.

* .NET 이식성 분석기 - [명령줄 도구](https://github.com/Microsoft/dotnet-apiport/releases) 또는 [Visual Studio Extension](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)으로, .NET Framework와 대상 .NET Core 간에 코드를 이식할 수 있는 정도에 대한 보고서를 생성할 수 있는 도구입니다. 이 보고서에는 대상 .NET Core 플랫폼에서 누락된 유형 및 API의 어셈블리별 분석이 포함되어 있습니다. 자세한 내용은 [.NET 이식성 분석기](../../standard/analyzers/portability-analyzer.md)를 참조하세요. 특정 대상 .NET 플랫폼 공개 화면에서 누락된 API의 간격을 식별하는 데 도움이 되므로 이식을 시작하기 전에 .NET 이식성 분석기 도구를 실행하는 것이 좋습니다.
* .NET API 분석기 - 여러 플랫폼에서 <xref:System.PlatformNotSupportedException>을 throw하는 .NET Standard API를 검색하고 더 이상 사용되지 않는 호출을 탐색하며, 다른 플랫폼에서 C# API에 대한 잠재적 호환성 위험을 검색하는 Roslyn 분석기입니다. 자세한 내용은 [.NET API 분석기](../../standard/analyzers/api-analyzer.md)를 참조하세요. 이 분석기는 이미 다른 플랫폼에서 런타임 동작의 차이점을 식별하기 위해 .NET Core 프로젝트를 만든 후에 유용합니다.
* 역방향 패키지 검색 - 형식을 검색하고 해당 형식을 포함하는 패키지를 찾을 수 있는 [유용한 웹 서비스](https://packagesearch.azurewebsites.net)입니다.

또한 [CsprojToVs2017](https://github.com/hvanbakel/CsprojToVs2017) 도구를 사용하여 작은 솔루션 또는 개별 프로젝트를 .NET Core 프로젝트 파일 형식으로 포팅할 수 있습니다.

> [!WARNING]
> CsprojToVs2017은 타사 도구입니다. 모든 프로젝트에서 작동한다는 보장은 없으며, 사용하는 동작이 미묘하게 변경될 수도 있습니다. CsprojToVs2017은 자동화할 수 있는 기본 사항을 자동화하는 _시작점_으로 사용해야 합니다. 프로젝트 파일 형식을 마이그레이션하는 보장된 솔루션은 아닙니다.

>[!div class="step-by-step"]
>[다음](net-framework-tech-unavailable.md)
