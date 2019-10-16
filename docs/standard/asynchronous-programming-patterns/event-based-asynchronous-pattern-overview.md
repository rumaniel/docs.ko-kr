---
title: 이벤트 기반 비동기 패턴 개요
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET Framework], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET Framework], asynchronous features
- AsyncOperation class
- AsyncCompletedEventArgs class
ms.assetid: 792aa8da-918b-458e-b154-9836b97735f3
ms.openlocfilehash: 05b5ab19c5206395ab138465eccf2035b5cebe3e
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046480"
---
# <a name="event-based-asynchronous-pattern-overview"></a>이벤트 기반 비동기 패턴 개요
많은 작업을 동시에 수행하면서 사용자 상호 작용에 대해 응답성을 유지하는 애플리케이션에는 일반적으로 여러 스레드를 사용하는 디자인이 필요합니다. <xref:System.Threading> 네임스페이스는 고성능 다중 스레드 애플리케이션을 만드는 데 필요한 모든 도구를 제공하지만 이러한 도구를 효과적으로 사용하려면 다중 스레드 소프트웨어 엔지니어링에 대한 풍부한 경험이 필요합니다. 비교적 단순한 다중 스레드 애플리케이션의 경우 <xref:System.ComponentModel.BackgroundWorker> 구성 요소가 간단한 솔루션을 제공합니다. 보다 정교한 비동기 애플리케이션의 경우 이벤트 기반 비동기 패턴을 준수하는 클래스 구현을 고려하세요.  
  
 이벤트 기반 비동기 패턴은 다중 스레드 디자인에 본질적으로 존재하는 복잡한 여러 가지 문제를 숨기면서 다중 스레드 애플리케이션의 장점을 이용할 수 있게 해줍니다. 이 패턴을 지원하는 클래스를 사용하면 다음이 가능합니다.  
  
- 애플리케이션을 중단하지 않고 &quot;백그라운드에서&quot; 다운로드 및 데이터베이스 작업과 같은 시간이 많이 걸리는 작업을 수행할 수 있습니다.  
  
- 여러 작업을 동시에 실행하고 각 작업이 완료되면 알림을 받을 수 있습니다.  
  
- 애플리케이션을 중지("차단")하지 않고 리소스가 사용 가능해질 때까지 기다릴 수 있습니다.  
  
- 익숙한 이벤트-대리자 모델을 사용하여 보류 중인 비동기 작업과 통신할 수 있습니다. 이벤트 처리기 및 대리자 사용에 대한 자세한 내용은 [이벤트](../../../docs/standard/events/index.md)를 참조하세요.  
  
 이벤트 기반 비동기 패턴을 지원하는 클래스는 _MethodName_**Async**라는 메서드를 하나 이상 포함합니다. 이러한 메서드는 현재 스레드에서 동일한 작업을 수행하는 동기 버전을 미러링할 수 있습니다. 또한 이 클래스에는 _MethodName_**Completed** 이벤트가 있을 수 있고 _MethodName_**AsyncCancel** 메서드가 있거나 단순히 **CancelAsync** 메서드가 있을 수 있습니다.  
  
 <xref:System.Windows.Forms.PictureBox>는 이벤트 기반 비동기 패턴을 지원하는 일반적인 구성 요소입니다. 해당 <xref:System.Windows.Forms.PictureBox.Load%2A> 메서드를 호출하여 이미지를 동기적으로 다운로드할 수 있지만 이미지가 크거나 네트워크 연결이 느린 경우 다운로드 작업이 완료되고 <xref:System.Windows.Forms.PictureBox.Load%2A>에 대한 호출이 반환될 때까지 애플리케이션이 응답을 중지합니다.  
  
 이미지가 로드되는 동안 애플리케이션이 계속 실행되도록 하려면 <xref:System.Windows.Forms.PictureBox.LoadAsync%2A> 메서드를 호출하고 다른 모든 이벤트를 처리하는 것처럼 <xref:System.Windows.Forms.PictureBox.LoadCompleted> 이벤트를 처리하면 됩니다. <xref:System.Windows.Forms.PictureBox.LoadAsync%2A> 메서드를 호출하면 별도의 스레드에서(&quot;백그라운드에서&quot;) 다운로드가 진행되는 동안 애플리케이션이 계속 실행됩니다. 이미지 로드 작업이 완료되면 이벤트 처리기가 호출되고, 이벤트 처리기는 <xref:System.ComponentModel.AsyncCompletedEventArgs> 매개 변수를 검토하여 다운로드가 성공적으로 완료되었는지 확인할 수 있습니다.  
  
 이벤트 기반 비동기 패턴을 사용하려면 비동기 작업을 취소할 수 있어야 하며, <xref:System.Windows.Forms.PictureBox> 컨트롤이 해당 <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> 메서드에 대해 이 요구 사항을 지원해야 합니다. <xref:System.Windows.Forms.PictureBox.CancelAsync%2A>를 호출하면 보류 중인 다운로드를 중지하기 위한 요청이 전송되고, 작업이 취소되면 <xref:System.Windows.Forms.PictureBox.LoadCompleted> 이벤트가 발생합니다.  
  
