---
title: .NET 둘러보기
description: .NET의 몇 가지 주요 기능에 대한 둘러보기입니다.
author: cartermp
ms.author: wiwagn
ms.date: 05/22/2017
ms.technology: dotnet-standard
ms.assetid: bbfe6465-329d-4982-869d-472e7ef85d93
ms.openlocfilehash: a83253e37d3afde9ed8266ec1195c9726f6462cc
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291599"
---
# <a name="tour-of-net"></a>.NET 둘러보기

.NET은 범용 개발 플랫폼입니다. 여러 플랫폼에서 다양한 시나리오가 가능하게 하는 다양한 프로그래밍 언어 지원, 비동기 및 동시 실행 프로그래밍 모델 및 기본 상호 운용성과 같은 여러 중요한 특징이 있습니다.

이 문서에서는 .NET의 몇 가지 주요 기능을 살펴볼 수 있습니다. .NET의 구조와 사용 목적은 [.NET 아키텍처 구성 요소](components.md) 항목을 참조하세요.

## <a name="how-to-run-the-code-samples"></a>코드 샘플을 실행하는 방법

코드 샘플을 실행하기 위한 개발 환경 설정 방법은 [시작](get-started.md) 항목을 참조하세요. 이 페이지의 코드 샘플을 복사하여 샘플을 실행할 환경에 붙여넣으세요. 

## <a name="programming-languages"></a>프로그래밍 언어

