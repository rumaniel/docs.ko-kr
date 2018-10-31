---
title: 구성 파일을 사용하여 서비스 구성
ms.date: 03/30/2017
helpviewer_keywords:
- configuring services [WCF]
ms.assetid: c9c8cd32-2c9d-4541-ad0d-16dff6bd2a00
ms.openlocfilehash: 11d24bec46cfb190fe1a7c2a7b9ac78ac4d5e799
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50200864"
---
# <a name="configuring-services-using-configuration-files"></a>구성 파일을 사용하여 서비스 구성
디자인 타임에 대신 배포 지점에서 서비스 동작 데이터 및 끝점을 제공 하는 유연성을 제공 구성 파일을 사용 하 여 Windows Communication Foundation (WCF) 서비스를 구성 합니다. 이 항목에서는 사용할 수 있는 기본 기술에 대해 간략하게 설명합니다.  
  
 WCF 서비스를 구성할 수 있습니다는 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 기술 구성 합니다. 가장 일반적으로 XML 요소는 WCF 서비스를 호스팅하는 인터넷 정보 서비스 (IIS) 사이트의 Web.config 파일에 추가 됩니다. 이 요소를 사용하여 엔드포인트 주소(서비스와의 통신에 사용되는 실제 주소)와 같은 세부 사항을 컴퓨터별로 변경할 수 있습니다. 또한 WCF 서비스에 대 한 가장 기본적인 기능을 신속 하 게 선택할 수 있도록 하는 여러 시스템 제공 요소가 포함 되어 있습니다. 부터 [!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)], WCF WCF 구성 요구 사항을 간소화 하는 새로운 기본 구성 모델이 함께 제공 됩니다. 모든 WCF 구성 특정 서비스를 제공 하지 않으면 런타임이 일부 표준 끝점 및 기본 바인딩/동작을 사용 하 여 서비스 자동으로 구성 합니다. 실제로 구성 작성은 주요 WCF 응용 프로그램 프로그래밍의 일부입니다.  
  
 자세한 내용은 [서비스에 대 한 바인딩을 구성](../../../docs/framework/wcf/configuring-bindings-for-wcf-services.md)합니다. 가장 목록 요소에 일반적으로 사용 되는, 참조 [System-Provided Bindings](../../../docs/framework/wcf/system-provided-bindings.md)합니다. 기본 엔드포인트, 바인딩 및 동작에 대한 자세한 내용은 [단순화된 구성](../../../docs/framework/wcf/simplified-configuration.md) 및 [WCF 서비스를 위한 단순화된 구성](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)을 참조하세요.  
  
> [!IMPORTANT]
>  서로 다른 두 버전의 서비스가 배포되는 병렬 배포 시나리오에서는 구성 파일에서 참조되는 어셈블리의 부분 이름을 지정해야 합니다. 이는 구성 파일이 모든 버전의 서비스에서 공유되며 이러한 서비스가 여러 가지 버전의 .NET Framework에서 실행될 수 있기 때문입니다.  
  
## <a name="systemconfiguration-webconfig-and-appconfig"></a>System.Configuration: Web.config 및 App.config  
 WCF의 System.Configuration 구성 시스템을 사용 하 여 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]입니다.  
  
 Visual Studio에서 서비스를 구성할 때 설정을 지정 하는 web.config 또는 App.config 파일을 사용 합니다. 구성 파일 이름은 서비스에 대해 선택한 호스팅 환경에 따라 결정됩니다. IIS를 사용하여 서비스를 호스트하는 경우에는 Web.config 파일을 사용합니다. 다른 호스팅 환경을 사용하는 경우에는 App.config 파일을 사용합니다.  
  
 Visual Studio에서 App.config 라는 파일은 최종 구성 파일을 만드는 사용 됩니다. 구성에 사용되는 최종 이름은 어셈블리 이름에 따라 달라집니다. 예를 들어, "Cohowinery.exe"라는 어셈블리에는 "Cohowinery.exe.config"의 최종 구성 파일 이름이 포함됩니다. 그러나 App.config 파일만 수정하면 됩니다. 이 파일의 변경 내용은 컴파일 타임에 최종 응용 프로그램 구성 파일에 자동으로 적용됩니다.  
  
 App.config 파일 사용 시 응용 프로그램이 시작되고 구성이 적용되면 구성 시스템에서는 App.config 파일을 Machine.config 파일의 내용과 병합합니다. 이 메커니즘을 통해 시스템 수준의 설정이 Machine.config 파일에 정의됩니다. App.config 파일을 사용하여 Machine.config 파일의 설정을 재정의할 수 있습니다. 또한 Machine.config 파일의 설정이 사용되도록 해당 설정을 잠글 수 있습니다. Web.config의 경우 구성 시스템에서는 응용 프로그램 디렉터리에 이르는 모든 디렉터리의 Web.config 파일을 적용된 구성에 병합합니다. 구성과 설정의 우선 순위에 대 한 자세한 내용은 항목을 참조 합니다 <xref:System.Configuration> 네임 스페이스입니다.  
  
