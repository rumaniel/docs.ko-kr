---
title: 사용자 지정 메시지 인터셉터
ms.date: 03/30/2017
ms.assetid: 73f20972-53f8-475a-8bfe-c133bfa225b0
ms.openlocfilehash: daa041bf63442dace0d33e1e3207d0857b6b7312
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928913"
---
# <a name="custom-message-interceptor"></a>사용자 지정 메시지 인터셉터
이 샘플에서는 채널 확장성 모델의 사용 방법을 보여 줍니다. 특히 채널 팩터리 및 채널 수신기를 만드는 사용자 지정 바인딩 요소를 구현하여 런타임 스택의 특정 지점에서 들어오고 보내는 모든 메시지를 가로채는 방법을 보여 줍니다. 또한 이 샘플에는 이 사용자 지정 팩터리의 사용을 보여 주는 클라이언트와 서버도 포함되어 있습니다.  
  
 이 샘플에서는 클라이언트와 서비스 모두가 콘솔 프로그램(.exe)입니다. 클라이언트와 서비스 모두 사용자 지정 바인딩 요소 및 관련 런타임 개체를 포함하는 공용 라이브러리(.dll)를 사용합니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Channels\MessageInterceptor`  
  
 이 샘플에서는 채널 프레임 워크 및 WCF 모범 사례를 사용 하 여 WCF (Windows Communication Foundation)에서 사용자 지정 계층화 된 채널을 만드는 권장 절차에 대해 설명 합니다. 사용자 지정 계층화된 채널을 만드는 단계는 다음과 같습니다.  
  
1. 채널 팩터리 및 채널 수신기에서 지원할 채널 셰이프를 결정합니다.  
  
2. 채널 셰이프를 지원하는 채널 팩터리 및 채널 수신기를 만듭니다.  
  
3. 사용자 지정 계층화된 채널을 채널 스택에 추가하는 바인딩 요소를 추가합니다.  
  
4. 새 바인딩 요소가 구성 시스템에 노출되도록 바인딩 요소 확장명 섹션을 추가합니다.  
  
## <a name="channel-shapes"></a>채널 셰이프  
 사용자 지정 계층화된 채널을 작성하는 첫 번째 단계는 채널에 필요한 셰이프를 결정하는 것입니다. 메시지 검사자를 위해 아래의 계층이 지원하는 모든 셰이프를 지원합니다. 예를 들어, 아래의 계층이 <xref:System.ServiceModel.Channels.IOutputChannel> 및 <xref:System.ServiceModel.Channels.IDuplexSessionChannel>을 빌드할 수 있는 경우 <xref:System.ServiceModel.Channels.IOutputChannel> 및 <xref:System.ServiceModel.Channels.IDuplexSessionChannel>도 노출합니다.  
  
## <a name="channel-factory-and-listener-factory"></a>채널 팩터리 및 수신기 팩터리  
 사용자 지정 계층화된 채널을 작성하는 두 번째 단계는 클라이언트 채널을 위한 <xref:System.ServiceModel.Channels.IChannelFactory> 구현 및 서비스 채널을 위한 <xref:System.ServiceModel.Channels.IChannelListener> 구현을 만드는 것입니다.  
  
 이 클래스는 내부 팩터리 및 수신기를 받고 `OnCreateChannel` 및 `OnAcceptChannel` 호출을 제외한 모두를 내부 팩터리 및 수신기에 위임합니다.  
  
```csharp  
class InterceptingChannelFactory<TChannel> : ChannelFactoryBase<TChannel>  
{ 
    //... 
}

