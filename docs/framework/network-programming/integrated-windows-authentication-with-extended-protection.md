---
title: 확장된 보호를 사용하는 Windows 통합 인증
ms.date: 03/30/2017
ms.assetid: 81731998-d5e7-49e4-ad38-c8e6d01689d0
ms.openlocfilehash: e07bc903a60dfff5e9caaf93f9c2bfd579541a96
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50189708"
---
# <a name="integrated-windows-authentication-with-extended-protection"></a>확장된 보호를 사용하는 Windows 통합 인증
<xref:System.Net.HttpWebRequest>, <xref:System.Net.HttpListener>, <xref:System.Net.Mail.SmtpClient>, <xref:System.Net.Security.SslStream>, <xref:System.Net.Security.NegotiateStream>, 그리고 <xref:System.Net> 및 관련 네임스페이스의 관련 클래스에 의해 Windows 통합 인증이 처리되는 방식에 영향을 미치는 기능이 향상되었습니다. 보안을 강화하기 위한 확장된 보호에 대한 지원이 추가되었습니다.  
  
 이러한 변경 내용은 이러한 클래스를 사용하여 Windows 통합 인증이 사용되는 경우 웹 요청을 만들고 응답을 수신하는 응용 프로그램에 영향을 미칠 수 있습니다. 이 변경 내용은 Windows 통합 인증을 사용하도록 구성된 웹 서버 및 클라이언트 응용 프로그램에 영향을 미칠 수도 있습니다.  
  
 이러한 변경 내용은 이러한 클래스를 사용하여 Windows 통합 인증이 사용되는 경우 다른 형식의 요청을 만들고 응답을 수신하는 응용 프로그램에 영향을 미칠 수도 있습니다.  
  
 확장된 보호를 지원하기 위한 변경 내용은 Windows 7 및 Windows Server 2008 R2의 응용 프로그램에만 사용할 수 있습니다. 확장된 보호 기능은 이전 버전의 Windows에서 사용할 수 없습니다.  
  
## <a name="overview"></a>개요  
 Windows 통합 인증의 디자인을 사용하면 일부 자격 증명 시도 응답이 유니버설이 될 수 있으므로 다시 사용되거나 전달될 수 있습니다. 시도 응답은 대상 관련 정보를 사용하거나 오히려 일부 채널 관련 정보를 사용하여 최소한으로 생성되어야 합니다. 그런 다음 서비스가 확장된 보호를 제공하여 자격 증명 시도 응답에 SPN(서비스 사용자 이름) 같은 서비스 관련 정보가 포함되어 있는지 확인할 수 있습니다. 자격 증명 교환에 이 정보가 포함되면 서비스는 부적절하게 사용되었을 수 있는 자격 증명 시도 응답의 악의적인 사용을 더 효과적으로 방지할 수 있습니다.  
  
 확장된 보호 디자인은 인증 릴레이 공격을 완화하도록 디자인된 인증 프로토콜의 향상된 기능입니다. 이 디자인은 채널 및 서비스 바인딩 정보의 개념을 기반으로 합니다.  
  
 전체 목표는 다음과 같습니다.  
  
1.  클라이언트가 확장된 보호를 지원하도록 업데이트된 경우 응용 프로그램은 모든 지원되는 인증 프로토콜에 채널 바인딩 및 서비스 바인딩 정보를 제공해야 합니다. 바인딩할 채널(TLS)이 있는 경우 채널 바인딩 정보만 제공될 수 있습니다. 서비스 바인딩 정보는 항상 제공되어야 합니다.  
  
2.  제대로 구성된 업데이트된 서버는 클라이언트 인증 토큰 내에 있을 경우 채널 및 서비스 바인딩 정보를 확인하고 채널 바인딩이 일치하지 않을 경우 인증 시도를 거부할 수 있습니다. 배포 시나리오에 따라 서버는 채널 바인딩 또는 서비스 바인딩을 확인하거나 두 바인딩을 모두 확인할 수 있습니다.  
  
3.  업데이트된 서버에는 정책에 따라 채널 바인딩 정보가 포함되지 않은 하위 수준 클라이언트 요청을 허용하거나 거부할 수 있습니다.  
  
 확장된 보호에서 사용되는 정보는 다음 두 부분 중 하나 또는 두 개로 구성됩니다.  
  
