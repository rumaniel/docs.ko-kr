---
title: Reliable Messaging 프로토콜 버전 1.0
ms.date: 03/30/2017
ms.assetid: a5509a5c-de24-4bc2-9a48-19138055dcce
ms.openlocfilehash: 6fceb49d107e4268a4b9fad6197335ff9e2af9ab
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67662802"
---
# <a name="reliable-messaging-protocol-version-10"></a>Reliable Messaging 프로토콜 버전 1.0

이 항목에서는 Ws-reliable Messaging에 대 한 Windows Communication Foundation (WCF) 구현 세부 정보를 다룹니다 HTTP 전송을 사용 하 여 상호 운용에 필요한 2005년 2월 (버전 1.0) 프로토콜입니다. WCF에는 제약 조건 및 자세한 내용은이 항목에서에서 확인 된 내용과 함께 Ws-reliable Messaging 사양을 따릅니다. WS-ReliableMessaging 버전 1.0 프로토콜을 구현 하는 WinFX부터 참고 합니다.

Ws-reliable Messaging 2005년 2월 프로토콜을 구현 하 여 WCF에는 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement>합니다.

편의상 이 항목에서는 다음 역할을 사용합니다.

- 개시자: WS-Reliable 메시지 시퀀스 만들기를 시작한 클라이언트입니다.

- 응답자: 개시자의 요청을 받은 서비스입니다.

이 문서에서는 다음 표에 있는 접두사와 네임스페이스를 사용합니다.

|접두사|네임스페이스|
|------------|---------------|
|wsrm|http://schemas.xmlsoap.org/ws/2005/02/rm|
|netrm|http://schemas.microsoft.com/ws/2006/05/rm|
|초|http://www.w3.org/2003/05/soap-envelope|
|wsa|http://schemas.xmlsoap.org/ws/2005/08/addressing|
|wsse|http://docs.oasis-open.org/wss/2004/01/oasis-200401-wssecurity-secext-1.0.xsd|

## <a name="messaging"></a>메시징

### <a name="sequence-establishment-messages"></a>시퀀스 설정 메시지

WCF 구현 `CreateSequence` 고 `CreateSequenceResponse` 메시지를 신뢰할 수 있는 메시지 시퀀스를 설정 합니다. 적용되는 제약 조건은 다음과 같습니다.

- B1101: WCF 시작자에서 선택적 Expires 요소를 생성 하지 않습니다는 `CreateSequence` 메시지 또는 경우에 때를 `CreateSequence` 메시지에 포함 되어는 `Offer` 요소를 선택적 `Expires` 요소에는 `Offer` 요소입니다.

- B1102: 에 액세스할 때 합니다 `CreateSequence` 메시지를 WCF`Responder` 둘 다를 송수신 `Expires` 요소는 존재 하지만 해당 값을 사용 하지 않는 경우.

WS-Reliable Messaging은 `Offer` 메커니즘을 사용하여 세션을 형성하는 상호 관련된 두 개의 역방향 시퀀스를 설정합니다.

- R1103: 경우 `CreateSequence` 포함는 `Offer` 요소를 신뢰할 수 있는 메시징 응답자 중 시퀀스를 허용 하며 응답 `CreateSequenceResponse` 를 포함 하는 `wsrm:Accept` 요소를 형성 하는 상관 관계가 지정 된 두 개의 역방향 시퀀스 또는 거부 된 `CreateSequence`요청 합니다.

- R1104: 역방향 시퀀스로 이동하는 `SequenceAcknowledgement` 및 애플리케이션 메시지는 `ReplyTo`의 `CreateSequence` 엔드포인트 참조로 보내야 합니다.

- R1105: `AcksTo`의 `ReplyTo` 및 `CreateSequence` 엔드포인트 참조에는 8비트 형식과 일치하는 주소 값이 있어야 합니다.

  WCF 응답자 확인의 URI 부분이 합니다 `AcksTo` 및 `ReplyTo` 시퀀스를 만들기 전에 EPRs 동일 합니다.

