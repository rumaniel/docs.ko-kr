---
title: 이벤트 기반 비동기 패턴 구현 시기 결정
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET Framework], asynchronous
- AsyncOperationManager class
- threading [.NET Framework], asynchronous features
- AsyncOperation class
- AsyncCompletedEventArgs class
ms.assetid: a00046aa-785d-4f7f-a8e5-d06475ea50da
ms.openlocfilehash: 5fca32953af91184fe99d8ef6afe5a2374f325d6
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663720"
---
# <a name="deciding-when-to-implement-the-event-based-asynchronous-pattern"></a>이벤트 기반 비동기 패턴 구현 시기 결정

이벤트 기반 비동기 패턴은 클래스의 비동기 동작을 표시하기 위한 패턴을 제공합니다. 이 패턴의 도입에 따라 .NET Framework는 비동기 동작을 표시하기 위한 두 가지 패턴 즉, <xref:System.IAsyncResult?displayProperty=nameWithType> 인터페이스를 기반으로 하는 비동기 패턴 및 이벤트 기반 패턴을 정의합니다. 이 항목에서는 두 패턴을 모두 구현하는 것이 적절한 경우에 대해 설명합니다.

<xref:System.IAsyncResult> 인터페이스를 사용한 비동기 프로그래밍에 대한 자세한 내용은 [APM(비동기 프로그래밍 모델)](../../../docs/standard/asynchronous-programming-patterns/asynchronous-programming-model-apm.md)을 참조하세요.

## <a name="general-principles"></a>일반 원칙

일반적으로 가능한 경우 언제든 이벤트 기반 비동기 패턴을 사용하여 비동기 기능을 표시해야 합니다. 그러나 이벤트 기반 패턴이 충족할 수 없는 몇 가지 요구 사항이 있습니다. 이러한 경우 이벤트 기반 패턴 외에도 <xref:System.IAsyncResult> 패턴을 구현해야 할 수 있습니다.

> [!NOTE]
> 이벤트 기반 패턴을 구현하지 않고 <xref:System.IAsyncResult> 패턴을 구현하는 경우는 거의 없습니다.

## <a name="guidelines"></a>지침

다음 목록은 이벤트 기반 비동기 패턴을 구현해야 하는 경우에 대한 지침을 설명합니다.

- 이벤트 기반 패턴을 기본 API로 사용하여 클래스의 비동기 동작을 표시합니다.

- 클래스가 Windows Forms와 같은 클라이언트 애플리케이션에서 주로 사용되는 경우 <xref:System.IAsyncResult> 패턴을 표시하지 않습니다.

- 요구 사항을 충족하는 데 필요한 경우에만 <xref:System.IAsyncResult> 패턴을 표시합니다. 예를 들어 기존 API와의 호환성을 위해 <xref:System.IAsyncResult> 패턴을 표시해야 할 수 있습니다.

- 이벤트 기반 패턴을 표시하지 않고 <xref:System.IAsyncResult> 패턴을 표시해서는 안 됩니다.

- <xref:System.IAsyncResult> 패턴을 표시해야 하는 경우 고급 옵션으로 그렇게 해야 합니다. 예를 들어 프록시 개체를 생성하는 경우 기본적으로 <xref:System.IAsyncResult> 패턴을 생성하는 옵션을 사용하여 이벤트 기반 패턴을 생성합니다.

- <xref:System.IAsyncResult> 패턴 구현 시 이벤트 기반 패턴 구현을 빌드합니다.

