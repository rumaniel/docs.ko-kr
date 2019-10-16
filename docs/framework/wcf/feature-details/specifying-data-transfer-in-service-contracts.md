---
title: 서비스 계약에서 데이터 전송 지정
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- service contracts [WCF], data transfer
ms.assetid: 7c5a26c8-89c9-4bcb-a4bc-7131e6d01f0c
ms.openlocfilehash: 47544cf74b4fa09fd8ee868ea940ef24a453840e
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834642"
---
# <a name="specifying-data-transfer-in-service-contracts"></a>서비스 계약에서 데이터 전송 지정
WCF (Windows Communication Foundation)는 메시징 인프라로 간주할 수 있습니다. 서비스 작업에서는 메시지를 받고 처리한 다음 보낼 수 있습니다. 메시지는 작업 계약을 사용하여 설명됩니다. 다음 계약을 예로 들 수 있습니다.  
  
```csharp  
[ServiceContract]  
public interface IAirfareQuoteService  
{  
    [OperationContract]  
    float GetAirfare(string fromCity, string toCity);  
}  
```  
  
```vb  
<ServiceContract()>  
Public Interface IAirfareQuoteService  
  
    <OperationContract()>  
    Function GetAirfare(fromCity As String, toCity As String) As Double  
End Interface  
```  
  
 여기서 `GetAirfare` 작업은 `fromCity` 및 `toCity`에 대한 정보가 있는 메시지를 수락한 다음 숫자가 포함된 메시지를 반환합니다.  
  
 이 항목에서는 작업 계약에서 메시지를 설명할 수 있는 여러 가지 방법에 대해 설명합니다.  
  
## <a name="describing-messages-by-using-parameters"></a>매개 변수를 사용하여 메시지 설명  
 메시지를 설명하는 가장 간단한 방법은 매개 변수 목록과 반환 값을 사용하는 것입니다. 앞의 예제에서 `fromCity` 및 `toCity` 문자열 매개 변수는 요청 메시지를 설명하는 데 사용되었고 float 반환 값은 회신 메시지를 설명하는 데 사용되었습니다. 반환 값으로만 회신 메시지를 설명할 수 없는 경우에는 out 매개 변수를 사용할 수도 있습니다. 예를 들어, 다음 연산의 경우 요청 메시지에는 `fromCity` 및 `toCity`가 있으며 회신 메시지에는 통화와 숫자가 함께 있습니다.  
  
```csharp  
[OperationContract]  
float GetAirfare(string fromCity, string toCity, out string currency);  
```  
  
```vb  
<OperationContract()>  
    Function GetAirfare(fromCity As String, toCity As String) As Double  
```  
  
 또한 참조 매개 변수를 사용하여 요청 및 회신 메시지의 매개 변수 부분을 만들 수 있습니다. 매개 변수는 serialize할 수 있는, 즉 XML로 변환할 수 있는 형식이어야 합니다. 기본적으로 WCF는 <xref:System.Runtime.Serialization.DataContractSerializer> 클래스 라는 구성 요소를 사용 하 여이 변환을 수행 합니다. `int`, `string`, `float` 및 `DateTime`과 같은 가장 기본적인 형식이 지원됩니다. 사용자 정의 형식에는 일반적으로 데이터 계약이 있어야 합니다. 자세한 내용은 [데이터 계약 사용](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)을 참조 하세요.  
  
```csharp
public interface IAirfareQuoteService  
{  
    [OperationContract]  
    float GetAirfare(Itinerary itinerary, DateTime date);  
  
    [DataContract]  
    public class Itinerary  
    {  
        [DataMember]  
        public string fromCity;  
        [DataMember]  
        public string toCity;  
   }  
}  
```  
  
