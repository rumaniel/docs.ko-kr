---
title: 마이크로 서비스 API 및 계약 만들기, 개선 및 버전 관리
description: 요구 사항의 변화에 따라 발전과 버전을 고려하여 마이크로 서비스 API 및 계약을 작성하세요.
ms.date: 09/20/2018
ms.openlocfilehash: 1972d02d8bf7935c71bfd383707ae19ea2baded9
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68672900"
---
# <a name="creating-evolving-and-versioning-microservice-apis-and-contracts"></a>마이크로 서비스 API 및 계약 만들기, 개선 및 버전 관리

마이크로 서비스 API는 서비스와 클라이언트 간 계약입니다. API 계약을 위반하지 않는 경우에만 독립적으로 마이크로 서비스를 확대할 수 있습니다. 계약이 중요한 이유가 바로 여기에 있습니다. 계약을 변경하면 클라이언트 애플리케이션이나 API 게이트웨이에 영향을 미칩니다.

API 정의의 특성은 사용 중인 프로토콜에 따라 다릅니다. 예를 들어, 메시징을 사용할 경우(예: [AMQP](https://www.amqp.org/)) API는 메시지 유형으로 구성됩니다. HTTP 및 RESTful 서비스를 사용할 경우 API는 URL과 요청 및 응답 JSON 형식으로 구성됩니다.

그러나 초기 계약에서 신중했다 하더라도 서비스 API는 시간에 따른 변화가 필요합니다. 이 상황에서, 특히 API가 여러 클라이언트 애플리케이션에서 사용하는 공개 API인 경우 보통은 모든 클라이언트가 새 API 계약으로 업그레이드하게 강제할 수 없습니다. 일반적으로 기존 및 새 서비스 계약 버전이 동시 실행되는 방식으로 서비스의 새 버전을 점진적으로 배포하게 됩니다. 따라서 서비스 버전 관리를 위한 전략을 갖추는 것이 중요합니다.

API에 특성이나 매개 변수를 추가하는 경우처럼 API 변경이 작은 경우 이전 API를 사용하는 클라이언트가 새 서비스 버전으로 전환하여 작업할 수 있어야 합니다. 누락된 특성에 대해 필요한 기본값을 제공할 수 있고 클라이언트는 추가 응답 특성을 무시할 수 있습니다.

그러나 때로는 서비스 API에 대한 대규모의 호환되지 않는 변경이 필요합니다. 클라이언트 애플리케이션이나 서비스가 즉시 새 버전으로 업그레이드하도록 강제할 수 없으므로 서비스는 당분간 기존 API 버전을 지원해야 합니다. REST와 같은 HTTP 기반 메커니즘을 사용한다면 URL이나 HTTP 헤더에 API 버전 번호를 포함하는 것이 한 방법이 됩니다. 그런 다음, 동일한 서비스 인스턴스 안에서 동시에 두 버전을 모두 구현할지 또는 한 API 버전을 각각 처리하는 다른 인스턴스를 배포할지 결정할 수 있습니다. 이를 위한 좋은 방법은 [중재자 패턴](https://en.wikipedia.org/wiki/Mediator_pattern)(예를 들어 [MediatR 라이브러리](https://github.com/jbogard/MediatR))를 통해 서로 다른 구현 버전을 독립 처리기로 분할하는 것입니다.

마지막으로 REST 아키텍처를 사용할 경우 서비스 버전 관리와 확대 가능한 API를 위해서 [하이퍼미디어](https://www.infoq.com/articles/mark-baker-hypermedia)가 가장 좋은 방법입니다.

## <a name="additional-resources"></a>추가 자료

- **Scott Hanselman. 쉬워진 ASP.NET Core RESTful Web API 버전 관리** \
  <https://www.hanselman.com/blog/ASPNETCoreRESTfulWebAPIVersioningMadeEasy.aspx>

- **RESTful Web API 버전 관리** \
  <https://docs.microsoft.com/azure/architecture/best-practices/api-design#versioning-a-restful-web-api>

- **Roy Fielding. 버전 관리, 하이퍼미디어 및 REST** \
  <https://www.infoq.com/articles/roy-fielding-on-versioning>

>[!div class="step-by-step"]
>[이전](asynchronous-message-based-communication.md)
>[다음](microservices-addressability-service-registry.md)