1.  채널 바인딩 토큰 또는 CBT.  
  
2.  SPN(서비스 사용자 이름) 형식의 서비스 바인딩 정보.  
  
 서비스 바인딩 정보는 특정 서비스 엔드포인트에 대해 인증하고자 하는 클라이언트의 의도를 나타냅니다. 다음 속성을 사용하여 클라이언트에서 서버로 전달합니다.  
  
-   분명한 텍스트 형식으로 클라이언트 인증을 수행하는 서버에서 SPN 값을 사용할 수 있어야 합니다.  
  
-   SPN 값은 공용입니다.  
  
-   메시지 가로채기(man-in-the-middle) 공격이 값을 삽입, 제거 또는 수정할 수 없도록 SPN은 이동 중에 암호로 보호되어야 합니다.  
  
 CBT는 내부 클라이언트 인증 채널을 통해 대화에 연결(바인딩)하는 데 사용되는 외부 보안 채널(예: TLS)의 속성입니다. CBT에는 다음 속성이 있어야 합니다(IETF RFC 5056에서도 정의됨).  
  
-   외부 채널이 있는 경우 CBT 값은 대화의 클라이언트 및 서버 쪽에서 개별적으로 도착하는 외부 채널 또는 서버 엔드포인트를 식별하는 속성이어야 합니다.  
  
-   클라이언트에서 보낸 CBT의 값은 공격자가 영향을 미칠 수 있는 것이 아니어야 합니다.  
  
-   CBT 값의 기밀성은 보장되지 않습니다. 그러나 이것은 서비스 바인딩 및 채널 바인딩 정보의 값이 항상 인증을 수행하는 서버를 제외한 다른 서버에서 검사될 수 있음을 의미하지 않습니다. CBT를 전달하는 프로토콜이 값을 암호화 중일 수 있기 때문입니다.  
  
-   공격자가 값을 삽입, 제거 또는 수정할 수 없도록 CBT는 이동 중에 무결성이 암호로 보호되어야 합니다.  
  
 채널 바인딩은 조작 방지 방식으로 SPN 및 CBT를 서버에 전송하는 클라이언트에서 수행됩니다. 서버는 정책에 따라 채널 바인딩 정보의 유효성을 검사하고 의도된 대상인지 확신할 수 없는 인증 시도를 거부합니다. 이 방식으로 두 개의 채널이 함께 암호로 바인딩됩니다.  
  
 기존 클라이언트 및 응용 프로그램과의 호환성을 유지하기 위해 아직 확장된 보호를 지원하지 않는 클라이언트의 인증 시도를 허용하도록 서버를 구성할 수 있습니다. 이것을 “완전 강화” 구성에 대비되는 “부분 강화” 구성이라고 합니다.  
  
 <xref:System.Net> 및 <xref:System.Net.Security> 네임스페이스의 여러 구성 요소는 호출하는 응용 프로그램 대신 Windows 통합 인증을 수행합니다. 이 섹션에서는 Windows 통합 인증 사용에 확장된 보호를 추가하기 위한 System.Net 구성 요소의 변경 내용을 설명합니다.  
  
 확장된 보호는 현재 Windows 7에서 지원됩니다. 응용 프로그램이 운영 체제에서 확장된 보호를 지원하는지 확인할 수 있는 메커니즘이 제공됩니다.  
  
## <a name="changes-to-support-extended-protection"></a>확장된 보호를 지원하기 위한 변경 내용  
 Windows 통합 인증과 함께 사용되는 인증 프로세스는 일반적으로 사용되는 인증 프로토콜에 따라 대상 컴퓨터에서 실행되고 다시 클라이언트 컴퓨터로 전송되는 시도를 포함합니다. 확장된 보호는 이 인증 프로세스에 새로운 기능을 추가합니다.  
  
 <xref:System.Security.Authentication.ExtendedProtection> 네임스페이스는 응용 프로그램에 대해 확장된 보호를 사용하는 인증을 지원합니다. 이 네임스페이스의 <xref:System.Security.Authentication.ExtendedProtection.ChannelBinding> 클래스는 채널 바인딩을 나타냅니다. 이 네임스페이스의 <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy> 클래스는 들어오는 클라이언트 연결을 확인하기 위해 서버에서 사용되는 확장된 보호 정책을 나타냅니다. 기타 클래스 멤버는 확장된 보호와 함께 사용됩니다.  
  
 서버 응용 프로그램의 경우 이러한 클래스에는 다음이 포함됩니다.  
  
 다음 요소가 포함된 <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy>:  
  
