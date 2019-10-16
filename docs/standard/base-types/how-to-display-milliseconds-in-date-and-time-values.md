---
title: '방법: 날짜 및 시간 값의 밀리초 표시'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DateTime.ToString method
- displaying date and time data
- time [.NET Framework], milliseconds
- dates [.NET Framework], milliseconds
- milliseconds [.NET Framework]
ms.assetid: ae1a0610-90b9-4877-8eb6-4e30bc5e00cf
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 135459f84cee0a3c356882b193ff561befb43145
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963370"
---
# <a name="how-to-display-milliseconds-in-date-and-time-values"></a>방법: 날짜 및 시간 값의 밀리초 표시
<xref:System.DateTime.ToString?displayProperty=nameWithType>과 같은 기본 날짜 및 시간 서식 지정 메서드에는 시간 값의 시, 분, 초가 포함되지만 밀리초 구성 요소는 제외됩니다. 이 항목에서는 형식이 지정된 날짜 및 시간 문자열에 날짜 및 시간의 밀리초 구성 요소를 포함하는 방법을 보여 줍니다.  
  
### <a name="to-display-the-millisecond-component-of-a-datetime-value"></a>DateTime 값의 밀리초 구성 요소를 표시하려면  
  
1. 날짜의 문자열 표현에 대한 작업을 하는 경우에는 정적 <xref:System.DateTime> 또는 <xref:System.DateTimeOffset> 메서드를 사용하여 해당 표현을 <xref:System.DateTime.Parse%28System.String%29?displayProperty=nameWithType> 또는 <xref:System.DateTimeOffset.Parse%28System.String%29?displayProperty=nameWithType> 값으로 변환합니다.  
  
2. 시간 밀리초 구성 요소의 문자열 표현을 추출하려면 날짜 및 시간 값의 <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> 또는 <xref:System.DateTimeOffset.ToString%2A> 메서드를 호출하고 `fff` 또는 `FFF` 사용자 지정 형식 패턴을 단독으로 또는 다른 사용자 지정 형식 지정자와 함께 `format` 매개 변수로 전달합니다.  
  
## <a name="example"></a>예  
 이 예제에서는 <xref:System.DateTime> 및 <xref:System.DateTimeOffset> 값의 밀리초 구성 요소를 단독으로 그리고 긴 날짜 및 시간 문자열에 포함하여 콘솔에 표시합니다.  
  
 [!code-csharp[Formatting.HowTo.Millisecond#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Millisecond/cs/Millisecond.cs#1)]
 [!code-vb[Formatting.HowTo.Millisecond#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Millisecond/vb/Millisecond.vb#1)]  
  
 `fff` 형식 패턴에서는 밀리초 값의 뒤에 0이 포함됩니다. `FFF` 형식 패턴에서는 표시되지 않습니다. 다음 예제에서 차이점을 보여 줍니다.  
  
 [!code-csharp[Formatting.HowTo.Millisecond#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Millisecond/cs/Millisecond.cs#2)]
 [!code-vb[Formatting.HowTo.Millisecond#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Millisecond/vb/Millisecond.vb#2)]  
  
 날짜 및 시간의 밀리초 구성 요소를 포함하는 전체 사용자 지정 형식 지정자를 정의할 때 발생하는 문제는 애플리케이션의 현재 문화권에서 사용되는 시간 요소의 정렬과 일치하지 않는 하드 코드된 형식이 정의될 수 있다는 것입니다. 더 나은 방법은 현재 문화권의 <xref:System.Globalization.DateTimeFormatInfo> 개체로 정의된 날짜 및 시간 표시 패턴 중 하나를 검색한 후 밀리초를 포함하도록 수정하는 것입니다. 이 방법도 예제에서 보여 줍니다. <xref:System.Globalization.DateTimeFormatInfo.FullDateTimePattern%2A?displayProperty=nameWithType> 속성에서 현재 문화권의 전체 날짜 및 시간 패턴을 검색한 후 해당 초 패턴 뒤에 사용자 지정 패턴 `.ffff`를 삽입합니다. 예제에서는 정규식을 사용하여 이 작업을 단일 메서드 호출에서 수행합니다.  
  
 사용자 지정 형식 지정자를 사용하여 밀리초가 아닌 초의 소수 자릿수를 표시할 수도 있습니다. 예를 들어 `f` 또는 `F` 사용자 지정 형식 지정자는 1/10초, `ff` 또는 `FF` 사용자 지정 형식 지정자는 1/100초, `ffff` 또는 `FFFF` 사용자 지정 형식 지정자는 1/10000초를 표시합니다. 반환된 문자열에서 밀리초의 소수 자릿수가 반올림되지 않고 잘립니다. 이 형식 지정자는 다음 예제에서 사용됩니다.  
  
 [!code-csharp[Formatting.HowTo.Millisecond#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Millisecond/cs/Millisecond.cs#3)]
 [!code-vb[Formatting.HowTo.Millisecond#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Millisecond/vb/Millisecond.vb#3)]  
  
> [!NOTE]
> 1/10000초, 1/100000초 등 1초의 매우 작은 소수 단위를 표시할 수 있습니다. 그러나 이러한 값은 의미가 없을 수 있습니다. 날짜 및 시간 값의 자릿수는 시스템 시계의 정밀도에 따라 달라집니다. Windows NT 3.5 이상 버전과 [!INCLUDE[windowsver](../../../includes/windowsver-md.md)] 운영 체제의 경우 시계의 정밀도는 약 10-15밀리초입니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Globalization.DateTimeFormatInfo>
- [사용자 지정 날짜 및 시간 형식 문자열](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)
