---
title: Char 데이터 형식(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Char
helpviewer_keywords:
- literal type characters [Visual Basic], C
- Char data type
- C literal type character [Visual Basic]
- data types [Visual Basic], assigning
- Char data type [Visual Basic], character literals
ms.assetid: cd7547a9-7855-4e8e-b216-35d74a362657
ms.openlocfilehash: 8313c2282a3b4b7b035f9f3b685a786c4471f53a
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630147"
---
# <a name="char-data-type-visual-basic"></a>Char 데이터 형식(Visual Basic)

0에서 65535 사이의 값에 해당 하는 부호 없는 16 비트 (2 바이트) 코드 요소를 저장 합니다. 각 *코드 포인트*또는 문자 코드는 단일 유니코드 문자를 나타냅니다.

## <a name="remarks"></a>설명

단일 문자만 포함 해야 하며의 `String`오버 헤드가 필요 하지 않은 경우 데이터형식을사용합니다.`Char` 일부 경우에는 `Char()` `Char` 요소의 배열을 사용 하 여 여러 문자를 포함할 수 있습니다.

의 `Char` 기본값은 코드 포인트가 0 인 문자입니다.

## <a name="unicode-characters"></a>유니코드 문자

유니코드의 처음 128 코드 요소 (0 – 127)는 표준 미국 키보드의 문자 및 기호에 해당 합니다. 이러한 첫 번째 128 코드 포인트가 ASCII 문자 집합에서 정의 하는 것과 동일 합니다. 두 번째 128 코드 요소 (128-255)는 특수 문자 (예: 라틴어 기반 영문자, 악센트, 통화 기호 및 분수)를 나타냅니다. 유니코드는 전 세계 텍스트 문자, 분음 부호, 수학 및 기술 기호를 비롯 한 다양 한 기호에 대해 나머지 코드 요소 (256-65535)를 사용 합니다.

변수에서 <xref:System.Char.IsPunctuation%2A> <xref:System.Char.IsDigit%2A> 및와같은메서드를사용하여유니코드분류를확인할수있습니다`Char` .

## <a name="type-conversions"></a>형식 변환

Visual Basic는와 숫자 형식 사이 `Char` 에서 직접 변환 되지 않습니다. <xref:Microsoft.VisualBasic.Strings.Asc%2A> 또는 `Char` `Integer` 함수를 사용 하 여 값을 해당 코드 포인트를 나타내는로 변환할 수 있습니다. <xref:Microsoft.VisualBasic.Strings.AscW%2A> <xref:Microsoft.VisualBasic.Strings.Chr%2A> 또는 `Integer` `Char` 함수를 사용 하 여 값을 해당 코드 포인트가 있는로 변환할 수 있습니다. <xref:Microsoft.VisualBasic.Strings.ChrW%2A>

형식 검사 스위치 ( [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md))가 on 인 경우 리터럴 형식 문자를 `Char` 데이터 형식으로 식별 하는 단일 문자 문자열 리터럴에 추가 해야 합니다. 다음은 이에 대한 예입니다. 가 on 이므로 `charVar` `Option Strict` 변수에 대 한 첫 번째 할당은 컴파일러 오류 [BC30512](../../misc/bc30512.md) 를 생성 합니다. 리터럴 형식 문자는 `c` 리터럴을 `Char` 값으로 식별 하기 때문에 두 번째는 성공적으로 컴파일됩니다.

```vb
Option Strict On

Module CharType
    Public Sub Main()
        Dim charVar As Char

        ' This statement generates compiler error BC30512 because Option Strict is On.  
        charVar = "Z"  

        ' The following statement succeeds because it specifies a Char literal.  
        charVar = "Z"c
    End Sub
End Module
```

## <a name="programming-tips"></a>프로그래밍 팁

- **음수.** `Char`는 부호 없는 형식이 며 음수 값을 나타낼 수 없습니다. 어떤 경우에는를 사용 `Char` 하 여 숫자 값을 포함 하면 안 됩니다.

- **Interop 고려 사항** .NET Framework 용으로 작성 되지 않은 구성 요소 (예: Automation 또는 COM 개체)와 상호 작용 하는 경우에는 다른 환경에서 문자 형식의 데이터 너비 (8 비트)가 서로 다를 수 있습니다. 이러한 구성 요소에 8 비트 인수를 전달 하는 경우 새 Visual Basic 코드 `Byte` `Char` 에서 대신로 선언 합니다.

- **넓혀.** 데이터 형식이로 `String`확대 됩니다. `Char` 즉,로 `Char` `String` 변환할 수 <xref:System.OverflowException?displayProperty=nameWithType>있으며이 발생 하지 않습니다.

- **문자를 입력 합니다.** 리터럴 형식 문자 `C` 를 단일 문자 문자열 리터럴에 `Char` 추가 하면 데이터 형식이 됩니다. `Char`에는 식별자 형식 문자가 없습니다.

- **프레임 워크 형식입니다.** .NET Framework에서 해당하는 형식은 <xref:System.Char?displayProperty=nameWithType> 구조체입니다.

## <a name="see-also"></a>참고자료

- <xref:System.Char?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Strings.Asc%2A>
- <xref:Microsoft.VisualBasic.Strings.AscW%2A>
- <xref:Microsoft.VisualBasic.Strings.Chr%2A>
- <xref:Microsoft.VisualBasic.Strings.ChrW%2A>
- [데이터 형식](../../../visual-basic/language-reference/data-types/index.md)
- [String 데이터 형식](../../../visual-basic/language-reference/data-types/string-data-type.md)
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [변환 요약](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [방법: 부호 없는 형식을 사용하는 Windows 함수 호출](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [데이터 형식의 효율적 사용](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
