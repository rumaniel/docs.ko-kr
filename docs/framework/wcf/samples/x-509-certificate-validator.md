---
title: X.509 Certificate Validator
ms.date: 03/30/2017
ms.assetid: 3b042379-02c4-4395-b927-e57c842fd3e0
ms.openlocfilehash: 628e4e12e1eafb6101503a59e3393777f9c30989
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67424634"
---
# <a name="x509-certificate-validator"></a>X.509 Certificate Validator

이 샘플에서는 사용자 지정 X.509 인증서 유효성 검사기를 구현하는 방법을 보여 줍니다. 이 방법은 기본 제공되는 X.509 인증서 유효성 검사기 중에서 애플리케이션의 요구 사항에 적절한 것이 없는 경우에 유용합니다. 이 샘플에서는 자체 발급된 인증서를 승인하는 사용자 지정 유효성 검사기가 있는 서비스를 보여 줍니다. 그런 인증서를 사용하여 클라이언트가 서비스에 인증합니다.

참고: 자체 발급 된 인증서를 생성할 수 있습니다 누구나 서비스에서 사용 하는 사용자 지정 유효성 검사기는 ChainTrust X509CertificateValidationMode에서 제공 하는 기본 동작 보다 덜 안전 합니다. 이 경우 프로덕션 코드에서 이 유효성 검사 논리를 사용하기 전에 보안 상의 영향을 세심하게 고려해야 합니다.

요약하면, 이 샘플에서는 다음 방법을 보여 줍니다.

- X.509 인증서를 사용하여 클라이언트를 인증하는 방법.

- 서버에서 사용자 지정 X509CertificateValidator를 기준으로 클라이언트의 유효성을 검증하는 방법.

- 서버의 X.509 인증서를 사용하여 서버를 인증하는 방법

서비스에서는 서비스와의 통신에 사용할 수 있는 단일 엔드포인트를 노출하며, 이 엔드포인트는 App.config 구성 파일을 사용하여 정의합니다. 엔드포인트는 하나의 주소, 바인딩 및 계약으로 구성됩니다. 표준 바인딩이 구성 된 `wsHttpBinding` 는 기본적으로 사용 `WSSecurity` 및 클라이언트 인증서 인증 합니다. 서비스 동작에서는 클라이언트 X.509 인증서의 유효성을 검사하기 위한 사용자 지정 모드와 유효성 검사기 클래스의 형식을 지정합니다. 동작에서는 serviceCertificate 요소를 사용하여 서버 인증서도 지정합니다. 서버 인증서에 대 한 동일한 값을 포함 해야 합니다 `SubjectName` 으로 `findValue` 에 [ \<serviceCertificate >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md).

```xml
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceModel.Samples.CalculatorService"
               behaviorConfiguration="CalculatorServiceBehavior">
        <!-- use host/baseAddresses to configure base address -->
        <!-- provided by host -->
        <host>
          <baseAddresses>
            <add baseAddress =
                "http://localhost:8001/servicemodelsamples/service" />
          </baseAddresses>
        </host>
        <!-- use base address specified above, provide one endpoint -->
        <endpoint address="certificate"
               binding="wsHttpBinding"
               bindingConfiguration="Binding"
               contract="Microsoft.ServiceModel.Samples.ICalculator" />
      </service>
    </services>
    <bindings>
      <wsHttpBinding>
        <!-- X509 certificate binding -->
        <binding name="Binding">
          <security mode="Message">
            <message clientCredentialType="Certificate" />
          </security>
        </binding>
      </wsHttpBinding>
    </bindings>
    <behaviors>
      <serviceBehaviors>
        <behavior name="CalculatorServiceBehavior">
          <serviceDebug includeExceptionDetailInFaults ="true"/>
          <serviceCredentials>
            <!-- The serviceCredentials behavior allows one -->
            <!-- to specify authentication constraints on -->
            <!-- client certificates. -->
            <clientCertificate>
              <!-- Setting the certificateValidationMode to -->
              <!-- Custom means that if the custom -->
              <!-- X509CertificateValidator does NOT throw -->
              <!-- an exception, then the provided certificate -->
              <!-- will be trusted without performing any -->
              <!-- validation beyond that performed by the custom -->
              <!-- validator. The security implications of this -->
              <!-- setting should be carefully considered before -->
              <!-- using Custom in production code. -->
              <authentication
                 certificateValidationMode="Custom"
                 customCertificateValidatorType =
"Microsoft.ServiceModel.Samples.CustomX509CertificateValidator, service" />
            </clientCertificate>
            <!-- The serviceCredentials behavior allows one to -->
            <!-- define a service certificate. -->
            <!-- A service certificate is used by a client to -->
            <!-- authenticate the service and provide message -->
            <!-- protection. This configuration references the -->
            <!-- "localhost" certificate installed during the setup -->
            <!-- instructions. -->
            <serviceCertificate findValue="localhost"
                 storeLocation="LocalMachine"
                 storeName="My" x509FindType="FindBySubjectName" />
          </serviceCredentials>
        </behavior>
      </serviceBehaviors>
    </behaviors>
      </system.serviceModel>
```

