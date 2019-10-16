---
title: 신뢰할 수 있는 세션 개요
ms.date: 03/30/2017
ms.assetid: a7fc4146-ee2c-444c-82d4-ef6faffccc2d
ms.openlocfilehash: 6dd90ef800daf236d77c419d48c0857ac2d78aa2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61962659"
---
# <a name="reliable-sessions-overview"></a>신뢰할 수 있는 세션 개요

Windows Communication Foundation (WCF) SOAP 신뢰할 수 있는 메시징은 SOAP 끝점 사이 종단 간 메시지 전송 안전성을 제공합니다. 전송 오류 및 SOAP 메시지 수준 오류를 극복하여 신뢰할 수 없는 네트워크에서 이를 구현합니다. 특히 SOAP 또는 전송 매개자를 통해 보낸 메시지에 대해 세션 기반, 단일 및 필요에 따라 순서가 지정된 배달을 제공합니다. 세션 기반 배달은 선택적 메시지 순서 지정 된 세션의 메시지를 그룹화를 제공 합니다.

이 항목에서는 신뢰할 수 있는 세션을 하는 방법을 설명 하를 사용 하는 경우 및 보안을 유지 하는 방법입니다.

## <a name="wcf-reliable-sessions"></a>WCF 신뢰할 수 있는 세션

WCF 신뢰할 수 있는 세션은 WS-ReliableMessaging 프로토콜에 의해 정의 된 대로 메시징 신뢰할 수 있는 soap 구현 합니다.

WCF SOAP 신뢰할 수 있는 메시징은 메시징 끝점을 구분 하는 매개 자의 형식이 나 개수에 관계 없이 두 개의 끝점 사이 종단 간 신뢰할 수 있는 세션을 제공 합니다. 여기에 SOAP (예를 들어, HTTP 프록시)를 사용 하지 않는 전송 매개자 또는 끝점 간의 메시지 흐름에 필요한 SOAP (예를 들어 SOAP 기반 라우터나 브리지)를 사용 하는 매개자입니다. 신뢰할 수 있는 세션 채널을 지 원하는 *대화형* 통신 이러한 채널에 의해 연결 된 서비스가 동시에 실행 하 고 교환 하 고 처리할 메시지의 짧은 대기 시간, 즉, 조건 내에서 상대적으로 짧은 있도록 시간 간격입니다. 이 결합 되므로 이러한 구성 요소 함께 진행 되거나 함께 실패 하는 서로 격리 되지 않습니다.

신뢰할 수 있는 세션에서는 다음 두 가지 유형의 오류를 마스킹합니다.

- 손실되거나 중복된 메시지 및 보낸 순서와 다른 순서로 도착한 메시지를 포함하는 SOAP 메시지 수준 오류

- 전송 오류

신뢰할 수 있는 세션은 WS-ReliableMessaging 프로토콜 및 내장 메모리 전송 창을 구현하여 SOAP 메시지 수준 오류를 마스킹하고 전송 오류가 발생할 경우 다시 연결합니다.

신뢰할 수 있는 세션은 TCP가 IP 패킷에 대해 제공하는 SOAP 메시지를 제공합니다. TCP 소켓 연결은 노드 간에 IP 패킷에 대한 단수형의 순서가 지정된 전송을 제공합니다. 신뢰할 수 있는 채널은 신뢰할 수 있는 전송과 동일한 유형을 제공하지만 다음과 같은 방법에서 TCP 소켓 안정성이 다릅니다.

- 안정성은 임의 크기 패킷(바이트)이 아닌 SOAP 메시지 수준에서 구현됩니다.

- 안정성은 TCP 통한 전송을 위해 뿐 아니라의 전송 중립적인 구현 됩니다.

- 안정성 특정 전송 세션 (예를 들어, TCP 연결을 제공 하는 세션)에 연결 되지 않습니다 및 따르면 여러 전송 세션 동시에 또는 순차적으로 신뢰할 수 있는 세션의 수명 동안.

- 신뢰할 수 있는 세션은 SOAP 엔드포인트 간의 연결에 필요한 전송 연결 수에 관계없이 발신자 및 수신자 SOAP 엔드포인트 사이에 위치합니다. 즉, TCP 안정성 전송 연결 끝나는, 종단 간 안정성을 제공 하는 신뢰할 수 있는 세션을 종료 합니다.