```vb  
Public Interface IAirfareQuoteService  
    <OperationContract()>  
    GetAirfare(itinerary as Itinerary, date as DateTime) as Double  
  
    <DataContract()>  
    Class Itinerary  
  
        <DataMember()>  
        Public fromCity As String  
        <DataMember()>  
        Public toCity As String  
    End Class  
End Interface  
```  
  
 `DataContractSerializer`는 사용자의 형식을 serialize하기에 적합하지 않은 경우도 있습니다. WCF는 매개 변수를 serialize 하는 데 사용할 수 있는 <xref:System.Xml.Serialization.XmlSerializer> 인 대체 serialization 엔진을 지원 합니다. <xref:System.Xml.Serialization.XmlSerializer>를 통해 `XmlAttributeAttribute`와 같은 특성을 사용하여 결과 XML을 보다 효과적으로 제어할 수 있습니다. 특정 연산이나 전체 서비스에 <xref:System.Xml.Serialization.XmlSerializer>를 사용하려면 <xref:System.ServiceModel.XmlSerializerFormatAttribute> 특성을 연산이나 서비스에 적용합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  
  
```csharp  
[ServiceContract]  
public interface IAirfareQuoteService  
{  
    [OperationContract]  
    [XmlSerializerFormat]  
    float GetAirfare(Itinerary itinerary, DateTime date);  
}  
public class Itinerary  
{  
    public string fromCity;  
    public string toCity;  
    [XmlAttribute]  
    public bool isFirstClass;  
}  
```  
  
```vb  
<ServiceContract()>  
Public Interface IAirfareQuoteService  
    <OperationContract()>  
    <XmlSerializerFormat>  
    GetAirfare(itinerary as Itinerary, date as DateTime) as Double  
  
End Interface  
  
Class Itinerary  
  
    Public fromCity As String  
    Public toCity As String  
    <XmlSerializerFormat()>  
    Public isFirstClass As Boolean  
End Class  
```  
  
 자세한 내용은 [XmlSerializer 클래스 사용](../../../../docs/framework/wcf/feature-details/using-the-xmlserializer-class.md)을 참조 하세요. 위 항목에 설명된 대로 수동으로 <xref:System.Xml.Serialization.XmlSerializer>로 전환할 특별한 이유가 없는 한 이 예제에서처럼 수동으로 전환하지 않는 것이 좋습니다.  
  
 .NET 매개 변수 이름을 계약 이름으로부터 격리시키려면 <xref:System.ServiceModel.MessageParameterAttribute> 특성을 사용하고, `Name` 속성을 사용하여 계약 이름을 설정합니다. 예를 들면, 다음 작업 계약은 이 항목의 첫 번째 예제에 해당합니다.  
  
```csharp  
[OperationContract]  
public float GetAirfare(  
    [MessageParameter(Name="fromCity")] string originCity,  
    [MessageParameter(Name="toCity")] string destinationCity);  
```  
  
```vb  
<OperationContract()>  
  Function GetAirfare(<MessageParameter(Name := "fromCity")> fromCity As String, <MessageParameter(Name := "toCity")> toCity As String) As Double  
```  
  
## <a name="describing-empty-messages"></a>빈 메시지 설명  
 빈 요청 메시지는 입력 매개 변수나 참조 매개 변수를 사용하지 않고 설명할 수 있습니다. 예를 들어 C#의 경우:  
  
 `[OperationContract]`  
  
 `public int GetCurrentTemperature();`  
  
 예를 들어 VB의 경우:  
  
 `<OperationContract()>`  
  
 `Function GetCurrentTemperature() as Integer`  
  
 빈 회신 메시지는 출력 또는 참조 매개 변수 없이 `void` 반환 형식을 사용하여 설명할 수 있습니다. 예:  
  
```csharp  
[OperationContract]  
public void SetTemperature(int temperature);  
```  
  
```vb  
<OperationContract()>  
Sub SetTemperature(temperature As Integer)  
```  
  
 이것은 다음과 같은 단방향 연산과는 다릅니다.  
  
```csharp  
[OperationContract(IsOneWay=true)]  
public void SetLightbulbStatus(bool isOn);  
```  
  
```vb  
<OperationContract(IsOneWay:=True)>  
Sub SetLightbulbStatus(isOne As Boolean)  
```  
  
 `SetTemperatureStatus` 연산은 빈 메시지를 반환합니다. 입력 메시지를 처리하는 데 문제가 있을 경우 대신 오류를 반환할 수도 있습니다. `SetLightbulbStatus` 연산은 아무 것도 반환하지 않습니다. 이 연산에서 오류 조건을 전달할 방법이 없습니다.  
  
