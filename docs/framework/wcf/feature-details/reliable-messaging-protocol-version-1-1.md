---
title: 안정적인 메시징 프로토콜 버전 1.1
ms.date: 03/30/2017
ms.assetid: 0da47b82-f8eb-42da-8bfe-e56ce7ba6f59
ms.openlocfilehash: 349c4dec8f127640d2709abcd63295aace6826df
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64754107"
---
# <a name="reliable-messaging-protocol-version-11"></a>안정적인 메시징 프로토콜 버전 1.1

이 항목에서는 WS-ReliableMessaging 대 한 Windows Communication Foundation (WCF) 구현 세부 정보를 다룹니다 HTTP 전송을 사용 하 여 상호 운용에 필요한 2007 년 2 월 (버전 1.1) 프로토콜입니다. WCF에는 제약 조건 및 자세한 내용은이 항목에서에서 확인 된 내용과 함께 WS-ReliableMessaging 사양을 따릅니다. 부터 WS-ReliableMessaging 버전 1.1 프로토콜을 구현 되는 [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)]합니다.

WS-ReliableMessaging 2007년 2월 프로토콜을 구현 하 여 WCF에는 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement>합니다.

편의상 이 항목에서는 다음 역할을 사용합니다.

- 개시자: Ws-reliable 메시지 시퀀스 만들기를 시작 하는 클라이언트입니다.

- 응답자: 개시자의 요청을 수신 하는 서비스입니다.

 이 문서에서는 다음 표에 있는 접두사와 네임스페이스를 사용합니다.

|접두사|네임스페이스|
|-|-|
|wsrm|http://docs.oasis-open.org/ws-rx/wsrm/200702|
|netrm|http://schemas.microsoft.com/ws/2006/05/rm|
|초|http://www.w3.org/2003/05/soap-envelope|
|wsa|http://schemas.xmlsoap.org/ws/2005/08/addressing|
|wsse|http://docs.oasis-open.org/wss/2004/01/oasis-200401-wssecurity-secext-1.0.xsd|
|wsrmp|http://docs.oasis-open.org/ws-rx/wsrmp/200702|
|netrmp|http://schemas.microsoft.com/ws-rx/wsrmp/200702|
|wsp|(WS-Policy 1.2 또는 WS-Policy 1.5)|

## <a name="messaging"></a>메시징

### <a name="sequence-creation"></a>시퀀스 만들기

WCF 구현 `CreateSequence` 고 `CreateSequenceResponse` 신뢰할 수 있는 메시징을 설정 하는 메시지 시퀀스입니다. 적용되는 제약 조건은 다음과 같습니다.

- B1101: WCF 시작자와 동일한 끝점 참조를 사용 합니다 `CreateSequence` 메시지의 `ReplyTo`를 `AcksTo` 및 `Offer/Endpoint`합니다.

- R1102: 합니다 `AcksTo`, `ReplyTo` 하 고 `Offer/Endpoint` 끝점 참조에 `CreateSequence` 메시지는 8 비트 형식과 일치 하도록 동일한 문자열 표현으로 주소 값을 가져야 합니다.

  - WCF 응답자 확인의 URI 부분이 합니다 `AcksTo`, `ReplyTo` 및 `Endpoint` 시퀀스를 만들기 전에 끝점 참조 동일 합니다.

- R1103: `AcksTo`, `ReplyTo` 및 `Offer/Endpoint` 끝점 참조에 `CreateSequence` 메시지는 동일한 참조 매개 변수 집합이 있어야 합니다.

  - WCF는 적용 하지 않습니다 하지만 참조 하는 것으로 가정의 매개 변수를 `AcksTo`, `ReplyTo` 및 `Offer/Endpoint` 끝점 참조 `CreateSequence` 동일 하 고 참조 매개 변수를 사용 하는 `ReplyTo` 에 대 한 끝점 참조 승인 및 역방향 시퀀스 메시지입니다.

- B1104: WCF 초기자 선택적 생성 하지 않습니다 `Expires` 또는 `Offer/Expires` 요소에는 `CreateSequence` 메시지입니다.

- B1105: 에 액세스할 때를 `CreateSequence` 메시지를 WCF 응답자는를 `Expires` 값을 `CreateSequence` 요소로 `Expires` 값는 `CreateSequenceResponse` 요소. WCF 응답자 읽고 무시이 고, 그렇지 합니다 `Expires` 고 `Offer/Expires` 값입니다.

- B1106: 에 액세스할 때 합니다 `CreateSequenceResponse` 메시지를 WCF 초기자 읽습니다 선택적 `Expires` 값 하지만 사용 하지 않습니다.

- B1107: WCF 개시자와 응답자 항상 생성 선택적 `IncompleteSequenceBehavior` 요소에는 `CreateSequence/Offer` 고 `CreateSequenceResponse` 요소입니다.

- B1108: WCF만 사용 합니다 `DiscardFollowingFirstGap` 및 `NoDiscard` 값을 `IncompleteSequenceBehavior` 요소입니다.

  - WS-ReliableMessaging은 `Offer` 메커니즘을 사용하여 세션을 형성하는 상호 관련된 두 개의 역방향 시퀀스를 설정합니다.

- B1109: 경우 `CreateSequence` 포함를 `Offer` 요소는 한 가지 방법은 WCF 응답 자가 제공된 된 시퀀스로 응답 하 여 거부를 `CreateSequenceResponse` 없이 `Accept` 요소입니다.

