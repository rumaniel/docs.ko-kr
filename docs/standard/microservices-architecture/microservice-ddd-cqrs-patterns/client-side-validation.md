---
title: 클라이언트 쪽 유효성 검사(프레젠테이션 레이어의 유효성 검사)
description: 컨테이너화된 .NET 응용 프로그램에 대한 .NET 마이크로 서비스 아키텍처 | 클라이언트 쪽 유효성 검사(프레젠테이션 레이어의 유효성 검사)
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.openlocfilehash: 70a1f716797e03acdcbf1c58d4b0302449d98fa9
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48582426"
---
# <a name="client-side-validation-validation-in-the-presentation-layers"></a>클라이언트 쪽 유효성 검사(프레젠테이션 레이어의 유효성 검사)

정보의 원본이 도메인 모델이며 궁극적으로 도메인 모델 수준에서 유효성 검사를 해야 하는 경우 도메인 모델 수준(서버 쪽) 및 클라이언트 쪽 모두에서 계속 유효성 검사를 처리할 수 있습니다.

클라이언트 쪽 유효성 검사는 사용자에게 매우 편리합니다. 그렇지 않은 경우 유효성 검사 오류를 반환할 수 있는 서버에 대한 왕복을 기다리는 데 드는 시간을 절약할 수 있습니다. 비즈니스 용어로 몇 초를 매일 수백 번 반복하게 되면 많은 시간과 비용, 노력이 추가됩니다. 간단하고 즉각적인 유효성 검사를 사용하면 사용자가 보다 효율적으로 작업하고 더 좋은 품질의 입력 및 출력을 생성할 수 있습니다.

보기 모델과 도메인 모델이 다른 것처럼 보기 모델 유효성 검사와 도메인 모델 유효성 검사는 유사하지만 용도가 다릅니다. DRY(반복 금지 원칙)에 대해 우려하는 경우 이 사례에서 코드를 재사용하면 결합될 수도 있음을 고려합니다. 또한 엔터프라이즈 응용 프로그램에서 서버 쪽을 클라이언트 쪽에 결합하는 것은 반복 금지 원칙을 따르는 것보다 중요하지 않습니다.

클라이언트 쪽 유효성 검사를 사용할 경우에도 서버 API가 가능한 공격 벡터일 수 있기 때문에 항상 서버 코드에서 명령 또는 DTO의 유효성을 검사해야 합니다. 클라이언트 응용 프로그램이 있는 경우 UX 관점에서 볼 때 예방하고 사용자가 잘못된 정보를 입력할 수 없도록 하는 것이 최선이기 때문에 일반적으로 둘 다 수행하는 것이 가장 좋습니다.

따라서 일반적으로 클라이언트 쪽 코드에서 ViewModels의 유효성을 검사합니다. 서비스에 보내기 전에 클라이언트 출력 DTO 또는 명령의 유효성을 검사할 수도 있습니다.

클라이언트 쪽 유효성 검사를 구현하는 작업은 빌드하는 클라이언트 응용 프로그램의 종류에 따라 달라집니다. .NET에서 대부분의 코드를 사용하는 웹 MVC 웹 응용 프로그램, JavaScript 또는 TypeScript로 코딩된 해당 유효성 검사를 사용하는 SPA 웹 응용 프로그램 또는 Xamarin 및 C#을 사용하는 코딩된 모바일 앱의 데이터 유효성을 검사하는지에 따라 다릅니다.

## <a name="additional-resources"></a>추가 자료

### <a name="validation-in-xamarin-mobile-apps"></a>Xamarin 모바일 앱의 유효성 검사

-   **텍스트 입력 유효성 검사 및 오류 표시**
    [*https://developer.xamarin.com/recipes/ios/standard\_controls/text\_field/validate\_input/*](https://developer.xamarin.com/recipes/ios/standard_controls/text_field/validate_input/)

-   **유효성 검사 콜백**
    [*https://developer.xamarin.com/samples/xamarin-forms/XAML/ValidationCallback/*](https://developer.xamarin.com/samples/xamarin-forms/XAML/ValidationCallback/)

### <a name="validation-in-aspnet-core-apps"></a>ASP.NET Core 앱의 유효성 검사

-   **Rick Anderson. 유효성 검사 추가**
    [*https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/validation*](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/validation)

### <a name="validation-in-spa-web-apps-angular-2-typescript-javascript"></a>SPA 웹앱의 유효성 검사(Angular 2, TypeScript, JavaScript)

-   **Ado Kukic. Angular 2 양식 유효성 검사**
    [*https://scotch.io/tutorials/angular-2-form-validation*](https://scotch.io/tutorials/angular-2-form-validation)

-   **양식 유효성 검사**
    [*https://angular.io/docs/ts/latest/cookbook/form-validation.html*](https://angular.io/docs/ts/latest/cookbook/form-validation.html)

-   **유효성 검사** Breeze 설명서
    [*https://breeze.github.io/doc-js/validation.html*](https://breeze.github.io/doc-js/validation.html)

요약하면 유효성 검사에 관해 가장 중요한 개념은 다음과 같습니다.

- 엔터티 및 집계는 고유한 일관성을 적용하고 "항상 유효"해야 합니다. 집계 루트는 동일한 집계 내에서 다중 엔터티 일관성을 담당합니다.

- 엔터티가 잘못된 상태를 입력해야 하는 경우 다양한 개체 모델을 사용하는 것이 좋습니다. 예를 들어 최종 도메인 엔터티를 만들 때까지 임시 DTO를 사용합니다.

- 집계 함수와 같은 여러 관련 개체를 만들어야 하고 해당 개체를 모두 만들어야만 유효한 경우 팩터리 패턴을 사용하는 것이 좋습니다.

- 유효성 검사 프레임워크는 프레젠테이션 계층 또는 응용 프로그램/서비스 계층과 같은 특정 계층에서 사용되기에 적합하지만 인프라 프레임워크에 대한 종속성이 커야 하기 때문에 도메인 모델 계층에서는 일반적으로 적합하지 않습니다.

- 대부분의 경우에 응용 프로그램이 예방적일 수 있기 때문에 클라이언트 쪽에서 중복 유효성을 검사하는 것이 적절합니다.

>[!div class="step-by-step"]
[이전](domain-model-layer-validations.md)
[다음](domain-events-design-implementation.md)