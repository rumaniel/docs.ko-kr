---
title: 메시징 활동-WCF
ms.date: 03/30/2017
ms.assetid: 8498f215-1823-4aba-a6e1-391407f8c273
ms.openlocfilehash: 7670a6694e15f0a9e25152102d6237ef1ed60941
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61771438"
---
# <a name="messaging-activities"></a>메시징 활동

메시징 작업을 사용하면 워크플로를 통해 WCF 메시지를 보내고 받을 수 있습니다. 워크플로에 메시징 작업을 추가하면 훨씬 더 복잡한 MEP(메시지 교환 패턴)를 모델링할 수 있습니다.

## <a name="message-exchange-patterns"></a>메시지 교환 패턴

다음과 같은 세 가지 기본 메시지 교환 패턴이 있습니다.

- **데이터 그램** -데이터 그램 MEP를 사용 하는 경우 클라이언트 메시지를 서비스에 보내지만 서비스가 응답 하지 않습니다. 이를 "실행 후 제거"라고도 합니다. 실행 후 제거 교환은 성공적인 전달에 대한 out-of-band 확인이 필요한 교환입니다. 메시지는 전송 중에 손실되어 서비스에 전달되지 않을 수 있습니다. 즉, 클라이언트가 메시지를 성공적으로 보내도 서비스가 메시지를 수신한다고 보장할 수는 있습니다. 데이터그램을 기반으로 사용자 고유의 MEP를 빌드할 수 있으므로 데이터그램은 메시징 작업의 기본 구성 요소입니다.

- **요청-응답** -보내면 클라이언트 요청-응답 MEP를 사용 하 여 서비스에 서비스 메시지 필요한 처리를 않으며 클라이언트에 다시 응답 한 다음 보냅니다. 이 패턴은 요청-응답 쌍으로 구성됩니다. RPC(원격 프로시저 호출) 및 브라우저 GET 요청 등이 요청-응답 호출에 해당합니다. 이 패턴을 반이중이라고도 합니다.

- **이중** -이중 MEP 클라이언트 및 서비스를 사용 하 여 메시지를 보낼 수 서로 순서에 관계 없이 합니다. 이중 MEP는 말로 전달되는 각 단어가 메시지에 해당하는 전화 통화와 같습니다.

메시징 작업을 사용하면 이러한 기본 MEP뿐 아니라 훨씬 더 복잡한 MEP도 구현할 수 있습니다.

## <a name="messaging-activities"></a>메시징 활동

[!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]에서는 다음과 같은 메시징 작업을 정의합니다.

- <xref:System.ServiceModel.Activities.Send>- <xref:System.ServiceModel.Activities.Send> 활동을 사용하여 메시지를 보냅니다.

- <xref:System.ServiceModel.Activities.SendReply> - <xref:System.ServiceModel.Activities.SendReply> 활동을 사용하여 수신된 메시지에 대한 응답을 보냅니다. 이 작업은 요청/회신 MEP를 구현할 때 워크플로 서비스에서 사용합니다.

- <xref:System.ServiceModel.Activities.Receive>- <xref:System.ServiceModel.Activities.Receive> 활동을 사용하여 메시지를 받습니다.

- <xref:System.ServiceModel.Activities.ReceiveReply>- <xref:System.ServiceModel.Activities.ReceiveReply> 활동을 사용하여 회신 메시지를 받습니다. 이 작업은 요청/회신 MEP를 구현할 때 워크플로 서비스 클라이언트에서 사용합니다.

## <a name="messaging-activities-and-message-exchange-patterns"></a>메시징 활동 및 메시지 교환 패턴

데이터그램 MEP는 메시지를 보내는 클라이언트와 메시지를 받는 서비스로 구성됩니다. 클라이언트가 워크플로이면 <xref:System.ServiceModel.Activities.Send> 작업을 사용하여 메시지를 보냅니다. 워크플로에서 이 메시지를 받으려면 <xref:System.ServiceModel.Activities.Receive> 작업을 사용합니다. <xref:System.ServiceModel.Activities.Send> 및 <xref:System.ServiceModel.Activities.Receive> 작업에는 `Content`라는 속성이 있습니다. 이 속성에는 보내거나 받는 데이터가 포함됩니다. 요청-응답 MEP를 구현하는 경우 클라이언트와 서비스 둘 다 활동 쌍을 사용합니다. 클라이언트는 <xref:System.ServiceModel.Activities.Send> 활동을 사용하여 메시지를 보내고 <xref:System.ServiceModel.Activities.ReceiveReply> 활동을 사용하여 서비스의 응답을 받습니다. 이러한 두 활동은 <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A> 속성을 통해 서로 연결됩니다. 이 속성은 원본 메시지를 보낸 <xref:System.ServiceModel.Activities.Send> 활동으로 설정됩니다. 서비스도 마찬가지로 연결된 활동 쌍인 <xref:System.ServiceModel.Activities.Receive>와 <xref:System.ServiceModel.Activities.SendReply>를 사용합니다. 이러한 두 활동은 <xref:System.ServiceModel.Activities.SendReply.Request%2A> 속성을 통해 연결됩니다. 이 속성은 원본 메시지를 받은 <xref:System.ServiceModel.Activities.Receive> 활동으로 설정됩니다. <xref:System.ServiceModel.Activities.ReceiveReply> 및 <xref:System.ServiceModel.Activities.SendReply>와 마찬가지로 <xref:System.ServiceModel.Activities.Send> 및 <xref:System.ServiceModel.Activities.Receive> 활동을 사용하면 <xref:System.ServiceModel.Channels.Message> 인스턴스나 메시지 계약 형식을 보낼 수 있습니다.

