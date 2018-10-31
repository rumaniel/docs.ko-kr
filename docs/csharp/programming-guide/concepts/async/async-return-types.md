---
title: 비동기 반환 형식(C#)
ms.date: 05/29/2017
ms.assetid: ddb2539c-c898-48c1-ad92-245e4a996df8
ms.openlocfilehash: 3d3c7d610dd1287d2c7284a5edd9c92810a74dba
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48036242"
---
# <a name="async-return-types-c"></a>비동기 반환 형식(C#)
비동기 메서드의 반환 형식은 다음과 같을 수 있습니다.

- <xref:System.Threading.Tasks.Task%601> - 값을 반환하는 비동기 메서드의 경우 
 
-  <xref:System.Threading.Tasks.Task> - 작업을 수행하지만 아무 값도 반환하지 않는 비동기 메서드의 경우

- `void` - 이벤트 처리기의 경우 

- C# 7.0부터 액세스 가능한 `GetAwaiter` 메서드가 있는 모든 형식. `GetAwaiter` 메서드에서 반환된 개체는 <xref:System.Runtime.CompilerServices.ICriticalNotifyCompletion?displayProperty=nameWithType> 인터페이스를 구현해야 합니다.
  
비동기 메서드에 대한 자세한 내용은 [async 및 await를 사용한 비동기 프로그래밍(C#)](../../../../csharp/programming-guide/concepts/async/index.md)을 참조하세요.  
  
다음 섹션 중 하나에서 각 반환 형식을 살펴보고 세 가지 형식 모두를 사용하는 전체 예제는 이 항목의 끝에 나와 있습니다.  
  
##  <a name="BKMK_TaskTReturnType"></a> 작업\<TResult\> 반환 형식  
<xref:System.Threading.Tasks.Task%601> 반환 형식은 피연산자의 형식이 `TResult`인 [Return](../../../../csharp/language-reference/keywords/return.md)(C#) 문이 포함된 비동기 메서드에 사용합니다.  
  
다음 예제에서 `GetLeisureHours` 비동기 메서드는 정수를 반환하는 `return` 문을 포함합니다. 따라서 메서드 선언은 `Task<int>`의 반환 형식을 지정해야 합니다.  <xref:System.Threading.Tasks.Task.FromResult%2A> 비동기 메서드는 문자열을 반환하는 작업에 대한 자리 표시자입니다.
  
[!code-csharp[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-returns1.cs)]

`ShowTodaysInfo` 메서드의 await 식 내에서 `GetLeisureHours`를 호출하면 await 식이 `GetLeisureHours`에서 반환된 작업에 저장된 정수 값(`leisureHours` 값)을 검색합니다. await 식에 대한 자세한 내용은 [await](../../../../csharp/language-reference/keywords/await.md)를 참조하세요.  
  
다음 코드와 같이 `GetLeisureHours` 호출을 `await`의 적용과 구분하면 이 과정을 더욱 잘 이해할 수 있습니다. 곧바로 대기 상태가 되지 않는 `GetLeisureHours` 메서드를 호출하면 메서드 선언에서 예상한 대로 `Task<int>`를 반환합니다. 예제에서 작업이 `infoTask` 변수에 할당됩니다. `infoTask`가 <xref:System.Threading.Tasks.Task%601>이기 때문에 `TResult` 형식의 <xref:System.Threading.Tasks.Task%601.Result> 속성을 포함합니다. 이 경우 `TResult`는 정수 형식을 나타냅니다. `await`가 `infoTask`에 적용되는 경우 await 식은 `infoTask`의 <xref:System.Threading.Tasks.Task%601.Result%2A> 속성 내용으로 평가됩니다. 값은 `ret` 변수에 할당됩니다.  
  
> [!IMPORTANT]
>  <xref:System.Threading.Tasks.Task%601.Result%2A> 속성은 차단 속성입니다. 해당 작업이 완료되기 전에 액세스하려고 하면, 작업이 완료되고 값을 사용할 수 있을 때까지 현재 활성화된 스레드가 차단됩니다. 대부분의 경우 속성에 직접 액세스하지 않고 `await`를 사용하여 값에 액세스해야 합니다. <br/> 앞의 예제에서는 `ShowTodaysInfo` 메서드가 응용 프로그램 종료 전에 실행을 완료할 수 있도록 <xref:System.Threading.Tasks.Task%601.Result%2A> 속성의 값을 검색하여 주 스레드를 차단했습니다.  

[!code-csharp[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-returns1a.cs#1)]
  
##  <a name="BKMK_TaskReturnType"></a> Task 반환 형식  
`return` 문을 포함하지 않거나 피연산자를 반환하지 않는 `return` 문을 포함하는 비동기 메서드의 반환 형식은 일반적으로 <xref:System.Threading.Tasks.Task>입니다. 이러한 메서드는 동기적으로 실행될 경우 `void`를 반환합니다. 비동기 메서드에 대해 <xref:System.Threading.Tasks.Task> 반환 형식을 사용하는 경우 호출된 비동기 메서드가 완료될 때까지 호출 메서드는 `await` 연산자를 사용하여 호출자의 완료를 일시 중단할 수 있습니다.  
  
다음 예제에서 `WaitAndApologize` 비동기 메서드에는 `return` 문이 없으므로 메서드가 <xref:System.Threading.Tasks.Task> 개체를 반환합니다. 이렇게 하면 `WaitAndApologize`가 대기됩니다. <xref:System.Threading.Tasks.Task> 형식에는 반환 값이 없으므로 `Result` 속성이 포함되어 있지 않습니다.  

[!code-csharp[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-returns2.cs)]  
  
동기 void를 반환하는 메서드에 대한 호출 문과 비슷하게 await 식 대신 await 문을 사용하여 `WaitAndApologize`가 대기됩니다. 이 경우 await 연산자를 적용하면 값이 산출되지 않습니다.  
  
앞의 <xref:System.Threading.Tasks.Task%601> 예제처럼 다음 코드와 같이 `WaitAndApologize` 호출을 await 연산자의 적용과 구분할 수 있습니다. 그러나 `Task`에는 `Result` 속성이 없으므로 await 연산자가 `Task`에 적용될 때 값이 생성되지 않습니다.  
  
다음 코드에서는 `WaitAndApologize` 메서드 호출과 해당 메서드에서 반환하는 작업 대기를 구분합니다.  
 
[!code-csharp[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-returns2a.cs#1)]  
 
##  <a name="BKMK_VoidReturnType"></a> Void 반환 형식

`void`반환 형식이 필요한 비동기 이벤트 처리기에 `void` 반환 형식을 사용합니다. 값을 반환하지 않는 이벤트 처리기 이외의 메서드의 경우 `void`를 반환하는 비동기 메서드를 대기할 수 없기 때문에 <xref:System.Threading.Tasks.Task>를 대신 반환해야 합니다. 이러한 메서드의 호출자는 호출된 비동기 메서드가 마치는 것을 기다리지 않고 완료될 때까지 계속 진행할 수 있어야 하므로, 해당 호출자는 비동기 메서드가 생성하는 모든 값 또는 예외와 독립되어 있어야 합니다.  
  
void를 반환하는 비동기 메서드의 호출자는 메서드에서 throw되는 예외를 catch할 수 없으므로 이러한 처리되지 않은 예외를 사용하면 응용 프로그램이 실패할 수 있습니다. <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601>를 반환하는 비동기 메서드에서 예외가 발생하는 경우 이 예외는 반환된 작업에 저장되고 작업이 대기 상태일 때 다시 throw됩니다. 따라서 예외를 생성할 수 있는 모든 비동기 메서드에 <xref:System.Threading.Tasks.Task> 또는 <xref:System.Threading.Tasks.Task%601>의 반환 형식이 있고 메서드 호출이 대기 상태인지 확인해야 합니다.  
  
비동기 메서드에서 예외를 catch하는 방법에 대한 자세한 내용은 [try-catch](../../../language-reference/keywords/try-catch.md) 문서의 [비동기 메서드의 예외](../../../language-reference/keywords/try-catch.md#exceptions-in-async-methods)를 참조하세요.  
  
다음 예제에서는 비동기 이벤트 처리기의 동작을 보여줍니다. 예제 코드에서 비동기 이벤트 처리기는 주 스레드가 완료되면 이를 알려야 합니다. 그런 다음, 주 스레드는 비동기 이벤트 처리기가 프로그램을 종료하기 전에 완료될 때까지 대기할 수 있습니다.
 
[!code-csharp[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-returns3.cs)]  
 
## <a name="generalized-async-return-types-and-valuetasktresult"></a>일반화된 비동기 반환 형식 및 ValueTask\<TResult\>

C# 7.0부터 비동기 메서드는 액세스 가능한 `GetAwaiter` 메서드가 있는 모든 형식을 반환할 수 있습니다.
 
<xref:System.Threading.Tasks.Task> 및 <xref:System.Threading.Tasks.Task%601>는 참조 형식이므로 특히 타이트 루프에서 할당이 발생하는 경우 성능이 중요한 경로의 메모리 할당으로 인해 성능이 저하될 수 있습니다. 일반화된 반환 형식이 지원되면 추가 메모리 할당을 방지하기 위해 참조 형식 대신 간단한 값 형식을 반환할 수 있습니다. 

.NET에서는 값을 반환하는 일반화된 작업의 간단한 구현으로 <xref:System.Threading.Tasks.ValueTask%601?displayProperty=nameWithType> 구조체를 제공합니다. <xref:System.Threading.Tasks.ValueTask%601?displayProperty=nameWithType> 형식을 사용하려면 `System.Threading.Tasks.Extensions` NuGet 패키지를 프로젝트에 추가해야 합니다. 다음 예제에서는 <xref:System.Threading.Tasks.ValueTask%601> 구조체를 사용하여 두 주사위 굴리기 값을 검색합니다. 
  
[!code-csharp[return-value](../../../../../samples/snippets/csharp/programming-guide/async/async-valuetask.cs)]

## <a name="see-also"></a>참고 항목

- <xref:System.Threading.Tasks.Task.FromResult%2A>   
- [연습: async 및 await를 사용하여 웹에 액세스(C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
- [비동기 프로그램의 제어 흐름(C#)](../../../../csharp/programming-guide/concepts/async/control-flow-in-async-programs.md)   
- [async](../../../../csharp/language-reference/keywords/async.md)   
- [await](../../../../csharp/language-reference/keywords/await.md)
