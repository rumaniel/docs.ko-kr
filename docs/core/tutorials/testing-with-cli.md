---
title: .NET Core 명령줄을 사용하여 프로젝트 구성 및 테스트
description: 이 자습서에서는 명령줄에서 .NET Core 프로젝트를 구성하고 테스트하는 방법을 설명합니다.
author: cartermp
ms.date: 09/10/2018
ms.custom: seodec18
ms.openlocfilehash: d93ba5f41f1e7b5818790d0853bd219466b317ee
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117374"
---
# <a name="organizing-and-testing-projects-with-the-net-core-command-line"></a>.NET Core 명령줄을 사용하여 프로젝트 구성 및 테스트

이 자습서에서는 [명령줄을 사용하여 Windows/Linux/macOS에서 .NET Core 시작](using-with-xplat-cli.md)에 따라 간단한 콘솔 앱 이상의 잘 구성된 고급 애플리케이션을 개발하는 과정을 안내합니다. 이 자습서에서는 폴더를 사용하여 코드를 구성하는 방법을 보여 준 후에 [xUnit](https://xunit.github.io/) 테스트 프레임워크를 사용하여 콘솔 애플리케이션을 확장하는 방법을 보여 줍니다.

## <a name="using-folders-to-organize-code"></a>폴더를 사용하여 코드 구성

콘솔 앱에 새 유형을 도입하려는 경우 유형이 포함된 파일을 앱에 추가하면 됩니다. 예를 들어 `AccountInformation` 및 `MonthlyReportRecords` 유형이 포함된 파일을 프로젝트에 추가하는 경우 프로젝트 파일 구조가 단순하며 쉽게 탐색할 수 있습니다.

```
/MyProject
|__AccountInformation.cs
|__MonthlyReportRecords.cs
|__MyProject.csproj
|__Program.cs
```

그러나 이 방법은 프로젝트의 크기가 비교적 작은 경우에만 효과적입니다. 프로젝트에 20개의 유형을 추가하면 어떻게 될지 상상이 되시나요? 프로젝트의 루트 디렉터리에 너무 많은 파일이 있으면 분명히 프로젝트 탐색과 유지 관리가 쉽지 않을 것입니다.

프로젝트를 구성하려면 유형 파일을 보관할 새 폴더를 만들고 이름을 *Models*로 지정합니다. *Models* 폴더에 유형 파일을 넣습니다.

```
/MyProject
|__/Models
   |__AccountInformation.cs
   |__MonthlyReportRecords.cs
|__MyProject.csproj
|__Program.cs
```

논리적으로 파일을 폴더로 그룹화하는 프로젝트는 탐색과 유지 관리가 용이합니다. 다음 섹션에서는 폴더 및 유닛 테스트를 사용하여 좀 더 복잡한 샘플을 만듭니다.

## <a name="organizing-and-testing-using-the-newtypes-pets-sample"></a>NewTypes Pets 샘플을 사용하여 구성 및 테스트

### <a name="building-the-sample"></a>샘플 빌드

다음 단계를 위해 [NewTypes Pets 샘플](https://github.com/dotnet/samples/tree/master/core/console-apps/NewTypesMsBuild)을 사용할 수도 있고, 고유한 파일과 폴더를 만들 수도 있습니다. 나중에 더 많은 유형을 추가할 수 있는 폴더 구조로 유형이 논리적으로 구성되며, 테스트도 나중에 더 많은 테스트를 추가할 수 있는 폴더에 논리적으로 배치됩니다.

샘플에는 두 유형 `Dog` 및 `Cat`이 포함되어 있으며, 두 유형이 공용 인터페이스 `IPet`을 구현하도록 합니다. `NewTypes` 프로젝트의 목표는 애완 동물 관련 유형을 *Pets* 폴더로 구성하는 것입니다. 나중에 *WildAnimals*등의 다른 유형 집합을 추가하면 *Pets* 폴더와 함께 *NewTypes* 폴더에 배치됩니다. *WildAnimals* 폴더에는 애완 동물이 아닌 동물 유형(예: `Squirrel` 및 `Rabbit`)이 포함될 수 있습니다. 이렇게 하면 유형을 추가해도 프로젝트의 체계적인 구성이 유지됩니다.

표시된 파일 내용으로 다음 폴더 구조를 만듭니다.

```
/NewTypes
|__/src
   |__/NewTypes
      |__/Pets
         |__Dog.cs
         |__Cat.cs
         |__IPet.cs
      |__Program.cs
      |__NewTypes.csproj
```

*IPet.cs*:

[!code-csharp[IPet interface](../../../samples/core/console-apps/NewTypesMsBuild/src/NewTypes/Pets/IPet.cs)]

*Dog.cs*:

[!code-csharp[Dog class](../../../samples/core/console-apps/NewTypesMsBuild/src/NewTypes/Pets/Dog.cs)]

*Cat.cs*:

[!code-csharp[Cat class](../../../samples/core/console-apps/NewTypesMsBuild/src/NewTypes/Pets/Cat.cs)]

*Program.cs*:

[!code-csharp[Main](../../../samples/core/console-apps/NewTypesMsBuild/src/NewTypes/Program.cs)]

*NewTypes.csproj*:

[!code-xml[NewTypes csproj](../../../samples/core/console-apps/NewTypesMsBuild/src/NewTypes/NewTypes.csproj)]

다음 명령을 실행합니다.

```dotnetcli
dotnet run
```

다음 출력이 표시됩니다.

```console
Woof!
Meow!
```

연습(옵션): 이 프로젝트를 확장하여 `Bird` 등의 새로운 애완 동물 유형을 추가할 수 있습니다. 새의 `TalkToOwner` 메서드를 통해 소유자에게 `Tweet!`을 제공합니다. 앱을 다시 실행합니다. 출력에 `Tweet!`이 포함됩니다.

### <a name="testing-the-sample"></a>샘플 테스트

`NewTypes` 프로젝트가 구현되었으며, 애완 동물 관련 유형을 폴더에 보관하여 구성했습니다. 다음으로, 테스트 프로젝트를 만들고 [xUnit](https://xunit.github.io/) 테스트 프레임워크를 사용하여 테스트 작성을 시작합니다. 유닛 테스트를 사용하면 애완동물 유형의 동작을 자동으로 검사하여 제대로 작동하는지 확인할 수 있습니다.

*src* 폴더를 다시 탐색하고 *test* 폴더를 만들며, 이 폴더 안에 *NewTypesTests* 폴더를 만듭니다. *NewTypesTests* 폴더의 명령 프롬프트에서 `dotnet new xunit`를 실행합니다. 이로 인해 *NewTypesTests.csproj* 및 *UnitTest1.cs*라는 두 파일이 생성됩니다.

테스트 프로젝트는 현재 `NewTypes`의 형식을 테스트할 수 없으며, `NewTypes` 프로젝트에 대한 프로젝트 참조가 필요합니다. 프로젝트 참조를 추가하려면 [`dotnet add reference`](../tools/dotnet-add-reference.md) 명령을 사용합니다.

```dotnetcli
dotnet add reference ../../src/NewTypes/NewTypes.csproj
```

또는 *NewTypesTests.csproj* 파일에 `<ItemGroup>` 노드를 추가하여 수동으로 프로젝트 참조를 추가할 수도 있습니다.

```xml
<ItemGroup>
  <ProjectReference Include="../../src/NewTypes/NewTypes.csproj" />
</ItemGroup>
```

*NewTypesTests.csproj*:

[!code-xml[NewTypesTests csproj](../../../samples/core/console-apps/NewTypesMsBuild/test/NewTypesTests/NewTypesTests.csproj)]

*NewTypesTests.csproj* 파일에는 다음이 포함되어 있습니다.

* .NET 테스트 인프라인 `Microsoft.NET.Test.Sdk`에 대한 패키지 참조
* xUnit 테스트 프레임워크인 `xunit`에 대한 패키지 참조
* 테스트 실행기인 `xunit.runner.visualstudio`에 대한 패키지 참조
* 테스트할 코드인 `NewTypes`에 대한 프로젝트 참조

*UnitTest1.cs*의 이름을 *PetTests.cs*로 변경하고 파일의 코드를 다음 코드로 바꿉니다.

```csharp
using System;
using Xunit;
using Pets;

public class PetTests
{
    [Fact]
    public void DogTalkToOwnerReturnsWoof()
    {
        string expected = "Woof!";
        string actual = new Dog().TalkToOwner();

        Assert.NotEqual(expected, actual);
    }

    [Fact]
    public void CatTalkToOwnerReturnsMeow()
    {
        string expected = "Meow!";
        string actual = new Cat().TalkToOwner();

        Assert.NotEqual(expected, actual);
    }
}
```

연습(옵션): 소유자에 대한 `Tweet!`을 생성하는 `Bird` 유형을 이전에 추가한 경우 *PetTests.cs* 파일에 테스트 메서드 `BirdTalkToOwnerReturnsTweet`을 추가하여 `TalkToOwner` 메서드가 `Bird` 유형에 대해 제대로 작동하는지 확인합니다.

> [!NOTE]
> `expected` 및 `actual` 값이 같다고 예상하는 경우에도 `Assert.NotEqual` 검사를 사용한 초기 어설션에서는 이러한 값이 *같지 않다*고 지정합니다. 테스트 논리를 검사하기 위해 항상 먼저 실패할 테스트를 만듭니다. 테스트가 실패했음을 확인한 후 테스트를 통과할 수 있도록 어설션을 조정합니다.

전체 프로젝트 구조는 다음과 같습니다.

```
/NewTypes
|__/src
   |__/NewTypes
      |__/Pets
         |__Dog.cs
         |__Cat.cs
         |__IPet.cs
      |__Program.cs
      |__NewTypes.csproj
|__/test
   |__NewTypesTests
      |__PetTests.cs
      |__NewTypesTests.csproj
```

*test/NewTypesTests* 디렉터리에서 시작합니다. [`dotnet restore`](../tools/dotnet-restore.md) 명령을 사용하여 테스트 프로젝트를 복원합니다. [`dotnet test`](../tools/dotnet-test.md) 명령을 사용하여 테스트를 실행합니다. 이 명령은 프로젝트 파일에 지정된 Test Runner를 시작합니다.

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

예상대로 테스트에 실패하고, 콘솔에 다음 출력이 표시됩니다.

```output
Test run for c:\Users\ronpet\repos\samples\core\console-apps\NewTypesMsBuild\test\NewTypesTests\bin\Debug\netcoreapp2.1\NewTypesTests.dll(.NETCoreApp,Version=v2.1)
Microsoft (R) Test Execution Command Line Tool Version 15.8.0
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...
[xUnit.net 00:00:00.77]     PetTests.DogTalkToOwnerReturnsWoof [FAIL]
[xUnit.net 00:00:00.78]     PetTests.CatTalkToOwnerReturnsMeow [FAIL]
Failed   PetTests.DogTalkToOwnerReturnsWoof
Error Message:
 Assert.NotEqual() Failure
Expected: Not "Woof!"
Actual:   "Woof!"
Stack Trace:
   at PetTests.DogTalkToOwnerReturnsWoof() in c:\Users\ronpet\repos\samples\core\console-apps\NewTypesMsBuild\test\NewTypesTests\PetTests.cs:line 13
Failed   PetTests.CatTalkToOwnerReturnsMeow
Error Message:
 Assert.NotEqual() Failure
Expected: Not "Meow!"
Actual:   "Meow!"
Stack Trace:
   at PetTests.CatTalkToOwnerReturnsMeow() in c:\Users\ronpet\repos\samples\core\console-apps\NewTypesMsBuild\test\NewTypesTests\PetTests.cs:line 22

Total tests: 2. Passed: 0. Failed: 2. Skipped: 0.
Test Run Failed.
Test execution time: 1.7000 Seconds
```

테스트 어설션을 `Assert.NotEqual`에서 `Assert.Equal`로 변경합니다.

[!code-csharp[PetTests class](../../../samples/core/console-apps/NewTypesMsBuild/test/NewTypesTests/PetTests.cs)]

`dotnet test` 명령을 사용하여 테스트를 다시 실행하면 다음 출력이 표시됩니다.

```output
Test run for c:\Users\ronpet\repos\samples\core\console-apps\NewTypesMsBuild\test\NewTypesTests\bin\Debug\netcoreapp2.1\NewTypesTests.dll(.NETCoreApp,Version=v2.1)
Microsoft (R) Test Execution Command Line Tool Version 15.8.0
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...

Total tests: 2. Passed: 2. Failed: 0. Skipped: 0.
Test Run Successful.
Test execution time: 1.6029 Seconds
```

테스트를 통과합니다. 애완 동물 유형의 메서드가 소유자에게 설명할 때 올바른 값을 반환합니다.

xUnit를 사용하여 프로젝트를 구성 및 테스트하는 기술을 배웠습니다. 이러한 기술을 활용하여 사용자 고유의 프로젝트에 적용해 보세요. *즐거운 코딩을 경험하시기 바랍니다!*