워크플로의 장기 실행 특성 때문에 이중 패턴의 통신도 장기 실행 대화를 지원해야 합니다. 장기 실행 대화를 지원하려면 대화를 시작하는 클라이언트가 나중에 데이터가 사용 가능하게 될 때 해당 대화를 다시 호출할 수 있는 기회를 서비스에 제공해야 합니다. 예를 들어 구매 주문 요청이 관리자의 승인을 얻기 위해 전송되었지만 하루, 일주일, 심지어 일 년 동안 처리되지 않을 수 있습니다. 따라서 구매 주문 승인을 관리하는 워크플로는 승인을 얻은 후 다시 시작되어야 합니다. 이 패턴의 이중 통신은 상관 관계를 사용하는 워크플로에서 지원됩니다. 이중 패턴을 구현하려면 <xref:System.ServiceModel.Activities.Send> 및 <xref:System.ServiceModel.Activities.Receive> 활동을 사용합니다. 에 <xref:System.ServiceModel.Activities.Receive> 활동을 사용 하 여 상관 관계 초기화 <xref:System.ServiceModel.Activities.CorrelationHandle>합니다. <xref:System.ServiceModel.Activities.Send> 작업에서는 이 상관 관계의 핸들을 <xref:System.ServiceModel.Activities.Send.CorrelatesWith%2A> 속성 값으로 설정합니다. 자세한 내용은 [영 속 이중](durable-duplex-correlation.md)합니다.

> [!NOTE]
> 워크플로 구현 되는 이중 콜백 상관 관계 ("영 속 이중")를 사용 하 여 장기 실행 대화를 위한 것입니다. 대화가 단기 실행(채널의 수명)이고 콜백 계약이 있는 WCF 이중과 다릅니다.

## <a name="message-formatting-and-messaging-activities"></a>메시지 서식 지정 및 메시징 활동

<xref:System.ServiceModel.Activities.Receive> 및 <xref:System.ServiceModel.Activities.ReceiveReply> 작업에는 `Content`라는 속성이 있습니다. 이 속성은 <xref:System.ServiceModel.Activities.ReceiveContent> 형식이며 <xref:System.ServiceModel.Activities.Receive> 또는 <xref:System.ServiceModel.Activities.ReceiveReply> 작업이 받는 데이터를 나타냅니다. .NET Framework에서는 <xref:System.ServiceModel.Activities.ReceiveMessageContent>에서 파생되는 <xref:System.ServiceModel.Activities.ReceiveParametersContent> 및 <xref:System.ServiceModel.Activities.ReceiveContent>라는 두 개의 관련 클래스를 정의합니다. <xref:System.ServiceModel.Activities.Receive> 또는 <xref:System.ServiceModel.Activities.ReceiveReply> 작업의 `Content` 속성을 이러한 형식 중 하나의 인스턴스로 설정하면 데이터를 워크플로 서비스로 받을 수 있습니다. 사용할 형식은 작업이 받는 데이터의 형식에 따라 다릅니다. 작업이 `Message` 개체나 메시지 계약 형식을 받으면 <xref:System.ServiceModel.Activities.ReceiveMessageContent>를 사용하고, 작업이 데이터 계약 집합 또는 serialize 가능한 XML 형식을 수신하면 <xref:System.ServiceModel.Activities.ReceiveParametersContent>를 사용합니다. <xref:System.ServiceModel.Activities.ReceiveParametersContent>를 사용하면 여러 매개 변수를 보낼 수 있는 반면 <xref:System.ServiceModel.Activities.ReceiveMessageContent>를 사용하면 하나의 개체, 즉 메시지(또는 메시지 계약 형식)만 보낼 수 있습니다.