-   운영 체제에서 확장된 보호를 사용하는 Windows 통합 인증을 지원하는지 여부를 나타내는 <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy.OSSupportsExtendedProtection%2A> 속성.  
  
-   확장된 보호 정책을 적용할 시기를 나타내는 <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement> 값입니다.  
  
-   배포 시나리오를 나타내는 <xref:System.Security.Authentication.ExtendedProtection.ProtectionScenario> 값. 이 값은 확장된 보호를 확인하는 방법에 영향을 줍니다.  
  
-   인증의 의도된 대상인 클라이언트 제공 SPN과 일치하는지 확인하는 데 사용되는 사용자 지정 SPN 목록이 포함된 선택적 <xref:System.Security.Authentication.ExtendedProtection.ServiceNameCollection>.  
  
-   유효성 검사에 사용할 사용자 지정 채널 바인딩이 포함된 선택적 <xref:System.Security.Authentication.ExtendedProtection.ChannelBinding>. 이 시나리오는 일반적인 경우가 아닙니다.  
  
 <xref:System.Security.Authentication.ExtendedProtection.Configuration> 네임스페이스는 응용 프로그램의 확장된 보호를 사용하여 인증 구성을 지원합니다.  
  
 기존 <xref:System.Net> 네임스페이스에서 확장된 보호를 지원하기 위해 다양한 기능이 변경되었습니다. 변경 내용은 다음과 같습니다.  
  
-   <xref:System.Net> 네임스페이스에 전송 컨텍스트를 나타내는 새로운 <xref:System.Net.TransportContext> 클래스가 추가되었습니다.  
  
-   클라이언트 응용 프로그램에 대한 확장된 보호를 지원하기 위해 <xref:System.Net.TransportContext>를 검색할 수 있는 <xref:System.Net.HttpWebRequest> 클래스의 새로운 <xref:System.Net.HttpWebRequest.EndGetRequestStream%2A> 및 <xref:System.Net.HttpWebRequest.GetRequestStream%2A> 오버로드 메서드가 추가되었습니다.  
  
-   서버 응용 프로그램을 지원하기 위해 <xref:System.Net.HttpListener> 및 <xref:System.Net.HttpListenerRequest> 클래스가 추가되었습니다.  
  
 기존 <xref:System.Net.Mail> 네임스페이스에서 SMTP 클라이언트 응용 프로그램에 대한 확장된 보호를 지원하기 위해 기능이 다음과 같이 변경되었습니다.  
  
-   SMTP 클라이언트 응용 프로그램에 대한 확장된 보호를 사용할 때 인증에 사용할 SPN을 나타내는 <xref:System.Net.Mail.SmtpClient> 클래스의 <xref:System.Net.Mail.SmtpClient.TargetName%2A> 속성이 추가되었습니다.  
  
 기존 <xref:System.Net.Security> 네임스페이스에서 확장된 보호를 지원하기 위해 다양한 기능이 변경되었습니다. 변경 내용은 다음과 같습니다.  
  
-   클라이언트 응용 프로그램에 대한 확장된 보호를 지원하기 위해 CBT를 전달할 수 있는 <xref:System.Net.Security.NegotiateStream> 클래스의 새로운 <xref:System.Net.Security.NegotiateStream.BeginAuthenticateAsClient%2A> 및 <xref:System.Net.Security.NegotiateStream.AuthenticateAsClient%2A> 오버로드 메서드가 추가되었습니다.  
  
