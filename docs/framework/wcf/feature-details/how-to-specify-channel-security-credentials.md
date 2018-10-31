---
title: '방법: 채널 보안 자격 증명 지정'
ms.date: 03/30/2017
ms.assetid: f8e03f47-9c4f-4dd5-8f85-429e6d876119
ms.openlocfilehash: f4c2977fe5bc819ff7e9b7a8030b2c2e20b71429
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50201467"
---
# <a name="how-to-specify-channel-security-credentials"></a>방법: 채널 보안 자격 증명 지정
Windows Communication Foundation (WCF) 서비스 모니커는 COM 응용 프로그램이 WCF 서비스를 호출할 수 있습니다. 대부분의 WCF 서비스 클라이언트를 인증 및 권한 부여에 대 한 자격 증명을 지정 해야 합니다. WCF 클라이언트에서 WCF 서비스를 호출할 때 응용 프로그램 구성 파일 또는 관리 코드에서 이러한 자격 증명을 지정할 수 있습니다. COM 응용 프로그램에서 WCF 서비스를 호출할 때 사용할 수는 <xref:System.ServiceModel.ComIntegration.IChannelCredentials> 인터페이스 자격 증명을 지정 합니다. 이 항목에서는 <xref:System.ServiceModel.ComIntegration.IChannelCredentials> 인터페이스를 사용하여 자격 증명을 지정하는 다양한 방식을 설명합니다.  
  
> [!NOTE]
>  <xref:System.ServiceModel.ComIntegration.IChannelCredentials>는 IDispatch 기반 인터페이스이며 Visual Studio 환경에서는 IntelliSense 기능을 가져오지 않습니다.  
  
 이 문서에 정의 된 WCF 서비스를 사용 합니다는 [메시지 보안 샘플](../../../../docs/framework/wcf/samples/message-security-sample.md)합니다.  
  
### <a name="to-specify-a-client-certificate"></a>클라이언트 인증서 지정  
  
1.  Message Security 디렉터리에서 Setup.bat 파일을 실행하여 필요한 테스트 인증서를 만든 후 설치합니다.  
  
2.  메시지 보안 프로젝트를 엽니다.  
  
3.  추가 `[ServiceBehavior(Namespace=``http://Microsoft.ServiceModel.Samples``)]` 에 `ICalculator` 인터페이스 정의 합니다.  
  
4.  추가 `bindingNamespace=``http://Microsoft.ServiceModel.Samples` 서비스용 App.config의 끝점 태그입니다.  
  
