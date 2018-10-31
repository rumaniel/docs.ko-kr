---
title: IPv6 및 Teredo를 사용하는 NAT 통과
ms.date: 03/30/2017
ms.assetid: 568cd245-3300-49ef-a995-d81bf845d961
ms.openlocfilehash: 32f3caa88e05c7261d5cb7646ac618d33ca1e060
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50185458"
---
# <a name="nat-traversal-using-ipv6-and-teredo"></a>IPv6 및 Teredo를 사용하는 NAT 통과
NAT(Network Address Translation) 통과 지원을 제공하도록 개선되었습니다. 이러한 변경 사항은 IPv6 및 Teredo와 함께 사용하도록 설계되었지만, 다른 IP 터널링 기술에도 적용할 수 있습니다. 이러한 개선사항은 <xref:System.Net> 및 관련 네임스페이스의 클래스에 영향을 미칩니다.  
  
 이러한 변경 사항은 IP 터널링 기술을 사용할 계획인 클라이언트와 서버 응용 프로그램에 영향을 미칠 수 있습니다.  
  
 NAT 통과를 지원하는 변경 사항은 .NET Framework 버전 4를 사용하는 응용 프로그램에만 사용할 수 있습니다. 이러한 기능은 이전 버전의 .NET Framework에서는 사용할 수 없습니다.  
  
## <a name="overview"></a>개요  
 IPv4(인터넷 프로토콜 버전 4)에서는 IPv4 주소를 32비트 길이로 정의합니다. 결과적으로 IPv4에서는 약 40억 개의 고유한 IP 주소(2^32)를 지원합니다. 1990년대에 인터넷에서 컴퓨터 및 네트워크 장치 수가 증가함에 따라 IPv4 주소 공간의 한계가 분명해졌습니다.  
  
 IPv4의 수명을 연장하는 데 사용된 여러 기술 중 하나로, NAT를 배포하여 하나의 고유한 공용 IP 주소가 다수의 개인 IP 주소(사설 인트라넷)를 나타내도록 했습니다. NAT 장치 뒤에 있는 개인 IP 주소가 하나의 공용 IPv4 주소를 공유합니다. NAT 장치는 전용 하드웨어 장치(예: 저렴한 무선 액세스 지점 및 라우터) 또는 NAT를 제공하는 서비스를 실행 중인 컴퓨터일 수 있습니다. 이 공용 IP 주소의 장치 또는 서비스는 공용 인터넷과 사설 인트라넷 사이의 IP 네트워크 패킷을 변환합니다.  
  
 이 체계는 인터넷에 있는 다른 IP 주소(일반적으로 서버)로 요청을 전송하는 사설 인트라넷에서 실행 중인 클라이언트 응용 프로그램에 적합합니다. NAT 장치 또는 서버에서 클라이언트 요청의 매핑을 유지할 수 있으므로 응답이 반환될 때 응답을 보낼 위치를 압니다. 하지만 이 체계를 사용하면 서비스를 제공하고 패킷을 수신 대기하며 응답하려는 NAT 장치 뒤에 있는 사설 인트라넷에서 실행 중인 응용 프로그램에 문제가 제기될 수 있습니다. 이 피어 투 피어 응용 프로그램의 경우 특히 해당됩니다.  
  
 IPv6 프로토콜에서 128 비트 길이의 IPv4 주소를 정의합니다. 결과적으로 IPv6에서는 3.2 x 10^38개의 고유한 주소(2^128)로 구성된 대규모 IP 주소 공간을 지원합니다. 이 크기의 주소 공간이 있으므로 인터넷에 연결된 모든 장치에 고유한 주소를 지정할 수 있습니다. 그러나 여기에는 문제가 있습니다. 대부분 여전히 IPv4만 사용하고 있습니다. 특히 소규모 회사, 조직 및 가정에서 사용하는 기존 라우터와 무선 액세스 지점 중 대부분에서는 IPv6을 지원하지 않습니다. 또한 이러한 고객에게 서비스를 제공하는 일부 인터넷 서비스 제공업체에서는 IPv6을 지원하지 않거나 해당 지원이 구성되어 있지 않습니다.  
  
 IPv4 패킷에 IPv6 주소를 터널링하기 위해 여러 IPv6 변환 기술이 개발되었습니다. 이러한 기술에는 IPv6 호스트가 다른 IPv6 네트워크에 연결하기 위해 IP4 네트워크를 트래버스해야 할 때 유니캐스트 IPv6 트래픽의 호스트 간 자동 터널링 및 주소 할당을 제공하는 6to4, ISATAP 및 Teredo 터널이 포함됩니다. IPv6 패킷은 IPv4 패킷으로 터널링되어 전송됩니다. NAT 장치를 통해 IPv6 주소의 NAT 통과를 허용하는 여러 터널링 기술이 사용됩니다.  
  
 Teredo는 IPv6을 IPv4 네트워크에 연결하는 IPv6 변환 기술 중 하나입니다. Teredo는 IETF(Internet Engineering Task Force)에서 게시한 RFC 4380에 설명되어 있습니다. Windows XP SP2 이상에서는 2001:0::/32 범위의 공용 IPv6 주소를 제공할 수 있는 가상 Teredo 어댑터에 대한 지원을 제공합니다. 이 IPv6 주소는 인터넷에서 입력되는 연결을 수신 대기하는 데 사용할 수 있고, 수신 대기 서비스에 연결하려는 IPv6 사용 클라이언트에 제공할 수 있습니다. 따라서 응용 프로그램이 IPv6 Teredo 주소를 사용하여 연결하기만 하면 되므로 NAT 장치 뒤에 있는 컴퓨터의 주소를 지정하는 방법을 고려하지 않아도 됩니다.  
  
