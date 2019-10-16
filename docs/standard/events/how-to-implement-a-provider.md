---
title: '방법: 공급자 구현'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- observer design pattern [.NET Framework], implementing providers
- providers [.NET Framework], in observer design pattern
- observables [.NET Framework], in observer design pattern
ms.assetid: 790b5d8b-d546-40a6-beeb-151b574e5ee5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 12c229b3a1436f9794258fec13905cce0fb767aa
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59324775"
---
# <a name="how-to-implement-a-provider"></a>방법: 공급자 구현
관찰자 디자인 패턴은 데이터를 모니터링하고 알림을 보내는 공급자와 해당 공급자로부터 알림(콜백)을 받는 하나 이상의 관찰자 간에 구분이 필요합니다. 이 항목에서는 공급자를 만드는 방법을 설명합니다. 관련 항목인 [방법: 관찰자 구현](../../../docs/standard/events/how-to-implement-an-observer.md)에서는 관찰자를 만드는 방법을 설명합니다.  
  
### <a name="to-create-a-provider"></a>공급자를 만들려면  
  
1. 공급자가 관찰자에게 보내야 하는 데이터를 정의합니다. 공급자와 이 공급자가 관찰자로 보내는 데이터가 단일 형식일 수 있지만, 일반적으로 서로 다른 형식으로 표시됩니다. 예를 들어 온도 모니터링 애플리케이션에서 `Temperature` 구조체는 공급자(다음 단계에 정의된 `TemperatureMonitor` 클래스로 표시됨)가 모니터링하고 관찰자가 구독하는 데이터를 정의합니다.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/data.cs#1)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/data.vb#1)]  
  
2. <xref:System.IObservable%601?displayProperty=nameWithType> 인터페이스를 구현하는 형식인 데이터 공급자를 정의합니다. 공급자의 제네릭 형식 인수는 공급자가 관찰자로 보내는 형식입니다. 다음 예제에서는 `Temperature`의 제네릭 형식 인수를 사용하여 구성된 <xref:System.IObservable%601?displayProperty=nameWithType> 구현인 `TemperatureMonitor` 클래스를 정의합니다.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#2)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#2)]  
  
3. 해당하는 경우 각 관찰자에게 알릴 수 있도록 공급자가 관찰자에 대한 참조를 저장할 방식을 결정합니다. 일반적으로 제네릭 <xref:System.Collections.Generic.List%601> 개체와 같은 컬렉션 개체가 이 용도로 사용됩니다. 다음 예제에서는 `TemperatureMonitor` 클래스 생성자에서 인스턴스화되는 private <xref:System.Collections.Generic.List%601> 개체를 정의합니다.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#3)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#3)]  
  
4. 구독자가 언제든지 알림 수신을 중지할 수 있도록 공급자가 해당 구독자에게 반환할 수 있는 <xref:System.IDisposable> 구현을 정의합니다. 다음 예제에서는 클래스가 인스턴스화될 때 구독자 컬렉션 및 구독자에 대한 참조를 전달받는 중첩 `Unsubscriber` 클래스를 정의합니다. 이 코드를 통해 구독자가 개체의 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 구현을 호출하여 구독자 컬렉션에서 자신을 제거할 수 있습니다.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#4)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#4)]  
  
5. <xref:System.IObservable%601.Subscribe%2A?displayProperty=nameWithType> 메서드를 구현합니다. 이 메서드는 <xref:System.IObserver%601?displayProperty=nameWithType> 인터페이스에 대한 참조를 전달받으며, 3단계에서 해당 용도로 디자인한 개체에 저장되어야 합니다. 그런 다음, 이 메서드는 4단계에서 개발한 <xref:System.IDisposable> 구현을 반환해야 합니다. 다음 예제는 `TemperatureMonitor` 클래스의 <xref:System.IObservable%601.Subscribe%2A> 메서드 구현을 보여줍니다.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#5)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#5)]  
  
6. 해당 <xref:System.IObserver%601.OnNext%2A?displayProperty=nameWithType>, <xref:System.IObserver%601.OnError%2A?displayProperty=nameWithType> 및 <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType> 구현을 호출하여 적절하게 관찰자에게 알립니다. 일부 경우에 오류가 발생하면 공급자가 <xref:System.IObserver%601.OnError%2A> 메서드를 호출하지 못할 수 있습니다. 예를 들어 다음 `GetTemperature` 메서드는 5초마다 온도 데이터를 읽는 모니터를 시뮬레이트하고 온도가 이전 값보다 .1도 이상 변경된 경우 관찰자에게 알립니다. 디바이스에서 온도를 보고하지 않으면(즉, 값이 null인 경우) 공급자는 전송이 완료되었음을 관찰자에게 알립니다. 각 관찰자의 <xref:System.IObserver%601.OnCompleted%2A> 메서드를 호출할 뿐만 아니라 `GetTemperature` 메서드는 <xref:System.Collections.Generic.List%601> 컬렉션을 지웁니다. 이 경우 공급자는 해당 관찰자의 <xref:System.IObserver%601.OnError%2A> 메서드를 호출하지 않습니다.  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#6)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#6)]  
  
## <a name="example"></a>예제  
 다음 예제에는 온도 모니터링 애플리케이션에 대한 <xref:System.IObservable%601> 구현을 정의하기 위한 전체 소스 코드가 포함되어 있습니다. 여기에는 관찰자로 전송된 데이터인 `Temperature` 구조체 및 <xref:System.IObservable%601> 구현인 `TemperatureMonitor` 클래스가 포함됩니다.  
  
 [!code-csharp[Conceptual.ObserverDesign.HowTo#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#7)]
 [!code-vb[Conceptual.ObserverDesign.HowTo#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#7)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.IObservable%601>
- [관찰자 디자인 패턴](../../../docs/standard/events/observer-design-pattern.md)
- [방법: 관찰자 구현](../../../docs/standard/events/how-to-implement-an-observer.md)
- [관찰자 디자인 패턴 유용한 정보](../../../docs/standard/events/observer-design-pattern-best-practices.md)
