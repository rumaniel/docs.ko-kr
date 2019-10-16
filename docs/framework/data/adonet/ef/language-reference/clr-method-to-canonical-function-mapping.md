---
title: 정식 함수 매핑에 대한 CLR 메서드
ms.date: 03/30/2017
ms.assetid: e3363261-2cb8-4b54-9555-2870be99b929
ms.openlocfilehash: 6f14ad8d9e8f919fe820447cc991b102319b38d5
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251221"
---
# <a name="clr-method-to-canonical-function-mapping"></a>정식 함수 매핑에 대한 CLR 메서드

Entity Framework에서는 문자열 조작 및 수식 함수와 같이 다수의 데이터베이스 시스템이 공통적으로 가지고 있는 기능을 구현하는 일련의 정식 함수를 제공합니다. 따라서 개발자는 다양한 데이터베이스 시스템을 대상으로 작업할 수 있습니다. 이러한 정식 함수는 LINQ to Entities와 같은 쿼리 기술에서 호출하면 사용 중인 공급자에 해당하는 올바른 저장소 함수로 변환됩니다. 그러면 함수 호출이 다양한 데이터 소스에서 공통적인 형태로 표현될 수 있으며, 따라서 다수의 데이터 소스에서 일관적인 쿼리를 사용할 수 있습니다. 피연산자가 숫자 형식인 경우 비트 AND, OR, NOT 및 XOR 연산자도 정식 함수에 매핑됩니다. 부울 피연산자의 경우 비트 AND, OR, NOT 및 XOR 연산자는 피연산자의 논리 AND, OR, NOT 및 XOR 연산을 컴퓨팅합니다. 자세한 내용은 [정식 함수](canonical-functions.md)를 참조 하세요.

LINQ 시나리오의 경우, Entity Framework에 대한 쿼리에서는 정식 함수를 통해 특정 CLR 메서드를 기본 데이터 소스에 대한 메서드에 매핑합니다. LINQ to Entities 쿼리의 메서드 호출이 정식 함수에 명시적으로 매핑되지 않는 경우 런타임에 <xref:System.NotSupportedException> 예외가 throw됩니다.

## <a name="systemstring-method-static-mapping"></a>System.String 메서드(정적) 매핑

|System.String 메서드(정적)|정식 함수|
|-------------------------------------|------------------------|
|System.String Concat(String `str0`, String `str1`)|Concat(`str0`, `str1`)|
|System.String Concat(String `str0`, String `str1`, String `str2`)|Concat(Concat(`str0`, `str1`), `str2`)|
|System.String Concat(String `str0`, String `str1`, String `str2`, String `str03`)|Concat(Concat(Concat(`str0`, `str1`), `str2`), `str3`)|
|Boolean Equals(String `a`, String `b`)|= 연산자|
|Boolean IsNullOrEmpty(String `value`)|(IsNull(`value`)) 또는 Length(`value`) = 0|
|Boolean op_Equality(String `a`, String `b`)|= 연산자|
|Boolean op_Inequality(String `a` , String `b`)|!= 연산자|
|Microsoft.VisualBasic.Strings.Trim(String `str`)|Trim(`str`)|
|Microsoft.VisualBasic.Strings.LTrim(String `str`)|Ltrim(`str`)|
|Microsoft.VisualBasic.Strings.RTrim(String `str`)|Rtrim(`str`)|
|Microsoft.VisualBasic.Strings.Len(String `expression`)|Length(`expression`)|
|Microsoft.VisualBasic.Strings.Left(String `str`, Int32 `Length`)|Left(`str`, `Length`)|
|Microsoft.VisualBasic.Strings.Mid(String `str`, Int32 `Start`, Int32 `Length`)|Substring(`str`, `Start`, `Length`)|
|Microsoft.VisualBasic.Strings.Right(String `str`, Int32 `Length`)|Right(`str`, `Length`)|
|Microsoft.VisualBasic.Strings.UCase(String `Value`)|ToUpper(`Value`)|
|Microsoft.VisualBasic.Strings.LCase(String Value)|ToLower(`Value`)|

## <a name="systemstring-method-instance-mapping"></a>System.String 메서드(인스턴스) 매핑

