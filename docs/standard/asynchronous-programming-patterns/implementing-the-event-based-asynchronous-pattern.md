---
title: 이벤트 기반 비동기 패턴 구현
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
- components [.NET Framework], asynchronous
- AsyncOperation class
- AsyncCompletedEventArgs class
ms.assetid: 43402d19-8d30-426d-8785-1a4478233bfa
ms.openlocfilehash: 3cb38cd9d7b27ab28b602e4e4c813d58d904abd3
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48584249"
---
# <a name="implementing-the-event-based-asynchronous-pattern"></a>이벤트 기반 비동기 패턴 구현
상당한 지연을 일으킬 수 있는 몇 가지 작업을 사용하여 클래스를 작성하는 경우 [이벤트 기반 비동기 패턴 개요](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)를 구현하여 비동기 기능을 부여하는 것을 고려할 수 있습니다.  
  
 이벤트 기반 비동기 패턴은 비동기 기능을 포함하는 클래스를 패키지하는 표준화된 방법을 제공합니다. <xref:System.ComponentModel.AsyncOperationManager>와 같은 도우미 클래스를 구현한 경우 클래스는 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)], 콘솔 응용 프로그램 및 Windows Forms 응용 프로그램을 비롯한 모든 응용 프로그램 모델에서 올바르게 작동합니다.  
  
 이벤트 기반 비동기 패턴을 구현하는 예제를 보려면 [방법: 이벤트 기반 비동기 패턴을 지원하는 구성 요소 구현](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)을 참조하세요.  
  
 간단한 비동기 작업의 경우 <xref:System.ComponentModel.BackgroundWorker> 구성 요소가 적합하다는 것을 알 수 있습니다. <xref:System.ComponentModel.BackgroundWorker>에 대한 자세한 내용은 [방법: 백그라운드에서 작업 실행](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)을 참조하세요.  
  
 다음 목록에서는 이 항목에서 설명하는 이벤트 기반 비동기 패턴의 기능에 대해 설명합니다.  
  
-   이벤트 기반 비동기 패턴 구현 기회  
  
-   비동기 메서드 명명  
  
-   선택적으로 취소 지원  
  
-   선택적으로 IsBusy 속성 지원  
  
-   선택적으로 진행률 보고 지원 제공  
  
-   선택적으로 증분 결과를 반환하기 위한 지원 제공  
  
-   메서드의 Out 및 Ref 매개 변수 처리  
  
## <a name="opportunities-for-implementing-the-event-based-asynchronous-pattern"></a>이벤트 기반 비동기 패턴 구현 기회  
 다음과 같은 경우에 이벤트 기반 비동기 패턴의 구현을 고려하세요.  
  
-   클래스의 클라이언트에 비동기 작업에 사용할 수 있는 <xref:System.Threading.WaitHandle> 및 <xref:System.IAsyncResult> 개체가 필요하지 않습니다. 즉, 폴링 및 <xref:System.Threading.WaitHandle.WaitAll%2A> 또는 <xref:System.Threading.WaitHandle.WaitAny%2A>가 클라이언트에서 빌드되어야 합니다.  
  
-   익숙한 이벤트/대리자 모델을 사용하여 클라이언트에서 비동기 작업이 관리되기를 원할 것입니다.  
  
 모든 작업은 비동기 구현의 후보가 될 수 있지만 긴 대기 시간을 발생시키는 작업을 비동기 방식으로 구현해야 합니다. 클라이언트가 메서드를 호출하며 추가 개입 없이도 완료 시 알림이 제공되는 작업이 특히 적합할 것입니다. 또한 연속적으로 실행되고, 클라이언트에 주기적으로 진행 상황, 증분 결과 또는 상태 변경을 알리는 작업이 적합할 것입니다.  
  
 이벤트 기반 비동기 패턴을 지원해야 하는 경우를 결정하는 방법에 대한 자세한 내용은 [이벤트 기반 비동기 패턴 구현 시기 결정](../../../docs/standard/asynchronous-programming-patterns/deciding-when-to-implement-the-event-based-asynchronous-pattern.md)을 참조하세요.  
  
