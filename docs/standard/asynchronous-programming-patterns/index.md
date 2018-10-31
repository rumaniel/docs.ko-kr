---
title: 비동기 프로그래밍 패턴
ms.date: 10/16/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- asynchronous design patterns, .NET
- .NET Framework, asynchronous design patterns
ms.assetid: 4ece5c0b-f8fe-4114-9862-ac02cfe5a5d7
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 50d76aef201fead37923a65cfeead16638b09842
ms.sourcegitcommit: b22705f1540b237c566721018f974822d5cd8758
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49452786"
---
# <a name="asynchronous-programming-patterns"></a>비동기 프로그래밍 패턴

.NET에서는 비동기 작업을 수행하기 위한 세 가지 패턴을 제공합니다.  

- 단일 메서드를 사용하여 비동기 작업 시작과 완료를 나타내는 **TAP(작업 기반 비동기 패턴)**. TAP는 .NET Framework 4에 도입되었습니다. **.NET에서 비동기 프로그램에 권장되는 방법입니다.** C#의 [async](~/docs/csharp/language-reference/keywords/async.md) 및 [await](~/docs/csharp/language-reference/keywords/await.md) 키워드와 Visual Basic의 [Async](~/docs/visual-basic/language-reference/modifiers/async.md) 및 [Await](~/docs/visual-basic/language-reference/operators/await-operator.md) 연산자는 TAP에 대한 언어 지원을 추가합니다. 자세한 내용은 [TAP(작업 기반 비동기 패턴)](task-based-asynchronous-pattern-tap.md)을 참조하세요.  

- 비동기 동작을 제공하기 위한 이벤트 기반 레거시 모델인 **EAP(이벤트 기반 비동기 패턴)**. 이 패턴에서는 `Async` 접미사가 있는 메서드가 필요하며 하나 이상의 이벤트, 이벤트 처리기 대리자 형식 및 `EventArg`에서 파생된 형식도 필요합니다. EAP는 .NET Framework 2.0에 도입되었습니다. 이 패턴 역시 신규 개발에서는 사용하지 않는 것이 좋습니다. 자세한 내용은 [EAP(이벤트 기반 비동기 패턴)](event-based-asynchronous-pattern-eap.md)를 참조하세요.  

- <xref:System.IAsyncResult> 인터페이스를 사용하여 비동기 동작을 제공하는 레거시 모델인 **APM(비동기 프로그래밍 모델)** 패턴(<xref:System.IAsyncResult> 패턴이라고도 함). 이 패턴에서는 동기 작업에 `Begin` 및 `End` 메소드(예를 들어 비동기 쓰기 작업을 구현하는 `BeginWrite` 및 `EndWrite`)가 필요합니다. 신규 개발에서는 이 패턴을 더 이상 사용하지 않는 것이 좋습니다. 자세한 내용은 [APM(비동기 프로그래밍 모델)](asynchronous-programming-model-apm.md)을 참조하세요.  
  
## <a name="comparison-of-patterns"></a>패턴 비교

위의 세 가지 패턴 모델이 비동기 작업을 수행하는 방법을 빠르게 비교하려는 경우 지정한 오프셋에서부터 지정된 양의 데이터를 제공된 버퍼로 읽어 들이는 `Read` 메서드를 사용할 수 있습니다.  
  
```csharp  
public class MyClass  
{  
    public int Read(byte [] buffer, int offset, int count);  
}  
```  

이 메서드에 해당하는 TAP 코드는 다음의 단일 `ReadAsync` 메서드를 노출합니다.  
  
```csharp
public class MyClass  
{  
    public Task<int> ReadAsync(byte [] buffer, int offset, int count);  
}  
```

그리고 이 메서드에 해당하는 EAP 코드는 다음 형식 및 멤버 집합을 노출합니다.  
  
```csharp  
public class MyClass  
{  
    public void ReadAsync(byte [] buffer, int offset, int count);  
    public event ReadCompletedEventHandler ReadCompleted;  
}  
```  
  
해당하는 APM 코드는 `BeginRead` 및 `EndRead` 메소드를 노출합니다.  
  
```csharp  
public class MyClass  
{  
    public IAsyncResult BeginRead(  
        byte [] buffer, int offset, int count,   
        AsyncCallback callback, object state);  
    public int EndRead(IAsyncResult asyncResult);  
}  
```  

## <a name="see-also"></a>참고 항목

- [비동기에 대한 자세한 설명](../async-in-depth.md)
- [C#의 비동기 프로그래밍](~/docs/csharp/async.md)
- [F#의 비동기 프로그래밍](~/docs/fsharp/tutorials/asynchronous-and-concurrent-programming/async.md)
- [Async 및 Await를 사용한 비동기 프로그래밍(Visual Basic)](~/docs/visual-basic/programming-guide/concepts/async/index.md)
