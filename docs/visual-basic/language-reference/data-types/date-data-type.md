---
title: Date 데이터 형식(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Date
helpviewer_keywords:
- Date data type
- dates [Visual Basic], Visual Basic data types
- times [Visual Basic], Date data type
- Date literals [Visual Basic]
- data values [Visual Basic]
- times [Visual Basic], Visual Basic data types
- dates [Visual Basic], Date data type
- data types [Visual Basic], assigning
- literals [Visual Basic], Date
- '# specifier for Date literals'
ms.assetid: d9edf5b0-e85e-438b-a1cf-1f321e7c831b
ms.openlocfilehash: ee966cdfcc957f1164c73f577fa668b203a82113
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630123"
---
# <a name="date-data-type-visual-basic"></a>Date 데이터 형식(Visual Basic)

0001년 1월 1일부터 9999년 12월 31일까지의 날짜와 오전 12:00:00(자정)부터 오후 11:59:59.9999999까지의 시간을 나타내는 IEEE 64비트(8비트) 값을 보유합니다. 각 증분은 일반 달력에서 1년 1월 1일 시작 이후 경과된 시간의 100나노초를 나타냅니다. 최대값은 10000년 1월 1일 시작 이전 100나노초를 나타냅니다.

## <a name="remarks"></a>설명

`Date` 데이터 형식을 사용하여 날짜 값, 시간 값 또는 날짜 및 시간 값을 포함합니다.

`Date`의 기본값은 0001년 1월 1일 0:00:00(자정)입니다.

<xref:Microsoft.VisualBasic.DateAndTime> 클래스에서 현재 날짜와 시간을 가져올 수 있습니다.

## <a name="format-requirements"></a>형식 요구 사항

숫자 기호(`# #`) 내의 `Date` 리터럴을 묶어야 합니다. M/d/yyyy(예: `#5/31/1993#`) 또는 yyyy-MM-dd(예: `#1993-5-31#`) 형식으로 날짜 값을 지정해야 합니다. 연도를 먼저 지정하는 경우 슬래시를 사용할 수 있습니다.  이 요구 사항은 사용자 로캘과 컴퓨터의 날짜 및 시간 형식 설정에 독립적입니다.

이러한 제한 이유는 애플리케이션을 실행하는 로캘에 따라 코드의 의미가 변경되면 안 되기 때문입니다. `#3/4/1998#`의 `Date` 리터럴을 하드 코딩하고 1998년 3월 4로 지정한다고 가정해 보세요. mm/dd/yyyy를 사용하는 로캘에서는 3/4/1998이 의도한 대로 컴파일됩니다. 그러나 여러 국가/지역에 응용 프로그램을 배포 한다고 가정 합니다. dd/mm/yyyy를 사용하는 로캘에서는 하드 코딩된 리터럴이 1998년 4월 3일로 컴파일됩니다. yyyy/mm/dd를 사용하는 로캘에서는 리터럴이 잘못 지정되며(0003년 4월 1998일) 컴파일러 오류가 발생합니다.

## <a name="workarounds"></a>해결 방법

`Date` 리터럴을 해당 로캘 형식이나 사용자 지정 형식으로 변환하려면 <xref:Microsoft.VisualBasic.Strings.Format%2A> 함수에 리터럴을 제공하고 미리 정의된 날짜 형식이나 사용자 정의 날짜 형식을 지정합니다. 다음은 이에 대한 예입니다.

```vb
MsgBox("The formatted date is " & Format(#5/31/1993#, "dddd, d MMM yyyy"))
```

또는 <xref:System.DateTime> 구조체의 오버로드된 생성자 중 하나를 사용하여 날짜 및 시간 값을 어셈블할 수 있습니다. 다음 예제에서는 1993년 5월 31일 오후 12:14를 나타내는 값을 만듭니다.

```vb
Dim dateInMay As New System.DateTime(1993, 5, 31, 12, 14, 0)
```

## <a name="hour-format"></a>시간 형식

12시간제 또는 24시간제 형식으로 시간 값을 지정할 수 있습니다(예: `#1:15:30 PM#` 또는 `#13:15:30#`). 그러나 분 또는 초를 지정하지 않는 경우 AM 또는 PM을 지정해야 합니다.

## <a name="date-and-time-defaults"></a>날짜 및 시간 기본값

날짜/시간 리터럴에 날짜를 포함하지 않으면 Visual Basic에서 값의 날짜 부분을 0001년 1월 1일로 설정합니다. 날짜/시간 리터럴에 시간을 포함하지 않으면 Visual Basic에서 값의 시간 부분을 그 날의 시작, 즉 자정(0:00:00)으로 설정합니다.

## <a name="type-conversions"></a>형식 변환

`Date` 값을 `String` 형식으로 변환하는 경우 Visual Basic에서 런타임 로캘에 지정된 약식 날짜 형식에 따라 날짜를 렌더링하고 런타임 로캘에 지정된 시간 형식(12시간제 또는 24시간제)에 따라 시간을 렌더링합니다.

## <a name="programming-tips"></a>프로그래밍 팁

- **Interop 고려 사항** 자동화 개체나 COM 개체와 같이 .NET Framework용으로 작성되지 않은 구성 요소를 조작하는 경우 다른 환경의 날짜/시간 형식이 Visual Basic `Date` 형식과 호환되지 않는 것에 유의하세요. 이러한 구성 요소에 날짜/시간 인수를 전달하는 경우 새로운 Visual Basic 코드에서 이 인수를 `Date` 대신 `Double`로 선언하고 변환 메서드 <xref:System.DateTime.FromOADate%2A?displayProperty=nameWithType> 및 <xref:System.DateTime.ToOADate%2A?displayProperty=nameWithType>를 사용합니다.

- **문자를 입력 합니다.** `Date`에는 리터럴 형식 문자 또는 식별자 형식 문자가 없습니다. 그러나 컴파일러가 숫자 기호(`# #`)로 묶인 리터럴을 `Date`로 처리합니다.

- **프레임 워크 형식입니다.** .NET Framework에서 해당하는 형식은 <xref:System.DateTime?displayProperty=nameWithType> 구조체입니다.

## <a name="example"></a>예제

`Date` 데이터 형식의 변수 또는 상수는 날짜와 시간을 모두 보유합니다. 다음은 이에 대한 예입니다.

```vb
Dim someDateAndTime As Date = #8/13/2002 12:14 PM#
```

## <a name="see-also"></a>참고자료

- <xref:System.DateTime?displayProperty=nameWithType>
- [데이터 형식](../../../visual-basic/language-reference/data-types/index.md)
- [표준 날짜 및 시간 형식 문자열](../../../standard/base-types/standard-date-and-time-format-strings.md)
- [사용자 지정 날짜 및 시간 형식 문자열](../../../standard/base-types/custom-date-and-time-format-strings.md)
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [변환 요약](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [데이터 형식의 효율적 사용](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
