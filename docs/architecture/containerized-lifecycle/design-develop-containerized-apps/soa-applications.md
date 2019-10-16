---
title: SOA 애플리케이션
description: 컨테이너는 SOA 애플리케이션을 배포하는 유용한 옵션이기도 합니다.
ms.date: 02/15/2019
ms.openlocfilehash: aa56ada7b14a465fb3dafd02b03b815782ac765b
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68672360"
---
# <a name="service-oriented-applications"></a>서비스 지향 애플리케이션

SOA(서비스 지향 아키텍처)라는 용어는 사람들 사이에서 여러 의미로 남용되었습니다. 하지만 한 가지 공통 분모가 있으니, SOA는 애플리케이션을 하위 시스템 또는 계층 같은 다양한 유형으로 분류할 수 있는 여러 서비스(가장 일반적인 것은 HTTP 서비스)로 분해하여 애플리케이션 아키텍처를 만든다는 것을 의미합니다.

현재는 이러한 서비스를 Docker 컨테이너로 배포할 수 있으며, 따라서 모든 종속성이 컨테이너 이미지에 포함되므로 배포 관련 이슈가 해결됩니다. 그러나 SOA를 확장해야 하는데 단일 인스턴스를 기반으로 배포하려는 경우 문제가 발생할 수 있습니다. 이 문제는 Docker 클러스터링 소프트웨어 또는 오케스트레이터를 사용하여 해결할 수 있습니다. 다음 섹션에서 마이크로서비스 접근 방식을 살펴볼 때 오케스트레이터에 대해 자세히 살펴보겠습니다.

Docker 컨테이너는 기존의 서비스 지향 아키텍처와 보다 발전된 마이크로 서비스 아키텍처 모두에 유용합니다(하지만 필수는 아님).

결국 가장 중요한 것은, 컨테이너 클러스터링 솔루션은 기존의 SOA 아키텍처와 각 마이크로서비스가 자체 데이터 모델을 소유하는 고급 마이크로서비스 아키텍처 둘 다에 유용하다는 것입니다. 또한 여러 데이터베이스가 있기 때문에 SOA 서비스에서 공유하는 모놀리식 데이터베이스를 사용하는 대신 데이터 계층을 확장할 수 있습니다. 하지만 데이터 분할에 대한 내용은 순전히 아키텍처와 디자인에 대해서만 다룹니다.

>[!div class="step-by-step"]
>[이전](state-and-data-in-docker-applications.md)
>[다음](orchestrate-high-scalability-availability.md)
