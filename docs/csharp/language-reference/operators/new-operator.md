---
title: new 연산자 - C# 참조
ms.custom: seodec18
ms.date: 06/25/2019
helpviewer_keywords:
- new operator keyword [C#]
ms.assetid: a212b697-a79b-4105-9923-1f7b108036e8
ms.openlocfilehash: 3d64c4805abe38c80301748ffa6b35fc87563b60
ms.sourcegitcommit: bab17fd81bab7886449217356084bf4881d6e7c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2019
ms.locfileid: "67403971"
---
# <a name="new-operator-c-reference"></a>new 연산자(C# 참조)

`new` 연산자는 새 유형의 인스턴스를 만듭니다.

`new` 키워드를 [멤버 선언 한정자](../keywords/new-modifier.md) 또는 [제네릭 형식 제약 조건](../keywords/new-constraint.md)으로 사용할 수도 있습니다.

## <a name="constructor-invocation"></a>생성자 호출

새 인스턴스 유형을 만들려면 일반적으로 `new` 연산자를 사용하여 해당 유형의 [생성자](../../programming-guide/classes-and-structs/constructors.md) 중 하나를 호출합니다.

[!code-csharp-interactive[invoke constructor](~/samples/csharp/language-reference/operators/NewOperator.cs#Constructor)]

다음 예제와 같이 `new` 연산자와 함께 [개체 또는 컬렉션 이니셜라이저](../../programming-guide/classes-and-structs/object-and-collection-initializers.md)를 사용하여 하나의 명령문에서 개체를 인스턴스화하고 초기화할 수 있습니다.

[!code-csharp-interactive[constructor with initializer](~/samples/csharp/language-reference/operators/NewOperator.cs#ConstructorWithInitializer)]

## <a name="array-creation"></a>배열 생성

또한 다음 예제와 같이 `new` 연산자를 사용하여 배열 인스턴스를 만듭니다.

[!code-csharp-interactive[create array](~/samples/csharp/language-reference/operators/NewOperator.cs#Array)]

배열 초기화 구문을 사용하여 배열 인스턴스를 만들고 하나의 명령문에 요소를 채웁니다. 다음 예제에서는 이를 수행하는 다양한 방법을 보여줍니다.

[!code-csharp-interactive[initialize array](~/samples/csharp/language-reference/operators/NewOperator.cs#ArrayInitialization)]

배열에 대한 자세한 내용은 [배열](../../programming-guide/arrays/index.md)을 참조하세요.

## <a name="instantiation-of-anonymous-types"></a>익명 형식의 인스턴스화

[익명 형식](../../programming-guide/classes-and-structs/anonymous-types.md)의 인스턴스를 만들려면 `new` 연산자와 개체 이니셜라이저 구문을 사용합니다.

[!code-csharp-interactive[anonymous type](~/samples/csharp/language-reference/operators/NewOperator.cs#AnonymousType)]

## <a name="destruction-of-type-instances"></a>형식 인스턴스의 소멸

앞서 만든 형식 인스턴스를 제거할 필요가 없습니다. 참조 형식과 값 형식 모두의 인스턴스는 자동으로 제거됩니다. 값 형식의 인스턴스는 포함된 컨텍스트가 제거되는 즉시 제거됩니다. 참조 유형의 인스턴스는 마지막 참조가 제거된 후 지정되지 않은 시간에 [가비지 수집기](../../../standard/garbage-collection/index.md)에 의해 제거됩니다.

파일 핸들과 같이 관리되지 않은 리소스를 포함하는 유형의 경우에는 결정적 정리를 사용하여 포함된 리소스가 가능한 빨리 릴리스되도록 하는 것이 좋습니다. 자세한 내용은 <xref:System.IDisposable?displayProperty=nameWithType> API 참조 및 [명령문 사용](../keywords/using-statement.md) 문서를 참조하세요.

## <a name="operator-overloadability"></a>연산자 오버로드 가능성

사용자 정의 형식은 `new` 연산자를 오버로드할 수 없습니다.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [new 연산자](~/_csharplang/spec/expressions.md#the-new-operator) 섹션을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 연산자](index.md)
- [개체 및 컬렉션 이니셜라이저](../../programming-guide/classes-and-structs/object-and-collection-initializers.md)