- B1110: 신뢰할 수 있는 메시징 응답자가 제공된 된 시퀀스를 거부 하는 경우 WCF 초기자 새로 설정 된 시퀀스를 오류입니다.

- B1111: 하는 경우 `CreateSequence` 없습니다를 `Offer` 요소를 양방향 WCF 응답 자가 제공된 된 시퀀스를 거부로 응답 하 여를 `CreateSequenceRefused` 오류.

- R1112: 두 개의 역방향 시퀀스를 사용 하 여 설정 된 경우는 `Offer` 메커니즘을를 `[address]` 의 속성을 `CreateSequenceResponse/Accept/AcksTo` 끝점 참조에는 대상 URI와 일치 해야 합니다의 `CreateSequence` 메시지 바이트.

- R1113: 두 개의 역방향 시퀀스를 사용 하 여 설정 된 경우는 `Offer` 메커니즘 개시자에서 응답자로 두 시퀀스의 모든 메시지를 보내야 같은 끝점 참조 합니다.

WCF는 WS-ReliableMessaging 사용 하 여 개시자와 응답자 간에 신뢰할 수 있는 세션을 설정. WCF WS-ReliableMessaging 구현에서는 단방향, 요청-회신 및 전체에 대 한 신뢰할 수 있는 세션을 제공 이중 메시징 패턴입니다. `Offer` 및 `CreateSequence`에서 WS-ReliableMessaging `CreateSequenceResponse` 메커니즘을 사용하면 상호 관련된 두 개의 역방향 시퀀스를 설정하고 모든 메시지 끝점에 적합한 세션 프로토콜을 제공합니다. WCF는 세션 무결성에 대 한 종단 간 보호를 포함 하 여 세션에 대 한 보안 보장을 제공 하므로 같은 상대방에 메시지가 동일한 대상 도착 하도록 유용 합니다. 이렇게 하면 응용 프로그램 메시지에서 "피기백킹"이라고 하는 시퀀스 승인을 사용할 수 있습니다. 따라서 제약 조건 R1102, R1112, 및 R1113 WCF에 적용 됩니다.

`CreateSequence` 메시지의 예입니다.

```xml
<s:Envelope>
  <s:Header>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CreateSequence</wsa:Action>
    <wsa:MessageID>urn:uuid:949cca61-8813-42ff-ab33-18d9e3fa82fa</wsa:MessageID>
    <wsa:ReplyTo>
        <wsa:Address>http://Business456.com/clientA</wsa:Address>
    </wsa:ReplyTo>
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:CreateSequence>
      <wsrm:AcksTo>
        <wsa:Address>http://Business456.com/clientA</wsa:Address>
      </wsrm:AcksTo>
      <wsrm:Offer>
        <wsrm:Identifier>urn:uuid:066b4730-fc82-458a-a5c1-210be4fb4e4e</wsrm:Identifier>
        <wsrm:Endpoint>
          <wsa:Address>http://Business456.com/clientA</wsa:Address>
        </wsrm:Endpoint>
        <wsrm:IncompleteSequenceBehavior>DiscardFollowingFirstGap</wsrm:IncompleteSequenceBehavior>
      </wsrm:Offer>
    </wsrm:CreateSequence>
  </s:Body>
</s:Envelope>
```

`CreateSequenceResponse` 메시지의 예입니다.

```xml
<s:Envelope>
  <s:Header>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CreateSequenceResponse</wsa:Action>
    <wsa:RelatesTo>urn:uuid:949cca61-8813-42ff-ab33-18d9e3fa82fa</wsa:RelatesTo>
    <wsa:To s:mustUnderstand="1">http://Business456.com/clientA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:CreateSequenceResponse>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
      <wsrm:IncompleteSequenceBehavior>DiscardFollowingFirstGap</wsrm:IncompleteSequenceBehavior>
      <wsrm:Accept>
        <wsrm:AcksTo>
          <wsa:Address>http://BusinessABC.com/serviceA</wsa:Address>
        </wsrm:AcksTo>
      </wsrm:Accept>
    </wsrm:CreateSequenceResponse>
  </s:Body>
</s:Envelope>
```

### <a name="closing-a-sequence"></a>시퀀스 닫기

WCF를 사용 합니다 `CloseSequence` 및 `CloseSequenceResponse` 신뢰할 수 있는 메시징 소스에서 시작 된 종료에 대 한 메시지입니다. WCF 신뢰할 수 있는 메시징 대상은 종료를 시작 하지 않습니다 하 고 WCF 신뢰할 수 있는 메시징 소스는 신뢰할 수 있는 메시징 대상에서 시작 된 종료를 지원 하지 않습니다. 적용되는 제약 조건은 다음과 같습니다.

- B1201: WCF 신뢰할 수 있는 메시징 소스는 항상 보냅니다는 `CloseSequence` 메시지 시퀀스를 종료 합니다.

- B1202: 보내기 전에 시퀀스 메시지 전체 범위의 승인을 기다린 신뢰할 수 있는 메시징 소스는 `CloseSequence` 메시지입니다.

- B1203: 신뢰할 수 있는 메시징 소스는 항상 선택적 포함 `LastMsgNumber` 요소 않으면 시퀀스에 메시지가 없습니다.

