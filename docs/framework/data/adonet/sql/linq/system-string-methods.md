---
title: System.String 메서드
ms.date: 03/30/2017
ms.assetid: ce307f14-87e6-4816-8694-8a4147f6b784
ms.openlocfilehash: 583c0d58562c1605f24b61489d481e19248ebed4
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792499"
---
# <a name="systemstring-methods"></a>System.String 메서드
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 다음 <xref:System.String> 메서드를 지원하지 않습니다.  
  
## <a name="unsupported-systemstring-methods-in-general"></a>일반적으로 지원되지 않는 System.String 메서드  
 일반적으로 지원되지 않는 <xref:System.String> 메서드입니다.  
  
- 문화권 인식 오버 로드 `CultureInfo`(를  /  `StringComparison`  / 사용 하는메서드)`IFormatProvider`  
  
- `char` 배열을 사용하거나 생성하는 메서드입니다.  
  
## <a name="unsupported-systemstring-static-methods"></a>지원되지 않는 System.String 정적 메서드  
  
|지원되지 않는 System.String 정적 메서드|  
|----------------------------------------------|  
|<xref:System.String.Copy%28System.String%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.Boolean%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%29?displayProperty=nameWithType>|  
|<xref:System.String.Compare%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType>|  
|<xref:System.String.CompareOrdinal%28System.String%2CSystem.String%29?displayProperty=nameWithType>|  
|<xref:System.String.CompareOrdinal%28System.String%2CSystem.Int32%2CSystem.String%2CSystem.Int32%2CSystem.Int32%29?displayProperty=nameWithType>|  
|<xref:System.String.Format%2A?displayProperty=nameWithType>|  
|<xref:System.String.Join%2A?displayProperty=nameWithType>|  
  
## <a name="unsupported-systemstring-non-static-methods"></a>지원되지 않는 System.String 비정적 메서드  
  
|지원되지 않는 System.String 비정적 메서드|  
|---------------------------------------------------|  
|<xref:System.String.IndexOfAny%28System.Char%5B%5D%29?displayProperty=nameWithType>|  
|<xref:System.String.Split%2A?displayProperty=nameWithType>|  
|<xref:System.String.ToCharArray?displayProperty=nameWithType>|  
|<xref:System.String.ToUpper%28System.Globalization.CultureInfo%29?displayProperty=nameWithType>|  
|<xref:System.String.TrimEnd%28System.Char%5B%5D%29?displayProperty=nameWithType>|  
|<xref:System.String.TrimStart%28System.Char%5B%5D%29?displayProperty=nameWithType>|  
  
## <a name="differences-from-net"></a>.NET과의 차이점  
  
- 쿼리에서는 서버에 적용되는 SQL Server 데이터 정렬에 대해 설명하지 않으므로 기본적으로 문화권 구분 및 대/소문자를 구분하지 않는 비교를 제공합니다. 이 동작은 .NET Framework의 대/소문자를 구분하는 의미와 기본적으로 다릅니다.  
  
- 가 `LastIndexOf` 0을 반환 하는 경우 문자열 `NULL` 은 이거나 찾은 위치가 0입니다.  
  
- 연결 또는 고정 길이 문자열인 `CHAR`, `NCHAR`로부터 예기치 않은 결과가 반환될 수 있습니다. 왜냐하면 이러한 형식은 데이터베이스에서 안쪽 여백이 자동으로 적용되기 때문입니다.  
  
- `Replace`, `ToLower`, `ToUpper`와 같은 여러 가지 메서드와 문자 인덱서는 `TEXT` 또는 `NTEXT` 열과 XML에 대한 유효한 변환을 갖지 않으므로 정상적으로 변환되는 경우에 `SqlExceptions`가 발생합니다. 이러한 동작은 이 형식을 허용하는 것으로 간주됩니다. 그러나 모든 문자열 작업은 `VARCHAR`, `NVARCHAR`, `VARCHAR(max)` 및 `NVARCHAR(max)`에 대한 CLR(공용 언어 런타임) 의미와 일치해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [데이터 형식 및 함수](data-types-and-functions.md)