|System.String 메서드(인스턴스)|정식 함수|참고|
|---------------------------------------|------------------------|-----------|
|Boolean Contains(String `value`)|`this` LIKE '%`value`%'|가 상수가 아니면 IndexOf (`this`, `value`) > 0으로 매핑됩니다. `value`|
|Boolean EndsWith(String `value`)|`this` LIKE `'`%`value`'|`value`가 상수가 아니면 Right(`this`, length(`value`)) = `value`에 매핑됩니다.|
|Boolean StartsWith(String `value`)|`this` LIKE '`value`%'|`value`가 상수가 아니면 IndexOf(`this`, `value`) = 1에 매핑됩니다.|
|길이|Length(`this`)||
|Int32 IndexOf(String `value`)|IndexOf(`this`, `value`) - 1||
|System.String Insert(Int32 `startIndex`, String `value`)|Concat(Concat(Substring(`this`, 1, `startIndex`), `value`), Substring(`this`, `startIndex`+1, Length(`this`) - `startIndex`))||
|System.String Remove(Int32 `startIndex`)|Substring(`this`, 1, `startIndex`)||
|System.String Remove(Int32 `startIndex`, Int32 `count`)|Concat (substring (`this`, 1, `startIndex`), substring (`this`, `startIndex` `count` `this``count` + + 1, Length ()-(`startIndex`)))  + |Remove(`startIndex`, `count`)는 `count`가 0 이상의 정수인 경우에만 지원됩니다.|
|System.String Replace(String `oldValue`, String `newValue`)|Replace(`this`, `oldValue`, `newValue`)||
|System.String Substring(Int32 `startIndex`)|Substring(`this`, `startIndex` +1, Length(`this`) - `startIndex`)||
|System.String Substring(Int32 `startIndex`, Int32 `length`)|Substring(`this`, `startIndex` +1, `length`)||
|System.String ToLower()|ToLower(`this`)||
|System.String ToUpper()|ToUpper(`this`)||
|System.String Trim()|Trim(`this`)||
|System.String TrimEnd(Char[] `trimChars`)|RTrim(`this`)||
|System.String TrimStart(Char[]`trimChars`)|LTrim(`this`)||
|Boolean Equals(String `value`)|= 연산자||

## <a name="systemdatetime-method-static-mapping"></a>System.DateTime 메서드(정적) 매핑

|System.DateTime 메서드(정적)|정식 함수|참고|
|---------------------------------------|------------------------|-----------|
|Boolean Equals(DateTime `t1`, DateTime `t2`)|= 연산자||
|System.DateTime.Now|CurrentDateTime()||
|System.DateTime.UtcNow|CurrentUtcDateTime()||
|Boolean op_Equality(DateTime `d1`, DateTime `d2`)|= 연산자||
|Boolean op_GreaterThan(DateTime `t1`, DateTime `t2`)|> 연산자||
|Boolean op_GreaterThanOrEqual(DateTime `t1`, DateTime `t2`)|> = 연산자||
|Boolean op_Inequality(DateTime `t1`, DateTime `t2`)|!= 연산자||
|부울 op_LessThan (datetime `t1`, datetime `t2`)|< 연산자||
|Boolean op_LessThanOrEqual(DateTime `t1`, DateTime `t2`)|< = 연산자||
|Microsoft.VisualBasic.DateAndTime.DatePart( _<br /><br /> DateInterval `Interval` 로 서의 ByVal\_<br /><br /> `DateValue` DateTime을 DateTime으로\_<br /><br /> 선택적 ByVal `FirstDayOfWeekValue` As FirstDayOfWeek = vbsunday,\_<br /><br /> 선택적 ByVal `FirstWeekOfYearValue` As FirstWeekOfYear = VbFirstJan1\_<br /><br /> ) As Integer||자세한 내용은 DatePart 함수 단원을 참조하세요.|
|Microsoft.VisualBasic.DateAndTime.Now|CurrentDateTime()||
|Microsoft.VisualBasic.DateAndTime.Year(DateTime `TimeValue`)|Year()||
|Microsoft.VisualBasic.DateAndTime.Month(DateTime `TimeValue`)|Month()||
|Microsoft.VisualBasic.DateAndTime.Day(DateTime `TimeValue`)|Day()||
|Microsoft.VisualBasic.DateAndTime.Hour(DateTime `TimeValue`)|Hour()||
|Microsoft.VisualBasic.DateAndTime.Minute(DateTime `TimeValue`)|Minute()||
|Microsoft.VisualBasic.DateAndTime.Second(DateTime `TimeValue`)|Second()||

