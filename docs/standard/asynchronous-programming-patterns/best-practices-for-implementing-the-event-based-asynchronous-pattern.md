---
title: 최선의 이벤트 기반 비동기 패턴 구현 방법
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
ms.assetid: 4acd2094-4f46-4eff-9190-92d0d9ff47db
ms.openlocfilehash: e50f455ab83b0b057f8ce3c32f874e6856632d70
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48836961"
---
# <a name="best-practices-for-implementing-the-event-based-asynchronous-pattern"></a>최선의 이벤트 기반 비동기 패턴 구현 방법
이벤트 기반 비동기 패턴은 익숙한 이벤트 및 대리자 의미 체계를 사용하여 클래스에 비동기 동작을 노출하는 효과적인 방법을 제공합니다. 이벤트 기반 비동기 패턴을 구현하려면 몇 가지 구체적인 동작 요구 사항을 따라야 합니다. 다음 섹션에서는 이벤트 기반 비동기 패턴을 따르는 클래스를 구현할 때 고려해야 할 요구 사항 및 지침을 설명합니다.  
  
 개요를 보려면 [이벤트 기반 비동기 패턴 구현](../../../docs/standard/asynchronous-programming-patterns/implementing-the-event-based-asynchronous-pattern.md)을 참조하세요.  
  
## <a name="required-behavioral-guarantees"></a>필요한 동작 보장  
 이벤트 기반 비동기 패턴을 구현하는 경우 클래스가 올바르게 동작하고 클래스의 클라이언트가 해당 동작을 사용할 수 있도록 보장하는 다양한 보장을 제공해야 합니다.  
  
### <a name="completion"></a>완료  
 성공적인 완료, 오류 또는 취소가 있는 경우 항상 <em>MethodName</em>**Completed** 이벤트 처리기를 호출합니다. 응용 프로그램이 유휴 상태로 유지되고 절대 완료되지 않는 상황이 응용 프로그램에 발생해서는 안 됩니다. 이 규칙에 대한 한 가지 예외는 비동기 작업 자체가 절대 완료되지 않도록 디자인된 경우입니다.  
  
### <a name="completed-event-and-eventargs"></a>완료된 이벤트 및 EventArgs  
 별개의 각 <em>MethodName</em>**Async** 메서드의 경우 다음 디자인 요구 사항을 적용합니다.  
  
-   동일한 클래스에서 <em>MethodName</em>**Completed** 이벤트를 메서드로 정의합니다.  
  
-   <xref:System.EventArgs> 클래스에서 파생되는 <em>MethodName</em>**Completed** 이벤트에 대한 <xref:System.ComponentModel.AsyncCompletedEventArgs> 클래스 및 수반하는 대리자를 정의합니다. 기본 클래스 이름은 <em>MethodName</em>**CompletedEventArgs** 형식이어야 합니다.  
  
-   <xref:System.EventArgs> 클래스가 <em>MethodName</em> 메서드의 반환 값에 관련되도록 합니다. <xref:System.EventArgs> 클래스를 사용할 경우 개발자가 결과를 캐스팅할 필요가 없도록 해야 합니다.  
  
     다음 코드 예제에서는 각각 이 디자인 요구 사항의 좋은 구현과 나쁜 구현을 보여 줍니다.  
  
```csharp  
// Good design  
private void Form1_MethodNameCompleted(object sender, xxxCompletedEventArgs e)   
{   
    DemoType result = e.Result;  
}  
  
// Bad design  
private void Form1_MethodNameCompleted(object sender, MethodNameCompletedEventArgs e)   
{   
    DemoType result = (DemoType)(e.Result);  
}  
```  
  
-   <xref:System.EventArgs>를 반환하는 반환 메서드에 대해 `void` 클래스를 정의하지 마세요. 대신 <xref:System.ComponentModel.AsyncCompletedEventArgs> 클래스의 인스턴스를 사용하세요.  
  
-   항상 <em>MethodName</em>**Completed** 이벤트가 발생하도록 합니다. 이 이벤트는 성공적인 완료, 오류 또는 취소 시 발생해야 합니다. 응용 프로그램이 유휴 상태로 유지되고 절대 완료되지 않는 상황이 응용 프로그램에 발생해서는 안 됩니다.  
  
-   비동기 작업에서 발생하는 모든 예외를 catch하고 catch된 예외를 <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A> 속성에 할당하도록 합니다.  
  
-   작업을 완료하는 중에 오류가 발생한 경우 결과에 액세스할 수 없습니다. <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A> 속성이 `null`이 아닌 경우 <xref:System.EventArgs> 구조의 모든 속성에 액세스할 때 예외가 발생해야 합니다. <xref:System.ComponentModel.AsyncCompletedEventArgs.RaiseExceptionIfNecessary%2A> 메서드를 사용하여 이 확인을 수행합니다.  
  
