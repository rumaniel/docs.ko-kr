---
title: 전송 보안 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 00959326-aa9d-44d0-af61-54933d4adc7f
ms.openlocfilehash: 463d2fc374870661185a625a0b07a102aa54498c
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988619"
---
# <a name="transport-security-overview"></a>전송 보안 개요
WCF (Windows Communication Foundation)의 전송 보안 메커니즘은 사용 되는 바인딩 및 전송에 따라 달라 집니다. 예를 들어 <xref:System.ServiceModel.WSHttpBinding> 클래스를 사용할 경우 전송은 HTTP이며, 전송 보안을 위한 기본 메커니즘은 HTTPS라고 알려진 HTTP를 통한 SSL(Secure Sockets Layer)입니다. 이 항목에서는 WCF 시스템에서 제공 하는 바인딩에 사용 되는 주요 전송 보안 메커니즘에 대해 설명 합니다.  
  
> [!NOTE]
> .NET Framework 3.5 이상에서 SSL 보안을 사용 하는 경우 WCF 클라이언트는 인증서 저장소의 중간 인증서와 SSL 협상 중에 받은 중간 인증서를 모두 사용 하 여 서비스에서 인증서 체인 유효성 검사를 수행 합니다. 인증서. .NET Framework 3.0은 로컬 인증서 저장소에 설치된 중간 인증서만 사용합니다.  
  
> [!WARNING]
> 전송 보안이 사용되는 경우에는 <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=nameWithType> 속성이 덮어쓰일 수 있습니다. 이러한 상황이 발생 하지 않도록 하려면 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.PrincipalPermissionMode%2A?displayProperty=nameWithType> 를로 <xref:System.ServiceModel.Description.PrincipalPermissionMode.None?displayProperty=nameWithType>설정 합니다. <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>는 서비스 설명에 설정할 수 있는 서비스 동작입니다.  
  
## <a name="basichttpbinding"></a>BasicHttpBinding  
 기본적으로 <xref:System.ServiceModel.BasicHttpBinding> 클래스는 보안을 제공하지 않습니다. 이 바인딩은 보안을 구현하지 않는 웹 서비스 공급자와의 상호 운용성을 위해 디자인되었습니다. 하지만 <xref:System.ServiceModel.BasicHttpSecurity.Mode%2A> 속성을 <xref:System.ServiceModel.BasicHttpSecurityMode.None> 이외의 값으로 설정하여 보안으로 전환할 수 있습니다. 전송 보안을 사용하려면 속성을 <xref:System.ServiceModel.BasicHttpSecurityMode.Transport>로 설정합니다.  
  
