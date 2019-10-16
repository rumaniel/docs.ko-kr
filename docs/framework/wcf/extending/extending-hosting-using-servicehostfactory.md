---
title: ServiceHostFactory를 사용하여 호스팅 확장명
ms.date: 03/30/2017
ms.assetid: bcc5ae1b-21ce-4e0e-a184-17fad74a441e
ms.openlocfilehash: de6a590b94285872dd77006eda7f86d5d629be9d
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70849908"
---
# <a name="extending-hosting-using-servicehostfactory"></a>ServiceHostFactory를 사용하여 호스팅 확장명
Wcf ( <xref:System.ServiceModel.ServiceHost> Windows Communication Foundation)에서 서비스를 호스팅하기 위한 표준 API는 wcf 아키텍처의 확장성 지점입니다. 사용자는 일반적으로 <xref:System.ServiceModel.ServiceHost>을 사용하여 서비스를 열기 전에 기본 엔드포인트를 명령적으로 추가하거나 동작을 수정하도록 <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening>을 재지정하기 위해 <xref:System.ServiceModel.Description.ServiceDescription>에서 호스트 클래스를 파생할 수 있습니다.  
  
 자체 호스팅 환경에서는 호스트를 인스턴스화하는 코드를 쓴 다음 해당 코드를 인스턴스화한 후에 그 코드에서 <xref:System.ServiceModel.ServiceHost>을 호출하기 때문에 사용자 지정 <xref:System.ServiceModel.ICommunicationObject.Open>를 만들 필요가 없습니다. 이러한 두 단계 사이에서 원하는 작업을 수행할 수 있습니다. 예를 들어 다음과 같이 새 <xref:System.ServiceModel.Description.IServiceBehavior>를 추가할 수 있습니다.  
  
```csharp
public static void Main()  
{  
   ServiceHost host = new ServiceHost( typeof( MyService ) );  
   host.Description.Add( new MyServiceBehavior() );  
   host.Open();  
  
   ...  
}  
```  
  
 이 접근 방법은 다시 사용할 수 없습니다. 설명을 조작하는 코드는 호스트 프로그램에 코딩되기 때문에(이 경우 Main() 함수) 다른 컨텍스트에서 해당 논리를 다시 사용하기 어렵습니다. 또한 명령적 코드가 필요 없는 <xref:System.ServiceModel.Description.IServiceBehavior>를 추가하는 다른 방법이 있습니다. <xref:System.ServiceModel.ServiceBehaviorAttribute>에서 특성을 파생시켜 서비스 구현 형식에 적용하거나 구성 가능한 사용자 지정 동작을 만들고 구성을 사용하여 이 동작을 동적으로 구성할 수 있습니다.  
  
 그러나 이 문제를 해결하기 위해 약간 변형된 예제를 사용할 수도 있습니다. 한 가지 방법은 `Main()` 외부의 ServiceBehavior를 추가하는 코드를 <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A>의 사용자 지정 파생 항목에 포함되는 <xref:System.ServiceModel.ServiceHost> 메서드로 이동하는 것입니다.  
  
```csharp
public class DerivedHost : ServiceHost  
{  
   public DerivedHost( Type t, params Uri baseAddresses ) :  
      base( t, baseAddresses ) {}  
  
   public override void OnOpening()  
   {  
  this.Description.Add( new MyServiceBehavior() );  
   }  
}  
```  
  
 그런 다음 `Main()` 대신 다음을 사용할 수 있습니다.  
  
```csharp
public static void Main()  
{  
   ServiceHost host = new DerivedHost( typeof( MyService ) );  
   host.Open();  
  
   ...  
}  
```  
  
 이제 사용자 지정 논리를 다양한 호스트 실행 파일에 쉽게 다시 사용할 수 있는 명확하고 추상적인 개념으로 캡슐화했습니다.  
  
 IIS(인터넷 정보 서비스) 또는 WAS(Windows Process Activation Service) 내부에서 이 사용자 지정 <xref:System.ServiceModel.ServiceHost>를 사용하는 방법이 확실하지 않습니다. 호스팅 환경은 애플리케이션 대신 <xref:System.ServiceModel.ServiceHost>를 인스턴스화하는 환경이기 때문에 이러한 환경은 자체 호스팅 환경과는 다릅니다. IIS 및 WAS 호스팅 인프라에서는 사용자 지정 <xref:System.ServiceModel.ServiceHost> 지시문에 대한 어떠한 정보도 알 수 없습니다.  
  
 <xref:System.ServiceModel.Activation.ServiceHostFactory>는 IIS 또는 WAS 내에서 사용자 지정 <xref:System.ServiceModel.ServiceHost>에 액세스할 때의 문제를 해결하도록 설계되었습니다. <xref:System.ServiceModel.ServiceHost>에서 파생되는 사용자 지정 호스트는 동적으로 구성되고 잠재적으로 다양한 형식이기 때문에 호스팅 환경은 이러한 호스트를 직접 인스턴스화하지 않습니다. 대신 WCF는 팩터리 패턴을 사용 하 여 호스팅 환경 및 서비스의 구체적인 형식 간에 간접 참조 계층을 제공 합니다. 이러한 경우가 아닌 한 <xref:System.ServiceModel.Activation.ServiceHostFactory>의 인스턴스를 반환하는 <xref:System.ServiceModel.ServiceHost>의 기본 구현을 사용합니다. 그러나 @ServiceHost 지시문에 팩터리 구현의 CLR 형식 이름을 지정 하 여 파생 호스트를 반환 하는 고유한 팩터리를 제공할 수도 있습니다.  
  
 일반적인 경우 팩터리를 구현하는 작업은 단순해야 합니다. 예를 들어 다음은 파생된 <xref:System.ServiceModel.Activation.ServiceHostFactory>를 반환하는 사용자 지정 <xref:System.ServiceModel.ServiceHost>입니다.  
  
```csharp
public class DerivedFactory : ServiceHostFactory  
{  
   public override ServiceHost CreateServiceHost( Type t, Uri[] baseAddresses )  
   {  
      return new DerivedHost( t, baseAddresses )  
   }  
}  
```  
  
 기본 팩터리 대신이 팩터리를 사용 하려면 다음과 같이 @ServiceHost 지시문에 형식 이름을 제공 합니다.  
  
`<% @ServiceHost Factory="DerivedFactory" Service="MyService" %>`  
  
 <xref:System.ServiceModel.ServiceHost>에서 반환하는 <xref:System.ServiceModel.Activation.ServiceHostFactory.CreateServiceHost%2A>에 대해 원하는 작업을 수행하는 데 기술적 제한은 없지만 가능한 간단하게 팩터리 구현을 유지하는 것이 좋습니다. 사용자 지정 논리가 많은 경우 다시 사용할 수 있도록 팩터리 내부 대신 호스트 내부에 해당 논리를 배치 하는 것이 좋습니다.  
  
 여기에서는 호스팅 API에 대한 하나 이상의 레이어를 언급해야 합니다. WCF에 <xref:System.ServiceModel.ServiceHostBase> 는와 <xref:System.ServiceModel.Activation.ServiceHostFactoryBase> <xref:System.ServiceModel.ServiceHost> 가<xref:System.ServiceModel.Activation.ServiceHostFactory> 각각 파생 되는 및도 있습니다. 이러한 경우는 상당한 부분의 메타데이터 시스템을 사용자 지정된 생성 항목과 스왑해야 하는 고급 시나리오에 적합합니다.