## <a name="describing-messages-by-using-message-contracts"></a>메시지 계약을 사용하여 메시지 설명  
 하나의 형식을 사용하여 전체 메시지를 나타내야 하는 경우가 있습니다. 이러한 목적을 위해 데이터 계약을 사용할 수는 있지만 메시지 계약을 사용하는 것이 좋습니다. 이렇게 하면 결과 XML에서 불필요한 래핑 수준이 생기지 않습니다. 또한 메시지 계약을 통해 결과 메시지를 보다 효과적으로 제어할 수 있습니다. 예를 들어 메시지 본문에 필요한 정보와 메시지 헤더에 필요한 사항을 결정할 수 있습니다. 다음 예제에서는 메시지 계약을 사용하는 방법을 보여 줍니다.  
  
```csharp  
[ServiceContract]  
public interface IAirfareQuoteService  
{  
    [OperationContract]  
    GetAirfareResponse GetAirfare(GetAirfareRequest request);  
}  
  
[MessageContract]  
public class GetAirfareRequest  
{  
    [MessageHeader] public DateTime date;  
    [MessageBodyMember] public Itinerary itinerary;  
}  
  
[MessageContract]  
public class GetAirfareResponse  
{  
    [MessageBodyMember] public float airfare;  
    [MessageBodyMember] public string currency;  
}  
  
[DataContract]  
public class Itinerary  
{  
    [DataMember] public string fromCity;  
    [DataMember] public string toCity;  
}  
```  
  
```vb  
<ServiceContract()>  
Public Interface IAirfareQuoteService  
    <OperationContract()>  
    Function GetAirfare(request As GetAirfareRequest) As GetAirfareResponse  
End Interface  
  
<MessageContract()>  
Public Class GetAirfareRequest  
    <MessageHeader()>   
    Public Property date as DateTime  
    <MessageBodyMember()>  
    Public Property itinerary As Itinerary  
End Class  
  
<MessageContract()>  
Public Class GetAirfareResponse  
    <MessageBodyMember()>  
    Public Property airfare As Double  
    <MessageBodyMember()> Public Property currency As String  
End Class  
  
<DataContract()>  
Public Class Itinerary  
    <DataMember()> Public Property fromCity As String  
    <DataMember()> Public Property toCity As String  
End Class  
```  
  
 자세한 내용은 [Using Message Contracts](../../../../docs/framework/wcf/feature-details/using-message-contracts.md)합니다.  
  
 앞의 예제의 경우 <xref:System.Runtime.Serialization.DataContractSerializer> 클래스가 기본적으로 사용됩니다. <xref:System.Xml.Serialization.XmlSerializer> 클래스는 메시지 계약에 사용할 수도 있습니다. 이 작업을 수행하려면 <xref:System.ServiceModel.XmlSerializerFormatAttribute> 특성을 연산이나 계약에 적용하고 메시지 헤더와 본문 멤버의 <xref:System.Xml.Serialization.XmlSerializer> 클래스와 호환되는 형식을 사용합니다.  
  
## <a name="describing-messages-by-using-streams"></a>스트림을 사용하여 메시지 설명  
 연산에서 메시지를 설명하는 또 다른 방법은 <xref:System.IO.Stream> 클래스 또는 작업 계약의 파생 클래스 중 하나를 사용하거나 메시지 계약 본문 멤버(이 경우 유일한 멤버여야 함)로 사용하는 것입니다. 들어오는 메시지의 경우 형식은 `Stream`이어야 하며, 파생 클래스는 사용할 수 없습니다.  
  
 WCF는 serializer를 호출 하는 대신 스트림에서 데이터를 검색 하 여 나가는 메시지에 직접 저장 하거나 들어오는 메시지에서 데이터를 검색 하 여 스트림에 직접 배치 합니다. 다음 예제에서는 스트림의 사용 방법을 보여 줍니다.  
  
```csharp  
[OperationContract]  
public Stream DownloadFile(string fileName);  
```  
  
```vb  
<OperationContract()>  
Function DownloadFile(fileName As String) As String  
```  
  
 하나의 메시지 본문에서 `Stream`과 비스트림 데이터를 결합할 수 없습니다. 메시지 헤더에 추가 데이터를 넣으려면 메시지 계약을 사용합니다. 다음 예제에서는 작업 계약을 정의할 때 잘못된 스트림 사용 방법을 보여 줍니다.  
  
