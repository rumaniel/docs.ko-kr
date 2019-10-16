---
title: 세션, 인스턴스 및 동시성
ms.date: 03/30/2017
ms.assetid: 50797a3b-7678-44ed-8138-49ac1602f35b
ms.openlocfilehash: d780488f7bb0bd46a22ef205b3954b6b4614cae0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69969207"
---
# <a name="sessions-instancing-and-concurrency"></a>세션, 인스턴스 및 동시성
*세션* 은 두 개의 끝점 사이에 전송된 모든 메시지의 상관 관계입니다. *인스턴스 만들기* 는 사용자 정의 서비스 개체와 관련 <xref:System.ServiceModel.InstanceContext> 개체의 수명 제어를 의미합니다. *동시성* 은 <xref:System.ServiceModel.InstanceContext> 에서 동시에 실행되는 스레드 수의 제어를 의미하는 용어입니다.  
  
 이 항목에서는 이러한 설정, 설정 사용 방법 및 설정 간의 다양한 상호 작용에 대해 설명합니다.  
  
## <a name="sessions"></a>세션  
 서비스 계약이 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=nameWithType> 속성을 <xref:System.ServiceModel.SessionMode.Required?displayProperty=nameWithType>로 설정할 경우 해당 계약은 모든 호출(호출을 지원하는 기본 메시지 교환)이 동일한 대화의 일부이어야 함을 의미합니다. 계약이 세션을 허용하지만 특정 세션이 필요 없음을 지정하는 경우, 클라이언트는 세션을 연결하여 설정하거나 설정하지 않을 수 있습니다. 세션이 종료되고 메시지가 동일한 세션 기반 채널을 통해 전송될 경우 예외가 throw됩니다.  
  
 WCF 세션에는 다음과 같은 주요 개념 기능이 있습니다.  
  
- 이러한 기능은 호출 애플리케이션에 의해 명시적으로 시작되고 종료됩니다.  
  
- 한 세션 동안 배달된 메시지는 수신된 순서대로 처리됩니다.  
  
- 세션은 메시지 그룹을 대화에 연결합니다. 상관 관계의 의미는 추상적입니다. 예를 들어, 공유된 네트워크 연결을 기반으로 메시지와 연결될 수 있는 세션 기반 채널이 있는 반면 메시지 본문의 공유 태그를 기반으로 메시지와 연결될 수 있는 세션 기반 채널도 있습니다. 세션에서 파생될 수 있는 기능은 상관 관계의 특성에 따라 다릅니다.  
  
- WCF 세션과 연결 된 일반 데이터 저장소는 없습니다.  
  
 ASP.NET 응용 프로그램의 <xref:System.Web.SessionState.HttpSessionState?displayProperty=nameWithType> 클래스와이 클래스에서 제공 하는 기능에 대해 잘 알고 있는 경우 해당 종류의 세션과 WCF 세션 간에 다음과 같은 차이점을 알 수 있습니다.  
  
- ASP.NET 세션은 항상 서버에서 시작 됩니다.  
  
- ASP.NET 세션은 암시적으로 순서가 지정 되지 않습니다.  
  
- ASP.NET 세션은 요청에 대해 일반 데이터 저장소 메커니즘을 제공 합니다.  
  
 클라이언트 애플리케이션과 서비스 애플리케이션은 서로 다른 방법으로 세션과 상호 작용합니다. 클라이언트 애플리케이션은 세션을 시작한 다음 세션 내에서 전송된 메시지를 수신하여 처리합니다. 서비스 애플리케이션은 세션을 확장성 지점으로 사용하여 추가 동작을 추가합니다. <xref:System.ServiceModel.InstanceContext> 와 직접 작업하거나 사용자 지정 인스턴스 컨텍스트 공급자를 구현하여 수행합니다.  
  
## <a name="instancing"></a>인스턴스 만들기  
 인스턴스 만들기 동작(<xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> 속성을 사용하여 설정)은 들어오는 메시지에 대한 응답으로 <xref:System.ServiceModel.InstanceContext>를 만드는 방법을 제어합니다. 기본적으로 각 <xref:System.ServiceModel.InstanceContext> 는 하나의 사용자 정의 서비스 개체와 연결되기 때문에 기본적인 경우 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> 속성을 설정하면 사용자 정의 서비스 개체의 인스턴스 만들기도 제어합니다. <xref:System.ServiceModel.InstanceContextMode> 열거형은 인스턴스 만들기 모드를 정의합니다.  
  
 사용할 수 있는 인스턴스 만들기 모드는 다음과 같습니다.  
  
- <xref:System.ServiceModel.InstanceContextMode.PerCall>: 각 클라이언트 <xref:System.ServiceModel.InstanceContext> 요청에 대해 새로운 (및 따라서 서비스 개체)가 만들어집니다.  
  
- <xref:System.ServiceModel.InstanceContextMode.PerSession>: <xref:System.ServiceModel.InstanceContext> 새 (및 따라서 서비스 개체)는 각각의 새 클라이언트 세션에 대해 생성 되 고 해당 세션의 수명 동안 유지 관리 됩니다 (세션을 지 원하는 바인딩이 필요 함).  
  
