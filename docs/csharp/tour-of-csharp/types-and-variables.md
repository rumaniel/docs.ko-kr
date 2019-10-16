---
title: C# 형식 및 변수 - C# 언어 둘러보기
description: C#에서 형식 정의 및 변수 선언에 대한 자세한 정보
ms.date: 08/10/2016
ms.assetid: f8a8051e-0049-43f1-b594-9c84cc7b1224
ms.openlocfilehash: 22a91b101d5361091b09217d4562703851c86940
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70105584"
---
# <a name="types-and-variables"></a>형식 및 변수

C#에는 두 가지 종류의 형식, 즉 *값 형식*과 *참조 형식*이 있습니다. 값 형식의 변수에는 해당 데이터가 직접 포함되지만 참조 형식의 변수에는 데이터(개체라고도 함)에 대한 참조가 저장됩니다. 참조 형식에서는 두 가지 변수가 같은 개체를 참조할 수 있으므로 한 변수에 대한 작업이 다른 변수에서 참조하는 개체에 영향을 미칠 수 있습니다. 값 형식에서는 변수에 데이터의 자체 사본이 들어 있으며 한 변수의 작업이 다른 변수에 영향을 미칠 수 없습니다(`ref` 및 `out` ref 및 out 매개 변수 제외).

C#의 값 형식은 *단순 형식*, *열거형 형식*, *구조체 형식* 및 *null 허용 값 형식*으로 세분화됩니다. C#의 참조 형식은 *클래스 형식*, *인터페이스 형식*, *배열 형식*, 및 *대리자 형식*으로 세분화됩니다.

다음은 C# 형식 시스템의 개요입니다.

- [값 형식][ValueTypes]
  - [단순 형식][SimpleTypes]
    - 부호 있는 정수: `sbyte`, `short`, `int`,`long`
    - 부호 없는 정수: `byte`, `ushort`, `uint`,`ulong`
    - 유니코드 문자: `char`
    - IEEE 이진 부동 소수점: `float`, `double`
    - 고정밀 10진수 부동 소수점: `decimal`
    - 부울: `bool`
  - [열거형 형식][EnumTypes]
    - `enum E {...}` 양식의 사용자 정의 형식
  - [구조체 형식][StructTypes]
    - `struct S {...}` 양식의 사용자 정의 형식
  - [Nullable 값 형식][NullableTypes]
    - `null` 값을 갖는 다른 모든 값 형식의 확장
- [참조 형식][ReferenceTypes]
  - [클래스 형식][ClassTypes]
    - 다른 모든 형식의 기본 클래스: `object`
    - 유니코드 문자열: `string`
    - `class C {...}` 양식의 사용자 정의 형식
  - [인터페이스 형식][InterfaceTypes]
    - `interface I {...}` 양식의 사용자 정의 형식
  - [배열 형식][ArrayTypes]
    - 단일 차원 및 다차원(예: `int[]` 및`int[,]`)
  - [대리자 형식][DelegateTypes]
    - `delegate int D(...)` 양식의 사용자 정의 형식

[ValueTypes]: ../language-reference/keywords/value-types-table.md
[SimpleTypes]: ../language-reference/keywords/value-types.md#simple-types
[EnumTypes]: ../language-reference/keywords/enum.md
[StructTypes]: ../language-reference/keywords/struct.md
[NullableTypes]: ../programming-guide/nullable-types/index.md
[ReferenceTypes]: ../language-reference/keywords/reference-types.md
[ClassTypes]: ../language-reference/keywords/class.md
[InterfaceTypes]: ../language-reference/keywords/interface.md
[DelegateTypes]: ../language-reference/keywords/delegate.md
[ArrayTypes]: ../programming-guide/arrays/index.md

숫자 형식에 대한 자세한 내용은 [정수 형식](../language-reference/builtin-types/integral-numeric-types.md) 및 [부동 소수점 형식 표](../language-reference/builtin-types/floating-point-numeric-types.md)를 참조하세요.

C#의 `bool` 형식은 부울 값, 즉 `true` 또는 `false`를 나타내는 데 사용됩니다.

C#의 문자 및 문자열 처리에서는 유니코드 인코딩이 사용됩니다. `char` 형식은 UTF-16 코드 단위를 나타내고, `string` 형식은 UTF-16 코드 단위 시퀀스를 나타냅니다.

C# 프로그램에서는 *형식 선언*을 사용하여 새 형식을 만듭니다. 형식 선언은 새 형식의 이름과 멤버를 지정합니다. 사용자 정의가 가능한 C#의 5가지 형식 범주는 클래스 형식, 구조체 형식, 인터페이스 형식, 열거형 형식 및 대리자 형식입니다.

`class` 형식은 데이터 멤버(필드) 및 함수 멤버(메서드, 속성 및 기타)를 포함하는 데이터 구조를 정의합니다. 클래스 형식은 단일 상속 및 다형성과 파생된 클래스가 기본 클래스를 확장하고 특수화할 수 있는 메커니즘을 지원합니다.

`struct` 형식은 데이터 멤버 및 함수 멤버로 구조체를 나타내는 클래스 형식과 유사합니다. 그러나 클래스와 달리 구조체는 값 형식이며 일반적으로 힙 할당이 필요하지 않습니다. 구조체 형식은 사용자 지정 상속을 지원하지 않으며 모든 구조체 형식은 `object` 형식에서 암시적으로 상속됩니다.

