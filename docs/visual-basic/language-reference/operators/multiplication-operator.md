---
title: '* 연산자 (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.*
helpviewer_keywords:
- arithmetic operators [Visual Basic], multiplication
- operators [Visual Basic], multiplication
- '* operator [Visual Basic]'
- multiplication operator [Visual Basic], syntax
- math operators [Visual Basic]
ms.assetid: 2b210382-99da-4195-89ba-b1d06f5e89ad
ms.openlocfilehash: b5b601c7604cb7ce1afaebc98b2157634a77fda4
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701087"
---
# <a name="-operator-visual-basic"></a>* 연산자(Visual Basic)
두 숫자를 곱합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
number1 * number2  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`number1`|필수. 임의의 숫자 식입니다.|  
|`number2`|필수. 임의의 숫자 식입니다.|  
  
## <a name="result"></a>결과  
 결과 `number1`과 `number2`의 곱입니다.  
  
## <a name="supported-types"></a>지원 형식  
 부호 없는 형식 및 부동 소수점 형식 및 `Decimal`를 포함 하는 모든 숫자 형식입니다.  
  
## <a name="remarks"></a>설명  
 결과의 데이터 형식은 피연산자의 형식에 따라 달라 집니다. 다음 표에서는 결과의 데이터 형식을 결정 하는 방법을 보여 줍니다.  
  
|피연산자 데이터 형식|Result 데이터 형식|  
|---|---|  
|두 식은 모두 정수 데이터 형식 ([SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md), [Byte](../../../visual-basic/language-reference/data-types/byte-data-type.md), [Short](../../../visual-basic/language-reference/data-types/short-data-type.md), [UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md), [Integer](../../../visual-basic/language-reference/data-types/integer-data-type.md), [UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md), [Long](../../../visual-basic/language-reference/data-types/long-data-type.md), [ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md))입니다.|@No__t의 데이터 형식에 적합 한 숫자 데이터 형식으로,-0 및 `number2`입니다. [연산자 결과의 데이터 형식](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md)에서 "정수 산술 연산" 표를 참조 하세요.|  
|두 식이 모두 [Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md) 입니다.|`Decimal`|  
|두 식이 모두 [단일](../../../visual-basic/language-reference/data-types/single-data-type.md) 입니다.|`Single`|  
|두 식이 모두 부동 소수점 데이터 형식 (`Single` 또는 [Double](../../../visual-basic/language-reference/data-types/double-data-type.md)) 이지만 `Single`가 아닙니다 (참고 `Decimal`은 부동 소수점 데이터 형식이 아님).|`Double`|  
  
 식이 [Nothing](../../../visual-basic/language-reference/nothing.md)으로 계산 되 면 0으로 처리 됩니다.  
  
## <a name="overloading"></a>오버로딩  
 연산자를 오버 로드할 수 있습니다. 즉, 피연산자가 해당 클래스 또는 구조체의 형식일 때 클래스 또는 구조체의 동작을 다시 정의할 수 있습니다. `*` 코드가 이러한 클래스 또는 구조체에서이 연산자를 사용 하는 경우 다시 정의 된 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 이 예에서는 `*` 연산자를 사용 하 여 두 숫자를 곱합니다. 결과는 두 피연산자의 곱입니다.  
  
 [!code-vb[VbVbalrOperators#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#4)]  
  
## <a name="see-also"></a>참조

- [*= 연산자](../../../visual-basic/language-reference/operators/multiplication-assignment-operator.md)
- [산술 연산자](../../../visual-basic/language-reference/operators/arithmetic-operators.md)
- [Visual Basic에서의 연산자 우선 순위](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Visual Basic의 산술 연산자](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
