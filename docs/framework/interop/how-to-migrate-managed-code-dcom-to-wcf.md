---
title: '방법: 관리 코드 DCOM을 WCF로 마이그레이션'
ms.date: 03/30/2017
ms.assetid: 52961ffc-d1c7-4f83-832c-786444b951ba
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 42edce63856b629511faeb165362da18ea3cecad
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833624"
---
# <a name="how-to-migrate-managed-code-dcom-to-wcf"></a>방법: 관리 코드 DCOM을 WCF로 마이그레이션
WCF(Windows Communication Foundation)는 분산 환경에서 서버와 클라이언트 간에 관리 코드 호출에 대해 DCOM(Distributed Component Object Model)보다 권장되는 안전한 선택 항목입니다. 이 문서에서는 다음과 같은 시나리오에 대해 코드를 DCOM에서 WCF로 마이그레이션하는 방법을 보여 줍니다.  
  
- 원격 서비스에서 값 방식으로 클라이언트에 개체를 반환합니다.  
  
- 클라이언트에서 값 방식으로 원격 서비스에 개체를 전송합니다.  
  
- 보안상 클라이언트에서 값 방식으로 서비스에 개체를 전송하는 기능은 WCF에서 허용되지 않습니다.  
  
 보안상 클라이언트에서 참조 방식으로 서비스에 개체를 전송하는 기능은 WCF에서 허용되지 않습니다. 클라이언트와 서버 간에 서로 대화하는 데 필요한 시나리오는 WCF에서 이중 서비스를 사용하여 수행할 수 있습니다.  이중 서비스에 대한 자세한 내용은 [이중 서비스](../wcf/feature-details/duplex-services.md)를 참조하세요.  
  
 WCF 서비스와 해당 서비스에 대한 클라이언트를 만드는 방법에 대한 자세한 내용은 [기본 WCF 프로그래밍](../wcf/basic-wcf-programming.md), [서비스 디자인 및 구현](../wcf/designing-and-implementing-services.md) 및 [클라이언트 빌드](../wcf/building-clients.md)를 참조하세요.  
  
## <a name="dcom-example-code"></a>DCOM 예제 코드  
 이러한 시나리오에서 WCF를 사용하여 설명한 DCOM 인터페이스의 구조는 다음과 같습니다.  
  
```csharp  
[ComVisible(true)]  
[Guid("AA9C4CDB-55EA-4413-90D2-843F1A49E6E6")]  
public interface IRemoteService  
{  
   Customer GetObjectByValue();  
   IRemoteObject GetObjectByReference();  
   void SendObjectByValue(Customer customer);  
}  
  
[ComVisible(true)]  
[Guid("A12C98DE-B6A1-463D-8C24-81E4BBC4351B")]  
public interface IRemoteObject  
{  
}  
  
public class Customer  
{  
}  
```  
  
## <a name="the-service-returns-an-object-by-value"></a>서비스에서 값 방식으로 개체 반환  
 이 시나리오에서는 서비스를 호출하고 해당 메서드가 개체를 반환한 다음 서버에서 값 방식으로 클라이언트에 전달됩니다. 이 시나리오는 다음과 같은 COM 호출을 나타냅니다.  
  
```csharp  
public interface IRemoteService  
{  
    Customer GetObjectByValue();  
}  
```  
  
 이 시나리오에서 클라이언트는 원격 서비스에서 개체의 역직렬화된 복사본을 받습니다. 클라이언트는 서비스를 콜백하지 않고 이 로컬 복사본과 상호 작용할 수 있습니다.  즉, 로컬 복사본에 대해 메서드를 호출할 때 서비스가 어떤 방식으로도 관련되지 않음을 클라이언트가 확신할 수 있습니다. WCF는 항상 값 방식으로 서비스에서 개체를 반환하므로, 다음 단계에서는 일반 WCF 서비스를 만드는 방법을 설명합니다.  
  
