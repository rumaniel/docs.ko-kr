---
title: 기존.NET 앱을 Azure IaaS(클라우드 인프라 지원)로 리프트 앤 시프트하기
description: Azure 클라우드와 Windows 컨테이너를 사용하여 기존.NET 응용 프로그램을 최신으로 변경합니다.
ms.date: 04/28/2018
ms.openlocfilehash: ae181784e7de5f66b34d2dc38c6e9ec2e004a0c3
ms.sourcegitcommit: c70542d02736e082e8dac67dad922c19249a8893
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/05/2019
ms.locfileid: "70373979"
---
# <a name="lift-and-shift-existing-net-apps-to-azure-iaas-cloud-infrastructure-ready"></a>기존.NET 앱을 Azure IaaS(클라우드 인프라 지원)로 리프트 앤 시프트하기

> 목표: 첫 번째 단계에서는 온-프레미스 투자 및 하드웨어와 네트워킹 유지 관리의 총 비용을 줄이기 위해 단순히 기존 응용 프로그램을 클라우드로 리호스팅합니다.

기존 응용 프로그램을 Azure 서비스 형태의 인프라(IaaS) 플랫폼으로 마이그레이션하는 *방법*을 살펴보기 전에, Azure의 IaaS로 직접 마이그레이션하려는 *이유*를 분석하는 것이 중요합니다. 이 최신화 성숙도 시나리오에서는 기본적으로 기존 온-프레미스 인프라를 사용하지 않고 클라우드의 VM을 사용합니다.

그 밖에 분석할 점은 Azure의 고급 관리 서비스를 추가하지 않고 순수 IaaS 클라우드로 마이그레이션하려는 *이유*입니다. 처음부터 IaaS가 필요한 사례를 결정하십시오.

다음 그림 2-1에서는 최신화 성숙도에서 클라우드 인프라 지원 응용 프로그램의 위치를 나타냅니다.

![클라우드 인프라 지원 응용 프로그램의 위치](./media/image2-1.png)

**그림 2-1.** 클라우드 인프라 지원 응용 프로그램의 위치

## <a name="why-migrate-existing-net-web-applications-to-azure-iaas"></a>기존.NET 웹 응용 프로그램을 Azure IaaS로 마이그레이션하는 이유

초기 IaaS 수준 에서도 클라우드로 마이그레이션하는 주된 이유는 비용 절감을 구현 하는 것입니다. 조직에서는 관리 인프라 서비스를 추가로 사용 하 여 하드웨어 유지 관리, 서버 또는 VM 프로 비전 및 배포 및 인프라 관리에 대 한 투자를 낮출 수 있습니다.

앱을 클라우드로 이동 하기로 결정 한 후에는 PaaS와 같은 고급 옵션 대신 IaaS를 선택할 수 있는 주된 이유가 IaaS 환경이 더 친숙 하다는 것입니다. 현재 온-프레미스 환경과 유사한 환경으로 전환 하면 더 낮은 학습 곡선이 제공 되므로 클라우드로 가장 빨리 경로를 사용할 수 있습니다.

그러나 클라우드에서 가장 빠른 경로를 사용할 경우 응용 프로그램이 클라우드에서 실행 되는 것이 가장 많은 이점을 얻을 수 있습니다. 모든 조직은 이미 도입 된 클라우드 최적화 및 클라우드 기본 완성도 수준을 기반으로 하는 클라우드 마이그레이션에서 가장 중요 한 이점을 얻을 수 있습니다.

또한 응용 프로그램이 이미 클라우드에서 실행 중일 때 IaaS 에서도 응용 프로그램을 현대화 하 고 다시 설계 하기가 더 쉬워졌습니다. 응용 프로그램 데이터 마이그레이션은 이미 수행 되었습니다. 또한 조직에서는 클라우드에서 작업 하는 데 필요한 기술을 획득 하 고 "클라우드 문화권"에서 작동 하도록 전환 했습니다.

## <a name="when-to-migrate-to-iaas-instead-of-to-paas"></a>PaaS가 아닌 IaaS로 마이그레이션하는 경우

다음 섹션에서는 주로 PaaS 플랫폼과 서비스를 기반으로 하는 클라우드 최적화 응용 프로그램에 대해 설명 합니다. 이러한 앱을 통해 클라우드로 마이그레이션하는 것이 가장 많은 이점을 누릴 수 있습니다. 

단순히 기존 응용 프로그램을 클라우드로 이동 하려는 경우에는 Azure App Service에서 실행 하기 위해 크게 수정 하지 않아도 되는 기존 응용 프로그램을 식별 합니다. 이러한 앱은 클라우드 최적화를 위한 첫 번째 후보가 되어야 합니다. 

그런 다음 여전히 Windows 컨테이너 및 PaaS로 이동할 수 없는 앱 (App Service 예: Azure Kubernetes Service와 같은 orchestrator 또는)에 대해 이러한 앱을 단순 일반 Vm (IaaS)으로 마이그레이션합니다. 

그러나 Vm을 올바르게 구성, 보호 및 유지 관리 하려면 Azure에서 PaaS 서비스를 사용 하는 것과 비교 하 여 훨씬 더 많은 시간과 IT 전문 지식이 필요 합니다. Azure Virtual Machines를 고려 하는 경우 VM 환경을 패치, 업데이트 및 관리 하는 데 필요한 지속적인 유지 관리 노력을 고려해 야 합니다. Azure Virtual Machines는 IaaS입니다.

