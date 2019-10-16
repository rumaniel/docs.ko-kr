---
title: WCF 클라이언트 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- clients [WCF], architecture
ms.assetid: f60d9bc5-8ade-4471-8ecf-5a07a936c82d
ms.openlocfilehash: adaaca596650c5bff486bd0c295c4f840ae58051
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916878"
---
# <a name="wcf-client-overview"></a>WCF 클라이언트 개요
이 섹션에서는 클라이언트 응용 프로그램에서 수행 하는 작업, WCF (Windows Communication Foundation) 클라이언트를 구성 하 고 만들고 사용 하는 방법 및 클라이언트 응용 프로그램의 보안을 설정 하는 방법을 설명 합니다.  
  
## <a name="using-wcf-client-objects"></a>WCF 클라이언트 개체 사용  
 클라이언트 응용 프로그램은 WCF 클라이언트를 사용 하 여 다른 응용 프로그램과 통신 하는 관리 되는 응용 프로그램입니다. WCF 서비스에 대 한 클라이언트 응용 프로그램을 만들려면 다음 단계를 수행 해야 합니다.  
  
1. 서비스 엔드포인트에 대한 서비스 계약, 바인딩 및 주소 정보를 가져옵니다.  
  
2. 해당 정보를 사용 하 여 WCF 클라이언트를 만듭니다.  
  
3. 작업을 호출합니다.  
  
4. WCF 클라이언트 개체를 닫습니다.  
  
 다음 단원에서는 이러한 단계에 대해 설명하고 다음과 같은 문제를 간략하게 소개합니다.  
  
- 오류 처리  
  
- 클라이언트 구성 및 보안  
  
- 이중 서비스에 대한 콜백 개체 만들기  
  
- 비동기적으로 서비스 호출  
  
- 클라이언트 채널을 사용하여 서비스 호출  
  
## <a name="obtain-the-service-contract-bindings-and-addresses"></a>서비스 계약, 바인딩 및 주소 가져오기  
 WCF에서 서비스 및 클라이언트는 관리 되는 특성, 인터페이스 및 메서드를 사용 하 여 계약을 모델링 합니다. 클라이언트 응용 프로그램에서 서비스에 연결하려면 서비스 계약에 대한 형식 정보를 가져와야 합니다. 일반적으로이 작업은 서비스에서 메타 데이터를 다운로드 하는 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)를 사용 하 여이 작업을 수행 하 고, 선택한 언어로 관리 되는 소스 코드 파일로 변환 하 고, 클라이언트 응용 프로그램 구성 파일을 만듭니다. WCF 클라이언트 개체를 구성 하는 데 사용할 수 있습니다. 예를 들어를 호출 `MyCalculatorService`하는 WCF 클라이언트 개체를 만들고 해당 서비스에 대 한 메타 데이터가에 `http://computerName/MyCalculatorService/Service.svc?wsdl`게시 된 것을 알고 있는 경우 다음 코드 예제에서는 svcutil.exe를 사용 하 여 파일을 `ClientCode.vb` 가져오는 방법을 보여 줍니다. 관리 코드의 서비스 계약을 포함 합니다.  
  
```  
svcutil /language:vb /out:ClientCode.vb /config:app.config http://computerName/MyCalculatorService/Service.svc?wsdl  
```  
  
 이 계약 코드를 클라이언트 응용 프로그램으로 컴파일하거나 클라이언트 응용 프로그램에서 WCF 클라이언트 개체를 만드는 데 사용할 수 있는 다른 어셈블리로 컴파일할 수 있습니다. 구성 파일을 사용하여 클라이언트 개체가 서비스에 제대로 연결하도록 구성할 수 있습니다.  
  
 이 프로세스에 대 한 예제를 보려면 [방법: 클라이언트](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)를 만듭니다. 계약에 대 한 자세한 내용은 [계약](../../../docs/framework/wcf/feature-details/contracts.md)을 참조 하세요.  
  
## <a name="create-a-wcf-client-object"></a>WCF 클라이언트 개체 만들기  
 WCF 클라이언트는 클라이언트가 원격 서비스와 통신 하는 데 사용할 수 있는 형식의 WCF 서비스를 나타내는 로컬 개체입니다. WCF 클라이언트 형식은 대상 서비스 계약을 구현 하기 때문에 대상 서비스 계약을 만들어 구성할 경우 클라이언트 개체를 직접 사용 하 여 서비스 작업을 호출할 수 있습니다. Wcf 런타임에서는 메서드 호출을 메시지로 변환 하 고, 서비스에 보내고, 회신을 수신 하 고, 해당 값을 WCF 클라이언트 개체에 반환 값 또는 `out` 또는 `ref` 매개 변수로 반환 합니다.  
  
 WCF 클라이언트 채널 개체를 사용 하 여 서비스에 연결 하 고 서비스를 사용할 수도 있습니다. 자세한 내용은 [WCF 클라이언트 아키텍처](../../../docs/framework/wcf/feature-details/client-architecture.md)를 참조 하세요.  
  