## <a name="naming-asynchronous-methods"></a>비동기 메서드 명명  
 비동기 메서드를 제공하려는 각 동기 메서드 *MethodName*에 대해 다음을 수행합니다.  
  
 다음 작업을 수행하는 _MethodName_**Async** 메서드를 정의합니다.  
  
-   `void`를 반환합니다.  
  
-   *MethodName* 메서드와 동일한 매개 변수를 사용합니다.  
  
-   여러 호출을 허용합니다.  
  
 필요에 따라 _MethodName_**Async**와 동일하지만 `userState`라는 추가 개체 값 매개 변수가 있는 _MethodName_**Async** 오버로드를 정의합니다. 메서드의 여러 동시 호출을 관리할 준비가 되었으면 이 작업을 수행합니다. 그러면 메서드 호출을 구분하기 위해 모든 이벤트 처리기에 `userState` 값이 다시 전달됩니다. 나중에 검색할 수 있게 사용자 상태를 저장하기 위한 장소로 이 작업을 수행하도록 선택할 수도 있습니다.  
  
 별개의 각 _MethodName_**Async** 메서드 시그니처에 대해 다음을 수행합니다.  
  
1.  해당 메서드와 같은 클래스에서 다음 이벤트를 정의합니다.  
  
    ```vb  
    Public Event MethodNameCompleted As MethodNameCompletedEventHandler  
    ```  
  
    ```csharp  
    public event MethodNameCompletedEventHandler MethodNameCompleted;  
    ```  
  
2.  다음 대리자 및 <xref:System.ComponentModel.AsyncCompletedEventArgs>를 정의합니다. 이러한 항목은 클래스 자체의 외부이면서 동일한 네임스페이스에서 정의될 수 있습니다.  
  
    ```vb  
    Public Delegate Sub MethodNameCompletedEventHandler( _  
        ByVal sender As Object, _  
        ByVal e As MethodNameCompletedEventArgs)  
  
    Public Class MethodNameCompletedEventArgs  
        Inherits System.ComponentModel.AsyncCompletedEventArgs  
    Public ReadOnly Property Result() As MyReturnType  
    End Property  
    ```  
  
    ```csharp  
    public delegate void MethodNameCompletedEventHandler(object sender,   
        MethodNameCompletedEventArgs e);  
  
    public class MethodNameCompletedEventArgs : System.ComponentModel.AsyncCompletedEventArgs  
    {  
        public MyReturnType Result { get; }  
    }  
    ```  
  
    -   필드에서는 데이터 바인딩이 불가능하므로 _MethodName_**CompletedEventArgs** 클래스가 해당 멤버를 필드가 아닌 읽기 전용 속성으로 노출하도록 합니다.  
  
    -   결과를 생성하지 않는 메서드에 대해서는 어떤 <xref:System.ComponentModel.AsyncCompletedEventArgs> 파생 클래스도 정의하지 마세요. <xref:System.ComponentModel.AsyncCompletedEventArgs> 자체의 인스턴스를 사용하세요.  
  
        > [!NOTE]
        >  적절한 경우 대리자 및 <xref:System.ComponentModel.AsyncCompletedEventArgs> 형식을 얼마든지 다시 사용할 수 있습니다. 이 경우 지정된 대리자 및 <xref:System.ComponentModel.AsyncCompletedEventArgs>가 단일 메서드에 연결되지 않으므로 해당 명명 체계가 메서드 이름과 일치하지 않게 됩니다.  
  
## <a name="optionally-support-cancellation"></a>선택적으로 취소 지원  
 클래스가 비동기 작업 취소를 지원하는 경우 아래 설명된 대로 취소가 클라이언트에 노출되어야 합니다. 취소 지원을 정의하기 전에 도달해야 하는 두 가지 의사 결정 지점이 있습니다.  
  
-   예상되는 추가 항목을 포함하여 클래스에 취소를 지원하는 비동기 작업이 하나만 포함되나요?  
  
