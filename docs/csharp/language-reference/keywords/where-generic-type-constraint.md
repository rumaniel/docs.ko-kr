---
title: where(제네릭 형식 제약 조건) - C# 참조
ms.custom: seodec18
ms.date: 04/12/2018
f1_keywords:
- whereconstraint
- whereconstraint_CSharpKeyword
helpviewer_keywords:
- where (generic type constraint) [C#]
ms.openlocfilehash: 4e51c5dd226533e7d1ce79a136dba19cbb252f92
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253910"
---
# <a name="where-generic-type-constraint-c-reference"></a>where(제네릭 형식 제약 조건)(C# 참조)

제네릭 정의의 `where` 절은 제네릭 형식, 메서드, 대리자 또는 로컬 함수의 형식 매개 변수에 대한 인수로 사용되는 형식에 대한 제약 조건을 지정합니다. 제약 조건은 인터페이스, 기본 클래스를 지정하거나 제네릭 형식을 참조, 값 또는 관리되지 않는 형식으로 요구할 수 있습니다. 형식 인수에서 갖추고 있어야 하는 기능을 선언합니다.

예를 들어 형식 매개 변수 `T`가 <xref:System.IComparable%601> 인터페이스를 구현하도록 제네릭 클래스 `MyGenericClass`를 선언할 수 있습니다.

[!code-csharp[using an interface constraint](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#1)]

> [!NOTE]
> 쿼리 식의 where 절에 대한 자세한 내용은 [where 절](where-clause.md)을 참조하세요.

`where` 절에는 기본 클래스 제약 조건이 포함될 수도 있습니다. 기본 클래스 제약 조건에서는 해당 제네릭 형식에 대한 형식 인수로 사용할 기본 클래스(또는 해당 기본 클래스)로 지정된 클래스가 해당 제네릭 형식에 대한 형식 인수로 사용할 형식에 있다고 명시합니다. 기본 클래스 제약 조건이 사용되는 경우 해당 형식 매개 변수에 대한 다른 제약 조건 앞에 나타나야 합니다. 일부 형식은 <xref:System.Object>, <xref:System.Array> 및 <xref:System.ValueType> 기본 클래스 제약 조건으로 허용되지 않습니다. C# 7.3 이전에는 기본 클래스 제약 조건으로 <xref:System.Enum>, <xref:System.Delegate> 및 <xref:System.MulticastDelegate>도 허용되지 않았습니다. 다음 예제에서는 이제 기본 클래스로 지정할 수 있는 형식을 보여 줍니다.

[!code-csharp[using an interface constraint](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#2)]

`where` 절은 형식이 `class` 또는 `struct`임을 지정할 수 있습니다. `struct` 제약 조건은 `System.ValueType`의 기본 클래스 제약 조건을 지정할 필요가 없습니다. `System.ValueType` 형식은 기본 클래스 제약 조건으로 사용할 수 없습니다. 다음 예제에서는 `class` 및 `struct` 제약 조건을 모두 보여 줍니다.

[!code-csharp[using the class and struct constraints](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#3)]

`where` 절은 `notnull` 제약 조건을 포함할 수 있습니다. `notnull` 제약 조건은 형식 매개 변수를 Null을 허용하지 않는 형식으로 제한합니다. 해당 형식은 [값 형식](struct.md)이거나 nullable이 아닌 참조 형식일 수 있습니다. [`nullable enable` 컨텍스트](../../nullable-references.md#nullable-contexts)에서 컴파일된 코드에 대해 C# 8.0부터 `notnull` 제약 조건을 사용할 수 있습니다. 다른 제약 조건과 달리 형식 인수가 `notnull` 제약 조건을 위반하면 컴파일러는 오류 대신 경고를 생성합니다. 경고는 `nullable enable` 컨텍스트에서만 생성됩니다. 

> [!IMPORTANT]
> `notnull` 제약 조건을 포함하는 제네릭 선언은 nullable 형식을 감지하지 않는 컨텍스트에서 사용될 수 있지만 컴파일러는 제약 조건을 적용하지 않습니다.

[!code-csharp[using the nonnull constraint](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#NotNull)]

`where` 절에 `unmanaged` 제약 조건이 포함될 수도 있습니다. `unmanaged` 제약 조건은 형식 매개 변수를 [관리되지 않는 형식](../builtin-types/unmanaged-types.md)으로 알려진 형식으로 제한합니다. `unmanaged` 제약 조건을 사용하면 C#에서 하위 수준의 interop 코드를 더 쉽게 작성할 수 있습니다. 이 제약 조건을 통해 모든 관리되지 않는 형식에서 재사용 가능한 루틴을 사용할 수 있습니다. `unmanaged` 제약 조건은 `class` 또는 `struct` 제약 조건과 결합할 수 없습니다. `unmanaged` 제약 조건에 따라 형식이 `struct`이어야 합니다.

[!code-csharp[using the unmanaged constraint](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#4)]

`where` 절에 `new()` 생성자 제약 조건이 포함될 수도 있습니다. 이 제약 조건을 사용하면 `new` 연산자를 사용하여 형식 매개 변수의 인스턴스를 만들 수 있습니다. [new () 제약 조건](new-constraint.md)을 사용하면 컴파일러는 제공된 인수에 액세스 가능하고 매개 변수가 없는 생성자(또는 기본 생성자)가 있어야 한다는 것을 알게 됩니다. 예:

[!code-csharp[using the new constraint](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#5)]

`new()` 제약 조건은 `where` 절 맨 끝에 나타납니다. `new()` 제약 조건은 `struct` 또는 `unmanaged` 제약 조건과 결합할 수 없습니다. 이러한 제약 조건을 충족하는 모든 형식에는 매개 변수가 없는 액세스 가능 생성자가 있어야 하므로 `new()` 제약 조건이 중복됩니다.

형식 매개 변수가 여러 개이면 각 형식 매개 변수에 하나의 `where` 절을 사용합니다. 예를 들면 다음과 같습니다.

[!code-csharp[using multiple where constraints](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#6)]

다음 예제와 같이 제약 조건은 제네릭 메서드의 형식 매개 변수에 연결할 수도 있습니다.

[!code-csharp[where constraints with generic methods](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#7)]

대리자에 대한 형식 매개 변수 제약 조건을 설명하는 구문은 메서드의 구문과 동일합니다.

[!code-csharp[where constraints with generic methods](~/samples/snippets/csharp/keywords/GenericWhereConstraints.cs#8)]

제네릭 대리자에 대한 자세한 내용은 [제네릭 대리자](../../programming-guide/generics/generic-delegates.md)를 참조하세요.

제약 조건의 구문 및 사용에 대한 자세한 내용은 [형식 매개 변수에 대한 제약 조건](../../programming-guide/generics/constraints-on-type-parameters.md)을 참조하세요.

## <a name="c-language-specification"></a>C# 언어 사양

 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [제네릭 소개](../../programming-guide/generics/index.md)
- [new 제약 조건](./new-constraint.md)
- [형식 매개 변수에 대한 제약 조건](../../programming-guide/generics/constraints-on-type-parameters.md)
