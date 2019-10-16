---
title: 상관 관계 문제 해결
ms.date: 03/30/2017
ms.assetid: 98003875-233d-4512-a688-4b2a1b0b5371
ms.openlocfilehash: d4b7b4ecd724416256cf0b2499d7180200f4e75c
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291557"
---
# <a name="troubleshooting-correlation"></a>상관 관계 문제 해결
상관 관계는 워크플로 서비스 메시지를 서로 연결하거나 올바른 워크플로 인스턴스에 연결하는 데 사용되지만, 제대로 구성되지 않으면 메시지가 수신되지 않고 애플리케이션이 올바르게 작동하지 않습니다. 이 항목에서는 상관 관계 문제를 해결하기 위한 몇 가지 방법을 간략히 설명하고 상관 관계를 사용할 때 발생할 수 있는 일반적인 문제도 설명합니다.

## <a name="handle-the-unknownmessagereceived-event"></a>UnknownMessageReceived 이벤트 처리
 <xref:System.ServiceModel.ServiceHostBase.UnknownMessageReceived> 이벤트는 서비스에서 기존 인스턴스와 연결할 수 없는 메시지를 포함하여 알 수 없는 메시지를 받을 경우에 발생합니다. 자체 호스팅 서비스의 경우 이 이벤트는 호스트 애플리케이션에서 처리할 수 있습니다.

```csharp
host.UnknownMessageReceived += delegate(object sender, UnknownMessageReceivedEventArgs e)
{
    Console.WriteLine("Unknown Message Received:");
    Console.WriteLine(e.Message);
};
```

 웹 호스팅 서비스의 경우에는 <xref:System.ServiceModel.Activities.Activation.WorkflowServiceHostFactory>에서 클래스를 파생시키고 <xref:System.ServiceModel.Activities.Activation.WorkflowServiceHostFactory.CreateWorkflowServiceHost%2A>를 재정의하여 이 이벤트를 처리할 수 있습니다.

```csharp
class CustomFactory : WorkflowServiceHostFactory
{
    protected override WorkflowServiceHost CreateWorkflowServiceHost(Activity activity, Uri[] baseAddresses)
    {
        // Create the WorkflowServiceHost.
        WorkflowServiceHost host = new WorkflowServiceHost(activity, baseAddresses);

        // Handle the UnknownMessageReceived event.
        host.UnknownMessageReceived += delegate(object sender, UnknownMessageReceivedEventArgs e)
        {
            Console.WriteLine("Unknown Message Received:");
            Console.WriteLine(e.Message);
        };

        return host;
    }
}
```

 그런 다음 서비스의 <xref:System.ServiceModel.Activities.Activation.WorkflowServiceHostFactory> 파일에서 이 사용자 지정 `svc`를 지정할 수 있습니다.

```
<% @ServiceHost Language="C#" Service="OrderServiceWorkflow" Factory="CustomFactory" %>
```

 이 처리기가 호출되면 <xref:System.ServiceModel.UnknownMessageReceivedEventArgs.Message%2A>의 <xref:System.ServiceModel.UnknownMessageReceivedEventArgs> 속성을 사용하여 메시지를 검색할 수 있으며 이 메시지는 다음 메시지와 비슷합니다.

```xml
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
  <s:Header>
    <To s:mustUnderstand="1" xmlns="http://schemas.microsoft.com/ws/2005/05/addressing/none">http://localhost:8080/OrderService</To>
    <Action s:mustUnderstand="1" xmlns="http://schemas.microsoft.com/ws/2005/05/addressing/none">http://tempuri.org/IService/AddItem</Action>
  </s:Header>
  <s:Body>
    <AddItem xmlns="http://tempuri.org/">
      <Item>Books</Item>
    </AddItem>
  </s:Body>
</s:Envelope>
```

 <xref:System.ServiceModel.ServiceHostBase.UnknownMessageReceived> 처리기에 디스패치된 메시지를 검사하면 메시지가 워크플로 서비스의 인스턴스에 연결되지 않은 원인을 확인할 수 있습니다.

