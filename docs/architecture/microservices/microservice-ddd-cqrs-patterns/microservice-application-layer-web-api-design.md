---
title: 마이크로 서비스 애플리케이션 레이어 및 웹 API 설계
description: 컨테이너화된 .NET 애플리케이션을 위한 .NET 마이크로 서비스 아키텍처 | 애플리케이션 계층 설계를 위한 SOLID 원칙의 간략한 설명
ms.date: 10/08/2018
ms.openlocfilehash: 3c3b9f74e76e01deafa1f97de5d3250d57716014
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68676520"
---
# <a name="design-the-microservice-application-layer-and-web-api"></a>마이크로 서비스 애플리케이션 계층 및 웹 API 설계하기

## <a name="use-solid-principles-and-dependency-injection"></a>SOLID 원칙 및 종속성 주입 사용하기

SOLID 원칙은 DDD 패턴을 통한 마이크로 서비스 개발처럼 현대적인 필수 애플리케이션에서 사용되는 중요한 기법입니다. SOLID는 5가지 기본 원칙을 묶은 머리글자어입니다.

- Single Responsibility(단일 책임) 원칙

- Open/closed(개방/폐쇄) 원칙

- Liskov 대체 원칙

- Interface Segregation(인터페이스 분리) 원칙

- Dependency Inversion(종속성 반전) 원칙

SOLID는 애플리케이션 또는 마이크로 서비스 내부 계층을 설계하는 방식과 계층 간의 종속성을 분리하는 방법에 관한 것입니다. 도메인이 아니라 애플리케이션의 기술적 설계와 관련이 있습니다. 마지막 원칙인 종속성 반전 원칙에서는 인프라 계층을 나머지 계층과 분리하여 DDD 계층의 분리 구현을 향상할 수 있습니다.

DI(종속성 주입)는 종속성 반전 원칙을 구현하는 한 방법입니다. 개체와 그 종속성 간의 느슨한 결합을 실현하기 위한 기술입니다. 협력자를 직접 인스턴스화하거나 고정 참조를 사용(즉, 새로 만들기 사용)하는 대신 클래스가 해당 작업을 수행하기 위해 필요한 개체를 클래스에 제공(또는 "주입")합니다. 대부분의 경우 클래스는 해당 생성자를 통해 해당 종속성을 선언하게 되며 명시적 종속성 원칙을 따르도록 허용합니다. 종속성 주입은 일반적으로 특정 IoC(Inversion of Control) 컨테이너를 기반으로 합니다. ASP.NET Core에는 간단한 기본 제공 IoC가 있지만 Autofac 또는 Ninject처럼 사용자가 원하는 IoC 컨테이너를 사용할 수도 있습니다.

SOLID 원칙에 따르면 클래스는 당연히 작고 잘 구성되며 쉽게 테스트됩니다. 그러나 클래스에 너무 많은 종속성이 주입된 것을 어떻게 알 수 있을까요? 생성자를 통해 DI를 사용할 경우 생성자에 대한 매개 변수 수를 살피기만 해도 이를 쉽게 감지할 수 있습니다. 종속성이 너무 많은 경우 이는 일반적으로 클래스가 너무 많은 작업을 시도하고 있으며 아마도 SRP([단일 책임 원칙](https://deviq.com/code-smells/))를 위반하고 있다는 신호입니다.

SOLID에 대해서는 다른 가이드에서 자세히 다룰 것입니다. 따라서 이 가이드에서는 이 항목에 대한 최소한의 지식만 요구합니다.

#### <a name="additional-resources"></a>추가 자료

- **SOLID: 기본 OOP 원칙** \
  <https://deviq.com/solid/>

- **Inversion of Control 컨테이너 및 종속성 주입 패턴** \
  <https://martinfowler.com/articles/injection.html>

- **Steve Smith. 새 항목은 붙이기 입니다** \
  <https://ardalis.com/new-is-glue>

> [!div class="step-by-step"]
> [이전](nosql-database-persistence-infrastructure.md)
> [다음](microservice-application-layer-implementation-web-api.md)