> [!NOTE]
> <xref:System.ServiceModel.Activities.ReceiveMessageContent>는 serialize할 수 있는 하나의 데이터 계약이나 XML 형식에 대해서도 사용할 수 있습니다. 하나의 매개 변수와 함께 <xref:System.ServiceModel.Activities.ReceiveParametersContent>를 사용하는 것과 <xref:System.ServiceModel.Activities.ReceiveMessageContent>에 직접 전달된 개체를 사용하는 것의 차이점은 통신 형식에 있습니다. 매개 변수의 내용은 작업 이름에 해당하는 XML 요소로 래핑되고 serialize된 개체는 매개 변수 이름을 사용하는 XML 요소로 래핑됩니다(예: `<Echo><msg>Hello, World</msg></Echo>`). 메시지 내용은 작업 이름으로 래핑되지 않습니다. 대신 serialize된 개체가 XML 정규화된 형식 이름을 사용하여 XML 요소 내에 배치됩니다(예: `<string>Hello, World</string>`).

<xref:System.ServiceModel.Activities.Send> 및 <xref:System.ServiceModel.Activities.SendReply> 작업에도 `Content`라는 속성이 있습니다. 이 속성은 <xref:System.ServiceModel.Activities.SendContent> 형식이며 <xref:System.ServiceModel.Activities.Send> 또는 <xref:System.ServiceModel.Activities.SendReply> 작업이 보내는 데이터를 나타냅니다. .NET Framework에서는 <xref:System.ServiceModel.Activities.SendMessageContent>에서 파생되는 <xref:System.ServiceModel.Activities.SendParametersContent> 및 <xref:System.ServiceModel.Activities.SendContent>라는 두 개의 관련 형식을 정의합니다. <xref:System.ServiceModel.Activities.Send> 또는 <xref:System.ServiceModel.Activities.SendReply> 작업의 `Content` 속성을 이러한 형식 중 하나의 인스턴스로 설정하면 워크플로 서비스에서 데이터를 보낼 수 있습니다. 사용할 형식은 작업이 보내는 데이터의 형식에 따라 다릅니다. 작업이 `Message` 개체나 메시지 계약 형식을 보내면 <xref:System.ServiceModel.Activities.SendMessageContent>를 사용하고, 작업이 데이터 계약 형식을 보내면 <xref:System.ServiceModel.Activities.SendParametersContent>를 사용합니다. <xref:System.ServiceModel.Activities.SendParametersContent>를 사용하면 여러 매개 변수를 보낼 수 있는 반면 <xref:System.ServiceModel.Activities.SendMessageContent>를 사용하면 하나의 개체, 즉 메시지(또는 메시지 계약 형식)만 보낼 수 있습니다.

메시징 작업을 사용하여 명령적으로 프로그래밍하는 경우 제네릭 <xref:System.Activities.InArgument%601> 및 <xref:System.Activities.OutArgument%601>를 사용하여 <xref:System.ServiceModel.Activities.Send>, <xref:System.ServiceModel.Activities.SendReply>, <xref:System.ServiceModel.Activities.Receive> 및 <xref:System.ServiceModel.Activities.ReceiveReply> 작업의 메시지 또는 매개 변수 속성에 할당되는 개체를 래핑합니다. 사용 하 여 <xref:System.Activities.InArgument%601> 에 대 한는 <xref:System.ServiceModel.Activities.Send> 하 고 <xref:System.ServiceModel.Activities.SendReply> 작업 및 <xref:System.Activities.OutArgument%601> 에 대 한 <xref:System.ServiceModel.Activities.Receive> 및 <xref:System.ServiceModel.Activities.ReceiveReply> 활동입니다. 데이터가 작업에 전달되는 중이므로 전송 작업에 `In` 인수가 사용됩니다. 다음 예제와 같이 데이터가 작업으로부터 전달되는 중이므로 수신 작업에 `Out` 인수가 사용됩니다.

```csharp
Receive reserveSeat = new Receive
{
    ...
    Content = new ReceiveParametersContent
    {
        Parameters =
        {
            { "ReservationInfo", new OutArgument<ReservationRequest>(reservationInfo) }
        }
    }
};
SendReply reserveSeat = new SendReply
{
    ...
    Request = reserveSeat,
    Content = new SendParametersContent
    {
        Parameters =
        {
            { "ReservationId", new InArgument<string>(reservationId) }
        }
    },
};
```

void를 반환하는 요청/응답 작업을 정의하는 워크플로 서비스를 구현할 때는 다음 예제와 같이 <xref:System.ServiceModel.Activities.SendReply> 작업을 인스턴스화하고 <xref:System.ServiceModel.Activities.SendReply.Content%2A> 속성을 콘텐츠 형식(<xref:System.ServiceModel.Activities.SendMessageContent> 또는 <xref:System.ServiceModel.Activities.SendParametersContent>) 중 하나의 빈 인스턴스로 설정합니다.

