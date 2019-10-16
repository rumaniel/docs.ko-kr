---
title: 리터럴
description: 리터럴 형식에 알아봅니다는 F# 프로그래밍 언어입니다.
ms.date: 06/28/2019
ms.openlocfilehash: 0c9ced0b505817a161ca39c6c9f853f94cedf410
ms.sourcegitcommit: eaa6d5cd0f4e7189dbe0bd756e9f53508b01989e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2019
ms.locfileid: "67610151"
---
# <a name="literals"></a>리터럴

> [!NOTE]
> 이 문서의 API 참조 링크 하면 MSDN (당분간).

이 항목에서는 테이블의 리터럴 형식을 지정 하는 방법을 보여 주는 F#입니다.

## <a name="literal-types"></a>리터럴 형식

다음 표에서 리터럴 형식에서 F#입니다. 16 진수 표기법으로 숫자를 나타내는 문자; 대/소문자 구분 하지 않습니다. 문자 형식을 식별 하는 대/소문자를 구분 하지 않습니다.

|형식|설명|접미사 또는 접두사|예제|
|----|-----------|----------------|--------|
|sbyte|부호 있는 8 비트 정수|y|`86y`<br /><br />`0b00000101y`|
|byte|부호 없는 8 비트 자연 수|uy|`86uy`<br /><br />`0b00000101uy`|
|int16|부호 있는 16 비트 정수|초|`86s`|
|uint16|부호 없는 16 비트 자연 수|us|`86us`|
|int<br /><br />int32|부호 있는 32 비트 정수|l 또는 없음|`86`<br /><br />`86l`|
|uint<br /><br />uint32|부호 없는 32 비트 자연 수|u 또는 ul|`86u`<br /><br />`86ul`|
|nativeint|서명 된 자연 수에 대 한 네이티브 포인터|n|`123n`|
|unativeint|부호 없는 자연 수는 네이티브 포인터|취소|`0x00002D3Fun`|
|int64|부호 있는 64 비트 정수|L|`86L`|
|uint64|부호 없는 64 비트 자연 수|UL|`86UL`|
|단일 float32|32 비트 부동 소수점 숫자|F 또는 f|`4.14F` 또는 `4.14f`|
|||lf|`0x00000000lf`|
|float; double|64 비트 부동 소수점 숫자|없음|`4.14` 또는 `2.3E+32` 또는 `2.3e+32`|
|||LF|`0x0000000000000000LF`|
|bigint|64 비트 표현으로 제한 되지 않는 정수|I|`9999999999999999999999999999I`|
|decimal|고정된 소수점 또는 유리수로 표현 되는 소수|M 또는 m|`0.7833M` 또는 `0.7833m`|
|Char|유니코드 문자|없음|`'a'`|
|문자열|유니코드 문자열|없음|`"text\n"`<br /><br />또는<br /><br />`@"c:\filename"`<br /><br />또는<br /><br />`"""<book title="Paradise Lost">"""`<br /><br />또는<br /><br />`"string1" + "string2"`<br /><br />참고 항목 [문자열](Strings.md)합니다.|
|byte|ASCII 문자|B|`'a'B`|
|byte[]|ASCII 문자열|B|`"text"B`|
|String 또는 byte]|축 자 문자열|@ prefix|`@"\\server\share"` (유니코드)<br /><br />`@"\\server\share"B` (ASCII)|

## <a name="named-literals"></a>명명 된 리터럴

값은 상수를 사용 하 여 표시할 수 있습니다 합니다 [리터럴](https://msdn.microsoft.com/library/465f36ce-d146-41c0-b425-679c509cd285) 특성입니다. 이 특성에 적용 하면 값을 상수로 컴파일됩니다.

패턴 일치 식에서에서 소문자로 시작 하는 식별자는 항상 바인딩을 위한 변수로 처리 됩니다 것이 아니라 리터럴로 하므로 일반적으로 사용 해야 문자가 대문자 리터럴을 정의할 때.

```fsharp
[<Literal>]
let SomeJson = """{"numbers":[1,2,3,4,5]}"""

[<Literal>]
let Literal1 = "a" + "b"

[<Literal>]
let FileLocation =   __SOURCE_DIRECTORY__ + "/" + __SOURCE_FILE__

[<Literal>]
let Literal2 = 1 ||| 64

[<Literal>]
let Literal3 = System.IO.FileAccess.Read ||| System.IO.FileAccess.Write
```

## <a name="remarks"></a>설명

유니코드 문자열에는 명시적 인코딩을 사용 하 여 지정할 수 있는 포함 될 수 있습니다 `\u` 뒤에 16 비트 16 진수 코드 (0000-FFFF) 또는 UTF-32 인코딩을 사용 하 여 지정할 수 있는 `\U` 를 나타내는 32 비트 16 진수 코드 뒤에 유니코드 코드 포인트 (00000000-0010FFFF)이 모든입니다.

이외의 다른 비트 연산자를 사용 하 여 `|||` 허용 되지 않습니다.

## <a name="integers-in-other-bases"></a>다른 밑에 있는 정수

부호 있는 32 비트 정수의 16 진수, 8 진수 또는 이진 사용 하 여 지정할 수도 있습니다는 `0x`, `0o` 또는 `0b` 각각 접두사입니다.

```fsharp
let numbers = (0x9F, 0o77, 0b1010)
// Result: numbers : int * int * int = (159, 63, 10)
```

## <a name="underscores-in-numeric-literals"></a>숫자 리터럴의 밑줄

밑줄 문자를 사용 하 여 숫자를 구분할 수 있습니다 (`_`).

```fsharp
let value = 0xDEAD_BEEF

let valueAsBits = 0b1101_1110_1010_1101_1011_1110_1110_1111

let exampleSSN = 123_456_7890
```

## <a name="see-also"></a>참고자료

- [Core.LiteralAttribute 클래스](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.literalattribute-class-%5bfsharp%5d)
