---
title: out 키워드(제네릭 한정자)(C# 참조)
ms.date: 07/20/2015
helpviewer_keywords:
- covariance, out keyword [C#]
- out keyword [C#]
ms.assetid: f8c20dec-a8bc-426a-9882-4076b1db1e00
ms.openlocfilehash: fedbdb12c1da108d17636770fb5c628195dce0d4
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48582699"
---
# <a name="out-generic-modifier-c-reference"></a>out(제네릭 한정자)(C# 참조)

제네릭 형식 매개 변수에서 `out` 키워드는 형식 매개 변수를 공변(covariant)으로 지정합니다. 제네릭 인터페이스 및 대리자에서 `out` 키워드를 사용할 수 있습니다.

공변성(covariance)을 통해 제네릭 매개 변수에 지정된 것보다 많은 파생 형식을 사용할 수 있습니다. 따라서 variant 인터페이스를 구현하는 클래스의 암시적 변환과 대리자 형식의 암시적 변환이 허용됩니다. 공변성(Covariance) 및 반공변성(Contravariance)은 참조 형식에 대해 지원되고 값 형식에 대해서는 지원되지 않습니다.

공변(covariant) 형식 매개 변수가 있는 인터페이스는 해당 메서드가 형식 인터페이스에 지정된 것보다 많은 파생 형식을 반환할 수 있도록 합니다. 예를 들어 .NET Framework 4의 <xref:System.Collections.Generic.IEnumerable%601>에서 T 형식은 공변(covariant)이므로 특수 변환 메서드를 사용하지 않고 `IEnumerable(Of String)` 형식의 개체를 `IEnumerable(Of Object)` 형식의 개체에 할당할 수 있습니다.

공변(covariant) 대리자에 동일한 형식의 다른 대리자를 할당할 수 있지만 더 파생된 제네릭 형식 매개 변수가 필요합니다.

자세한 내용은 [공변성(Covariance) 및 반공변성(Contravariance)](../../programming-guide/concepts/covariance-contravariance/index.md)을 참조하세요.

## <a name="example---covariant-generic-interface"></a>예제 - 공변(covariant) 제네릭 인터페이스

다음 예제에서는 공변(covariant) 제네릭 인터페이스를 선언, 확장 및 구현하는 방법을 보여 줍니다. 또한 공변(covariant) 인터페이스를 구현하는 클래스에 대해 암시적 변환을 사용하는 방법을 보여 줍니다.

[!code-csharp[csVarianceKeywords#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csvariancekeywords/cs/program.cs#3)]

제네릭 인터페이스에서 형식 매개 변수가 다음 조건을 충족하는 경우 공변(covariant)으로 선언할 수 있습니다.

- 형식 매개 변수는 인터페이스 메서드의 반환 형식으로만 사용되고 메서드 인수의 형식으로 사용되지 않습니다.

    > [!NOTE]
    > 그러나 이 규칙에는 한 가지 예외가 있습니다. 공변(covariant) 인터페이스에 메서드 매개 변수로 반공변(contravariant) 제네릭 대리자가 있는 경우 공변(covariant) 형식을 이 대리자에 대한 제네릭 형식 매개 변수로 사용할 수 있습니다. 공변(covariant) 및 반공변(contravariant) 제네릭 대리자에 대한 자세한 내용은 [대리자의 가변성](../../programming-guide/concepts/covariance-contravariance/variance-in-delegates.md) 및 [Func 및 Action 제네릭 대리자에 가변성 사용](../../programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)을 참조하세요.

- 형식 매개 변수는 인터페이스 메서드에 대한 제네릭 제약 조건으로 사용되지 않습니다.

## <a name="example---covariant-generic-delegate"></a>예제 - 공변(covariant) 제네릭 대리자

다음 예제에서는 공변(covariant) 제네릭 대리자를 선언, 인스턴스화 및 호출하는 방법을 보여 줍니다. 또한 대리자 형식을 암시적으로 변환하는 방법을 보여 줍니다.

[!code-csharp[csVarianceKeywords#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csvariancekeywords/cs/program.cs#4)]

제네릭 대리자에서 형식이 메서드 반환 형식으로만 사용되고 메서드 인수에 사용되지 않는 경우 공변(covariant)으로 선언할 수 있습니다.

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [제네릭 인터페이스의 가변성](../../programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)
- [in](in-generic-modifier.md)
- [한정자](modifiers.md)