### <a name="step-1-define-the-wcf-service-interface"></a>1단계: WCF 서비스 인터페이스 정의  
 WCF 서비스에 대한 공용 인터페이스를 정의하고 [<xref:System.ServiceModel.ServiceContractAttribute>] 특성으로 표시합니다.  클라이언트에 노출하려는 메서드를 [<xref:System.ServiceModel.OperationContractAttribute>] 특성으로 표시합니다. 다음 예제에서는 이러한 특성을 사용하여 클라이언트가 호출할 수 있는 서버 쪽 인터페이스 및 인터페이스 메서드를 식별하는 방법을 보여 줍니다. 이 시나리오에 사용되는 메서드는 굵게 표시됩니다.  
  
```csharp  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Web;   
. . .  
[ServiceContract]  
public interface ICustomerManager  
{  
    [OperationContract]  
    void StoreCustomer(Customer customer);  
  
    [OperationContract]     Customer GetCustomer(string firstName, string lastName);   
  
}  
```  
  
### <a name="step-2-define-the-data-contract"></a>2단계: 데이터 계약 정의  
 다음에는 서비스와 해당 클라이언트 간에 데이터를 교환하는 방법을 설명하는 서비스에 대한 데이터 계약을 만들어야 합니다.  데이터 계약에 설명된 클래스는 [<xref:System.Runtime.Serialization.DataContractAttribute>] 특성으로 표시해야 합니다. 클라이언트와 서버 둘 다에 표시할 개별 속성 또는 필드는 [<xref:System.Runtime.Serialization.DataMemberAttribute>] 특성으로 표시되어야 합니다. 데이터 계약의 클래스에서 파생된 형식을 허용하려면 [<xref:System.Runtime.Serialization.KnownTypeAttribute>] 특성을 사용하여 식별해야 합니다. WCF는 서비스 인터페이스의 형식 및 알려진 형식으로 식별된 형식만 직렬화하거나 역직렬화합니다. 알려진 형식이 아닌 형식을 사용하려고 하면 예외가 발생합니다.  
  
 데이터 계약에 대한 자세한 내용은 [데이터 계약](../wcf/samples/data-contracts.md)을 참조하세요.  
  
```csharp  
[DataContract]  
[KnownType(typeof(PremiumCustomer))]  
public class Customer  
{  
    [DataMember]  
    public string Firstname;  
    [DataMember]  
    public string Lastname;  
    [DataMember]  
    public Address DefaultDeliveryAddress;  
    [DataMember]  
    public Address DefaultBillingAddress;  
}  
 [DataContract]  
public class PremiumCustomer : Customer  
{  
    [DataMember]  
    public int AccountID;  
}  
  
 [DataContract]  
public class Address  
{  
    [DataMember]  
    public string Street;  
    [DataMember]  
    public string Zipcode;  
    [DataMember]  
    public string City;  
    [DataMember]  
    public string State;  
    [DataMember]  
    public string Country;  
}  
```  
  
### <a name="step-3-implement-the-wcf-service"></a>3단계: WCF 서비스 구현  
 다음에는 이전 단계에서 정의한 인터페이스를 구현하는 WCF 서비스 클래스를 구현해야 합니다.  
  
```csharp  
public class CustomerService: ICustomerManager    
{  
    public void StoreCustomer(Customer customer)  
    {  
        // write to a database  
    }  
    public Customer GetCustomer(string firstName, string lastName)  
    {  
        // read from a database  
    }  
}  
```  
  
### <a name="step-4-configure-the-service-and-the-client"></a>4단계: 서비스 및 클라이언트 구성  
 WCF 서비스를 실행하려면 특정 WCF 바인딩을 사용하여 특정 URL에 해당 서비스 인터페이스를 노출하는 엔드포인트를 선언해야 합니다. 바인딩은 클라이언트와 서버가 통신하는 데 필요한 전송, 인코딩 및 프로토콜 세부 정보를 지정합니다. 일반적으로 서비스 프로젝트의 구성 파일(web.config)에 바인딩을 추가합니다. 다음은 예제 서비스에 대한 바인딩 항목을 보여 줍니다.  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service name="Server.CustomerService">  
        <endpoint address="http://localhost:8083/CustomerManager"   
                  binding="basicHttpBinding"  
                  contract="Shared.ICustomerManager" />  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