- <xref:System.ServiceModel.InstanceContextMode.Single>: 단일 <xref:System.ServiceModel.InstanceContext> (및 따라서 서비스 개체)는 응용 프로그램의 수명에 대 한 모든 클라이언트 요청을 처리 합니다.  
  
 다음 코드 예제에서는 명시적으로 서비스 클래스에 설정되는 기본 <xref:System.ServiceModel.InstanceContextMode> 값인 <xref:System.ServiceModel.InstanceContextMode.PerSession> 을 보여 줍니다.  
  
```  
[ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]   
public class CalculatorService : ICalculatorInstance   
{   
    ...  
}  
```  
  
 또한 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> 속성은 <xref:System.ServiceModel.InstanceContext>가 해제되는 주기를 제어하는 반면에 <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=nameWithType> 및 <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A?displayProperty=nameWithType> 속성은 서비스 개체가 해제되는 시점을 제어합니다.  
  
### <a name="well-known-singleton-services"></a>잘 알려진 singleton 서비스  
 단일 인스턴스 서비스 개체에 대한 변형된 개체가 유용한 경우도 있습니다. 서비스 개체를 직접 만들고 해당 개체를 사용하여 서비스 호스트를 만들 수 있습니다. 이렇게 하려면 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> 속성도 <xref:System.ServiceModel.InstanceContextMode.Single>로 설정해야 하며, 그렇지 않으면 서비스 호스트를 열 때 예외가 throw됩니다.  
  
 <xref:System.ServiceModel.ServiceHost.%23ctor%28System.Object%2CSystem.Uri%5B%5D%29?displayProperty=nameWithType> 생성자를 사용하여 이러한 서비스를 만듭니다. singleton 서비스에서 사용할 특정 개체 인스턴스를 제공하려면 사용자 지정 <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer?displayProperty=nameWithType>를 구현하는 대신 제공합니다. 예를 들어, 매개 변수가 없는 기본 public 생성자를 구현하지 않는 경우와 같이 서비스 구현 형식을 생성하기 어려운 경우 이 오버로드를 사용할 수 있습니다.  
  
 이 생성자에 개체가 제공 되 면 WCF (Windows Communication Foundation) 인스턴스 동작과 관련 된 일부 기능이 다르게 작동 합니다. 예를 들어 singleton 개체 인스턴스를 제공하는 경우 <xref:System.ServiceModel.InstanceContext.ReleaseServiceInstance%2A?displayProperty=nameWithType> 호출은 아무런 효과가 없습니다. 마찬가지로 다른 인스턴스 해제 메커니즘도 무시됩니다. <xref:System.ServiceModel.ServiceHost>는 항상 모든 작업에 대해 <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=nameWithType> 속성이 <xref:System.ServiceModel.ReleaseInstanceMode.None?displayProperty=nameWithType>으로 설정된 것처럼 동작합니다.  
  
### <a name="sharing-instancecontext-objects"></a>InstanceContext 개체 공유  
 또한 해당 연결을 직접 수행하여 <xref:System.ServiceModel.InstanceContext> 개체와 연결된 세션 채널 또는 호출을 제어할 수도 있습니다.  
  
## <a name="concurrency"></a>동시성  
 동시성은 <xref:System.ServiceModel.InstanceContext> 에서 동시에 활성화되는 스레드 수의 제어입니다. <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A?displayProperty=nameWithType> 열거형과 함께 <xref:System.ServiceModel.ConcurrencyMode>를 사용하여 이를 제어합니다.  
  
 사용할 수 있는 세 가지 동시성 모드는 다음과 같습니다.  
  
- <xref:System.ServiceModel.ConcurrencyMode.Single>: 각 인스턴스 컨텍스트는 한 번에 인스턴스 컨텍스트에서 메시지를 처리 하는 최대 하나의 스레드를 가질 수 있습니다. 동일한 인스턴스 컨텍스트를 사용하려는 다른 스레드는 원래 스레드가 인스턴스 컨텍스트를 종료할 때까지 차단되어야 합니다.  
  
- <xref:System.ServiceModel.ConcurrencyMode.Multiple>: 각 서비스 인스턴스는 메시지를 동시에 처리 하는 여러 스레드를 가질 수 있습니다. 이 동시성 모드를 사용하려면 스레드로부터 안전하게 서비스를 구현해야 합니다.  
  
- <xref:System.ServiceModel.ConcurrencyMode.Reentrant>: 각 서비스 인스턴스는 한 번에 하나의 메시지를 처리 하지만 다시 재진입용 작업 호출을 허용 합니다. 서비스는 WCF 클라이언트 개체를 통해 호출 하는 경우에만 이러한 호출을 허용 합니다.  
  