> [!CAUTION]
> 다운로드가 <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> 요청이 수행된 것처럼 완료될 수 있으므로 <xref:System.ComponentModel.AsyncCompletedEventArgs.Cancelled%2A>가 취소 요청을 반영하지 않을 수 있습니다. 이를 ‘경합 상태’라고 하며, 이는 다중 스레드 프로그래밍에서 일반적인 문제입니다.  다중 스레드 프로그래밍 문제에 대한 자세한 내용은 [관리되는 스레딩을 구현하는 최선의 방법](../../../docs/standard/threading/managed-threading-best-practices.md)을 참조하세요.  
  
## <a name="characteristics-of-the-event-based-asynchronous-pattern"></a>이벤트 기반 비동기 패턴의 특징  
 이벤트 기반 비동기 패턴은 특정 클래스에서 지원하는 작업의 복잡성에 따라 여러 가지 형식을 취할 수 있습니다. 가장 단순한 클래스는 단일 _MethodName_**Async** 메서드 및 해당 _MethodName_**Completed** 이벤트를 포함할 수 있습니다. 더 복잡한 클래스는 여러 _MethodName_**Async** 메서드, 각 해당 _MethodName_**Completed** 이벤트 및 이러한 메서드의 동기 버전을 포함할 수 있습니다. 클래스는 선택적으로 각 비동기 메서드에 대해 취소, 진행률 보고 및 증분 결과를 지원할 수 있습니다.  
  
 또한 비동기 메서드는 보류 중인 여러 호출(여러 동시 호출)을 지원하여 비동기 메서드가 보류 중인 다른 작업을 완료하기 전에 코드에서 비동기 메서드를 원하는 만큼 호출할 수 있습니다. 이 상황을 올바르게 처리하기 위해서는 애플리케이션이 각 작업의 완료를 추적해야 할 수 있습니다.  
  
### <a name="examples-of-the-event-based-asynchronous-pattern"></a>이벤트 기반 비동기 패턴의 예  
 <xref:System.Media.SoundPlayer> 및 <xref:System.Windows.Forms.PictureBox> 구성 요소는 이벤트 기반 비동기 패턴의 간단한 구현을 나타냅니다. <xref:System.Net.WebClient> 및 <xref:System.ComponentModel.BackgroundWorker> 구성 요소는 이벤트 기반 비동기 패턴의 보다 복잡한 구현을 나타냅니다.  
  
 다음은 이러한 패턴을 준수하는 클래스 선언의 예입니다.  
  