## <a name="systemdatetime-method-instance-mapping"></a>System.DateTime 메서드(인스턴스) 매핑

|System.DateTime 메서드(인스턴스)|정식 함수|
|-----------------------------------------|------------------------|
|Boolean Equals(DateTime `value`)|= 연산자|
|Day|Day(`this`)|
|Hour|Hour(`this`)|
|Millisecond|Millisecond(`this`)|
|Minute|Minute(`this`)|
|Month|Month(`this`)|
|Second|Second(`this`)|
|Year|Year(`this`)|

## <a name="systemdatetimeoffset-method-instance-mapping"></a>System.DateTimeOffset 메서드(인스턴스) 매핑

나열된 속성의 `get` 메서드에 대한 매핑이 나와 있습니다.

|System.DateTimeOffset 메서드(인스턴스)|정식 함수|참고|
|-----------------------------------------------|------------------------|-----------|
|Day|Day(`this`)|SQL Server 2005에 대해서는 지원되지 않습니다.|
|Hour|Hour(`this`)|SQL Server 2005에 대해서는 지원되지 않습니다.|
|Millisecond|Millisecond(`this`)|SQL Server 2005에 대해서는 지원되지 않습니다.|
|Minute|Minute(`this`)|SQL Server 2005에 대해서는 지원되지 않습니다.|
|Month|Month(`this`)|SQL Server 2005에 대해서는 지원되지 않습니다.|
|Second|Second(`this`)|SQL Server 2005에 대해서는 지원되지 않습니다.|
|Year|Year(`this`)|SQL Server 2005에 대해서는 지원되지 않습니다.|

> [!NOTE]
> <xref:System.DateTimeOffset.Equals%2A> 메서드는 비교된 `true` 개체가 같으면 <xref:System.DateTimeOffset>를 반환하고, 그렇지 않으면 `false`를 반환합니다. <xref:System.DateTimeOffset.CompareTo%2A> 메서드는 비교된 <xref:System.DateTimeOffset> 개체가 같으면 0을 반환하고, 크면 1을 반환하고, 작으면 -1을 반환합니다.

## <a name="systemdatetimeoffset-method-static-mapping"></a>System.DateTimeOffset    (  )

나열된 속성의 `get` 메서드에 대한 매핑이 나와 있습니다.

|System.DateTimeOffset    (  )|정식 함수|참고|
|---------------------------------------------|------------------------|-----------|
|System.DateTimeOffset.Now()|CurrentDateTimeOffset()|SQL Server 2005에 대해서는 지원되지 않습니다.|

## <a name="systemtimespan-method-instance-mapping"></a>System.TimeSpan    (    )

나열된 속성의 `get` 메서드에 대한 매핑이 나와 있습니다.

|System.TimeSpan 메서드(인스턴스)|정식 함수|참고|
|-----------------------------------------|------------------------|-----------|
|시|Hour(`this`)|SQL Server 2005에 대해서는 지원되지 않습니다.|
|밀리초|Millisecond(`this`)|SQL Server 2005에 대해서는 지원되지 않습니다.|
|분|Minute(`this`)|SQL Server 2005에 대해서는 지원되지 않습니다.|
|Seconds|Second(`this`)|SQL Server 2005에 대해서는 지원되지 않습니다.|

> [!NOTE]
> <xref:System.TimeSpan.Equals%2A> 메서드는 비교된 `true` 개체가 같으면 <xref:System.TimeSpan>를 반환하고, 그렇지 않으면 `false`를 반환합니다. <xref:System.TimeSpan.CompareTo%2A> 메서드는 비교된 <xref:System.TimeSpan> 개체가 같으면 0을 반환하고, 크면 1을 반환하고, 작으면 -1을 반환합니다.

### <a name="datepart-function"></a>DatePart 함수

`DatePart` 함수는 `Interval`의 값에 따라 다양한 정식 함수 중 하나에 매핑됩니다. 다음 표에서는 지원되는 `Interval` 값에 대한 정식 함수 매핑을 보여 줍니다.

