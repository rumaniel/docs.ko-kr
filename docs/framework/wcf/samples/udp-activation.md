---
title: UDP 활성화
ms.date: 03/30/2017
ms.assetid: 4b0ccd10-0dfb-4603-93f9-f0857c581cb7
ms.openlocfilehash: 13444ab1be440c8e1a5f945cd512afa33772ea57
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044635"
---
# <a name="udp-activation"></a>UDP 활성화
이 샘플은 전송을 기반으로 [합니다. UDP](../../../../docs/framework/wcf/samples/transport-udp.md) 샘플. 전송을 확장 합니다 [. WAS](../../../../docs/framework/wcf/samples/transport-udp.md) (Windows process activation Service)를 사용한 프로세스 활성화를 지원 하기 위한 UDP 샘플입니다.  
  
 이 샘플은 크게 세 부분으로 구성됩니다.  
  
- UDP 프로토콜 활성기(활성화할 애플리케이션을 대신하여 UDP 메시지를 수신하는 독립 실행형 프로세스)  
  
- UDP 사용자 지정 전송을 사용하여 메시지를 보내는 클라이언트  
  
- WAS에서 활성화한 작업자 프로세스에서 호스팅되고 UDP 사용자 지정 전송을 통해 메시지를 수신하는 서비스  
  
## <a name="udp-protocol-activator"></a>UDP 프로토콜 활성기  
 UDP 프로토콜 활성기는 WCF 클라이언트와 WCF 서비스 간의 브리지입니다. 전송 계층에서 UDP 프로토콜을 통한 데이터 통신을 제공합니다. 주요 기능 두 가지는 다음과 같습니다.  
  
- WAS LA(수신기 어댑터) - 들어오는 메시지에 대한 응답으로 WAS와 공동 작업하여 프로세스를 활성화합니다.  
  
- UDP 프로토콜 수신기 - 활성화할 애플리케이션을 대신하여 UDP 메시지를 수락합니다.  
  
 활성기는 서버 컴퓨터에서 독립 실행형 프로그램으로 실행되어야 합니다. 일반적으로 NetTcpActivator 및 NetPipeActivator와 같은 WAS 수신기 어댑터는 장기간 실행되는 Windows 서비스에서 구현됩니다. 그러나 이 샘플에서는 단순성을 위해 프로토콜 활성기를 독립 실행형 애플리케이션으로 구현합니다.  
  
### <a name="was-listener-adapter"></a>WAS 수신기 어댑터  
 UDP용 WAS 수신기 어댑터는 `UdpListenerAdapter` 클래스에서 구현됩니다. 이는 WAS와 상호 작용하여 UDP 프로토콜의 애플리케이션 활성화를 수행하는 모듈입니다. 이 작업은 다음과 같은 Webhost API를 호출하여 수행됩니다.  
  
- `WebhostRegisterProtocol`  
  
- `WebhostUnregisterProtocol`  
  
- `WebhostOpenListenerChannelInstance`  
  
- `WebhostCloseAllListenerChannelInstances`  
  
 처음에 `WebhostRegisterProtocol`을 호출한 후 수신기 어댑터는 %windir%\system32\inetsrv에 있는 applicationHost.config에 등록된 모든 응용 프로그램에 대해 WAS로부터 `ApplicationCreated` 콜백을 수신합니다. 이 샘플에서는 UDP 프로토콜(프로토콜 ID: &quot;net.udp&quot;)을 사용하는 애플리케이션만 처리합니다. 다른 구현에서는 애플리케이션의 동적 구성 변경 사항(예: 사용 안 함에서 사용으로의 애플리케이션 전환)에 응답하는 경우 이를 다르게 처리할 수 있습니다.  
  
 `ConfigManagerInitializationCompleted` 콜백이 수신되면 이는 WAS가 프로토콜의 초기화에 대한 모든 알림을 완료했음을 나타냅니다. 이때 수신기 어댑터는 활성화 요청을 처리할 준비가 되어 있습니다.  
  
 애플리케이션에 대해 처음으로 새 요청이 들어올 때 수신기 어댑터는 `WebhostOpenListenerChannelInstance`를 WAS로 호출하고 WAS는 작업자 프로세스를 시작합니다(아직 시작되지 않은 경우). 그런 다음 프로토콜 처리기가 로드되고 수신기 어댑터와 가상 애플리케이션 간의 통신이 시작될 수 있습니다.  
  
 수신기 어댑터는 <`listenerAdapters`> 섹션에서 다음과 같이%SystemRoot%\System32\inetsrv\ApplicationHost.config에 등록 됩니다.  
  
