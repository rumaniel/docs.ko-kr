---
title: 서비스에 보안 설정
ms.date: 03/30/2017
helpviewer_keywords:
- configuration [WCF], securing services
- WCF security
- WCF, security
ms.assetid: f0ecc6f7-f4b5-42a4-9cb1-b02e28e26620
ms.openlocfilehash: b2ee61d6bad457918f1bd5006dfd7eaa27e46caa
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964169"
---
# <a name="securing-services"></a>서비스에 보안 설정
WCF (Windows Communication Foundation) 서비스의 보안은 전송 보안과 권한 부여의 두 가지 주요 요구 사항으로 구성 됩니다. (보안 이벤트 감사의 세 번째 요구 사항은 [감사](../../../docs/framework/wcf/feature-details/auditing-security-events.md)에 설명 되어 있습니다.) 간단히 말해서 전송 보안은 인증(서비스와 클라이언트 모두에 대해 ID 확인), 기밀성(메시지 암호화) 및 무결성(변조 확인을 위한 디지털 서명)을 포함합니다. 권한 부여는 리소스에 대한 액세스 제어입니다. 예를 들어, 권한 있는 사용자에게만 파일 읽기를 허용합니다. WCF의 기능을 사용 하면 두 가지 주요 요구 사항이 쉽게 구현 됩니다.  
  
 <xref:System.ServiceModel.BasicHttpBinding> 클래스 ( [ 또는basicHttpBinding>요소구성의경우)를제외하고미리정의된모든바인딩에대해기본적으로전송보안이사용됩니다.\<](../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md) 이 단원의 항목에서는 IIS(인터넷 정보 서비스)에 호스트되는 인트라넷 서비스에 대한 전송 보안 및 권한 부여 구현, IIS에 호스트되는 서비스에 대한 전송 보안 및 권한 부여 구현의 두 가지 기본 시나리오에 대해 설명합니다.  
  
> [!NOTE]
> Windows XP Home은 Windows 인증을 지원하지 않습니다. 따라서 해당 시스템에서 서비스를 실행하지 않아야 합니다.  
  
## <a name="security-basics"></a>보안 기본 사항  
 보안은 *자격 증명*에 의존합니다. 자격 증명은 엔터티가 요청 대상이 맞음을 증명합니다. *엔터티* 는 개인, 소프트웨어 프로세스, 회사 또는 권한이 부여 될 수 있는 모든 것이 될 수 있습니다. 예를 들어 서비스의 클라이언트는 *id* *클레임* 을 만들고 자격 증명은 어떤 식으로든 클레임을 증명 합니다. 일반 시나리오에서 자격 증명 교환이 발생합니다. 첫째, 서비스에서 ID 클레임을 만들어 자격 증명을 사용하여 클라이언트에게 증명합니다. 클라이언트는 ID 클레임을 만들고 서비스에 자격 증명을 제시합니다. 두 당사자 모두가 서로의 자격 증명을 신뢰하는 경우 모든 메시지가 기밀하게 교환되고 모든 메시지에 서명하여 무결성을 보호하는 *보안 컨텍스트* 를 설정할 수 있습니다. 서비스에서는 클라이언트의 ID를 설정한 후 자격 증명의 클레임과 그룹의 *역할* 또는 *멤버 자격* 을 일치시킬 수 있습니다. 어느 경우든 클라이언트가 속하는 그룹 또는 역할을 사용하여 서비스는 클라이언트에 역할 또는 그룹 권한을 기반으로 제한된 작업을 수행할 수 있는 *권한을 부여* 합니다.  
  