- R1106: `AcksTo`의 `ReplyTo` 및 `CreateSequence` 엔드포인트 참조에는 동일한 참조 매개 변수 집합이 있어야 합니다.

  WCF 하지 않지만 가정 [참조 매개 변수는]의 `AcksTo` 하 고 `ReplyTo` 에 `CreateSequence` 에서 [참조 매개 변수]를 사용 하 여 동일 `ReplyTo` 승인 및 역방향 시퀀스 메시지에 대 한 끝점 참조 합니다.

- R1107: 두 개의 역방향 시퀀스를 사용 하 여 설정 된 경우는 `Offer` 메커니즘 `SequenceAcknowledgement` 및 역방향 시퀀스에서 응용 프로그램 메시지를 보내야 합니다를 `ReplyTo` 의 끝점 참조는 `CreateSequence`합니다.

- R1108: Offer 메커니즘을 사용 하 여 두 개의 역방향 시퀀스가 설정 된 경우는 `[address]` 의 속성을 `wsrm:AcksTo` 끝점 참조 자식 요소의 `wsrm:Accept` 요소의 `CreateSequenceResponse` 일치 해야 바이트 별 대상 URI는 `CreateSequence`.

- R1109: 두 개의 역방향 시퀀스를 사용 하 여 설정 된 경우는 `Offer` 메커니즘, 초기자 및 응답자의 메시지 승인을 보낸 메시지를 같은 끝점 참조로 보내야 합니다.

  WCF는 개시자와 응답자 간에 신뢰할 수 있는 세션을 설정 하려면 Ws-reliable Messaging을 사용 합니다. WCF의 Ws-reliable Messaging 구현에서는 단방향, 요청-회신 및 전체에 대 한 신뢰할 수 있는 세션 제공 이중 메시징 패턴입니다. Ws-reliable Messaging `Offer` 메커니즘 `CreateSequence` / `CreateSequenceResponse` 두 상관 관계가 지정 된 역방향 시퀀스를 설정할 수 있습니다 하 고 모든 메시지 끝점에 적합 한 세션 프로토콜을 제공 합니다. WCF는 세션 무결성에 대 한 종단 간 보호를 포함 하 여 세션에 대 한 보안 보장을 제공 하므로 같은 상대방 메시지가 동일한 대상에 도착 하는 확인 여기이 유용 합니다. 이렇게 하면 애플리케이션 메시지에서 피기백킹이라고 하는 시퀀스 승인을 사용할 수 있습니다. 따라서 제약 조건 R1104, R1105, 및 R1108 WCF에 적용 됩니다.

`CreateSequence` 메시지의 예입니다.

```xml
<s:Envelope>
  <s:Header>
    <a:Action s:mustUnderstand="1">
      http://schemas.xmlsoap.org/ws/2005/02/rm/CreateSequence
    </a:Action>
    <a:ReplyTo>
      <a:Address>
         http://Business456.com/clientA
      </a:Address>
    </a:ReplyTo>
    <a:MessageID>
      urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36
    </a:MessageID>
    <a:To s:mustUnderstand="1">
      http://Business456.com/clientA
    </a:To>
  </s:Header>
  <s:Body>
    <wsrm:CreateSequence>
      <wsrm:AcksTo>
       <wsa:Address>
         http://Business456.com/clientA
       </wsa:Address>
     </wsrm:AcksTo>
     <wsrm:Offer>
      <wsrm:Identifier>
        urn:uuid:0afb8d36-bf26-4776-b8cf-8c91fddb5496
      </wsrm:Identifier>
     </wsrm:Offer>
   </wsrm:CreateSequence>
  </s:Body>
</s:Envelope>
```

 `CreateSequenceResponse` 메시지의 예입니다.

```xml
<s:Envelope>
  <s:Header>
    <a:Action s:mustUnderstand="1">
      http://schemas.xmlsoap.org/ws/2005/02/rm/CreateSequenceResponse
    </a:Action>
    <a:RelatesTo>
      urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36
    </a:RelatesTo>
    <a:To s:mustUnderstand="1">
      http://Business456.com/clientA
    </a:To>
  </s:Header>
  <s:Body>
   <wsrm:CreateSequenceResponse>
    <Identifier>
     urn:uuid:eea0a36c-b38a-43e8-8c76-2fabe2d76386
    </Identifier>
    <Accept>
    <AcksTo>
      <a:Address>
        http://BusinessABC.com/serviceA
      </a:Address>
    </AcksTo>
    </Accept>
   </wsrm:CreateSequenceResponse>
  </s:Body>
</s:Envelope>
```

