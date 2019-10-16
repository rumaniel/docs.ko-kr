---
title: 관리되는 스레딩을 구현하는 최선의 방법
ms.date: 10/15/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- threading [.NET Framework], design guidelines
- threading [.NET Framework], best practices
- managed threading
ms.assetid: e51988e7-7f4b-4646-a06d-1416cee8d557
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1066a3533dedd5976f2dd73b1858ad8fa0c1f653
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392701"
---
# <a name="managed-threading-best-practices"></a>관리 스레딩을 구현하는 최선의 방법
다중 스레딩에는 신중한 프로그래밍이 필요합니다. 대부분의 작업의 경우 스레드 풀 스레드로 실행에 대한 요청을 큐에 대기시켜 복잡성을 줄일 수 있습니다. 이 항목에서는 다중 스레드의 작업 조정 또는 차단되는 스레드 처리 등의 더욱 어려운 상황을 다룹니다.  
  
> [!NOTE]
> .NET Framework 4부터 작업 병렬 라이브러리 및 PLINQ는 다중 스레드 프로그래밍의 일부 복잡성 및 위험을 줄여주는 API를 제공합니다. 자세한 내용은 [.NET의 병렬 프로그래밍](../../../docs/standard/parallel-programming/index.md)을 참조하세요.  
  
## <a name="deadlocks-and-race-conditions"></a>교착 상태 및 경합 상태  
 다중 스레딩은 처리량 및 응답성을 사용하여 문제를 해결하지만 이 과정에서 교착 상태 및 경합 상태의 새로운 문제를 유발합니다.  
  
### <a name="deadlocks"></a>교착 상태  
 교착 상태는 두 개의 각 스레드가 다른 스레드가 이미 잠근 리소스를 잠그려고 할 때 발생합니다. 두 스레드는 더 이상 진행할 수 없습니다.  
  
 관리되는 스레딩 클래스의 많은 메서드는 교착 상태를 감지하는 데 도움이 되는 시간 제한을 제공합니다. 예를 들어 다음 코드는 `lockObject`라는 개체에 대한 잠금을 획득하려고 합니다. 잠금이 300밀리초 내에 획득되지 않으면 <xref:System.Threading.Monitor.TryEnter%2A?displayProperty=nameWithType>는 `false`를 반환합니다.  
  
```vb  
If Monitor.TryEnter(lockObject, 300) Then  
    Try  
        ' Place code protected by the Monitor here.  
    Finally  
        Monitor.Exit(lockObject)  
    End Try  
Else  
    ' Code to execute if the attempt times out.  
End If  
```  
  
```csharp  
if (Monitor.TryEnter(lockObject, 300)) {  
    try {  
        // Place code protected by the Monitor here.  
    }  
    finally {  
        Monitor.Exit(lockObject);  
    }  
}  
else {  
    // Code to execute if the attempt times out.  
}  
```  
  
