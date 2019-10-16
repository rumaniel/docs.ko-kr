---
title: 청크 채널
ms.date: 03/30/2017
ms.assetid: e4d53379-b37c-4b19-8726-9cc914d5d39f
ms.openlocfilehash: 6bd7f1f31426c2d355b42f04ad770aac60183838
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70990109"
---
# <a name="chunking-channel"></a>청크 채널

WCF (Windows Communication Foundation)를 사용 하 여 대용량 메시지를 보내는 경우 해당 메시지를 버퍼링 하는 데 사용 되는 메모리 양을 제한 하는 것이 좋습니다. 가능한 한 가지 솔루션은 본문에 대량의 데이터가 있다고 가정하고 메시지 본문을 스트리밍하는 것입니다. 그러나 일부 프로토콜에서는 전체 메시지를 버퍼링해야 합니다. 이와 같은 두 가지 예로 신뢰할 수 있는 메시징과 보안을 들 수 있습니다. 가능한 또 다른 솔루션은 큰 메시지를 청크라는 더 작은 메시지로 나누고 이러한 청크를 한 번에 하나씩 보낸 다음 받는 쪽에서 큰 메시지를 다시 구성하는 것입니다. 애플리케이션은 이 청크 및 청크 취소를 직접 수행하거나 사용자 지정 채널을 사용하여 수행할 수 있습니다. 이 Chunking Channel 샘플에서는 사용자 지정 프로토콜이나 계층화된 채널을 사용하여 임의 크기의 메시지를 청크 및 청크 취소하는 방법을 보여 줍니다.

청크는 항상 보낼 전체 메시지를 생성한 후에만 사용해야 합니다. 청크 채널은 항상 보안 채널 및 신뢰할 수 있는 세션 채널 아래에 계층화되어야 합니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Channels\ChunkingChannel`

## <a name="chunking-channel-assumptions-and-limitations"></a>청크 채널 가정 및 제한 사항

### <a name="message-structure"></a>메시지 구조

청크 채널에서는 청크할 메시지에 대해 다음 메시지 구조를 가정합니다.

```xml
<soap:Envelope ...>
  <!-- headers -->
  <soap:Body>
    <operationElement>
      <paramElement>data to be chunked</paramElement>
    </operationElement>
  </soap:Body>
</soap:Envelope>
```

ServiceModel을 사용하는 경우 입력 매개 변수가 하나인 계약 작업은 입력 메시지에 이 메시지 형식을 사용합니다. 마찬가지로 출력 매개 변수나 반환 값이 하나인 계약 작업은 출력 메시지에 이 메시지 형식을 사용합니다. 다음은 이러한 작업의 예입니다.

```csharp
[ServiceContract]
interface ITestService
{
    [OperationContract]
    Stream EchoStream(Stream stream);

    [OperationContract]
    Stream DownloadStream();

    [OperationContract(IsOneWay = true)]
    void UploadStream(Stream stream);
}
```

### <a name="sessions"></a>세션

청크 채널에서는 메시지(청크)가 배달 순서를 유지하면서 한 번에 배달되어야 합니다. 이는 기본 채널 스택이 세션 채널 스택이어야 한다는 것을 의미합니다. 세션은 전송(예: TCP 전송)에 의해 제공되거나 세션 프로토콜 채널(예: ReliableSession 채널)에 의해 제공될 수 있습니다.

### <a name="asynchronous-send-and-receive"></a>비동기 발신 및 수신

비동기 발신 및 수신 메서드는 이 버전의 Chunking Channel 샘플에서 구현되지 않습니다.

## <a name="chunking-protocol"></a>청크 프로토콜

청크 채널은 연속된 청크의 시작 및 끝과 각 청크의 시퀀스 번호를 나타내는 프로토콜을 정의합니다. 다음 세 개의 예제 메시지는 시작, 청크 및 끝 메시지를 보여 주며 각각의 주요 특성을 설명하는 주석을 제공합니다.

### <a name="start-message"></a>시작 메시지

```xml
<s:Envelope xmlns:a="http://www.w3.org/2005/08/addressing"
            xmlns:s="http://www.w3.org/2003/05/soap-envelope">
  <s:Header>
<!--Original message action is replaced with a chunking-specific action. -->
    <a:Action s:mustUnderstand="1">http://samples.microsoft.com/chunkingAction</a:Action>
<!--
Original message is assigned a unique id that is transmitted
in a MessageId header. Note that this is different from the WS-Addressing MessageId header.
-->
    <MessageId s:mustUnderstand="1" xmlns="http://samples.microsoft.com/chunking">
