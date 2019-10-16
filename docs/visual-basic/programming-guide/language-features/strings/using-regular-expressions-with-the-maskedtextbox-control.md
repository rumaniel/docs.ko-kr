---
title: Visual Basic에서 MaskedTextBox 컨트롤과 함께 정규식 사용
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], regular expressions
- strings [Visual Basic], masked edit
ms.assetid: 2a048fb0-7053-487d-b2c5-ffa5e22ed6f9
ms.openlocfilehash: e0165fb8d573878ae19378b2656d89627680b804
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62024510"
---
# <a name="using-regular-expressions-with-the-maskedtextbox-control-in-visual-basic"></a>Visual Basic에서 MaskedTextBox 컨트롤과 함께 정규식 사용
이 예제에서는 간단한 정규식 작업을 변환 하는 방법에 설명 합니다 <xref:System.Windows.Forms.MaskedTextBox> 제어 합니다.  
  
## <a name="description-of-the-masking-language"></a>마스킹 언어 설명  
 표준 <xref:System.Windows.Forms.MaskedTextBox> 에 사용 되는 언어를 마스킹 기반는 `Masked Edit` Visual Basic 6.0에서 제어 하 고 해당 플랫폼에서 마이그레이션하는 사용자에 잘 알고 있어야 합니다.  
  
 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A> 의 속성을 <xref:System.Windows.Forms.MaskedTextBox> 컨트롤 입력된 마스크를 사용 하 여 지정 합니다. 마스크 다음 테이블에서 마스킹 요소 중 하나 이상이 구성 된 문자열 이어야 합니다.  
  
|요소를 마스킹|설명|정규식 요소|  
|---------------------|-----------------|--------------------------------|  
|0|0에서 9 사이의 한 자리 수입니다. 필수 항목입니다.|\d|  
|9|숫자 또는 공백이 있습니다. 선택적 항목입니다.|[ \d]?|  
|#|숫자 또는 공백이 있습니다. 선택적 항목입니다. 이 위치에 정보를 마스크에 입력 하지 않으면 공간으로 렌더링 됩니다. 더하기 (+) 및 빼기 (-) 기호를 사용할 수 있습니다.|[ \d+-]?|  
|L|ASCII 문자입니다. 필수 항목입니다.|[a-zA-Z]|  
|?|ASCII 문자입니다. 선택적 항목입니다.|[a-zA-Z]?|  
|&|문자. 필수 항목입니다.|[\p{Ll}\p{Lu}\p{Lt}\p{Lm}\p{Lo}]|  
|C|문자. 선택적 항목입니다.|[\p{Ll}\p{Lu}\p{Lt}\p{Lm}\p{Lo}]?|  
|A|영숫자입니다. 선택적 항목입니다.|\W|  
|.|10 진수 자리 표시자 적절 한 문화권입니다.|사용할 수 없습니다.|  
|,|Culture에 따른 천 단위 자리 표시자입니다.|사용할 수 없습니다.|  
|:|Culture에 따른 시간 구분 기호입니다.|사용할 수 없습니다.|  
|/|Culture에 따른 날짜 구분 기호입니다.|사용할 수 없습니다.|  
|$|문화권에 적합 한 통화 기호입니다.|사용할 수 없습니다.|  
|\<|소문자로 뒤에 있는 모든 문자를 변환 합니다.|사용할 수 없습니다.|  
|>|대문자로 뒤에 있는 모든 문자를 변환 합니다.|사용할 수 없습니다.|  
|&#124;|이전의 등록 취소 또는 아래쪽으로 이동 합니다.|사용할 수 없습니다.|  
|&#92;|리터럴로 설정 마스크 문자를 이스케이프 합니다. "\\\\" 백슬래시 이스케이프 시퀀스입니다.|&#92;|  
|다른 모든 문자입니다.|리터럴입니다. 모든 마스크가 아닌 요소 내에 그대로 표시 됩니다 <xref:System.Windows.Forms.MaskedTextBox>합니다.|다른 모든 문자입니다.|  
  
 소수점 (.), 1/1000 (,), 시간 (:), (/), 날짜 및 통화 ($) 기호 기본 응용 프로그램의 문화권에서 정의 된 대로 해당 기호를 표시 합니다. 사용 하 여 다른 문화권에 대 한 기호를 표시 하도록 할 수 있습니다는 <xref:System.Windows.Forms.MaskedTextBox.FormatProvider%2A> 속성입니다.  
  
## <a name="regular-expressions-and-masks"></a>정규식과 마스크  
 사용자 입력 유효성 검사에 정규식 및 마스크를 사용할 수 있습니다, 있지만 완전히 동일 하지 않습니다. 정규식 마스크 보다 더 복잡 한 패턴을 표현할 수 있지만 더 간결 하 고 관련 형식으로에 마스크 동일한 정보를 표현할 수 있습니다.  
  
 다음 표에서 각 4 정규식 및 해당 하는 마스크를 비교합니다.  
  
|정규식|마스크|노트|  
|------------------------|----------|-----------|  
|`\d{2}/\d{2}/\d{4}`|`00/00/0000`|`/` 마스크의 문자를 논리적 날짜 구분 기호 이며 사용자에 게 응용 프로그램의 현재 문화권에 적합 한 날짜 구분 기호로 표시 됩니다.|  
|`\d{2}-[A-Z][a-z]{2}-\d{4}`|`00->L<LL-0000`|날짜 (일, 월의 약어 및 연도) 미국 형식 뒤에 두 문자는 소문자 초기 대문자를 사용 하 여 표시 되는 세 자리 월의 약어입니다.|  
|`(\(\d{3}\)-)?\d{3}-d{4}`|`(999)-000-0000`|미국 전화 번호로 지역 번호는 선택 사항입니다. 사용자 필요에 따라 문자 입력을 원하지 않는, 경우 그녀 공간을 입력 하거나 첫 번째 0이 나타나는 마스크의 위치에 있는 직접 마우스 포인터를 놓습니다.|  
|`$\d{6}.00`|`$999,999.00`|0-999999 사이의 통화 값입니다. 통화, 1000 단위 구분 및 10 진수 문자 바뀝니다 런타임 시 문화권별 해당 합니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.MaskedTextBox.Mask%2A>
- <xref:System.Windows.Forms.MaskedTextBox>
- [Visual Basic의 문자열 유효성 검사](../../../../visual-basic/programming-guide/language-features/strings/validating-strings.md)
- [MaskedTextBox 컨트롤](../../../../framework/winforms/controls/maskedtextbox-control-windows-forms.md)