## <a name="reliable-sessions-and-bindings"></a>신뢰할 수 있는 세션 및 바인딩

앞에서 설명한 대로 신뢰할 수 있는 세션은 전송 중립적입니다. 또한 요청-회신 또는 이중와 같은 여러 메시지 교환 패턴을 통해 신뢰할 수 있는 세션을 설정할 수 있습니다. WCF 신뢰할 수 있는 세션 바인딩 집합의 속성으로 노출 됩니다.

사용 하는 끝점에서 신뢰할 수 있는 세션을 사용 합니다.

- HTTP 기반 전송 표준 바인딩:

  - `WsHttpBinding` 및 요청-회신 또는 단방향 계약을 노출합니다.

  - 요청-회신 또는 간단한 단방향 서비스 계약을 통해 신뢰할 수 있는 세션을 사용할 때

  - `WsDualHttpBinding` 및 이중, 요청-회신 또는 단방향 계약을 노출합니다.

  - `WsFederationHttpBinding` 및 요청-회신 또는 단방향 계약을 노출합니다.

- TCP 기반 전송 표준 바인딩:

  - `NetTcpBinding` 및 이중, 요청-회신 또는 단방향 계약을 노출합니다.

다른 바인딩에서 신뢰할 수 있는 세션을 사용 하 여 HTTPS와 같은 사용자 지정 바인딩을 만들어 (문제에 대 한 자세한 내용은 참조 하십시오 <a href="#reliable-sessions-and-security">신뢰할 수 있는 세션 및 보안</a>) 또는 명명된 된 파이프 바인딩의 합니다.

다른 기본 채널 형식에 대 한 신뢰할 수 있는 세션을 누적 할 수 있습니다 하 고 결과 신뢰할 수 있는 세션 채널 모양이 달라 집니다. 클라이언트와 서버 모두에서 지원 되는 신뢰할 수 있는 세션 채널 형식에 사용 되는 기본 채널의 형식에 따라 달라 집니다. 다음 표에서는 기본 채널 형식의 기능으로서 클라이언트에서 지원되는 세션 채널 형식에 대해 설명합니다.

| 지원 되는 신뢰할 수 있는 세션 채널 형식입니다.&#8224; | `IRequestChannel` | `IRequestSessionChannel` | `IDuplexChannel` | `IDuplexSessionChannel` |
| ----------------------------------------------- | :---------------: | :----------------------: | :--------------: | :---------------------: |
| `IOutputSessionChannel`                         | 예               | 예                      | 예              | 예                     |
| `IRequestSessionChannel`                        | 예               | 예                      | 아니요               | 아니요                      |
| `IDuplexSessionChannel`                         | 아니요                | 아니요                       | 예              | 예                     |

&#8224;지원 되는 채널 형식은 제네릭에 대 한 사용 가능한 값 `TChannel` 에 전달 되는 매개 변수 값을 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.BuildChannelFactory%60%601%28System.ServiceModel.Channels.BindingContext%29> 메서드.

다음 표에서는 기본 채널 형식의 기능으로서 서버에서 지원되는 세션 채널 형식에 대해 설명합니다.

| 지원 되는 신뢰할 수 있는 세션 채널 형식입니다.&#8225; | `IReplyChannel` | `IReplySessionChannel` | `IDuplexChannel` | `IDuplexSessionChannel` |
| ----------------------------------------------- | :-------------: | :--------------------: | :--------------: | :---------------------: |
| `IInputSessionChannel`                          | 예             | 예                    | 예              | 예                     |
| `IReplySessionChannel`                          | 예             | 예                    | 아니요               | 아니요                      |
| `IDuplexSessionChannel`                         | 아니요              | 아니요                     | 예              | 예                     |

&#8225;지원 되는 채널 형식은 제네릭에 대 한 사용 가능한 값 `TChannel` 에 전달 되는 매개 변수 값을 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.BuildChannelListener%60%601%28System.ServiceModel.Channels.BindingContext%29> 메서드.

## <a name="reliable-sessions-and-security"></a>신뢰할 수 있는 세션 및 보안

