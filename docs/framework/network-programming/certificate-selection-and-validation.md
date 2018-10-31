---
title: 인증서 선택 및 유효성 검사
ms.date: 03/30/2017
ms.assetid: c933aca2-4cd0-4ff1-9df9-267143f25a6f
ms.openlocfilehash: 2767f8fc62d44e480962690a3cbe379fea0f9662
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50048374"
---
# <a name="certificate-selection-and-validation"></a>인증서 선택 및 유효성 검사
<xref:System.Net> 클래스는 SSL(Secure Sockets Layer) 연결에 대한 <xref:System.Security.Cryptography.X509Certificates>를 선택하고 유효성을 검사하는 여러 가지 방법을 지원합니다. 클라이언트는 서버에 인증하기 위해 하나 이상의 인증서를 선택할 수 있습니다. 서버는 인증을 위해 클라이언트 인증서에 하나 이상의 특정 특성이 있도록 요구할 수 있습니다.  
  
## <a name="definition"></a>정의  
 인증서는 인증 기관의 디지털 시그니처, 공개 키, 특성(예: 버전 번호, 일련 번호, 만료 날짜)을 포함하는 ASCII 바이트 스트림입니다. 인증서는 암호화된 연결을 설정하거나 서버에 클라이언트를 인증하는 데 사용됩니다.  
  
## <a name="client-certificate-selection-and-validation"></a>클라이언트 인증서 선택 및 유효성 검사  
 클라이언트는 특정 SSL 연결에 대해 하나 이상의 인증서를 선택할 수 있습니다. SSL 연결을 사용하여 클라이언트 인증서를 웹 서버 또는 SMTP 메일 서버에 연결할 수 있습니다. 클라이언트는 <xref:System.Security.Cryptography.X509Certificates.X509Certificate> 또는 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> 클래스 개체 컬렉션에 인증서를 추가합니다. 전자 메일을 예로 사용할 경우, 인증서 컬렉션은 <xref:System.Net.Mail.SmtpClient> 클래스의 <xref:System.Net.Mail.SmtpClient.ClientCertificates%2A> 속성과 연결된 <xref:System.Security.Cryptography.X509Certificates.X509CertificateCollection> 인스턴스입니다. <xref:System.Net.HttpWebRequest> 클래스에는 비슷한 <xref:System.Net.HttpWebRequest.ClientCertificates%2A> 속성이 있습니다.  
  
 <xref:System.Security.Cryptography.X509Certificates.X509Certificate> 및 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> 클래스 간의 주요 차이점은 <xref:System.Security.Cryptography.X509Certificates.X509Certificate> 클래스의 경우 개인 키가 인증서 저장소에 상주해야 한다는 것입니다.  
  
 인증서가 컬렉션에 추가되고 특정 SSL 연결과 관련된 경우에도 서버가 요청하지 않으면 인증서가 서버에 전송되지 않습니다. 여러 클라이언트 인증서가 연결에 설정된 경우 서버에서 제공하는 인증서 발급자 목록과 클라이언트 인증서 발급자 이름 간의 일치를 고려하는 알고리즘에 따라 최상의 인증서가 사용됩니다.  
  
 <xref:System.Net.Security.SslStream> 클래스는 SSL 핸드셰이크를 통해 훨씬 더 강력한 제어 기능을 제공합니다. 클라이언트는 사용할 클라이언트 인증서를 선택할 대리자를 지정할 수 있습니다.  
  
 원격 서버는 클라이언트 인증서가 유효하고, 최신 상태이며, 적절한 인증 기관에서 서명되었는지 확인할 수 있습니다. <xref:System.Net.ServicePointManager.ServerCertificateValidationCallback%2A>에 대리자를 추가하여 인증서 유효성 검사를 적용할 수 있습니다.  
  
## <a name="client-certificate-selection"></a>클라이언트 인증서 선택  
 .NET Framework는 다음과 같은 방식으로 서버에 제공할 클라이언트 인증서를 선택합니다.  
  
1.  이전에 클라이언트 인증서가 서버에 제공된 경우 처음 제공될 때 인증서가 캐시되고 후속 클라이언트 인증서 요청에 다시 사용됩니다.  
  
2.  대리자가 있는 경우 항상 대리자의 결과를 선택할 클라이언트 인증서로 사용합니다. 가능한 경우 캐시된 인증서를 사용하되, 대리자가 null을 반환하고 인증서 컬렉션이 비어 있지 않으면 캐시된 익명 자격 증명을 사용하지 마세요.  
  
3.  클라이언트 인증서에 대한 첫 번째 인증인 경우 프레임워크는 연결과 관련된 <xref:System.Security.Cryptography.X509Certificates.X509Certificate> 또는 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> 클래스 개체의 인증서를 열거하고, 서버에서 제공하는 인증서 발급자 목록과 클라이언트 인증서 발급자 이름 간에 일치 항목을 찾습니다. 일치하는 첫 번째 인증서가 서버에 전송됩니다. 일치하는 인증서가 없거나 인증서 컬렉션이 비어 있으면 익명 자격 증명이 서버에 전송되지 않습니다.  
  
## <a name="tools-for-certificate-configuration"></a>인증서 구성 도구  
 클라이언트 및 서버 인증서 구성을 위해 다양한 도구를 사용할 수 있습니다.  
  
 *Winhttpcertcfg.exe* 도구는 클라이언트 인증서를 구성하는 데 사용할 수 있습니다. *Winhttpcertcfg.exe* 도구는 Windows Server 2003 Resource Kit의 도구 중 하나로 제공됩니다. [www.microsoft.com](https://www.microsoft.com)에서 Windows Server 2003 Resource Kit 도구의 일부로 다운로드할 수도 있습니다.  
  
*HttpCfg.exe* 도구는 <xref:System.Net.HttpListener> 클래스에 대한 서버 인증서를 구성하는 데 사용할 수 있습니다. *HttpCfg.exe* 도구는 Windows Server 2003 및 Windows XP 서비스 팩 2 지원 도구 중 하나로 제공됩니다. *HttpCfg.exe* 및 기타 지원 도구는 Windows Server 2003 또는 Windows XP에 기본적으로 설치되지 않습니다. Windows Server 2003. 지원 도구는 Windows Server 2003 CD-ROM에 있는 다음 폴더와 파일을 통해 별도로 설치됩니다.  
  
 \Support\Tools\Suptools.msi  
  
 Windows XP 서비스 팩 2에서 사용할 Windows XP 지원 도구는 [www.microsoft.com](https://www.microsoft.com)에서 다운로드할 수 있습니다.  
  
 *HttpCfg.exe* 도구 버전의 소스 코드도 Windows Server SDK와 함께 샘플로 제공됩니다. *HttpCfg.exe* 샘플의 소스 코드는 Windows SDK의 일부로 다음 폴더 아래에 네트워킹 샘플과 함께 기본적으로 설치됩니다.  
  
 *C:\Program Files\Microsoft SDKs\Windows\v1.0\Samples\NetDS\http\serviceconfig*  
  
 이러한 도구 외에도 <xref:System.Security.Cryptography.X509Certificates.X509Certificate> 및 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> 클래스는 파일 시스템에서 인증서를 로드하기 위한 메서드를 제공합니다.  
  
## <a name="see-also"></a>참고 항목  
 [네트워크 프로그래밍의 보안](../../../docs/framework/network-programming/security-in-network-programming.md)  
 [.NET Framework의 네트워크 프로그래밍](../../../docs/framework/network-programming/index.md)
