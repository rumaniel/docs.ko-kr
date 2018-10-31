---
title: IPv6 사용 및 사용 안 함
ms.date: 03/30/2017
ms.assetid: 6408d3ef-c9ba-49d9-b15e-fe74bd3ef031
ms.openlocfilehash: 9dbbbbb522628de81be3d3d1382867de99c570d0
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50183089"
---
# <a name="enabling-and-disabling-ipv6"></a>IPv6 사용 및 사용 안 함
IPv6 프로토콜을 사용하려면 IPv6을 지원하는 운영 체제 버전을 실행 중인지 확인하고 운영 체제와 네트워킹 클래스가 제대로 구성되어 있는지 확인합니다.  
  
## <a name="configuration-steps"></a>구성 단계  
 다음 표에는 다양한 구성이 나와 있습니다.  
  
|운영 체제 IPv6 사용?|네트워킹 클래스 IPv6 사용?|설명|  
|-------------------------------------|---------------------------------------|-----------------|  
|아니요|아니요|IPv6 주소를 구문 분석할 수 있습니다.|  
|아니요|예|IPv6 주소를 구문 분석할 수 있습니다.|  
|예|아니요|IPv6 주소를 구문 분석하고 사용되지 않음으로 표시된 이름 확인 메서드로 IPv6 주소를 확인할 수 있습니다.|  
|예|예|사용되지 않음으로 표시된 항목이 포함된 모든 메서드를 사용하여 IPv6 주소를 구문 분석 및 확인할 수 있습니다.|  
  
 System.Net 네임스페이스의 모든 클래스에 대한 IPv6 지원을 사용하도록 설정하려면 컴퓨터 구성 파일 또는 응용 프로그램 구성 파일을 수정해야 합니다. 응용 프로그램 구성 파일이 컴퓨터 구성 파일보다 우선 적용됩니다.  
  
 컴퓨터 구성 파일 *machine.config*를 수정하여 IPv6 지원을 사용하는 방법의 예제는 [방법: IPv6 지원을 사용하도록 컴퓨터 구성 파일 수정](../../../docs/framework/network-programming/how-to-modify-the-computer-configuration-file-to-enable-ipv6-support.md)을 참조하세요. 또한 운영 체제에 대한 IPv6 지원이 사용하도록 설정되어 있는지 확인합니다.  
  
 .NET Framework의 경우 구성 파일에 구성 스위치가 다음과 같이 설정되어 있습니다.  
  
```xml  
<system.net>…  
    <settings>…  
        <ipv6 enabled="true"/>…  
    </settings>…  
</system.net>  
```  
  
 .NET Framework 버전 1.1 이하의 경우 **ipv6 enabled** 구성 스위치 값은 <xref:System.Net.Dns?displayProperty=nameWithType> 클래스의 멤버가 IPv6 주소를 반환하는지 여부를 지정합니다.  
  
 .NET Framework 버전 2.0 이상의 경우 Windows에서 IPv6을 지원하면 <xref:System.Net.Dns?displayProperty=nameWithType> 클래스의 멤버(예: <xref:System.Net.Dns.GetHostEntry%2A?displayProperty=nameWithType> 메서드)는 한 가지 제한과 함께 IPv6 주소를 반환합니다. DNS <xref:System.Net.Dns?displayProperty=nameWithType>의 사용되지 않는 멤버(예: <xref:System.Net.Dns.Resolve%2A?displayProperty=nameWithType> 메서드)는 구성 파일에서 ipv6 enabled 설정에 대한 값을 읽고 인식합니다.  
  
## <a name="see-also"></a>참고 항목  
 [인터넷 프로토콜 버전 6](../../../docs/framework/network-programming/internet-protocol-version-6.md)  
 [소켓](../../../docs/framework/network-programming/sockets.md)  
 [네트워크 설정 스키마](../../../docs/framework/configure-apps/file-schema/network/index.md)  
 [\<ipv6> 요소(네트워크 설정)](../../../docs/framework/configure-apps/file-schema/network/ipv6-element-network-settings.md)
