---
title: '방법: 구성 파일을 사용하여 서비스에 대한 메타데이터 게시'
ms.date: 03/30/2017
ms.assetid: f061443f-92df-4824-b36a-609c4cd14a17
ms.openlocfilehash: 26894a3951b91879a7b3e6f66731891113394082
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045301"
---
# <a name="how-to-publish-metadata-for-a-service-using-a-configuration-file"></a>방법: 구성 파일을 사용하여 서비스에 대한 메타데이터 게시
이 항목은 WCF (Windows Communication Foundation) 서비스용 게시 메타 데이터를 보여 주는 두 가지 방법 항목 중 하나입니다. 서비스에서 메타데이터를 게시하는 방법을 지정하는 두 가지 방법은 구성 파일을 사용하는 방법과 코드를 사용하는 방법입니다. 이 항목에서는 구성 파일을 사용하여 서비스에 대해 메타데이터를 게시하는 방법에 대해 설명합니다.  
  
> [!CAUTION]
> 이 항목에서는 보호되지 않은 방식으로 메타데이터를 게시하는 방법을 보여 줍니다. 즉, 모든 클라이언트가 서비스에서 메타데이터를 검색할 수 있습니다. 서비스에서 메타 데이터를 안전한 방식으로 게시 해야 하는 경우 [사용자 지정 보안 메타 데이터 끝점](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md)을 참조 하세요.  
  
 코드에 메타 데이터를 게시 [하는 방법에 대 한 자세한 내용은 방법: 코드](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md)를 사용 하 여 서비스에 대 한 메타 데이터를 게시 합니다. 메타데이터를 게시하면 클라이언트에서 WS-Transfer GET 요청을 사용하는 메타데이터 또는 `?wsdl` 쿼리 문자열을 사용하는 HTTP/GET 요청을 검색할 수 있습니다. 코드가 작동 하는지 확인할 수 있도록 기본 WCF 서비스를 만듭니다. 편의상 다음 코드로 된 기본 자체 호스팅 서비스가 제공됩니다.  
  
```csharp  
using System;  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Description;  
  
namespace Metadata.Samples  
{  
    [ServiceContract]  
    public interface ISimpleService  
    {  
        [OperationContract]  
        string SimpleMethod(string msg);  
    }  
  
    class SimpleService : ISimpleService  
    {  
        public string SimpleMethod(string msg)  
        {  
            Console.WriteLine("The caller passed in " + msg);  
            return "Hello " + msg;  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            ServiceHost host = new ServiceHost(typeof(SimpleService),  
                new Uri("http://localhost:8001/MetadataSample"));   
            try  
            {  
                // Open the service host to accept incoming calls  
                host.Open();  
  
                // The service can now be accessed.  
                Console.WriteLine("The service is ready.");  
                Console.WriteLine("Press <ENTER> to terminate service.");  
                Console.WriteLine();  
                Console.ReadLine();  
  
                // Close the ServiceHostBase to shutdown the service.  
                host.Close();  
            }  
            catch (CommunicationException commProblem)  
            {  
                Console.WriteLine("There was a communication problem. " + commProblem.Message);  
                Console.Read();  
            }  
        }  
    }  
}  
```  
  
 이 서비스는 구성 파일을 사용하여 구성된 자체 호스팅 서비스입니다. 다음 구성 파일을 사용해 작업을 시작합니다.  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service name="Metadata.Example.SimpleService">  
        <endpoint address=""  
                  binding="basicHttpBinding"  
                  contract="Metadata.Example.ISimpleService" />  
      </service>  
    </services>  
    <behaviors>  
  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
### <a name="to-publish-metadata-for-a-wcf-service-using-an-application-configuration-file"></a>애플리케이션 구성 파일을 사용하여 WCF 서비스의 메타데이터를 게시하려면  
  
1. App.config 파일 내에서 `</services>` 요소를 닫은 후`<behaviors>` 요소를 만듭니다.  

2. 내 합니다 `<behaviors>` 요소를 추가 `<serviceBehaviors>` 요소입니다.  

3. 추가 `<behavior>` 요소를를 `<serviceBehaviors>` 요소에 대 한 값을 지정 합니다 `name` 특성을 `<behavior>` 요소입니다.  

4. `<serviceMetadata>` 요소를 `<behavior>` 요소에 추가합니다. `httpGetEnabled` 특성을 `true`로 설정하고 `policyVersion` 특성을 Policy15로 설정합니다. `httpGetEnabled`를 사용하면 서비스가 HTTP GET 요청으로 수행된 메타데이터 요청에 응답할 수 있습니다. `policyVersion`에 따라 서비스는 메타데이터를 생성할 때 WS-Policy 1.5를 준수합니다.  