```csharp  
//Incorrect:  
// [OperationContract]  
// public void UploadFile (string fileName, Stream fileData);  
```  
  
```vb  
'Incorrect:  
    '<OperationContract()>  
    Public Sub UploadFile(fileName As String, fileData As StreamingContext)  
```  
  
 다음 샘플에서는 작업 계약을 정의할 때 올바른 스트림 사용 방법을 보여 줍니다.  
  
```csharp  
[OperationContract]  
public void UploadFile (UploadFileMessage message);  
//code omitted  
[MessageContract]  
public class UploadFileMessage  
{  
    [MessageHeader] public string fileName;  
    [MessageBodyMember] public Stream fileData;  
}  
```  
  
```vb  
<OperationContract()>  
Public Sub UploadFile(fileName As String, fileData As StreamingContext)  
'Code Omitted  
<MessageContract()>  
Public Class UploadFileMessage  
   <MessageHeader()>  
    Public Property fileName As String  
    <MessageBodyMember()>  
    Public Property fileData As Stream  
End Class  
```  
  
 자세한 내용은 [대량 데이터 및 스트리밍](../../../../docs/framework/wcf/feature-details/large-data-and-streaming.md)을 참조 하세요.  
  
## <a name="using-the-message-class"></a>Message 클래스 사용  
 보내거나 받은 메시지를 프로그래밍 방식으로 완벽하게 제어하려면 다음 예제 코드에서처럼 <xref:System.ServiceModel.Channels.Message> 클래스를 직접 사용하면 됩니다.  
  
```csharp  
[OperationContract]  
public void LogMessage(Message m);  
```  
  
```vb  
<OperationContract()>  
Sub LogMessage(m As Message)  
```  
  
 이는 [메시지 클래스 사용](../../../../docs/framework/wcf/feature-details/using-the-message-class.md)에 자세히 설명 되어 있는 고급 시나리오입니다.  
  
## <a name="describing-fault-messages"></a>오류 메시지 설명  
 반환 값과 출력 또는 참조 매개 변수를 사용하여 설명하는 메시지 이외에, 단방향이 아닌 연산은 적어도 두 개의 메시지, 즉 일반 응답 메시지와 오류 메시지를 반환할 수 있습니다. 다음 작업 계약을 예로 들 수 있습니다.  
  
```csharp  
[OperationContract]  
float GetAirfare(string fromCity, string toCity, DateTime date);  
```  
  
```vb  
<OperationContract()>  
Function GetAirfare(fromCity As String, toCity As String, date as DateTime)  
```  
  
 이 연산은 `float` 숫자가 포함된 일반 메시지 또는 오류 코드 및 설명이 포함된 오류 메시지를 반환할 수 있습니다. 서비스 구현에서 <xref:System.ServiceModel.FaultException>을 throw하여 이 연산을 수행할 수 있습니다.  
  
 <xref:System.ServiceModel.FaultContractAttribute> 특성을 사용하여 가능한 추가 오류 메시지를 지정할 수 있습니다. 추가 오류는 다음 예제 코드에서처럼 <xref:System.Runtime.Serialization.DataContractSerializer>를 사용하여 serialize할 수 있어야 합니다.  
  
```csharp  
[OperationContract]  
[FaultContract(typeof(ItineraryNotAvailableFault))]  
float GetAirfare(string fromCity, string toCity, DateTime date);  
  
//code omitted  
  
[DataContract]  
public class ItineraryNotAvailableFault  
{  
    [DataMember]  
    public bool IsAlternativeDateAvailable;  
  
    [DataMember]  
    public DateTime alternativeSuggestedDate;  
}  
```  
  
