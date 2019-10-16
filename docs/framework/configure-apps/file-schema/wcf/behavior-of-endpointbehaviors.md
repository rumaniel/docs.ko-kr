---
title: <endpointBehaviors>의 <behavior>
ms.date: 03/30/2017
ms.assetid: b90ca3bc-3c22-4174-b903-e3a39898bd27
ms.openlocfilehash: 81c9ec7bd82fa0b947e438632b293ab9110067f5
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70398235"
---
# <a name="behavior-of-endpointbehaviors"></a>\<endpointbehaviors의 \<동작 > >
`behavior` 요소는 엔드포인트의 동작에 대한 설정 컬렉션을 포함합니다. 각 동작은 해당 `name`으로 인덱싱됩니다. 엔드포인트는 이 이름을 통해 각 동작에 연결할 수 있습니다. [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)]부터는 바인딩 및 동작에 이름이 필요하지 않습니다. 기본 구성 및 이름이 없는 바인딩 및 동작에 대 한 자세한 내용은 [WCF 서비스에 대 한](../../../wcf/samples/simplified-configuration-for-wcf-services.md) [간소화 된 구성](../../../wcf/simplified-configuration.md) 및 단순화 된 구성을 참조 하세요.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<endpointBehaviors >** ](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<동작 >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.ServiceModel>
  <behaviors>
    <endpointBehaviors>
      <behavior name="String" />
    </endpointBehaviors>
  </behaviors>
</system.ServiceModel>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|name|동작의 구성 이름을 포함하는 고유 문자열입니다. 이 값은 요소의 식별 문자열 역할을 하므로 고유한 사용자 정의 문자열이어야 합니다. [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)]부터는 바인딩 및 동작에 이름이 필요하지 않습니다. 기본 구성 및 이름이 없는 바인딩 및 동작에 대 한 자세한 내용은 [WCF 서비스에 대 한](../../../wcf/samples/simplified-configuration-for-wcf-services.md) [간소화 된 구성](../../../wcf/simplified-configuration.md) 및 단순화 된 구성을 참조 하세요.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<clientCredentials>](clientcredentials.md)|클라이언트를 서비스에 인증하는 데 사용되는 자격 증명을 지정합니다.|  
|[\<callbackDebug>](callbackdebug.md)|WCF (Windows Communication Foundation) 콜백 개체에 대 한 서비스 디버깅을 지정 합니다.|  
|[\<callbackTimeouts>](callbacktimeouts.md)|클라이언트 콜백에 대한 제한 시간을 지정합니다.|  
|[\<clientVia>](clientvia.md)|메시지가 이동할 경로를 지정합니다.|  
|[\<dataContractSerializer>](datacontractserializer.md)|DataContractSerializer에 대한 구성 데이터가 들어 있습니다.|  
|[\<dispatcherSynchronization>](dispatchersynchronization.md)|서비스에서 응답을 비동기적으로 보낼 수 있도록 하는 엔드포인트 동작을 지정합니다.|  
|[\<enableWebScript>](enablewebscript.md)|ASP.NET AJAX 웹 페이지에서 서비스를 사용할 수 있게 하는 엔드포인트 동작을 설정합니다. 동작은 \<webHttpBinding > 표준 바인딩과 \<webMessageEncoding > binding 요소 중 하 나와 함께 사용 해야 합니다.|  
|[\<endpointDiscovery>](endpointdiscovery.md)|검색 기능, 범위 및 해당 메타데이터에 대한 사용자 지정 확장 등 엔드포인트에 대한 다양한 검색 설정을 지정합니다.|  
|[\<soapProcessing>](soapprocessing.md)|서로 다른 바인딩 형식과 메시지 버전 간에 메시지 마샬링을 위해 사용되는 클라이언트 엔드포인트 동작을 정의합니다.|  
|[\<synchronousReceive>](synchronousreceive-element.md)|서비스 또는 클라이언트 애플리케이션에서 메시지 수신을 위한 런타임 동작을 지정합니다. 이 구성 요소에는 특성이나 자식 요소가 없습니다.|  
|[\<transactedBatching>](transactedbatching.md)|받기 작업에 트랜잭션 일괄 처리가 지원되는지 여부를 지정합니다.|  
|[\<webHttp>](webhttp.md)|구성을 통해 엔드포인트에서 WebHttpBehavior를 지정합니다. 이 동작은 \<webHttpBinding > 표준 바인딩과 함께 사용 될 경우 WCF 서비스에 대해 웹 프로그래밍 모델을 사용 하도록 설정 합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<endpointBehaviors>](endpointbehaviors.md)|엔드포인트 동작 요소의 컬렉션입니다.|
