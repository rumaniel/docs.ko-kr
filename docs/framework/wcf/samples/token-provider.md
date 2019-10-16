---
title: Token Provider
ms.date: 03/30/2017
ms.assetid: 947986cf-9946-4987-84e5-a14678d96edb
ms.openlocfilehash: 9f008204c6ff8d3d134dbb17fc445b460f757f13
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70038746"
---
# <a name="token-provider"></a>Token Provider
이 샘플에서는 사용자 지정 토큰 공급자를 구현하는 방법을 보여 줍니다. WCF (Windows Communication Foundation)의 토큰 공급자는 보안 인프라에 자격 증명을 제공 하는 데 사용 됩니다. 일반적으로 토큰 공급자는 대상을 검사하고 적절한 자격 증명을 발급하여 보안 인프라에서 메시지의 보안을 유지할 수 있도록 합니다. WCF는 기본 자격 증명 관리자 토큰 공급자와 함께 제공 됩니다. WCF는 또한 CardSpace 토큰 공급자와 함께 제공 됩니다. 사용자 지정 토큰 공급자는 다음과 같은 경우에 유용합니다.

- 이러한 토큰 공급자가 작동되지 않는 자격 증명 저장소가 있는 경우

- WCF 클라이언트 프레임 워크에서 자격 증명을 사용 하는 경우 사용자가 세부 정보를 제공 하는 시점에서 자격 증명을 변환 하는 사용자 지정 메커니즘을 제공 하려는 경우

- 사용자 지정 토큰을 빌드하고 있는 경우

 이 샘플에서는 사용자의 입력을 다른 형식을 변형하는 사용자 지정 토큰 공급자를 빌드하는 방법을 보여 줍니다.

 즉, 이 샘플에서는 다음 방법을 보여 줍니다.

- 클라이언트에서 사용자 이름/암호 쌍을 사용하여 인증하는 방법.

- 사용자 지정 토큰 공급자로 클라이언트를 구성하는 방법

- 사용자 이름과 암호가 일치하는지 확인하는 사용자 지정 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator>와 함께 암호를 사용하여 서버에서 클라이언트 자격 증명의 유효성을 검사하는 방법

- 서버의 X.509 인증서를 사용하여 클라이언트에서 서버를 인증하는 방법

 또한 이 샘플에서는 사용자 지정 토큰 인증 프로세스 후에 호출자의 ID에 액세스할 수 있는 방법을 보여 줍니다.

 서비스에서는 서비스와의 통신에 사용할 수 있는 단일 엔드포인트를 노출하며, 이 엔드포인트는 App.config 구성 파일을 사용하여 정의합니다. 엔드포인트는 하나의 주소, 바인딩 및 계약으로 구성됩니다. 바인딩은 기본적으로 메시지 보안이 사용되는 표준 `wsHttpBinding`으로 구성됩니다. 이 샘플에서는 클라이언트 사용자 이름 인증을 사용하도록 표준 `wsHttpBinding`를 설정합니다. 또한 서비스에서는 serviceCredentials 동작을 사용하여 서비스 인증서를 구성합니다. serviceCredentials 동작을 사용하면 서비스 인증서를 구성할 수 있습니다. 서비스 인증서는 클라이언트에서 서비스를 인증하고 메시지 보호를 제공하는 데 사용됩니다. 다음 구성에서는 뒤에 나오는 설치 지침에 설명된 대로 샘플 설치 중에 설치되는 localhost 인증서를 참조합니다.

