---
title: struct(C# 참조)
ms.date: 07/20/2015
f1_keywords:
- struct_CSharpKeyword
helpviewer_keywords:
- struct keyword [C#]
- structs [C#], struct keyword
ms.assetid: ff3dd9b7-dc93-4720-8855-ef5558f65c7c
ms.openlocfilehash: 46cf0b66a50685a717818fe762ad4f1de36d6156
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50185747"
---
# <a name="struct-c-reference"></a>struct(C# 참조)

`struct` 형식은 인벤토리의 항목 특성이나 사각형의 좌표와 같은 관련 변수의 소규모 그룹을 캡슐화하는 데 일반적으로 사용되는 값 형식입니다. 다음 예제에서는 간단한 구조체 선언을 보여줍니다.

```csharp
public struct Book
{
    public decimal price;
    public string title;
    public string author;
}
```

## <a name="remarks"></a>설명

구조체는 [생성자](../../programming-guide/classes-and-structs/constructors.md), [상수](../../programming-guide/classes-and-structs/constants.md), [필드](../../programming-guide/classes-and-structs/fields.md), [메서드](../../programming-guide/classes-and-structs/methods.md), [속성](../../programming-guide/classes-and-structs/properties.md), [인덱서](../../programming-guide/indexers/index.md), [연산자](../../programming-guide/statements-expressions-operators/operators.md), [이벤트](../../programming-guide/events/index.md) 및 [중첩 형식](../../programming-guide/classes-and-structs/nested-types.md)도 포함할 수 있습니다. 그러나 이러한 멤버가 여러 개 필요한 경우에는 구조체 대신 클래스 형식을 지정하는 것이 좋습니다.

예제를 보려면 [구조체 사용](../../programming-guide/classes-and-structs/using-structs.md)을 참조하세요.

구조체는 인터페이스를 구현할 수는 있지만 다른 구조체를 상속할 수는 없습니다. 그러므로 구조체 멤버를 `protected`로 선언할 수는 없습니다.

자세한 내용은 [구조체](../../programming-guide/classes-and-structs/structs.md)를 참조하세요.

## <a name="examples"></a>예제

예제 및 자세한 내용은 [구조체 사용](../../programming-guide/classes-and-structs/using-structs.md)을 참조하세요.

## <a name="c-language-specification"></a>C# 언어 사양

예제를 보려면 [구조체 사용](../../programming-guide/classes-and-structs/using-structs.md)을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [기본값 표](default-values-table.md)
- [기본 제공 형식 표](built-in-types-table.md)
- [유형](types.md)
- [값 형식](value-types.md)
- [class](class.md)
- [interface](interface.md)
- [클래스 및 구조체](../../programming-guide/classes-and-structs/index.md)