- R1204: 신뢰할 수 있는 메시징 대상은 전송 하 여 종료 시작 해서는 안을 `CloseSequence` 메시지입니다.

- B1205: 수신 시는 `CloseSequence` 메시지를 WCF 신뢰할 수 있는 메시징 소스 시퀀스를 불완전 한 것으로 간주 하 고 오류를 보냅니다.

 `CloseSequence` 메시지의 예입니다.

```xml
<s:Envelope>
  <s:Header>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CloseSequence</wsa:Action>
    <wsa:MessageID>urn:uuid:6ce1d4c3-e1c1-474f-a8c9-4210e37f7877</wsa:MessageID>
    <wsa:ReplyTo>
      <wsa:Address>http://Business456.com/clientA</wsa:Address>
    </wsa:ReplyTo>
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:CloseSequence>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
      <wsrm:LastMsgNumber>30</wsrm:LastMsgNumber>
    </wsrm:CloseSequence>
  </s:Body>
</s:Envelope>
```

예제 `CloseSequenceResponse` 메시지:

```xml
<s:Envelope>
  <s:Header>
    <wsrm:SequenceAcknowledgement>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
      <wsrm:AcknowledgementRange Lower="1" Upper="30"></wsrm:AcknowledgementRange>
      <wsrm:Final></wsrm:Final>
      <netrm:BufferRemaining>8</netrm:BufferRemaining>
    </wsrm:SequenceAcknowledgement>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CloseSequenceResponse</wsa:Action>
    <wsa:RelatesTo>urn:uuid:6ce1d4c3-e1c1-474f-a8c9-4210e37f7877</wsa:RelatesTo>
    <wsa:To s:mustUnderstand="1">http://Business456.com/clientA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:CloseSequenceResponse>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
    </wsrm:CloseSequenceResponse>
  </s:Body>
</s:Envelope>
```

### <a name="sequence-termination"></a>시퀀스 종료

WCF에서 주로 사용 합니다 `TerminateSequence/TerminateSequenceResponse` 핸드셰이크를 완료 한 후를 `CloseSequence/CloseSequenceResponse` 핸드셰이크입니다. WCF 신뢰할 수 있는 메시징 대상은 종료를 시작 하지 않습니다 하 고 신뢰할 수 있는 메시징 소스는 신뢰할 수 있는 메시징 대상에서 시작 된 종료를 지원 하지 않습니다. 적용되는 제약 조건은 다음과 같습니다.

- B1301: WCF 초기자만 보냅니다 합니다 `TerminateSequence` 성공적으로 완료 된 후 메시지를 `CloseSequence/CloseSequenceResponse` 핸드셰이크입니다.

- R1302: WCF는 유효성을 검사 합니다 `LastMsgNumber` 모든 요소는 일치 `CloseSequence` 및 `TerminateSequence` 지정된 된 순서에 대 한 메시지입니다. 즉, `LastMsgNumber`가 모든 `CloseSequence` 및 `TerminateSequence` 메시지에 없거나, 모든 `CloseSequence` 및 `TerminateSequence` 메시지에 있으며 이러한 메시지에서 동일합니다.

- B1303: 수신 하는 경우는 `TerminateSequence` 후 메시지를 `CloseSequence/CloseSequenceResponse` 핸드셰이크를 사용 하 여 응답 신뢰할 수 있는 메시징 대상은 `TerminateSequenceResponse` 메시지입니다. 신뢰할 수 있는 메시징 소스에 `TerminateSequence` 메시지를 보내기 전의 최종 승인이 있으므로 신뢰할 수 있는 메시징 대상은 시퀀스가 종료되고 리소스를 즉시 회수함을 인식하고 있습니다.

- B1304: 수신 하는 경우는 `TerminateSequence` 이전에 메시지를 `CloseSequence/CloseSequenceResponse` 핸드셰이크를 사용 하 여 응답 WCF 신뢰할 수 있는 메시징 대상은 `TerminateSequenceResponse` 메시지. 신뢰할 수 있는 메시징 대상이 시퀀스에서 일치하지 않는 부분이 없음을 확인한 경우에는 클라이언트가 최종 승인을 받을 수 있도록 신뢰할 수 있는 메시징 대상이 애플리케이션 대상에서 지정한 시간 동안 기다린 다음 리소스를 회수합니다. 그렇지 않은 경우 신뢰할 수 있는 메시징 대상이 리소스를 바로 회수하고 애플리케이션 대상에 `Faulted` 이벤트를 발생시켜 시퀀스에 오류가 발생하여 종료되었음을 알려 줍니다.

`TerminateSequence` 메시지의 예입니다.

```xml
<s:Envelope>
  <s:Header>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/TerminateSequence</wsa:Action>
    <wsa:MessageID>urn:uuid:3597a398-4f3c-40f4-9335-8f1515572fdf</wsa:MessageID>
    <wsa:ReplyTo>
      <wsa:Address>http://Business456.com/clientA</wsa:Address>
    </wsa:ReplyTo>
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:TerminateSequence>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
      <wsrm:LastMsgNumber>30</wsrm:LastMsgNumber>
      </wsrm:TerminateSequence>
  </s:Body>
</s:Envelope>
```

예제 `TerminateSequenceResponse` 메시지:

