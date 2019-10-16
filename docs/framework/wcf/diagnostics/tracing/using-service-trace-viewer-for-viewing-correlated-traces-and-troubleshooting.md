---
title: Service Trace Viewer를 사용하여 상호 관련된 추적 보기 및 문제 해결
ms.date: 03/30/2017
ms.assetid: 05d2321c-8acb-49d7-a6cd-8ef2220c6775
ms.openlocfilehash: 8f51f49bf7346ea19e8f64b5ec537d36cce0d354
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662853"
---
# <a name="using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting"></a>Service Trace Viewer를 사용하여 상호 관련된 추적 보기 및 문제 해결

이 항목에서는 추적 데이터 형식, 추적 데이터를 보는 방법 및 Service Trace Viewer를 사용하여 애플리케이션 문제를 해결하는 방법에 대해 설명합니다.

## <a name="using-the-service-trace-viewer-tool"></a>Service Trace Viewer 도구 사용

Windows Communication Foundation (WCF) Service Trace Viewer 도구를 사용 하면 오류의 근본 원인을 찾으려고 WCF 수신기에 의해 생성 된 진단 추적 정보를 상호 연결할 수 있습니다. 도구를 쉽게 보고, 그룹화 하 고 진단, 복구 및 WCF 서비스를 사용 하 여 문제를 확인할 수 있도록 추적을 필터링 하는 방법을 제공 합니다. 이 도구를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [Service Trace Viewer 도구 (SvcTraceViewer.exe)](../../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)합니다.

이 항목에서는 실행 하 여 생성 된 추적의 스크린 샷을 합니다 [Tracing and Message Logging](../../../../../docs/framework/wcf/samples/tracing-and-message-logging.md) 샘플을 사용 하 여 볼 때 합니다 [Service Trace Viewer 도구 (SvcTraceViewer.exe)](../../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)합니다. 이 항목에서는 추적의 내용, 동작 및 상관 관계를 이해하는 방법과 문제 해결 시 많은 수의 추적을 분석하는 방법을 보여 줍니다.

## <a name="viewing-trace-content"></a>추적 내용 보기

추적 이벤트에는 다음과 같은 가장 중요한 정보가 들어 있습니다.

- 동작 이름(설정된 경우)

- 내보내기 시간

- 추적 수준

- 추적 소스 이름

- 프로세스 이름

- 스레드 ID

- 대상에 추적에 관련 된 자세한 정보를 얻을 수 있는 Microsoft 문서를 가리키는 URL 인 고유한 추적 식별자입니다.

 오른쪽 위 패널 또는 Service Trace Viewer에서에서 볼 수 있습니다 이러한 모든 합니다 **기본 정보** 추적을 선택할 때 오른쪽 아래 패널의 서식이 지정 된 보기에는 섹션입니다.

> [!NOTE]
> 클라이언트와 서비스가 동일한 컴퓨터에 있는 경우 두 애플리케이션에 대한 추적이 있습니다. 이러한 필터링 할 수 있습니다 사용 하 여 **프로세스 이름** 열.

서식이 지정된 보기에서는 사용 가능한 경우 추적 및 추가 세부 정보에 대한 설명을 볼 수도 있습니다. 추가 세부 정보에는 예외 형식 및 메시지, 호출 스택, 메시지 동작, 보낸 사람/받는 사람 필드 및 기타 예외 정보가 포함될 수 있습니다.

XML 보기에서 유용한 xml 태그는 다음과 같습니다.

- `<SubType>` (추적 수준)입니다.

- `<TimeCreated>`.

- `<Source>` (추적 소스 이름)입니다.

- `<Correlation>` (작업 id에 추적을 내보낼 때 설정).

- `<Execution>` (프로세스 및 스레드 id)입니다.

- `<Computer>`.

- `<ExtendedData>`를 포함 하 여 `<Action>`, `<MessageID>` 고 `<ActivityId>` 메시지를 보낼 때 메시지 헤더에 설정 합니다.

"채널을 통해 메시지를 보냈습니다." 추적을 검사하면 다음 내용을 볼 수 있습니다.

