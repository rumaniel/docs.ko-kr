---
title: CType 함수(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.CType
helpviewer_keywords:
- expression conversion results
- explicit data type conversions [Visual Basic]
- CType function
- conversions [Visual Basic], expression
ms.assetid: dd4b29e7-6fa1-428c-877e-69955420bb72
ms.openlocfilehash: 4a0391b0a5d76f36803b433369d4832c02b05e09
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71592105"
---
# <a name="ctype-function-visual-basic"></a>CType 함수(Visual Basic)

식을 지정한 데이터 형식, 개체, 구조체, 클래스 또는 인터페이스로 명시적으로 변환한 결과를 반환 합니다.

## <a name="syntax"></a>구문

```vb
CType(expression, typename)
```

## <a name="parts"></a>요소

`expression` 모든 유효한 식입니다. @No__t-0의 값이 `typename`에서 허용 하는 범위를 벗어나면 Visual Basic에서 예외를 throw 합니다.

`typename` `Dim` 문의 `As` 절, 즉 모든 데이터 형식, 개체, 구조체, 클래스 또는 인터페이스의 이름에 적합 한 식입니다.

## <a name="remarks"></a>설명

> [!TIP]
> 다음 함수를 사용 하 여 형식 변환을 수행할 수도 있습니다.
>
> - 특정 데이터 형식으로 변환을 수행 하는 `CByte`, `CDbl`, `CInt`와 같은 형식 변환 함수 자세한 내용은 [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)를 참조하세요.
> - [DirectCast operator](../../../visual-basic/language-reference/operators/directcast-operator.md) 또는 [TryCast operator](../../../visual-basic/language-reference/operators/trycast-operator.md). 이러한 연산자를 적용 하려면 한 형식이 다른 형식에서 상속 하거나 다른 형식을 구현 해야 합니다. @No__t-1 데이터 형식으로 변환할 때 `CType` 보다 약간 더 나은 성능을 제공할 수 있습니다.

`CType`은 인라인으로 컴파일되어 있습니다. 즉, 변환 코드는 식을 계산 하는 코드의 일부입니다. 변환을 수행 하기 위해 프로시저가 호출 되지 않기 때문에 코드가 더 빨리 실행 되는 경우도 있습니다.

@No__t-0에서-1 @no__t로의 변환이 정의 되지 않은 경우 (예: `Integer`에서 `Date`) Visual Basic 컴파일 타임 오류 메시지를 표시 합니다.

런타임에 변환이 실패 하면 적절 한 예외가 throw 됩니다. 축소 변환에 실패 하는 경우 <xref:System.OverflowException>이 가장 일반적인 결과입니다. 변환이 정의 되어 있지 않으면 <xref:System.InvalidCastException>이 throw 됩니다. 예를 들어 `expression`이 `Object` 형식이 고 런타임 형식이 `typename`로 변환 되지 않은 경우이 문제가 발생할 수 있습니다.

@No__t-0 또는 `typename`의 데이터 형식이 정의한 클래스 또는 구조체 인 경우 해당 클래스 또는 구조체에 대 한 `CType`를 변환 연산자로 정의할 수 있습니다. 이렇게 하면 `CType`이 *오버 로드 된 연산자*역할을 합니다. 이 작업을 수행 하는 경우 throw 할 수 있는 예외를 포함 하 여 클래스 또는 구조체에서 변환의 동작을 제어할 수 있습니다.

## <a name="overloading"></a>오버로딩

@No__t-0 연산자는 코드 외부에서 정의 된 클래스 또는 구조체에서 오버 로드 될 수도 있습니다. 코드가 이러한 클래스나 구조체 간에 변환 되는 경우 `CType` 연산자의 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.

## <a name="converting-dynamic-objects"></a>동적 개체 변환

동적 개체의 형식 변환은 <xref:System.Dynamic.DynamicObject.TryConvert%2A> 또는 <xref:System.Dynamic.DynamicMetaObject.BindConvert%2A> 메서드를 사용 하는 사용자 정의 동적 변환에 의해 수행 됩니다. 동적 개체로 작업 하는 경우 <xref:Microsoft.VisualBasic.Conversion.CTypeDynamic%2A> 메서드를 사용 하 여 동적 개체를 변환 합니다.

## <a name="example"></a>예제

다음 예에서는 `CType` 함수를 사용 하 여 식을 `Single` 데이터 형식으로 변환 합니다.

[!code-vb[VbVbalrFunctions#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#24)]

추가 예제는 [암시적 변환과 명시적 변환](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)을 참조 하세요.

## <a name="see-also"></a>참조

- <xref:System.OverflowException>
- <xref:System.InvalidCastException>
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [변환 함수](../../../visual-basic/language-reference/functions/conversion-functions.md)
- [Operator 문](../../../visual-basic/language-reference/statements/operator-statement.md)
- [방법: 변환 연산자 정의 @ no__t-0
- [.NET Framework의 형식 변환](../../../standard/base-types/type-conversion.md)
