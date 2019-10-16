---
title: dateTimeInvalidLocalFormat MDA
ms.date: 03/30/2017
helpviewer_keywords:
- dates [.NET Framework], formatting
- invalid date time local format
- invalid local formats
- MDAs (managed debugging assistants), invalid local formats
- managed debugging assistants (MDAs), invalid local formats
- dateTimeInvalidLocalFormat MDA
- date formatting
- time formatting
- UTC formatting
ms.assetid: c4a942bb-2651-4b65-8718-809f892a0659
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 32217b9e681179c246560ff5b51b65b4f4e044d5
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052881"
---
# <a name="datetimeinvalidlocalformat-mda"></a>dateTimeInvalidLocalFormat MDA
UTC(협정 세계 표준시)로 저장된 <xref:System.DateTime> 인스턴스가 로컬 <xref:System.DateTime> 인스턴스에만 사용해야 하는 형식을 사용하여 형식이 지정되면 `dateTimeInvalidLocalFormat` MDA가 활성화됩니다. 미지정 또는 기본 <xref:System.DateTime> 인스턴스의 경우 이 MDA는 활성화되지 않습니다.  
  
## <a name="symptom"></a>증상  
 애플리케이션이 로컬 형식을 사용하여 수동으로 UTC <xref:System.DateTime> 인스턴스를 직렬화하고 있습니다.  
  
```csharp
DateTime myDateTime = DateTime.UtcNow;  
Serialize(myDateTime.ToString("yyyy-MM-dd'T'HH:mm:ss.fffffffzzz"));  
```  
  
### <a name="cause"></a>원인  
 <xref:System.DateTime.ToString%2A?displayProperty=nameWithType> 메서드에 대한 ‘z’ 형식에는 로컬 표준 시간대 오프셋이 포함됩니다(예: 시드니 시간의 경우 “+10:00”). 이와 같이 <xref:System.DateTime> 값이 로컬인 경우 이 형식은 의미 있는 결과만 생성합니다. 값이 UTC 시간인 경우 <xref:System.DateTime.ToString%2A?displayProperty=nameWithType>에는 로컬 표준 시간대 오프셋이 포함되지만 표준 시간대 지정자를 표시하거나 조정하지 않습니다.  
  
### <a name="resolution"></a>해결  
 UTC <xref:System.DateTime> 인스턴스는 UTC임을 나타내는 방식으로 형식이 지정되어야 합니다. ‘Z’를 사용하여 UTC 시간을 나타내기 위한 권장 형식:  
  
```csharp
DateTime myDateTime = DateTime.UtcNow;  
Serialize(myDateTime.ToString("yyyy-MM-dd'T'HH:mm:ss.fffffffZ"));  
```  
  
 인스턴스가 로컬, UTC 또는 미지정인지 여부에 관계없이 올바르게 직렬화되는 <xref:System.DateTime.Kind%2A> 속성을 사용하여 <xref:System.DateTime>을 직렬화하는 “o” 형식이 있습니다.  
  
```csharp
DateTime myDateTime = DateTime.UtcNow;  
Serialize(myDateTime.ToString("o"));  
```  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 런타임에 영향을 주지 않습니다.  
  
## <a name="output"></a>출력  
 이 MDA 활성화로 인한 특별한 출력은 없습니다. 그러나 호출 스택을 사용하여 MDA를 활성화한 <xref:System.DateTime.ToString%2A> 호출의 위치를 확인할 수 있습니다.  
  
## <a name="configuration"></a>구성하기  
  
```xml  
<mdaConfig>  
  <assistants>  
    <dateTimeInvalidLocalFormat />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>예제  
 다음 방식으로 <xref:System.Xml.XmlConvert> 또는 <xref:System.Data.DataSet>을 사용하여 UTC <xref:System.DateTime> 값을 간접적으로 직렬화하고 있는 애플리케이션을 고려해 보세요.  
  
```csharp
DateTime myDateTime = DateTime.UtcNow;  
String serialized = XMLConvert.ToString(myDateTime);  
```  
  
 <xref:System.Xml.XmlConvert> 및 <xref:System.Data.DataSet> serialization은 기본적으로 serialization에 로컬 형식을 사용합니다. UTC와 같은 다른 종류의 <xref:System.DateTime> 값을 직렬화하려면 추가 옵션이 필요합니다.  
  
 이 특정 예제에서는 `XmlDateTimeSerializationMode.RoundtripKind`를 `XmlConvert`의 `ToString` 호출에 전달합니다. 이렇게 하면 데이터가 UTC 시간으로 직렬화됩니다.  
  
 <xref:System.Data.DataSet>을 사용할 경우 <xref:System.Data.DataColumn>의 <xref:System.Data.DataColumn.DateTimeMode%2A> 속성을 <xref:System.Data.DataSetDateTime.Utc>로 설정합니다.  
  
```csharp
DateTime myDateTime = DateTime.UtcNow;  
String serialized = XmlConvert.ToString(myDateTime,   
    XmlDateTimeSerializationMode.RoundtripKind);  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Globalization.DateTimeFormatInfo>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
