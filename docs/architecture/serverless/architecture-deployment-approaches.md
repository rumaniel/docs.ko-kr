---
title: 아키텍처 배포 방법-서버 리스 앱
description: IaaS, PaaS, 컨테이너 및 서버를 사용 하지 않는 비교를 통해 엔터프라이즈 아키텍처가 클라우드에 배포 되는 다양 한 방법에 대 한 가이드입니다.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 4cc8442509fc8a0e2cc0eb797365423458e77684
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834333"
---
# <a name="architecture-deployment-approaches"></a>아키텍처 배포 접근 방식

비즈니스 응용 프로그램을 디자인 하는 데 사용 되는 아키텍처 방법에 관계 없이 이러한 응용 프로그램의 구현 또는 배포는 달라질 수 있습니다. 비즈니스는 물리적 하드웨어에서 서버를 사용 하지 않는 기능에 이르기까지 모든 응용 프로그램을 호스트 합니다.

## <a name="n-tier-applications"></a>N 계층 응용 프로그램

[N 계층 아키텍처 패턴](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier) 은 완성 된 아키텍처로, 다양 한 논리 계층을 별도의 물리적 계층으로 분리 하는 응용 프로그램을 의미 합니다. N 계층 아키텍처는 N 계층 아키텍처의 물리적 구현입니다. 이 아키텍처의 가장 일반적인 구현에는 다음이 포함 됩니다.

* 프레젠테이션 계층 (예: 웹 앱)
* API 또는 데이터 액세스 계층 (예: REST API).
* SQL database와 같은 데이터 계층

![N 계층 아키텍처](./media/n-tier-architecture.png)

N 계층 솔루션에는 다음과 같은 특징이 있습니다.

* 프로젝트는 일반적으로 계층과 정렬 됩니다.
* 테스트는 계층에 따라 다르게 접근 될 수 있습니다.
* 계층은 추상화 계층을 제공 합니다. 예를 들어 프레젠테이션 계층은 일반적으로 데이터 계층의 구현 세부 정보를 무시 합니다.
* 일반적으로 레이어는 인접 레이어와만 상호 작용 합니다.
* 릴리스는 종종 프로젝트에서 관리 되므로 계층 수준에서 관리 됩니다. 간단한 API 변경으로 인해 전체 중간 계층의 새로운 릴리스가 필요할 수 있습니다.

이 방법은 다음과 같은 몇 가지 이점을 제공 합니다.

* 데이터베이스 격리 (프런트 엔드가 데이터베이스 백 엔드에 직접 액세스할 수 없는 경우가 많음)
* API (예: 모바일, 데스크톱 및 웹 앱 클라이언트는 모두 동일한 Api를 다시 사용할 수 있음)를 다시 사용 합니다.
* 계층을 서로 독립적으로 확장할 수 있습니다.
* 리팩터링 격리: 다른 계층에 영향을 주지 않고 한 계층을 리팩터링할 수 있습니다.

## <a name="on-premises-and-infrastructure-as-a-service-iaas"></a>온-프레미스 및 IaaS (Infrastructure as a Service)

응용 프로그램을 호스트 하는 일반적인 접근 방식은 하드웨어를 구입 하 고 운영 체제를 비롯 한 모든 소프트웨어 설치를 관리 해야 합니다. 처음에는 비용이 많이 드는 데이터 센터 및 물리적 하드웨어가 참여 했습니다. 운영 실제 하드웨어와 함께 제공 되는 문제는 다음과 같은 여러 가지입니다.

* "Just-in-time" 또는 최대 수요 시나리오를 위해 과도 하 게 구입 해야 하는 경우
* 하드웨어에 대 한 물리적 액세스를 보호 합니다.
* 하드웨어 오류 (예: 디스크 오류)에 대 한 책임입니다.
* 성능을.
* 라우터 및 부하 분산 장치 구성
* 전원 중복성.
* 소프트웨어 액세스 보안.

![IaaS 접근 방식](./media/iaas-approach.png)