```xml  
<add name="net.udp" identity="S-1-5-21-2127521184-1604012920-1887927527-387045" />  
```  
  
### <a name="protocol-listener"></a>프로토콜 수신기  
 UDP 프로토콜 수신기는 가상 애플리케이션을 대신하여 UDP 엔드포인트에서 수신 대기하는 프로토콜 활성기 내에 있는 모듈입니다. 이 수신기는 `UdpSocketListener` 클래스에서 구현됩니다. 엔드포인트는 사이트의 프로토콜 바인딩에서 포트 번호가 추출되는 `IPEndpoint`로 표시됩니다.  
  
### <a name="control-service"></a>제어 서비스  
 이 샘플에서는 WCF를 사용 하 여 활성기와 WAS 작업자 프로세스 간에 통신 합니다. 활성기에 상주하는 서비스를 제어 서비스라고 합니다.  
  
## <a name="protocol-handlers"></a>프로토콜 처리기  
 수신기 어댑터가 `WebhostOpenListenerChannelInstance`를 호출한 후 WAS 프로세스 관리자는 작업자 프로세스를 시작합니다(시작되지 않은 경우). 그런 다음 작업자 프로세스 내부의 애플리케이션 관리자는 해당 `ListenerChannelId`에 대한 요청과 함께 UDP PPH(프로세스 프로토콜 처리기)를 로드합니다. PPH은 호출을 차례로 `IAdphManager`호출 합니다.`StartAppDomainProtocolListenerChannel` UDP AppDomain 프로토콜 처리기 (ADPH)를 시작 합니다.  
  
## <a name="hostedudptransportconfiguration"></a>HostedUDPTransportConfiguration  
 이 정보는 다음과 같이 Web.config에 등록됩니다.  
  
```xml  
<serviceHostingEnvironment>  
<add name="net.udp" transportConfigurationType="Microsoft.ServiceModel.Samples.Hosting.HostedUdpTransportConfiguration, UdpActivation, Version=1.0.0.0, Culture=neutral, PublicKeyToken=6fa904d2da1848d6" />  
</serviceHostingEnvironment>  
```  
  
## <a name="special-setup-for-this-sample"></a>이 샘플의 특수 설치 절차  
 이 샘플은 Windows Vista, Windows Server 2008 또는 Windows 7에서만 빌드하고 실행할 수 있습니다. 샘플을 실행하려면 먼저 모든 구성 요소가 올바르게 설치되어 있어야 합니다. 다음 단계에 따라 샘플을 설치합니다.  
  
#### <a name="to-set-up-this-sample"></a>이 샘플을 설치하려면  
  
