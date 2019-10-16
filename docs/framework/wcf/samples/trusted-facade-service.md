---
title: 신뢰된 외관 서비스
ms.date: 03/30/2017
ms.assetid: c34d1a8f-e45e-440b-a201-d143abdbac38
ms.openlocfilehash: ea2aa3840c48ba24bafeee3f10d0cb903b25dcac
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045428"
---
# <a name="trusted-facade-service"></a>신뢰된 외관 서비스
이 시나리오 샘플에서는 WCF (Windows Communication Foundation) 보안 인프라를 사용 하 여 한 서비스에서 다른 서비스로 호출자의 id 정보를 전달 하는 방법을 보여 줍니다.  
  
 서비스에 의해 제공되는 기능을 외관 서비스를 사용하여 공용 네트워크에 노출하는 것은 일반적인 디자인 패턴입니다. 일반적으로 외관 서비스는 DMZ, 완충 지역 및 스크린된 서브넷이라고도 하는 경계 네트워크에 상주하며 비즈니스 논리를 구현하고 내부 데이터에 액세스할 수 있는 백 엔드 서비스와 통신합니다. 외관 서비스와 백 엔드 서비스 간의 통신 채널은 방화벽을 통과하며 일반적으로 단일 용도로만 제한됩니다.  
  
 이 샘플은 다음 구성 요소로 구성되어 있습니다.  
  
- 계산기 클라이언트  
  
- 계산기 외관 서비스  
  
- 계산기 백 엔드 서비스  
  
 외관 서비스는 요청의 유효성을 검사하고 호출자를 인증합니다. 인증과 유효성 검사에 성공하고 나면 주변 네트워크에서 내부 네트워크로의 제어된 통신 채널을 사용하여 백 엔드 서비스에 요청을 전달합니다. 외관 서비스는 호출자의 ID에 대한 정보를 전달된 요청의 일부로 포함하므로 백 엔드 서비스는 이 정보를 해당 처리에서 사용할 수 있습니다. 호출자의 ID는 메시지 `Username` 헤더 내의 `Security` 보안 토큰을 사용하여 전송됩니다. 이 샘플에서는 WCF 보안 인프라를 사용 하 여 `Security` 헤더에서이 정보를 전송 및 추출 합니다.  
  
> [!IMPORTANT]
> 백 엔드 서비스는 호출자를 인증하기 위해 외관 서비스를 신뢰합니다. 따라서 백 엔드 서비스는 호출자를 다시 인증하지 않으며 전달된 요청에서 외관 서비스에 의해 제공된 ID 정보를 사용합니다. 이 신뢰 관계 때문에 백 엔드 서비스는 전달된 메시지가 신뢰할 수 있는 소스(이 경우에는 외관 서비스)에서 제공되는지 확인하기 위해 외관 서비스를 인증해야 합니다.  
  
## <a name="implementation"></a>구현  
 이 샘플에는 두 개의 통신 경로가 있습니다. 첫 번째는 클라이언트와 외관 서비스 간의 경로이고 두 번째는 외관 서비스와 백 엔드 서비스 간의 경로입니다.  
  
### <a name="communication-path-between-client-and-faade-service"></a>클라이언트와 외관 서비스 간의 통신 경로  
 클라이언트에서 외관 서비스로의 통신 경로에는 `wsHttpBinding` 클라이언트 자격 증명 유형을 가진 `UserName` 이 사용됩니다. 이는 클라이언트가 외관 서비스에 대해 인증하기 위해 사용자 이름과 암호를 사용하고 외관 서비스가 클라이언트에 대해 인증하기 위해 X.509 인증서를 사용한다는 것을 의미합니다. 바인딩 구성은 다음 예제와 같습니다.  
  
```xml  
<bindings>  
  <wsHttpBinding>  
    <binding name="Binding1">  
      <security mode="Message">  
        <message clientCredentialType="UserName"/>  
      </security>  
    </binding>  
  </wsHttpBinding>  
</bindings>  
```  
  
 외관 서비스는 사용자 지정 `UserNamePasswordValidator` 구현을 사용하여 호출자를 인증합니다. 여기서는 데모용이기 때문에 인증은 호출자의 사용자 이름이 제공된 암호와 일치하는지만 확인합니다. 실제 상황에서는 Active Directory 또는 사용자 지정 ASP.NET 멤버 자격 공급자를 사용하여 사용자가 인증될 것입니다. 유효성 검사기 구현은 `FacadeService.cs` 파일에 있습니다.  
  
