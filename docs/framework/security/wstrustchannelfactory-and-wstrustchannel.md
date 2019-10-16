---
title: WSTrustChannelFactory 및 WSTrustChannel
ms.date: 03/30/2017
ms.assetid: 96cec467-e963-4132-b18b-7d0b3a2e979f
author: BrucePerlerMS
ms.openlocfilehash: e00f3ae25a50c2fb3f34f4c04d02cde574b3da17
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044910"
---
# <a name="wstrustchannelfactory-and-wstrustchannel"></a>WSTrustChannelFactory 및 WSTrustChannel
WCF(Windows Communication Foundation)에 알고 있다면 WCF 클라이언트가 이미 페더레이션을 인식한다는 것을 알고 있습니다. <xref:System.ServiceModel.WSFederationHttpBinding> 또는 유사한 사용자 지정 바인딩을 사용하여 WCF 클라이언트를 구성하면 서비스에 페더레이션된 인증을 사용하도록 설정할 수 있습니다.

 WCF는 백그라운드에서 STS(보안 토큰 서비스)가 발급한 토큰을 가져와 이 토큰을 사용해서 서비스에 인증합니다. 이 접근 방법의 주요 제한 사항은 서버와 클라이언트의 통신을 볼 수 없다는 점입니다. WCF는 바인딩에서 발급된 토큰 매개 변수에 따라 STS에 RST(요청 보안 토큰)를 자동으로 생성합니다. 이는 클라이언트가 요청별로 RST 매개 변수를 변경하거나, 표시 클레임 등의 정보를 가져오기 위해 RSTR(요청 보안 토큰 응답)을 검사하거나, 나중에 사용하기 위해 토큰을 캐시할 수 없음을 의미합니다.

 현재 WCF 클라이언트는 기본 페더레이션 시나리오에 적합합니다. 그러나 WIF(Windows Identity Foundation)가 지원하는 주요 시나리오 중 하나의 경우 WCF가 쉽게 허용하지 않는 수준에서 RST를 제어해야 합니다. 따라서 WIF는 STS와의 통신에 대한 제어를 강화하는 기능을 추가합니다.

 WIF는 다음과 같은 페더레이션 시나리오를 지원합니다.

- WIF 종속성 없이 WCF 클라이언트를 사용하여 페더레이션된 서비스에 인증

- WCF 클라이언트의 WIF가 STS에 대한 RST에 ActAs 또는 OnBehalfOf 요소를 삽입할 수 있도록 허용