## <a name="major-sections-of-the-configuration-file"></a>구성 파일의 주요 섹션  
 구성 파일의 주요 섹션에는 다음 요소가 포함됩니다.  
  
```xml  
<system.ServiceModel>  
  
   <services>  
   <!—- Define the service endpoints. This section is optional in the new  
    default configuration model in .NET Framework 4. -->  
      <service>  
         <endpoint/>  
      </service>  
   </services>  
  
   <bindings>  
   <!-- Specify one or more of the system-provided binding elements,  
    for example, <basicHttpBinding> -->   
   <!-- Alternatively, <customBinding> elements. -->  
      <binding>  
      <!-- For example, a <BasicHttpBinding> element. -->  
      </binding>  
   </bindings>  
  
   <behaviors>  
   <!-- One or more of the system-provided or custom behavior elements. -->  
      <behavior>  
      <!-- For example, a <throttling> element. -->  
      </behavior>  
   </behaviors>  
  
</system.ServiceModel>  
```  
  
> [!NOTE]
>  바인딩 및 동작 섹션은 선택 사항이며 필요 시에만 포함됩니다.  
  
### <a name="the-services-element"></a>\<서비스 > 요소  
 `services` 요소에는 응용 프로그램에서 호스트하는 모든 서비스에 대한 사양이 포함됩니다. [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]의 간소화된 구성 모델부터 이 섹션은 선택 사항입니다.  
  
 [\<services>](../../../docs/framework/configure-apps/file-schema/wcf/services.md)  
  
### <a name="the-service-element"></a>\<서비스 > 요소  
 각 서비스에는 다음 특성이 있습니다.  
  
-   `name`. 서비스 계약의 구현을 제공하는 형식을 지정합니다. 네임스페이스, 마침표, 형식 이름순으로 구성되는 정규화된 이름입니다. 예를 들면 `"MyNameSpace.myServiceType"`과 같습니다.  
  
-   `behaviorConfiguration`. `behavior` 요소에 있는 `behaviors` 요소 중 하나의 이름을 지정합니다. 지정한 동작은 서비스에서 가장을 허용할지 여부와 같은 작업을 제어합니다. 해당 값이 빈 이름이거나 `behaviorConfiguration` 이 제공되지 않으면 기본 서비스 동작 집합이 서비스에 추가됩니다.  
  
-   [\<service>](../../../docs/framework/configure-apps/file-schema/wcf/service.md)  
  
### <a name="the-endpoint-element"></a>\<끝점 > 요소  
 각 엔드포인트에는 다음 특성으로 표시되는 주소, 바인딩 및 계약이 필요합니다.  
  
-   `address`. 절대 주소이거나 서비스의 기본 주소에 대한 상대 주소일 수 있는 서비스의 URI(Uniform Resource Identifier)를 지정합니다. 이 특성이 빈 문자열로 설정되면 서비스에 <xref:System.ServiceModel.ServiceHost>를 만들 때 지정되는 기본 주소에서 엔드포인트를 사용할 수 있음을 나타냅니다.  
  
-   `binding`. 일반적으로 <xref:System.ServiceModel.WSHttpBinding>과 같은 시스템 제공 바인딩을 지정하지만 사용자 정의 바인딩을 지정할 수도 있습니다. 지정된 바인딩에 따라 전송 형식, 사용된 보안 및 인코딩 그리고 신뢰할 수 있는 세션, 트랜잭션 또는 스트리밍을 지원하거나 사용할 수 있는지 여부를 확인합니다.  
  
-   `bindingConfiguration`. 바인딩의 기본값을 수정해야 하는 경우 `binding` 요소에서 해당 `bindings` 요소를 구성하여 수행할 수 있습니다. 이 특성에는 기본값을 변경하는 데 사용되는 `name` 요소의 `binding` 특성과 동일한 값을 지정해야 합니다. 이름을 지정하지 않거나 바인딩에서 `bindingConfiguration`을 지정하지 않으면 바인딩 형식의 기본 바인딩이 엔드포인트에 사용됩니다.  
  
