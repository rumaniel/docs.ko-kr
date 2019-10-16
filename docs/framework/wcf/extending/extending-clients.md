---
title: 클라이언트 확장
ms.date: 03/30/2017
helpviewer_keywords:
- proxy extensions [WCF]
ms.assetid: 1328c61c-06e5-455f-9ebd-ceefb59d3867
ms.openlocfilehash: 91277e1a4d0a1d001d62d677dbd087bec5d875f0
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70797169"
---
# <a name="extending-clients"></a>클라이언트 확장
호출 응용 프로그램에서 서비스 모델 계층은 응용 프로그램 코드의 메서드 호출을 아웃바운드 메시지로 변환하고, 이를 기본 채널에 제공하며, 결과를 다시 응용 프로그램 코드의 반환 값 및 out 매개 변수로 변환한 후 결과를 다시 호출자에게 반환하는 역할을 합니다. 서비스 모델 확장은 클라이언트 또는 디스패처 기능, 사용자 지정 동작, 메시지 및 매개 변수 가로채기 그리고 다른 확장명 기능이 포함된 통신 동작 및 기능 또는 실행을 수정하거나 구현합니다.  
  
 이 항목에서는 wcf (Windows Communication Foundation) <xref:System.ServiceModel.Dispatcher.ClientRuntime> 클라이언트 <xref:System.ServiceModel.Dispatcher.ClientOperation> 응용 프로그램에서 및 클래스를 사용 하 여 wcf 클라이언트의 기본 실행 동작을 수정 하거나 메시지, 매개 변수 또는 반환 값을 가로채 거 나 수정 하는 방법에 대해 설명 합니다. 채널 계층에서 보내거나 검색 하기 이전 또는 이후입니다. 서비스 런타임을 확장 하는 방법에 대 한 자세한 내용은 [디스패처 확장](extending-dispatchers.md)을 참조 하세요. 사용자 지정 개체를 수정 하 고 클라이언트 런타임에 삽입 하는 동작에 대 한 자세한 내용은 [동작을 사용 하 여 런타임 구성 및 확장](configuring-and-extending-the-runtime-with-behaviors.md)을 참조 하세요.  
  
## <a name="clients"></a>클라이언트  
 클라이언트에서 WCF 클라이언트 개체 또는 클라이언트 채널은 메서드 호출을 나가는 메시지 및 들어오는 메시지를 호출 하는 응용 프로그램에 반환 되는 작업 결과로 변환 합니다. 클라이언트 형식에 대 한 자세한 내용은 [WCF 클라이언트 아키텍처](../feature-details/client-architecture.md)를 참조 하세요.  
  
 WCF 클라이언트 형식에는이 끝점과 작업 수준 기능을 처리 하는 런타임 형식이 있습니다. 응용 프로그램에서 작업을 호출하면 <xref:System.ServiceModel.Dispatcher.ClientOperation>은 아웃바운드 개체를 메시지로 변환하고 인터셉터를 처리하며, 아웃바운드 호출이 대상 계약을 따르는지 확인한 후 아웃바운드 메시지를 <xref:System.ServiceModel.Dispatcher.ClientRuntime>에 전달합니다. 이 ClientRuntime 클래스는 아웃바운드 채널 및 인바운드 채널(이중 서비스의 경우)을 생성 및 관리하고, 헤더 수정과 같은 추가 아웃바운드 메시지 프로세스를 처리하며, 양방향으로 메시지 인터셉터를 처리할 뿐 아니라 인바운드 이중 호출을 적절한 클라이언트 측<xref:System.ServiceModel.Dispatcher.DispatchRuntime> 개체에 라우트하는 역할도 합니다. <xref:System.ServiceModel.Dispatcher.ClientOperation>과 <xref:System.ServiceModel.Dispatcher.ClientRuntime>은 모두 오류를 포함한 메시지가 클라이언트에 반환될 때 비슷한 서비스를 제공합니다.  
  
 이러한 두 런타임 클래스는 WCF 클라이언트 개체 및 채널의 처리를 사용자 지정 하기 위한 기본 확장입니다. <xref:System.ServiceModel.Dispatcher.ClientRuntime> 클래스를 사용하면 계약의 모든 메시지에 대해 클라이언트 실행을 가로채 확장할 수 있으며, <xref:System.ServiceModel.Dispatcher.ClientOperation> 클래스를 사용하면 지정된 작업의 모든 메시지에 대해 클라이언트 실행을 가로채 확장할 수 있습니다.  
  
 속성 수정이나 사용자 지정 삽입 작업은 계약, 끝점 및 작업 동작을 통해 수행됩니다. 이러한 유형의 동작을 사용 하 여 클라이언트 런타임 사용자 지정을 수행 하는 방법에 대 한 자세한 내용은 동작을 사용 하 여 [런타임 구성 및 확장](configuring-and-extending-the-runtime-with-behaviors.md)을 참조 하세요.  
  