### <a name="sequence"></a>Sequence

다음은 시퀀스에 적용되는 제약 조건의 목록입니다.

- B1201:WCF 생성 하 고 액세스 시퀀스 번호 보다 높은 `xs:long`의 최대 포함 값, 9223372036854775807 합니다.

- B1202:WCF 동작 URI와 본문이 비어 있는 마지막 메시지를 항상 생성의 `http://schemas.xmlsoap.org/ws/2005/02/rm/LastMessage`합니다.

- B1203: WCF 수신 하 고 포함 된 시퀀스 헤더가 있는 메시지를 배달 한 `LastMessage` 요소가 동작 URI가 아닌 `http://schemas.xmlsoap.org/ws/2005/02/rm/LastMessage`합니다.

시퀀스 헤더의 예입니다.

```xml
<wsrm:Sequence>
  <wsrm:Identifier>
    urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36
  </wsrm:Identifier>
  <wsrm:MessageNumber>
    10
  </wsrm:MessageNumber>
  <wsrm:LastMessage/>
 </wsrm:Sequence>
```

### <a name="ackrequested-header"></a>AckRequested 헤더

WCF를 사용 하 여 `AckRequested` 헤더를 연결 유지 메커니즘으로 합니다. WCF에서 선택적 생성 되지 않습니다 `MessageNumber` 요소입니다. 사용 하 여 메시지를 받으면를 `AckRequested` 포함 된 헤더를 `MessageNumber` 요소에 WCF 무시를 `MessageNumber` 요소의 값을 다음 예와에서 같이 합니다.

```xml
<wsrm:AckRequested>
  <wsrm:Identifier>
    urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36
  </wsrm:Identifier>
</wsrm:AckRequested>
```

### <a name="sequenceacknowledgement-header"></a>SequenceAcknowledgement 헤더

WCF는 Ws-reliable Messaging에 제공 된 시퀀스 승인에 피기백 메커니즘을 사용 합니다.

- R1401: 두 개의 역방향 시퀀스를 사용 하 여 설정 된 경우는 `Offer` 메커니즘을 `SequenceAcknowledgement` 받는 사람된에 게 전송 된 모든 응용 프로그램 메시지에서 헤더를 포함 될 수 있습니다.

- B1402: WCF 시퀀스 메시지를 받기 전에 승인을 생성 해야 하면 (예를 들어 충족 하는 `AckRequested` 메시지), WCF 생성를 `SequenceAcknowledgement` 다음 예제 에서처럼 0-0 범위가 포함 된 헤더.

  ```xml
  <wsrm:SequenceAcknowledgement>
    <wsrm:Identifier>
      urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36
    </wsrm:Identifier>
    <wsrm:AcknowledgementRange Upper="0" Lower="0"/>
  </wsrm:SequenceAcknowledgement>
  ```

- B1403: WCF를 생성 하지 않습니다 `SequenceAcknowledgement` 포함 하는 헤더를 `Nack` 요소가 있지만 지원 `Nack` 요소입니다.

### <a name="ws-reliablemessaging-faults"></a>WS-ReliableMessaging 오류

다음은 Ws-reliable Messaging 오류의 WCF 구현에 적용 되는 제약 조건의 목록입니다.

- B1501: WCF를 생성 하지 않습니다 `MessageNumberRollover` 오류입니다.

- B1502:WCF 끝점 발생할 `CreateSequenceRefused` 사양에 설명 된 대로 오류가 발생 합니다.

