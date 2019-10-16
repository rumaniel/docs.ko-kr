---
title: C#에서 기본 인터페이스 메서드를 사용하여 안전하게 인터페이스 업데이트
description: 이 고급 자습서에서는 해당 인터페이스를 구현하는 모든 클래스 및 구성 요소를 훼손하지 않고 기존 인터페이스 정의에 새 기능을 안전하게 추가할 수 있는 방법을 살펴봅니다.
ms.date: 05/06/2019
ms.custom: mvc
ms.openlocfilehash: 71fce2594dbf5ef3175a6b9bdf4e6edba754bb84
ms.sourcegitcommit: 992f80328b51b165051c42ff5330788627abe973
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2019
ms.locfileid: "72275988"
---
# <a name="tutorial-update-interfaces-with-default-interface-methods-in-c-80"></a>자습서: C# 8.0에서 기본 인터페이스 메서드로 인터페이스를 업데이트

.NET Core 3.0의 C# 8.0에서부터, 인터페이스 멤버 선언 시 구현을 정의할 수 있습니다. 가장 일반적인 시나리오는 이미 릴리스되어 수많은 클라이언트가 사용하는 인터페이스에 멤버를 안전하게 추가하는 것입니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
>
> * 구현으로 메서드를 추가하여 안전하게 인터페이스를 확장합니다.
> * 매개 변수가 있는 구현을 생성하여 향상된 유연성을 제공합니다.
> * 구현자가 재정의 형식으로 더 구체적인 구현을 제공하도록 지원합니다.

## <a name="prerequisites"></a>전제 조건

C# 8.0 컴파일러를 포함하여 .NET Core를 실행하도록 머신을 설정해야 합니다. C# 8.0 컴파일러는 [Visual Studio 2019 버전 16.3](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) 또는 [.NET CORE 3.0 SDK](https://dotnet.microsoft.com/download)부터 사용할 수 있습니다.

## <a name="scenario-overview"></a>시나리오 개요

