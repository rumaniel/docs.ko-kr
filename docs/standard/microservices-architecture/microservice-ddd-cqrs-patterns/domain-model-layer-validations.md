---
title: 도메인 모델 레이어에서 유효성 검사 디자인
description: 컨테이너화된 .NET 응용 프로그램에 대한 .NET 마이크로 서비스 아키텍처 | 도메인 모델 레이어에서 유효성 검사 디자인
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.openlocfilehash: 6ff325bb062da2ebff815fc847d2247707a0bf7f
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50188055"
---
# <a name="designing-validations-in-the-domain-model-layer"></a>도메인 모델 레이어에서 유효성 검사 디자인

DDD에서 유효성 검사 규칙을 고정으로 생각할 수 있습니다. 집계의 기본 역할은 해당 집계 내의 모든 엔터티에 대한 상태 변경 내용에 고정을 적용하는 것입니다.

도메인 엔터티는 항상 유효한 엔터티여야 합니다. 항상 true여야 하는 개체에 대한 특정 수의 고정이 있습니다. 예를 들어 주문 항목 개체는 항상 양의 정수 더하기 아티클 이름 및 가격이어야 하는 수량을 가져야 합니다. 따라서 고정 적용은 도메인 엔터티(특히 집계 루트)의 책임이며 엔터티 개체는 유효하지 않고 존재할 수 없어야 합니다. 고정 규칙은 단순히 계약으로 표시되고 위반될 때 예외 또는 알림이 발생합니다.