```xml
<s:Envelope>
  <s:Header>
    <wsrm:SequenceAcknowledgement>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
      <wsrm:AcknowledgementRange Lower="1" Upper="30"></wsrm:AcknowledgementRange>
      <wsrm:Final></wsrm:Final>
      <netrm:BufferRemaining>8</netrm:BufferRemaining>
    </wsrm:SequenceAcknowledgement>
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/TerminateSequenceResponse</wsa:Action>
    <wsa:RelatesTo>urn:uuid:3597a398-4f3c-40f4-9335-8f1515572fdf</wsa:RelatesTo>
    <wsa:To s:mustUnderstand="1">://Business456.com/clientA</wsa:To>
  </s:Header>
  <s:Body>
    <wsrm:TerminateSequenceResponse>
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
    </wsrm:TerminateSequenceResponse>
  </s:Body>
</s:Envelope>
```

### <a name="sequences"></a>시퀀스

다음은 시퀀스에 적용되는 제약 조건의 목록입니다.

- B1401:WCF 생성 하 고 액세스 시퀀스 번호 보다 높은 `xs:long`의 최대 포함 값, 9223372036854775807 합니다.

`Sequence` 헤더의 예입니다.

```xml
<wsrm:Sequence s:mustUnderstand="1">
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
  <wsrm:MessageNumber>1</wsrm:MessageNumber>
</wsrm:Sequence>
```

### <a name="request-acknowledgement"></a>승인 요청

WCF를 사용 하는 `AckRequested` 헤더를 연결 유지 메커니즘으로 합니다.

`AckRequested` 헤더의 예입니다.

```xml
<wsrm:AckRequested>
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
</wsrm:AckRequested>
```

### <a name="sequenceacknowledgement"></a>SequenceAcknowledgement

WCF는 Ws-reliable Messaging에 제공 된 시퀀스 승인에 "피기백" 메커니즘을 사용 합니다. 적용되는 제약 조건은 다음과 같습니다.

- R1601: 두 개의 역방향 시퀀스를 사용 하 여 설정 된 경우는 `Offer` 메커니즘을 `SequenceAcknowledgement` 받는 사람된에 게 전송 된 모든 응용 프로그램 메시지에서 헤더를 포함 될 수 있습니다. 원격 엔드포인트에서는 피기백된 `SequenceAcknowledgement` 헤더에 액세스할 수 있어야 합니다.

- B1602: WCF를 생성 하지 않습니다 `SequenceAcknowledgement` 포함 하는 헤더 `Nack` 요소입니다. WCF는 각 유효성을 검사 `Nack` 요소에 시퀀스 번호가 포함 하지만 그렇지 않은 경우 무시를 `Nack` 요소와 값입니다.

 `SequenceAcknowledgement` 헤더의 예입니다.

```xml
<wsrm:SequenceAcknowledgement>
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
  <wsrm:AcknowledgementRange Lower="1" Upper="1"></wsrm:AcknowledgementRange>
</wsrm:SequenceAcknowledgement>
```

### <a name="ws-reliablemessaging-faults"></a>WS-ReliableMessaging 오류

다음은 WS-ReliableMessaging 오류의 WCF 구현에 적용 되는 제약 조건의 목록입니다. 적용되는 제약 조건은 다음과 같습니다.

- B1701: WCF를 생성 하지 않습니다 `MessageNumberRollover` 오류입니다.

- B1702: SOAP 1.2를 통해 서비스 끝점 연결 제한에 도달 하 고 새 연결을 처리할 수 없는 경우 WCF에서는 발생 하는 중첩 `CreateSequenceRefused` 오류 하위 코드, `netrm:ConnectionLimitReached`다음 예제에서와 같이 합니다.

```xml
<s:Envelope>
  <s:Header>
    <wsa:Action>http://docs.oasis-open.org/ws-rx/wsrm/200702/fault</wsa:Action>
  </s:Header>
  <s:Body>
    <s:Fault>
      <s:Code>
        <s:Value>s:Receiver</s:Value>
        <s:Subcode>
          <s:Value>wsrm:CreateSequenceRefused</s:Value>
          <s:Subcode>
            <s:Value>netrm:ConnectionLimitReached</s:Value>
          </s:Subcode>
        </s:Subcode>
      </s:Code>
      <s:Reason>
        <s:Text xml:lang="en">Server 'http://BusinessABC.com/serviceA' is too busy to process this request. Try again later.</s:Text>
      </s:Reason>
    </s:Fault>
  </s:Body>
</s:Envelope>
```

### <a name="ws-addressing-faults"></a>WS-Addressing 오류

WS-ReliableMessaging에서는 Ws-addressing 때문에 WCF WS-ReliableMessaging 구현 생성 하 고 Ws-addressing 오류를 전송할 수 있습니다. 이 섹션에서는 WCF에서 명시적으로 생성 하 고 WS-ReliableMessaging 계층에서 전송 하는 Ws-addressing 오류에 설명 합니다.

- B1801:WCF 생성 하 고 전송 된 `Message Addressing Header Required` 오류 중 하나가 true 인 경우:

  - `CreateSequence`, `CloseSequence` 또는 `TerminateSequence` 메시지에 `MessageId` 헤더가 없습니다.

  - `CreateSequence`, `CloseSequence` 또는 `TerminateSequence` 메시지에 `ReplyTo` 헤더가 없습니다.

  - `CreateSequenceResponse`, `CloseSequenceResponse` 또는 `TerminateSequenceResponse` 메시지에 `RelatesTo` 헤더가 없습니다.

