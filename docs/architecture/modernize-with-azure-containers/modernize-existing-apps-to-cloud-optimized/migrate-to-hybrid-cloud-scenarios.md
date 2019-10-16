---
title: 하이브리드 클라우드로 마이그레이션 시나리오
description: Azure 클라우드와 Windows 컨테이너를 사용하여 기존 .NET 응용 프로그램 최신화 | 하이브리드 클라우드 시나리오로 마이그레이션
ms.date: 04/30/2018
ms.openlocfilehash: 5f0819495080bc29ed1239b4a7ab8af31141881b
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72318461"
---
# <a name="migrate-to-hybrid-cloud-scenarios"></a>하이브리드 클라우드로 마이그레이션 시나리오

일부 조직과 기업에서는 자체 규정이나 정책으로 인해 일부 응용 프로그램을 Microsoft Azure나 그 밖에 공용 클라우드로 마이그레이션할 수 없습니다. 하지만 조직에서 응용 프로그램의 일부를 공용 클라우드에 두고 나머지 응용 프로그램을 온-프레미스에 두게 되면 이점을 얻을 가능성이 높습니다. 하지만 혼재된 환경은 공용 클라우드와 온-프레미스에서 사용된 다양한 플랫폼과 기술로 인해 지나치게 복잡해질 수 있습니다.

Microsoft에서는 Azure 하이브리드 클라우드에서 일관성을 유지하면서  온-프레미스와 공용 클라우드의 기존 자산을 최적화할 수 있는 최상의 하이브리드 클라우드 솔루션을 제공합니다. Azure Stack(온-프레미스)과 Azure(공용 클라우드) 덕분에, 클라우드나 온-프레미스에서 동작하는 응용 프로그램을 만들 수 있는, 기존 기술을 극대화하고 유연하고 통일된 접근 방식을 사용할 수 있습니다.

보안과 관련 하 여 하이브리드 클라우드를 통해 관리 및 보안을 중앙 집중화할 수 있습니다. 온-프레미스 및 클라우드 앱에 대 한 Single Sign-On 제공 하 여 데이터 센터에서 클라우드로 모든 자산에 대 한 제어를 얻을 수 있습니다. 하이브리드 클라우드로 Active Directory를 확장 하 고 id 관리를 사용 하 여이를 수행 합니다.

마지막으로, 데이터를 원활 하 게 배포 및 분석 하 고, 클라우드 및 온-프레미스 자산에 대해 동일한 쿼리 언어를 사용 하 고, Azure에서 분석 및 심층 학습을 적용 하 여 원본에 관계 없이 데이터를 보강 할 수 있습니다.

## <a name="azure-stack"></a>Azure Stack

Azure Stack는 조직의 데이터 센터에서 Azure 서비스를 제공할 수 있도록 하는 하이브리드 클라우드 플랫폼입니다. Azure Stack는 edge 및 연결 되지 않은 환경과 같은 주요 시나리오에서 최신 응용 프로그램에 대 한 새로운 옵션을 지원 하거나 특정 보안 및 규정 준수 요구 사항을 충족 하도록 설계 되었습니다.

그림 4-13은 Microsoft에서 제공 하는 진정한 하이브리드 클라우드 플랫폼에 대 한 개요를 보여 줍니다.

![Azure Stack 및 Azure를 사용 하는 Microsoft 하이브리드 클라우드 플랫폼의 다이어그램입니다.](./media/migrate-to-hybrid-cloud-scenarios/microsoft-hybrid-cloud-platform.png)

**그림 4-13.** Azure Stack 및 Azure를 사용 하는 Microsoft 하이브리드 클라우드 플랫폼

Azure Stack는 요구 사항을 충족 하기 위해 두 가지 배포 옵션으로 제공 됩니다.

- Azure Stack 통합 시스템

- Azure Stack 개발 키트

### <a name="azure-stack-integrated-systems"></a>Azure Stack 통합 시스템

Azure Stack 통합 시스템은 Microsoft 및 하드웨어 파트너의 파트너 관계를 통해 제공 됩니다. 파트너 관계는 관리의 단순성에 맞춰 조정 되는 클라우드 지향 혁신을 제공 하는 솔루션을 만듭니다. Azure Stack는 하드웨어 및 소프트웨어의 통합 시스템으로 제공 되므로 클라우드의 혁신을 채택 하면서도 유연 하 고 유연 하 게 제어할 수 있습니다. Azure Stack 통합 시스템의 크기는 4 개에서 12 개 사이의 노드 이며 하드웨어 파트너와 Microsoft에서 공동으로 지원 됩니다. Azure Stack 통합 시스템을 사용 하 여 프로덕션 워크 로드에 대 한 새 시나리오를 구현할 수 있습니다.

### <a name="azure-stack-development-kit"></a>Azure Stack 개발 키트

Microsoft Azure Stack Development Kit는 Azure Stack을 평가 하 고 학습 하는 데 사용할 수 있는 Azure Stack의 단일 노드 배포입니다. Azure와 일치 하는 Api 및 도구를 사용 하 여 개발할 수 있는 개발자 환경으로 Azure Stack Development Kit를 사용할 수도 있습니다. Azure Stack Development Kit은 프로덕션 환경으로 사용 하기 위한 것이 아닙니다.

### <a name="additional-resources"></a>추가 자료

- **Azure 하이브리드 클라우드**

    <https://azure.microsoft.com/overview/hybrid-cloud/>

- **Azure Stack**

    <https://azure.microsoft.com/overview/azure-stack/>

- **Windows 컨테이너에 대 한 Active Directory 서비스 계정**

    <https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/manage-serviceaccounts>

- **Active Directory 지원으로 컨테이너 만들기**

    <https://blogs.msdn.microsoft.com/containerstuff/2017/01/30/create-a-container-with-active-directory-support/>

- **Azure 하이브리드 혜택 라이선스**

    <https://azure.microsoft.com/pricing/hybrid-benefit/>

>[!div class="step-by-step"]
>[이전](modernize-your-apps-lifecycle-with-ci-cd-pipelines-and-devops-tools-in-the-cloud.md)
>[다음](../walkthroughs-technical-get-started-overview.md)
