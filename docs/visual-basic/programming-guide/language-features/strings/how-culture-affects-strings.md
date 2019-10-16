---
title: Visual Basic에서 문화권이 문자열에 영향을 주는 방식
ms.date: 07/20/2015
helpviewer_keywords:
- locale [Visual Basic], effect on strings
- strings [Visual Basic], locale dependence
ms.assetid: c4664444-ee0d-47bf-bef1-eaa3c54bdd7f
ms.openlocfilehash: d090a6e89a470958dd323c3f249ed0658dc1cefa
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69955096"
---
# <a name="how-culture-affects-strings-in-visual-basic"></a>Visual Basic에서 문화권이 문자열에 영향을 주는 방식
이 도움말 페이지에서는 Visual Basic 문화권 정보를 사용 하 여 문자열 변환 및 비교를 수행 하는 방법을 설명 합니다.  
  
## <a name="when-to-use-culture-specific-strings"></a>문화권 관련 문자열을 사용 하는 경우  
 일반적으로 사용자에 게 제공 되는 모든 데이터에 대해 문화권별 문자열을 사용 하 고 응용 프로그램의 내부 데이터에 대해 문화권 고정 문자열을 사용 해야 합니다.  
  
 예를 들어 응용 프로그램에서 사용자에 게 날짜를 문자열로 입력 하도록 요청 하는 경우 사용자는 문화권에 따라 문자열의 형식을 지정 하 고 응용 프로그램에서 문자열을 적절 하 게 변환 해야 합니다. 그런 다음 응용 프로그램에서 해당 날짜를 사용자 인터페이스에 표시 하는 경우 사용자의 문화권에 해당 날짜를 표시 해야 합니다.  
  
 그러나 응용 프로그램이 날짜를 중앙 서버에 업로드 하는 경우에는 잠재적으로 서로 다른 날짜 형식 간의 혼동을 방지 하기 위해 하나의 특정 문화권에 따라 문자열의 형식을 지정 해야 합니다.  
  
## <a name="culture-sensitive-functions"></a>문화권 구분 함수  
 `Str` 및`Val` 함수를 제외 하 고 모든 Visual Basic 문자열 변환 함수는 응용 프로그램의 문화권 정보를 사용 하 여 변환 및 비교가 응용 프로그램의 문화권에 적합 한지 확인 합니다. 정의.  
  
 다른 문화권 설정을 사용 하는 컴퓨터에서 실행 되는 응용 프로그램에서 문자열 변환 함수를 성공적으로 사용 하려면 특정 문화권 설정을 사용 하는 함수를 이해 하 고 현재 문화권 설정을 사용 하는 것이 중요 합니다. 응용 프로그램의 문화권 설정은 기본적으로 운영 체제의 문화권 설정에서 상속 됩니다. 자세한 내용은,,, <xref:Microsoft.VisualBasic.Strings.Asc%2A>,,, 및 <xref:Microsoft.VisualBasic.Strings.Format%2A> [형식 변환 함수](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)를 참조 <xref:Microsoft.VisualBasic.Conversion.Hex%2A> <xref:Microsoft.VisualBasic.Strings.AscW%2A> <xref:Microsoft.VisualBasic.Strings.Chr%2A> <xref:Microsoft.VisualBasic.Strings.ChrW%2A> <xref:Microsoft.VisualBasic.Conversion.Oct%2A>하세요.  
  
 ( `Str` 숫자를 문자열로 변환) 및 `Val` (문자열을 숫자로 변환) 함수는 문자열과 숫자 사이를 변환할 때 응용 프로그램의 문화권 정보를 사용 하지 않습니다. 대신 마침표 (.)만 유효한 소수 구분 기호로 인식 합니다. 이러한 함수의 문화권을 인식 하는 analogues은 다음과 같습니다.  
  
- **현재 문화권을 사용 하는 변환입니다.** 및 함수는 숫자를 문자열로 변환 하 고 및 `CInt` 함수는 `CDbl` 문자열을 숫자로 변환 합니다. `Format` `CStr`  
  