- WCF에서는 오류가 발생 하는 추가, B1503:When 서비스 끝점이 해당 연결 제한에 도달 하 고 새 연결을 처리할 수 없습니다 `CreateSequenceRefused` 오류 하위 코드, `netrm:ConnectionLimitReached`다음 예제에서와 같이 합니다.

  ```xml
  <s:Envelope>
    <s:Header>
      <wsa:Action>
        http://schemas.xmlsoap.org/ws/2005/08/addressing/fault
      </wsa:Action>
    </s:Header>
    <s:Body>
      <s:Fault>
        <s:Code>
          <s:Value>
            s:Receiver
          </s:Value>
          <s:Subcode>
            <s:Value>
              wsrm:CreateSequenceRefused
            </s:Value>
            <s:Subcode>
              <s:Value>
                netrm:ConnectionLimitReached
              </s:Value>
            </s:Subcode>
          </s:Subcode>
        </s:Code>
        <s:Reason>
          <s:Text xml:lang="en">
            [Reason]
          </s:Text>
        </s:Reason>
      </s:Fault>
    </s:Body>
  </s:Envelope>
  ```

### <a name="ws-addressing-faults"></a>WS-Addressing 오류

Ws-reliable Messaging에서는 Ws-addressing 때문에 WCF Ws-reliable Messaging 구현 Ws-addressing 오류를 생성할 수 있습니다. 이 섹션에서는 WCF Ws-reliable Messaging 계층에서 명시적으로 생성 하는 Ws-addressing 오류에 설명 합니다.

- 다음 중 하나가 true 인 경우 B1601:WCF 메시지 주소 지정 헤더 필요 오류를 생성 합니다.

  - 메시지에 `Sequence` 헤더 및 `Action` 헤더가 없습니다.

  - `CreateSequence` 메시지에 `MessageId` 헤더가 없습니다.

  - `CreateSequence` 메시지에 `ReplyTo` 헤더가 없습니다.

- B1602:WCF 누락 된 메시지, 작업 지원 되지 않습니다 오류를 생성 한 `Sequence` 헤더 있고는 `Action` Ws-reliable Messaging 사양에서 인식 되지 않는 헤더입니다.

- B1603:WCF 끝점에서 사용할 수 없게 끝점 검사에 따라 시퀀스를 처리 하지 않습니다 나타냅니다 오류를 생성 합니다 `CreateSequence` 메시지의 주소 지정 헤더입니다.

## <a name="protocol-composition"></a>프로토콜 구성

### <a name="composition-with-ws-addressing"></a>WS-Addressing을 사용하여 구성

WCF에서는 두 가지 버전을의 Ws-addressing을 지원합니다. Ws-addressing 2004/08 [WS-ADDR]과 W3C Ws-addressing 1.0 권장 사항 [WS-ADDR-CORE] 및 [SOAP-WS-ADDR].

WS-Reliable Messaging 사양에는 WS-Addressing 2004/08만 언급되어 있지만 WS-Addressing 버전만 사용하도록 제한되지는 않습니다. 다음은 WCF에 적용 되는 제약 조건의 목록입니다.

- R2101: 두 Ws-addressing 2004/08과 Ws-addressing 1.0 Ws-reliable Messaging과 함께 사용할 수 있습니다.

- 제공 된 Ws-reliable Messaging 시퀀스 또는 한 쌍의 역방향 시퀀스를 사용 하 여 상관 관계가 지정 된 전체 R2102:A 단일 버전의 Ws-addressing을 사용 해야 합니다는 `wsrm:Offer` 메커니즘입니다.

### <a name="composition-with-soap"></a>SOAP를 사용하여 구성

WCF는 SOAP 1.1 및 SOAP 1.2 Ws-reliable Messaging를 모두 사용할 수 있도록 지원 합니다.

### <a name="composition-with-ws-security-and-ws-secureconversation"></a>WS-Security 및 WS-SecureConversation을 사용하여 구성

WCF 보안 전송 (HTTPS), Ws-security를 사용 하 여 구성 및 컴퍼지션 Ws-secure Conversation을 사용 하 여 사용 하 여 Ws-reliable Messaging 시퀀스에 대 한 보호를 제공 합니다. 다음은 WCF에 적용 되는 제약 조건의 목록입니다.