|간격 값|정식 함수|
|--------------------|------------------------|
|DateInterval.Year|Year()|
|DateInterval.Month|Month()|
|DateInterval.Day|Day()|
|DateInterval.Hour|Hour()|
|DateInterval.Minute|Minute()|
|DateInterval.Second|Second()|

## <a name="mathematical-function-mapping"></a>수치 연산 함수 매핑

|CLR 메서드|정식 함수|
|----------------|------------------------|
|System.Decimal.Ceiling(Decimal `d`)|Ceiling(`d`)|
|System.Decimal.Floor(Decimal `d`)|Floor(`d`)|
|System.Decimal.Round(Decimal `d`)|Round(`d`)|
|System.Math.Ceiling(Decimal `d`)|Ceiling(`d`)|
|System.Math.Floor(Decimal `d`)|Floor(`d`)|
|System.Math.Round(Decimal `d`)|Round(`d`)|
|System.Math.Ceiling(Double `a`)|Ceiling(`a`)|
|System.Math.Floor(Double `a`)|Floor(`a`)|
|System.Math.Round(Double `a`)|Round(`a`)|
|System.Math.Round(Double value, Int16 digits)|Round(value, digits)|
|System.Math.Round(Double value, Int32 digits)|Round(value, digits)|
|System.Math.Round(Decimal value, Int16 digits)|Round(value, digits)|
|System.Math.Round(Decimal value, Int32, digits)|Round(value, digits)|
|System.Math.Abs(Int16 value)|Abs(value)|
|System.Math.Abs(Int32 value)|Abs(value)|
|System.Math.Abs(Int64 value)|Abs(value)|
|System.Math.Abs(Byte value)|Abs(value)|
|System.Math.Abs(Single value)|Abs(value)|
|System.Math.Abs(Double value)|Abs(value)|
|System.Math.Abs(Decimal value)|Abs(value)|
|System.Math.Truncate(Double value, Int16 digits)|Truncate(value, digits)|
|System.Math.Truncate(Double value, Int32 digits)|Truncate(value, digits)|
|System.Math.Truncate(Decimal value, Int16 digits)|Truncate(value, digits)|
|System.Math.Truncate(Decimal value, Int32 digits)|Truncate(value, digits)|
|System.Math.Power(Int32 value, Int64 exponent)|Power(value, exponent)|
|System.Math.Power(Int32 value, Double exponent)|Power(value, exponent)|
|System.Math.Power(Int32 value, Decimal exponent)|Power(value, exponent)|
|System.Math.Power(Int64 value, Int64 exponent)|Power(value, exponent)|
|System.Math.Power(Int64 value, Double exponent)|Power(value, exponent)|
|System.Math.Power(Int64 value, Decimal exponent)|Power(value, exponent)|
|System.Math.Power(Double value, Int64 exponent)|Power(value, exponent)|
|System.Math.Power(Double value, Double exponent)|Power(value, exponent)|
|System.Math.Power(Double value, Decimal exponent)|Power(value, exponent)|
|System.Math.Power(Decimal value, Int64 exponent)|Power(value, exponent)|
|System.Math.Power(Decimal value, Double exponent)|Power(value, exponent)|
|System.Math.Power(Decimal value, Decimal exponent)|Power(value, exponent)|

## <a name="bitwise-operator-mapping"></a>비트 연산자 매핑

|비트 연산자|부울이 아닌 피연산자에 대한 정식 함수|부울 피연산자에 대한 정식 함수|
|----------------------|--------------------------------------------------|---------------------------------------------|
|비트 AND 연산자|BitWiseAnd|op1 AND op2|
|비트 OR 연산자|BitWiseOr|op1 OR op2|
|비트 NOT 연산자|BitWiseNot|NOT(op)|
|비트 XOR 연산자|BitWiseXor|((op1 AND NOT(op2)) OR (NOT(op1) AND op2))|

## <a name="other-mapping"></a>기타 매핑

|메서드|정식 함수|
|------------|------------------------|
|Guid.NewGuid()|NewGuid()|

## <a name="see-also"></a>참고자료

- [LINQ to Entities](linq-to-entities.md)