## <a name="use-tracking-to-monitor-the-progress-of-the-workflow"></a>추적을 사용하여 워크플로 진행 상태 모니터링
 추적을 통해 워크플로의 진행 상태를 모니터링할 수 있습니다. 기본적으로 워크플로 수명 주기 이벤트, 활동 수명 주기 이벤트, 오류 전파 및 책갈피 다시 시작에 대하여 추적 레코드가 내보내집니다. 또한 사용자 지정 활동에서 사용자 지정 추적 레코드를 내보낼 수 있습니다. 상관 관계 문제를 해결하는 경우에는 활동 추적 레코드, 책갈피 다시 시작 레코드 및 오류 전파 레코드가 가장 유용합니다. 활동 추적 레코드는 워크플로의 현재 진행 상태를 확인하는 데 사용할 수 있으며 현재 메시지를 기다리고 있는 메시징 활동을 식별하는 데 유용합니다. 책갈피 다시 시작 레코드는 워크플로에서 메시지를 받았음을 나타내므로 유용하며, 오류 전파 레코드에서는 워크플로의 오류에 대한 레코드를 제공합니다. 추적을 사용하도록 설정하려면 <xref:System.Activities.Tracking.TrackingParticipant>의 <xref:System.ServiceModel.Activities.WorkflowServiceHost.WorkflowExtensions%2A>에서 원하는 <xref:System.ServiceModel.Activities.WorkflowServiceHost>를 지정합니다. 다음 예제에서는 기본 추적 프로필을 사용 하 여 [사용자 지정 추적](../../../../docs/framework/windows-workflow-foundation/samples/custom-tracking.md) 샘플에서 `ConsoleTrackingParticipant`을 구성 합니다.

