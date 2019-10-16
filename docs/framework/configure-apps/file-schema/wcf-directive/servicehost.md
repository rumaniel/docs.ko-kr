---
title: '@ServiceHost'
ms.date: 03/30/2017
ms.assetid: 96ba6967-00f2-422f-9aa7-15de4d33ebf3
ms.openlocfilehash: a56fb1bb9395425222347914fe3f4c17f1a451b7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69920333"
---
# <a name="servicehost"></a>\@ServiceHost
서비스 호스트를 생성하는 데 사용되는 팩터리를 호스트할 서비스 및 .svc 파일에 제공된 호스팅 코드에 액세스하거나 이를 컴파일하는 데 필요한 다른 프로그래밍 요소에 연결합니다.  
  
## <a name="syntax"></a>구문  
  
```  
<% @ServiceHost   
Service = "Service, ServiceNamespace"   
Factory = "Factory, FactoryNamespace"  
Debug = "Debug"  
Language = "Language"   
CodeBehind = "CodeBehind"%>  
```  
  
## <a name="attributes"></a>특성  
  
#### <a name="service"></a>서비스  
 호스트되는 서비스의 CLR 형식 이름입니다. 이 이름은 하나 이상의 서비스 계약을 구현하는 형식의 정규화된 이름이어야 합니다.  
  
#### <a name="factory"></a>Factory  
 서비스 호스트를 인스턴스화하는 데 사용되는 서비스 호스트 팩터리의 CLR 형식 이름입니다. 이 특성은 선택적 요소입니다. 지정되지 않은 경우 <xref:System.ServiceModel.Activation.ServiceHostFactory>의 인스턴스를 반환하는 <xref:System.ServiceModel.ServiceHost> 기본값이 사용됩니다.  
  
#### <a name="debug"></a>디버그  
 디버그 기호를 사용 하 여 WCF (Windows Communication Foundation) 서비스를 컴파일해야 하는지 여부를 나타냅니다. `true`디버그 기호를 사용 하 여 WCF 서비스를 컴파일해야 하면이 고, 그렇지 않으면입니다. 그렇지 않으면 `false`입니다.  
  
#### <a name="language"></a>언어  
 파일(.svc) 내의 인라인 코드를 모두 컴파일할 때 사용되는 언어를 지정합니다. C#, Visual Basic .NET 및 JScript .NET을 각각 나타내는 C#, VB 및 JS를 비롯한 모든 .NET 지원 언어를 값으로 나타낼 수 있습니다. 이 특성은 선택적 요소입니다.  
  
#### <a name="codebehind"></a>CodeBehind  
 XML Web services를 구현하는 클래스가 동일한 파일에 있지 않고, 어셈블리로 컴파일되어 있지 않으며, \Bin 디렉터리에 저장된 경우 XML Web services를 구현하는 소스 파일을 지정합니다.  
  
## <a name="remarks"></a>설명  
 서비스 <xref:System.ServiceModel.ServiceHost> 를 호스트 하는 데 사용 되는은 WCF (Windows Communication Foundation) 프로그래밍 모델 내의 확장성 지점입니다. 팩터리 패턴은 호스팅 환경에서 직접 인스턴스화하면 안 되는 다형 형식이므로 <xref:System.ServiceModel.ServiceHost>를 인스턴스화하는 데 사용됩니다.  
  
 기본 구현에서는 <xref:System.ServiceModel.Activation.ServiceHostFactory>를 사용하여 <xref:System.ServiceModel.ServiceHost>의 인스턴스를 만듭니다. 그러나 [ \@ServiceHost](servicehost.md) 지시문에 팩터리 구현의 CLR 형식 이름을 지정 하 여 고유한 팩터리 (파생 호스트를 반환 하는 팩터리)를 제공할 수 있습니다.  
  
 기본 팩터리 대신 사용자 지정 서비스 호스트 팩터리를 사용 하려면 다음과 같이 [@ServiceHost](servicehost.md) 지시문에 형식 이름을 제공 하면 됩니다.  
  
```xml  
<% @ServiceHost Factory="DerivedFactory" Service="MyService" %>  
```  
  
 팩터리 구현을 가능하면 간단하게 유지합니다. 사용자 지정 논리가 많은 경우 팩터리 내부 대신 호스트 내부에 해당 로직을 배치하면 코드를 재사용할 수 있습니다.  
  
 예를 들어에 대해 `MyService`AJAX 사용 끝점을 사용 하도록 설정 하려면 다음 예제와 같이 [@ServiceHost](servicehost.md) 지시문에서 `Factory` 기본값 <xref:System.ServiceModel.Activation.ServiceHostFactory>대신 특성 값 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> 에 대해를 지정 합니다.  
  
## <a name="example"></a>예제  
  
```  
<% @ServiceHost   
Service="MyService"  
Language="C#"  
Debug="true"  
Factory="WebScriptServiceHostFactory"  
%>  
```  
  
## <a name="see-also"></a>참고자료

- [사용자 지정 서비스 호스트](../../../wcf/samples/custom-service-host.md)
