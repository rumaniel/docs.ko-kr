---
title: '방법: 이벤트 기반 비동기 패턴을 지원하는 구성 요소 구현'
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
- threading [Windows Forms], asynchronous features
- AsyncCompletedEventArgs class
ms.assetid: 61f676b5-936f-40f6-83ce-f22805ec9c2f
ms.openlocfilehash: 44a1019ac8169138aa95b03e2027d9539cbf8391
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71957365"
---
# <a name="how-to-implement-a-component-that-supports-the-event-based-asynchronous-pattern"></a>방법: 이벤트 기반 비동기 패턴을 지원하는 구성 요소 구현
상당한 지연을 일으킬 수 있는 몇 가지 작업을 사용하여 클래스를 작성하는 경우 [이벤트 기반 비동기 패턴 개요](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)를 구현하여 비동기 기능을 부여하는 것을 고려할 수 있습니다.  
  
 이 연습에서는 이벤트 기반 비동기 패턴을 구현하는 구성 요소를 만드는 방법을 보여줍니다. ASP.NET, 콘솔 애플리케이션 및 Windows Forms 애플리케이션을 포함한 모든 애플리케이션 모델에서 구성 요소가 올바르게 작동하도록 하는 <xref:System.ComponentModel?displayProperty=nameWithType> 네임스페이스의 도우미 클래스를 사용하는 것이 좋습니다. 이 구성 요소도 <xref:System.Windows.Forms.PropertyGrid> 컨트롤과 고유한 사용자 지정 디자이너를 사용하여 디자인할 수 있습니다.  
  
 완료하면 소수를 비동기적으로 계산하는 애플리케이션이 생깁니다. 애플리케이션에는 기본 UI(사용자 인터페이스) 스레드 및 각 소수는 계산을 위한 스레드가 있습니다. 큰 숫자가 소수인지 테스트하는 데는 상당한 시간이 걸릴 수도 있지만 이 지연으로 기본 UI 스레드가 중단되지 않으며 계산 중에도 폼이 빠르게 응답하게 됩니다. 원하는 계산 수만큼 동시에 또는 선택적으로 취소 보류 계산을 실행할 수 있습니다.  
  
 이 연습에서 설명하는 작업은 다음과 같습니다.  
  
- 구성 요소 만들기  
  
- 공용 비동기 이벤트 및 대리자 정의  
  
- 전용 대리자 정의  
  
- 공용 이벤트 구현  
  
- 완료 메서드 구현  
  
- 작업자 메서드 구현  
  
- 시작 및 취소 메서드 구현  
  
 이 항목의 코드를 단일 목록으로 복사하려면 [방법: 이벤트 기반 비동기 패턴의 클라이언트 구현](../../../docs/standard/asynchronous-programming-patterns/how-to-implement-a-client-of-the-event-based-asynchronous-pattern.md)을 참조하세요.  
  
## <a name="creating-the-component"></a>구성 요소 만들기  
 첫 번째 단계는 이벤트 기반 비동기 패턴을 구현하는 구성 요소를 만드는 것입니다.  
  
### <a name="to-create-the-component"></a>구성 요소를 만들려면  
  
- <xref:System.ComponentModel.Component>에서 상속되는 `PrimeNumberCalculator`라는 클래스를 만듭니다.  
  
## <a name="defining-public-asynchronous-events-and-delegates"></a>공용 비동기 이벤트 및 대리자 정의  
 구성 요소는 이벤트를 사용하는 클라이언트와 통신합니다. _MethodName_**Completed** 이벤트는 클라이언트에 비동기 작업의 완료를 알리고 _MethodName_**ProgressChanged** 이벤트는 클라이언트에 비동기 작업의 진행률을 알립니다.  
  
### <a name="to-define-asynchronous-events-for-clients-of-your-component"></a>구성 요소의 클라이언트에 대한 비동기 이벤트를 정의하려면:  
  
1. <xref:System.Threading?displayProperty=nameWithType> 및 <xref:System.Collections.Specialized?displayProperty=nameWithType> 네임스페이스를 파일 맨 위로 가져옵니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#11](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#11)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#11](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#11)]  
  
2. `PrimeNumberCalculator` 클래스 정의 전에 진행률 및 완료 이벤트에 대한 대리자를 선언합니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#7](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#7)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#7](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#7)]  
  
