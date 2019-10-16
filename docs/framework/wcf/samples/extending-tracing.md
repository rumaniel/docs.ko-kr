---
title: 추적 확장
ms.date: 03/30/2017
ms.assetid: 2b971a99-16ec-4949-ad2e-b0c8731a873f
ms.openlocfilehash: 957ba3f1fc8c778ebb5b481d329af9906a36fde9
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044962"
---
# <a name="extending-tracing"></a>추적 확장
이 샘플에서는 클라이언트 및 서비스 코드에 사용자 정의 동작 추적을 작성 하 여 WCF (Windows Communication Foundation) 추적 기능을 확장 하는 방법을 보여 줍니다. 이렇게 하면 사용자가 작업의 논리 단위에 대한 추적 동작 및 그룹 추적을 만들 수 있습니다. 전송(같은 엔드포인트 내)과 전파(엔드포인트 사이)를 통해 동작을 상호 연결시킬 수도 있습니다. 이 샘플에서는 클라이언트와 서버 모두에 대해 추적이 사용됩니다. 클라이언트 및 서비스 구성 파일에서 추적을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [추적 및 메시지 로깅](../../../../docs/framework/wcf/samples/tracing-and-message-logging.md)을 참조 하세요.  
  
 이 샘플은 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md)을 기반으로 합니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\ExtendingTracing`  
  
## <a name="tracing-and-activity-propagation"></a>추적 및 동작 전파  
 사용자 정의 동작 추적을 사용 하면 사용자가 추적 작업을 만들어 논리적 작업 단위로 추적을 그룹화 하 고, 전송 및 전파를 통해 동작을 상호 연결 하 고, WCF 추적의 성능 비용을 줄일 수 있습니다 (예: 디스크 공간 비용). 로그 파일의  
  
### <a name="adding-custom-sources"></a>사용자 지정 소스 추가  
 사용자 정의 추적은 클라이언트와 서비스 코드 모두에 추가할 수 있습니다. 클라이언트 또는 서비스 구성 파일에 추적 소스를 추가 하면 이러한 사용자 지정 추적을 기록 하 고 [Service Trace Viewer 도구 (svctraceviewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)에 표시할 수 있습니다. 다음 코드에서는 `ServerCalculatorTraceSource`라는 사용자 정의 추적 소스를 구성 파일에 추가하는 방법을 보여 줍니다.  
  
```xml  
<system.diagnostics>  
    <sources>  
        <source name="System.ServiceModel" switchValue="Warning" propagateActivity="true">  
            <listeners>  
                <add type="System.Diagnostics.DefaultTraceListener" name="Default">  
                    <filter type="" />  
                </add>  
                <add name="xml">  
                    <filter type="" />  
                </add>  
            </listeners>  
        </source>  
        <source name="ServerCalculatorTraceSource" switchValue="Information,ActivityTracing">  
            <listeners>  
                <add type="System.Diagnostics.DefaultTraceListener" name="Default">  
                    <filter type="" />  
                </add>  
                <add name="xml">  
                    <filter type="" />  
                </add>  
            </listeners>  
        </source>  
    </sources>  
    <sharedListeners>  
       <add initializeData="C:\logs\ServerTraces.svclog" type="System.Diagnostics.XmlWriterTraceListener"  
        name="xml" traceOutputOptions="Callstack">  
            <filter type="" />  
        </add>  
    </sharedListeners>  
    <trace autoflush="true" />  
</system.diagnostics>....  
....  
```  
  
### <a name="correlating-activities"></a>동작 상호 연결  
 엔드포인트 사이에서 직접 동작을 상호 연결하려면 `propagateActivity` 추적 소스에서 `true` 특성을 `System.ServiceModel`로 설정해야 합니다. 또한 WCF 작업을 거치지 않고 추적을 전파 하려면 ServiceModel 동작 추적을 해제 해야 합니다. 다음 코드 예제에서 이를 확인할 수 있습니다.  
  
> [!NOTE]
> ServiceModel 동작 추적을 끄는 것은 `switchValue` 속성으로 표시되는 추적 수준을 off로 설정하는 것과 같지 않습니다.  
  
```xml  
<system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Warning" propagateActivity="true">  
  
    ...  
  
       </source>  
    </sources>  
</system.diagnostics>  
```  
  
### <a name="lessening-performance-cost"></a>수행 비용 절감  
 `ActivityTracing` 추적 소스에서 `System.ServiceModel`을 off로 설정하면 ServiceModel 동작 추적이 포함되지 않고 사용자 정의 동작 추적만 포함된 추적 파일이 생성됩니다. 그러면 로그 파일의 크기가 훨씬 작아집니다. 그러나 WCF 처리 추적과의 상관 관계를 설정할 기회가 손실 됩니다.  
  
##### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
## <a name="see-also"></a>참고자료

- [AppFabric 모니터링 샘플](https://go.microsoft.com/fwlink/?LinkId=193959)
