---
title: async - C# 참조
ms.custom: seodec18
ms.date: 05/22/2017
f1_keywords:
- async_CSharpKeyword
helpviewer_keywords:
- async keyword [C#]
- async method [C#]
- async [C#]
ms.assetid: 16f14f09-b2ce-42c7-a875-e4eca5d50674
ms.openlocfilehash: ab9c1be484d9cc77324e3105124a1b1f2257251d
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70925352"
---
# <a name="async-c-reference"></a>async(C# 참조)

`async` 한정자를 사용하여 메서드, [람다 식](../../programming-guide/statements-expressions-operators/lambda-expressions.md) 또는 [무명 메서드](../operators/delegate-operator.md)를 비동기로 지정합니다. 메서드 또는 식에 이 한정자를 사용하면 *비동기 메서드*라고 합니다. 다음 예제에서는 `ExampleMethodAsync`라는 비동기 메서드를 정의합니다.
  
```csharp  
public async Task<int> ExampleMethodAsync()  
{  
    // . . . .  
}  
```  

비동기 프로그래밍이 처음이거나 비동기 메서드가 [`await` 연산자](../operators/await.md)를 사용하여 호출자의 스레드를 차단하지 않고 장기 실행 작업을 수행할 수 있는 방법을 잘 모르겠으면 [async 및 await를 사용한 비동기 프로그래밍](../../programming-guide/concepts/async/index.md)의 소개 내용을 참조하세요. 다음 코드는 비동기 메서드 안에 있으며 <xref:System.Net.Http.HttpClient.GetStringAsync%2a?displayProperty=nameWithType> 메서드를 호출합니다.
  
```csharp  
string contents = await httpClient.GetStringAsync(requestUrl);  
```  
  
비동기 메서드는 대기 중인 작업이 완료될 때까지 메서드가 일시 중단되는 지점인 첫 번째 `await` 식에 도달하기 전에는 동기적으로 실행됩니다. 다음 단원의 예제에서처럼 그 동안에는 제어가 메서드 호출자에게 반환됩니다.  
  
`async` 키워드에서 수정하는 메서드에 `await` 식 또는 문이 없는 경우 해당 메서드가 동기적으로 실행됩니다. `await` 문이 포함되지 않은 모든 비동기 메서드에서는 오류가 발생할 수 있으므로 컴파일러 경고가 나타납니다. [컴파일러 경고(수준 1) CS4014](../compiler-messages/cs4014.md)를 참조하세요.  
  
 `async` 키워드는 메서드, 람다 식 또는 무명 메서드를 수정할 때만 키워드로 사용됩니다. 다른 모든 컨텍스트에서는 식별자로 해석됩니다.  
  
## <a name="example"></a>예  
다음 예제에서는 비동기 이벤트 처리기, `StartButton_Click`, 비동기 메서드 및 `ExampleMethodAsync` 간의 제어 흐름과 구조를 보여 줍니다. 비동기 메서드의 결과는 웹 페이지의 문자 수입니다. 이 코드는 Visual Studio에서 만든 WPF(Windows Presentation Foundation) 앱 또는 Windows 스토어 앱에 적합합니다. 앱을 설정하는 방법은 코드 주석을 참조하세요.  

Visual Studio에서 이 코드를 WPF(Windows Presentation Foundation) 앱 또는 Windows 스토어 앱으로 실행할 수 있습니다. `StartButton`이라는 Button 컨트롤과 `ResultsTextBox`라는 Textbox 컨트롤이 필요합니다. 다음과 같이 작성되도록 이름과 처리기를 설정해야 합니다.  

```xaml
<Button Content="Button" HorizontalAlignment="Left" Margin="88,77,0,0" VerticalAlignment="Top" Width="75"  
        Click="StartButton_Click" Name="StartButton"/>  
<TextBox HorizontalAlignment="Left" Height="137" Margin="88,140,0,0" TextWrapping="Wrap"   
         Text="&lt;Enter a URL&gt;" VerticalAlignment="Top" Width="310" Name="ResultsTextBox"/>  
```
  
코드를 WPF 앱으로 실행하려면  

- 이 코드를 MainWindow.xaml.cs의 `MainWindow` 클래스에 붙여넣습니다.  
- System.Net.Http에 대한 참조를 추가합니다.  
- System.Net.Http에 대한 `using` 지시문을 추가합니다.  
  
코드를 Windows 스토어 앱으로 실행하려면  

- 이 코드를 MainPage.xaml.cs의 `MainPage` 클래스에 붙여넣습니다.  
- System.Net.Http 및 System.Threading.Tasks에 대한 using 지시문을 추가합니다.  
  
[!code-csharp[wpf-async](../../../../samples/snippets/csharp/language-reference/keywords/async/wpf/mainwindow.xaml.cs#1)]
  
> [!IMPORTANT]
> 작업 및 작업 완료를 기다리는 동안 실행되는 코드에 대한 자세한 내용은 [async 및 await를 사용한 비동기 프로그래밍](../../programming-guide/concepts/async/index.md)을 참조하세요. 비슷한 요소를 사용하는 전체 WPF 예제를 보려면 [연습: Async 및 Await를 사용하여 웹에 액세스](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)를 참조하세요.  
  
## <a name="return-types"></a>반환 형식  
비동기 메서드의 반환 형식은 다음과 같을 수 있습니다.

- <xref:System.Threading.Tasks.Task>
- <xref:System.Threading.Tasks.Task%601>
- [void](./void.md). `async void` 메서드는 호출자가 `await` 해당 메서드를 사용할 수 없으며 성공적으로 완료 또는 오류 조건을 보고하는 다른 메커니즘을 구현해야 하기 때문에 이벤트 처리기 이외의 코드에 대해 일반적으로 사용되지 않습니다.
- C# 7.0부터 액세스 가능한 `GetAwaiter` 메서드가 있는 모든 형식. `System.Threading.Tasks.ValueTask<TResult>` 형식은 이러한 구현 중 하나입니다. NuGet 패키지 `System.Threading.Tasks.Extensions`를 추가하면 사용할 수 있습니다. 

비동기 메서드는 모든 [in](./in-parameter-modifier.md), [ref](./ref.md) 또는 [out](./out-parameter-modifier.md) 매개 변수를 선언할 수 없고 [참조 반환 값](../../programming-guide/classes-and-structs/ref-returns.md)을 가질 수도 없지만, 이러한 매개 변수가 있는 메서드를 호출할 수는 있습니다.  
  
메서드의 [return](./return.md) 문에서 `TResult` 형식의 피연산자를 지정할 경우 비동기 메서드의 반환 형식으로 `Task<TResult>`를 지정합니다. 메서드가 완료되었을 때 의미 있는 값이 반환되지 않을 경우 `Task`를 사용합니다. 즉, 이 메서드를 호출하면 `Task`가 반환되지만 `Task`가 완료되면 `await`를 기다리는 모든 `Task` 식이 `void`가 됩니다.  
  
`void` 반환 형식은 주로 해당 반환 형식이 필요한 이벤트 처리기를 정의할 때 사용합니다. `void` 반환 비동기 메서드의 호출자는 기다릴 수 없으므로 메서드가 throw하는 예외를 catch할 수 없습니다.  

C# 7.0부터 `GetAwaiter` 메서드가 있는 다른 형식(일반적으로 값 형식)을 반환하여 성능이 중요한 코드 섹션에서 메모리 할당을 최소화합니다. 

자세한 내용과 예제는 [비동기 반환 형식](../../programming-guide/concepts/async/async-return-types.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Runtime.CompilerServices.AsyncStateMachineAttribute>
- [await](../operators/await.md)
- [연습: Async 및 Await를 사용하여 웹에 액세스](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)
- [Async 및 Await를 사용한 비동기 프로그래밍](../../programming-guide/concepts/async/index.md)
