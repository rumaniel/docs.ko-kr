---
title: in(제네릭 한정자) - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- contravariance, in keyword [C#]
- in keyword [C#]
ms.openlocfilehash: f736540a37d3226bccfc07749dcf06ca018663e8
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54694573"
---
# <a name="in-generic-modifier-c-reference"></a>in(제네릭 한정자)(C# 참조)

제네릭 형식 매개 변수에서 `in` 키워드는 형식 매개 변수를 반공변(contravariant)으로 지정합니다. 제네릭 인터페이스 및 대리자에서 `in` 키워드를 사용할 수 있습니다.

반공변성(Contravariance)을 통해 제네릭 매개 변수에 지정된 것보다 적은 파생 형식을 사용할 수 있습니다. 따라서 공변(contravariant) 인터페이스를 구현하는 클래스의 암시적 변환과 대리자 형식의 암시적 변환이 허용됩니다. 제네릭 형식 매개 변수의 공변성(Covariance) 및 반공변성(Contravariance)은 참조 형식에 대해 지원되고 값 형식에 대해서는 지원되지 않습니다.

메서드 매개 변수의 형식을 정의하고 메서드의 반환 형식을 정의하지 않는 경우에만 형식을 제네릭 인터페이스 또는 대리자에서 반공변(contravariant)으로 선언할 수 있습니다. `In`, `ref` 및 `out` 매개 변수는 고정이어야 합니다. 즉 공변(covariant) 또는 반공변(contravariant)입니다.

반공변(contravariant) 형식 매개 변수가 있는 인터페이스는 해당 메서드가 인터페이스 형식 매개 변수에 지정된 형식보다 덜 파생된 형식의 인수를 사용할 수 있도록 합니다. 예를 들어 <xref:System.Collections.Generic.IComparer%601> 인터페이스에서 T 형식은 반공변(contravariant)이므로 `Employee`가 `Person`을 상속하는 경우 특수 변환 메서드를 사용하지 않고 `IComparer<Person>` 형식의 개체를 `IComparer<Employee>` 형식의 개체에 할당할 수 있습니다.

반공변(contravariant) 대리자에 동일한 형식의 다른 대리자를 할당할 수 있지만 덜 파생된 제네릭 형식 매개 변수가 필요합니다.

자세한 내용은 [공변성(Covariance) 및 반공변성(Contravariance)](../../programming-guide/concepts/covariance-contravariance/index.md)을 참조하세요.

## <a name="contravariant-generic-interface"></a>반공변(contravariant) 제네릭 인터페이스

다음 예제에서는 반공변(contravariant) 제네릭 인터페이스를 선언, 확장 및 구현하는 방법을 보여 줍니다. 또한 이 인터페이스를 구현하는 클래스에 대해 암시적 변환을 사용하는 방법을 보여 줍니다.

[!code-csharp[csVarianceKeywords#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csvariancekeywords/cs/program.cs#1)]

## <a name="contravariant-generic-delegate"></a>반공변(contravariant) 제네릭 대리자

다음 예제에서는 반공변(contravariant) 제네릭 대리자를 선언, 인스턴스화 및 호출하는 방법을 보여 줍니다. 또한 대리자 형식을 암시적으로 변환하는 방법을 보여 줍니다.

[!code-csharp[csVarianceKeywords#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csvariancekeywords/cs/program.cs#2)]

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [out](out-generic-modifier.md)
- [공 분산 및 반공 분산](../../programming-guide/concepts/covariance-contravariance/index.md)
- [한정자](modifiers.md)