53f183ee-04aa-44a0-b8d3-e45224563109
</MessageId>
<!--
ChunkingStart header signals the start of a chunked message.
-->
    <ChunkingStart s:mustUnderstand="1" i:nil="true" xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://samples.microsoft.com/chunking" />
<!--
Original message action is transmitted in OriginalAction.
This is required to re-create the original message on the other side.
-->
    <OriginalAction xmlns="http://samples.microsoft.com/chunking">
http://tempuri.org/ITestService/EchoStream
    </OriginalAction>
   <!--
    All original message headers are included here.
   -->
  </s:Header>
  <s:Body>
<!--
Chunking assumes this structure of Body content:
<element>
  <childelement>large data to be chunked<childelement>
</element>
The start message contains just <element> and <childelement> without
the data to be chunked.
-->
    <EchoStream xmlns="http://tempuri.org/">
      <stream />
    </EchoStream>
  </s:Body>
</s:Envelope>
```

### <a name="chunk-message"></a>청크 메시지

```xml
<s:Envelope
  xmlns:a="http://www.w3.org/2005/08/addressing"
  xmlns:s="http://www.w3.org/2003/05/soap-envelope">
  <s:Header>
   <!--
    All chunking protocol messages have this action.
   -->
    <a:Action s:mustUnderstand="1">
      http://samples.microsoft.com/chunkingAction
    </a:Action>
<!--
Same as MessageId in the start message. The GUID indicates which original message this chunk belongs to.
-->
    <MessageId s:mustUnderstand="1"
               xmlns="http://samples.microsoft.com/chunking">
      53f183ee-04aa-44a0-b8d3-e45224563109
    </MessageId>
<!--
The sequence number of the chunk.
This number restarts at 1 with each new sequence of chunks.
-->
    <ChunkNumber s:mustUnderstand="1"
                 xmlns="http://samples.microsoft.com/chunking">
      1096
    </ChunkNumber>
  </s:Header>
  <s:Body>
<!--
The chunked data is wrapped in a chunk element.
The encoding of this data (and the entire message)
depends on the encoder used. The chunking channel does not mandate an encoding.
-->
    <chunk xmlns="http://samples.microsoft.com/chunking">
kfSr2QcBlkHTvQ==
    </chunk>
  </s:Body>
</s:Envelope>
```

### <a name="end-message"></a>끝 메시지

```xml
<s:Envelope xmlns:a="http://www.w3.org/2005/08/addressing"
            xmlns:s="http://www.w3.org/2003/05/soap-envelope">
  <s:Header>
    <a:Action s:mustUnderstand="1">
      http://samples.microsoft.com/chunkingAction
    </a:Action>
<!--
Same as MessageId in the start message. The GUID indicates which original message this chunk belongs to.
-->
    <MessageId s:mustUnderstand="1"
               xmlns="http://samples.microsoft.com/chunking">
      53f183ee-04aa-44a0-b8d3-e45224563109
    </MessageId>
<!--
ChunkingEnd header signals the end of a chunk sequence.
-->
    <ChunkingEnd s:mustUnderstand="1" i:nil="true"
                 xmlns:i="http://www.w3.org/2001/XMLSchema-instance"
                 xmlns="http://samples.microsoft.com/chunking" />
<!--
ChunkingEnd messages have a sequence number.
-->
    <ChunkNumber s:mustUnderstand="1"
                 xmlns="http://samples.microsoft.com/chunking">
      79
    </ChunkNumber>
  </s:Header>
  <s:Body>
<!--
The ChunkingEnd message has the same <element><childelement> structure
as the ChunkingStart message.
-->
    <EchoStream xmlns="http://tempuri.org/">
      <stream />
    </EchoStream>
  </s:Body>