클라이언트 엔드포인트 구성은 구성 이름, 서비스 엔드포인트의 절대 주소, 바인딩 및 계약으로 구성됩니다. 클라이언트 바인딩에는 적절한 모드 및 메시지 `clientCredentialType`이 구성됩니다.

```xml
<system.serviceModel>
    <client>
      <!-- X509 certificate based endpoint -->
      <endpoint name="Certificate"
        address=
        "http://localhost:8001/servicemodelsamples/service/certificate"
                binding="wsHttpBinding"
                bindingConfiguration="Binding"
                behaviorConfiguration="ClientCertificateBehavior"
                contract="Microsoft.ServiceModel.Samples.ICalculator">
      </endpoint>
    </client>
    <bindings>
        <wsHttpBinding>
            <!-- X509 certificate binding -->
            <binding name="Binding">
                <security mode="Message">
                    <message clientCredentialType="Certificate" />
               </security>
            </binding>
       </wsHttpBinding>
    </bindings>
    <behaviors>
      <endpointBehaviors>
        <behavior name="ClientCertificateBehavior">
          <clientCredentials>
            <serviceCertificate>
              <!-- Setting the certificateValidationMode to -->
              <!-- PeerOrChainTrust means that if the certificate -->
              <!-- is in the user's Trusted People store, then it -->
              <!-- is trusted without performing a validation of -->
              <!-- the certificate's issuer chain. -->
              <!-- This setting is used here for convenience so -->
              <!-- that the sample can be run without having to -->
              <!-- have certificates issued by a certification -->
              <!-- authority (CA). This setting is less secure -->
              <!-- than the default, ChainTrust. The security -->
              <!-- implications of this setting should be -->
              <!-- carefully considered before using -->
              <!-- PeerOrChainTrust in production code.-->
              <authentication
                  certificateValidationMode="PeerOrChainTrust" />
            </serviceCertificate>
          </clientCredentials>
        </behavior>
      </endpointBehaviors>
    </behaviors>
  </system.serviceModel>
```

클라이언트 구현에서는 사용할 클라이언트 인증서를 설정합니다.

```csharp
// Create a client with Certificate endpoint configuration
CalculatorClient client = new CalculatorClient("Certificate");
try
{
    client.ClientCredentials.ClientCertificate.SetCertificate(StoreLocation.CurrentUser, StoreName.My, X509FindType.FindBySubjectName, "test1");

    // Call the Add service operation.
    double value1 = 100.00D;
    double value2 = 15.99D;
    double result = client.Add(value1, value2);
    Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);

    // Call the Subtract service operation.
    value1 = 145.00D;
    value2 = 76.54D;
    result = client.Subtract(value1, value2);
    Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);

    // Call the Multiply service operation.
    value1 = 9.00D;
    value2 = 81.25D;
    result = client.Multiply(value1, value2);
    Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);

    // Call the Divide service operation.
    value1 = 22.00D;
    value2 = 7.00D;
    result = client.Divide(value1, value2);
    Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);
    client.Close();
}
catch (TimeoutException e)
{
    Console.WriteLine("Call timed out : {0}", e.Message);
    client.Abort();
}
catch (CommunicationException e)
{
    Console.WriteLine("Call failed : {0}", e.Message);
    client.Abort();
}
catch (Exception e)
{
    Console.WriteLine("Call failed : {0}", e.Message);
    client.Abort();
}
```