- R2301: 개별 메시지의 무결성 뿐만 아니라 Ws-reliable Messaging 시퀀스의 무결성 및 기밀성을 보호 하려면 WCF가 Ws-secure Conversation을 사용 해야 해야 합니다.

- R2302:AWS-보안 대화 세션 Ws-reliable Messaging 시퀀스를 설정 하기 전에 설정 해야 합니다.

- R2303: Ws-reliable Messaging 시퀀스 수명이 Ws-secure Conversation 세션의 수명을 초과 하는 경우는 `SecurityContextToken` Ws-secure Conversation 갱신을 해당 Ws-secure Conversation 갱신 바인딩을 사용 하 여 사용 하 여 설정 합니다.

- B2304:WS-신뢰할 수 있는 메시징 시퀀스 또는 한 쌍의 상호 관련 된 역방향 시퀀스는 항상 단일 Ws-secureconversation 세션에 바인딩됩니다.

  WCF 소스를 생성 합니다 `wsse:SecurityTokenReference` 의 요소 확장성 섹션에 있는 요소를 `CreateSequence` 메시지입니다.

- R2305:When Ws-secure Conversation을 사용 하 여 구성을 `CreateSequence` 메시지에 포함 해야 합니다는 `wsse:SecurityTokenReference` 요소입니다.

## <a name="ws-reliable-messaging-ws-policy-assertion"></a>WS-Reliable Messaging WS-Policy Assertion

Ws-reliable Messaging Ws-policy Assertion을 사용 하 여 WCF `wsrm:RMAssertion` 끝점 기능을 설명 합니다. 다음은 WCF에 적용 되는 제약 조건의 목록입니다.

- B3001: WCF 첨부 `wsrm:RMAssertion` Ws-policy Assertion을 `wsdl:binding` 요소입니다. WCF에는 첨부 파일을 모두 지 원하는 `wsdl:binding` 고 `wsdl:port` 요소입니다.

- B3002: Ws-reliable Messaging 어설션의 다음과 같은 선택적 속성을 지원 하 고 WCF에 제어를 제공 하는 WCF`ReliableMessagingBindingElement`:

  - `wsrm:InactivityTimeout`

  - `wsrm:AcknowledgementInterval`

  다음은 예제입니다.

  ```xml
  <wsrm:RMAssertion>
    <wsrm:InactivityTimeout Milliseconds="600000" />
    <wsrm:AcknowledgementInterval Milliseconds="200" />
  </wsrm:RMAssertion>
  ```

## <a name="flow-control-ws-reliable-messaging-extension"></a>흐름 제어 WS-Reliable Messaging 확장

WCF를 시퀀스 메시지 흐름 선택적 추가 긴밀 하 게 제어할 수 있도록 확장성 Ws-reliable Messaging을 사용 합니다.

흐름 제어를 설정 하 여 활성화 합니다 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.FlowControlEnabled?displayProperty=nameWithType> 속성을 `true`입니다. 다음은 WCF에 적용 되는 제약 조건의 목록입니다.

- B4001: WCF를 생성 하는 신뢰할 수 있는 메시징 흐름 제어를 사용 하는 경우는 `netrm:BufferRemaining` 의 요소 확장성에 요소를 `SequenceAcknowledgement` 헤더입니다.

- B4002: WCF 신뢰할 수 있는 메시징 흐름 제어를 사용 하는 경우 필요 하지 않습니다는 `netrm:BufferRemaining` 요소에 `SequenceAcknowledgement` 헤더를 다음 예제에서와 같이 합니다.

  ```xml
  <wsrm:SequenceAcknowledgement>
    <wsrm:Identifier>
      http://fabrikam123.com/abc
    </wsrm:Identifier>
    <wsrm:AcknowledgementRange Upper="1" Lower="1"/>
    <netrm:BufferRemaining>
      8
    </netrm:BufferRemaining>
  </wsrm:SequenceAcknowledgement>
  ```

- B4003: WCF를 사용 하 여 `netrm:BufferRemaining` 얼마나 많은 신뢰할 수 있는 메시징 대상에 새 메시지를 나타내기 위해 버퍼링 할 수 있습니다.

