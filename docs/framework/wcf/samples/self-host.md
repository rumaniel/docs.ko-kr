---
title: 자체 호스팅
ms.date: 03/30/2017
helpviewer_keywords:
- Self hosted service
- Self Host Sample [Windows Communication Foundation]
ms.assetid: 05e68661-1ddf-4abf-a899-9bb1b8272a5b
ms.openlocfilehash: a1fecb0ade00604d9a6e019ec50ceca04abeb545
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044760"
---
# <a name="self-host"></a>자체 호스팅
이 샘플에서는 콘솔 애플리케이션에서 자체 호스팅 서비스를 구현하는 방법을 보여 줍니다. 이 샘플은 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md)을 기반으로 합니다. 서비스 구성 파일이 Web.config에서 App.config로 이름이 바뀌고 호스트에서 사용하는 기본 주소를 구성하도록 수정되었습니다. 서비스 소스 코드가 구성된 기본 주소를 제공하는 서비스 호스트를 만들고 여는 정적 `Main` 기능을 구현하도록 수정되었습니다. 서비스 구현이 각 작업에 대해 콘솔에 출력을 쓰도록 수정되었습니다. 클라이언트는 서비스의 올바른 엔드포인트 주소를 구성하기 위한 부분을 제외하고는 수정되지 않았습니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 샘플에서는 다음 샘플 코드에 표시된 것과 같이 지정된 <xref:System.ServiceModel.ServiceHost> 형식에 `CalculatorService`를 만드는 정적 main 함수를 구현합니다.  
  
```csharp
// Host the service within this EXE console application.  
public static void Main()  
{  
    // Create a ServiceHost for the CalculatorService type.  
    using (ServiceHost serviceHost =   
           new ServiceHost(typeof(CalculatorService)))  
    {  
        // Open the ServiceHost to create listeners   
        // and start listening for messages.  
        serviceHost.Open();  
  
        // The service can now be accessed.  
        Console.WriteLine("The service is ready.");  
        Console.WriteLine("Press <ENTER> to terminate service.");  
        Console.WriteLine();  
        Console.ReadLine();  
    }  
}  
```  
  
 인터넷 정보 서비스(IIS) 또는 WAS(Windows Process Activation Service)에 서비스가 호스팅된 경우 서비스의 기본 주소는 호스팅 환경에 의해 제공됩니다. 자체 호스팅의 경우에는 직접 기본 주소를 지정해야 합니다. 이 작업은 다음 샘플 `add` 구성에서 보여 주는 것 처럼 요소, [ \<baseaddresses](../../../../docs/framework/configure-apps/file-schema/wcf/baseaddresses.md)의 자식 >, [ \<호스트 >](../../../../docs/framework/configure-apps/file-schema/wcf/host.md)의 자식, [ \<서비스 >](../../../../docs/framework/configure-apps/file-schema/wcf/service.md) 자식 등을 사용 하 여 수행 됩니다.  
  
```xml  
<service   
    name="Microsoft.ServiceModel.Samples.CalculatorService"  
    behaviorConfiguration="CalculatorServiceBehavior">  
  <host>  
    <baseAddresses>  
      <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
    </baseAddresses>  
  </host>  
  ...  
</service>  
```  
  
 샘플을 실행하면 작업 요청 및 응답이 서비스와 클라이언트 콘솔 창 모두에 표시됩니다. 서비스와 클라이언트를 종료하려면 각 콘솔 창에서 Enter 키를 누릅니다.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\SelfHost`  
  
## <a name="see-also"></a>참고자료

- [AppFabric 호스팅 및 지 속성 샘플](https://go.microsoft.com/fwlink/?LinkId=193961)