- **특정 문화권을 사용 하는 변환입니다.** 각 숫자 개체에는 `ToString(IFormatProvider)` 숫자를 문자열로 `Parse(String, IFormatProvider)` 변환 하는 메서드와 문자열을 숫자로 변환 하는 메서드가 있습니다. 예 `Double` 를 들어 형식은 <xref:System.Double.ToString%28System.IFormatProvider%29> 및 <xref:System.Double.Parse%28System.String%2CSystem.IFormatProvider%29> 메서드를 제공 합니다.  
  
 자세한 내용은 <xref:Microsoft.VisualBasic.Conversion.Str%2A> 및 <xref:Microsoft.VisualBasic.Conversion.Val%2A>를 참조하세요.  
  
## <a name="using-a-specific-culture"></a>특정 문화권 사용  
 웹 서비스에 날짜 (문자열로 형식이 지정 됨)를 전송 하는 응용 프로그램을 개발 하 고 있다고 가정 합니다. 이 경우 응용 프로그램은 문자열 변환에 특정 문화권을 사용 해야 합니다. 이유를 설명 하려면 날짜의 <xref:System.DateTime.ToString> 메서드를 사용한 결과를 고려 합니다. 응용 프로그램에서이 메서드를 사용 하 여 날짜를 7 년 7 월 4 2005 일 형식으로 지정 하는 경우에는 미국 영어 (en-us) 문화권을 사용 하 여 실행할 때 "7/4/2005 12:00:00 AM"을 반환 하지만 독일어 (de-de) 문화권으로 실행 하면 "04.07.2005 00:00:00"이 반환 됩니다.  
  
 특정 문화권 형식으로 문자열 변환을 수행 해야 하는 경우 .NET Framework에 기본 제공 되는 `CultureInfo` 클래스를 사용 해야 합니다. 문화권의 이름을 <xref:System.Globalization.CultureInfo.%23ctor%2A> 생성자에 `CultureInfo` 전달 하 여 특정 문화권에 대 한 새 개체를 만들 수 있습니다. 지원 되는 문화권 이름은 <xref:System.Globalization.CultureInfo> 클래스 도움말 페이지에 나열 되어 있습니다.  
  
 또는 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 속성에서 *고정 문화권* 의 인스턴스를 가져올 수 있습니다. 고정 문화권은 영어 문화권을 기반으로 하지만 약간의 차이가 있습니다. 예를 들어 고정 문화권은 12 시간 시계 대신 24 시간제를 지정 합니다.  
  
 날짜를 문화권의 문자열로 변환 하려면 <xref:System.Globalization.CultureInfo> 개체를 date 개체의 <xref:System.DateTime.ToString%28System.IFormatProvider%29> 메서드에 전달 합니다. 예를 들어 다음 코드는 응용 프로그램의 문화권 설정에 관계 없이 "07/04/2005 00:00:00"를 표시 합니다.  
  
 [!code-vb[VbVbalrConcepts#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConcepts/VB/Class1.vb#1)]  
  
> [!NOTE]
> 날짜 리터럴은 항상 영어 문화권에 따라 해석 됩니다.  
  
## <a name="comparing-strings"></a>문자열 비교  
 다음과 같은 두 가지 중요 한 상황에서 문자열 비교가 필요 합니다.  
  
- **사용자에 게 표시할 데이터를 정렬 합니다.** 문자열이 적절 하 게 정렬 되도록 현재 문화권에 따라 작업을 사용 합니다.  
  
- **두 응용 프로그램 내부 문자열이 정확 하 게 일치 하는지 확인 (일반적으로 보안상의 목적)** 현재 문화권을 무시 하는 작업을 사용 합니다.  
  
 Visual Basic <xref:Microsoft.VisualBasic.Strings.StrComp%2A> 함수를 사용 하 여 두 가지 유형의 비교를 수행할 수 있습니다. 비교 유형을 제어 `Compare` 하는 선택적 인수를 지정 합니다. `Text` 대부분의 입력 및 출력 `Binary` 은 정확히 일치 하는 항목을 결정 하는 데 사용할 수 있습니다.  
  
 함수 `StrComp` 는 정렬 순서를 기반으로 두 비교 문자열 간의 관계를 나타내는 정수를 반환 합니다. 결과 값이 양수 이면 첫 번째 문자열이 두 번째 문자열 보다 큰지 나타냅니다. 음수 결과는 첫 번째 문자열이 더 작으므로 0은 문자열이 일치 함을 나타냅니다.  
  
 [!code-vb[VbVbalrStrings#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class1.vb#22)]  
  
 `StrComp` 함수의 .NET Framework 파트너 <xref:System.String.Compare%2A?displayProperty=nameWithType> (메서드)를 사용할 수도 있습니다. 기본 문자열 클래스의 오버 로드 된 정적 메서드입니다. 다음 예제에서는이 메서드를 사용 하는 방법을 보여 줍니다.  
  
 [!code-vb[VbVbalrStrings#48](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#48)]  
  
 비교를 수행 하는 방법을 보다 세밀 하 게 제어 하기 위해 <xref:System.String.Compare%2A> 메서드의 추가 오버 로드를 사용할 수 있습니다. 메서드를 사용 하 여 `comparisonType` 인수를 사용 하 여 사용할 비교 형식을 지정할 수 있습니다. <xref:System.String.Compare%2A?displayProperty=nameWithType>  
  
|`comparisonType` 인수 값|비교 유형|사용 시기|  
|---|---|---|  
|`Ordinal`|문자열의 구성 요소 바이트를 기준으로 하는 비교입니다.|비교할 때이 값을 사용 합니다 .이 값은 대/소문자 구분 식별자, 보안 관련 설정 또는 해당 바이트가 정확히 일치 해야 하는 기타 비 언어적 식별자입니다.|  
|`OrdinalIgnoreCase`|문자열의 구성 요소 바이트를 기준으로 하는 비교입니다.<br /><br /> `OrdinalIgnoreCase`는 고정 문화권 정보를 사용 하 여 두 문자가 대문자 표시의 차이점을 확인 합니다.|대/소문자를 구분 하지 않는 식별자, 보안 관련 설정 및 Windows에 저장 된 데이터를 비교할 때이 값을 사용 합니다.|  
|`CurrentCulture` 또는 `CurrentCultureIgnoreCase`|현재 문화권의 문자열 해석을 기반으로 하는 비교입니다.|사용자에 게 표시 되는 데이터, 대부분의 사용자 입력 및 언어 해석이 필요한 기타 데이터를 비교할 때 이러한 값을 사용 합니다.|  
|`InvariantCulture` 또는 `InvariantCultureIgnoreCase`|고정 문화권의 문자열 해석을 기반으로 하는 비교입니다.<br /><br /> 고정 문화권은 허용 된 `Ordinal` 범위 `OrdinalIgnoreCase`를 벗어난 문자를 동일한 고정 문자로 처리 하기 때문에이는 및와는 다릅니다.|데이터 유지를 비교 하거나 고정 정렬 순서가 필요한 언어적으로 관련 된 데이터를 표시 하는 경우에만 이러한 값을 사용 합니다.|  
  
### <a name="security-considerations"></a>보안 고려 사항  
 애플리케이션에서 비교 또는 대/소문자 변경 작업의 결과에 따라 보안 결정 다음 작업을 사용 해야 합니다 <xref:System.String.Compare%2A?displayProperty=nameWithType> 메서드를 통과 `Ordinal` 또는 `OrdinalIgnoreCase` 에 대 한는 `comparisonType` 인수입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Globalization.CultureInfo>
- [Visual Basic의 문자열 소개](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
- [형식 변환 함수](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
