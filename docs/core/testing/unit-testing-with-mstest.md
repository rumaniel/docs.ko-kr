---
title: MSTest 및 .NET Core를 사용한 C# 유닛 테스트
description: dotnet test 및 MSTest를 사용하여 샘플 솔루션을 단계별로 빌드하는 대화형 환경을 통해 C# 및 .NET Core의 단위 테스트 개념을 알아봅니다.
author: ncarandini
ms.author: wiwagn
ms.date: 09/08/2017
ms.custom: seodec18
ms.openlocfilehash: d9ad21aded45c8955e24b93fd4ddf8a86b989055
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71116177"
---
# <a name="unit-testing-c-with-mstest-and-net-core"></a>MSTest 및 .NET Core를 사용한 C# 유닛 테스트

이 자습서에서는 샘플 솔루션을 단계별로 빌드하는 대화형 환경을 통해 단위 테스트 개념을 알아볼 수 있습니다. 미리 빌드된 솔루션을 사용하여 이 자습서를 진행하려는 경우 시작하기 전에 [샘플 코드를 보거나 다운로드](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-mstest/). 다운로드 지침은 [샘플 및 자습서](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)를 참조하세요.

[!INCLUDE [testing an ASP.NET Core project from .NET Core](../../../includes/core-testing-note-aspnet.md)]

## <a name="create-the-source-project"></a>소스 프로젝트 만들기

셸 창을 엽니다. 솔루션을 저장할 *unit-testing-using-mstest*라는 디렉터리를 만듭니다. 이 새 디렉터리 내에서 [`dotnet new sln`](../tools/dotnet-new.md)을 실행하여 클래스 라이브러리 및 테스트 프로젝트에 대한 새 솔루션 파일을 만듭니다. 다음으로 *PrimeService* 디렉터리를 만듭니다. 다음 개요에는 지금까지의 디렉터리 및 파일 구조가 나와 있습니다.

```console
/unit-testing-using-mstest
    unit-testing-using-mstest.sln
    /PrimeService
```

*PrimeService*를 현재 디렉터리로 만들고 [`dotnet new classlib`](../tools/dotnet-new.md)를 실행하여 소스 프로젝트를 만듭니다. *Class1.cs*의 이름을 *PrimeService.cs*로 바꿉니다. 다음과 같이 `PrimeService` 클래스의 실패 구현을 만듭니다.

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

디렉터리를 다시 *unit-testing-using-mstest* 디렉터리로 변경합니다. [`dotnet sln add PrimeService/PrimeService.csproj`](../tools/dotnet-sln.md)를 실행하여 클래스 라이브러리 프로젝트를 솔루션에 추가합니다. 

## <a name="create-the-test-project"></a>테스트 프로젝트 만들기

다음으로 *PrimeService.Tests* 디렉터리를 만듭니다. 다음 개요에는 디렉터리 구조가 나와 있습니다.

```console
/unit-testing-using-mstest
    unit-testing-using-mstest.sln
    /PrimeService
        Source Files
        PrimeService.csproj
    /PrimeService.Tests
```

*PrimeService.Tests* 디렉터리를 현재 디렉터리로 만들고 [`dotnet new mstest`](../tools/dotnet-new.md)를 사용하여 새 프로젝트를 만듭니다. dotnet new 명령은 MSTest를 테스트 라이브러리로 사용하는 테스트 프로젝트를 만듭니다. 생성된 템플릿이 *PrimeServiceTests.csproj* 파일에 Test Runner를 구성했습니다.

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.3.0" />
  <PackageReference Include="MSTest.TestAdapter" Version="1.1.18" />
  <PackageReference Include="MSTest.TestFramework" Version="1.1.18" />
</ItemGroup>
```

테스트 프로제트는 다른 패키지에 단위 테스트를 만들고 실행하도록 요구합니다. 이전 단계의 `dotnet new`는 MSTest SDK, MSTest 테스트 프레임워크 및 MSTest Runner를 추가했습니다. 이제 `PrimeService` 클래스 라이브러리를 프로젝트에 다른 종속성으로 추가합니다. [`dotnet add reference`](../tools/dotnet-add-reference.md) 명령을 사용합니다.

```dotnetcli
dotnet add reference ../PrimeService/PrimeService.csproj
```

GitHub의 [샘플 리포지토리](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-mstest/PrimeService.Tests/PrimeService.Tests.csproj)에서 전체 파일을 볼 수 있습니다.

다음 개요에는 최종 솔루션 레이아웃이 나와 있습니다.

```console
/unit-testing-using-mstest
    unit-testing-using-mstest.sln
    /PrimeService
        Source Files
        PrimeService.csproj
    /PrimeService.Tests
        Test Source Files
        PrimeServiceTests.csproj
