---
title: Byte 데이터 형식(Visual Basic)
ms.date: 01/31/2018
f1_keywords:
- vb.Byte
helpviewer_keywords:
- Byte data type
- data types [Visual Basic], assigning
ms.assetid: eed44dff-eaee-4937-a89f-444e418e74f6
ms.openlocfilehash: e1725b709c03b0d77cf7e28761396236b5ef1a00
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64622438"
---
# <a name="byte-data-type-visual-basic"></a>Byte 데이터 형식 (Visual Basic)
값 범위에 있는 0에서 255 까지의 부호 없는 8 비트 (1 바이트) 정수를 보유 합니다.

## <a name="remarks"></a>설명

사용 된 `Byte` 이진 데이터를 포함 하도록 데이터 형식입니다.  
  
`Byte`의 기본값은 0입니다.

## <a name="literal-assignments"></a>리터럴 할당

선언 하 고 초기화할 수 있습니다는 `Byte` 변수 (Visual Basic 2017부터) 이진 리터럴을 또는 10 진수 리터럴, 16 진수 리터럴, 8 진수 리터럴을 할당 합니다. 정수 계열 리터럴을의 범위를 벗어난 경우는 `Byte` (경우 즉, 보다 작거나 <xref:System.Byte.MinValue?displayProperty=nameWithType> 보다 크거나 <xref:System.Byte.MaxValue?displayProperty=nameWithType>), 컴파일 오류가 발생 합니다.

다음 예제에서는 10 진수, 16 진수 표현 된 201 및 이진 리터럴로의 암시적으로 변환 됩니다 [정수](integer-data-type.md) 에 `byte` 값입니다.

[!code-vb[Byte](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#Byte)]

> [!NOTE]
> 접두사를 사용할 `&h` 또는 `&H` 16 진수 리터럴, 접두사를 나타내는 `&b` 또는 `&B` 이진 리터럴 및 접두사를 나타내는 `&o` 또는 `&O` 8 진수 리터럴을 나타냅니다. 10진수 리터럴에는 접두사가 없습니다.

Visual Basic 2017부터 사용할 수도 있습니다 밑줄 문자 `_`, 가독성 향상을 위해 숫자 구분 기호를 다음 예제와 같이 보여 줍니다.

[!code-vb[Byte](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#ByteS)]  

Visual Basic 15.5부터 사용할 수도 있습니다는 밑줄 문자 (`_`) 접두사 및 16 진수, 이진 또는 8 진수 숫자 사이의 선행 구분 기호로 합니다. 예를 들어:

```vb
Dim number As Byte = &H_6A
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

## <a name="programming-tips"></a>프로그래밍 팁

- **음수를 사용할 수 있습니다.** 때문에 `Byte` 부호 없는 형식에는 음수를 나타낼 수 없습니다. 단항 빼기를 사용 하는 경우 (`-`) 형식으로 계산 되는 식에 연산자 `Byte`, Visual Basic 변환 식이 `Short` 첫 번째입니다.
  
- **형식 변환 합니다.** Visual Basic을 읽거나 파일을 작성 하는 경우, Dll, 메서드 및 속성을 호출할 때 자동 데이터 형식 간에 변환할 수 있습니다. 에 저장 된 이진 데이터 `Byte` 변수 및 배열 이러한 형식으로 변환 하는 동안 유지 됩니다. 사용 하지 않아야는 `String` 의 내용이 ANSI 및 유니코드 형식 간에 변환 하는 동안 손상 될 수 있으므로 이진 데이터에 대 한 변수입니다.

- **확대 합니다.** `Byte` 데이터 형식으로 확장 되는지를 `Short`, `UShort`, `Integer`, `UInteger`를 `Long`, `ULong`, `Decimal`, `Single`, 또는 `Double`합니다. 즉, 변환할 수 있습니다 `Byte` 발생 없이 이러한 형식 중 하나에 <xref:System.OverflowException?displayProperty=nameWithType> 오류입니다.
  
- **형식 문자입니다.** `Byte` 에 리터럴 형식 문자 또는 식별자 형식 문자가 없습니다.

- **Framework 형식입니다.** .NET Framework에서 해당하는 형식은 <xref:System.Byte?displayProperty=nameWithType> 구조체입니다.

## <a name="example"></a>예제

 다음 예에서 `b` 되는 `Byte` 변수입니다. 문은 변수의 범위 및 비트 시프트 연산자의 응용 프로그램을 보여 줍니다.

 [!code-vb[VbVbalrDataTypes#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#16)]  

## <a name="see-also"></a>참고자료

- <xref:System.Byte?displayProperty=nameWithType>
- [데이터 형식](../../../visual-basic/language-reference/data-types/index.md)
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [변환 요약](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [데이터 형식의 효율적 사용](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
