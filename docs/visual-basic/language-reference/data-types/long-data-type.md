---
title: Long 데이터 형식(Visual Basic)
ms.date: 01/31/2018
f1_keywords:
- vb.Long
helpviewer_keywords:
- identifier type characters [Visual Basic], &
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- '& identifier type character'
- integer numbers
- literal type characters [Visual Basic], L
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- L literal type character [Visual Basic]
- integers [Visual Basic], types
- Long keyword [Visual Basic]
- data types [Visual Basic], integral
- data types [Visual Basic], assigning
- Long data type
ms.assetid: b4770c34-1804-4f8c-b512-c10b0893e516
ms.openlocfilehash: 040306b49bbf6b0f30556309457510ca873d8a74
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50197225"
---
# <a name="long-data-type-visual-basic"></a>Long 데이터 형식 (Visual Basic)

포함 까지의 부호 있는 64 비트 (8 바이트) 정수 값-9223372036854775808에서 9223372036854775807 (9.2... E + 18).  
  
## <a name="remarks"></a>설명

 사용 된 `Long` 데이터 형식에 맞게 너무 큰 정수를 포함 하는 `Integer` 데이터 형식.  
  
 `Long`의 기본값은 0입니다.

## <a name="literal-assignments"></a>리터럴 할당 

선언 하 고 초기화할 수 있습니다는 `Long` 변수 (Visual Basic 2017부터) 이진 리터럴을 또는 10 진수 리터럴, 16 진수 리터럴, 8 진수 리터럴을 할당 합니다. 정수 리터럴이 `Long` 범위를 벗어나는 경우(즉 <xref:System.Int64.MinValue?displayProperty=nameWithType>보다 작거나 <xref:System.Int64.MaxValue?displayProperty=nameWithType>보다 큰 경우) 컴파일 오류가 발생합니다.

다음 예제에서는 10진수, 16진수 및 이진 리터럴로 표현된 4,294,967,296과 같은 정수가 `Long` 값에 할당됩니다.
  
[!code-vb[long](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#Long)]  

> [!NOTE]
> 접두사를 사용할 `&h` 또는 `&H` 16 진수 리터럴, 접두사를 나타내는 `&b` 또는 `&B` 이진 리터럴 및 접두사를 나타내는 `&o` 또는 `&O` 8 진수 리터럴을 나타냅니다. 10진수 리터럴에는 접두사가 없습니다.

Visual Basic 2017부터 사용할 수도 있습니다 밑줄 문자 `_`, 가독성 향상을 위해 숫자 구분 기호를 다음 예제와 같이 보여 줍니다.

[!code-vb[long](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#LongS)]

Visual Basic 15.5부터 사용할 수도 있습니다는 밑줄 문자 (`_`) 접두사 및 16 진수, 이진 또는 8 진수 숫자 사이의 선행 구분 기호로 합니다. 예를 들어:

```vb
Dim number As Long = &H_0FAC_0326_1489_D68C
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

숫자 리터럴을 포함할 수도 있습니다는 `L` [문자를 입력](../../programming-guide\language-features\data-types/type-characters.md) 나타내기 위해는 `Long` 다음 예제와 같이 데이터 형식입니다.

```vb
Dim number = &H_0FAC_0326_1489_D68CL
```

## <a name="programming-tips"></a>프로그래밍 팁

-   **Interop 고려 사항입니다.** 예제에서는 자동화 개체나 COM 개체에 대 한.NET Framework 용으로 작성 되지 구성 요소와 상호 작용 하는 경우에 유의 해야 `Long` 다른 환경에서 다른 데이터 너비 (32 비트)에 있습니다. 이러한 구성 요소는 32 비트 인수를 전달 하는 경우로 선언 `Integer` 대신 `Long` 새 Visual Basic 코드에서.  
  
-   **확대 합니다.** 합니다 `Long` 데이터 형식으로 확장 되는지를 `Decimal`를 `Single`, 또는 `Double`합니다. 이는 `Long` 오류 발생 없이 <xref:System.OverflowException?displayProperty=nameWithType>를 이러한 형식 중 하나로 변환할 수 있음을 의미합니다.  
  
-   **형식 문자입니다.** 리터럴 형식 문자 `L`를 리터럴에 추가하면 `Long` 데이터 형식이 됩니다. 식별자 형식 문자 `&`를 식별자에 추가하면 `Long`가 됩니다.  
  
-   **Framework 형식입니다.** .NET Framework에서 해당하는 형식은 <xref:System.Int64?displayProperty=nameWithType> 구조체입니다.  

## <a name="see-also"></a>참고자료

<xref:System.Int64>
[데이터 형식](../../../visual-basic/language-reference/data-types/index.md)   
[정수 데이터 형식](../../../visual-basic/language-reference/data-types/integer-data-type.md)   
[Short 데이터 형식](../../../visual-basic/language-reference/data-types/short-data-type.md)   
[형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
[변환 요약](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
[데이터 형식의 효율적 사용](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
