---
title: interface(C# 참조)
ms.date: 07/20/2015
f1_keywords:
- interface_CSharpKeyword
helpviewer_keywords:
- interface keyword [C#]
ms.assetid: 7da38e81-4f99-4bc5-b07d-c986b687eeba
ms.openlocfilehash: 4adc7ba106e0044ba6aff94ea3180d9c8e3ded7b
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48872945"
---
# <a name="interface-c-reference"></a>interface(C# 참조)

인터페이스에는 [메서드](../../programming-guide/classes-and-structs/methods.md), [속성](../../programming-guide/classes-and-structs/properties.md), [이벤트](../../programming-guide/events/index.md) 또는 [인덱서](../../programming-guide/indexers/index.md)의 시그니처만 포함됩니다. 인터페이스를 구현하는 클래스나 구조체는 인터페이스 정의에서 지정된 인터페이스 멤버를 구현해야 합니다. 다음 예제에서 `ImplementationClass` 클래스는 매개 변수가 없고 `void`를 반환하는 `SampleMethod`라는 메서드를 구현해야 합니다.

자세한 내용과 예제는 [인터페이스](../../programming-guide/interfaces/index.md)를 참조하세요.

## <a name="example"></a>예

[!code-csharp[csrefKeywordsTypes#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#14)]

인터페이스는 네임스페이스 또는 클래스의 멤버일 수 있으며 다음 멤버의 시그니처를 포함할 수 있습니다.

- [메서드](../../programming-guide/classes-and-structs/methods.md)

- [속성](../../programming-guide/classes-and-structs/using-properties.md)

- [인덱서](../../programming-guide/indexers/using-indexers.md)

- [이벤트](event.md)

인터페이스는 하나 이상의 기본 인터페이스에서 상속할 수 있습니다.

기본 형식 목록에 기본 클래스 및 인터페이스가 포함된 경우 기본 클래스가 목록의 첫 번째 항목이어야 합니다.

인터페이스를 구현하는 클래스는 해당 인터페이스의 멤버를 명시적으로 구현할 수 있습니다. 명시적으로 구현된 멤버는 클래스 인스턴스를 통해 액세스할 수 없고 인터페이스 인스턴스를 통해서만 액세스할 수 있습니다.

명시적 인터페이스 구현에 대한 자세한 내용과 코드 예제는 [명시적 인터페이스 구현](../../programming-guide/interfaces/explicit-interface-implementation.md)을 참조하세요.

## <a name="example"></a>예

다음 예제에서는 인터페이스의 구현 방법을 보여 줍니다. 이 예제에서 인터페이스에는 속성 선언이 포함되어 있고, 클래스에는 구현이 포함되어 있습니다. `IPoint`를 구현하는 클래스의 모든 인스턴스에는 정수 속성 `x` 및 `y`가 있습니다.

[!code-csharp[csrefKeywordsTypes#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#15)]

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../../../csharp/language-reference/index.md)  
- [C# 프로그래밍 가이드](../../programming-guide/index.md)  
- [C# 키워드](index.md)  
- [참조 형식](reference-types.md)  
- [인터페이스](../../programming-guide/interfaces/index.md)  
- [속성 사용](../../programming-guide/classes-and-structs/using-properties.md)  
- [인덱서 사용](../../programming-guide/indexers/using-indexers.md)  
- [class](class.md)  
- [struct](struct.md)  
- [인터페이스](../../programming-guide/interfaces/index.md)
