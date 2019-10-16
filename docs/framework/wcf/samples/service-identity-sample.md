---
title: Service Identity 샘플
ms.date: 03/30/2017
ms.assetid: 79fa8c1c-85bb-4b67-bc67-bfaf721303f8
ms.openlocfilehash: 0d5fce313200cdfdb8007ceffe9ff97b033d9f82
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045516"
---
# <a name="service-identity-sample"></a>Service Identity 샘플
이 Service Identity 샘플에서는 서비스의 ID를 설정하는 방법을 보여 줍니다. 클라이언트는 디자인 타임에 서비스의 메타데이터를 사용하여 ID를 검색한 다음 런타임에 서비스의 ID를 인증할 수 있습니다. 서비스 ID의 개념을 사용하면 클라이언트가 작업을 호출하기 전에 서비스를 인증함으로써 인증되지 않은 호출로부터 클라이언트를 보호할 수 있습니다. 보안 연결에서는 또한 서비스가 클라이언트의 액세스를 허용하기 전에 클라이언트의 자격 증명을 인증하는데, 이 부분은 샘플에서 다루지 않습니다. 서버 인증을 표시 하는 [클라이언트](../../../../docs/framework/wcf/samples/client.md) 의 샘플을 참조 하세요.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

 이 샘플에서는 다음 기능을 보여 줍니다.

- 서비스의 여러 엔드포인트에서 서로 다른 형식의 ID를 설정하는 방법. 각 ID 형식은 서로 다른 기능을 갖습니다. 사용할 ID 형식은 엔드포인트의 바인딩에 사용되는 보안 자격 증명의 형식에 따라 달라집니다.

- ID는 구성에서 선언을 통해 또는 코드에서 명령을 통해 설정할 수 있습니다. 클라이언트와 서버 모두 구성을 사용하여 ID를 설정하는 것이 일반적입니다.

- 클라이언트에서 사용자 지정 ID를 설정하는 방법. 사용자 지정 ID는 일반적으로 기존 ID 형식을 사용자 지정한 것으로서, 이를 통해 클라이언트가 서비스의 자격 증명에 제공된 다른 클레임 정보를 검사하여 서비스 호출에 앞서 권한 부여 결정을 내릴 수 있습니다.

    > [!NOTE]
    > 이 샘플에서는 identity.com이라는 특정 인증서의 ID와 이 인증서 내부에 포함된 RSA 키를 검사합니다. 클라이언트의 구성에서 인증서 및 RSA ID 형식을 사용할 경우 이 값이 serialize되는 서비스에서 WSDL을 검사하면 이 값을 손쉽게 얻을 수 있습니다.

 다음 샘플 코드에서는 WSHttpBinding을 사용하여 인증서의 DNS(도메인 이름 서버)로 서비스 엔드포인트의 ID를 구성하는 방법을 보여 줍니다.

```csharp
//Create a service endpoint and set its identity to the certificate's DNS
WSHttpBinding wsAnonbinding = new WSHttpBinding (SecurityMode.Message);
// Client are Anonymous to the service
wsAnonbinding.Security.Message.ClientCredentialType = MessageCredentialType.None;
WServiceEndpoint ep = serviceHost.AddServiceEndpoint(typeof(ICalculator),wsAnonbinding, String.Empty);
EndpointAddress epa = new EndpointAddress(dnsrelativeAddress,EndpointIdentity.CreateDnsIdentity("identity.com"));
ep.Address = epa;
```

 또한 이 ID는 App.config 파일의 구성에서 지정할 수도 있습니다. 다음 예제에서는 서비스 엔드포인트에 대해 UPN(User Principal Name) ID를 설정하는 방법을 보여 줍니다.