-   제한 시간 초과를 오류로 모델링합니다. 제한 시간 초과가 발생하면 <em>MethodName</em>**Completed** 이벤트를 발생시키고 <xref:System.TimeoutException>을<xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A> 속성에 할당합니다.  
  
-   클래스가 여러 동시 호출을 지원하는 경우 <em>MethodName</em>**Completed** 이벤트에 `userSuppliedState` 개체가 포함되도록 합니다.  
  
-   적절한 스레드 및 응용 프로그램 수명 주기의 적절한 시간에 <em>MethodName</em>**Completed** 이벤트가 발생하도록 합니다. 자세한 내용은 스레딩 및 컨텍스트 섹션을 참조하세요.  
  
### <a name="simultaneously-executing-operations"></a>작업 동시 실행  
  
-   클래스가 여러 동시 호출을 지원하는 경우 개발자가 개체 반환 상태 매개 변수 또는 `userSuppliedState`라는 작업 ID를 사용하는 <em>MethodName</em>**Async** 오버로드를 별도로 정의하여 각 호출을 추적할 수 있도록 합니다. 이 매개 변수는 항상 <em>MethodName</em>**Async** 메서드 시그니처의 마지막 매개 변수여야 합니다.  
  
-   클래스가 개체 반환 상태 매개 변수 또는 작업 ID를 사용하는 <em>MethodName</em>**Async** 오버로드를 정의하는 경우 해당 작업 ID로 작업의 수명을 추적해야 하며, 해당 작업 ID를 완료 처리기에 다시 제공해야 합니다. 도움이 되는 도우미 클래스가 있습니다. 동시성 관리에 대한 자세한 내용은 [방법: 이벤트 기반 비동기 패턴을 지원하는 구성 요소 구현](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)을 참조하세요.  
  
-   클래스가 상태 매개 변수 없이 <em>MethodName</em>**Async** 메서드를 정의하고 클래스가 여러 동시 호출을 지원하지 않는 경우 이전 <em>MethodName</em>**Async** 호출이 완료되기 전에 <em>MethodName</em>**Async**를 호출하려는 시도에서 <xref:System.InvalidOperationException>이 발생하도록 합니다.  
  
-   일반적으로 처리 중인 작업이 여러 개 있도록 `userSuppliedState` 매개 변수 없이 <em>MethodName</em>**Async** 메서드를 여러 번 호출한 경우 예외를 발생시키지 마세요. 클래스가 명시적으로 해당 상황을 처리할 수 없는 경우 예외를 발생시킬 수 있지만 개발자가 구분할 수 없는 이러한 여러 콜백을 처리할 수 있다고 가정합니다.  
  
### <a name="accessing-results"></a>결과 액세스  
  
-   비동기 작업을 실행하는 중에 오류가 발생한 경우 결과에 액세스할 수 없습니다. <xref:System.ComponentModel.AsyncCompletedEventArgs>가 <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A>이 아닌 경우 `null`의 속성에 액세스하면 <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A>에서 참조하는 예외가 발생하도록 합니다. <xref:System.ComponentModel.AsyncCompletedEventArgs> 클래스는 이 용도로 <xref:System.ComponentModel.AsyncCompletedEventArgs.RaiseExceptionIfNecessary%2A> 메서드를 제공합니다.  
  
-   결과에 액세스하려는 모든 시도에서 작업이 취소되었음을 나타내는 <xref:System.InvalidOperationException>이 발생하도록 합니다. <xref:System.ComponentModel.AsyncCompletedEventArgs.RaiseExceptionIfNecessary%2A?displayProperty=nameWithType> 메서드를 사용하여 이 확인을 수행합니다.  
  
### <a name="progress-reporting"></a>진행률 보고  
  
-   가능한 경우 진행률 보고를 지원합니다. 그러면 개발자가 클래스를 사용할 때 더 나은 응용 프로그램 사용자 경험을 제공할 수 있습니다.  
  
-   **ProgressChanged** 또는 <em>MethodName</em>**ProgressChanged** 이벤트를 구현하는 경우 특정 비동기 작업의 <em>MethodName</em>**Completed** 이벤트가 발생한 후 해당 작업에 대해 그러한 이벤트가 발생하지 않도록 합니다.  
  
-   표준 <xref:System.ComponentModel.ProgressChangedEventArgs>를 채우는 경우 <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A>가 항상 백분율로 해석될 수 있도록 합니다. 백분율이 정확할 필요는 없지만 백분율을 나타내야 합니다. 진행률 보고 메트릭이 백분율이 아닌 다른 메트릭이어야 하는 경우 <xref:System.ComponentModel.ProgressChangedEventArgs> 클래스에서 클래스를 파생시키고 <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A>를 0으로 둡니다. 백분율이 아닌 보고 메트릭을 사용하는 것을 피하세요.  
  