### <a name="interoperation-with-iis"></a>IIS와의 상호 운용  
 <xref:System.ServiceModel.BasicHttpBinding> 클래스는 기존의 웹 서비스와 상호 운용하는 데 주로 사용되고, 이러한 서비스의 대부분은 IIS(인터넷 정보 서비스)에 의해 호스팅됩니다. 따라서 이 바인딩에 대한 전송 보안은 IIS 사이트와 매끄럽게 상호 운용하도록 디자인되었습니다. 이를 위해서는 보안 모드를<xref:System.ServiceModel.BasicHttpSecurityMode.Transport>로 설정한 다음 클라이언트 자격 증명 형식을 설정하면 됩니다. 자격 증명 형식 값은 IIS 디렉터리 보안 메커니즘에 해당됩니다. 다음 코드에서는 설정되는 모드와 Windows로 설정된 자격 증명 형식을 보여 줍니다. 이러한 구성은 클라이언트와 서버가 같은 Windows 도메인에 있는 경우에 사용할 수 있습니다.  
  
 [!code-csharp[c_ProgrammingSecurity#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#10)] 
 [!code-vb[c_ProgrammingSecurity#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#10)]  
  
 또는 다음 구성을 사용할 수도 있습니다.  
  
```xml  
<bindings>  
  <basicHttpBinding>  
    <binding name="SecurityByTransport">  
      <security mode="Transport">  
        <transport clientCredentialType="Windows" />  
       </security>  
     </binding>  
  </basicHttpBinding>  
</bindings>  
```  
  
 다음 단원에서는 기타 다른 클라이언트 자격 증명 형식에 대해 설명합니다.  
  
#### <a name="basic"></a>Basic  
 IIS의 기본 인증 방식입니다. 이 모드를 사용하려면 Windows 사용자 계정과 적절한 NTFS 파일 시스템 권한으로 IIS 서버를 구성해야 합니다. IIS 6.0에 대 한 자세한 내용은 [기본 인증 사용 및 영역 이름 구성](https://go.microsoft.com/fwlink/?LinkId=88592)을 참조 하세요. IIS 7.0에 대 한 자세한 내용은 [기본 인증 구성 (IIS 7)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772009(v=ws.10))을 참조 하세요.  
  
#### <a name="certificate"></a>Certificate  
 IIS에는 클라이언트가 인증서를 사용하여 로그온해야 하는 옵션이 있습니다. 또한 이 기능을 사용하면 IIS에서 클라이언트 인증서를 Windows 계정에 매핑할 수 있습니다. IIS 6.0에 대 한 자세한 내용은 [iis 6.0에서 클라이언트 인증서 사용](https://go.microsoft.com/fwlink/?LinkId=88594)을 참조 하십시오. IIS 7.0에 대 한 자세한 내용은 [iis 7에서 서버 인증서 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732230(v=ws.10))을 참조 하십시오.  
  
#### <a name="digest"></a>Digest  
 다이제스트 인증은 기본 인증과 비슷하지만 자격 증명을 일반 텍스트가 아닌 해시로 보낼 수 있는 이점이 있습니다. IIS 6.0에 대 한 자세한 내용은 [iis 6.0의 다이제스트 인증](https://go.microsoft.com/fwlink/?LinkID=88443)을 참조 하세요. IIS 7.0에 대 한 자세한 내용은 [다이제스트 인증 구성 (IIS 7)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754104(v=ws.10))을 참조 하세요.  
  
#### <a name="windows"></a>Windows  
 IIS의 Windows 통합 인증입니다. 이 값으로 설정하는 경우 도메인 컨트롤러가 Kerberos 프로토콜인 Windows 도메인에 서버가 있어야 합니다. 서버가 Kerberos 기반 도메인에 있지 않거나 Kerberos 시스템에 오류가 있는 경우에는 다음 단원에 설명되어 있는 NTLM(NT LAN Manager) 값을 사용할 수 있습니다. IIS 6.0에 대 한 자세한 내용은 [iis 6.0의 Windows 통합 인증](https://go.microsoft.com/fwlink/?LinkId=88597)을 참조 하세요. IIS 7.0에 대 한 자세한 내용은 [iis 7에서 서버 인증서 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732230(v=ws.10))을 참조 하십시오.
  
#### <a name="ntlm"></a>NTLM  
 Kerberos 프로토콜에 오류가 있는 경우 이를 통해 서버가 인증에 NTLM을 사용할 수 있습니다. IIS 6.0에서 IIS를 구성 하는 방법에 대 한 자세한 내용은 [NTLM 인증 강제](https://go.microsoft.com/fwlink/?LinkId=88598)적용을 참조 하세요. IIS 7.0의 경우 Windows 인증에 NTLM 인증이 포함 됩니다. 자세한 내용은 [IIS 7에서 서버 인증서 구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732230(v=ws.10))을 참조하십시오.
  
## <a name="wshttpbinding"></a>WsHttpBinding  
 <xref:System.ServiceModel.WSHttpBinding> 클래스는 WS-* 사양을 구현하는 서비스와 상호 운용하도록 디자인되었습니다. 이 바인딩의 전송 보안은 HTTP 또는 SSL(Secure Sockets Layer) over HTTP입니다. SSL을 사용 하는 WCF 응용 프로그램을 만들려면 IIS를 사용 하 여 응용 프로그램을 호스팅합니다. 또는 자체 호스팅 애플리케이션을 만들려면 HttpCfg.exe 도구를 사용하여 X.509 인증서를 컴퓨터의 특정 포트에 바인딩합니다. 포트 번호는 WCF 응용 프로그램의 일부로 끝점 주소로 지정 됩니다. 전송 모드 사용 시 엔드포인트 주소에 HTTPS 프로토콜이 포함되어야 하고, 그렇지 않으면 런타임에 예외가 throw됩니다. 자세한 내용은 [HTTP 전송 보안](../../../../docs/framework/wcf/feature-details/http-transport-security.md)을 참조 하세요.  
  
 클라이언트 인증의 경우 <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A> 클래스의 <xref:System.ServiceModel.HttpTransportSecurity> 속성을 <xref:System.ServiceModel.HttpClientCredentialType> 열거형 값 중 하나로 설정합니다. 열거형 값은 <xref:System.ServiceModel.BasicHttpBinding>에 대한 클라이언트 자격 증명 형식과 같으며 IIS 서비스와 호스팅되도록 디자인되었습니다.  
  
 다음 예제에서는 Windows 클라이언트 자격 증명 형식과 함께 사용되는 바인딩을 보여 줍니다.  
  
 [!code-csharp[c_ProgrammingSecurity#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#11)]
 [!code-vb[c_ProgrammingSecurity#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#11)]  
  
## <a name="wsdualhttpbinding"></a>WSDualHttpBinding  
 이 바인딩에서는 전송 수준 보안이 아닌 메시지 수준 보안만을 제공합니다.  
  
## <a name="nettcpbinding"></a>NetTcpBinding  
 <xref:System.ServiceModel.NetTcpBinding> 클래스는 메시지 전송에 TCP를 사용합니다. 전송 모드에 대한 보안은 TCP를 통한 TLS(전송 계층 보안) 구현을 통해 제공되며 TLS 구현은 운영 체제에 의해 제공됩니다.  
  
 다음 코드에서와 같이<xref:System.ServiceModel.TcpTransportSecurity.ClientCredentialType%2A> 클래스의 <xref:System.ServiceModel.TcpTransportSecurity> 속성을 <xref:System.ServiceModel.TcpClientCredentialType> 값 중 하나로 설정하여 클라이언트의 자격 증명 형식을 지정할 수도 있습니다.  
  
 [!code-csharp[c_ProgrammingSecurity#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#12)]
 [!code-vb[c_ProgrammingSecurity#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#12)]  
  
#### <a name="client"></a>클라이언트  
 클라이언트에서는 <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> 클래스의 <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential> 메서드를 사용하여 인증서를 지정해야 합니다.  
  
> [!NOTE]
> Windows 보안을 사용하는 경우 인증서는 필요하지 않습니다.  
  
 다음 코드에서는 인증서를 고유하게 식별하는 인증서의 지문을 사용합니다. 자세한 내용은 [인증서 작업](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)을 참조하세요.  
  
 [!code-csharp[c_ProgrammingSecurity#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#13)]
 [!code-vb[c_ProgrammingSecurity#13](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#13)]  
  
 또는 동작 섹션의 [ \<clientCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md) 요소를 사용 하 여 클라이언트의 구성에서 인증서를 지정 합니다.  
  
```xml  
<behaviors>  
  <behavior>  
   <clientCredentials>  
     <clientCertificate findValue= "101010101010101010101010101010000000000"   
      storeLocation="LocalMachine" storeName="My"   
      X509FindType="FindByThumbPrint"/>  
     </clientCertificate>  
   </clientCredentials>  
 </behavior>  
</behaviors>    
```  
  
## <a name="netnamedpipebinding"></a>NetNamedPipeBinding  
 <xref:System.ServiceModel.NetNamedPipeBinding> 클래스는 컴퓨터 내의 효율적 통신을 위해 디자인되었습니다. 명명된 파이프 채널을 동일한 네트워크에 있는 두 컴퓨터 간에 만들 수도 있지만, 이 클래스는 동일한 컴퓨터에서 실행되는 프로세스를 위해 만들어진 클래스입니다. 이 바인딩에서는 전송 수준 보안만을 제공합니다. 이 바인딩을 사용하는 애플리케이션을 만들려면 엔드포인트 주소에는 &quot;net.pipe&quot;가 엔드포인트 주소의 프로토콜로 포함되어야 합니다.  
  
## <a name="wsfederationhttpbinding"></a>WSFederationHttpBinding  
 이 바인딩에서는 전송 보안을 사용할 때 HTTPS라고도 하는 HTTP를 통한 SSL을 발급된 토큰(<xref:System.ServiceModel.WSFederationHttpSecurityMode.TransportWithMessageCredential>)과 함께 사용합니다. 페더레이션 응용 프로그램에 대 한 자세한 내용은 [페더레이션 및 발급 된 토큰](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)을 참조 하세요.  
  
## <a name="netpeertcpbinding"></a>NetPeerTcpBinding  
 <xref:System.ServiceModel.NetPeerTcpBinding> 클래스는 피어 투 피어 네트워킹 기능을 사용하는 효율적인 통신을 위해 디자인된 보안 전송입니다. 클래스 및 바인딩의 이름에서 알 수 있듯이 TCP가 프로토콜입니다. 보안 모드가 전송으로 설정되어 있는 경우 바인딩은 TCP를 통한 TLS를 구현합니다. 피어 투 피어 기능에 대 한 자세한 내용은 [피어 투 피어 네트워킹](../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md)을 참조 하세요.  
  
## <a name="msmqintegrationbinding-and-netmsmqbinding"></a>MsmqIntegrationBinding 및 NetMsmqBinding  
 메시지 큐 (이전에는 MSMQ 라고 함)를 사용한 전송 보안에 대 한 자세한 설명은 [전송 보안을 사용 하 여 메시지 보안](../../../../docs/framework/wcf/feature-details/securing-messages-using-transport-security.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [WCF 보안 프로그래밍](../../../../docs/framework/wcf/feature-details/programming-wcf-security.md)