3. `PrimeNumberCalculator` 클래스 정의에서 클라이언트에 진행률 및 완료를 보고하는 이벤트를 선언합니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#8](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#8)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#8](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#8)]  
  
4. `PrimeNumberCalculator` 클래스 정의 후 각 계산의 결과를 `CalculatePrimeCompleted`.event에 대한 클라이언트 이벤트 처리기에 보고하기 위해 `CalculatePrimeCompletedEventArgs` 클래스를 파생시킵니다. `AsyncCompletedEventArgs` 속성 외에도 이 클래스를 사용하면 클라이언트가 테스트된 숫자, 숫자가 소수인지 여부 및 소수가 아닌 경우 첫 번째 제수를 확인할 수 있습니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#6](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#6)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#6](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#6)]  
  
## <a name="checkpoint"></a>검사점  
 이때 구성 요소를 빌드할 수 있습니다.  
  
### <a name="to-test-your-component"></a>구성 요소를 테스트하려면  
  
- 구성 요소를 컴파일합니다.  
  
     두 개의 컴파일러 경고를 받게 됩니다.  
  
    ```console  
    warning CS0067: The event 'AsynchronousPatternExample.PrimeNumberCalculator.ProgressChanged' is never used  
    warning CS0067: The event 'AsynchronousPatternExample.PrimeNumberCalculator.CalculatePrimeCompleted' is never used  
    ```  
  
     이러한 경고는 다음 섹션에서 지워집니다.  
  
## <a name="defining-private-delegates"></a>전용 대리자 정의  
 `PrimeNumberCalculator` 구성 요소의 비동기 측면은 <xref:System.Threading.SendOrPostCallback>으로 알려진 특수 대리자를 사용하여 내부적으로 구현됩니다. <xref:System.Threading.SendOrPostCallback>은 <xref:System.Threading.ThreadPool> 스레드에서 실행되는 콜백 메서드를 나타냅니다. 콜백 메서드에는 <xref:System.Object> 형식의 단일 매개 변수를 사용하는 시그니처가 있어야 합니다. 즉, 래퍼 클래스의 대리자 간에 상태를 전달해야 합니다. 자세한 내용은 <xref:System.Threading.SendOrPostCallback>을 참조하세요.  
  
### <a name="to-implement-your-components-internal-asynchronous-behavior"></a>구성 요소의 내부 비동기 동작을 구현하려면:  
  
