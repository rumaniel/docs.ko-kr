---
title: UShort 데이터 형식(Visual Basic)
ms.date: 01/31/2018
f1_keywords:
- vb.ushort
helpviewer_keywords:
- numbers [Visual Basic], whole
- literal type characters [Visual Basic], US
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- data types [Visual Basic], integral
- UShort data type
- US literal type characters [Visual Basic]
ms.assetid: 138db892-665d-4ba8-9cae-d8d91c4a8f39
ms.openlocfilehash: d85219fad631b09c19eac054b87d4843b0c73a45
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64646933"
---
# <a name="ushort-data-type-visual-basic"></a>UShort 데이터 형식 (Visual Basic)

0에서 65,535 범위의 부호 없는 16 비트 (2 바이트) 정수를 저장 합니다.  
  
## <a name="remarks"></a>설명

 사용 된 `UShort` 데이터 형식에 비해 너무 큰 이진 데이터를 포함 하도록 `Byte`합니다.  
  
 `UShort`의 기본값은 0입니다.  

## <a name="literal-assignments"></a>리터럴 할당

선언 하 고 초기화할 수 있습니다는 `UShort` 변수 (Visual Basic 2017부터) 이진 리터럴을 또는 10 진수 리터럴, 16 진수 리터럴, 8 진수 리터럴을 할당 합니다. 정수 리터럴이 `UShort` 범위를 벗어나는 경우(즉 <xref:System.UInt16.MinValue?displayProperty=nameWithType>보다 작거나 <xref:System.UInt16.MaxValue?displayProperty=nameWithType>보다 큰 경우) 컴파일 오류가 발생합니다.

다음 예제에서는 10 진수, 16 진수 표현 된 65,034와 같은 정수가 및 이진 리터럴로에 할당 된 `UShort` 값입니다.
  
[!code-vb[UShort](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#UShort)]

> [!NOTE]
> 접두사를 사용할 `&h` 또는 `&H` 16 진수 리터럴, 접두사를 나타내는 `&b` 또는 `&B` 이진 리터럴 및 접두사를 나타내는 `&o` 또는 `&O` 8 진수 리터럴을 나타냅니다. 10진수 리터럴에는 접두사가 없습니다.

Visual Basic 2017부터 사용할 수도 있습니다 밑줄 문자 `_`, 가독성 향상을 위해 숫자 구분 기호를 다음 예제와 같이 보여 줍니다.

[!code-vb[UShort](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#UShortS)]

Visual Basic 15.5부터 사용할 수도 있습니다는 밑줄 문자 (`_`) 접두사 및 16 진수, 이진 또는 8 진수 숫자 사이의 선행 구분 기호로 합니다. 예를 들어:

```vb
Dim number As UShort = &H_FF8C
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

숫자 리터럴을 포함할 수도 있습니다는 `US` 또는 `us` [문자를 입력](../../programming-guide/language-features/data-types/type-characters.md) 나타내기 위해는 `UShort` 다음 예제와 같이 데이터 형식입니다.

```vb
Dim number = &H_5826us
```

## <a name="programming-tips"></a>프로그래밍 팁
  
- **음수를 사용할 수 있습니다.** 때문에 `UShort` 부호 없는 형식에는 음수를 나타낼 수 없습니다. 단항 빼기를 사용 하는 경우 (`-`) 형식으로 계산 되는 식에 연산자 `UShort`, Visual Basic 변환 식이 `Integer` 첫 번째입니다.  
  
- **CLS 규격입니다.** 합니다 `UShort` 데이터 형식이 아닙니다 부분 합니다 [공용 언어 사양](https://www.ecma-international.org/publications/standards/Ecma-335.htm) (CLS), CLS 규격 코드를 사용 하는 구성 요소를 사용할 수 없습니다 있도록 합니다.
  
- **확대 합니다.** `UShort` 데이터 형식으로 확장 되는지를 `Integer`, `UInteger`, `Long`, `ULong`를 `Decimal`, `Single`, 및 `Double`합니다. 즉, 변환할 수 있습니다 `UShort` 발생 없이 이러한 형식 중 하나에 <xref:System.OverflowException?displayProperty=nameWithType> 오류입니다.  
  
- **형식 문자입니다.** 리터럴 형식 문자를 추가 `US` 리터럴에 리터럴에 `UShort` 데이터 형식입니다. `UShort` 에 식별자 형식 문자가 없습니다.  
  
- **Framework 형식입니다.** .NET Framework에서 해당하는 형식은 <xref:System.UInt16?displayProperty=nameWithType> 구조체입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.UInt16>
- [데이터 형식](../../../visual-basic/language-reference/data-types/index.md)
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [변환 요약](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [방법: 부호 없는 형식을 사용하는 Windows 함수 호출](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [데이터 형식의 효율적 사용](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
