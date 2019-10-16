---
title: '완화: WCF 서비스 및 인증서 인증'
ms.date: 03/30/2017
ms.assetid: ef19c91a-b9df-4bf0-a28e-eb1e99c4bc95
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0fcb4de714c8a0f1f2c61f3a12815a5a0a3ddc83
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70789815"
---
# <a name="mitigation-wcf-services-and-certificate-authentication"></a>완화: WCF 서비스 및 인증서 인증

.NET Framework 4.6은 WCF SSL 프로토콜 기본 목록에 TLS 1.1 및 TLS 1.2를 추가합니다. 클라이언트와 서버 컴퓨터에.NET Framework 4.6 및 이후 버전이 설치되어 있으면 TLS 1.2가 협상에 사용됩니다.

## <a name="impact"></a>영향

TLS 1.2는 MD5 인증서 인증을 지원하지 않습니다. 결과적으로 고객이 해시 알고리즘에 대해 MD5를 사용하는 SSL 인증서를 사용 하는 경우 WCF 클라이언트에서 WCF 서비스에 연결하지 못합니다. 자세한 내용은 [완화: WCF 서비스 및 인증서 인증](mitigation-wcf-services-and-certificate-authentication.md)을 참조하세요.

## <a name="mitigation"></a>완화

다음 중 하나를 수행하여 WCF 클라이언트가 WCF 서버에 연결할 수 있도록 함으로써 이 문제를 해결할 수 있습니다.

- MD5 알고리즘을 사용 하지 않도록 인증서를 업데이트합니다. 이것은 권장되는 해결 방법입니다.

- 소스 코드에서 바인딩이 동적으로 구성되지 않은 경우 TLS 1.1 또는 이전 버전의 프로토콜을 사용하도록 애플리케이션의 구성 파일을 업데이트합니다. 이렇게 하면 MD5 해시 알고리즘에서 인증서를 계속 사용할 수 있습니다.

  > [!CAUTION]
  > MD5 해시 알고리즘을 사용하는 인증서는 안전하지 않은 것으로 간주되므로 이 해결 방법은 권장되지 않습니다.

  다음 구성 파일에 이 내용이 나와 있습니다.

  ```xml
  <configuration>
      <system.serviceModel>
          <bindings>
              <netTcpBinding>
                  <binding>
                      <security mode= "None|Transport|Message|TransportWithMessageCredential" >
                          <transport clientCredentialType="None|Windows|Certificate"
                                              protectionLevel="None|Sign|EncryptAndSign"
                                              sslProtocols="Ssl3|Tls1|Tls11">
                          </transport>
                      </security>
                  </binding>
              </netTcpBinding>
          </bindings>
      </system.ServiceModel>
  </configuration>
  ```

- 소스 코드에서 바인딩이 동적으로 구성된 경우 소스 코드에서 TLS 1.1(<xref:System.Security.Authentication.SslProtocols.Tls11?displayProperty=nameWithType>) 또는 이전 버전의 프로토콜을 사용하도록 <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A?displayProperty=nameWithType> 속성을 업데이트합니다.

  > [!CAUTION]
  > MD5 해시 알고리즘을 사용하는 인증서는 안전하지 않은 것으로 간주되므로 이 해결 방법은 권장되지 않습니다.

## <a name="see-also"></a>참고 항목

- [런타임 변경 내용](runtime-changes-in-the-net-framework-4-6.md)
