---
title: 메시지 큐에 대한 메시지 보안
ms.date: 03/30/2017
ms.assetid: 329aea9c-fa80-45c0-b2b9-e37fd7b85b38
ms.openlocfilehash: 039ec21296392321fec40df2cae7383ccb3be6ea
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70039348"
---
# <a name="message-security-over-message-queuing"></a>메시지 큐에 대한 메시지 보안
이 샘플에서는 클라이언트에 대해 X.509v3 인증서를 통한 WS-Security 인증을 사용하며 MSMQ를 통해 서버의 X.509v3 인증서를 사용한 서버 인증을 수행해야 하는 응용 프로그램의 구현 방법을 보여 줍니다. 메시지 보안에서는 MSMQ 저장소에 있는 메시지의 암호화가 유지되며 응용 프로그램에서 메시지의 자체 인증을 수행할 수 있도록 하는 것이 더 좋습니다.

 이 샘플은 [트랜잭션 된 MSMQ 바인딩](../../../../docs/framework/wcf/samples/transacted-msmq-binding.md) 샘플을 기반으로 합니다. 메시지가 암호화되고 서명됩니다.

### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.

2. 서비스가 처음 실행되는 경우 서비스에서는 큐가 있는지 확인하고 큐가 없으면 큐를 만듭니다. 서비스를 처음 실행하여 큐를 만들거나 MSMQ 큐 관리자를 통해 큐를 만들 수 있습니다. Windows 2008에서 큐를 만들려면 다음 단계를 수행하세요.

    1. Visual Studio 2012에서 서버 관리자를 엽니다.

    2. **기능** 탭을 확장 합니다.

    3. **개인 메시지 큐**를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**, **개인 큐**를 선택 합니다.

    4. **트랜잭션** 상자를 확인 합니다.

    5. 새 `ServiceModelSamplesTransacted` 큐의 이름으로을 입력 합니다.

3. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.

### <a name="to-run-the-sample-on-the-same-computer"></a>단일 컴퓨터 구성에서 샘플을 실행하려면

1. Makecert.exe 및 FindPrivateKey.exe가 포함된 폴더가 경로에 있는지 확인합니다.

2. 샘플 설치 폴더에서 Setup.bat를 실행하여 이 작업은 샘플 실행에 필요한 모든 인증서를 설치합니다.

    > [!NOTE]
    > 샘플 사용을 마쳤으면 Cleanup.bat를 실행하여 인증서를 제거해야 합니다. 다른 보안 샘플에도 동일한 인증서가 사용됩니다.  
  
3. \service\bin에서 Service.exe를 실행합니다.  
  
4. \client\bin에서 Client.exe를 실행합니다. 클라이언트 콘솔 애플리케이션에 클라이언트 동작이 표시됩니다.  
  
5. 클라이언트와 서비스가 통신할 수 없는 경우 [WCF 샘플에 대 한 문제 해결 팁](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))을 참조 하세요.  
  
### <a name="to-run-the-sample-across-computers"></a>다중 컴퓨터 구성에서 샘플을 실행하려면  
  
1. Setup.bat, Cleanup.bat 및 ImportClientCert.bat 파일을 서비스 컴퓨터에 복사합니다.  
  
2. 클라이언트 컴퓨터에 클라이언트 이진 파일용 디렉터리를 만듭니다.  
  
3. 클라이언트 프로그램 파일을 클라이언트 컴퓨터의 클라이언트 디렉터리로 복사합니다. Setup.bat, Cleanup.bat 및 ImportServiceCert.bat 파일도 클라이언트로 복사합니다.  
  
4. 서버에서 `setup.bat service`를 실행합니다. 인수`service` 를 사용 하 여를 실행 하면 컴퓨터의 정규화 된 도메인 이름으로 서비스 인증서가 생성 되 `setup.bat` 고 서비스 인증서가 이름이 .cer 인 파일로 내보내집니다.  
  
5. 컴퓨터의 정규화 된 도메인 이름과 같은 새 인증서 이름 ( `findValue` [ \<serviceCertificate >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)특성에서)을 반영 하도록 서비스의 setup.exe를 편집 합니다.  
  
6. 서비스 디렉터리에서 클라이언트 컴퓨터의 클라이언트 디렉터리로 Service.cer 파일을 복사합니다.  
  
7. 클라이언트에서 `setup.bat client`를 실행합니다. `setup.bat` 인수를 사용하여 `client`를 실행하면 client.com이라는 클라이언트 인증서가 생성되어 Client.cer이라는 파일로 내보내집니다.  
  