- B1802:WCF 생성 하 고 전송 합니다 `Endpoint Unavailable` 오류 있는 수신 대기 중인 끝점이 없습니다를 주소 지정 헤더의 검사를 기반으로 시퀀스를 처리할 수는 `CreateSequence` 메시지입니다.

## <a name="protocol-composition"></a>프로토콜 구성

### <a name="composition-with-ws-addressing"></a>WS-Addressing을 사용하여 구성

WCF에서는 두 가지 버전을의 Ws-addressing을 지원합니다. Ws-addressing 2004/08 [WS-ADDR]과 W3C Ws-addressing 1.0 권장 사항 [WS-ADDR-CORE] 및 [SOAP-WS-ADDR].

WS-ReliableMessaging 사양에는 WS-Addressing 2004/08만 언급되어 있지만 WS-Addressing 버전만 사용하도록 제한되지는 않습니다. 다음은 WCF에 적용 되는 제약 조건의 목록입니다.

- R2101: Ws-addressing 2004/08과 Ws-addressing 1.0 모두 Ws-reliable Messaging과 함께 사용할 수 있습니다.

- R2102: 제공 된 WS-ReliableMessaging 시퀀스 또는 한 쌍의 역방향 시퀀스를 사용 하 여 상관 관계가 지정 된 전체에서 단일 버전의 Ws-addressing을 사용 해야 합니다는 `Offer` 메커니즘입니다.

### <a name="composition-with-soap"></a>SOAP를 사용하여 구성

WCF는 SOAP 1.1 및 SOAP 1.2 Ws-reliable Messaging를 모두 지원합니다.

### <a name="composition-with-ws-security-and-ws-secureconversation"></a>WS-Security 및 WS-SecureConversation을 사용하여 구성

WCF 보안 전송 (HTTPS), Ws-security를 사용 하 여 구성 및 컴퍼지션 Ws-secure Conversation을 사용 하 여 사용 하 여 WS-ReliableMessaging 시퀀스에 대 한 보호를 제공 합니다. WS-ReliableMessaging 1.1 프로토콜, WS-Security 1.1 및 WS-Secure Conversation 1.3 프로토콜을 함께 사용해야 합니다. 다음은 WCF에 적용 되는 제약 조건의 목록입니다.

- R2301: 개별 메시지의 무결성 뿐만 아니라 WS-ReliableMessaging 시퀀스의 무결성 및 기밀성을 보호 하려면 WCF에 필요한 Ws-secure Conversation을 사용 해야 합니다.

- R2302:AWS-WS-ReliableMessaging 시퀀스를 설정 하기 전에 보안 대화 세션을 설정 해야 합니다.

- R2303: WS-ReliableMessaging 시퀀스 수명이 Ws-secure Conversation 세션의 수명을 초과 하는 경우는 `SecurityContextToken` Ws-secure Conversation 갱신을 해당 Ws-secure Conversation 갱신 바인딩을 사용 하 여 사용 하 여 설정 합니다.

- B2304:WS-ReliableMessaging 시퀀스 또는 한 쌍의 상호 관련 된 역방향 시퀀스는 항상 단일 Ws-secureconversation 세션에 바인딩됩니다.

- R2305: WCF 응답자를 실행 하려면으로 Ws-secure Conversation을 사용 하 여 구성 하는 경우는 `CreateSequence` 메시지에 포함 합니다 `wsse:SecurityTokenReference` 요소 및 `wsrm:UsesSequenceSTR` 헤더입니다.

 `UsesSequenceSTR` 헤더의 예입니다.

```xml
<wsrm:UsesSequenceSTR></wsrm:UsesSequenceSTR>
```

### <a name="composition-with-ssltls-sessions"></a>SSL/TLS 세션을 사용하여 구성

WCF는 SSL/TLS 세션을 사용 하 여 컴퍼지션을 지원 하지 않습니다.

- B2401: WCF를 생성 하지 않습니다는 `wsrm:UsesSequenceSSL` 헤더입니다.

- R2402: 신뢰할 수 있는 메시징 개시자를 보내면 안을 `CreateSequence` 메시지를 `wsrm:UsesSequenceSSL` WCF 응답자 헤더입니다.

### <a name="composition-with-ws-policy"></a>WS-Policy를 사용하여 구성

WCF는 Ws-policy의 두 버전을 지원합니다. Ws-policy 1.2와 Ws-policy 1.5 합니다.

## <a name="ws-reliablemessaging-ws-policy-assertion"></a>WS-ReliableMessaging WS-Policy Assertion

WS-ReliableMessaging Ws-policy Assertion을 사용 하 여 WCF `wsrm:RMAssertion` 끝점 기능을 설명 합니다. 다음은 WCF에 적용 되는 제약 조건의 목록입니다.

- B3001: WCF 첨부 `wsrmn:RMAssertion` Ws-policy Assertion을 `wsdl:binding` 요소입니다. WCF에는 첨부 파일을 모두 지 원하는 `wsdl:binding` 고 `wsdl:port` 요소입니다.

- B3002: WCF는 생성 하지 않습니다는 `wsp:Optional` 태그입니다.

- B3003: 에 액세스할 때 합니다 `wsrmp:RMAssertion` Ws-policy Assertion WCF 무시는 `wsp:Optional` 태그 하 고 WS-RM 정책을 필수 항목으로 처리 합니다.

