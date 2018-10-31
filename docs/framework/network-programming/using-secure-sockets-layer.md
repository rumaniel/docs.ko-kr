---
title: SSL(Secure Sockets Layer) 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Networking
- SSL
- Secure Sockets Layer
- requesting data from Internet, Secure Sockets Layer
- sending data, Secure Sockets Layer
- Network Resources
- data requests, Secure Sockets Layer
- receiving data, Secure Sockets Layer
- Internet, Secure Sockets Layer
ms.assetid: 6e4289e6-d1b7-4e82-ab0d-e83e3b6063ed
ms.openlocfilehash: 41baeb9724d142bb860e51fa3ee84fb6c3f6261e
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50188692"
---
# <a name="using-secure-sockets-layer"></a>SSL(Secure Sockets Layer) 사용
<xref:System.Net> 클래스는 SSL(Secure Sockets Layer)을 사용하여 여러 네트워크 프로토콜에 대한 연결을 암호화합니다.  
  
 HTTP 연결의 경우 <xref:System.Net.WebRequest> 및 <xref:System.Net.WebResponse> 클래스는 SSL을 사용하여 SSL을 지원하는 웹 호스트와 통신합니다. 제공된 URI에 따라 <xref:System.Net.WebRequest> 클래스가 SSL 사용을 결정합니다. URI가 “https:”로 시작하는 경우 SSL이 사용됩니다. URI가 “http:”로 시작하는 경우에는 암호화되지 않은 연결이 사용됩니다.  
  
 FTP(파일 전송 프로토콜)와 함께 SSL을 사용하려면 <xref:System.Net.FtpWebRequest.GetResponse>를 호출하기 전에 <xref:System.Net.FtpWebRequest.EnableSsl> 속성을 true로 설정합니다. 마찬가지로, SMTP(Simple Mail Transfer Protocol)와 함께 SSL을 사용하려면 이메일을 보내기 전에 <xref:System.Net.Mail.SmtpClient.EnableSsl> 속성을 true로 설정합니다.  
  
 <xref:System.Net.Security.SslStream> 클래스는 SSL에 대한 스트림 기반 추상화를 제공하고 SSL 핸드셰이크를 구성할 수 있는 여러 가지 방법을 제공합니다.  
  
## <a name="example"></a>예  
  
### <a name="code"></a>코드  
  
```vb  
Dim MyURI As String = "https://www.contoso.com/"  
Dim Wreq As WebRequest = WebRequest.Create(MyURI)  
  
Dim serverUri As String = "ftp://ftp.contoso.com/file.txt"  
Dim request As FtpWebRequest = CType(WebRequest.Create(serverUri), FtpWebRequest)  
request.Method = WebRequestMethods.Ftp.DeleteFile  
request.EnableSsl = True  
Dim response As FtpWebResponse = CType(request.GetResponse(), FtpWebResponse)  
```  
  
```csharp  
String MyURI = "https://www.contoso.com/";  
WebRequest WReq = WebRequest.Create(MyURI);  
  
String serverUri = "ftp://ftp.contoso.com/file.txt"  
FtpWebRequest request = (FtpWebRequest)WebRequest.Create(serverUri);  
request.EnableSsl = true;  
request.Method = WebRequestMethods.Ftp.DeleteFile;  
FtpWebResponse response = (FtpWebResponse)request.GetResponse();  
```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
-   **System.Net** 네임스페이스에 대한 참조.  
  
## <a name="see-also"></a>참고 항목  
 [네트워크 프로그래밍의 보안](../../../docs/framework/network-programming/security-in-network-programming.md)  
 [.NET Framework의 네트워크 프로그래밍](../../../docs/framework/network-programming/index.md)  
 [인증서 선택 및 유효성 검사](../../../docs/framework/network-programming/certificate-selection-and-validation.md)