8. 클라이언트 컴퓨터의 Client.exe.config 파일에서 엔드포인트의 주소 값을 서비스의 새 주소와 일치하도록 변경합니다. 이렇게 하려면 localhost를 서버의 정규화된 도메인 이름으로 바꿉니다.  서비스의 인증서 이름도 서비스 컴퓨터의 정규화된 도메인 이름과 일치하게 변경해야 합니다(`findValue`에 있는 `defaultCertificate`의 `serviceCertificate` 요소에 있는 `clientCredentials` 특성).  
  
9. 클라이언트 디렉터리에서 서버의 서비스 디렉터리로 Client.cer 파일을 복사합니다.  
  
10. 클라이언트에서 `ImportServiceCert.bat`를 실행합니다. 이 작업은 Service.cer 파일의 서비스 인증서를 CurrentUser - TrustedPeople 저장소로 가져옵니다.  
  
11. 서버에서 `ImportClientCert.bat`를 실행하여 Client.cer 파일에서 LocalMachine - TrustedPeople 저장소로 클라이언트 인증서를 가져옵니다.  
  
12. 서비스 컴퓨터의 명령 프롬프트에서 Service.exe를 실행합니다.  
  
13. 클라이언트 컴퓨터의 명령 프롬프트에서 Client.exe를 실행합니다. 클라이언트와 서비스가 통신할 수 없는 경우 [WCF 샘플에 대 한 문제 해결 팁](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))을 참조 하세요.  
  
### <a name="to-clean-up-after-the-sample"></a>샘플 실행 후 정리를 수행하려면  
  
- 샘플 실행을 완료했으면 샘플 폴더에서 Cleanup.bat를 실행합니다.  
  
    > [!NOTE]
    > 다중 컴퓨터 구성에서 이 샘플을 실행할 경우에는 이 스크립트로 클라이언트의 서비스 인증서를 제거할 수 없습니다. 컴퓨터에서 인증서를 사용 하는 WCF (Windows Communication Foundation) 샘플을 실행 한 경우에는 CurrentUser-비트 사용자 저장소에 설치 된 서비스 인증서를 지워야 합니다. 이렇게 하려면 다음 명령을 사용 합니다. `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`예를 들면 `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`와 같습니다.

## <a name="requirements"></a>요구 사항
 이 샘플을 실행하려면 MSMQ가 설치되어 실행 중이어야 합니다.

## <a name="demonstrates"></a>세부 항목
 클라이언트는 서비스의 공개 키를 사용하여 메시지를 암호화하고 자체 인증서로 메시지에 서명합니다. 큐로부터 메시지를 읽는 서비스는 신뢰할 수 있는 사용자 저장소에 포함된 인증서를 사용하여 클라이언트 인증서를 인증합니다. 그리고 메시지를 해독한 후 서비스 작업에 디스패치합니다.

 Windows Communication Foundation (WCF) 메시지는 MSMQ 메시지 본문에서 페이로드로 전달 되기 때문에 본문은 MSMQ 저장소에서 암호화 된 상태로 유지 됩니다. 그러면 원치 않는 노출로부터 메시지를 보호할 수 있습니다. MSMQ 자체에서는 전달하는 메시지의 암호화 여부를 인식하지 못합니다.

 샘플에서는 MSMQ에서 메시지 수준의 상호 인증을 사용하는 방법을 보여 줍니다. 인증서는 out-of-band로 교환됩니다. 대기 중인 응용 프로그램의 경우에는 서비스와 클라이언트가 동시에 실행 중이어야 할 필요가 없기 때문에 항상 적용됩니다.

## <a name="description"></a>설명
 샘플 클라이언트 및 서비스 코드는 한 가지 차이점이 있는 [트랜잭션 된 MSMQ 바인딩](../../../../docs/framework/wcf/samples/transacted-msmq-binding.md) 샘플과 같습니다. 작업 계약에는 보호 수준에서 주석을 달아야 하기 때문에 메시지에 서명과 암호화가 필요합니다.