-   적절한 스레드 및 응용 프로그램 수명 주기의 적절한 시간에 `ProgressChanged` 이벤트가 발생하도록 합니다. 자세한 내용은 스레딩 및 컨텍스트 섹션을 참조하세요.  
  
### <a name="isbusy-implementation"></a>IsBusy 구현  
  
-   클래스가 여러 동시 호출을 지원하는 경우 `IsBusy` 속성을 노출하지 마세요. 예를 들어, XML 웹 서비스 프록시는 비동기 메서드의 여러 동시 호출을 지원하므로 `IsBusy` 속성을 노출하지 않습니다.  
  
-   `IsBusy` 속성은 <em>MethodName</em>**Async** 메서드가 호출된 후 <em>MethodName</em>**Completed** 이벤트가 발생하기 전에 `true`를 반환해야 합니다. 그렇지 않으면 `false`를 반환해야 합니다. <xref:System.ComponentModel.BackgroundWorker> 및 <xref:System.Net.WebClient> 구성 요소는 `IsBusy` 속성을 노출하는 클래스의 예입니다.  
  
### <a name="cancellation"></a>취소  
  
-   가능한 경우 취소를 지원합니다. 그러면 개발자가 클래스를 사용할 때 더 나은 응용 프로그램 사용자 경험을 제공할 수 있습니다.  
  
-   취소의 경우 <xref:System.ComponentModel.AsyncCompletedEventArgs.Cancelled%2A> 개체에 <xref:System.ComponentModel.AsyncCompletedEventArgs> 플래그를 설정합니다.  
  
-   결과에 액세스하려는 모든 시도에서 작업이 취소되었음을 나타내는 <xref:System.InvalidOperationException>이 발생하도록 합니다. <xref:System.ComponentModel.AsyncCompletedEventArgs.RaiseExceptionIfNecessary%2A?displayProperty=nameWithType> 메서드를 사용하여 이 확인을 수행합니다.  
  
-   취소 메서드에 대한 호출은 항상 성공적으로 반환되고 예외를 발생시키지 않도록 합니다. 일반적으로 클라이언트는 어느 시점에서든 작업이 진정으로 취소 가능한지에 대한 알림을 받지 않으며, 이전에 발생한 취소가 성공적인지에 대한 알림도 받지 않습니다. 그러나 응용 프로그램은 완료 상태에 참여하므로 취소가 성공적일 때 응용 프로그램에는 항상 알림이 제공됩니다.  
  
-   작업이 취소되면 <em>MethodName</em>**Completed** 이벤트를 발생시킵니다.  
  
### <a name="errors-and-exceptions"></a>오류 및 예외  
  
-   비동기 작업에서 발생하는 모든 예외를 catch하고 <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A?displayProperty=nameWithType> 속성 값을 해당 예외로 설정합니다.  
  
### <a name="threading-and-contexts"></a>스레딩 및 컨텍스트  
 클래스가 올바로 작동하도록 하려면 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 및 Windows Forms 응용 프로그램을 비롯한 지정된 응용 프로그램 모델에 대해 올바른 스레드 또는 컨텍스트에서 클라이언트의 이벤트 처리기가 호출되도록 해야 합니다. 모든 응용 프로그램 모델에서 비동기 클래스가 올바르게 동작하도록 하기 위해 두 개의 중요한 도우미 클래스인 <xref:System.ComponentModel.AsyncOperation> 및 <xref:System.ComponentModel.AsyncOperationManager>가 제공됩니다.  
  
 <xref:System.ComponentModel.AsyncOperationManager>는 <xref:System.ComponentModel.AsyncOperationManager.CreateOperation%2A>을 반환하는 하나의 메서드 <xref:System.ComponentModel.AsyncOperation>을 제공합니다. <em>MethodName</em>**Async** 메서드는 <xref:System.ComponentModel.AsyncOperationManager.CreateOperation%2A>을 호출하고 클래스는 반환된 <xref:System.ComponentModel.AsyncOperation>을 사용하여 비동기 작업의 수명을 추적합니다.  
  
 클라이언트에 진행률, 증분 결과 및 완료를 보고하려면 <xref:System.ComponentModel.AsyncOperation.Post%2A>에 대해 <xref:System.ComponentModel.AsyncOperation.OperationCompleted%2A> 및 <xref:System.ComponentModel.AsyncOperation> 메서드를 호출합니다. <xref:System.ComponentModel.AsyncOperation>은 클라이언트의 이벤트 처리기에 대한 호출을 올바른 스레드 또는 컨텍스트로 마샬링하는 작업을 담당합니다.  
  