이 자습서는 고객 관계 라이브러리의 버전 1부터 시작합니다. [GitHub의 샘플 리포지토리](https://github.com/dotnet/samples/tree/master/csharp/tutorials/default-interface-members-versions/starter/customer-relationship)에서 시작 애플리케이션을 다운로드할 수 있습니다. 이 라이브러리를 구축한 회사는 기존 애플리케이션이 있는 고객이 자사의 라이브러리를 채택할 것을 의도했으며, 구현할 라이브러리의 사용자에게 최소의 인터페이스 정의를 제공했습니다. 다음은 고객에 대한 인터페이스 정의입니다.

[!code-csharp[InitialCustomerInterface](~/samples/csharp/tutorials/default-interface-members-versions/starter/customer-relationship/ICustomer.cs?name=SnippetICustomerVersion1)]

이들은 주문을 나타내는 두 번째 인터페이스를 정의했습니다.

[!code-csharp[InitialOrderInterface](~/samples/csharp/tutorials/default-interface-members-versions/starter/customer-relationship/IOrder.cs?name=SnippetIorderVersion1)]

이러한 인터페이스에서, 팀은 사용자가 고객을 위해 더 나은 경험을 만들 수 있는 라이브러리를 빌드할 수 있었습니다. 이들의 목표는 기존 고객과 더 깊은 관계를 형성하고 신규 고객과의 관계를 개선하는 것이었습니다.

이제, 다음 릴리스를 위해 라이브러리를 업그레이드할 시간입니다. 요청된 기능 중 하나는 주문건이 많은 고객을 위해 충성도 할인을 지원하는 것입니다. 고객이 주문할 때마다 이 새로운 충성도 할인이 적용됩니다. 특정 할인은 각 개인 고객의 속성입니다. 구현된 각 `ICustomer`마다 고객 할인에 대해 다른 규칙을 설정할 수 있습니다. 

이 기능을 추가하는 가장 일반적인 방법은 충성도 할인을 적용할 메서드로 `ICustomer` 인터페이스를 개선하는 것입니다. 이러한 설계 제안은 숙련된 개발자 사이에서 우려를 일으켰습니다. "인터페이스는 릴리스된 후에는 변경이 불가합니다! 주요 변경 사항입니다!” C#8.0은 인터페이스 업그레이드를 위해 *기본 인터페이스 구현*을 추가했습니다. 라이브러리 작성자가 인터페이스에 새 멤버를 추가하고 해당 멤버에 대한 기본 구현을 제공할 수 있습니다.

기본 인터페이스 구현을 통해 구현자는 해당 구현을 재지정하고 개발자는 인터페이스를 업그레이드할 수 있습니다. 라이브러리의 사용자는 기본 구현을 일반적인 변경으로 받아들일 수 있습니다. 비즈니스 규칙이 다른 경우 재지정할 수 있습니다.

## <a name="upgrade-with-default-interface-methods"></a>기본 인터페이스 메서드를 사용하여 업그레이드

팀은 가장 가능성 있는 기본 구현, 즉 고객을 위한 충성도 할인에 합의했습니다.

업그레이드는 할인 자격을 갖추기 위해 필요한 주문 수, 할인율, 이 두 가지 속성에 기능을 제공해야 합니다. 이로써 기본 인터페이스 메서드에 완벽한 시나리오가 됩니다. `ICustomer` 인터페이스에 메서드를 추가하고 가장 가능성이 높은 구현을 제공할 수 있습니다. 모든 기존, 그리고 새 구현은 기본 구현을 사용하거나 자체 구현을 제공할 수 있습니다.

먼저, 구현에 새 메서드를 추가합니다.

[!code-csharp[InitialOrderInterface](~/samples/csharp/tutorials/default-interface-members-versions/finished/customer-relationship/ICustomer.cs?name=SnippetLoyaltyDiscountVersionOne)]

라이브러리 작성자는 구현을 확인하기 위해 첫 번재 테스트를 작성했습니다.

[!code-csharp[TestDefaultImplementation](~/samples/csharp/tutorials/default-interface-members-versions/finished/customer-relationship/Program.cs?name=SnippetTestDefaultImplementation)]

테스트의 다음 부분을 확인합니다.

[!code-csharp[TestDefaultImplementation](~/samples/csharp/tutorials/default-interface-members-versions/finished/customer-relationship/Program.cs?name=SnippetHighlightCast)]

`SampleCustomer`에서 `ICustomer`로의 캐스트가 필요합니다. `SampleCustomer` 클래스는 `ComputeLoyaltyDiscount`에 대한 구현을 제공할 필요가 없으며, `ICustomer` 인터페이스에서 제공합니다. 그러나 `SampleCustomer` 클래스는 인터페이스에서 멤버를 상속하지 않습니다. 이 규칙은 바뀌지 않았습니다. 인터페이스에서 선언 및 구현된 메서드를 호출하려면 변수는 인터페이스 유형(이 예에서는 `ICustomer`)이어야 합니다.

## <a name="provide-parameterization"></a>매개 변수화 제공

시작이 좋습니다. 그러나 기본 구현은 너무 제한적입니다. 이 시스템의 많은 소비자가 구매 건수에 다른 임계값, 다른 멤버십 기간 또는 다른 할인율을 선택할 수 있습니다. 이러한 매개 변수를 설정하는 방법을 제공하여 더 많은 고객에게 향상된 업그레이드 환경을 제공할 수 있습니다. 기본 구현을 제어하는 세 개의 매개 변수를 설정하는 정적 메서드를 추가해 보겠습니다.

[!code-csharp[VersionTwoImplementation](~/samples/csharp/tutorials/default-interface-members-versions/finished/customer-relationship/ICustomer.cs?name=SnippetLoyaltyDiscountVersionTwo)]

이 작은 코드 조각에 표시되는 많은 새 언어 기능이 있습니다. 이제 인터페이스는 필드 및 메서드를 포함한 정적 멤버를 포함할 수 있습니다. 서로 다른 액세스 한정자도 사용할 수 있습니다. 추가 필드는 비공개이고 새 메서드는 공개입니다. 어떠한 한정자도 인터페이스 멤버에서 허용됩니다.

충성도 할인을 계산하기 위해 일반 공식을 사용하지만 매개 변수는 다른 애플리케이션은 사용자 지정 구현을 제공할 필요가 없지만, 정적 메서드를 통해 인수를 설정할 수 있습니다. 예를 들어, 다음 코드는 멤버십이 1개월 이상인 고객에게 보답하는 “고객 감사”를 설정합니다.

[!code-csharp[SetLoyaltyThresholds](~/samples/csharp/tutorials/default-interface-members-versions/finished/customer-relationship/Program.cs?name=SnippetSetLoyaltyThresholds)]

## <a name="extend-the-default-implementation"></a>기본 구현 확장

지금까지 추가한 코드는 사용자가 기본 구현과 같은 것을 원하거나, 관련 없는 규칙 세트를 제공하는 시나리오에 편리한 구현을 제공했습니다. 최종 기능을 위해, 코드를 약간 리팩터링하여 사용자가 기본 구현을 기반으로 구축하려는 시나리오를 구현해 보겠습니다. 

신규 고객을 유치하고 싶은 스타트업 회사가 있다고 해보겠습니다. 이 회사는 신규 고객의 첫 주문에 50% 할인을 제공합니다. 한편, 기존 고객에게는 표준 할인이 적용됩니다. 라이브러리 작성자는 이 인터페이스를 구현하는 클래스가 해당 구현에서 코드를 재사용할 수 있도록 기본 구현을 `protected static` 메서드로 이동해야 합니다. 인터페이스 멤버의 기본 구현은 이 공유 메서드로 호출합니다.

[!code-csharp[VersionTwoImplementation](~/samples/csharp/tutorials/default-interface-members-versions/finished/customer-relationship/ICustomer.cs?name=SnippetFinalVersion)]

이 인터페이스를 구현하는 클래스의 구현에서 재지정은 정적 도우미 메서드를 호출하며, 이 논리를 확장하여 “신규 고객” 할인을 제공할 수 있습니다.

[!code-csharp[VersionTwoImplementation](~/samples/csharp/tutorials/default-interface-members-versions/finished/customer-relationship/SampleCustomer.cs?name=SnippetOverrideAndExtend)]

[GitHub의 샘플 리포지토리](https://github.com/dotnet/samples/tree/master/csharp/tutorials/default-interface-members-versions/finished/customer-relationship)에서 완성된 전체 코드를 볼 수 있습니다. [GitHub의 샘플 리포지토리](https://github.com/dotnet/samples/tree/master/csharp/tutorials/default-interface-members-versions/starter/customer-relationship)에서 시작 애플리케이션을 다운로드할 수 있습니다.

이러한 새 기능은 신규 멤버에 대한 합리적인 기본 구현이 있는 경우 인터페이스를 안전하게 업데이트할 수 있음을 의미합니다. 여러 클래스를 통해 구현할 수 있는 단일 기능 아이디어를 표현하려면 인터페이스를 신중하게 설계하세요. 이를 통해 동일한 기능 아이디어에 새로운 요구 사항이 발견될 경우 해당 인터페이스 정의를 훨씬 쉽게 업그레이드할 수 있습니다.