1. 다음 명령을 사용 하 여 ASP.NET 4.0을 설치 합니다.  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
    ```  
  
2. Windows Vista에서 프로젝트를 빌드합니다. 컴파일이 끝나면 빌드 후 단계에서 다음 작업을 수행합니다.  
  
    - "Default Web Site" 사이트에 UDP 바인딩을 설치합니다.  
  
    - 가상 애플리케이션 &quot;ServiceModelSamples&quot;를 만들어 실제 경로인 &quot;%SystemDrive%\inetpub\wwwroot\servicemodelsamples&quot;를 가리킵니다.  
  
    - 또한 이 가상 애플리케이션에 대해 &quot;net.udp&quot; 프로토콜을 사용하도록 설정합니다.  
  
3. 사용자 인터페이스 애플리케이션인 &quot;WasNetActivator.exe&quot;를 시작합니다. **설치** 탭을 클릭 하 고 다음 확인란을 선택한 후 **설치** 를 클릭 하 여 설치 합니다.  
  
    - UDP Listener Adapter  
  
    - UDP Protocol Handlers  
  
4. "Wasnetactivator.exe" 사용자 인터페이스 응용 프로그램의 **활성화** 탭을 클릭 합니다. **시작** 단추를 클릭 하 여 수신기 어댑터를 시작 합니다. 이제 프로그램을 실행할 준비가 되었습니다.  
  
    > [!NOTE]
    > 이 샘플 사용을 마친 다음에는 Cleanup.bat를 실행하여 "Default Web Site"에서 net.udp 바인딩을 제거해야 합니다.  
  
## <a name="sample-usage"></a>샘플 사용  
 컴파일 후에는 다음과 같이 네 개의 다른 이진 파일이 생성됩니다.  
  
- Client.exe: 클라이언트 코드입니다. App.config는 클라이언트 구성 파일 Client.exe.config로 컴파일됩니다.  
  
- UDPActivation.dll: 모든 주요 UDP 구현이 포함된 라이브러리입니다.  
  
- Service.dll: 서비스 코드입니다. 이 파일은 가상 애플리케이션 ServiceModelSamples의 \bin 디렉터리에 복사됩니다. 서비스 파일은 Service.svc이고 구성 파일은 Web.config입니다. 컴파일 후 이러한 파일은 %SystemDrive%\Inetpub\wwwroot\ServiceModelSamples 위치에 복사됩니다.  
  
- WasNetActivator: UDP 활성기 프로그램입니다.  
  
- 필요한 모든 요소가 올바르게 설치되었는지 확인합니다. 다음 단계에서는 샘플을 실행하는 방법을 설명합니다.  
  
1. 다음과 같은 Windows 서비스가 시작되었는지 확인합니다.  
  
    - WAS(Windows Process Activation Service)  
  
    - 인터넷 정보 서비스 (IIS): W3SVC.  
  
2. 그런 다음 활성기인 WasNetActivator.exe를 시작합니다. **활성화** 탭의 드롭다운 목록에서 유일한 프로토콜인 **UDP**를 선택 합니다. **시작** 단추를 클릭 하 여 활성기를 시작 합니다.  
  
3. 활성기가 시작되었으면 명령 창에서 Client.exe를 실행하여 클라이언트 코드를 실행할 수 있습니다. 다음은 샘플 출력입니다.  
  
    ```  
    Testing Udp Activation.  
    Start the status service.  
    Sending UDP datagrams.  
    Type a word that you want to say to the server: Hello, world!  
        Sending datagram: Hello, world![0]  
        Sending datagram: Hello, world![1]  
        Sending datagram: Hello, world![2]  
        Sending datagram: Hello, world![3]  
        Sending datagram: Hello, world![4]  
    Calling UDP duplex contract (ICalculatorContract).  
        0 + 0 = 0  
        1 + 2 = 3  
        2 + 4 = 6  
        3 + 6 = 9  
        4 + 8 = 12  
    Getting status and dump server traces:  
        Operation 'Hello' is called: Hello, world![0]  
        Operation 'Hello' is called: Hello, world![1]  
        Operation 'Hello' is called: Hello, world![2]  
        Operation 'Hello' is called: Hello, world![3]  
        Operation 'Hello' is called: Hello, world![4]  
        Operation 'Add' is called: 0 + 0  
        Operation 'Add' is called: 1 + 2  
        Operation 'Add' is called: 2 + 4  
        Operation 'Add' is called: 3 + 6  
        Operation 'Add' is called: 4 + 8  
    Press <ENTER> to complete test.  
    ```  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Transport\UdpActivation`  
