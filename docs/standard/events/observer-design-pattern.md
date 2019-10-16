---
title: 관찰자 디자인 패턴
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- IObserver(Of T) interface
- IObservable<T> interface
- IObserver<T> interface
- IObservable(Of T) interface
- observer design pattern [.NET Framework]
ms.assetid: 3680171f-f522-453c-aa4a-54f755a78f88
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 06dbc4b7124aa873fd8471794fa25b0f47f8ce3d
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663573"
---
# <a name="observer-design-pattern"></a>관찰자 디자인 패턴

관찰자 디자인 패턴은 구독자가 공급자에 등록하고 공급자로부터 알림을 받을 수 있게 합니다. 이는 푸시 기반 알림이 필요한 시나리오에 적합합니다. 이 패턴은 ‘공급자’(‘주체’ 또는 ‘관찰 가능 대상’이라고도 함) 및 0개 이상의 ‘관찰자’를 정의합니다.     관찰자는 공급자에 등록하며 미리 정의된 조건, 이벤트 또는 상태 변경이 발생할 때마다 공급자가 해당 메서드 중 하나를 호출하여 자동으로 모든 관찰자에게 알립니다. 이 메서드 호출에서 공급자는 관찰자에게 현재 상태 정보를 제공할 수도 있습니다. .NET Framework에서는 제네릭 <xref:System.IObservable%601?displayProperty=nameWithType> 및 <xref:System.IObserver%601?displayProperty=nameWithType> 인터페이스를 구현하여 관찰자 디자인 패턴을 적용합니다. 제네릭 형식 매개 변수는 알림 정보를 제공하는 형식을 나타냅니다.

## <a name="applying-the-pattern"></a>패턴 적용

관찰자 디자인 패턴은 데이터 소스(비즈니스 논리) 계층 및 사용자 인터페이스(표시) 계층과 같은 두 가지 구성 요소 또는 애플리케이션 계층의 명확한 구분을 지원하기 때문에 분산된 푸시 기반 알림에 적합합니다. 공급자가 콜백을 사용하여 해당 클라이언트에 현재 정보를 제공할 때마다 패턴을 구현할 수 있습니다.

패턴을 구현하려면 다음을 제공해야 합니다.

- 관찰자에게 알림을 전송하는 개체인 공급자 또는 주체. 공급자는 <xref:System.IObservable%601> 인터페이스를 구현하는 클래스 또는 구조체입니다. 공급자는 공급자로부터 알림을 수신하려는 관찰자가 호출하는 단일 메서드 <xref:System.IObservable%601.Subscribe%2A?displayProperty=nameWithType>를 구현해야 합니다.

- 공급자로부터 알림을 수신하는 개체인 관찰자. 관찰자는 <xref:System.IObserver%601> 인터페이스를 구현하는 클래스 또는 구조체입니다. 관찰자는 모두 공급자에 의해 호출되는 다음 세 개의 메서드를 구현해야 합니다.

  - <xref:System.IObserver%601.OnNext%2A?displayProperty=nameWithType> - 관찰자에게 새 정보나 현재 정보를 제공합니다.

  - <xref:System.IObserver%601.OnError%2A?displayProperty=nameWithType> - 오류가 발생했음을 관찰자에게 알립니다.

  - <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType> - 공급자가 알림 전송을 완료했음을 나타냅니다.

- 공급자가 관찰자를 추적할 수 있게 해주는 메커니즘. 일반적으로 공급자는 <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> 개체와 같은 컨테이너 개체를 사용하여 알림을 구독한 <xref:System.IObserver%601> 구현에 대한 참조를 보유합니다. 이 목적으로 스토리지 컨테이너를 사용하면 공급자가 0개에서 무한대 개수까지 관찰자를 처리할 수 있습니다. 관찰자가 알림을 수신하는 순서는 정의되지 않습니다. 공급자가 임의 메서드를 사용하여 순서를 결정할 수 있습니다.

- 알림이 완료될 때 공급자가 관찰자를 제거할 수 있도록 하는 <xref:System.IDisposable> 구현. 관찰자는 <xref:System.IObservable%601.Subscribe%2A> 메서드로부터 <xref:System.IDisposable> 구현에 대한 참조를 수신하므로 공급자가 알림 전송을 완료하기 전에 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 메서드를 호출하여 구독을 취소할 수도 있습니다.

