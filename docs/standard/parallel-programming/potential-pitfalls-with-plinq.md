---
title: PLINQ에서 발생할 수 있는 문제
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, pitfalls
ms.assetid: 75a38b55-4bc4-488a-87d5-89dbdbdc76a2
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e44fd3e6f806eef3805416dafd90a4855e79b3c7
ms.sourcegitcommit: 15d99019aea4a5c3c91ddc9ba23692284a7f61f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49121933"
---
# <a name="potential-pitfalls-with-plinq"></a>PLINQ에서 발생할 수 있는 문제
대부분의 경우 PLINQ는 순차적인 LINQ to Objects 쿼리에 대해 상당한 성능 향상을 제공할 수 있습니다. 그러나 쿼리 실행을 병렬 처리하는 작업에는 순차적 코드에서는 일반적이지 않거나 전혀 발생하지 않는 문제를 일으킬 수 있는 복잡성이 있습니다. 이 항목에서는 PLINQ 쿼리를 작성할 때 주의해야 할 사항을 나열합니다.  
  
## <a name="do-not-assume-that-parallel-is-always-faster"></a>병렬이 항상 더 빠르다고 가정하지 마세요.  
 경우에 따라 병렬 처리로 인해 PLINQ 쿼리가 LINQ to Objects 쿼리보다 느리게 실행됩니다. 소스 요소가 적고 빠른 사용자 대리자가 있는 쿼리의 속도가 훨씬 빠를 가능성이 없다는 것이 경험적인 기본 규칙입니다. 그러나 많은 요소가 성능에 관련되므로 PLINQ를 사용할지 결정하기 전에 실제 결과를 측정하는 것이 좋습니다. 자세한 내용은 [PLINQ의 속도 향상 이해](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)를 참조하세요.  
  
## <a name="avoid-writing-to-shared-memory-locations"></a>공유 메모리 위치에 쓰기 방지  
 순차적 코드에서는 정적 변수 또는 클래스 필드에서 읽거나 쓰는 것은 일반적입니다. 그러나 여러 스레드가 해당 변수에 동시에 액세스할 때마다 경합 상태가 발생할 가능성이 큽니다. 잠금을 사용하여 변수에 대한 액세스를 동기화할 수 있지만 동기화의 비용으로 성능이 저하될 수 있습니다. 따라서 가능한 한 PLINQ 쿼리에서 공유된 상태에 대한 액세스를 방지하거나 최소한의 제한으로 액세스하는 것이 좋습니다.  
  
