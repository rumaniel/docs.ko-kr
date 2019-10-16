---
title: Partial 클래스 및 메서드 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- partial methods [C#]
- partial classes [C#]
- C# language, partial classes and methods
ms.assetid: 804cecb7-62db-4f97-a99f-60975bd59fa1
ms.openlocfilehash: 53c3ac6e4fa6313488c47d851e0897bd512521b7
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596281"
---
# <a name="partial-classes-and-methods-c-programming-guide"></a>Partial 클래스 및 메서드(C# 프로그래밍 가이드)

[클래스](../../language-reference/keywords/class.md), [구조체](../../language-reference/keywords/struct.md), [인터페이스](../../language-reference/keywords/interface.md) 또는 메서드의 정의를 둘 이상의 소스 파일에 분할할 수 있습니다. 각 소스 파일에는 형식 또는 메서드 정의 섹션이 있으며 모든 부분은 애플리케이션이 컴파일될 때 결합됩니다.

## <a name="partial-classes"></a>partial 클래스

클래스 정의를 분할하는 것이 바람직한 몇 가지 상황이 있습니다.

- 대규모 프로젝트에서 작업하는 경우 클래스를 개별 파일에 분산하면 여러 프로그래머가 동시에 클래스에 대해 작업할 수 있습니다.

- 자동으로 생성된 소스로 작업하는 경우 소스 파일을 다시 만들지 않고도 클래스에 코드를 추가할 수 있습니다. Visual Studio에서는 Windows Forms, 웹 서비스 래퍼 코드 등에 만들 때 이 방식을 사용합니다. Visual Studio에서 만든 파일을 수정하지 않고도 이러한 클래스를 사용하는 코드를 만들 수 있습니다.

- 클래스 정의를 분할하려면 다음과 같이 [partial](../../language-reference/keywords/partial-type.md) 키워드 한정자를 사용합니다.

  [!code-csharp[csProgGuideObjects#26](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#26)]

`partial` 키워드는 클래스, 구조체 또는 인터페이스의 다른 부분을 네임스페이스에서 정의할 수 있음을 나타냅니다. 모든 부분은 `partial` 키워드를 사용해야 합니다. 최종 형식을 생성하려면 컴파일 시간에 모든 부분을 사용할 수 있어야 합니다. 모든 부분에 `public`, `private` 등의 동일한 액세스 가능성이 있어야 합니다.

부분이 abstract로 선언된 경우 전체 형식이 abstract로 간주됩니다. 부분이 sealed로 선언된 경우 전체 형식이 sealed로 간주됩니다. 부분이 기본 형식을 선언하는 경우 전체 형식이 해당 클래스를 상속합니다.

기본 클래스를 지정하는 부분은 모두 일치해야 하지만 기본 클래스를 생략하는 부분도 여전히 기본 형식을 상속합니다. 부분에서 다른 기본 인터페이스를 지정할 수 있으며, 최종 형식은 모든 partial 선언에 나열된 모든 인터페이스를 구현합니다. 부분 정의에 선언된 클래스, 구조체 또는 인터페이스 멤버는 다른 모든 부분에서 사용할 수 있습니다. 최종 형식은 컴파일 시간의 모든 부분 조합입니다.

> [!NOTE]
> 대리자 또는 열거형 선언에서는 `partial` 한정자를 사용할 수 없습니다.

다음 예제에서는 중첩된 대상 형식 자체는 부분이 아니어도 중첩된 형식이 부분일 수 있음을 보여 줍니다.

[!code-csharp[csProgGuideObjects#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#25)]

컴파일 시간에 부분 형식(Partial Type) 정의의 특성이 병합됩니다. 예를 들어 다음 선언을 살펴보세요.

[!code-csharp[csProgGuideObjects#23](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#23)]

이러한 선언은 다음 선언과 동일합니다.

[!code-csharp[csProgGuideObjects#24](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#24)]

다음은 모든 부분 형식(Partial Type) 정의에서 병합됩니다.

- XML 주석

- 인터페이스

- 제네릭 형식 매개 변수 특성

- 클래스 특성

- 멤버

예를 들어 다음 선언을 살펴보세요.

[!code-csharp[csProgGuideObjects#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#21)]

이러한 선언은 다음 선언과 동일합니다.

[!code-csharp[csProgGuideObjects#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#22)]

### <a name="restrictions"></a>제한

partial 클래스 정의로 작업할 때 따라야 할 몇 가지 규칙이 있습니다.

- 동일한 형식의 일부로 작성된 모든 부분 형식(Partial Type) 정의를 `partial`로 수정해야 합니다. 예를 들어 다음 클래스 선언은 오류를 생성합니다.

  [!code-csharp[csProgGuideObjects#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#20)]

- `partial` 한정자는 `class`, `struct` 또는 `interface` 키워드 바로 앞에만 올 수 있습니다.

- 다음 예제와 같이 부분 형식(Partial Type) 정의에 중첩된 부분 형식(Partial Type)을 사용할 수 있습니다.

  [!code-csharp[csProgGuideObjects#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#19)]

- 동일한 형식의 일부로 작성된 모든 부분 형식(Partial Type) 정의는 동일한 어셈블리와 동일한 모듈(.exe 또는 .dll 파일)에서 정의해야 합니다. 부분 정의는 여러 모듈에 걸쳐 있을 수 없습니다.

- 모든 부분 형식(Partial Type) 정의에서 클래스 이름 및 제네릭 형식 매개 변수가 일치해야 합니다. 제네릭 형식은 부분일 수 있습니다. 각 부분 선언에서 동일한 매개 변수 이름을 동일한 순서로 사용해야 합니다.

- 부분 형식(Partial Type) 정의에서 다음 키워드는 선택 사항이지만, 부분 형식(Partial Type) 정의에 있는 경우 동일한 형식의 다른 부분 정의에서 지정된 키워드와 충돌할 수 없습니다.

  - [public](../../language-reference/keywords/public.md)

  - [private](../../language-reference/keywords/private.md)

  - [protected](../../language-reference/keywords/protected.md)

  - [internal](../../language-reference/keywords/internal.md)

  - [abstract](../../language-reference/keywords/abstract.md)

  - [sealed](../../language-reference/keywords/sealed.md)

  - 기본 클래스

  - [new](../../language-reference/keywords/new-modifier.md) 한정자(중첩된 부분)

  - 제네릭 제약 조건

자세한 내용은 [형식 매개 변수에 대한 제약 조건](../generics/constraints-on-type-parameters.md)을 참조하세요.

## <a name="example-1"></a>예제 1

### <a name="description"></a>설명

다음 예제에서는 `Coords` 클래스의 생성자 및 필드가 하나의 partial 클래스 정의에서 선언되고 `PrintCoords` 멤버가 다른 partial 클래스 정의에서 선언됩니다.

### <a name="code"></a>코드

[!code-csharp[csProgGuideObjects#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#17)]

## <a name="example-2"></a>예제 2

### <a name="description"></a>설명

다음 예제에서는 partial 구조체와 인터페이스도 개발할 수 있음을 보여 줍니다.

### <a name="code"></a>코드

[!code-csharp[csProgGuideObjects#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#18)]

## <a name="partial-methods"></a>부분 메서드

partial 클래스 또는 구조체에는 부분 메서드(Partial Method)가 포함될 수 있습니다. 클래스의 한 부분에는 메서드의 시그니처가 포함되어 있습니다. 동일한 부분이나 다른 부분에서 선택적 구현을 정의할 수 있습니다. 구현을 제공하지 않으면 메서드와 모든 메서드 호출이 컴파일 시간에 제거됩니다.

부분 메서드(Partial Method)를 사용하면 클래스 중 한 부분의 구현자가 이벤트와 비슷하게 메서드를 정의할 수 있습니다. 클래스 중 다른 부분의 구현자는 메서드를 구현할지 여부를 결정할 수 있습니다. 메서드가 구현되지 않은 경우 컴파일러는 메서드 시그니처 및 모든 메서드 호출을 제거합니다. 호출의 인수 평가에서 발생하는 모든 결과를 포함하여 메서드 호출은 런타임에 영향을 주지 않습니다. 따라서 partial 클래스의 코드는 구현이 제공되지 않은 경우에도 부분 메서드(Partial Method)를 자유롭게 사용할 수 있습니다. 메서드가 호출되었지만 구현되지 않은 경우 컴파일 시간 또는 런타임 오류가 발생하지 않습니다.

부분 메서드(Partial Method)는 생성된 코드를 사용자 지정하는 방법으로 특히 유용합니다. 생성된 코드가 메서드를 호출할 수 있지만 개발자가 메서드를 구현할지 여부를 결정할 수 있도록 메서드 이름과 시그니처를 예약할 수 있습니다. partial 클래스와 마찬가지로, 부분 메서드(Partial Method)는 코드 생성기에 의해 생성된 코드와 개발자가 직접 만든 코드가 런타임 비용 없이 함께 작동할 수 있도록 합니다.

부분 메서드(Partial Method) 선언은 정의와 구현, 두 부분으로 이루어집니다. partial 클래스의 개별 부분이나 동일한 부분에 있을 수 있습니다. 구현 선언이 없는 경우 컴파일러는 정의하는 선언과 모든 메서드 호출을 최적화합니다.

```csharp
// Definition in file1.cs
partial void onNameChanged();

// Implementation in file2.cs
partial void onNameChanged()
{
  // method body
}
```

- 부분 메서드(Partial Method) 선언은 상황별 키워드 [partial](../../language-reference/keywords/partial-type.md)로 시작해야 하고, 메서드에서 [void](../../language-reference/keywords/void.md)를 반환해야 합니다.

- 부분 메서드(Partial Method)는 [in](../../language-reference/keywords/in-parameter-modifier.md) 또는 [ref](../../language-reference/keywords/ref.md) 매개 변수를 사용할 수 있지만 [out](../../language-reference/keywords/out-parameter-modifier.md) 매개 변수는 사용할 수 없습니다.

- 부분 메서드(Partial Method)는 암시적으로 [private](../../language-reference/keywords/private.md)이므로 [가상](../../language-reference/keywords/virtual.md)일 수 없습니다.

- 부분 메서드(Partial Method)는 본문의 존재 여부에 따라 정의하는지, 구현하는지가 결정되기 때문에 [extern](../../language-reference/keywords/extern.md)일 수 없습니다.

- 부분 메서드(Partial Method)는 [static](../../language-reference/keywords/static.md) 및 [unsafe](../../language-reference/keywords/unsafe.md) 한정자를 사용할 수 없습니다.

- 부분 메서드(Partial Method)는 제네릭일 수 있습니다. 제약 조건은 정의하는 부분 메서드(Partial Method) 선언에 배치되며 필요에 따라 구현하는 선언에서 반복될 수 있습니다. 매개 변수 및 형식 매개 변수 이름이 정의하는 선언과 구현하는 선언에서 동일할 필요는 없습니다.

- 정의 및 구현된 부분 메서드(Partial Method)에 대한 [대리자](../../language-reference/keywords/delegate.md)는 만들 수 있지만 정의만 된 부분 메서드(Partial Method)에 대한 대리자는 만들 수 없습니다.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](../../language-reference/language-specification/index.md)의 [부분 형식](~/_csharplang/spec/classes.md#partial-types)을 참조하세요. 언어 사양은 C# 구문 및 사용법에 대 한 신뢰할 수 있는 소스 됩니다.

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [클래스](./classes.md)
- [구조체](./structs.md)
- [인터페이스](../interfaces/index.md)
- [partial(형식)](../../language-reference/keywords/partial-type.md)