.NET은 여러 프로그래밍 언어를 지원합니다. .NET 구현은 무엇보다 언어와 관련이 없는 런타임과 언어 상호 운용성을 지정하는 [CLI(공용 언어 인프라)](https://visualstudio.microsoft.com/license-terms/ecma-c-common-language-infrastructure-standards/)를 구현합니다. 즉 어떤 .NET 언어를 선택해도 .NET에서 앱과 서비스를 빌드할 수 있습니다.

Microsoft에서는 C#과 F#, VB(Visual Basic) 이 세 가지 .NET 언어를 적극적으로 개발하고 지원합니다. 

* C#은 C 스타일 언어의 표현력과 우아함은 그대로 유지하면서 간단하고 형식이 안전한 개체 지향 언어입니다. C나 이와 비슷한 언어에 익숙한 사용자라면 누구나 거의 문제 없이 C#을 사용할 수 있을 것입니다. C#에 대한 자세한 내용은 [C# 가이드](../csharp/index.md)를 참조하세요.

* F#은 일반적인 개체 지향 프로그래밍과 명령형 프로그래밍을 지원하며 다양한 플랫폼에서 사용할 수 있는 함수 우선 프로그래밍 언어입니다. F#에 대한 자세한 내용을 보려면 [F# 가이드](../fsharp/index.md)를 참조하세요.

* Visual Basic은 .NET에서 실행되는 다양한 앱을 만들 수 있는 배우기 쉬운 언어입니다. .NET 언어 중에서 VB 구문이 일반적인 인간 언어와 가장 유사하여 소프트웨어를 처음 개발하는 사람도 쉽게 배울 수 있습니다.

## <a name="automatic-memory-management"></a>자동 메모리 관리

.NET에서는 [GC(가비지 수집)](garbagecollection/index.md)를 사용하여 프로그램의 메모리를 자동으로 관리합니다. GC는 메모리 관리를 지연하는 방식으로 작동하며 메모리를 즉각적으로 수집하기보다는 앱의 처리량을 우선합니다. .NET GC의 자세한 내용은 [GC(가비지 수집) 기본 사항](garbagecollection/fundamentals.md)을 확인하세요.

다음 두 줄에서는 모두 메모리를 할당합니다.

[!code-csharp[MemoryManagement](../../samples/csharp/snippets/tour/MemoryManagement.csx#L1-L2)]

할당 취소는 가비지 수집기의 예약 실행을 통해 메모리를 회수할 때 자동으로 수행되기 때문에 메모리 할당을 취소하는 유사 키워드는 없습니다.

가비지 수집기는 *메모리 안전성*을 보장해주는 서비스 중 하나입니다. 프로그램이 할당된 메모리만 액세스하면 메모리가 안전합니다. 예를 들어 런타임은 앱이 배열의 범위를 넘어 할당되지 않은 메모리를 액세스하지 못하도록 합니다.

다음 예제에서 런타임은 `InvalidIndexException` 예외를 throw하여 메모리 안전성을 강화합니다.

[!code-csharp[MemoryManagement](../../samples/csharp/snippets/tour/MemoryManagement.csx#L4-L5)]

## <a name="working-with-unmanaged-resources"></a>관리되지 않는 리소스로 작업하기

일부 개체는 *관리되지 않는 리소스*를 참조합니다. 관리되지 않는 리소스는 .NET 런타임에서 자동 유지 관리되지 않는 리소스입니다. 예를 들어, 파일 핸들은 관리되지 않는 리소스입니다. <xref:System.IO.FileStream> 개체는 관리되는 개체이지만, 관리되지 않는 파일 핸들을 참조합니다. <xref:System.IO.FileStream> 사용을 마치면 파일 핸들을 릴리스해야 합니다.

.NET에서는 관리되지 않는 리소스를 참조하는 개체가 <xref:System.IDisposable> 인터페이스를 구현합니다. 개체 사용을 마치면 관리되지 않는 모든 리소스 릴리스를 담당하는 개체의 <xref:System.IDisposable.Dispose> 메서드를 호출합니다. 다음 예제와 같이 .NET 언어는 이러한 개체에 대해 편리한 [`using` 문](../csharp/language-reference/keywords/using.md)을 제공합니다.

[!code-csharp[UnmanagedResources](../../samples/csharp/snippets/tour/UnmanagedResources.csx#L1-L6)]

`using` 블록이 완료되면 .NET 런타임은 파일 핸들을 릴리스하는 `stream` 개체의 <xref:System.IDisposable.Dispose> 메서드를 자동으로 호출합니다. 예외로 인해 블록에 대한 제어가 없어지는 경우에도 런타임은 같은 방식으로 호출합니다.

자세한 내용은 다음 항목을 참조하세요.

* C#의 경우 [using 문(C# 참조)](../csharp/language-reference/keywords/using-statement.md) 항목을 참조하세요.
* F#의 경우 [리소스 관리: use 키워드](../fsharp/language-reference/resource-management-the-use-keyword.md)를 참조하세요.
* VB의 경우 [Using 문(Visual Basic)](../visual-basic/language-reference/statements/using-statement.md) 항목을 참조하세요.

## <a name="type-safety"></a>형식 안전성

개체는 특정 형식의 인스턴스입니다. 지정된 개체에 허용되는 유일한 작업은 해당 형식의 작업입니다. `Dog` 형식에는 `Jump` 및 `WagTail` 메서드가 있을 수 있지만 `SumTotal` 메서드는 없습니다. 프로그램은 지정된 형식에 속하는 메서드만 호출합니다. 다른 모든 호출에서는 컴파일 시간 오류 또는 런타임 예외가 발생합니다(동적 기능 또는 `object`를 사용하는 경우).

.NET 언어는 기본 및 파생 클래스의 계층 구조로 이루어진 개체 지향 언어입니다. .NET 런타임에서는 개체 계층 구조에 맞는 개체 캐스트 및 호출만 허용됩니다. .NET 언어에서 정의된 모든 형식은 기본 <xref:System.Object> 형식에서 파생됩니다.

[!code-csharp[TypeSafety](../../samples/csharp/snippets/tour/TypeSafety.csx#L19-L23)]

또한 형식 안전성은 접근자 키워드의 충실도를 보장하여 캡슐화 적용을 지원하는 데 사용됩니다. 접근자 키워드는 다른 코드에서 지정된 형식의 멤버에 대한 액세스를 제어하는 아티팩트입니다. 일반적으로 형식 내에서 해당 동작을 관리하는 데 사용하는 다양한 종류의 데이터에 사용됩니다.

[!code-csharp[TypeSafety](../../samples/csharp/snippets/tour/TypeSafety.csx#L3-L3)]

C#, VB 및 F#은 지역 *형식 유추*를 지원합니다. 형식 유추는 컴파일러가 오른쪽에 있는 식에서 왼쪽에 있는 식의 형식을 유추함을 의미합니다. 형식 안전성이 손상되거나 무시되는 것은 아닙니다. 결과 형식은 강력한 형식이며 수반되는 모든 특성을 포함합니다. 이전 예제에서 `dog`는 형식 유추를 도입하도록 다시 작성하고 나머지는 변경하지 않습니다.

[!code-csharp[TypeSafety](../../samples/csharp/snippets/tour/TypeSafety.csx#L28-L34)]

F#에는 C# 및 VB에 있는 메서드-지역 형식 유추보다 더 심화된 형식 유추 기능이 있습니다. 자세한 내용은 [형식 유추](../fsharp/language-reference/type-inference.md)를 참조하세요.

## <a name="delegates-and-lambdas"></a>대리자 및 람다 식

대리자는 메서드 시그니처로 표시됩니다. 해당 시그니처가 있는 모든 메서드는 대리자에 할당할 수 있으며 대리자가 호출될 때 실행됩니다.

대리자는 형식이 안전하다는 점을 제외하면 C++ 함수 포인터와 유사합니다. 대리자는 CLR 형식 시스템 내에서 일종의 연결이 끊긴 메서드입니다. 일반 메서드는 클래스에 연결되고 정적 또는 인스턴스 호출 규칙을 통해서만 직접 호출할 수 있습니다.

.NET에서 대리자는 이벤트 처리기에서, 비동기 작업을 정의할 때, LINQ의 토대인 람다 식에서 일반적으로 사용됩니다. 자세한 내용은 [대리자 및 람다 식](delegates-lambdas.md) 항목을 참조하세요.

## <a name="generics"></a>제네릭

제네릭은 프로그래머가 해당 클래스를 디자인할 때 *형식 매개 변수*를 도입할 수 있게 합니다. 이렇게 하면 클라이언트 코드(형식의 사용자)에서 형식 매개 변수 대신 사용할 형식을 정확하게 지정할 수 있습니다.

제네릭은 프로그래머가 제네릭 데이터 구조를 구현할 수 있도록 돕기 위해 추가되었습니다. 제네릭이 도입되기 전에는 `List` 같은 형식을 제네릭으로 만들기 위해 `object` 형식인 요소로 작업해야 했습니다. 따라서 미묘한 런타임 오류와 함께 다양한 성능 및 의미 체계 문제가 발생했습니다. 후자의 경우 가장 심각한 문제는 예를 들어 데이터 구조에 정수와 문자열이 둘 다 포함되어 있을 때 목록의 멤버로 작업하면 `InvalidCastException`이 throw되는 것입니다.

다음 샘플에서는 <xref:System.Collections.Generic.List%601> 형식 인스턴스를 사용하여 실행 중인 기본 프로그램을 보여 줍니다.

[!code-csharp[GenericsShort](../../samples/csharp/snippets/tour/GenericsShort.csx)]

자세한 내용은 [제네릭 형식(제네릭) 개요](generics.md) 항목을 참조하세요.

## <a name="async-programming"></a>비동기 프로그래밍

비동기 프로그래밍은 런타임, 프레임워크 라이브러리 및 .NET 언어 구문의 비동기 지원을 포함하는 .NET 내의 최고급 개념입니다. 내부적으로 운영 체제를 활용하여 I/O 바인딩된 작업을 최대한 효율적으로 수행하는 개체(예: `Task`)를 기반으로 합니다.

.NET의 비동기 프로그래밍에 대해 자세히 알아보려면 [비동기 개요](async.md) 항목부터 살펴보세요.

## <a name="language-integrated-query-linq"></a>LINQ(Language-Integrated Query)

LINQ는 데이터에 적용할 간단하고 선언적인 코드를 작성할 수 있게 해주는 C# 및 VB에 대한 강력한 기능 집합입니다. 데이터는 다양한 형식(예: 메모리 내 개체, SQL 데이터베이스 또는 XML 문서)일 수 있지만 작성하는 LINQ 코드는 일반적으로 각 데이터 소스마다 다르게 표시되지 않습니다.

자세히 알아보고 몇 가지 샘플을 확인하려면 [LINQ(Language-Integrated Query)](using-linq.md) 항목을 참조하세요.

## <a name="native-interoperability"></a>기본 상호 운용성

모든 운영 체제에는 시스템 서비스를 제공하는 API(애플리케이션 프로그래밍 인터페이스)가 있습니다. .NET은 이러한 API를 호출하는 여러 가지 방법을 제공합니다.

기본 상호 운용성은 대체로 “플랫폼 호출” 또는 줄여서 P/Invoke를 통해 수행되며, Linux 및 Windows 플랫폼에서 지원됩니다. 기본 상호 운용성을 수행하는 Windows 전용 방법은 “COM interop”라고 하며, 관리 코드에서 [COM 구성 요소](/cpp/atl/introduction-to-com)로 작업하는 데 사용됩니다. 이 방법은 P/Invoke 인프라를 기반으로 하지만 약간 다른 방식으로 작동합니다.

Java 및 Objective-C에 대한 Mono(및 Xamarin)의 상호 운용성 지원은 대부분 비슷하게 작성되었습니다. 즉, 동일한 원칙을 사용합니다.

기본 상호 운용성에 대한 자세한 내용은 [기본 상호 운용성](native-interop/index.md) 문서를 참조하세요.

## <a name="unsafe-code"></a>안전하지 않은 코드

언어 지원에 따라 CLR에서는 기본 메모리에 액세스하고 `unsafe` 코드를 통해 포인터 연산을 수행할 수 있습니다. 이러한 작업은 특정 알고리즘 및 시스템 상호 운용성에 필요합니다. 강력하기는 하지만, 시스템 API와의 상호 운용하거나 가장 효율적인 알고리즘을 구현하는 데 필요한 경우가 아니면 안전하지 않은 코드는 사용하지 않는 것이 좋습니다. 안전하지 않은 코드는 환경에 따라 다르게 실행될 수도 있고 가비지 수집기 및 형식 안전성의 이점을 잃을 수도 있습니다. 안전하지 않은 코드를 최대한 제한 및 중앙 집중화하고 해당 코드를 철저히 테스트하는 것이 좋습니다.

다음 예제에서는 `StringBuilder` 클래스에서 `ToString()` 메서드의 수정된 버전입니다. `unsafe` 코드를 통해 메모리 청크를 직접 이동하여 알고리즘을 효율적으로 구현할 수 있는 방법을 보여 줍니다.

[!code-csharp[Unsafe](../../samples/csharp/snippets/tour/Unsafe.csx)]

## <a name="next-steps"></a>다음 단계

C# 기능을 살펴보고 싶은 경우 [C# 둘러보기](../csharp/tour-of-csharp/index.md)를 확인하세요.

F# 기능을 살펴보고 싶은 경우 [F# 둘러보기](../fsharp/tour.md)를 참조하세요.

사용자가 직접 코드 작성을 시작하려는 경우에는 [시작](get-started.md)을 방문하세요.

.NET의 중요한 구성 요소에 대해 알아보려면 [.NET 아키텍처 구성 요소](components.md)를 확인하세요.