- 이벤트 기반 패턴과 <xref:System.IAsyncResult> 패턴이 모두 동일한 클래스에 표시되지 않도록 합니다. “상위 수준” 클래스에 이벤트 기반 패턴을 표시하고 “하위 수준” 클래스에 <xref:System.IAsyncResult> 패턴을 표시합니다. 예를 들어 <xref:System.Net.WebClient> 구성 요소의 이벤트 기반 패턴을 <xref:System.Web.HttpRequest> 클래스의 <xref:System.IAsyncResult> 패턴과 비교합니다.

  - 호환성을 위해 필요한 경우 이벤트 기반 패턴 및 <xref:System.IAsyncResult> 패턴을 동일한 클래스에 표시합니다. 예를 들어 <xref:System.IAsyncResult> 패턴을 사용하는 API를 이미 릴리스한 경우 이전 버전과의 호환성을 위해 <xref:System.IAsyncResult> 패턴을 유지해야 합니다.

  - 결과 개체 모델의 복잡성이 구현을 분리하는 이점보다 더 큰 경우 이벤트 기반 패턴 및 <xref:System.IAsyncResult> 패턴을 동일한 클래스에 표시합니다. 이벤트 기반 패턴 표시를 피하는 것보다 단일 클래스에 두 패턴을 모두 표시하는 것이 더 좋습니다.

  - 이벤트 기반 패턴과 <xref:System.IAsyncResult> 패턴을 모두 단일 클래스에 표시해야 하는 경우 <xref:System.ComponentModel.EditorBrowsableState.Advanced>로 설정된 <xref:System.ComponentModel.EditorBrowsableAttribute>를 사용하여 <xref:System.IAsyncResult> 패턴 구현을 고급 기능으로 표시합니다. 이는 Visual Studio IntelliSense와 같은 환경에서 <xref:System.IAsyncResult> 속성 및 메서드를 표시하지 않도록 설계한다는 것을 나타냅니다. 이러한 속성 및 메서드는 여전히 완벽하게 사용할 수 있지만, IntelliSense를 통해 작업하는 개발자는 API를 더욱 명확하게 볼 수 있습니다.

## <a name="criteria-for-exposing-the-iasyncresult-pattern-in-addition-to-the-event-based-pattern"></a>이벤트 기반 패턴 외에도 IAsyncResult 패턴을 표시하기 위한 조건

이벤트 기반 비동기 패턴은 앞서 언급한 시나리오에 따른 많은 이점이 있지만, 성능이 가장 중요한 요구 사항인 경우 알고 있어야 하는 몇 가지 단점이 있습니다.

<xref:System.IAsyncResult> 패턴뿐만 아니라 이벤트 기반 패턴이 다루지 않는 세 가지 시나리오가 있습니다.

- 하나의 <xref:System.IAsyncResult>에서 차단 대기

- 여러 <xref:System.IAsyncResult> 개체에서 차단 대기

- <xref:System.IAsyncResult>에서 완료를 위한 폴링

이벤트 기반 패턴을 사용하여 이러한 시나리오를 다룰 수 ​​있지만, 그렇게 하면 <xref:System.IAsyncResult> 패턴을 사용하는 것보다 더 복잡하고 번거롭습니다.

개발자는 일반적으로 성능 요구 사항이 매우 높은 서비스에 대해 <xref:System.IAsyncResult> 패턴을 흔히 사용합니다. 예를 들어 완료를 위한 폴링 시나리오는 고성능 서버 기술입니다.

또한 이벤트 기반 패턴은 더 많은 개체 특히, <xref:System.EventArgs>를 생성하고 스레드 간에 동기화되므로 <xref:System.IAsyncResult> 패턴보다 덜 효율적입니다.

다음 목록은 <xref:System.IAsyncResult> 패턴을 사용하기로 한 경우 따라야 할 몇 가지 권장 사항을 보여줍니다.

- 특히 <xref:System.Threading.WaitHandle> 또는 <xref:System.IAsyncResult> 개체에 대한 지원이 필요한 경우에만 <xref:System.IAsyncResult> 패턴을 표시합니다.

- <xref:System.IAsyncResult> 패턴을 사용하는 기존 API가 있는 경우에만 <xref:System.IAsyncResult> 패턴을 표시합니다.

- <xref:System.IAsyncResult> 패턴을 기반으로 하는 기존 API가 있는 경우 다음 릴리스에서 이벤트 기반 패턴을 표시하는 것도 고려합니다.

- 확인한 고성능 요구 사항을 이벤트 기반 패턴으로 충족할 수 없지만 <xref:System.IAsyncResult> 패턴으로 충족할 수 있는 경우에만 <xref:System.IAsyncResult> 패턴을 표시합니다.

## <a name="see-also"></a>참고 항목

- [방법: 이벤트 기반 비동기 패턴을 지원하는 구성 요소 구현](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)
- [EAP(이벤트 기반 비동기 패턴)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)
- [이벤트 기반 비동기 패턴 구현](../../../docs/standard/asynchronous-programming-patterns/implementing-the-event-based-asynchronous-pattern.md)
- [최선의 이벤트 기반 비동기 패턴 구현 방법](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)
- [이벤트 기반 비동기 패턴 개요](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)
