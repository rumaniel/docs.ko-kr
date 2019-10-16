---
title: 코드로 WCF 서비스 구성
ms.date: 03/30/2017
ms.assetid: 193c725d-134f-4d31-a8f8-4e575233bff6
ms.openlocfilehash: d2ef7b2095bf7f238a25f2db0e5d3cf47e885550
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855648"
---
# <a name="configuring-wcf-services-in-code"></a>코드로 WCF 서비스 구성
WCF (Windows Communication Foundation)를 사용 하면 개발자가 구성 파일 또는 코드를 사용 하 여 서비스를 구성할 수 있습니다.  구성 파일은 배포 후 서비스를 구성해야 하는 경우에 유용합니다. 구성 파일을 사용할 경우 IT 전문가가 구성 파일을 업데이트하기만 하면 되고 다시 컴파일할 필요가 없습니다. 하지만 구성 파일은 관리하기가 복잡하고 어려울 수 있습니다. 구성 파일 디버깅은 지원되지 않으며 구성 요소는 이름으로 참조되므로 구성 파일을 작성하기가 어렵고 오류가 발생하기 쉽습니다. WCF를 사용 하면 코드에서 서비스를 구성할 수도 있습니다. 이전 버전의 WCF (4.0 및 이전 버전)에서 코드의 서비스 구성은 자체 호스팅 시나리오에서 쉽기 때문에 클래스 <xref:System.ServiceModel.ServiceHost> 를 통해 ServiceHost를 호출 하기 전에 끝점과 동작을 구성할 수 있었습니다. 그러나 웹 호스팅 시나리오에서는 <xref:System.ServiceModel.ServiceHost> 클래스에 직접 액세스할 수 없습니다. 웹 호스팅 서비스를 구성하려면 `System.ServiceModel.ServiceHostFactory`를 만들고 필요한 구성을 수행하는 <xref:System.ServiceModel.Activation.ServiceHostFactory>를 만들어야 했습니다. .NET 4.5 부터는 WCF 둘 다 구성 하는 간단한 방법인 자체 호스팅 및 웹 호스팅 코드에서 서비스를 제공 합니다.  
  
## <a name="the-configure-method"></a>Configure 메서드  
 서비스 구현 클래스에서 다음 서명으로 `Configure`라는 공용 정적 메서드를 정의하기만 하면 됩니다.  
  
```csharp  
public static void Configure(ServiceConfiguration config)  
```  
  
 Configure 메서드는 개발자가 엔드포인트 및 동작을 추가할 수 있도록 해 주는 <xref:System.ServiceModel.ServiceConfiguration> 인스턴스를 사용합니다. 이 메서드는 서비스 호스트가 열리기 전에 WCF에서 호출 됩니다. 정의할 때 app.config 또는 web.config 파일에 지정된 서비스 구성 설정이 무시됩니다.  
  
 다음 코드 조각은 `Configure` 메서드를 정의하는 방법과 서비스 엔드포인트, 엔드포인트 동작 및 서비스 동작을 추가하는 방법을 설명합니다.  
  
```csharp  
public class Service1 : IService1  
    {  
        public static void Configure(ServiceConfiguration config)  
        {  
            ServiceEndpoint se = new ServiceEndpoint(new ContractDescription("IService1"), new BasicHttpBinding(), new EndpointAddress("basic"));  
            se.Behaviors.Add(new MyEndpointBehavior());  
            config.AddServiceEndpoint(se);  
  
            config.Description.Behaviors.Add(new ServiceMetadataBehavior { HttpGetEnabled = true });  
            config.Description.Behaviors.Add(new ServiceDebugBehavior { IncludeExceptionDetailInFaults = true });  
        }  
  
        public string GetData(int value)  
        {  
            return $"You entered: {value}";
        }  
  
        public CompositeType GetDataUsingDataContract(CompositeType composite)  
        {  
            if (composite == null)  
            {  
                throw new ArgumentNullException("composite");  
            }  
            if (composite.BoolValue)  
            {  
                composite.StringValue += "Suffix";  
            }  
            return composite;  
        }  
    }  
```  
  
 서비스에 https와 같은 프로토콜을 사용하려면 프로토콜을 사용하는 엔드포인트를 명시적으로 추가하거나 프로토콜 및 정의된 각 서비스 계약과 호환되는 각 기본 주소에 엔드포인트를 추가하는 ServiceConfiguration.EnableProtocol(Binding)을 호출하여 엔드포인트를 자동으로 추가할 수 있습니다. 다음 코드에서는 ServiceConfiguration.EnableProtocol 메서드를 사용하는 방법을 보여 줍니다.  
  