- R3004: 지정 하는 정책을 WCF SSL/TLS 세션을 사용 하 여 작성 되지 않습니다, 때문에 WCF 받아들이지 않는 `wsrmp:SequenceTransportSecurity`합니다.

- B3005: WCF는 항상 생성 된 `wsrmp:DeliveryAssurance` 요소입니다.

- B3006: WCF는 항상 지정 된 `wsrmp:ExactlyOnce` 배달 보증 합니다.

- B3007: WCF에서는 발생 하는 WS-ReliableMessaging 어설션의 다음과 같은 속성을 읽는 및 WCF에 제어를 제공`ReliableSessionBindingElement`:

  - `netrmp:InactivityTimeout`

  - `netrmp:AcknowledgementInterval`

  `RMAssertion`의 예입니다.

  ```xml
  <wsrmp:RMAssertion>
    <wsp:Policy>
      <wsrmp:SequenceSTR/>
      <wsrmp:DeliveryAssurance>
        <wsp:Policy>
          <wsrmp:ExactlyOnce/>
          <wsrmp:InOrder/>
        </wsp:Policy>
      </wsrmp:DeliveryAssurance>
    </wsp:Policy>
    <netrmp:InactivityTimeout Milliseconds="600000"/>
    <netrmp:AcknowledgementInterval Milliseconds="200"/>
  </wsrmp:RMAssertion>
  ```

## <a name="flow-control-ws-reliablemessaging-extension"></a>흐름 제어 WS-ReliableMessaging 확장명

WCF를 시퀀스 메시지 흐름 선택적 추가 긴밀 하 게 제어할 수 있도록 WS-ReliableMessaging 확장성을 사용 합니다.

흐름 제어를 설정 하 여 활성화 합니다 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.FlowControlEnabled?displayProperty=nameWithType> 속성을 `true`입니다. 다음은 WCF에 적용 되는 제약 조건의 목록입니다.

- B4001: WCF를 생성 하는 신뢰할 수 있는 메시징 흐름 제어를 사용 하는 경우는 `netrm:BufferRemaining` 의 요소 확장성에 요소를 `SequenceAcknowledgement` 헤더를 다음 예제에서와 같이 합니다.

  ```xml
  <wsrm:SequenceAcknowledgement>
    <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>
    <wsrm:AcknowledgementRange Upper="1" Lower="1"/>
    <netrm:BufferRemaining>8</netrm:BufferRemaining>
  </wsrm:SequenceAcknowledgement>
  ```

- B4002: 신뢰할 수 있는 메시징 흐름 제어 활성화 된 경우 WCF는 필요 하지는 `netrm:BufferRemaining` 요소에는 `SequenceAcknowledgement` 헤더입니다.

- B4003: WCF 신뢰할 수 있는 메시징 대상은 사용 하 여 `netrm:BufferRemaining` 얼마나 많은 새 메시지를 나타내기 위해 버퍼링 할 수 있습니다.

- B4004:When 신뢰할 수 있는 메시징 흐름 제어를 사용의 값을 사용 하는 WCF 신뢰할 수 있는 메시징 소스 `netrm:BufferRemaining` 메시지 전송을 스로틀 하 합니다.

- B4005: WCF 생성 `netrm:BufferRemaining` 정수는 0과 4096 사이의 값을 읽고 0 사이의 정수 값 및 `xs:int`의 `maxInclusive` 값 214748364 합니다.

## <a name="message-exchange-patterns"></a>메시지 교환 패턴

이 섹션에서는 WS-ReliableMessaging 다른 메시지 교환 패턴에 사용 되는 경우 WCF의 동작을 설명 합니다. 각 메시지 교환 패턴에 대해 다음 두 가지 배포 시나리오를 고려합니다.

- 주소를 지정할 수 없는 개시자: 개시자가 방화벽 뒤에 있는; 응답자는 HTTP 응답 에서만 개시자에 게 메시지를 배달할 수 있습니다.

- 초기자 주소 지정 가능 합니다. 개시자와 응답자 모두 HTTP 요청에 보낼 수 즉, 두 개의 역방향 HTTP 연결을 설정할 수 있습니다.

### <a name="one-way-non-addressable-initiator"></a>주소를 지정할 수 없는 단방향 개시자

#### <a name="binding"></a>바인딩

WCF에는 하나의 HTTP 채널을 통해 하나의 시퀀스를 사용 하 여 단방향 메시지 교환 패턴을 제공 합니다. WCF는 HTTP 요청을 사용 하 여 시작자에 게 응답자 로부터 모든 메시지를 전송 하 고 HTTP 응답에 시작자에서 모든 메시지를 전송 합니다.

#### <a name="createsequence-exchange"></a>CreateSequence 교환

WCF 시작자에서 전송를 `CreateSequence` 없이 메시지 `Offer` 요소는 HTTP 요청에 예상는 `CreateSequenceResponse` HTTP 응답에는 메시지입니다. WCF 응답자는 시퀀스를 만들고 전송 합니다 `CreateSequenceResponse` 없이 메시지 `Accept` HTTP 응답에는 요소입니다.

#### <a name="sequenceacknowledgement"></a>SequenceAcknowledgement

WCF 초기자를 제외한 모든 메시지의 회신에 대 한 승인을 처리 합니다 `CreateSequence` 메시지와 오류 메시지입니다. WCF 응답자는 항상 독립 실행형 승인을 모든 시퀀스에 대 한 HTTP 응답에 전송 및 `AckRequested` 메시지입니다.

