---
title: void(C# 참조)
ms.date: 07/20/2015
f1_keywords:
- void_CSharpKeyword
- void
helpviewer_keywords:
- void keyword [C#]
ms.assetid: 0d2d8a95-fe20-4fbd-bf5d-c1e54bce71d4
ms.openlocfilehash: 223db893dd42181c234d9a07c1a1c00af26f0c30
ms.sourcegitcommit: 700b9003ea6bdd83a53458bbc436c9b5778344f1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2018
ms.locfileid: "48261591"
---
# <a name="void-c-reference"></a>void(C# 참조)
메서드에 대한 반환 형식으로 사용될 경우 `void`는 메서드가 값을 반환하지 않도록 지정합니다.

`void`는 메서드의 매개 변수 목록에서 허용되지 않습니다. 매개 변수를 사용하지 않고 값을 반환하지 않는 메서드는 다음과 같이 선언됩니다.

```csharp
public void SampleMethod()
{
    // Body of the method.
}
```

`void`는 또한 알 수 없는 형식에 대한 포인터를 선언하기 위해 안전하지 않은 컨텍스트에서도 사용됩니다. 자세한 내용은 [포인터 형식](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)을 참조하세요.

`void`는 .NET Framework <xref:System.Void?displayProperty=nameWithType> 형식의 별칭입니다.

## <a name="c-language-specification"></a>C# 언어 사양
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../../../csharp/language-reference/index.md)  
- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [C# 키워드](../../../csharp/language-reference/keywords/index.md)  
- [참조 형식](../../../csharp/language-reference/keywords/reference-types.md)  
- [값 형식](../../../csharp/language-reference/keywords/value-types.md)  
- [메서드](../../../csharp/programming-guide/classes-and-structs/methods.md)  
- [안전하지 않은 코드 및 포인터](../../../csharp/programming-guide/unsafe-code-pointers/index.md)