```vb  
Public Class AsyncExample  
    ' Synchronous methods.  
    Public Function Method1(ByVal param As String) As Integer   
    Public Sub Method2(ByVal param As Double)   
  
    ' Asynchronous methods.  
    Overloads Public Sub Method1Async(ByVal param As String)   
    Overloads Public Sub Method1Async(ByVal param As String, ByVal userState As Object)   
    Public Event Method1Completed As Method1CompletedEventHandler  
  
    Overloads Public Sub Method2Async(ByVal param As Double)   
    Overloads Public Sub Method2Async(ByVal param As Double, ByVal userState As Object)   
    Public Event Method2Completed As Method2CompletedEventHandler  
  
    Public Sub CancelAsync(ByVal userState As Object)   
  
    Public ReadOnly Property IsBusy () As Boolean  
  
    ' Class implementation not shown.  
End Class  
```  
  
```csharp  
public class AsyncExample  
{  
    // Synchronous methods.  
    public int Method1(string param);  
    public void Method2(double param);  
  
    // Asynchronous methods.  
    public void Method1Async(string param);  
    public void Method1Async(string param, object userState);  
    public event Method1CompletedEventHandler Method1Completed;  
  
    public void Method2Async(double param);  
    public void Method2Async(double param, object userState);  
    public event Method2CompletedEventHandler Method2Completed;  
  
    public void CancelAsync(object userState);  
  
    public bool IsBusy { get; }  
  
    // Class implementation not shown.  
}  
```  
  
 가상의 `AsyncExample` 클래스에는 두 개의 메서드가 있는데, 이러한 두 메서드는 둘 다 동기 및 비동기 호출을 지원합니다. 동기 오버로드는 임의의 메서드 호출처럼 동작하고 호출 스레드에 대한 작업을 실행합니다. 작업에 시간이 많이 걸리는 경우 호출이 반환되기 전에 현저한 지연이 있을 수 있습니다. 비동기 오버로드는 다른 스레드에 대한 작업을 시작한 다음 즉시 반환되어 작업이 "백그라운드에서" 실행되는 동안 호출 스레드가 계속될 수 있도록 합니다.  
  
### <a name="asynchronous-method-overloads"></a>비동기 메서드 오버로드  
 비동기 작업에 대해서는 잠재적으로 두 오버로드 즉, 단일 호출과 다중 호출이 있습니다. 이러한 두 가지 형식은 해당 메서드 시그니처로 구별할 수 있습니다. 다중 호출 형식에는 `userState`라는 추가 매개 변수가 있습니다. 이 형식을 사용하면 코드에서 보류 중인 비동기 작업이 완료될 때까지 기다리지 않고 `Method1Async(string param, object userState)`를 여러 번 호출할 수 있습니다. 반면에 이전 호출이 완료되기 전에 `Method1Async(string param)`을 호출하려고 하면 메서드에 <xref:System.InvalidOperationException>이 발생합니다.  
  
 다중 호출 오버로드의 `userState` 매개 변수를 사용하면 비동기 작업 간에 구별할 수 있습니다. `Method1Async(string param, object userState)`에 대한 각 호출에 고유한 값(예: GUID 또는 해시 코드)을 제공하고, 각 작업이 완료되면 이벤트 처리기가 완료 이벤트가 발생한 작업 인스턴스를 확인할 수 있습니다.  
  
### <a name="tracking-pending-operations"></a>보류 중인 작업 추적  
 다중 호출 오버로드를 사용하는 경우 코드에서 보류 중인 작업의 `userState` 개체(작업 ID)를 추적해야 합니다. `Method1Async(string param, object userState)`에 대한 각 호출에 대해 일반적으로 새 고유 `userState` 개체를 생성하여 컬렉션에 추가합니다. 이 `userState` 개체에 해당하는 작업에서 완료 이벤트가 발생하면 완료 메서드 구현에서 <xref:System.ComponentModel.AsyncCompletedEventArgs.UserState%2A?displayProperty=nameWithType>를 검토하고 컬렉션에서 제거합니다. 이 방법을 사용할 경우 `userState` 매개 변수는 작업 ID 역할을 합니다.  
  
