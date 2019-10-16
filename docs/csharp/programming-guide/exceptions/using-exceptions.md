---
title: 예외 사용 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- exception handling [C#], about exception handling
- exceptions [C#], about exceptions
ms.assetid: 71472c62-320a-470a-97d2-67995180389d
ms.openlocfilehash: 8d0fe4b8c2ba3e64aa7ee34fc9d02b29bda5c017
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69590174"
---
# <a name="using-exceptions-c-programming-guide"></a>예외 사용(C# 프로그래밍 가이드)
C#에서는 런타임 시 프로그램의 오류가 예외라는 메커니즘을 사용하여 프로그램 전체에 전파됩니다. 오류가 발생하는 코드에서 예외를 throw하고, 오류를 수정할 수 있는 코드에서 예외를 catch합니다. .NET Framework CLR(공용 언어 런타임) 또는 프로그램의 코드에서 예외를 throw할 수 있습니다. 예외가 throw되면 예외에 대한 `catch` 문이 발견될 때까지 호출 스택이 전파됩니다. Catch되지 않은 예외는 대화 상자를 표시하는 시스템에서 제공하는 제네릭 예외 처리기에 의해 처리됩니다.  
  
 예외는 <xref:System.Exception>에서 파생된 클래스로 표현됩니다. 이 클래스는 예외의 형식을 식별하며 예외에 대한 세부 정보가 들어 있는 속성을 포함합니다. 예외를 throw하는 것에는 예외에서 파생된 클래스의 인스턴스를 만드는 것, 선택적으로 예외의 속성을 구성하는 것, 그리고 `throw` 키워드를 사용하여 개체를 throw하는 것이 포함됩니다. 예:  
  
 [!code-csharp[csProgGuideExceptions#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#1)]  
  
 예외가 throw되면 런타임은 현재 문을 확인하여 `try` 블록 내에 있는지 알아봅니다. 있는 경우, `try` 블록과 연결된 `catch` 블록을 확인하여 예외를 catch할 수 있는지 알아봅니다. `Catch` 블록은 일반적으로 예외 형식을 지정합니다. `catch` 블록의 형식이 예외와 동일한 형식이거나 예외의 기본 클래스인 경우 `catch` 블록이 메서드를 처리할 수 있습니다. 예:  
  
 [!code-csharp[csProgGuideExceptions#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#2)]  
  
 예외를 throw하는 문이 `try` 블록 내에 없거나 이를 감싸는 `try` 블록에 일치하는 `catch` 블록이 없는 경우 런타임은 호출 메서드에서 `try` 문과 `catch` 블록을 확인합니다. 런타임은 호출 스택까지 계속 확인하여 호환되는 `catch` 블록을 검색합니다. `catch` 블록을 찾아서 실행한 후에는 해당 `catch` 블록 다음의 문으로 제어가 전달됩니다.  
  
 `try` 문은 `catch` 블록을 둘 이상 포함할 수 있습니다. 예외를 처리할 수 있는 첫 번째 `catch` 문이 실행됩니다. 그 뒤의 `catch` 문은 호환되더라도 무시됩니다. 따라서 catch 블록은 가장 구체적인 것(또는 가장 많이 파생된 것)에서 가장 덜 구체적인 것 순으로 정렬해야 합니다. 예:  
  
 [!code-csharp[csProgGuideExceptions#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#3)]  
  
 `catch` 블록이 실행되기 전에 런타임은 `finally` 블록을 확인합니다. 프로그래머는 `Finally` 블록을 사용해 중단된 `try` 블록으로부터 남겨질 수 있는 모호한 상태를 정리하거나, 런타임 시 가비지 수집기를 기다리지 않은 채 외부 리소스(예: 그래픽 핸들, 데이터베이스 연결 또는 파일 스트림)를 해제하여 개체를 마무리할 수 있습니다. 예:  
  
 [!code-csharp[csProgGuideExceptions#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#4)]  
  
 `WriteByte()`에서 예외를 throw한 경우, `file.Close()`가 호출되지 않으면 파일을 다시 열려고 시도하는 두 번째 `try` 블록이 실패하고 파일이 잠금 상태로 유지됩니다. `finally` 블록은 예외가 throw되도 실행되므로, 이전 예제의 `finally` 블록을 통해 파일을 정확히 닫고 오류를 방지할 수 있습니다.  
  
 예외가 throw된 후 호출 스택에서 호환되는 `catch` 블록을 찾지 못하면 다음 세 가지 중 하나가 발생합니다.  
  
- 예외가 종료자 내부에 있으면 종료자가 중단되고 기본 종료자(있는 경우)가 호출됩니다.  
  
- 호출 스택에 정적 생성자 또는 정적 필드 이니셜라이저가 포함된 경우 새 예외의 <xref:System.Exception.InnerException%2A> 속성에 할당된 원래 예외와 함께 <xref:System.TypeInitializationException>이 throw됩니다.  
  
- 스레드의 시작에 도달하면 스레드가 종료됩니다.  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [예외 및 예외 처리](./index.md)
