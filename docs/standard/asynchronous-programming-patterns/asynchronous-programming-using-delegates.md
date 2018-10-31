---
title: 대리자를 사용한 비동기 프로그래밍
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- BeginInvoke method
- asynchronous programming, delegates
- asynchronous delegates
- calling synchronous methods in asynchronous manner
- EndInvoke method
- calling asynchronous methods
- delegates [.NET Framework], asynchronous
- synchronous calling in asynchronous manner
ms.assetid: 38a345ca-6963-4436-9608-5c9defef9c64
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: bad5372af1d771dc93a20e61090ef84126f3e1eb
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48033326"
---
# <a name="asynchronous-programming-using-delegates"></a>대리자를 사용한 비동기 프로그래밍
대리자를 사용하면 비동기 방식으로 동기 메서드를 호출할 수 있습니다. 대리자를 동기적으로 호출하면 `Invoke` 메서드는 현재 스레드에서 직접 대상 메서드를 호출합니다. `BeginInvoke` 메서드가 호출되면 CLR(공용 언어 런타임)에서 요청을 대기하고 호출자에게 즉시 반환합니다. 대상 메서드는 스레드 풀의 스레드에서 비동기적으로 호출됩니다. 요청을 제출하는 원래 스레드는 계속해서 대상 메서드와 함께 실행됩니다. `BeginInvoke` 메서드 호출에서 콜백 메서드가 지정된 경우 대상 메서드가 종료될 때 콜백 메서드가 호출됩니다. 콜백 메서드에서 `EndInvoke` 메서드는 반환 값 및 입/출력 또는 출력 전용 매개 변수를 가져옵니다. `BeginInvoke`를 호출할 때 콜백 메서드를 지정하지 않으면 `BeginInvoke`를 호출한 스레드에서 `EndInvoke`가 호출될 수 있습니다.  
  
> [!IMPORTANT]
>  컴파일러는 사용자가 지정한 대리자 시그니처를 사용하여 `Invoke`, `BeginInvoke` 및 `EndInvoke` 메서드를 통해 대리자 클래스를 내보내야 합니다. `BeginInvoke` 및 `EndInvoke` 메서드는 네이티브로 데코레이팅해야 합니다. 이러한 메서드는 네이티브로 표시되므로 CLR은 클래스 로드 타임에 구현을 자동으로 제공합니다. 로더는 이러한 메서드가 재정의되지 않도록 보장합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [동기 메서드를 비동기 방식으로 호출](../../../docs/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)  
 대리자를 사용하여 일반적인 메서드에 대해 비동기 호출을 수행하는 방법을 살펴보고 비동기 호출이 반환될 때까지 기다리는 4가지 방법을 보여 주는 간단한 코드 예제를 제공합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [EAP(이벤트 기반 비동기 패턴)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)  
 .NET Framework를 사용한 비동기 프로그래밍에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목

* <xref:System.Delegate>