5. 다음 코드 예제와 같이 `behaviorConfiguration` 특성을 `<service>` 요소에 추가하고 1단계에 추가된 `name` 요소의 `<behavior>` 특성을 지정합니다.  
  
    ```xml  
    <services>  
      <service  
          name="Metadata.Example.SimpleService"  
          behaviorConfiguration="SimpleServiceBehavior">  
        ...  
      </service>  
    </services>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="SimpleServiceBehavior">  
          <serviceMetadata httpGetEnabled="True" policyVersion="Policy15" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
6. 다음 코드 예제와 같이 계약이 `<endpoint>`로 설정된 하나 이상의 `IMetadataExchange` 요소를 추가합니다.  
  
    ```xml  
    <services>  
      <service  
          name="Metadata.Example.SimpleService"  
          behaviorConfiguration="SimpleServiceBehavior">  
  
        <endpoint address=""  
                  binding="wsHttpBinding"  
                  contract="Metadata.Example.ISimpleService" />  
  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange" />  
      </service>  
    </services>  
    ```  
  
7. 이전 단계에 추가된 메타데이터 엔드포인트에 대해 `binding` 특성을 다음 중 하나로 설정합니다.  
  
    - HTTP 게시의 경우 `mexHttpBinding`  
  
    - HTTPS 게시의 경우 `mexHttpsBinding`  
  
    - 명명된 파이프 게시의 경우 `mexNamedPipeBinding`  
  
    - TCP 게시의 경우 `mexTcpBinding`  
  
8. 이전 단계에 추가된 메타데이터 엔드포인트에 대해 주소를 다음과 같이 설정합니다.  
  
    - 기본 주소가 메타데이터 바인딩과 동일한 경우 호스트 애플리케이션의 기본 주소를 게시 지점으로 사용하는 빈 문자열  
  
    - 호스트 애플리케이션에 기본 주소가 있는 경우 상대 주소  
  
    - 절대 경로  
  
9. 콘솔 애플리케이션을 빌드하고 실행합니다.  
  
10. Internet Explorer를 사용 하 여 서비스의 기본 주소 (http://localhost:8001/MetadataSample 이 예제에서는)로 이동 하 여 메타 데이터 게시가 설정 되었는지 확인 합니다. 그렇지 않으면 결과 페이지의 맨 위에 메시지가 표시 됩니다. "이 서비스에 대 한 메타 데이터 게시는 현재 사용할 수 없습니다."  
  
### <a name="to-use-default-endpoints"></a>기본 엔드포인트를 사용하려면  
  
1. 기본 엔드포인트를 사용하는 서비스에서 메타데이터를 구성하려면 이전 예제와 같이 구성 파일에 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>를 구성하되 엔드포인트는 지정하지 마세요. 이렇게 구성하면 구성 파일이 다음과 같아집니다.  
  
    ```xml  
    <configuration>  
      <system.serviceModel>  
        <behaviors>  
          <serviceBehaviors>  
            <behavior name="SimpleServiceBehavior">  
              <serviceMetadata httpGetEnabled="True" policyVersion="Policy12" />  
            </behavior>  
          </serviceBehaviors>  
        </behaviors>  
  
      </system.serviceModel>  
    </configuration>  
    ```  
  
     서비스에 포함된 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>의 `httpGetEnabled`가 `true`로 설정되어 있으므로 서비스의 메타데이터 게시 기능은 사용하도록 설정되었으며, 엔드포인트를 명시적으로 추가하지 않았으므로 런타임이 기본 엔드포인트를 추가합니다. 기본 엔드포인트, 바인딩 및 동작에 대한 자세한 내용은 [단순화된 구성](../../../../docs/framework/wcf/simplified-configuration.md) 및 [WCF 서비스를 위한 단순화된 구성](../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 서비스에 대 한 메타 데이터를 게시 하는 기본 WCF 서비스 및 구성 파일의 구현을 보여 줍니다.  
  
```csharp  
using System;  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Description;  
  
namespace Metadata.Samples  
{  
    [ServiceContract]  
    public interface ISimpleService  
    {  
        [OperationContract]  
        string SimpleMethod(string msg);  
    }  
  
    class SimpleService : ISimpleService  
    {  
        public string SimpleMethod(string msg)  
        {  
            Console.WriteLine("The caller passed in " + msg);  
            return "Hello " + msg;  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            ServiceHost host = new ServiceHost(typeof(SimpleService),  
                new Uri("http://localhost:8001/MetadataSample"));   
            try  
            {  
                // Open the service host to accept incoming calls  
                host.Open();  
  
                // The service can now be accessed.  
                Console.WriteLine("The service is ready.");  
                Console.WriteLine("Press <ENTER> to terminate service.");  
                Console.WriteLine();  
                Console.ReadLine();  
  
                // Close the ServiceHostBase to shutdown the service.  
                host.Close();  
            }  
            catch (CommunicationException commProblem)  
            {  
                Console.WriteLine("There was a communication problem. " + commProblem.Message);  
                Console.Read();  
            }  
        }  
    }  
}  
```  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="SimpleServiceBehavior">  
          <serviceMetadata httpGetEnabled="True" policyVersion="Policy12" />  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Description.ServiceMetadataBehavior>
- [방법: 관리 되는 응용 프로그램에서 WCF 서비스 호스팅](../../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)
- [자체 호스팅](../../../../docs/framework/wcf/samples/self-host.md)
- [메타데이터 아키텍처 개요](../../../../docs/framework/wcf/feature-details/metadata-architecture-overview.md)
- [메타데이터 사용](../../../../docs/framework/wcf/feature-details/using-metadata.md)
- [방법: 코드를 사용 하 여 서비스에 대 한 메타 데이터 게시](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md)