```  
  
 다음에는 서비스에서 지정된 바인딩 정보와 일치하도록 클라이언트를 구성해야 합니다. 이렇게 하려면 클라이언트의 애플리케이션 구성 파일(app.config)에 다음을 추가합니다.  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <client>  
      <endpoint name="customermanager"   
                address="http://localhost:8083/CustomerManager"   
                binding="basicHttpBinding"   
                contract="Shared.ICustomerManager"/>  
  </system.serviceModel>  
</configuration>  
```  
  
### <a name="step-5-run-the-service"></a>5단계: 서비스 실행  
 끝으로, 서비스 앱에 다음 줄을 추가하고 앱을 시작하여 콘솔 애플리케이션에서 자체 호스트할 수 있습니다. WCF 서비스 애플리케이션을 호스트하는 다른 방법에 대한 자세한 내용은 [호스팅 서비스](../wcf/hosting-services.md)를 참조하세요.  
  
```csharp  
ServiceHost customerServiceHost = new ServiceHost(typeof(CustomerService));  
customerServiceHost.Open();  
```  
  
### <a name="step-6-call-the-service-from-the-client"></a>6단계: 클라이언트에서 서비스 호출  
 클라이언트에서 서비스를 호출하려면 서비스에 대한 채널 팩터리를 만들고 채널을 요청해야 합니다. 그러면 클라이언트에서 직접 `GetCustomer` 메서드를 호출할 수 있습니다. 채널은 서비스의 인터페이스를 구현하고 내부 요청/응답 논리를 자동으로 처리합니다.  해당 메서드 호출의 반환 값은 역직렬화된 서비스 응답 복사본입니다.  
  
```csharp  
ChannelFactory<ICustomerManager> factory =   
     new ChannelFactory<ICustomerManager>("customermanager");  
ICustomerManager service = factory.CreateChannel();  
Customer customer = service.GetCustomer("Mary", "Smith");  
```  
  
## <a name="the-client-sends-a-by-value-object-to-the-server"></a>클라이언트에서 값 방식으로 서버에 개체 전송  
 이 시나리오에서는 클라이언트가 값 방식으로 서버에 개체를 전송합니다. 즉, 서버가 개체의 역직렬화된 복사본을 받게 됩니다.  서버는 해당 복사본에 대해 메서드를 호출할 수 있으며 클라이언트 코드에 대한 콜백이 없음을 확신할 수 있습니다. 앞에서 설명한 것처럼 데이터의 일반 WCF 교환은 값 방식입니다.  이 경우 이러한 개체 중 하나에 대해 메서드를 호출하면 로컬에서만 실행되며 클라이언트에서 코드를 호출하지 않습니다.  
  
 이 시나리오는 다음과 같은 COM 메서드 호출을 나타냅니다.  
  
```csharp  
public interface IRemoteService  
{  
    void SendObjectByValue(Customer customer);  
}  
```  
  
 이 시나리오에서는 첫 번째 예제에 표시된 것과 동일한 서비스 인터페이스 및 데이터 계약을 사용합니다. 또한 클라이언트와 서비스가 동일한 방식으로 구성됩니다. 이 예제에서는 동일한 방식으로 개체를 전송 및 실행하기 위해 채널을 만듭니다. 그러나 이 예제의 경우 값 방식으로 개체를 전달하여 서비스를 호출하는 클라이언트를 만듭니다. 클라이언트가 서비스 계약에서 호출하는 서비스 메서드는 굵게 표시됩니다.  
  
```csharp  
[ServiceContract]  
public interface ICustomerManager  
{  
    [OperationContract]     void StoreCustomer(Customer customer);  
  
    [OperationContract]  
    Customer GetCustomer(string firstName, string lastName);  
}  
```  
  
