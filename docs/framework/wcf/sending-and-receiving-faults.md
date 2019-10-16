---
title: 오류 보내기 및 받기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- handling faults [WCF], sending
ms.assetid: 7be6fb96-ce2a-450b-aebe-f932c6a4bc5d
ms.openlocfilehash: 447928ec3e6c0eaab997f839ab1aab49c677ad44
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044463"
---
# <a name="sending-and-receiving-faults"></a>오류 보내기 및 받기

SOAP 오류는 오류 조건 정보를 서비스에서 클라이언트로 전달하고 이중 클라이언트의 경우에는 상호 운용 가능한 방식으로 클라이언트에서 서비스로 전달합니다. 일반적으로 서비스는 사용자 지정 오류 내용을 정의하고 이들을 반환할 수 있는 작업을 지정합니다. 자세한 내용은 [오류 정의 및 지정](../../../docs/framework/wcf/defining-and-specifying-faults.md)을 참조 하세요. 이 항목에서는 해당 오류 조건이 발생한 경우 서비스 또는 이중 클라이언트가 그러한 오류를 보낼 수 있는 방법과 클라이언트 또는 서비스 응용 프로그램이 이러한 오류를 처리하는 방법에 대해 설명합니다. WCF (Windows Communication Foundation) 응용 프로그램의 오류 처리에 대 한 개요는 [계약 및 서비스에서 오류 지정 및 처리](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)를 참조 하세요.

## <a name="sending-soap-faults"></a>SOAP 오류 보내기

선언된 SOAP 오류는 작업에 사용자 지정 SOAP 오류 유형을 지정하는 <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType>가 있는 오류입니다. 선언되지 않은 SOAP 오류는 작업 계약에 지정되지 않은 오류입니다.

### <a name="sending-declared-faults"></a>선언된 오류 보내기

선언된 SOAP 오류를 보내려면 SOAP 오류가 적합한 오류 조건을 검색하고 새 <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType>을 throw합니다. 여기서, 형식 매개 변수는 해당 작업의 <xref:System.ServiceModel.FaultContractAttribute>에 지정된 형식의 새 개체입니다. 다음 코드 예제에서는 <xref:System.ServiceModel.FaultContractAttribute>를 사용하여 `SampleMethod` 작업이 `GreetingFault`의 세부 유형이 있는 SOAP 오류를 반환할 수 있도록 지정하는 방법을 보여 줍니다.

