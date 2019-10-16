---
title: 오류 정의 및 지정
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- handling faults [WCF], specifying
- handling faults [WCF], defining
ms.assetid: c00c84f1-962d-46a7-b07f-ebc4f80fbfc1
ms.openlocfilehash: 37ded0aad547df616d2b8b73e7cb145514da080d
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972361"
---
# <a name="defining-and-specifying-faults"></a>오류 정의 및 지정
SOAP 오류는 오류 조건 정보를 서비스에서 클라이언트로 전달하고 양방향인 경우 상호 운용 가능한 방식으로 클라이언트에서 서비스로 전달합니다. 이 항목에서는 사용자 지정 오류 내용을 정의하는 시간과 방법에 대해 설명하고 이들을 반환할 수 있는 작업을 지정합니다. 서비스 또는 이중 클라이언트에서 이러한 오류를 보낼 수 있는 방법과 클라이언트 또는 서비스 응용 프로그램이 이러한 오류를 처리 하는 방법에 대 한 자세한 내용은 [오류 전송 및 수신](../../../docs/framework/wcf/sending-and-receiving-faults.md)을 참조 하세요. WCF (Windows Communication Foundation) 응용 프로그램의 오류 처리에 대 한 개요는 [계약 및 서비스에서 오류 지정 및 처리](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)를 참조 하세요.  
  
## <a name="overview"></a>개요  
 선언된 SOAP 오류는 작업에 사용자 지정 SOAP 오류 유형을 지정하는 <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType>가 있는 오류입니다. 선언되지 않은 SOAP 오류는 작업 계약에 지정되지 않은 오류입니다. 이 항목에서는 이러한 오류 조건을 식별하고, 클라이언트가 사용자 지정 SOAP 오류의 알림을 받을 때 이러한 오류 조건을 제대로 처리하는 데 사용할 수 있는 서비스에 대한 오류 계약을 만드는 과정을 도와 줍니다. 기본 작업은 순서대로 다음과 같습니다.  
  
1. 서비스 클라이언트에서 알아야 하는 오류 조건을 정의합니다.  
  
2. 이러한 오류 조건에 대한 SOAP 오류의 사용자 지정 콘텐츠를 정의합니다.  
  
3. throw하는 특정 SOAP 오류가 WSDL로 클라이언트에 노출되도록 작업을 표시합니다.  
  
### <a name="defining-error-conditions-that-clients-should-know-about"></a>클라이언트가 알아야 하는 오류 조건 정의  
 SOAP 오류는 특정 작업에 대한 오류 정보를 전달하는 공개적으로 설명된 메시지입니다. WSDL로 다른 작업 메시지와 함께 설명되므로 클라이언트는 작업을 호출할 때 이러한 오류를 알고 처리합니다. 그러나 WCF 서비스는 관리 코드로 작성 되므로 오류로 변환 되 고 클라이언트로 반환 되는 오류 조건을 결정 하는 것은 형식 오류와 서비스의 오류 조건 및 버그를 구분할 수 있는 기회를 제공 합니다. 클라이언트를 사용 하 여 대화를 합니다.  
  
 예를 들어 다음 코드 예제에서는 두 개의 정수를 받고 다른 정수를 반환하는 작업을 보여 줍니다. 여기서 여러 개의 예외가 throw될 수 있으므로 오류 계약을 디자인할 때 클라이언트에 중요한 오류 조건을 결정해야 합니다. 이 경우 서비스에서 <xref:System.DivideByZeroException?displayProperty=nameWithType> 예외를 감지해야 합니다.  
  
```csharp  
[ServiceContract]  
public class CalculatorService  
{  
    [OperationContract]   
    int Divide(int a, int b)  
    {  
      if (b==0) throw new Exception("Division by zero!");  
      return a/b;  
    }  
}  
```  
  
```vb
<ServiceContract> _
Public Class CalculatorService
    <OperationContract> _
    Public Function Divide(a As Integer, b As Integer) As Integer
        If b = 0 Then Throw New DivideByZeroException("Division by zero!")
        Return a / b
    End Function
End Class
```
  
 앞의 예제에서 작업은 0으로 나누기와 관련된 사용자 지정 SOAP 오류, 수학 연산과 관련이 있지만 0으로 나누기와 관련된 정보를 포함하는 사용자 지정 오류, 다른 여러 오류 상태에 대한 여러 개의 오류 또는 SOAP 오류 없음을 반환할 수 있습니다.  
  