이 샘플에서는 사용자 지정 X509CertificateValidator를 사용하여 인증서의 유효성을 검사합니다. 샘플에서는 <xref:System.IdentityModel.Selectors.X509CertificateValidator>로부터 파생된 CustomX509CertificateValidator를 구현합니다. 자세한 내용은 <xref:System.IdentityModel.Selectors.X509CertificateValidator>에 대한 설명서를 참조하십시오. 이 특정 사용자 지정 유효성 검사기 샘플에서는 다음 코드에 표시된 것과 같이 자체 발급된 모든 X.509 인증서를 승인하는 Validate 메서드를 구현합니다.

```csharp
public class CustomX509CertificateValidator : X509CertificateValidator
{
  public override void Validate ( X509Certificate2 certificate )
  {
   // Only accept self-issued certificates
   if (certificate.Subject != certificate.Issuer)
     throw new Exception("Certificate is not self-issued");
   }
}
```

 서비스 코드에 유효성 검사기를 구현하고 나면 사용할 유효성 검사기 인스턴스에 대한 정보를 서비스 호스트에 알려야 합니다. 이것은 다음 코드를 사용하여 실행됩니다.

```csharp
serviceHost.Credentials.ClientCertificate.Authentication.CertificateValidationMode = X509CertificateValidationMode.Custom;
serviceHost.Credentials.ClientCertificate.Authentication.CustomCertificateValidator = new CustomX509CertificateValidator();
```

 또는 다음과 같이 구성에서도 같은 작업을 수행할 수 있습니다.

```xml
<behaviors>
    <serviceBehaviors>
     <behavior name="CalculatorServiceBehavior">
       ...
   <serviceCredentials>
    <!--The serviceCredentials behavior allows one to specify -->
    <!--authentication constraints on client certificates.-->
    <clientCertificate>
    <!-- Setting the certificateValidationMode to Custom means -->
    <!--that if the custom X509CertificateValidator does NOT -->
    <!--throw an exception, then the provided certificate will -->
    <!--be trusted without performing any validation beyond that -->
    <!--performed by the custom validator. The security -->
    <!--implications of this setting should be carefully -->
    <!--considered before using Custom in production code. -->
    <authentication certificateValidationMode="Custom"
       customCertificateValidatorType =
"Microsoft.ServiceModel.Samples. CustomX509CertificateValidator, service" />
   </clientCertificate>
   ...
  </behavior>
 </serviceBehaviors>
</behaviors>
```

샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 클라이언트에서 모든 메서드를 성공적으로 호출할 수 있어야 합니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.

## <a name="setup-batch-file"></a>설치 배치 파일

이 샘플에 포함된 Setup.bat 배치 파일을 사용하면 서버 인증서 기반 보안이 필요한 자체 호스팅 애플리케이션을 실행하도록 관련 인증서가 있는 서버를 구성할 수 있습니다. 다중 컴퓨터 구성이나 호스트되지 않는 환경에서 이 배치 파일을 사용하려면 배치 파일을 수정해야 합니다.

다음 부분에는 적절한 구성으로 실행되게 수정할 수 있도록 배치 파일의 다양한 섹션에 대한 간략한 개요가 소개되어 있습니다.

- 서버 인증서 만들기

     Setup.bat 배치 파일에서 다음 행은 사용할 서버 인증서를 만듭니다. %SERVER_NAME% 변수는 서버 이름을 지정합니다. 이 변수를 변경하여 고유의 서버 이름을 지정합니다. 기본값은 localhost입니다.

    ```bash
    echo ************
    echo Server cert setup starting
    echo %SERVER_NAME%
    echo ************
    echo making server cert
    echo ************
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe
    ```

