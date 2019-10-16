---
title: 익명 함수 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- lambda expressions [C#], as anonymous functions
- anonymous functions [C#]
- anonymous methods [C#]
ms.assetid: 6ce3f04d-0c71-4728-9127-634c7e9a8365
ms.openlocfilehash: 078596dcbfd907be53cae2ab3e7dcaa9e311c3f4
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69588824"
---
# <a name="anonymous-functions-c-programming-guide"></a>익명 함수(C# 프로그래밍 가이드)

익명 함수는 대리자 형식이 예상되는 곳에서 항상 사용할 수 있는 “인라인” 문 또는 식입니다. 이를 사용하여 명명된 대리자를 초기화하거나 명명된 대리자 형식 대신 이를 메서드 매개 변수로 전달할 수 있습니다.

[람다 식](lambda-expressions.md) 또는 [무명 메서드](../../language-reference/operators/delegate-operator.md)를 사용하여 익명 함수를 만들 수 있습니다. 인라인 코드를 작성하는 더 간결하고 이해하기 쉬운 방법을 제공하는 람다 식을 사용하는 것이 좋습니다. 무명 메서드와 달리 일부 형식의 람다 식은 식 트리 형식으로 변환될 수 있습니다.

## <a name="the-evolution-of-delegates-in-c"></a>C\#에서 대리자의 발전

 C# 1.0에서는 코드의 다른 위치에 정의된 메서드를 사용하여 명시적으로 초기화하는 방식으로 대리자의 인스턴스를 만들었습니다. C# 2.0에서는 대리자 호출에서 실행될 수 있는 이름 없는 인라인 문 블록을 작성하는 방법으로 무명 메서드의 개념을 소개했습니다. C# 3.0에서는 개념적으로 무명 메서드와 비슷하지만 더 간결하고 표현이 다양한 람다 식을 소개했습니다. 이러한 두 기능을 함께 *익명 함수*라고 합니다. 일반적으로 .NET Framework의 버전 3.5 이상을 대상으로 하는 애플리케이션은 람다 식을 사용해야 합니다.  
  
 다음 예제에서는 C# 1.0에서 C# 3.0까지 대리자 만들기의 발전을 보여 줍니다.  
  
 [!code-csharp[csProgGuideLINQ#65](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#65)]  
  
## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [익명 함수 식](~/_csharplang/spec/expressions.md#anonymous-function-expressions) 섹션을 참조하세요.
  
## <a name="see-also"></a>참고 항목

- [문, 식, 연산자](./index.md)
- [람다 식](./lambda-expressions.md)
- [대리자](../delegates/index.md)
- [식 트리(C#)](../concepts/expression-trees/index.md)
