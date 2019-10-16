---
title: '방법: 날짜 또는 시간을 나타내는 문자열 확인 (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], validating
- String data type [Visual Basic], validation
ms.assetid: ae7d4b29-3436-4032-bdbf-4650eb1c8e19
ms.openlocfilehash: f24ff05e48327c21c02eb92b07db17266f743a80
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62024614"
---
# <a name="how-to-validate-strings-that-represent-dates-or-times-visual-basic"></a>방법: 날짜 또는 시간을 나타내는 문자열 확인 (Visual Basic)
다음 코드 예제에서는 `Boolean` 문자열이 유효한 날짜 또는 시간을 나타내는지 여부를 나타내는 값입니다.  
  
## <a name="example"></a>예제  
 [!code-vb[VbVbcnRegEx#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnRegEx/VB/Class1.vb#2)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 바꿉니다 `("01/01/03")` 고 `"9:30 PM"` 유효성을 검사 하려는 시간과 날짜를 사용 하 여 합니다. 사용 하 여 다른 하드 코드 된 문자열을 사용 하 여 문자열을 바꿀 수 있습니다는 `String` 변수나 메서드를 사용 하 여 반환 하는 문자열 같은 `InputBox`합니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 이 메서드를 사용 하 여 문자열 변환 하려고 하기 전에 유효성을 검사 합니다 `String` 에 `DateTime` 변수. 날짜 또는 시간을 먼저 확인 하 여 런타임 시 예외를 생성을 방지할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.Information.IsDate%2A>
- <xref:Microsoft.VisualBasic.Interaction.InputBox%2A>
- [Visual Basic의 문자열 유효성 검사](../../../../visual-basic/programming-guide/language-features/strings/validating-strings.md)
