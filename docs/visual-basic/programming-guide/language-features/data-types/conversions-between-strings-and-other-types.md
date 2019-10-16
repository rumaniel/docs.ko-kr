---
title: 문자열과 다른 형식 사이의 변환(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- data type conversion [Visual Basic], string
- conversions [Visual Basic], type
- string conversion [Visual Basic]
- conversions [Visual Basic], data type
- type conversion [Visual Basic], string
- regional options
ms.assetid: c3a99596-f09a-44a5-81dd-1b89a094f1df
ms.openlocfilehash: 1e42fca7800a76cab10fd60058e34d31ae8b8830
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61907324"
---
# <a name="conversions-between-strings-and-other-types-visual-basic"></a>문자열과 다른 형식 사이의 변환(Visual Basic)
숫자를 변환할 수 있습니다 `Boolean`, 또는 날짜/시간 값을 `String`입니다. 반대 방향으로 변환할 수도 있습니다-숫자 문자열 값에서 `Boolean`, 또는 `Date` -문자열의 내용을 대상 데이터 형식의 유효한 값으로 해석 될 수 있습니다. 그렇지 않을 경우 런타임 오류가 발생 합니다.  
  
 어느 방향으로 이러한 모든 할당에 대 한 변환을 축소 변환 됩니다. 형식 변환 키워드를 사용 해야 (`CBool`, `CByte`, `CDate`, `CDbl`, `CDec`를 `CInt`, `CLng`를 `CSByte`, `CShort`를 `CSng`, `CStr`, `CUInt`, `CULng`하십시오 `CUShort`, 및 `CType`). 합니다 <xref:Microsoft.VisualBasic.Strings.Format%2A> 및 <xref:Microsoft.VisualBasic.Conversion.Val%2A> 함수 문자열 및 숫자 간의 변환에 대 한 추가 제어를 제공 합니다.  
  
 클래스 또는 구조체를 정의 하는 경우 간의 형식 변환 연산자를 정의할 수 있습니다 `String` 및 클래스 또는 구조체의 형식입니다. 자세한 내용은 [방법: 변환 연산자 정의](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)합니다.  
  
## <a name="conversion-of-numbers-to-strings"></a>숫자를 문자열로 변환  
 사용할 수는 `Format` 뿐만 아니라 적절 한 숫자를 포함할 수 있는 형식된 문자열을 숫자로 변환할 작동 하지만 또한 등의 통화 기호를 기호 서식 지정 (같은 `$`), 천 단위 구분 기호 또는 *자릿수 구분 기호* (같은 `,`), 및 소수 구분 기호 (같은 `.`). `Format` 자동으로에 따라 적절 한 기호를 사용 하는 **국가별 옵션** 는 Windows에 지정 된 설정을 **제어판**합니다.  
  
 연결 (`&`) 연산자는 다음 예제와 같이 암시적으로 숫자를 문자열로 변환할 수 있습니다.  
  
```  
' The following statement converts count to a String value.  
Str = "The total count is " & count  
```  
  
## <a name="conversion-of-strings-to-numbers"></a>문자열을 숫자로 변환  
 사용할 수는 `Val` 함수를 명시적으로 문자열의 숫자를 숫자로 변환 합니다. `Val` 숫자, 공백, 탭, 줄 바꿈 또는 마침표 이외의 문자를 발견할 때까지 문자열을 읽습니다. 시퀀스를 "& O" 및 "& H" 숫자 체계의 기본을 변경 하 고 검색을 종료 합니다. 읽기를 중단 될 때까지 `Val` 모든 적절 한 문자는 숫자 값으로 변환 합니다. 다음 문은 값을 반환 하는 예를 들어 `141.825`합니다.  
  
 `Val("   14   1.825 miles")`  
  
 문자열을 숫자 값으로 변환 하는 Visual Basic을 사용 하 여는 **국가별 옵션** 는 Windows에 지정 된 설정을 **제어판** 1000 단위를 해석 하 구분 기호, 소수 구분 기호 및 통화 기호입니다. 즉, 설정 중 하나에 변환이 성공할 수도 있습니다. 예를 들어 `"$14.20"` 허용 되는 모든 프랑스어 로캘이 있지만 영어 (미국) 로캘을에 있습니다.  
  
## <a name="see-also"></a>참고자료

- [Visual Basic의 형식 변환](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
- [확대 변환과 축소 변환](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [암시적 변환과 명시적 변환](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [방법: Visual Basic에서 다른 형식으로 변환할 개체](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)
- [배열 규칙](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)
- [데이터 형식](../../../../visual-basic/language-reference/data-types/index.md)
- [형식 변환 함수](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [.NET Framework 기반의 국가별 응용 프로그램 소개](/visualstudio/ide/introduction-to-international-applications-based-on-the-dotnet-framework)
