---
title: <serviceDebug>
ms.date: 03/30/2017
ms.assetid: 6d7ea986-f232-49fe-842c-f934d9966889
ms.openlocfilehash: 4eb79cc91ef489501c4c8bb6311f240d855ed053
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399630"
---
# <a name="servicedebug"></a>\<serviceDebug>
WCF (Windows Communication Foundation) 서비스에 대 한 디버깅 및 도움말 정보 기능을 지정 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<serviceBehaviors >** ](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<동작 >** ](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<serviceDebug >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<serviceDebug httpHelpPageBinding="String"
              httpHelpPageBindingConfiguration="String"
              httpHelpPageEnabled="Boolean"
              httpHelpPageUrl="Uri"
              httpsHelpPageBinding="String"
              httpsHelpPageBindingConfiguration="String"
              httpsHelpPageEnabled="Boolean"
              httpsHelpPageUrl="Uri"
              includeExceptionDetailInFaults="Boolean" />
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|httpHelpPageBinding|HTTP를 사용하여 서비스 도움말 페이지에 액세스할 때 사용할 바인딩 형식을 지정하는 문자열 값입니다.<br /><br /> <xref:System.ServiceModel.Channels.IReplyChannel?displayProperty=nameWithType>을 지원하는 내부 바인딩 요소가 있는 바인딩만 지원됩니다. 또한 바인딩의 <xref:System.ServiceModel.Channels.MessageVersion?displayProperty=nameWithType> 속성은 <xref:System.ServiceModel.Channels.MessageVersion.None?displayProperty=nameWithType>이어야 합니다.|  
|httpHelpPageBindingConfiguration|이 바인딩의 추가 구성 정보를 참조하는 `httpHelpPageBinding` 특성에 지정된 바인딩의 이름을 지정하는 문자열입니다. 이와 동일한 이름이 `<bindings>` 섹션에서 정의되어야 합니다.|  
|httpHelpPageEnabled|WCF가 `httpHelpPageUrl` 특성으로 지정 된 주소에 HTML 도움말 페이지를 게시할지 여부를 제어 하는 부울 값입니다. 기본값은 `true`입니다.<br /><br /> HTML 브라우저에 HTML 도움말 페이지가 게시되지 않게 하려면 이 속성을 `false`로 설정합니다.<br /><br /> `httpHelpPageUrl` 특성으로 지정된 위치에 HTML 도움말 페이지가 게시되게 하려면 이 특성을 `true`로 설정해야 합니다 또한 다음 조건 중 하나도 충족해야 합니다.<br /><br /> `httpHelpPageUrl` -특성은 HTTP 프로토콜 체계를 지 원하는 절대 주소입니다.<br />-HTTP 프로토콜 체계를 지 원하는 서비스의 기본 주소가 있습니다.<br /><br /> HTTP 프로토콜 체계를 지원하지 않는 절대 주소가 `httpHelpPageUrl` 특성에 지정되면 예외가 throw되지만, 앞의 조건을 모두 충족하지 않는 시나리오에서는 예외가 발생하지 않고 HTML 도움말 페이지도 생성되지 않습니다.|  
|httpHelpPageUrl|HTML 브라우저를 사용하여 엔드포인트를 볼 때 사용자에게 표시되는 사용자 지정 HTML 도움말 파일의 상대 또는 절대 HTTP 기반 URL을 지정하는 URI입니다.<br /><br /> 이 특성을 사용하면 HTML 브라우저 등의 HTTP/Get 요청으로부터 반환되는 사용자 지정 HTML 도움말 파일을 사용하도록 설정할 수 있습니다. HTML 도움말 파일의 위치는 다음과 같이 확인됩니다.<br /><br /> 1.  이 특성의 값이 상대 주소이면 HTML 도움말 파일의 위치는 HTTP 요청을 지원하는 서비스 기준 주소에 이 속성 값을 추가한 것입니다.<br />2.  이 특성의 값이 절대 주소이고 HTTP 요청을 지원할 경우 HTML 도움말 파일의 위치는 이 속성의 값입니다.<br />3.  이 특성의 값이 절대 주소이지만 HTTP 요청을 지원하지 않으면 예외가 throw됩니다.<br /><br /> 이 특성은 `httpHelpPageEnabled` 특성이 인 `true`경우에만 유효 합니다.|  
|httpsHelpPageBinding|HTTPS를 사용하여 서비스 도움말 페이지에 액세스할 때 사용할 바인딩 형식을 지정하는 문자열 값입니다.<br /><br /> <xref:System.ServiceModel.Channels.IReplyChannel>을 지원하는 내부 바인딩 요소가 있는 바인딩만 지원됩니다. 또한 바인딩의 <xref:System.ServiceModel.Channels.MessageVersion?displayProperty=nameWithType> 속성은 <xref:System.ServiceModel.Channels.MessageVersion.None?displayProperty=nameWithType>이어야 합니다.|  
|httpsHelpPageBindingConfiguration|이 바인딩의 추가 구성 정보를 참조하는 `httpsHelpPageBinding` 특성에 지정된 바인딩의 이름을 지정하는 문자열입니다. 이와 동일한 이름이 `<bindings>` 섹션에서 정의되어야 합니다.|  
|httpsHelpPageEnabled|WCF가 `httpsHelpPageUrl` 특성으로 지정 된 주소에 HTML 도움말 페이지를 게시할지 여부를 제어 하는 부울 값입니다. 기본값은 `true`입니다.<br /><br /> HTML 브라우저에 HTML 도움말 페이지가 게시되지 않게 하려면 이 속성을 `false`로 설정합니다.<br /><br /> `httpsHelpPageUrl` 특성으로 지정된 위치에 HTML 도움말 페이지가 게시되게 하려면 이 특성을 `true`로 설정해야 합니다 또한 다음 조건 중 하나도 충족해야 합니다.<br /><br /> `httpsHelpPageUrl` -특성은 HTTPS 프로토콜 체계를 지 원하는 절대 주소입니다.<br />-HTTPS 프로토콜 체계를 지 원하는 서비스의 기본 주소가 있습니다.<br /><br /> HTTPS 프로토콜 체계를 지원하지 않는 절대 주소가 `httpsHelpPageUrl` 특성에 지정되면 예외가 throw되지만, 앞의 조건을 모두 충족하지 않는 시나리오에서는 예외가 발생하지 않고 HTML 도움말 페이지도 생성되지 않습니다.|  
|httpsHelpPageUrl|HTML 브라우저를 사용하여 엔드포인트를 볼 때 사용자에게 표시되는 사용자 지정 HTML 도움말 파일의 상대 또는 절대 HTTPS 기반 URL을 지정하는 URI입니다.<br /><br /> 이 특성을 사용하면 HTML 브라우저 등의 HTTPS/Get 요청으로부터 반환되는 사용자 지정 HTML 도움말 파일을 사용하도록 설정할 수 있습니다. HTML 도움말 파일의 위치는 다음과 같이 확인됩니다.<br /><br /> -이 속성의 값이 상대 주소 이면 HTML 도움말 파일의 위치는 HTTPS 요청을 지 원하는 서비스 기본 주소와이 속성 값을 더한 값입니다.<br />-이 속성의 값이 절대 주소이 고 HTTPS 요청을 지 원하는 경우 HTML 도움말 파일의 위치는이 속성의 값입니다.<br />-이 속성의 값이 절대 이지만 HTTPS 요청을 지원 하지 않으면 예외가 throw 됩니다.<br /><br /> 이 특성은 `httpHelpPageEnabled` 특성이 인 `true`경우에만 유효 합니다.|  
|includeExceptionDetailInFaults|디버깅 목적으로 클라이언트에 반환되는 SOAP 오류의 세부 정보에 관리되는 예외 정보를 포함할지 여부를 지정하는 값입니다. 기본값은 `false`입니다.<br /><br /> 이 특성을 `true`로 설정한 경우 관리되는 예외 정보가 디버깅을 위해 클라이언트로 전달되게 하고, 웹 브라우저에서 서비스를 검색하는 사용자를 위해 HTML 정보 파일을 게시할 수 있습니다. **주의:**  관리되는 예외 정보를 클라이언트에 반환하면 보안상 위험할 수 있습니다. 예외 정보가 내부 서비스 구현 정보를 공개하여 권한 없는 클라이언트에서 이를 사용할 수 있기 때문입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|동작 요소를 지정합니다.|  
  
## <a name="remarks"></a>설명  
 로 `includeExceptionDetailInFaults` <xref:System.ServiceModel.FaultContractAttribute>설정 하면 서비스가를 사용 하 여 선언 되지 않은 경우에도 응용 프로그램 코드에 의해 throw 되는 모든 예외가 반환 됩니다. `true` 이 설정은 서버가 예기치 않은 예외를 throw하는 경우를 디버깅할 때 유용합니다. 이 특성을 사용하면 알 수 없는 예외가 serialize된 형태로 반환되어 예외를 보다 자세하게 검토할 수 있습니다.  
  
> [!CAUTION]
> 관리되는 예외 정보를 클라이언트에 반환하면 예외 정보가 내부 서비스 구현 정보를 노출하여 권한이 없는 클라이언트에서 사용할 수 있으므로 보안상 위험할 수 있습니다. 보안 문제로 인해 제어된 디버깅 시나리오에서만 이 작업을 수행하는 것이 좋습니다. 애플리케이션을 배포할 때는 `includeExceptionDetailInFaults`를 `false`로 설정해야 합니다.  
  
 관리 되는 예외와 관련 된 보안 문제에 대 한 자세한 내용은 [계약 및 서비스에서 오류 지정 및 처리](../../../wcf/specifying-and-handling-faults-in-contracts-and-services.md)를 참조 하세요. 코드 샘플은 [서비스 디버그 동작](../../../wcf/samples/service-debug-behavior.md)을 참조 하세요.  
  
 또한 `httpsHelpPageEnabled` 및 `httpsHelpPageUrl`을 설정하여 도움말 페이지를 사용하거나 사용하지 않도록 설정할 수 있습니다. 각 서비스는 서비스의 WSDL을 가져오기 위한 엔드포인트를 비롯하여 서비스에 대한 정보를 포함하는 도움말 페이지를 선택적으로 노출할 수 있습니다. 이는 `httpHelpPageEnabled`를 `true`로 설정하여 활성화할 수 있습니다. 이렇게 하면 서비스의 기본 주소에 대한 GET 요청으로 도움말 페이지가 반환될 수 있습니다. 이 주소는 `httpHelpPageUrl` 특성을 설정하여 변경할 수 있습니다. 또한 HTTP 대신 HTTPS를 사용하여 보안을 유지할 수 있습니다.  
  
 선택적 `httpHelpPageBinding` 및 `httpHelpPageBinding` 특성을 사용하면 서비스 웹 페이지에 액세스하는 데 사용되는 바인딩을 구성할 수 있습니다. 바인딩을 지정하지 않으면 서비스 도움말 페이지 액세스에 기본 바인딩(HTTP의 경우 `HttpTransportBindingElement`, HTTPS의 경우 `HttpsTransportBindingElement`)이 적절하게 사용됩니다. 기본 제공 WCF 바인딩에는 이러한 특성을 사용할 수 없습니다. F: IReplyChannel >를 지 원하는 내부 바인딩 요소가 있는 바인딩만 지원 됩니다. 또한 바인딩의 <xref:System.ServiceModel.Channels.MessageVersion?displayProperty=nameWithType> 속성은 <xref:System.ServiceModel.Channels.MessageVersion.None?displayProperty=nameWithType>이어야 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.ServiceDebugElement>
- <xref:System.ServiceModel.Description.ServiceDebugBehavior>
- [계약 및 서비스에서 오류 지정 및 처리](../../../wcf/specifying-and-handling-faults-in-contracts-and-services.md)
- [예외 및 오류 처리](../../../wcf/extending/handling-exceptions-and-faults.md)
- [서비스 디버그 동작](../../../wcf/samples/service-debug-behavior.md)
