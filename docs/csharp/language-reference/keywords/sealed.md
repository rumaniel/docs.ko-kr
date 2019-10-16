---
title: sealed 한정자 - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- sealed
- sealed_CSharpKeyword
helpviewer_keywords:
- sealed keyword [C#]
ms.assetid: 8e4ed5d3-10be-47db-9488-0da2008e6f3f
ms.openlocfilehash: 7b9551fe892b0335fb445ab9edce4facca0badbe
ms.sourcegitcommit: 34593b4d0be779699d38a9949d6aec11561657ec
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66833343"
---
# <a name="sealed-c-reference"></a>sealed(C# 참조)

클래스에 적용된 경우 `sealed` 한정자는 다른 클래스가 해당 클래스에서 상속하지 못하도록 합니다. 다음 예제에서 `B` 클래스는 `A` 클래스에서 상속하지만 `B` 클래스에서 상속할 수 있는 클래스는 없습니다.

```csharp
class A {}
sealed class B : A {}
```

기본 클래스의 가상 메서드 또는 속성을 재정의하는 메서드 또는 속성에 `sealed` 한정자를 사용할 수도 있습니다. 이렇게 하면 사용자 클래스에서 클래스가 파생되고 특정 가상 메서드 또는 속성을 재정의하지 못하도록 할 수 있습니다.

## <a name="example"></a>예

다음 예제에서 `Z`는 `Y`에서 상속하지만 `Z`는 `X`에서 선언되고 `Y`에서 봉인된 가상 함수 `F`를 재정의할 수 없습니다.

[!code-csharp[csrefKeywordsModifiers#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#16)]

클래스에서 새 메서드 또는 속성을 정의할 때 [virtual](virtual.md)로 선언하지 않으면 파생 클래스가 재정의하지 못하도록 할 수 있습니다.

추상 클래스는 추상 메서드 또는 속성 구현을 제공하는 클래스에 상속되어야 하므로 봉인 클래스에 [abstract](abstract.md) 한정자를 사용하면 오류가 발생합니다.

메서드 또는 속성에 적용된 경우 `sealed` 한정자는 항상 [override](override.md)와 함께 사용해야 합니다.

구조체는 암시적으로 봉인되므로 상속할 수 없습니다.

자세한 내용은 [상속](../../programming-guide/classes-and-structs/inheritance.md)을 참조하세요.

더 많은 예제를 보려면 [추상 및 봉인 클래스와 클래스 멤버](../../programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)를 참조하세요.

## <a name="example"></a>예

[!code-csharp[csrefKeywordsModifiers#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#17)]

앞의 예제에서 다음 문을 사용하여 봉인된 클래스에서 상속을 시도할 수 있습니다.

`class MyDerivedC: SealedClass {}   // Error`

그 결과 다음 오류 메시지가 표시됩니다.

`'MyDerivedC': cannot derive from sealed type 'SealedClass'`

## <a name="remarks"></a>설명

클래스, 메서드 또는 속성을 봉인할지 여부를 결정하려면 일반적으로 다음 두 가지 사항을 고려해야 합니다.

- 파생 클래스가 사용자 클래스의 사용자 지정을 통해 얻을 수 있는 잠재적인 이점

- 파생 클래스가 사용자 클래스를 수정하여 더 이상 올바르게 또는 예상대로 작동하지 않을 가능성

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [정적 클래스 및 정적 클래스 멤버](../../programming-guide/classes-and-structs/static-classes-and-static-class-members.md)
- [추상/봉인된 클래스 및 클래스 멤버](../../programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)
- [액세스 한정자](../../programming-guide/classes-and-structs/access-modifiers.md)
- [한정자](modifiers.md)
- [override](override.md)
- [virtual](virtual.md)
