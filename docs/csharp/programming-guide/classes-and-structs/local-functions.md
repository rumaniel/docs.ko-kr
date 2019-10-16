---
title: 로컬 함수 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 06/14/2017
helpviewer_keywords:
- local functions [C#]
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f572f683511fe90951f841c80eae448a9cb6054b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785082"
---
# <a name="local-functions-c-programming-guide"></a>로컬 함수(C# 프로그래밍 가이드)

C# 7.0부터 C#에서는 *로컬 함수*를 지원합니다. 로컬 함수는 다른 멤버에 중첩된 형식의 private 메서드입니다. 포함하는 멤버에서만 호출할 수 있습니다. 로컬 함수는 다음에서 선언하고 호출할 수 있습니다.

- 메서드, 특히 반복기 메서드 및 비동기 메서드
- 생성자
- 속성 접근자
- 이벤트 접근자
- 무명 메서드
- 람다 식
- 종료자
- 다른 로컬 함수

그러나 식 본문 멤버 내에서는 로컬 함수를 선언할 수 없습니다.

> [!NOTE]
> 로컬 함수에서도 지원하는 기능을 람다 식으로 구현할 수 있는 경우도 있습니다. 비교를 보려면 [로컬 함수 및 람다 식 비교](../../local-functions-vs-lambdas.md)를 참조하세요.

로컬 함수는 코드의 의도를 명확하게 합니다. 코드를 읽는 모든 사용자가 포함하는 메서드를 통해서만 메서드를 호출할 수 있음을 알 수 있습니다. 팀 프로젝트의 경우 로컬 함수를 사용하면 다른 개발자가 실수로 클래스 또는 구조체의 다른 곳에서 직접 메서드를 호출하는 경우를 방지할 수도 있습니다.
 
## <a name="local-function-syntax"></a>로컬 함수 구문

로컬 함수는 포함하는 멤버 내의 중첩 메서드로 정의됩니다. 해당 정의는 다음 구문을 사용합니다.

```txt
<modifiers: async | unsafe> <return-type> <method-name> <parameter-list>
```

로컬 함수는 [async](../../language-reference/keywords/async.md) 및 [unsafe](../../language-reference/keywords/unsafe.md) 한정자를 사용할 수 있습니다. 

해당 메서드 매개 변수를 비롯하여 포함하는 멤버에 정의된 모든 지역 변수는 로컬 함수에서 액세스할 수 있습니다. 

메서드 정의와 달리 로컬 함수 정의에는 다음 요소를 포함할 수 없습니다.

- 멤버 액세스 한정자. 모든 로컬 함수는 private이므로 `private` 키워드 등의 액세스 한정자를 포함하면 컴파일러 오류 CS0106,“이 항목의 ‘private’ 한정자가 유효하지 않습니다.”가 생성됩니다.
 
- [static](../../language-reference/keywords/static.md) 키워드입니다. `static` 키워드를 포함하면 컴파일러 오류 CS0106, “이 항목의 ‘static’ 한정자가 유효하지 않습니다.”가 생성됩니다.

또한 로컬 함수나 해당 매개 변수 및 형식 매개 변수에는 특성을 적용할 수 없습니다. 
 
다음 예제에서는 `GetText` 메서드에 대해 private인 로컬 함수 `AppendPathSeparator`를 정의합니다.
   
[!code-csharp[LocalFunctionExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions1.cs)]  
   
## <a name="local-functions-and-exceptions"></a>로컬 함수 및 예외

로컬 함수의 유용한 기능 중 하나는 예외가 즉시 나타나도록 할 수 있다는 것입니다. 메서드 반복기의 경우 반환된 시퀀스가 열거된 경우에만 예외가 나타나고 반복기를 검색할 때는 나타나지 않습니다. 비동기 메서드의 경우 비동기 메서드에서 throw된 예외는 반환된 작업을 대기할 때 관찰됩니다. 

다음 예제에서는 지정된 범위 사이의 홀수를 열거하는 `OddSequence` 메서드를 정의합니다. 100보다 큰 숫자를 `OddSequence` 열거자 메서드에 전달하기 때문에 메서드가 <xref:System.ArgumentOutOfRangeException>을 throw합니다. 예제의 출력에서 볼 수 있듯이 예외는 숫자를 반복하는 경우에만 나타나고 열거자를 검색할 때는 나타나지 않습니다.

[!code-csharp[LocalFunctionIterator1](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-iterator1.cs)] 

대신, 다음 예제와 같이 로컬 함수에서 반복기를 반환하여 유효성 검사를 수행할 때, 반복기를 검색하기 전에 예외를 throw할 수 있습니다.

[!code-csharp[LocalFunctionIterator2](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-iterator2.cs)]

유사한 방식으로 로컬 함수를 사용하여 비동기 작업 외부에서 예외를 처리할 수 있습니다. 일반적으로 비동기 메서드에서 throw된 예외의 경우 <xref:System.AggregateException>의 내부 예외를 검사해야 합니다. 로컬 함수를 사용하면 코드가 빨리 실패하여 예외가 throw되는 동시에 관찰할 수 있습니다.

다음 예제에서는 `GetMultipleAsync`라는 비동기 메서드를 사용하여 지정된 시간(초) 동안 일시 중지하고 해당 시간(초)의 임의 배수인 값을 반환합니다. 최대 지연 시간은 5초입니다. 값이 5보다 크면 <xref:System.ArgumentOutOfRangeException>이 발생합니다. 다음 예제와 같이 값 6이 `GetMultipleAsync` 메서드에 전달될 때 throw되는 예외는 `GetMultipleAsync` 메서드 실행이 시작된 후에 <xref:System.AggregateException>에 래핑됩니다.

[!code-csharp[LocalFunctionAsync`](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-async1.cs)] 

메서드 반복기와 마찬가지로, 이 예제의 코드를 리팩터링하여 비동기 메서드를 호출하기 전에 유효성 검사를 수행할 수 있습니다. 다음 예제의 출력에서 볼 수 있듯이, <xref:System.ArgumentOutOfRangeException>이 <xref:System.AggregateException>에 래핑되지 않습니다.

[!code-csharp[LocalFunctionAsync`](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-async2.cs)] 

## <a name="see-also"></a>참고 항목

- [메서드](methods.md)
