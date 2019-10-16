---
title: 다중 컨테이너 및 마이크로 서비스 기반 .NET 애플리케이션 디자인 및 개발
description: 컨테이너화된 .NET 애플리케이션에 대한 .NET 마이크로 서비스 아키텍처 | 다중 컨테이너 및 마이크로 서비스 기반 .NET 애플리케이션 디자인 및 개발을 위한 외부 아키텍처 이해
ms.date: 10/02/2018
ms.openlocfilehash: 8c2f828e9913a0efcdf580371124b0f624daeffe
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "70295230"
---
# <a name="designing-and-developing-multi-container-and-microservice-based-net-applications"></a>다중 컨테이너 및 마이크로 서비스 기반 .NET 애플리케이션 디자인 및 개발

*컨테이너화된 마이크로 서비스 애플리케이션의 개발은 다중 컨테이너 애플리케이션 빌드를 의미합니다. 그러나 다중 컨테이너 애플리케이션은 3계층 애플리케이션과 같이 더 간단할 수 있으며, 마이크로 서비스 아키텍처를 사용하여 빌드하지 못할 수 있습니다.*

이전에 “마이크로 서비스 아키텍처를 구축할 때 Docker가 필요한가요?”라는 질문을 제기했습니다. 대답은 명확히 “아니요”입니다. Docker는 지원 기능으로, 중요한 이점을 제공할 수 있지만, 컨테이너 및 Docker가 마이크로 서비스에 대한 명백한 요구 사항은 아닙니다. 예를 들어 간단한 프로세스 또는 Docker 컨테이너로 실행되는 마이크로 서비스를 지원하는 Azure Service Fabric을 사용할 때 Docker 유무와 관계없이 마이크로 서비스 기반 애플리케이션을 만들 수 있습니다.

그러나 Docker 컨테이너를 기반으로 하는 마이크로 서비스 기반 애플리케이션을 설계 및 개발하는 방법을 알고 있는 경우 다른 간단한 애플리케이션 모델을 설계 및 개발할 수도 있습니다. 예를 들어 다중 컨테이너 접근 방식이 필요한 3계층 애플리케이션을 설계할 수도 있습니다. 이런 이유로 그리고 컨테이너 업계 내에서 마이크로 서비스 아키텍처가 중요한 추세이므로 이 섹션에서는 Docker 컨테이너를 사용하여 마이크로 서비스 아키텍처를 구현하는 데 중점을 둡니다.

>[!div class="step-by-step"]
>[이전](../docker-application-development-process/docker-app-development-workflow.md)
>[다음](microservice-application-design.md)