[!code-csharp[FaultContractAttribute#4](../../../samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/services.cs#4)]
[!code-vb[FaultContractAttribute#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/services.vb#4)]

`GreetingFault` 오류 정보를 클라이언트에게 전달하려면 적합한 오류 조건을 catch하고 다음 코드 예제처럼 새 <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType> 개체가 인수인 `GreetingFault` 유형의 새 `GreetingFault`을 throw합니다. 클라이언트가 WCF 클라이언트 응용 프로그램 인 경우 형식이 형식의 <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType> `GreetingFault`인 관리 되는 예외입니다.

[!code-csharp[FaultContractAttribute#5](../../../samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/services.cs#5)]
[!code-vb[FaultContractAttribute#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/services.vb#5)]

### <a name="sending-undeclared-faults"></a>선언되지 않은 오류 보내기

선언 되지 않은 오류는 WCF 응용 프로그램의 문제를 신속 하 게 진단 하 고 디버깅 하는 데 매우 유용할 수 있지만 디버깅 도구로 서의 유용성은 제한 되어 있습니다. 일반적으로 디버깅할 때 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> 속성을 사용하는 것이 좋습니다. 이 값을 true로 설정하면 클라이언트에 <xref:System.ServiceModel.FaultException%601> 형식의 <xref:System.ServiceModel.ExceptionDetail> 예외와 같은 오류가 발생합니다.

> [!IMPORTANT]
> 관리 되는 예외는 내부 애플리케이션 정보를 노출할 수, 있으므로 설정 <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> 나 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> 에 `true` WCF 클라이언트에서는 개인적으로 포함 하 여 내부 서비스 작업 예외에 대 한 정보를 허용 하려면 식별할 수 있는 정보나 기타 중요 한 정보입니다.
>
> 그러므로 임시로 서비스 애플리케이션을 디버깅하려는 경우 권장되는 유일한 방법은 <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> 또는 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType>를 `true`로 설정하는 것입니다. 또한 이 방법으로 처리되지 않은 관리되는 예외를 반환하는 메서드의 WSDL에는 <xref:System.ServiceModel.FaultException%601> 형식의 <xref:System.ServiceModel.ExceptionDetail>에 대한 계약이 포함되지 않습니다. 클라이언트는 알 수 없는 SOAP 오류의 가능성을 예상 해야 합니다 (WCF 클라이언트에 반환 <xref:System.ServiceModel.FaultException?displayProperty=nameWithType> 개체) 디버깅 정보를 제대로 가져올 수 있습니다.

선언되지 않은 SOAP 오류를 보내려면 <xref:System.ServiceModel.FaultException?displayProperty=nameWithType> 개체(즉, 제네릭 형식 <xref:System.ServiceModel.FaultException%601>이 아님)를 throw하고 문자열을 생성자에게 전달합니다. 이는 메서드를 <xref:System.ServiceModel.FaultException?displayProperty=nameWithType> <xref:System.ServiceModel.FaultException%601.ToString%2A?displayProperty=nameWithType> 호출 하 여 문자열을 사용할 수 있는 throw 된 예외로 WCF 클라이언트 응용 프로그램에 노출 됩니다.

> [!NOTE]
> 문자열 형식의 SOAP 오류를 선언한 다음 서비스에서 형식 매개 변수가 <xref:System.ServiceModel.FaultException%601>인 <xref:System.String?displayProperty=nameWithType>로 throw하면 문자열 값이 <xref:System.ServiceModel.FaultException%601.Detail%2A?displayProperty=nameWithType> 속성에 지정되며 <xref:System.ServiceModel.FaultException%601.ToString%2A?displayProperty=nameWithType>에서 사용할 수 없습니다.

## <a name="handling-faults"></a>오류 처리

WCF 클라이언트에서 클라이언트 응용 프로그램에 관심이 있는 통신 중에 발생 하는 SOAP 오류는 관리 되는 예외로 발생 합니다. 모든 프로그램을 실행 하는 동안 발생할 수 있는 많은 예외가 있지만 WCF 클라이언트 프로그래밍 모델을 사용 하는 응용 프로그램은 통신의 결과로 다음과 같은 두 형식의 예외를 처리할 수 있습니다.

- <xref:System.TimeoutException>

- <xref:System.ServiceModel.CommunicationException>

작업이 지정된 제한 시간을 초과하면 <xref:System.TimeoutException> 개체가 throw됩니다.

서비스나 클라이언트에 복구할 수 있는 통신 오류 조건이 있는 경우 <xref:System.ServiceModel.CommunicationException> 개체가 throw됩니다.

<xref:System.ServiceModel.CommunicationException> 클래스에는 두 가지 중요한 파생 형식인 <xref:System.ServiceModel.FaultException>과 제네릭 <xref:System.ServiceModel.FaultException%601> 형식이 있습니다.

수신자가 작업 계약에 예상되지 않거나 지정되지 않은 오류를 받으면 <xref:System.ServiceModel.FaultException> 예외가 throw됩니다. 일반적으로 이러한 예외는 응용 프로그램이 디버깅 중이고 서비스의 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> 속성이 `true`로 설정된 경우 발생합니다.

양방향 작업(즉, <xref:System.ServiceModel.FaultException%601>가 <xref:System.ServiceModel.OperationContractAttribute>로 설정된 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 특성이 있는 메서드)에 대한 응답으로 작업 계약에 지정된 오류를 받은 경우 클라이언트에서 `false` 예외가 throw됩니다.

> [!NOTE]
> <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> WCF 서비스 <xref:System.ServiceModel.ExceptionDetail>에 또는 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> 속성이로 설정 된 경우 클라이언트 `true` 는이를 형식의 선언 <xref:System.ServiceModel.FaultException%601> 되지 않은로 설정 합니다. 클라이언트는 이러한 특정 오류를 catch하거나 <xref:System.ServiceModel.FaultException>에 대한 catch 블록의 오류를 처리할 수 있습니다.

일반적으로 <xref:System.ServiceModel.FaultException%601>, <xref:System.TimeoutException> 및 <xref:System.ServiceModel.CommunicationException> 예외만 클라이언트와 서비스에 관련된 것입니다.

> [!NOTE]
> 물론 다른 예외도 발생합니다. 예기치 않은 예외가 <xref:System.OutOfMemoryException?displayProperty=nameWithType>과 같은 오류를 포함합니다. 일반적으로 응용 프로그램은 그러한 메서드를 catch하지 않아야 합니다.

### <a name="catch-fault-exceptions-in-the-correct-order"></a>올바른 순서로 오류 예외 catch

<xref:System.ServiceModel.FaultException%601>은 <xref:System.ServiceModel.FaultException>에서 파생되고 <xref:System.ServiceModel.FaultException>은 <xref:System.ServiceModel.CommunicationException>에서 파생되므로 적합한 순서로 이러한 예외를 catch하는 것이 중요합니다. 예를 들어 먼저 <xref:System.ServiceModel.CommunicationException>을 catch하는 try/catch 블록이 있는 경우 모든 지정된 SOAP 오류와 지정되지 않은 SOAP 오류가 여기서 처리됩니다. 사용자 지정 <xref:System.ServiceModel.FaultException%601> 예외를 처리할 이후 catch 블록은 호출되지 않습니다.

하나의 작업이 여러 개의 지정된 오류를 반환할 수 있습니다. 각 오류는 고유한 형식이며 별도로 처리해야 합니다.

### <a name="handle-exceptions-when-closing-the-channel"></a>채널을 닫을 때 예외 처리

위에서 설명한 대부분의 논의는 응용 프로그램 메시지, 즉 클라이언트 응용 프로그램이 WCF 클라이언트 개체에서 작업을 호출 하는 경우 클라이언트에서 명시적으로 보내는 메시지를 처리 하는 과정에서 전송 되는 오류를 처리 해야 합니다.

로컬 개체 외에도 개체를 삭제하면 재활용 프로세스 중에 발생하는 예외를 발생시키거나 마스킹할 수 있습니다. WCF 클라이언트 개체를 사용 하는 경우 비슷한 상황이 발생할 수 있습니다. 작업을 호출할 때 설정된 연결을 통해 메시지를 보내게 됩니다. 연결을 완전히 종료할 수 없거나 연결이 이미 종료된 경우, 모든 작업이 제대로 반환되어도 채널을 닫으면 예외가 throw될 수 있습니다.

일반적으로 클라이언트 개체 채널은 다음 중 한 가지 방법으로 닫힙니다.

- WCF 클라이언트 개체가 재활용 될 때.

- 클라이언트 응용 프로그램이 <xref:System.ServiceModel.ClientBase%601.Close%2A?displayProperty=nameWithType>를 호출하는 경우

- 클라이언트 응용 프로그램이 <xref:System.ServiceModel.ICommunicationObject.Close%2A?displayProperty=nameWithType>를 호출하는 경우

- 클라이언트 응용 프로그램이 세션에 대한 종료 작업을 호출하는 경우

모든 경우에 채널을 닫으면 응용 프로그램 수준에서 복잡한 기능을 지원할 메시지를 보낼 수 있는 기본 채널을 닫도록 채널에 지시합니다. 예를 들어 계약에 세션이 필요한 경우 세션이 설정될 때까지 바인딩 과정에서 서비스 채널과 메시지를 교환하여 세션을 설정합니다. 채널이 닫히면 기본 세션 채널은 세션이 종료되었음을 서비스에 알립니다. 이 때 채널이 이미 중단되었거나 닫혔거나 사용할 수 없는 경우(예: 네트워크 케이블이 연결되지 않은 경우) 클라이언트 채널은 세션이 종료되었으며 예외가 발생할 수 있음을 서비스 채널에 알릴 수 없습니다.

### <a name="abort-the-channel-if-necessary"></a>필요한 경우 채널 중단

채널을 닫아도 예외가 throw될 수 있으므로 올바른 순서로 오류 예외를 catch하는 것뿐만 아니라 catch 블록에서 호출에 사용된 채널을 중단하는 것도 중요합니다.

작업별 오류 정보가 제공되고 다른 작업에서 이 정보를 사용할 수 있으면 드물긴 하지만 채널을 중단하지 않아도 됩니다. 다른 모든 경우에는 채널을 중단하는 것이 좋습니다. 이러한 모든 사항을 보여 주는 샘플은 [예상 된 예외](../../../docs/framework/wcf/samples/expected-exceptions.md)를 참조 하세요.

다음 코드 예제에서는 선언된 오류와 선언되지 않은 오류를 비롯하여 기본 클라이언트 응용 프로그램에서 SOAP 오류 예외를 처리하는 방법을 보여 줍니다.

> [!NOTE]
> 이 샘플 코드에서는 `using` 구문을 사용하지 않습니다. 채널을 닫으면 예외가 throw 될 수 있으므로 응용 프로그램에서 WCF 클라이언트를 먼저 만든 다음 동일한 try 블록에서 WCF 클라이언트를 열고 사용 하 고 닫는 것이 좋습니다. 자세한 내용은 [Wcf 클라이언트 개요](../../../docs/framework/wcf/wcf-client-overview.md) 를 참조 하 고 [Close 및 Abort를 사용 하 여 wcf 클라이언트 리소스를 해제](../../../docs/framework/wcf/samples/use-close-abort-release-wcf-client-resources.md)합니다.

[!code-csharp[FaultContractAttribute#3](../../../samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/client.cs#3)]
[!code-vb[FaultContractAttribute#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/client.vb#3)]

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.FaultException>
- <xref:System.ServiceModel.FaultException%601>
- <xref:System.ServiceModel.CommunicationException?displayProperty=nameWithType>
- [예상되는 예외](../../../docs/framework/wcf/samples/expected-exceptions.md)
- [Close 및 Abort를 사용 하 여 WCF 클라이언트 리소스 해제](../../../docs/framework/wcf/samples/use-close-abort-release-wcf-client-resources.md)
