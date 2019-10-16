---
title: 문자열을 .NET Framework 데이터 형식으로 변환
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 65455ef3-9120-412c-819b-d0f59f88ac09
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 31f277d11cba8191c326d56f017b8acc6503c6b7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968719"
---
# <a name="converting-strings-to-net-framework-data-types"></a>문자열을 .NET Framework 데이터 형식으로 변환
문자열을 .NET Framework 데이터 형식으로 변환하려면 애플리케이션 요구 사항에 적합한 **XmlConvert** 메서드를 사용합니다. **XmlConvert** 클래스에서 사용 가능한 변환 메서드의 전체 목록은 <xref:System.Xml.XmlConvert>를 참조하세요.  
  
 **ToString** 메서드에서 반환된 문자열은 전달된 데이터를 문자열 버전으로 표시한 것입니다. 또한 일부 .NET Framework 형식에서는 **XmlConvert** 클래스를 사용하여 변환을 수행하지만, 이러한 형식은 **System.Convert** 클래스에 있는 메서드를 사용하지 않습니다. **XmlConvert** 클래스는 XSD(XML 스키마) 데이터 형식 사양을 준수하며, **XmlConvert**가 매핑할 수 있는 데이터 형식을 갖습니다.  
  
 다음 표에서는 XSD(XML 스키마) 데이터 형식 매핑을 사용할 때 반환되는 .NET Framework 데이터 형식 및 문자열 형식의 목록을 보여 줍니다. 이러한 .NET Framework 형식은 **System.Convert**에 의해 처리될 수 없습니다.  
  
|.NET Framework 형식|반환 문자열|  
|-------------------------|---------------------|  
|부울|"true", "false"|  
|Single.PositiveInfinity|"INF"|  
|Single.NegativeInfinity|"-INF"|  
|Double.PositiveInfinity|"INF"|  
|Double.NegativeInfinity|"-INF"|  
|DateTime|형식은 "yyyy-MM-ddTHH:mm:sszzzzzz" 및 해당 하위 집합입니다.|  
|Timespan|형식은 PnYnMnTnHnMnS입니다. 즉, `P2Y10M15DT10H30M20S`는 2년 10개월 15일 10시간 30분 20초의 지속 시간을 나타냅니다.|  
  
> [!NOTE]
> **ToString** 메서드를 사용하여 이 테이블에 나열된 특정 .NET Framework 형식을 변환하는 경우, 반환되는 문자열의 형식은 기본 형식이 아니라 XSD(XML 스키마) 문자열 형식입니다.  
  
 **DateTime** 및 **Timespan**의 값 형식은 다릅니다. 즉, **DateTime**은 순간적인 시각을 나타내며 **TimeSpan**은 시간 간격을 나타냅니다. **DateTime** 및 **Timespan** 형식은 XSD(XML 스키마) 데이터 형식 사양에 지정되어 있습니다. 예:  
  
```vb  
Dim writer As New XmlTextWriter("myfile.xml", Nothing)  
Dim [date] As New DateTime(2001, 8, 4)  
writer.WriteElementString("Date", XmlConvert.ToString([date]))  
```  
  
```csharp  
XmlTextWriter writer = new XmlTextWriter("myfile.xml", null);  
DateTime date = new DateTime (2001, 08, 04);  
writer.WriteElementString("Date", XmlConvert.ToString(date));  
```  
  
 **출력**  
  
 `<Date>2001-08-04T00:00:00</Date>`.  
  
 다음 코드는 정수를 문자열로 변환합니다.  
  
```vb  
Dim writer As New XmlTextWriter("myfile.xml", Nothing)  
Dim value As Int32 = 200  
writer.WriteElementString("Number", XmlConvert.ToString(value))  
```  
  
```csharp  
XmlTextWriter writer = new XmlTextWriter("myfile.xml", null);  
Int32 value = 200;  
writer.WriteElementString("Number", XmlConvert.ToString(value));  
```  
  
 **출력**  
  
 `<Number>200</Number>`  
  
 하지만 문자열을 **Boolean**, **Single** 또는 **Double**로 변환하는 경우 반환되는 .NET Framework 형식은 **System.Convert** 클래스를 사용하는 경우의 반환 형식과는 다릅니다.  
  
## <a name="string-to-boolean"></a>문자열을 Boolean 형식으로 변환  
 다음 표에서는 **ToBoolean** 메서드를 사용하여 문자열을 **Boolean**으로 변환하는 경우 지정된 입력 문자열에 대해 생성되는 형식을 보여줍니다.  
  
|유효한 문자열 입력 매개 변수|.NET Framework 출력 형식|  
|----------------------------------|--------------------------------|  
|"true"|Boolean.True|  
|"1"|Boolean.True|  
|"false"|Boolean.False|  
|"0"|Boolean.False|  
  
 예를 들어, 다음과 같이 XML을 가정합니다.  
  
 **입력**  
  
```xml  
<Boolean>true</Boolean>  
<Boolean>1</Boolean>   
```  
  
 두 가지 모두 다음 코드에 의해 파악되며, **bvalue**는 **System.Boolean.True**입니다.  
  
```vb  
Dim bvalue As Boolean = _  
   XmlConvert.ToBoolean(reader.ReadElementString())  
Console.WriteLine(bvalue)  
```  
  
```csharp  
Boolean bvalue = XmlConvert.ToBoolean(reader.ReadElementString());  
Console.WriteLine(bvalue);  
```  
  
## <a name="string-to-single"></a>문자열을 Single 형식으로 변환  
 다음 표에서는 **ToSingle** 메서드를 사용하여 문자열을 **Single**로 변환하는 경우 지정된 입력 문자열에 대해 생성되는 형식을 보여줍니다.  
  
|유효한 문자열 입력 매개 변수|.NET Framework 출력 형식|  
|----------------------------------|--------------------------------|  
|"INF"|Single.PositiveInfinity|  
|"-INF"|Single.NegativeInfinity|  
  
## <a name="string-to-double"></a>문자열을 Double 형식으로 변환  
 다음 표에서는 **ToDouble** 메서드를 사용하여 문자열을 **Single**로 변환하는 경우 지정된 입력 문자열에 대해 생성되는 형식을 보여줍니다.  
  
|유효한 문자열 입력 매개 변수|.NET Framework 출력 형식|  
|----------------------------------|--------------------------------|  
|"INF"|Double.PositiveInfinity|  
|"-INF"|Double.NegativeInfinity|  
  
 다음 코드는 `<Infinity>INF</Infinity>`를 작성합니다.  
  
```vb  
Dim value As Double = Double.PositiveInfinity  
writer.WriteElementString("Infinity", XmlConvert.ToString(value))  
```  
  
```csharp  
Double value = Double.PositiveInfinity;  
writer.WriteElementString("Infinity", XmlConvert.ToString(value));  
```  
  
## <a name="see-also"></a>참고 항목

- [XML 데이터 형식 변환](../../../../docs/standard/data/xml/conversion-of-xml-data-types.md)
- [.NET Framework 형식을 문자열로 변환](../../../../docs/standard/data/xml/converting-dotnet-types-to-strings.md)
