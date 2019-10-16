---
title: String 데이터 형식(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.String
helpviewer_keywords:
- strings [Visual Basic], character
- strings [Visual Basic], fixed-length
- string keyword [Visual Basic]
- fixed-length strings [Visual Basic], string data type
- literals [Visual Basic], string
- text [Visual Basic], String data type
- $ identifier type character
- String data type
- fixed-length strings
- string literals [Visual Basic]
- data types [Visual Basic], assigning
- String literals [Visual Basic]
- identifier type characters [Visual Basic], $
ms.assetid: 15ac03f5-cabd-42cc-a754-1df3893c25d9
ms.openlocfilehash: 6d2fd226735622de5cd7197060c05b8ac12b69f1
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71696840"
---
# <a name="string-data-type-visual-basic"></a>String 데이터 형식(Visual Basic)
0에서 65535 사이의 값 범위에 해당 하는 부호 없는 16 비트 (2 바이트) 코드 요소의 시퀀스를 저장 합니다. 각 *코드 포인트*또는 문자 코드는 단일 유니코드 문자를 나타냅니다. 문자열은 0에서 약 20억 (2 ^ 31) 자의 유니코드 문자를 포함할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 데이터 형식을 사용 하 여 `Char` 요소의 배열인 `Char()`의 배열 관리 오버 헤드 없이 여러 문자를 포함할 수 있습니다.  
  
 @No__t-0의 기본값은-1 (null 참조) @no__t입니다. 이 값은 빈 문자열 (값 `""`)과 다릅니다.  
  
## <a name="unicode-characters"></a>유니코드 문자  
 유니코드의 처음 128 코드 요소 (0 – 127)는 표준 미국 키보드의 문자 및 기호에 해당 합니다. 이러한 첫 번째 128 코드 포인트가 ASCII 문자 집합에서 정의 하는 것과 동일 합니다. 두 번째 128 코드 요소 (128-255)는 특수 문자 (예: 라틴어 기반 영문자, 악센트, 통화 기호 및 분수)를 나타냅니다. 유니코드는 다양 한 기호에 대해 나머지 코드 요소 (256-65535)를 사용 합니다. 여기에는 전 세계 텍스트 문자, 분음 부호, 수학 및 기술 기호가 포함 됩니다.  
  
 @No__t-2 변수의 개별 문자에 <xref:System.Char.IsDigit%2A> 및 <xref:System.Char.IsPunctuation%2A>과 같은 메서드를 사용 하 여 해당 유니코드 분류를 확인할 수 있습니다.  
  
## <a name="format-requirements"></a>형식 요구 사항  
 @No__t-0 리터럴을 따옴표 (`" "`)로 묶어야 합니다. 문자열의 문자 중 하나로 따옴표를 포함 해야 하는 경우에는 두 개의 연속 된 따옴표 (`""`)를 사용 합니다. 다음은 이에 대한 예입니다.  
  
```vb  
Dim j As String = "Joe said ""Hello"" to me."  
Dim h As String = "Hello"  
' The following messages all display the same thing:  
' "Joe said "Hello" to me."  
MsgBox(j)  
MsgBox("Joe said " & """" & h & """" & " to me.")  
MsgBox("Joe said """ & h & """ to me.")  
```  
  
 문자열의 따옴표를 나타내는 연속 된 따옴표는 `String` 리터럴을 시작 하 고 종료 하는 따옴표와는 독립적입니다.  
  
## <a name="string-manipulations"></a>문자열 조작  
 @No__t-0 변수에 문자열을 할당 하면 해당 문자열은 변경할 수 없습니다. 즉, 해당 문자열의 길이 또는 *내용을 변경할 수*없습니다. 어떤 방식으로든 문자열을 변경 하는 경우 Visual Basic는 새 문자열을 만들어 이전 문자열을 무시 합니다. 그러면 `String` 변수가 새 문자열을 가리킵니다.  
  
 다양 한 문자열 함수를 사용 하 여 `String` 변수의 내용을 조작할 수 있습니다. 다음 예에서는 <xref:Microsoft.VisualBasic.Strings.Left%2A> 함수를 보여 줍니다.  
  
```vb  
Dim S As String = "Database"  
' The following statement sets S to a new string containing "Data".  
S = Microsoft.VisualBasic.Left(S, 4)  
```  
  
 다른 구성 요소에 의해 생성 된 문자열은 선행 또는 후행 공백으로 채워질 수 있습니다. 이러한 문자열을 수신 하는 경우 <xref:Microsoft.VisualBasic.Strings.Trim%2A>, <xref:Microsoft.VisualBasic.Strings.LTrim%2A> 및 <xref:Microsoft.VisualBasic.Strings.RTrim%2A> 함수를 사용 하 여 이러한 공백을 제거할 수 있습니다.  
  
 문자열 조작에 대 한 자세한 내용은 [문자열](../../../visual-basic/programming-guide/language-features/strings/index.md)을 참조 하세요.  
  
## <a name="programming-tips"></a>프로그래밍 팁  
  
- **음수.** @No__t-0에 의해 유지 되는 문자는 부호가 없으며 음수 값을 나타낼 수 없습니다. 어떤 경우 든 `String`을 사용 하 여 숫자 값을 저장 하면 안 됩니다.  
  
- **Interop 고려 사항** .NET Framework 용으로 작성 되지 않은 구성 요소 (예: Automation 또는 COM 개체)와 상호 작용 하는 경우 다른 환경에서는 문자열 문자에 다른 데이터 너비 (8 비트)가 있다는 점에 주의 해야 합니다. 8 비트 문자에 대 한 문자열 인수를 이러한 구성 요소에 전달 하는 경우 새 Visual Basic 코드의 `String` 대신 `Byte` 요소의 배열인 `Byte()`으로 선언 합니다.  
  
- **문자를 입력 합니다.** 식별자 형식 문자 `$`을 식별자에 추가 하면 `String` 데이터 형식이 됩니다. `String`에는 리터럴 형식 문자가 없습니다. 그러나 컴파일러는 따옴표 (`" "`)로 묶인 리터럴을 `String`로 처리 합니다.  
  
- **프레임 워크 형식입니다.** .NET Framework에서 해당 하는 형식은 <xref:System.String?displayProperty=nameWithType> 클래스입니다.  
  
## <a name="see-also"></a>참조

- <xref:System.String?displayProperty=nameWithType>
- [데이터 형식](../../../visual-basic/language-reference/data-types/index.md)
- [Char 데이터 형식](../../../visual-basic/language-reference/data-types/char-data-type.md)
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [변환 요약](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [방법: 부호 없는 형식을 사용하는 Windows 함수 호출](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [데이터 형식의 효율적 사용](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
