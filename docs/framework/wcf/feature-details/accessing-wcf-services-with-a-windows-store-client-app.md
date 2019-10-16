---
title: Windows 스토어 클라이언트 응용 프로그램을 사용하여 WCF 서비스에 액세스
ms.date: 03/30/2017
ms.assetid: e2002ef4-5dee-4a54-9d87-03b33d35fc52
ms.openlocfilehash: 7a50454c5189c48704adfaaed2c90d2638dd677f
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928967"
---
# <a name="accessing-wcf-services-with-a-windows-store-client-app"></a>Windows 스토어 클라이언트 응용 프로그램을 사용하여 WCF 서비스에 액세스
Windows 8에서는 Windows 스토어 애플리케이션이라는 새로운 형식의 애플리케이션을 제공합니다. 이러한 애플리케이션은 터치 스크린 인터페이스를 바탕으로 설계되었습니다. .NET Framework 4.5에서는 Windows 스토어 애플리케이션을 사용하여 WCF 서비스를 호출할 수 있습니다.  
  
## <a name="wcf-support-in-windows-store-applications"></a>Windows 스토어 애플리케이션의 WCF 지원  
 Windows 스토어 애플리케이션 내에서 일부 WCF 기능을 사용할 수 있습니다. 자세한 내용은 다음 단원을 참조하세요.  
  