5.  메시지 보안 샘플을 빌드하고 Service.exe를 실행합니다. Internet Explorer를 사용 하 고 서비스의 URI로 이동 (http://localhost:8000/ServiceModelSamples/Service) 서비스가 작동 하는지 확인 합니다.  
  
6.  Visual Basic 6.0을 열고 새 표준 .exe 파일을 만듭니다. 폼에 단추를 추가하고 단추를 두 번 클릭하여 다음 코드를 클릭 처리기에 추가합니다.  
  
    ```  
        monString = "service:mexAddress=http://localhost:8000/ServiceModelSamples/Service?wsdl"  
        monString = monString + ", address=http://localhost:8000/ServiceModelSamples/Service"  
        monString = monString + ", contract=ICalculator, contractNamespace=http://Microsoft.ServiceModel.Samples"  
        monString = monString + ", binding=BasicHttpBinding_ICalculator, bindingNamespace=http://Microsoft.ServiceModel.Samples"  
  
        Set monikerProxy = GetObject(monString)  
  
        'Set the Service Certificate.  
     monikerProxy.ChannelCredentials.SetServiceCertificateAuthentication "CurrentUser", "NoCheck", "PeerOrChainTrust"  
    monikerProxy.ChannelCredentials.SetDefaultServiceCertificateFromStore "CurrentUser", "TrustedPeople", "FindBySubjectName", "localhost"  
  
        'Set the Client Certificate.  
        monikerProxy.ChannelCredentials.SetClientCertificateFromStoreByName "CN=client.com", "CurrentUser", "My"  
        MsgBox monikerProxy.Add(3, 4)  
    ```  
  
7.  Visual Basic 응용 프로그램을 실행하고 결과를 확인합니다.  
  
     Visual Basic 응용 프로그램에 메시지 상자가 나타나며 Add(3, 4)를 호출한 결과가 표시됩니다. <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetClientCertificateFromFile%28System.String%2CSystem.String%2CSystem.String%29> 또는 <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetClientCertificateFromStoreByName%28System.String%2CSystem.String%2CSystem.String%29>을 <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetClientCertificateFromStore%28System.String%2CSystem.String%2CSystem.String%2CSystem.Object%29> 대신 사용하여 클라이언트 인증서를 설정할 수도 있습니다.  
  
    ```  
    monikerProxy.ChannelCredentials.SetClientCertificateFromFile "C:\MyClientCert.pfx", "password", "DefaultKeySet"  
    ```  
  
> [!NOTE]
>  이 호출이 작동하려면 클라이언트가 실행 중인 컴퓨터에서 클라이언트 인증서가 신뢰되어야 합니다.  
  
> [!NOTE]
>  모니커의 형식이 잘못되었거나 서비스를 사용할 수 없는 경우 `GetObject`를 호출하면 "구문이 잘못되었습니다."라는 오류가 반환됩니다. 이 오류가 발생하면 사용하고 있는 모니커가 올바르고 서비스를 사용할 수 있는지 확인하세요.  
  
### <a name="to-specify-user-name-and-password"></a>사용자 이름 및 암호 지정  
  
1.  `wsHttpBinding`을 사용하도록 Service App.config 파일을 수정합니다. 이 때 사용자 이름과 암호를 확인해야 합니다.  
  
  
  
2.  `clientCredentialType`을 UserName으로 설정합니다.  
  
  
  
3.  Visual Basic 6.0을 열고 새 표준 .exe 파일을 만듭니다. 폼에 단추를 추가하고 단추를 두 번 클릭하여 다음 코드를 클릭 처리기에 추가합니다.  
  
    ```  
    monString = "service:mexAddress=http://localhost:8000/ServiceModelSamples/Service?wsdl"  
    monString = monString + ", address=http://localhost:8000/ServiceModelSamples/Service"  
    monString = monString + ", contract=ICalculator, contractNamespace=http://Microsoft.ServiceModel.Samples"  
    monString = monString + ", binding=WSHttpBinding_ICalculator, bindingNamespace=http://Microsoft.ServiceModel.Samples"  
  
    Set monikerProxy = GetObject(monString)  
  
    monikerProxy.ChannelCredentials.SetServiceCertificateAuthentication "CurrentUser", "NoCheck", "PeerOrChainTrust"  
    monikerProxy.ChannelCredentials.SetUserNameCredential "username", "password"  
  
    MsgBox monikerProxy.Add(3, 4)  
    ```  
  
4.  Visual Basic 응용 프로그램을 실행하고 결과를 확인합니다. Visual Basic 응용 프로그램에 메시지 상자가 나타나며 Add(3, 4)를 호출한 결과가 표시됩니다.  
  
    > [!NOTE]
    >  이 샘플의 서비스 모니커에 지정된 바인딩이 WSHttpBinding_ICalculator로 변경되었습니다. 또한 <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetUserNameCredential%28System.String%2CSystem.String%29>을 호출할 때 유효한 사용자 이름과 암호를 제공해야 합니다.  
  
### <a name="to-specify-windows-credentials"></a>Windows 자격 증명 지정  
  
1.  Service App.config 파일에서 `clientCredentialType`을 Windows로 설정합니다.  
  
  
  
2.  Visual Basic 6.0을 열고 새 표준 .exe 파일을 만듭니다. 폼에 단추를 추가하고 단추를 두 번 클릭하여 다음 코드를 클릭 처리기에 추가합니다.  
  
    ```  
    monString = "service:mexAddress=http://localhost:8000/ServiceModelSamples/Service?wsdl"  
    monString = monString + ", address=http://localhost:8000/ServiceModelSamples/Service"  
    monString = monString + ", contract=ICalculator, contractNamespace=http://Microsoft.ServiceModel.Samples"  
    monString = monString + ", binding=WSHttpBinding_ICalculator, bindingNamespace=http://Microsoft.ServiceModel.Samples"  
    monString = monString + ", upnidentity=domain\userID"  
  
    Set monikerProxy = GetObject(monString)  
     monikerProxy.ChannelCredentials.SetWindowsCredential "domain", "userID", "password", 1, True  
  
    MsgBox monikerProxy.Add(3, 4)  
    ```  
  
3.  Visual Basic 응용 프로그램을 실행하고 결과를 확인합니다. Visual Basic 응용 프로그램에 메시지 상자가 나타나며 Add(3, 4)를 호출한 결과가 표시됩니다.  
  
    > [!NOTE]
    >  "domain", "userID" 및 "password"를 유효한 값으로 바꿔야 합니다.  
  
### <a name="to-specify-an-issue-token"></a>발급 토큰 지정  
  
1.  발급 토큰은 페더레이션 보안을 사용하는 응용 프로그램에서만 사용됩니다. 페더레이션된 보안에 대 한 자세한 내용은 참조 하세요. [페더레이션 및 발급 된 토큰](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md) 하 고 [페더레이션 샘플](../../../../docs/framework/wcf/samples/federation-sample.md)합니다.  
  
     다음 Visual Basic 코드 예제에서는 <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetIssuedToken%28System.String%2CSystem.String%2CSystem.String%29> 메서드를 호출하는 방법을 보여 줍니다.  
  
    ```  
        monString = "service:mexAddress=http://localhost:8000/ServiceModelSamples/Service?wsdl"  
        monString = monString + ", address=http://localhost:8000/SomeService/Service"  
        monString = monString + ", contract=ICalculator, contractNamespace=http://SomeService.Samples"  
        monString = monString + ", binding=WSHttpBinding_ISomeContract, bindingNamespace=http://SomeService.Samples"  
  
        Set monikerProxy = GetObject(monString)  
    monikerProxy.SetIssuedToken("http://somemachine/sts", "bindingType", "binding")  
    ```  
  
     이 메서드의 매개 변수에 대한 자세한 내용은 <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetIssuedToken%28System.String%2CSystem.String%2CSystem.String%29>을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [페더레이션](../../../../docs/framework/wcf/feature-details/federation.md)  
 [방법: 페더레이션 서비스에서 자격 증명 구성](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)  
 [방법: 페더레이션 클라이언트 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)  
 [메시지 보안](../../../../docs/framework/wcf/feature-details/message-security-in-wcf.md)  
 [바인딩 및 보안](../../../../docs/framework/wcf/feature-details/bindings-and-security.md)