- B4004: WCF 신뢰할 수 있는 메시징 서비스를 신뢰할 수 있는 메시징 대상 응용 프로그램은 메시지를 빠르게 수신할 수 있는 경우 전송 된 메시지의 수를 제한 합니다. 신뢰할 수 있는 메시징 대상은 메시지를 버퍼링하고 요소의 값을 0으로 줄입니다.

- B4005: WCF 생성 `netrm:BufferRemaining` 정수는 0과 4096 사이의 값을 읽고 0 사이의 정수 값 및 `xs:int`의 `maxInclusive` 값 214748364 합니다.

## <a name="message-exchange-patterns"></a>메시지 교환 패턴

이 섹션에서는 다른 메시지 교환 패턴에 사용 되는 Ws-reliable Messaging 경우 WCF의 동작을 설명 합니다. 각 메시지 교환 패턴에 대해 다음 두 가지 배포 시나리오를 고려합니다.

- 주소를 지정할 수 없는 개시자: 개시자가 방화벽; 응답자는 HTTP 응답 에서만 개시자에 게 메시지를 배달할 수 있습니다.

- 초기자 주소 지정 가능 합니다. 개시자와 응답자 모두 HTTP 요청에 보낼 수 즉, 두 개의 역방향 HTTP 연결을 설정할 수 있습니다.

### <a name="one-way-non-addressable-initiator"></a>주소를 지정할 수 없는 단방향 개시자

#### <a name="binding"></a>바인딩

WCF에는 하나의 HTTP 채널을 통해 하나의 시퀀스를 사용 하 여 단방향 메시지 교환 패턴을 제공 합니다. WCF는 HTTP 요청을 사용 하 여 rms rmd에 게 모든 메시지를 rmd에 게 HTTP 응답을 RMS에서 모든 메시지를 전송 합니다.

#### <a name="createsequence-exchange"></a>CreateSequence 교환

WCF 시작 자가 생성을 `CreateSequence` 제공 하지 않는 메시지입니다. WCF 응답자는 `CreateSequence` 에서 시퀀스를 만들기 전에 제공 되지 않습니다. WCF 응답자는 회신 합니다 `CreateSequence` 사용 하 여 요청을 `CreateSequenceResponse` 메시지입니다.

#### <a name="sequenceacknowledgement"></a>SequenceAcknowledgement

WCF 초기자를 제외한 모든 메시지의 회신에 대 한 승인을 처리 합니다 `CreateSequence` 메시지와 오류 메시지입니다. WCF 응답자는 항상 독립 실행형 승인을 두 시퀀스에 대 한 응답에서 생성 및 `AckRequested` 메시지입니다.

#### <a name="terminatesequence-message"></a>TerminateSequence 메시지

WCF는 처리 `TerminateSequence` 단방향 작업으로는 빈 본문과 HTTP 202 상태 코드가 HTTP 응답을 의미 합니다.

### <a name="one-way-addressable-initiator"></a>주소를 지정할 수 있는 단방향 개시자

#### <a name="binding"></a>바인딩

WCF에는 한 개의 시퀀스를 통해 인바운드 및 아웃 바운드 Http 채널을 사용 하 여 단방향 메시지 교환 패턴을 제공 합니다. WCF는 HTTP 요청을 사용 하 여 모든 메시지를 전송 합니다. 모든 HTTP 응답에는 빈 본문과 HTTP 202 상태 코드가 포함됩니다.

#### <a name="createsequence-exchange"></a>CreateSequence 교환

WCF 시작 자가 생성을 `CreateSequence` 제공 하지 않는 메시지입니다. WCF 보안 응답자는 `CreateSequence` 에서 시퀀스를 만들기 전에 제공 되지 않습니다. WCF 응답자 전송 합니다 `CreateSequenceResponse` 메시지는 HTTP 요청에 사용 하 여 해결 합니다 `ReplyTo` 끝점 참조 합니다.

### <a name="duplex-addressable-initiator"></a>주소를 지정할 수 있는 이중 개시자

#### <a name="binding"></a>바인딩