</s:Envelope>
```

## <a name="chunking-channel-architecture"></a>청크 채널 아키텍처

청크 채널은 상위 수준에서 일반적인 채널 아키텍처를 따르는 `IDuplexSessionChannel`입니다. `ChunkingBindingElement` 및 `ChunkingChannelFactory`를 빌드할 수 있는 `ChunkingChannelListener`가 있습니다. `ChunkingChannelFactory`는 요청을 받은 경우 `ChunkingChannel`의 인스턴스를 만듭니다. `ChunkingChannelListener`는 새 내부 채널이 수락된 경우 `ChunkingChannel`의 인스턴스를 만듭니다. `ChunkingChannel` 자체는 메시지를 보내고 받는 작업을 담당합니다.

다음 하위 수준에서 `ChunkingChannel`은 서버 구성 요소에 의존하여 청크 프로토콜을 구현합니다. 보내는 쪽에서 채널은 실제 청크를 수행하는 <xref:System.Xml.XmlDictionaryWriter>라는 사용자 지정 `ChunkingWriter`를 사용합니다. `ChunkingWriter`는 내부 채널을 직접 사용하여 청크를 보냅니다. 사용자 지정 `XmlDictionaryWriter`를 사용하면 원본 메시지의 큰 본문이 기록될 때 청크를 보낼 수 있습니다. 이는 전체 원본 메시지를 버퍼링하지 않는다는 것을 의미합니다.

![청크 채널 송신 아키텍처를 보여 주는 다이어그램입니다.](./media/chunking-channel/chunking-channel-send.gif)

받는 쪽 `ChunkingChannel`은 내부 채널의 메시지를 끌어와 <xref:System.Xml.XmlDictionaryReader>라는 사용자 지정 `ChunkingReader`에 전달하여 들어오는 청크로부터 원본 메시지를 다시 구성합니다. `ChunkingChannel`은 `ChunkingReader`라는 사용자 지정 `Message` 구현에서 이 `ChunkingMessage`를 래핑하고 이 메시지를 위 계층에 반환합니다. 이렇게 `ChunkingReader`와 `ChunkingMessage`를 함께 사용하면 전체 원본 메시지 본문을 버퍼링하는 대신 위 계층에서 읽을 때 원본 메시지 본문의 청크를 취소할 수 있습니다. `ChunkingReader`에는 구성 가능한 최대 버퍼링된 청크 수까지 들어오는 청크를 버퍼링하는 큐가 있습니다. 이 최대 한도에 도달하면 판독기는 위 계층에서 원본 메시지 본문을 읽어서 큐의 메시지가 비워지기를 기다리거나 최대 수신 시간 제한에 도달할 때까지 기다립니다.

![청크 채널 수신 아키텍처를 보여 주는 다이어그램입니다.](./media/chunking-channel/chunking-channel-receive.gif)

## <a name="chunking-programming-model"></a>청크 프로그래밍 모델

서비스 개발자는 `ChunkingBehavior` 특성을 계약 내의 작업에 적용하여 청크할 메시지를 지정할 수 있습니다. 이 특성은 청크를 입력 메시지, 출력 메시지 또는 둘 다에 적용할지 여부를 개발자가 지정할 수 있게 하는 `AppliesTo` 속성을 노출합니다. 다음 예제에서는 `ChunkingBehavior` 특성의 사용법을 보여 줍니다.

```csharp
[ServiceContract]
interface ITestService
{
    [OperationContract]
    [ChunkingBehavior(ChunkingAppliesTo.Both)]
    Stream EchoStream(Stream stream);

    [OperationContract]
    [ChunkingBehavior(ChunkingAppliesTo.OutMessage)]
    Stream DownloadStream();

