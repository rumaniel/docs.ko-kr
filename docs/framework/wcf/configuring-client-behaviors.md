---
title: 클라이언트 동작 구성
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: df5b32fa-e73b-4e8e-b66f-357c748e0173
ms.openlocfilehash: 83fdc77bd17115f9952f2ca6c494ed0eb873cd9c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61608777"
---
# <a name="configuring-client-behaviors"></a>클라이언트 동작 구성
두 가지 방법으로 동작을 구성 하는 Windows Communication Foundation (WCF):에 정의 된 동작 구성을 참조 하거나는 `<behavior>` 또는 프로그래밍 방식으로 호출을 클라이언트 응용 프로그램 구성 파일의 섹션 응용 프로그램입니다. 이 항목에서는 두 접근 방식 모두에 대해 설명합니다.  
  
 구성 파일을 사용할 경우 동작 구성은 구성 설정의 명명된 컬렉션입니다. 각 동작 구성의 이름은 고유해야 합니다. 이 문자열은 엔드포인트를 동작에 연결하는 엔드포인트 구성의 `behaviorConfiguration` 특성에 사용됩니다.  
  
## <a name="example"></a>예제  
 다음 구성 코드에서는 `myBehavior`라는 동작을 정의합니다. 클라이언트 엔드포인트는 `behaviorConfiguration` 특성에서 이 동작을 참조합니다.  
  
```xml  
<configuration>  
    <system.serviceModel>  
        <behaviors>  
            <endpointBehaviors>  
                <behavior name="myBehavior">  
                    <clientVia />  
                </behavior>  
            </endpointBehaviors>  
        </behaviors>  
        <bindings>  
            <basicHttpBinding>  
                <binding name="myBinding" maxReceivedMessageSize="10000" />  
            </basicHttpBinding>  
        </bindings>  
        <client>  
            <endpoint address="myAddress" binding="basicHttpBinding" bindingConfiguration="myBinding" behaviorConfiguration="myBehavior" contract="myContract" />  
        </client>  
    </system.serviceModel>  
</configuration>  
```  
  
## <a name="using-behaviors-programmatically"></a>프로그래밍 방식으로 동작 사용  
 또한 구성 하거나 적절 한 배치 하 여 동작을 프로그래밍 방식으로 삽입 `Behaviors` Windows Communication Foundation (WCF) 클라이언트 개체 또는 클라이언트를 열기 전에 클라이언트 채널 팩터리 개체의 속성입니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 채널 개체를 만들기 전에 <xref:System.ServiceModel.Description.ServiceEndpoint.Behaviors%2A> 속성에서 반환된 <xref:System.ServiceModel.Description.ServiceEndpoint>의 <xref:System.ServiceModel.ChannelFactory.Endpoint%2A> 속성에 액세스하여 프로그래밍 방식으로 동작을 삽입하는 방법을 보여 줍니다.  
  
 [!code-csharp[ChannelFactoryBehaviors#10](../../../samples/snippets/csharp/VS_Snippets_CFX/channelfactorybehaviors/cs/client.cs#10)]
 [!code-vb[ChannelFactoryBehaviors#10](../../../samples/snippets/visualbasic/VS_Snippets_CFX/channelfactorybehaviors/vb/client.vb#10)]  
  
## <a name="see-also"></a>참고자료

- [\<behaviors>](../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md)
