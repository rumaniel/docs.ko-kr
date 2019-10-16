---
title: '>> 연산자 (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.>>
helpviewer_keywords:
- operator>>
- '>> operator [Visual Basic]'
- bit shift operators [Visual Basic]
- operator >>
- right shift operators [Visual Basic]
ms.assetid: 054dc6a6-47d9-47ef-82da-cfa2b59fbf8f
ms.openlocfilehash: 337d651e831dc2ab132056f6e9a1f2b5300bf7f8
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701324"
---
# <a name="-operator-visual-basic"></a>> > 연산자 (Visual Basic)
비트 패턴에 산술 오른쪽 시프트를 수행 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
result = pattern >> amount  
```  
  
## <a name="parts"></a>요소  
 `result`  
 필수. 정수 숫자 값입니다. 결과 비트 패턴을 이동한입니다. 데이터 형식이 동일 `pattern`합니다.  
  
 `pattern`  
 필수. 정수 계열 숫자 식입니다. 이동할 비트 패턴입니다. 데이터 형식은 정수 계열 형식 이어야 합니다 (`SByte`, `Byte`, `Short`, `UShort`를 `Integer`를 `UInteger`를 `Long`, 또는 `ULong`).  
  
 `amount`  
 필수. 숫자 식입니다. 비트 패턴을 이동할 비트 수입니다. 데이터 형식 이어야 합니다 `Integer` 변환할 또는 `Integer`합니다.  
  
## <a name="remarks"></a>설명  
 산술 시프트는 순환 하지 않습니다. 즉, 결과의 한쪽 끝에서 이동 하는 비트가 다른 쪽 끝에서는 다시 계산 되지 않습니다. 산술 오른쪽 시프트에서 가장 오른쪽 비트 위치를 넘어 이동 하는 비트는 무시 되 고 맨 왼쪽 (부호) 비트가 왼쪽에서 비워진 비트 위치로 전파 됩니다. 즉, `pattern`에 음수 값이 있으면 빈 위치가 1로 설정 됩니다. 그렇지 않으면 0으로 설정 됩니다.  
  
 @No__t-0, `UShort`, `UInteger` 및 `ULong` 데이터 형식은 부호가 없으므로 전파할 부호 비트가 없습니다. @No__t-0이 부호 없는 형식이 면 빈 위치는 항상 0으로 설정 됩니다.  
  
 결과에 포함 될 수 있는 것 보다 더 많은 비트로 이동 하지 않도록 하려면 Visual Basic는-1 @no__t의 데이터 형식에 해당 하는 크기 마스크와 `amount` 값을 마스크 합니다. 이러한 값의 이진은 이동 양에 사용 됩니다. 크기 마스크는 다음과 같습니다.  
  
|@No__t 데이터 형식-0|크기 마스크 (10 진수)|크기 마스크 (16 진수)|  
|----------------------------|---------------------------|-------------------------------|  
|`SByte`, `Byte`|7|&H00000007|  
|`Short`, `UShort`|15|&H0000000F|  
|`Integer`, `UInteger`|31|&H0000001F|  
|`Long`, `ULong`|63|&H0000003F|  
  
 @No__t-0이 0 인 경우 `result`의 값은 `pattern`의 값과 동일 합니다. @No__t-0이 음수 이면 부호 없는 값으로 사용 되 고 적절 한 크기 마스크로 마스크 됩니다.  
  
 산술 시프트는 오버플로 예외를 생성 하지 않습니다.  
  
## <a name="overloading"></a>오버로딩  
 연산자를 오버 로드할 수 있습니다. 즉, 피연산자가 해당 클래스 또는 구조체의 형식일 때 클래스 또는 구조체의 동작을 다시 정의할 수 있습니다. `>>` 코드가 이러한 클래스 또는 구조체에서이 연산자를 사용 하는 경우 다시 정의 된 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 `>>` 연산자를 사용 하 여 정수 값에 대 한 산술 오른쪽 시프트를 수행 합니다. 결과는 항상 이동 하는 식의 데이터 형식과 같습니다.  
  
 [!code-vb[VbVbalrOperators#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#14)]  
  
 앞의 예제 결과는 다음과 같습니다.  
  
- `result1`은 2560 (0000 1010 0000 0000)입니다.  
  
- `result2`은 160 (0000 0000 1010 0000)입니다.  
  
- `result3`은 2 (0000 0000 0000 0010)입니다.  
  
- `result4`은 640 (0000 0010 1000 0000)입니다.  
  
- `result5`은 0 (오른쪽으로 15 자리 이동)입니다.  
  
 @No__t-0의 이동 크기는 18과 15로 계산 되며 2와 같습니다.  
  
 다음 예에서는 음수 값에 대 한 산술 변화를 보여 줍니다.  
  
 [!code-vb[VbVbalrOperators#55](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#55)]  
  
 앞의 예제 결과는 다음과 같습니다.  
  
- `negresult1`은-512 (1111 1110 0000 0000)입니다.  
  
- (부호 비트가 전파 됨)입니다.  
  
## <a name="see-also"></a>참조

- [비트 시프트 연산자](../../../visual-basic/language-reference/operators/bit-shift-operators.md)
- [할당 연산자](../../../visual-basic/language-reference/operators/assignment-operators.md)
- [>>= 연산자](../../../visual-basic/language-reference/operators/right-shift-assignment-operator.md)
- [Visual Basic에서의 연산자 우선 순위](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Visual Basic의 산술 연산자](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