> [!NOTE]
>  명시적으로 응용 프로그램 모델의 정책에 반대하되 이벤트 기반 비동기 패턴 사용의 다른 이점을 이용하려는 경우 이러한 규칙을 피해 갈 수 있습니다. 예를 들어, Windows Forms에서 작동하는 클래스가 자유 스레드가 되도록 할 수 있습니다. 개발자가 암시된 제한 사항을 이해하는 한 자유 스레드 클래스를 만들 수 있습니다. 콘솔 응용 프로그램은 <xref:System.ComponentModel.AsyncOperation.Post%2A> 호출 실행을 동기화하지 않습니다. 이로 인해 `ProgressChanged` 이벤트가 잘못 발생할 수 있습니다. <xref:System.ComponentModel.AsyncOperation.Post%2A> 호출이 serialize되어 실행되도록 하려면 <xref:System.Threading.SynchronizationContext?displayProperty=nameWithType> 클래스를 구현하여 설치합니다.  
  
 <xref:System.ComponentModel.AsyncOperation> 및 <xref:System.ComponentModel.AsyncOperationManager>를 사용하여 비동기 작업을 사용하도록 설정하는 방법에 대한 자세한 내용은 [방법: 이벤트 기반 비동기 패턴을 지원하는 구성 요소 구현](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)을 참조하세요.  
  
## <a name="guidelines"></a>지침  
  
-   이상적으로는 각 메서드 호출이 다른 메서드 호출과 별개여야 합니다. 호출을 공유 리소스와 결합하는 것을 피해야 합니다. 리소스가 호출 간에 공유되는 경우 구현에 적절한 동기화 메커니즘을 제공해야 합니다.  
  
-   클라이언트가 동기화를 구현해야 하는 디자인은 사용하지 않는 것이 좋습니다. 예를 들어, 전역 정적 개체를 매개 변수로 받는 비동기 메서드가 있을 수 있습니다. 이러한 메서드의 여러 동시 호출로 인해 데이터 손상이나 교착 상태가 발생할 수 있습니다.  
  
-   여러 호출 오버로드로 메서드를 구현하는 경우(시그니처에 `userState`가 있음) 클래스가 사용자 상태 또는 작업 ID 및 해당 보류 중인 작업의 컬렉션을 관리해야 합니다. 다양한 호출에서 컬렉션에 `lock` 개체를 추가 및 제거하므로 이 컬렉션은 `userState` 영역으로 보호해야 합니다.  
  
-   실현 가능하고 적절한 경우 `CompletedEventArgs` 클래스 재사용을 고려하세요. 이 경우 지정된 대리자 및 <xref:System.EventArgs> 형식이 단일 메서드에 연결된 것이 아니므로 명명이 메서드 이름과 일치하지 않습니다. 그러나 개발자가 <xref:System.EventArgs>에 대한 속성에서 검색된 값을 강제로 캐스팅하도록 하는 것은 절대 허용되지 않습니다.  
  
-   <xref:System.ComponentModel.Component>에서 파생되는 클래스를 작성하는 경우 고유한 <xref:System.Threading.SynchronizationContext> 클래스를 구현하여 설치하지 마세요. 구성 요소가 아니라 응용 프로그램 모델이 사용되는 <xref:System.Threading.SynchronizationContext>를 제어합니다.  
  
-   모든 종류의 다중 스레딩을 사용할 때는 매우 심각하고 복잡한 버그에 잠재적으로 노출됩니다. 다중 스레딩을 사용하는 솔루션을 구현하기 전에 [관리되는 스레딩을 구현하는 최선의 방법](../../../docs/standard/threading/managed-threading-best-practices.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.ComponentModel.AsyncOperation>  
- <xref:System.ComponentModel.AsyncOperationManager>  
- <xref:System.ComponentModel.AsyncCompletedEventArgs>  
- <xref:System.ComponentModel.ProgressChangedEventArgs>  
- <xref:System.ComponentModel.BackgroundWorker>  
- [이벤트 기반 비동기 패턴 구현](../../../docs/standard/asynchronous-programming-patterns/implementing-the-event-based-asynchronous-pattern.md)  
- [EAP(이벤트 기반 비동기 패턴)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)  
- [이벤트 기반 비동기 패턴 구현 시기 결정](../../../docs/standard/asynchronous-programming-patterns/deciding-when-to-implement-the-event-based-asynchronous-pattern.md)  
- [최선의 이벤트 기반 비동기 패턴 구현 방법](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)  
- [방법: 이벤트 기반 비동기 패턴을 지원하는 구성 요소 사용](../../../docs/standard/asynchronous-programming-patterns/how-to-use-components-that-support-the-event-based-asynchronous-pattern.md)  
- [방법: 이벤트 기반 비동기 패턴을 지원하는 구성 요소 구현](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)
