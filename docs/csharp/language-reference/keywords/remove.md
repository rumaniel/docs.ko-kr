---
title: 상황별 키워드 제거 - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- remove_CSharpKeyword
helpviewer_keywords:
- remove event accessor [C#]
ms.assetid: c8223426-c17b-4fe2-8406-01564cf1dd2b
ms.openlocfilehash: b5c604cbb0fef158750b0fa487374ab293795fc7
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65633715"
---
# <a name="remove-c-reference"></a>remove(C# 참조)

`remove` 상황별 키워드는 클라이언트 코드가 [event](event.md)에서 구독을 취소할 때 호출되는 사용자 지정 이벤트 접근자를 정의하는 데 사용됩니다. 사용자 지정 `remove` 접근자를 제공하는 경우 [add](add.md) 접근자도 제공해야 합니다.

## <a name="example"></a>예제

다음 예제에서는 사용자 지정 [add](add.md) 및 `remove` 접근자가 있는 이벤트를 보여 줍니다. 전체 예제를 보려면 [방법:  인터페이스 이벤트 구현](../../programming-guide/events/how-to-implement-interface-events.md)을 참조하세요.

 [!code-csharp[csrefKeywordsContextual#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsContextual/CS/csrefKeywordsContextual.cs#15)]

일반적으로 고유한 사용자 지정 이벤트 접근자를 제공할 필요가 없습니다. 이벤트를 선언할 때 컴파일러에서 자동으로 생성되는 접근자만으로도 대부분의 시나리오에 충분합니다.

## <a name="see-also"></a>참고 항목

- [이벤트](../../programming-guide/events/index.md)