> [!IMPORTANT]
> WCF에서 노출하는 API 대신 WinRT 배포 API를 사용하세요. 자세한 내용은 [WinRT 배포 API](https://go.microsoft.com/fwlink/?LinkId=236265)를 참조하세요.  
  
> [!WARNING]
> 서비스 참조 추가 기능을 사용하여 Windows 런타임 구성 요소에 웹 서비스 참조를 추가할 수는 없습니다.  
  
### <a name="supported-bindings"></a>지원되는 바인딩  
 Windows 스토어 애플리케이션에서는 다음과 같은 WCF 바인딩이 지원됩니다.  
  
1. <xref:System.ServiceModel.BasicHttpBinding>  
  
2. <xref:System.ServiceModel.NetTcpBinding>  
  
3. <xref:System.ServiceModel.NetHttpBinding>  
  
4. <xref:System.ServiceModel.Channels.CustomBinding>
  
 Windows 스토어 애플리케이션에서는 다음과 같은 바인딩 요소가 지원됩니다.  
  
1. <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>  
  
2. <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>  
  
3. <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement>  
  
4. <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>  
  
5. <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>  
  
6. <xref:System.ServiceModel.Channels.TcpTransportBindingElement>  
  
7. <xref:System.ServiceModel.Channels.HttpTransportBindingElement>  
  
8. <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>  
  
9. <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>  
  
 텍스트 인코딩과 이진 인코딩 모두가 지원됩니다. 모든 WCF 전송 모드가 지원됩니다. 자세한 내용은 [Streaming Message Transfer](../../../../docs/framework/wcf/feature-details/streaming-message-transfer.md)를 참조하세요.  
  
### <a name="add-service-reference"></a>서비스 참조 추가  
 Windows 스토어 애플리케이션에서 WCF 서비스를 호출하려면 Visual Studio 2012의 서비스 참조 추가 기능을 사용하세요. Windows 스토어 애플리케이션 내에서 서비스 참조 추가 기능이 완료될 때 몇 가지 변경 내용을 확인할 수 있습니다. 먼저, 구성 파일이 생성되지 않습니다. Windows 스토어 애플리케이션은 구성 파일을 사용하지 않으므로 코드로 구성되어야 합니다. 이 구성 코드는 서비스 참조 추가를 통해 생성된 References.cs 파일에 있습니다. 이 파일을 보려면 솔루션 탐색기에서 "모든 파일 표시"를 선택 해야 합니다. 해당 파일은 프로젝트 내의 서비스 참조 노드 및 Reference.svcmap 노드 아래에 있습니다. Windows 스토어 애플리케이션 내의 WCF 서비스에 대해 생성된 모든 작업은 태스크 기반 비동기 패턴을 사용하여 비동기화됩니다. 자세한 내용은 비동기 [작업-작업을 사용 하 여 비동기 프로그래밍 단순화](https://msdn.microsoft.com/magazine/ff959203.aspx)를 참조 하세요.  
  
 이제 구성이 코드로 생성되므로 서비스 참조가 업데이트될 때마다 Reference.cs 파일의 모든 변경 내용을 덮어쓰게 됩니다. 이러한 문제를 해결하기 위해 구성 코드는 부분 메서드(Partial Method) 내에서 생성됩니다. 부분 메서드는 클라이언트 프록시 클래스에서 구현할 수 있습니다. 부분 메서드는 다음과 같이 선언됩니다.  
  
```csharp  
static partial void Configure(System.ServiceModel.Description.ServiceEndpoint serviceEndpoint,  
            System.ServiceModel.Description.ClientCredentials clientCredentials);  
```  
  
 이 부분 메서드를 구현하고 다음과 같이 클라이언트 프록시 클래스에서 바인딩 또는 엔드포인트를 변경할 수 있습니다.  
  
```csharp  
public partial class Service1Client : System.ServiceModel.ClientBase<MetroWcfClient.ServiceRefMultiEndpt.IService1>, MetroWcfClient.ServiceRefMultiEndpt.IService1  
    {   
        static partial void Configure(System.ServiceModel.Description.ServiceEndpoint serviceEndpoint,   
            System.ServiceModel.Description.ClientCredentials clientCredentials)  
        {  
            if (serviceEndpoint.Name ==   
                    ServiceRefMultiEndpt.Service1Client.EndpointConfiguration.BasicHttpBinding_IService1.ToString())  
            {  
                serviceEndpoint.Binding.SendTimeout = new System.TimeSpan(0, 1, 0);  
            }  
            else if (serviceEndpoint.Name ==   
                    ServiceRefMultiEndpt.Service1Client.EndpointConfiguration.BasicHttpBinding_IService11.ToString())  
            {  
                serviceEndpoint.Binding.SendTimeout = new System.TimeSpan(0, 1, 0);  
                clientCredentials.UserName.UserName = "username1";  
                clientCredentials.UserName.Password = "password";  
            }  
            else if (serviceEndpoint.Name ==   
                    ServiceRefMultiEndpt.Service1Client.EndpointConfiguration.NetTcpBinding_IService1.ToString())  
            {  
                serviceEndpoint.Binding.Name = "MyTcpBinding";  
                serviceEndpoint.Address = new System.ServiceModel.EndpointAddress("net.tcp://localhost/tcp");  
            }  
        }  
    }  
```  
  
### <a name="serialization"></a>Serialization  
 Windows 스토어 애플리케이션에서는 다음과 같은 serializer가 지원됩니다.  
  
1. DataContractSerializer  
  
2. DataContractJsonSerializer  
  
3. XmlSerializer  
  
> [!WARNING]
> 이제 XmlDictionaryWriter.Write(DateTime)는 DateTime 개체를 문자열로 씁니다.  
  
### <a name="security"></a>보안  

Windows 스토어 응용 프로그램에서 지원 되는 보안 모드는 다음과 같습니다.
  
1. <xref:System.ServiceModel.SecurityMode.None>  
  
2. <xref:System.ServiceModel.SecurityMode.Transport>  
  
3. <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential>
  
4. <xref:System.ServiceModel.SecurityMode.Message>
  
Windows 스토어 응용 프로그램에서는 다음과 같은 클라이언트 자격 증명 형식이 지원 됩니다.
  
1. 없음  
  
2. Basic  
  
3. Digest  
  
4. Negotiate  
  
5. NTLM  
  
6. Windows  
  
7. Username(메시지 보안)  
  
8. Windows(전송 보안)  
  
 Windows 스토어 애플리케이션이 기본 Windows 자격 증명에 액세스하여 이를 보내도록 하려면 Package.appmanifest 파일 내에서 이 기능을 사용하도록 설정해야 합니다. 이 파일을 열고 기능 탭을 선택한 다음 "기본 Windows 자격 증명"을 선택 합니다. 그러면 도메인 자격 증명이 필요한 인트라넷 리소스에 애플리케이션을 연결할 수 있습니다.  
  
> [!IMPORTANT]
> Windows 스토어 응용 프로그램이 컴퓨터 간 호출을 수행 하도록 하려면 "홈/회사 네트워킹" 이라는 다른 기능을 사용 하도록 설정 해야 합니다. 이 설정은 Package.appmanifest 파일의 기능 탭 아래에도 있습니다. 홈/회사 네트워킹 확인란을 선택합니다. 그러면 집이나 회사와 같이 사용자가 신뢰할 수 있는 장소의 네트워크에 대한 인바운드 및 아웃바운드 액세스 권한이 애플리케이션에 부여됩니다. 중요한 인바운드 포트는 항상 차단됩니다. 인터넷의 서비스에 액세스하려면 인터넷(클라이언트) 기능도 사용하도록 설정해야 합니다.  
  
### <a name="misc"></a>기타  
 Windows 스토어 애플리케이션에 는 다음 클래스를 사용할 수 있습니다.  
  
1. <xref:System.ServiceModel.ChannelFactory>  
  
2. <xref:System.ServiceModel.DuplexChannelFactory%601>
  
3. <xref:System.ServiceModel.CallbackBehaviorAttribute>  
  
### <a name="defining-service-contracts"></a>서비스 계약 정의  
 태스크 기반 비동기 패턴을 사용하여 비동기 서비스 작업만 정의하는 것이 좋습니다. 그러면 서비스 작업을 호출하는 동안 Windows 스토어 애플리케이션이 응답을 유지합니다.  
  
> [!WARNING]
> 동기 작업을 정의하더라도 예외가 throw되지는 않지만 비동기 작업만 정의하는 것이 좋습니다.  
  
### <a name="calling-wcf-services-from-windows-store-applications"></a>Windows 스토어 애플리케이션에서 WCF 서비스 호출  
 앞에서 설명한 것처럼 모든 구성은 생성된 프록시 클래스의 GetBindingForEndpoint 메서드에서 코드로 수행되어야 합니다. 서비스 작업 호출은 다음 코드 조각과 같이 태스크 기반 비동기 메서드를 호출할 때와 동일한 방법으로 수행됩니다.  
  
```csharp  
void async SomeMethod()  
{  
    ServiceClient proxy = new ServiceClient();  
    Task<T> results = await proxy.CallAsync(param1, param2);  
    T result = results.Result;  
    if (result.Success)  
    {  
       // Do something with result  
    }  
}  
```  
  
 비동기 호출을 수행하는 메서드에서는 async 키워드가 사용되고 비동기 메서드를 호출할 때는 await 키워드가 사용됩니다.  
  
## <a name="see-also"></a>참고자료

- [Windows 스토어 앱의 WCF 블로그](https://blogs.msdn.microsoft.com/piyushjo/2011/09/21/wcf-in-windows-8-metro-styled-apps-absolutely-supported/)
- [WCF Windows 스토어 클라이언트 및 보안](https://blogs.msdn.microsoft.com/piyushjo/2011/10/11/calling-a-wcf-service-from-a-metro-application-adding-security/)
- [Windows 스토어 앱 및 컴퓨터 간 호출](https://blogs.msdn.microsoft.com/piyushjo/2011/10/21/calling-a-wcf-service-from-a-metro-application-cross-machine-scenario/)
- [Windows 스토어 앱에서 Azure에 배포 된 WCF 서비스 호출](https://blogs.msdn.com/b/piyushjo/archive/2011/10/22/calling-a-wcf-service-from-a-metro-application-cross-machine-scenario.aspx)
- [WCF 보안 프로그래밍](../../../../docs/framework/wcf/feature-details/programming-wcf-security.md)
- [바인딩](../../../../docs/framework/wcf/bindings.md)