```xml
<E2ETraceEvent xmlns="http://schemas.microsoft.com/2004/06/E2ETraceEvent">
   <System xmlns="http://schemas.microsoft.com/2004/06/windows/eventlog/system">
      <EventID>262163</EventID>
      <Type>3</Type>
      <SubType Name="Information">0</SubType>
      <Level>8</Level>
      <TimeCreated SystemTime="2006-08-04T18:45:30.8491051Z" />
      <Source Name="System.ServiceModel" />
       <Correlation ActivityID="{27c6331d-8998-43aa-a382-03239013a6bd}"/>
       <Execution ProcessName="client" ProcessID="1808" ThreadID="1" />
       <Channel />
       <Computer>TEST1</Computer>
   </System>
   <ApplicationData>
       <TraceData>
          <DataItem>
             <TraceRecord xmlns="http://schemas.microsoft.com/2004/10/E2ETraceEvent/TraceRecord" Severity="Information">
                 <TraceIdentifier>http://msdn.microsoft.com/library/System.ServiceModel.Channels.MessageSent.aspx</TraceIdentifier>
                 <Description>Sent a message over a channel.</Description>
                 <AppDomain>client.exe</AppDomain>
                 <Source>System.ServiceModel.Channels.ClientFramingDuplexSessionChannel/35191196</Source>
                <ExtendedData xmlns="http://schemas.microsoft.com/2006/08/ServiceModel/MessageTransmitTraceRecord">

                  <MessageProperties>
                     <AllowOutputBatching>False</AllowOutputBatching>
                  </MessageProperties>
                  <MessageHeaders>
                     <Action d4p1:mustUnderstand="1" xmlns:d4p1="http://www.w3.org/2003/05/soap-envelope" xmlns="http://www.w3.org/2005/08/addressing">http://Microsoft.ServiceModel.Samples/ICalculator/Multiply</Action>
                     <MessageID xmlns="http://www.w3.org/2005/08/addressing">urn:uuid:7c6670d8-4c9c-496e-b6a0-2ceb6db35338</MessageID>
                     <ActivityId CorrelationId="b02e2189-0816-4387-980c-dd8e306440f5" xmlns="http://schemas.microsoft.com/2004/09/ServiceModel/Diagnostics">27c6331d-8998-43aa-a382-03239013a6bd</ActivityId>
                     <ReplyTo xmlns="http://www.w3.org/2005/08/addressing">
                        <Address>http://www.w3.org/2005/08/addressing/anonymous</Address>
                    </ReplyTo>
                    <To d4p1:mustUnderstand="1" xmlns:d4p1="http://www.w3.org/2003/05/soap-envelope" xmlns="http://www.w3.org/2005/08/addressing">net.tcp://localhost/servicemodelsamples/service</To>
                  </MessageHeaders>
                  <RemoteAddress>net.tcp://localhost/servicemodelsamples/service</RemoteAddress>
                </ExtendedData>
            </TraceRecord>
          </DataItem>
       </TraceData>
   </ApplicationData>
</E2ETraceEvent>
```

## <a name="servicemodel-e2e-tracing"></a>ServiceModel E2E 추적

경우는 `System.ServiceModel` 추적 원본으로 설정 된를 `switchValue` Off가 아닌 및 `ActivityTracing`, WCF 작업 및 처리 하는 WCF에 대 한 전송을 만듭니다.

동작은 해당 처리 단위와 관련된 모든 추적을 그룹화하는 논리적인 처리 단위입니다. 예를 들어 요청별로 하나의 동작을 정의할 수 있습니다. 전송은 엔드포인트 내의 동작 사이에 인과 관계를 만듭니다. 동작 ID를 전파하면 엔드포인트를 통해 동작을 서로 연결할 수 있습니다. 설정 하 여 이렇게 `propagateActivity` = `true` 모든 끝점에서 구성에서 합니다. 동작, 전송 및 전파를 통해 오류 상관 관계를 수행할 수 있습니다. 이 방법으로 오류에 대한 근본 원인을 신속하게 찾을 수 있습니다.

클라이언트에서 각 개체 모델 호출 (예를 들어, Open ChannelFactory, 추가, 나누기, 및 등입니다.)에 대해 하나의 WCF 동작이 만들어집니다. 각 작업 호출은 "Process Action" 동작에서 처리 됩니다.

추출 된 다음 스크린샷에서 [Tracing and Message Logging](../../../../../docs/framework/wcf/samples/tracing-and-message-logging.md) 왼쪽된 패널 샘플 만들기 시간을 기준으로 정렬 하는 클라이언트 프로세스에서 만들어진 활동의 목록을 표시 합니다. 다음은 발생한 동작 순서 목록입니다.

