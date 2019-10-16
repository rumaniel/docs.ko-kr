---
title: <network> 요소(네트워크 설정)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#network
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings/smtp/network
helpviewer_keywords:
- <network> element
- network element
ms.assetid: 2c2c6ad4-ed11-48ab-b28e-2bc0ba9b42c7
ms.openlocfilehash: bac288bb28c4176e52366d0e0b7d8bc7d313cf96
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698015"
---
# <a name="network-element-network-settings"></a>\<network > 요소 (네트워크 설정)
외부 SMTP (Simple Mail Transport Protocol) 서버에 대 한 네트워크 옵션을 구성 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **@no__t -4c.net >** ](system-net-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t-2[ **\<mailSettings >** ](mailsettings-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t @ no__t-4 @ no__t-5[ **\<smtp >** ](smtp-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5 @ no__t-6 @ no__t-7 **\<network >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<network  
  clientDomain="string"   
  defaultCredentials="true|false"  
  enableSsl="true|false"  
  host="string"   
  password="string"  
  port="integer"   
  targetName="string"  
  userName="string"  
/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`clientDomain`|SMTP 메일 서버에 연결 하기 위해 초기 SMTP 프로토콜 요청에 사용할 클라이언트 도메인 이름을 지정 합니다. 기본값은 요청을 보내는 로컬 컴퓨터의 localhost 이름입니다.|  
|`defaultCredentials`|Smtp 트랜잭션을 위해 SMTP 메일 서버에 액세스 하는 데 기본 사용자 자격 증명을 사용할지 여부를 지정 합니다. 기본값은 `false`입니다.|  
|`enableSsl`|SMTP 메일 서버에 액세스 하는 데 SSL을 사용할지 여부를 지정 합니다. 기본값은 `false`입니다.|  
|`host`|SMTP 트랜잭션에 사용할 SMTP 메일 서버의 호스트 이름을 지정 합니다. 이 특성에는 기본값이 없습니다.|  
|`password`|SMTP 메일 서버에 대 한 인증에 사용할 암호를 지정 합니다. 이 특성에는 기본값이 없습니다.|  
|`port`|SMTP 메일 서버에 연결 하는 데 사용할 포트 번호를 지정 합니다. 기본값은 25입니다.|  
|`targetName`|SMTP 트랜잭션에 대해 확장 된 보호를 사용 하는 경우 인증에 사용할 SPN (서비스 공급자 이름)을 지정 합니다. 이 특성에는 기본값이 없습니다.|  
|`userName`|SMTP 메일 서버에 대 한 인증에 사용할 사용자 이름을 지정 합니다. 이 특성에는 기본값이 없습니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<smtp > 요소 (네트워크 설정)](smtp-element-network-settings.md)|SMTP (Simple Mail Transport Protocol) 메일 전송 옵션을 구성 합니다.|  
  
## <a name="remarks"></a>설명  
 일부 SMTP 서버에서는를 사용 하기 전에 서버에 대해 사용자를 인증 해야 합니다. 호스트에서 기본 네트워크 자격 증명을 사용 하 여 자신을 인증 하려면 `defaultCredentials` 특성을 `true`로 설정 합니다. @No__t-0 속성은 적용 가능한 구성 파일에서 `defaultCredentials` 특성의 현재 값을 가져오는 데 사용할 수 있습니다.  
  
 기본 인증 (사용자 이름 및 암호)을 사용 하 여 SMTP 서버에 대해 자신을 인증할 수도 있습니다. 이 옵션을 사용 하려면 지정 된 SMTP 서버에 대 한 유효한 사용자 이름 및 암호를 지정 해야 합니다.  
  
> [!NOTE]
> 기본 인증은 `userName` 및 `password` 값을 암호화 되지 않은 서버로 보냅니다. 네트워크 트래픽을 모니터링 하는 모든 자격 증명을 확인 하 고 하는 서버에 연결 하는 데 사용할 수 있습니다. Kerberos 또는 NT LAN Manager (NTLM)와 같은 보다 안전한 인증 메커니즘을 사용 하는 것을 고려해 야 합니다. @No__t-0 `true` 인 경우 서버에서 이러한 프로토콜을 지 원하는 경우 Kerberos 또는 NTLM이 사용 됩니다.  
  
 기본 인증 및 기본 네트워크 자격 증명 옵션은 함께 사용할 수 없습니다. `defaultCredentials` @no__t을-1로 설정 하 고 사용자 이름과 암호를 지정 하는 경우 기본 네트워크 자격 증명이 사용 되며 기본 인증 데이터는 무시 됩니다.  
  
 기본 인증의 경우 `userName`을 지정 하는 경우 메일 서버에 대 한 인증을 위해 `password`도 지정 해야 합니다.  
  
 @No__t-0 속성은 적용 가능한 구성 파일에서 `userName` 특성의 현재 값을 가져오는 데 사용할 수 있습니다. @No__t-0 속성은 적용 가능한 구성 파일에서 `password` 특성의 현재 값을 가져오는 데 사용할 수 있습니다. 일반적으로 `password` 특성은 보안상의 이유로 구성 파일에 입력 되지 않습니다.  
  
 @No__t-0 특성은 초기 SMTP 프로토콜 요청에 사용 된 클라이언트 도메인 이름을 SMTP 서버로 변경 합니다. @No__t-0 특성은 기본적으로 사용 되는 localhost 이름이 아니라 로컬 컴퓨터의 정규화 된 도메인 이름으로 설정할 수 있습니다. 이 큰 SMTP 프로토콜 표준 준수를 제공합니다. 기본값은 요청을 보내는 로컬 컴퓨터의 localhost 이름입니다. @No__t-0 속성은 적용 가능한 구성 파일에서 `clientDomain` 특성의 현재 값을 가져오는 데 사용할 수 있습니다.  
  
 @No__t-0 특성은 확장 된 보호를 사용 하는 경우 인증에 사용 됩니다. 기본값은 "SMTPSVC/\<host >" 형식입니다. 여기서 \<host >는 SMTP 메일 서버의 호스트 이름입니다. @No__t-0 속성은 적용 가능한 구성 파일에서 `targetName` 특성의 현재 값을 가져오는 데 사용할 수 있습니다.  
  
 @No__t-0 특성은 SMTP 메일 서버에 액세스 하는 데 SSL을 사용할지 여부를 지정 합니다. <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType> 클래스 SMTP 서비스 확장에 대해만 지원 SMTP 보안 전송 계층 보안을 통해 3207 RFC에에서 정의 된 대로 합니다. 이 모드에서는 SMTP 세션이 시작 된 암호화 되지 않은 채널에 다음 STARTTLS 명령을 실행 하는 SSL을 사용 하 여 보안 통신을 전환 하려면 서버에 클라이언트에서 발생 합니다. RFC 3207 게시 하 여는 Task Force IETF (Internet Engineering)에 대 한 자세한 내용은 참조 하세요.  
  
 대체 연결 메서드 명령을 보내는 모든 프로토콜 하기 전에 SSL 세션을 선불 하 게 설정 하는 경우 이 연결 방법을 SMTPS 라고 하 고 기본적으로 포트 465를 사용 합니다. 이 대체 연결 방법은 SSL을 사용 하 여 현재 지원 되지 않습니다.  
  
 @No__t-0 속성은 적용 가능한 구성 파일에서 `enableSsl` 특성의 현재 값을 가져오는 데 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 기본 네트워크 자격 증명을 사용 하 여 전자 메일을 보낼 적절 한 SMTP 매개 변수를 지정 합니다.  
  
```xml  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="Network">  
        <network  
          clientDomain="www.contoso.com"  
          defaultCredentials="true"  
          enableSsl="false"  
          host="mail.contoso.com"  
          port="25"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>참조

- <xref:System.Net.Configuration.SmtpNetworkElement?displayProperty=nameWithType>
- <xref:System.Net.Configuration.SmtpSection?displayProperty=nameWithType>
- <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>
- [네트워크 설정 스키마](index.md)
