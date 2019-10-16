---
title: 이중 서비스
ms.date: 05/09/2018
dev_langs:
- csharp
- vb
ms.assetid: 396b875a-d203-4ebe-a3a1-6a330d962e95
ms.openlocfilehash: 4fd8b679dcd4ac9efce5fa915118736b15206068
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834775"
---
# <a name="duplex-services"></a>이중 서비스

이중 서비스 계약은 양쪽 엔드포인트에서 메시지를 다른 사용자에게 독립적으로 전송할 수 있는 메시지 교환 패턴입니다. 따라서 이중 서비스에서는 클라이언트 엔드포인트로 메시지를 보내 이벤트와 비슷한 동작을 제공할 수 있습니다. 이중 통신은 클라이언트가 서비스에 연결할 때 이루어지며, 서비스에서 클라이언트로 메시지를 다시 보낼 수 있는 채널을 제공합니다. 이중 서비스의 이벤트와 비슷한 동작은 세션 내에서만 작동합니다.

이중 계약을 만들려면 인터페이스 쌍을 만듭니다. 첫 번째는 클라이언트가 호출할 수 있는 작업을 설명하는 서비스 계약 인터페이스입니다. 해당 서비스 계약에서는 <xref:System.ServiceModel.ServiceContractAttribute.CallbackContract%2A?displayProperty=nameWithType> 속성에 *콜백 계약* 을 지정 해야 합니다. 콜백 계약은 서비스가 클라이언트 엔드포인트에서 호출할 수 있는 작업을 정의하는 인터페이스입니다. 시스템이 제공하는 이중 바인딩은 세션을 사용하지만 이중 계약에서는 세션이 필요 없습니다.

다음은 이중 계약의 예제입니다.

[!code-csharp[c_DuplexServices#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/service.cs#0)]
[!code-vb[c_DuplexServices#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/service.vb#0)]

`CalculatorService` 클래스는 기본 `ICalculatorDuplex` 인터페이스를 구현합니다. 서비스는 <xref:System.ServiceModel.InstanceContextMode.PerSession> 인스턴스 모드를 사용하여 각 세션의 결과를 유지합니다. `Callback`이라는 private 속성이 클라이언트에 대한 콜백 채널에 액세스합니다. 서비스는 다음 샘플 코드에 표시된 것처럼 콜백 인터페이스를 통해 클라이언트에 다시 전송하는 메시지의 콜백을 사용합니다.

[!code-csharp[c_DuplexServices#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/service.cs#1)]
[!code-vb[c_DuplexServices#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/service.vb#1)]

클라이언트는 서비스에서 메시지를 수신하기 위해 이중 계약의 콜백 인터페이스를 구현하는 클래스를 제공해야 합니다. 다음 샘플 코드에서는 `CallbackHandler` 인터페이스를 구현하는 `ICalculatorDuplexCallback` 클래스를 보여 줍니다.

[!code-csharp[c_DuplexServices#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/client.cs#2)]
[!code-vb[c_DuplexServices#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/client.vb#2)]

이중 계약에 대해 생성 된 WCF 클라이언트는 생성 시 <xref:System.ServiceModel.InstanceContext> 클래스를 제공 해야 합니다. 이 <xref:System.ServiceModel.InstanceContext> 클래스는 콜백 인터페이스를 구현하는 개체의 사이트로 사용되고 서비스에서 다시 전송된 메시지를 처리합니다. <xref:System.ServiceModel.InstanceContext> 클래스는 `CallbackHandler` 클래스의 인스턴스를 사용하여 생성됩니다. 이 개체는 콜백 인터페이스를 통해 서비스에서 클라이언트로 전송된 메시지를 처리합니다.

[!code-csharp[c_DuplexServices#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/client.cs#3)]
[!code-vb[c_DuplexServices#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/client.vb#3)]

서비스의 구성은 세션 통신 및 이중 통신 모두를 지원하는 바인딩을 제공하도록 설정되어야 합니다. `wsDualHttpBinding` 요소는 세션 통신을 지원하며 각 방향에 대해 하나씩, 이중 HTTP 연결을 제공하여 이중 통신을 허용합니다.

클라이언트에서는 다음 샘플 구성과 같이 서버가 클라이언트에 연결하는 데 사용할 수 있는 주소를 구성해야 합니다.

> [!NOTE]
> 보안 대화를 사용하여 인증할 수 없는 이중이 아닌 클라이언트는 일반적으로 <xref:System.ServiceModel.Security.MessageSecurityException>을 throw합니다. 그러나 보안 대화를 사용하는 이중 클라이언트가 인증할 수 없는 경우 클라이언트는 대신 <xref:System.TimeoutException>을 수신합니다.

`WSHttpBinding` 요소를 사용하여 클라이언트/서비스를 만들고 클라이언트 콜백 엔드포인트가 없는 경우 다음 오류를 수신합니다.

```console
HTTP could not register URL
htp://+:80/Temporary_Listen_Addresses/<guid> because TCP port 80 is being used by another application.
```

다음 샘플 코드에서는 클라이언트 끝점 주소를 프로그래밍 방식으로 지정 하는 방법을 보여 줍니다.

```csharp
WSDualHttpBinding binding = new WSDualHttpBinding();
EndpointAddress endptadr = new EndpointAddress("http://localhost:12000/DuplexTestUsingCode/Server");
binding.ClientBaseAddress = new Uri("http://localhost:8000/DuplexTestUsingCode/Client/");
```

```vb
Dim binding As New WSDualHttpBinding()
Dim endptadr As New EndpointAddress("http://localhost:12000/DuplexTestUsingCode/Server")
binding.ClientBaseAddress = New Uri("http://localhost:8000/DuplexTestUsingCode/Client/")
```

다음 샘플 코드에서는 구성에서 클라이언트 엔드포인트 주소를 지정하는 방법을 보여 줍니다.

```xml
<client>
    <endpoint name ="ServerEndpoint"
          address="http://localhost:12000/DuplexTestUsingConfig/Server"
          bindingConfiguration="WSDualHttpBinding_IDuplexTest"
            binding="wsDualHttpBinding"
           contract="IDuplexTest" />
</client>
<bindings>
    <wsDualHttpBinding>
        <binding name="WSDualHttpBinding_IDuplexTest"
          clientBaseAddress="http://localhost:8000/myClient/" >
            <security mode="None"/>
         </binding>
    </wsDualHttpBinding>
</bindings>
```

> [!WARNING]
> 이중 모델에서는 서비스 또는 클라이언트가 해당 채널을 닫을 때 자동으로 감지 되지 않습니다. 따라서 클라이언트가 예기치 않게 종료 되는 경우 기본적으로 서비스에 알림이 표시 되지 않거나 서비스가 예기치 않게 종료 되는 경우 클라이언트에 게 알림이 표시 되지 않습니다. 연결이 끊어진 <xref:System.ServiceModel.CommunicationException> 서비스를 사용 하는 경우 예외가 발생 합니다. 클라이언트와 서비스는 선택하는 경우 서로에게 알리도록 자체 프로토콜을 구현할 수 있습니다. 오류 처리에 대 한 자세한 내용은 [WCF 오류 처리](../wcf-error-handling.md)를 참조 하세요.

## <a name="see-also"></a>참조

- [이중](../samples/duplex.md)
- [클라이언트 런타임 동작 지정](../specifying-client-run-time-behavior.md)
- [방법: 채널 팩터리를 만들어 채널을 만들고 관리 하는 데 사용](how-to-create-a-channel-factory-and-use-it-to-create-and-manage-channels.md)
