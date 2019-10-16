---
title: '방법: 날짜 및 시간 값 라운드트립'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- round-trip date and time values
- dates [.NET Framework], round-trip values
- time zones [.NET Framework], round-trip date and time values
- time [.NET Framework], round-trip values
- formatting strings [.NET Framework], round-trip values
ms.assetid: b609b277-edc6-4c74-b03e-ea73324ecbdb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: fc3393c27d2955528822c193c36a0f6d86f5c148
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663804"
---
# <a name="how-to-round-trip-date-and-time-values"></a>방법: 날짜 및 시간 값 라운드트립

많은 애플리케이션에서 날짜 및 시간 값은 단일 시점을 명확하게 식별하는 데 사용됩니다. 이 항목에서는 복원된 값이 저장된 값과 같은 시간을 식별할 수 있도록 <xref:System.DateTime> 값, <xref:System.DateTimeOffset> 값 그리고 표준 시간대 정보가 있는 날짜 및 시간 값을 저장하고 복원하는 방법을 보여줍니다.

### <a name="to-round-trip-a-datetime-value"></a>DateTime 값을 라운드트립하려면

1. “o” 형식 지정자와 함께 <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> 메서드를 호출하여 <xref:System.DateTime> 값을 해당 문자열 표현으로 변환합니다.

2. <xref:System.DateTime> 값의 문자열 표현을 파일에 저장하거나 프로세스, 애플리케이션 도메인 또는 컴퓨터 경계를 넘어 전달합니다.

3. <xref:System.DateTime> 값을 나타내는 문자열을 검색합니다.

4. <xref:System.DateTime.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=nameWithType> 메서드를 호출하고 `styles` 매개 변수의 값으로 <xref:System.Globalization.DateTimeStyles.RoundtripKind?displayProperty=nameWithType>를 전달합니다.

다음 예제는 <xref:System.DateTime> 값을 라운드트립하는 방법을 보여줍니다.

