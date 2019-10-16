---
title: 마이크로 서비스 아키텍처
description: 컨테이너화된 .NET 애플리케이션용 .NET 마이크로 서비스 아키텍처 | 마이크로 서비스 아키텍처의 30.000 피트 보기.
ms.date: 09/20/2018
ms.openlocfilehash: d1c58d218be9e5f8c0ae8ae732f9bdd06674a2c2
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834393"
---
# <a name="microservices-architecture"></a>마이크로 서비스 아키텍처

이름에서 알 수 있듯이 마이크로 서비스 아키텍처는 작은 서비스의 집합인 서버 애플리케이션을 빌드하는 방법입니다. 즉, 이 방식이 프런트 엔드에도 사용되고 있지만 마이크로 서비스 아키텍처는 주로 백 엔드를 지향합니다. 각 서비스는 자체 프로세스에서 실행되며 HTTP/HTTPS, WebSockets 또는 [AMQP](https://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol)와 같은 프로토콜을 사용하여 다른 프로세스와 통신합니다. 각 마이크로 서비스는 특정 컨텍스트 경계 내에서 특정 엔드투엔드 도메인이나 비즈니스 기능을 구현하고 자율적으로 개발되고 독립적으로 배포될 수 있어야 합니다. 마지막으로 각 마이크로 서비스는 관련 도메인 데이터 모델과 도메인 논리(주권 및 분산 데이터 관리)를 소유해야 하며 다양한 데이터 스토리지 기술(SQL, NoSQL) 및 프로그래밍 언어를 기반으로 할 수 있습니다.

마이크로 서비스의 크기는 얼마여야 하나요? 마이크로 서비스를 개발하는 경우 크기는 중요하지 않습니다. 대신 중요한 점은 각 서비스에 대해 개발, 배포 및 크기 조정의 자율성을 갖도록 느슨하게 결합된 서비스를 만드는 것입니다. 물론 마이크로 서비스를 식별하고 디자인하는 경우 다른 마이크로 서비스에서 과도한 직접 종속성이 없다면 가능한 작게 만들어야 합니다. 마이크로 서비스의 크기보다 중요한 점은 내부 응집력 및 다른 서비스로부터의 독립성입니다.

마이크로 서비스 아키텍처를 사용하는 이유는 무엇인가요? 즉, 장기 유연성을 제공합니다. 마이크로 서비스를 사용하면 세부적이고 자율적인 수명 주기를 포함하는 많은 독립적으로 배포 가능한 서비스에 기반한 애플리케이션을 만들 수 있도록 하여 복잡한 대규모의 확장성이 뛰어난 시스템에서 유지 관리 기능을 향상시킬 수 있습니다.

추가 이점으로 마이크로 서비스를 독립적으로 확장할 수 있습니다. 단위로 확장해야 하는 단일 모놀리식 애플리케이션 대신 특정 마이크로 서비스를 확장할 수 있습니다. 이런 방식으로 확장해야 하는 애플리케이션의 다른 영역을 확장하지 않고 추가 처리 기능이 필요한 기능 영역 또는 요청을 지원하는 네트워크 대역폭을 확장할 수 있습니다. 즉, 하드웨어를 적게 사용하기 때문에 비용이 절감됩니다.

![두 배포 방법 간의 차이점을 보여 주는 다이어그램입니다.](./media/microservices-architecture/monolith-deployment-vs-microservice-approach.png)

**그림 4-6** 모놀리식 배포 대 마이크로 서비스 접근 방식

그림 4-6에 나와 있는 것처럼 일반적인 모놀리식 접근 방식에서는 여러 서버/VM에서 전체 앱을 복제하여 애플리케이션을 확장합니다. 마이크로 서비스 방식에서는 기능이 더 작은 서비스로 분리되므로 각 서비스를 독립적으로 확장할 수 있습니다. 마이크로 서비스 접근 방식을 사용하면 복잡한 대규모의 확장형 애플리케이션의 특정한 일부 영역을 변경할 수 있기 때문에 각 마이크로 서비스를 신속하게 변경하고 반복할 수 있습니다.

세분화된 마이크로 서비스 기반 애플리케이션을 구축하는 작업은 연속 통합 및 지속적인 업데이트 사례를 사용합니다. 또한 애플리케이션이 새 기능을 사용하도록 가속화합니다. 애플리케이션의 세분화된 컴퍼지션을 사용하면 격리된 마이크로 서비스를 실행하고 테스트하며, 해당 서비스 간에 지우기 계약을 유지하면서 자율적으로 변경할 수도 있습니다. 인터페이스 또는 계약을 변경하지 않으면 다른 마이크로 서비스를 중단하지 않고 마이크로 서비스의 내부 구현을 변경하거나 새 기능을 추가할 수 있습니다.

마이크로 서비스 기반 시스템을 사용하여 프로덕션에 성공할 수 있는 중요한 측면은 다음과 같습니다.

- 서비스와 인프라의 모니터링 및 상태 검사

- 서비스에 대한 확장성 있는 인프라(즉, 클라우드 및 오케스트레이터)

- 여러 수준의 보안 설계 및 구현: 인증, 권한 부여, 암호 관리, 보안 통신 등

- 일반적으로 다양한 마이크로 서비스에 중점을 두고 다양한 팀과 함께 신속한 애플리케이션 배달

- DevOps 및 CI/CD 사례 및 인프라

이 중에서 처음 3개만을 이 가이드에서 다루거나 소개합니다. 애플리케이션 수명 주기와 관련된 마지막 두 가지는 추가 [Microsoft 플랫폼 및 도구를 사용하여 컨테이너화된 Docker 애플리케이션 수명 주기](https://aka.ms/dockerlifecycleebook) eBook에서 다룹니다.

## <a name="additional-resources"></a>추가 자료

- **Mark Russinovich 마이크로 서비스: 클라우드 기반의 애플리케이션 혁명** \
  <https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/>

- **Martin Fowler. 마이크로 서비스** \
  <https://www.martinfowler.com/articles/microservices.html>

- **Martin Fowler. 마이크로 서비스 필수 구성 요소** \
  <https://martinfowler.com/bliki/MicroservicePrerequisites.html>

- **Jimmy Nilsson. 청크 클라우드 컴퓨팅** \
  <https://www.infoq.com/articles/CCC-Jimmy-Nilsson>

- **Cesar de la Torre. Microsoft 플랫폼 및 도구를 사용하여 컨테이너화된 Docker 애플리케이션 수명 주기**(다운로드 가능한 eBook)\
  <https://aka.ms/dockerlifecycleebook>

>[!div class="step-by-step"]
>[이전](service-oriented-architecture.md)
>[다음](data-sovereignty-per-microservice.md)