```  
public class MyUserNamePasswordValidator : UserNamePasswordValidator  
{  
    public override void Validate(string userName, string password)  
    {  
        // check that username matches password  
        if (null == userName || userName != password)  
        {  
            Console.WriteLine("Invalid username or password");  
            throw new SecurityTokenValidationException(  
                       "Invalid username or password");  
        }  
    }  
}  
```  
  
 사용자 지정 유효성 검사기는 외관 서비스 구성 파일에서 `serviceCredentials` 동작 안에 사용하도록 구성됩니다. 이 동작은 또한 서비스의 X.509 인증서를 구성하는 데 사용됩니다.  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="FacadeServiceBehavior">  
      <!--The serviceCredentials behavior allows you to define -->  
      <!--a service certificate. -->  
      <!--A service certificate is used by the service to  -->  
      <!--authenticate itself to its clients and to provide  -->  
      <!--message protection. -->  
      <!--This configuration references the "localhost"  -->  
      <!--certificate installed during the setup instructions. -->  
      <serviceCredentials>  
        <serviceCertificate   
               findValue="localhost"   
               storeLocation="LocalMachine"   
               storeName="My"   
               x509FindType="FindBySubjectName" />  
        <userNameAuthentication userNamePasswordValidationMode="Custom"  
            customUserNamePasswordValidatorType=  
           "Microsoft.ServiceModel.Samples.MyUserNamePasswordValidator,  
            FacadeService"/>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
### <a name="communication-path-between-faade-service-and-backend-service"></a>외관 서비스와 백 엔드 서비스 간의 통신 경로  
 외관 서비스에서 백 엔드 서비스로의 통신 경로는 여러 바인딩 요소로 구성된 `customBinding` 을 사용합니다. 이 바인딩은 두 가지 작업을 수행합니다. 이 바인딩은 통신이 보안되었는지, 그리고 신뢰할 수 있는 소스에서 제공되는지 확인하기 위해 외관 서비스와 백 엔드 서비스를 인증합니다. 또한 `Username` 보안 토큰 내에서 초기 호출자의 ID를 전송합니다. 이 경우 초기 호출자의 사용자 이름만 백 엔드 서비스에 전송되고 암호는 메시지에 포함되지 않습니다. 이는 백 엔드 서비스가 요청을 전달하기 전에 호출자를 인증하기 위해 외관 서비스를 신뢰하기 때문입니다. 외관 서비스가 백 엔드 서비스에 대해 자체 인증하므로 백 엔드 서비스는 전달된 요청에 포함된 정보를 신뢰할 수 있습니다.  
  
 이 통신 경로에 대한 바인딩 구성은 다음과 같습니다.  
  
```xml  
<bindings>  
  <customBinding>  
    <binding name="ClientBinding">  
      <security authenticationMode="UserNameOverTransport"/>  
      <windowsStreamSecurity/>  
      <tcpTransport/>  
    </binding>  
  </customBinding>  
</bindings>  
```  
  
 [ \<보안 >](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) 바인딩 요소는 초기 호출자의 사용자 이름 전송 및 추출을 처리 합니다. [ \<Windowsstreamsecurity >](../../../../docs/framework/configure-apps/file-schema/wcf/windowsstreamsecurity.md) 및 [ \<tcptransport >](../../../../docs/framework/configure-apps/file-schema/wcf/tcptransport.md) 는 외관 및 백 엔드 서비스와 메시지 보호를 인증 하는 데 사용 됩니다.  
  
 요청을 전달 하기 위해 외관 서비스 구현은 초기 호출자의 사용자 이름을 제공 해야 하므로 WCF 보안 인프라가이를 전달 된 메시지에 저장할 수 있습니다. 외관 서비스가 백 엔드 서비스와 통신하기 위해 사용하는 클라이언트 프록시 인스턴스의 `ClientCredentials` 속성에서 초기 호출자의 사용자 이름을 설정함으로써 외관 서비스 구현에서 해당 사용자 이름이 제공됩니다.  
  
 다음 코드에서는 `GetCallerIdentity` 메서드가 외관 서비스에서 구현되는 방법을 보여 줍니다. 다른 메서드에도 동일한 패턴이 사용됩니다.  
  