```xml
<endpoint address="upnidentity"
        behaviorConfiguration=""
        binding="wsHttpBinding"
        bindingConfiguration="WSHttpBinding_Windows"
        name="WSHttpBinding_ICalculator_Windows"
        contract="Microsoft.ServiceModel.Samples.ICalculator">
  <!-- Set the UPN identity for this endpoint -->
  <identity>
      <userPrincipalName value="host\myservice.com" />
  </identity >
</endpoint>
```

 사용자 지정 ID는 <xref:System.ServiceModel.EndpointIdentity> 및 <xref:System.ServiceModel.Security.IdentityVerifier> 클래스에서 파생하여 클라이언트에 설정할 수 있습니다. 개념적으로 <xref:System.ServiceModel.Security.IdentityVerifier> 클래스는 서비스의 `AuthorizationManager` 클래스와 동등한 클라이언트로 간주할 수 있습니다. 다음 코드 예제에서는 `OrgEndpointIdentity`의 구현을 보여 주는데, 이는 서버 인증서의 주체 이름에 일치시킬 조직 이름을 저장합니다. 조직 이름에 대한 권한 부여 검사는 `CheckAccess` 클래스의 `CustomIdentityVerifier` 메서드에서 이루어집니다.

```csharp
// This custom EndpointIdentity stores an organization name
public class OrgEndpointIdentity : EndpointIdentity
{
    private string orgClaim;
    public OrgEndpointIdentity(string orgName)
    {
        orgClaim = orgName;
    }
    public string OrganizationClaim
    {
        get { return orgClaim; }
        set { orgClaim = value; }
    }
}

//This custom IdentityVerifier uses the supplied OrgEndpointIdentity to
//check that X.509 certificate's distinguished name claim contains
//the organization name e.g. the string value "O=Contoso"
class CustomIdentityVerifier : IdentityVerifier
{
    public override bool CheckAccess(EndpointIdentity identity, AuthorizationContext authContext)
    {
        bool returnvalue = false;
        foreach (ClaimSet claimset in authContext.ClaimSets)
        {
            foreach (Claim claim in claimset)
            {
                if (claim.ClaimType == "http://schemas.microsoft.com/ws/2005/05/identity/claims/x500distinguishedname")
                {
                    X500DistinguishedName name = (X500DistinguishedName)claim.Resource;
                    if (name.Name.Contains(((OrgEndpointIdentity)identity).OrganizationClaim))
                    {
                        Console.WriteLine("Claim Type: {0}",claim.ClaimType);
                        Console.WriteLine("Right: {0}", claim.Right);
                        Console.WriteLine("Resource: {0}",claim.Resource);
                        Console.WriteLine();
                        returnvalue = true;
                    }
                }
            }
        }
        return returnvalue;
    }
}
```

 이 샘플에서는 언어별 ID 솔루션 폴더에 있는 identity.com이라는 인증서를 사용합니다.

### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.

2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.

3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.

### <a name="to-run-the-sample-on-the-same-computer"></a>단일 컴퓨터 구성에서 샘플을 실행하려면

1. [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 또는 [!INCLUDE[wv](../../../../includes/wv-md.md)]에서 MMC 스냅인 도구를 사용하여 ID 솔루션 폴더의 Identity.pfx 인증서 파일을 LocalMachine/My(개인) 인증서 저장소로 가져옵니다. 이 파일은 암호로 보호됩니다. 가져오는 동안 암호를 묻는 메시지가 나타납니다. 암호 `xyz` 상자에를 입력 합니다. 자세한 내용은 [방법: MMC 스냅인](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md) 을 사용 하 여 인증서 보기 항목을 참조 하십시오. 이 작업이 완료 되 면 관리자 권한으로 Visual Studio에 대 한 개발자 명령 프롬프트에서 Setup.exe를 실행 합니다. 그러면이 인증서가 클라이언트에서 사용 하기 위해 CurrentUser/Trusted 사용자 저장소로 복사 됩니다.

2. 에서 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]관리자 권한으로 Visual Studio 2012 명령 프롬프트 내의 샘플 설치 폴더에서 setup.exe를 실행 합니다. 이 작업은 샘플 실행에 필요한 모든 인증서를 설치합니다.

    > [!NOTE]
    > 설치 .bat 배치 파일은 Visual Studio 2012 명령 프롬프트에서 실행 되도록 디자인 되었습니다. Visual Studio 2012 명령 프롬프트 내에서 설정 된 PATH 환경 변수는 Setup. .bat 스크립트에 필요한 실행 파일을 포함 하는 디렉터리를 가리킵니다. 샘플 사용을 마쳤으면 Cleanup.bat를 실행하여 인증서를 제거해야 합니다. 다른 보안 샘플에도 동일한 인증서가 사용됩니다.  
  