1. `PrimeNumberCalculator` 클래스에 <xref:System.Threading.SendOrPostCallback> 대리자를 선언하고 만듭니다. `InitializeDelegates`라는 유틸리티 메서드에서 <xref:System.Threading.SendOrPostCallback> 개체를 만듭니다.  
  
     각각 클라이언트에 진행률 및 완료를 보고하는 두 개의 대리자가 필요합니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#9](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#9)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#9](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#9)]  
    [!code-csharp[System.ComponentModel.AsyncOperationManager#20](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#20)]
    [!code-vb[System.ComponentModel.AsyncOperationManager#20](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#20)]  
  
2. 구성 요소의 생성자에서 `InitializeDelegates` 메서드를 호출합니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#21](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#21)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#21](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#21)]  
  
3. `PrimeNumberCalculator` 클래스에서 실제 작업이 비동기적으로 수행되도록 처리하는 대리자를 선언합니다. 이 대리자는 숫자가 소수인지 테스트하는 작업자 메서드를 래핑합니다. 대리자는 비동기 작업의 수명을 추적하는 데 사용되는 <xref:System.ComponentModel.AsyncOperation> 매개 변수를 사용합니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#22](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#22)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#22](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#22)]  
  
4. 보류 중인 비동기 작업의 수명을 관리하기 위한 컬렉션을 만듭니다. 클라이언트에는 실행 및 완료 시 작업을 추적하는 방법이 필요하며, 이 추적을 수행하려면 클라이언트가 비동기 메서드를 호출할 때 고유한 토큰 또는 작업 ID를 전달해야 합니다. `PrimeNumberCalculator` 구성 요소는 작업 ID를 해당 호출과 연결하여 각 호출을 추적해야 합니다. 클라이언트가 고유하지 않은 작업 ID를 전달하면 `PrimeNumberCalculator` 구성 요소가 예외를 발생시켜야 합니다.  
  
     `PrimeNumberCalculator` 구성 요소는 <xref:System.Collections.Specialized.HybridDictionary>라는 특수 컬렉션 클래스를 사용하여 작업 ID를 추적합니다. 클래스 정의에서 `userTokenToLifetime`이라는 <xref:System.Collections.Specialized.HybridDictionary>를 만듭니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#23](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#23)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#23](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#23)]  
  
## <a name="implementing-public-events"></a>공용 이벤트 구현  
 이벤트 기반 비동기 패턴을 구현하는 구성 요소는 이벤트를 사용하는 클라이언트와 통신합니다. 이러한 이벤트는 <xref:System.ComponentModel.AsyncOperation> 클래스를 통해 적절한 스레드에서 호출됩니다.  
  
### <a name="to-raise-events-to-your-components-clients"></a>구성 요소의 클라이언트에 이벤트를 발생시키려면:  
  
1. 클라이언트에 보고할 공용 이벤트를 구현합니다. 각각 진행률 및 완료를 보고하기 위한 두 개의 이벤트가 필요합니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#24](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#24)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#24](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#24)]  
  
## <a name="implementing-the-completion-method"></a>완료 메서드 구현  
 완료 대리자는 비동기 작업이 성공적인 완료, 오류 또는 취소로 종료될 경우 기본적인 자유 스레드 비동기 동작이 호출되는 메서드입니다. 이 호출은 임의 스레드에서 발생합니다.  
  
 이 메서드는 클라이언트의 작업 ID가 고유한 클라이언트 토큰의 내부 컬렉션에서 제거되는 위치입니다. 또한 이 메서드는 해당 <xref:System.ComponentModel.AsyncOperation>에서 <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A> 메서드를 호출하여 특정 비동기 작업의 수명을 종료합니다. 이 호출은 애플리케이션 모델에 적절한 스레드에서 완료 이벤트를 발생시킵니다. <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A> 메서드를 호출한 후에는 <xref:System.ComponentModel.AsyncOperation>의 이 인스턴스를 더 이상 사용할 수 없고 이후에 이를 사용하려고 시도하면 예외가 throw됩니다.  
  
 `CompletionMethod` 시그니처는 비동기 작업의 결과를 설명하는 데 필요한 모든 상태를 포함해야 합니다. 이 시그니처는 이 특정 비동기 작업으로 테스트된 숫자의 상태, 숫자가 소수인지 여부 및 소수가 아닌 경우 첫 번째 제수의 값을 포함합니다. 또한 발생한 예외를 설명하는 상태 및 이 특정 작업에 해당하는 <xref:System.ComponentModel.AsyncOperation>을 포함합니다.  
  
### <a name="to-complete-an-asynchronous-operation"></a>비동기 작업을 완료하려면:  
  
- 완료 메서드를 구현합니다. 이 메서드는 클라이언트의 `CalculatePrimeCompletedEventHandler`를 통해 클라이언트로 반환되는 `CalculatePrimeCompletedEventArgs`를 채우는 데 사용할 6개의 매개 변수를 사용합니다. 이 메서드는 내부 컬렉션에서 클라이언트의 작업 ID 토큰을 제거하고 <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A> 호출을 통해 비동기 작업 수명을 종료합니다. <xref:System.ComponentModel.AsyncOperation>은 애플리케이션 모델에 적합한 스레드 또는 컨텍스트에 대한 호출을 마샬링합니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#26](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#26)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#26](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#26)]  
  
## <a name="checkpoint"></a>검사점  
 이때 구성 요소를 빌드할 수 있습니다.  
  
### <a name="to-test-your-component"></a>구성 요소를 테스트하려면  
  
- 구성 요소를 컴파일합니다.  
  
     하나의 컴파일러 경고를 받게 됩니다.  
  
    ```console  
    warning CS0169: The private field 'AsynchronousPatternExample.PrimeNumberCalculator.workerDelegate' is never used  
    ```  
  
     이 경고는 다음 섹션에서 해결됩니다.  
  
## <a name="implementing-the-worker-methods"></a>작업자 메서드 구현  
 지금까지 `PrimeNumberCalculator` 구성 요소에 대해 지원되는 비동기 코드를 구현했습니다. 이제 실제 작업을 수행하는 코드를 구현할 수 있습니다. 세 가지 메서드 `CalculateWorker` , `BuildPrimeNumberList` 및 `IsPrime`을 구현합니다. `BuildPrimeNumberList` 및 `IsPrime`은 함께 테스트 숫자의 제곱근까지 모든 소수를 찾아서 숫자가 소수인지 확인하는 에라토스테네스의 체라는 잘 알려진 알고리즘을 구성합니다. 해당 지점에서 제수를 찾을 수 없으면 테스트 숫자는 소수입니다.  
  
 효율성 최대화를 위해 이 구성 요소를 작성한 경우 이 구성 요소는 여러 테스트 숫자에 대한 다양한 호출을 통해 검색된 모든 소수를 기억합니다. 2, 3, 5와 같은 사소한 제수도 확인합니다. 그러나 이 예제의 목적은 시간이 오래 걸리는 작업을 비동기적으로 실행하는 방법을 보여주는 것이므로 이러한 최적화는 연습용으로 유지됩니다.  
  
 `CalculateWorker` 메서드는 대리자로 래핑되고 `BeginInvoke` 호출을 통해 비동기적으로 호출됩니다.  
  
> [!NOTE]
> 진행률 보고는 `BuildPrimeNumberList` 메서드에서 구현됩니다. 빠른 컴퓨터에서는 `ProgressChanged` 이벤트가 연속적으로 발생할 수 있습니다. 이러한 이벤트가 발생하는 클라이언트 스레드에서 이 상황을 처리할 수 있어야 합니다. 사용자 인터페이스 코드가 메시지로 넘쳐 유지할 수 없어서 응답하지 않을 수 있습니다. 이 상황을 처리하는 예제 사용자 인터페이스는 [방법: 이벤트 기반 비동기 패턴의 클라이언트 구현](../../../docs/standard/asynchronous-programming-patterns/how-to-implement-a-client-of-the-event-based-asynchronous-pattern.md)을 참조하세요.  
  
### <a name="to-execute-the-prime-number-calculation-asynchronously"></a>소수 계산을 비동기적으로 실행하려면:  
  
1. `TaskCanceled` 유틸리티 메서드를 구현합니다. 이 메서드는 지정된 작업 ID의 작업 수명 컬렉션을 확인하고 작업 ID를 찾을 수 없는 경우 `true`를 반환합니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#32](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#32)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#32](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#32)]  
  
2. `CalculateWorker` 메서드를 구현합니다. 이 메서드는 두 개의 매개 변수인 테스트할 숫자 및 <xref:System.ComponentModel.AsyncOperation>을 사용합니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#27](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#27)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#27](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#27)]  
  
3. `BuildPrimeNumberList`를 구현해야 합니다. 이 메서드는 두 개의 매개 변수인 테스트할 숫자 및 <xref:System.ComponentModel.AsyncOperation>을 사용합니다. <xref:System.ComponentModel.AsyncOperation>을 사용하여 진행률 및 증분 결과를 보고합니다. 이 메서드를 사용하면 클라이언트의 이벤트 처리기가 애플리케이션 모델에 대한 적절한 스레드 또는 컨텍스트에서 호출됩니다. `BuildPrimeNumberList`는 소수를 찾을 경우 `ProgressChanged` 이벤트에 대한 클라이언트 이벤트 처리기에 이 소수를 증분 결과로 보고합니다. 이 작업에는 `LatestPrimeNumber`라는 하나의 추가된 속성을 포함하는 `CalculatePrimeProgressChangedEventArgs`라는 <xref:System.ComponentModel.ProgressChangedEventArgs>에서 파생된 클래스가 필요합니다.  
  
     또한 `BuildPrimeNumberList` 메서드는 `TaskCanceled` 메서드를 정기적으로 호출하고 메서드가 `true`를 반환하는 경우 종료됩니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#5)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#5)]  
  
4. `IsPrime`를 구현해야 합니다. 이 메서드는 세 개의 매개 변수인 알려진 소수 목록, 테스트할 숫자 및 발견된 첫 번째 제수의 출력 매개 변수를 사용합니다. 소수 목록이 제공된 경우 테스트 숫자가 소수인지 확인합니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#28](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#28)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#28](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#28)]  
  
5. <xref:System.ComponentModel.ProgressChangedEventArgs>에서 `CalculatePrimeProgressChangedEventArgs`를 파생시킵니다. 이 클래스는 `ProgressChanged` 이벤트에 대한 클라이언트 이벤트 처리기에 증분 결과를 보고하는 데 필요합니다. `LatestPrimeNumber`라는 하나의 추가된 속성을 포함합니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#29](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#29)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#29](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#29)]  
  
## <a name="checkpoint"></a>검사점  
 이때 구성 요소를 빌드할 수 있습니다.  
  
### <a name="to-test-your-component"></a>구성 요소를 테스트하려면  
  
- 구성 요소를 컴파일합니다.  
  
     계속해서 비동기 작업을 시작 및 취소하는 `CalculatePrimeAsync` 및 `CancelAsync` 메서드를 작성합니다.  
  
## <a name="implementing-the-start-and-cancel-methods"></a>시작 및 취소 메서드 구현  
 메서드를 래핑하는 대리자에서 `BeginInvoke`를 호출하여 자체 스레드에서 작업자 메서드를 시작합니다. 특정 비동기 작업의 수명을 관리하려면 <xref:System.ComponentModel.AsyncOperationManager> 도우미 클래스에서 <xref:System.ComponentModel.AsyncOperationManager.CreateOperation%2A> 메서드를 호출합니다. 이렇게 하면 클라이언트의 이벤트 처리기에 대한 호출을 올바른 스레드 또는 컨텍스트로 마샬링하는 <xref:System.ComponentModel.AsyncOperation>이 반환됩니다.  
  
 해당 <xref:System.ComponentModel.AsyncOperation>에서 <xref:System.ComponentModel.AsyncOperation.PostOperationCompleted%2A>를 호출하여 특정 보류 작업을 취소합니다. 이렇게 하면 해당 작업이 종료되고 이후에 <xref:System.ComponentModel.AsyncOperation>을 호출하면 예외가 throw됩니다.  
  
### <a name="to-implement-start-and-cancel-functionality"></a>시작 및 취소 기능을 구현하려면:  
  
1. `CalculatePrimeAsync` 메서드를 구현합니다. 클라이언트 제공 토큰(작업 ID)이 현재 보류 중인 작업을 나타내는 모든 토큰에 관련해서 고유한지 확인합니다. 클라이언트가 고유하지 않은 토큰으로 전달되면 `CalculatePrimeAsync`가 예외를 발생시킵니다. 그렇지 않으면 토큰이 작업 ID 컬렉션에 추가됩니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#3)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#3)]  
  
2. `CancelAsync` 메서드를 구현합니다. `taskId` 매개 변수가 토큰 컬렉션에 있는 경우 제거됩니다. 이렇게 하면 취소된 작업의 실행이 시작되지 않습니다. 작업이 실행 중인 경우 `BuildPrimeNumberList` 메서드는 해당 작업 ID가 수명 컬렉션에서 제거되었음을 감지할 때 종료됩니다.  
  
     [!code-csharp[System.ComponentModel.AsyncOperationManager#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#4)]
     [!code-vb[System.ComponentModel.AsyncOperationManager#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#4)]  
  
## <a name="checkpoint"></a>검사점  
 이때 구성 요소를 빌드할 수 있습니다.  
  
### <a name="to-test-your-component"></a>구성 요소를 테스트하려면  
  
- 구성 요소를 컴파일합니다.  
  
 이제 `PrimeNumberCalculator` 구성 요소가 완료되고 사용할 준비가 되었습니다.  
  
 `PrimeNumberCalculator` 구성 요소를 사용하는 예제 클라이언트는 [방법: 이벤트 기반 비동기 패턴의 클라이언트 구현](../../../docs/standard/asynchronous-programming-patterns/how-to-implement-a-client-of-the-event-based-asynchronous-pattern.md)을 참조하세요.  
  
## <a name="next-steps"></a>다음 단계  
 `CalculatePrimeAsync` 메서드의 동기 메서드인 `CalculatePrime`을 작성하여 이 예제를 채울 수 있습니다. 이렇게 하면 `PrimeNumberCalculator` 구성 요소가 이벤트 기반 비동기 패턴을 완전히 준수하게 됩니다.  
  
 여러 테스트 숫자에 대한 다양한 호출을 통해 검색된 모든 소수 목록을 유지하면 이 예제를 향상할 수 있습니다. 이 방법을 사용하면 각 작업이 이전 작업에서 수행된 작업을 활용합니다. 이 목록을 `lock` 영역으로 보호하면 여러 스레드에 의한 목록 액세스가 직렬화되므로 주의해야 합니다.  
  
 2, 3, 5와 같은 사소한 제수를 테스트하여 이 예제를 향상할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [방법: 백그라운드에서 작업 실행](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)
- [이벤트 기반 비동기 패턴 개요](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)
- [EAP(이벤트 기반 비동기 패턴)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)
