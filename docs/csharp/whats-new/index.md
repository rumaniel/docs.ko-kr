---
title: C#의 새로운 기능 - C# 가이드
description: C# 언어 진화 과정
ms.date: 11/13/2017
ms.assetid: 77deec51-a14d-46d4-9bb3-faf449477149
ms.openlocfilehash: b079c21ee90a797b038b96ae68123a538464c382
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50201441"
---
# <a name="whats-new-in-c"></a>C#의 새로운 기능 #

이 페이지는 C# 언어의 각 주요 릴리스에서 새로운 기능에 대해 설명합니다. 링크된 문서에서는 각 릴리스에 추가된 주요 기능을 자세히 설명합니다. 출시되거나 공개 미리 보기 상태의 릴리스된 새 기능 관련 정보를 확인할 수 있습니다. 예정된 릴리스에서 고려되는 기능을 비롯한 자세한 언어 기능 상태는 GitHub의 [dotnet/roslyn 리포지토리에서](https://github.com/dotnet/roslyn/blob/master/docs/Language%20Feature%20Status.md) 확인할 수 있습니다.

> [!IMPORTANT]
> C# 언어는 일부 기능의 경우 *표준 라이브러리*의 형식 및 메서드를 사용합니다. 한 가지 예는 예외 처리입니다. 모든 `throw` 문 또는 식은 throw된 개체가 <xref:System.Exception>에서 파생되는지 확인합니다. 마찬가지로 모든 `catch`는 발견되는 형식이 <xref:System.Exception>에서 파생되는지 확인합니다. 각 버전은 새 요구 사항을 추가할 수 있습니다. 이전 환경에서 최신 언어 기능을 사용하려면 특정 라이브러리를 설치해야 합니다. 이러한 종속성은 각 특정 버전에 대한 페이지에서 설명합니다. 이 종속성의 배경은 [언어 및 라이브러리 간 관계](relationships-between-language-and-library.md)에서 자세히 알아볼 수 있습니다. 

포인트 릴리스에서 최신 기능을 사용하려면 [컴파일러 언어 버전을 구성](../language-reference/configure-language-version.md)하고 해당 버전을 선택해야 합니다.

* [C# 7.3](csharp-7-3.md):
  - 이 페이지에서는 C# 언어의 최신 기능을 설명합니다. C# 7.3은 현재 [Visual Studio 2017 버전 15.7](https://visualstudio.microsoft.com/vs/whatsnew/) 및 [.NET Core 2.1 SDK 2.1.300 RC1](../../core/whats-new/index.md)에서 사용 가능합니다.
* [C# 7.2](csharp-7-2.md):
  - 이 페이지에서는 C# 언어에 추가된 기능을 설명합니다. C# 7.2는 현재 [Visual Studio 2017 버전 15.5](https://visualstudio.microsoft.com/vs/whatsnew/) 및 [.NET Core 2.0 SDK](../../core/whats-new/index.md)에서 사용 가능합니다.
* [C# 7.1](csharp-7-1.md):
  - 이 페이지에서는 C# 7.1에 추가된 기능을 설명합니다. 이러한 기능은 [Visual Studio 2017 버전 15.3](https://visualstudio.microsoft.com/vs/whatsnew/) 및 [.NET Core 2.0 SDK](../../core/whats-new/index.md)에 추가되었습니다.
* [C# 7.0](csharp-7.md):
  - 이 페이지에서는 C# 7.0에 추가된 기능을 설명합니다. 이러한 기능은 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/whatsnew/) 및 [.NET Core 1.0](../../core/whats-new/index.md) 이상에 추가되었습니다.
* [C# 6](csharp-6.md):
  - 이 페이지에서는 C# 6에 추가된 기능을 설명합니다. 이러한 기능은 Windows 개발자를 위한 Visual Studio 2015와 macOS 및 Linux에서 C#을 사용하는 개발자를 위한 .NET Core 1.0에서 사용할 수 있습니다.
* [플랫폼 간 지원](../../core/index.md):
  - C#은 .NET Core 지원을 통해 여러 플랫폼에서 실행됩니다. macOS 또는 지원되는 여러 Linux 배포판 중 하나에서 C#을 사용해보고 싶다면 .NET Core에 관해 알아보세요.
* [.NET 컴파일러 플랫폼 SDK](../roslyn-sdk/index.md):
  - .NET 컴파일러 플랫폼 SDK를 사용하면 C# 코드에서 정적 분석을 수행하는 코드를 작성할 수 있습니다. 이러한 API를 사용하여 잠재적인 오류나 잘못된 사례를 찾고, 수정 사항을 제안하거나 구현할 수 있습니다.

## <a name="previous-versions"></a>이전 버전

다음은 이전 버전의 C# 언어와 Visual Studio .NET에 추가된 주요 기능입니다.

* Visual Studio .NET 2013:
  - 이 버전의 Visual Studio에는 버그 수정, 성능 향상 및 [.NET Compiler Platform SDK](../roslyn-sdk/index.md)로 발전한 .NET Compiler Platform("Roslyn")의 기술 미리 보기가 포함되었습니다.
* C# 5, Visual Studio .NET 2012:
  - `Async` / `await` 및 [호출자 정보](../programming-guide/concepts/caller-information.md) 특성.
* C# 4, Visual Studio .NET 2010:
  - `Dynamic`, [명명된 인수](../programming-guide/classes-and-structs/named-and-optional-arguments.md), 선택적 매개 변수, 제네릭 [공변성(Covariance) 및 반공변성(Contravariance)](../programming-guide/concepts/covariance-contravariance/index.md).
* C# 3, Visual Studio .NET 2008:
  - 개체 및 컬렉션 이니셜라이저, 람다 식, 확장 메서드, 익명 형식, 자동 속성, 로컬 `var` 형식 유추 및 [LINQ(Language Integrated Query)](../programming-guide/concepts/linq/index.md).
* C# 2, Visual Studio .NET 2005:
  - 무명 메서드, 제네릭, nullable 형식, 반복기/yield, `static` 클래스, 대리자의 공변성(Covariance) 및 반공변성(Contravariance).
* C# 1.1, Visual Studio .NET 2003:
  - `#line` pragma 및 xml 문서 주석.
* C# 1, Visual Studio .NET 2002:
  - [C#](../csharp.md)의 첫 번째 릴리스.
