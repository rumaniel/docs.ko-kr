---
title: dotnet test 및 xUnit을 사용하여 .NET Core에서 C# 코드 유닛 테스트
description: dotnet test 및 xUnit을 사용하여 샘플 솔루션을 단계별로 빌드하는 대화형 환경을 통해 C# 및 .NET Core의 단위 테스트 개념을 알아봅니다.
author: ardalis
ms.author: wiwagn
ms.date: 11/29/2017
ms.custom: seodec18
ms.openlocfilehash: d85e3e69721d8933565b1c80fb7ed21b2291e60e
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117291"
---
# <a name="unit-testing-c-in-net-core-using-dotnet-test-and-xunit"></a>dotnet 테스트 및 xUnit을 사용하여 .NET Core에서 C# 단위 테스트

이 자습서에서는 샘플 솔루션을 단계별로 빌드하는 대화형 환경을 통해 단위 테스트 개념을 알아볼 수 있습니다. 미리 빌드된 솔루션을 사용하여 이 자습서를 진행하려는 경우 시작하기 전에 [샘플 코드를 보거나 다운로드](https://github.com/dotnet/samples/tree/master/core/getting-started/unit-testing-using-dotnet-test/). 다운로드 지침은 [샘플 및 자습서](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)를 참조하세요.

[!INCLUDE [testing an ASP.NET Core project from .NET Core](../../../includes/core-testing-note-aspnet.md)]

## <a name="creating-the-source-project"></a>소스 프로젝트 만들기

셸 창을 엽니다. 솔루션을 저장하기 위한 *unit-testing-using-dotnet-test*라는 디렉터리를 만듭니다.
이 새 디렉터리 내에서 [`dotnet new sln`](../tools/dotnet-new.md)을 실행하여 새 솔루션을 만듭니다. 솔루션이 있으면 클래스 라이브러리와 단위 테스트 프로젝트를 모두 더 쉽게 관리할 수 있습니다.
솔루션 디렉터리 내에 *PrimeService* 디렉터리를 만듭니다. 지금까지의 디렉터리 및 파일 구조는 다음과 같아야 합니다.

```
/unit-testing-using-dotnet-test
    unit-testing-using-dotnet-test.sln
    /PrimeService
```

*PrimeService*를 현재 디렉터리로 만들고 [`dotnet new classlib`](../tools/dotnet-new.md)를 실행하여 소스 프로젝트를 만듭니다. *Class1.cs*의 이름을 *PrimeService.cs*로 바꿉니다. 먼저 다음과 같이 `PrimeService` 클래스의 실패 구현을 만듭니다.

```csharp
using System;

namespace Prime.Services
{
    public class PrimeService
    {
        public bool IsPrime(int candidate)
        {
            throw new NotImplementedException("Please create a test first.");
        }
    }
}
```

디렉터리를 다시 *unit-testing-using-dotnet-test* 디렉터리로 변경합니다.

[dotnet sln](../tools/dotnet-sln.md) 명령을 실행하여 클래스 라이브러리 프로젝트를 솔루션에 추가합니다.

```dotnetcli
dotnet sln add ./PrimeService/PrimeService.csproj
```

## <a name="creating-the-test-project"></a>테스트 프로젝트 만들기

다음으로 *PrimeService.Tests* 디렉터리를 만듭니다. 다음 개요에는 디렉터리 구조가 나와 있습니다.

```
/unit-testing-using-dotnet-test
    unit-testing-using-dotnet-test.sln
    /PrimeService
        Source Files
        PrimeService.csproj
    /PrimeService.Tests
```

*PrimeService.Tests* 디렉터리를 현재 디렉터리로 만들고 [`dotnet new xunit`](../tools/dotnet-new.md)를 사용하여 새 프로젝트를 만듭니다. 이 명령은 [xUnit](https://xunit.github.io/)을 테스트 라이브러리로 사용하는 테스트 프로젝트를 만듭니다. 생성된 템플릿은 다음 코드와 유사한 *PrimeServiceTests.csproj* 파일에서 Test Runner를 구성합니다.

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.3.0" />
  <PackageReference Include="xunit" Version="2.2.0" />
  <PackageReference Include="xunit.runner.visualstudio" Version="2.2.0" />
</ItemGroup>
```

테스트 프로제트는 다른 패키지에 단위 테스트를 만들고 실행하도록 요구합니다. 이전 단계의 `dotnet new`는 xUnit 및 xUnit runner를 추가했습니다. 이제 `PrimeService` 클래스 라이브러리를 프로젝트에 다른 종속성으로 추가합니다. [`dotnet add reference`](../tools/dotnet-add-reference.md) 명령을 사용합니다.

```dotnetcli
dotnet add reference ../PrimeService/PrimeService.csproj
```

GitHub의 [샘플 리포지토리](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-dotnet-test/PrimeService.Tests/PrimeService.Tests.csproj)에서 전체 파일을 볼 수 있습니다.

최종 솔루션 레이아웃은 다음과 같습니다.

```
/unit-testing-using-dotnet-test
    unit-testing-using-dotnet-test.sln
    /PrimeService
        Source Files
        PrimeService.csproj
    /PrimeService.Tests
        Test Source Files
        PrimeServiceTests.csproj
```

솔루션에 테스트 프로젝트를 추가하려면 *unit-testing-using-dotnet-test* 디렉터리에서 [dotnet sln](../tools/dotnet-sln.md) 명령을 실행합니다.

```dotnetcli
dotnet sln add ./PrimeService.Tests/PrimeService.Tests.csproj
```

## <a name="creating-the-first-test"></a>첫 번째 테스트 만들기

하나의 실패 테스트를 작성하고, 테스트가 성공하도록 만듭니다. 이 작업을 반복합니다. *PrimeService.Tests* 디렉터리에서 *UnitTest1.cs*를 제거하고 새 C# 파일 *PrimeService_IsPrimeShould.cs*를 만듭니다. 다음 코드를 추가합니다.

```csharp
using Xunit;
using Prime.Services;

namespace Prime.UnitTests.Services
{
    public class PrimeService_IsPrimeShould
    {
        private readonly PrimeService _primeService;

        public PrimeService_IsPrimeShould()
        {
            _primeService = new PrimeService();
        }

        [Fact]
        public void IsPrime_InputIs1_ReturnFalse()
        {
            var result = _primeService.IsPrime(1);

            Assert.False(result, "1 should not be prime");
        }
    }
}
```

`[Fact]` 특성은 Test Runner에서 실행하는 테스트 메서드를 나타냅니다. *PrimeService.Tests* 폴더에서 [`dotnet test`](../tools/dotnet-test.md)를 실행하여 테스트 및 클래스 라이브러리를 빌드한 다음 테스트를 실행합니다. xUnit Test Runner에는 테스트를 실행할 프로그램 진입점이 포함되어 있습니다. `dotnet test`는 만든 단위 테스트 프로젝트를 사용하여 Test Runner를 시작합니다.

테스트가 실패합니다. 구현은 아직 만들지 않았습니다. `PrimeService` 클래스에서 작동하는 가장 간단한 코드를 작성하여 이 테스트를 통과시킵니다. 기존 `IsPrime` 메서드 구현을 다음 코드로 바꿉니다.

```csharp
public bool IsPrime(int candidate)
{
    if (candidate == 1)
    {
        return false;
    }
    throw new NotImplementedException("Please create a test first.");
}
```

*PrimeService.Tests* 디렉터리에서 `dotnet test`를 다시 실행합니다. `dotnet test` 명령은 `PrimeService` 프로젝트에 대한 빌드를 실행한 다음 `PrimeService.Tests` 프로젝트에 대한 빌드를 실행합니다. 두 프로젝트를 모두 빌드한 후 이 단일 테스트를 실행합니다. 전달합니다.

## <a name="adding-more-features"></a>더 많은 기능 추가

이제 하나의 테스트를 통과했으므로 더 작성할 수 있습니다. 소수에 대한 몇 가지 다른 간단한 사례가 있습니다 (0, -1). 이러한 사례를 `[Fact]` 특성과 함께 새 테스트로 추가할 수도 있지만, 이렇게 하면 금방 지루해질 수 있습니다. 유사한 테스트 모음을 작성하는 데 사용할 수 있는 다른 xUnit 특성이 있습니다.

- `[Theory]`는 같은 코드를 실행하지만, 다른 입력 인수가 포함된 테스트 모음을 나타냅니다.

- `[InlineData]` 특성은 해당 입력에 대한 값을 지정합니다.

새 테스트를 만드는 대신 이러한 두 가지 특성 `[Theory]` 및 `[InlineData]`를 적용하여 *PrimeService_IsPrimeShould.cs* 파일에서 단일 이론을 만듭니다. 이 이론은 가장 작은 소수인 2보다 작은 몇 가지 값을 테스트하는 메서드입니다.

[!code-csharp[Sample_TestCode](../../../samples/core/getting-started/unit-testing-using-dotnet-test/PrimeService.Tests/PrimeService_IsPrimeShould.cs?name=Sample_TestCode)]

`dotnet test`를 다시 실행하면 이러한 두 가지 테스트가 실패합니다. 모든 테스트를 통과하려면 *PrimeService.cs* 파일에서 `IsPrime` 메서드의 시작 부분에 있는 `if` 절을 변경합니다.

```csharp
if (candidate < 2)
```

기본 라이브러리에서 더 많은 테스트, 더 많은 이론, 더 많은 코드를 추가하여 계속 반복합니다. [테스트의 완료된 버전](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-dotnet-test/PrimeService.Tests/PrimeService_IsPrimeShould.cs) 및 [라이브러리의 완전한 구현](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-dotnet-test/PrimeService/PrimeService.cs)을 얻게 됩니다.

### <a name="additional-resources"></a>추가 자료

- [xUnit.net 공식 사이트](https://xunit.github.io)
- [ASP.NET Core에서 컨트롤러 논리 테스트](/aspnet/core/mvc/controllers/testing)
