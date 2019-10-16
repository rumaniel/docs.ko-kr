---
title: Send 활동의 캐시 공유 수준 변경
ms.date: 03/30/2017
ms.assetid: 03926a64-753d-460e-ac06-2a4ff8e1bbf5
ms.openlocfilehash: 587440bd343513aeff51f1ed0947573fbe612f22
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69952585"
---
# <a name="changing-the-cache-sharing-levels-for-send-activities"></a>Send 활동의 캐시 공유 수준 변경
<xref:System.ServiceModel.Activities.SendMessageChannelCache> 확장을 사용하면 <xref:System.ServiceModel.Activities.Send> 메시징 활동을 사용하여 서비스 엔드포인트로 메시지를 전송하는 워크플로에 대한 채널 캐시 설정, 채널 팩터리 캐시 설정 및 캐시 공유 수준을 사용자 지정할 수 있습니다. 이러한 워크플로는 일반적으로 클라이언트 워크플로이지만 <xref:System.ServiceModel.WorkflowServiceHost>에서 호스팅되는 워크플로 서비스일 수도 있습니다. 채널 팩터리 캐시는 캐시된 <xref:System.ServiceModel.ChannelFactory%601> 개체를 포함하고, 채널 캐시는 캐시된 채널을 포함합니다.  
  
> [!NOTE]
> 워크플로에서 <xref:System.ServiceModel.Activities.Send> 메시징 활동을 사용하여 메시지 또는 매개 변수를 보낼 수 있습니다. 워크플로 런타임에서는 <xref:System.ServiceModel.Channels.IRequestChannel> 활동을 <xref:System.ServiceModel.Activities.ReceiveReply> 활동과 함께 사용할 경우 <xref:System.ServiceModel.Activities.Send> 형식 채널을 만드는 캐시에 채널 팩터리를 추가하고, <xref:System.ServiceModel.Channels.IOutputChannel> 없이 <xref:System.ServiceModel.Activities.Send> 활동만 사용할 경우 <xref:System.ServiceModel.Activities.ReceiveReply> 형식 채널을 만드는 캐시에 채널 팩터리를 추가합니다.  
  
## <a name="the-cache-sharing-levels"></a>캐시 공유 수준  
 기본적으로 <xref:System.ServiceModel.WorkflowServiceHost>에서 호스팅되는 워크플로에서 <xref:System.ServiceModel.Activities.Send> 메시징 활동에 사용되는 캐시는 <xref:System.ServiceModel.WorkflowServiceHost>의 모든 워크플로 인스턴스에서 공유됩니다(호스트 수준 캐싱). <xref:System.ServiceModel.WorkflowServiceHost>에서 호스팅되지 않는 클라이언트 워크플로의 경우 워크플로 인스턴스에서만 캐시를 사용할 수 있습니다(인스턴스 수준 캐싱). 안전하지 않은 캐싱을 사용하지 않는 경우 구성에 정의된 엔드포인트를 사용하지 않는 <xref:System.ServiceModel.Activities.Send> 활동에 대해서만 캐시를 사용할 수 있습니다.  
  
 워크플로의 <xref:System.ServiceModel.Activities.Send> 활동에 대해 사용할 수 있는 다양한 캐시 공유 수준과 권장 사용법은 다음과 같습니다.  
  
- **호스트 수준**: 호스트 공유 수준에서는 워크플로 서비스 호스트에서 호스팅되는 워크플로 인스턴스에서만 캐시를 사용할 수 있습니다. 또한 프로세스 수준 캐시에서 워크플로 서비스 호스트 간에 캐시를 공유할 수 있습니다.  
  
- **인스턴스 수준**: 인스턴스 공유 수준에서는 특정 워크플로 인스턴스에서 해당 수명 동안 캐시를 사용할 수 있지만 다른 워크플로 인스턴스에서는 캐시를 사용할 수 없습니다.  
  
