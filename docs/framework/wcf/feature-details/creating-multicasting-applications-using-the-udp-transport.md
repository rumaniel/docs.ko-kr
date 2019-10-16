---
title: UDP 전송을 사용하여 멀티캐스트 애플리케이션 만들기
ms.date: 03/30/2017
ms.assetid: 7485154a-6e85-4a67-a9d4-9008e741d4df
ms.openlocfilehash: b65a277b6e76767d1e3bfdbebbac5051759986e0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61857196"
---
# <a name="creating-multicasting-applications-using-the-udp-transport"></a>UDP 전송을 사용하여 멀티캐스트 애플리케이션 만들기
멀티캐스트 애플리케이션은 점대점 연결을 설정하지 않고도 작은 메시지를 많은 수신자에게 동시에 보냅니다. 그러한 애플리케이션은 신뢰성보다 속도를 강조합니다. 달리 말해, 특정 메시지가 실제로 수신되었는지를 보장하는 것보다 데이터를 적시에 보내는 것이 더 중요합니다. WCF는 이제 <xref:System.ServiceModel.UdpBinding>을 사용한 멀티캐스트 애플리케이션 작성을 지원합니다. 이 전송은 서비스에서 작은 메시지를 많은 클라이언트에 동시에 보내야 할 때 유용합니다. 이러한 서비스의 예로는 주식 시세 애플리케이션이 있습니다.  
  
## <a name="implementing-a-multicast-application"></a>멀티캐스트 애플리케이션 구현  
 멀티캐스트 애플리케이션을 구현하려면 멀티캐스트 메시지에 응답해야 하는 각 소프트웨어 구성 요소에 대해 서비스 계약을 정의하고 서비스 계약을 구현합니다. 예를 들어 주식 시세 애플리케이션에서 서비스 계약을 정의할 수 있습니다.  
  
```csharp
// Shared contracts between the client and the service  
[ServiceContract]
interface IStockTicker
{
    [OperationContract(IsOneWay = true)]
    void SendStockInfo(StockInfo[] stockInfo);
}

[DataContract]
class StockInfo
{
    [DataMember]
    public string Symbol;

    [DataMember]
    public float Price;

    public StockInfo(string symbol, float price)
    {
        this.Symbol = symbol;
        this.Price = price;
    }
}
```  
  
 멀티캐스트 메시지를 수신하려는 각 애플리케이션은 이 인터페이스를 노출하는 서비스를 호스팅해야 합니다.  예를 들어, 다음은 멀티캐스트 메시지를 수신하는 방법을 보여 주는 코드 샘플입니다.  
  
```csharp
// Service Address
string serviceAddress = "soap.udp://224.0.0.1:40000";
// Binding
UdpBinding myBinding = new UdpBinding();
// Host
ServiceHost host = new ServiceHost(typeof(StockTickerService), new Uri(serviceAddress));
// Add service endpoint
host.AddServiceEndpoint(typeof(IStockTicker), myBinding, string.Empty);
// Openup the service host
host.Open();

Console.WriteLine("Start receiving stock information");
Console.ReadLine();
```  
  
 이 애플리케이션은 모든 서비스를 수신 대기할 UDP 주소를 지정합니다. 새로운 <xref:System.ServiceModel.ServiceHost>가 만들어지고 <xref:System.ServiceModel.UdpBinding>을 사용해서 서비스 엔드포인트가 노출됩니다. 그런 후 <xref:System.ServiceModel.ServiceHost>가 열리고 들어오는 메시지에 대한 수신 대기를 시작합니다.  
  
 이러한 유형의 시나리오에서는 클라이언트가 실제로 멀티캐스트 메시지를 전송합니다. 정확한 UDP 주소에서 수신 대기하는 각 서비스가 멀티캐스트 메시지를 수신합니다. 다음 예제는 멀티캐스트 메시지를 보내는 클라이언트입니다.  
  
```csharp
// Multicast Address
string serviceAddress = "soap.udp://224.0.0.1:40000";

// Binding
UdpBinding myBinding = new UdpBinding();

// Channel factory
ChannelFactory<IStockTicker> factory 
    = new ChannelFactory<IStockTicker>(myBinding,
                new EndpointAddress(serviceAddress));

// Call service
IStockTicker proxy = factory.CreateChannel();

while (true)
{
    // This will continue to mulicast stock information
    proxy.SendStockInfo(GetStockInfo());
    Console.WriteLine($"sent stock info at {DateTime.Now}");
    // Wait for one second before sending another update
    System.Threading.Thread.Sleep(new TimeSpan(0, 0, 1));
}
```  
  
 이 코드는 주식 정보를 생성한 다음 IStockTicker 서비스 계약을 사용하여 정확한 UDP 주소에서 수신 대기하는 호출 서비스에 멀티캐스트 메시지를 전송합니다.  
  
### <a name="udp-and-reliable-messaging"></a>UDP 및 신뢰할 수 있는 메시징  
 UDP 프로토콜은 가볍기 때문에 UDP 바인딩은 신뢰할 수 있는 메시징을 지원하지 않습니다. 원격 엔드포인트에서 메시지를 수신했는지 확인해야 할 경우 HTTP 또는 TCP와 같이 신뢰할 수 있는 메시지를 지원하는 전송을 사용하세요. 신뢰할 수 있는 메시징 참조에 대 한 자세한 내용은 https://go.microsoft.com/fwlink/?LinkId=231830  
  
### <a name="two-way-multicast-messaging"></a>양방향 멀티캐스트 메시징  
 멀티캐스트 메시지가 일반적으로 단방향이지만, UdpBinding은 요청/회신 메시지 교환을 지원하지 않습니다. UDP 전송을 사용하여 보낸 메시지에는 보낸 사람 및 받는 사람 주소가 모두 포함되어 있습니다. 보낸 사람 주소를 사용할 때는 도중에 악의적으로 변경될 수 있으므로 주의해야 합니다.  이 주소는 다음 코드를 사용하여 점검할 수 있습니다.  
  
```csharp
if (address.AddressFamily == AddressFamily.InterNetwork)
{
    // IPv4
    byte[] addressBytes = address.GetAddressBytes();
    return ((addressBytes[0] & 0xE0) == 0xE0);
}
else
{
    // IPv6
    return address.IsIPv6Multicast;
}
```  
  
 이 코드는 보낸 사람 주소의 첫 번째 바이트를 보고 멀티캐스트 주소인지를 나타내는 0xE0이 들어 있는지 확인합니다.  
  
### <a name="security-considerations"></a>보안 고려 사항  
 멀티캐스트 메시지를 수신 대기하는 경우 ICMP 패킷을 라우터로 전송하여 멀티캐스트 주소에서 수신 대기 중임을 알립니다. 로컬 서브넷에서 권한이 있는 모든 사용자는 이러한 형식의 패킷을 수신 대기하고 수신 대기할 멀티캐스트 주소와 포트를 결정할 수 있습니다.  
  
 보안 목적을 위해 보낸 사람의 IP 주소를 사용하지 마십시오. 이 정보가 스푸핑되면 애플리케이션이 잘못된 컴퓨터로 응답을 보낼 수 있습니다. 이 위협을 줄이는 한 가지 방법은 메시지 수준 보안을 사용하는 것입니다. 네트워크 수준 IPSec(Internet Protocol Security) 및/또는 NAP(Network Access Protection)에서도 사용 가능합니다.