## <a name="windows-security-mechanisms"></a>Windows 보안 메커니즘  
 클라이언트와 서비스 컴퓨터가 모두 네트워크에 로그온해야 하는 Windows 도메인에 있는 경우 Windows 인프라가 자격 증명을 제공합니다. 이러한 경우 컴퓨터 사용자가 네트워크에 로그온하면 자격 증명이 설정됩니다. 네트워크의 모든 사용자와 모든 컴퓨터가 신뢰할 수 있는 사용자 및 컴퓨터 집합에 속하는지 확인해야 합니다. Windows 시스템에서는 그러한 모든 사용자와 컴퓨터를 *보안 주체*라고도 합니다.  
  
 *Kerberos* 컨트롤러를 기반으로 하는 Windows 도메인에서 Kerberos 컨트롤러는 각 보안 주체에 티켓을 부여하는 방법을 사용합니다. 컨트롤러가 부여하는 티켓은 시스템의 다른 티켓 부여자가 신뢰합니다. 엔터티가 일부 작업을 수행하거나 *리소스* (예: 컴퓨터의 파일 또는 디렉터리)에 액세스하려고 할 때마다 티켓의 유효성을 검사하여 유효하면 주체에 작업을 위한 다른 티켓이 부여됩니다. 이 티켓 부여 방법은 모든 작업에 대해 주체를 유효성 검사하는 대체 방법보다 더 효율적입니다.  
  
 Windows 도메인에 사용된 이전의 보안되지 않은 메커니즘은 NTLM(NT LAN Manager)입니다. Kerberos를 사용할 수 없는 경우(일반적으로 Windows 도메인 외부의 작업 그룹의 경우), NTLM을 대체 방법으로 사용할 수 있습니다. NTLM을 IIS에 대한 보안 옵션으로 사용할 수도 있습니다.  
  
 Windows 시스템에서 각 컴퓨터와 사용자를 역할 및 그룹에 할당하여 권한을 부여합니다. 예를 들어, *관리자*역할에 속하는 사용자 또는 사용자 그룹이 모든 Windows 컴퓨터를 설정하고 제어해야 합니다. 다른 역할은 훨씬 제한된 권한을 가진 *사용자*역할이 있습니다. 역할 이외에 사용자는 그룹에 할당됩니다. 그룹을 사용하면 여러 사용자가 동일한 역할로 작업을 수행할 수 있습니다. 따라서 실제로 사용자를 그룹에 할당하여 Windows 컴퓨터를 관리합니다. 예를 들어, 여러 사용자를 컴퓨터 사용자 그룹에 할당하고 훨씬 제한된 사용자 집합을 관리자 그룹에 할당할 수 있습니다. 로컬 컴퓨터에서 관리자는 새 그룹을 만든 후 다른 사용자(또는 다른 그룹)를 해당 그룹에 할당할 수도 있습니다.  
  
 Windows를 실행하는 컴퓨터에서 디렉터리에 있는 모든 폴더를 보호할 수 있습니다. 즉, 폴더를 선택하고 파일에 액세스할 수 있는 사용자를 제어하고, 해당 사용자가 파일을 복사, 변경(최대 권한이 부여된 경우) 또는 삭제할 수 있는지 여부와 파일을 폴더에 추가할 수 있는지 여부를 제어할 수 있습니다. 이를 액세스 제어라고 하며 여기에 사용되는 메커니즘을 ACL(액세스 제어 목록)이라고 합니다. ACL을 만들 때 도메인의 개별 멤버와 그룹에 액세스 권한을 할당할 수 있습니다.  
  
 WCF 인프라는 이러한 Windows 보안 메커니즘을 사용 하도록 디자인 되었습니다. 따라서 인트라넷에 배포되고 해당 클라이언트가 Windows 도메인의 멤버로 제한되는 서비스를 만들면 보안이 쉽게 구현됩니다. 유효한 사용자만 도메인에 로그온할 수 있습니다. 사용자는 로그온한 후 Kerberos 컨트롤러를 사용하여 다른 컴퓨터 또는 애플리케이션에 보안 컨텍스트를 설정할 수 있습니다. 로컬 컴퓨터에서 그룹을 쉽게 만들 수 있으며, 특정 폴더를 보호하면 해당 그룹을 사용하여 컴퓨터에서 액세스 권한을 할당할 수 있습니다.  
  
## <a name="implementing-windows-security-on-intranet-services"></a>인트라넷 서비스에서 Windows 보안 구현  
 Windows 도메인에서 단독으로 실행되는 애플리케이션을 보안하려면 <xref:System.ServiceModel.WSHttpBinding> 또는 <xref:System.ServiceModel.NetTcpBinding> 바인딩의 기본 보안 설정을 사용할 수 있습니다. 기본적으로 동일한 Windows 도메인의 모든 사용자가 WCF 서비스에 액세스할 수 있습니다. 이러한 사용자는 네트워크에 로그온되어 있기 때문에 신뢰됩니다. 서비스와 클라이언트 사이의 메시지는 기밀성을 위해 암호화되고 무결성을 위해 서명됩니다. Windows 보안 [을 사용 하는 서비스를 만드는 방법에 대 한 자세한 내용은 방법: Windows 자격 증명](../../../docs/framework/wcf/how-to-secure-a-service-with-windows-credentials.md)을 사용 하 여 서비스를 보호 합니다.  
  
