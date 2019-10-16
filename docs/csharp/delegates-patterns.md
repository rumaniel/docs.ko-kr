---
title: 대리자에 대한 일반적인 패턴
description: 코드에서 대리자를 사용하여 구성 요소 간의 강력한 결합을 방지하기 위한 일반적인 패턴에 대해 알아봅니다.
ms.date: 06/20/2016
ms.assetid: 0ff8fdfd-6a11-4327-b061-0f2526f35b43
ms.openlocfilehash: ea0e0b7af361b76c4b46b0a180e07b44c1fa07e1
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59095700"
---
# <a name="common-patterns-for-delegates"></a>대리자에 대한 일반적인 패턴

[이전](delegates-strongly-typed.md)

대리자는 구성 요소 간 결합이 최소화된 소프트웨어 디자인을 사용하는 메커니즘을 제공합니다.

이러한 디자인의 가장 좋은 예는 LINQ입니다. LINQ 쿼리 식 패턴은 모든 기능에 대리자를 사용합니다. 간단한 다음 예제를 살펴보세요.

```csharp
var smallNumbers = numbers.Where(n => n < 10);
```

이 예제에서는 숫자 시퀀스를 값 10보다 작은 숫자로만 필터링합니다.
`Where` 메서드는 필터를 통과하는 시퀀스의 요소를 결정하는 대리자를 사용합니다. LINQ 쿼리를 만들 때 이러한 특정 용도를 위해 대리자의 구현을 제공합니다.

Where 메서드의 프로토타입은 다음과 같습니다.

```csharp
public static IEnumerable<TSource> Where<TSource> (this IEnumerable<TSource> source, Func<TSource, bool> predicate);
```

이 예제에서는 LINQ의 일부인 모든 메서드가 반복됩니다. 이러한 메서드는 모두 특정 쿼리를 관리하는 코드에 대해 대리자를 사용합니다. 이 API 디자인 패턴은 매우 간단하게 배우고 이해할 수 있습니다.

이 간단한 예제에서는 어떻게 대리자에 구성 요소 간 결합이 거의 필요하지 않은지를 보여 줍니다. 특정 기본 클래스에서 파생되는 클래스를 만들 필요가 없습니다. 특정 인터페이스를 구현하지 않아도 됩니다.
현재 작업에 기본적으로 필요한 하나의 메서드만 구현하면 됩니다.

## <a name="building-your-own-components-with-delegates"></a>대리자를 사용하여 고유한 구성 요소 빌드

대리자를 사용하는 디자인으로 구성 요소를 만들어 해당 예제에서 빌드해 보겠습니다.

큰 시스템의 로그 메시지에 사용할 수 있는 구성 요소를 정의해 보겠습니다. 라이브러리 구성 요소는 여러 가지 다른 플랫폼의 다양한 환경에서 사용할 수 있습니다. 로그를 관리하는 구성 요소에는 공통된 기능이 많이 있습니다. 시스템의 모든 구성 요소에서 전달된 메시지를 수락해야 합니다. 이러한 메시지는 핵심 구성 요소에서 관리할 수 있는 우선 순위가 다릅니다. 메시지는 최종 보관된 양식에 타임스탬프가 있어야 합니다. 고급 시나리오의 경우 소스 구성 요소에 따라 메시지를 필터링할 수 있습니다.

메시지가 기록되는 위치와 같이 자주 변경되는 기능이 있습니다. 일부 환경에서는 메시지가 오류 콘솔에 기록되고, 다른 환경에서는 파일에 기록될 수 있습니다. 데이터베이스 스토리지, OS 이벤트 로그, 기타 문서 스토리지 등에 기록될 수도 있습니다.

또한 다양한 시나리오에서 사용될 수 있는 출력의 조합이 있습니다. 메시지를 콘솔 및 파일에 기록하려고 할 수 있습니다.

대리자 기반 디자인은 뛰어난 유연성을 제공하며 나중에 추가할 수 있는 스토리지 메커니즘을 지원하기가 쉽습니다.

이 디자인에서 기본 로그 구성 요소는 비가상이며 sealed 클래스일 수도 있습니다. 모든 대리자 집합을 연결하여 다양한 스토리지 미디어에 메시지를 기록할 수 있습니다. 멀티캐스트 대리자에 대한 기본 제공 지원을 통해 메시지가 여러 위치(파일 및 콘솔)에 기록되어야 하는 시나리오를 쉽게 지원할 수 있습니다.

## <a name="a-first-implementation"></a>첫 번째 구현