## <a name="use-azure-migrate-to-analyze-and-migrate-your-existing-applications-to-azure"></a>Azure Migrate를 사용 하 여 기존 응용 프로그램을 분석 하 고 Azure로 마이그레이션

클라우드로 마이그레이션하는 것은 어려울 필요가 없습니다. 그러나 많은 조직에서 시작 하 여 환경에 대 한 심층 가시성을 얻고 응용 프로그램, 워크 로드 및 데이터를 긴밀 하 게 상호 종속 시킬 수 있습니다. 이러한 표시가 없으면 경로를 앞으로 계획 하기가 어려울 수 있습니다. 성공적인 마이그레이션에 필요한 사항에 대 한 자세한 정보를 제외 하 고 조직 내에서 올바른 대화를 수행할 수 없습니다. 잠재적 비용 혜택에 대 한 충분 한 사항이 나 워크 로드를 리프트 앤 시프트 할 수 있는지 또는 워크 로드를 성공적으로 마이그레이션하는 데 상당한 재작업이 필요한 지를 알 수 없습니다. 수많은 조직 주저 없습니다.

[Azure Migrate](https://aka.ms/azuremigrate) 는 Azure로 마이그레이션하는 데 도움이 되는 지침, 통찰력 및 메커니즘을 제공 하는 새로운 서비스입니다. Azure Migrate 제공:

- 온-프레미스 가상 머신에 대 한 검색 및 평가

- 다중 계층 응용 프로그램의 신뢰도 높은 검색을 위한 기본 제공 종속성 매핑

- Azure virtual machines에 대 한 인텔리전트 올바른 크기 조정

- 잠재적 문제를 수정 위한 지침과 함께 호환성 보고

- 데이터베이스 검색 및 마이그레이션을 위해 Azure Database Management Service와 통합

Azure Migrate를 통해 비즈니스에 미치는 영향을 최소화 하면서 워크 로드를 마이그레이션할 수 있으며 Azure에서 예상 대로 실행할 수 있습니다. 적절 한 도구와 지침을 사용 하면 중요 한 성능 및 안정성 요구를 충족 하는 동시에 투자 수익률을 최대한 달성할 수 있습니다.

그림 2-2은 Azure Migrate에서 수행 하는 모든 서버 및 응용 프로그램 연결에 대 한 기본 제공 종속성 매핑을 보여 줍니다.

![클라우드 인프라 지원 응용 프로그램의 위치](./media/image2-2.png)

**그림 2-2.** 클라우드 인프라 지원 응용 프로그램의 위치

## <a name="use-azure-site-recovery-to-migrate-your-existing-vms-to-azure-vms"></a>Azure Site Recovery를 사용 하 여 기존 Vm을 Azure Vm으로 마이그레이션

종단 간 [Azure Migrate](https://aka.ms/azuremigrate)의 일부로 [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) 는 Azure의 vm으로 웹 앱을 쉽게 마이그레이션하는 데 사용할 수 있는 도구입니다. Site Recovery를 사용 하 여 온-프레미스 Vm 및 물리적 서버를 Azure에 복제 하거나 보조 온-프레미스 위치에 복제할 수 있습니다. 지원 되는 Azure VM, 온-프레미스 *Hyper-v* VM, *VMware* Vm 또는 Windows 또는 Linux 물리적 서버에서 실행 되는 워크 로드를 복제할 수도 있습니다. Azure로 복제 하면 보조 데이터 센터를 유지 관리 하는 비용과 복잡성이 제거 됩니다.

Site Recovery은 부분적으로 온-프레미스이 고 일부는 Azure에 있는 하이브리드 환경에 대해서도 수행 됩니다. Site Recovery를 사용 하면 Vm 및 온-프레미스 물리적 서버에서 실행 되는 앱을 사이트 작동이 중단 된 상태로 유지 하 여 비즈니스 연속성을 보장할 수 있습니다. Vm 및 물리적 서버에서 실행 되는 워크 로드를 복제 하 여 기본 사이트를 사용할 수 없는 경우 보조 위치에서 계속 사용할 수 있도록 합니다. 작업을 다시 실행 하는 경우 기본 사이트로 작업을 복구 합니다.

그림 2-3에서는 Azure Site Recovery를 사용 하 여 여러 VM 마이그레이션을 실행 하는 방법을 보여 줍니다.

![클라우드 인프라 지원 응용 프로그램의 위치](./media/image2-3.png)

**그림 2-3.** 클라우드 인프라 지원 응용 프로그램의 위치

### <a name="additional-resources"></a>추가 자료

- **Azure Migrate 데이터 시트**

    <https://aka.ms/azuremigration\_datasheet>

- **Azure Migrate**

    <https://aka.ms/azuremigrate>

- **Azure 마이그레이션 센터**

    <https://azure.microsoft.com/migration/>

- **Site Recovery를 사용 하 여 Azure로 마이그레이션**

    <https://docs.microsoft.com/azure/site-recovery/site-recovery-migrate-to-azure>

- **Azure Site Recovery 서비스 개요**

    <https://docs.microsoft.com/azure/site-recovery/site-recovery-overview>

- **AWS의 Vm을 Azure Vm으로 마이그레이션**

    <https://docs.microsoft.com/azure/site-recovery/site-recovery-migrate-aws-to-azure>

>[!div class="step-by-step"]
>[이전](index.md)
>[다음](migrate-your-relational-databases-to-azure.md) <!-- Next Chapter -->
