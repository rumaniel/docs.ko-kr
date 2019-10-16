---
title: <client>의 <endpoint>
ms.date: 03/30/2017
ms.assetid: de6238ae-bbf8-48e9-a1b5-e24c0bea8afa
ms.openlocfilehash: f1ffbc1e8efac70523d7f631c8cf9ba9a1622bfc
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855314"
---
# <a name="endpoint-of-client"></a>\<클라이언트 >의 \<끝점 >
클라이언트에서 서버의 서비스 엔드포인트와 연결하는 데 사용하는 채널 엔드포인트의 contract, binding 및 address 속성을 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<클라이언트 >** ](client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<끝점 >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<endpoint address="String"
          behaviorConfiguration="String"
          binding="String"
          bindingConfiguration="String"
          contract="String"
          endpointConfiguration="String"
          kind="String"
          name="String">
</endpoint>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|주소|필수 문자열 특성입니다.<br /><br /> 엔드포인트의 주소를 지정합니다. 기본값은 빈 문자열입니다. 주소는 절대 URI이어야 합니다.|  
|behaviorConfiguration|엔드포인트를 인스턴스화할 때 사용할 동작의 이름을 포함하는 문자열입니다. 동작 이름은 서비스가 정의된 지점의 범위에 속해야 합니다. 기본값은 빈 문자열입니다.|  
|바인딩(binding)|필수 문자열 특성입니다.<br /><br /> 사용할 바인딩의 형식을 나타내는 문자열입니다. 형식에 등록된 구성 섹션이 있어야 형식을 참조할 수 있습니다. 이 형식은 바인딩의 형식 이름 대신 섹션 이름으로 등록됩니다.|  
|bindingConfiguration|선택 사항입니다. 엔드포인트가 인스턴스화될 때 사용할 바인딩 구성의 이름을 포함하는 문자열입니다. 바인딩 구성은 엔드포인트가 정의된 지점의 범위에 속해야 합니다. 기본값은 빈 문자열입니다.<br /><br /> 이 특성은 구성 파일에서 특정 바인딩 구성을 참조하기 위해 `binding`과 함께 사용됩니다. 사용자 지정 바인딩을 사용하려는 경우 이 특성을 설정하세요. 그렇지 않으면 예외가 throw될 수 있습니다.|  
|계약(contract)|필수 문자열 특성입니다.<br /><br /> 이 엔드포인트가 공개하는 계약을 나타내는 문자열입니다. 어셈블리는 계약 형식을 구현해야 합니다.|  
|endpointConfiguration|이 표준 엔드포인트의 추가 구성 정보를 참조하는 `kind` 특성에 의해 설정되는 표준 엔드포인트의 이름을 지정하는 문자열입니다. 이와 동일한 이름이 `<standardEndpoints>` 섹션에서 정의되어야 합니다.|  
|kind|적용되는 표준 엔드포인트의 형식을 지정하는 문자열입니다. 이 형식이 `<extensions>` 섹션 또는 machine.config에 등록되어야 합니다. 지정하지 않으면 일반 채널 엔드포인트가 만들어집니다.|  
|name|선택적 문자열 특성입니다. 이 특성은 지정된 계약의 엔드포인트를 고유하게 식별합니다. 지정한 계약 형식에 대해 여러 클라이언트를 정의할 수 있습니다. 각 정의는 고유한 구성 이름으로 식별됩니다. 이 특성을 생략하면 해당하는 엔드포인트가 지정된 계약 형식과 연결된 기본 엔드포인트로 사용됩니다. 기본값은 빈 문자열입니다.<br /><br /> 바인딩의 `name` 특성은 WSDL을 통해 정의를 내보내는 데 사용됩니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<headers>](headers.md)|주소 헤더 컬렉션입니다.|  
|[\<identity>](identity.md)|한 엔드포인트에서 다른 엔드포인트와 메시지를 교환할 때 상대 엔드포인트를 인증할 수 있도록 하는 ID입니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<client>](client.md)|클라이언트가 연결할 수 있는 엔드포인트의 목록을 정의하는 구성 섹션입니다.|  
  
## <a name="example"></a>예제  
 이것은 채널 엔드포인트 구성의 예제입니다.  
  
```xml  
<endpoint address="/HelloWorld/"
          bindingConfiguration="usingDefaults"
          name="MyBinding"
          binding="customBinding"
          contract="HelloWorld">
</endpoint>
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.ChannelEndpointElement>
- <xref:System.ServiceModel.Configuration.ClientSection>
- <xref:System.ServiceModel.Configuration.ChannelEndpointElementCollection>
- <xref:System.ServiceModel.Configuration.ClientSection.Endpoints%2A>
- <xref:System.ServiceModel.Configuration.ChannelEndpointElement>
- [WCF 클라이언트 구성](../../../wcf/feature-details/client-configuration.md)
- [클라이언트](../../../wcf/feature-details/clients.md)
