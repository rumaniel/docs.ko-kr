---
title: '방법: 요청-회신 계약 만들기'
ms.date: 03/30/2017
ms.assetid: 801d90da-3d45-4284-9c9f-56c8aadb4060
ms.openlocfilehash: f5af7f3a0954e9becf1b9098f372878b537fec9c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645816"
---
# <a name="how-to-create-a-request-reply-contract"></a>방법: 요청-회신 계약 만들기
요청-회신 계약에서는 회신을 반환하는 메서드를 지정합니다. 회신은 이 계약 조건 하의 요청에 따라 전송되고 상호 관련되어야 합니다. 메서드가 회신을 반환하지 않는 경우(C#에서는 `void`, Visual Basic에서는 `Sub`)에도 인프라에서 빈 메시지를 만들어 호출자에게 보냅니다. 빈 회신 메시지가 전송되지 않도록 하려면 작업에 대한 단방향 계약을 사용합니다.  
  
### <a name="to-create-a-request-reply-contract"></a>요청-회신 계약을 만들려면  
  
1. 선택한 프로그래밍 언어로 인터페이스를 만듭니다.  
  
2. 인터페이스에 <xref:System.ServiceModel.ServiceContractAttribute> 특성을 적용합니다.  
  
3. 클라이언트가 호출할 수 있는 각 메서드에 <xref:System.ServiceModel.OperationContractAttribute> 특성을 적용합니다.  
  
4. 선택 사항입니다. 빈 회신 메시지가 전송되지 않도록 하려면 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 속성의 값을 `true`로 설정합니다. 기본적으로 모든 작업은 요청-회신 계약 하에서 수행됩니다.  
  
## <a name="example"></a>예제  
 다음 샘플에서는 `Add` 및 `Subtract` 메서드를 제공하는 계산기 서비스에 대한 계약을 정의합니다. `Multiply` 메서드는 <xref:System.ServiceModel.OperationContractAttribute> 클래스에 의해 표시되지 않으므로 계약의 일부가 아니며, 따라서 클라이언트에 액세스할 수 없습니다.  
  
```csharp
using System.ServiceModel;

[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    // It would be equivalent to write explicitly:
    // [OperationContract(IsOneWay=false)]
    int Add(int a, int b);
    
    [OperationContract]
    int Subtract(int a, int b);
    
    int Multiply(int a, int b)
}
```
  
- 작업 계약을 지정 하는 방법에 대 한 자세한 내용은 참조는 <xref:System.ServiceModel.OperationContractAttribute> 클래스 및 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 속성입니다.  
  
- <xref:System.ServiceModel.ServiceContractAttribute> 및 <xref:System.ServiceModel.OperationContractAttribute> 특성을 적용하면 서비스를 배포한 후에 WSDL(웹 서비스 기술 언어) 문서에서 서비스 계약 정의가 자동으로 생성됩니다. 서비스의 HTTP 기본 주소에 `?wsdl`을 추가하면 문서가 다운로드됩니다. 예를 들면 `http://microsoft/CalculatorService?wsdl`과 같습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.OperationContractAttribute>
- [서비스 계약 디자인](../../../../docs/framework/wcf/designing-service-contracts.md)
- [방법: 이중 계약 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)