### <a name="define-the-content-of-error-conditions"></a>오류 조건의 콘텐츠 정의  
 오류 조건이 유용하게 사용자 지정 SOAP 오류를 반환할 수 있는 오류 조건으로 식별되고 나면 다음 단계로 해당 오류의 콘텐츠를 정의하고 콘텐츠 구조가 serialize될 수 있도록 합니다. 이전 섹션의 코드 예제에서는 `Divide` 작업과 관련이 있는 오류를 보여 주지만 `Calculator` 서비스에 다른 작업이 있는 경우 하나의 사용자 지정 SOAP 오류에서 `Divide`를 포함한 모든 계산기 오류 조건을 클라이언트에 알릴 수 있습니다. 다음 코드 예제에서는 `MathFault`를 비롯하여 모든 수학 연산의 오류를 보고할 수 있는 사용자 지정 SOAP 오류인 `Divide`를 만드는 방법을 보여 줍니다. 클래스에서 작업(`Operation` 속성)과 문제를 설명하는 값(`ProblemType` 속성)을 지정할 수 있지만 클래스 및 이러한 속성을 사용자 지정 SOAP 오류로 클라이언트에 전송하려면 serialize할 수 있어야 합니다. 따라서 <xref:System.Runtime.Serialization.DataContractAttribute?displayProperty=nameWithType> 및 <xref:System.Runtime.Serialization.DataMemberAttribute?displayProperty=nameWithType> 특성이 사용되어 형식과 해당 속성을 serialize할 수 있고 가능한 한 상호 운용될 수 있도록 합니다.  
  
 [!code-csharp[Faults#2](../../../samples/snippets/csharp/VS_Snippets_CFX/faults/cs/service.cs#2)]
 [!code-vb[Faults#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faults/vb/service.vb#2)]  
  
 데이터를 serialize 할 수 있는지 확인 하는 방법에 대 한 자세한 내용은 [서비스 계약의 데이터 전송 지정](../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)을 참조 하세요. 에서 제공 하는 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> serialization 지원 목록은 [데이터 계약 Serializer에서 지 원하는 형식](../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)을 참조 하세요.  
  
### <a name="mark-operations-to-establish-the-fault-contract"></a>오류 계약을 설정하도록 작업 표시  
 사용자 지정 SOAP 오류의 일부로 반환되는 serialize될 수 있는 데이터 구조를 정의하고 나면 마지막 단계로 해당 형식의 SOAP 오류를 throw하는 것으로 작업 계약을 표시합니다. 이렇게 하려면 <xref:System.ServiceModel.FaultContractAttribute?displayProperty=nameWithType> 특성을 사용하고 생성한 사용자 지정 데이터 형식을 전달합니다. 다음 코드 예제에서는 <xref:System.ServiceModel.FaultContractAttribute> 특성을 사용하여 `Divide` 작업에서 `MathFault` 형식의 SOAP 오류를 반환할 수 있도록 지정하는 방법을 보여 줍니다. 이제 다른 수학 기반 연산에서도 `MathFault`를 반환할 수 있도록 지정할 수 있습니다.  
  
 [!code-csharp[Faults#1](../../../samples/snippets/csharp/VS_Snippets_CFX/faults/cs/service.cs#1)]
 [!code-vb[Faults#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faults/vb/service.vb#1)]  
  
 둘 이상의 <xref:System.ServiceModel.FaultContractAttribute> 특성으로 작업을 표시하여 해당 작업에서 둘 이상의 사용자 지정 오류를 반환하도록 지정할 수 있습니다.  
  
 작업 구현에서 오류 계약을 구현 하는 다음 단계는 [오류 송수신](../../../docs/framework/wcf/sending-and-receiving-faults.md)항목에 설명 되어 있습니다.  
  
#### <a name="soap-wsdl-and-interoperability-considerations"></a>SOAP, WSDL 및 상호 운용성 고려 사항  
 경우에 따라, 특히 다른 플랫폼과 상호 운용하는 경우 오류가 SOAP 메시지에 나타나는 방식이나 WSDL 메타데이터에 설명되는 방식의 제어가 중요할 수 있습니다.  
  
 <xref:System.ServiceModel.FaultContractAttribute> 특성에는 해당 오류의 메타데이터에 생성되는 WSDL 오류 요소 이름을 제어할 수 있는 <xref:System.ServiceModel.FaultContractAttribute.Name%2A> 속성이 있습니다.  
  
 SOAP 표준에 따라 오류에는 `Action`, `Code` 및 `Reason`이 있을 수 있습니다. `Action`은 <xref:System.ServiceModel.FaultContractAttribute.Action%2A> 속성에 의해 제어됩니다. <xref:System.ServiceModel.FaultException.Code%2A> 속성과 <xref:System.ServiceModel.FaultException.Reason%2A> 속성은 모두 제네릭 <xref:System.ServiceModel.FaultException?displayProperty=nameWithType>의 부모 클래스인 <xref:System.ServiceModel.FaultException%601?displayProperty=nameWithType> 클래스의 속성입니다. `Code` 속성에는 <xref:System.ServiceModel.FaultCode.SubCode%2A> 멤버가 포함되어 있습니다.  
  
 오류를 생성하는 비서비스에 액세스하는 경우 특정 제한 사항이 있습니다. WCF는 스키마가 설명 하 고 데이터 계약과 호환 되는 세부 유형의 오류만 지원 합니다. 예를 들어 위에서 언급 한 것 처럼 WCF는 세부 정보 형식에서 XML 특성을 사용 하는 오류를 지원 하지 않습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.FaultContractAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- [계약 및 서비스에서 오류 지정 및 처리](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)
- [오류 보내기 및 받기](../../../docs/framework/wcf/sending-and-receiving-faults.md)
- [방법: 서비스 계약에서 오류 선언](../../../docs/framework/wcf/how-to-declare-faults-in-service-contracts.md)
- [보호 수준 이해](../../../docs/framework/wcf/understanding-protection-level.md)
- [방법: ProtectionLevel 속성 설정](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md)
- [서비스 계약에서 데이터 전송 지정](../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)