```vb  
<OperationContract()>  
<FaultContract(GetType(ItineraryNotAvailableFault))>  
Function GetAirfare(fromCity As String, toCity As String, date as DateTime) As Double  
  
'Code Omitted  
<DataContract()>  
Public Class  
  <DataMember()>  
  Public Property IsAlternativeDateAvailable As Boolean  
  <DataMember()>  
  Public Property alternativeSuggestedDate As DateTime  
End Class  
```  
  
 이러한 추가 오류는 해당하는 데이터 계약 형식의 <xref:System.ServiceModel.FaultException%601>을 throw하여 생성될 수 있습니다. 자세한 내용은 [예외 및 오류 처리](../../../../docs/framework/wcf/extending/handling-exceptions-and-faults.md)를 참조 하세요.  
  
 <xref:System.Xml.Serialization.XmlSerializer> 클래스를 사용하여 오류를 설명할 수 없습니다. <xref:System.ServiceModel.XmlSerializerFormatAttribute>는 오류 계약에 영향을 주지 않습니다.  
  
## <a name="using-derived-types"></a>파생 형식 사용  
 특정 연산 또는 메시지 계약에 기본 형식을 사용한 다음 실제로 연산을 호출할 때는 파생 형식을 사용해야 하는 경우가 있습니다. 이 경우 파생 형식을 사용할 수 있도록 <xref:System.ServiceModel.ServiceKnownTypeAttribute> 특성 또는 일부 대체 메커니즘을 사용해야 합니다. 다음 연산을 예로 들 수 있습니다.  
  
```csharp  
[OperationContract]  
public bool IsLibraryItemAvailable(LibraryItem item);  
```  
  
```vb
<OperationContract()>  
    Function IsLibraryItemAvailable(item As LibraryItem) As Boolean  
```  
  
 `Book` 및 `Magazine` 이 두 형식이 `LibraryItem`에서 파생된다고 가정합니다. 이 형식을 `IsLibraryItemAvailable` 연산에서 사용하려면 다음과 같이 연산을 변경합니다.  
  
 `[OperationContract]`  
  
 `[ServiceKnownType(typeof(Book))]`  
  
 `[ServiceKnownType(typeof(Magazine))]`  
  
 `public bool IsLibraryItemAvailable(LibraryItem item);`  
  
 또는 다음 예제 코드에서처럼 기본 <xref:System.Runtime.Serialization.KnownTypeAttribute>가 사용 중인 경우 <xref:System.Runtime.Serialization.DataContractSerializer> 특성을 사용할 수 있습니다.  
  
```csharp  
[OperationContract]  
public bool IsLibraryItemAvailable(LibraryItem item);  
  
// code omitted   
  
[DataContract]  
[KnownType(typeof(Book))]  
[KnownType(typeof(Magazine))]  
public class LibraryItem  
{  
    //code omitted  
}  
```  
  
```vb  
<OperationContract()>  
Function IsLibraryItemAvailable(item As LibraryItem) As Boolean  
  
'Code Omitted  
<DataContract()>  
<KnownType(GetType(Book))>  
<KnownType(GetType(Magazine))>  
Public Class LibraryItem  
  'Code Omitted  
End Class  
```  
  
 <xref:System.Xml.Serialization.XmlIncludeAttribute>를 사용할 때 <xref:System.Xml.Serialization.XmlSerializer> 특성을 사용할 수 있습니다.  
  
 특정 연산 또는 전체 서비스에 <xref:System.ServiceModel.ServiceKnownTypeAttribute> 특성을 적용할 수 있습니다. 호출할 메서드의 형식이나 이름을 사용하여 <xref:System.Runtime.Serialization.KnownTypeAttribute> 특성과 같은 알려진 형식 목록을 가져옵니다. 자세한 내용은 [데이터 계약 알려진 형식을](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)합니다.  
  
