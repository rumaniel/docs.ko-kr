---
title: 컬렉션 이니셜라이저를 사용하여 사전을 초기화하는 방법 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 12/20/2018
helpviewer_keywords:
- collection initializers [C#], with Dictionary
ms.assetid: 25283922-f8ee-40dc-a639-fac30804ec71
ms.openlocfilehash: 22f80365b974df66999ac68f7bc2a9ffa7d445a5
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596811"
---
# <a name="how-to-initialize-a-dictionary-with-a-collection-initializer-c-programming-guide"></a>컬렉션 이니셜라이저를 사용하여 사전을 초기화하는 방법(C# 프로그래밍 가이드)

<xref:System.Collections.Generic.Dictionary%602>에는 키/값 쌍의 컬렉션이 있습니다. 해당 <xref:System.Collections.Generic.Dictionary%602.Add*> 메서드는 두 개의 매개 변수를 사용하며, 하나는 키에, 다른 하나는 값에 사용됩니다. <xref:System.Collections.Generic.Dictionary%602> 또는 여러 매개 변수를 사용하는 `Add` 메서드를 초기화하는 한 가지 방법은 다음 예제와 같이 각 매개 변수 집합을 중괄호로 묶는 것입니다. 또한 다음 예에서와 같이 인덱스 이니셜라이저를 사용하는 방법도 있습니다.

## <a name="example"></a>예

다음 코드 예제에서 <xref:System.Collections.Generic.Dictionary%602>는 `StudentName` 유형의 인스턴스를 사용하여 초기화됩니다.  첫 번째 초기화에서는 `Add` 메서드와 두 인수를 사용합니다. 컴파일러는 각 `int` 키 및 `StudentName` 값 쌍에 `Add`에 대한 호출을 생성합니다. 두 번째 초기화에서는 `Dictionary` 클래스의 공용 읽기/쓰기 인덱서 메서드를 사용합니다.

[!code-csharp[InitializerExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/HowToDictionaryInitializer.cs#HowToDictionaryInitializer)]  

첫 번째 선언에서 컬렉션의 각 요소에는 두 쌍의 중괄호가 있습니다. 안쪽 중괄호는 `StudentName`에 대한 개체 이니셜라이저를 묶고, 바깥쪽 중괄호는 `students`<xref:System.Collections.Generic.Dictionary%602>에 추가할 키/값 쌍에 대한 이니셜라이저를 묶습니다. 마지막으로, 사전에 대한 전체 컬렉션 이니셜라이저가 중괄호로 묶여 있습니다. 두 번째 초기화에서 할당의 왼쪽은 키이고, 오른쪽은 값이며 `StudentName`에 개체 이니셜라이저를 사용합니다.

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [개체 이니셜라이저 및 컬렉션 이니셜라이저](./object-and-collection-initializers.md)
