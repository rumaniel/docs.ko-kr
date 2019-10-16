---
title: '방법: SecurityBindingElement를 사용하여 사용자 지정 바인딩 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [WCF], creating custom bindings
ms.assetid: 203a9f9e-3a73-427c-87aa-721c56265b29
ms.openlocfilehash: da67d923b36d673c87c90ba79b72ad4e1fc64a0c
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988755"
---
# <a name="how-to-create-a-custom-binding-using-the-securitybindingelement"></a>방법: SecurityBindingElement를 사용하여 사용자 지정 바인딩 만들기
WCF (Windows Communication Foundation)에는 구성할 수 있지만 WCF에서 지 원하는 모든 보안 옵션을 구성할 때 완벽 한 유연성을 제공 하지는 않는 여러 시스템 제공 바인딩이 포함 되어 있습니다. 이 항목에서는 개별 바인딩 요소에서 직접 사용자 지정 바인딩을 만드는 방법에 대해 설명하고, 이와 같은 바인딩을 만들 때 지정할 수 있는 일부 보안 설정에 대해 강조합니다. 사용자 지정 바인딩을 만드는 방법에 대 한 자세한 내용은 [바인딩 확장](../../../../docs/framework/wcf/extending/extending-bindings.md)을 참조 하세요.  
  
> [!WARNING]
> <xref:System.ServiceModel.Channels.SecurityBindingElement>는 <xref:System.ServiceModel.Channels.IDuplexSessionChannel>가 <xref:System.ServiceModel.TransferMode>로 설정된 경우 TCP 전송에서 사용하는 기본 채널 셰이프인 <xref:System.ServiceModel.TransferMode.Buffered> 채널 셰이프를 지원하지 않습니다. 이 시나리오에서 <xref:System.ServiceModel.TransferMode>를 사용하려면 <xref:System.ServiceModel.TransferMode.Streamed>를 <xref:System.ServiceModel.Channels.SecurityBindingElement>으로 설정해야 합니다.  
  
## <a name="creating-a-custom-binding"></a>사용자 지정 바인딩 만들기  
 WCF에서 모든 바인딩은 *바인딩 요소로*구성 됩니다. 각 바인딩 요소는 <xref:System.ServiceModel.Channels.BindingElement> 클래스에서 파생됩니다. 표준 시스템 제공 바인딩의 경우 바인딩 요소가 자동으로 생성되어 구성되지만 일부 속성 설정을 사용자 지정할 수 있습니다.  
  
 이와 달리 사용자 지정 바인딩을 만들려면 바인딩 요소를 만들어 구성하고 바인딩 요소에서 <xref:System.ServiceModel.Channels.CustomBinding>을 만들어야 합니다.  
  
 이렇게 하려면 <xref:System.ServiceModel.Channels.BindingElementCollection> 클래스 인스턴스로 표시되는 컬렉션에 개별 바인딩 요소를 추가한 다음 `Elements`의 `CustomBinding` 속성을 해당 개체와 같게 만듭니다. 다음 순서로 바인딩 요소를 추가 해야 합니다. 트랜잭션 흐름, 신뢰할 수 있는 세션, 보안, 복합 이중, 단방향, 스트림 보안, 메시지 인코딩 및 전송입니다. 나열된 모든 바인딩 요소가 모든 바인딩에서 필요한 것은 아닙니다.  
  
## <a name="securitybindingelement"></a>SecurityBindingElement  
 세 가지 바인딩 요소가 메시지 수준 보안과 관련이 있으며 이러한 요소는 모두 <xref:System.ServiceModel.Channels.SecurityBindingElement> 클래스에서 파생됩니다. 이 세 가지는 <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>, <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 및 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>입니다. <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>는 혼합 모드 보안을 제공하는 데 사용됩니다. 다른 두 가지 요소는 메시지 계층이 보안을 제공할 때 사용합니다.  
  
 전송 수준 보안이 제공될 경우 다음과 같은 추가 클래스가 사용됩니다.  
  
- <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>  
  
- <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>  
  
- <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>  
  
## <a name="required-binding-elements"></a>필요한 바인딩 요소  
 바인딩에 결합하여 사용할 수 있는 바인딩 요소는 많습니다. 그러나 이러한 조합이 모두 올바른 것은 아닙니다. 이 단원에서는 보안 바인딩에 있어야 하는 필수 요소에 대해 설명합니다.  
  
 올바른 보안 바인딩은 다음을 비롯한 많은 요인에 의해 결정됩니다.  
  
- 보안 모드  
  
- 전송 프로토콜  
  
- 계약에 지정된 MEP(메시지 교환 패턴)  
  
 다음 표에서는 위 요인의 조합별로 올바른 바인딩 요소 스택 구성을 보여 줍니다. 이는 최소 요구 사항입니다. 메시지 인코딩 바인딩 요소, 트랜잭션 바인딩 요소 및 기타 바인딩 요소와 같은 추가 바인딩 요소를 바인딩에 추가할 수 있습니다.  
  
