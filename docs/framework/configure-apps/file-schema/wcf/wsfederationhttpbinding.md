---
title: <wsFederationHttpBinding>
ms.date: 03/30/2017
helpviewer_keywords:
- wsFederationBinding element
ms.assetid: 9c3312b4-2137-4e71-bf3f-de1cf8e9be79
ms.openlocfilehash: a605d3241ec62f5648e3439b327153f3fb4590df
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399030"
---
# <a name="wsfederationhttpbinding"></a>\<wsFederationHttpBinding>

WS-Federation을 지원하는 바인딩을 정의합니다.

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<바인딩 >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<wsFederationHttpBinding >**  

## <a name="syntax"></a>구문

```xml
<wsFederationHttpBinding>
  <binding bypassProxyOnLocal="Boolean"
           closeTimeout="TimeSpan"
           hostNameComparisonMode="StrongWildcard/Exact/WeakWildcard"
           maxBufferPoolSize="integer"
           maxReceivedMessageSize="integer"
           messageEncoding="Text/Mtom"
           name="string"
           openTimeout="TimeSpan"
           privacyNoticeAt="Uri"
           privacyNoticeVersion="Integer"
           proxyAddress="Uri"
           receiveTimeout="TimeSpan"
           sendTimeout="TimeSpan"
           textEncoding="UnicodeFffeTextEncoding/Utf16TextEncoding/ Utf8TextEncoding"
           transactionFlow="Boolean"
           useDefaultWebProxy="Boolean">
    <security mode="None/Message/TransportWithMessageCredential">
      <message algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
               issuedTokenType="string"
               issuedKeyType="SymmetricKey/PublicKey"
               negotiateServiceCredential="Boolean">
        <claimTypeRequirements>
          <add claimType="URI"
               isOptional="Boolean" />
        </claimTypeRequirements>
        <issuer address="Uri" >
          <headers>
            <add name="String"
                 namespace="String" />
          </headers>
          <identity>
            <certificate encodedValue="String" />
            <certificateReference findValue="String"
                                  isChainIncluded="Boolean"
                                  storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
                                  storeLocation="LocalMachine/CurrentUser"
                                  X509FindType="System.Security.Cryptography.X509certificates.X509findtype" />
            <dns value="String" />
            <rsa value="String" />
            <servicePrincipalName value="String" />
            <usePrincipalName value="String" />
          </identity>
        </issuer>
        <issuerMetadata address="String">
          <headers>
            <add name="String"
                 namespace="String" />
          </headers>
          <identity>
            <certificate encodedValue="String" />
            <certificateReference findValue="String"
                                  isChainIncluded="Boolean"
                                  storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"
                                  storeLocation="LocalMachine/CurrentUser"
                                  x509FindType="System.Security.Cryptography.X509certificates.X509findtype" />
            <dns value="String" />
            <rsa value="String" />
            <servicePrincipalName value="String" />
            <usePrincipalName value="String" />
          </identity>
        </issuerMetadata>
        <tokenRequestParameters>
          <xmlElement>
          </xmlElement>
        </tokenRequestParameters>
      </message>
    </security>
    <reliableSession ordered="Boolean"
                     inactivityTimeout="TimeSpan"
                     enabled="Boolean" />
    <readerQuotas maxArrayLength="Integer"
                  maxBytesPerRead="Integer"
                  maxDepth="Integer"
                  maxNameTableCharCount="Integer"
                  maxStringContentLength="Integer" />
  </binding>
</wsFederationBinding>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.

### <a name="attributes"></a>특성

|특성|Description|
|---------------|-----------------|
|bypassProxyOnLocal|로컬 주소에 대해 프록시 서버를 사용하지 않을 것인지 여부를 나타내는 부울 값입니다. 기본값은 `false`입니다.|
|closeTimeout|닫기 작업을 완료하기 위해 제공된 시간 간격을 지정하는 <xref:System.TimeSpan> 값입니다. 이 값은 <xref:System.TimeSpan.Zero>보다 크거나 같아야 합니다. 기본값은 00:01:00입니다.|
|hostnameComparisonMode|URI 구문 분석에 사용되는 HTTP 호스트 이름 비교 모드를 지정합니다. 이 특성은 <xref:System.ServiceModel.HostNameComparisonMode> 형식이며 URI에 대해 비교할 때 호스트 이름이 서비스에 연결하는 데 사용되는지 여부를 나타냅니다. 기본값은 <xref:System.ServiceModel.HostNameComparisonMode.StrongWildcard>이며 이 값은 비교 시 호스트 이름을 무시합니다.|
|maxBufferPoolSize|이 바인딩의 최대 버퍼 풀 크기를 지정하는 정수입니다. 기본값은 524,288바이트(512 * 1024)입니다. WCF(Windows Communication Foundation)의 많은 부분에서 버퍼를 사용합니다. 버퍼를 사용할 때마다 만들고 삭제하면 비용이 많이 들며, 버퍼에 대한 가비지 수집 역시 비용이 많이 듭니다. 버퍼 풀이 있으면 이 풀로부터 버퍼를 가져와 사용한 다음 다시 풀로 반환할 수 있습니다. 따라서 버퍼를 만들고 삭제하는 데 오버헤드를 피할 수 있습니다.|
|maxReceivedMessageSize|헤더를 비롯하여 이 바인딩으로 구성된 채널에서 받을 수 있는 최대 메시지 크기(바이트)를 지정하는 양의 정수입니다. 이 한도를 초과하는 메시지를 보낸 사람은 SOAP 오류를 받습니다. 수신자는 메시지를 삭제하고 추적 로그에 이벤트 항목을 만듭니다. 기본값은 65536입니다.|
|messageEncoding|메시지를 인코딩하는 데 사용되는 인코더를 정의합니다. 유효한 값은 다음과 같습니다.<br /><br /> 본문 텍스트 메시지 인코더를 사용 합니다.<br />Mtom MTOM (메시지 전송 조직 메커니즘) 1.0 인코더를 사용 합니다.<br /><br /> 기본값은 Text입니다.<br /><br /> 이 특성은 <xref:System.ServiceModel.WSMessageEncoding> 형식입니다.|
|name|바인딩의 구성 이름을 포함하는 문자열입니다. 이 값은 바인딩의 ID로 사용되므로 고유해야 합니다. [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)]부터는 바인딩 및 동작에 이름이 필요하지 않습니다. 기본 구성 및 이름이 없는 바인딩 및 동작에 대 한 자세한 내용은 [WCF 서비스에 대 한](../../../wcf/samples/simplified-configuration-for-wcf-services.md) [간소화 된 구성](../../../wcf/simplified-configuration.md) 및 단순화 된 구성을 참조 하세요.|
|openTimeout|열기 작업을 완료하기 위해 제공된 시간 간격을 지정하는 <xref:System.TimeSpan> 값입니다. 이 값은 <xref:System.TimeSpan.Zero>보다 크거나 같아야 합니다. 기본값은 00:01:00입니다.|
|privacyNoticeAt|개인 정보 알림이 있는 URI를 지정하는 문자열입니다.|
|privacyNoticeVersion|현재 개인 정보 알림의 버전을 지정하는 정수입니다.|
|proxyAddress|HTTP 프록시의 주소를 지정하는 URI입니다. `useDefaultWebProxy`가 `true`일 경우 이 설정은 `null`이어야 합니다. 기본값은 `null`입니다.|
|receiveTimeout|받기 작업을 완료하기 위해 제공된 시간 간격을 지정하는 <xref:System.TimeSpan> 값입니다. 이 값은 <xref:System.TimeSpan.Zero>보다 크거나 같아야 합니다. 기본값은 00:10:00입니다.|
|sendTimeout|보내기 작업을 완료하기 위해 제공된 시간 간격을 지정하는 <xref:System.TimeSpan> 값입니다. 이 값은 <xref:System.TimeSpan.Zero>보다 크거나 같아야 합니다. 기본값은 00:01:00입니다.|
|textEncoding|바인딩에서 메시지를 내보내는 데 사용되는 문자 집합 인코딩을 설정합니다. 유효한 값은 다음과 같습니다.<br /><br /> -   BigEndianUnicode: 유니코드가 나 Endian 인코딩입니다.<br />유니코드 16 비트 인코딩입니다.<br />-   UTF8: 8 비트 인코딩<br /><br /> 기본값은 UTF8입니다. 이 특성은 <xref:System.Text.Encoding> 형식입니다.|
|transactionFlow|바인딩에서 WS-Transactions 이동을 지원할지 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다.|
|useDefaultWebProxy|시스템의 자동 구성된 HTTP 프록시 사용 여부를 지정하는 부울 값입니다. 이 특성이 `null`이면 프록시 주소는 `true`이어야 합니다(설정되지 않음). 기본값은 `true`입니다.|

### <a name="child-elements"></a>자식 요소

|요소|설명|
|-------------|-----------------|
|[\<security>](security-of-wsfederationhttpbinding.md)|메시지에 대한 보안 설정을 정의합니다. 이 요소는 <xref:System.ServiceModel.Configuration.WSFederationHttpSecurityElement> 형식입니다.|
|[\<readerQuotas>](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms731325(v=vs.100))|이 바인딩으로 구성된 엔드포인트에서 처리할 수 있는 SOAP 메시지의 복잡성에 대한 제약 조건을 정의합니다. 이 요소는 <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement> 형식입니다.|
|[\<reliableSession>](https://docs.microsoft.com/previous-versions/ms731375(v=vs.90))|채널 엔드포인트 간에 신뢰할 수 있는 세션이 설정되는지 여부를 지정합니다.|

### <a name="parent-elements"></a>부모 요소

|요소|설명|
|-------------|-----------------|
|[\<bindings>](bindings.md)|이 요소는 표준 및 사용자 지정 바인딩의 컬렉션을 보유합니다.|

## <a name="remarks"></a>설명

페더레이션은 인증 및 권한 부여를 위해 여러 시스템에서 ID를 공유하는 기능입니다. 이러한 ID는 사용자나 시스템을 가리킬 수 있습니다. 페더레이션 HTTP는 SOAP 보안과 혼합 모드 보안을 모두 지원하지만 전송 보안만을 사용하여 지원하지는 않습니다. 이 바인딩은 WS-페더레이션 프로토콜 Windows Communication Foundation (WCF) 지원을 제공합니다. 이 바인딩으로 구성된 서비스는 HTTP 전송을 사용해야 합니다.

바인딩은 바인딩 요소의 스택으로 구성됩니다. 가 기본값인 로 설정된 경우

`wsFederationHttpBinding`에 있는 바인딩 요소의 스택은`wsHttpBinding`

[ \<security >](security-of-wsfederationhttpbinding.md) 이 기본값인 <xref:System.ServiceModel.WSFederationHttpSecurityMode.Message>로 설정 된 경우

는 `wsFederationHttpBinding` [ \<메시지 >](message-element-of-wsfederationhttpbinding.md)의 메시지 보안 설정에 대 한 세부 정보를 제어 합니다. 보안 > 요소는 바인딩이 생성 된 후 바인딩에 사용 되는 보안을 변경할 수 없기 때문에 get 액세스만 제공 합니다. [ \<](security-of-wsfederationhttpbinding.md)

또한 `wsFederationHttpBinding` 은 개인 정보 알림이 있는 URI를 설정 하 고 검색 하는 privacyNoticeAt 특성도 제공 합니다.

정책 보안을 유지하는 것은 페더레이션 시나리오에서 특히 중요합니다. HTTPS와 같은 특정 형식의 보안을 사용하여 악의적인 사용자로부터 정책을 보호할 것을 권장합니다.

이러한 바인딩을 사용하는 페더레이션 시나리오에서 서비스 정책은 발급된(SAML) 토큰을 암호화하기 위한 키, 토큰에 추가할 클레임 형식 등의 중요한 정보를 포함할 수 있습니다. 이 정책이 훼손되면 공격자는 발급된 토큰의 키를 확인할 수 있게 되므로 추가적인 정보 변조, 정보 노출 및 기타 악의적인 동작이 발생할 수 있습니다. 이를 방지하려면 정책을 서비스에서 안전하게(예: HTTPS 사용) 가져와야 합니다.

이 바인딩에 [대 한 자세한 내용은 방법: WSFederationHttpBinding](../../../wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)를 만듭니다.

## <a name="example"></a>예제

```xml
<configuration>
  <system.ServiceModel>
    <bindings>
      <wsFederationHttpBinding>
        <binding bypassProxyOnLocal="false"
                 transactionFlow="false"
                 hostNameComparisonMode="WeakWildcard"
                 maxReceivedMessageSize="1000"
                 messageEncoding="Mtom"
                 proxyAddress="http://foo/bar"
                 textEncoding="Utf16TextEncoding"
                 useDefaultWebProxy="false">
          <reliableSession ordered="false"
                           inactivityTimeout="00:02:00"
                           enabled="true" />
          <security mode="None">
            <message negotiateServiceCredential="false"
                     algorithmSuite="Aes128"
                     issuedTokenType="saml"
                     issuedKeyType="PublicKey">
              <issuer address="http://localhost/Sts" />
            </message>
          </security>
        </binding>
      </wsFederationBinding>
    </bindings>
  </system.ServiceModel>
</configuration>
```

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.WSFederationHttpBinding>
- <xref:System.ServiceModel.Configuration.WSFederationHttpBindingElement>
- [방법: WSFederationHttpBinding 만들기](../../../wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)
- [바인딩](../../../wcf/bindings.md)
- [시스템 제공 바인딩 구성](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