## <a name="specifying-the-use-and-style"></a>사용 및 스타일 지정  
 WSDL(웹 서비스 기술 언어)을 사용하여 서비스를 설명하는 경우 문서 스타일과 RPC(원격 프로시저 호출) 스타일이 일반적으로 사용됩니다. 문서 스타일에서 전체 메시지 본문은 스키마를 사용하여 설명되고 WSDL은 해당 스키마 내의 요소를 참조하여 여러 메시지 본문 부분을 설명합니다. RPC 스타일에서 WSDL은 요소가 아닌 각 메시지 부분의 스키마 형식을 참조합니다. 이 두 스타일 중 하나를 수동으로 선택해야 하는 경우도 있습니다. 둘 중 하나만 수동으로 설정하려면 <xref:System.ServiceModel.DataContractFormatAttribute>가 사용 중인 경우에는 `Style` 특성을 적용한 다음 <xref:System.Runtime.Serialization.DataContractSerializer> 속성을 설정하고, `Style`를 사용하는 경우에는 <xref:System.ServiceModel.XmlSerializerFormatAttribute> 특성에 <xref:System.Xml.Serialization.XmlSerializer>을 설정합니다.  
  
 또한 <xref:System.Xml.Serialization.XmlSerializer>는 serialize된 두 가지 형식의 XML `Literal` 및 `Encoded`를 지원합니다. `Literal`은 가장 일반적으로 허용되는 폼이며 <xref:System.Runtime.Serialization.DataContractSerializer>에서 유일하게 지원하는 폼입니다. `Encoded`는 SOAP 사양의 5단원에 설명된 레거시 폼이며 새 서비스에는 사용하지 않는 것이 좋습니다. `Encoded` 모드로 전환하려면 `Use` 특성에서 <xref:System.ServiceModel.XmlSerializerFormatAttribute> 속성을 `Encoded`로 설정합니다.  
  
 대부분의 경우 `Style` 및 `Use` 속성에 대한 기본 설정을 변경하면 안 됩니다.  
  
## <a name="controlling-the-serialization-process"></a>Serialization 프로세스 제어  
 여러 가지 방법으로 데이터를 serialize하는 방법을 사용자 지정할 수 있습니다.  
  
### <a name="changing-server-serialization-settings"></a>서버 Serialization 설정 변경  
 기본 <xref:System.Runtime.Serialization.DataContractSerializer>가 사용 중인 경우 <xref:System.ServiceModel.ServiceBehaviorAttribute> 특성을 서비스에 적용하여 서비스에서 serialization 프로세스의 몇 가지 특성을 제어할 수 있습니다. 특히 `MaxItemsInObjectGraph` 속성을 사용하여 <xref:System.Runtime.Serialization.DataContractSerializer>가 deserialize하는 개체의 최대 개수를 제한하는 할당량을 설정할 수도 있습니다. `IgnoreExtensionDataObject` 속성을 사용하여 라운드트립 버전 관리 기능을 해제할 수 있습니다. 할당량에 대한 자세한 내용은 [데이터에 대한 보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-for-data.md)을 참조하세요. 라운드트립에 대 한 자세한 내용은 [전방 호환 데이터 계약](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)을 참조 하세요.  
  
```csharp  
[ServiceBehavior(MaxItemsInObjectGraph=100000)]  
public class MyDataService:IDataService  
{  
    public DataPoint[] GetData()  
    {  
       // Implementation omitted  
    }  
}  
```  
  
```vb  
<ServiceBehavior(MaxItemsInObjectGraph:=100000)>  
Public Class MyDataService Implements IDataService  
  
    Function GetData() As DataPoint()  
         ‘ Implementation omitted  
    End Function  
End Interface  
```  
  
### <a name="serialization-behaviors"></a>Serialization 동작  
 WCF에서 두 동작을 사용할 수 있습니다. <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> 및 특정 작업에 사용 중인 serializer에 따라 자동으로 연결 되는 <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior>입니다. 이러한 동작은 자동으로 적용되므로 일반적으로 사용자가 알아야 할 필요는 없습니다.  
  
 그러나 `DataContractSerializerOperationBehavior`에는 serialization 프로세스를 사용자 지정하는 데 사용할 수 있는 `MaxItemsInObjectGraph`, `IgnoreExtensionDataObject` 및 `DataContractSurrogate` 속성이 있습니다. 처음 두 속성은 앞 단원에서 설명한 것과 의미가 같습니다. `DataContractSurrogate` 속성을 사용하여 serialization 프로세스를 사용자 지정하고 확장하는 데 필요한 강력한 메커니즘인 데이터 계약 서로게이트를 사용하도록 설정할 수 있습니다. 자세한 내용은 [데이터 계약 서로게이트](../../../../docs/framework/wcf/extending/data-contract-surrogates.md)를 참조 하세요.  
  
 `DataContractSerializerOperationBehavior`를 사용하여 클라이언트와 서버 serialization 모두를 사용자 지정할 수 있습니다. 다음 예제에서는 클라이언트에 `MaxItemsInObjectGraph` 할당량을 늘리는 방법을 보여 줍니다.  
  
