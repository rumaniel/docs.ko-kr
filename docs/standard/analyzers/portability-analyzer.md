---
title: .NET 이식성 분석기 - .NET
description: .NET 이식성 분석기 도구를 사용하여 .NET Core, .NET Standard, UWP 및 Xamarin을 비롯한 다양한 .NET 구현에서 코드가 얼마나 이식성이 있는지 평가하는 방법을 알아봅니다.
ms.date: 09/13/2019
ms.technology: dotnet-standard
ms.assetid: 0375250f-5704-4993-a6d5-e21c499cea1e
ms.openlocfilehash: 246c1d25a99e61d7e2f69f1b65ae3534d22571ba
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053996"
---
# <a name="the-net-portability-analyzer"></a>.NET 이식성 분석기

라이브러리가 다중 플랫폼을 지원하도록 만들고 싶으세요? .NET Framework 애플리케이션을 .NET Core에서 실행하는 데 필요한 작업량을 확인하고 싶으세요?  [.Net 이식성 분석기](https://github.com/microsoft/dotnet-apiport)는 어셈블리를 분석하여 지정된 대상 .NET 플랫폼에 이식할 수 있는 애플리케이션 또는 라이브러리에 대해 누락된 .NET API에 대한 자세한 보고서를 제공하는 도구입니다. 이식성 분석기는 프로젝트당 어셈블리를 분석하는 [Visual Studio 확장](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) 및 지정된 파일 또는 디렉터리별로 어셈블리를 분석하는 [ApiPort 콘솔 앱](https://aka.ms/apiportdownload)으로 제공됩니다.

프로젝트를 .NET Core와 같은 대상 플랫폼을 대상으로 하도록 변환하고 나면 Roslyn 기반 [API 분석기 도구]([https://docs.microsoft.com/en-us/dotnet/standard/analyzers/api-analyzer](api-analyzer.md)를 사용하여 PlatformNotSupportedException 및 일부 다른 호환성 문제를 발생시키는 API를 식별할 수 있습니다.

## <a name="common-targets"></a>공통 대상

- [.NET Core](../../core/index.md): 모듈형 디자인을 포함하고, Side-by-Side를 이용하며, 플랫폼 간 시나리오를 대상으로 합니다. Side-by-Side를 사용하면 다른 앱을 중단하지 않고 새로운 .NET Core 버전을 채택할 수 있습니다. 플랫폼 간을 지원하는 .NET Core에 앱을 이식하는 것이 목표인 경우에 권장되는 대상입니다. 
- .[NET Standard](../../standard/net-standard.md): 모든 .NET 구현에서 사용할 수 있는 .NET Standard API를 포함합니다. 모든 .NET 지원 플랫폼에서 라이브러리를 실행하도록 하는 것이 목표인 경우에 권장되는 대상입니다.  
- [ASP.NET Core](/aspnet/core): 최신 웹 프레임워크는 .NET Core를 기반으로 합니다. 웹앱을 .NET Core에 이식하여 여러 플랫폼을 지원하는 것이 목표인 경우에 권장되는 대상입니다.
- .NET Core + [플랫폼 확장](../../core/porting/windows-compat-pack.md): 많은 .NET Framework 가용 기술을 제공하는 Windows Compatibility Pack 외에도 .NET Core API가 포함되어 있습니다. 이는 .NET Framework에서 Windows의 .NET Core로 앱을 이식하기 위해 권장되는 대상입니다.
- .NET Standard + [플랫폼 확장](../../core/porting/windows-compat-pack.md): 많은 .NET Framework 가용 기술을 제공하는 Windows Compatibility Pack 외에도 .NET Standard API가 포함되어 있습니다. 이는 .NET Framework에서 Windows의 .NET Core로 라이브러리를 이식하기 위해 권장되는 대상입니다.

## <a name="how-to-use-the-net-portability-analyzer"></a>.NET 이식성 분석기를 사용하는 방법

Visual Studio에서 .NET 이식성 분석기 사용을 시작하려면 먼저 [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)에서 확장을 다운로드하고 설치해야 합니다. Visual Studio 2017 이상에서 작동합니다. **분석** > **이식성 분석기 설정**을 통해 Visual Studio에서 구성하고 대상 플랫폼을 선택할 수 있습니다. 이 플랫폼은 현재 어셈블리가 빌드된 플랫폼/버전과 비교하여 이식성 간격을 평가하려는 .NET 플랫폼/버전입니다.

![이식성 스크린샷](./media/portability-analyzer/portability-screenshot.png)

ApiPort 콘솔 애플리케이션을 사용하여 [ApiPort 리포지토리](https://aka.ms/apiportdownload)에서 다운로드할 수도 있습니다. `listTargets` 명령 옵션을 사용하여 사용 가능한 대상 목록을 표시한 다음, `-t` 또는 `--target` 명령 옵션을 지정하여 대상 플랫폼을 선택할 수 있습니다. 

### <a name="analyze-portability"></a>이식성 분석
Visual Studio에서 전체 프로젝트를 분석하려면 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **어셈블리 이식성 분석**을 선택합니다. 전체 프로젝트를 분석하지 않으려면 **분석** 메뉴로 이동한 다음 **어셈블리 이식성 분석**을 선택합니다. 여기서 프로젝트의 실행 파일 또는 DLL을 선택합니다.

![솔루션 탐색기에서 이식성 분석기](./media/portability-analyzer/portability-solution-explorer.png)

[ApiPort 콘솔 앱](https://aka.ms/apiportdownload)을 사용할 수도 있습니다. 

- 현재 디렉터리를 분석하려면 다음 명령을 입력합니다. `ApiPort.exe analyze -f .`
- .dll 파일의 특정 목록을 분석하려면 다음 명령을 입력합니다. `ApiPort.exe analyze -f first.dll -f second.dll -f third.dll`
- 자세한 도움말을 가져오려면 `ApiPort.exe -?`를 실행합니다.

소유하고 이식하려는 모든 관련 exe 및 dll 파일을 포함시키고, 앱이 종속되어 있지만 소유하지 않고 이식할 수 없는 파일은 제외하는 것이 좋습니다. 이렇게 하면 가장 관련성이 높은 이식성 보고서가 제공됩니다.  

### <a name="view-and-interpret-portability-result"></a>이식성 결과 보기 및 해석

대상 플랫폼에서 지원되지 않는 API만 보고서에 표시됩니다. Visual Studio에서 분석을 실행한 후 .NET 이식성 보고서 파일 링크가 팝업으로 나타납니다. [ApiPort 콘솔 앱](https://aka.ms/apiportdownload)을 사용하는 경우 .NET 이식성 보고서는 지정한 형식으로 파일로 저장됩니다. 기본값은 현재 디렉터리의 Excel 파일( *.xlsx*)에 있습니다.

#### <a name="portability-summary"></a>이식성 요약 

![이식성 요약](./media/portability-analyzer/portabilitysummary.png)

보고서의 이식성 요약 섹션에는 실행에 포함된 각 어셈블리에 대한 이식성 백분율이 표시됩니다. 이전 예제에서 `svcutil` 앱에 사용되는 .NET Framework API의 71.24%는 .NET Core + 플랫폼 확장에서 사용할 수 있습니다. 여러 어셈블리에 대해 .NET Portability Analyzer 도구를 실행하는 경우 각 어셈블리에는 이식성 요약 보고서에 행이 있어야 합니다.

#### <a name="details"></a>세부 정보

![이식성 세부 정보](./media/portability-analyzer/portabilitydetails.png)

보고서의 **세부 정보** 섹션에는 선택된 **대상 플랫폼**에서 누락된 API가 나열되어 있습니다. 

- 대상 유형: 형식에는 대상 플랫폼에서 API가 누락되어 있습니다. 
- 대상 멤버: 메서드가 대상 플랫폼에서 누락되었습니다. 
- 어셈블리 이름: 누락된 API가 거주하는 .NET Framework 어셈블리입니다. 
- 선택한 각 대상 플랫폼은 ".NET Core"와 같은 하나의 열입니다. "지원되지 않음" 값은 API가 이 대상 플랫폼에서 지원되지 않음을 의미합니다. 
- 권장 변경 내용: 변경할 권장 API 또는 기술입니다. 현재 이 필드는 많은 API에 대해 비어 있거나 만료되었습니다. 많은 수의 API 때문에 유지하는 데 큰 어려움을 겪고 있습니다. 고객에게 유용한 정보를 제공하기 위해 대체 솔루션을 찾고 있습니다.

#### <a name="missing-assemblies"></a>어셈블리 누락

![이식성 세부 정보](./media/portability-analyzer/missingassemblies.png)

보고서에서 누락된 어셈블리 섹션을 찾을 수 있습니다. 이 어셈블리 목록은 분석된 어셈블리에서 참조되고 분석되지 않았음을 알려줍니다. 사용자가 소유한 어셈블리인 경우 API 수준의 세부 이식성 보고서를 가져올 수 있도록 API 이식성 분석기 실행에 포함합니다. 타사 라이브러리인 경우 대상 플랫폼을 지원하는 최신 버전이 있는지 확인합니다. 그렇다면 최신 버전으로 이동하는 것이 좋습니다. 결국, 이 목록에는 앱이 사용하는 모든 타사 어셈블리가 포함되어 있으며 대상 플래폼을 지원하는 버전이 있음을 확인할 수 있습니다.  

.NET 이식성 분석기에 대한 자세한 내용은 [GitHub 문서](https://github.com/Microsoft/dotnet-apiport#documentation) 및 [A Brief Look at the .NET Portability Analyzer](https://channel9.msdn.com/Blogs/Seth-Juarez/A-Brief-Look-at-the-NET-Portability-Analyzer)(.NET 이식성 분석기 간단하게 살펴보기) Channel 9 비디오를 참조하세요.
