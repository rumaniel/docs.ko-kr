---
title: UInteger 데이터 형식 (Visual Basic)
ms.date: 01/31/2018
f1_keywords:
- vb.uinteger
helpviewer_keywords:
- numbers [Visual Basic], whole
- UInteger data type
- literal type characters [Visual Basic], UI
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- UI literal type characters [Visual Basic]
- data types [Visual Basic], integral
ms.assetid: db7ddd34-4f23-46f5-84dd-8b0f83bb8729
ms.openlocfilehash: 12447e56f89914121dcc9eda2bee0700343baf12
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64646994"
---
# <a name="uinteger-data-type"></a>UInteger 데이터 형식

0에서 4294967295 까지의 부호 없는 32 비트 (4 바이트) 정수를 저장 합니다.  
  
## <a name="remarks"></a>설명

 `UInteger` 데이터 형식은 가장 효율적인 데이터 너비의 가장 큰 부호 없는 값을 제공 합니다.  
  
 `UInteger`의 기본값은 0입니다.  
  
## <a name="literal-assignments"></a>리터럴 할당

선언 하 고 초기화할 수 있습니다는 `UInteger` 변수 (Visual Basic 2017부터) 이진 리터럴을 또는 10 진수 리터럴, 16 진수 리터럴, 8 진수 리터럴을 할당 합니다. 정수 리터럴이 `UInteger` 범위를 벗어나는 경우(즉 <xref:System.UInt32.MinValue?displayProperty=nameWithType>보다 작거나 <xref:System.UInt32.MaxValue?displayProperty=nameWithType>보다 큰 경우) 컴파일 오류가 발생합니다.

다음 예제에서는 10진수, 16진수 및 이진 리터럴로 표현된 3,000,000,000과 같은 정수가 `UInteger` 값에 할당됩니다.
  
[!code-vb[UInteger](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#UInt)]  

> [!NOTE] 
> 접두사를 사용할 `&h` 또는 `&H` 16 진수 리터럴, 접두사를 나타내는 `&b` 또는 `&B` 이진 리터럴 및 접두사를 나타내는 `&o` 또는 `&O` 8 진수 리터럴을 나타냅니다. 10진수 리터럴에는 접두사가 없습니다.

Visual Basic 2017부터 사용할 수도 있습니다 밑줄 문자 `_`, 가독성 향상을 위해 숫자 구분 기호를 다음 예제와 같이 보여 줍니다.

[!code-vb[UInteger](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#UIntS)]  

Visual Basic 15.5부터 사용할 수도 있습니다는 밑줄 문자 (`_`) 접두사 및 16 진수, 이진 또는 8 진수 숫자 사이의 선행 구분 기호로 합니다. 예를 들어:

```vb
Dim number As UInteger = &H_0F8C_0326
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

숫자 리터럴을 포함할 수도 있습니다는 `UI` 또는 `ui` [문자를 입력](../../programming-guide/language-features/data-types/type-characters.md) 나타내기 위해는 `UInteger` 다음 예제와 같이 데이터 형식입니다.

```vb
Dim number = &H_0FAC_14D7ui
```

## <a name="programming-tips"></a>프로그래밍 팁

 `UInteger` 하 고 `Integer` 데이터 형식 때문에 32 비트 프로세서에서 최적의 성능을 제공 작은 정수 형식 (`UShort`, `Short`, `Byte`, 및 `SByte`) 비트 수가 사용 하더라도, 데 더 오래 걸릴 로드, 저장 및 인출 합니다.  
  
- **음수를 사용할 수 있습니다.** 때문에 `UInteger` 부호 없는 형식에는 음수를 나타낼 수 없습니다. 단항 빼기를 사용 하는 경우 (`-`) 형식으로 계산 되는 식에 연산자 `UInteger`, Visual Basic 변환 식이 `Long` 첫 번째입니다.  
  
- **CLS 규격입니다.** 합니다 `UInteger` 데이터 형식이 아닙니다 부분 합니다 [공용 언어 사양](https://www.ecma-international.org/publications/standards/Ecma-335.htm) (CLS), CLS 규격 코드를 사용 하는 구성 요소를 사용할 수 없습니다 있도록 합니다.
  
- **Interop 고려 사항입니다.** 예제에서는 자동화 개체나 COM 개체에 대 한.NET Framework 용으로 작성 되지 구성 요소와 상호 작용 하는 경우와 같은 형식은 있음을 염두에 둡니다 `uint` 다른 환경에서 다른 데이터 너비 (16 비트)를 가질 수 있습니다. 이러한 구성 요소는 16 비트 인수를 전달 하는 경우로 선언 `UShort` 대신 `UInteger` 관리 되는 Visual Basic 코드에서.  
  
- **확대 합니다.** `UInteger` 데이터 형식으로 확장 되는지를 `Long`를 `ULong`, `Decimal`를 `Single`, 및 `Double`합니다. 즉, 변환할 수 있습니다 `UInteger` 발생 없이 이러한 형식 중 하나에 <xref:System.OverflowException?displayProperty=nameWithType> 오류입니다.  
  
- **형식 문자입니다.** 리터럴 형식 문자를 추가 `UI` 리터럴에 리터럴에 `UInteger` 데이터 형식입니다. `UInteger` 에 식별자 형식 문자가 없습니다.  
  
- **Framework 형식입니다.** .NET Framework에서 해당하는 형식은 <xref:System.UInt32?displayProperty=nameWithType> 구조체입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.UInt32>
- [데이터 형식](../../../visual-basic/language-reference/data-types/index.md)
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [변환 요약](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [방법: 부호 없는 형식을 사용하는 Windows 함수 호출](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [데이터 형식의 효율적 사용](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