```xml
<system.serviceModel>
    <services>
      <service
          name="Microsoft.ServiceModel.Samples.CalculatorService"
          behaviorConfiguration="CalculatorServiceBehavior">
        <host>
          <baseAddresses>
            <!-- configure base address provided by host -->
            <add baseAddress ="http://localhost:8000/servicemodelsamples/service"/>
          </baseAddresses>
        </host>
        <!-- use base address provided by host -->
        <endpoint address=""
                  binding="wsHttpBinding"
                  bindingConfiguration="Binding1"
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />
      </service>
    </services>

    <bindings>
      <wsHttpBinding>
        <binding name="Binding1">
          <security mode="Message">
            <message clientCredentialType="UserName" />
          </security>
        </binding>
      </wsHttpBinding>
    </bindings>

    <behaviors>
      <serviceBehaviors>
        <behavior name="CalculatorServiceBehavior">
          <serviceDebug includeExceptionDetailInFaults="False" />
          <!--
        The serviceCredentials behavior allows one to define a service certificate.
        A service certificate is used by a client to authenticate the service and provide message protection.
        This configuration references the "localhost" certificate installed during the setup instructions.
        -->
          <serviceCredentials>
            <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />
          </serviceCredentials>
        </behavior>
      </serviceBehaviors>
    </behaviors>
  </system.serviceModel>
```

 클라이언트 엔드포인트 구성은 구성 이름, 서비스 엔드포인트의 절대 주소, 바인딩 및 계약으로 구성됩니다. 클라이언트 바인딩에는 적절한 `Mode` 및 메시지 `clientCredentialType`이 구성됩니다.

```xml
<system.serviceModel>
  <client>
    <endpoint name=""
              address="http://localhost:8000/servicemodelsamples/service"
              binding="wsHttpBinding"
              bindingConfiguration="Binding1"
              contract="Microsoft.ServiceModel.Samples.ICalculator">
    </endpoint>
  </client>

  <bindings>
    <wsHttpBinding>
      <binding name="Binding1">
        <security mode="Message">
          <message clientCredentialType="UserName" />
        </security>
      </binding>
    </wsHttpBinding>
  </bindings>
</system.serviceModel>
```

 다음 단계에서는 사용자 지정 토큰 공급자를 개발 하 고 WCF 보안 프레임 워크와 통합 하는 방법을 보여 줍니다.

1. 사용자 지정 토큰 공급자를 작성합니다.

     사용자 이름과 암호를 가져오는 사용자 지정 토큰 공급자가 샘플에서 구현됩니다. 암호는 이 사용자 이름과 일치해야 합니다. 이 사용자 지정 토큰 공급자는 데모용으로만 제공된 것이므로 실제 배포에서는 사용하지 않는 것이 좋습니다.

     이 작업을 수행하려면 사용자 지정 토큰 공급자가 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 클래스를 파생하고 <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%28System.TimeSpan%29> 메서드를 재정의해야 합니다. 이 메서드는 새 `UserNameSecurityToken`을 만들고 반환합니다.

    ```csharp
    protected override SecurityToken GetTokenCore(TimeSpan timeout)
    {
        // obtain username and password from the user using console window
        string username = GetUserName();
        string password = GetPassword();
        Console.WriteLine("username: {0}", username);

        // return new UserNameSecurityToken containing information obtained from user
        return new UserNameSecurityToken(username, password);
    }
    ```

2. 사용자 지정 보안 토큰 관리자를 씁니다.

     <xref:System.IdentityModel.Selectors.SecurityTokenManager>는 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 메서드에서 전달되는 특정 <xref:System.IdentityModel.Selectors.SecurityTokenRequirement>에 대한 `CreateSecurityTokenProvider`를 만드는 데 사용됩니다. 또한 보안 토큰 관리자는 토큰 인증자와 토큰 serializer를 만드는 데 사용되지만 이 샘플에서는 설명하지 않습니다. 이 샘플에서 사용자 지정 보안 토큰 관리자는 <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> 클래스에서 상속되며 `CreateSecurityTokenProvider` 메서드를 재정의하여 전달된 토큰 요구 사항에서 사용자 이름 공급자가 요청됨을 나타낼 때 사용자 지정 사용자 이름 토큰 공급자를 반환합니다.

    ```csharp
    public class MyUserNameSecurityTokenManager : ClientCredentialsSecurityTokenManager
    {
        MyUserNameClientCredentials myUserNameClientCredentials;

        public MyUserNameSecurityTokenManager(MyUserNameClientCredentials myUserNameClientCredentials)
            : base(myUserNameClientCredentials)
        {
            this.myUserNameClientCredentials = myUserNameClientCredentials;
        }

        public override SecurityTokenProvider CreateSecurityTokenProvider(SecurityTokenRequirement tokenRequirement)
        {
            // if token requirement matches username token return custom username token provider
            // otherwise use base implementation
            if (tokenRequirement.TokenType == SecurityTokenTypes.UserName)
            {
                return new MyUserNameTokenProvider();
            }
            else
            {
                return base.CreateSecurityTokenProvider(tokenRequirement);
            }
        }
    }
    ```

