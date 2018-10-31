---
title: '방법: IPv6 지원을 사용하도록 컴퓨터 구성 파일 수정'
ms.date: 03/30/2017
ms.assetid: 5611b677-b9cc-43b8-a434-60e18d89aada
ms.openlocfilehash: 32aa1c3fa50d5c0486da4ef6799c77ead605b504
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50187259"
---
# <a name="how-to-modify-the-computer-configuration-file-to-enable-ipv6-support"></a>방법: IPv6 지원을 사용하도록 컴퓨터 구성 파일 수정
다음 코드 예제에서는 컴퓨터 구성 파일 *machine.config*를 수정하여 IPv6 지원을 사용하도록 설정하는 방법을 보여 줍니다. *machine.config* 파일은 Windows가 설치된 디렉터리의 *%Windir%\Microsoft.NET\Framework* 폴더에 저장됩니다. 컴퓨터에 설치된 .NET Framework의 각 버전에 해당하는 *%Windir%\Microsoft.NET\Framework* 아래의 폴더에는 개별 *machine.config* 파일이 있습니다(예: *C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\machine.config*).  
  
 이러한 설정은 컴퓨터 구성 파일보다 우선하는 응용 프로그램의 구성 파일에서 만들 수도 있습니다.  
  
 .NET Framework 버전 1.1 이하의 경우 **ipv6 enabled** 구성 스위치 값은 <xref:System.Net.Dns?displayProperty=nameWithType> 클래스의 멤버가 IPv6 주소를 반환하는지 여부를 지정합니다.  
  
 .NET Framework 버전 2.0 이상의 경우 Windows에서 IPv6을 지원하면 <xref:System.Net.Dns?displayProperty=nameWithType> 클래스의 모든 멤버(예: <xref:System.Net.Dns.GetHostEntry%2A?displayProperty=nameWithType> 메서드)는 한 가지 제한과 함께 IPv6 주소를 반환합니다. <xref:System.Net.Dns?displayProperty=nameWithType> 클래스의 사용되지 않는 멤버(예: <xref:System.Net.Dns.Resolve%2A?displayProperty=nameWithType> 메서드)는 구성 파일에서 값을 읽고 인식합니다.  
  
> [!NOTE]
>  .NET Framework 버전 2.0 이상의 경우 기본적으로 IPv6이 사용됩니다. .NET Framework 버전 1.1 이하의 경우 IPv6은 기본적으로 사용되지 않습니다.  
  
## <a name="example"></a>예  
  
```xml  
<system.net>  
    …………  
    <settings>  
        …………  
        <ipv6 enabled="true"/>   
    ……………  
    </settings>  
    ………………  
<system.net>  
```  
  
## <a name="see-also"></a>참고 항목  
 [IPv6 주소 지정](../../../docs/framework/network-programming/ipv6-addressing.md)  
 [네트워크 설정 스키마](../../../docs/framework/configure-apps/file-schema/network/index.md)  
 [\<ipv6> 요소(네트워크 설정)](../../../docs/framework/configure-apps/file-schema/network/ipv6-element-network-settings.md)