- **캐시 없음**: 구성에 정의 된 끝점을 사용 하는 워크플로가 있는 경우 기본적으로 캐시가 해제 됩니다. 또한 이 경우 캐시를 설정하면 안전하지 않으므로 캐시를 해제된 상태로 두는 것이 좋습니다. 예를 들어 전송할 때마다 다른 ID(다른 자격 증명 또는 가장 사용)가 필요한 경우가 있습니다.  
  
## <a name="changing-the-cache-sharing-level-for-a-client-workflow"></a>클라이언트 워크플로에 대한 캐시 공유 수준 변경  
 클라이언트 워크플로의 캐시 공유를 설정하려면 <xref:System.ServiceModel.Activities.SendMessageChannelCache> 클래스의 인스턴스를 원하는 워크플로 인스턴스 집합에 확장으로 추가합니다. 그러면 모든 워크플로 인스턴스에서 캐시를 공유하게 됩니다. 다음 코드 예제에서는 이러한 단계를 수행하는 방법을 보여 줍니다.  
  
 먼저 <xref:System.ServiceModel.Activities.SendMessageChannelCache> 형식의 인스턴스를 선언합니다.  
  
```csharp  
// Create an instance of SendMessageChannelCache with default cache settings.  
static SendMessageChannelCache sharedChannelCacheExtension =  
    new SendMessageChannelCache();  
```  
  
 다음은 각 클라이언트 워크플로 인스턴스에 캐시 확장을 추가합니다.  
  
```csharp 
WorkflowApplication clientInstance1 = new WorkflowApplication(new clientWorkflow1());  
WorkflowApplication clientInstance2 = new WorkflowApplication(new clientWorkflow2());  
  
// Share the cache extension object   
  
clientInstance1.Extensions.Add(sharedChannelCacheExtension);  
clientInstance2.Extensions.Add(sharedChannelCacheExtension);  
```  
  
## <a name="changing-the-cache-sharing-level-for-a-hosted-workflow-service"></a>호스팅된 워크플로 서비스에 대한 캐시 공유 수준 변경  
 호스팅된 워크플로 서비스의 캐시 공유를 설정하려면 <xref:System.ServiceModel.Activities.SendMessageChannelCache> 클래스의 인스턴스를 모든 워크플로 서비스 호스트에 확장으로 추가합니다. 그러면 모든 워크플로 서비스 호스트에서 캐시를 공유하게 됩니다. 다음 코드 예제에서는 이러한 단계를 수행하는 방법을 보여 줍니다.  
  
 먼저 클래스 수준에서 <xref:System.ServiceModel.Activities.SendMessageChannelCache> 형식 인스턴스를 선언합니다.  
  
```csharp  
// Create static instance of SendMessageChannelCache with default cache settings.  
static SendMessageChannelCache sharedChannelCacheExtension = new  
    SendMessageChannelCache();  
```  
  
 다음은 각 워크플로 서비스 호스트에 정적 캐시 확장을 추가합니다.  
  
```csharp  
WorkflowServiceHost host1 = new WorkflowServiceHost(new serviceWorkflow1(), new Uri(baseAddress1));  
WorkflowServiceHost host2 = new WorkflowServiceHost(new serviceWorkflow2(), new Uri(baseAddress2));  
  
// Share the static cache to get an AppDomain level cache.  
host1.WorkflowExtensions.Add(sharedChannelCacheExtension);  
host2.WorkflowExtensions.Add(sharedChannelCacheExtension);  
```  
  
 호스팅된 워크플로 서비스의 캐시 공유를 인스턴스 수준으로 설정하려면 `Func<SendMessageChannelCache>` 대리자를 워크플로 서비스 호스트에 확장으로 추가한 다음 <xref:System.ServiceModel.Activities.SendMessageChannelCache> 클래스의 새 인스턴스를 인스턴스화하는 코드에 이 대리자를 할당합니다. 그러면 워크플로 서비스 호스트의 모든 워크플로 인스턴스에서 단일 캐시를 공유하는 대신 개별 워크플로 인스턴스마다 다른 캐시가 생성됩니다. 다음 코드 예제에서는 람다 식을 사용하여 대리자가 가리키는 <xref:System.ServiceModel.Activities.SendMessageChannelCache> 확장을 직접 정의함으로써 이 작업을 수행하는 방법을 보여 줍니다.  
  