## <a name="avoid-over-parallelization"></a>과도한 병렬화 방지  
 `AsParallel` 연산자를 사용하면 소스 컬렉션을 분할하고 작업자 스레드를 동기화하는 오버헤드 비용이 발생합니다. 병렬화의 이점은 컴퓨터의 프로세서 수로 더 제한됩니다. 하나의 프로세서에서 여러 계산 바인딩된 스레드를 실행하여 얻을 수 있는 속도 향상이 없습니다. 따라서 쿼리를 과도하게 병렬 처리하지 않도록 주의해야 합니다.  
  
 과도한 병렬 처리가 발생할 수 있는 가장 일반적인 시나리오는 다음 코드 조각에 표시된 대로 중첩된 루프에 있습니다.  
  
 [!code-csharp[PLINQ#20](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#20)]
 [!code-vb[PLINQ#20](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#20)]  
  
 이 경우에서 다음 조건 중 하나 이상이 적용되지 않는 한 외부 데이터 소스(고객)만을 병렬 처리하는 것이 가장 좋습니다.  
  
-   내부 데이터 소스(cust.Orders)가 매우 긴 것으로 알려져 있습니다.  
  
-   각 순서에서 비용이 많이 드는 계산을 수행하고 있습니다. (이 예제에 나와 있는 작업은 비용이 많이 들지 않습니다.)  
  
-   대상 시스템은 `cust.Orders`에서 쿼리를 병렬화하여 생성될 스레드의 수를 처리할 충분한 프로세서를 가진 것으로 알려져 있습니다.  
  
 모든 경우에서 최적의 쿼리 형태를 결정하는 가장 좋은 방법은 테스트하고 측정하는 것입니다. 자세한 내용은 [방법: PLINQ 쿼리 성능 측정](../../../docs/standard/parallel-programming/how-to-measure-plinq-query-performance.md)을 참조하세요.  
  
## <a name="avoid-calls-to-non-thread-safe-methods"></a>스레드로부터 안전하지 않은 메서드에 대한 호출 방지  
 PLINQ 쿼리에서 스레드로부터 안전하지 않은 인스턴스 메서드를 작성하면 프로그램에서 감지하거나 감지하지 않을 수도 있는 데이터 손상이 발생할 수 있습니다. 예외가 발생할 수도 있습니다. 다음 예제에서는 여러 스레드가 `Filestream.Write` 메서드를 동시에 호출하려고 합니다. 이는 클래스에서 지원되지 않습니다.  
  
```vb  
Dim fs As FileStream = File.OpenWrite(…)  
a.Where(...).OrderBy(...).Select(...).ForAll(Sub(x) fs.Write(x))  
```  
  
```csharp  
FileStream fs = File.OpenWrite(...);  
a.Where(...).OrderBy(...).Select(...).ForAll(x => fs.Write(x));  
```  
  
## <a name="limit-calls-to-thread-safe-methods"></a>스레드로부터 안전한 메서드에 대한 호출 제한  
 .NET Framework에서 대부분의 정적 메서드는 스레드로부터 안전하고 여러 스레드에서 동시에 호출될 수 있습니다. 그러나 이러한 경우에도 관련된 동기화로 인해 쿼리 속도가 상당히 느려질 수 있습니다.  
  
> [!NOTE]
>  쿼리에서 <xref:System.Console.WriteLine%2A>에 일부 호출을 삽입하여 이를 직접 테스트할 수 있습니다. 이 메서드는 설명 목적으로 설명서 예제에서 사용되지만 PLINQ 쿼리에서 사용하지 마세요.  
  
## <a name="avoid-unnecessary-ordering-operations"></a>불필요한 순서 지정 작업 방지  
 PLINQ는 쿼리를 병렬로 실행할 때 소스 시퀀스를 여러 스레드에서 동시에 작동할 수 있는 파티션으로 나눕니다. 기본적으로 파티션이 처리되고 결과가 전달되는 순서는 예측할 수 없습니다(`OrderBy` 같은 연산자 제외). 소스 시퀀스의 순서를 유지하도록 PLINQ에 지시할 수 있지만 이 지시는 성능에 부정적인 영향을 줍니다. 가능한 한 순서 유지에 의존하지 않도록 쿼리를 구성하는 것이 좋습니다. 자세한 내용은 [PLINQ에서 순서 유지](../../../docs/standard/parallel-programming/order-preservation-in-plinq.md)를 참조하세요.  
  
## <a name="prefer-forall-to-foreach-when-it-is-possible"></a>가능할 경우 ForEach 대신 ForAll을 사용하는 것이 좋습니다.  
 PLINQ는 여러 스레드에서 쿼리를 실행하지만 `foreach` 루프(Visual Basic의 `For Each`)의 결과를 사용하는 경우 쿼리 결과는 한 스레드로 다시 병합되고 열거자에 의해 직렬로 액세스되어야 합니다. 경우에 따라 이 상황은 피할 수 없지만, 가능한 한 `ForAll` 메서드를 사용하여 <xref:System.Collections.Concurrent.ConcurrentBag%601?displayProperty=nameWithType> 같은 스레드로부터 안전한 컬렉션을 작성하는 등의 방법으로 스레드가 고유한 결과를 출력하도록 할 수 있습니다.  
  
 동일한 문제가 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType>에 적용됩니다. 즉, 다음 코드보다 `source.AsParallel().Where().ForAll(...)`을 사용하는 것이 좋습니다.  
  
 `Parallel.ForEach(source.AsParallel().Where(), ...)`.  
  
## <a name="be-aware-of-thread-affinity-issues"></a>스레드 선호도 문제 인식  
 STA(단일 스레드 아파트) 구성 요소에 대한 COM 상호 운용성, Windows Forms 및 WPF(Windows Presentation Foundation)와 같은 일부 기술은 특정 스레드에서 실행하는 코드를 필요로 하는 스레드 선호도 제한 사항이 적용됩니다. 예를 들어 Windows Forms 및 WPF에서 컨트롤은 작성된 스레드에서만 액세스될 수 있습니다. PLINQ 쿼리에서 Windows Forms 컨트롤의 공유 상태에 액세스하려고 하면 디버거에서 실행 중인 경우 예외가 발생합니다. (이 설정은 해제할 수 있습니다.) 그러나 쿼리를 UI 스레드에서 사용하는 경우 해당 코드가 한 스레드에서만 실행되므로 쿼리 결과를 열거하는 `foreach` 루프에서 이 컨트롤에 액세스할 수 있습니다.  
  
## <a name="do-not-assume-that-iterations-of-foreach-for-and-forall-always-execute-in-parallel"></a>ForEach, For 및 ForAll의 반복이 항상 병렬로 실행된다고 가정하지 마세요.  
 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType>, <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> 또는 <xref:System.Linq.ParallelEnumerable.ForAll%2A> 루프에서 개별 반복이 실행될 수 있지만 병렬로 실행할 필요가 없다는 것을 유념해야 합니다. 따라서 반복의 병렬 실행 또는 특정 순서로 반복 실행의 정확성에 의존하는 코드를 작성하지 마세요.  
  
 예를 들어 다음 코드는 교착 상태의 가능성이 있습니다.  
  
```vb  
Dim mre = New ManualResetEventSlim()  
Enumerable.Range(0, Environment.ProcessorCount * 100).AsParallel().ForAll(Sub(j)   
   If j = Environment.ProcessorCount Then  
       Console.WriteLine("Set on {0} with value of {1}", Thread.CurrentThread.ManagedThreadId, j)  
       mre.Set()  
   Else  
       Console.WriteLine("Waiting on {0} with value of {1}", Thread.CurrentThread.ManagedThreadId, j)  
       mre.Wait()  
   End If  
End Sub) ' deadlocks  
```  
  
```csharp  
ManualResetEventSlim mre = new ManualResetEventSlim();  
Enumerable.Range(0, Environment.ProcessorCount * 100).AsParallel().ForAll((j) =>  
{  
    if (j == Environment.ProcessorCount)  
    {  
        Console.WriteLine("Set on {0} with value of {1}", Thread.CurrentThread.ManagedThreadId, j);  
        mre.Set();  
    }  
    else  
    {  
        Console.WriteLine("Waiting on {0} with value of {1}", Thread.CurrentThread.ManagedThreadId, j);  
        mre.Wait();  
    }  
}); //deadlocks  
```  
  
 이 예제에서는 하나의 반복이 이벤트를 설정하고 다른 모든 반복은 이벤트를 기다립니다. 대기 중인 반복은 이벤트 설정 반복이 완료될 때까지 완료할 수 없습니다. 그러나 대기 중인 반복은 이벤트 설정 반복이 실행될 기회를 갖기 전에 병렬 루프를 실행하는 데 사용되는 모든 스레드를 차단할 수 있습니다. 이로 인해 교착 상태가 발생하고 이벤트 설정 반복은 실행되지 않으며 대기 중인 반복은 시작되지 않습니다.  
  
 특히 병렬 루프의 하나의 반복은 다른 루프의 반복이 진행되기를 기다리면 안 됩니다. 병렬 루프가 반대 순서로 순차적으로 반복되도록 결정하는 경우 교착 상태가 발생합니다.  
  
## <a name="see-also"></a>참고 항목

- [PLINQ(병렬 LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
