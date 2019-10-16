---
title: CStr 함수의 반환 값(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- times [Visual Basic], CStr Function return values
- type conversion [Visual Basic]
- dates [Visual Basic], CStr Function return values
- CStr function
- strings [Visual Basic], return value
- Date data type [Visual Basic], converting
- dates [Visual Basic]
- String data type [Visual Basic], converting
ms.assetid: 3aa744e7-1419-45d5-85e3-e5abc2953673
ms.openlocfilehash: cd525ea5a295411e509f3bc37285675d15a8c4f4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69930046"
---
# <a name="return-values-for-the-cstr-function-visual-basic"></a>CStr 함수의 반환 값(Visual Basic)
다음 표에서는의 `CStr` `expression`여러 데이터 형식에 대 한 반환 값을 설명 합니다.  
  
|형식이 `expression` 인 경우|`CStr` return|  
|-----------------------------|--------------------|  
|[Boolean 데이터 형식](../../../visual-basic/language-reference/data-types/boolean-data-type.md)|"True" 또는 "False"를 포함 하는 문자열입니다.|  
|[Date 데이터 형식](../../../visual-basic/language-reference/data-types/date-data-type.md)|시스템의 간단한 날짜 `Date` 형식 값 (날짜 및 시간)을 포함 하는 문자열입니다.|  
|[숫자 데이터 형식](../../../visual-basic/programming-guide/language-features/data-types/numeric-data-types.md)|숫자를 나타내는 문자열입니다.|  
  
## <a name="cstr-and-date"></a>CStr 및 Date  
 형식 `Date` 에는 항상 날짜 및 시간 정보가 포함 됩니다. 형식 변환의 목적을 위해 Visual Basic은 1/1/0001 (1 년 1 월 1 일)을 날짜의 *중립 값* 으로 간주 하 고 00:00:00 (자정)을 시간에 대 한 중립 값으로 간주 합니다. `CStr`결과 문자열에 중립 값을 포함 하지 않습니다. 예를 들어 문자열로 변환 `#January 1, 0001 9:30:00#` 하는 경우 결과는 "9:30:00 AM"이 고 날짜 정보는 표시 되지 않습니다. 그러나 날짜 정보는 여전히 원래 `Date` 값과 같은 함수를 사용 하 여 복구할 수 있습니다 <xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A>합니다.  
  
> [!NOTE]
> 함수 `CStr` 는 응용 프로그램의 현재 문화권 설정에 따라 변환을 수행 합니다. 숫자의 문자열 표현을 특정 문화권에서을 사용 수의 `ToString(IFormatProvider)` 메서드. 예를 들어 형식의 <xref:System.Double.ToString%2A?displayProperty=nameWithType> `Double` 값을로 `String`변환할 때를 사용 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A>
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [Boolean 데이터 형식](../../../visual-basic/language-reference/data-types/boolean-data-type.md)
- [Date 데이터 형식](../../../visual-basic/language-reference/data-types/date-data-type.md)