-   취소를 지원하는 비동기 작업이 보류 중인 여러 작업을 취소할 수 있나요? 즉, _MethodName_**Async** 메서드가 `userState` 매개 변수를 사용하며 하나의 호출이 끝나기를 기다리지 않고 여러 번 호출할 수 있도록 허용하나요?  
  
 아래 표에 나오는 이러한 두 가지 질문에 대한 답변을 사용하여 취소 메서드의 시그니처를 확인하세요.  
  
### <a name="visual-basic"></a>Visual Basic  
  
||다중 동시 작업 지원|한 번에 하나의 작업|  
|------|------------------------------------------------|----------------------------------|  
|전체 클래스에서 단일 비동기 작업|`Sub MethodNameAsyncCancel(ByVal userState As Object)`|`Sub MethodNameAsyncCancel()`|  
|클래스의 여러 비동기 작업|`Sub CancelAsync(ByVal userState As Object)`|`Sub CancelAsync()`|  
  
### <a name="c"></a>C#  
  
||다중 동시 작업 지원|한 번에 하나의 작업|  
|------|------------------------------------------------|----------------------------------|  
|전체 클래스에서 단일 비동기 작업|`void MethodNameAsyncCancel(object userState);`|`void MethodNameAsyncCancel();`|  
|클래스의 여러 비동기 작업|`void CancelAsync(object userState);`|`void CancelAsync();`|  
  
 `CancelAsync(object userState)` 메서드를 정의하는 경우 클라이언트는 단일 비동기 메서드의 모든 호출 간에서 뿐만 아니라 개체에 대해 호출된 모든 비동기 메서드 간을 구분할 수 있도록 하는 상태 값을 선택할 때 주의해야 합니다.  
  
 Visual Studio의 IntelliSense와 같은 디자인 환경에서 메서드를 보다 쉽게 검색할 수 있도록 하기 위해 단일 비동기 작업 버전을 _MethodName_**AsyncCancel**로 명명하고 있습니다. 이렇게 하면 관련된 멤버가 그룹화되고 비동기 기능과 관련이 없는 다른 멤버에서 구분될 수 있습니다. 후속 버전에 추가되는 비동기 작업이 있을 수 있다고 예상될 경우 `CancelAsync`를 정의하는 것이 더 바람직합니다.  
  
 위 표의 여러 메서드를 같은 클래스에는 정의하지 마세요. 그렇게 하는 것은 의미가 없으며 메서드가 증가하면 클래스 인터페이스만 복잡해집니다.  
  
 이러한 메서드는 일반적으로 즉시 반환되며 작업이 실제로 취소될 수도 있고 그렇지 않을 수도 있습니다. _MethodName_**Completed** 이벤트에 대한 이벤트 처리기에서 _MethodName_**CompletedEventArgs** 개체는 클라이언트가 취소 발생 여부를 확인하는 데 사용할 수 있는 `Cancelled` 필드를 포함합니다.  
  
 [최선의 이벤트 기반 비동기 패턴 구현 방법](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)에 설명된 취소 의미 체계를 준수하세요.  
  
## <a name="optionally-support-the-isbusy-property"></a>선택적으로 IsBusy 속성 지원  
 클래스가 여러 동시 호출을 지원하지 않으면 `IsBusy` 속성 노출을 고려합니다. 이 방법을 사용하면 개발자들은 _MethodName_**Async** 메서드에서 예외를 catch하지 않고도 _MethodName_**Async** 메서드가 실행 중인지 여부를 확인할 수 있습니다.  
  
 [최선의 이벤트 기반 비동기 패턴 구현 방법](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)에 설명된 `IsBusy` 의미 체계를 준수하세요.  
  
## <a name="optionally-provide-support-for-progress-reporting"></a>선택적으로 진행률 보고 지원 제공  
 일반적으로 비동기 작업이 작업 중에 진행률을 보고하는 것이 유용할 수 있습니다. 이벤트 기반 비동기 패턴은 이러한 작업에 대한 지침을 제공합니다.  
  
