---
title: Double 데이터 형식(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Double
helpviewer_keywords:
- 'identifier type characters [Visual Basic], #'
- trailing zeros
- real numbers
- trailing 0 characters [Visual Basic]
- 0 characters [Visual Basic], trailing
- literal type characters [Visual Basic], R
- data types [Visual Basic], assigning
- Double data type [Visual Basic]
- '# identifier type character'
- double-precision numbers
- floating-point numbers [Visual Basic], Double data type
- R literal type character [Visual Basic]
- zeros, trailing
- Double data type
ms.assetid: 0c5670f7-fcb1-453a-bef1-374730cd38fd
ms.openlocfilehash: 92adb26702d94dee08e51decd845d019c797e195
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630089"
---
# <a name="double-data-type-visual-basic"></a>Double 데이터 형식(Visual Basic)

음수 324 값의 경우-1.79769313486231570 E + 308부터-4.94065645841246544 E-324 까지의 값 범위에 해당 하는 부호 있는 IEEE 64 비트 (8 바이트) 배정밀도 부동 소수점 숫자를 포함 합니다. 양수 값입니다. 배정밀도 숫자는 실수의 근사값을 저장 합니다.

## <a name="remarks"></a>설명

`Double` 데이터 형식은 숫자에 대해 가능한 가장 크고 가장 작은 크고 많을을 제공 합니다.

`Double`의 기본값은 0입니다.

## <a name="programming-tips"></a>프로그래밍 팁

- **소수.** 부동 소수점 숫자를 사용 하는 경우 항상 메모리에 정확한 표현이 없다는 점을 명심 하십시오. 이로 인해 값 비교 및 `Mod` 연산자와 같은 특정 작업에서 예기치 않은 결과가 발생할 수 있습니다. 자세한 내용은 [데이터 형식 문제 해결](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)을 참조 하세요.

- **후행 0입니다.** 부동 소수점 데이터 형식에는 후행 0 문자에 대 한 내부 표현이 없습니다. 예를 들어 4.2000과 4.2를 구분 하지 않습니다. 따라서 부동 소수점 값을 표시 하거나 인쇄할 때 후행 0 문자는 표시 되지 않습니다.

- **문자를 입력 합니다.** 리터럴 형식 문자 `R`를 리터럴에 추가하면 `Double` 데이터 형식이 됩니다. 예를 들어 정수 값 뒤에가 `R`오는 경우 값이 `Double`로 변경 됩니다.

  ```vb
  ' Visual Basic expands the 4 in the statement Dim dub As Double = 4R to 4.0:
  Dim dub As Double = 4.0R
  ```

  식별자 형식 문자 `#`를 식별자에 추가하면 `Double`가 됩니다. 다음 예제에서 변수 `num` 는 `Double`로 형식화 됩니다.

  ```vb
  Dim num# = 3
  ```

- **프레임 워크 형식입니다.** .NET Framework에서 해당하는 형식은 <xref:System.Double?displayProperty=nameWithType> 구조체입니다.

## <a name="see-also"></a>참고자료

- <xref:System.Double?displayProperty=nameWithType>
- [데이터 형식](../../../visual-basic/language-reference/data-types/index.md)
- [Decimal 데이터 형식](../../../visual-basic/language-reference/data-types/decimal-data-type.md)
- [Single 데이터 형식](../../../visual-basic/language-reference/data-types/single-data-type.md)
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [변환 요약](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [데이터 형식의 효율적 사용](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
- [데이터 형식 문제 해결](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [형식 문자](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)