### <a name="authorization-using-the-principalpermissionattribute-class"></a>PrincipalPermissionAttribute 클래스를 사용하여 권한 부여  
 컴퓨터에서 리소스 액세스를 제한해야 하는 경우에 가장 쉬운 방법은 <xref:System.Security.Permissions.PrincipalPermissionAttribute> 클래스를 사용하는 것입니다. 이 특성을 사용하면 사용자가 지정된 Windows 그룹이나 역할에 속하는지 또는 특정 사용자인지를 확인하여 서비스 작업 호출을 제한할 수 있습니다. 자세한 내용은 [방법: PrincipalPermissionAttribute 클래스](../../../docs/framework/wcf/how-to-restrict-access-with-the-principalpermissionattribute-class.md)를 사용 하 여 액세스를 제한 합니다.  
  
### <a name="impersonation"></a>가장  
 가장은 리소스에 대한 액세스를 제어하는 데 사용할 수 있는 다른 메커니즘입니다. 기본적으로 IIS가 호스트하는 서비스는 ASPNET 계정의 ID로 실행됩니다. ASPNET 계정은 권한이 있는 리소스에만 액세스할 수 있습니다. ASPNET 서비스 계정을 제외하도록 폴더에 대한 ACL을 설정하고 특정한 다른 ID에 해당 폴더에 대한 액세스를 허용할 수 있습니다. ASPNET 계정에서 폴더에 액세스할 수 없는 경우 사용자에게 폴더에 대한 액세스를 허용하는 방법이 문제가 됩니다. 이 경우 가장을 사용하면 됩니다. 가장을 사용하면 서비스에서 클라이언트의 자격 증명을 사용하여 특정 리소스에 액세스할 수 있습니다. 다른 예로는 특정 사용자에게만 권한이 있는 SQL Server 데이터베이스에 액세스하는 경우가 있습니다. 가장을 [사용 하는 방법에 대 한 자세한 내용은 방법: 서비스](../../../docs/framework/wcf/how-to-impersonate-a-client-on-a-service.md) 및 [위임 및 가장](../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)에 대 한 클라이언트를 가장 합니다.  
  
## <a name="security-on-the-internet"></a>인터넷 보안  
 인터넷 보안은 인트라넷 보안과 동일한 요구 사항으로 구성됩니다. 서비스는 자격 증명을 제공하여 인증서를 증명하고, 클라이언트는 서비스에 대한 ID를 증명해야 합니다. 클라이언트의 ID가 증명되면 서비스는 클라이언트가 리소스에 대해 갖는 액세스 권한을 제어할 수 있습니다. 그러나 인터넷의 특성이 서로 다르기 때문에 제공되는 자격 증명이 Windows 도메인에 사용된 자격 증명과 다릅니다. Kerberos 컨트롤러는 자격 증명에 대한 티켓을 사용하여 도메인에서 사용자 인증을 처리하지만, 인터넷에서는 서비스와 클라이언트가 다양한 방법 중 하나를 사용하여 자격 증명을 제공합니다. 그러나이 항목은 인터넷에서 액세스할 수 있는 WCF 서비스를 만들 수 있도록 하는 일반적인 방법을 제시 하는 것입니다.  
  
### <a name="using-iis-and-aspnet"></a>IIS 및 ASP.NET 사용  
 인터넷 보안 요구 사항과 문제 해결 메커니즘은 새로운 기능이 아닙니다. IIS는 Microsoft의 인터넷 웹 서버 이며 이러한 문제를 해결 하는 많은 보안 기능을 제공 합니다. 또한 ASP.NET에는 WCF 서비스에서 사용할 수 있는 보안 기능이 포함 되어 있습니다. 이러한 보안 기능을 활용 하려면 IIS에서 WCF 서비스를 호스팅합니다.  
  
