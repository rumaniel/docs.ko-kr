---
title: + 연산자 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.+
helpviewer_keywords:
- arithmetic operators [Visual Basic], addition
- + operator
- concatenation operators [Visual Basic], syntax
- strings [Visual Basic], concatenating
- sum operator [Visual Basic]
ms.assetid: 5694778f-0a2c-4539-8009-f66f318fb46d
ms.openlocfilehash: 3187551afb7d25470f48dad894188766a811bb0a
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701007"
---
# <a name="-operator-visual-basic"></a>+ 연산자(Visual Basic)
숫자 식의 양수 값을 두 개 더 추가 하거나 반환 합니다. 를 사용 하 여 두 문자열 식을 연결할 수도 있습니다.  
  
## <a name="syntax"></a>구문  
  
```vb
expression1 + expression2
```
  
로 구분하거나 여러

```vb  
+expression1  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`expression1`|필수. 임의의 숫자 또는 문자열 식입니다.|  
|`expression2`|@No__t-0 연산자가 음수 값을 계산 하는 경우에만 필요 합니다. 임의의 숫자 또는 문자열 식입니다.|  
  
## <a name="result"></a>결과  
 @No__t-0이 고 @no__t가 모두 숫자인 경우 결과는 산술 합입니다.  
  
 @No__t-0이 없으면 `+` 연산자는 변경 되지 않은 식 값의 *단항* id 연산자입니다. 이 경우 작업은 `expression1`의 부호를 유지 하는 것으로 구성 되므로 `expression1`이 음수 이면 결과는 음수입니다.  
  
 @No__t-0과 `expression2`이 모두 문자열이 면 결과는 값의 연결입니다.  
  
 @No__t-0 및 `expression2`이 혼합 유형인 경우 수행 되는 작업은 해당 유형, 해당 내용 및 [Option Strict 문의](../../../visual-basic/language-reference/statements/option-strict-statement.md)설정에 따라 달라 집니다. 자세한 내용은 "주의"의 표를 참조 하십시오.  
  
## <a name="supported-types"></a>지원 형식  
 부호 없는 형식 및 부동 소수점 형식 및 `Decimal` @no__t을 포함 하는 모든 숫자 형식입니다.  
  
## <a name="remarks"></a>설명  
 일반적으로 `+`은 가능한 경우 산술 덧셈을 수행 하 고 두 식이 모두 문자열인 경우에만 연결 합니다.  
  
 두 식이 모두 `Object` 이면 Visual Basic는 다음 작업을 수행 합니다.  
  
|식의 데이터 형식|컴파일러 작업|  
|---|---|  
|두 식은 모두 숫자 데이터 형식 (`SByte`, `Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single` 또는 @no__t)입니다.|추가. 결과 데이터 형식은 및 `expression1` `expression2`의 데이터 형식에 적합 한 숫자 형식입니다. [연산자 결과의 데이터 형식](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md)에서 "정수 산술 연산" 표를 참조 하세요.|  
|두 식의 형식은 모두 `String`입니다.|연결.|  
|한 식은 숫자 데이터 형식이 고 다른 하나는 문자열입니다.|@No__t-0이-1 @no__t 경우 컴파일러 오류를 생성 합니다.<br /><br /> @No__t-0 `Off` 이면 `String`를 `Double`으로 암시적으로 변환 하 여를 추가 합니다.<br /><br /> @No__t-0을 `Double`로 변환할 수 없는 경우 <xref:System.InvalidCastException> 예외를 throw 합니다.|  
|한 식은 숫자 데이터 형식이 고 다른 하나는 [Nothing](../../../visual-basic/language-reference/nothing.md) 입니다.|@No__t-0 값을 0으로 하 여를 추가 합니다.|  
|한 식은 문자열이 고 다른 식은 `Nothing`입니다.|@No__t-0 값을 ""로 연결 합니다.|  
  
 한 식이 `Object` 식인 경우 Visual Basic는 다음 작업을 수행 합니다.  
  
|식의 데이터 형식|컴파일러 작업|  
|---|---|  
|`Object` 식은 숫자 값을 포함 하 고 다른 식은 숫자 데이터 형식입니다.|@No__t-0이-1 @no__t 경우 컴파일러 오류를 생성 합니다.<br /><br /> @No__t-0 `Off` 이면를 추가 합니다.|  
|`Object` 식은 숫자 값을 포함 하 고 다른 하나는-1 @no__t 형식입니다.|@No__t-0이-1 @no__t 경우 컴파일러 오류를 생성 합니다.<br /><br /> @No__t-0 `Off` 이면 `String`를 `Double`으로 암시적으로 변환 하 여를 추가 합니다.<br /><br /> @No__t-0을 `Double`로 변환할 수 없는 경우 <xref:System.InvalidCastException> 예외를 throw 합니다.|  
|`Object` 식은 문자열을 포함 하 고 다른 식은 숫자 데이터 형식입니다.|@No__t-0이-1 @no__t 경우 컴파일러 오류를 생성 합니다.<br /><br /> @No__t-0 `Off` 인 경우는 문자열 `Object`를 `Double`로 암시적으로 변환 하 고을 추가 합니다.<br /><br /> @No__t-0 문자열을 `Double`로 변환할 수 없는 경우 <xref:System.InvalidCastException> 예외를 throw 합니다.|  
|`Object` 식은 문자열을 포함 하 고 다른 하나는-1 @no__t 형식입니다.|@No__t-0이-1 @no__t 경우 컴파일러 오류를 생성 합니다.<br /><br /> @No__t-0 `Off` 인 경우에는 `Object`를 `String`으로 암시적으로 변환 하 고 연결 합니다.|  
  
 두 식이 모두 `Object` 식인 경우 Visual Basic는 다음 작업을 수행 합니다 (`Option Strict Off`에만 해당).  
  
|식의 데이터 형식|컴파일러 작업|  
|---|---|  
|@No__t-0 식에는 모두 숫자 값이 포함 됩니다.|추가.|  
|@No__t-0 식의 형식은 `String`입니다.|연결.|  
|한 `Object` 식에는 숫자 값이 포함 되 고 다른 하나에는 문자열이 포함 됩니다.|문자열 `Object`을 `Double`로 암시적으로 변환 하 고을 추가 합니다.<br /><br /> @No__t-0 문자열을 숫자 값으로 변환할 수 없는 경우 <xref:System.InvalidCastException> 예외를 throw 합니다.|  
  
 @No__t-0 식이 [Nothing](../../../visual-basic/language-reference/nothing.md) 또는 <xref:System.DBNull>로 계산 되는 경우 `+` 연산자는 값을 ""의 `String`로 처리 합니다.  
  
> [!NOTE]
> @No__t-0 연산자를 사용 하는 경우 더하기 또는 문자열 연결의 발생 여부를 확인 하지 못할 수 있습니다. 모호성을 제거 하 고 자체 문서화 코드를 제공 하려면 연결에 `&` 연산자를 사용 합니다.  
  
## <a name="overloading"></a>오버로딩  
 연산자를 오버 로드할 수 있습니다. 즉, 피연산자가 해당 클래스 또는 구조체의 형식일 때 클래스 또는 구조체의 동작을 다시 정의할 수 있습니다. `+` 코드가 이러한 클래스 또는 구조체에서이 연산자를 사용 하는 경우 다시 정의 된 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 `+` 연산자를 사용 하 여 숫자를 추가 합니다. 피연산자가 둘 다 숫자인 경우 Visual Basic 산술 결과를 계산 합니다. 산술 결과는 두 피연산자의 합계를 나타냅니다.  
  
 [!code-vb[VbVbalrOperators#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#6)]  
  
 @No__t-0 연산자를 사용 하 여 문자열을 연결할 수도 있습니다. 피연산자가 둘 다 문자열이 면 Visual Basic 연결 합니다. 연결 결과는 두 피연산자의 콘텐츠로 구성 된 단일 문자열을 나타냅니다.  
  
 피연산자가 혼합 형식인 경우 결과는 [Option Strict 문의](../../../visual-basic/language-reference/statements/option-strict-statement.md)설정에 따라 달라 집니다. 다음 예에서는 `Option Strict`이-1 @no__t 경우의 결과를 보여 줍니다.  
  
 [!code-vb[VbVbalrOperators#53](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class3.vb#53)]  
  
 [!code-vb[VbVbalrOperators#50](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class2.vb#50)]  
[!code-vb[VbVbalrOperators#51](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class2.vb#51)]  
  
 다음 예에서는 `Option Strict`이-1 @no__t 경우의 결과를 보여 줍니다.  
  
 [!code-vb[VbVbalrOperators#54](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class2.vb#54)]  
  
 [!code-vb[VbVbalrOperators#50](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class2.vb#50)]  
[!code-vb[VbVbalrOperators#52](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class2.vb#52)]  
  
 모호성을 없애기 위해 연결에는-1 @no__t 대신 `&` 연산자를 사용 해야 합니다.  
  
## <a name="see-also"></a>참조

- [& 연산자](../../../visual-basic/language-reference/operators/concatenation-operator.md)
- [연결 연산자](../../../visual-basic/language-reference/operators/concatenation-operators.md)
- [산술 연산자](../../../visual-basic/language-reference/operators/arithmetic-operators.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Visual Basic에서의 연산자 우선 순위](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [Visual Basic의 산술 연산자](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
- [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md)