- 채널 팩터리 생성(ClientBase)

- 채널 팩터리 열기

- 작업 추가 처리

- 응답 메시지를 보안 세션 (첫 번째 요청에서의이 OCCURRED) 및 처리 된 세 가지 보안 인프라를 설정 합니다. RST, RSTR, SCT (메시지 처리 1, 2, 3).

- 빼기, 곱하기 및 나누기 요청 처리

- 채널 팩터리 닫기, 보안 세션 닫기 및 보안 메시지 응답 취소 처리

 wsHttpBinding이 사용되기 때문에 보안 인프라 메시지가 표시됩니다.

> [!NOTE]
> Wcf에서 응답 메시지를 별도 동작 (Process message)에서 처음 처리 되 고 살펴보겠습니다 전송을 통해 요청 메시지를 포함 하는 해당 Process Action 동작 시키기 전에 합니다. 이는 인프라 메시지와 비동기 요청에 대해 발생하며, 그 이유는 메시지를 검사하고, activityId 헤더를 읽고, 이 ID를 갖는 기존의 Process Action 동작을 식별하여 서로 관련시켜야 하기 때문입니다. 동기 요청의 경우에는 응답을 차단하므로 응답이 어떤 Process Action과 연결되어 있는지 알 수 있습니다.

다음 이미지는 만든 시간 (왼쪽된 패널) 중첩 된 활동 및 추적 (오른쪽 위 패널)으로 나열 하는 WCF 클라이언트 동작을 보여줍니다.

![WCF 클라이언트 생성 시간을 기준으로 표시 되는 작업을 보여주는 스크린샷.](./media/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting/wcf-client-activities-creation-time.gif)

왼쪽 패널에서 동작을 선택하면 중첩된 동작과 추적이 오른쪽 위 패널에 표시됩니다. 따라서 이 보기는 선택한 부모 동작을 기준으로 왼쪽에 동작 목록을 축소한 계층 구조 보기입니다. 선택한 Process action Add가 첫 번째 요청이므로 이 동작에 Set Up Secure Session 동작(전송, 다시 전송)이 포함되며 추가 작업의 실제 처리를 추적합니다.

Process action Add 동작 왼쪽된 패널에서 두 번 클릭, 추가 관련 된 클라이언트 WCF 작업의 그래픽 표시를 보면 합니다. 왼쪽의 첫 번째 동작은 기본 동작인 루트 동작(0000)입니다. WCF는 앰비언트 동작 전송합니다. 이 정의 되어 있지 않으면 WCF는 0000에서 전송 합니다. 이때 두 번째 동작인 Process Action Add가 0에서 전송합니다. 그런 다음 Setup Secure Session이 표시됩니다.

다음 이미지는 활동을 앰비언트 동작 (여기서 0), 특히 WCF 클라이언트 그래프 뷰 표시 작업을 처리 하 고 보안 세션을 설정 합니다.

![앰비언트 동작 및 프로세스 동작을 보여 주는 Trace Viewer에서 그래프로 표시 합니다.](./media/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting/wcf-activities-graph-ambient-process.gif)

오른쪽 위 패널에서 Process Action Add 동작과 관련된 추적이 모두 표시됩니다. 특히 같은 동작으로 요청 메시지("채널을 통해 메시지를 보냈습니다.")를 보내고 응답("채널을 통해 메시지를 받았습니다")을 받았습니다. 다음 그래프에서 이를 확인할 수 있습니다. 쉽게 구별할 수 있도록 Set up Secure Session 동작은 그래프에 축소되어 있습니다.

다음 이미지에는 Process Action 동작에 대 한 추적의 목록을 보여 줍니다. 요청을 전송 하 고 동일한 동작에서 응답을 수신 합니다.

![스크린 샷의 Trace Viewer Process Action 동작에 대 한 추적의 목록을 표시 합니다.](./media/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting/process-action-traces.gif)

이때 클라이언트 추적만 이해를 돕기 위해 로드 하지만 서비스 추적 (받은 요청 메시지와 보낸 응답 메시지) 도구에 로드 이기도 한 경우 동일한 동작에서 나타나며 및 `propagateActivity` 로 설정 된 `true.` 뒷부분에 나오는 그림에 나와 있습니다.

