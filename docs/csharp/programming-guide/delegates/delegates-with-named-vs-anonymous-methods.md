---
title: '대리자 비교: 명명된 메서드 및 무명 메서드 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- delegates [C#], with named vs. anonymous methods
- methods [C#], in delegates
ms.assetid: 98fa8c61-66b6-4146-986c-3236c4045733
ms.openlocfilehash: 9df143fb183ef2fc7e951b2cee47d18ce4b11942
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69590652"
---
# <a name="delegates-with-named-vs-anonymous-methods-c-programming-guide"></a>대리자 비교: 명명된 메서드 및 무명 메서드(C# 프로그래밍 가이드)
[대리자](../../language-reference/keywords/delegate.md)는 명명된 메서드에 연결할 수 있습니다. 명명된 메서드를 사용하여 대리자를 인스턴스화하면 메서드가 매개 변수로 전달됩니다. 예를 들면 다음과 같습니다.  
  
 [!code-csharp[csProgGuideDelegates#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#1)]  
  
 이 코드는 명명된 메서드를 사용하여 호출됩니다. 명명된 메서드를 사용하여 생성된 대리자는 [정적](../../language-reference/keywords/static.md) 메서드 또는 인스턴스 메서드를 캡슐화할 수 있습니다. 명명된 메서드는 이전 버전의 C#에서 대리자를 인스턴스화할 수 있는 유일한 방법입니다. 그러나 새 메서드 생성이 불필요한 오버헤드인 경우 C#에서 대리자를 인스턴스화하고 호출 시 대리자에서 처리할 코드 블록을 즉시 지정할 수 있습니다. 블록에는 람다 식 또는 무명 메서드가 포함될 수 있습니다. 자세한 내용은 [무명 함수](../statements-expressions-operators/anonymous-functions.md)를 참조하세요.  
  
## <a name="remarks"></a>설명  
 대리자 매개 변수로 전달하는 메서드에는 대리자 선언과 동일한 시그니처가 있어야 합니다.  
  
 대리자 인스턴스는 정적 또는 인스턴스 메서드를 캡슐화할 수 있습니다.  
  
 대리자는 [out](../../language-reference/keywords/out-parameter-modifier.md) 매개 변수를 사용할 수 있지만, 멀티캐스트 이벤트 대리자의 경우 호출될 대리자를 알 수 없기 때문에 사용하지 않는 것이 좋습니다.  
  
## <a name="example-1"></a>예제 1  
 다음은 대리자를 선언하고 사용하는 간단한 예제입니다. 대리자 `Del` 및 연결된 메서드 `MultiplyNumbers`에 동일한 시그니처가 있습니다.  
  
 [!code-csharp[csProgGuideDelegates#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#2)]  
  
## <a name="example-2"></a>예제 2  
 다음 예제에서는 한 대리자가 정적 메서드와 인스턴스 메서드 모두에 매핑되며 각각의 특정 정보를 반환합니다.  
  
 [!code-csharp[csProgGuideDelegates#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#3)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [대리자](./index.md)
- [방법: 대리자 조합(멀티캐스트 대리자)](./how-to-combine-delegates-multicast-delegates.md)
- [이벤트](../events/index.md)