이에 대한 이유는 개체가 있어 본 적 없어야 하는 상태에 있으므로 많은 버그가 발생하기 때문입니다. 다음은 [온라인 토론](https://jeffreypalermo.com/blog/the-fallacy-of-the-always-valid-entity/)에서 Greg Young의 좋은 설명입니다.

사용자 프로필을 사용하는 SendUserCreationEmailService가 있다고 제안해 보겠습니다. 해당 서비스에서 해당 이름이 Null이 아니라고 어떻게 합리화할 수 있나요? 다시 확인할까요? 또는 확인을 하지 않고 낙관할 가능성이 있습니다. 누군가가 당신에게 보내기 전에 유효성 검사를 고려했기를 희망합니다. 물론 TDD를 사용하여 작성해야 하는 첫 번째 테스트 중 하나는 Null 이름으로 고객에게 보내면 오류를 발생시켜야 한다는 것입니다. 하지만 이러한 종류의 테스트를 계속해서 다시 작성하면 "잠깐, Null이 되는 이름을 허용하지 않았다면 이런 모든 테스트를 하지 않았을텐데"라는 것을 깨닫게 됩니다.

## <a name="implementing-validations-in-the-domain-model-layer"></a>도메인 모델 레이어에서 유효성 검사 구현

유효성 검사는 도메인 엔터티 생성자 또는 엔터티를 업데이트할 수 있는 메서드에서 일반적으로 구현됩니다. 데이터를 확인하고 유효성 검사에 실패하는 경우 예외를 발생하는 것과 같은 유효성 검사를 구현하는 여러 방법이 있습니다. 유효성 검사에 대해 사양 패턴을 사용하고 발생할 때 각 유효성 검사에 대한 예외를 반환하는 대신 오류 컬렉션을 반환하는 알림 패턴과 같은 더 많은 고급 패턴이 있습니다.

### <a name="validating-conditions-and-throwing-exceptions"></a>조건 유효성 검사 및 예외 throw

다음 코드 예제에서는 예외를 발생시켜 도메인 엔터티에서 유효성을 검사하는 가장 간단한 방법을 보여 줍니다. 이 섹션 끝의 참조 테이블에서 이전에 설명한 패턴을 기반으로 하는 더 많은 고급 구현에 대한 링크를 볼 수 있습니다.

```csharp
public void SetAddress(Address address)
{
    _shippingAddress = address?? throw new ArgumentNullException(nameof(address));
}
```

적절한 예제는 내부 상태가 변경되지 않았거나 메서드에 대한 모든 변경이 발생했다는 것을 확인해야 함을 보여 줍니다. 예를 들어 다음 구현은 개체를 유효하지 않은 상태에 둘 수 있습니다.

```csharp
public void SetAddress(string line1, string line2,
    string city, string state, int zip)
{
    _shipingAddress.line1 = line1 ?? throw new ...
    _shippingAddress.line2 = line2;
    _shippingAddress.city = city ?? throw new ...
    _shippingAddress.state = (IsValid(state) ? state : throw new …);
}
```

상태 값이 유효하지 않은 경우 첫 번째 주소 줄 및 도시는 이미 변경되었습니다. 잘못된 주소를 만들 수 있습니다.

만들어진 후 엔터티가 유효한지 확인하도록 예외를 발생시켜 엔터티 생성자에서 유사한 방법을 사용할 수 있습니다.

### <a name="using-validation-attributes-in-the-model-based-on-data-annotations"></a>데이터 주석을 기반으로 하는 모델에서 유효성 검사 특성 사용

다른 방법은 데이터 주석을 기반으로 하는 유효성 검사 특성을 사용하는 것입니다. 유효성 검사 특성은 모델 유효성 검사를 구성하는 방법을 제공하며 데이터베이스 테이블의 필드에 대한 유효성 검사와 개념적으로 유사합니다. 데이터 형식이나 필수 필드를 할당하는 등 제약 조건이 포함됩니다. 다른 종류의 유효성 검사에는 신용 카드 번호, 전화 번호 또는 이메일 주소와 같은 비즈니스 규칙을 적용하기 위해 데이터에 패턴을 적용하는 것이 포함됩니다. 유효성 검사 특성은 요구 사항을 쉽게 적용할 수 있도록 합니다.

그러나 다음 코드에서와 같이 이 방법은 MVC 컨트롤러에서 호출해야 하는 Microsoft.AspNetCore.Mvc.ModelState에서 ModelState.IsValid에 대한 종속성을 사용하기 때문에 DDD 모델에서 매우 귀찮을 수 있습니다. 모델 유효성 검사는 각 컨트롤러 작업을 호출하기 전에 발생하며, ModelState.IsValid 호출의 결과를 검사하고 적절하게 반응하는 것은 컨트롤러 메서드의 책임입니다. 이를 사용하는 결정은 모델을 해당 인프라와 함께 하도록 밀접하게 결합하려는 방법에 따라 다릅니다.

```csharp
using System.ComponentModel.DataAnnotations;
// Other using statements ...
// Entity is a custom base class which has the ID
public class Product : Entity
{
    [Required]
    [StringLength(100)]
    public string Title { get; private set; }

    [Required]
    [Range(0, 999.99)]
    public decimal Price { get; private set; }

    [Required]
    [VintageProduct(1970)]
    [DataType(DataType.Date)]
    public DateTime ReleaseDate { get; private set; }

    [Required]
    [StringLength(1000)]
    public string Description { get; private set; }

    // Constructor...
    // Additional methods for entity logic and constructor...
}
```

그러나 DDD의 관점에서 도메인 모델은 엔터티의 동작 메서드에서 예외를 사용하거나 유효성 검사 규칙을 적용하도록 사양 및 알림 패턴을 구현하여 가장 잘 유지됩니다. ASP.NET Core의 데이터 주석과 같은 유효성 검사 프레임워크 또는 FluentValidation과 같은 다른 유효성 검사 프레임워크는 응용 프로그램 프레임워크를 호출하기 위해 요구 사항을 수행합니다. 예를 들어 데이터 주석에서 ModelState.IsValid 메서드를 호출할 때 ASP.NET 컨트롤러를 호출해야 합니다.

UI 계층 내에서 모델 유효성 검사를 허용하도록 입력을 허용하는 ViewModel 클래스(도메인 엔터티 대신)의 응용 프로그램 계층에서 데이터 주석을 사용하는 것이 가능합니다. 그러나 도메인 모델 내의 유효성 검사를 제외하고 수행되어서는 안 됩니다.

### <a name="validating-entities-by-implementing-the-specification-pattern-and-the-notification-pattern"></a>사양 패턴 및 알림 패턴을 구현하여 엔터티의 유효성 검사

마지막으로 도메인 모델에서 유효성 검사를 구현하는 보다 정교한 방법은 나중에 나열된 추가 리소스의 일부에서 설명된 것처럼 알림 패턴과 함께 사양 패턴을 구현하는 것입니다.

이러한 패턴 중 하나만 사용할 수도 있습니다. 예를 들어 제어 문을 사용하여 수동으로 유효성을 검사하지만 유효성 검사 오류 목록을 배치하고 반환하도록 알림 패턴을 사용합니다.

### <a name="using-deferred-validation-in-the-domain"></a>도메인에서 지연된 유효성 검사 사용

도메인에서 지연된 유효성 검사를 처리하는 다양한 방법이 있습니다. Vaughn Vernon은 그의 저서 [도메인 기반 디자인 구현](https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577)의 유효성 검사에 대한 섹션에서 이에 대해 설명합니다.

### <a name="two-step-validation"></a>2단계 유효성 검사

또한 2단계 유효성 검사를 고려합니다. 명령 DTO(데이터 전송 개체) 및 엔터티 내 도메인 수준 유효성 검사에서 필드 수준 유효성 검사를 사용합니다. 유효성 검사 오류를 쉽게 처리할 수 있도록 예외 대신 결과 개체를 반환하여 이를 수행할 수 있습니다.

예를 들어 데이터 주석과 함께 필드 유효성 검사를 사용하여 유효성 검사 정의를 중복하지 않습니다. 그러나 실행은 DTO의 경우 서버 쪽 및 클라이언트 쪽 모두가 될 수 있습니다(예: 명령 및 Viewmodel).

## <a name="additional-resources"></a>추가 자료

-   **Rachel Appel. ASP.NET Core MVC의 모델 유효성 검사 소개**
    [*https://docs.microsoft.com/aspnet/core/mvc/models/validation*](https://docs.microsoft.com/aspnet/core/mvc/models/validation)

-   **Rick Anderson. 유효성 검사 추가**
    [*https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/validation*](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/validation)

-   **Martin Fowler. 유효성 검사에서 예외 Throw를 알림으로 교체**
    [*https://martinfowler.com/articles/replaceThrowWithNotification.html*](https://martinfowler.com/articles/replaceThrowWithNotification.html)

-   **사양 및 알림 패턴**
    [*https://www.codeproject.com/Tips/790758/Specification-and-Notification-Patterns*](https://www.codeproject.com/Tips/790758/Specification-and-Notification-Patterns)

-   **Lev Gorodinski. DDD(도메인 기반 디자인)에서 유효성 검사**
    [*http://gorodinski.com/blog/2012/05/19/validation-in-domain-driven-design-ddd/*](http://gorodinski.com/blog/2012/05/19/validation-in-domain-driven-design-ddd/)

-   **Colin Jack. 도메인 모델 유효성 검사**
    [*http://colinjack.blogspot.com/2008/03/domain-model-validation.html*](http://colinjack.blogspot.com/2008/03/domain-model-validation.html)

-   **Jimmy Bogard. DDD 세계에서 유효성 검사**
    [*https://lostechies.com/jimmybogard/2009/02/15/validation-in-a-ddd-world/*](https://lostechies.com/jimmybogard/2009/02/15/validation-in-a-ddd-world/)


>[!div class="step-by-step"]
[이전](enumeration-classes-over-enum-types.md)
[다음](client-side-validation.md)