```csharp  
ChannelFactory<IDataService> factory = new ChannelFactory<IDataService>(binding, address);  
foreach (OperationDescription op in factory.Endpoint.Contract.Operations)  
{  
    DataContractSerializerOperationBehavior dataContractBehavior =  
                op.Behaviors.Find<DataContractSerializerOperationBehavior>()  
                as DataContractSerializerOperationBehavior;  
    if (dataContractBehavior != null)  
    {  
        dataContractBehavior.MaxItemsInObjectGraph = 100000;  
    }  
}  
IDataService client = factory.CreateChannel();  
```  
  
```vb  
Dim factory As ChannelFactory(Of IDataService) = New ChannelFactory(Of IDataService)(binding, address)  
For Each op As OperationDescription In factory.Endpoint.Contract.Operations  
        Dim dataContractBehavior As DataContractSerializerOperationBehavior = op.Behaviors.Find(Of DataContractSerializerOperationBehavior)()  
        If dataContractBehavior IsNot Nothing Then  
            dataContractBehavior.MaxItemsInObjectGraph = 100000  
        End If  
     Next  
    Dim client As IDataService = factory.CreateChannel  
```  
  
다음은 자체 호스팅 사례의 서비스에 해당 하는 코드입니다.
  
```csharp  
ServiceHost serviceHost = new ServiceHost(typeof(IDataService))  
foreach (ServiceEndpoint ep in serviceHost.Description.Endpoints)  
{  
foreach (OperationDescription op in ep.Contract.Operations)  
{  
        DataContractSerializerOperationBehavior dataContractBehavior =  
           op.Behaviors.Find<DataContractSerializerOperationBehavior>()  
                as DataContractSerializerOperationBehavior;  
        if (dataContractBehavior != null)  
        {  
            dataContractBehavior.MaxItemsInObjectGraph = 100000;  
        }  
}  
}  
serviceHost.Open();  
```  
  
```vb  
Dim serviceHost As ServiceHost = New ServiceHost(GetType(IDataService))  
        For Each ep As ServiceEndpoint In serviceHost.Description.Endpoints  
            For Each op As OperationDescription In ep.Contract.Operations  
                Dim dataContractBehavior As DataContractSerializerOperationBehavior = op.Behaviors.Find(Of DataContractSerializerOperationBehavior)()  
  
                If dataContractBehavior IsNot Nothing Then  
                    dataContractBehavior.MaxItemsInObjectGraph = 100000  
                End If  
            Next  
        Next  
        serviceHost.Open()  
```  
  
 웹 호스팅의 경우 새 `ServiceHost` 파생 클래스를 만들고 서비스 호스트 팩터리를 사용하여 연결해야 합니다.  
  
### <a name="controlling-serialization-settings-in-configuration"></a>구성에서 Serialization 설정 제어  
 `MaxItemsInObjectGraph` 및 `IgnoreExtensionDataObject`는 다음 예제에서처럼 `dataContractSerializer` 엔드포인트 또는 서비스 동작을 사용하여 구성을 통해 제어될 수 있습니다.  
  
```xml  
<configuration>  
    <system.serviceModel>  
        <behaviors>  
            <endpointBehaviors>  
                <behavior name="LargeQuotaBehavior">  
                    <dataContractSerializer  
                      maxItemsInObjectGraph="100000" />  
                </behavior>  
            </endpointBehaviors>  
        </behaviors>  
        <client>  
            <endpoint address="http://example.com/myservice"  
                  behaviorConfiguration="LargeQuotaBehavior"  
                binding="basicHttpBinding" bindingConfiguration=""   
                            contract="IDataService"  
                name="" />  
        </client>  
    </system.serviceModel>  
</configuration>  
```  
  