[!code-csharp[Formatting.HowTo.RoundTrip#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#1)]
[!code-vb[Formatting.HowTo.RoundTrip#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#1)]

<xref:System.DateTime> 값을 라운드트립할 경우 이 기술은 모든 현지 시간 및 세계시에 대한 시간을 성공적으로 유지합니다. 예를 들어 로컬 <xref:System.DateTime> 값이 미국에 있는 시스템에 저장되는 경우입니다. 태평양 표준 시간대는 미국에 있는 시스템에서 복원됩니다. 중앙 표준 시간대인 복원된 날짜 및 시간은 원래 시간보다 2시간이 늦어지며 이것은 두 표준 시간대 사이의 시간 차이를 반영합니다. 그러나 이 기술은 지정되지 않은 시간에 대해 반드시 정확하지는 않습니다. <xref:System.DateTime.Kind%2A> 속성이 <xref:System.DateTimeKind.Unspecified>인 모든 <xref:System.DateTime> 값은 로컬 시간인 것처럼 취급됩니다. 그러지 않은 경우 <xref:System.DateTime>은 올바른 시점을 성공적으로 식별하지 못합니다. 이 제한에 대한 해결책은 저장 및 복원 작업의 표준 시간대와 날짜 및 시간 값을 밀접하게 연결하는 것입니다.

### <a name="to-round-trip-a-datetimeoffset-value"></a>DateTimeOffset 값을 라운드트립하려면

1. “o” 형식 지정자와 함께 <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=nameWithType> 메서드를 호출하여 <xref:System.DateTimeOffset> 값을 해당 문자열 표현으로 변환합니다.

2. <xref:System.DateTimeOffset> 값의 문자열 표현을 파일에 저장하거나 프로세스, 애플리케이션 도메인 또는 컴퓨터 경계를 넘어 전달합니다.

3. <xref:System.DateTimeOffset> 값을 나타내는 문자열을 검색합니다.

4. <xref:System.DateTimeOffset.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=nameWithType> 메서드를 호출하고 `styles` 매개 변수의 값으로 <xref:System.Globalization.DateTimeStyles.RoundtripKind?displayProperty=nameWithType>를 전달합니다.

다음 예제는 <xref:System.DateTimeOffset> 값을 라운드트립하는 방법을 보여줍니다.

[!code-csharp[Formatting.HowTo.RoundTrip#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#2)]
[!code-vb[Formatting.HowTo.RoundTrip#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#2)]

이 기술은 <xref:System.DateTimeOffset> 값을 항상 단일 시점으로 명확하게 식별합니다. 그런 다음, <xref:System.DateTimeOffset.ToUniversalTime%2A?displayProperty=nameWithType> 메서드를 호출하여 값을 UTC(협정 세계시)로 변환하거나 <xref:System.DateTimeOffset.ToOffset%2A?displayProperty=nameWithType> 또는 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> 메서드를 호출하여 값을 특정 표준 시간대의 시간으로 변환할 수 있습니다. 이 기술의 주요 제한은 특정 표준 시간대의 시간을 나타내는 <xref:System.DateTimeOffset> 값에 대해 날짜 및 시간 연산을 수행하면 해당 표준 시간대에 대해 정확한 결과를 얻을 수 없다는 것입니다. 이는 <xref:System.DateTimeOffset> 값이 인스턴스화될 때 해당 표준 시간대에서 분리되기 때문입니다. 따라서 날짜 및 시간 계산을 수행할 경우에 해당 표준 시간대의 조정 규칙은 더 이상 적용될 수 없습니다. 날짜 및 시간 값과 동반되는 표준 시간대를 포함하는 사용자 지정 형식을 정의하여 이 문제를 해결할 수 있습니다.

### <a name="to-round-trip-a-date-and-time-value-with-its-time-zone"></a>해당 표준 시간대를 사용하여 날짜 및 시간 값을 라운드트립하려면

1. 두 필드가 있는 클래스 또는 구조체를 정의합니다. 첫 번째 필드는 <xref:System.DateTime> 또는 <xref:System.DateTimeOffset> 개체이며, 두 번째 필드는 <xref:System.TimeZoneInfo> 개체입니다. 다음 예제는 이러한 형식의 단순 버전입니다.

    [!code-csharp[Formatting.HowTo.RoundTrip#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#3)]
    [!code-vb[Formatting.HowTo.RoundTrip#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#3)]

2. <xref:System.SerializableAttribute> 특성을 사용하여 클래스를 표시합니다.

3. <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=nameWithType> 메서드를 사용하여 개체를 직렬화합니다.

4. <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A> 메서드를 사용하여 개체를 복원합니다.

5. deserialize된 개체를 적절한 형식의 개체로 캐스트(C#에서)하거나 변환(Visual Basic에서)합니다.

다음 예제는 날짜 및 시간과 표준 시간대 정보를 모두 저장하는 개체를 라운드트립하는 방법을 보여줍니다.

[!code-csharp[Formatting.HowTo.RoundTrip#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#4)]
[!code-vb[Formatting.HowTo.RoundTrip#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#4)]

날짜 및 시간과 표준 시간대 개체 결합의 구현으로 인해 날짜 값이 표준 시간대 값과 동기화되지 않게 된 경우 이 기술은 저장 및 복원 이전과 이후에 모두 올바른 시점을 항상 명확하게 반영해야 합니다.

## <a name="compiling-the-code"></a>코드 컴파일

이러한 예제에는 다음이 필요합니다.

- C# `using` 문 또는 Visual Basic `Imports` 문을 사용하여 다음 네임스페이스를 가져와야 합니다.

  - <xref:System>(C#만 해당).

  - <xref:System.Globalization?displayProperty=nameWithType>.

  - <xref:System.IO?displayProperty=nameWithType>.

  - <xref:System.Runtime.Serialization?displayProperty=nameWithType>.

  - <xref:System.Runtime.Serialization.Formatters.Binary?displayProperty=nameWithType>.

- `DateInTimeZone` 클래스 이외의 각 코드 예제가 클래스 또는 Visual Basic 모듈에 포함되어야 하며, 메서드에 래핑되고, `Main` 메서드에서 호출되어야 합니다.

## <a name="see-also"></a>참고 항목

- [서식 지정 작업 수행](../../../docs/standard/base-types/performing-formatting-operations.md)
- [DateTime, DateTimeOffset, TimeSpan 및 TimeZoneInfo 중 선택](../../../docs/standard/datetime/choosing-between-datetime.md)
- [표준 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)