> [!NOTE]
> 둘 이상의 스레드를 안전하게 사용하는 코드를 이해하고 개발하기는 쉽지 않습니다. <xref:System.ServiceModel.ConcurrencyMode.Multiple> 또는 <xref:System.ServiceModel.ConcurrencyMode.Reentrant> 값을 사용하기 전에 이러한 모드에 대해 해당 서비스가 적절하게 디자인되었는지 확인합니다. 자세한 내용은 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A>을 참조하세요.  
  
 동시성 사용은 인스턴스 만들기 모드와 관련됩니다. 인스턴스 <xref:System.ServiceModel.InstanceContextMode.PerCall> 만들기에서 각 메시지가 새 <xref:System.ServiceModel.InstanceContext> 에 의해 처리 되 고 따라서 둘 이상의 <xref:System.ServiceModel.InstanceContext>스레드가에서 활성화 되지 않기 때문에 동시성이 관련 되지 않습니다.  
  
 다음 코드 예제에서는 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> 속성을 <xref:System.ServiceModel.ConcurrencyMode.Multiple>로 설정하는 방법을 보여 줍니다.  
  
```  
[ServiceBehavior(ConcurrencyMode=ConcurrencyMode.Multiple, InstanceContextMode = InstanceContextMode.Single)]   
public class CalculatorService : ICalculatorConcurrency   
{   
    ...  
}  
```  
  
## <a name="sessions-interact-with-instancecontext-settings"></a>세션이 InstanceContext 설정과 상호 작용  
 세션 및 <xref:System.ServiceModel.InstanceContext>는 계약의 <xref:System.ServiceModel.SessionMode> 열거형 값 조합 및 채널과 특정 서비스 개체 간의 연결을 제어하는 서비스 구현의 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> 속성에 따라 상호 작용합니다.  
  
 다음 표에서는 서비스에서 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=nameWithType> 속성과 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> 속성의 값을 조합하는 경우 세션을 지원하거나 지원하지 않는 들어오는 채널의 결과를 보여 줍니다.  
  
|InstanceContextMode 값|<xref:System.ServiceModel.SessionMode.Required>|<xref:System.ServiceModel.SessionMode.Allowed>|<xref:System.ServiceModel.SessionMode.NotAllowed>|  
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|  
|PerCall|-세션 channel을 사용한 동작: 각 호출에 <xref:System.ServiceModel.InstanceContext> 대 한 세션 및입니다.<br />-세션 없는 채널이 있는 동작: 예외가 throw됩니다.|-세션 channel을 사용한 동작: 각 호출에 <xref:System.ServiceModel.InstanceContext> 대 한 세션 및입니다.<br />-세션 없는 채널이 있는 동작: 각 <xref:System.ServiceModel.InstanceContext> 호출에 대 한입니다.|-세션 channel을 사용한 동작: 예외가 throw됩니다.<br />-세션 없는 채널이 있는 동작: 각 <xref:System.ServiceModel.InstanceContext> 호출에 대 한입니다.|  
|PerSession|-세션 channel을 사용한 동작: 각 채널에 <xref:System.ServiceModel.InstanceContext> 대 한 세션 및입니다.<br />-세션 없는 채널이 있는 동작: 예외가 throw됩니다.|-세션 channel을 사용한 동작: 각 채널에 <xref:System.ServiceModel.InstanceContext> 대 한 세션 및입니다.<br />-세션 없는 채널이 있는 동작: 각 <xref:System.ServiceModel.InstanceContext> 호출에 대 한입니다.|-세션 channel을 사용한 동작: 예외가 throw됩니다.<br />-세션 없는 채널이 있는 동작: 각 <xref:System.ServiceModel.InstanceContext> 호출에 대 한입니다.|  
|Single|-세션 channel을 사용한 동작: 세션 하나 <xref:System.ServiceModel.InstanceContext> 및 모든 호출에 대 한 세션입니다.<br />-세션 없는 채널이 있는 동작: 예외가 throw됩니다.|-세션 channel을 사용한 동작: 생성 되거나 사용자 <xref:System.ServiceModel.InstanceContext> 가 지정한 단일 항목에 대 한 세션 및입니다.<br />-세션 없는 채널이 있는 동작: 만들어지거나 사용자가 지정한 단일 항목 에대한입니다.<xref:System.ServiceModel.InstanceContext>|-세션 channel을 사용한 동작: 예외가 throw됩니다.<br />-세션 없는 채널이 있는 동작: 만든 각 singleton 또는 사용자 지정 singleton에 대한입니다.<xref:System.ServiceModel.InstanceContext>|  
  
## <a name="see-also"></a>참고자료

- [세션 사용](../../../../docs/framework/wcf/using-sessions.md)
- [방법: 세션이 필요한 서비스 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-that-requires-sessions.md)
- [방법: 제어 서비스 인스턴스](../../../../docs/framework/wcf/feature-details/how-to-control-service-instancing.md)
- [동시성](../../../../docs/framework/wcf/samples/concurrency.md)
- [인스턴스 만들기](../../../../docs/framework/wcf/samples/instancing.md)
- [세션](../../../../docs/framework/wcf/samples/session.md)