신뢰할 수 있는 세션을 보호 하는 것이 통신 당사자 (서비스 및 클라이언트) 인증 되 고 세션에서 교환 되는 메시지 변조 되지 않도록 해야 합니다. 또한 각 개별 신뢰할 수 있는 세션의 무결성을 확인 하는 것이 반드시 합니다. 신뢰할 수 있는 세션을 표시 하 고 보안 세션 채널에서 관리 하는 보안 컨텍스트에 바인딩하여 보안이 설정 됩니다. 보안 채널은 보안 세션을 제공합니다. 세션 설정 동안 교환된 보안 토큰은 신뢰할 수 있는 세션의 메시지 보안을 유지하는 데 사용됩니다.

신뢰할 수 있는 세션을 통해 경우 TCP 세션이 신뢰할 수 있는 세션에 연결 됩니다. 따라서 전송 보안 신뢰할 수 있는 세션에 보안 연결을 확인 합니다. 이 경우 연결 재설정이 꺼집니다.

HTTPS를 사용하는 경우에만 예외입니다. Secure Sockets Layer (SSL) 세션은 신뢰할 수 있는 세션에 바인딩되어 있지 않은 합니다. 세션 (SSL 세션) 보안 컨텍스트를 공유 하는 다른;에서 보호 되지 때문에이 위협으로 인해 이 수 또는 응용 프로그램에 따라 실제 위협이 되지 않을 수 있습니다.

## <a name="using-reliable-sessions"></a>신뢰할 수 있는 세션을 사용 하 여

WCF 신뢰할 수 있는 세션을 사용 하려면 신뢰할 수 있는 세션을 지 원하는 바인딩을 사용 하 여 끝점을 만듭니다. WCF 신뢰할 수 있는 세션을 사용 하 여 제공 하는 시스템 제공 바인딩 중 하나 사용 하 여 사용 하도록 설정 또는이 작업을 수행 하는 고유한 사용자 지정 바인딩을 만듭니다.

기본적으로 신뢰할 수 있는 세션을 지원하고 사용하도록 설정하는 시스템 정의 바인딩은 다음과 같습니다.

- <xref:System.ServiceModel.WSDualHttpBinding>

옵션으로 신뢰할 수 있는 세션을 지원 하지만 기본적으로 사용 하지 않는 시스템 제공 바인딩은 다음과 같습니다.

- <xref:System.ServiceModel.WSHttpBinding>

- <xref:System.ServiceModel.WSFederationHttpBinding>

- <xref:System.ServiceModel.NetTcpBinding>

사용자 지정 바인딩을 만드는 방법의 예제를 참조 하세요. [방법: HTTPS를 사용 하 여 사용자 지정 신뢰할 수 있는 세션 바인딩 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-reliable-session-binding-with-https.md)합니다.

신뢰할 수 있는 세션을 지 원하는 WCF 바인딩 설명은 참조 하세요 [System-Provided Bindings](../../../../docs/framework/wcf/system-provided-bindings.md)합니다.

## <a name="when-to-use-reliable-sessions"></a>신뢰할 수 있는 세션을 사용 하는 경우

응용 프로그램에서 신뢰할 수 있는 세션을 사용 하는 경우를 이해 하는 것이 반드시 합니다. WCF는 동시에 활성 및 활성 상태는 끝점 간에 신뢰할 수 있는 세션을 지원 합니다. 응용 프로그램에 필요한 끝점 중 하나가 시간의 기간 동안 사용할 수 없게 경우 안정성을 달성 하기 위해 큐를 사용 합니다.

시나리오에서 TCP를 통해 연결 하는 두 개의 끝점에 필요한 경우 TCP 신뢰할 수 있는 메시지 교환을 제공 하기에 충분할 수 있습니다. TCP 되도록 하므로 신뢰할 수 있는 세션을 사용 하는 것이 반드시 하지만 패킷 및 한 번만 순서 대로 도착 합니다.

시나리오는 다음과 같은 특징이 있는 있으면 다음 심각 하 게 고려해 야 신뢰할 수 있는 세션을 사용 하 여 합니다.

- SOAP 라우터와 같은 SOAP 매개자

- 프록시 매개자 또는 전송 브리지

- 일시적인 연결

- HTTP 통한 세션

## <a name="see-also"></a>참고자료

- [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
- [WS 신뢰할 수 있는 세션](../../../../docs/framework/wcf/samples/ws-reliable-session.md)