-   필요에 따라 비동기 작업에서 발생되고 적절한 스레드에 대해 호출될 이벤트를 정의합니다. <xref:System.ComponentModel.ProgressChangedEventArgs> 개체는 0에서 100 사이여야 하는 정수 값 진행률 표시기를 제공합니다.  
  
-   다음과 같이 이벤트에 이름을 지정합니다.  
  
    -   `ProgressChanged`: 클래스에 비동기 작업이 여러 개 있는 경우(또는 이후 버전에서 여러 비동기 작업을 포함하도록 확장될 예정임)  
  
    -   _MethodName_**ProgressChanged**: 클래스에 비동기 작업이 하나만 있는 경우.  
  
     이 명명 옵션은 선택적으로 취소 지원 섹션에 설명된 대로 취소 메서드의 경우와 비슷합니다.  
  
 이 이벤트는 <xref:System.ComponentModel.ProgressChangedEventHandler> 대리자 시그니처와 <xref:System.ComponentModel.ProgressChangedEventArgs> 클래스를 사용해야 합니다. 또는 추가 도메인 관련 진행률 표시기를 제공할 수 있는 경우(예를 들어 다운로드 작업에 대해 읽은 바이트 수 및 총 바이트 수) <xref:System.ComponentModel.ProgressChangedEventArgs>의 파생 클래스를 정의해야 합니다.  
  
 클래스가 지원하는 비동기 메서드의 수와 관계없이 해당 클래스에 대한 `ProgressChanged` or _MethodName_**ProgressChanged** 이벤트는 하나만 있습니다. 클라이언트는 여러 동시 작업에 대한 진행률 업데이트 내용을 구분하기 위해 _MethodName_**Async** 메서드에 전달되는 `userState` 개체를 사용하게 됩니다.  
  
 여러 작업이 진행률을 지원하고 각각이 다른 진행률 표시기를 반환하는 경우가 있을 수 있습니다. 이 경우 단일 `ProgressChanged` 이벤트로는 적절하지 않으며 여러 `ProgressChanged` 이벤트를 지원하는 것을 고려하세요. 이 경우 각 _MethodName_**Async** 메서드에 대해 _MethodName_**ProgressChanged** 명명 패턴을 사용하세요.  
  
 [최선의 이벤트 기반 비동기 패턴 구현 방법](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)에 설명된 진행률 보고 의미 체계를 준수하세요.  
  
## <a name="optionally-provide-support-for-returning-incremental-results"></a>선택적으로 증분 결과를 반환하기 위한 지원 제공  
 경우에 따라 비동기 작업이 완료되기 전에 증분 결과를 반환할 수 있습니다. 이 시나리오를 지원하는 데 사용할 수 있는 옵션에는 여러 가지가 있습니다. 몇 가지 예제는 다음과 같습니다.  
  
### <a name="single-operation-class"></a>단일 작업 클래스  
 클래스가 단일 비동기 작업만 지원하며 해당 작업이 증분 결과를 반환할 수 있으면 다음을 수행합니다.  
  
-   증분 결과 데이터를 전달하도록 <xref:System.ComponentModel.ProgressChangedEventArgs> 형식을 확장하고 확장된 데이터로 _MethodName_**ProgressChanged** 이벤트를 정의합니다.  
  
-   보고할 증분 결과가 있을 때 이 _MethodName_**ProgressChanged** 이벤트를 발생시킵니다.  
  
 이 솔루션은 _MethodName_**ProgressChanged** 이벤트처럼 “모든 작업”에 대한 증분 결과를 반환하기 위해 동일한 이벤트가 발생하는 문제가 없으므로 단일 비동기 작업 클래스에 특수하게 적용됩니다.  
  
### <a name="multiple-operation-class-with-homogeneous-incremental-results"></a>유형이 같은 증분 결과를 갖는 다중 작업 클래스  
 이 경우 클래스는 각각이 증분 결과를 반환할 수 있는 여러 비동기 메서드를 지원하며 이러한 모든 증분 결과가 모두 동일한 형식의 데이터를 갖습니다.  
  
 모든 증분 결과에 동일한 <xref:System.EventArgs> 구조체가 작동하므로 단일 작업 클래스에 대해 위에서 설명된 모델을 따릅니다. _MethodName_**ProgressChanged** 이벤트 대신 다중 비동기 메서드에 적용되는 `ProgressChanged` 이벤트를 정의합니다.  
  
