---
title: '방법: 개체 이니셜라이저를 사용하여 개체 초기화 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 12/20/2018
helpviewer_keywords:
- object initializers [C#], how to use
- objects [C#], initializing
ms.assetid: 4b75ebb2-2e29-43de-929c-d736a8f27ce6
ms.openlocfilehash: 7b31e28c23a70e9f0794c82feb2a984c40ee9d0f
ms.sourcegitcommit: 4c41ec195caf03d98b7900007c3c8e24eba20d34
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67267575"
---
# <a name="how-to-initialize-objects-by-using-an-object-initializer-c-programming-guide"></a>방법: 개체 이니셜라이저를 사용하여 개체 초기화(C# 프로그래밍 가이드)

개체 이니셜라이저를 사용하여 형식에 대한 생성자를 명시적으로 호출하지 않고 선언적 방식으로 형식 개체를 초기화할 수 있습니다.  
  
다음 예제에서는 명명된 개체와 함께 개체 이니셜라이저를 사용하는 방법을 보여 줍니다. 컴파일러는 먼저 기본 인스턴스 생성자에 액세스한 다음 멤버 초기화를 처리하여 개체 이니셜라이저를 처리합니다. 따라서 클래스에서 매개 변수가 없는 생성자가 `private`으로 선언된 경우 공용 액세스가 필요한 개체 이니셜라이저는 실패합니다.
  
무명 형식을 정의하는 경우 개체 이니셜라이저를 사용해야 합니다. 자세한 내용은 [방법: 쿼리에서 요소 속성의 하위 집합 반환](how-to-return-subsets-of-element-properties-in-a-query.md)을 참조하세요.  
  
## <a name="example"></a>예  

다음 예제에서는 개체 이니셜라이저를 사용하여 새 `StudentName` 형식을 초기화하는 방법을 보여 줍니다. 이 예제에서는 `StudentName` 형식의 속성을 설정합니다.
  
[!code-csharp[InitializerObjectExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/HowToObjectInitializers.cs#HowToObjectInitializers)]  

개체 이니셜라이저를 사용하여 개체의 이니셜라이저를 설정할 수 있습니다. 다음 예제에서는 인덱서를 사용하여 여러 포지션의 선수를 가져오고 설정하는 `BaseballTeam` 클래스를 정의합니다. 이 이니셜라이저는 포지션을 가리키는 약어 또는 각 포지션에 사용되는 번호를 기준으로 선수에게 야구 득점표를 할당할 수 있습니다.

[!code-csharp[InitializerIndexerExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/HowToIndexInitializer.cs#HowToIndexInitializer)]  

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [개체 이니셜라이저 및 컬렉션 이니셜라이저](object-and-collection-initializers.md)