"가상 컴퓨터"를 통해 하드웨어를 가상화 하면 IaaS (Infrastructure as a Service)를 사용할 수 있습니다. 호스트 컴퓨터는 자체 메모리, CPU 및 저장소에 대 한 할당을 사용 하 여 인스턴스에 리소스를 제공 하기 위해 효과적으로 분할 됩니다. 팀은 필요한 Vm을 프로 비전 하 고 연결 된 네트워크 및 저장소에 대 한 액세스를 구성 합니다.

자세한 내용은 [가상 컴퓨터 N 계층 참조 아키텍처](https://docs.microsoft.com/azure/architecture/reference-architectures/virtual-machines-windows/n-tier)를 참조 하세요.

가상화 및 IaaS (Infrastructure as a Service)는 많은 문제를 해결 하지만 인프라 팀에 게 많은 책임도 있습니다. 팀은 운영 체제 버전을 유지 관리 하 고, 보안 패치를 적용 하 고, 대상 컴퓨터에 타사 종속성을 설치 합니다. 앱은 종종 테스트 환경에 비해 프로덕션 컴퓨터에서 다르게 동작 합니다. 다른 종속성 버전 및/또는 OS SKU 수준 때문에 문제가 발생 합니다. 많은 조직에서 이러한 목표에 N 계층 응용 프로그램을 배포 하지만 많은 회사에서 [Platform as a Service](#platform-as-a-service-paas)와 같은 더 많은 클라우드 네이티브 모델에 배포 하는 것이 좋습니다. 마이크로 서비스를 사용 하는 아키텍처는 탄력성 및 복원 력을 확장 하기 위한 요구 사항 때문에 더 어렵습니다.

자세한 내용은 [가상 컴퓨터](https://docs.microsoft.com/azure/virtual-machines/)를 참조 하세요.

## <a name="platform-as-a-service-paas"></a>PaaS (Platform as a Service)

PaaS (Platform as a Service)는 개발자가 직접 연결할 수 있는 구성 된 솔루션을 제공 합니다. PaaS는 관리 되는 호스팅을 위한 또 다른 용어입니다. 기본 운영 체제, 보안 패치 및 대부분의 경우 타사 종속성을 관리할 필요가 없습니다. 플랫폼의 예로는 웹 응용 프로그램, 데이터베이스 및 모바일 백 엔드가 있습니다.

PaaS는 IaaS에 일반적으로 발생 하는 문제를 해결 합니다. PaaS는 개발자가 배포 방법이 아닌 코드 또는 데이터베이스 스키마에 집중할 수 있도록 합니다. PaaS의 이점은 다음과 같습니다.

* 유휴 컴퓨터에 투자 하는 오버 헤드를 제거 하는 사용 모델에 대 한 비용을 지불 합니다.
* 직접 배포 및 향상 된 DevOps, CI (지속적인 통합) 및 CD (지속적인 업데이트) 파이프라인을 제공 합니다.
* 자동 업그레이드, 업데이트 및 보안 패치.
* 푸시 단추 확장 및 확장 (탄력적 크기 조정).

일반적으로 PaaS의 주요 단점은 공급 업체의 잠금입니다. 예를 들어 일부 PaaS 공급자는 ASP.NET, node.js 또는 다른 특정 언어 및 플랫폼만 지원 합니다. Azure App Service 같은 제품은 여러 플랫폼을 처리 하 고 웹 앱을 호스팅하기 위한 다양 한 언어와 프레임 워크를 지원 하기 위해 발전 했습니다.

![Platform as a Service 아키텍처](./media/paas-architecture.png)

## <a name="software-as-a-service-saas"></a>SaaS (Software as a Service)

SaaS (Software as a Service) 또는 SaaS는 중앙에서 호스트 되 고 로컬 설치 또는 프로 비전 없이 사용할 수 있습니다. SaaS는 소프트웨어를 배포 하기 위한 플랫폼으로 PaaS 위에 호스트 되는 경우가 많습니다. SaaS는 기존 소프트웨어를 실행 하 고 연결 하는 서비스를 제공 합니다. SaaS는 종종 업계 및 수직으로 특정 합니다. SaaS는 종종 사용 허가를 받고 일반적으로 클라이언트/서버 모델을 제공 합니다. 최신 SaaS 제품은 클라이언트에 웹 기반 앱을 사용 합니다. 회사는 일반적으로 SaaS를 라이선스 제공에 대 한 비즈니스 솔루션으로 간주 합니다. 응용 프로그램의 확장성 및 유지 관리에 대 한 아키텍처 고려 사항으로 구현 되는 경우가 많습니다. 실제로 대부분의 SaaS 솔루션은 IaaS, PaaS 및/또는 서버 리스 백 엔드를 기반으로 빌드됩니다.

[샘플 응용 프로그램](https://docs.microsoft.com/azure/sql-database/saas-tenancy-welcome-wingtip-tickets-app)을 통해 SaaS에 대해 자세히 알아보세요.

## <a name="containers-and-functions-as-a-service-faas"></a>컨테이너 및 FaaS (함수 as a Service)

컨테이너는 IaaS 오버 헤드 없이 PaaS와 유사한 이점을 사용할 수 있는 흥미로운 솔루션입니다. 컨테이너는 기본적으로 고유한 응용 프로그램을 실행 하는 데 필요한 완전 한 필수를 포함 하는 런타임입니다. 호스트 운영 체제의 커널 또는 핵심 부분과 저장소와 같은 서비스는 호스트에서 공유 됩니다. 공유 커널을 사용 하면 컨테이너를 간단 하 게 사용할 수 있습니다. 즉, 일반 가상 컴퓨터의 기가바이트 크기와 비교할 때 크기가 약간 메가바이트입니다. 호스트를 이미 실행 중인 경우 컨테이너를 신속 하 게 시작 하 여 고가용성을 용이 하 게 할 수 있습니다. 컨테이너를 신속 하 게 실행 하는 기능을 통해 복원 력을 추가로 제공할 수도 있습니다. Docker는 더 인기 있는 컨테이너 구현 중 하나입니다.

컨테이너의 이점은 다음과 같습니다.

* 경량 및 이식 가능
* 자체 포함 되어 있으므로 종속성을 설치할 필요가 없습니다.
* 호스트에 관계 없이 일관 된 환경 제공 (클라우드 서버와 동일 하 게 노트북에서 동일 하 게 실행)
* 규모 확장을 위해 신속 하 게 프로 비전 할 수 있습니다.
* 오류 복구를 위해 신속 하 게 다시 시작할 수 있습니다.

컨테이너는 컨테이너 호스트에서 실행 되며,이는 다시 운영 체제 미 설치 컴퓨터 또는 가상 머신에서 실행 될 수 있습니다. 동일한 컨테이너의 여러 컨테이너 또는 인스턴스는 단일 호스트에서 실행 될 수 있습니다. 진정한 장애 조치 (failover) 및 복원 력을 위해 컨테이너를 호스트 간에 확장 해야 합니다.

Docker 컨테이너에 대 한 자세한 내용은 [docker 란?](../microservices/container-docker-introduction/docker-defined.md)을 참조 하세요.

일반적으로 호스트 간에 컨테이너를 관리 하려면 Kubernetes와 같은 오케스트레이션 도구가 필요 합니다. 오케스트레이션 솔루션을 구성 하 고 관리 하면 프로젝트에 오버 헤드와 복잡성이 추가 될 수 있습니다. 다행히 많은 클라우드 공급자는 PaaS 솔루션을 통해 오케스트레이션 서비스를 제공 하 여 컨테이너 관리를 간소화 합니다.

다음 그림은 Kubernetes 설치 예제를 보여 줍니다. 설치 주소에서 노드를 확장 하 고 장애 조치 (failover) 합니다. 마스터 서버에서 관리 하는 Docker 컨테이너 인스턴스를 실행 합니다. *Kubelet* 는 Kubernetes에서 Docker로 명령을 릴레이 하는 클라이언트입니다.

![Kubernetes](./media/kubernetes-example.png)

오케스트레이션에 대 한 자세한 내용은 [Kubernetes On Azure](https://docs.microsoft.com/azure/aks/intro-kubernetes)를 참조 하세요.

FaaS (함수 서비스)는 서버를 사용 하지 않는 것과 비슷한 특수 한 컨테이너 서비스입니다. [Openfaas](https://github.com/openfaas/faas)라고 하는 faas의 특정 구현은 서버를 사용 하지 않는 기능을 제공 하기 위해 컨테이너 위에 위치 합니다. OpenFaaS는 코드 조각을 실행 하는 데 필요한 모든 컨테이너 종속성을 패키지 하는 템플릿을 제공 합니다. 템플릿을 사용 하면 코드를 기능 단위로 배포 하는 과정이 간단해 집니다. OpenFaaS는 기존 인프라를 사용할 수 있기 때문에 이미 컨테이너 및 orchestrator를 포함 하는 아키텍처를 대상으로 합니다. 서버를 사용 하지 않는 기능을 제공 하지만 특히 Docker 및 orchestrator를 사용 해야 합니다.

## <a name="serverless"></a>서버

서버를 사용 하지 않는 아키텍처에서는 코드와 해당 호스팅 환경을 명확 하 게 구분 합니다. *트리거에서*호출 하는 *함수* 에서 코드를 구현 합니다. 해당 함수가 종료 되 면 필요한 모든 리소스가 해제 될 수 있습니다. 트리거는 수동, 시간이 지정 된 프로세스, HTTP 요청 또는 파일 업로드 일 수 있습니다. 트리거의 결과는 코드를 실행 하는 것입니다. 서버를 사용 하지 않는 플랫폼은 다를 수 있지만 데이터베이스에 쓰기 또는 큐 결과 등의 작업을 간소화 하기 위해 미리 정의 된 Api 및 바인딩에 대 한 액세스를 제공 합니다.

서버를 사용 하지 않는 아키텍처는 호스트 환경에서 코드에 초점을 맞추기 위해 과도 하 게 의존 하는 아키텍처입니다. *서버를 더 작은*것으로 간주할 수 있습니다.

컨테이너 솔루션은 개발자가 서버를 사용 하지 않는 이미지에 코드를 게시 하는 기존 빌드 스크립트를 제공 합니다. 기타 구현에서는 기존 PaaS 솔루션을 사용 하 여 확장 가능한 아키텍처를 제공 합니다.

추상화는 DevOps 팀이 서버 및 특정 컨테이너를 프로 비전 하거나 관리할 필요가 없음을 의미 합니다. 서버를 사용 하지 않는 플랫폼은 관련 SDK를 사용 하 여 작성 된 스크립트 또는 패키지 된 실행 파일로 코드를 호스팅하고 코드 크기를 조정 하는 데 필요한 리소스를 할당 합니다.

다음 그림에서는 서버를 사용 하지 않는 네 가지 구성 요소를 보여 줍니다. HTTP 요청으로 인해 체크 아웃 API 코드가 실행 됩니다. Checkout API는 데이터베이스에 코드를 삽입 하 고 insert는 여러 다른 함수를 실행 하 여 작업을 계산 하 고 순서를 수행 하는 등의 작업을 수행 합니다.

![서버를 사용 하지 않는 구현](./media/serverless-implementation.png)

서버를 사용 하지 않는 이점은 다음과 같습니다.

* **고밀도.** 서버를 사용 하지 않는 동일한 코드의 많은 인스턴스는 컨테이너 또는 가상 컴퓨터와 비교 하 여 동일한 호스트에서 실행 될 수 있습니다. 인스턴스는 여러 호스트에 걸쳐 확장 되 고 복원 력이 향상 됩니다.
* **마이크로 요금 청구**. 서버를 사용 하지 않는 대부분의 공급자는 서버를 사용 하지 않는 실행을 기준으로 청구 되므로 특정 시나리오에서 많은 비용 절감 효과가
* **빠른 크기 조정**. 서버를 사용 하지 않는 경우 작업을 자동으로 신속 하 게 대응 하도록 확장할 수 있습니다.
* **출시 시간 단축** 개발자는 코드에 집중 하 고 서버를 사용 하지 않는 플랫폼에 직접 배포 합니다. 구성 요소는 서로 독립적으로 해제할 수 있습니다.

서버를 사용 하지 않는 것이 계산의 컨텍스트에서 가장 자주 설명 되지만 데이터에도 적용 될 수 있습니다. 예를 들어 [AZURE SQL](https://docs.microsoft.com/azure/sql-database) 및 [Cosmos DB](https://docs.microsoft.com/azure/cosmos-db) 는 둘 다 호스트 컴퓨터 또는 클러스터를 구성 하지 않아도 되는 클라우드 데이터베이스를 제공 합니다. 이 책에서는 서버 리스 계산에 집중 합니다.

## <a name="summary"></a>요약

하이브리드 방식을 포함 하 여 아키텍처에 사용할 수 있는 광범위 한 선택 항목이 있습니다. 서버를 사용 하지 않는 응용 프로그램 기능, 관리 및 비용을 제어 하 고 이식성으로 간소화 합니다. 그러나 서버를 사용 하지 않는 많은 플랫폼은 솔루션을 미세 조정 하는 데 도움이 되는 구성을 노출 합니다. 바람직한 프로그래밍 관행으로 인해 더 많은 이식 가능한 코드와 서버 리스 서버가 없는 플랫폼 잠금이 발생할 수도 있습니다. 다음 표에서는 아키텍처 방법을 나란히 보여 줍니다. 확장 요구 사항에 따라 서버 리스를 선택 하 고, 런타임을 관리할 지 여부를 선택 하 고, 워크 로드를 작은 구성 요소로 얼마나 잘 나눌 수 있는지를 선택 합니다. 다음 장에서 서버 리스 및 기타 결정 사항에 대 한 잠재적인 문제에 대해 알아봅니다.

|         |IaaS     |PaaS     |컨테이너|서버|
|---------|---------|---------|---------|----------|
|**소수 자릿수**|VM       |인스턴스 |앱      |기능  |
|**추상화**|하드웨어|플랫폼|OS 호스트|런타임   |
|**Unit** |VM       |프로젝트  |이미지    |코드      |
|**수명(lifetime)**|개월|일 단위|시간 (분)|시간 (분)|
|**책임**|응용 프로그램, 종속성, 런타임 및 운영 체제|응용 프로그램 및 종속성|응용 프로그램, 종속성 및 런타임|기능

* **크기 조정** 은 응용 프로그램의 크기를 조정 하는 데 사용 되는 단위를 나타냅니다.
* **추상화** 는 구현에 의해 추상화 된 계층을 참조 합니다.
* **단위** 는 배포 되는 항목의 범위를 나타냅니다.
* **수명은** 특정 인스턴스의 일반적인 런타임을 나타냅니다.
* 응용 프로그램을 빌드, 배포 및 유지 관리 하기 위한 오버 헤드 **를 의미 합니다** .

다음 장은 서버를 사용 하지 않는 아키텍처, 사용 사례 및 디자인 패턴에 중점을 둡니다.

## <a name="recommended-resources"></a>권장 리소스

* [Azure 응용 프로그램 아키텍처 가이드](https://docs.microsoft.com/azure/architecture/guide/)
* [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db)
* [Azure SQL](https://docs.microsoft.com/azure/sql-database)
* [N 계층 아키텍처 패턴](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier)
* [Azure의 Kubernetes](https://docs.microsoft.com/azure/aks/intro-kubernetes)
* [마이크로 서비스](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/microservices)
* [가상 컴퓨터 N 계층 참조 아키텍처](https://docs.microsoft.com/azure/architecture/reference-architectures/virtual-machines-windows/n-tier)
* [가상 컴퓨터](https://docs.microsoft.com/azure/virtual-machines/)
* [Docker란?](../microservices/container-docker-introduction/docker-defined.md)
* [정문 ticket SaaS 응용 프로그램](https://docs.microsoft.com/azure/sql-database/saas-tenancy-welcome-wingtip-tickets-app)

>[!div class="step-by-step"]
>[이전](architecture-approaches.md)
>[다음](serverless-architecture.md)
