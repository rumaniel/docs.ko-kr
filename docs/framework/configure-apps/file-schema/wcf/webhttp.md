---
title: <webHttp>
ms.date: 03/30/2017
ms.assetid: 1f9d0754-d41e-44ce-a298-e51cb3096c64
ms.openlocfilehash: 00644d248e6fb85d7cf712620e6ac74405e6b0c3
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399161"
---
# <a name="webhttp"></a>\<webHttp>
이 요소는 구성을 통해 엔드포인트에서 <xref:System.ServiceModel.Description.WebHttpBehavior>를 지정합니다. 이 동작은 [ \<webHttpBinding >](webhttpbinding.md) 표준 바인딩과 함께 사용 될 경우 WCF (Windows Communication Foundation) 서비스에 대 한 웹 프로그래밍 모델을 사용 하도록 설정 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<endpointBehaviors >** ](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<webHttp >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<webHttp />
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|automaticFormatSelectionEnabled|이 속성이 `true`로 설정되면 WCF 인프라가 사용할 가장 적절한 형식을 결정합니다. 기본적으로 자동 형식 선택은 이전 버전과의 호환성을 위해 사용되지 않습니다. 자동 형식 선택은 프로그래밍 방식이나 구성을 통해 사용하도록 설정할 수 있습니다.|  
|defaultBodyStyle|반환된 메시지의 기본 본문 스타일을 지정합니다. 자세한 내용은 및 <xref:System.ServiceModel.Web.WebMessageBodyStyle> [WCF 웹 HTTP 형식 지정](../../../wcf/feature-details/wcf-web-http-formatting.md)을 참조 하세요.|  
|defaultOutgoingResponseFormat|메시지의 나가는 기본 응답 형식을 지정합니다. 자세한 내용은 [WCF 웹 HTTP 형식 지정](../../../wcf/feature-details/wcf-web-http-formatting.md)을 참조 하세요.|  
|faultExceptionEnabled|내부 서버 오류(HTTP 상태 코드: 500)가 발생할 때 FaultException이 생성되는지 여부를 지정하는 플래그를 가져오거나 설정합니다.|  
|helpEnabled|도움말 페이지를 사용할 수 있는지 여부를 결정하는 값을 가져오거나 설정합니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|엔드포인트 동작 집합을 지정합니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.WebHttpElement>
- <xref:System.ServiceModel.Description.WebHttpBehavior>
- [AJAX 통합 및 JSON 지원](../../../wcf/feature-details/ajax-integration-and-json-support.md)
- [\<webHttpBinding>](webhttpbinding.md)