#### <a name="using-aspnet-membership-and-role-providers"></a>ASP.NET 멤버 자격 및 역할 공급자 사용  
 ASP.NET에는 멤버 자격 및 역할 공급자가 포함되어 있습니다. 공급자는 호출자를 인증하는 사용자 이름/암호 쌍으로 구성된 데이터베이스이며 각 호출자의 액세스 권한을 지정할 수 있습니다. WCF를 사용 하면 구성을 통해 기존 멤버 자격 및 역할 공급자를 쉽게 사용할 수 있습니다. 이 내용을 설명하는 샘플 애플리케이션에 대해서는 [Membership and Role Provider](../../../docs/framework/wcf/samples/membership-and-role-provider.md) 샘플을 참조하세요.  
  
### <a name="credentials-used-by-iis"></a>IIS에 사용되는 자격 증명  
 Kerberos 컨트롤러에서 지원하는 Windows 도메인과 달리 인터넷은 시간에 관계없이 로그인하는 수백만 명의 사용자를 단일의 컨트롤러에서 관리할 수 없는 환경입니다. 대신 대부분의 인터넷에는 Secure Sockets Layer(또는 SSL) 인증서라고도 하는 X.509 형태의 자격 증명이 있습니다. 이러한 인증서는 일반적으로 *인증 기관*에 의해 발급되며, 인증 기관은 인증서의 신뢰성과 발급 받은 사람을 보증하는 타사일 수 있습니다. 인터넷에서 서비스를 노출하려면 그런 신뢰할 수 있는 인증서를 제공하여 서비스를 인증해야 합니다.  
  
 여기서 인증서를 어떻게 발급 받는지에 대한 질문이 발생합니다. Authenticode 또는 VeriSign과 같은 타사 인증 기관으로 이동하여 서비스를 배포할 준비가 되면 서비스에 대한 인증서를 구매합니다. 그러나 WCF를 사용 하는 개발 단계에서 아직 인증서를 구매 하기 위해 커밋할 준비가 되지 않은 경우 프로덕션 배포를 시뮬레이션 하는 데 사용할 수 있는 x.509 인증서를 만드는 도구와 기술이 있습니다. 자세한 내용은 [Working with Certificates](../../../docs/framework/wcf/feature-details/working-with-certificates.md)합니다.  
  
## <a name="security-modes"></a>보안 모드  
 WCF 보안 프로그래밍에는 몇 가지 중요 한 결정 사항이 있습니다. 가장 기본적인 사항 중 하나로 *보안 모드*를 선택합니다. *전송 모드* 와 *메시지 모드*의 두 가지 주요 보안 모드가 있습니다.  
  
 두 주요 모드의 의미를 결합하는 세 번째 모드는 *메시지 자격 증명을 사용한 전송 모드*입니다.  
  
 아래에 설명한 것처럼 보안 모드에 따라 메시지가 보안되는 방법이 결정되고, 모드별로 장단점이 있습니다. 보안 모드 [를 설정 하는 방법에 대 한 자세한 내용은 방법: 보안 모드](../../../docs/framework/wcf/how-to-set-the-security-mode.md)를 설정 합니다.  
  
#### <a name="transport-mode"></a>전송 모드  
 네트워크와 애플리케이션 사이에는 여러 계층이 있습니다. 그 중 하나로 엔드포인트 간의 메시지 전송을 관리하는 *전송* 계층 이 있습니다. 현재는 WCF가 메시지 전송을 안전 하 게 보호할 수 있는 여러 전송 프로토콜을 사용 한다는 것을 이해 하는 데만 필요 합니다. 전송에 대 한 자세한 내용은 [전송](../../../docs/framework/wcf/feature-details/transports.md)을 참조 하세요.  
  
 일반적으로 사용되는 프로토콜은 HTTP 및 TCP입니다. 이러한 각 프로토콜은 프로토콜별로 특정한 메커니즘을 사용하여 메시지 전송을 보안할 수 있습니다. 예를 들어, HTTP 프로토콜은 SSL over HTTP(약어로 "HTTPS")를 사용하여 보안됩니다. 따라서 보안을 위한 전송 모드를 선택하면 해당 프로토콜에 명시된 메커니즘을 사용하는 것입니다. 예를 들어, <xref:System.ServiceModel.WSHttpBinding> 클래스를 선택하고 보안 모드를 전송으로 설정하면 HTTPS(SSL over HTTP)를 보안 메커니즘으로 선택한 것입니다. 전송 모드는 비교적 낮은 수준에서 보안이 통합되므로 메시지 모드보다 더 효율적이라는 이점이 있습니다. 전송 모드를 사용할 경우 전송 사양에 따라 보안 메커니즘을 구현해야 하므로, 메시지가 지점 간에만 전송을 통해 안전하게 전달될 수 있습니다.  
  