```csharp 
serviceHost.WorkflowExtensions.Add(() => new SendMessageChannelCache  
{  
    // Use FactorySettings property to add custom factory cache settings.  
    FactorySettings = new ChannelCacheSettings   
    { MaxItemsInCache = 5, },  
    // Use ChannelSettings property to add custom channel cache settings.  
    ChannelSettings = new ChannelCacheSettings   
    { MaxItemsInCache = 10 },  
});  
```  
  
## <a name="customizing-cache-settings"></a>캐시 설정 사용자 지정  
 채널 팩터리 캐시 및 채널 캐시에 대한 캐시 설정을 사용자 지정할 수 있습니다. 캐시 설정은 <xref:System.ServiceModel.Activities.ChannelCacheSettings> 클래스에서 정의됩니다. 클래스 <xref:System.ServiceModel.Activities.SendMessageChannelCache> 는 매개 변수가 없는 생성자의 채널 팩터리 캐시 및 채널 캐시에 대 한 기본 캐시 설정을 정의 합니다. 다음 표에서는 각 캐시 유형에 대한 이러한 캐시 설정의 기본값을 보여 줍니다.  
  
|설정|LeaseTimeout(분)|IdleTimeout(분)|MaxItemsInCache|  
|-|-|-|-|  
|팩터리 캐시 기본값|TimeSpan.MaxValue|2|16|  
|채널 캐시 기본값|5|2|16|  
  
 팩터리 캐시 및 채널 캐시 설정을 사용자 지정하려면 매개 변수가 있는 생성자 <xref:System.ServiceModel.Activities.SendMessageChannelCache>을 사용하여 <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> 클래스를 인스턴스화하고 <xref:System.ServiceModel.Activities.ChannelCacheSettings>의 새 인스턴스를 사용자 지정 값과 함께 각 `factorySettings` 및 `channelSettings` 매개 변수에 전달합니다. 다음에는 이 클래스의 새 인스턴스를 워크플로 서비스 호스트 또는 워크플로 인스턴스에 확장으로 추가합니다. 다음 코드 예제에서는 워크플로 인스턴스에 대해 이러한 단계를 수행하는 방법을 보여 줍니다.  
  
```csharp  
ChannelCacheSettings factorySettings = new ChannelCacheSettings{  
                        MaxItemsInCache = 5,   
                        IdleTimeout = TimeSpan.FromMinutes(5),   
                        LeaseTimeout = TimeSpan.FromMinutes(20)};  
  
ChannelCacheSettings channelSettings = new ChannelCacheSettings{  
                        MaxItemsInCache = 5,   
                        IdleTimeout = TimeSpan.FromMinutes(2),  
                        LeaseTimeout = TimeSpan.FromMinutes(10) };  
  
SendMessageChannelCache customChannelCacheExtension =   
    new SendMessageChannelCache(factorySettings, channelSettings);  
  
clientInstance.Extensions.Add(customChannelCacheExtension);  
```  
  
 워크플로 서비스의 구성에 엔드포인트가 정의되어 있을 때 캐싱을 사용하려면 <xref:System.ServiceModel.Activities.SendMessageChannelCache> 매개 변수를 <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A>로 설정한 상태에서 매개 변수가 있는 생성자 `allowUnsafeCaching`을 사용하여 `true` 클래스를 인스턴스화합니다. 다음에는 이 클래스의 새 인스턴스를 워크플로 서비스 호스트 또는 워크플로 인스턴스에 확장으로 추가합니다. 다음 코드 예제에서는 워크플로 인스턴스에 대해 캐싱을 사용하도록 설정하는 방법을 보여 줍니다.  
  