```csharp
// Define a service contract.
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]
public interface IOrderProcessor
{
    [OperationContract(IsOneWay = true, ProtectionLevel=ProtectionLevel.EncryptAndSign)]
    void SubmitPurchaseOrder(PurchaseOrder po);
}
```

 필수 토큰을 사용하여 서비스 및 클라이언트를 식별하는 방식으로 메시지를 보호할 수 있도록 App.config에는 자격 증명 정보가 포함됩니다.

 클라이언트 구성에서는 서비스를 인증할 서비스 인증서를 지정합니다. 여기서는 LocalMachine 저장소를 서비스의 유효성에 의존하는 신뢰할 수 있는 저장소로 사용합니다. 여기서는 클라이언트의 서비스 인증을 위해 메시지와 함께 첨부되는 클라이언트 인증서도 지정합니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>

  <system.serviceModel>

    <client>
      <!-- Define NetMsmqEndpoint -->
      <endpoint address="net.msmq://localhost/private/ServiceModelSamplesMessageSecurity"
                binding="netMsmqBinding"
                bindingConfiguration="messageSecurityBinding"
                contract="Microsoft.ServiceModel.Samples.IOrderProcessor"
                behaviorConfiguration="ClientCertificateBehavior" />
    </client>

    <bindings>
        <netMsmqBinding>
            <binding name="messageSecurityBinding">
                <security mode="Message">
                    <message clientCredentialType="Certificate"/>
                </security>
            </binding>
        </netMsmqBinding>
    </bindings>

    <behaviors>
      <endpointBehaviors>
        <behavior name="ClientCertificateBehavior">
          <!--
        The clientCredentials behavior allows one to define a certificate to present to a service.
        A certificate is used by a client to authenticate itself to the service and provide message integrity.
        This configuration references the "client.com" certificate installed during the setup instructions.
        -->
          <clientCredentials>
            <clientCertificate findValue="client.com" storeLocation="CurrentUser" storeName="My" x509FindType="FindBySubjectName" />
            <serviceCertificate>
                <defaultCertificate findValue="localhost" storeLocation="CurrentUser" storeName="TrustedPeople" x509FindType="FindBySubjectName"/>
              <!--
            Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate
            is in the user's Trusted People store, then it is trusted without performing a
            validation of the certificate's issuer chain. This setting is used here for convenience so that the
            sample can be run without having to have certificates issued by a certification authority (CA).
            This setting is less secure than the default, ChainTrust. The security implications of this
            setting should be carefully considered before using PeerOrChainTrust in production code.
            -->
              <authentication certificateValidationMode="PeerOrChainTrust" />
            </serviceCertificate>
          </clientCredentials>
        </behavior>
      </endpointBehaviors>
    </behaviors>

  </system.serviceModel>
</configuration>
```

 보안 모드는 Message로 설정되며 ClientCredentialType은 Certificate로 설정됩니다.

 서비스 구성에는 클라이언트에서 서비스를 인증할 때 사용된 서비스의 자격 증명을 지정하는 서비스 동작이 포함됩니다. 서버 인증서 주체 이름은 `findValue` [ \<serviceCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)의 특성에 지정 됩니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>

  <appSettings>
    <!-- Use appSetting to configure MSMQ queue name. -->
    <add key="queueName" value=".\private$\ServiceModelSamplesMessageSecurity" />
  </appSettings>

  <system.serviceModel>
    <services>
      <service
          name="Microsoft.ServiceModel.Samples.OrderProcessorService"
          behaviorConfiguration="PurchaseOrderServiceBehavior">
        <host>
          <baseAddresses>
            <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>
          </baseAddresses>
        </host>
        <!-- Define NetMsmqEndpoint -->
        <endpoint address="net.msmq://localhost/private/ServiceModelSamplesMessageSecurity"
                  binding="netMsmqBinding"
                  bindingConfiguration="messageSecurityBinding"
                  contract="Microsoft.ServiceModel.Samples.IOrderProcessor" />
        <!-- The mex endpoint is exposed at http://localhost:8000/ServiceModelSamples/service/mex. -->
        <endpoint address="mex"
                  binding="mexHttpBinding"
                  contract="IMetadataExchange" />
      </service>
    </services>

    <bindings>
        <netMsmqBinding>
            <binding name="messageSecurityBinding">
                <security mode="Message">
                    <message clientCredentialType="Certificate" />
                </security>
            </binding>
        </netMsmqBinding>
    </bindings>

    <behaviors>
      <serviceBehaviors>
        <behavior name="PurchaseOrderServiceBehavior">
          <serviceMetadata httpGetEnabled="True"/>
          <!--
               The serviceCredentials behavior allows one to define a service certificate.
               A service certificate is used by the service to authenticate itself to its clients and to provide message protection.
               This configuration references the "localhost" certificate installed during the setup instructions.
          -->
          <serviceCredentials>
            <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />
            <clientCertificate>
                <certificate findValue="client.com" storeLocation="LocalMachine" storeName="TrustedPeople" x509FindType="FindBySubjectName"/>
              <!--
            Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate
            is in the user's Trusted People store, then it is trusted without performing a
            validation of the certificate's issuer chain. This setting is used here for convenience so that the
            sample can be run without having to have certificates issued by a certification authority (CA).
            This setting is less secure than the default, ChainTrust. The security implications of this
            setting should be carefully considered before using PeerOrChainTrust in production code.
            -->
              <authentication certificateValidationMode="PeerOrChainTrust" />
            </clientCertificate>
          </serviceCredentials>
        </behavior>
      </serviceBehaviors>
    </behaviors>

  </system.serviceModel>

</configuration>
```

 이 샘플에서는 다음 샘플 코드에서와 같이 구성을 이용하여 인증을 제어하는 방법과 보안 컨텍스트에서 호출자의 ID를 가져오는 방법을 보여 줍니다.