#### <a name="closesequence-exchange"></a>CloseSequence 교환

WCF 시작자에서 전송를 `CloseSequence` 하며 HTTP 요청에서 메시지를 `CreateSequenceResponse` HTTP 응답에는 메시지입니다. WCF 응답자 전송 된 `CloseSequenceResponse` HTTP 응답에는 메시지입니다.

#### <a name="terminatesequence-exchange"></a>TerminateSequence 교환

WCF 시작자에서 전송를 `TerminateSequence` 하며 HTTP 요청에서 메시지를 `TerminateSequenceResponse` HTTP 응답에는 메시지입니다. WCF 응답자 전송 된 `TerminateSequenceResponse` HTTP 응답에는 메시지입니다.

### <a name="one-way-addressable-initiator"></a>주소를 지정할 수 있는 단방향 개시자

#### <a name="binding"></a>바인딩

WCF는 하나를 통해 하나의 시퀀스를 사용 하 여 단방향 메시지 교환 패턴을 제공 인바운드 및 아웃 바운드 HTTP 채널입니다. WCF는 HTTP 요청을 사용 하 여 모든 메시지를 전송 합니다. 모든 HTTP 응답에는 빈 본문과 HTTP 202 상태 코드가 포함됩니다.

#### <a name="createsequence-exchange"></a>CreateSequence 교환

WCF 시작자에서 전송 된 `CreateSequence` 없이 메시지 `Offer` 요소는 HTTP 요청에 합니다. WCF 응답자는 시퀀스를 만들고 전송 합니다 `CreateSequenceResponse` 없이 메시지 `Accept` 는 HTTP 요청에는 요소입니다.

### <a name="duplex-addressable-initiator"></a>주소를 지정할 수 있는 이중 개시자

#### <a name="binding"></a>바인딩

WCF 제공 하나 위로 마우스를 두 개를 사용 하 여 완전히 비동기적인 양방향 메시지 교환 패턴을 시퀀스 인바운드 및 아웃 바운드 HTTP 채널입니다. 이 메시지 교환 패턴은 제한된 방식으로 `Request/Reply`, `Addressable` 개시자 메시지 교환 패턴과 혼합하여 사용할 수 있습니다. WCF는 HTTP 요청을 사용 하 여 모든 메시지를 전송 합니다. 모든 HTTP 응답에는 빈 본문과 HTTP 202 상태 코드가 포함됩니다.

#### <a name="createsequence-exchange"></a>CreateSequence 교환

WCF 시작자에서 전송 된 `CreateSequence` 메시지는 `Offer` 요소는 HTTP 요청에 합니다. WCF 응답자는 합니다 `CreateSequence` 에 `Offer` 요소를 다음 시퀀스를 만들고 전송 합니다 `CreateSequenceResponse` 메시지는 `Accept` 요소.

#### <a name="sequence-lifetime"></a>시퀀스 수명

WCF는 개의 전체 이중 세션으로 두 시퀀스를 처리합니다.

한 개의 시퀀스를 오류는 오류를 생성 하면 WCF는 두 시퀀스를 오류 원격 끝점이 필요 합니다. 한 개의 시퀀스를 오류는 오류를 읽으면 WCF에는 두 시퀀스 오류입니다.

WCF 해당 아웃 바운드 시퀀스 닫고 해당 인바운드 시퀀스에서 메시지를 계속 처리할 수 있습니다. 반대로, WCF에서는 인바운드 시퀀스의 종료를 처리 하 고 계속 해 서 해당 아웃 바운드 시퀀스에서 메시지를 보낼 수 있습니다.

### <a name="request-reply-and-one-way-non-addressable-initiator"></a>요청-회신 및 단방향의 주소를 지정할 수 없는 개시자

#### <a name="binding"></a>바인딩

하나를 통해 HTTP 채널을 시퀀스 하는 두 개를 사용 하 여 요청-회신 메시지 교환 패턴 및 WCF 단방향 제공 합니다. WCF는 HTTP 요청을 사용 하 여 시작자에 게 응답자 로부터 모든 메시지를 전송 하 고 HTTP 응답에 시작자에서 모든 메시지를 전송 합니다.

#### <a name="createsequence-exchange"></a>CreateSequence 교환

WCF 시작자에서 전송를 `CreateSequence` 메시지는 `Offer` 요소는 HTTP 요청에 예상는 `CreateSequenceResponse` HTTP 응답에는 메시지입니다. WCF 응답자는 시퀀스를 만들고 전송 합니다 `CreateSequenceResponse` 메시지는 `Accept` HTTP 응답에는 요소입니다.

#### <a name="one-way-message"></a>단방향 메시지

단방향 메시지 교환을 성공적으로 완료 하려면 WCF 초기자 HTTP 요청에 요청 시퀀스 메시지를 전송 하 고 독립 실행형 받습니다 `SequenceAcknowledgement` HTTP 응답에는 메시지입니다. `SequenceAcknowledgement`는 전송된 메시지를 승인해야 합니다.

WCF 응답자는 승인, 오류 또는 빈 본문과 HTTP 202 상태 코드가 포함 된 응답을 사용 하 여 요청에 회신할 수 있습니다.

#### <a name="two-way-messages"></a>양방향 메시지