#### <a name="message-mode"></a>메시지 모드  
 반면에 메시지 모드에서는 보안 데이터를 모든 메시지에 포함시켜 보안을 제공합니다. XML 및 SOAP 보안 헤더를 사용하여 메시지의 무결성과 기밀성을 확인하는 데 필요한 자격 증명과 기타 데이터를 모든 메시지에 포함시킵니다. 모든 메시지에는 보안 데이터가 포함되어 있으므로, 각 메시지가 개별적으로 처리되어야 하기 때문에 성능이 감소됩니다. 전송 모드에서 전송 계층을 보안한 후에는 모든 메시지가 자유롭게 전달됩니다. 그러나 메시지 보안은 전송 보안보다 더 유연하다는 한 가지 이점이 있습니다. 즉, 전송에 의해 보안 요구 사항이 결정되지 않습니다. 모든 형식의 클라이언트 자격 증명을 사용하여 메시지를 보안할 수 있습니다. 전송 모드에서는 전송 프로토콜에 따라 사용 가능한 클라이언트 자격 증명 형식이 결정됩니다.  
  
#### <a name="transport-with-message-credentials"></a>메시지 자격 증명을 사용한 전송  
 세 번째 모드에서는 전송 보안과 메시지 보안의 장점을 결합합니다. 이 모드에서는 전송 보안을 사용하여 모든 메시지의 기밀성과 무결성을 효과적으로 확인합니다. 동시에 모든 메시지에는 메시지를 인증할 수 있는 자격 증명 데이터가 포함되어 있습니다. 인증을 사용하여 권한 부여를 구현할 수도 있습니다. 발신자를 인증하여 발신자의 ID에 따라 리소스에 대한 액세스를 허용하거나 거부할 수 있습니다.  
  
## <a name="specifying-the-client-credential-type-and-credential-value"></a>클라이언트 자격 증명 형식 및 자격 증명 값 지정  
 보안 모드를 선택한 후 클라이언트 자격 증명 형식을 지정할 수도 있습니다. 클라이언트 자격 증명 형식은 클라이언트가 서버에 자신을 인증하는 데 사용해야 하는 형식을 지정합니다.  
  
 모든 시나리오에 클라이언트 자격 증명 형식이 필요한 것은 아닙니다. HTTPS(SSL over HTTP)를 사용하여 서비스가 클라이언트에 자체 인증합니다. 이 인증의 일부로 *협상*이라는 프로세스에서 서비스의 인증서를 클라이언트에 보냅니다 SSL 보안 전송에서는 모든 메시지가 기밀 상태로 유지됩니다.  
  
 클라이언트를 인증해야 하는 서비스를 만들 경우 선택한 전송 및 모드에 따라 클라이언트 자격 증명 형식을 다르게 선택합니다. 예를 들어, HTTP 전송을 사용하고 전송 모드를 선택한 경우 기본, 다이제스트 등과 같은 다양한 선택 옵션이 제공됩니다. 이러한 자격 증명 형식에 대 한 자세한 내용은 [HTTP 인증 이해](../../../docs/framework/wcf/feature-details/understanding-http-authentication.md)를 참조 하세요.  
  
 Windows 도메인에서 네트워크의 다른 사용자만 사용할 수 있는 서비스를 만들 경우 Windows 클라이언트 자격 증명 형식을 사용하는 것이 가장 간편합니다. 서비스에 인증서를 제공해야 할 수도 있습니다. 이는 [방법: 클라이언트 자격 증명 값](../../../docs/framework/wcf/how-to-specify-client-credential-values.md)을 지정 합니다.  
  
