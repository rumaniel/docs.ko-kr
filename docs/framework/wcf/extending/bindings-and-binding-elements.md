---
title: 바인딩 및 바인딩 요소
ms.date: 03/30/2017
helpviewer_keywords:
- binding elements [WCF]
ms.assetid: 765ff77b-7682-4ea3-90eb-e4d751e37379
ms.openlocfilehash: d4d69495c1ae19b6799fdb9981f6b332cc2580d3
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795845"
---
# <a name="bindings-and-binding-elements"></a>바인딩 및 바인딩 요소
바인딩은 클라이언트 또는 서비스 끝점이 생성 될 때마다 서비스 런타임에 의해 평가 되는 *바인딩 요소*라는 특수 구성 요소의 컬렉션입니다. 한 바인딩 내에 있는 바인딩 요소의 형식과 순서는 엔드포인트 채널 스택에서 프로토콜 및 전송 채널의 선택 및 스택 순서를 결정합니다.  
  
 특히 시스템 제공 바인딩에는 캡슐화된 바인딩 요소의 가장 일반적으로 수정되는 속성을 반영하는 여러 개의 구성 속성도 있습니다.  
  
 바인딩에는 전송 바인딩 요소가 하나만 있어야 합니다. 각 전송 바인딩 요소는 기본 메시지 인코딩 바인딩 요소를 나타내며, 이러한 요소는 하나의 메시지 인코딩 바인딩 요소를 바인딩에 추가하여 재정의할 수 있습니다. 바인딩에는 전송 및 인코더 바인딩 요소 외에, 엔드포인트 간에 SOAP 메시지를 보내고 서비스하는 데 필요한 기능을 함께 구현하는 여러 개의 프로토콜 바인딩 요소가 포함될 수 있습니다. 자세한 내용은 [바인딩을 사용 하 여 서비스 및 클라이언트 구성](../using-bindings-to-configure-services-and-clients.md)을 참조 하세요.  
  
## <a name="extending-bindings-and-binding-elements"></a>바인딩 및 바인딩 요소 확장명  
 WCF (Windows Communication Foundation)에는 다양 한 시나리오를 다루는 시스템 제공 바인딩이 포함 되어 있습니다. 자세한 내용은 [시스템 제공 바인딩](../system-provided-bindings.md)을 참조 하세요. 그러나 WCF에 포함 되지 않은 바인딩을 만들고 사용 해야 하는 경우가 있을 수 있습니다. 다음 시나리오에서는 새 바인딩을 만들어야 합니다.  
  
- 새 전송, 인코딩 또는 프로토콜 바인딩 요소와 같은 새 바인딩 요소를 사용하려면 해당 바인딩 요소를 포함하는 새 바인딩을 만들어야 합니다. 예를 들어 UDP 전송용 사용자 지정 `UdpTransportBindingElement`를 추가한 경우 새 바인딩을 만들어 사용해야 합니다. 형식을 사용 하 여이 동작을 수행 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType> 하는 방법에 대 한 자세한 내용은 [사용자 지정 바인딩](custom-bindings.md)을 참조 하세요.  
  
- 시스템 제공 바인딩이 public 속성에 노출되지 않는 방식으로 기존 바인딩 요소를 구성합니다. 예를 들어 서명 및 암호화 작업이 수행되는 순서를 변경하려면 새 바인딩을 만들어야 합니다. 이 동작을 [수행 하는 방법에 대 한 자세한 내용은 방법: 시스템 제공 바인딩을](how-to-customize-a-system-provided-binding.md)사용자 지정 합니다.  
  
- 특정 구성 옵션만 노출하는 회사 표준 바인딩을 설정합니다. 예를 들어 보안을 비활성화할 수 없는 회사의 <xref:System.ServiceModel.WSHttpBinding> 변수를 만들려면 보안은 항상 설정된 상태에서 <xref:System.ServiceModel.WSHttpBinding>처럼 동작하는 새 바인딩을 만듭니다. 자세한 내용은 [사용자 정의 바인딩 만들기](creating-user-defined-bindings.md)를 참조 하세요.  
  
- 일부 메타데이터를 사용자 지정하지만 일반적으로 일부 사용자 지정 바인딩 요소를 반드시 구성하거나 사용하지 않습니다. 바인딩 및 바인딩 요소에 대 한 메타 데이터 지원을 제공 하는 방법에 대 한 자세한 내용은 [구성 및 메타 데이터 지원](configuration-and-metadata-support.md)을 참조 하세요.  

## <a name="channels-bindings-and-binding-elements"></a>채널, 바인딩 및 바인딩 요소  
 바인딩 및 바인딩 요소는 특성 및 동작을 포함하는 애플리케이션 프로그래밍 모델과 팩터리 및 수신기, 메시지 인코더, 전송 및 프로토콜 구현을 포함하는 채널 모델 사이를 연결합니다. 일반적으로, 바인딩 요소와 바인딩이 구현되면 애플리케이션 계층에서 채널을 사용할 수 있습니다.  
  
 채널 계층은 서비스 계층 간에 메시지를 핸드오프하고 받으며 엔드포인트 사이에서 해당 메시지를 전송합니다. 클라이언트에서 채널 계층은 네트워크 엔드포인트에 채널을 만드는 채널 팩터리 스택입니다. 서비스에서 채널 계층은 네트워크 엔드포인트에서 받은 채널을 수락하는 채널 수신기 스택입니다.  
  
 일반적으로 채널에는 프로토콜 채널과 전송 채널의 두 가지 유형이 있습니다. 전송 채널은 네트워크 엔드포인트 간에 실제로 메시지를 전송합니다. 전송 채널에는 기본 메시지 인코더가 있어야 하며 해당 채널은 메시지 인코더 바인딩 요소를 통해 제공되는 대체 메시지 인코더를 사용할 수 있어야 합니다. 메시지 인코더는 <xref:System.ServiceModel.Channels.Message?displayProperty=nameWithType>를 연결 표시로 또는 그 반대로 바꿉니다. 프로토콜 채널은 WS-Security 또는 WS-ReliableMessaging과 같은 SOAP 수준 프로토콜을 구현합니다.  
  
 전송 및 프로토콜 채널의 기본 요구 사항은 해당 채널이 필수 채널 인터페이스를 구현하는 것입니다. 작업 채널 계층을 만들려면 연결된 팩터리와 수신기 등이 있어야 합니다. WCF에서 채널 구현을 사용 하려면 각 채널에 대해에서 <xref:System.ServiceModel.Channels.BindingElement> 파생 되는 연결 된 바인딩 요소가 있어야 하며,에서 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>파생되는구성파일에포함할관련바인딩확장요소가있어야합니다.  
  
 앞에서도 언급했듯이 메시지 인코더, 프로토콜 및 전송 채널 구현을 위한 바인딩 요소를 쌓아 채널 스택을 구성할 수 있으며, 순서가 지정된 집합에 이들을 정렬하는 메커니즘이 바인딩이 됩니다. 바인딩 및 바인딩 요소는 애플리케이션 프로그래밍 모델을 채널 모델에 연결합니다. 코드에서 직접 채널 구현을 사용할 수 있지만 인코더, 전송 및 프로토콜이 바인딩 요소로 구현되지 않은 경우에는 해당 채널 구현을 서비스 계층 프로그래밍 모델에서 사용할 수 없습니다.  
  
 채널 및 해당 바인딩 요소를 개발 하는 방법에 대 한 자세한 내용은 [채널 계층 확장](extending-the-channel-layer.md)을 참조 하세요.