-   서버 응용 프로그램에 대한 확장된 보호를 지원하기 위해 <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy>를 전달할 수 있는 <xref:System.Net.Security.NegotiateStream> 클래스의 새로운 <xref:System.Net.Security.NegotiateStream.BeginAuthenticateAsServer%2A> 및 <xref:System.Net.Security.NegotiateStream.AuthenticateAsServer%2A> 오버로드 메서드가 추가되었습니다.  
  
-   클라이언트 및 서버 응용 프로그램에 대한 확장된 보호를 지원하기 위해 <xref:System.Net.Security.SslStream> 클래스의 새로운 <xref:System.Net.Security.SslStream.TransportContext%2A> 속성이 추가되었습니다.  
  
 <xref:System.Net.Security> 네임스페이스에서 SMTP 클라이언트에 대한 확장된 보호 구성을 지원하기 위해 <xref:System.Net.Configuration.SmtpNetworkElement> 속성이 추가되었습니다.  
  
## <a name="extended-protection-for-client-applications"></a>클라이언트 응용 프로그램에 대한 확장된 보호  
 대부분의 클라이언트 응용 프로그램에 대한 확장된 보호는 자동으로 지원됩니다. Windows의 기본 버전이 확장된 보호를 지원하면 <xref:System.Net.HttpWebRequest> 및 <xref:System.Net.Mail.SmtpClient> 클래스는 항상 확장된 보호를 지원합니다. <xref:System.Net.HttpWebRequest> 인스턴스는 <xref:System.Uri>에서 생성된 SPN을 보냅니다. 기본적으로 <xref:System.Net.Mail.SmtpClient> 인스턴스는 SMTP 메일 서버의 호스트 이름에서 생성된 SPN을 보냅니다.  
  
 사용자 지정 인증의 경우 클라이언트 응용 프로그램은 <xref:System.Net.TransportContext.GetChannelBinding%2A> 메서드를 통해 <xref:System.Net.TransportContext> 및 CBT를 검색할 수 있는 <xref:System.Net.HttpWebRequest> 클래스의 <xref:System.Net.HttpWebRequest.EndGetRequestStream%28System.IAsyncResult%2CSystem.Net.TransportContext%40%29?displayProperty=nameWithType> 또는 <xref:System.Net.HttpWebRequest.GetRequestStream%28System.Net.TransportContext%40%29?displayProperty=nameWithType> 메서드를 사용할 수 있습니다.  
  
 <xref:System.Net.HttpWebRequest> 인스턴스를 통해 지정된 서비스에 전송되는 Windows 통합 인증에 사용할 SPN은 <xref:System.Net.AuthenticationManager.CustomTargetNameDictionary%2A> 속성을 설정하여 재정의할 수 있습니다.  
  
 <xref:System.Net.Mail.SmtpClient.TargetName%2A> 속성을 통해 SMTP 연결에 대한 Windows 통합 인증에 사용할 사용자 지정 SPN을 설정할 수 있습니다.  
  
## <a name="extended-protection-for-server-applications"></a>서버 응용 프로그램에 대한 확장된 보호  
 <xref:System.Net.HttpListener>는 HTTP 인증을 수행할 때 서비스 바인딩의 유효성을 검사하기 위한 메커니즘을 자동으로 제공합니다.  
  
 가장 안전한 시나리오는 HTTPS:// 접두사에 대한 확장된 보호를 사용하는 것입니다. 이 경우 <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement>를 <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement.WhenSupported> 또는 <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement.Always>로 설정하고 <xref:System.Security.Authentication.ExtendedProtection.ProtectionScenario>를 <xref:System.Security.Authentication.ExtendedProtection.ProtectionScenario.TransportSelected>로 설정하여 <xref:System.Net.HttpListener.ExtendedProtectionPolicy%2A?displayProperty=nameWithType>를 <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy>로 설정합니다. <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement.WhenSupported> 값은 <xref:System.Net.HttpListener>를 부분 강화 모드로 전환하지만 <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement.Always>는 완전 강화 모드에 해당합니다.  
  
 이 구성에서 외부 보안 채널을 통해 서버에 대한 요청을 만들 경우 외부 채널이 쿼리되어 채널 바인딩이 있는지 확인됩니다. 이 채널 바인딩이 인증 SSPI 호출에 전달됩니다. 이 호출은 인증 Blob의 채널 바인딩이 일치하는지 검사합니다. 세 가지 가능한 결과는 다음과 같습니다.  
  
