---
title: 관찰자 디자인 패턴 모범 사례
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- observer design pattern [.NET Framework], best practices
- best practices [.NET Framework], observer design pattern
ms.assetid: c834760f-ddd4-417f-abb7-a059679d5b8c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c37480f18c100d66e78e851439bd15e2ecfdd381
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64615189"
---
# <a name="observer-design-pattern-best-practices"></a>관찰자 디자인 패턴 모범 사례
.NET Framework에서는 관찰자 디자인 패턴이 인터페이스 집합으로 구현됩니다. <xref:System.IObservable%601?displayProperty=nameWithType> 인터페이스는 데이터 공급자를 나타냅니다. 이 데이터 공급자는 관찰자가 알림 구독을 취소할 수 있도록 하는 <xref:System.IDisposable> 구현도 제공합니다. <xref:System.IObserver%601?displayProperty=nameWithType> 인터페이스는 관찰자를 나타냅니다. 이 항목에는 이러한 인터페이스를 사용하여 관찰자 디자인 패턴을 구현할 때 개발자가 따라야 하는 모범 사례에 대해 설명합니다.  
  
## <a name="threading"></a>스레딩  
 일반적으로 공급자는 컬렉션 개체로 표시되는 구독자 목록에 특정 관찰자를 추가하여 <xref:System.IObservable%601.Subscribe%2A?displayProperty=nameWithType> 메서드를 구현하며, 구독자 목록에서 특정 관찰자를 제거하여 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 메서드를 구현합니다. 관찰자는 언제든지 이러한 메서드를 호출할 수 있습니다. 또한 공급자/관찰자 계약에서는 <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType> 콜백 메서드 후 구독 취소 담당자를 지정하지 않으므로 공급자와 관찰자가 모두 목록에서 같은 멤버를 제거하려고 할 수 있습니다. 이러한 가능성 때문에 <xref:System.IObservable%601.Subscribe%2A> 및 <xref:System.IDisposable.Dispose%2A> 메서드는 모두 스레드로부터 안전해야 합니다. 일반적으로는 이를 위해 [동시 컬렉션](../../../docs/standard/parallel-programming/data-structures-for-parallel-programming.md) 또는 잠금을 사용합니다. 스레드로부터 안전하지 않은 구현은 스레드로부터 안전하지 않음을 명시적으로 문서화해야 합니다.  
  
 추가로 보장할 내용은 공급자/관찰자 계약을 기반으로 하는 계층에 지정해야 합니다. 구현자는 관찰자 계약에 대한 사용자의 혼동을 방지하기 위해 추가 요구를 사항을 적용하는 경우 이를 명확하게 표시해야 합니다.  
  
## <a name="handling-exceptions"></a>예외 처리  
 데이터 공급자와 관찰자는 느슨하게 결합되므로 관찰자 디자인 패턴의 예외는 정보 제공용으로 사용됩니다. 이는 공급자와 관찰자가 관찰자 디자인 패턴에서 예외를 처리하는 방식에 영향을 줍니다.  
  
### <a name="the-provider----calling-the-onerror-method"></a>공급자 - OnError 메서드 호출  
 <xref:System.IObserver%601.OnError%2A> 메서드는 <xref:System.IObserver%601.OnNext%2A?displayProperty=nameWithType> 메서드와 같이 관찰자에 대한 정보 메시지로 사용됩니다. 그러나 <xref:System.IObserver%601.OnNext%2A> 메서드는 현재 또는 업데이트된 데이터를 관찰자에게 제공하는 반면 <xref:System.IObserver%601.OnError%2A> 메서드는 공급자가 유효한 데이터를 제공할 수 없음을 나타냅니다.  
  
 공급자는 예외를 처리하고 <xref:System.IObserver%601.OnError%2A> 메서드를 호출할 때 다음의 모범 사례를 따라야 합니다.  
  
- 공급자는 특정 요구 사항이 있는 경우 자체 예외를 처리해야 합니다.  
  
- 공급자는 관찰자가 특정 방식으로 예외를 처리한다고 예상하거나 처리하도록 요구해서는 안 됩니다.  
  
- 공급자는 업데이트 제공 기능을 손상시키는 예외를 처리할 때 <xref:System.IObserver%601.OnError%2A> 메서드를 호출해야 합니다. 이러한 예외에 대한 정보를 관찰자에게 전달할 수 있습니다. 다른 경우에는 관찰자에게 예외에 대해 알릴 필요가 없습니다.  
  
 공급자가 <xref:System.IObserver%601.OnError%2A> 또는 <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType> 메서드를 호출한 후에는 추가 알림이 표시되지 않아야 하며 공급자는 해당 관찰자의 구독을 취소할 수 있습니다. 그러나 관찰자는 <xref:System.IObserver%601.OnError%2A> 또는 <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType> 알림을 받기 전이나 받은 후를 포함하여 언제든지 직접 구독을 취소할 수 있습니다. 관찰자 디자인 패턴에서는 구독 취소 담당자(공급자 또는 관찰자)가 지정되지 않으므로 공급자와 관찰자가 모두 구독 취소를 시도할 수 있습니다. 일반적으로 관찰자는 구독 취소 시 구독자 컬렉션에서 제거됩니다. 단일 스레드 애플리케이션에서는 제거를 시도하기 전에 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 구현에서 개체 참조가 유효하며 개체가 구독자 컬렉션의 멤버임을 확인해야 합니다. 다중 스레드 애플리케이션에서는 <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=nameWithType> 개체와 같은 스레드로부터 안전한 컬렉션 개체를 사용해야 합니다.  
  
### <a name="the-observer----implementing-the-onerror-method"></a>관찰자 - OnError 메서드를 구현  
 관찰자는 공급자로부터 오류 알림을 받으면 예외를 정보로 처리해야 하며 특정 작업을 수행하지 않아도 됩니다.  
  
 관찰자는 공급자로의 <xref:System.IObserver%601.OnError%2A> 메서드 호출에 응답할 때 다음 모범 사례를 따라야 합니다.  
  
- 관찰자는 <xref:System.IObserver%601.OnNext%2A> 또는 <xref:System.IObserver%601.OnError%2A> 등의 인터페이스 구현에서 예외를 throw해서는 안 됩니다. 관찰자가 예외를 throw하는 경우 해당 예외는 처리되지 않습니다.  
  
- 호출 스택을 유지하려면 <xref:System.Exception> 메서드로 전달된 <xref:System.IObserver%601.OnError%2A> 개체를 throw하려는 관찰자는 예외를 throw하기 전에 래핑해야 합니다. 이렇게 하려면 표준 예외 개체를 사용해야 합니다.  
  
## <a name="additional-best-practices"></a>추가 모범 사례  
 <xref:System.IObservable%601.Subscribe%2A?displayProperty=nameWithType> 메서드에서 등록 취소를 시도하면 null 참조가 생성될 수 있으므로 이러한 방식은 사용하지 않는 것이 좋습니다.  
  
 관찰자 하나를 여러 공급자에 연결할 수는 있지만, <xref:System.IObserver%601> 인스턴스를 <xref:System.IObservable%601> 인스턴스 하나에만 연결하는 패턴을 사용하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목

- [관찰자 디자인 패턴](../../../docs/standard/events/observer-design-pattern.md)
- [방법: 관찰자 구현](../../../docs/standard/events/how-to-implement-an-observer.md)
- [방법: 공급자 구현](../../../docs/standard/events/how-to-implement-a-provider.md)
