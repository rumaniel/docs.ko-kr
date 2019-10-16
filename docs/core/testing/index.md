---
title: .NET Core 및 .NET Standard의 단위 테스트
description: 이 문서에서는 .NET Core 및 .NET Standard 프로젝트에 대한 단위 테스트의 간략한 개요를 제공합니다.
author: ardalis
ms.author: wiwagn
ms.date: 08/30/2017
ms.custom: seodec18
ms.openlocfilehash: 835e7c0cffbcd5857c33694586b4d63511ecadb8
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70926293"
---
# <a name="unit-testing-in-net-core-and-net-standard"></a>.NET Core 및 .NET Standard의 단위 테스트

.NET Core를 통해 쉽게 단위 테스트를 만들 수 있습니다. 이 문서에서는 단위 테스트를 소개하고 이 테스트와 다른 테스트의 차이점을 설명합니다. 페이지 아래쪽에 있는 연결된 리소스는 테스트 프로젝트를 솔루션에 추가하는 방법을 보여줍니다. 테스트 프로젝트를 설정한 후에 명령줄 또는 Visual Studio를 사용하여 단위 테스트를 실행할 수 있습니다.

**ASP.NET Core** 프로젝트를 테스트하는 경우 [ASP.NET Core의 통합 테스트](/aspnet/core/test/integration-tests#test-app-prerequisites)를 참조하세요.

.NET Core 2.0 이상은 [.NET Standard 2.0](../../standard/net-standard.md)을 지원하며 해당 라이브러리를 사용하여 단위 테스트를 보여줍니다.

C#, F# 및 Visual Basic에서 개인 프로젝트에 대한 시작점으로 기본 제공.NET Core 2.0 이상의 단위 테스트 프로젝트 템플릿을 사용합니다.

## <a name="what-are-unit-tests"></a>단위 테스트란?

자동화된 테스트가 있다면 소프트웨어 애플리케이션이 작성자가 의도한 대로 수행되는지 확인하는 좋은 방법입니다. 소프트웨어 애플리케이션에 대해 여러 종류의 테스트가 있습니다. 여기에는 통합 테스트, 웹 테스트, 부하 테스트 등이 포함됩니다. **단위 테스트**는 개별 소프트웨어 구성 요소와 메서드를 테스트합니다. 단위 테스트는 개발자의 제어 내에서만 코드를 테스트해야 합니다. 인프라 문제를 테스트하지 않습니다. 인프라 문제에는 데이터베이스, 파일 시스템 및 네트워크 리소스가 포함됩니다. 

또한 테스트를 작성하는 모범 사례가 있습니다. 예를 들어 [TDD(테스트 기반 개발)](https://deviq.com/test-driven-development/)는 확인하려는 코드보다 단위 테스트를 먼저 작성한 경우입니다. TDD는 책을 작성하기 전에 책에 대한 개요를 만드는 것과 같습니다. 이 기능을 통해 개발자가 간단하고 읽을 수 있고 효율적인 코드를 작성할 수 있습니다. 

> [!NOTE]
> ASP.NET 팀은 [이러한 규칙](https://github.com/aspnet/Home/wiki/Engineering-guidelines#unit-tests-and-functional-tests)을 따라 개발자가 테스트 클래스 및 메서드에 대해 적절한 이름을 제공할 수 있도록 합니다.

단위 테스트를 작성하는 경우 인프라에 대한 종속성을 도입하지 않습니다. 테스트가 느리고 불안정해지며 통합 테스트를 위해 예약되어야 합니다. [명시적 종속성 원칙](https://deviq.com/explicit-dependencies-principle/)을 따르고 [종속성 주입](/aspnet/core/fundamentals/dependency-injection)을 사용하여 애플리케이션에서 이러한 종속성을 방지할 수 있습니다. 통합 테스트의 개별 프로젝트에서 단위 테스트를 유지할 수도 있습니다. 이렇게 하면 단위 테스트 프로젝트가 인프라 패키지에 대한 참조 또는 종속성을 갖지 않습니다.

## <a name="next-steps"></a>다음 단계

.NET Core 프로젝트의 단위 테스트에 대한 자세한 내용:

.NET Core 단위 테스트 프로젝트는 다음에 지원됩니다.

* [C#](../../csharp/index.md)
* [F#](../../fsharp/index.md)
* [Visual Basic](../../visual-basic/index.md) 

다음 중에서 선택할 수도 있습니다.

* [xUnit](https://xunit.github.io) 
* [NUnit](https://nunit.org)
* [MSTest](https://github.com/Microsoft/testfx-docs)

다음 연습에서 자세히 알아볼 수 있습니다.

* .NET Core CLI와 함께 [*xUnit* 및 *C#* 을 사용하여 단위 테스트 만들기](unit-testing-with-dotnet-test.md)
* .NET Core CLI와 함께 [*NUnit* 및 *C#* 을 사용하여 단위 테스트 만들기](unit-testing-with-nunit.md)
* .NET Core CLI와 함께 [*MSTest* 및 *C#* 을 사용하여 단위 테스트 만들기](unit-testing-with-mstest.md)
* .NET Core CLI와 함께 [*xUnit* 및 *F#* 을 사용하여 단위 테스트 만들기](unit-testing-fsharp-with-dotnet-test.md)
* .NET Core CLI와 함께 [*NUnit* 및 *F#* 을 사용하여 단위 테스트 만들기](unit-testing-fsharp-with-nunit.md)
* .NET Core CLI와 함께 [*MSTest* 및 *F#* 을 사용하여 단위 테스트 만들기](unit-testing-fsharp-with-mstest.md)
* .NET Core CLI와 함께 [*xUnit* 및 *Visual Basic*을 사용하여 단위 테스트 만들기](unit-testing-visual-basic-with-dotnet-test.md)
* .NET Core CLI와 함께 [*NUnit* 및 *Visual Basic*을 사용하여 단위 테스트 만들기](unit-testing-visual-basic-with-nunit.md)
* .NET Core CLI와 함께 [*MSTest* 및 *Visual Basic*을 사용하여 단위 테스트 만들기](unit-testing-visual-basic-with-mstest.md)

다음 문서에서 자세히 알아볼 수 있습니다.

* Visual Studio Enterprise는 .NET Core를 위한 훌륭한 테스트 도구를 제공합니다. [Live Unit Testing](/visualstudio/test/live-unit-testing) 또는 [ 코드 검사](https://github.com/Microsoft/vstest-docs/blob/master/docs/analyze.md#working-with-code-coverage)를 통해 자세히 알아보세요.
* 선택적 단위 테스트를 실행하는 방법에 대한 추가 정보는 [선택적 단위 테스트 실행](selective-unit-tests.md) 또는 [Visual Studio를 사용하여 테스트 포함 및 제외](/visualstudio/test/live-unit-testing#include-and-exclude-test-projects-and-test-methods)를 참조하세요.
* [.NET Core 및 Visual Studio와 xUnit을 사용하는 방법](https://xunit.github.io/docs/getting-started-dotnet-core.html)
