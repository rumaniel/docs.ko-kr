---
title: .NET Core 및 오픈 소스
ms.date: 03/30/2017
ms.assetid: e6bd4655-ce37-4003-8462-468a6fe2c40f
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 90dd72fae71f4283e6eefeb7c878b32e9c155cff
ms.sourcegitcommit: b22705f1540b237c566721018f974822d5cd8758
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49454397"
---
# <a name="net-core-and-open-source"></a>.NET Core 및 오픈 소스
이 항목에서는 .NET Core에 대한 간략한 개요 및 자세한 정보를 찾는 방법을 보여줍니다. .NET Core 주제에 대한 전체 목록은 [.NET Core 가이드](../../core/index.md)를 참조하세요.
  
<a name="BKMK_WhatisNETCore"></a>   
## <a name="what-is-net-core"></a>.NET Core란?  
 .NET Core는 .NET Standard의 일반적인 용도를 위한 모듈식 플랫폼 간 오픈 소스 구현입니다. .NET Framework와 동일한 많은 API를 포함하고 있으며(.NET Core는 작은 집합) 다양한 운영 체제 및 대상 칩을 지원하는 런타임, 프레임워크, 컴파일러 및 도구 구성 요소를 포함합니다. .NET Core 구현은 주로 ASP.NET Core 작업을 기반으로 하지만 많은 최신 구현에 대한 필요와 욕구에 의해서도 구현됩니다. 장치, 클라우드 및 포함/IoT 시나리오에 사용할 수 있습니다.  
  
 .NET Core를 시작하려면 [.NET Core 홈 페이지](https://www.microsoft.com/net/core)를 방문하십시오.  
  
 다음은 .NET Core의 주요 특성입니다.  
  
-   **플랫폼 간:** .NET Core는 필요한 앱 기능을 구현하고 플랫폼 대상에 관계없이 이 코드를 재사용하기 위한 주요 기능을 제공합니다. 현재 Windows, Linux 및 macOS의 세 개 주요 운영 체제(OS)를 지원합니다. 지원되는 운영 체제 간에 수정하지 않고 실행되는 앱과 라이브러리를 작성할 수 있습니다. 지원되는 운영 체제의 목록을 보려면 [.NET Core roadmap](https://github.com/dotnet/core/blob/master/roadmap.md)(.NET Core 로드맵)을 방문하세요.
  
-   **오픈 소스:** .NET Core는 [.NET Foundation](https://www.dotnetfoundation.org/)에서 관리하는 여러 프로젝트 중 하나이며 [GitHub](https://github.com/)에서 사용 가능합니다.  오픈 소스 프로젝트로서의 .NET Core는 더욱 투명한 개발 프로세스를 장려하고 활동 및 참여 커뮤니티를 촉진합니다.  
  
-   **유연한 배포:** 응용 프로그램을 배포하는 방법은 프레임워크 종속 배포 또는 자체 포함 배포의 두 가지가 있습니다. 프레임워크 종속 배포를 사용하는 경우, 사용자 응용 프로그램 및 제3자 종속 프로그램만 설치되고 사용자의 응용 프로그램이 .NET Core의 시스템 전체 버전에 따라 존재하게 됩니다.  자체 포함 배포를 사용하는 경우, 응용 프로그램을 빌드하는 데 사용된 .NET Core 버전도 응용 프로그램 및 타사 종속 프로그램과 함께 배포되며 다른 버전과 함께 나란히 실행할 수 있습니다.    자세한 내용은 [.NET Core 응용 프로그램 배포](../../core/deploying/index.md)를 참조하십시오.

-   **모듈식:** .NET Core는 NuGet을 통해 작은 어셈블리 패키지로 릴리스되므로 모듈식입니다. 대부분의 핵심 기능을 포함하는 하나의 큰 어셈블리 대신, .NET Core는 작은 기능 중심 패키지로 제공됩니다. 이렇게 하면 더 많은 Agile 개발 모델을 활성화하고 필요한 NuGet 패키지만 포함하도록 응용 프로그램을 최적화할 수 있습니다. 작은 응용 프로그램 노출 영역 혜택에는 보안 강화, 서비스 절감, 성능 향상 및 사용한 만큼만 지불하는 비용 감소가 포함됩니다.  
  
## <a name="the-net-core-platform"></a>.NET Core 플랫폼  
 .NET Core 플랫폼은 관리되는 컴파일러, 런타임, 기본 클래스 라이브러리 및 ASP.NET Core와 같은 다양한 응용 프로그램 모델을 포함하는 여러 요소로 구성됩니다. 다음의 [GitHub](https://github.com/) 리포지토리를 방문하여 다양한 구성 요소에 대해 자세히 알아보고 참여할 수 있습니다.  
  
-   [.NET Core](https://github.com/dotnet/core)  
  
-   [CoreFX - .NET Core 기본 라이브러리](https://github.com/dotnet/corefx)  
  
-   [CoreCLR - .NET Core 런타임](https://github.com/dotnet/coreclr)  
  
-   [CLI - .NET Core 명령줄 도구](https://github.com/dotnet/cli)  
  
-   [Roslyn - .NET 컴파일러 플랫폼](https://github.com/dotnet/roslyn)  
  
-   [ASP.NET Core](https://github.com/aspnet/home)  
  
## <a name="see-also"></a>참고 항목  
- [.NET Core 홈 페이지](https://www.microsoft.com/net/core)  
- [.NET Core 가이드](../../core/index.md)  
- [ASP.NET Core 설명서](/aspnet/core/)