### <a name="add-code-to-the-client-that-sends-a-by-value-object"></a>클라이언트에 값 방식으로 개체를 전송하는 코드 추가  
 다음 코드에서는 클라이언트가 새로운 값 방식 customer 개체를 만들고, `ICustomerManager` 서비스와 통신하는 채널을 만든 다음 customer 개체를 전송하는 방법을 보여 줍니다.  
  
 customer 개체가 직렬화되어 서비스로 전송되며, 서비스에서 해당 개체의 새 복사본으로 역직렬화됩니다.  이 개체에 대한 서비스를 호출하는 모든 메서드는 서버에서 로컬로만 실행됩니다. 이 코드는 파생된 형식(`PremiumCustomer`)을 보내는 것을 보여줍니다.  서비스 계약에는 `Customer` 개체가 필요하지만 서비스 데이터 계약에서 [<xref:System.Runtime.Serialization.KnownTypeAttribute>] 특성을 사용하여 `PremiumCustomer`도 허용됨을 나타냅니다.  WCF에서 이 서비스 인터페이스를 통해 다른 형식을 직렬화하거나 deserialization하려고 하면 실패합니다.  
  
```csharp  
PremiumCustomer customer = new PremiumCustomer();  
customer.Firstname = "John";  
customer.Lastname = "Doe";  
customer.DefaultBillingAddress = new Address();  
customer.DefaultBillingAddress.Street = "One Microsoft Way";  
customer.DefaultDeliveryAddress = customer.DefaultBillingAddress;  
customer.AccountID = 42;  
  
ChannelFactory<ICustomerManager> factory =  
   new ChannelFactory<ICustomerManager>("customermanager");  
ICustomerManager customerManager = factory.CreateChannel();  
customerManager.StoreCustomer(customer);  
```  
  
## <a name="the-service-returns-an-object-by-reference"></a>서비스에서 참조 방식으로 개체 반환  
 이 시나리오에서는 클라이언트 앱이 원격 서비스를 호출하고 해당 메서드가 개체를 반환한 다음 서비스에서 참조 방식으로 클라이언트에 전달됩니다.  
  
 앞에서 설명한 것처럼 WCF 서비스는 항상 값 방식으로 개체를 반환합니다.  그러나 <xref:System.ServiceModel.EndpointAddress10> 클래스를 사용하여 비슷한 결과를 얻을 수 있습니다.  <xref:System.ServiceModel.EndpointAddress10>은 서버에서 세션 참조 방식 개체를 가져오기 위해 클라이언트가 사용할 수 있는 직렬화 가능 값 방식 개체입니다.  
  
 이 시나리오에 표시된 WCF의 참조 방식 개체 동작은 DCOM과 다릅니다.  DCOM에서는 서버가 참조 방식 개체를 클라이언트에 직접 반환할 수 있으며, 클라이언트가 서버에서 실행되는 해당 개체의 메서드를 호출할 수 있습니다.  그러나 WCF에서는 반환된 개체가 항상 값 방식입니다.  클라이언트는 <xref:System.ServiceModel.EndpointAddress10>으로 표시된 해당 값 방식 개체를 사용하여 고유한 세션 참조 방식 개체를 만들어야 합니다.  세션 개체에 대한 클라이언트 메서드 호출은 서버에서 실행됩니다. 즉, WCF의 이 참조 방식 개체는 세션으로 구성된 일반 WCF 서비스입니다.  
  
 WCF에서 세션은 두 엔드포인트 간에 전송된 여러 메시지를 서로 관련시키는 방법입니다.  즉, 클라이언트가 이 서비스에 대한 연결을 확보하고 나면 클라이언트와 서버 간에 세션이 설정됩니다.  클라이언트는 이 단일 세션 내에서 수행되는 모든 상호 작용을 수행하는 데 하나의 고유한 서버 쪽 개체 인스턴스를 사용합니다. 세션 WCF 계약은 연결 지향 네트워크 요청/응답 패턴과 비슷합니다.  
  
 이 시나리오는 다음과 같은 DCOM 메서드로 나타냅니다.  
  
```csharp  
public interface IRemoteService  
{  
    IRemoteObject GetObjectByReference();  
}  
```  
  
