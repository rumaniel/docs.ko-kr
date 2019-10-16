---
title: NuGet 패키지 게시
description: .NET 라이브러리를 NuGet에 게시하는 모범 사례 권장 사항입니다.
author: jamesnk
ms.author: mairaw
ms.date: 10/02/2018
ms.openlocfilehash: 9c8442b52ed2c54d2fb3368a2e886c5fc2b19148
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65640763"
---
# <a name="publishing-a-nuget-package"></a>NuGet 패키지 게시

NuGet 패키지는 패키지 리포지토리에서 게시되고 사용됩니다. NuGet.org가 가장 널리 알려지고 사용되는 리포지토리지만, NuGet 패키지는 여러 장소에 게시할 수 있습니다.

* **[NuGet.org](https://www.nuget.org/)** 는 NuGet 패키지에 대한 기본 온라인 리포지토리입니다. NuGet.org의 모든 패키지는 모두에게 공개적으로 제공됩니다. 기본적으로 Visual Studio에는 패키지 소스로 NuGet.org가 있으며, 많은 개발자에게 NuGet.org는 상호 작용할 수 있는 유일한 패키지 리포지토리입니다. NuGet.org는 커뮤니티 피드백을 원하는 안정적인 패키지 및 시험판 패키지를 게시하기 가장 좋은 곳입니다.

* **[MyGet](https://myget.org/)** 은 오픈 소스 프로젝트에 대한 사용자 지정 패키지 피드를 지원하는 리포지토리 서비스입니다. MyGet 공용 사용자 지정 피드는 CI 서비스로 만든 시험판 패키지를 게시하기에 이상적인 곳입니다. 또한 MyGet은 상업적으로 개인 피드를 제공합니다.

* **[로컬 피드](/nuget/hosting-packages/local-feeds)** 를 통해 폴더를 패키지 리포지토리처럼 취급할 수 있고 NuGet에서 폴더의 `*.nupkg` 파일에 액세스할 수도록 만듭니다. 로컬 피드는 NuGet.org에 NuGet 패키지를 게시하기 전에 해당 패키지를 테스트하는 데 유용합니다.

> [!NOTE]
> 패키지가 업로드되면 NuGet.org는 [패키지 삭제를 허용하지 않습니다](/nuget/policies/deleting-packages). 패키지는 UI에 공개적으로 표시되지 않도록 나열을 취소할 수 있지만, `*.nupkg`는 복원 시 계속 다운로드할 수 있습니다. 또한 nuget.org에서는 중복 패키지 버전을 허용하지 않습니다. 오류가 있는 NuGet 패키지를 수정하려면 잘못된 패키지를 나열 취소하고 버전 번호를 늘리고 패키지의 새 버전을 게시해야 합니다.

**✔️** [커뮤니티 피드백을 원하는 안정적인 패키지 및 시험판 패키지를 NuGet.org에 게시합니다](/nuget/create-packages/publish-a-package).

**✔️** 연속 통합 빌드에서 시험판 패키지를 MyGet 피드에 게시합니다.

**✔️** 로컬 피드 또는 MyGet을 사용하여 개발 환경에서 패키지를 테스트합니다. 패키지가 작동하는지 확인하고 해당 패키지를 NuGet.org에 게시하세요.

## <a name="nugetorg-security"></a>NuGet.org 보안

공격자가 NuGet 계정에 액세스하여 라이브러리의 악성 버전을 업로드할 수 없는 것이 중요합니다. NuGet.org는 패키지가 게시될 때 2단계 인증 및 전자 메일 알림을 제공합니다. NuGet.org에 로그인한 후 **계정 설정** 페이지에서 이러한 기능을 사용하도록 설정하세요.

![대체 텍스트](./media/publish-nuget-package/nuget-2fa.png " NuGet 계정 보안")

**✔️** Microsoft 계정을 사용하여 NuGet에 로그인합니다.

**✔️** NuGet에 액세스에 대해 2단계 인증을 사용하도록 설정합니다.

**✔️** 패키지가 게시될 때 전자 메일 알림을 사용하도록 설정합니다.

>[!div class="step-by-step"]
>[이전](sourcelink.md)
>[다음](versioning.md)