#### <a name="credential-values"></a>자격 증명 값  
 *자격 증명 값* 은 서비스에 사용되는 실제 자격 증명입니다. 자격 증명 형식을 지정한 경우 실제 자격 증명을 사용하여 서비스를 구성해야 할 수도 있습니다. Windows를 선택하고 서비스가 Windows 도메인에서 실행되는 경우에는 실제 자격 증명 값을 지정하지 않습니다.  
  
## <a name="identity"></a>클레임  
 WCF에서 용어 *id* 는 서버와 클라이언트에서 서로 다른 의미를 갖습니다. 간략하게 말해서 서비스를 실행할 때 ID는 인증 후에 보안 컨텍스트에 할당됩니다. 실제 ID를 보려면 <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> 클래스의 <xref:System.ServiceModel.ServiceSecurityContext.PrimaryIdentity%2A> 및 <xref:System.ServiceModel.ServiceSecurityContext> 속성을 확인합니다. 자세한 내용은 [방법: 보안 컨텍스트](../../../docs/framework/wcf/how-to-examine-the-security-context.md)를 검사 합니다.  
  
 반대로 클라이언트에서는 ID가 서비스의 유효성을 검사하는 데 사용됩니다. 디자인 타임에 클라이언트 개발자는 [ \<id >](../../../docs/framework/configure-apps/file-schema/wcf/identity.md) 요소를 서비스에서 가져온 값으로 설정할 수 있습니다. 런타임에 클라이언트는 서비스의 실제 ID와 비교하여 요소 값을 확인합니다. 확인에 실패하면 클라이언트는 통신을 종료합니다. 값은 서비스가 특정 사용자의 ID로 실행되는 경우 UPN(User Principal Name)이고, 서비스가 컴퓨터 계정에서 실행되는 경우 SPN(서비스 사용자 이름)입니다. 자세한 내용은 [서비스 Id 및 인증](../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)합니다. 자격 증명은 인증서이거나 인증서를 식별하는 인증서에 있는 필드일 수 있습니다.  
  
## <a name="protection-levels"></a>보호 수준  
 `ProtectionLevel` 속성은 여러 특성 클래스(예: <xref:System.ServiceModel.ServiceContractAttribute> 및 <xref:System.ServiceModel.OperationContractAttribute> 클래스)에서 발생됩니다. 보호 수준은 서비스를 지원하는 메시지(또는 메시지 부분)가 서명되어 있는지, 서명 및 암호화되어 있는지 또는 서명이나 암호화 없이 보내졌는지를 지정하는 값입니다. 속성에 대 한 자세한 내용은 [보호 수준 이해](../../../docs/framework/wcf/understanding-protection-level.md)및 프로그래밍 예제 [를 참조 하십시오. 방법: ProtectionLevel 속성](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md)을 설정 합니다. 컨텍스트를 사용 하 `ProtectionLevel` 여 서비스 계약을 디자인 하는 방법에 대 한 자세한 내용은 [서비스 계약 디자인](../../../docs/framework/wcf/designing-service-contracts.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel>
- <xref:System.ServiceModel.Description.ServiceCredentials>
- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
- [서비스 ID 및 인증](../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)
- [보호 수준 이해](../../../docs/framework/wcf/understanding-protection-level.md)
- [위임 및 가장](../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)
- [서비스 계약 디자인](../../../docs/framework/wcf/designing-service-contracts.md)
- [보안](../../../docs/framework/wcf/feature-details/security.md)
- [보안 개요](../../../docs/framework/wcf/feature-details/security-overview.md)
- [방법: ProtectionLevel 속성 설정](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md)
- [방법: Windows 자격 증명을 사용 하 여 서비스 보호](../../../docs/framework/wcf/how-to-secure-a-service-with-windows-credentials.md)
- [방법: 보안 모드 설정](../../../docs/framework/wcf/how-to-set-the-security-mode.md)
- [방법: 클라이언트 자격 증명 형식 지정](../../../docs/framework/wcf/how-to-specify-the-client-credential-type.md)
- [방법: PrincipalPermissionAttribute 클래스를 사용 하 여 액세스 제한](../../../docs/framework/wcf/how-to-restrict-access-with-the-principalpermissionattribute-class.md)
- [방법: 서비스에서 클라이언트 가장](../../../docs/framework/wcf/how-to-impersonate-a-client-on-a-service.md)
- [방법: 보안 컨텍스트 검사](../../../docs/framework/wcf/how-to-examine-the-security-context.md)