```csharp
// Service class which implements the service contract.
// Added code to write output to the console window.
public class OrderProcessorService : IOrderProcessor
{
    private string GetCallerIdentity()
    {
        // The client certificate is not mapped to a Windows identity by default.
        // ServiceSecurityContext.PrimaryIdentity is populated based on the information
        // in the certificate that the client used to authenticate itself to the service.
        return ServiceSecurityContext.Current.PrimaryIdentity.Name;
    }

    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]
    public void SubmitPurchaseOrder(PurchaseOrder po)
    {
        Console.WriteLine("Client's Identity {0} ", GetCallerIdentity());
        Orders.Add(po);
        Console.WriteLine("Processing {0} ", po);
    }
  //…
}
```

 서비스 코드를 실행하면 클라이언트 ID가 표시됩니다. 다음은 서비스 코드의 출력 샘플입니다.

```
The service is ready.
Press <ENTER> to terminate service.

Client's Identity CN=client.com; ECA6629A3C695D01832D77EEE836E04891DE9D3C
Processing Purchase Order: 6536e097-da96-4773-9da3-77bab4345b5d
        Customer: somecustomer.com
        OrderDetails
                Order LineItem: 54 of Blue Widget @unit price: $29.99
                Order LineItem: 890 of Red Widget @unit price: $45.89
        Total cost of this order: $42461.56
        Order status: Pending
```

## <a name="comments"></a>설명

- 클라이언트 인증서 만들기

     배치 파일의 다음 줄에서는 클라이언트 인증서를 만듭니다. 지정된 클라이언트 이름은 만든 인증서의 제목 이름에 사용됩니다. 인증서는 `My` 저장소 위치에 있는 `CurrentUser` 저장소에 저장됩니다.

    ```bat
    echo ************
    echo making client cert
    echo ************
    makecert.exe -sr CurrentUser -ss MY -a sha1 -n CN=%CLIENT_NAME% -sky exchange -pe
    ```

- 서버의 신뢰할 수 있는 인증서 저장소에 클라이언트 인증서 설치.

     배치 파일의 다음 줄에서는 서버에서 관련된 신뢰 여부를 결정할 수 있도록 서버의 TrustedPeople 저장소에 클라이언트 인증서를 복사합니다. 신뢰할 수 있는 사용자 저장소에 설치 된 인증서를 WCF (Windows Communication Foundation) 서비스에서 신뢰할 수 있도록 하려면 클라이언트 인증서 유효성 검사 모드를 또는 `PeerOrChainTrust` `PeerTrust` 값으로 설정 해야 합니다. 구성 파일을 사용하여 이런 작업을 수행하는 방법을 보려면 앞서 소개된 서비스 구성 샘플을 참조하십시오.

    ```bat
    echo ************
    echo copying client cert to server's LocalMachine store
    echo ************
    certmgr.exe -add -r CurrentUser -s My -c -n %CLIENT_NAME% -r LocalMachine -s TrustedPeople
    ```

- 서버 인증서 만들기

     Setup.bat 배치 파일에서 다음 줄은 사용할 서버 인증서를 만듭니다.

    ```bat
    echo ************
    echo Server cert setup starting
    echo %SERVER_NAME%
    echo ************
    echo making server cert
    echo ************
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe
    ```

     %SERVER_NAME% 변수는 서버 이름을 지정합니다. 인증서는 LocalMachine 저장소에 저장됩니다. 서비스의 인수 (예: `setup.bat service`)를 사용 하 여 설치 일괄 처리 파일을 실행 하는 경우% 서비스 이름%에는 컴퓨터의 정규화 된 도메인 이름이 포함 됩니다. 그렇지 않은 경우 기본값은 localhost입니다.

- 클라이언트의 신뢰할 수 있는 인증서 저장소에 서버 인증서 설치

     다음 줄은 클라이언트의 신뢰할 수 있는 사용자 저장소에 서버 인증서를 복사합니다. 이 단계는 Makecert.exe에서 생성한 인증서를 클라이언트 컴퓨터에서 절대적으로 신뢰하지는 않기 때문에 필요합니다. Microsoft에서 발급한 인증서와 같이 클라이언트가 신뢰할 수 있는 루트 인증서를 기반으로 하는 인증서가 이미 있는 경우 클라이언트 인증서 저장소를 서버 인증서로 채우는 이 단계를 수행할 필요가 없습니다.

    ```
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople
    ```

    > [!NOTE]
    > 미국 영어 버전이 아닌 Microsoft Windows 버전을 사용하는 경우 Setup.bat 파일을 편집하여 "NT AUTHORITY\NETWORK SERVICE" 계정 이름을 해당 국가별 계정 이름으로 바꿔야 합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Net\MSMQ\MessageSecurity`  