#### <a name="creating-a-new-wcf-object"></a>새 WCF 개체 만들기  
 <xref:System.ServiceModel.ClientBase%601> 클래스 사용을 설명하기 위해 다음 서비스 계약이 생성되어 있는 것으로 가정합니다.  
  
> [!NOTE]
> Visual Studio를 사용 하 여 WCF 클라이언트를 만들면 프로젝트에 서비스 참조를 추가할 때 개체가 개체 브라우저에 자동으로 로드 됩니다.  
  
 [!code-csharp[C_GeneratedCodeFiles#12](../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/proxycode.cs#12)]  
  
 Visual Studio를 사용 하지 않는 경우 생성 된 계약 코드를 검사 하 여 및 서비스 계약 인터페이스 <xref:System.ServiceModel.ClientBase%601> `ISampleService`를 확장 하는 형식을 찾습니다. 이 경우 형식은 다음 코드와 비슷합니다.  
  
 [!code-csharp[C_GeneratedCodeFiles#14](../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/proxycode.cs#14)]  
  
 생성자 중 하나를 사용하여 이 클래스를 로컬 개체로 만든 다음 구성하여 `ISampleService` 형식 서비스에 연결하는 데 사용할 수 있습니다.  
  
 WCF 클라이언트 개체를 먼저 만든 다음이 개체를 사용 하 여 단일 try/catch 블록 내에서 닫는 것이 좋습니다. 문 ( `using` `Using` Visual Basic)은 특정 오류 모드에서 예외를 마스킹할 수 있으므로 사용 하면 안 됩니다. 자세한 내용은 다음 섹션을 참조 하 [고 Close 및 Abort를 사용 하 여 WCF 클라이언트 리소스를 해제](../../../docs/framework/wcf/samples/use-close-abort-release-wcf-client-resources.md)합니다.  
  
### <a name="contracts-bindings-and-addresses"></a>계약, 바인딩 및 주소  
 WCF 클라이언트 개체를 만들려면 먼저 client 개체를 구성 해야 합니다. 특히 사용할 서비스 *끝점이* 있어야 합니다. 엔드포인트는 서비스 계약, 바인딩 및 주소의 조합입니다. 끝점에 대 한 자세한 내용은 끝점을 [참조 하세요. 주소, 바인딩 및 계약](../../../docs/framework/wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)). 일반적으로이 정보는 svcutil.exe 도구에서 생성 하는 것과 같은 클라이언트 응용 프로그램 구성 파일의 [ \<끝점 >](../../../docs/framework/configure-apps/file-schema/wcf/endpoint-of-client.md) 요소에 있으며 클라이언트 개체를 만들 때 자동으로 로드 됩니다. WCF 클라이언트 형식에는이 정보를 프로그래밍 방식으로 지정할 수 있도록 하는 오버 로드도 있습니다.  
  
 예를 들어, 이전 예제에 사용된 `ISampleService`에 대해 생성된 구성 파일에는 다음과 같은 엔드포인트 정보가 포함되어 있습니다.  
  
 [!code-xml[C_GeneratedCodeFiles#19](../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/common/client.exe.config#19)]  
  
 이 구성 파일은 `<client>` 요소에서 대상 엔드포인트를 지정합니다. 여러 대상 끝점을 사용 하는 <xref:System.ServiceModel.ClientBase%601.%23ctor%2A?displayProperty=nameWithType> 방법에 대 한 자세한 내용은 <xref:System.ServiceModel.ChannelFactory%601.%23ctor%2A?displayProperty=nameWithType> 또는 생성자를 참조 하십시오.  
  
## <a name="calling-operations"></a>작업 호출  
 클라이언트 개체를 만들고 구성한 후에는 try/catch 블록을 만들고, 개체가 로컬인 것과 같은 방식으로 작업을 호출 하 고, WCF 클라이언트 개체를 닫습니다. 클라이언트 응용 프로그램에서 첫 번째 작업을 호출 하면 WCF는 기본 채널을 자동으로 열고 개체를 재활용할 때 기본 채널이 닫힙니다. 또는 다른 작업을 호출하기 이전 또는 이후에 채널을 명시적으로 열었다가 닫을 수 있습니다.  
  
 예를 들어, 다음과 같은 서비스 계약을 가정해 봅니다.  
  
```csharp  
namespace Microsoft.ServiceModel.Samples  
{  
    using System;  
    using System.ServiceModel;  
  
    [ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]  
    public interface ICalculator  
   {  
        [OperationContract]  
        double Add(double n1, double n2);  
        [OperationContract]  
        double Subtract(double n1, double n2);  
        [OperationContract]  
        double Multiply(double n1, double n2);  
        [OperationContract]  
        double Divide(double n1, double n2);  
    }  
}  
```  
  
```vb  
Namespace Microsoft.ServiceModel.Samples  
  
    Imports System  
    Imports System.ServiceModel  
  
    <ServiceContract(Namespace:= _  
    "http://Microsoft.ServiceModel.Samples")> _   
   Public Interface ICalculator  
        <OperationContract> _   
        Function Add(n1 As Double, n2 As Double) As Double  
        <OperationContract> _   
        Function Subtract(n1 As Double, n2 As Double) As Double  
        <OperationContract> _   
        Function Multiply(n1 As Double, n2 As Double) As Double  
        <OperationContract> _   
     Function Divide(n1 As Double, n2 As Double) As Double  
End Interface  
```  
  
 다음 코드 예제에서 보여 주는 것 처럼 WCF 클라이언트 개체를 만들고 해당 메서드를 호출 하 여 작업을 호출할 수 있습니다. WCF 클라이언트 개체의 열기, 호출 및 닫기는 단일 try/catch 블록 내에서 발생 합니다. 자세한 내용은 [Wcf 클라이언트를 사용 하 여 서비스 액세스](../../../docs/framework/wcf/feature-details/accessing-services-using-a-client.md) 및 [Close 및 Abort를 사용 하 여 wcf 클라이언트 리소스 릴리스를](../../../docs/framework/wcf/samples/use-close-abort-release-wcf-client-resources.md)참조 하세요.  
  
 [!code-csharp[C_GeneratedCodeFiles#20](../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/proxycode.cs#20)]  
  
## <a name="handling-errors"></a>오류 처리  
 기본 클라이언트 채널을 명시적으로 열거나 작업을 호출하여 자동으로 열 때, 클라이언트 또는 채널 개체를 사용하여 작업을 호출할 경우 또는 기본 클라이언트 채널을 닫을 때 클라이언트 응용 프로그램에서 예외가 발생할 수 있습니다. 적어도 응용 프로그램에서 가능한 <xref:System.TimeoutException?displayProperty=nameWithType> 및 <xref:System.ServiceModel.CommunicationException?displayProperty=nameWithType> 예외를 비롯하여 작업에서 반환되는 SOAP 오류로 인해 throw되는 <xref:System.ServiceModel.FaultException?displayProperty=nameWithType> 개체를 처리하도록 하는 것이 좋습니다. 작업 계약에 지정된 SOAP 오류는 형식 매개 변수가 SOAP 오류의 세부 유형인 <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType>으로, 클라이언트 응용 프로그램에서 발생됩니다. 클라이언트 응용 프로그램에서 오류 조건을 처리 하는 방법에 대 한 자세한 내용은 오류 [보내기 및 받기](../../../docs/framework/wcf/sending-and-receiving-faults.md)를 참조 하십시오. 전체 샘플은 클라이언트에서 오류를 처리 하는 방법을 보여 줍니다. [예상 되는 예외](../../../docs/framework/wcf/samples/expected-exceptions.md)를 참조 하세요.  
  
## <a name="configuring-and-securing-clients"></a>클라이언트 구성 및 보안  
 클라이언트를 구성하려면 클라이언트 생성자와 속성을 사용하여 클라이언트 또는 채널 개체에 대한 대상 엔드포인트 정보를 프로그래밍 방식으로 로드할 수도 있지만, 일반적으로 구성 파일에서 이 정보를 로드해야 합니다. 그러나 다양한 보안 시나리오에 대해 특정 클라이언트 동작을 활성화하는 추가 구성 단계를 수행해야 합니다.  
  
 예를 들어, 서비스 계약에 대한 보안 요구 사항이 서비스 계약 인터페이스에 선언되어 있고, Svcutil.exe에서 구성 파일을 만든 경우 해당 파일에는 일반적으로 서비스의 보안 요구 사항을 지원할 수 있는 바인딩이 포함되어 있습니다. 그러나, 클라이언트 자격 증명 구성처럼 추가 보안 구성이 필요한 경우도 있습니다. WCF 클라이언트의 보안 구성에 대 한 자세한 내용은 [클라이언트 보안](../../../docs/framework/wcf/securing-clients.md)을 참조 하세요.  
  
 또한 클라이언트 응용 프로그램에서 사용자 지정 런타임 동작과 같은 사용자 지정 수정을 사용할 수 있는 경우도 있습니다. 사용자 지정 클라이언트 동작을 구성 하는 방법에 대 한 자세한 내용은 [클라이언트 동작 구성](../../../docs/framework/wcf/configuring-client-behaviors.md)을 참조 하세요.  
  
## <a name="creating-callback-objects-for-duplex-services"></a>이중 서비스에 대한 콜백 개체 만들기  
 이중 서비스는 계약 요구 사항에 따라 서비스를 호출하도록 콜백 개체를 제공하기 위해 클라이언트 응용 프로그램에서 구현해야 하는 콜백 계약을 지정합니다. 콜백 개체는 정식 서비스가 아니지만(예를 들어, 콜백 개체를 사용하여 채널을 시작할 수 없음) 구현 및 구성을 위해 일종의 서비스로 간주될 수 있습니다.  
  
 이중 서비스의 클라이언트는 다음을 수행해야 합니다.  
  
- 콜백 계약 클래스 구현  
  
- 콜백 계약 구현 클래스의 인스턴스를 만들고이를 사용 하 여 WCF 클라이언트 <xref:System.ServiceModel.InstanceContext?displayProperty=nameWithType> 생성자에 전달 하는 개체를 만듭니다.  
  
- 작업 호출 및 작업 콜백 처리  
  
 이중 WCF 클라이언트 개체는 콜백 서비스의 구성을 비롯 하 여 콜백을 지 원하는 데 필요한 기능을 노출 하는 것을 제외 하 고 비 이중 WCF 클라이언트 개체와 동일 하 게 작동 합니다.  
  
 예를 들어, 콜백 클래스에서 <xref:System.ServiceModel.CallbackBehaviorAttribute?displayProperty=nameWithType> 특성의 속성을 사용하여 콜백 개체 런타임 동작을 다양하게 제어할 수 있습니다. 또 다른 예로, <xref:System.ServiceModel.Description.CallbackDebugBehavior?displayProperty=nameWithType> 클래스를 사용하여 콜백 개체를 호출하는 서비스에 예외 정보를 반환할 수 있습니다. 자세한 내용은 [이중 서비스](../../../docs/framework/wcf/feature-details/duplex-services.md)를 참조 하세요. 전체 샘플은 [이중](../../../docs/framework/wcf/samples/duplex.md)을 참조 하세요.  
  
 IIS(인터넷 정보 서비스) 5.1을 실행하는 Windows XP 컴퓨터에서 이중 클라이언트는 <xref:System.ServiceModel.WSDualHttpBinding?displayProperty=nameWithType> 클래스를 사용하여 클라이언트 기본 주소를 지정해야 합니다. 그렇지 않으면 예외가 throw됩니다. 다음 코드 예제에서는 코드에서 이 작업을 수행하는 방법을 보여 줍니다.  
  
 [!code-csharp[S_DualHttp#8](../../../samples/snippets/csharp/VS_Snippets_CFX/s_dualhttp/cs/program.cs#8)]
 [!code-vb[S_DualHttp#8](../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_dualhttp/vb/module1.vb#8)]  
  
 다음 코드에서는 구성 파일에서 이 작업을 수행하는 방법을 보여 줍니다.  
  
 [!code-csharp[S_DualHttp#134](../../../samples/snippets/csharp/VS_Snippets_CFX/s_dualhttp/cs/program.cs#134)]  
  
## <a name="calling-services-asynchronously"></a>비동기적으로 서비스 호출  
 작업이 호출되는 방법은 클라이언트 개발자에 의해 지정됩니다. 작업을 구성하는 메시지는 관리되는 코드에 표시될 때 동기 메서드나 비동기 메서드에 매핑될 수 있기 때문입니다. 따라서 작업을 비동기적으로 호출하는 클라이언트를 빌드하려면 Svcutil.exe에서 `/async` 옵션을 사용하여 비동기 클라이언트 코드를 생성할 수 있습니다. 자세한 내용은 [방법: 서비스 작업을 비동기적](../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md)으로 호출 합니다.  
  
## <a name="calling-services-using-wcf-client-channels"></a>WCF 클라이언트 채널을 사용하여 서비스 호출  
 WCF 클라이언트 형식은를 <xref:System.ServiceModel.ClientBase%601>확장 합니다. 자체는 <xref:System.ServiceModel.IClientChannel?displayProperty=nameWithType> 인터페이스에서 파생 되며 기본 채널 시스템을 노출 합니다. <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType> 클래스와의 대상 서비스 계약을 사용하여 서비스를 호출할 수 있습니다. 자세한 내용은 [WCF 클라이언트 아키텍처](../../../docs/framework/wcf/feature-details/client-architecture.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.ClientBase%601?displayProperty=nameWithType>
- <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType>