- 클라이언트의 신뢰할 수 있는 인증서 저장소에 서버 인증서 설치:

     Setup.bat 배치 파일에서 다음 행은 클라이언트의 신뢰할 수 있는 사용자 저장소로 서버 인증서를 복사합니다. 이 단계는 Makecert.exe에서 생성한 인증서를 클라이언트 시스템에서 암시적으로 신뢰하지는 않기 때문에 필요합니다. Microsoft에서 발급한 인증서와 같이 클라이언트가 신뢰할 수 있는 루트 인증서를 기반으로 하는 인증서가 이미 있는 경우 클라이언트 인증서 저장소를 서버 인증서로 채우는 이 단계를 수행할 필요가 없습니다.

    ```bash
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople
    ```

- 클라이언트 인증서 만들기:

     Setup.bat 배치 파일에서 다음 줄은 사용할 클라이언트 인증서를 만듭니다. %USER_NAME% 변수는 클라이언트 이름을 지정합니다. 이 값은 클라이언트 코드에서 찾는 이름이기 때문에 "test1"으로 설정됩니다. %USER_NAME% 값을 변경한 경우에는 Client.cs 소스 파일에서 해당 값을 변경하고 클라이언트를 다시 빌드해야 합니다.

     인증서는 CurrentUser 저장소 위치에 있는 My (Personal) 저장소에 저장됩니다.

    ```bash
    echo ************
    echo Client cert setup starting
    echo %USER_NAME%
    echo ************
    echo making client cert
    echo ************
    makecert.exe -sr CurrentUser -ss MY -a sha1 -n CN=%USER_NAME% -sky exchange -pe
    ```

- 서버의 신뢰할 수 있는 인증서 저장소에 클라이언트 인증서 설치:

     Setup.bat 배치 파일에서 다음 줄은 신뢰할 수 있는 사용자 저장소로 클라이언트 인증서를 복사합니다. 이 단계는 Makecert.exe에서 생성한 인증서를 서버 시스템에서 암시적으로 신뢰하지는 않기 때문에 필요합니다. Microsoft에서 발급한 인증서와 같이 신뢰할 수 있는 루트 인증서를 기반으로 하는 인증서가 이미 있는 경우 서버 인증서 저장소를 클라이언트 인증서로 채우는 이 단계는 필요하지 않습니다.

    ```bash
    certmgr.exe -add -r CurrentUser -s My -c -n %USER_NAME% -r LocalMachine -s TrustedPeople
    ```

#### <a name="to-set-up-and-build-the-sample"></a>샘플을 설치하고 빌드하려면

1. 지침에 따라 솔루션을 빌드하려면 [Building Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)합니다.

2. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행하려면 다음 지침을 사용합니다.

#### <a name="to-run-the-sample-on-the-same-computer"></a>단일 컴퓨터 구성에서 샘플을 실행하려면

1. 관리자 권한으로 연 Visual Studio 2012 명령 프롬프트에서 샘플 설치 폴더에서 Setup.bat를 실행 합니다. 이 작업은 샘플 실행에 필요한 모든 인증서를 설치합니다.

    > [!IMPORTANT]
    > Setup.bat 배치 파일은 Visual Studio 2012 명령 프롬프트에서 실행 되도록 설계 되었습니다. 경로 환경 변수 집합을 Visual Studio 2012 명령 프롬프트 내에서 Setup.bat 스크립트에 필요한 실행 파일이 포함 된 디렉터리를 가리킵니다.

2. service\bin에서 Service.exe를 실행합니다.

3. \client\bin에서 Client.exe를 실행합니다. 클라이언트 콘솔 애플리케이션에 클라이언트 동작이 표시됩니다.

4. 클라이언트와 서비스가 통신할 수 없는 경우 참조 [WCF 샘플에 대 한 문제 해결 팁](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))합니다.

#### <a name="to-run-the-sample-across-computers"></a>다중 컴퓨터 구성에서 샘플을 실행하려면

1. 서비스 컴퓨터에 디렉터리를 만듭니다.

