---
title: 문 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- statements [C#], about statements
- C# language, statements
ms.assetid: 901bcde7-87de-4e15-833c-f9cfd40c8ce3
ms.openlocfilehash: 2c50d9e8db2668f2138653858e42b8ed07d3e1e9
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70168959"
---
# <a name="statements-c-programming-guide"></a>문(C# 프로그래밍 가이드)
프로그램이 수행하는 작업은 문으로 표현됩니다. 일반적인 작업으로 지정된 조건에 따라 변수 선언, 값 할당, 메서드 호출, 컬렉션 반복, 하나 또는 다른 코드 블록으로 분기 등이 있습니다. 프로그램에서 문이 실행되는 순서를 제어 흐름 또는 실행 흐름이라고 합니다. 제어 흐름은 프로그램이 런타임 시 수신하는 입력에 대응하는 방식에 따라 프로그램을 실행할 때마다 달라질 수 있습니다.  
  
 문은 세미콜론으로 끝나는 코드 한 줄이나 일련의 한 줄 문으로 이루어진 블록일 수 있습니다. 문 블록은 {} 괄호로 묶여 있으며 중첩 블록을 포함할 수 있습니다. 다음 코드는 한 줄 문과 여러 줄 문 블록의 두 가지 예제를 보여 줍니다.  
  
 [!code-csharp[csProgGuideStatements#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#1)]  
  
## <a name="types-of-statements"></a>문 유형  
 다음 표에는 다양한 유형의 C# 문과 관련 키워드가 나와 있으며 자세한 정보를 포함하는 항목에 대한 링크가 있습니다.  
  
|범주|C# 키워드/참고 사항|  
|--------------|---------------------------|  
|[선언문](#declaration-statements)|선언문은 새 변수 또는 상수를 소개합니다. 필요에 따라 변수 선언에서 변수에 값을 할당할 수 있습니다. 상수 선언에서 대입은 필수입니다.|  
|[식 문](expressions.md)|값을 계산하는 식 문은 값을 변수에 저장해야 합니다. 자세한 내용은 [식 문](#expression-statements)을 참조하세요.|  
|선택 영역 문|선택 문을 사용하면 하나 이상의 지정된 조건에 따라 코드의 다른 섹션으로 분기할 수 있습니다. 자세한 내용은 다음 항목을 참조하세요.<br /><br /> [if](../../language-reference/keywords/if-else.md), [else](../../language-reference/keywords/if-else.md), [switch](../../language-reference/keywords/switch.md), [case](../../language-reference/keywords/switch.md)|  
|반복 문|반복 문을 사용하면 배열과 같은 컬렉션을 반복하거나, 지정한 조건이 충족될 때까지 동일한 문 집합을 반복해서 수행할 수 있습니다. 자세한 내용은 다음 항목을 참조하세요.<br /><br /> [do](../../language-reference/keywords/do.md), [for](../../language-reference/keywords/for.md), [foreach](../../language-reference/keywords/foreach-in.md), [in](../../language-reference/keywords/foreach-in.md), [while](../../language-reference/keywords/while.md)|  
|점프 문|점프 문은 컨트롤을 다른 코드 섹션으로 전송합니다. 자세한 내용은 다음 항목을 참조하세요.<br /><br /> [break](../../language-reference/keywords/break.md), [continue](../../language-reference/keywords/continue.md), [default](../../language-reference/keywords/switch.md), [goto](../../language-reference/keywords/goto.md), [return](../../language-reference/keywords/return.md), [yield](../../language-reference/keywords/yield.md)|  
|예외 처리 문|예외 처리 문을 사용하면 런타임 시 발생하는 예외 조건에서 정상적으로 복구할 수 있습니다. 자세한 내용은 다음 항목을 참조하세요.<br /><br /> [throw](../../language-reference/keywords/throw.md), [try-catch](../../language-reference/keywords/try-catch.md), [try-finally](../../language-reference/keywords/try-finally.md), [try-catch-finally](../../language-reference/keywords/try-catch-finally.md)|  
|[Checked 및 Unchecked](../../language-reference/keywords/checked-and-unchecked.md)|checked 및 unchecked 문을 사용하면 결과가 저장되는 변수가 너무 작아서 결과 값을 수용할 수 없는 경우 수치 연산에서 오버플로가 발생할 수 있는지 여부를 지정할 수 있습니다. 자세한 내용은 [checked](../../language-reference/keywords/checked.md) 및 [unchecked](../../language-reference/keywords/unchecked.md)를 참조하세요.|  
|`await` 문|메서드에 [async](../../language-reference/keywords/async.md) 한정자를 표시하면 메서드에서 [await](../../language-reference/operators/await.md) 연산자를 사용할 수 있습니다. 컨트롤이 비동기 메서드의 `await` 식에 도달하면 컨트롤이 호출자로 돌아가고 대기 중인 작업이 완료될 때까지 메서드의 진행이 일시 중단됩니다. 작업이 완료되면 메서드가 실행이 다시 시작될 수 있습니다.<br /><br /> 간단한 예제는 [메서드](../classes-and-structs/methods.md)의 "Async 메서드" 섹션을 참조하세요. 자세한 내용은 [async 및 await를 사용한 비동기 프로그래밍](../concepts/async/index.md)을 참조하세요.|  
|`yield return` 문|반복기는 배열 목록과 같은 컬렉션에 대해 사용자 지정 반복을 수행합니다. 반복기는 [yield return](../../language-reference/keywords/yield.md) 문을 사용하여 각 요소를 한 번에 하나씩 반환합니다. `yield return` 문에 도달하면 코드의 현재 위치가 기억됩니다. 다음에 반복기가 호출되면 해당 위치에서 실행이 다시 시작됩니다.<br /><br /> 자세한 내용은 [반복기](../concepts/iterators.md)를 참조하세요.|  
|`fixed` 문|fixed 문은 가비지 수집기에서 이동 가능한 변수를 재배치할 수 없도록 합니다. 자세한 내용은 [fixed](../../language-reference/keywords/fixed-statement.md)를 참조하세요.|  
|`lock` 문|lock 문을 사용하면 한 번에 하나의 스레드만 코드 블록에 액세스할 수 있도록 제한할 수 있습니다. 자세한 내용은 [lock](../../language-reference/keywords/lock-statement.md)을 참조하세요.|  
|레이블 문|문에 레이블을 지정한 다음 [goto](../../language-reference/keywords/goto.md) 키워드를 사용하여 레이블 문으로 점프합니다. 다음 행의 예제를 참조하세요.|  
|[빈 명령문](#the-empty-statement)|빈 문은 하나의 세미콜론으로 구성됩니다. 아무 작업도 수행하지 않으며, 문이 필요하지만 아무 작업도 수행할 필요가 없는 위치에서 사용할 수 있습니다.|  
  
## <a name="declaration-statements"></a>선언문

다음 코드는 초기 할당이 있거나 할당되지 않은 변수 선언과 필요한 초기화가 있는 상수 선언의 예를 보여 줍니다.

 [!code-csharp[csProgGuideStatements#23](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#23)]

## <a name="expression-statements"></a>식 문

다음 코드는 할당, 할당을 통한 개체 만들기 및 메서드 호출을 포함하는 식 명문의 예를 보여 줍니다.

 [!code-csharp[csProgGuideStatements#24](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#24)]

## <a name="the-empty-statement"></a>빈 문

다음 예제에서는 빈 문의 두 가지 사용을 보여 줍니다.

 [!code-csharp[csProgGuideStatements#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#25)]

## <a name="embedded-statements"></a>포함 문

 [do](../../language-reference/keywords/do.md), [while](../../language-reference/keywords/while.md), [for](../../language-reference/keywords/for.md) 및 [foreach](../../language-reference/keywords/foreach-in.md)를 비롯한 일부 문은 항상 포함 문이 뒤에 나옵니다. 이 포함 명령문은 단일 명령문이나 명령문 블록에서 {} 괄호로 묶인 여러 명령문일 수 있습니다. 한 줄로 된 각 포함 명령문을 다음 예제와 같이 {} 괄호로 묶을 수 있습니다.  
  
 [!code-csharp[csProgGuideStatements#26](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#26)]  
  
 {} 괄호로 묶이지 않은 포함 문은 선언문 또는 레이블 문이 될 수 없습니다. 이는 다음 예제에서 확인할 수 있습니다.  
  
 [!code-csharp[csProgGuideStatements#27](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#27)]  
  
 오류를 해결하려면 포함 문을 블록에 배치합니다.  
  
 [!code-csharp[csProgGuideStatements#28](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#28)]  
  
## <a name="nested-statement-blocks"></a>중첩된 문 블록  
 다음 코드와 같이 문 블록을 중첩할 수 있습니다.  
  
 [!code-csharp[csProgGuideStatements#29](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#29)]  
  
## <a name="unreachable-statements"></a>연결할 수 없는 문  
 상황에 따라 제어 흐름이 특정 문에 연결할 수 없다고 확인될 경우 컴파일러는 다음 예제와 같이 경고 CS0162를 생성합니다.  
  
 [!code-csharp[csProgGuideStatements#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#22)]  
  
## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [문](~/_csharplang/spec/statements.md) 섹션을 참조하세요.
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [문 키워드](../../language-reference/keywords/statement-keywords.md)  
- [식](expressions.md)  
