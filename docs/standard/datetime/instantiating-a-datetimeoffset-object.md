---
title: DateTimeOffset 개체 인스턴스화
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- instantiating time zone objects
- time zone objects [.NET Framework], instantiation
- DateTimeOffset structure, converting to DateTime
- DateTimeOffset structure, instantiating
ms.assetid: 9648375f-d368-4373-a976-3332ece00c0a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 50cc71b62581e1fb9302fe241abf6349afd33f8d
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106637"
---
# <a name="instantiating-a-datetimeoffset-object"></a>DateTimeOffset 개체 인스턴스화

<xref:System.DateTimeOffset> 구조체는 새 <xref:System.DateTimeOffset> 값을 만들 수 있는 여러 가지 방법을 제공합니다. 이 중 상당수는 새 <xref:System.DateTime> 값을 인스턴스화하는 데 사용할 수 있는 메서드에 직접 해당 하며, utc (협정 세계시)를 기준으로 날짜 및 시간 값의 오프셋을 지정할 수 있도록 향상 된 기능을 제공 합니다. 특히 다음과 같은 방법으로 값을 <xref:System.DateTimeOffset> 인스턴스화할 수 있습니다.

- 날짜 및 시간 리터럴을 사용 합니다.

- 생성자를 <xref:System.DateTimeOffset> 호출 합니다.

- 값을 암시적으로 값으로 <xref:System.DateTimeOffset> 변환 합니다.

- 날짜 및 시간의 문자열 표현 구문 분석

이 항목에서는 새 <xref:System.DateTimeOffset> 값을 인스턴스화하는 이러한 메서드를 설명 하는 코드 예제 및 자세한 정보를 제공 합니다.

## <a name="date-and-time-literals"></a>날짜 및 시간 리터럴

이를 지 원하는 언어의 경우 값을 <xref:System.DateTime> 인스턴스화하는 가장 일반적인 방법 중 하나는 날짜와 시간을 하드 코딩 된 리터럴 값으로 제공 하는 것입니다. 예를 들어 다음 Visual Basic 코드는 오전 10:00 <xref:System.DateTime> 에 2008 년 1 월 1 일에 해당 하는 값을 가진 개체를 만듭니다.