## <a name="scenarios"></a>시나리오  
 클라이언트 시스템을 확장하는 데에는 다음과 같은 여러 가지 이유가 있습니다.  
  
- 사용자 지정 메시지 유효성 확인. 메시지가 특정 스키마에 유효하도록 지정하고자 할 수 있습니다. 이 작업은 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector> 인터페이스를 구현한 다음 <xref:System.ServiceModel.Dispatcher.DispatchRuntime.MessageInspectors%2A> 속성에 할당하여 수행할 수 있습니다. 예제는 [방법: 클라이언트](how-to-inspect-or-modify-messages-on-the-client.md) 에서 메시지 검사 또는 수정 및 [방법: 클라이언트](how-to-inspect-or-modify-messages-on-the-client.md)에서 메시지를 검사 하거나 수정 합니다.  
  
- 사용자 지정 메시지 로깅. 끝점을 통해 이동하는 응용 프로그램 메시지의 일부를 검사하고 기록하도록 지정하고자 할 수 있습니다. 이 작업도 메시지 인터셉터 인터페이스를 통해 수행할 수 있습니다.  
  
- 사용자 지정 메시지 변환. 응용 프로그램 코드를 수정하기 보다는 특정 변환을 런타임에 메시지에 적용하도록 지정하고자 할 수 있습니다(예: 버전 관리). 이 작업도 메시지 인터셉터 인터페이스를 통해 수행할 수 있습니다.  
  
- 사용자 지정 데이터 모델. 사용자는 기본적으로 WCF에서 지원 되는 데이터 또는 serialization 모델 (즉 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>,, 및 <xref:System.ServiceModel.Channels.Message?displayProperty=nameWithType> 개체)이 아닌 데이터 또는 serialization 모델을 사용할 수 있습니다. 이 작업은 메시지 포맷터 인터페이스를 구현하여 수행할 수 있습니다. 자세한 내용은 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter?displayProperty=nameWithType> 및 <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A?displayProperty=nameWithType> 속성을 참조하십시오.  
  
- 사용자 지정 매개 변수 유효성 검사. XML 형식이 아닌 다른 형식의 매개 변수가 유효하도록 지정하고자 할 수 있습니다. 이 작업은 매개 변수 검사자 인터페이스를 사용하여 수행할 수 있습니다. 예는 [방법: 매개 변수](how-to-inspect-or-modify-parameters.md) 또는 [클라이언트 유효성 검사](../samples/client-validation.md)를 검사 하거나 수정 합니다.  
  
### <a name="using-the-clientruntime-class"></a>ClientRuntime 클래스 사용  
 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 클래스는 메시지를 가로채서 클라이언트 동작을 확장하는 확장 개체를 추가할 수 있는 확장성 지점입니다. 가로채기 개체는 특정 계약의 모든 메시지를 처리하고, 특정 작업의 메시지만 처리하며, 사용자 지정 채널 초기화를 수행하고, 다른 사용자 지정 클라이언트 애플리케이션 동작을 구현할 수 있습니다.  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackDispatchRuntime%2A> 속성은 서비스 개시 콜백 클라이언트에 대한 디스패치 런타임 개체를 반환합니다.  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.OperationSelector%2A> 속성은 사용자 지정 작업 선택자 개체를 적용합니다.  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.ChannelInitializers%2A> 속성을 사용하면 클라이언트 채널을 검사하거나 수정할 수 있는 채널 이니셜라이저를 추가할 수 있습니다.  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.Operations%2A> 속성은 해당 작업의 메시지에 특정한 기능을 제공하는 사용자 지정 메시지 인터셉터를 추가할 수 있는 <xref:System.ServiceModel.Dispatcher.ClientOperation> 개체의 컬렉션을 가져옵니다.  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.ManualAddressing%2A> 속성을 사용하면 응용 프로그램에서 일부 자동 주소 헤더를 비활성화하고 주소를 직접 제어할 수 있습니다.  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.Via%2A> 속성은 중간 매개자와 기타 시나리오를 지원하도록 전송 수준에서 메시지 대상 값을 설정합니다.  
  