class InterceptingChannelListener<TChannel> : ListenerFactoryBase<TChannel>  
{ 
    //...
}  
```  
  
## <a name="adding-a-binding-element"></a>바인딩 요소 추가  
 이 샘플에서는 사용자 지정 바인딩 요소인 `InterceptingBindingElement`를 정의합니다. `InterceptingBindingElement`는를 `ChannelMessageInterceptor` 입력으로 사용 하 고이 `ChannelMessageInterceptor` 를 통해 전달 되는 메시지를 조작 합니다. 이는 public이어야 하는 유일한 클래스입니다. 팩터리, 수신기 및 채널 모두 public 런타임 인터페이스의 내부 구현이 될 수 있습니다.  
  
```csharp
public class InterceptingBindingElement : BindingElement 
{
}
```  
  
## <a name="adding-configuration-support"></a>구성 지원 추가  
 바인딩 구성과 통합하기 위해 라이브러리에서는 구성 섹션 처리기를 바인딩 요소 확장 섹션으로 정의합니다. 클라이언트 및 서버 구성 파일은 구성 시스템에 바인딩 요소 확장을 등록해야 합니다. 구성 시스템에 바인딩 요소를 노출하려는 구현자는 이 클래스에서 파생할 수 있습니다.  
  
```csharp
public abstract class InterceptingElement : BindingElementExtensionElement 
{ 
    //... 
}
```  
  
## <a name="adding-policy"></a>정책 추가  
 정책 시스템과 통합하기 위해 `InterceptingBindingElement`는 IPolicyExportExtension을 구현하여 정책 생성에 참여해야 함을 나타냅니다. 생성된 클라이언트에 정책을 가져오는 것을 지원하기 위해 사용자는 `InterceptingBindingElementImporter`의 파생 클래스를 등록하고 해당 정책을 사용하는 `CreateMessageInterceptor` 클래스를 생성하도록 `ChannelMessageInterceptor`()를 재정의할 수 있습니다.  
  
## <a name="example-droppable-message-inspector"></a>예제: Droppable 메시지 검사자  
 메시지를 삭제하는 `ChannelMessageInspector`의 구현 예제가 샘플에 포함되어 있습니다.  
  
```csharp  
class DroppingServerElement : InterceptingElement  
{  
    protected override ChannelMessageInterceptor CreateMessageInterceptor()  
    {  
        return new DroppingServerInterceptor();  
    }  
}  
```  
  
 다음과 같이 구성에서 이 예제에 액세스할 수 있습니다.  
  
```xml  
<configuration>  
    ...  
    <system.serviceModel>  
        ...  
        <extensions>  
            <bindingElementExtensions>  
                <add name="droppingInterceptor"   
                   type=  
          "Microsoft.ServiceModel.Samples.DroppingServerElement, library"/>  
            </bindingElementExtensions>  
        </extensions>  
    </system.serviceModel>  
</configuration>  
```  
  
 클라이언트와 서버 모두 이 새로 생성된 구성 섹션을 사용하여 런타임 채널 스택의 최하위(전송 수준 위)에 사용자 지정 팩터리를 삽입합니다.  
  
```xml  
<customBinding>  
  <binding name="sampleBinding">  
    <droppingInterceptor/>  
    <httpTransport/>  
  </binding>  
</customBinding>  
```  
  
 클라이언트에서는 `MessageInterceptor` 라이브러리를 사용하여 사용자 지정 헤더를 짝수 번호의 메시지에 추가합니다. 한편 서비스는 `MessageInterceptor` 라이브러리를 사용하여 이 특수 헤더가 없는 메시지를 삭제합니다.  
  
 서비스와 클라이언트를 차례로 실행한 후 다음과 같은 클라이언트 출력이 나타나야 합니다.  
  
```console  
Reporting the next 10 wind speed  
100 kph  
Server dropped a message.  
90 kph  
80 kph  
Server dropped a message.  
70 kph  
60 kph  
Server dropped a message.  
50 kph  
40 kph  
Server dropped a message.  
30 kph  
20 kph  
Server dropped a message.  
10 kph  
Press ENTER to shut down client  
```  
  
 클라이언트가 서로 다른 10가지 풍속을 서비스에 보고하지만, 그 중 절반에만 특수 헤더를 태그합니다.  
  
 서비스에서는 다음과 같이 출력됩니다.  
  
```console  
Press ENTER to exit.  
Dangerous wind detected! Reported speed (90) is greater than 64 kph.  
Dangerous wind detected! Reported speed (70) is greater than 64 kph.  
5 wind speed reports have been received.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. 다음 명령을 사용 하 여 ASP.NET 4.0을 설치 합니다.  
  
    ```console  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
    ```  
  
2. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
3. 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따르세요.  
  
4. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
5. 먼저 Service.exe를 실행한 다음 Client.exe를 실행하고 두 콘솔 창의 출력을 확인합니다.  
