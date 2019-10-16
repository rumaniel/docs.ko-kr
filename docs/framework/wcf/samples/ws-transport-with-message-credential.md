---
title: WS Transport With Message Credential
ms.date: 03/30/2017
ms.assetid: 0d092f3a-b309-439b-920b-66d8f46a0e3c
ms.openlocfilehash: a2eade01ff3397d8f7ea790558909111c43b131d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69959786"
---
# <a name="ws-transport-with-message-credential"></a>WS Transport With Message Credential
이 샘플에서는 메시지로 전달되는 클라이언트 자격 증명과 SSL 전송 보안을 조합하여 사용하는 방법을 보여 줍니다. 이 샘플에서는 `wsHttpBinding` 바인딩을 사용합니다.  
  
 기본적으로 `wsHttpBinding` 바인딩은 HTTP 통신을 제공합니다. 전송 보안용으로 구성된 경우, 바인딩은 HTTPS 통신을 지원합니다. HTTPS는 통신을 통해 전송되는 메시지의 기밀성 및 무결성을 보호합니다. 하지만 서비스에 대한 클라이언트의 인증에 사용되는 인증 메커니즘은 HTTPS 전송에서 지원되는 범위로 제한됩니다. WCF (Windows Communication Foundation)는 이러한 `TransportWithMessageCredential` 제한을 극복 하기 위해 설계 된 보안 모드를 제공 합니다. 이 보안 모드가 구성되어 있으면 전송 보안을 사용하여 전송되는 메시지에 기밀성과 무결성을 제공하고 서비스 인증을 수행할 수 있습니다. 그러나 클라이언트 인증은 메시지에 직접 클라이언트 자격 증명을 추가 하 여 수행 됩니다. 그러면 전송 보안 모드의 성능 이점을 유지 하면서 클라이언트 인증에 대해 메시지 보안 모드에서 지 원하는 모든 자격 증명 형식을 사용할 수 있습니다.  
  
 이 샘플에서는 `UserName` 자격 증명 형식을 사용하여 클라이언트를 서비스에 인증합니다.  
  
 이 샘플은 계산기 서비스를 구현 하는 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md) 을 기반으로 합니다. `wsHttpBinding` 바인딩은 클라이언트 및 서비스의 애플리케이션 구성 파일에서 지정 및 구성됩니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 샘플의 프로그램 코드는 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md) 서비스의 코드와 거의 동일 합니다. 서비스 계약에서 제공되는 추가 작업으로 `GetCallerIdentity`가 있습니다. 이 작업에서는 호출자의 ID 이름을 호출자에게 반환합니다.  

```csharp
public string GetCallerIdentity()  
{  
    // Use ServiceSecurityContext.WindowsIdentity to get the name of the caller.  
    return ServiceSecurityContext.Current.WindowsIdentity.Name;  
}  
```

 샘플을 빌드하고 실행하기 전에 Web Server Certificate Wizard를 사용하여 인증서를 만들고 할당해야 합니다. 구성 파일 설정의 엔드포인트 정의와 바인딩 정의를 사용하면 클라이언트의 다음 샘플 구성에 표시된 것과 같이 `TransportWithMessageCredential` 보안 모드를 활성화할 수 있습니다.  
  
```xml  
<system.serviceModel>  
  <client>  
    <endpoint name=""  
              address="https://localhost/servicemodelsamples/service.svc"   
              binding="wsHttpBinding"   
              bindingConfiguration="Binding1"   
              contract="Microsoft.ServiceModel.Samples.ICalculator" />  
  </client>  
  
  <bindings>  
    <wsHttpBinding>  
      <!--   
        This configuration defines the security mode as TransportWithMessageCredential.  
        and the clientCredentialType as UserName.  
        -->  
      <binding name="Binding1">  
        <security mode ="TransportWithMessageCredential">  
          <message clientCredentialType="UserName" />  
        </security>  
      </binding>  
    </wsHttpBinding>  
  </bindings>  
</system.serviceModel>  
```  
  
 지정된 주소에서는 https:// 체계를 사용합니다. 바인딩 구성에서는 보안 모드를 `TransportWithMessageCredential`로 설정합니다. 서비스의 Web.config 파일에도 같은 보안 모드를 지정해야 합니다.  
  
 이 샘플에 사용 된 인증서는 makecert.exe를 사용 하 여 만든 테스트 인증서 이므로 브라우저에서와 `https://localhost/servicemodelsamples/service.svc`같은 https: 주소에 액세스 하려고 하면 보안 경고가 나타납니다. WCF 클라이언트가 테스트 인증서를 사용 하 여 작동 하도록 허용 하기 위해 일부 추가 코드를 클라이언트에 추가 하 여 보안 경고를 표시 하지 않습니다. 이 코드 및 함께 사용되는 클래스는 프로덕션 인증서를 사용할 때에는 필요가 없습니다.  

```csharp
// WARNING: This code is only needed for test certificates such as those created by makecert. It is   
// not recommended for production code.  
PermissiveCertificatePolicy.Enact("CN=ServiceModelSamples-HTTPS-Server");  
```
  
 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.  
  
```  
Username authentication required.  
Provide a valid machine or domain account. [domain\\user]  
   Enter username:   
YourDomainName\YourAccountName  
   Enter password:   
********  
YourDomainName\YourAccountName  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. [인터넷 정보 서비스 (IIS) 서버 인증서 설치 지침](../../../../docs/framework/wcf/samples/iis-server-certificate-installation-instructions.md)을 수행 했는지 확인 합니다.  
  
3. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
4. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