```  
public string GetCallerIdentity()  
{  
    CalculatorClient client = new CalculatorClient();  
    client.ClientCredentials.UserName.UserName = ServiceSecurityContext.Current.PrimaryIdentity.Name;  
    string result = client.GetCallerIdentity();  
    client.Close();  
    return result;  
}  
```  
  
 위 코드에서 볼 수 있듯이 `ClientCredentials` 속성에서는 암호가 설정되지 않고 사용자 이름만 설정됩니다. 이 경우 WCF 보안 인프라는 암호 없이 사용자 이름 보안 토큰을 만듭니다 .이 경우에는이 시나리오에 필요한 것과 같습니다.  
  
 백 엔드 서비스에서는 사용자 이름 보안 토큰에 포함된 정보가 인증되어야 합니다. 기본적으로 WCF 보안은 제공 된 암호를 사용 하 여 Windows 계정에 사용자를 매핑하려고 시도 합니다. 이 경우에는 제공된 암호가 없으며 외관 서비스에 의해 인증이 이미 수행되었으므로 백 엔드 서비스는 사용자 이름을 인증할 필요가 없습니다. WCF에서이 기능을 구현 하기 위해 토큰 `UserNamePasswordValidator` 에 사용자 이름을 지정 하 고 추가 인증을 수행 하지 않는 사용자 지정가 제공 됩니다.  
  
```  
public class MyUserNamePasswordValidator : UserNamePasswordValidator  
{  
    public override void Validate(string userName, string password)  
    {  
        // Ignore the password because it is empty,   
        // we trust the facade service to authenticate the client.  
        // Accept the username information here so that the   
        // application gets access to it.  
        if (null == userName)  
        {  
            Console.WriteLine("Invalid username");  
            throw new   
             SecurityTokenValidationException("Invalid username");  
        }  
    }  
}  
```  
  
 사용자 지정 유효성 검사기는 외관 서비스 구성 파일에서 `serviceCredentials` 동작 안에 사용하도록 구성됩니다.  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="BackendServiceBehavior">  
      <serviceCredentials>  
        <userNameAuthentication userNamePasswordValidationMode="Custom"  
           customUserNamePasswordValidatorType=  
          "Microsoft.ServiceModel.Samples.MyUserNamePasswordValidator,   
           BackendService"/>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 신뢰할 수 있는 외관 서비스 계정에 대한 사용자 이름과 정보를 추출하기 위해 백 엔드 서비스 구현에서는 `ServiceSecurityContext` 클래스를 사용합니다. 다음 코드에서는 `GetCallerIdentity` 메서드를 구현하는 방법을 보여 줍니다.  
  
```  
public string GetCallerIdentity()  
{  
    // Facade service is authenticated using Windows authentication.  
    //Its identity is accessible.  
    // On ServiceSecurityContext.Current.WindowsIdentity.  
    string facadeServiceIdentityName =   
          ServiceSecurityContext.Current.WindowsIdentity.Name;  
  
    // The client name is transmitted using Username authentication on   
    //the message level without the password  
    // using a supporting encrypted UserNameToken.  
    // Claims extracted from this supporting token are available in   
    // ServiceSecurityContext.Current.AuthorizationContext.ClaimSets   
    // collection.  
    string clientName = null;  
    foreach (ClaimSet claimSet in   
        ServiceSecurityContext.Current.AuthorizationContext.ClaimSets)  
    {  
        foreach (Claim claim in claimSet)  
        {  
            if (claim.ClaimType == ClaimTypes.Name &&   
                                   claim.Right == Rights.Identity)  
            {  
                clientName = (string)claim.Resource;  
                break;  
            }  
        }  
    }  
    if (clientName == null)  
    {  
        // In case there was no UserNameToken attached to the request.  
        // In the real world implementation the service should reject   
        // this request.  
        return "Anonymous caller via " + facadeServiceIdentityName;  
    }  
  
    return clientName + " via " + facadeServiceIdentityName;  
}  
```  
  
 외관 서비스 계정 정보는 `ServiceSecurityContext.Current.WindowsIdentity` 속성을 사용하여 추출됩니다. 초기 호출자에 대한 정보에 액세스하기 위해 백 엔드 서비스는 `ServiceSecurityContext.Current.AuthorizationContext.ClaimSets` 속성을 사용합니다. 이 속성은 `Identity` 형식을 가진 `Name`클레임을 찾습니다. 이 클레임은 `Username` 보안 토큰에 포함 된 정보에서 WCF 보안 인프라에 의해 자동으로 생성 됩니다.  
  