```csharp  
SendMessageChannelCache customChannelCacheExtension =   
    new SendMessageChannelCache{ AllowUnsafeCaching = true };  
  
clientInstance.Extensions.Add(customChannelCacheExtension);  
```  
  
 채널 팩터리 및 채널에 대해 캐시를 완전히 비활성화하려면 채널 팩터리 캐시를 사용하지 않도록 설정합니다. 해당 채널 팩터리에서 채널을 소유하므로 캐시를 비활성화하면 채널 캐시도 해제됩니다. 채널 팩터리 캐시를 사용하지 않도록 설정하려면 `factorySettings` 값 0을 사용하여 <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> 인스턴스로 초기화되는 <xref:System.ServiceModel.Activities.ChannelCacheSettings> 생성자에 <xref:System.ServiceModel.Activities.ChannelCacheSettings.MaxItemsInCache%2A> 매개 변수를 전달합니다. 다음 코드 예제에서는 이를 보여 줍니다.  
  
```csharp  
// Disable the factory cache. This results in the channel cache to be turned off as well.  
ChannelCacheSettings factorySettings = new ChannelCacheSettings  
    { MaxItemsInCache = 0 };  
  
ChannelCacheSettings channelSettings = new ChannelCacheSettings();  
  
SendMessageChannelCache customChannelCacheExtension =   
    new SendMessageChannelCache(factorySettings, channelSettings);   
  
clientInstance.Extensions.Add(customChannelCacheExtension);  
```  
  
 채널 팩터리 캐시만 사용하고 채널 캐시는 사용하지 않도록 설정하려면 `channelSettings` 값 0을 사용하여 <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> 인스턴스로 초기화되는 <xref:System.ServiceModel.Activities.ChannelCacheSettings> 생성자에 <xref:System.ServiceModel.Activities.ChannelCacheSettings.MaxItemsInCache%2A> 매개 변수를 전달하면 됩니다. 다음 코드 예제에서는 이를 보여 줍니다.  
  
```csharp  
ChannelCacheSettings factorySettings = new ChannelCacheSettings();  
// Disable only the channel cache.  
ChannelCacheSettings channelSettings = new ChannelCacheSettings  
    { MaxItemsInCache = 0};  
  
SendMessageChannelCache customChannelCacheExtension =   
    new SendMessageChannelCache(factorySettings, channelSettings);   
  
clientInstance.Extensions.Add(customChannelCacheExtension);  
```  
  
 호스팅된 워크플로 서비스의 경우 애플리케이션 구성 파일에서 팩터리 캐시 및 채널 캐시 설정을 지정할 수 있습니다. 이렇게 하려면 팩터리 및 채널 캐시의 캐시 설정을 포함하는 서비스 동작을 추가하고 이 서비스 동작을 서비스에 추가합니다. 다음 예제에서는 사용자 지정 팩터리 캐시 및 채널 캐시 설정을 사용 하 `MyChannelCacheBehavior` 여 서비스 동작을 포함 하는 구성 파일의 내용을 보여 줍니다. 이 서비스 동작은 특성을 `behaviorConfiguration` 통해 서비스에 추가 됩니다.  
  
```xml  
<configuration>    
  <system.serviceModel>  
    <!-- List of other config sections here -->   
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="MyChannelCacheBehavior">  
          <sendMessageChannelCache allowUnsafeCaching ="false" >  
            <!-- Control only the host level settings -->   
            <factorySettings maxItemsInCache = "8" idleTimeout = "00:05:00" leaseTimeout="10:00:00" />  
            <channelSettings maxItemsInCache = "32" idleTimeout = "00:05:00" leaseTimeout="00:06:00" />  
          </sendMessageChannelCache>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <services>  
      <service name="MyService" behaviorConfiguration="MyChannelCacheBehavior" />  
    </services>  
  </system.serviceModel>  
</configuration>  
```
