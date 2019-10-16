---
title: C# 프로그램 구조 - C# 언어 둘러보기
description: C# 프로그램의 기본 구성 요소에 대해 알아보기
ms.date: 08/10/2016
ms.assetid: 984f0314-507f-47a0-af56-9011243f5e65
ms.openlocfilehash: 5102c72d68108f698a0456b9c14e6713778f4325
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834163"
---
# <a name="program-structure"></a>프로그램 구조

C#의 핵심적인 조직 개념은 ***프로그램***, ***네임스페이스***, ***형식***, ***멤버*** 및 ***어셈블리***입니다. C# 프로그램은 하나 이상의 소스 파일로 구성됩니다. 프로그램은 멤버를 포함하고 네임스페이스로 구성될 수 있는 형식을 선언합니다. 클래스와 인터페이스는 형식의 예입니다. 필드, 메서드, 속성 및 이벤트는 멤버의 예입니다. C# 프로그램을 컴파일하면 실제로 어셈블리로 패키지됩니다. 어셈블리는 일반적으로 ***애플리케이션***을 구현하는지 또는 ***라이브러리***를 구현하는지에 따라 각각 파일 확장명 `.exe` 또는 `.dll`을 갖습니다.

예제에서는 `Acme.Collections`라는 네임스페이스에서 `Stack`이라는 클래스를 선언합니다.

[!code-csharp[Stack](../../../samples/snippets/csharp/tour/program-structure/program.cs#L1-L34)]

이 클래스의 정규화된 이름은 `Acme.Collections.Stack`입니다. 클래스에는 필드 `top`, 2개의 메서드 `Push` 및 `Pop`, 중첩된 클래스 `Entry` 등의 여러 멤버가 포함됩니다. `Entry` 클래스는 필드 `next` 및 필드 `data`, 생성자의 세 멤버가 포함됩니다. 예제의 소스 코드가 파일 `acme.cs`에 포함된다고 가정할 경우 다음 명령줄은

```console
csc /t:library acme.cs
```

예제를 라이브러리(`Main` 진입점이 없는 코드)를 컴파일하고 `acme.dll`이라는 어셈블리를 생성합니다.

> [!IMPORTANT]
> 위 예제에서는 `csc`를 명령줄 C# 컴파일러로 사용합니다. 이 컴파일러는 Windows 실행 파일입니다. 다른 플랫폼에서도 C#을 사용하려면 .NET Core용 도구를 사용해야 합니다. .NET Core 에코시스템은 `dotnet` CLI를 사용하여 명령줄 빌드를 관리합니다. 여기에는 종속성 관리 및 C# 컴파일러 호출이 포함됩니다. .NET Core에서 지원되는 플랫폼의 이러한 도구에 대한 자세한 설명을 보려면 [이 자습서](../../core/tutorials/using-with-xplat-cli.md)를 참조하세요.

어셈블리에는 IL(중간 언어) 명령 형식의 실행 코드와 메타데이터 형식의 기호 정보가 포함됩니다. 실행되기 전에 어셈블리의 IL 코드는 .NET 공용 언어 런타임의 JIT(Just-In-Time) 컴파일러에 의해 자동으로 프로세서 특정 코드로 변환됩니다.

어셈블리는 코드와 메타데이터를 모두 포함하는 기능의 자체 설명 단위이므로 C#에 `#include` 지시문 및 헤더 파일이 필요하지 않습니다. 특정 어셈블리에 포함된 공용 형식 및 멤버는 프로그램을 컴파일할 때 해당 어셈블리를 참조하는 것만으로 C# 프로그램에서 사용 가능해집니다. 예를 들어 이 프로그램에서는 `acme.dll` 어셈블리의 `Acme.Collections.Stack` 클래스를 사용합니다.

[!code-csharp[UsingStack](../../../samples/snippets/csharp/tour/program-structure/Program.cs#L38-L52)]

프로그램이 파일 `example.cs`에 저장되는 경우 `example.cs`가 컴파일될 때 acme.dll 어셈블리가 컴파일러의 /r 옵션을 사용하여 참조될 수 있습니다.

```console
csc /r:acme.dll example.cs
```

이를 통해 실행 시 출력을 생성하는 `example.exe`라는 실행 가능한 어셈블리가 만들어집니다.

```console
100
10
1
```

C#은 프로그램의 소스 텍스트가 여러 소스 파일에 저장되도록 허용합니다. 다중 파일 C# 프로그램이 컴파일되면 모든 소스 파일이 함께 처리되고 소스 파일은 서로 자유롭게 참조될 수 있습니다. 개념적으로는 마치 모든 소스 파일이 처리되기 전에 하나의 큰 파일로 연결되는 것처럼 보입니다. 극소수의 경우를 제외하고 선언 순서는 중요하지 않으므로 C#에서는 정방향 선언이 절대 필요하지 않습니다. C#은 소스 파일을 하나의 공용 형식만 선언하도록 제한하거나 소스 파일 이름이 소스 파일에 선언된 형식과 일치하도록 요구하지 않습니다.

>[!div class="step-by-step"]
>[이전](index.md)
>[다음](types-and-variables.md)
