---
title: 여러 마이크로 서비스에서 생성된 시각적 UI 셰이프 및 레이아웃을 포함하여 마이크로 서비스를 기반으로 복합 UI 만들기
description: 컨테이너화된 .NET 응용 프로그램의 .NET 마이크로 서비스 아키텍처 | 여러 마이크로 서비스에서 생성된 시각적 UI 셰이프 및 레이아웃을 포함하여 마이크로 서비스를 기반으로 복합 UI 만들기
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.openlocfilehash: 3c5f4c5a1dd1c1065be63ad916af078050c069c1
ms.sourcegitcommit: 9bd8f213b50f0e1a73e03bd1e840c917fbd6d20a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50033651"
---
# <a name="creating-composite-ui-based-on-microservices-including-visual-ui-shape-and-layout-generated-by-multiple-microservices"></a>여러 마이크로 서비스에서 생성된 시각적 UI 셰이프 및 레이아웃을 포함하여 마이크로 서비스를 기반으로 복합 UI 만들기

마이크로 서비스 아키텍처는 서버 쪽에서 데이터 및 논리를 처리하기 시작합니다. 그러나 고급 방법은 마이크로 서비스에 따라 응용 프로그램 UI를 디자인하는 것입니다. 즉, 서버에 마이크로 서비스를 배치하고 모놀리식 클라이언트 앱이 마이크로 서비스를 사용하는 대신 마이크로 서비스에서 생성되는 복합 UI가 있습니다. 이 방법으로 마이크로 서비스는 논리 및 시각적 표현 모두를 사용하여 완료될 수 있습니다.

그림 4-20에서는 모놀리식 클라이언트 응용 프로그램에서 마이크로 서비스를 사용하는 간단한 방법을 보여줍니다. 물론 HTML 및 JavaScript를 생성하면 ASP.NET MVC 서비스가 생성될 수 있습니다. 그림은 마이크로 서비스를 사용하는 단일(모놀리식) 클라이언트 UI가 있음을 간단히 강조 표시합니다. 여기서는 UI 셰이프(HTML 및 JavaScript)가 아니라 논리 및 데이터에만 집중합니다.

![](./media/image20.png)

**그림 4-20**. 백 엔드 마이크로 서비스를 소비하는 모놀리식 UI 응용 프로그램

반면, 복합 UI는 정확하게 마이크로 서비스 자체에서 생성하고 구성했습니다. 일부 마이크로 서비스는 UI 특정 영역의 시각적 셰이프를 제어합니다. 주요 차이는 템플릿에 기반한 클라이언트 UI 구성 요소(예: TS 클래스)가 있으며 해당 템플릿에 대한 data-shaping-UI ViewModel가 각 마이크로 서비스에서 제공된다는 점입니다.

클라이언트 응용 프로그램 시작 시 클라이언트 UI 구성 요소(예: TypeScript 클래스)는 각각 지정된 시나리오에 ViewModels를 제공하는 인프라 마이크로 서비스를 사용하여 등록됩니다. 마이크로 서비스가 모양을 변경하면 UI도 변경됩니다.

그림 4-21은 복합 UI 방법의 버전을 보여줍니다. 다양한 기술을 기반으로 세분화된 부분을 집계하는 다른 마이크로 서비스가 있기 때문에 간소화됩니다. 이것은 기존 웹 접근 방식(ASP.NET MVC) 또는 SPA(단일 페이지 응용 프로그램)를 빌드하는지에 따라 다릅니다.

![](./media/image21.png)

**그림 4-21**. 백 엔드 마이크로 서비스에서 셰이프된 복합 UI 응용 프로그램 예제

해당 UI 컴퍼지션 마이크로 서비스는 각각 작은 API 게이트웨이와 유사합니다. 그러나 이 경우에는 각각 작은 UI 영역을 담당합니다.

따라서 마이크로 서비스에서 제어하는 복합 UI 방법은 사용 중인 UI 기술에 따라 더 어렵거나 쉬워질 수 있습니다. 예를 들어, SPA 또는 네이티브 모바일 앱을 빌드하기 위해 기존 웹 응용 프로그램을 빌드하는 동일한 기술을 사용하지 않습니다(Xamarin 앱을 개발하는 경우 마찬가지로 이 방법이 좀 더 어려울 수 있음).

[eShopOnContainers](https://aka.ms/MicroservicesArchitecture) 응용 프로그램 예제는 여러 가지 이유로 모놀리식 UI 방법을 사용합니다. 먼저 마이크로 서비스 및 컨테이너에 대한 소개입니다. UI를 디자인하고 개발하는 경우 복합 UI를 사용하는 것이 고급 기능이지만 더 복잡합니다. 다음으로 eShopOnContainers는 Xamarin에 기반한 기본 모바일 앱을 제공합니다. 그러면 클라이언트 C\#에서 더 복잡해 집니다.

그러나 다음 참조를 사용하여 마이크로 서비스를 기반으로 하는 복합 UI에 대해 자세히 알아봅니다.

## <a name="additional-resources"></a>추가 자료

-   **ASP.NET을 사용한 복합 UI(특정 워크샵)**
    [*https://go.particular.net/workshop-composite-ui-demo*](https://go.particular.net/workshop-composite-ui-demo)

-   **Ruben Oostinga 마이크로 서비스 아키텍처의 모놀리식 프런트 엔드**
    [*https://xebia.com/blog/the-monolithic-frontend-in-the-microservices-architecture/*](https://xebia.com/blog/the-monolithic-frontend-in-the-microservices-architecture/)

-   **Mauro Servienti 뛰어난 UI 구성의 비결**
    [*https://particular.net/blog/secret-of-better-ui-composition*](https://particular.net/blog/secret-of-better-ui-composition)

-   **Viktor Farcic 마이크로 서비스에 프런트 엔드 웹 구성 요소 포함하기**
    [*https://technologyconversations.com/2015/08/09/including-front-end-web-components-into-microservices/*](https://technologyconversations.com/2015/08/09/including-front-end-web-components-into-microservices/)

-   **마이크로 서비스 아키텍처에서 프런트 엔드 관리**\
    [*https://allegro.tech/2016/03/Managing-Frontend-in-the-microservices-architecture.html*](https://allegro.tech/2016/03/Managing-Frontend-in-the-microservices-architecture.html)


>[!div class="step-by-step"]
[이전](microservices-addressability-service-registry.md)
[다음](resilient-high-availability-microservices.md)