3. 사용자 지정 클라이언트 자격 증명을 씁니다.

     클라이언트 자격 증명 클래스는 클라이언트 프록시에 대해 구성된 자격 증명을 나타내는 데 사용되며 토큰 인증자, 토큰 공급자 및 토큰 serializer를 가져오는 데 사용되는 보안 토큰 관리자를 만듭니다.

    ```csharp
    public class MyUserNameClientCredentials : ClientCredentials
    {
        public MyUserNameClientCredentials()
            : base()
        {
        }

        protected override ClientCredentials CloneCore()
        {
            return new MyUserNameClientCredentials();
        }

        public override SecurityTokenManager CreateSecurityTokenManager()
        {
            // return custom security token manager
            return new MyUserNameSecurityTokenManager(this);
        }
    }
    ```

4. 사용자 지정 클라이언트 자격 증명을 사용하도록 클라이언트를 구성합니다.

     클라이언트가 사용자 지정 클라이언트 자격 증명을 이용할 수 있도록 이 샘플에서는 기본 클라이언트 자격 증명 클래스를 삭제하고 새 클라이언트 자격 증명 클래스를 제공합니다.

    ```csharp
    static void Main()
    {
        // ...
           // Create a client with given client endpoint configuration
          CalculatorClient client = new CalculatorClient();

          // set new credentials
           client.ChannelFactory.Endpoint.Behaviors.Remove(typeof(ClientCredentials));
         client.ChannelFactory.Endpoint.Behaviors.Add(new MyUserNameClientCredentials());
       // ...
    }
    ```

 서비스에서 호출자의 정보를 표시하려면 다음 코드 예제와 같이 <xref:System.ServiceModel.ServiceSecurityContext.PrimaryIdentity%2A>를 사용합니다. <xref:System.ServiceModel.ServiceSecurityContext.Current%2A>에는 현재 호출자에 대한 클레임 정보가 포함됩니다.

```csharp
static void DisplayIdentityInformation()
{
    Console.WriteLine("\t\tSecurity context identity  :  {0}",
        ServiceSecurityContext.Current.PrimaryIdentity.Name);
}
```

 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.

## <a name="setup-batch-file"></a>설치 배치 파일
 이 샘플에 포함된 Setup.bat 배치 파일을 사용하면 관련 인증서로 서버를 구성하여 서버 인증서 기반 보안이 필요한 자체 호스팅 응용 프로그램을 실행할 수 있습니다. 다중 컴퓨터 구성이나 호스트되지 않는 환경에서 이 배치 파일을 사용하려면 배치 파일을 수정해야 합니다.

 다음 부분에는 적절한 구성으로 실행되게 수정할 수 있도록 배치 파일의 다양한 섹션에 대한 간략한 개요가 소개되어 있습니다.

- 서버 인증서 만들기

     Setup.bat 배치 파일에서 다음 행은 사용할 서버 인증서를 만듭니다. `%SERVER_NAME%`변수는 서버 이름을 지정합니다. 이 변수를 변경하여 고유의 서버 이름을 지정합니다. 이 배치 파일의 기본값은 localhost입니다.

    ```
    echo ************
    echo Server cert setup starting
    echo %SERVER_NAME%
    echo ************
    echo making server cert
    echo ************
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe
    ```

- 클라이언트의 신뢰할 수 있는 인증서 저장소에 서버 인증서 설치:

     Setup.bat 배치 파일에서 다음 행은 클라이언트의 신뢰할 수 있는 사용자 저장소로 서버 인증서를 복사합니다. 이 단계는 Makecert.exe에서 생성한 인증서를 클라이언트 컴퓨터에서 절대적으로 신뢰하지는 않기 때문에 필요합니다. Microsoft에서 발급한 인증서와 같이 클라이언트가 신뢰할 수 있는 루트 인증서를 기반으로 하는 인증서가 이미 있는 경우 클라이언트 인증서 저장소를 서버 인증서로 채우는 이 단계를 수행할 필요가 없습니다.

    ```
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople
    ```