### <a name="multiple-operation-class-with-heterogeneous-incremental-results"></a>유형이 다른 증분 결과를 갖는 다중 작업 클래스  
 클래스가 각각이 다른 데이터 형식을 반환하는 여러 비동기 메서드를 지원하는 경우 다음을 수행해야 합니다.  
  
-   진행률 보고에서 증분 결과 보고를 구분합니다.  
  
-   각 비동기 메서드가 해당 메서드의 증분 결과 데이터를 처리할 수 있도록 적절한 <xref:System.EventArgs>를 사용하여 별도의 _MethodName_**ProgressChanged** 이벤트를 정의합니다.  
  
 [최선의 이벤트 기반 비동기 패턴 구현 방법](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)에 설명된 대로 적절한 스레드에서 해당 이벤트 처리기를 호출합니다.  
  
## <a name="handling-out-and-ref-parameters-in-methods"></a>메서드의 Out 및 Ref 매개 변수 처리  
 일반적으로 `out` 및 `ref`의 사용이 .NET Framework에서는 권장되지 않지만 이러한 매개 변수가 있을 때 따라야 하는 규칙은 다음과 같습니다.  
  
 동기 메서드를 *MethodName*으로 명명한 경우:  
  
-   *MethodName*에 대한 `out` 매개 변수는 _MethodName_**Async**에 속하지 않아야 합니다. 좀 더 적절한 이름이 없는 경우 *MethodName*의 동일한 매개 변수와 이름이 같은 _MethodName_**CompletedEventArgs**에 속해야 합니다.  
  
-   *MethodName*에 대한 `ref` 매개 변수가 _MethodName_**Async**에 속해야 하고 좀 더 적절한 이름이 없는 경우 *MethodName*의 동일한 매개 변수와 이름이 같은 _MethodName_**CompletedEventArgs**에 속해야 합니다.  
  
 예를 들어 다음이 지정될 경우  
  
```vb  
Public Function MethodName(ByVal arg1 As String, ByRef arg2 As String, ByRef arg3 As String) As Integer  
```  
  
```csharp  
public int MethodName(string arg1, ref string arg2, out string arg3);  
```  
  
 비동기 메서드 및 해당 <xref:System.ComponentModel.AsyncCompletedEventArgs> 클래스는 다음과 같습니다.  
  
```vb  
Public Sub MethodNameAsync(ByVal arg1 As String, ByVal arg2 As String)  
  
Public Class MethodNameCompletedEventArgs  
    Inherits System.ComponentModel.AsyncCompletedEventArgs  
    Public ReadOnly Property Result() As Integer   
    End Property  
    Public ReadOnly Property Arg2() As String   
    End Property  
    Public ReadOnly Property Arg3() As String   
    End Property  
End Class  
```  
  
```csharp  
public void MethodNameAsync(string arg1, string arg2);  
  
public class MethodNameCompletedEventArgs : System.ComponentModel.AsyncCompletedEventArgs  
{  
    public int Result { get; };  
    public string Arg2 { get; };  
    public string Arg3 { get; };  
}  
```  
  
## <a name="see-also"></a>참고 항목

- <xref:System.ComponentModel.ProgressChangedEventArgs>  
- <xref:System.ComponentModel.AsyncCompletedEventArgs>  
- [방법: 이벤트 기반 비동기 패턴을 지원하는 구성 요소 구현](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)  
- [방법: 백그라운드에서 작업 실행](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)  
- [방법: 배경 작업을 사용하는 양식 구현](../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)  
- [이벤트 기반 비동기 패턴 구현 시기 결정](../../../docs/standard/asynchronous-programming-patterns/deciding-when-to-implement-the-event-based-asynchronous-pattern.md)  
- [최선의 이벤트 기반 비동기 패턴 구현 방법](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)  
- [EAP(이벤트 기반 비동기 패턴)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)  