서비스에서 활동 모델 WCF 개념을 다음과 같이 매핑합니다.

1. ServiceHost를 생성하고 엽니다. 이렇게 하면 보안의 경우 여러 호스트 관련 동작을 만들 수 있습니다.

2. Open ServiceHost 내부 및 외부로 전송하여 ServiceHost에서 각 수신기에 대한 Listen At 동작을 만듭니다.

3. 수신기 클라이언트에서 시작 된 통신 요청을 감지 하면 클라이언트에서 보낸 모든 바이트가 처리 되는, "Receive Bytes" 동작으로 전송 합니다. 이 동작에서 클라이언트-서비스 상호 작용 중에 발생한 연결 오류가 표시됩니다.

4. 각 바이트 집합 수신 되는 메시지에 해당 하는,에서는 처리 "메시지 처리" 작업을 이러한 바이트는 WCF 메시지 개체를 만들겠습니다. 이 동작에서 악의적인 메시지 또는 잘못된 봉투와 관련된 오류가 표시됩니다.

5. 메시지가 형성되면 Process Action 동작으로 전송합니다. `propagateActivity`가 클라이언트와 서버에서 모두 `true`로 설정되는 경우 이 동작에는 클라이언트에서 정의되고 앞에서 설명한 것과 동일한 ID를 갖게 됩니다. 이 단계에서 먼저 끝점을 통해 직접적인 상관 관계의 이점을 활용 하도록 요청에 관련 된 WCF에서 내보낸 모든 추적이 응답 메시지 처리를 포함 하 여 같은 동작에 있으므로 합니다.

6. Out of process 작업에 대 한 WCF에서 내보낸 추적과 사용자 코드에서 내보낸 추적을 격리 하기 위한 "사용자 코드 실행" 작업을 만들겠습니다. 앞의 예제에서 해당 하는 경우 클라이언트가 전파 한 동작이에 없는 사용자 코드 실행"작업의"서비스가 추가 응답을 보냅니다"추적을 내보냅니다.

다음 그림에서 왼쪽의 첫 번째 동작은 기본 동작인 루트 동작(0000)입니다. 다음 세 동작은 ServiceHost를 여는 동작입니다. 열 5의 동작은 수신기이고, 나머지 동작(6 - 8)은 바이트 처리부터 사용자 코드 활성화까지 메시지를 처리하는 WCF입니다.

다음 이미지에는 WCF 서비스 작업의 그래프 뷰를 보여 줍니다.

![스크린 샷의 Trace Viewer WCF 서비스 동작의 목록을 표시 합니다.](./media/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting/wcf-service-activities.gif)

다음 스크린 샷에서는 클라이언트와 서비스 모두의 동작을 보여 주고 여러 프로세스에 걸쳐 Process Action Add 동작을 강조 표시합니다(주황색). 화살표는 클라이언트와 서비스가 보내고 받은 요청 및 응답 메시지를 서로 연결합니다. Process Action의 추적이 그래프에서 프로세스 간에 구분되어 있지만 오른쪽 위 패널에 같은 동작의 일부로 표시되어 있습니다. 이 패널에서 보낸 메시지에 대한 클라이언트 추적을 확인한 다음 받고 처리한 메시지에 대한 서비스 추적을 확인할 수 있습니다.

다음 이미지는 모두 WCF 클라이언트 및 서비스 동작 그래프 보기를 표시 합니다.

![모두 WCF 클라이언트 및 서비스 동작을 보여 주는 Trace Viewer에서 그래프로 표시 합니다.](./media/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting/wcf-client-service-activities.gif)

다음 오류 시나리오에서 서비스 및 클라이언트의 오류와 경고 추적이 서로 관련되어 있습니다. 예외가 서비스의 사용자 코드에서 먼저 throw됩니다("서비스가 사용자 코드에서 이 요청을 처리할 수 없습니다." 예외에 대한 경고 추적이 포함된 맨 오른쪽의 녹색 동작). 응답이 클라이언트에게 전송되면 오류 메시지를 표시하기 위해 경고 추적이 다시 내보내집니다(왼쪽의 분홍색 동작). 그런 다음 클라이언트가 해당 WCF 클라이언트를 닫습니다(왼쪽 아래의 노란색 동작). 그러면 서비스에 대한 연결이 중단됩니다. 서비스가 오류를 throw합니다(오른쪽의 가장 긴 분홍색 동작).