> [!NOTE]
> Setup.bat 배치 파일은 Windows SDK 명령 프롬프트에서 실행되도록 디자인되었습니다. MSSDK 환경 변수는 SDK가 설치되는 디렉터리를 가리켜야 합니다. 이 환경 변수는 Windows SDK 명령 프롬프트 내에서 자동으로 설정됩니다.

#### <a name="to-set-up-and-build-the-sample"></a>샘플을 설치하고 빌드하려면

1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.

2. 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따르세요.

#### <a name="to-run-the-sample-on-the-same-computer"></a>단일 컴퓨터 구성에서 샘플을 실행하려면

1. 관리자 권한으로 연 Visual Studio 2012 명령 프롬프트 내의 샘플 설치 폴더에서 Setup.exe를 실행 합니다. 이 작업은 샘플 실행에 필요한 모든 인증서를 설치합니다.

    > [!NOTE]
    > 설치 .bat 배치 파일은 Visual Studio 2012 명령 프롬프트에서 실행 되도록 디자인 되었습니다. Visual Studio 2012 명령 프롬프트 내에서 설정 된 PATH 환경 변수는 Setup. .bat 스크립트에 필요한 실행 파일을 포함 하는 디렉터리를 가리킵니다.  
  
2. service\bin에서 service.exe를 실행합니다.  
  
3. \client\bin에서 Client.exe를 실행합니다. 클라이언트 콘솔 애플리케이션에 클라이언트 동작이 표시됩니다.  
  
4. 사용자 이름 프롬프트에서 사용자 이름을 입력합니다.  
  
5. 암호 프롬프트에서 사용자 이름 프롬프트에 입력한 것과 동일한 문자열을 사용합니다.  
  
6. 클라이언트와 서비스가 통신할 수 없는 경우 [WCF 샘플에 대 한 문제 해결 팁](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))을 참조 하세요.  
  
#### <a name="to-run-the-sample-across-computers"></a>다중 컴퓨터 구성에서 샘플을 실행하려면  
  
1. 서비스 컴퓨터에 서비스 이진 파일용 디렉터리를 만듭니다.  
  
2. 서비스 프로그램 파일을 서비스 컴퓨터의 서비스 디렉터리에 복사합니다. Setup.bat 및 Cleanup.bat 파일도 서비스 컴퓨터로 복사합니다.  
  
3. 컴퓨터의 정규화된 도메인 이름을 포함하는 주체 이름을 가진 서버 인증서가 있어야 합니다. 이 새로운 인증서 이름을 반영하도록 Service.exe.config 파일을 업데이트해야 합니다. Setup.bat 배치 파일을 수정하여 서버 인증서를 만들 수 있습니다. Setup.exe 파일은 관리자 권한으로 연 Visual Studio 용 개발자 명령 프롬프트에서 실행 해야 합니다. 서비스를 호스팅하는 데 사용되는 컴퓨터의 정규화된 호스트 이름으로 `%SERVER_NAME%` 변수를 설정해야 합니다.  
  
4. 서버 인증서를 클라이언트의 CurrentUser-TrustedPeople 저장소에 복사합니다. 서버 인증서가 클라이언트의 신뢰할 수 있는 발급자에 의해 발급된 경우 이 작업을 수행할 필요가 없습니다.  
  
5. 서비스 컴퓨터의 Service.exe.config 파일에서 기본 주소 값을 변경하여 localhost 대신 정규화된 컴퓨터 이름을 지정합니다.  
  
6. 서비스 컴퓨터의 명령 프롬프트에서 service.exe를 실행합니다.  
  
7. 언어별 폴더의 \client\bin\ 폴더에서 클라이언트 프로그램 파일을 클라이언트 컴퓨터로 복사합니다.  
  
8. 클라이언트 컴퓨터의 Client.exe.config 파일에서 끝점의 주소 값을 서비스의 새 주소와 일치하도록 변경합니다.  
  
9. 클라이언트 컴퓨터의 명령 프롬프트 창에서 `Client.exe`를 실행합니다.  
  
10. 클라이언트와 서비스가 통신할 수 없는 경우 [WCF 샘플에 대 한 문제 해결 팁](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))을 참조 하세요.  
  
#### <a name="to-clean-up-after-the-sample"></a>샘플 실행 후 정리를 수행하려면  
  
1. 샘플 실행을 완료했으면 샘플 폴더에서 Cleanup.bat를 실행합니다.  
