---
title: 사용자 지정 스트림 업그레이드
ms.date: 03/30/2017
ms.assetid: e3da85c8-57f3-4e32-a4cb-50123f30fea6
ms.openlocfilehash: bfb20a38d5d603a7f538235ee88045c92fc8cc85
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64587305"
---
# <a name="custom-stream-upgrades"></a>사용자 지정 스트림 업그레이드
TCP, 명명된 파이프 등의 스트림 지향 전송은 클라이언트와 서버 간의 연속 바이트 스트림에서 작동합니다. 이 스트림은 <xref:System.IO.Stream> 개체에 의해 나타날 수 있습니다. 스트림 업그레이드에서 클라이언트는 선택적 프로토콜 계층을 채널 스택에 추가하려고 하고 통신 채널의 반대쪽에서도 추가하도록 요청합니다. 스트림 업그레이드는 원래 <xref:System.IO.Stream> 개체를 업그레이드된 개체로 바꾸는 과정으로 이루어집니다.  
  
 예를 들어 전송 스트림 바로 위에 압축 스트림을 빌드할 수 있습니다. 이 경우 원래 전송 <xref:System.IO.Stream>은 원래 스트림을 중심으로 압축 <xref:System.IO.Stream>을 래핑하는 스트림으로 바뀝니다.  
  
 각각 이전 업그레이드를 래핑하여 여러 스트림 업그레이드를 적용할 수 있습니다.  
  
## <a name="how-stream-upgrades-work"></a>스트림 업그레이드의 작동 방식  
 스트림 업그레이드 프로세스에는 네 가지 구성 요소가 있습니다.  
  
1. 업그레이드 스트림 *초기자* 프로세스를 시작: 런타임 시에 채널 전송 계층을 업그레이드 하려면 해당 연결의 다른 end로 요청을 시작할 수 것입니다.  
  
2. 업그레이드 스트림 *수락자* 업그레이드: 런타임 시 다른 컴퓨터에서 업그레이드 요청을 수신 하 고 가능한 경우 업그레이드를 수락 합니다.  
  
3. 업그레이드 *공급자* 만듭니다 합니다 *초기자* 클라이언트에서와 *수락자* 서버의.  
  
4. 스트림 업그레이드 *바인딩 요소* 서비스와 클라이언트의 바인딩에 추가 되 고 런타임에 공급자를 만듭니다.  
  
 여러 업그레이드의 경우 개시자와 수락자는 상태 컴퓨터를 캡슐화하여 각 시작에 올바른 업그레이드 전환을 적용합니다.  
  
## <a name="how-to-implement-a-stream-upgrade"></a>스트림 업그레이드 구현 방법  
 Windows Communication Foundation (WCF) 4 개를 제공 합니다. `abstract` 구현할 수 있는 클래스:  
  
- <xref:System.ServiceModel.Channels.StreamUpgradeInitiator?displayProperty=nameWithType>  
  
- <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor?displayProperty=nameWithType>  
  
- <xref:System.ServiceModel.Channels.StreamUpgradeProvider?displayProperty=nameWithType>  
  
- <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement?displayProperty=nameWithType>  
  
 사용자 지정 스트림 업그레이드를 구현하려면 다음을 수행합니다. 이 절차에서는 클라이언트 및 서버 컴퓨터 둘 다에 최소 스트림 업그레이드 프로세스를 구현합니다.  
  
1. <xref:System.ServiceModel.Channels.StreamUpgradeInitiator>를 구현하는 클래스를 만듭니다.  
  
    1. <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.InitiateUpgrade%2A> 메서드를 재정의하여 업그레이드할 스트림을 사용하고 업그레이드된 스트림을 반환합니다. 이 메서드는 동기적으로 작동합니다. 비동기적으로 업그레이드를 시작하는 유사한 메서드가 있습니다.  
  
    2. <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A> 메서드를 재정의하여 추가 업그레이드를 확인합니다.  
  
2. <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor>를 구현하는 클래스를 만듭니다.  
  
    1. <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.AcceptUpgrade%2A> 메서드를 재정의하여 업그레이드할 스트림을 사용하고 업그레이드된 스트림을 반환합니다. 이 메서드는 동기적으로 작동합니다. 비동기적으로 업그레이드를 수락하는 유사한 메서드가 있습니다.  
  
    2. <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A> 메서드를 재정의하여 업그레이드 프로세스의 이 시점에서 이 업그레이드 수락자가 요청된 업그레이드를 지원하는지 여부를 확인합니다.  
  
3. <xref:System.ServiceModel.Channels.StreamUpgradeProvider>를 구현하는 클래스를 만듭니다. <xref:System.ServiceModel.Channels.StreamUpgradeProvider.CreateUpgradeAcceptor%2A> 및 <xref:System.ServiceModel.Channels.StreamUpgradeProvider.CreateUpgradeInitiator%2A> 메서드를 재정의하여 2단계와 1단계에서 정의된 수락자와 개시자의 인스턴스를 반환합니다.  
  