2. \service\bin에서 서비스 컴퓨터의 가상 디렉터리로 서비스 프로그램 파일을 복사합니다. Setup.bat, Cleanup.bat, GetComputerName.vbs 및 ImportClientCert.bat 파일도 서비스 컴퓨터에 복사합니다.

3. 클라이언트 컴퓨터에 클라이언트 이진 파일용 디렉터리를 만듭니다.

4. 클라이언트 프로그램 파일을 클라이언트 컴퓨터의 클라이언트 디렉터리로 복사합니다. Setup.bat, Cleanup.bat 및 ImportServiceCert.bat 파일도 클라이언트로 복사합니다.

5. 서버에서 실행 `setup.bat service` 관리자 권한으로 연 Visual Studio 용 개발자 명령 프롬프트에서. 실행 중인 `setup.bat` 사용 하 여는 `service` 인수가 컴퓨터의 정규화 된 도메인 이름 서비스 인증서를 만들고 Service.cer 이라는 파일로 서비스 인증서를 내보냅니다.

6. 새 인증서 이름을 반영 되도록 Service.exe.config를 편집 (에서 `findValue` 특성을 [ \<serviceCertificate >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)) 컴퓨터의 정규화 된 도메인 이름으로 같습니다. 컴퓨터 이름을 변경할 수도 합니다 \<서비스 > /\<baseAddresses > localhost에서 서비스 컴퓨터의 정규화 된 이름으로 요소입니다.

7. 서비스 디렉터리에서 클라이언트 컴퓨터의 클라이언트 디렉터리로 Service.cer 파일을 복사합니다.

8. 클라이언트에서 실행 `setup.bat client` 관리자 권한으로 연 Visual Studio 용 개발자 명령 프롬프트에서. `setup.bat` 인수를 사용하여 `client`를 실행하면 client.com이라는 클라이언트 인증서가 생성되어 Client.cer이라는 파일로 내보내집니다.

9. 클라이언트 컴퓨터의 Client.exe.config 파일에서 엔드포인트의 주소 값을 서비스의 새 주소와 일치하도록 변경합니다. 이렇게 하려면 localhost를 서버의 정규화된 도메인 이름으로 바꿉니다.

10. 클라이언트 디렉터리에서 서버의 서비스 디렉터리로 Client.cer 파일을 복사합니다.

11. 클라이언트에서 ImportServiceCert.bat를 관리자 권한으로 연 Visual Studio 용 개발자 명령 프롬프트에서 실행 합니다. 이 작업은 Service.cer 파일의 서비스 인증서를 CurrentUser - TrustedPeople 저장소로 가져옵니다.

12. 서버에서 열고 ImportClientCert.bat를 관리자 권한으로 연 Visual Studio 용 개발자 명령 프롬프트에서를 실행 합니다. 이 작업은 Client.cer 파일의 클라이언트 인증서를 LocalMachine - TrustedPeople 저장소로 가져옵니다.

13. 서버 컴퓨터의 명령 프롬프트 창에서 Service.exe를 실행합니다.

14. 클라이언트 컴퓨터의 명령 프롬프트 창에서 Client.exe를 실행합니다. 클라이언트와 서비스가 통신할 수 없는 경우 참조 [WCF 샘플에 대 한 문제 해결 팁](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))합니다.

#### <a name="to-clean-up-after-the-sample"></a>샘플 실행 후 정리를 수행하려면

1. 샘플 실행을 완료했으면 샘플 폴더에서 Cleanup.bat를 실행합니다. 그러면 인증서 저장소에서 서버 및 클라이언트 인증서가 제거됩니다.

> [!NOTE]
> 다중 컴퓨터 구성에서 이 샘플을 실행할 경우에는 이 스크립트로 클라이언트의 서비스 인증서를 제거할 수 없습니다. 컴퓨터 인증서를 사용 하는 Windows Communication Foundation (WCF) 샘플을 실행 하는 경우에 CurrentUser-TrustedPeople 저장소에에서 설치 된 서비스 인증서를 선택 취소 해야 합니다. 이 작업을 수행 하려면 다음 명령을 사용 합니다. `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` 예를 들어: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`합니다.