[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#1)]

<xref:System.DateTimeOffset>리터럴을 지 원하는 <xref:System.DateTime> 언어를 사용 하는 경우 날짜 및 시간 리터럴을 사용 하 여 값을 초기화할 수도 있습니다. 예를 들어 다음 Visual Basic 코드는 개체를 <xref:System.DateTimeOffset> 만듭니다.

[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#2)]

콘솔 출력에서 볼 <xref:System.DateTimeOffset> 수 있듯이 이러한 방식으로 생성 된 값에는 현지 표준 시간대의 오프셋이 할당 됩니다. 즉, 다른 컴퓨터에서 코드를 실행 하는 경우 문자 리터럴을 사용 하 여 할당 된 값은단일시점을식별하지않습니다.<xref:System.DateTimeOffset>

## <a name="datetimeoffset-constructors"></a>DateTimeOffset 생성자

<xref:System.DateTimeOffset> 형식은 6 개의 생성자를 정의 합니다. 이들 중 4 개는 UTC <xref:System.DateTime> 에서 날짜 및 시간의 오프셋을 정의 하 <xref:System.TimeSpan> 는 형식의 추가 매개 변수를 사용 하 여 생성자에 직접 해당 합니다. 이를 통해 개별 날짜 및 <xref:System.DateTimeOffset> 시간 구성 요소의 값을 기준으로 값을 정의할 수 있습니다. 예를 들어 다음 코드에서는 이러한 4 개의 생성자를 사용 <xref:System.DateTimeOffset> 하 여 값이 7/1/2008 12:05 AM + 01:00 인 개체를 인스턴스화합니다.

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#3)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#3)]

개체를 <xref:System.DateTimeOffset> <xref:System.Globalization.PersianCalendar> 생성자에 대 한 인수 중 하나로 사용 하 여 인스턴스화된 개체의 값이 콘솔에 표시 되는 경우이 개체의 값은 페르시아 력이 아닌 양력에서 날짜로 표시 됩니다. 이란어 달력을 사용 하 여 날짜를 출력 하려면 <xref:System.Globalization.PersianCalendar> 항목의 예제를 참조 하세요.

다른 두 생성자는 <xref:System.DateTimeOffset> <xref:System.DateTime> 값에서 개체를 만듭니다. 그 중 첫 번째 매개 변수는 <xref:System.DateTime> <xref:System.DateTimeOffset> 값으로 변환할 단일 매개 변수입니다. 결과 <xref:System.DateTimeOffset> 값의 오프셋은 생성자의 단일 매개 <xref:System.DateTime.Kind%2A> 변수 속성에 따라 달라 집니다. 값이 <xref:System.DateTimeKind.Utc?displayProperty=nameWithType>이면 오프셋이와 동일 하 게 <xref:System.TimeSpan.Zero?displayProperty=nameWithType>설정 됩니다. 그렇지 않은 경우 해당 오프셋은 현지 표준 시간대의 값으로 설정됩니다. 다음 예제에서는이 생성자를 사용 하 여 UTC 및 <xref:System.DateTimeOffset> 현지 표준 시간대를 나타내는 개체를 인스턴스화하는 방법을 보여 줍니다.

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#4)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#4)]

> [!NOTE]
> 단일 <xref:System.DateTimeOffset> <xref:System.DateTime> <xref:System.DateTimeOffset> 매개 변수가 있는 생성자의 오버 로드를 호출 하는 것은 값을 값으로 암시적으로 변환 하는 것과 같습니다. <xref:System.DateTime>

값에서 개체를 <xref:System.DateTimeOffset> 만드는 두 번째 생성자에는 두 개의 매개 변수 ( <xref:System.DateTime> 변환할 값)와 <xref:System.TimeSpan> UTC에서의 날짜 및 시간 오프셋을 나타내는 값이 있습니다. <xref:System.DateTime> 이 오프셋 값은 생성자의 첫 <xref:System.DateTime.Kind%2A> 번째 매개 변수의 속성과 일치 해야 합니다. <xref:System.ArgumentException> 그렇지 않으면이 throw 됩니다. 첫 번째 매개 변수의 <xref:System.DateTimeKind.Utc?displayProperty=nameWithType> <xref:System.TimeSpan.Zero?displayProperty=nameWithType>속성이 인 경우 두 번째 매개 변수 값은 이어야 합니다. <xref:System.DateTime.Kind%2A> 첫 번째 매개 변수의 <xref:System.DateTimeKind.Local?displayProperty=nameWithType> 속성이인경우두번째매개변수값은로컬시스템표준시간대의오프셋이어야합니다.<xref:System.DateTime.Kind%2A> 첫 번째 매개 변수의 <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType> 속성이인경우오프셋은모든유효한값일수있습니다.<xref:System.DateTime.Kind%2A> 다음 코드에서는이 생성자를 호출 하 여 <xref:System.DateTime> <xref:System.DateTimeOffset> 값으로 변환 하는 방법을 보여 줍니다.

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#5)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#5)]

## <a name="implicit-type-conversion"></a>암시적 형식 변환

형식은 값에서 값<xref:System.DateTimeOffset> 으로의 암시적 형식 변환을 하나 지원 합니다. <xref:System.DateTime> <xref:System.DateTimeOffset> 암시적 형식 변환은 명시적 캐스팅(C#의 경우) 또는 변환(Visual Basic의 경우)을 필요로 하지 않고 정보를 손실하지 않는 형식 간의 변환입니다. 이를 사용하면 다음과 같은 코드를 사용할 수 있습니다.

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#6)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#6)]

결과 <xref:System.DateTimeOffset> 값의 오프셋은 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 속성 값에 따라 다릅니다. 값이 <xref:System.DateTimeKind.Utc?displayProperty=nameWithType>이면 오프셋이와 동일 하 게 <xref:System.TimeSpan.Zero?displayProperty=nameWithType>설정 됩니다. 값이 <xref:System.DateTimeKind.Local?displayProperty=nameWithType> 또는 <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType>인 경우 오프셋은 현지 표준 시간대의 값과 동일 하 게 설정 됩니다.

## <a name="parsing-the-string-representation-of-a-date-and-time"></a>날짜 및 시간의 문자열 표현 구문 분석

형식은 날짜 및 시간의 <xref:System.DateTimeOffset> 문자열 표현을 값으로 변환 하는 데 사용할 수 있는 네 가지 메서드를 지원 합니다. <xref:System.DateTimeOffset>

- <xref:System.DateTimeOffset.Parse%2A>는 날짜 및 시간의 문자열 표현을 <xref:System.DateTimeOffset> 값으로 변환 하려고 시도 하 고 변환이 실패 하는 경우 예외를 throw 합니다.

- <xref:System.DateTimeOffset.TryParse%2A>는 날짜 및 시간의 문자열 표현을 <xref:System.DateTimeOffset> 값으로 변환 하려고 시도 하 고 변환이 실패 하는 경우를 반환 `false` 합니다.

- <xref:System.DateTimeOffset.ParseExact%2A>는 지정 된 형식의 <xref:System.DateTimeOffset> 날짜 및 시간에 대 한 문자열 표현을 값으로 변환 하려고 합니다. 변환이 실패하면 메서드는 예외를 throw합니다.

- <xref:System.DateTimeOffset.TryParseExact%2A>는 지정 된 형식의 <xref:System.DateTimeOffset> 날짜 및 시간에 대 한 문자열 표현을 값으로 변환 하려고 합니다. 변환에 실패하는 경우 메서드가 `false`을 반환합니다.

다음 예제에서는 <xref:System.DateTimeOffset> 값을 인스턴스화하기 위해 이러한 4 개의 문자열 변환 메서드 각각에 대 한 호출을 보여 줍니다.

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#7)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#7)]

## <a name="see-also"></a>참고자료

- [날짜, 시간 및 표준 시간대](../../../docs/standard/datetime/index.md)