### <a name="step-1-define-the-sessionful-wcf-service-interface-and-implementation"></a>1단계: 세션 WCF 서비스 인터페이스와 구현 정의  
 먼저 세션 개체를 포함하는 WCF 서비스 인터페이스를 정의합니다.  
  
 이 코드에서 세션 개체는 `ServiceContract` 특성으로 표시됩니다.이 경우 개체는 일반 WCF 서비스 인터페이스로 식별됩니다.  또한 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A> 속성이 세션 서비스를 나타내도록 설정됩니다.  
  
```csharp  
[ServiceContract(SessionMode = SessionMode.Allowed)]  
public interface ISessionBoundObject  
{  
    [OperationContract]  
    string GetCurrentValue();  
  
    [OperationContract]  
    void SetCurrentValue(string value);  
}  
```  
  
 다음 코드에서는 서비스 구현을 보여 줍니다.  
  
 서비스가 [ServiceBehavior] 특성으로 표시되고 해당 InstanceContextMode 속성이 InstanceContextMode.PerSessions로 설정되어 각 세션에 대해 이 형식의 고유 인스턴스를 만들어야 함을 나타냅니다.  
  
```csharp  
[ServiceBehavior(InstanceContextMode = InstanceContextMode.PerSession)]  
    public class MySessionBoundObject : ISessionBoundObject  
    {  
        private string _value;  
  
        public string GetCurrentValue()  
        {  
            return _value;  
        }  
  
        public void SetCurrentValue(string val)  
        {  
            _value = val;  
        }  
  
    }  
```  
  
### <a name="step-2-define-the-wcf-factory-service-for-the-sessionful-object"></a>2단계: 세션 개체에 대한 WCF 팩터리 서비스 정의  
 세션 개체를 만드는 서비스를 정의 및 구현해야 합니다. 다음 코드에서는 이 작업을 수행하는 방법을 보여 줍니다. 이 코드에서는 <xref:System.ServiceModel.EndpointAddress10> 개체를 반환하는 다른 WCF 서비스를 만듭니다.  이는 세션 개체를 만드는 데 사용할 수 있는 직렬화 가능한 형식의 엔드포인트입니다.  
  
```csharp  
[ServiceContract]  
    public interface ISessionBoundFactory  
    {  
        [OperationContract]  
        EndpointAddress10 GetInstanceAddress();  
    }  
```  
  
 다음은이 서비스의 구현입니다. 이 구현에서는 세션 개체를 만들기 위해 단일 채널 팩터리를 유지 관리합니다.  `GetInstanceAddress`를 호출하면 채널을 만들고 이 채널과 연결된 원격 주소를 가리키는 <xref:System.ServiceModel.EndpointAddress10> 개체를 만듭니다.   <xref:System.ServiceModel.EndpointAddress10>은 값 방식으로 클라이언트에 반환될 수 있는 데이터 형식입니다.
  
```csharp  
public class SessionBoundFactory : ISessionBoundFactory  
    {  
        public static ChannelFactory<ISessionBoundObject> _factory =   
            new ChannelFactory<ISessionBoundObject>("sessionbound");  
  
        public SessionBoundFactory()  
        {  
        }  
  
        public EndpointAddress10 GetInstanceAddress()  
        {  
            IClientChannel channel = (IClientChannel)_factory.CreateChannel();  
            return EndpointAddress10.FromEndpointAddress(channel.RemoteAddress);  
        }  
    }  
```  
  
### <a name="step-3-configure-and-start-the-wcf-services"></a>3단계: WCF 서비스 구성 및 시작  
 이러한 서비스를 호스트하려면 서버의 구성 파일(web.config)에 다음 내용을 추가해야 합니다.  
  
1. 세션 개체의 엔드포인트를 설명하는 `<client>` 섹션을 추가합니다.  이 시나리오에서는 서버가 클라이언트 역할도 하며 이 기능을 사용할 수 있도록 구성해야 합니다.  
  
