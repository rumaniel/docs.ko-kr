---
title: 암시적 변환과 명시적 변환(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- conversions [Visual Basic], type
- variables [Visual Basic], changing data type
- casting
- conversions [Visual Basic], data type
- type conversion [Visual Basic], implicit conversions
- CType function [Visual Basic], conversions
- casting, data types
- data type conversion [Visual Basic], explicit
- type conversion [Visual Basic], explicit conversions
- data types [Visual Basic], casting
- conversions [Visual Basic], implicit
- explicit data type conversions [Visual Basic]
- conversions [Visual Basic]
- changing data types [Visual Basic]
- conversions [Visual Basic], explicit
- data type conversion [Visual Basic], implicit
- implicit data type conversions [Visual Basic]
ms.assetid: 77de1659-af8a-492c-967e-e7ef60ccce66
ms.openlocfilehash: 4bcf2d76a2983294f244b72f286842a92fb5e64e
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68512860"
---
# <a name="implicit-and-explicit-conversions-visual-basic"></a>암시적 변환과 명시적 변환(Visual Basic)

*암시적 변환* 에는 소스 코드에 특별 한 구문이 필요 하지 않습니다. 다음 예제에서는를에 `k` `q`할당 하기 전에 Visual Basic의 값을 단 정밀도 부동 소수점 값으로 암시적으로 변환 합니다.

```vb
Dim k As Integer
Dim q As Double
' Integer widens to Double, so you can do this with Option Strict On.
k = 432
q = k
```

*명시적 변환은* 형식 변환 키워드를 사용 합니다. Visual Basic는 괄호 안의 식을 원하는 데이터 형식으로 강제 변환 하는 몇 가지 키워드를 제공 합니다. 이러한 키워드는 함수 처럼 동작 하지만 컴파일러가 코드를 인라인으로 생성 하므로 함수 호출을 사용 하는 것 보다 약간 더 빠릅니다.

위의 예에서는 다음 확장에서 키워드는 `CInt` 를에 `k`할당 하기 전에 `q` 값을 다시 정수로 변환 합니다.

```vb
' q had been assigned the value 432 from k.
q = Math.Sqrt(q)
k = CInt(q)
' k now has the value 21 (rounded square root of 432).
```

## <a name="conversion-keywords"></a>변환 키워드

다음 표에서는 사용 가능한 변환 키워드를 보여 줍니다.

|형식 변환 키워드|식을 데이터 형식으로 변환 합니다.|변환할 수 있는 식의 데이터 형식|
|---|---|---|
|`CBool`|[Boolean 데이터 형식](../../../../visual-basic/language-reference/data-types/boolean-data-type.md)|모든 숫자 형식 (, `Byte` `SByte`, 열거형 형식 포함), `String`,`Object`|
|`CByte`|[Byte 데이터 형식](../../../../visual-basic/language-reference/data-types/byte-data-type.md)|모든 숫자 형식 (및 `SByte` 열거 형식 포함) `String`, `Boolean`,,`Object`|
|`CChar`|[Char 데이터 형식](../../../../visual-basic/language-reference/data-types/char-data-type.md)|`String`, `Object`|
|`CDate`|[Date 데이터 형식](../../../../visual-basic/language-reference/data-types/date-data-type.md)|`String`, `Object`|
|`CDbl`|[Double 데이터 형식](../../../../visual-basic/language-reference/data-types/double-data-type.md)|모든 숫자 형식 (, `Byte` `SByte` `Boolean` ,`String`열거형 형식 포함),,,`Object`|
|`CDec`|[Decimal 데이터 형식](../../../../visual-basic/language-reference/data-types/decimal-data-type.md)|모든 숫자 형식 (, `Byte` `SByte` `Boolean` ,`String`열거형 형식 포함),,,`Object`|
|`CInt`|[Integer 데이터 형식](../../../../visual-basic/language-reference/data-types/integer-data-type.md)|모든 숫자 형식 (, `Byte` `SByte` `Boolean` ,`String`열거형 형식 포함),,,`Object`|
|`CLng`|[Long 데이터 형식](../../../../visual-basic/language-reference/data-types/long-data-type.md)|모든 숫자 형식 (, `Byte` `SByte` `Boolean` ,`String`열거형 형식 포함),,,`Object`|
|`CObj`|[Object 데이터 형식](../../../../visual-basic/language-reference/data-types/object-data-type.md)|모든 형식|
|`CSByte`|[SByte 데이터 형식](../../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|모든 숫자 형식 (및 `Byte` 열거 형식 포함) `String`, `Boolean`,,`Object`|
|`CShort`|[Short 데이터 형식](../../../../visual-basic/language-reference/data-types/short-data-type.md)|모든 숫자 형식 (, `Byte` `SByte` `Boolean` ,`String`열거형 형식 포함),,,`Object`|
|`CSng`|[Single 데이터 형식](../../../../visual-basic/language-reference/data-types/single-data-type.md)|모든 숫자 형식 (, `Byte` `SByte` `Boolean` ,`String`열거형 형식 포함),,,`Object`|
|`CStr`|[String 데이터 형식](../../../../visual-basic/language-reference/data-types/string-data-type.md)|모든 숫자 형식 (, `Byte` `SByte`, 열거형 형식 포함), `Boolean`, `Char`, `Char` array, `Date`,`Object`|
|`CType`|쉼표 (`,`) 뒤에 지정 된 형식|기본 *데이터 형식* (기본 형식의 배열 포함)으로 변환 하는 경우 해당 변환 키워드에 대해 허용 되는 것과 동일한 형식입니다.<br /><br /> *복합 데이터 형식*으로 변환 하는 경우, 구현 하는 인터페이스 및 해당 형식이 상속 하는 클래스<br /><br /> 오버 로드 `CType`된 클래스 또는 구조체 (해당 클래스 또는 구조체)로 변환 하는 경우|
|`CUInt`|[UInteger 데이터 형식](../../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|모든 숫자 형식 (, `Byte` `SByte` `Boolean` ,`String`열거형 형식 포함),,,`Object`|
|`CULng`|[ULong 데이터 형식](../../../../visual-basic/language-reference/data-types/ulong-data-type.md)|모든 숫자 형식 (, `Byte` `SByte` `Boolean` ,`String`열거형 형식 포함),,,`Object`|
|`CUShort`|[UShort 데이터 형식](../../../../visual-basic/language-reference/data-types/ushort-data-type.md)|모든 숫자 형식 (, `Byte` `SByte` `Boolean` ,`String`열거형 형식 포함),,,`Object`|

## <a name="the-ctype-function"></a>CType 함수

[CType 함수](../../../../visual-basic/language-reference/functions/ctype-function.md) 는 두 인수에 대해 작동 합니다. 첫 번째는 변환할 식이고 두 번째는 대상 데이터 형식 또는 개체 클래스입니다. 첫 번째 인수는 형식이 아니라 식 이어야 합니다.

`CType`는 *인라인 함수*입니다. 즉, 컴파일 코드에서 함수 호출을 생성 하지 않고 변환을 수행 하는 경우가 많습니다. 이것은 성능을 향상시킵니다.

를 다른 형식 변환 `CType` 키워드와 비교 하려면 [DirectCast operator](../../../../visual-basic/language-reference/operators/directcast-operator.md) 및 [TryCast operator](../../../../visual-basic/language-reference/operators/trycast-operator.md)를 참조 하세요.

### <a name="elementary-types"></a>기본 형식

다음 예에서는 `CType`의 사용법을 보여줍니다.

```vb
k = CType(q, Integer)
' The following statement coerces w to the specific object class Label.
f = CType(w, Label)
```

### <a name="composite-types"></a>복합 형식

를 사용 `CType` 하 여 값을 복합 데이터 형식 및 기본 형식으로 변환할 수 있습니다. 다음 예제와 같이이를 사용 하 여 개체 클래스를 해당 인터페이스 중 하나의 형식으로 강제 변환할 수도 있습니다.

```vb
' Assume class cZone implements interface iZone.
Dim h As Object
' The first argument to CType must be an expression, not a type.
Dim cZ As cZone
' The following statement coerces a cZone object to its interface iZone.
h = CType(cZ, iZone)
```

### <a name="array-types"></a>배열 형식

`CType`는 다음 예제와 같이 배열 데이터 형식을 변환할 수도 있습니다.

```vb
Dim v() As classV
Dim obArray() As Object
' Assume some object array has been assigned to obArray.
' Check for run-time type compatibility.
If TypeOf obArray Is classV()
    ' obArray can be converted to classV.
    v = CType(obArray, classV())
End If
```

자세한 내용 및 예제는 [배열 변환](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)을 참조 하세요.

### <a name="types-defining-ctype"></a>CType을 정의 하는 형식

정의한 클래스 또는 `CType` 구조체를 정의할 수 있습니다. 이를 통해 클래스 또는 구조체의 형식으로 값을 변환할 수 있습니다. 자세한 내용 및 예제를 보려면 [방법: 변환 연산자](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)를 정의 합니다.

> [!NOTE]
> 변환 키워드와 함께 사용 되는 값은 대상 데이터 형식에 대해 유효 해야 합니다. 그렇지 않으면 오류가 발생 합니다. `Long` 예를 들어를 `Integer`로 변환 하려고 하면의 `Long` 값이 `Integer` 데이터 형식에 대 한 유효한 범위 내에 있어야 합니다.

> [!CAUTION]
> 소스 형식이 대상 형식에서 파생 되지 않은 경우 런타임에 한 클래스 형식에서 다른 형식으로 변환 하는작업이실패합니다.`CType` 이러한 오류는 <xref:System.InvalidCastException> 예외를 throw 합니다.

그러나 형식 중 하나가 정의 된 구조체 또는 클래스이 고 해당 구조체 또는 클래스에서를 정의한 `CType` 경우 `CType`의 요구 사항을 충족 하는 경우 변환이 성공할 수 있습니다. [방법: 변환 연산자](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)를 정의 합니다.

명시적 변환을 수행 하는 것은 지정 된 데이터 형식 또는 개체 클래스로 식을 *캐스팅* 하는 것으로 알려져 있습니다.

## <a name="see-also"></a>참고자료

- [Visual Basic 형식 변환](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
- [문자열과 다른 형식 사이의 변환](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)
- [방법: Visual Basic에서 개체를 다른 형식으로 변환](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)
- [구조체](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [데이터 형식](../../../../visual-basic/language-reference/data-types/index.md)
- [형식 변환 함수](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [데이터 형식 문제 해결](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)
