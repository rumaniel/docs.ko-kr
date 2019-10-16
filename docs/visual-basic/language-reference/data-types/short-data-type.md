---
title: Short 데이터 형식(Visual Basic)
ms.date: 01/31/2018
f1_keywords:
- vb.Short
helpviewer_keywords:
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- data types [Visual Basic], integral
- S literal type character [Visual Basic]
- Short data type
- literal type characters [Visual Basic], S
ms.assetid: 65fcbcf3-a841-400e-885e-301497729a8b
ms.openlocfilehash: eedc2804652fb6f2f73e7288d6db830a6f4bd98a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64647017"
---
# <a name="short-data-type-visual-basic"></a>Short 데이터 형식 (Visual Basic)
부호 있는 16 비트 (2 바이트) 정수 값 범위에 있는-32,768부터 32,767 까지의 저장 합니다.  
  
## <a name="remarks"></a>설명  
 사용 된 `Short` 의 전체 데이터 너비를 필요 하지 않은 정수 값을 포함 하는 데이터 형식 `Integer`합니다. 일부 경우에 공용 언어 런타임 팩 수에 `Short` 변수 밀접 하 게 함께 및 메모리 사용량을 저장 합니다.  
  
 `Short`의 기본값은 0입니다.  
  
## <a name="literal-assignments"></a>리터럴 할당

선언 하 고 초기화할 수 있습니다는 `Short` 변수 (Visual Basic 2017부터) 이진 리터럴을 또는 10 진수 리터럴, 16 진수 리터럴, 8 진수 리터럴을 할당 합니다. 정수 리터럴이 `Short` 범위를 벗어나는 경우(즉 <xref:System.Int16.MinValue?displayProperty=nameWithType>보다 작거나 <xref:System.Int16.MaxValue?displayProperty=nameWithType>보다 큰 경우) 컴파일 오류가 발생합니다.

다음 예제에서는 10 진수, 16 진수 표현 된 1,034와 같은 정수가 및 이진 리터럴로의 암시적으로 변환 됩니다 [정수](integer-data-type.md) 에 `Short` 값입니다.

[!code-vb[Short](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#Short)]

> [!NOTE]
> 접두사를 사용할 `&h` 또는 `&H` 16 진수 리터럴, 접두사를 나타내는 `&b` 또는 `&B` 이진 리터럴 및 접두사를 나타내는 `&o` 또는 `&O` 8 진수 리터럴을 나타냅니다. 10진수 리터럴에는 접두사가 없습니다.

Visual Basic 2017부터 사용할 수도 있습니다 밑줄 문자 `_`, 가독성 향상을 위해 숫자 구분 기호를 다음 예제와 같이 보여 줍니다.

[!code-vb[Short](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#ShortS)]

Visual Basic 15.5부터 사용할 수도 있습니다는 밑줄 문자 (`_`) 접두사 및 16 진수, 이진 또는 8 진수 숫자 사이의 선행 구분 기호로 합니다. 예를 들어:

```vb
Dim number As Short = &H_3264
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

숫자 리터럴을 포함할 수도 있습니다는 `S` [문자를 입력](../../programming-guide/language-features/data-types/type-characters.md) 나타내기 위해는 `Short` 다음 예제와 같이 데이터 형식입니다.

```vb
Dim number = &H_3264S
```

## <a name="programming-tips"></a>프로그래밍 팁

- **확대 합니다.** `Short` 데이터 형식으로 확장 되는지를 `Integer`를 `Long`, `Decimal`를 `Single`, 또는 `Double`합니다. 이는 `Short` 오류 발생 없이 <xref:System.OverflowException?displayProperty=nameWithType>를 이러한 형식 중 하나로 변환할 수 있음을 의미합니다.  
  
- **형식 문자입니다.** 리터럴 형식 문자 `S`를 리터럴에 추가하면 `Short` 데이터 형식이 됩니다. `Short` 에 식별자 형식 문자가 없습니다.  
  
- **Framework 형식입니다.** .NET Framework에서 해당하는 형식은 <xref:System.Int16?displayProperty=nameWithType> 구조체입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Int16?displayProperty=nameWithType>
- [데이터 형식](../../../visual-basic/language-reference/data-types/index.md)
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [변환 요약](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [Integer 데이터 형식](../../../visual-basic/language-reference/data-types/integer-data-type.md)
- [Long 데이터 형식](../../../visual-basic/language-reference/data-types/long-data-type.md)
- [데이터 형식의 효율적 사용](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