-   `contract`. 계약을 정의하는 인터페이스를 지정합니다. 이 특성은 `name` 요소의 `service` 특성으로 지정된 CLR(공통 언어 런타임)에 구현된 인터페이스입니다.  
  
-   [\<끝점 > 요소 참조](https://msdn.microsoft.com/library/13aa23b7-2f08-4add-8dbf-a99f8127c017)  
  
### <a name="the-bindings-element"></a>\<바인딩 > 요소  
 `bindings` 요소에는 서비스에 정의된 엔드포인트에서 사용할 수 있는 모든 바인딩에 대한 사양이 포함됩니다.  
  
 [\<bindings>](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)  
  
### <a name="the-binding-element"></a>\<바인딩 > 요소  
 합니다 `binding` 에 포함 된 요소를 `bindings` 요소에는 시스템 제공 바인딩 중 하나가 될 수 있습니다 (참조 [System-Provided Bindings](../../../docs/framework/wcf/system-provided-bindings.md)) 또는 사용자 지정 바인딩을 (참조 [사용자 지정 바인딩을](../../../docs/framework/wcf/extending/custom-bindings.md)). `binding` 요소에는 `name` 요소의 `bindingConfiguration` 특성에 지정된 엔드포인트와 바인딩을 연관시키는 `endpoint` 특성이 있습니다. 이름을 지정하지 않는 경우 이 바인딩은 해당 바인딩 형식의 기본값에 해당합니다.  
  
 서비스 및 클라이언트를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [Windows Communication Foundation 응용 프로그램 구성](https://msdn.microsoft.com/library/13cb368e-88d4-4c61-8eed-2af0361c6d7a)합니다.  
  
 [\<binding>](../../../docs/framework/misc/binding.md)  
  
### <a name="the-behaviors-element"></a>\<동작 > 요소  
 서비스의 동작을 정의하는 `behavior` 요소에 대한 컨테이너 요소입니다.  
  
 [\<동작 >](../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md)  
  
### <a name="the-behavior-element"></a>\<동작 > 요소  
 각 `behavior` 요소는 `name` 특성으로 식별되며 <`throttling`>과 같은 시스템 제공 동작이나 사용자 지정 동작을 제공합니다. 이름을 지정하지 않는 경우 이 동작 요소는 기본 서비스 또는 엔드포인트 동작에 해당합니다.  
  
 [\<동작 >](../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md)  
  
## <a name="how-to-use-binding-and-behavior-configurations"></a>바인딩 및 동작 구성 사용 방법  
 WCF 쉽게 참조 시스템을 사용 하 여 구성에서 끝점 간의 구성을 공유할 수 있습니다. 구성 값을 엔드포인트에 직접 할당하는 대신 바인딩 관련 구성 값은 `bindingConfiguration` 섹션의 `<binding>` 요소로 그룹화됩니다. 바인딩 구성은 바인딩에 대한 설정의 명명된 그룹입니다. 엔드포인트는 이름별로 `bindingConfiguration`을 참조할 수 있습니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
 <system.serviceModel>  
  <bindings>  
    <basicHttpBinding>  
     <binding name="myBindingConfiguration1" closeTimeout="00:01:00" />  
     <binding name="myBindingConfiguration2" closeTimeout="00:02:00" />  
     <binding closeTimeout="00:03:00" />  <!—- Default binding for basicHttpBinding -->  
    </basicHttpBinding>  
     </bindings>  
     <services>  
      <service name="MyNamespace.myServiceType">  
       <endpoint   
          address="myAddress" binding="basicHttpBinding"   
          bindingConfiguration="myBindingConfiguration1"  
          contract="MyContract"  />  
       <endpoint   
          address="myAddress2" binding="basicHttpBinding"   
          bindingConfiguration="myBindingConfiguration2"  
          contract="MyContract" />  
       <endpoint   
          address="myAddress3" binding="basicHttpBinding"   
          contract="MyContract" />  
       </service>  
      </services>  
    </system.serviceModel>  
</configuration>  
```  
  
 `name` 의 `bindingConfiguration` 은 `<binding>` 요소에 설정됩니다. 합니다 `name` 바인딩 형식 범위 내에서 고유한 문자열 이어야 합니다-이 경우에 [< basicHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md), 또는 기본 바인딩을 참조 하는 빈 값입니다. 엔드포인트는 `bindingConfiguration` 특성을 이 문자열에 설정하여 구성에 연결됩니다.  
  
 `behaviorConfiguration` 은 다음 샘플과 동일한 방식으로 구현됩니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="myBehavior">  
           <callbackDebug includeExceptionDetailInFaults="true" />  
         </behavior>  
      </endpointBehaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="true" />  
        </behavior>  
      </serviceBehaviors>  
  
    </behaviors>  
    <services>  
     <service name="NewServiceType">  
       <endpoint   
          address="myAddress3" behaviorConfiguration="myBehavior"  
          binding="basicHttpBinding"  
          contract="MyContract" />  
      </service>  
    </services>  
   </system.serviceModel>  
</configuration>  
```  
  
 기본 서비스 동작 집합이 서비스에 추가됩니다. 이 시스템에서는 설정을 다시 정의하지 않고 엔드포인트가 일반 구성을 공유할 수 있습니다. 시스템 수준의 범위가 필요하면 Machine.config에서 동작 구성 또는 바인딩을 만듭니다. 모든 App.config 파일에서 구성 설정을 사용할 수 있습니다. [Configuration Editor Tool (SvcConfigEditor.exe)](../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md) 를 사용하면 구성을 쉽게 만들 수 있습니다.  
  
## <a name="behavior-merge"></a>동작 병합  
 일반적인 동작의 집합을 지속적으로 사용하려는 경우 이 동작 병합 기능을 통해 동작을 더욱 쉽게 관리할 수 있습니다. 이 기능을 사용하면 여러 가지 수준의 구성 계층에서 동작을 지정하고 서비스가 여러 가지 수준의 구성 계층에서 동작을 상속하도록 할 수 있습니다. 이에 대한 동작 방식을 보여 주기 위해 IIS에서 다음과 같은 가상 디렉터리 레이아웃이 있다고 가정합니다.  
  
 `~\Web.config~\Service.svc~\Child\Web.config~\Child\Service.svc`
  
 및 `~\Web.config` 파일에 다음 내용을:  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceDebug includeExceptionDetailInFaults="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
 또한 ~\Child\Web.config에 있는 자식 Web.config의 내용은 다음과 같습니다.  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
 ~\Child\Service.svc에 있는 서비스는 serviceDebug 및 serviceMetadata 동작이 둘 다 있는 것처럼 동작합니다. ~\Service.svc에 있는 서비스에는 serviceDebug 동작만 있습니다. 결과적으로 동일한 이름(이 경우 빈 문자열)의 두 동작 컬렉션이 병합됩니다.  
  
 사용 하 여 동작 컬렉션을 지울 수도 있습니다는 \<지우기 > 태그를 사용 하 여 컬렉션에서 개별 동작을 제거할는 \<제거 > 태그입니다. 예를 들어 다음 두 구성을 사용하면 자식 서비스에 serviceMetadata 동작만 있게 됩니다.  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <remove name="serviceDebug"/>  
          <serviceMetadata httpGetEnabled="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <clear/>  
          <serviceMetadata httpGetEnabled="True" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
 동작 병합은 위에 나와 있는 것처럼 이름 없는 동작 컬렉션뿐만 아니라 명명된 동작 컬렉션에도 수행됩니다.  
  
 동작 병합은 IIS 호스팅 환경에서 수행되며 이 환경에서 Web.config 파일은 루트 Web.config 파일 및 machine.config와 계층적으로 병합됩니다. 그러나 응용 프로그램 환경에서도 동작 병합이 수행되며 이 환경에서는 machine.config가 App.config 파일과 병합될 수 있습니다.  
  
 동작 병합은 구성의 엔드포인트 동작과 서비스 동작에 모두 적용됩니다.  
  
 자식 동작 컬렉션에 부모 동작 컬렉션에 이미 있는 동작이 포함되어 있으면 자식 동작이 부모 동작을 재정의합니다. 부모 동작 컬렉션 만약 `<serviceMetadata httpGetEnabled="False" />` 자식 동작 컬렉션 했으며 `<serviceMetadata httpGetEnabled="True" />`자식 동작은 동작 컬렉션의 부모 동작을 재정의 하 고 httpGetEnabled는 "true"입니다.  
  
## <a name="see-also"></a>참고 항목  
 [단순화된 구성](../../../docs/framework/wcf/simplified-configuration.md)  
 [Windows Communication Foundation 응용 프로그램 구성](https://msdn.microsoft.com/library/13cb368e-88d4-4c61-8eed-2af0361c6d7a)  
 [\<service>](../../../docs/framework/configure-apps/file-schema/wcf/service.md)  
 [\<binding>](../../../docs/framework/misc/binding.md)
