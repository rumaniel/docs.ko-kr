---
title: <system.serviceModel>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#system.ServiceModel
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.ServiceModel
helpviewer_keywords:
- <system.serviceModel> element
- system.serviceModel element
ms.assetid: 78519531-ad7a-40d3-b3e7-42f1103d8854
ms.openlocfilehash: 2125ce00b0e23f2e93ff251549f9c1276892b16b
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399450"
---
# <a name="systemservicemodel"></a>\<system.serviceModel>
이 구성 섹션에는 WCF (Windows Communication Foundation) ServiceModel 구성 요소가 모두 포함 되어 있습니다.  

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp; **\<System.servicemodel >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.serviceModel>
  <behaviors>
  </behaviors>
  <bindings>
  </bindings>
  <client>
  </client>
  <comContracts>
  </comContracts>
  <commonBehaviors>
  </commonBehaviors>
  <diagnostics>
  </diagnostics>
  <extensions>
  </extensions>
  <protocolMapping>
  </protocolMapping>
  <routing>
  </routing>
  <serviceHostingEnvironment>
  </serviceHostingEnvironment>
  <services>
  </services>
  <standardEndpoints>
  </standardEndpoints>
  <tracking>
  </tracking>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
 없음  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<behaviors>](behaviors.md)|이 섹션은 두 자식 컬렉션 `endpointBehaviors` 및 `serviceBehaviors`를 정의합니다.  각 컬렉션은 엔드포인트 및 서비스가 사용하는 동작 요소를 각각 정의합니다. 각 동작 요소는 고유한 `name` 특성으로 식별됩니다.|  
|[\<bindings>](bindings.md)|이 섹션에는 표준 및 사용자 지정 바인딩 컬렉션이 포함됩니다. 각 항목은 고유한 `name`으로 식별됩니다. 서비스에서는 `name`을 통해 바인딩을 연결하여 바인딩을 사용합니다.|  
|[\<client>](client.md)|이 섹션에는 클라이언트가 서비스에 연결하는 데 사용하는 엔드포인트의 목록이 포함됩니다.|  
|[\<comContracts>](comcontracts.md)|이 섹션은 WCF 및 COM interop에 사용하도록 설정된 COM 계약을 정의합니다.|  
|[\<commonBehaviors>](commonbehaviors.md)|이 섹션은 machine.config 파일에서만 정의할 수 있습니다. 이 섹션은 두 자식 컬렉션 `endpointBehaviors` 및 `serviceBehaviors`를 정의합니다.  각 컬렉션은 컴퓨터의 모든 WCF 끝점과 서비스에서 사용 하는 동작 요소를 각각 정의 합니다.  동작이 및 `<commonBehaviors>` `<behaviors>` 섹션 모두에서 정의 되는 경우 동작 > 섹션의 \<동작이 우선 합니다.|  
|[\<diagnostics>](diagnostics.md)|이 섹션에는 WCF의 진단 기능에 대한 설정이 포함됩니다. 사용자는 추적, 성능 카운터 및 WMI 공급자를 사용하거나 사용하지 않도록 설정하고 사용자 지정 메시지 필터를 추가할 수 있습니다.|  
|[\<extensions>](extensions-section.md)|이 섹션에는 사용자 정의 바인딩, 동작 및 확장의 기타 측면을 만들 수 있도록 하는 확장명 컬렉션이 포함됩니다.|  
|[\<protocolMapping>](protocolmapping.md)|이 섹션에서는 전송 프로토콜 체계 (예: http, net.tcp, net.pipe 등)와 WCF 바인딩 간의 기본 프로토콜 매핑 집합을 정의 합니다.|  
|[\<routing>](routing.md)|이 섹션에서는 들어오는 메시지를 평가할 때 사용할 WCF (Windows Communication Foundation 형식)<xref:System.ServiceModel.Dispatcher.MessageFilter> 와 메시지를 보낼 대상 끝점을 정의 하는 라우팅 테이블을 결정 하는 라우팅 필터 집합을 정의 합니다. 필터 일치.|  
|[\<serviceHostingEnvironment>](servicehostingenvironment.md)|이 섹션은 특정 전송을 위해 서비스 호스팅 환경에서 인스턴스화하는 형식을 정의합니다. 이 섹션이 비어 있으면 기본 형식이 사용됩니다.|  
|[\<services>](services.md)|이 섹션에는 서비스의 컬렉션이 포함됩니다. 이 요소에는 어셈블리에 정의된 서비스별로 서비스의 설정을 지정하는 `service` 요소가 포함됩니다.|  
|[\<standardEndpoints>](standardendpoints.md)|이 섹션은 다시 사용할 수 있는 미리 구성된 엔드포인트인 표준 엔드포인트의 컬렉션을 정의합니다. 표준 엔드포인트에는 고정 값으로 설정된 하나 이상의 주소, 바인딩 및 계약 특성이 있습니다. 예를 들어 검색 엔드포인트에서는 계약이 고정됩니다. 표준 엔드포인트를 사용자 지정 바인딩 정의와 유사한 새 속성과 함께 사용하여 서비스 엔드포인트를 확장할 수도 있습니다.|
|[\<tracking>](tracking-of-wcf.md)|이 섹션에서는 워크플로 서비스에 대 한 추적 설정을 정의 합니다.|

### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|\<configuration>|.NET 구성 파일에 있는 모든 구성 요소의 루트 요소입니다.|  
  
## <a name="remarks"></a>설명  
 WCF는 다른 제품의 구성 섹션에 요소를 추가 하지 않습니다.  
  
 WCF 서비스는 구성 파일의 `services` 섹션에 정의 되어 있습니다. 어셈블리에는 여러 개의 서비스가 포함될 수 있습니다. 서비스별로 해당 `service` 구성 섹션이 있습니다. 해당 단원 및 내용에서는 특정 서비스의 서비스 계약, 동작 및 엔드포인트를 정의합니다.  
  
 서비스의 `name` 특성만 필수입니다.  기본적으로 서비스 이름은 서비스를 구현하는 데 사용되는 기본 CLR 형식을 설명하지만 <xref:System.ServiceModel.ServiceContractAttribute>에서 ConfigurationName 속성을 변경하여 CLR 형식 요구 사항을 재정의할 수 있습니다.  
  
 `behaviorConfiguration` 특성은 선택 사항이며 이 특성은 서비스에 사용되는 서비스 동작을 식별합니다. 이 특성에 지정된 동작은 동일한 파일이나 부모 파일과 같은 동일한 구성 파일의 범위에 정의된 서비스 동작에 연결되어야 합니다.  
  
 각 서비스는 `endpoint` 요소에 정의된 하나 이상의 엔드포인트를 노출합니다. 각 엔드포인트에는 고유한 주소와 바인딩이 있습니다. 구성 파일 내에서 사용되는 모든 바인딩은 파일 범위 내에서 정의되어야 합니다.  
  
 바인딩은 `name` 및 `bindingConfiguration` 특성을 조합하여 엔드포인트에 연결됩니다. `binding` 특성은 바인딩이 정의된 섹션을 정의합니다. `bindingConfiguration` 특성은 바인딩 섹션에서 사용되는 구성된 바인딩을 정의합니다. 바인딩 섹션에서는 여러 개의 구성된 바인딩을 정의할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음은 WCF 구성 파일의 예제입니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.serviceModel>
    <behaviors>
      <!-- List of Behaviors -->
    </behaviors>
    <client>
      <!-- List of Endpoints -->
    </client>
    <diagnostics wmiProviderEnabled="false"
                 performanceCountersEnabled="false"
                 tracingEnabled="false">
    </diagnostics>
    <serviceHostingEnvironment>
      <!-- List of entries -->
    </serviceHostingEnvironment>
    <comContracts>
      <!-- List of COM+ Contracts -->
    </comContracts>
    <services>
      <!-- List of Services -->
    </services>
    <bindings>
      <!-- List of Bindings -->
    </bindings>
  </system.serviceModel>
</configuration>
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.ServiceModelSectionGroup>