- 속성 <xref:System.ServiceModel.Dispatcher.ClientRuntime.MessageInspectors%2A> 은 WCF 클라이언트를 통해 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector> 이동 하는 모든 메시지에 대 한 사용자 지정 메시지 인터셉터를 추가할 수 있는 개체의 컬렉션을 가져옵니다.  
  
 또한 계약 정보를 검색하는 다음과 같은 몇 가지 속성이 있습니다.  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractName%2A>  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractNamespace%2A>  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractClientType%2A>  
  
 WCF 클라이언트가 이중 WCF 클라이언트 인 경우 다음 속성도 콜백 WCF 클라이언트 정보를 검색 합니다.  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackClientType%2A>  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackDispatchRuntime%2A>  
  
 전체 wcf 클라이언트에서 wcf 클라이언트 실행을 확장 하려면 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 클래스에서 사용할 수 있는 속성을 검토 하 여 속성을 수정 하거나 인터페이스를 구현 하 고이를 속성에 추가 하 여 검색할 기능을 만듭니다. 빌드하려는 특정 확장을 선택했으면, 호출 시 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 클래스에 대한 액세스를 제공하는 클라이언트 동작을 구현하여 적합한<xref:System.ServiceModel.Dispatcher.ClientRuntime> 속성에 확장을 삽입합니다.  
  
 작업 동작(<xref:System.ServiceModel.Description.IOperationBehavior>를 구현하는 개체), 계약 동작(<xref:System.ServiceModel.Description.IContractBehavior>를 구현하는 개체) 또는 끝점 동작(<xref:System.ServiceModel.Description.IEndpointBehavior>를 구현하는 개체)을 사용하여 사용자 지정 확장 개체를 컬렉션에 삽입할 수 있습니다. 설치 동작 개체는 사용자 지정 특성을 구현하여 프로그래밍의 선언적 방식으로 또는 사용자 지정 <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> 개체를 구현하여 적합한 동작 컬렉션에 추가되기 때문에, 응용 프로그램 구성 파일을 통해 동작 삽입이 가능합니다. 자세한 내용은 [동작을 사용 하 여 런타임 구성 및 확장](configuring-and-extending-the-runtime-with-behaviors.md)을 참조 하세요.  
  
 WCF 클라이언트에서 가로채기를 [보여 주는 예제는 방법: 클라이언트](how-to-inspect-or-modify-messages-on-the-client.md)에서 메시지를 검사 하거나 수정 합니다.  
  
### <a name="using-the-clientoperation-class"></a>ClientOperation 클래스 사용  
 <xref:System.ServiceModel.Dispatcher.ClientOperation> 클래스는 하나의 서비스 작업으로 범위가 제한된 사용자 지정 확장에 대한 클라이언트 런타임 수정 및 삽입 지점의 위치입니다. 계약의 모든 메시지에 대한 클라이언트 런타임 동작을 수정하려면 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 클래스를 사용합니다.  
  
 특정 서비스 작업을 나타내는 <xref:System.ServiceModel.Dispatcher.ClientRuntime.Operations%2A> 개체를 찾으려면 <xref:System.ServiceModel.Dispatcher.ClientOperation> 속성을 사용합니다. 다음 속성을 사용 하 여 WCF 클라이언트 시스템에 사용자 지정 개체를 삽입할 수 있습니다.  
  
- 작업에 대한 사용자 지정 <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A> 구현을 삽입하거나 현재 포맷터를 수정하려면 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> 속성을 사용합니다.  
  
- 사용자 지정 <xref:System.ServiceModel.Dispatcher.ClientOperation.ParameterInspectors%2A> 구현을 삽입하거나 현재 구현을 수정하려면 <xref:System.ServiceModel.Dispatcher.IParameterInspector> 속성을 사용합니다.  
  
 다음 속성을 사용하면 포맷터 및 사용자 지정 매개 변수 검사자와 상호 작용하여 시스템을 수정할 수 있습니다.  
  