1.  서버의 기본 운영 체제가 확장된 보호를 지원하지 않습니다. 요청이 응용 프로그램에 노출되지 않고 권한 없는(401) 응답이 클라이언트에 반환됩니다. 오류의 원인을 나타내는 메시지가 <xref:System.Net.HttpListener> 추적 소스에 기록됩니다.  
  
2.  SSPI 호출이 실패하고, 이것은 클라이언트가 외부 채널에서 검색되는 예상 값과 일치하지 않는 채널 바인딩을 지정했거나 클라이언트가 서버에 대한 확장된 보호 정책에 <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement.Always>를 사용하도록 구성된 경우 채널 바인딩을 제공하지 못했음을 나타냅니다. 두 경우에 모두 요청이 응용 프로그램에 노출되지 않고 권한 없는(401) 응답이 클라이언트에 반환됩니다. 오류의 원인을 나타내는 메시지가 <xref:System.Net.HttpListener> 추적 소스에 기록됩니다.  
  
3.  클라이언트는 올바른 채널 바인딩을 지정하거나, 서버에 대한 확장된 보호 정책이 <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement.WhenSupported>를 사용하여 구성되므로 채널 바인딩을 지정하지 않고 연결할 수 있습니다. 요청은 처리를 위해 응용 프로그램에 반환됩니다. 서비스 이름 확인은 자동으로 수행되지 않습니다. 응용 프로그램은 <xref:System.Net.HttpListenerRequest.ServiceName%2A> 속성을 사용하여 자체 서비스 이름 유효성 검사를 수행할 수 있지만 이러한 상황에서는 작업이 중복됩니다.  
  
 응용 프로그램이 HTTP 요청 본문 내에서 앞뒤로 전달되는 Blob을 기반으로 인증을 수행하도록 자체 SSPI를 호출하고 채널 바인딩을 지원하려고 할 경우 응용 프로그램은 <xref:System.Net.HttpListener>를 통해 외부 보안 채널에서 예상 채널 바인딩을 검색하여 네이티브 Win32 [AcceptSecurityContext](https://go.microsoft.com/fwlink/?LinkId=147021) 함수에 전달해야 합니다. 이렇게 하려면 <xref:System.Net.HttpListenerRequest.TransportContext%2A> 속성을 사용하여 <xref:System.Net.TransportContext.GetChannelBinding%2A> 메서드를 호출하여 CBT를 검색합니다. 엔드포인트 바인딩만 지원됩니다. <xref:System.Security.Authentication.ExtendedProtection.ChannelBindingKind.Endpoint> 이외의 다른 항목이 지정되면 <xref:System.NotSupportedException>이 throw됩니다. 기본 운영 체제가 채널 바인딩을 지원하면 <xref:System.Net.TransportContext.GetChannelBinding%2A> 메서드는 `pInput` 매개 변수에 전달되는 SecBuffer 구조체의 pvBuffer 멤버로 [AcceptSecurityContext](https://go.microsoft.com/fwlink/?LinkId=147021) 함수에 전달하기에 적합한 채널 바인딩에 대한 포인터를 래핑하는 <xref:System.Security.Authentication.ExtendedProtection.ChannelBinding><xref:System.Runtime.InteropServices.SafeHandle>을 반환합니다. <xref:System.Security.Authentication.ExtendedProtection.ChannelBinding.Size%2A> 속성에는 채널 바인딩의 길이(바이트)가 포함됩니다. 기본 운영 체제가 채널 바인딩을 지원하지 않으면 이 함수는 `null`을 반환합니다.  
  
 또 다른 가능한 시나리오는 프록시가 사용되지 않을 경우 HTTP:// 접두사에 대한 확장된 보호를 사용하는 것입니다. 이 경우 <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement>를 <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement.WhenSupported> 또는 <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement.Always>로 설정하고 <xref:System.Security.Authentication.ExtendedProtection.ProtectionScenario>를 <xref:System.Security.Authentication.ExtendedProtection.ProtectionScenario.TransportSelected>로 설정하여 <xref:System.Net.HttpListener.ExtendedProtectionPolicy%2A?displayProperty=nameWithType>를 <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy>로 설정합니다. <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement.WhenSupported> 값은 <xref:System.Net.HttpListener>를 부분 강화 모드로 전환하지만 <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement.Always>는 완전 강화 모드에 해당합니다.  
  
 허용되는 서비스 이름의 기본 목록은 <xref:System.Net.HttpListener>를 사용하여 등록된 접두사를 기반으로 만들어집니다. 이 기본 목록은 <xref:System.Net.HttpListener.DefaultServiceNames%2A> 속성을 통해 검사할 수 있습니다. 이것은 포괄적인 목록이 아니므로 응용 프로그램은 <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy> 클래스에 대한 생성자에서 기본 서비스 이름 목록 대신 사용할 사용자 지정 서비스 이름 컬렉션을 지정할 수 있습니다.  
  
 이 구성에서 외부 보안 채널을 사용하지 않고 서버에 대한 요청을 만들 경우 일반적으로 인증은 채널 바인딩 확인 없이 진행됩니다. 인증에 성공하면 컨텍스트가 쿼리되어 클라이언트가 제공하고 허용 가능한 서비스 이름 목록에 대해 유효성 검사된 서비스 이름이 있는지 확인됩니다. 네 가지 가능한 결과는 다음과 같습니다.  
  
1.  서버의 기본 운영 체제가 확장된 보호를 지원하지 않습니다. 요청이 응용 프로그램에 노출되지 않고 권한 없는(401) 응답이 클라이언트에 반환됩니다. 오류의 원인을 나타내는 메시지가 <xref:System.Net.HttpListener> 추적 소스에 기록됩니다.  
  
2.  클라이언트의 기본 운영 체제가 확장된 보호를 지원하지 않습니다. <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement.WhenSupported> 구성에서 인증 시도가 성공하고 요청이 응용 프로그램에 반환됩니다. <xref:System.Security.Authentication.ExtendedProtection.PolicyEnforcement.Always> 구성에서 인증 시도가 실패합니다. 요청이 응용 프로그램에 노출되지 않고 권한 없는(401) 응답이 클라이언트에 반환됩니다. 오류의 원인을 나타내는 메시지가 <xref:System.Net.HttpListener> 추적 소스에 기록됩니다.  
  
3.  클라이언트의 기본 운영 체제가 확장된 보호를 지원하지만 응용 프로그램이 서비스 바인딩을 지정하지 않았습니다. 요청이 응용 프로그램에 노출되지 않고 권한 없는(401) 응답이 클라이언트에 반환됩니다. 오류의 원인을 나타내는 메시지가 <xref:System.Net.HttpListener> 추적 소스에 기록됩니다.  
  
4.  클라이언트가 서비스 바인딩을 지정했습니다. 서비스 바인딩은 허용되는 서비스 바인딩 목록에 비교됩니다. 일치할 경우 요청이 응용 프로그램에 반환됩니다. 일치하지 않을 경우 요청이 응용 프로그램에 노출되지 않고 권한 없는(401) 응답이 클라이언트에 자동으로 반환됩니다. 오류의 원인을 나타내는 메시지가 <xref:System.Net.HttpListener> 추적 소스에 기록됩니다.  
  
 허용되는 서비스 이름 목록을 사용하는 이 간단한 방법으로 부족할 경우 응용 프로그램은 <xref:System.Net.HttpListenerRequest.ServiceName%2A> 속성을 쿼리하여 자체 서비스 이름 유효성 검사를 제공할 수 있습니다. 위의 사례 1 및 2에서 속성은 `null`을 반환합니다. 사례 3에서 속성은 빈 문자열을 반환합니다. 사례 4에서는 클라이언트에서 지정된 서비스 이름이 반환됩니다.  
  
 이러한 확장된 보호 기능은 다른 요청 형식을 사용하여 인증할 경우 및 신뢰할 수 있는 프록시가 사용될 경우 서버 응용 프로그램에서 인증에 사용될 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Security.Authentication.ExtendedProtection>  
 <xref:System.Security.Authentication.ExtendedProtection.Configuration>
