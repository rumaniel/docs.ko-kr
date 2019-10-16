---
title: Message Security Anonymous
ms.date: 03/30/2017
helpviewer_keywords:
- WS Security
ms.assetid: c321cbf9-8c05-4cce-b5a5-4bf7b230ee03
ms.openlocfilehash: fdcf0c25e4e6cab2c99457112b892f5d2c5bd3b4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69930618"
---
# <a name="message-security-anonymous"></a>Message Security Anonymous
Message Security Anonymous 샘플에서는 클라이언트 인증 없이 메시지 수준 보안을 사용 하지만 서버의 x.509을 사용 하 여 서버를 인증 해야 하는 WCF (Windows Communication Foundation) 응용 프로그램을 구현 하는 방법을 보여 줍니다. 인증서. 클라이언트와 서버 간의 모든 응용 프로그램 메시지는 서명 및 암호화됩니다. 이 샘플은 [WSHttpBinding](../../../../docs/framework/wcf/samples/wshttpbinding.md) 샘플을 기반으로 합니다. 이 샘플은 IIS(인터넷 정보 서비스)에 의해 호스트되는 클라이언트 콘솔 프로그램(.exe) 및 서비스 라이브러리(.dll)로 구성됩니다. 이 서비스는 요청-회신 통신 패턴을 정의하는 계약을 구현합니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

 이 샘플은 클라이언트가 인증되지 않은 경우 `True`를 반환하는 새 작업을 계산기 인터페이스에 추가합니다.

```csharp
public class CalculatorService : ICalculator
{
    public bool IsCallerAnonymous()
    {
        // ServiceSecurityContext.IsAnonymous returns true if the caller is not authenticated.
        return ServiceSecurityContext.Current.IsAnonymous;
    }
    ...
}
```

 서비스는 구성 파일(Web.config)을 사용하여 서비스와 통신하기 위한 단일 엔드포인트를 노출합니다. 끝점은 하나의 주소, 바인딩 및 계약으로 구성됩니다. 바인딩은 `wsHttpBinding` 바인딩을 사용하여 구성됩니다. `wsHttpBinding` 바인딩의 기본 보안 모드는 `Message`입니다. `clientCredentialType` 특성은 `None`으로 설정됩니다.

```xml
<system.serviceModel>

  <protocolMapping>
    <add scheme="http" binding="wsHttpBinding" />
  </protocolMapping>

  <bindings>
    <wsHttpBinding>
     <!-- This configuration defines the security mode as Message and -->
     <!-- the clientCredentialType as None. This mode provides -->
     <!-- server authentication only using the service certificate. -->

     <binding>
       <security mode="Message">
         <message clientCredentialType="None" />
       </security>
     </binding>
    </wsHttpBinding>
  </bindings>
  ...
</system.serviceModel>
```

 서비스 인증에 사용할 자격 증명은 [ \<> 동작](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)에서 지정 됩니다. 다음 샘플 코드와 같이 서버 인증서는 `SubjectName` 특성에 지정된 값과 동일한 `findValue` 값을 포함해야 합니다.

```xml
<behaviors>
  <serviceBehaviors>
    <behavior>
      <!--
    The serviceCredentials behavior allows you to define a service certificate.
    A service certificate is used by a client to authenticate the service and provide message protection.
    This configuration references the "localhost" certificate installed during the setup instructions.
    -->
      <serviceCredentials>
        <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />
      </serviceCredentials>
      <serviceMetadata httpGetEnabled="True"/>
      <serviceDebug includeExceptionDetailInFaults="False" />
    </behavior>
  </serviceBehaviors>
</behaviors>
```

 클라이언트 끝점 구성은 서비스 끝점의 절대 주소, 바인딩 및 계약으로 구성됩니다. `wsHttpBinding` 바인딩의 클라이언트 보안 모드는 `Message`입니다. `clientCredentialType` 특성은 `None`으로 설정됩니다.

```xml
<system.serviceModel>
  <client>
    <endpoint name=""
             address="http://localhost/servicemodelsamples/service.svc"
             binding="wsHttpBinding"
             behaviorConfiguration="ClientCredentialsBehavior"
             bindingConfiguration="Binding1"
             contract="Microsoft.ServiceModel.Samples.ICalculator" />
  </client>

  <bindings>
    <wsHttpBinding>
      <!--This configuration defines the security mode as -->
      <!--Message and the clientCredentialType as None. -->
      <binding name="Binding1">
        <security mode = "Message">
          <message clientCredentialType="None"/>
        </security>
      </binding>
    </wsHttpBinding>
  </bindings>
  ...
</system.serviceModel>
```

 서비스의 인증서를 인증하기 위해 샘플에서는 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A>가 <xref:System.ServiceModel.Security.X509CertificateValidationMode.PeerOrChainTrust>로 설정됩니다. 클라이언트의 App.config 파일에 있는 `behaviors` 섹션에서 이 작업을 수행합니다. 이는 인증서가 사용자의 신뢰할 수 있는 사용자 저장소에 있는 경우 인증서의 발급자 체인에 대한 유효성 검사를 수행하지 않고 인증서가 신뢰된다는 것을 의미합니다. 여기서 이 설정은 편의상 사용된 것이므로 CA(인증 기관)에서 발급된 인증서를 요구하지 않고 샘플을 실행할 수 있습니다. 이 설정은 기본 ChainTrust보다 덜 안전합니다. 프로덕션 코드에서 `PeerOrChainTrust`를 사용하기 전에 이 설정의 보안 문제를 신중하게 고려해야 합니다.

 클라이언트 구현은 `IsCallerAnonymous` 메서드에 대 한 호출을 추가 하 고, 그렇지 않은 경우 [WSHttpBinding](../../../../docs/framework/wcf/samples/wshttpbinding.md) 샘플과는 다릅니다.

