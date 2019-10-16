---
title: 대리자 연산자 - C# 참조
ms.date: 07/18/2019
helpviewer_keywords:
- delegate [C#]
- anonymous method [C#]
ms.openlocfilehash: 1fe281776bd75d8fa869065cd24e85f04fec849d
ms.sourcegitcommit: 09d699aca28ae9723399bbd9d3d44aa0cbd3848d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68331832"
---
# <a name="delegate-operator-c-reference"></a>대리자 연산자(C# 참조)

`delegate` 연산자는 대리자 형식으로 변환될 수 있는 무명 메서드를 만듭니다.

[!code-csharp-interactive[anonymous method](~/samples/csharp/language-reference/operators/DelegateOperator.cs#AnonymousMethod)]

C# 3으로 시작하는 [람다 식](../../programming-guide/statements-expressions-operators/lambda-expressions.md)은 익명 함수를 만드는 더 간결하고 이해하기 쉬운 방법을 제공합니다. [=> 연산자](lambda-operator.md)를 사용하여 람다 식을 구성합니다.

[!code-csharp-interactive[lambda expression](~/samples/csharp/language-reference/operators/DelegateOperator.cs#Lambda)]

`delegate` 연산자를 사용하는 경우 매개 변수 목록을 생략할 수 있습니다. 이렇게 하면 다음 예제와 같이 매개 변수 목록을 사용하여 생성된 무명 메서드를 대리자 형식으로 변환할 수 있습니다.

[!code-csharp-interactive[no parameter list](~/samples/csharp/language-reference/operators/DelegateOperator.cs#WithoutParameterList)]

이 기능은 람다 식에서 지원되지 않는 무명 메서드의 유일한 기능입니다. 다른 모든 경우 인라인 코드를 작성하는 데 람다 식이 선호됩니다. 람다 식의 기능(예: 외부 변수 캡처)에 대한 자세한 내용은 [람다 식](../../programming-guide/statements-expressions-operators/lambda-expressions.md)을 참조하세요.

`delegate` 키워드를 사용하여 [대리자 형식](../builtin-types/reference-types.md#the-delegate-type)을 선언할 수도 있습니다.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [익명 함수 식](~/_csharplang/spec/expressions.md#anonymous-function-expressions) 섹션을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 연산자](index.md)