### <a name="shared-type-serialization-object-graph-preservation-and-custom-serializers"></a>공유 형식 Serialization, 개체 그래프 유지 및 사용자 지정 Serializer  
 <xref:System.Runtime.Serialization.DataContractSerializer>는 .NET 형식 이름이 아니라 데이터 계약 이름을 사용하여 serialize합니다. 이러한 serialization 방식은 서비스 기반 아키텍처 개념과 일치하며, 연결 계약에 영향을 주지 않고 .NET 형식을 변경할 수 있는 등 유연성을 높여 줍니다. 드문 경우지만 실제 .NET 형식 이름을 serialize해야 하는 경우가 있으며, 이 경우 .NET Framework Remoting 기술과 유사한 클라이언트와 서버 간 밀접한 결합이 가능합니다. 드문 경우 지만 .NET Framework remoting에서 WCF로 마이그레이션할 때 발생 하는 경우를 제외 하 고이 방법은 권장 되지 않습니다. 이 경우에는 <xref:System.Runtime.Serialization.NetDataContractSerializer> 클래스 대신 <xref:System.Runtime.Serialization.DataContractSerializer> 클래스를 사용해야 합니다.  
  
 <xref:System.Runtime.Serialization.DataContractSerializer>는 일반적으로 개체 그래프를 개체 트리로 serialize합니다. 즉, 같은 개체를 두 번 이상 참조하는 경우 두 번 이상 serialize됩니다. `PurchaseOrder`와 `billTo`라고 하는 두 가지 주소 형식 필드가 있는 `shipTo` 인스턴스를 예로 들 수 있습니다. 두 필드가 같은 주소 인스턴스로 설정된 경우 serialization 및 deserialization 후 두 개의 동일한 주소 인스턴스가 생깁니다. <xref:System.Xml.Serialization.XmlSerializer> 및 `Style`에 대해 앞 단원에서 설명한 대로 `Use`에서 사용할 수 있는 레거시 SOAP 인코딩 표준을 제외하고, XML로 개체 그래프를 나타낼 표준 상호 운용 가능한 방법이 없기 때문에 이와 같이 수행됩니다. 개체 그래프를 트리로 serialize하면 순환 참조가 있는 그래프를 serialize할 수 없는 등의 단점이 있습니다. 상호 운용이 가능하지 않아도 실제 개체 그래프 serialization으로 전환해야 하는 경우도 있습니다. 이 작업은 <xref:System.Runtime.Serialization.DataContractSerializer>로 설정된 `preserveObjectReferences` 매개 변수를 사용하여 생성된 `true`를 사용하여 수행할 수 있습니다.  
  
 기본 제공 serializer가 사용자 시나리오에 적합하지 않은 경우도 있습니다. 대부분의 경우 <xref:System.Runtime.Serialization.XmlObjectSerializer> 및 <xref:System.Runtime.Serialization.DataContractSerializer>가 모두 파생된 <xref:System.Runtime.Serialization.NetDataContractSerializer> 추상화를 사용할 수 있습니다.  
  
 앞의 세 가지 경우(.NET 형식 유지, 개체 그래프 유지 및 `XmlObjectSerializer` 기반의 완전한 사용자 지정 serialization) 모두 사용자 지정 serializer를 연결해야 합니다. 그렇게 하려면 다음 단계를 수행합니다.  
  
1. <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>에서 파생되는 고유한 동작을 작성합니다.  
  
2. 두 개의 `CreateSerializer` 메서드를 재정의하여 고유한 serializer(<xref:System.Runtime.Serialization.NetDataContractSerializer>, <xref:System.Runtime.Serialization.DataContractSerializer>가 `preserveObjectReferences`로 설정된 `true` 또는 사용자 지정 <xref:System.Runtime.Serialization.XmlObjectSerializer>)를 반환합니다.  
  
3. 서비스 호스트를 열거나 클라이언트 채널을 만들기 전에 기존 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> 동작을 제거하고 이전 단계에서 만든 사용자 지정 파생 클래스에 연결합니다.  
  
 고급 직렬화 개념에 대 한 자세한 내용은 [serialization 및 Deserialization](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md)을 참조 하세요.  
  
## <a name="see-also"></a>참조

- [XmlSerializer 클래스 사용](../../../../docs/framework/wcf/feature-details/using-the-xmlserializer-class.md)
- [방법: 스트리밍 사용](../../../../docs/framework/wcf/feature-details/how-to-enable-streaming.md)
- [방법: 클래스 또는 구조체에 대 한 기본 데이터 계약 만들기 @ no__t-0
