---
title: virtual - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- virtual_CSharpKeyword
- virtual
helpviewer_keywords:
- virtual keyword [C#]
ms.assetid: 5da9abae-bc1e-434f-8bea-3601b8dcb3b2
ms.openlocfilehash: 586e50818fc8ceaad5ca1925c0636b31015d81d4
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70925366"
---
# <a name="virtual-c-reference"></a>virtual(C# 참조)

`virtual` 키워드는 메서드, 속성, 인덱서 또는 이벤트 선언을 수정하고 파생 클래스에서 재정의하도록 허용하는 데 사용됩니다. 예를 들어 이 메서드는 이를 상속하는 모든 클래스에서 재정의할 수 있습니다.

```csharp
public virtual double Area() 
{
    return x * y;
}
```

가상 멤버의 구현은 파생 클래스의 [재정의 멤버](override.md)로 변경할 수 있습니다. `virtual` 키워드 사용 방법에 대한 자세한 내용은 [Override 및 New 키워드를 사용하여 버전 관리](../../programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md) 및 [Override 및 New 키워드를 사용해야 하는 경우](../../programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md)를 참조하세요.

## <a name="remarks"></a>설명

가상 메서드가 호출되면 재정의 멤버에 대해 개체의 런타임 형식이 확인됩니다. 파생 클래스가 멤버를 재정의하지 않은 경우 가장 많이 파생된 클래스의 재정의 멤버(원래 멤버일 수 있음)가 호출됩니다.

기본적으로 메서드는 가상이 아닙니다. 가상이 아닌 메서드는 재정의할 수 없습니다.

`virtual` 한정자는 `static`, `abstract`, `private` 또는 `override` 한정자와 사용할 수 없습니다. 다음 예제에서는 가상 속성을 보여 줍니다.

[!code-csharp[csrefKeywordsModifiers#26](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#26)]

선언과 호출 구문에서의 차이점을 제외하면 가상 속성은 추상 메서드처럼 작동합니다.

- 정적 속성에서 `virtual` 한정자를 사용하는 것은 오류입니다.

- `override` 한정자를 사용하는 속성 선언을 포함함으로써 상속된 가상 속성을 파생 클래스에서 재정의할 수 있습니다.

## <a name="example"></a>예

이 예제에서 `Shape` 클래스는 두 개의 좌표 `x`, `y`와 `Area()` 가상 메서드를 포함합니다. `Circle`, `Cylinder` 및 `Sphere`와 같은 서로 다른 도형의 클래스는 `Shape` 클래스를 상속하며, 각 모양에 대해 노출 영역이 계산됩니다. 각 파생 클래스에는 `Area()`의 자체 재정의 구현이 있습니다.

다음 선언에 나와 있는 것처럼 상속된 클래스 `Circle`, `Sphere` 및 `Cylinder`는 모두 기본 클래스를 초기화하는 생성자를 사용합니다.

```csharp
public Cylinder(double r, double h): base(r, h) {}
```

다음 프로그램은 메서드와 연결된 개체에 따라 `Area()` 메서드의 적절한 구현을 호출하여 각 그림의 해당 영역을 계산하고 표시합니다.

[!code-csharp[csrefKeywordsModifiers#23](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#23)]

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [다형성](../../programming-guide/classes-and-structs/polymorphism.md)
- [abstract](abstract.md)
- [override](override.md)
- [new(한정자)](new-modifier.md)