|보안 모드|전송|계약 메시지 교환 패턴|계약 메시지 교환 패턴|계약 메시지 교환 패턴|  
|-------------------|---------------|---------------------------------------|---------------------------------------|---------------------------------------|  
|||`Datagram`|`Request Reply`|`Duplex`|  
|전송|Https||||  
|||OneWayBindingElement|||  
|||HttpsTransportBindingElement|HttpsTransportBindingElement||  
||TCP||||  
|||OneWayBindingElement|||  
|||SSL 또는 Windows StreamSecurityBindingElement|SSL 또는 Windows StreamSecurityBindingElement|SSL 또는 Windows StreamSecurityBindingElement|  
|||TcpTransportBindingElement|TcpTransportBindingElement|TcpTransportBindingElement|  
|메시지|Http|SymmetricSecurityBindingElement|SymmetricSecurityBindingElement|SymmetricSecurityBindingElement (인증 모드 = Ws-secureconversation)|  
|||||CompositeDuplexBindingElement|  
|||OneWayBindingElement||OneWayBindingElement|  
|||HttpTransportBindingElement|HttpTransportBindingElement|HttpTransportBindingElement|  
||Tcp|SecurityBindingElement|SecurityBindingElement|SymmetricSecurityBindingElement (인증 모드 = Ws-secureconversation)|  
|||TcpTransportBindingElement|TcpTransportBindingElement|TcpTransportBindingElement|  
|혼합(메시지 자격 증명을 사용한 전송)|Https|TransportSecurityBindingElement|TransportSecurityBindingElement||  
|||OneWayBindingElement|||  
|||HttpsTransportBindingElement|HttpsTransportBindingElement||  
||TCP|TransportSecurityBindingElement|SymmetricSecurityBindingElement (인증 모드 = Ws-secureconversation)|SymmetricSecurityBindingElement (인증 모드 = Ws-secureconversation)|  
|||OneWayBindingElement|||  
|||SSL 또는 Windows StreamSecurityBindingElement|SSL 또는 Windows StreamSecurityBindingElement|SSL 또는 Windows StreamSecurityBindingElement|  
|||TcpTransportBindingElement|TcpTransportBindingElement|TcpTransportBindingElement|  
  
 SecurityBindingElement에 대해 구성 가능한 설정이 많이 있습니다. 자세한 내용은 [SecurityBindingElement 인증 모드](../../../../docs/framework/wcf/feature-details/securitybindingelement-authentication-modes.md)를 참조 하세요.  
  
 자세한 내용은 [보안 대화 및 보안 세션](../../../../docs/framework/wcf/feature-details/secure-conversations-and-secure-sessions.md)을 참조 하세요.  
  
## <a name="procedures"></a>절차  
  
#### <a name="to-create-a-custom-binding-that-uses-a-symmetricsecuritybindingelement"></a>SymmetricSecurityBindingElement를 사용하여 사용자 지정 바인딩을 만들려면  
  
1. 이름이 <xref:System.ServiceModel.Channels.BindingElementCollection>인 `outputBec` 클래스의 인스턴스를 만듭니다.  
  
2. `M:System.ServiceModel.Channels.SecurityBindingElement.CreateSspiNegotiationBindingElement(true)` 클래스의 인스턴스를 반환하는 정적 메서드 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>를 호출합니다.  
  
3. <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 클래스의 `outputBec`에서 `Add` 메서드를 호출하여 <xref:System.Collections.ObjectModel.Collection%601>를 컬렉션(<xref:System.ServiceModel.Channels.BindingElement>)에 추가합니다.  
  
4. <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> 클래스의 인스턴스를 만들고 이를 컬렉션(`outputBec`)에 추가합니다. 이를 통해 바인딩에서 사용하는 인코딩이 지정됩니다.  
  
5. <xref:System.ServiceModel.Channels.HttpTransportBindingElement>를 만들고 이를 컬렉션(`outputBec`)에 추가합니다. 이를 통해 바인딩이 HTTP 전송을 사용하도록 지정됩니다.  
  
6. <xref:System.ServiceModel.Channels.CustomBinding> 클래스의 인스턴스를 만들고 `outputBec` 컬렉션을 생성자에게 전달함으로써 새 사용자 지정 바인딩을 만듭니다.  
  
7. 결과 사용자 지정 바인딩은 표준 <xref:System.ServiceModel.WSHttpBinding>과 동일한 특징을 많이 공유합니다. 메시지 수준 보안 및 Windows 자격 증명을 지정하지만 보안 세션은 사용하지 않도록 설정하고, 서비스 자격 증명은 대역 외로 지정되어야 하며, 서명을 암호화하지 않습니다. 마지막 항목은 4단계에서처럼 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.MessageProtectionOrder%2A> 속성의 설정을 통해서만 제어할 수 있습니다. 다른 두 가지는 표준 바인딩의 설정을 사용하여 제어할 수 있습니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>설명  
 다음 예제에서는 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>를 사용하는 사용자 지정 바인딩을 만들기 위한 완전한 함수를 제공합니다.  
  
### <a name="code"></a>코드  
 [!code-csharp[c_CustomBinding#20](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#20)]
 [!code-vb[c_CustomBinding#20](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_custombinding/vb/source.vb#20)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Channels.SecurityBindingElement>
- <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>
- <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [바인딩 확장](../../../../docs/framework/wcf/extending/extending-bindings.md)
- [시스템 제공 바인딩](../../../../docs/framework/wcf/system-provided-bindings.md)