3. \service\bin 디렉터리에서 Service.exe를 시작합니다. 서비스가 준비 되었음을 나타내고 > enter 키를 눌러 \<서비스를 종료 하 라는 메시지가 표시 되는지 확인 합니다.  
  
4. 빌드하고 실행하려면 \client\bin 디렉터리에서 Client.exe를 시작하거나 Visual Studio에서 F5 키를 누릅니다. 클라이언트 콘솔 애플리케이션에 클라이언트 동작이 표시됩니다.  
  
5. 클라이언트와 서비스가 통신할 수 없는 경우 [WCF 샘플에 대 한 문제 해결 팁](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))을 참조 하세요.  
  
### <a name="to-run-the-sample-across-computers"></a>다중 컴퓨터 구성에서 샘플을 실행하려면  
  
1. 샘플의 클라이언트 부분을 빌드하기 전에 Client.cs 파일의 `CallServiceCustomClientIdentity` 메서드에서 서비스의 엔드포인트 주소 값을 변경해야 합니다. 그런 다음 샘플을 빌드합니다.  
  
2. 서비스 컴퓨터에 디렉터리를 만듭니다.  
  
3. 서비스 프로그램 파일을 service\bin에서 서비스 컴퓨터에 있는 디렉터리에 복사합니다. Setup.bat 및 Cleanup.bat 파일도 서비스 컴퓨터로 복사합니다.  
  
4. 클라이언트 컴퓨터에 클라이언트 이진 파일용 디렉터리를 만듭니다.  
  
5. 클라이언트 프로그램 파일을 클라이언트 컴퓨터의 클라이언트 디렉터리로 복사합니다. Setup.bat, Cleanup.bat 및 ImportServiceCert.bat 파일도 클라이언트로 복사합니다.  
  
6. 서비스에서 관리자 권한으로 `setup.bat service` 연 Visual Studio 용 개발자 명령 프롬프트를 실행 합니다. 인수`service` 를 사용 하 여를 실행 하면 컴퓨터의 정규화 된 도메인 이름으로 서비스 인증서가 생성 되 `setup.bat` 고 서비스 인증서가 이름이 .cer 인 파일로 내보내집니다.  
  
7. 서비스 디렉터리에서 클라이언트 컴퓨터의 클라이언트 디렉터리로 Service.cer 파일을 복사합니다.  
  
8. 클라이언트 컴퓨터의 Client.exe.config 파일에서 엔드포인트의 주소 값을 서비스의 새 주소와 일치하도록 변경합니다. 여러 개의 인스턴스를 변경해야 합니다.  
  
9. 클라이언트에서 관리자 권한으로 연 Visual Studio 용 개발자 명령 프롬프트 열고 importservicecert.bat를 실행 합니다. 이 작업은 Service.cer 파일의 서비스 인증서를 CurrentUser - TrustedPeople 저장소로 가져옵니다.  
  
10. 서비스 컴퓨터의 명령 프롬프트에서 Service.exe를 실행합니다.  
  
11. 클라이언트 컴퓨터의 명령 프롬프트에서 Client.exe를 실행합니다. 클라이언트와 서비스가 통신할 수 없는 경우 [WCF 샘플에 대 한 문제 해결 팁](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))을 참조 하세요.  
  
### <a name="to-clean-up-after-the-sample"></a>샘플 실행 후 정리를 수행하려면  
  
- 샘플 실행을 완료했으면 샘플 폴더에서 Cleanup.bat를 실행합니다.  
  
    > [!NOTE]
    > 다중 컴퓨터 구성에서 이 샘플을 실행할 경우에는 이 스크립트로 클라이언트의 서비스 인증서를 제거할 수 없습니다. 컴퓨터에서 인증서를 사용 하는 WCF (Windows Communication Foundation) 샘플을 실행 한 경우에는 CurrentUser-비트 사용자 저장소에 설치 된 서비스 인증서를 지워야 합니다. 이렇게 하려면 다음 명령을 사용 합니다. `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`예를 들면 `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`와 같습니다.