- 아웃바운드 메시지에 대한 serialization을 제어하려면 <xref:System.ServiceModel.Dispatcher.ClientOperation.SerializeRequest%2A> 속성을 사용합니다.  
  
- 인바운드 메시지에 대한 deserialization을 제어하려면 <xref:System.ServiceModel.Dispatcher.ClientOperation.DeserializeReply%2A> 속성을 사용합니다.  
  
- 요청 메시지에 대한 WS-Addressing 동작을 제어하려면 <xref:System.ServiceModel.Dispatcher.ClientOperation.Action%2A> 속성을 사용합니다.  
  
- 비동기 작업과 연결 <xref:System.ServiceModel.Dispatcher.ClientOperation.EndMethod%2A> 된 WCF 클라이언트 메서드를 지정 하려면 및를사용합니다.<xref:System.ServiceModel.Dispatcher.ClientOperation.BeginMethod%2A>  
  
- SOAP 오류에 세부 유형으로 표시될 수 있는 형식이 포함된 컬렉션을 가져오려면 <xref:System.ServiceModel.Dispatcher.ClientOperation.FaultContractInfos%2A> 속성을 사용합니다.  
  
- 작업이 호출될 때 세션이 초기화되는지 또는 삭제되는지 여부를 각각 제어하려면 <xref:System.ServiceModel.Dispatcher.ClientOperation.IsInitiating%2A> 및 <xref:System.ServiceModel.Dispatcher.ClientOperation.IsTerminating%2A> 속성을 사용합니다.  
  
- 작업이 단방향 작업인지 제어하려면 <xref:System.ServiceModel.Dispatcher.ClientOperation.IsOneWay%2A> 속성을 사용합니다.  
  
- 포함하는 <xref:System.ServiceModel.Dispatcher.ClientOperation.Parent%2A> 개체를 가져오려면 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 속성을 사용합니다.  
  
- 작업 이름을 가져오려면 <xref:System.ServiceModel.Dispatcher.ClientOperation.Name%2A> 속성을 사용합니다.  
  
- 작업에 매핑되는 메서드를 제어하려면 <xref:System.ServiceModel.Dispatcher.ClientOperation.SyncMethod%2A> 속성을 사용합니다.  
  
 하나의 서비스 작업에서 WCF 클라이언트 실행을 확장 하려면 <xref:System.ServiceModel.Dispatcher.ClientOperation> 클래스에서 사용할 수 있는 속성을 검토 하 여 속성을 수정 하거나 인터페이스를 구현 하 고이를 속성에 추가 하 여 검색할 기능을 만듭니다. 빌드하려는 특정 확장을 선택했으면, 호출 시 <xref:System.ServiceModel.Dispatcher.ClientOperation> 클래스에 대한 액세스를 제공하는 클라이언트 동작을 구현하여 적합한<xref:System.ServiceModel.Dispatcher.ClientOperation> 속성에 확장을 삽입합니다. 그러면 해당 동작에서 <xref:System.ServiceModel.Dispatcher.ClientRuntime> 속성을 사용자의 요구 사항에 맞게 수정할 수 있습니다.  
  
 일반적으로 작업 동작(<xref:System.ServiceModel.Description.IOperationBehavior> 인터페이스를 구현하는 개체) 구현으로도 충분하지만, 특정 작업에 대한 <xref:System.ServiceModel.Description.OperationDescription>을 찾아 여기에 동작을 연결하여 끝점 동작과 계약 동작을 사용하여 같은 결과를 얻을 수 있습니다. 자세한 내용은 [동작을 사용 하 여 런타임 구성 및 확장](configuring-and-extending-the-runtime-with-behaviors.md)을 참조 하세요.  
  
 구성에서 사용자 지정 동작을 사용하려면 사용자 지정 동작 구성 섹션 처리기를 사용하여 동작을 설치합니다. 사용자 지정 특성을 만들어 동작을 설치할 수도 있습니다.  
  
 WCF 클라이언트에서 가로채기를 [보여 주는 예제는 방법: 매개 변수](how-to-inspect-or-modify-parameters.md)를 검사 하거나 수정 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Dispatcher.ClientRuntime>
- <xref:System.ServiceModel.Dispatcher.ClientOperation>
- [방법: 클라이언트에서 메시지 검사 또는 수정](how-to-inspect-or-modify-messages-on-the-client.md)
- [방법: 매개 변수 검사 또는 수정](how-to-inspect-or-modify-parameters.md)