### <a name="race-conditions"></a>경합 조건  
 경합 상태는 두 개 이상의 스레드에 의존하는 프로그램의 결과가 특정 코드 블록에 먼저 도달하는 경우에 발생하는 버그입니다. 프로그램을 여러 번 실행하면 서로 다른 결과를 생성하며 지정된 실행의 결과는 예측할 수 없습니다.  
  
 경합 상태의 간단한 예는 필드를 증가시키는 경우입니다. 클래스에 `objCt++;`(C#) 또는 `objCt += 1`(Visual Basic)과 같은 코드를 사용하는, 클래스의 인스턴스가 생성될 때마다 증가되는 개인 **정적** 필드(Visual Basic에서 **Shared**)가 있다고 가정합니다. 이 작업은 `objCt`에서 레지스터로 값을 로드하고, 값을 증가시키고 `objCt`에 저장해야 합니다.  
  
 다중 스레드 애플리케이션에서 값을 로드하고 증가시킨 스레드는 세 단계 모두를 수행하는 다른 스레드에 의해 선점될 수 있습니다. 첫 번째 스레드가 실행을 다시 시작하고 해당 값을 저장할 때 그 사이에 값이 변경된 사실을 고려하지 않고 `objCt`를 덮어씁니다.  
  
 이 특정 경합 상태는 <xref:System.Threading.Interlocked.Increment%2A?displayProperty=nameWithType>와 같은 <xref:System.Threading.Interlocked> 클래스의 메서드를 사용하여 쉽게 피할 수 있습니다. 다중 스레딩 간에 데이터를 동기화하는 다른 기술에 대해 알아보려면 [다중 스레딩을 위한 데이터 동기화](../../../docs/standard/threading/synchronizing-data-for-multithreading.md)를 참조하세요.  
  
 경합 상태는 다중 스레드의 작업을 동기화할 때에도 발생할 수 있습니다. 코드 줄을 작성할 때마다 줄을 실행하기 전에(또는 줄을 구성하는 개별 컴퓨터 명령 전에) 스레드가 선점되었고 다른 스레드가 먼저 사용한 경우 발생할 수 있는 상황을 고려해야 합니다.  
  
## <a name="static-members-and-static-constructors"></a>정적 멤버 및 정적 생성자  
 클래스는 해당 클래스 생성자(C#에서 `static` 생성자, Visual Basic에서 `Shared Sub New`)가 실행을 완료할 때까지 초기화되지 않습니다. 초기화되지 않는 형식에서 코드의 실행을 방지하려면 공용 언어 런타임은 클래스 생성자가 실행을 완료할 때까지 다른 스레드에서 클래스의 `static` 멤버(Visual Basic에서 `Shared` 멤버)로 모든 호출을 차단합니다.  
  
 예를 들어 클래스 생성자가 새 스레드를 시작하고 스레드 프로시저가 클래스의 `static` 멤버를 호출하는 경우 새 스레드는 클래스 생성자가 완료할 때까지 차단됩니다.  
  
 이는 `static` 생성자를 가질 수 있는 모든 형식에 적용됩니다.  

## <a name="number-of-processors"></a>프로세서 수

시스템에 다중 프로세서 또는 하나의 프로세스만 사용할 수 있는지 여부에 따라 다중 스레드 아키텍처가 영향을 받을 수 있습니다. 자세한 내용은 [프로세서의 수](https://docs.microsoft.com/previous-versions/dotnet/netframework-1.1/1c9txz50(v%3dvs.71)#number-of-processors)를 참조하세요.

런타임 시 사용 가능한 프로세서 수를 확인하려면 <xref:System.Environment.ProcessorCount?displayProperty=nameWithType> 속성을 사용합니다.
  
## <a name="general-recommendations"></a>일반 권장 사항  
 다중 스레드를 사용하는 경우 다음 지침을 고려합니다.  
  
- 다른 스레드를 종료하는 데 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>를 사용하지 마세요. 다른 스레드에서 **Abort**를 호출하는 것은 해당 처리에서 해당 스레드가 어떤 지점에 도달했는지 알지 못하면서 해당 스레드에서 예외를 throw하는 것과 유사합니다.  
  
- 여러 스레드의 활동을 동기화하는 데 <xref:System.Threading.Thread.Suspend%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Thread.Resume%2A?displayProperty=nameWithType>을 사용하지 마세요. <xref:System.Threading.Mutex>, <xref:System.Threading.ManualResetEvent>, <xref:System.Threading.AutoResetEvent> 및 <xref:System.Threading.Monitor>를 사용하세요.  
  
- 기본 프로그램(예: 이벤트 사용)에서 작업자 스레드의 실행을 제어하지 마세요. 대신 작업자 스레드가 작업을 확보할 때까지 대기하고, 실행하고, 완료되면 프로그램의 다른 부분에 알릴 수 있도록 프로그램을 디자인합니다. 작업자 스레드가 차단되지 않는 경우 스레드 풀 스레드를 사용하는 것이 좋습니다. <xref:System.Threading.Monitor.PulseAll%2A?displayProperty=nameWithType>은 작업자 스레드가 차단되는 경우에 유용합니다.  
  
- 잠금 개체로 형식을 사용하지 마세요. 즉, C#에서 `lock(typeof(X))` 또는 Visual Basic에서 `SyncLock(GetType(X))`과 같은 코드를 피하거나 <xref:System.Type> 개체와 함께 <xref:System.Threading.Monitor.Enter%2A?displayProperty=nameWithType>을 사용하지 마세요. 제공된 형식의 경우 애플리케이션 도메인당 <xref:System.Type?displayProperty=nameWithType> 인스턴스가 하나만 있습니다. 잠금을 사용하는 형식이 공용인 경우 개인 외의 코드는 잠금을 사용할 수 있으며 교착 상태가 발생합니다. 추가 문제는 [최선의 안정성 구현 방법](../../../docs/framework/performance/reliability-best-practices.md)을 참조하세요.  
  
- 인스턴스를 잠글 때 주의합니다(예: C#에서 `lock(this)` 또는 Visual Basic에서 `SyncLock(Me)`). 형식 외부의 애플리케이션에 있는 다른 코드가 개체에서 잠금을 사용하는 경우 교착 상태가 발생할 수 있습니다.  
  
- 모니터링을 시작한 스레드가 모니터링 중에 있는 동안 예외가 발생한 경우에도 항상 해당 모니터링을 유지하는지 확인합니다. C# [lock](../../csharp/language-reference/keywords/lock-statement.md) 문 및 Visual Basic [SyncLock](../../visual-basic/language-reference/statements/synclock-statement.md) 문은 <xref:System.Threading.Monitor.Exit%2A?displayProperty=nameWithType>이 호출되었는지 확인하는 **finally** 블록을 사용하여 이 동작을 자동으로 제공합니다. **Exit**이 호출될지 확인할 수 없는 경우 **뮤텍스**를 사용하도록 설계를 변경하는 것이 좋습니다. 뮤텍스는 현재 소유하고 있는 스레드가 종료되면 자동으로 해제됩니다.  
  
- 다른 리소스를 필요로 하는 작업에 대해 다중 스레드를 사용하고 단일 리소스에 다중 스레드를 할당하지 마세요. 예를 들어 해당 스레드는 I/O 작업 중에 차단되어 다른 스레드의 실행을 허용하므로 I/O와 관련된 모든 작업은 자체 스레드를 소유함으로써 이익을 얻습니다. 사용자 입력은 전용 스레드를 활용하는 다른 리소스입니다. 단일 프로세서 컴퓨터에서 집중적 계산을 포함하는 작업은 사용자 입력 및 I/O와 관련된 작업과 공존하지만 여러 계산 집약적인 작업은 서로 경쟁합니다.  
  
- 간단한 상태 변경에 `lock` 문(Visual Basic의 `SyncLock`)을 사용하는 대신 <xref:System.Threading.Interlocked> 클래스의 메서드를 사용하는 것이 좋습니다. `lock` 문은 좋은 일반 용도의 도구이지만 <xref:System.Threading.Interlocked> 클래스는 원자성이어야 하는 업데이트에 더 나은 성능을 제공합니다. 경합이 없는 경우 내부적으로 단일 잠금 접두사를 실행합니다. 코드 검토에서 다음 예제에서와 같은 코드를 감시합니다. 첫 번째 예제에서 상태 변수가 증가됩니다.  
  
    ```vb  
    SyncLock lockObject  
        myField += 1  
    End SyncLock  
    ```  
  
    ```csharp  
    lock(lockObject)   
    {  
        myField++;  
    }  
    ```  
  
     다음과 같이 `lock` 문 대신 <xref:System.Threading.Interlocked.Increment%2A> 메서드를 사용하여 성능을 향상시킬 수 있습니다.  
  
    ```vb  
    System.Threading.Interlocked.Increment(myField)  
    ```  
  
    ```csharp  
    System.Threading.Interlocked.Increment(myField);  
    ```  
  
    > [!NOTE]
    > .NET Framework 2.0 이상에서는 1보다 큰 원자성 증분에 대해 <xref:System.Threading.Interlocked.Add%2A> 메서드를 사용합니다.  
  
     두 번째 예제에서 참조 형식 변수는 null 참조인 경우에만 업데이트됩니다(Visual Basic에서 `Nothing`).  
  
    ```vb  
    If x Is Nothing Then  
        SyncLock lockObject  
            If x Is Nothing Then  
                x = y  
            End If  
        End SyncLock  
    End If  
    ```  
  
    ```csharp  
    if (x == null)  
    {  
        lock (lockObject)  
        {  
            x ??= y;
        }  
    }  
    ```  
  
     다음과 같이 <xref:System.Threading.Interlocked.CompareExchange%2A> 메서드를 대신 사용하여 성능을 향상시킬 수 있습니다.  
  
    ```vb  
    System.Threading.Interlocked.CompareExchange(x, y, Nothing)  
    ```  
  
    ```csharp  
    System.Threading.Interlocked.CompareExchange(ref x, y, null);  
    ```  
  
    > [!NOTE]
    > .NET Framework 2.0 부터 <xref:System.Threading.Interlocked.CompareExchange%60%601%28%60%600%40%2C%60%600%2C%60%600%29> 메서드 오버로드에서는 참조 형식에 대해 형식이 안전한 대안을 제공합니다.
  
## <a name="recommendations-for-class-libraries"></a>클래스 라이브러리에 대한 권장 사항  
 다중 스레딩에 대한 클래스 라이브러리를 설계할 때 다음 지침을 고려합니다.  
  
- 가능한 경우 동기화의 필요성을 피합니다. 많이 사용되는 코드의 경우 특히 그렇습니다. 예를 들어 경합 상태를 제거하는 대신 허용하도록 알고리즘을 조정할 수 있습니다. 불필요한 동기화는 성능을 저하시키고 교착 상태 및 경합 상태의 가능성을 만듭니다.  
  
- 기본적으로 정적 데이터(Visual Basic에서 `Shared`)를 스레드로부터 안전하게 만듭니다.  
  
- 기본적으로 인스턴스 데이터를 스레드로부터 안전하게 만들지 마세요. 스레드로부터 안전한 코드를 만드는 잠금을 추가하면 성능을 저하시키고 잠금 경합이 증가하고 교착 상태가 발생할 가능성을 만듭니다. 공용 애플리케이션 모델에서 한 번에 하나의 스레드만이 스레드 보안의 필요성을 최소화하는 사용자 코드를 실행합니다. 이러한 이유로 .NET Framework 클래스 라이브러리는 기본적으로 스레드로부터 안전하지 않습니다.  
  
- 정적 상태를 변경하는 정적 메서드를 제공 하지 마세요. 일반적인 서버 시나리오에서 정적 상태는 요청 간 공유되며 여러 스레드가 동시에 해당 코드를 실행할 수 있음을 의미합니다. 스레드 버그가 발생할 가능성을 엽니다. 요청 간에 공유되지 않는 인스턴스로 데이터를 캡슐화하는 디자인 패턴을 사용하는 것이 좋습니다. 또한 정적 데이터가 동기화되는 경우 상태를 변경하는 정적 메서드 간 호출은 성능에 부정적인 영향을 주어 교착 상태 또는 중복된 동기화를 발생시킬 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [스레딩](../../../docs/standard/threading/index.md)
- [스레드 및 스레딩](../../../docs/standard/threading/threads-and-threading.md)
