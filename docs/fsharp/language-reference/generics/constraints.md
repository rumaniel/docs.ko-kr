---
title: 제약 조건
description: 제네릭 형식 F# 매개 변수에 적용 되는 제약 조건에 대해 학습 하 여 제네릭 형식 또는 함수에서 형식 인수에 대 한 요구 사항을 지정 합니다.
ms.date: 05/16/2016
ms.openlocfilehash: 9912ba63138d893a7c616661dd2b1cbdbe51916c
ms.sourcegitcommit: 878ca7550b653114c3968ef8906da2b3e60e3c7a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2019
ms.locfileid: "71736797"
---
# <a name="constraints"></a>제약 조건

이 항목에서는 제네릭 형식 매개 변수에 적용할 수 있는 제약 조건에 대해 설명 하 여 제네릭 형식 또는 함수의 형식 인수에 대 한 요구 사항을 지정 합니다.

## <a name="syntax"></a>구문

```fsharp
type-parameter-list when constraint1 [ and constraint2]
```

## <a name="remarks"></a>설명

제네릭 형식에 사용할 수 있는 형식을 제한 하기 위해 적용할 수 있는 여러 가지 제약 조건이 있습니다. 다음 표에서는 이러한 제약 조건을 나열 하 고 설명 합니다.

|제약 조건|구문|설명|
|----------|------|-----------|
|형식 제약 조건|*type-parameter* :&gt; *type*|제공 된 형식은 지정 된 형식에서 파생 되거나 지정 된 형식에서 파생 되어야 합니다. 형식이 인터페이스 이면 제공 된 형식이 인터페이스를 구현 해야 합니다.|
|Null 제약 조건|*유형-매개 변수* : null|제공 된 형식은 null 리터럴을 지원 해야 합니다. 여기에는 모든 .NET 개체 형식이 포함 F# 되지만 목록, 튜플, 함수, 클래스, 레코드 또는 공용 구조체 형식은 포함 되지 않습니다.|
|명시적 멤버 제약 조건|[(]*형식 매개 변수* [또는... 또는 *형식 매개 변수*)]: (*멤버 시그니처에*)|제공 된 형식 인수 중 하나 이상에 지정 된 서명이 있는 멤버가 있어야 합니다. 일반적인 용도로는 사용할 수 없습니다. 명시적 멤버 제약 조건의 유효한 대상이 되려면 암시적 형식 확장의 일부 또는 형식에 대해 명시적으로 멤버를 정의 해야 합니다.|
|생성자 제약 조건|*형식-매개 변수* : (new: unit-&gt; ' a)|제공 된 형식에는 매개 변수가 없는 생성자가 있어야 합니다.|
|값 형식 제약 조건|: struct|제공 된 형식은 .NET 값 형식 이어야 합니다.|
|참조 형식 제약 조건|: 구조체가 아닙니다.|제공 된 형식은 .NET 참조 형식 이어야 합니다.|
|열거형 형식 제약 조건|: enum @ no__t-0*기본 형식*&gt;|제공 된 형식은 지정 된 기본 형식을 포함 하는 열거형 형식 이어야 합니다. 일반적인 용도로는 사용할 수 없습니다.|
|대리자 제약 조건|: delegate&lt;*tuple-parameter-type*, *return-type*&gt;|제공 된 형식은 지정 된 인수와 반환 값을 포함 하는 대리자 형식 이어야 합니다. 일반적인 용도로는 사용할 수 없습니다.|
|비교 제약 조건|: 비교|제공 된 형식은 비교를 지원 해야 합니다.|
|같음 제약 조건|: 같음|제공 된 형식이 같음을 지원 해야 합니다.|
|관리 되지 않는 제약 조건|: 관리 되지 않음|제공 된 형식은 관리 되지 않는 형식 이어야 합니다. 관리 되지 않는 형식은 특정 기본 형식 (`sbyte`, `byte`, `char`, `nativeint`, `unativeint`, `float32`, `float`, `int16`, `int32`, 0), 열거형 형식, 4 또는 제네릭이 아닌 형식입니다. 모든 관리 되지 않는 형식의 필드를 포함 하는 구조체입니다.|

코드에서 제약 조건 형식에 사용할 수 있지만 일반적으로 형식이 아닌 기능을 사용 해야 하는 경우 제약 조건을 추가 해야 합니다. 예를 들어 형식 제약 조건을 사용 하 여 클래스 형식을 지정 하는 경우 제네릭 함수 또는 형식에서 해당 클래스의 메서드 중 하나를 사용할 수 있습니다.

제약 조건을 사용 하지 않고 형식 매개 변수를 명시적으로 작성 하는 경우 제약 조건을 지정 해야 하는 경우가 있습니다. 컴파일러는 사용 중인 기능을 형식에 대해 런타임에 제공 될 수 있는 모든 형식에서 사용할 수 있는지 확인할 방법이 없습니다. 변수에.

코드에서 F# 사용 하는 가장 일반적인 제약 조건은 기본 클래스 또는 인터페이스를 지정 하는 형식 제약 조건입니다. 다른 제약 조건은 산술 연산자에 대 한 F# 연산자 오버 로드를 구현 하는 데 사용 되는 명시적 멤버 제약 조건 등의 특정 기능을 구현 하기 위해 라이브러리에서 사용 되거나 주로 F# 제공 됩니다. 공용 언어 런타임에서 지 원하는 전체 제약 조건 집합을 지원 합니다.

형식 유추 프로세스 중에 일부 제약 조건은 컴파일러에 의해 자동으로 유추 됩니다. 예를 들어 함수에 `+` 연산자를 사용 하는 경우 컴파일러는 식에 사용 되는 변수 형식에 대해 명시적 멤버 제약 조건을 유추 합니다.

다음 코드에서는 몇 가지 제약 조건 선언을 보여 줍니다.

```fsharp
// Base Type Constraint
type Class1<'T when 'T :> System.Exception> =
class end

// Interface Type Constraint
type Class2<'T when 'T :> System.IComparable> = 
class end

// Null constraint
type Class3<'T when 'T : null> =
class end

// Member constraint with instance member
type Class5<'T when 'T : (member Method1 : 'T -> int)> =
class end

// Member constraint with property
type Class6<'T when 'T : (member Property1 : int)> =
class end

// Constructor constraint
type Class7<'T when 'T : (new : unit -> 'T)>() =
member val Field = new 'T()

// Reference type constraint
type Class8<'T when 'T : not struct> =
class end

// Enumeration constraint with underlying value specified
type Class9<'T when 'T : enum<uint32>> =
class end

// 'T must implement IComparable, or be an array type with comparable
// elements, or be System.IntPtr or System.UIntPtr. Also, 'T must not have
// the NoComparison attribute.
type Class10<'T when 'T : comparison> =
class end

// 'T must support equality. This is true for any type that does not
// have the NoEquality attribute.
type Class11<'T when 'T : equality> =
class end

type Class12<'T when 'T : delegate<obj * System.EventArgs, unit>> =
class end

type Class13<'T when 'T : unmanaged> =
class end

// Member constraints with two type parameters
// Most often used with static type parameters in inline functions
let inline add(value1 : ^T when ^T : (static member (+) : ^T * ^T -> ^T), value2: ^T) =
value1 + value2

// ^T and ^U must support operator +
let inline heterogenousAdd(value1 : ^T when (^T or ^U) : (static member (+) : ^T * ^U -> ^T), value2 : ^U) =
value1 + value2

// If there are multiple constraints, use the and keyword to separate them.
type Class14<'T,'U when 'T : equality and 'U : equality> =
class end
```

## <a name="see-also"></a>참조

- [제네릭](index.md)
- [제약 조건](constraints.md)