```csharp
Receive rcv = new Receive()
{
ServiceContractName = "IService",
OperationName = "NullReturningContract",
Content = new ReceiveParametersContent( new Dictionary<string, OutArgument>() { { "message", new OutArgument<string>() } } )
};
SendReply sr = new SendReply()
{
Request = rcv
   Content = new SendParametersContent();
};
```

## <a name="add-service-reference"></a>서비스 참조 추가

Visual Studio 2012 일반적인 캡슐화 하는 사용자 지정 메시징 작업을 생성 워크플로 응용 프로그램에서 워크플로 서비스를 호출할 때 <xref:System.ServiceModel.Activities.Send> 고 <xref:System.ServiceModel.Activities.ReceiveReply> 요청/회신 MEP에에서 사용 되는 작업입니다. 이 기능을 사용 하려면 Visual Studio에서 클라이언트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** > **서비스 참조**합니다. 주소 상자에 서비스의 기본 주소를 입력하고 이동을 클릭합니다. 사용 가능한 서비스에 표시 되는 **Services:** 상자입니다. 서비스 노드를 확장하여 지원되는 계약을 표시합니다. 호출 하려는 계약을 선택 하 고 사용 가능한 작업 목록에 표시 되는 **Operations** 상자입니다. 그런 다음 생성된 된 작업에 대 한 네임 스페이스를 지정 하 고 클릭 수 **확인**합니다. 그러면 프로젝트가 다시 빌드된 후 작업이 성공적으로 완료되었음을 알리고 사용자 지정 작업이 도구 상자에 표시된 대화 상자가 나타냅니다. 이 대화 상자에는 서비스 계약에 대해 정의된 작업마다 하나씩 작업이 있습니다. 프로젝트를 다시 빌드한 후에는 사용자 지정 작업을 워크플로에 끌어서 놓고 속성 창에서 필수 속성을 설정할 수 있습니다.

## <a name="messaging-activity-templates"></a>메시징 작업 템플릿

쉽게 클라이언트 및 서비스에서 요청/응답 MEP 설정 하려면 Visual Studio 2012 두 개의 메시징 작업 템플릿을 제공 합니다. `System.ServiceModel.Activities.Design.ReceiveAndSendReply`는 서비스에서 사용되고 `System.ServiceModel.Activities.Design.SendAndReceiveReply`는 클라이언트에서 사용됩니다. 두 경우 모두 템플릿이 워크플로에 적절한 메시징 작업을 추가합니다. 서비스에서는 `System.ServiceModel.Activities.Design.ReceiveAndSendReply`가 <xref:System.ServiceModel.Activities.Receive> 작업과 그 뒤에 <xref:System.ServiceModel.Activities.SendReply> 작업을 추가합니다. <xref:System.ServiceModel.Activities.SendReply.Request> 속성은 자동으로 <xref:System.ServiceModel.Activities.Receive> 작업으로 설정됩니다. 클라이언트에서는 `System.ServiceModel.Activities.Design.SendAndReceiveReply`가 <xref:System.ServiceModel.Activities.Send> 작업과 그 뒤에 <xref:System.ServiceModel.Activities.ReceiveReply> 작업을 추가합니다. <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A> 속성은 자동으로 <xref:System.ServiceModel.Activities.Send> 작업으로 설정됩니다. 이러한 템플릿을 사용하려면 워크플로에 원하는 템플릿을 끌어서 놓기만 하면 됩니다.

## <a name="messaging-activities-and-transactions"></a>메시징 활동 및 트랜잭션

워크플로 서비스가 호출되면 트랜잭션을 서비스 작업에 전달할 수 있습니다. 이 작업을 수행하려면 <xref:System.ServiceModel.Activities.Receive> 작업 안에 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 작업을 배치합니다. <xref:System.ServiceModel.Activities.TransactedReceiveScope> 작업은 `Receive` 작업과 본문을 포함합니다. 서비스에 전달된 트랜잭션은 <xref:System.ServiceModel.Activities.TransactedReceiveScope>의 본문이 실행되는 동안 앰비언트 상태로 유지됩니다. 본문이 실행을 마치면 트랜잭션이 완료됩니다. 워크플로 및 트랜잭션에 대 한 자세한 내용은 참조 하세요 [워크플로 트랜잭션을](../../../../docs/framework/windows-workflow-foundation/workflow-transactions.md)합니다.

## <a name="see-also"></a>참고자료

- [워크플로 서비스에서 오류를 수신 하는 방법](https://go.microsoft.com/fwlink/?LinkId=189151)
- [장기 실행 워크플로 서비스 만들기](creating-a-long-running-workflow-service.md)