## <a name="running-the-sample"></a>샘플 실행  
 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다. 외관 및 백 엔드 서비스 콘솔 창에서 Enter 키를 눌러 서비스를 종료할 수 있습니다.  
  
```  
Username authentication required.  
Provide a valid machine or domain ac  
   Enter username:  
user  
   Enter password:  
****  
user via MyMachine\testaccount  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
 신뢰할 수 있는 외관 시나리오 샘플에 포함된 Setup.bat 배치 파일을 사용하면 클라이언트에 자체 인증하는 데 인증서 기반 보안이 필요한 외관 서비스를 실행하기 위해 관련 인증서로 서버를 구성할 수 있습니다. 자세한 내용은 이 항목의 끝에 있는 설치 절차를 참조하세요.  
  
 다음은 배치 파일의 여러 다른 섹션에 대한 간략한 개요입니다.  
  
- 서버 인증서 만들기  
  
     Setup.bat 배치 파일에서 다음 행은 사용할 서버 인증서를 만듭니다.  
  
    ```  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
     `%SERVER_NAME%` 변수는 서버 이름을 지정합니다. 기본값은 localhost입니다. 인증서는 LocalMachine 저장소에 저장됩니다.  
  
- 클라이언트의 신뢰할 수 있는 인증서 저장소에 외관 서비스의 인증서 설치  
  
     다음 줄은 클라이언트의 신뢰할 수 있는 사용자 저장소에 외관 서비스의 인증서를 복사합니다. 이 단계는 Makecert.exe에서 생성한 인증서를 클라이언트 컴퓨터에서 절대적으로 신뢰하지는 않기 때문에 필요합니다. Microsoft에서 발급한 인증서와 같이 클라이언트가 신뢰할 수 있는 루트 인증서를 기반으로 하는 인증서가 이미 있는 경우 클라이언트 인증서 저장소를 서버 인증서로 채우는 이 단계를 수행할 필요가 없습니다.  
  
    ```  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
#### <a name="to-run-the-sample-on-the-same-machine"></a>단일 컴퓨터 구성에서 샘플을 실행하려면  
  
1. Makecert.exe가 있는 폴더가 경로에 포함되는지 확인합니다.  
  
2. 샘플 설치 폴더에서 Setup.bat를 실행하여 이 작업은 샘플 실행에 필요한 모든 인증서를 설치합니다.  
  
3. \BackendService\bin 디렉터리에서 BackendService.exe를 별도의 콘솔 창에 실행합니다.  
  
4. \FacadeService\bin 디렉터리에서 FacadeService.exe를 별도의 콘솔 창에 실행합니다.  
  
5. \client\bin에서 Client.exe를 실행합니다. 클라이언트 콘솔 애플리케이션에 클라이언트 동작이 표시됩니다.  
  
6. 클라이언트와 서비스가 통신할 수 없는 경우 [WCF 샘플에 대 한 문제 해결 팁](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))을 참조 하세요.  
  
#### <a name="to-clean-up-after-the-sample"></a>샘플 실행 후 정리를 수행하려면  
  
1. 샘플 실행을 완료했으면 샘플 폴더에서 Cleanup.bat를 실행합니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Scenario\TrustedFacade`  