WCF에는 두 시퀀스를 사용 하 여 인바운드 및 아웃 바운드 HTTP 채널을 통해 완전히 비동기적인 양방향 메시지 교환 패턴을 제공 합니다. WCF는 HTTP 요청을 사용 하 여 모든 메시지를 전송 합니다. 모든 HTTP 응답에는 빈 본문과 HTTP 202 상태 코드가 포함됩니다.

#### <a name="createsequence-exchange"></a>CreateSequence 교환

WCF 시작 자가 생성을 `CreateSequence` 제품을 사용 하 여 메시지입니다. WCF 보안 응답자는 `CreateSequence` 에서 시퀀스를 만들기 전에 제공 합니다. WCF 전송 합니다 `CreateSequenceResponse` 로 주소가 지정 된 HTTP 요청에는 `CreateSequence`의 `ReplyTo` 끝점 참조 합니다.

#### <a name="sequence-lifetime"></a>시퀀스 수명

WCF 개의 전체 이중 세션으로 두 시퀀스를 처리합니다.

한 개의 시퀀스를 오류는 오류를 생성 하면 WCF는 두 시퀀스를 오류 원격 끝점이 필요 합니다. 한 개의 시퀀스를 오류는 오류를 읽으면 WCF에는 두 시퀀스 오류입니다.

WCF 해당 아웃 바운드 시퀀스 닫고 해당 인바운드 시퀀스에서 메시지를 계속 처리할 수 있습니다. 반대로, WCF에서는 인바운드 시퀀스의 종료를 처리 하 고 계속 해 서 해당 아웃 바운드 시퀀스에서 메시지를 보낼 수 있습니다.

### <a name="request-reply-non-addressable-initiator"></a>요청-회신, 주소를 지정할 수 없는 개시자

#### <a name="binding"></a>바인딩

하나를 통해 HTTP 채널을 시퀀스 하는 두 개를 사용 하 여 요청-회신 메시지 교환 패턴 및 WCF 단방향 제공 합니다. WCF는 HTTP 요청을 사용 하 여 요청 시퀀스 메시지를 전송 하 고 HTTP 응답을 사용 하 여 회신 시퀀스의 메시지를 전송 합니다.

#### <a name="createsequence-exchange"></a>CreateSequence 교환

WCF 시작 자가 생성을 `CreateSequence` 제품을 사용 하 여 메시지입니다. WCF 보안 응답자는 `CreateSequence` 에서 시퀀스를 만들기 전에 제공 합니다. WCF 응답자는 회신 합니다 `CreateSequence` 사용 하 여 요청을 `CreateSequenceResponse` 메시지입니다.

#### <a name="one-way-message"></a>단방향 메시지

단방향 메시지 교환 프로토콜을 성공적으로 완료 하려면 WCF 초기자 HTTP 요청에 요청 시퀀스 메시지를 전송 하 고 독립 실행형 받습니다 `SequenceAcknowledgement` HTTP 응답에는 메시지입니다. `SequenceAcknowledgement`는 전송된 메시지를 승인해야 합니다.

WCF 응답자는 승인, 오류 또는 빈 본문과 HTTP 202 상태 코드가 포함 된 응답을 사용 하 여 요청에 회신할 수 있습니다.

#### <a name="two-way-messages"></a>양방향 메시지

양방향 메시지 교환 프로토콜을 성공적으로 완료 하려면 WCF 초기자 HTTP 요청에 요청 시퀀스 메시지를 전송 하 고 HTTP 응답에 회신 시퀀스 메시지를 수신 합니다. 응답에 전송된 요청 시퀀스 메시지를 승인하는 `SequenceAcknowledgement`가 있어야 합니다.

WCF 응답자는 응용 프로그램 회신, 오류 또는 빈 본문과 HTTP 202 상태 코드가 포함 된 응답을 사용 하 여 요청에 회신할 수 있습니다.

단방향 메시지가 있고 애플리케이션이 회신하는 시간 때문에 요청 시퀀스 메시지의 시퀀스 번호와 응답 메시지의 시퀀스 번호는 상관 관계가 없습니다.

#### <a name="retrying-replies"></a>회신 다시 시도