`interface` 형식은 계약을 공용 함수 멤버의 명명된 집합으로 정의합니다. `interface`를 구현하는 `class` 또는 `struct`는 인터페이스의 함수 멤버 구현을 제공해야 합니다. `interface`는 여러 기본 인터페이스에서 상속될 수 있으며 `class` 또는 `struct`는 여러 인터페이스를 구현할 수 있습니다.

`delegate` 형식은 특정 매개 변수 목록 및 반환 형식이 있는 메서드에 대한 참조를 나타내는 형식입니다. 대리자는 메서드를 변수에 할당되고 매개 변수로 전달될 수 있는 엔터티로 취급할 수 있도록 합니다. 대리자는 함수 언어에서 제공하는 함수 형식과 유사합니다. 또한 다른 언어에 나오는 함수 포인터의 개념과 비슷하지만 함수 포인터와 달리 대리자는 개체 지향적이며 형식 안전 방식입니다.

`class`, `struct`, `interface` 및 `delegate` 형식은 모두 제네릭을 지원하므로 다른 형식으로 매개 변수화할 수 있습니다.

`enum` 형식은 명명된 상수가 있는 고유한 형식입니다. 모든 `enum` 형식은 8가지 정수 형식 중 하나인 내부 형식을 갖습니다. `enum` 형식의 값 집합은 내부 형식의 값 집합과 동일합니다.

C#은 형식의 단일 차원 및 다차원 배열을 지원합니다. 위에 나열된 형식과 달리, 배열 형식은 사용하기 전에 먼저 선언할 필요가 없습니다. 대신, 배열 형식은 형식 이름을 대괄호로 묶어 생성합니다. 예를 들어 `int[]`는`int`의 1차원 배열이고, `int[,]`는 `int`의 2차원 배열이고 `int[][]`는 `int`의 1차원 배열의 1차원 배열입니다.

Null 허용 값 형식도 사용하기 전에 먼저 선언할 필요가 없습니다. null을 허용하지 않는 값 형식 `T`의 경우 `T?`, 추가 값 `null`을 보유할 수 있는 해당 null 허용 값 형식이 있습니다. 예를 들어 `int?`는 32비트 정수 또는 값 `null`을 보유할 수 있는 형식입니다.

C#의 형식 시스템은 모든 형식의 값이 `object`로 취급될 수 있도록 통합됩니다. C#의 모든 형식은 `object` 클래스 형식에서 직접 또는 간접적으로 파생되고 `object`는 모든 형식의 기본 클래스입니다. 참조 형식의 값은 `object`로 인식함으로써 간단히 개체로 처리됩니다. 값 형식의 값은 *boxing* 및 *unboxing 작업*을 수행하여 개체로 처리됩니다. 다음 예제에서 `int` 값은 `object`로 변환되었다가 다시 `int`로 변환됩니다.

[!code-csharp[Boxing](../../../samples/snippets/csharp/tour/types-and-variables/Program.cs#L1-L10)]

값 형식의 값이 `object` 형식으로 변환되면 "box"라고도 하는 `object` 인스턴스가 값을 보유하기 위해 할당되고 값이 해당 box에 복사됩니다. 반대로 `object` 참조가 값 형식으로 캐스트될 때 참조된 `object`가 올바른 값 형식의 box인지 확인한 후 확인 결과가 성공이면 box의 값이 복사됩니다.

C# 통합 형식 시스템은 결과적으로 값 형식이 "요청 시" 개체가 될 수 있음을 의미합니다. 통합 때문에 `object` 형식을 사용하는 범용 라이브러리는 참조 형식 및 값 형식 둘 다에 사용될 수 있습니다.

C#에는 필드, 배열 요소, 지역 변수 및 매개 변수를 포함하는 여러 종류의 *변수*가 있습니다. 변수는 스토리지 위치를 나타내고, 모든 변수는 아래와 같이 변수에 저장될 수 있는 값을 결정하는 형식을 갖습니다.

- Null을 허용하지 않는 값 형식
  - 정확한 해당 형식의 값
- Null 허용 값 형식
  - `null` 값 또는 정확한 해당 형식의 값
- object
  - `null` 참조, 참조 형식의 개체에 대한 참조 또는 값 형식의 boxed 값에 대한 참조
- 클래스 형식
  - `null` 참조, 해당 클래스 형식의 인스턴스에 대한 참조 또는 해당 클래스 형식에서 파생된 클래스의 인스턴스에 대한 참조
- 인터페이스 유형
  - `null` 참조, 해당 인터페이스 형식을 구현하는 클래스 형식의 인스턴스에 대한 참조 또는 해당 인터페이스 형식을 구현하는 값 형식의 boxed 값에 대한 참조
- 배열 형식
  - `null` 참조, 해당 배열 형식의 인스턴스에 대한 참조 또는 호환되는 배열 형식의 인스턴스에 대한 참조
- 대리자 형식
  - `null` 참조 또는 호환되는 대리자 형식의 인스턴스에 대한 참조

> [!div class="step-by-step"]
> [이전](program-structure.md)
> [다음](expressions.md)
