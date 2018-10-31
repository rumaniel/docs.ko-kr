---
title: 인터넷 인증
ms.date: 03/30/2017
helpviewer_keywords:
- authentication [.NET Framework], classes
- IAuthenticationModule interface
- ICredentialLookup interface
- CredentialCache class, about CredentialCache class
- receiving data, authentication
- AuthenticationManager class, about AuthenticationManager class
- Internet, authentication
- sending data, authentication
- network resources, authentication
- user authentication, classes for authentication
- NetworkCredential class, about NetworkCredential class
- client authentication, classes for authentication
ms.assetid: d342e87c-f672-4660-a513-41a2f2b80c4a
ms.openlocfilehash: 245e94cab61c0c60672476aadb417fc798b30362
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50181045"
---
# <a name="internet-authentication"></a>인터넷 인증
<xref:System.Net> 클래스는 표준 인터넷 인증 방법인 기본, 다이제스트, 협상, NTLM 및 Kerberos 인증뿐 아니라 직접 만들 수 있는 사용자 지정 방법을 포함한 다양한 클라이언트 인증 메커니즘을 지원합니다.  
  
 인증 자격 증명은 <xref:System.Net.ICredentials> 인터페이스를 구현하는 <xref:System.Net.NetworkCredential> 및 <xref:System.Net.CredentialCache> 클래스에 저장됩니다. 이러한 클래스 중 하나를 쿼리하여 자격 증명이 있는지 확인할 경우 해당 클래스는 **NetworkCredential** 클래스의 인스턴스를 반환합니다. 인증 프로세스는 <xref:System.Net.AuthenticationManager> 클래스에서 관리되고 실제 인증 프로세스는 <xref:System.Net.IAuthenticationModule> 인터페이스를 구현하는 인증 모듈 클래스에서 수행됩니다. 사용자 지정 인증 모듈을 사용하기 전에 **AuthenticationManager**에 등록해야 합니다. 기본, 다이제스트, 협상, NTLM 및 Kerberos 인증 방법용 모듈은 기본적으로 등록되어 있습니다.  
  
 **NetworkCredential**은 URI로 식별되는 단일 인터넷 리소스와 연결된 자격 증명 집합을 저장하고 <xref:System.Net.NetworkCredential.GetCredential%2A> 메서드 호출에 대한 응답으로 자격 증명을 반환합니다. **NetworkCredential** 클래스는 일반적으로 제한된 수의 인터넷 리소스에 액세스하는 응용 프로그램에서 사용되거나 모든 경우에 동일한 자격 증명 집합을 사용하는 응용 프로그램에서 사용됩니다.  
  
 **CredentialCache** 클래스는 다양한 웹 리소스에 대한 자격 증명 컬렉션을 저장합니다. <xref:System.Net.CredentialCache.GetCredential%2A> 메서드가 호출되면 **CredentialCache**는 웹 리소스의 URI 및 요청된 인증 체계를 통해 확인되는 적절한 자격 증명 집합을 반환합니다. 다양한 인증 체계가 적용된 다양한 인터넷 리소스를 사용하는 응용 프로그램은 **CredentialCache** 클래스를 사용하는 것이 유용합니다. 이 응용 프로그램은 모든 자격 증명을 저장하고 요청 시 제공하기 때문입니다.  
  
 인터넷 리소스가 인증을 요청하면 <xref:System.Net.WebRequest.GetResponse%2A?displayProperty=nameWithType> 메서드는 <xref:System.Net.WebRequest>를 자격 증명 요청과 함께 **AuthenticationManager**에 보냅니다. 그러면 요청이 다음 프로세스에 따라 인증됩니다.  
  
1.  **AuthenticationManager**는 각 등록된 인증 모듈에서 모듈이 등록된 순서대로 <xref:System.Net.IAuthenticationModule.Authenticate%2A> 메서드를 호출합니다. **AuthenticationManager**는 **null**을 반환하지 않는 첫 번째 모듈을 사용하여 인증 프로세스를 수행합니다. 프로세스 세부 정보는 관련된 인증 모듈 형식에 따라 달라집니다.  
  
2.  인증 프로세스가 완료되면 인증 모듈은 <xref:System.Net.Authorization>을 인터넷 리소스에 액세스하는 데 필요한 정보가 포함된 **WebRequest**에 반환합니다.  
  
 일부 인증 체계에서는 리소스에 대한 요청을 먼저 만들지 않고 사용자를 인증할 수 있습니다. 응용 프로그램은 리소스에서 사용자를 사전 인증하여 서버에 대한 하나 이상의 왕복을 제거하는 방식으로 시간을 단축할 수 있습니다. 또는 나중에 사용자에게 더 빨리 응답할 수 있도록 프로그램 시작 중에 인증을 수행할 수 있습니다. 사전 인증을 사용하는 인증 체계는 <xref:System.Net.IAuthenticationModule.PreAuthenticate%2A> 속성을 **true**로 설정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [기본 인증 및 다이제스트 인증](../../../docs/framework/network-programming/basic-and-digest-authentication.md)  
 [NTLM 및 Kerberos 인증](../../../docs/framework/network-programming/ntlm-and-kerberos-authentication.md)  
 [네트워크 프로그래밍의 보안](../../../docs/framework/network-programming/security-in-network-programming.md)