- 공급자가 해당 관찰자에게 전송하는 데이터를 포함하는 개체. 이 개체의 형식은 <xref:System.IObservable%601> 및 <xref:System.IObserver%601> 인터페이스의 제네릭 형식 매개 변수에 해당합니다. 이 개체는 <xref:System.IObservable%601> 구현과 동일할 수도 있지만 일반적으로 별도 형식입니다.

> [!NOTE]
> 관찰자 디자인 패턴 구현 외에도 <xref:System.IObservable%601> 및 <xref:System.IObserver%601> 인터페이스를 사용하여 빌드된 라이브러리 탐색에 관심이 있을 수 있습니다. 예를 들어 [.NET용 사후 확장(Rx)](https://docs.microsoft.com/previous-versions/dotnet/reactive-extensions/hh242985(v=vs.103))은 비동기 프로그래밍을 지원하기 위해 일련의 확장 메서드와 LINQ 표준 시퀀스 연산자로 구성됩니다.

## <a name="implementing-the-pattern"></a>패턴 구현

다음 예제에서는 관찰자 디자인 패턴을 사용하여 공항의 수하물 찾는 곳 정보 시스템을 구현합니다. `BaggageInfo` 클래스는 도착 항공편과 각 항공편의 수하물을 찾을 수 있는 컨베이어 벨트에 대한 정보를 제공합니다. 다음 예제에서 이를 확인할 수 있습니다.

[!code-csharp[Conceptual.ObserverDesignPattern#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesignpattern/cs/provider.cs#1)]
[!code-vb[Conceptual.ObserverDesignPattern#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesignpattern/vb/provider.vb#1)]

`BaggageHandler` 클래스는 도착 항공편 및 수하물을 찾을 수 있는 컨베이어 벨트에 대한 정보를 받아야 합니다. 내부적으로 다음 두 개의 컬렉션을 유지 관리합니다.

- `observers` - 업데이트된 정보를 수신할 클라이언트 컬렉션입니다.

- `flights` - 항공편 및 할당된 컨베이어 벨트 컬렉션입니다.

두 컬렉션 모두 `BaggageHandler` 클래스 생성자에서 인스턴스화되는 제네릭 <xref:System.Collections.Generic.List%601> 개체로 표시됩니다. `BaggageHandler` 클래스의 소스 코드는 다음 예제에 나와 있습니다.

[!code-csharp[Conceptual.ObserverDesignPattern#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesignpattern/cs/provider.cs#2)]
[!code-vb[Conceptual.ObserverDesignPattern#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesignpattern/vb/provider.vb#2)]

업데이트된 정보를 수신하려는 클라이언트는 `BaggageHandler.Subscribe` 메서드를 호출합니다. 클라이언트가 이전에 알림을 구독하지 않은 경우 클라이언트의 <xref:System.IObserver%601> 구현에 대한 참조가 `observers` 컬렉션에 추가됩니다.

오버로드된 `BaggageHandler.BaggageStatus` 메서드를 호출하여 항공편의 수하물을 내리는 중인지 여부를 나타낼 수 있습니다. 내리는 중이면 메서드에 항공편 번호, 출발 공항 및 수하물을 내리는 중인 컨베이어 벨트가 전달됩니다. 더 이상 내리지 않는 경우 메서드에 항공편 번호만 전달됩니다. 수하물을 내리는 경우 메서드는 메서드에 전달된 `BaggageInfo` 정보가 `flights` 컬렉션에 있는지 여부를 확인합니다. 그러지 않은 경우 메서드는 정보를 추가하고 각 관찰자의 `OnNext` 메서드를 호출합니다. 더 이상 수하물을 내리지 않는 항공편의 경우 메서드는 항공편에 대한 정보가 `flights` 컬렉션에 저장되었는지 여부를 확인합니다. 저장된 경우 메서드는 각 관찰자의 `OnNext` 메서드를 호출하고 `flights` 컬렉션에서 `BaggageInfo` 개체를 제거합니다.

그날의 마지막 항공편이 착륙하고 해당 수하물이 처리되면 `BaggageHandler.LastBaggageClaimed` 메서드가 호출됩니다. 이 메서드는 각 관찰자의 `OnCompleted` 메서드를 호출하여 모든 알림이 완료되었음을 나타내고 `observers` 컬렉션을 지웁니다.

공급자의 <xref:System.IObservable%601.Subscribe%2A> 메서드는 <xref:System.IObserver%601.OnCompleted%2A> 메서드가 호출되기 전에 관찰자가 알림 수신을 중지할 수 있도록 하는 <xref:System.IDisposable> 구현을 반환합니다. `Unsubscriber(Of BaggageInfo)` 클래스의 소스 코드는 다음 예제에 나와 있습니다. `BaggageHandler.Subscribe` 메서드에서 클래스가 인스턴스화되면 `observers` 컬렉션에 대한 참조 및 컬렉션에 추가된 관찰자에 대한 참조가 전달됩니다. 이러한 참조는 지역 변수에 할당됩니다. 개체의 `Dispose` 메서드가 호출되면 관찰자가 `observers` 컬렉션에 여전히 있는지 여부를 확인하고, 있을 경우 관찰자를 제거합니다.

[!code-csharp[Conceptual.ObserverDesignPattern#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesignpattern/cs/provider.cs#3)]
[!code-vb[Conceptual.ObserverDesignPattern#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesignpattern/vb/provider.vb#3)]

다음 예제에서는 수하물 찾는 곳 정보를 표시하는 기본 클래스인 `ArrivalsMonitor`라는 <xref:System.IObserver%601> 구현을 제공합니다. 정보는 출발 도시 이름별 사전순으로 표시됩니다. `ArrivalsMonitor`의 메서드는 `overridable`(Visual Basic) 또는 `virtual`(C#)로 표시되므로 모두 파생 클래스를 통해 재정의할 수 있습니다.

[!code-csharp[Conceptual.ObserverDesignPattern#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesignpattern/cs/observer.cs#4)]
[!code-vb[Conceptual.ObserverDesignPattern#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesignpattern/vb/observer.vb#4)]

`ArrivalsMonitor` 클래스에는 `Subscribe` 및 `Unsubscribe` 메서드가 포함됩니다. `Subscribe` 메서드를 통해 클래스는 <xref:System.IObservable%601.Subscribe%2A> 호출에서 반환된 <xref:System.IDisposable> 구현을 전용 변수에 저장할 수 있습니다. `Unsubscribe` 메서드를 통해 클래스는 공급자의 <xref:System.IDisposable.Dispose%2A> 구현을 호출하여 알림 구독을 취소할 수 있습니다. `ArrivalsMonitor`에서는 <xref:System.IObserver%601.OnNext%2A>, <xref:System.IObserver%601.OnError%2A> 및 <xref:System.IObserver%601.OnCompleted%2A> 메서드의 구현도 제공합니다. <xref:System.IObserver%601.OnNext%2A> 구현에만 상당한 양의 코드가 포함됩니다. 메서드는 도착 항공편의 출발 공항 및 수하물을 찾을 수 있는 컨베이어 벨트에 대한 정보를 유지 관리하는 private, sorted, generic <xref:System.Collections.Generic.List%601> 개체로 작동합니다. `BaggageHandler` 클래스가 새 항공편 도착을 보고하면 <xref:System.IObserver%601.OnNext%2A> 메서드 구현에서 해당 항공편에 대한 정보를 목록에 추가합니다. `BaggageHandler` 클래스가 항공편의 수하물을 내렸다고 보고하면 <xref:System.IObserver%601.OnNext%2A> 메서드가 목록에서 해당 항공편을 제거합니다. 변경될 때마다 목록이 정렬되고 콘솔에 표시됩니다.

다음 예제에는 `BaggageHandler` 클래스를 인스턴스화하는 애플리케이션 진입점과 `ArrivalsMonitor` 클래스의 두 인스턴스가 포함되어 있으며, `BaggageHandler.BaggageStatus` 메서드를 사용하여 도착 항공편에 대한 정보를 추가하고 제거합니다. 각각의 경우에서 관찰자는 업데이트를 수신하고 수하물을 찾는 곳 정보를 올바르게 표시합니다.

[!code-csharp[Conceptual.ObserverDesignPattern#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesignpattern/cs/program.cs#5)]
[!code-vb[Conceptual.ObserverDesignPattern#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesignpattern/vb/module1.vb#5)]

## <a name="related-topics"></a>관련 항목

|제목|설명|
|-----------|-----------------|
|[관찰자 디자인 패턴 유용한 정보](../../../docs/standard/events/observer-design-pattern-best-practices.md)|관찰자 디자인 패턴을 구현하는 애플리케이션을 개발할 때 채택할 모범 사례를 설명합니다.|
|[방법: 공급자 구현](../../../docs/standard/events/how-to-implement-a-provider.md)|온도 모니터링 애플리케이션에 대한 공급자의 단계별 구현을 제공합니다.|
|[방법: 관찰자 구현](../../../docs/standard/events/how-to-implement-an-observer.md)|온도 모니터링 애플리케이션에 대한 관찰자의 단계별 구현을 제공합니다.|
