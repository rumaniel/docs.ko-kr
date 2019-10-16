---
title: 마이크로 서비스 기반 복합 UI 만들기
description: 마이크로 서비스 아키텍처 백 엔드에 대해서만은 아닙니다. 프런트 엔드에서 사용하는 Peek 뷰를 가져옵니다.
ms.date: 09/20/2018
ms.openlocfilehash: 1861d3bb6e5d4a0226aa8f3f72a2e0d3e83be56f
ms.sourcegitcommit: 992f80328b51b165051c42ff5330788627abe973
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72275732"
---
# <a name="creating-composite-ui-based-on-microservices"></a>마이크로 서비스 기반 복합 UI 만들기

마이크로 서비스 아키텍처는 서버 쪽에서 데이터 및 논리를 처리하기 시작하지만, 많은 경우 UI는 여전히 모놀리식으로 처리됩니다. 그러나 [마이크로 프런트 엔드](https://martinfowler.com/articles/micro-frontends.html)라는 고급 방법은 마이크로 서비스에 따라 애플리케이션 UI를 디자인하는 것입니다. 즉, 서버에 마이크로 서비스를 배치하고 모놀리식 클라이언트 앱이 마이크로 서비스를 사용하는 대신 마이크로 서비스에서 생성되는 복합 UI가 있습니다. 이 방법으로 마이크로 서비스는 논리 및 시각적 표현 모두를 사용하여 완료될 수 있습니다.

그림 4-20에서는 모놀리식 클라이언트 애플리케이션에서 마이크로 서비스를 사용하는 간단한 방법을 보여줍니다. 물론 HTML 및 JavaScript를 생성하면 ASP.NET MVC 서비스가 생성될 수 있습니다. 그림은 마이크로 서비스를 사용하는 단일(모놀리식) 클라이언트 UI가 있음을 간단히 강조 표시합니다. 여기서는 UI 셰이프(HTML 및 JavaScript)가 아니라 논리 및 데이터에만 집중합니다.

![마이크로 서비스에 연결하는 모놀리식 UI 앱의 다이어그램입니다.](./media/microservice-based-composite-ui-shape-layout/monolith-ui-consume-microservices.png)

**그림 4-20**. 백 엔드 마이크로 서비스를 소비하는 모놀리식 UI 애플리케이션

반면, 복합 UI는 정확하게 마이크로 서비스 자체에서 생성하고 구성했습니다. 일부 마이크로 서비스는 UI 특정 영역의 시각적 셰이프를 제어합니다. 주요 차이는 템플릿에 기반한 클라이언트 UI 구성 요소(예: TypeScript 클래스)가 있으며 해당 템플릿에 대한 data-shaping-UI ViewModel이 각 마이크로 서비스에서 제공된다는 점입니다.

클라이언트 애플리케이션 시작 시 클라이언트 UI 구성 요소(예: TypeScript 클래스)는 각각 지정된 시나리오에 ViewModels를 제공하는 인프라 마이크로 서비스를 사용하여 등록됩니다. 마이크로 서비스가 모양을 변경하면 UI도 변경됩니다.

그림 4-21은 복합 UI 방법의 버전을 보여줍니다. 다양한 기법을 기반으로 세분화된 부분을 집계하는 다른 마이크로 서비스가 있기 때문에 이러한 작업이 간소화됩니다. 기존 웹 접근 방식(ASP.NET MVC) 또는 SPA(단일 페이지 애플리케이션)를 빌드하는 여부에 따라 다릅니다.

![많은 뷰 모델로 구성된 복합 UI의 다이어그램입니다.](./media/microservice-based-composite-ui-shape-layout/microservice-generate-composite-ui.png)

**그림 4-21**. 백 엔드 마이크로 서비스에서 셰이프된 복합 UI 애플리케이션 예제

해당 UI 컴퍼지션 마이크로 서비스는 각각 작은 API 게이트웨이와 유사합니다. 그러나 이 경우에는 각각은 작은 UI 영역을 담당합니다.

따라서 마이크로 서비스에서 제어하는 복합 UI 방법은 사용중인 UI 기술에 따라 더 어렵거나 쉬워질 수 있습니다. 예를 들어, SPA 혹은 네이티브 모바일 앱을 빌드하기 위해 기존 웹 애플리케이션을 빌드하는 동일한 기술을 사용하지 않습니다(Xamarin 앱을 개발하는 경우 마찬가지로 이 방법이 좀 더 어려울 수 있음).

[eShopOnContainers](https://aka.ms/MicroservicesArchitecture) 애플리케이션 예제는 여러 가지 이유로 모놀리식 UI 방법을 사용합니다. 먼저 마이크로 서비스 및 컨테이너에 대한 소개입니다. UI를 디자인하고 개발하는 경우 복합 UI를 사용하는 것이 고급 기능이지만 더 복잡합니다. 다음으로 eShopOnContainers는 Xamarin에 기반한 기본 모바일 앱을 제공합니다. 그러면 클라이언트 C\#에서 더 복잡해 집니다.

그러나 다음 참조를 사용하여 마이크로 서비스를 기반으로 하는 복합 UI에 대해 자세히 알아봅니다.

## <a name="additional-resources"></a>추가 자료

- **마이크로 프런트 엔드(Martin Fowler의 블로그)**  
  <https://martinfowler.com/articles/micro-frontends.html>
  
- **마이크로 프런트 엔드(Michael Geers 사이트)**  
  <https://micro-frontends.org/>
  
- **ASP.NET을 사용한 복합 UI(특정 워크샵)**  
  <https://github.com/Particular/Workshop/tree/master/demos/asp-net-core>

- **Ruben Oostinga 마이크로 서비스 아키텍처의 모놀리식 프런트 엔드**  
  <https://xebia.com/blog/the-monolithic-frontend-in-the-microservices-architecture/>

- **Mauro Servienti 뛰어난 UI 구성의 비밀**  
  <https://particular.net/blog/secret-of-better-ui-composition>

- **Viktor Farcic 마이크로 서비스에 프런트 엔드 웹 구성 요소 포함하기**  
  <https://technologyconversations.com/2015/08/09/including-front-end-web-components-into-microservices/>

- **마이크로 서비스 아키텍처에서 프런트 엔드 관리**  
  <https://allegro.tech/2016/03/Managing-Frontend-in-the-microservices-architecture.html>

>[!div class="step-by-step"]
>[이전](microservices-addressability-service-registry.md)
>[다음](resilient-high-availability-microservices.md)