2. `<services>` 섹션에서 팩터리와 세션 개체의 서비스 엔드포인트를 선언합니다.  그러면 클라이언트가 서비스 엔드포인트와 통신하고 <xref:System.ServiceModel.EndpointAddress10>을 확보한 다음 세션 채널을 만들 수 있습니다.  
  
 다음은 이러한 설정을 사용 하는 구성 파일의 예입니다.  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <client>  
      <endpoint name="sessionbound"  
                address="net.tcp://localhost:8081/SessionBoundObject"  
                binding="netTcpBinding"  
                contract="Shared.ISessionBoundObject"/>  
    </client>  
  
    <services>  
      <service name="Server.MySessionBoundObject">  
        <endpoint address="net.tcp://localhost:8081/SessionBoundObject"  
                  binding="netTcpBinding"   
                  contract="Shared.ISessionBoundObject" />  
      </service>  
      <service name="Server.SessionBoundFactory">  
        <endpoint address="net.tcp://localhost:8081/SessionBoundFactory"  
                  binding="netTcpBinding"   
                  contract="Shared.ISessionBoundFactory" />  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
```  
  
 서비스를 자체 호스트하고 앱을 시작하려면 콘솔 애플리케이션에 다음 줄을 추가합니다.  
  
```csharp  
ServiceHost factoryHost = new ServiceHost(typeof(SessionBoundFactory));  
factoryHost.Open();  
  
ServiceHost sessionBoundServiceHost = new ServiceHost(  
typeof(MySessionBoundObject));  
sessionBoundServiceHost.Open();  
```  
  
### <a name="step-4-configure-the-client-and-call-the-service"></a>4단계: 클라이언트 구성 및 서비스 호출  
 프로젝트의 애플리케이션 구성 파일(app.config)에 다음 항목을 만들어 WCF 서비스와 통신하도록 클라이언트를 구성합니다.  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <client>  
      <endpoint name="sessionbound"   
                address="net.tcp://localhost:8081/SessionBoundObject"   
                binding="netTcpBinding"   
                contract="Shared.ISessionBoundObject"/>  
      <endpoint name="factory"   
                address="net.tcp://localhost:8081/SessionBoundFactory"   
                binding="netTcpBinding"   
                contract="Shared.ISessionBoundFactory"/>  
    </client>    
  </system.serviceModel>  
</configuration>  
```  
  
 서비스를 호출하려면 다음을 수행하는 코드를 클라이언트에 추가합니다.  
  
1. `ISessionBoundFactory` 서비스에 대한 채널을 만듭니다.  
  
2. 채널을 사용하여 `ISessionBoundFactory` 서비스를 호출하고 <xref:System.ServiceModel.EndpointAddress10> 개체를 가져옵니다.  
  
3. <xref:System.ServiceModel.EndpointAddress10>을 사용하여 세션 개체를 가져올 채널을 만듭니다.  
  
4. `SetCurrentValue` 및 `GetCurrentValue` 메서드를 호출하여 여러 호출에서 동일한 개체 인스턴스가 사용됨을 보여 줍니다.  
  
```csharp  
ChannelFactory<ISessionBoundFactory> factory =  
        new ChannelFactory<ISessionBoundFactory>("factory");  
  
ISessionBoundFactory sessionBoundFactory = factory.CreateChannel();  
  
EndpointAddress10 address = sessionBoundFactory.GetInstanceAddress();  
  
ChannelFactory<ISessionBoundObject> sessionBoundObjectFactory =  
    new ChannelFactory<ISessionBoundObject>(  
        new NetTcpBinding(),  
        address.ToEndpointAddress());  
  
ISessionBoundObject sessionBoundObject =  
        sessionBoundObjectFactory.CreateChannel();  
  
sessionBoundObject.SetCurrentValue("Hello");  
if (sessionBoundObject.GetCurrentValue() == "Hello")  
{  
    Console.WriteLine("Session-full instance management works as expected");  
}  
```  
  
## <a name="see-also"></a>참조

- [기본 WCF 프로그래밍](../wcf/basic-wcf-programming.md)
- [서비스 디자인 및 구현](../wcf/designing-and-implementing-services.md)
- [클라이언트 빌드](../wcf/building-clients.md)
- [이중 서비스](../wcf/feature-details/duplex-services.md)
