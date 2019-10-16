---
title: 순환 추적
ms.date: 03/30/2017
ms.assetid: 5ff139f9-8806-47bc-8f33-47fe6c436b92
ms.openlocfilehash: ad3e4acca7e4bce24c839e71381bf321365a4b2e
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045687"
---
# <a name="circular-tracing"></a>순환 추적

이 샘플에서는 순환 버퍼 추적 수신기의 구현 방법을 보여 줍니다. 프로덕션 서비스의 대표적인 시나리오는 장기간 사용 가능한 서비스가 있고 낮은 수준으로 추적 로깅을 사용하도록 설정한 경우입니다. 이러한 서비스는 많은 디스크 공간을 사용합니다. 서비스의 문제를 해결할 때는 추적 로그에서 가장 최근의 데이터가 문제 해결과 직접적인 관련이 있습니다. 이 샘플에서는 구성 가능한 최대 데이터 크기에 맞게 디스크에 가장 최근의 추적만 유지하는 순환 버퍼 추적 수신기를 구현하는 방법을 보여 줍니다. 이 샘플은 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md) 을 기반으로 하며 사용자 지정 추적 수신기를 포함 합니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

이 샘플에서는 [추적 및 메시지 로깅](../../../../docs/framework/wcf/samples/tracing-and-message-logging.md) 샘플에 대해 잘 알고 있으며 [추적 및 메시지 로깅](../../../../docs/framework/wcf/samples/tracing-and-message-logging.md) 샘플에 대해 제공 된 설명서를 읽었습니다.

## <a name="circular-buffer-trace-listener"></a>순환 버퍼 추적 수신기

순환 버퍼 추적 수신기의 구현은 각각 필요한 전체 추적 로그 데이터 크기의 최대 절반까지 저장할 수 있는 두 개의 파일이 있는 것을 전제로 합니다. 수신기는 파일 하나를 만든 다음 데이터 크기의 절반에 도달할 때까지 이 파일에 기록하고 그런 다음 두 번째 파일로 전환합니다. 수신기가 두 번째 파일에서도 크기 제한에 도달하면 새 추적으로 첫 번째 파일을 덮어씁니다.

이 수신기는 `XmlWriteTraceListener` 에서 파생 되며 [서비스 추적 뷰어 도구 (svctraceviewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)를 사용 하 여 로그를 볼 수 있습니다. 로그를 볼 때는 Service Trace Viewer 도구에서 두 개의 로그 파일을 동시에 열어 쉽게 다시 결합할 수 있습니다. Service Trace Viewer 도구는 추적이 올바른 순서대로 표시되도록 자동으로 정렬합니다.

## <a name="configuration"></a>Configuration

수신기 및 소스 요소에 대한 다음 코드를 추가하여 순환 버퍼 추적 수신기를 사용하도록 서비스를 구성할 수 있습니다. 순환 추적 수신기의 구성에서 `maxFileSizeKB` 특성을 설정하여 최대 파일 크기를 지정합니다. 다음 코드는 이 설정을 보여 줍니다.

```xml
<system.diagnostics>
  <sources>
    <source name="System.ServiceModel" switchValue="Information,ActivityTracing" propagateActivity="true">
      <listeners>
        <add name="CircularTraceListener" />
      </listeners>
    </source>
  </sources>
  <sharedListeners>
    <add name="CircularTraceListener" type="Microsoft. Samples.ServiceModel.CircularTraceListener,CircularTraceListener"
         initializeData="c:\logs\CircularTracing-service.svclog" maxFileSizeKB="100" />
  </sharedListeners>
  <trace autoflush="true" />
</system.diagnostics>
```

#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 해야 합니다.

2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.

3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\CircularTracing`

## <a name="see-also"></a>참고자료

- [AppFabric 모니터링 샘플](https://go.microsoft.com/fwlink/?LinkId=193959)