```

*unit-testing-using-mstest* 디렉터리에서 [`dotnet sln add .\PrimeService.Tests\PrimeService.Tests.csproj`](../tools/dotnet-sln.md)를 실행합니다. 

## <a name="create-the-first-test"></a>첫 번째 테스트 만들기

하나의 실패 테스트를 작성하고, 테스트가 성공하도록 만듭니다. 이 작업을 반복합니다. *PrimeService.Tests* 디렉터리에서 *UnitTest1.cs*를 제거하고 다음과 같은 내용으로 새 C# 파일 *PrimeService_IsPrimeShould.cs*를 만듭니다.

```csharp
using Microsoft.VisualStudio.TestTools.UnitTesting;
using Prime.Services;

namespace Prime.UnitTests.Services
{
    [TestClass]
    public class PrimeService_IsPrimeShould
    {
        private readonly PrimeService _primeService;

        public PrimeService_IsPrimeShould()
        {
            _primeService = new PrimeService();
        }

        [TestMethod]
        public void IsPrime_InputIs1_ReturnFalse()
        {
            var result = _primeService.IsPrime(1);

            Assert.IsFalse(result, "1 should not be prime");
        }
    }
}
```

[TestClass 특성](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute)은 단위 테스트가 포함된 클래스를 나타냅니다. [TestMethod 특성](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute)은 메서드가 테스트 메서드임을 나타냅니다. 

이 파일을 저장하고 [`dotnet test`](../tools/dotnet-test.md)를 실행하여 테스트 및 클래스 라이브러리를 빌드한 다음 테스트를 실행합니다. MSTest Test Runner에는 테스트를 실행할 프로그램 진입점이 포함되어 있습니다. `dotnet test`는 만든 단위 테스트 프로젝트를 사용하여 Test Runner를 시작합니다.

테스트가 실패합니다. 구현은 아직 만들지 않았습니다. `PrimeService` 클래스에서 작동하는 가장 간단한 코드를 작성하여 이 테스트를 통과시킵니다.

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

*unit-testing-using-mstest* 디렉터리에서 `dotnet test`를 다시 실행합니다. `dotnet test` 명령은 `PrimeService` 프로젝트에 대한 빌드를 실행한 다음 `PrimeService.Tests` 프로젝트에 대한 빌드를 실행합니다. 두 프로젝트를 모두 빌드한 후 이 단일 테스트를 실행합니다. 전달합니다.

## <a name="add-more-features"></a>더 많은 기능 추가

이제 하나의 테스트를 통과했으므로 더 작성할 수 있습니다. 소수에 대한 몇 가지 다른 간단한 사례가 있습니다 (0, -1). 새 테스트를 [TestMethod 특성](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute)과 함께 추가할 수도 있지만, 이렇게 하면 금방 지루해질 수 있습니다. 비슷한 테스트 모음을 작성하는 데 사용할 수 있는 다른 MSTest 특성이 있습니다.  [DataTestMethod 특성](xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataTestMethodAttribute)은 같은 코드를 실행하지만 다른 입력 인수가 있는 테스트 도구 모음을 나타냅니다. [DataRow 특성](xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataRowAttribute)을 사용하여 그러한 입력의 값을 지정할 수 있습니다.

새 테스트를 만드는 대신 이러한 두 특성을 적용하여 단일 데이터 기반 테스트를 만듭니다. 이 데이터 기반 테스트는 가장 작은 소수인 2보다 작은 몇 가지 값을 테스트하는 메서드입니다.

[!code-csharp[Sample_TestCode](../../../samples/core/getting-started/unit-testing-using-mstest/PrimeService.Tests/PrimeService_IsPrimeShould.cs?name=Sample_TestCode)]

`dotnet test`를 실행합니다. 그러면 이러한 테스트 중 2개가 실패합니다. 모든 테스트가 통과하도록 하려면 메서드의 시작 부분에서 `if` 절을 변경합니다.

```csharp
if (candidate < 2)
```

기본 라이브러리에서 더 많은 테스트, 더 많은 이론, 더 많은 코드를 추가하여 계속 반복합니다. [테스트의 완료된 버전](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-mstest/PrimeService.Tests/PrimeService_IsPrimeShould.cs) 및 [라이브러리의 완전한 구현](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-mstest/PrimeService/PrimeService.cs)을 얻게 됩니다.

작은 라이브러리 및 이 라이브러리에 대한 단위 테스트 집합을 작성했습니다. 새 패키지 및 테스트 추가가 정상 워크플로에 포함되도록 솔루션을 구조화했습니다. 애플리케이션의 목표를 해결하는 데 대부분의 시간과 노력을 들였습니다.

## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting>
- [단위 테스트에서 MSTest 프레임워크 사용](/visualstudio/test/using-microsoft-visualstudio-testtools-unittesting-members-in-unit-tests)
- [MSTest V2 테스트 프레임워크 문서](https://github.com/Microsoft/testfx-docs)