> [!NOTE]
> 호출에서 `userState`의 고유한 값을 다중 호출 오버로드에 제공할 때는 주의해야 합니다. 고유하지 않은 작업 ID를 사용할 경우 비동기 클래스에서 <xref:System.ArgumentException>이 throw됩니다.  
  
### <a name="canceling-pending-operations"></a>보류 중인 작업 취소  
 비동기 작업이 완료되기 전에 언제든지 해당 작업을 취소할 수 있어야 합니다. 이벤트 기반 비동기 패턴을 구현하는 클래스는 `CancelAsync` 메서드(비동기 메서드가 하나뿐인 경우) 또는 _MethodName_**AsyncCancel** 메서드(여러 비동기 메서드가 있는 경우)를 포함합니다.  
  
 여러 호출을 허용하는 메서드는 각 작업의 수명을 추적하는 데 사용될 수 있는 `userState` 매개 변수를 사용합니다. `CancelAsync`는 보류 중인 특정 작업을 취소할 수 있게 해주는 `userState` 매개 변수를 사용합니다.  
  
 보류 중인 작업을 한 번에 하나만 지원하는 메서드(예: `Method1Async(string param)`)는 취소할 수 없습니다.  
  
### <a name="receiving-progress-updates-and-incremental-results"></a>진행률 업데이트 및 증분 결과 받기  
 이벤트 기반 비동기 패턴을 준수하는 클래스는 진행률 및 증분 결과를 추적하기 위한 이벤트를 선택적으로 제공할 수 있습니다. 일반적으로 이 이벤트는 `ProgressChanged` 또는 _MethodName_**ProgressChanged**로 명명되며, 해당 이벤트 처리기가 <xref:System.ComponentModel.ProgressChangedEventArgs> 매개 변수를 사용합니다.  
  
 `ProgressChanged`이벤트의 이벤트 처리기는 <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A?displayProperty=nameWithType> 속성을 검토하여 완료된 비동기 작업의 백분율을 확인할 수 있습니다. 이 속성은 범위가 0~100이며, <xref:System.Windows.Forms.ProgressBar.Value%2A>의 <xref:System.Windows.Forms.ProgressBar> 속성을 업데이트하는 데 사용될 수 있습니다. 보류 중인 비동기 작업이 여러 개인 경우 <xref:System.ComponentModel.ProgressChangedEventArgs.UserState%2A?displayProperty=nameWithType> 속성을 사용하여 진행률을 보고 중인 작업을 구별할 수 있습니다.  
  
 일부 클래스는 비동기 작업이 진행됨에 따라 증분 결과를 보고할 수 있습니다. 이러한 결과는 <xref:System.ComponentModel.ProgressChangedEventArgs>에서 파생되는 클래스에 저장되며 파생 클래스에 속성으로 나타납니다. `ProgressChanged` 속성에 액세스하는 것처럼 <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A> 이벤트의 이벤트 처리기에서 이러한 결과에 액세스할 수 있습니다. 보류 중인 비동기 작업이 여러 개인 경우 <xref:System.ComponentModel.ProgressChangedEventArgs.UserState%2A> 속성을 사용하여 증분 결과를 보고 중인 작업을 구별할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.ComponentModel.ProgressChangedEventArgs>
- <xref:System.ComponentModel.BackgroundWorker>
- <xref:System.ComponentModel.AsyncCompletedEventArgs>
- [방법: 이벤트 기반 비동기 패턴을 지원하는 구성 요소 사용](../../../docs/standard/asynchronous-programming-patterns/how-to-use-components-that-support-the-event-based-asynchronous-pattern.md)
- [방법: 백그라운드에서 작업 실행](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)
- [방법: 백그라운드 작업을 사용하는 양식 구현](../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)
- [EAP(이벤트 기반 비동기 패턴)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)
- [최선의 이벤트 기반 비동기 패턴 구현 방법](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)
- [이벤트 기반 비동기 패턴 구현 시기 결정](../../../docs/standard/asynchronous-programming-patterns/deciding-when-to-implement-the-event-based-asynchronous-pattern.md)
