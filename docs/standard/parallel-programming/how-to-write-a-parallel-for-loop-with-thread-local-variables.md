---
title: '방법: 스레드 로컬 변수를 사용하는 Parallel.For 루프 작성'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel for loops, how to use local state
ms.assetid: 68384064-7ee7-41e2-90e3-71f00bde01bb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6ffac3df82268399aa35ff494e462e2b23c3894b
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54610801"
---
# <a name="how-to-write-a-parallelfor-loop-with-thread-local-variables"></a>방법: 스레드 로컬 변수를 사용하는 Parallel.For 루프 작성
이 예제에서는 스레드 로컬 변수를 사용하여, <xref:System.Threading.Tasks.Parallel.For%2A> 루프에 의해 만들어진 각 별도 작업의 상태를 저장하고 검색하는 방법을 보여 줍니다. 스레드 지역 데이터를 사용하여, 공유 상태에 대한 많은 수의 액세스를 동기화하는 오버헤드를 방지할 수 있습니다. 반복할 때마다 공유 리소스에 쓰는 대신 작업의 반복이 모두 완료될 때까지 값을 계산하여 저장합니다. 그런 다음 공유 리소스에 최종 결과를 한 번 쓰거나, 최종 결과를 다른 메서드로 전달할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Threading.Tasks.Parallel.For%60%601%28System.Int32%2CSystem.Int32%2CSystem.Func%7B%60%600%7D%2CSystem.Func%7BSystem.Int32%2CSystem.Threading.Tasks.ParallelLoopState%2C%60%600%2C%60%600%7D%2CSystem.Action%7B%60%600%7D%29> 메서드를 호출하여 1백만 개의 요소가 포함된 배열의 값 합계를 계산합니다. 각 요소의 값은 해당 인덱스와 같습니다.  
  
 [!code-csharp[TPL_Parallel#05](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/forandforeach_simple.cs#05)]
 [!code-vb[TPL_Parallel#05](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/forwiththreadlocal.vb#05)]  
  
 모든 <xref:System.Threading.Tasks.Parallel.For%2A> 메서드의 처음 두 매개 변수는 시작 및 끝 반복 값을 지정합니다. 메서드의 이 오버로드에서 세 번째 매개 변수는 로컬 상태를 초기화하는 위치입니다. 이 컨텍스트에서 로컬 상태는 수명이 현재 스레드에 대한 루프의 첫 번째 반복 바로 전에서 마지막 반복 바로 후까지 연장되는 변수를 의미합니다.  
  
 세 번째 매개 변수의 형식은 <xref:System.Func%601>이며, 여기서 `TResult`는 스레드 지역 변수를 저장하는 변수의 형식입니다. 해당 형식은 제네릭 <xref:System.Threading.Tasks.Parallel.For%60%601%28System.Int32%2CSystem.Int32%2CSystem.Func%7B%60%600%7D%2CSystem.Func%7BSystem.Int32%2CSystem.Threading.Tasks.ParallelLoopState%2C%60%600%2C%60%600%7D%2CSystem.Action%7B%60%600%7D%29> 메서드를 호출할 때 제공되는 제네릭 형식 인수에 의해 정의되며, 이 경우 <xref:System.Int64>입니다. 형식 인수는 컴파일러에 스레드 로컬 상태를 저장하는 데 사용되는 임시 변수의 형식을 알립니다. 이 예제에서 `() => 0`(또는 Visual Basic의 경우 `Function() 0`) 식은 스레드 지역 변수를 0으로 초기화합니다. 제네릭 형식 인수가 참조 형식 또는 사용자 정의 값 형식인 경우 식은 다음과 같습니다.  
  
```csharp  
() => new MyClass()  
```  
  
```vb  
Function() new MyClass()  
```  
  
 네 번째 매개 변수는 루프 논리를 정의합니다. 이 매개 변수는 시그니처가 `Func<int, ParallelLoopState, long, long>`(C#의 경우) 또는 `Func(Of Integer, ParallelLoopState, Long, Long)`(Visual Basic의 경우)인 대리자 또는 람다 식이어야 합니다. 첫 번째 매개 변수는 루프의 해당 반복에 대한 루프 카운터의 값입니다. 두 번째 매개 변수는 루프를 중단하는 데 사용할 수 있는 <xref:System.Threading.Tasks.ParallelLoopState> 개체입니다. 이 개체는 <xref:System.Threading.Tasks.Parallel> 클래스에 의해 루프의 각 발생으로 제공됩니다. 세 번째 매개 변수는 스레드 지역 변수입니다. 마지막 매개 변수는 반환 형식입니다. 이 경우 반환 형식은 <xref:System.Int64>입니다. 이 형식이 사용자가 <xref:System.Threading.Tasks.Parallel.For%2A> 형식 인수에 지정한 형식이기 때문입니다. 해당 변수의 이름은 `subtotal`로 지정되며 람다 식에 의해 반환됩니다. 반환 값은 이후에 루프가 반복될 때마다 `subtotal`을 초기화하는 데 사용됩니다. 또한 이 마지막 매개 변수를 각 반복에 전달된 다음 마지막 반복이 완료될 때 `localFinally` 대리자에게 전달되는 값으로 생각할 수 있습니다.  
  
 다섯 번째 매개 변수는 특정 스레드에 대한 모든 반복이 완료된 후 한 번 호출되는 메서드를 정의합니다. 입력 인수의 형식은 다시 <xref:System.Threading.Tasks.Parallel.For%60%601%28System.Int32%2CSystem.Int32%2CSystem.Func%7B%60%600%7D%2CSystem.Func%7BSystem.Int32%2CSystem.Threading.Tasks.ParallelLoopState%2C%60%600%2C%60%600%7D%2CSystem.Action%7B%60%600%7D%29> 메서드의 형식 인수 및 본문 람다 식에 의해 반환되는 형식에 해당합니다. 이 예제에서 값은 <xref:System.Threading.Interlocked.Add%2A?displayProperty=nameWithType> 메서드를 호출하여 스레드로부터 안전한 방법으로 클래스 범위에서 변수에 더해집니다. 스레드 지역 변수를 사용하여, 루프가 반복될 때마다 이 클래스 변수에 쓰는 것을 방지했습니다.  
  
 람다 식을 사용하는 방법은 [PLINQ 및 TPL의 람다 식](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [데이터 병렬 처리](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)
- [병렬 프로그래밍](../../../docs/standard/parallel-programming/index.md)
- [TPL(작업 병렬 라이브러리)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)
- [PLINQ 및 TPL의 람다 식](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)
