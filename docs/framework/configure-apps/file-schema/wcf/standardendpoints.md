---
title: <standardEndpoints>
ms.date: 03/30/2017
ms.assetid: d62153d7-a6e6-462a-a784-cca61e9c2ba1
ms.openlocfilehash: 76a5303650c4e2b2887d29f511d3088c78b58fe2
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399507"
---
# <a name="standardendpoints"></a>\<standardEndpoints>
이 구성 섹션에서는 다시 사용할 수 있는 미리 구성된 엔드포인트인 표준 엔드포인트의 컬렉션을 정의할 수 있습니다. 표준 엔드포인트에는 고정 값으로 설정된 하나 이상의 주소, 바인딩 및 계약 특성이 있습니다. 예를 들어 검색 엔드포인트에서는 계약이 고정됩니다. 표준 엔드포인트를 사용자 지정 바인딩 정의와 유사한 새 속성과 함께 사용하여 서비스 엔드포인트를 확장할 수도 있습니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<standardEndpoints >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.serviceModel>
  <standardEndpoints>
  </standardEndpoints>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
 없음  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<announcementEndpoint>](announcementendpoint.md)|고정 알림 계약이 있는 표준 엔드포인트를 정의합니다. 서비스에서는 선택적으로 서비스가 열리거나 닫힐 때 각각 온라인 및 오프라인 알림 메시지를 보내 가용성을 알릴 수 있습니다. WCF (Windows Communication Foundation) 서비스는 [ \<servicediscovery >](servicediscovery.md) 요소에서 알림 끝점을 지정 하 고 AnnouncementClient를 사용 하 여 공지를 수행 합니다. 다른 서비스에서 알림을 수신 대기 하려는 클라이언트는 실제로 WCF 서비스 역할을 합니다. 따라서 [ \<서비스 >](services.md) 섹션에서 해당 클라이언트에 대 한 알림 끝점을 구성 해야 합니다.|  
|[\<discoveryEndpoint>](discoveryendpoint.md)|고정 검색 계약이 있는 표준 엔드포인트를 정의합니다. 서비스 구성에 추가되면 검색 메시지를 수신하는 위치를 지정합니다. 클라이언트 구성에 추가되면 검색 쿼리를 보내는 위치를 지정합니다.|  
|[\<dynamicEndpoint>](dynamicendpoint.md)|이 구성 요소는 애플리케이션이 런타임에 엔드포인트 주소를 동적으로 찾을 수 있는 클라이언트 프로그램으로 기능하도록 설정하기 위한 정보를 포함하는 표준 엔드포인트를 정의합니다.|  
|[\<mexEndpoint>](mexendpoint.md)|고정 IMetadataExchange 계약이 있는 표준 엔드포인트를 정의합니다. 모든 메타데이터 교환 엔드포인트가 IMetadataExchange를 계약으로 지정하므로 고유의 엔드포인트를 정의하는 대신 이 표준 지점을 사용할 수 있습니다.|  
|[\<udpAnnouncementEndpoint>](udpannouncementendpoint.md)|서비스에서 UDP 바인딩을 통해 알림 메시지를 보내는 데 사용하는 표준 엔드포인트를 정의합니다. 고정된 계약이 있으며 두 가지 버전의 검색을 지원합니다. 또한 WS-Discovery 사양(WS-Discovery April 2005 또는 WS-Discovery 버전 1.1)에 지정된 고정된 UDP 바인딩 및 기본 주소 값이 있습니다. 알림 메시지를 보내고 받는 데 사용할 멀티캐스트 주소를 지정할 수 있습니다.|  
|[\<udpDiscoveryEndpoint>](udpdiscoveryendpoint.md)|UDP 멀티캐스트 바인딩을 통한 검색 작업에 대해 미리 구성된 표준 엔드포인트를 정의합니다. 이 엔드포인트에는 고정된 계약이 있으며 두 가지 버전의 WS-Discovery 프로토콜을 지원합니다. 또한 WS-Discovery 사양(WS-Discovery April 2005 또는 WS-Discovery V1.1)에 지정된 고정된 UDP 바인딩 및 기본 주소가 있습니다.|  
|[\<webHttpEndpoint>](webhttpendpoint.md)|Webhttp > 동작을 자동으로 [ \<](webhttpbinding.md) 추가 [하는 고정 된 webHttpBinding > 바인딩을 사용 하 여 표준 끝점을 정의 합니다. \<](webhttp.md) REST 서비스를 작성할 때는 이 엔드포인트를 사용합니다.|  
|[\<webScriptEndpoint>](webscriptendpoint.md)|EnableWebScript > 동작을 자동으로 추가 [하는 고정 \<된 webHttpBinding >](webhttpbinding.md) 바인딩을 사용 하 여 표준 끝점을 정의 합니다. [ \<](enablewebscript.md) ASP.NET AJAX 애플리케이션에서 호출되는 서비스를 기록할 때 이 엔드포인트를 사용합니다.|  
|[\<workflowControlEndpoint>](workflowcontrolendpoint.md)|워크플로 인스턴스의 실행(만들기, 실행, 일시 중단, 종료 등)을 제어하기 위한 표준 엔드포인트를 정의합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|\<system.ServiceModel>|모든 WCF 구성 요소의 루트 요소입니다.|  
  
## <a name="see-also"></a>참고자료

- [표준 엔드포인트](../../../wcf/feature-details/standard-endpoints.md)