작은 규모로 시작해 보겠습니다. 초기 구현에서는 새 메시지를 수락하고 연결된 대리자를 사용하여 메시지를 기록합니다. 메시지를 콘솔에 기록하는 대리자에서 시작할 수 있습니다.

[!code-csharp[LoggerImplementation](../../samples/csharp/delegates-and-events/Logger.cs#FirstImplementation "A first Logger implementation.")]

위의 정적 클래스는 사용할 수 있는 가장 간단한 클래스입니다. 메시지를 콘솔에 기록하는 메서드에 대한 단일 구현을 작성해야 합니다. 

[!code-csharp[LogToConsole](../../samples/csharp/delegates-and-events/Program.cs#LogToConsole "A Console logger.")]

마지막으로 로거에 선언된 WriteMessage 대리자에 대리자를 연결함으로써 대리자를 연결해야 합니다.

[!code-csharp[ConnectDelegate](../../samples/csharp/delegates-and-events/Program.cs#ConnectDelegate "Connect to the delegate")]

## <a name="practices"></a>사례

지금까지 샘플은 매우 간단하지만 대리자 관련 디자인에 대한 몇 가지 중요한 지침을 보여 줍니다.

Core Framework에 정의된 대리자 형식을 사용하면 사용자가 대리자를 사용하기가 더 쉽습니다. 새 형식을 정의할 필요가 없으며, 라이브러리를 사용하는 개발자는 특수화된 새 대리자 형식을 배울 필요가 없습니다.

사용되는 인터페이스는 최대한 최소화되고 유연합니다. 새 출력 로거를 만들려면 메서드 하나를 만들어야 합니다. 이 메서드는 정적 메서드이거나 인스턴스 메서드일 수 있습니다. 모든 액세스 권한이 있을 수 있습니다.

## <a name="formatting-output"></a>출력 서식 지정

이 첫 번째 버전을 약간 더 강력하게 만든 후 다른 로깅 메커니즘을 만들어 보겠습니다.

다음으로 로그 클래스에서 보다 구조적인 메시지를 만들도록 `LogMessage()` 메서드에 몇 가지 인수를 추가해 보겠습니다.

[!code-csharp[Severity](../../samples/csharp/delegates-and-events/Logger.cs#Severity "Define severities")]
[!code-csharp[NextLogger](../../samples/csharp/delegates-and-events/Logger.cs#LoggerTwo "Refine the Logger")]

그런 다음 해당 `Severity` 인수를 사용하여 로그의 출력으로 전송되는 메시지를 필터링해 보겠습니다. 

[!code-csharp[FinalLogger](../../samples/csharp/delegates-and-events/Logger.cs#LoggerFinal "Finish the Logger")]

## <a name="practices"></a>사례

로깅 인프라에 새 기능을 추가했습니다. 로거 구성 요소는 모든 출력 메커니즘에 매우 느슨하게 결합되므로 로거 대리자를 구현하는 코드에 영향을 주지 않고 이러한 새 기능을 추가할 수 있습니다.

계속 구축하면 이 느슨한 결합을 통해 다른 위치를 변경하지 않고 사이트의 일부를 업데이트할 때 유연성을 향상시킬 수 있는 방법에 대한 예제가 더 많이 표시됩니다. 실제로 더 큰 애플리케이션에서는 로거 출력 클래스가 다른 어셈블리에 있을 수 있으며 심지어 다시 작성할 필요도 없습니다.

## <a name="building-a-second-output-engine"></a>두 번째 출력 엔진 구축

로그 구성 요소가 함께 제공됩니다. 메시지를 파일에 기록하는 출력 엔진을 하나 더 추가해 보겠습니다. 그러면 약간 더 복잡한 출력 엔진이 됩니다. 이 엔진은 파일 작업을 캡슐화하는 클래스가 되고 기록할 때마다 파일이 항상 닫히도록 합니다. 또한 각 메시지가 생성된 후 모든 데이터가 디스크로 플러시되도록 합니다.

다음 해당 파일 기반 로거입니다.

[!code-csharp[FileLogger](../../samples/csharp/delegates-and-events/FileLogger.cs#FileLogger "Log to files")]

이 클래스를 만들었으면 인스턴스화하고 해당 LogMessage 메서드를 로거 구성 요소에 연결합니다.

[!code-csharp[FileLogger](../../samples/csharp/delegates-and-events/Program.cs#FileLogger "Log to files")]

이러한 두 메서드는 함께 사용할 수 있습니다. 두 로그 메서드를 연결하고 메시지를 콘솔 및 파일에 생성할 수 있습니다.

```csharp
var fileOutput = new FileLogger("log.txt");
Logger.WriteMessage += LogToConsole;
```

나중에 시스템에 문제를 발생시키지 않고 동일한 애플리케이션에서도 대리자 중 하나를 제거할 수 있습니다.

```csharp
Logger.WriteMessage -= LogToConsole;
```

## <a name="practices"></a>사례

이제 로깅 하위 시스템에 대한 두 번째 출력 처리기를 추가했습니다.
파일 시스템을 올바르게 지원하려면 조금 더 많은 인프라가 필요합니다. 대리자는 인스턴스 메서드입니다. 전용 메서드이기도 합니다.
대리자 인프라는 대리자를 연결할 수 있기 때문에 더 큰 액세스 가능성이 필요하지 않습니다.

두 번째로 대리자 기반 디자인에서는 코드를 추가하지 않고도 여러 출력 메서드를 사용합니다. 따라서 여러 출력 메서드를 지원하기 위해 추가 인프라를 구축하지 않아도 됩니다. 이러한 메서드는 호출 목록에서 또 다른 메서드가 됩니다.

파일 로깅 출력 메서드의 코드에 특별히 주의해야 합니다. 예외를 throw하지 않도록 이 코드를 코딩해야 합니다. 이는 항상 엄격한 요건은 아니지만 종종 좋은 사례가 됩니다. 대리자 메서드 중 하나가 예외를 throw하는 경우 호출 목록에 있는 나머지 대리자가 호출되지 않습니다.

마지막으로 파일 로거는 각 로그 메시지에서 파일을 열고 닫아 해당 리소스를 관리해야 합니다. 파일을 열어 두고 작업이 완료되면 IDisposable을 구현하여 파일을 닫도록 선택할 수 있습니다.
두 메서드에는 장점과 단점이 있습니다. 둘 다 클래스 간 결합을 약간 더 많이 만듭니다.

두 시나리오를 지원하기 위해 로거 클래스의 코드를 업데이트할 필요가 없습니다.

## <a name="handling-null-delegates"></a>Null 대리자 처리

마지막으로 출력 메커니즘을 선택하지 않은 경우에 보다 강력하도록 LogMessage 메서드를 업데이트해 보겠습니다. `WriteMessage` 대리자에 연결된 호출 목록이 없는 경우 현재 구현에서는 `NullReferenceException`을 throw합니다.
메서드가 연결되지 않은 경우에도 자동으로 계속되는 디자인을 원할 수 있습니다. `Delegate.Invoke()` 메서드와 결합된 null 조건부 연산자를 사용하면 간단합니다.

```csharp
public static void LogMessage(string msg)
{
    WriteMessage?.Invoke(msg);
}
```

왼쪽 피연산자(이 경우 `WriteMessage`)가 null이면 null 조건부 연산자(`?.`)가 단락됩니다. 즉, 메시지를 기록하려고 시도하지 않는다는 의미입니다.

`System.Delegate` 또는 `System.MulticastDelegate`에 대한 설명서에 나열된 `Invoke()` 메서드를 찾을 수 없습니다. 컴파일러는 선언된 모든 대리자 형식에 대해 형식이 안전한 `Invoke` 메서드를 생성합니다. 따라서 이 예제에서 `Invoke`는 단일 `string` 인수를 사용하고 void 반환 형식을 갖습니다.

## <a name="summary-of-practices"></a>사례의 요약

다른 기록기 및 다른 기능으로 확장할 수 있는 로그 구성 요소의 시작 부분을 살펴보았습니다. 디자인에서 대리자를 사용하면 서로 다른 구성 요소가 매우 느슨하게 결합됩니다. 그러면 여러 가지 장점을 제공합니다. 새 출력 메커니즘을 만들어 시스템에 연결하기가 매우 쉽습니다. 이러한 다른 메커니즘에는 로그 메시지를 기록하는 메서드 하나만 있으면 됩니다. 이 디자인은 새 기능을 추가할 때 매우 복원력이 있습니다. 모든 기록기에 필요한 계약은 하나의 메서드를 구현하는 것입니다. 해당 메서드는 정적 메서드이거나 인스턴스 메서드일 수 있습니다. 공용, 개인 또는 기타 법적 액세스할 수 있습니다.

로거 클래스는 새로운 변경 사항 없이 원하는 대로 기능 향상 또는 변경을 수행할 수 있습니다. 모든 클래스와 마찬가지로 새로운 변경 위험이 없으면 공용 API를 수정할 수 없습니다. 그러나 로거와 모든 출력 엔진 간 결합은 대리자를 통해서만 가능하므로 다른 형식(예: 인터페이스 또는 기본 클래스)이 관련되지 않습니다. 결합은 최대한 작아야 합니다.

[다음](events-overview.md)
