---
title: 단방향 서비스
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation [WCF], one-way service contracts
- WCF [WCF], one-way service contracts
- service contracts [WCF], defining one-way
ms.assetid: 19053a36-4492-45a3-bfe6-0365ee0205a3
ms.openlocfilehash: d567674baa92ad096b10a1199fa3f04f05939df5
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991166"
---
# <a name="one-way-services"></a>단방향 서비스
서비스 작업의 기본 동작은 요청-회신 패턴입니다. 요청-회신 패턴의 경우 서비스 작업이 `void` 메서드로 코드에 표현된 경우에도 클라이언트에서 회신 메시지를 기다립니다. 단방향 작업을 사용하는 경우 하나의 메시지만 전송됩니다. 수신자는 회신 메시지를 보내지 않으며 발신자도 메시지를 기다리지 않습니다.  
  
 다음과 같은 경우 단방향 디자인 패턴을 사용합니다.  
  
- 클라이언트가 작업을 호출해야 하며 작업 수준에서 작업 결과에 영향을 받지 않는 경우.  
  
- <xref:System.ServiceModel.NetMsmqBinding> 또는 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> 클래스를 사용하는 경우. 이 시나리오에 대 한 자세한 내용은 [WCF의 큐](../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)를 참조 하십시오.  
  
 단방향 작업의 경우 오류 정보를 클라이언트로 전달하는 응답 메시지가 없습니다. 신뢰할 수 있는 세션과 같은 기본 바인딩의 기능을 사용하거나 두 개의 단방향 작업(하나는 서비스 작업을 호출하기 위한 클라이언트에서 서비스로의 단방향 계약이며, 다른 하나는 서비스가 클라이언트에서 구현하는 콜백을 사용하여 오류를 다시 클라이언트에 전달할 수 있는 서비스와 클라이언트 간 단방향 계약)을 사용하는 이중 서비스 계약을 디자인하여 오류 상태를 검색할 수 있습니다.  
  
 단방향 서비스 계약을 만들려면 다음 샘플 코드에서처럼 서비스 계약을 정의하고, <xref:System.ServiceModel.OperationContractAttribute> 클래스를 각 작업에 적용하여, <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 속성을 `true`로 설정합니다.  
  
```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IOneWayCalculator  
{  
    [OperationContract(IsOneWay=true)]  
    void Add(double n1, double n2);  
    [OperationContract(IsOneWay = true)]  
    void Subtract(double n1, double n2);  
    [OperationContract(IsOneWay = true)]  
    void Multiply(double n1, double n2);  
    [OperationContract(IsOneWay = true)]  
    void Divide(double n1, double n2);  
}  
```  
  
 전체 예제는 [단방향](../../../../docs/framework/wcf/samples/one-way.md) 샘플을 참조 하세요.  
  
## <a name="clients-blocking-with-one-way-operations"></a>단방향 작업을 사용하여 클라이언트 차단  
 일부 단방향 응용 프로그램은 네트워크 연결에 아웃 바운드 데이터를 기록 하는 즉시 반환 하지만, 일부 시나리오에서는 바인딩 또는 서비스를 구현 하면 단방향 작업을 사용 하 여 WCF 클라이언트가 차단 될 수 있습니다. WCF 클라이언트 응용 프로그램에서 WCF 클라이언트 개체는 아웃 바운드 데이터가 네트워크 연결에 기록 될 때까지 반환 되지 않습니다. 이는 단방향 작업을 비롯한 모든 메시지 교환 패턴에 적용되며, 전송에 데이터를 쓰는 동안 발생한 문제로 인해 클라이언트가 반환될 수 없음을 의미합니다. 문제에 따라 예외가 발생하거나 메시지를 서비스에 보낼 때 지연될 수 있습니다.  
  
 예를 들어, 전송에서 엔드포인트를 찾을 수 없는 경우 장시간 지연되지 않고 <xref:System.ServiceModel.EndpointNotFoundException?displayProperty=nameWithType> 예외가 throw됩니다. 그러나 다른 이유로 연결이 끊어져 서비스에서 데이터를 읽지 못하게 될 수도 있어 클라이언트 전송의 보내기 작업이 반환될 수 없습니다. 이 경우 클라이언트 전송 바인딩의 <xref:System.ServiceModel.Channels.Binding.SendTimeout%2A?displayProperty=nameWithType> 기간을 초과하면 <xref:System.TimeoutException?displayProperty=nameWithType>이 throw됩니다. 서비스에 너무 많은 메시지가 발생되어 서비스가 특정 지점 이후부터는 메시지를 처리할 수 없을 수도 있습니다. 이 경우에도 서비스가 메시지를 처리할 수 있게 되거나 예외가 throw될 때까지 단방향 클라이언트가 차단됩니다.  
  
 이 이외에도 서비스의 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A?displayProperty=nameWithType> 속성이 <xref:System.ServiceModel.ConcurrencyMode.Single>로 설정되고 바인딩에 세션을 사용하는 경우가 해당됩니다. 이 경우 디스패처는 세션의 요구 사항에 따라 들어오는 메시지에 순서를 지정하므로, 서비스에서 해당 세션의 이전 메시지를 처리할 때까지는 연결이 끊어져 다음 메시지를 읽을 수 없게 됩니다. 마찬가지로 클라이언트가 차단되지만, 예외 발생 여부는 클라이언트에 설정된 제한 시간 이전에 기다리는 데이터를 서비스가 처리할 수 있는지에 따라 결정됩니다.  
  
 이 문제는 클라이언트 개체와 클라이언트 전송의 보내기 작업 사이에 버퍼를 삽입하여 어느 정도 해결할 수 있습니다. 예를 들어, 비동기 호출을 사용하거나 메모리 내 메시지 큐를 사용하면 클라이언트 개체가 빠르게 반환되도록 합니다. 두 방법 모두 기능을 향상시키지만 스레드 풀과 메시지 큐의 크기가 제한됩니다.  
  
 따라서 서비스와 클라이언트의 여러 가지 컨트롤을 검사한 다음 애플리케이션 시나리오를 테스트하여 서비스 또는 클라이언트에 대한 최상의 구성을 결정하는 것이 좋습니다. 예를 들어, 세션 사용으로 인해 서비스에서 메시지 처리가 차단되는 경우 각 메시지가 다른 서비스 인스턴스에 의해 처리될 수 있도록 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> 속성을 <xref:System.ServiceModel.InstanceContextMode.PerCall>로 설정하고, 한 번에 둘 이상의 스레드에서 메시지를 디스패치할 수 있도록 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A>를 <xref:System.ServiceModel.ConcurrencyMode.Multiple>로 설정합니다. 또 다른 방법은 서비스 및 클라이언트 바인딩의 읽기 할당량을 늘리는 것입니다.  
  
## <a name="see-also"></a>참고자료

- [단방향](../../../../docs/framework/wcf/samples/one-way.md)