```csharp  
public class Service1 : IService1   
{   
    public string GetData(int value);   
    public static void Configure(ServiceConfiguration config)   
    {   
        // Enable "Add Service Reference" support   
       config.Description.Behaviors.Add( new ServiceMetadataBehavior { HttpGetEnabled = true });   
       // set up support for http, https, net.tcp, net.pipe   
       config.EnableProtocol(new BasicHttpBinding());   
       config.EnableProtocol(new BasicHttpBinding());   
       config.EnableProtocol(new NetTcpBinding());   
       config.EnableProtocol(new NetNamedPipeBinding());   
       // add an extra BasicHttpBinding endpoint at http:///basic   
       config.AddServiceEndpoint(typeof(IService1), new BasicHttpBinding(),"basic");   
    }   
}   
```  
  
 <`protocolMappings`> 섹션의 설정은 <xref:System.ServiceModel.ServiceConfiguration> 프로그래밍 방식으로에 응용 프로그램 끝점을 추가 하지 않은 경우에만 사용 됩니다. 필요에 따라를 호출 <xref:System.ServiceModel.ServiceConfiguration.LoadFromConfiguration%2A> 하 여 기본 응용 프로그램 구성 파일에서 서비스 구성을 로드 한 다음 설정을 변경할 수 있습니다. <xref:System.ServiceModel.ServiceConfiguration.LoadFromConfiguration> 클래스를 사용하면 중앙 집중식 구성에서 구성을 로드할 수도 있습니다. 다음 코드에서는 이를 구현하는 방법을 보여 줍니다.  
  
```csharp
public class Service1 : IService1   
{   
    public void DoWork();   
    public static void Configure(ServiceConfiguration config)   
    {   
          config.LoadFromConfiguration(ConfigurationManager.OpenMappedExeConfiguration(new ExeConfigurationFileMap { ExeConfigFilename = @"c:\sharedConfig\MyConfig.config" }, ConfigurationUserLevel.None));   
    }   
}  
```  
  
> [!IMPORTANT]
> 는 <xref:System.ServiceModel.ServiceConfiguration.LoadFromConfiguration%2A> <`host``service`>의 < > 태그 내에서 < > 설정을 무시 합니다.`system.serviceModel` 개념적으로 <`host`>는 서비스 구성이 아니라 호스트 구성에 대 한 것 이며, 구성 메서드가 실행 되기 전에 로드 됩니다.  
  
## <a name="see-also"></a>참고자료

- [구성 파일을 사용하여 서비스 구성](../../../docs/framework/wcf/configuring-services-using-configuration-files.md)
- [클라이언트 동작 구성](../../../docs/framework/wcf/configuring-client-behaviors.md)
- [단순화된 구성](../../../docs/framework/wcf/simplified-configuration.md)
- [구성](../../../docs/framework/wcf/samples/configuration-sample.md)
- [IIS 및 WAS에서 구성 기반 활성화](../../../docs/framework/wcf/feature-details/configuration-based-activation-in-iis-and-was.md)
- [구성 및 메타데이터 지원](../../../docs/framework/wcf/extending/configuration-and-metadata-support.md)
- [구성](../../../docs/framework/wcf/diagnostics/exceptions-reference/configuration.md)
- [방법: 구성에서 서비스 바인딩 지정](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)
- [방법: 구성에서 서비스 끝점 만들기](../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md)
- [방법: 구성 파일을 사용 하 여 서비스에 대 한 메타 데이터 게시](../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)
- [방법: 구성에서 클라이언트 바인딩 지정](../../../docs/framework/wcf/how-to-specify-a-client-binding-in-configuration.md)
