---
title: '방법: 이중 페더레이션 바인딩 만들기'
ms.date: 03/30/2017
ms.assetid: 4331d2bc-5455-492a-9189-634a82597726
ms.openlocfilehash: 71c970fa45d7d4ccd55fceddb2360d0aa0a768f8
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68972054"
---
# <a name="how-to-create-a-duplex-federated-binding"></a>방법: 이중 페더레이션 바인딩 만들기

<xref:System.ServiceModel.WSFederationHttpBinding>은 데이터그램 및 요청/응답 메시지 교환 계약만 지원합니다. 이중 메시지 교환 계약을 사용하려면 사용자 지정 바인딩을 만들어야 합니다. 다음 절차에서는 HTTP 및 TCP 전송에 대해서는 메시지 모드 보안을 사용하고 TCP 전송에 대해서는 혼합 모드 보안을 사용하여 구성에서 이 작업을 수행하는 방법을 보여 줍니다. 3개의 바인딩을 모두 보여 주는 샘플 코드는 이 항목의 끝에 나옵니다.

코드에서 바인딩을 만들 수도 있습니다. 만들 바인딩 요소 스택에 대 한 자세한 내용은 [방법: SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)를 사용 하 여 사용자 지정 바인딩을 만듭니다.

## <a name="to-create-a-duplex-federated-custom-binding-with-http"></a>HTTP를 사용하여 이중 페더레이션 사용자 지정 바인딩을 만들려면

1. 구성 파일의 [ 바인딩>노드에서customBinding>요소를만듭니다.\<](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)

2. CustomBinding > `name` 요소 내에서 특성을 로`FederationDuplexHttpMessageSecurityBinding`설정 하 여 [바인딩 > 요소를 만듭니다. \<](../../../../docs/framework/misc/binding.md) [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)

3. 바인딩 > `authenticationMode` 요소 내에서 특성을 로`SecureConversation`설정 하 여 [보안 > 요소를 만듭니다. \<](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) [ \<](../../../../docs/framework/misc/binding.md)

4. `authenticationMode` `IssuedTokenForCertificate` [Security > 요소 내에서 특성을 또는로 설정 하 여 secureConversationBootstrap > 요소를 만듭니다. \<](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md) `IssuedTokenForSslNegotiated`

5. Security > 요소 다음에 빈 [ \<compositeDuplex >](../../../../docs/framework/configure-apps/file-schema/wcf/compositeduplex.md) 요소를 만듭니다. [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)

6. CompositeDuplex > 요소 다음에 빈 [ \<oneWay >](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md) 요소를 만듭니다. [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/compositeduplex.md)

7. OneWay > 요소 다음에 빈 [ \<httptransport >](../../../../docs/framework/configure-apps/file-schema/wcf/httptransport.md) 요소를 만듭니다. [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/oneway.md)

## <a name="to-create-a-duplex-federated-custom-binding-with-tcp-message-security-mode"></a>TCP 메시지 보안 모드를 사용하여 이중 페더레이션 사용자 지정 바인딩을 만들려면

1. 구성 파일의 [ 바인딩>노드에서customBinding>요소를만듭니다.\<](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)

2. CustomBinding > `name` 요소 내에서 특성을 로`FederationDuplexTcpMessageSecurityBinding`설정 하 여 [바인딩 > 요소를 만듭니다. \<](../../../../docs/framework/misc/binding.md) [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)

3. 바인딩 > `authenticationMode` 요소 내에서 특성을 로`SecureConversation`설정 하 여 [보안 > 요소를 만듭니다. \<](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) [ \<](../../../../docs/framework/misc/binding.md)

4. `authenticationMode` `IssuedTokenForCertificate` [Security > 요소 내에서 특성을 또는로 설정 하 여 secureConversationBootstrap > 요소를 만듭니다. \<](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md) `IssuedTokenForSslNegotiated`

5. Security > 요소 다음에 빈 [ \<tcptransport >](../../../../docs/framework/configure-apps/file-schema/wcf/tcptransport.md) 요소를 만듭니다. [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)

## <a name="to-create-a-duplex-federated-custom-binding-with-tcp-mixed-security-mode"></a>TCP 혼합 보안 모드를 사용하여 이중 페더레이션 사용자 지정 바인딩을 만들려면

1. 구성 파일의 [ 바인딩>노드에서customBinding>요소를만듭니다.\<](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)

2. CustomBinding > `name` 요소 내에서 특성을 로`FederationDuplexTcpTransportSecurityWithMessageCredentialBinding`설정 하 여 [바인딩 > 요소를 만듭니다. \<](../../../../docs/framework/misc/binding.md) [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)

3. 바인딩 > `authenticationMode` 요소 내에서 특성을 로`SecureConversation`설정 하 여 [보안 > 요소를 만듭니다. \<](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) [ \<](../../../../docs/framework/misc/binding.md)

4. `authenticationMode` `IssuedTokenForCertificate` [Security > 요소 내에서 특성을 또는로 설정 하 여 secureConversationBootstrap > 요소를 만듭니다. \<](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md) `IssuedTokenForSslNegotiated`

5. Security > 요소 다음에 빈 [ \<sslstreamsecurity >](../../../../docs/framework/configure-apps/file-schema/wcf/sslstreamsecurity.md) 요소를 만듭니다. [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)

6. Sslstreamsecurity > 요소 다음에 빈 [ \<tcptransport >](../../../../docs/framework/configure-apps/file-schema/wcf/tcptransport.md) 요소를 만듭니다. [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/sslstreamsecurity.md)

## <a name="code-sample"></a>코드 예제

### <a name="sample-with-3-bindings"></a>3개의 바인딩에 대한 샘플

1. 구성 파일에 다음 코드를 삽입합니다.

## <a name="example"></a>예제

```xml
<bindings>
   <customBinding>
      <binding name="FederationDuplexHttpMessageSecurityBinding">
<!-- duplex contract requires secure conversation with require cancellation = true -->
          <security authenticationMode="SecureConversation">
              <secureConversationBootstrap authenticationMode="IssuedTokenForSslNegotiated" />
          </security>
          <compositeDuplex />
          <oneWay />
          <httpTransport />
       </binding>
<!-- duplex over https is not supported -->
       <binding name="FederationDuplexTcpMessageSecurityBinding">
<!-- duplex contract requires secure conversation with require cancellation = true -->
          <security authenticationMode="SecureConversation">
              <secureConversationBootstrap authenticationMode="IssuedTokenForSslNegotiated" />
          </security>
          <tcpTransport />
       </binding>
       <binding name="FederationDuplexTcpTransportSecurityWithMessageCredentialsBinding">
<!-- duplex contract requires secure conversation with require cancellation = true -->
          <security authenticationMode="SecureConversation">
              <secureConversationBootstrap authenticationMode="IssuedTokenOverTransport" />
          </security>
<!-- requireClientCertificate = true or <windowsStreamSecurity /> can be used, but does not make sense for most scenarios -->
          <sslStreamSecurity />
          <tcpTransport />
       </binding>
    </customBinding>
</bindings>
```