WCF 양방향 메시지 교환 프로토콜 상관 관계에 대 한 HTTP 요청-회신 상관 관계에 의존합니다. 이 인해 WCF 초기자 해도 요청 시퀀스 메시지가 승인 되 면 있지만 HTTP 응답에는 승인, 사용자 메시지 또는 오류를 전달 하는 경우에 대신 요청 시퀀스 메시지를 다시 시도 합니다. WCF 응답자는 회신이 상호 관련 된 요청의 HTTP 요청 레그에서 회신을 다시 시도 합니다.

#### <a name="lastmessage-exchange"></a>LastMessage 교환

WCF 개시자를 생성 하 여 HTTP 요청 레그에서 본문이 비어 마지막 메시지를 전송 합니다. WCF는 응답이 필요 하지만 실제 응답 메시지를 무시 합니다. WCF 응답 자가 요청 시퀀스의 본문이 비어 있는 마지막 메시지에 회신 시퀀스의 본문이 비어 있는 마지막 메시지를 사용 하 여 회신합니다.

WCF 응답자는 동작 URI가 아닌 마지막 메시지를 받으면 `http://schemas.xmlsoap.org/ws/2005/02/rm/LastMessage`, 마지막 메시지를 사용 하 여 WCF 응답 합니다. 양방향 메시지 교환 프로토콜의 경우 마지막 메시지에 애플리케이션 메시지가 포함되어 있으며, 단방향 메시지 교환 프로토콜의 경우 마지막 메시지는 비어 있습니다.

WCF 응답자는 회신 시퀀스의 본문이 비어 있는 마지막 메시지에 대 한 승인이 필요 하지 않습니다.

#### <a name="terminatesequence-exchange"></a>TerminateSequence 교환

WCF 초기자 생성 및 전송 요청 시퀀스의 모든 요청이 유효한 회신을 수신 하는 경우 `TerminateSequence` HTTP 요청 레그에서 메시지입니다. WCF는 응답이 필요 하지만 실제 응답 메시지를 무시 합니다. 요청 시퀀스에 회신 하는 WCF 응답자 `TerminateSequence` 회신 시퀀스의 메시지 `TerminateSequence` 메시지입니다.

정상적인 종료 시퀀스에서 두 `TerminateSequence` 메시지 모두에 전체 범위의 `SequenceAcknowledgement`가 포함되어 있습니다.

### <a name="requestreply-addressable-initiator"></a>요청/회신, 주소를 지정할 수 있는 개시자

#### <a name="binding"></a>바인딩

WCF에는 두 시퀀스를 통해 인바운드 및 아웃 바운드 HTTP 채널을 사용 하 여 요청-회신 메시지 교환 패턴을 제공 합니다. WCF는 HTTP 요청을 사용 하 여 모든 메시지를 전송 합니다. 모든 HTTP 응답에는 빈 본문과 HTTP 202 상태 코드가 포함됩니다.

#### <a name="createsequence-exchange"></a>CreateSequence 교환

WCF 시작 자가 생성을 `CreateSequence` 제품을 사용 하 여 메시지입니다. WCF 보안 응답자는 `CreateSequence` 에서 시퀀스를 만들기 전에 제공 합니다. WCF 전송 합니다 `CreateSequenceResponse` 로 주소가 지정 된 HTTP 요청에는 `CreateSequence`의 `ReplyTo` 끝점 참조 합니다.

#### <a name="requestreply-correlation"></a>요청/회신 상관 관계

WCF 시작 자가 있는지 확인 모든 응용 프로그램 요청 메시지를 `MessageId` 및 `ReplyTo` 끝점 참조 합니다. WCF 초기자 적용 되는 `CreateSequence` 메시지의 `ReplyTo` 각 응용 프로그램 요청 메시지에 대 한 끝점 참조 합니다. WCF 응답자 필요는 들어오는 요청 메시지를 `MessageId` 및 `ReplyTo`합니다. WCF 응답자 되도록 둘 다의 끝점 참조의 URI는 `CreateSequence` 모든 응용 프로그램 요청 메시지 동일 합니다.