4. <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement>를 구현하는 클래스를 만듭니다.  
  
    1. 클라이언트의 <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement.BuildClientStreamUpgradeProvider%2A> 메서드와 서비스의 <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement.BuildServerStreamUpgradeProvider%2A> 메서드를 재정의합니다.  
  
    2. 클라이언트의 <xref:System.ServiceModel.Channels.BindingElement.BuildChannelFactory%2A> 메서드와 서비스의 <xref:System.ServiceModel.Channels.BindingElement.BuildChannelListener%2A> 메서드를 재정의하여 업그레이드 바인딩 요소를 <xref:System.ServiceModel.Channels.BindingContext.BindingParameters%2A>에 추가합니다.  
  
5. 서버 및 클라이언트 컴퓨터의 바인딩에 새 스트림 업그레이드 바인딩 요소를 추가합니다.  
  
## <a name="security-upgrades"></a>보안 업그레이드  
 보안 업그레이드 추가는 일반적인 스트림 업그레이드 프로세스의 특수화된 버전입니다.  
  
 WCF는 이미 스트림 보안 업그레이드에 대 한 두 개의 바인딩 요소를 제공 합니다. 전송 수준 보안의 구성은 구성하여 사용자 지정 바인딩에 추가할 수 있는 <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement> 및 <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>에 의해 캡슐화됩니다. 이러한 바인딩 요소는 클라이언트 및 서버 스트림 업그레이드 공급자를 빌드하는 <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement> 클래스를 확장합니다. 두 바인딩 요소에는 특수화된 보안 스트림 업그레이드 공급자 클래스를 만드는 메서드가 있습니다. 이 메서드는 `public`이 아니므로 두 경우 모두 바인딩 요소를 바인딩에 추가하기만 하면 됩니다.  
  
 위의 두 바인딩 요소가 만족하지 않는 보안 시나리오의 경우 위의 개시자, 수락자 및 공급자 기본 클래스에서 보안과 관련된 세 개의 `abstract` 클래스가 파생됩니다.  
  
1. <xref:System.ServiceModel.Channels.StreamSecurityUpgradeInitiator?displayProperty=nameWithType>  
  
2. <xref:System.ServiceModel.Channels.StreamSecurityUpgradeAcceptor?displayProperty=nameWithType>  
  
3. <xref:System.ServiceModel.Channels.StreamSecurityUpgradeProvider?displayProperty=nameWithType>  
  
 보안 스트림 업그레이드를 구현하는 프로세스는 이러한 세 클래스에서 파생된다는 차이를 제외하고 이전과 동일합니다. 이 클래스의 추가 속성을 재정의하여 런타임에 보안 정보를 제공합니다.  
  
## <a name="multiple-upgrades"></a>여러 업그레이드  
 추가 업그레이드를 만들려면 요청이 위의 프로세스를 반복합니다. <xref:System.ServiceModel.Channels.StreamUpgradeProvider> 및 바인딩 요소의 추가 확장을 만듭니다. 바인딩에 바인딩 요소를 추가합니다. 추가 바인딩 요소는 바인딩에 추가된 첫 번째 바인딩 요소에서 시작하여 순차적으로 처리됩니다. <xref:System.ServiceModel.Channels.BindingElement.BuildChannelFactory%2A> 및<xref:System.ServiceModel.Channels.BindingElement.BuildChannelListener%2A>에서 각 업그레이드 공급자는 기존의 업그레이드 바인딩 매개 변수에 해당 공급자의 계층을 설정하는 방법을 확인할 수 있습니다. 그런 다음 기존의 업그레이드 바인딩 매개 변수를 새 복합 업그레이드 바인딩 매개 변수로 바꿔야 합니다.  
  
 또는 한 업그레이드 공급자가 여러 업그레이드를 지원할 수 있습니다. 예를 들어 보안과 압축을 모두 지원하는 사용자 지정 스트림 업그레이드 공급자를 구현할 수 있습니다. 다음 단계를 수행합니다.  
  
1. 개시자와 수락자를 만드는 공급자 클래스를 쓰도록 <xref:System.ServiceModel.Channels.StreamSecurityUpgradeProvider>를 서브클래싱합니다.  
  
2. 압축 스트림과 보안 스트림의 콘텐츠 형식을 순서대로 반환하도록 <xref:System.ServiceModel.Channels.StreamSecurityUpgradeInitiator> 메서드를 재정의하여 <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A>를 서브클래싱합니다.  
  
3. <xref:System.ServiceModel.Channels.StreamSecurityUpgradeAcceptor> 메서드의 사용자 지정 콘텐츠 형식을 이해하는 <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A>를 서브클래싱합니다.  
  
4. <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A> 및 <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A>에 대한 각 호출 후에 스트림이 업그레이드됩니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Channels.StreamUpgradeInitiator>
- <xref:System.ServiceModel.Channels.StreamSecurityUpgradeInitiator>
- <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor>
- <xref:System.ServiceModel.Channels.StreamSecurityUpgradeAcceptor>
- <xref:System.ServiceModel.Channels.StreamUpgradeProvider>
- <xref:System.ServiceModel.Channels.StreamSecurityUpgradeProvider>
- <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement>
- <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>
- <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>