- WIF를 단독으로 사용하여 STS에서 토큰을 가져온 다음 WCF 클라이언트가 이 토큰으로 인증할 수 있도록 설정 자세한 내용은 [ClaimsAwareWebService](https://go.microsoft.com/fwlink/?LinkID=248406) 샘플을 참조하세요.

 첫 번째 시나리오는 다음과 같이 설명이 필요 하지 않습니다. 기존 WCF 클라이언트는 WIF 신뢰 당사자 및 STSs와 계속 작동 합니다. 이 항목에서는 나머지 두 시나리오에 대해 설명합니다.

## <a name="enhancing-an-existing-wcf-client-with-actas--onbehalfof"></a>ActAs/OnBehalfOf를 사용하여 기존 WCF 클라이언트 향상
일반적인 ID 위임 시나리오에서 클라이언트는 중간 계층 서비스를 호출한 다음 백 엔드 서비스를 호출합니다. 중간 계층 서비스는 클라이언트로 작동하거나 클라이언트 대신 작동합니다.

> [!TIP]
> ActAs와 OnBehalfOf 간의 차이점은 무엇일까요?
>
> WS-TRUST 프로토콜 관점에서:
>
> 1. ActAs RST 요소는 요청자가 두 개의 고유 엔터티인 요청자와 ActAs 요소의 토큰이 나타내는 외부 엔터티에 대한 클레임을 포함하는 토큰을 원함을 나타냅니다.
> 2. OnBehalfOf RST 요소는 요청자가 OnBehalfOf 요소의 토큰이 나타내는 외부 엔터티 하나에 대한 클레임만 포함하는 토큰을 원함을 나타냅니다.
>
> ActAs 기능은 일반적으로 복합 위임이 필요한 시나리오에서 사용됩니다. 이 경우 발급된 토큰의 최종 수신자가 전체 위임 체인을 검사하고 클라이언트뿐 아니라 모든 매개 지점을 확인할 수 있습니다. 따라서 전체 ID 위임 체인에 따라 액세스 제어, 감사 및 기타 관련 활동을 수행할 수 있습니다. ActAs 기능은 일반적으로 애플리케이션/비즈니스 논리 계층에서 정보를 전달할 필요가 없도록 계층 간에 인증하고 ID 정보를 전달하기 위해 다중 계층 시스템에서 사용됩니다.
>
> OnBehalfOf 기능은 원래 클라이언트의 ID만 중요한 시나리오에서 사용되며, 실제로 Windows에서 사용할 수 있는 ID 가장 기능과 동일합니다. OnBehalfOf를 사용하는 경우 발급된 토큰의 최종 수신자는 원래 클라이언트에 대한 클레임만 볼 수 있으며, 매개 지점에 대한 정보는 유지되지 않습니다. OnBehalfOf 기능이 사용되는 한 가지 일반적인 패턴은 클라이언트가 STS에 직접 액세스할 수 없고 프록시 게이트웨이를 통해 통신하는 프록시 패턴입니다. 프록시 게이트웨이는 호출자를 인증하고 호출자에 대한 정보를 RST 메시지의 OnBehalfOf 요소에 넣은 다음 처리를 위해 실제 STS로 보냅니다. 결과 토큰에는 프록시의 클라이언트와 관련된 클레임만 포함되어 프록시를 발급된 토큰의 수신자에 완전히 투명하게 만듭니다. WIF는 \<wsse:SecurityTokenReference> 또는 \<wsa:EndpointReferences>를 \<wst:OnBehalfOf>의 자식으로 지원하지 않습니다. WS-Trust 사양에서는 프록시가 대신 작동하는 원래 요청자를 식별하는 세 가지 방법을 허용합니다. 이러한 항목은 다음과 같습니다.
>
> - 보안 토큰 참조. 메시지에 포함되어 있거나 대역 외에서 검색될 수 있는 토큰에 대한 참조입니다.
> - 엔드포인트 참조. 대역 외에서 다시 데이터를 조회하는 키로 사용됩니다.
> - 보안 토큰. 원래 요청자를 직접 식별합니다.
>
> WIF는 암호화되었거나 암호화되지 않은 보안 토큰만 \<wst:OnBehalfOf>의 직계 자식 요소로 지원합니다.

 이 정보는 RST의 ActAs 및 OnBehalfOf 토큰 요소를 사용하여 WS-Trust 발급자에게 전달됩니다.

 WCF는 임의의 XML 요소를 RST에 추가할 수 있게 해주는 확장성 지점을 바인딩에 노출합니다. 그러나 확장성 지점은 바인딩에 연결되어 있으므로 호출마다 RST 콘텐츠가 변경되어야 하는 시나리오에서는 각 호출에 대해 클라이언트를 다시 만들어야 하므로 성능이 저하됩니다. WIF는 `ChannelFactory` 클래스의 확장 메서드를 사용하여 개발자가 대역 외에서 가져온 토큰을 RST에 연결할 수 있게 합니다. 다음 코드 예제에서는 클라이언트를 나타내는 토큰(예: X.509, 사용자 이름 또는 SAML(Security Assertion Markup Language) 토큰)을 가져와서 발급자에게 전송되는 RST에 연결하는 방법을 보여 줍니다.

```csharp
IHelloService serviceChannel = channelFactory.CreateChannelActingAs<IHelloService>(clientSamlToken);
serviceChannel.Hello("Hi!");
```

 WIF는 다음과 같은 이점을 제공합니다.

- 채널별로 RST를 수정할 수 있으므로 중간 계층 서비스에서 각 클라이언트에 대한 채널 팩터리를 다시 만들 필요가 없으며 성능이 개선됩니다.

- 이 방법은 기존 WCF 클라이언트에서 작동하며, ID 위임 의미 체계를 설정하려는 기존 WCF 중간 계층 서비스에 편리한 업그레이드 경로를 사용할 수 있게 합니다.

 그러나 STS와 클라이언트의 통신은 여전히 볼 수 없습니다. 이 기능은 세 번째 시나리오에서 살펴보겠습니다.

## <a name="communicating-directly-with-an-issuer-and-using-the-issued-token-to-authenticate"></a>발급자와 직접 통신 및 발급된 토큰을 사용하여 인증
일부 고급 시나리오에서는 WCF 클라이언트 개선만으로 충분하지 않습니다. WCF만 사용하는 개발자는 일반적으로 메시지 인/메시지 아웃 계약을 사용하며 발급자 응답의 클라이언트 쪽 구문 분석을 수동으로 처리합니다.

WIF는 클라이언트가 WS-Trust 발급자와 직접 통신할 수 있게 해주는 <xref:System.ServiceModel.Security.WSTrustChannelFactory> 및 <xref:System.ServiceModel.Security.WSTrustChannel> 클래스를 도입합니다. <xref:System.ServiceModel.Security.WSTrustChannelFactory> 및 <xref:System.ServiceModel.Security.WSTrustChannel> 클래스는 다음 코드 예제와 같이 강력한 형식의 RST 및 RSTR 개체가 클라이언트와 발급자 간에 흐를 수 있게 합니다.

```csharp
WSTrustChannelFactory trustChannelFactory = new WSTrustChannelFactory(stsBinding, stsAddress);
WSTrustChannel channel = (WSTrustChannel) trustChannelFactory.CreateChannel();
RequestSecurityToken rst = new RequestSecurityToken(RequestTypes.Issue);
rst.AppliesTo = new EndpointAddress(serviceAddress);
RequestSecurityTokenResponse rstr = null;
SecurityToken token = channel.Issue(rst, out rstr);
```

<xref:System.ServiceModel.Security.WSTrustChannel.Issue%2A> 메서드의 `out` 매개 변수는 클라이언트 쪽 검사를 위한 RSTR 액세스를 허용합니다.

지금까지 토큰을 가져오는 방법만 살펴보았습니다. <xref:System.ServiceModel.Security.WSTrustChannel> 개체에서 반환되는 토큰은 신뢰 당사자에 인증하는 데 필요한 모든 정보를 포함하는 `GenericXmlSecurityToken`입니다. 다음 코드 예제에서는 이 토큰을 사용하는 방법을 보여 줍니다.

```csharp
IHelloService serviceChannel = channelFactory.CreateChannelWithIssuedToken<IHelloService>( token );
serviceChannel.Hello("Hi!");
```

`ChannelFactory` 개체의 <xref:System.ServiceModel.ChannelFactory%601.CreateChannelWithIssuedToken%2A> 확장 메서드는 대역 외에서 토큰을 가져왔으며, 발급자에 대한 일반적인 WCF 호출을 중지하고, 대신 가져온 토큰을 사용하여 신뢰 당사자에 인증해야 함을 WIF에 나타냅니다. 이 경우 다음과 같은 이점이 있습니다.

- 토큰 발급 프로세스를 완전히 제어할 수 있습니다.

- 나가는 RST에 이러한 속성을 직접 설정하여 ActAs/OnBehalfOf 시나리오를 지원합니다.

- RSTR의 내용에 따라 동적 클라이언트 쪽 트러스트를 결정할 수 있습니다.

- <xref:System.ServiceModel.Security.WSTrustChannel.Issue%2A> 메서드에서 반환되는 토큰을 캐시하고 다시 사용할 수 있습니다.

- <xref:System.ServiceModel.Security.WSTrustChannelFactory> 및 <xref:System.ServiceModel.Security.WSTrustChannel>을 사용하면 WCF 모범 사례에 따라 채널 캐싱, 오류 및 복구 의미 체계를 제어할 수 있습니다.

## <a name="see-also"></a>참고자료

- [WIF 기능](wif-features.md)