```csharp
host.WorkflowExtensions.Add(new ConsoleTrackingParticipant());
```

 ConsoleTrackingParticipant와 같은 추적 참가자는 콘솔 창이 있는 자체 호스팅 워크플로 서비스에 유용합니다. 웹 호스팅 서비스의 경우 추적 정보를 지 속성 저장소에 기록 하는 추적 참가자 (예: 기본 제공 <xref:System.Activities.Tracking.EtwTrackingParticipant> 또는 파일에 정보를 기록 하는 사용자 지정 추적 참가자)를 사용 해야 합니다.

 웹 호스팅 워크플로 서비스에 대 한 추적을 추적 하 고 구성 하는 방법에 대 한 자세한 내용은 [워크플로 추적 및 추적](../../../../docs/framework/windows-workflow-foundation/workflow-tracking-and-tracing.md), [워크플로에 대 한 추적 구성](../../../../docs/framework/windows-workflow-foundation/configuring-tracking-for-a-workflow.md)및 [ &#91;WF&#93; 샘플 추적](../../../../docs/framework/windows-workflow-foundation/samples/tracking.md) 샘플을 참조 하세요.

## <a name="use-wcf-tracing"></a>WCF 추적 사용
 WCF 추적은 워크플로 서비스 간의 메시지 흐름에 대한 추적을 제공합니다. 이 추적 정보는 상관 관계 문제, 특히 내용 기반 상관 관계 문제를 해결하는 데 유용합니다. 추적을 사용하도록 설정하려면 `system.diagnostics` 파일(워크플로 서비스가 웹 호스팅 서비스인 경우) 또는 `web.config` 파일(워크플로 서비스가 자체 호스팅 서비스인 경우)의 `app.config` 섹션에서 원하는 추적 수신기를 지정합니다. 메시지의 내용을 추적 파일에 포함하려면 `true`의 `logEntireMessage` 섹션에 있는 `messageLogging` 요소에서 `diagnostics`에 `system.serviceModel`를 지정합니다. 다음 예제에서는 메시지 내용을 포함한 추적 정보를 `service.svclog`라는 파일에 기록하도록 구성합니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.diagnostics>
    <sources>
      <source name="System.ServiceModel" switchValue="Information" propagateActivity="true">
        <listeners>
          <add name="corr"/>
        </listeners>
      </source>
      <source name="System.ServiceModel.MessageLogging">
        <listeners>
          <add name="corr"/>
        </listeners>
      </source>
    </sources>

    <sharedListeners>
      <add name="corr" type="System.Diagnostics.XmlWriterTraceListener" initializeData="c:\logs\service.svclog">
      </add>
    </sharedListeners>
  </system.diagnostics>

  <system.serviceModel>
    <diagnostics>
      <messageLogging logEntireMessage="true" logMalformedMessages="false"
         logMessagesAtServiceLevel="false" logMessagesAtTransportLevel="true" maxSizeOfMessageToLog="2147483647">
      </messageLogging>
    </diagnostics>
  </system.serviceModel>
</configuration>
```

 @No__t-0에 포함 된 추적 정보를 보려면 [서비스 추적 뷰어 도구 (svctraceviewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md) 를 사용 합니다. 이 도구를 사용하면 메시지 내용을 볼 수 있을 뿐 아니라 내용 기반 상관 관계의 경우 전달되는 정확한 정보와 해당 정보가<xref:System.ServiceModel.CorrelationQuery>와 일치하는지 여부를 확인할 수 있으므로 내용 기반 상관 관계의 문제를 해결하는 데 특히 유용합니다. WCF 추적에 대 한 자세한 내용은 [서비스 추적 뷰어 도구 (svctraceviewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md), [추적 구성](../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md)및 추적을 사용 하 여 [응용 프로그램 문제 해결](../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)을 참조 하세요.

## <a name="common-context-exchange-correlation-issues"></a>일반적인 컨텍스트 교환 상관 관계 문제
 일부 형식의 상관 관계에서는 특정 형식의 바인딩을 사용해야 상관 관계가 올바르게 작동합니다. 예제에는 <xref:System.ServiceModel.BasicHttpBinding> 같은 양방향 바인딩이 필요한 요청-회신 상관 관계와 <xref:System.ServiceModel.BasicHttpContextBinding> 같은 컨텍스트 기반 바인딩이 필요한 컨텍스트 교환 상관 관계가 포함되어 있습니다. 대부분의 바인딩은 양방향 작업을 지원하므로 요청-회신 상관 관계의 경우에는 이러한 사항이 일반적인 문제가 아니지만, 컨텍스트 기반 바인딩은 <xref:System.ServiceModel.BasicHttpContextBinding>, <xref:System.ServiceModel.WSHttpContextBinding> 및 <xref:System.ServiceModel.NetTcpContextBinding>을 비롯한 일부만 있습니다. 이러한 바인딩 중 하나를 사용하지 않으면 워크플로 서비스에 대한 초기 호출은 성공하지만 후속 호출은 다음 <xref:System.ServiceModel.FaultException>과 함께 실패합니다.

```output
There is no context attached to the incoming message for the service
and the current operation is not marked with "CanCreateInstance = true".
In order to communicate with this service check whether the incoming binding
supports the context protocol and has a valid context initialized.
```

 컨텍스트 상관 관계에 사용되는 컨텍스트 정보는 <xref:System.ServiceModel.Activities.SendReply>에 의해 컨텍스트 상관 관계를 초기화하는 <xref:System.ServiceModel.Activities.Receive> 활동에 반환되거나(양방향 작업을 사용할 경우) 호출자에 의해 지정될 수 있습니다(단방향 작업을 사용할 경우). 컨텍스트를 호출자가 보내지 않거나 워크플로 서비스에서 반환하지 않는 경우에는 후속 작업이 호출될 때 위에서 설명한 것과 동일한 <xref:System.ServiceModel.FaultException>이 반환됩니다.

## <a name="common-request-reply-correlation-issues"></a>일반적인 요청-회신 상관 관계 문제
 요청-회신 상관 관계는 워크플로 서비스에서 양방향 작업을 구현 하 고 다른 웹 서비스에서 양방향 작업을 호출 하는 <xref:System.ServiceModel.Activities.Send> @ no__t-4 @ no__t-5 쌍을 사용 하 여 <xref:System.ServiceModel.Activities.Receive> @ no__t-1 @ no__t-2 쌍과 함께 사용 됩니다. WCF 서비스에서 양방향 작업을 호출 하는 경우 서비스는 기존 명령적 코드 기반 WCF 서비스 이거나 워크플로 서비스 일 수 있습니다. 요청-회신 상관 관계를 사용하려면 <xref:System.ServiceModel.BasicHttpBinding> 같은 양방향 바인딩을 사용해야 하며 작업이 양방향이어야 합니다.

 워크플로 서비스에서 양방향 작업을 병렬로 수행 하거나 <xref:System.ServiceModel.Activities.Receive> @ no__t-1 @ no__t 또는 <xref:System.ServiceModel.Activities.Send> @ no__t-4 쌍을 겹치는 경우에는 <xref:System.ServiceModel.Activities.WorkflowServiceHost>에서 제공 하는 암시적 상관 관계 핸들 관리가 충분 하지 않을 수 있습니다. 특히 스트레스가 높습니다. 시나리오와 메시지는 제대로 라우팅되지 않을 수 있습니다. 이 문제를 방지하려면 요청-회신 상관 관계를 사용할 때 항상 <xref:System.ServiceModel.Activities.CorrelationHandle>을 명시적으로 지정하는 것이 좋습니다. Workflow designer의 **도구 상자** 에 있는 메시징 섹션에서 **SendAndReceiveReply** 및 **ReceiveAndSendReply** 템플릿을 사용 하면 기본적으로 <xref:System.ServiceModel.Activities.CorrelationHandle>이 명시적으로 구성 됩니다. 코드를 사용하여 워크플로를 바인딩하는 경우 <xref:System.ServiceModel.Activities.CorrelationHandle>은 쌍의 첫 번째 활동에 대한 <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A>에서 지정됩니다. 다음 예제에서는 <xref:System.ServiceModel.Activities.Receive>에 <xref:System.ServiceModel.Activities.CorrelationInitializer.CorrelationHandle%2A>을 명시적으로 지정하여 <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> 활동을 구성합니다.

```csharp
Variable<CorrelationHandle> RRHandle = new Variable<CorrelationHandle>();

Receive StartOrder = new Receive
{
    CanCreateInstance = true,
    ServiceContractName = OrderContractName,
    OperationName = "StartOrder",
    CorrelationInitializers =
    {
        new RequestReplyCorrelationInitializer
        {
            CorrelationHandle = RRHandle
        }
    }
};

SendReply ReplyToStartOrder = new SendReply
{
    Request = StartOrder,
    Content = ... // Contains the return value, if any.
};

// Construct a workflow using StartOrder and ReplyToStartOrder.
```

 @No__t-0 @ no__t-1 @ no__t-2 쌍 또는 <xref:System.ServiceModel.Activities.Send> @ no__t-4 @ no__t-5 쌍 사이에는 지 속성이 허용 되지 않습니다. 두 활동이 모두 완료될 때까지 유지되는 비지속성 영역이 만들어집니다. 지연 활동과 같은 활동이 이 비지속성 영역에 있고 워크플로가 유휴 상태가 되도록 하는 경우 워크플로가 유휴 상태가 될 때 워크플로를 유지하도록 호스트를 구성한 경우에도 워크플로가 유지되지 않습니다. 유지 활동과 같은 활동이 비지속성 영역에 명시적으로 유지하려고 하는 경우 치명적 예외가 throw되고 워크플로가 중단되며 <xref:System.ServiceModel.FaultException>이 호출자에게 반환됩니다. 심각한 예외 메시지는 "InvalidOperationException: 지속 활동은 지 속성 블록 내에 포함 될 수 없습니다. " 이 예외는 호출자에게 반환되지 않지만 추적을 사용하는 경우 나타날 수 있습니다. 호출자에게 반환되는 <xref:System.ServiceModel.FaultException> 메시지는 "WorkflowInstance '5836145b-7da2-49d0-a052-a49162adeab6'이(가) 완료되었으므로 작업을 수행할 수 없습니다."입니다.

 요청-회신 상관 관계에 대 한 자세한 내용은 [request-reply](../../../../docs/framework/wcf/feature-details/request-reply-correlation.md)를 참조 하세요.

## <a name="common-content-correlation-issues"></a>일반적인 내용 상관 관계 문제
 내용 기반 상관 관계는 워크플로 서비스에서 여러 개의 메시지를 받으며 교환되는 메시지의 일부 데이터로 원하는 인스턴스를 식별할 수 있는 경우에 사용됩니다. 내용 기반 상관 관계는 메시지에 있는 이 데이터(예: 고객 번호 또는 주문 ID)를 사용하여 메시지를 올바른 워크플로 인스턴스에 라우트합니다. 이 단원에서는 내용 기반 상관 관계를 사용할 때 발생할 수 있는 몇 가지 일반적인 문제를 설명합니다.

### <a name="ensure-the-identifying-data-is-unique"></a>식별 데이터가 고유한지 확인
 인스턴스를 식별하는 데 사용되는 데이터는 상관 관계 키로 해시됩니다. 상관 관계에는 고유한 데이터를 사용해야 합니다. 그렇지 않으면 해시된 키에서 충돌이 발생하여 메시지가 잘못 라우트될 수 있습니다. 예를 들어 동일한 이름을 가진 고객이 여러 명 있을 수 있으므로 고객 이름에만 의존하는 상관 관계는 충돌을 일으킬 수 있습니다. 메시지를 연결하는 데 사용되는 데이터에 콜론(:)을 포함하면 안 됩니다. 이는 이후에 해시되는 문자열을 만들기 위해 메시지 쿼리의 키와 값을 구분하는 데 콜론이 이미 사용되기 때문입니다. 지속성이 사용되는 경우 현재 식별 데이터가 이전에 유지된 인스턴스에서 사용되지 않았는지 확인합니다. 지속성을 임시로 사용하지 않도록 설정하면 이 문제를 손쉽게 식별할 수 있습니다. WCF 추적은 계산된 상관 관계 키를 확인하는 데 사용할 수 있으며 이 종류의 문제를 디버깅하는 데 유용합니다.

### <a name="race-conditions"></a>경합 조건
 서비스에서 메시지를 받는 시간과 상관 관계가 실제로 초기화되는 시간 사이에는 약간의 시간 차가 있으며 그 동안 후속 메시지는 무시됩니다. 워크플로 서비스에서 단방향 작업을 통해 클라이언트에서 전달된 데이터를 사용하여 내용 기반 상관 관계를 초기화하고 호출자가 즉시 후속 메시지를 보내는 경우 이러한 후속 메시지는 이 간격 동안 무시됩니다. 양방향 작업을 사용하여 상관 관계를 초기화하거나 <xref:System.ServiceModel.Activities.TransactedReceiveScope>를 사용하면 이 문제를 방지할 수 있습니다.

### <a name="correlation-query-issues"></a>상관 관계 쿼리 문제
 상관 관계 쿼리는 메시지를 상호 연결하는 데 사용되는 메시지 데이터를 지정하는 데 사용됩니다. 이 데이터는 XPath 쿼리를 사용하여 지정합니다. 모든 사항이 올바른 것으로 보이는데도 서비스로 보내는 메시지가 디스패치되지 않을 경우 문제를 해결하는 한 가지 방법은 XPath 쿼리 대신 메시지 데이터의 값과 일치하는 리터럴 값을 지정하는 것입니다. 리터럴 값을 지정하려면 `string` 함수를 사용합니다. 다음 예제에서는 <xref:System.ServiceModel.MessageQuerySet>에 리터럴 값 `11445`를 사용하도록 `OrderId`을 구성하고 XPath 쿼리를 주석 처리합니다.

```csharp
MessageQuerySet = new MessageQuerySet
{
    {
        "OrderId",
        //new XPathMessageQuery("sm:body()/tempuri:StartOrderResponse/tempuri:OrderId")
        new XPathMessageQuery("string('11445')")
    }
}
```

 상관 관계 데이터가 검색 되지 않도록 XPath 쿼리가 잘못 구성 된 경우 다음 메시지와 함께 오류가 반환 됩니다. "상관 관계 쿼리가 빈 결과 집합을 생성 했습니다. 엔드포인트에 대해 상관 관계 쿼리가 올바르게 구성되었는지 확인하세요."라는 메시지와 함께 오류가 반환됩니다. 이 문제를 신속하게 해결하는 한 가지 방법은 이전 단원에서 설명한 대로 XPath 쿼리를 리터럴 값으로 바꾸는 것입니다. **상관 관계 이니셜라이저 추가** 또는 **CorrelatesOn 정의** 대화 상자에서 XPath 쿼리 작성기를 사용 하 고 워크플로 서비스에서 메시지 계약을 사용 하는 경우이 문제가 발생할 수 있습니다. 다음 예제에서는 메시지 계약 클래스를 정의합니다.

```csharp
[MessageContract]
public class AddItemMessage
{
    [MessageHeader]
    public string CartId;

    [MessageBodyMember]
    public string Item;
}
```

 이 메시지 계약은 워크플로의 <xref:System.ServiceModel.Activities.Receive> 활동에서 사용됩니다. 메시지 헤더의 `CartId`는 메시지를 올바른 인스턴스와 상호 연결하는 데 사용됩니다. `CartId`를 검색하는 XPath 쿼리가 워크플로 디자이너의 상관 관계 대화 상자를 사용하여 만들어지는 경우 다음과 같은 잘못된 XPath 쿼리가 생성됩니다.

```
sm:body()/xg0:AddItemMessage/xg0:CartId
```

 <xref:System.ServiceModel.Activities.Receive> 활동이 데이터에 대한 매개 변수를 사용한다면 이 XPath 쿼리가 올바르지만 이 활동이 메시지 계약을 사용하므로 올바르지 않습니다. 다음 XPath 쿼리는 헤더에서 `CartId`를 검색하는 올바른 XPath 쿼리입니다.

```
sm:header()/tempuri:CartId
```

이는 메시지 본문을 검사하여 확인할 수 있습니다.

```xml
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
  <s:Header>
    <Action s:mustUnderstand="1" xmlns="http://schemas.microsoft.com/ws/2005/05/addressing/none">http://tempuri.org/IService/AddItem</Action>
    <h:CartId xmlns:h="http://tempuri.org/">80c95b41-c98d-4660-a6c1-99412206e54c</h:CartId>
  </s:Header>
  <s:Body>
    <AddItemMessage xmlns="http://tempuri.org/">
      <Item>Books</Item>
    </AddItemMessage>
  </s:Body>
</s:Envelope>
```

다음 예제에서는 이전 메시지 계약을 사용하여 데이터를 받는 <xref:System.ServiceModel.Activities.Receive> 작업에 대해 구성된 `AddItem` 활동을 보여 줍니다. XPath 쿼리는 올바르게 구성되어 있습니다.

```xaml
<Receive CorrelatesWith="[CCHandle] OperationName="AddItem" ServiceContractName="p:IService">
  <Receive.CorrelatesOn>
    <XPathMessageQuery x:Key="key1">
      <XPathMessageQuery.Namespaces>
        <ssx:XPathMessageContextMarkup>
          <x:String x:Key="xg0">http://schemas.datacontract.org/2004/07/MessageContractWFService</x:String>
        </ssx:XPathMessageContextMarkup>
      </XPathMessageQuery.Namespaces>sm:header()/tempuri:CartId</XPathMessageQuery>
  </Receive.CorrelatesOn>
  <ReceiveMessageContent DeclaredMessageType="m:AddItemMessage">
    <p1:OutArgument x:TypeArguments="m:AddItemMessage">[AddItemMessage]</p1:OutArgument>
  </ReceiveMessageContent>
</Receive>
```
