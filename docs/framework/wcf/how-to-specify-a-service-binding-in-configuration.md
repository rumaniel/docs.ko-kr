---
title: '방법: 구성에서 서비스 바인딩 지정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 885037f7-1c2b-4d7a-90d9-06b89be172f2
ms.openlocfilehash: d3224b1d732fb82ffe68e8ce0bd410850004cb95
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69967162"
---
# <a name="how-to-specify-a-service-binding-in-configuration"></a>방법: 구성에서 서비스 바인딩 지정
이 예제에서 `ICalculator` 계약이 기본 계산기 서비스에 대해 정의되고, 서비스가 `CalculatorService` 클래스에 구현된 다음 해당 엔드포인트가 Web.config 파일에 구성됩니다. 여기서 서비스는 <xref:System.ServiceModel.BasicHttpBinding>을 사용하는 것으로 지정됩니다. 구성 대신 코드를 사용 하 여이 서비스를 구성 하는 방법에 대 한 [자세한 내용은 방법: 코드](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-code.md)에서 서비스 바인딩을 지정 합니다.  
  
 일반적으로 바인딩 및 주소 정보를 코드에서 명령적으로 지정하지 않고 구성에서 선언적으로 지정하는 것이 좋습니다. 일반적으로 배포된 서비스의 바인딩과 주소가 서비스를 배포할 때 사용된 바인딩 및 주소와 다르기 때문에 코드로 엔드포인트를 정의하는 것은 효과적이지 않습니다. 일반적으로 바인딩 및 주소 지정 정보를 코드와 구분하면 애플리케이션을 다시 컴파일하거나 다시 배포할 필요 없이 해당 정보를 변경할 수 있습니다.  
  
 [구성 편집기 도구 (SvcConfigEditor)](../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)를 사용 하 여 다음 구성 단계를 모두 수행할 수 있습니다.  
  
 이 예제의 소스 복사에 대해서는 [Basicbinding](../../../docs/framework/wcf/samples/basicbinding.md)을 참조 하세요.  
  
### <a name="to-specify-the-basichttpbinding-to-use-to-configure-the-service"></a>서비스를 구성하는 데 사용할 BasicHttpBinding을 지정하려면  
  
1. 서비스 유형에 대한 서비스 계약을 정의합니다.  
  
     [!code-csharp[C_HowTo_ConfigureServiceBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureservicebinding/cs/source.cs#1)]
     [!code-vb[C_HowTo_ConfigureServiceBinding#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_configureservicebinding/vb/source.vb#1)]  
  
2. 서비스 클래스에 서비스 계약을 구현합니다.  
  
     [!code-csharp[C_HowTo_ConfigureServiceBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureservicebinding/cs/source.cs#2)]
     [!code-vb[C_HowTo_ConfigureServiceBinding#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_configureservicebinding/vb/source.vb#2)]  
  
    > [!NOTE]
    > 주소 또는 바인딩 정보는 서비스 구현 내에 지정되지 않습니다. 또한 구성 파일에서 해당 정보를 가져오기 위해 코드를 쓰지 않아도 됩니다.  
  
3. Web.config 파일을 만들어 `CalculatorService`을 사용하는 <xref:System.ServiceModel.WSHttpBinding>에 대한 엔드포인트를 구성합니다.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.serviceModel>  
        <services>  
          <service name=" CalculatorService" >  
            <endpoint   
            <!-- Leave the address blank to be populated by default -->  
            <!-- from the hosting environment,in this case IIS, so -->  
            <!-- the address will just be that of the IIS Virtual -->  
            <!-- Directory. -->  
                address=""   
            <!-- Specify the binding type -->  
                binding="wsHttpBinding"  
            <!-- Specify the binding configuration name for that -->  
            <!-- binding type. This is optional but useful if you -->  
            <!-- want to modify the properties of the binding. -->  
            <!-- The bindingConfiguration name Binding1 is defined -->  
            <!-- below in the bindings element. -->  
                bindingConfiguration="Binding1"  
                contract="ICalculator" />  
          </service>  
        </services>  
        <bindings>  
          <wsHttpBinding>  
            <binding name="Binding1">  
              <!-- Binding property values can be modified here. -->  
              <!-- See the next procedure. -->  
            </binding>  
          </wsHttpBinding>  
       </bindings>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
4. 다음 줄이 포함된 Service.svc 파일을 만든 다음 IIS(인터넷 정보 서비스) 가상 디렉터리에 넣습니다.  
  
    ```  
    <%@ServiceHost language=c# Service="CalculatorService" %>   
    ```  
  
### <a name="to-modify-the-default-values-of-the-binding-properties"></a>바인딩 속성의 기본값을 수정하려면  
  
1. 의 <xref:System.ServiceModel.WSHttpBinding>기본 속성 값 중 하나를 수정 하려면 [ \<wsHttpBinding >](../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) 요소 내에 새 바인딩 구성 `<binding name="Binding1">` 이름을 만들고이 바인딩에서 바인딩의 특성에 대 한 새 값을 설정 합니다. 요소인. 예를 들어 기본 열기 및 닫기 시간 제한 값을 1분에서 2분으로 변경하려면 구성 파일에 다음을 추가합니다.  
  
    ```xml  
    <wsHttpBinding>  
      <binding name="Binding1"  
               closeTimeout="00:02:00"  
               openTimeout="00:02:00">  
      </binding>  
    </wsHttpBinding>  
    ```  
  
## <a name="see-also"></a>참고자료

- [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
- [엔드포인트 주소 지정](../../../docs/framework/wcf/specifying-an-endpoint-address.md)