## <a name="enhancements-to-support-nat-traversal-and-teredo"></a>NAT 통과 및 Teredo를 지원하기 위한 개선사항  
 IPv6 및 Teredo를 사용하여 NAT 통과를 지원하기 위해 <xref:System.Net>, <xref:System.Net.NetworkInformation> 및 <xref:System.Net.Sockets> 네임스페이스에 향상된 기능이 추가되었습니다.  
  
 호스트에서 유니캐스트 IP 주소 목록을 가져오기 위해 <xref:System.Net.NetworkInformation.IPGlobalProperties?displayProperty=nameWithType> 클래스에 여러 메서드가 추가되었습니다. 로컬 컴퓨터에서 안정적인 유니캐스트 IP 주소 테이블을 검색하기 위해 <xref:System.Net.NetworkInformation.IPGlobalProperties.BeginGetUnicastAddresses%2A> 메서드에서 비동기 요청을 시작합니다. 로컬 컴퓨터에서 안정적인 유니캐스트 IP 주소 테이블을 검색하기 위해 <xref:System.Net.NetworkInformation.IPGlobalProperties.EndGetUnicastAddresses%2A> 메서드에서 보류 중인 비동기 요청을 종료합니다. <xref:System.Net.NetworkInformation.IPGlobalProperties.GetUnicastAddresses%2A> 메서드는 로컬 컴퓨터에서 안정적인 유니캐스트 IP 주소 테이블을 검색하기 위한 동기 요청이며, 필요한 경우 주소 테이블이 안정화될 때까지 대기합니다.  
  
 <xref:System.Net.IPAddress.IsIPv6Teredo%2A?displayProperty=nameWithType> 속성을 사용하여 <xref:System.Net.IPAddress>가 IPv6 Teredo 주소인지 판별할 수 있습니다.  
  
 이러한 새 <xref:System.Net.NetworkInformation.IPGlobalProperties> 클래스 메서드를 <xref:System.Net.IPAddress.IsIPv6Teredo%2A> 속성과 함께 사용하면 응용 프로그램에서 Teredo 주소를 쉽게 찾을 수 있습니다. 로컬 Teredo 주소에 대한 정보를 원격 응용 프로그램과 통신하는 경우 일반적으로 응용 프로그램에서는 이 정보만 알면 됩니다. 예를 들어, 피어 투 피어 응용 프로그램에서 모든 IPv6 주소를 결혼 정보 회사 서버에 전송할 수 있습니다. 그러면 직접 통신이 가능하도록 다른 피어에 해당 주소를 전달할 수 있습니다.  
  
 일반적으로 응용 프로그램에서는 로컬 Teredo 주소가 아니라 <xref:System.Net.IPAddress.IPv6Any?displayProperty=nameWithType>에서 수신 대기하도록 수신 대기 서비스를 설정합니다. 원격 클라이언트 또는 피어에 수신 대기 서비스 호스트에 대한 직접 IPv6 라우트가 있으면 클라이언트나 피어에서 Teredo를 사용하여 패킷을 터널링하지 않고, IPv6을 사용하여 직접 연결할 수 있습니다.  
  
 TCP 응용 프로그램의 경우 <xref:System.Net.Sockets.TcpListener?displayProperty=nameWithType> 클래스에는 NAT 통과를 사용하게 설정하는 <xref:System.Net.Sockets.TcpListener.AllowNatTraversal%2A> 메서드가 있습니다. UDP 응용 프로그램의 경우 <xref:System.Net.Sockets.UdpClient?displayProperty=nameWithType> 클래스에는 NAT 통과를 사용하게 설정하는 <xref:System.Net.Sockets.UdpClient.AllowNatTraversal%2A> 메서드가 있습니다.  
  
 <xref:System.Net.Sockets.Socket?displayProperty=nameWithType> 및 관련 클래스를 사용하는 응용 프로그램의 경우 <xref:System.Net.Sockets.Socket.GetSocketOption%2A> 및 <xref:System.Net.Sockets.Socket.SetSocketOption%2A> 메서드를 <xref:System.Net.Sockets.SocketOptionName.IPProtectionLevel?displayProperty=nameWithType> 소켓 옵션과 함께 사용하여 NAT 통과를 쿼리, 사용 또는 사용하지 않게 설정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Net.IPAddress.IsIPv6Teredo%2A?displayProperty=nameWithType>  
 <xref:System.Net.NetworkInformation.IPGlobalProperties.BeginGetUnicastAddresses%2A?displayProperty=nameWithType>  
 <xref:System.Net.NetworkInformation.IPGlobalProperties.EndGetUnicastAddresses%2A?displayProperty=nameWithType>  
 <xref:System.Net.NetworkInformation.IPGlobalProperties.GetUnicastAddresses%2A?displayProperty=nameWithType>  
 <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=nameWithType>  
 <xref:System.Net.Sockets.Socket.SetIPProtectionLevel%2A?displayProperty=nameWithType>  
 <xref:System.Net.Sockets.TcpListener.AllowNatTraversal%2A?displayProperty=nameWithType>  
 <xref:System.Net.Sockets.UdpClient.AllowNatTraversal%2A?displayProperty=nameWithType>