```csharp
// Create a client with a client endpoint configuration.
CalculatorClient client = new CalculatorClient();

// Call the GetCallerIdentity operation.
Console.WriteLine("IsCallerAnonymous returned: {0}", client.IsCallerAnonymous());

// Call the Add service operation.
double value1 = 100.00D;
double value2 = 15.99D;
double result = client.Add(value1, value2);
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);

...

//Closing the client gracefully closes the connection and cleans up resources.
client.Close();

Console.WriteLine();
Console.WriteLine("Press <ENTER> to terminate client.");
Console.ReadLine();
```

 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.

```
IsCallerAnonymous returned: True
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714
Press <ENTER> to terminate client.
```

 Message Security Anonymous 샘플에 포함된 Setup.bat 배치 파일을 사용하면 인증서 기반 보안이 필요한 호스트된 응용 프로그램을 실행하도록 관련 인증서가 있는 서버를 구성할 수 있습니다. 배치 파일은 두 가지 모드로 실행될 수 있습니다. 단일 컴퓨터 모드에서 배치 파일을 실행하려면 명령줄에 `setup.bat`를 입력합니다. 서비스 모드에서 실행하려면 `setup.bat service`를 입력합니다. 다중 컴퓨터 구성에서 샘플을 실행할 경우 이 모드를 사용합니다. 자세한 내용은 이 항목의 끝에 있는 설치 절차를 참조하세요.

 다음은 배치 파일의 여러 다른 섹션에 대한 간략한 개요입니다.

- 서버 인증서 만들기

     Setup.bat 배치 파일에서 다음 행은 사용할 서버 인증서를 만듭니다.

    ```bat
    echo ************
    echo Server cert setup starting
    echo %SERVER_NAME%
    echo ************
    echo making server cert
    echo ************
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe
    ```

     %SERVER_NAME% 변수는 서버 이름을 지정합니다. 인증서는 LocalMachine 저장소에 저장됩니다. `setup.bat service` 등의 서비스 인수와 함께 설치 배치 파일을 실행하는 경우 %SERVER_NAME%에는 컴퓨터의 정규화된 도메인 이름이 포함됩니다. 그렇지 않은 경우 기본적으로 localhost입니다.

- 클라이언트의 신뢰할 수 있는 인증서 저장소에 서버 인증서 설치

     다음 줄은 클라이언트의 신뢰할 수 있는 사용자 저장소에 서버 인증서를 복사합니다. 이 단계는 Makecert.exe에서 생성한 인증서를 클라이언트 컴퓨터에서 절대적으로 신뢰하지는 않기 때문에 필요합니다. Microsoft에서 발급한 인증서와 같이 클라이언트가 신뢰할 수 있는 루트 인증서를 기반으로 하는 인증서가 이미 있는 경우 클라이언트 인증서 저장소를 서버 인증서로 채우는 이 단계를 수행할 필요가 없습니다.

    ```
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople
    ```

- 인증서의 프라이빗 키에 대한 사용 권한 부여

     설정 .bat 배치 파일의 다음 줄은 LocalMachine 저장소에 저장 된 서버 인증서를 ASP.NET 작업자 프로세스 계정에 액세스할 수 있도록 합니다.

    ```bat
    echo ************
    echo setting privileges on server certificates
    echo ************
    for /F "delims=" %%i in ('"%MSSDK%\bin\FindPrivateKey.exe" My LocalMachine -n CN^=%SERVER_NAME% -a') do set PRIVATE_KEY_FILE=%%i set WP_ACCOUNT=NT AUTHORITY\NETWORK SERVICE
    (ver | findstr "5.1") && set WP_ACCOUNT=%COMPUTERNAME%\ASPNET
    echo Y|cacls.exe "%PRIVATE_KEY_FILE%" /E /G "%WP_ACCOUNT%":R
    iisreset
    ```

> [!NOTE]
> 미국 영어 버전이 아닌 Windows 버전을 사용하는 경우 Setup.bat 파일을 편집하여 `NT AUTHORITY\NETWORK SERVICE` 계정 이름을 해당 국가별 계정 이름으로 바꾸어야 합니다.

### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.

2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.

### <a name="to-run-the-sample-on-the-same-computer"></a>단일 컴퓨터 구성에서 샘플을 실행하려면

1. Makecert.exe 및 FindPrivateKey.exe가 있는 폴더가 경로에 포함되는지 확인합니다.

2. Visual Studio에 대 한 개발자 명령 프롬프트의 샘플 설치 폴더에서 Setup.exe를 실행 하 여 관리자 권한으로 실행 합니다. 이 작업은 샘플 실행에 필요한 모든 인증서를 설치합니다.

    > [!NOTE]
    > 설치 배치 파일은 Visual Studio 용 개발자 명령 프롬프트에서 실행 되도록 설계 되었습니다. PATH 환경 변수는 SDK가 설치되는 디렉터리를 가리켜야 합니다. 이 환경 변수는 Visual Studio에 대 한 개발자 명령 프롬프트 내에서 자동으로 설정 됩니다.  
  
3. 주소 `http://localhost/servicemodelsamples/service.svc`를 입력 하 여 브라우저를 사용 하 여 서비스에 대 한 액세스를 확인 합니다.  
  
4. \client\bin에서 Client.exe를 실행합니다. 클라이언트 콘솔 애플리케이션에 클라이언트 동작이 표시됩니다.  
  
5. 클라이언트와 서비스가 통신할 수 없는 경우 [WCF 샘플에 대 한 문제 해결 팁](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))을 참조 하세요.  
  
### <a name="to-run-the-sample-across-computers"></a>다중 컴퓨터 구성에서 샘플을 실행하려면  
  
1. 서비스 컴퓨터에 디렉터리를 만듭니다. IIS(인터넷 정보 서비스) 관리 도구를 사용하여 이 디렉터리에 servicemodelsamples라는 가상 응용 프로그램을 만듭니다.  
  
2. \inetpub\wwwroot\servicemodelsamples에서 서비스 컴퓨터의 가상 디렉터리로 서비스 프로그램 파일을 복사합니다. \bin 하위 디렉터리에 파일을 복사해야 합니다. Setup.bat 및 Cleanup.bat 파일도 서비스 컴퓨터로 복사합니다.  
  
3. 클라이언트 컴퓨터에 클라이언트 이진 파일용 디렉터리를 만듭니다.  
  
4. 클라이언트 프로그램 파일을 클라이언트 컴퓨터의 클라이언트 디렉터리로 복사합니다. Setup.bat, Cleanup.bat 및 ImportServiceCert.bat 파일도 클라이언트로 복사합니다.  
  
5. 서버에서 관리자 권한으로 `setup.bat service` 연 Visual Studio 용 개발자 명령 프롬프트를 실행 합니다. 인수`service` 를 사용 하 여를 실행 하면 컴퓨터의 정규화 된 도메인 이름으로 서비스 인증서가 생성 되 `setup.bat` 고 서비스 인증서가 이름이 .cer 인 파일로 내보내집니다.  
  
6. 컴퓨터의 정규화 된 도메인 이름과 같은 새 인증서 이름 ( `findValue` [ \<serviceCertificate >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)특성)을 반영 하도록 web.config를 편집 합니다.  
  
7. 서비스 디렉터리에서 클라이언트 컴퓨터의 클라이언트 디렉터리로 Service.cer 파일을 복사합니다.  
  
8. 클라이언트 컴퓨터의 Client.exe.config 파일에서 엔드포인트의 주소 값을 서비스의 새 주소와 일치하도록 변경합니다.  
  
9. 클라이언트에서 관리자 권한으로 연 Visual Studio 용 개발자 명령 프롬프트 열고 importservicecert.bat를 실행 합니다. 이 작업은 Service.cer 파일의 서비스 인증서를 CurrentUser - TrustedPeople 저장소로 가져옵니다.  
  
10. 클라이언트 컴퓨터의 명령 프롬프트에서 Client.exe를 실행합니다. 클라이언트와 서비스가 통신할 수 없는 경우 [WCF 샘플에 대 한 문제 해결 팁](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))을 참조 하세요.  
  
### <a name="to-clean-up-after-the-sample"></a>샘플 실행 후 정리를 수행하려면  
  
- 샘플 실행을 완료한 후 샘플 폴더에서 Cleanup.bat를 실행합니다.  
  
> [!NOTE]
> 다중 컴퓨터 구성에서 이 샘플을 실행할 경우에는 이 스크립트로 클라이언트의 서비스 인증서를 제거할 수 없습니다. 컴퓨터에서 인증서를 사용 하는 WCF (Windows Communication Foundation) 샘플을 실행 한 경우에는 CurrentUser-비트 사용자 저장소에 설치 된 서비스 인증서를 지워야 합니다. 이렇게 하려면 다음 명령을 사용 합니다. `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` 예를 들면 다음과 같습니다. `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com.`