양방향 메시지 교환 프로토콜을 성공적으로 완료 하려면 WCF 초기자 HTTP 요청에 요청 시퀀스 메시지를 전송 하 고 HTTP 응답에 회신 시퀀스 메시지를 수신 합니다. 응답에 전송된 요청 시퀀스 메시지를 승인하는 `SequenceAcknowledgement`가 있어야 합니다.

WCF 응답자는 응용 프로그램 회신, 오류 또는 빈 본문과 HTTP 202 상태 코드가 포함 된 응답을 사용 하 여 요청에 회신할 수 있습니다.

단방향 메시지가 있고 애플리케이션이 회신하는 시간 때문에 요청 시퀀스 메시지의 시퀀스 번호와 응답 메시지의 시퀀스 번호는 상관 관계가 없습니다.

#### <a name="retrying-replies"></a>회신 다시 시도

WCF 양방향 메시지 교환 프로토콜 상관 관계에 대 한 HTTP 요청-회신 상관 관계에 의존합니다. 이 때문에 WCF 초기자 해도 요청 시퀀스 메시지가 승인 되는 요청 시퀀스 메시지 다시 시도 하지만 HTTP 응답을 전달 하면 대신는 `SequenceAcknowledgement`, 응용 프로그램 회신 또는 오류입니다. WCF 응답자는 회신이 상호 관련 된 요청의 HTTP 응답에 회신을 다시 시도 합니다.

#### <a name="closesequence-exchange"></a>CloseSequence 교환

모든 회신 시퀀스 메시지와 모든 단방향 요청 시퀀스 메시지에 대 한 승인을 받으면 WCF 초기자 전송를 `CloseSequence` 하며 HTTP 요청에서 요청 시퀀스 메시지를 `CloseSequenceResponse` HTTP 응답에 있습니다.

요청 시퀀스를 닫으면 회신 시퀀스가 암시적으로 닫힙니다. 즉 WCF 초기자 회신 시퀀스의 마지막에 포함 됩니다 `SequenceAcknowledgement` 에 `CloseSequence` 메시지 및 회신 시퀀스에 없는 `CloseSequence` exchange 합니다.

WCF 응답자는 승인 하 고 전송 하는 모든 회신의 `CloseSequenceResponse` HTTP 응답에는 메시지입니다.

#### <a name="terminatesequence-exchange"></a>TerminateSequence 교환

수신 후 합니다 `CloseSequenceResponse` 메시지를 WCF 초기자 전송를 `TerminateSequence` 하며 HTTP 요청에서 요청 시퀀스 메시지를 `TerminateSequenceResponse` HTTP 응답에 합니다.

`CloseSequence` 교환과 마찬가지로 요청 시퀀스를 종료하면 회신 시퀀스가 암시적으로 종료됩니다. 즉 WCF 초기자 회신 시퀀스의 마지막에 포함 됩니다 `SequenceAcknowledgement` 에 `TerminateSequence` 메시지 및 회신 시퀀스에 없는 `TerminateSequence` exchange 합니다.

WCF 응답자 전송 된 `TerminateSequenceResponse` HTTP 응답에는 메시지입니다.

### <a name="requestreply-addressable-initiator"></a>요청/회신, 주소를 지정할 수 있는 개시자

#### <a name="binding"></a>바인딩

WCF 제공 하나 위로 마우스를 두 개를 사용 하 여 요청-회신 메시지 교환 패턴을 시퀀스 인바운드 및 아웃 바운드 HTTP 채널입니다. 이 메시지 교환 패턴은 제한된 방식으로 `Duplex, Addressable` 개시자 메시지 교환 패턴과 혼합하여 사용할 수 있습니다. WCF는 HTTP 요청을 사용 하 여 모든 메시지를 전송 합니다. 모든 HTTP 응답에는 빈 본문과 HTTP 202 상태 코드가 포함됩니다.

#### <a name="createsequence-exchange"></a>CreateSequence 교환

WCF 시작자에서 전송 된 `CreateSequence` 메시지는 `Offer` 요소는 HTTP 요청에 합니다. WCF 응답자는 `CreateSequence` 에 `Offer` 요소 다음 시퀀스를 만들고 전송 합니다 `CreateSequenceResponse` 메시지는 `Accept` 요소입니다.

#### <a name="requestreply-correlation"></a>요청/회신 상관 관계

다음 사항은 모든 상호 관련된 요청 및 회신에 적용됩니다.

- WCF 있는지 확인 모든 응용 프로그램 요청 메시지를 `ReplyTo` 끝점 참조 및 `MessageId`합니다.

- 각 응용 프로그램 요청 메시지의 로컬 끝점 참조를 적용 하는 WCF `ReplyTo`합니다. 로컬 엔드포인트 참조는 개시자에 대한 `CreateSequence` 메시지의 `ReplyTo`와 응답자에 대한 `CreateSequence` 메시지의 `To`입니다.

- WCF는 들어오는 요청 메시지를 통해는 `MessageId` 및 `ReplyTo`합니다.

- WCF 하면는 `ReplyTo` 모든 응용 프로그램 요청 메시지의 끝점 참조 URI 앞부분에 정의 된 대로 로컬 끝점 참조와 일치 합니다.

- WCF는 모든 회신 올바른 주의 해야 하면 `RelatesTo` 하 고 `To` 헤더 `wsa` 요청/회신 상관 관계 규칙입니다.