    [OperationContract(IsOneWay=true)]
    [ChunkingBehavior(ChunkingAppliesTo.InMessage)]
    void UploadStream(Stream stream);

}
```

이 프로그래밍 모델에서 `ChunkingBindingElement`는 청크할 메시지를 식별하는 동작 URI 목록을 컴파일합니다. 보내는 각 메시지의 동작을 이 목록과 비교하여 메시지를 청크해야 할지 직접 보내야 할지를 결정합니다.

## <a name="implementing-the-send-operation"></a>Send 작업 구현

상위 수준에서 Send 작업은 보내는 메시지를 청크해야 하는지 먼저 확인하고 그럴 필요가 없는 경우 내부 채널을 사용하여 메시지를 직접 보냅니다.

메시지를 청크해야 할 경우 Send는 새 `ChunkingWriter`를 만들고 보내는 메시지에서 `WriteBodyContents`를 호출하여 이 `ChunkingWriter`를 전달합니다. 그런 다음 `ChunkingWriter`는 메시지 청크(원본 메시지 헤더를 시작 청크 메시지에 복사하는 작업 포함)를 수행하고 내부 채널을 사용하여 청크를 보냅니다.

주목할 만한 몇 가지 세부 사항은 다음과 같습니다.

- Send는 `ThrowIfDisposedOrNotOpened`가 Opened인지 확인하기 위해 먼저 `CommunicationState`를 호출합니다.

- 보내기는 동기화되므로 각 세션에 대해 한 번에 하나의 메시지만 보낼 수 있습니다. 청크된 메시지를 보낼 때 다시 설정되는 `ManualResetEvent`이라는 `sendingDone`가 있습니다. 끝 청크 메시지가 보내지고 나면 이 이벤트가 설정됩니다. Send 메서드는 보내는 메시지를 보내려고 시도하기 전에 이 이벤트가 설정되기를 기다립니다.

- Send는 보내는 도중 동기화된 상태 변경을 방지하기 위해 `CommunicationObject.ThisLock`을 잠급니다. <xref:System.ServiceModel.Channels.CommunicationObject> 상태 및 상태 시스템에 대한 자세한 내용은 <xref:System.ServiceModel.Channels.CommunicationObject> 설명서를 참조하세요.

- Send에 전달되는 시간 제한은 모든 청크의 보내기를 포함하는 전체 Send 작업의 시간 제한으로 사용됩니다.

- 전체 원본 메시지 본문의 버퍼링을 방지하기 위해 사용자 지정 <xref:System.Xml.XmlDictionaryWriter> 디자인이 선택되었습니다. <xref:System.Xml.XmlDictionaryReader>를 사용하여 본문에서 `message.GetReaderAtBodyContents`를 가져올 경우에는 전체 본문이 버퍼링됩니다. 대신에 <xref:System.Xml.XmlDictionaryWriter> `message.WriteBodyContents`전달 되는 사용자 지정이 있습니다. 메시지가 작성기에서 WriteBase64를 호출할 경우 작성기는 청크를 메시지에 패키지하고 내부 채널을 사용하여 보냅니다. 청크가 보내질 때까지 WriteBase64는 차단됩니다.

## <a name="implementing-the-receive-operation"></a>Receive 작업 구현

상위 수준에서 Receive 작업은 먼저 들어오는 메시지가 `null`이 아니고 해당 동작이 `ChunkingAction`인지 확인합니다. 두 조건을 충족하지 않을 경우 메시지는 Receive에서 변경되지 않은 상태로 반환됩니다. 두 조건을 충족할 경우 Receive는 새 `ChunkingReader`와 `ChunkingMessage`를 호출하여 이를 래핑하는 새 `GetNewChunkingMessage` 메시지를 만듭니다. 새 `ChunkingMessage`를 반환하기 전에 Receive는 threadpool 스레드를 사용하여 `ReceiveChunkLoop`를 실행합니다. 따라서 끝 청크 메시지가 수신되거나 수신 시간 제한에 도달할 때까지 루프에서 `innerChannel.Receive`가 호출되고 `ChunkingReader`에 청크가 보내집니다.

주목할 만한 몇 가지 세부 사항은 다음과 같습니다.

- Send와 마찬가지로 Receive는 `ThrowIfDisposedOrNotOepned`가 Opened인지 확인하기 위해 먼저 `CommunicationState`를 호출합니다.

- 또한 Receive는 동기화되므로 세션에서 한 번에 하나의 메시지만 수신할 수 있습니다. 시작 청크 메시지가 수신되고 나면 끝 청크 메시지가 수신될 때까지 수신되는 이후의 모든 메시지가 청크로 간주되므로 이 기능이 특히 중요합니다. 현재 청크 취소하는 중인 메시지에 속하는 모든 청크가 수신될 때까지 Receive는 내부 채널에서 메시지를 끌어올 수 없습니다. 이를 위해 Receive는 끝 청크 메시지가 수신될 때 설정되고 새 시작 청크 메시지가 수신될 때 다시 설정되는 `ManualResetEvent`라는 `currentMessageCompleted`를 사용합니다.

- Send와 달리 Receive에서는 동기화된 상태 전환이 수신 중에 허용됩니다. 예를 들어, Close가 수신 중에 호출되어 원본 메시지의 보류 중인 수신이 완료되거나 지정된 시간 제한 값에 도달할 때까지 대기할 수 있습니다.

- Receive에 전달되는 시간 제한은 모든 청크의 수신을 포함하는 전체 Receive 작업의 시간 제한으로 사용됩니다.

- 메시지를 소비하는 계층이 들어오는 청크 메시지의 속도보다 느린 속도로 메시지 본문을 소비하는 중이면 `ChunkingReader`는 `ChunkingBindingElement.MaxBufferedChunks`에 지정된 한도까지 이러한 들어오는 청크를 버퍼링합니다. 해당 한도에 도달하고 나면 버퍼링된 청크가 소비되거나 수신 시간 제한에 도달할 때까지 청크를 더 이상 하위 계층에서 끌어오지 않습니다.

## <a name="communicationobject-overrides"></a>CommunicationObject 재정의

### <a name="onopen"></a>OnOpen

`OnOpen`은 `innerChannel.Open`을 호출하여 내부 채널을 엽니다.

### <a name="onclose"></a>OnClose

`OnClose`는 먼저 `stopReceive`를 `true`로 설정하여 보류 중인 `ReceiveChunkLoop`를 중지할 것을 알립니다. 그런 다음이 중지 될 `receiveStopped` 때 `ReceiveChunkLoop` 설정 되는 <xref:System.Threading.ManualResetEvent>을 기다립니다. `ReceiveChunkLoop`가 지정된 시간 제한 내에 중지한다고 가정하고 `OnClose`는 남은 시간 제한을 사용하여 `innerChannel.Close`를 호출합니다.

### <a name="onabort"></a>OnAbort

`OnAbort`는 `innerChannel.Abort`를 호출하여 내부 채널을 중단합니다. 보류 중인 `ReceiveChunkLoop`가 있을 경우 보류 중인 `innerChannel.Receive` 호출에서 예외를 가져옵니다.

### <a name="onfaulted"></a>OnFaulted

채널에 오류가 발생하여 `ChunkingChannel`가 재정의되지 않을 경우 `OnFaulted`에는 특수한 동작이 필요하지 않습니다.

## <a name="implementing-channel-factory"></a>채널 팩터리 구현

`ChunkingChannelFactory`는 `ChunkingDuplexSessionChannel`의 인스턴스를 만들고 내부 채널 팩터리에 상태 전환을 적용하는 작업을 담당합니다.

`OnCreateChannel`은 내부 채널 팩터리를 사용하여 `IDuplexSessionChannel` 내부 채널을 만듭니다. 그런 다음 새 `ChunkingDuplexSessionChannel`을 만들어 청크할 메시지 동작 목록 및 수신 시에 버퍼링할 최대 청크 수와 함께 이 내부 채널을 전달합니다. 이 생성자의 `ChunkingChannelFactory`에 전달되는 두 개의 매개 변수는 청크할 메시지 동작 목록 및 버퍼링할 최대 청크 수입니다. `ChunkingBindingElement` 관련 단원에서 이러한 값의 출처에 대해 설명합니다.

`OnOpen`, `OnClose`, `OnAbort` 및 동등한 해당 비동기 항목은 내부 채널 팩터리에서 해당 상태 전환 메서드를 호출합니다.

## <a name="implementing-channel-listener"></a>채널 수신기 구현

`ChunkingChannelListener`는 내부 채널 수신기에 대한 래퍼입니다. 해당 내부 수신기에 대한 대리자 호출 외에 이 래퍼의 기본 기능은 내부 채널 수신기에서 받은 채널 주위에 새 `ChunkingDuplexSessionChannels`를 래핑하는 것입니다. 이 작업은 `OnAcceptChannel` 및 `OnEndAcceptChannel`에서 수행됩니다. 새로 만든 `ChunkingDuplexSessionChannel`에는 위에 설명된 다른 매개 변수와 함께 내부 채널이 전달됩니다.

## <a name="implementing-binding-element-and-binding"></a>바인딩 요소 및 바인딩 구현

`ChunkingBindingElement`는 `ChunkingChannelFactory` 및 `ChunkingChannelListener`를 만드는 작업을 담당합니다. 는 `ChunkingBindingElement` t > 및 `CanBuildChannelFactory` t>`CanBuildChannelListener`의 \<t가 형식 `IDuplexSessionChannel` (청크 채널에서 지 원하는 유일한 채널)이 고 바인딩의 다른 바인딩 요소가이를 지원 하는지 확인 합니다. \< 채널 유형입니다.

`BuildChannelFactory`\<T >은 요청 된 채널 형식을 생성할 수 있는지 먼저 확인 한 다음 청크 할 메시지 동작 목록을 가져옵니다. 자세한 내용은 다음 단원을 참조하세요. 그런 다음 새 `ChunkingChannelFactory`를 만들어 내부 채널 팩터리(`context.BuildInnerChannelFactory<IDuplexSessionChannel>`에서 반환), 메시지 동작 목록 및 버퍼링할 최대 청크 수를 전달합니다. 최대 청크 수는 `MaxBufferedChunks`에 의해 노출되는 `ChunkingBindingElement`라는 속성에서 제공됩니다.

`BuildChannelListener<T>`에서도 `ChunkingChannelListener`를 만들어 내부 채널 수신기에 전달하는 구현 방법이 비슷합니다.

이 샘플에는 `TcpChunkingBinding`이라는 예제 바인딩이 포함되어 있습니다. 이 바인딩은 두 개의 바인딩 요소인 `TcpTransportBindingElement` 및 `ChunkingBindingElement`로 구성됩니다. `MaxBufferedChunks` 속성을 노출하는 것 외에도 이 바인딩은 `TcpTransportBindingElement`(헤더에 대해 `MaxReceivedMessageSize` + 100KB로 설정)와 같은 일부 `ChunkingUtils.ChunkSize` 속성을 설정합니다.

또한 `TcpChunkingBinding`은 `IBindingRuntimePreferences`를 구현하고 동기 Receive 호출만 구현된다는 것을 나타내는 `ReceiveSynchronously` 메서드에서 true를 반환합니다.

### <a name="determining-which-messages-to-chunk"></a>청크할 메시지 결정

청크 채널은 `ChunkingBehavior` 특성을 통해 식별된 메시지만 청크합니다. `ChunkingBehavior` 클래스는 `IOperationBehavior`를 구현하며 `AddBindingParameter` 메서드 호출에 의해 구현됩니다. 이 메서드에서 `ChunkingBehavior`는 해당 `AppliesTo` 속성의 값(`InMessage`, `OutMessage` 또는 둘 다)을 확인하여 청크해야 하는 메시지를 결정합니다. 그런 다음 `OperationDescription`의 메시지 컬렉션에서 이러한 각 메시지의 동작을 가져와 `ChunkingBindingParameter`의 인스턴스 내에 포함된 문자열 컬렉션에 추가합니다. 그런 다음 이 `ChunkingBindingParameter`를 제공된 `BindingParameterCollection`에 추가합니다.

바인딩의 각 바인딩 요소가 채널 팩터리나 채널 수신기를 빌드할 때 `BindingParameterCollection` 내에서 이 `BindingContext`이 해당 바인딩 요소에 전달됩니다. 의 `ChunkingBindingElement`는의 `BuildChannelFactory<T>` 구현 이며 `BuildChannelListener<T>` 에서이 `ChunkingBindingParameter` `BindingContext’`를 끌어옵니다 .`BindingParameterCollection` 그런 다음 `ChunkingBindingParameter` 내에 포함된 동작 컬렉션이 `ChunkingChannelFactory` 또는 `ChunkingChannelListener`에 전달된 다음 `ChunkingDuplexSessionChannel`에 전달됩니다.

## <a name="running-the-sample"></a>샘플 실행

#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. 다음 명령을 사용 하 여 ASP.NET 4.0을 설치 합니다.

    ```console
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable
    ```

2. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.

3. 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따르세요.

4. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.

5. 먼저 Service.exe를 실행한 다음 Client.exe를 실행하고 두 콘솔 창에서 출력을 살펴봅니다.

샘플을 실행할 경우의 예상 출력은 다음과 같습니다.

클라이언트

```console
Press enter when service is available

 > Sent chunk 1 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 > Sent chunk 2 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 > Sent chunk 3 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 > Sent chunk 4 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 > Sent chunk 5 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 > Sent chunk 6 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 > Sent chunk 7 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 > Sent chunk 8 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 > Sent chunk 9 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 > Sent chunk 10 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 < Received chunk 1 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 < Received chunk 2 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 < Received chunk 3 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 < Received chunk 4 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 < Received chunk 5 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 < Received chunk 6 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 < Received chunk 7 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 < Received chunk 8 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 < Received chunk 9 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 < Received chunk 10 of message 5b226ad5-c088-4988-b737-6a565e0563dd
```

서버:

```console
Service started, press enter to exit
 < Received chunk 1 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 < Received chunk 2 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 < Received chunk 3 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 < Received chunk 4 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 < Received chunk 5 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 < Received chunk 6 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 < Received chunk 7 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 < Received chunk 8 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 < Received chunk 9 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 < Received chunk 10 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10
 > Sent chunk 1 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 > Sent chunk 2 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 > Sent chunk 3 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 > Sent chunk 4 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 > Sent chunk 5 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 > Sent chunk 6 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 > Sent chunk 7 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 > Sent chunk 8 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 > Sent chunk 9 of message 5b226ad5-c088-4988-b737-6a565e0563dd
 > Sent chunk 10 of message 5b226ad5-c088-4988-b737-6a565e0563dd
```
