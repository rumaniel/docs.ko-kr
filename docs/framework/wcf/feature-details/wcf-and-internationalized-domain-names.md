---
title: WCF 및 IDN(Internationalized Domain Name)
ms.date: 03/30/2017
ms.assetid: c8a3e10a-8bc2-4a78-8d86-a562ba6e65fa
ms.openlocfilehash: 1db62f3e7d073fd1bf9bf9d4d0e17703310f2e69
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988592"
---
# <a name="wcf-and-internationalized-domain-names"></a>WCF 및 IDN(Internationalized Domain Name)
IDN(Internationalized Domain Name)을 사용하는 WCF 서비스에 대한 지원이 추가되었습니다. IDN(Internationalized Domain Name)은 비 ASCII 문자가 포함된 도메인 이름입니다. 이 지원을 통해 IDN 이름을 사용하는 WCF 서비스와 IDN 이름을 사용하는 웹 서비스와 통신하는 WCF 클라이언트를 둘 다 호스트할 수 있습니다.  
  
## <a name="systemuri-and-idn"></a>System.Uri 및 IDN  
 <xref:System.Uri>에는 <xref:System.Uri.Host%2A>와 <xref:System.Uri.DnsSafeHost%2A>라는 두 가지 속성이 있습니다. 이러한 속성에는 IDN 구성 설정에 따라 유니코드 또는 Punycode 값이 들어 있습니다.  
  
 IDN은 다음 XML을 사용하여 애플리케이션의 구성 파일에서 사용할 수 있습니다.  
  
```xml  
<configuration>  
  <uri>  
    <idn enabled="All/AllExceptIntranet/None" />  
  </uri>  
</configuration>  
```  
  
 Idn \<> 요소는 다음 값 중 하나로 설정할 수 있는 enabled 특성을 포함 합니다.  
  
1. "None"  
  
2. "AllExceptIntranet"  
  
3. 모두가  
  
 IDN 설정이 "None"으로 설정 된 경우에는 Uri 또는 Uri. DnsSafeHost를 통해 변환이 수행 되지 않습니다. IDN 설정이 "All"로 설정 되 면 uri로 설정 됩니다. 호스트는 유니코드 및 uri로 유지 됩니다. DnsSafeHost는 Punycode로 변환 됩니다. IDN 설정이 "AllExceptIntranet" (uri)로 설정 된 경우 DnsSafeHost는 인터넷 주소에 대해 Punycode로 변환 되며 인트라넷 주소에 대해서는 유니코드로 유지 됩니다. 이 설정은 정확한 DNS 이름 확인을 위해 중요합니다. Windows 8 및 최신 버전에서는 이 설정을 구성하지 않아도 됩니다.  
  
> [!WARNING]
> Punycode를 사용하여 주소를 하드 코딩하지 마세요. WCF는 사용자가 적용하는 구성 설정을 기준으로 변환해 줍니다.  
  
> [!WARNING]
> applicationHost.exe.config에 유니코드 문자를 추가하는 경우 파일을 UTF-8 인코딩으로 저장하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Uri?displayProperty=nameWithType>
