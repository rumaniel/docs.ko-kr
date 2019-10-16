---
title: <webMessageEncoding>
ms.date: 03/30/2017
ms.assetid: 892ca485-e21a-4a44-8e40-633161ef6796
ms.openlocfilehash: 1015c8b812d54288a7b2773282e6c935d7634bae
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70399150"
---
# <a name="webmessageencoding"></a>\<webMessageEncoding>
WCF(Windows Communication Foundation) 바인딩에 사용될 경우 일반 텍스트 XML, JSON(JavaScript Object Notation) 메시지 인코딩 및 "원시" 이진 콘텐츠를 읽고 쓸 수 있게 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<바인딩 >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<customBinding >** ](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<바인딩 >** \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<webMessageEncoding >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<webMessageEncoding maxReadPoolSize="Integer"
                    maxWritePoolSize="Integer"
                    writeEncoding="UnicodeFffeTextEncoding/Utf16TextEncoding/Utf8TextEncoding" />
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`maxReadPoolSize`|새 판독기를 할당하지 않고 동시에 읽을 수 있는 메시지 수입니다. 풀 크기가 커지면 작업 집합이 커지는 단점이 있지만 동작이 많을 경우의 시스템 안정성이 높아집니다. 기본값으로 각 내부 인코더(텍스트, JSON 및 "원시")에 대해 64개의 판독기가 사용됩니다.<br /><br /> 이 값을 늘리면 메모리 사용량이 증가하지만, 판독기를 새로 만들 필요 없이 이미 만들어진 풀의 판독기를 사용할 수 있기 때문에 인코더가 갑자기 많은 메시지가 들어오는 경우에 대비할 수 있습니다.|  
|`maxWritePoolSize`|새 작성기를 할당하지 않고 동시에 보낼 수 있는 메시지 수입니다. 풀 크기가 커지면 작업 집합이 커지는 단점이 있지만 동작이 많을 경우의 시스템 안정성이 높아집니다. 기본값으로 각 내부 인코더(텍스트, JSON 및 "원시")에 대해 16개의 작성기가 사용됩니다.<br /><br /> 이 값을 늘리면 메모리 사용량이 증가하지만, 작성기를 새로 만들 필요 없이 풀에서 이미 만들어진 작성기를 사용할 수 있기 때문에 인코더가 갑자기 많은 메시지가 나가는 경우에 대비할 수 있습니다.|  
|`writeEncoding`|바인딩에서 메시지를 내보내는 데 사용되는 문자 집합 인코딩을 지정합니다. 유효한 값은<br /><br /> -   UnicodeFffeTextEncoding: 유니코드 빅 Endian 인코딩입니다.<br />-   Utf16TextEncoding: 유니코드 인코딩입니다.<br />-   Utf8TextEncoding: 8 비트 인코딩입니다.<br /><br /> 기본값은 Utf8TextEncoding입니다. 이 특성은 <xref:System.Text.Encoding> 형식입니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<readerQuotas>](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms731325(v=vs.100))|이 바인딩으로 구성된 엔드포인트에서 처리할 수 있는 SOAP 메시지의 복잡성에 대한 제약 조건을 정의합니다. 이 요소는 <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement> 형식입니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<binding>](../../../misc/binding.md)|사용자 지정 바인딩의 모든 바인딩 기능을 정의합니다.|  
  
## <a name="remarks"></a>설명  
 인코딩은 메시지를 바이트 시퀀스로 변형하는 프로세스입니다. 디코딩은 역프로세스입니다. 이러한 프로세스에서는 문자 인코딩을 지정해야 합니다.  
  
 `webMessageEncoding` 요소는 일반 텍스트 XML 및 JSON 인코딩과 "원시" 이진 데이터 처리를 일련의 내부 인코더에 위임하는 방식으로 동작하며 이 위임은 복합 메시지 인코더에 의해 수행됩니다.  
  
 이 바인딩 요소와 요소의 복합 인코더는 `webHttpBinding` 요소에 사용되는 SOAP 메시징을 사용하지 않는 시나리오에서 인코딩을 제어하는 데 사용됩니다. 이러한 시나리오에는 POX("Plain Old XML"), REST(Representational State Transfer), RSS(Really Simple Syndication) 및 Atom 배포, AJAX(Asynchronous JavaScript and XML) 등이 있습니다. 복합 메시지 인코더는 SOAP 또는 WS-Addressing을 지원하지 않습니다.  
  
 바인딩 요소는 `writeEncoding` 특성을 사용하여 쓰기 문자 인코딩으로 구성할 수 있습니다. 제공된 <xref:System.Text.Encoding> 값은 JSON 및 텍스트 XML에 대한 쓰기 동작을 지정합니다. 읽기의 경우 유효한 모든 메시지 인코딩 및 텍스트 인코딩이 인식됩니다.  
  
 `maxReadPoolSize` 및 `maxWritePoolSize`를 사용하여 할당할 판독기 및 작성기의 최대 수를 각각 설정할 수도 있습니다. 기본적으로 64개의 판독기와 16개의 작성기가 할당됩니다.  
  
 또한 [ \<readerquotas >](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms731325(v=vs.100)) 요소를 사용 하 여 메시지 복잡성을 사용 하 여 끝점 처리 리소스를 연결 하려고 시도 하는 dos (서비스 거부) 공격 클래스 로부터 보호 하는 기본 복잡성 제약 조건을 설정 합니다.  
  
## <a name="example"></a>예제  
  
```xml  
<webMessageEncoding maxReadPoolSize="256"
                    maxWritePoolSize="128"
                    messageVersion="None"
                    textEncoding="utf-8" />
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.WebMessageEncodingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>
- <xref:System.ServiceModel.Channels.WebMessageEncodingBindingElement>
- [메시지 인코딩](message-encoding.md)
- [메시지 인코더 선택](../../../wcf/feature-details/choosing-a-message-encoder.md)
- [바인딩](../../../wcf/bindings.md)
- [바인딩 확장](../../../wcf/extending/extending-bindings.md)
- [사용자 지정 바인딩](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