![추적 뷰어를 사용 하 여](../../../../../docs/framework/wcf/diagnostics/tracing/media/wcfc-e2etrace9s.gif "wcfc_e2etrace9s")

서비스와 클라이언트의 오류 상관 관계

이러한 추적을 생성하는 데 사용된 샘플은 wsHttpBinding을 사용하는 일련의 동기 요청입니다. 보안을 사용하지 않거나 비동기 요청이 있는 시나리오의 경우 이 그래프에 차이가 있습니다. 여기서 Process Action 동작은 비동기 호출을 구성하는 시작 및 끝 작업을 포함하며 호출 동작에 대한 전송을 표시합니다. 추가 시나리오에 대 한 자세한 내용은 참조 하세요. [종단 간 추적 시나리오](../../../../../docs/framework/wcf/diagnostics/tracing/end-to-end-tracing-scenarios.md)합니다.

## <a name="troubleshooting-using-the-service-trace-viewer"></a>Service Trace Viewer를 사용하여 문제 해결

Service Trace Viewer 도구에서 추적 파일을 로드하면 왼쪽 패널에서 빨간색 또는 노란색 동작을 선택하여 애플리케이션에서 문제의 원인을 추적할 수 있습니다. 000 동작에는 일반적으로 사용자에게 버블링되는 처리되지 않은 예외가 있습니다.

다음 이미지에는 문제 원인을 찾으려면 빨간색 또는 노란색 작업을 선택 하는 방법을 보여 줍니다.
![문제 원인을 찾기 위한 빨간색 또는 노란색 작업의 스크린샷.](./media/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting/service-trace-viewer.gif)

오른쪽 위 패널에서는 왼쪽에서 선택한 동작에 대한 추적을 검사할 수 있습니다. 그런 다음 이 패널에서 빨간색 또는 노란색 추적을 검사하고 이들 추적이 상호 연결된 방식을 볼 수 있습니다. 앞의 그래프에서는 동일한 Process Action 동작에서 클라이언트와 서비스 모두에 대한 경고 추적을 볼 수 있습니다.

이러한 추적이 오류의 근본 원인을 제공하지 않으면 왼쪽 패널에서 선택한 동작(여기서는 Process action)을 두 번 클릭하여 그래프를 사용할 수 있습니다. 그러면 관련된 동작이 있는 그래프가 표시됩니다. 확장할 수 있습니다 다음 관련된 활동 ("+" 기호 클릭) 관련된 작업에서 빨간색 이나 노란색에서 첫 번째로 내보낸된 추적을 찾으려고 합니다. 문제의 근본 원인을 추적할 때까지 빨간색 또는 노란색 추적 바로 전에 발생한 동작을 계속 확장하면서 관련된 동작이나 엔드포인트 간의 메시지 흐름으로의 전송을 살펴 봅니다.

![추적 뷰어를 사용 하 여](../../../../../docs/framework/wcf/diagnostics/tracing/media/wcfc-e2etrace9s.gif "wcfc_e2etrace9s")

동작을 확장하여 문제의 근본 원인 추적

ServiceModel `ActivityTracing`이 해제되어 있지만 ServiceModel 추적이 설정된 경우 0000 동작에 내보낸 ServiceModel 추적을 확인할 수 있습니다. 하지만 이렇게 하려면 이러한 추적의 상관 관계를 이해해야 합니다.

메시지 로깅을 사용하도록 설정된 경우 메시지 탭을 사용하여 오류의 영향을 받는 메시지를 확인할 수 있습니다. 빨간색 또는 노란색 메시지를 두 번 클릭하여 관련 동작에 대한 그래프 보기를 볼 수 있습니다. 이러한 동작은 오류가 발생한 요청과 가장 관련이 높은 동작입니다.

![스크린 샷의 추적 뷰어에 메시지 로깅을 사용 합니다.](./media/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting/message-logging-enabled.gif)

문제 해결을 시작 하려면 빨간색 또는 노란색 메시지 추적을 선택 하 고 근본 원인을 추적을 두 번 클릭 합니다.

## <a name="see-also"></a>참고자료

- [엔드투엔드 추적 시나리오](../../../../../docs/framework/wcf/diagnostics/tracing/end-to-end-tracing-scenarios.md)
- [Service Trace Viewer 도구(SvcTraceViewer.exe)](../../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)
- [추적](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)
