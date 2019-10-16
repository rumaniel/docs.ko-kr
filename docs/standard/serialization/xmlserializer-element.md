---
title: <xmlSerializer> 요소
ms.date: 03/30/2017
helpviewer_keywords:
- <xmlSerializer> element
- XML serialization, configuration
- xmlSerializer element
ms.assetid: d129d10c-3eb7-45d9-8098-5fa853825e47
ms.openlocfilehash: 2919e8d4c1af858973ff3d2b58b4d3bc4f925527
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62018070"
---
# <a name="xmlserializer-element"></a>\<xmlSerializer > 요소
<xref:System.Xml.Serialization.XmlSerializer>의 진행에 대한 추가 검사가 수행되었는지 여부를 지정합니다.  
  
 \<configuration>  
\<system.xml.serialization>  
  
## <a name="syntax"></a>구문  
  
```xml  
<xmlSerializer checkDeserializerAdvance = "true"|"false" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|**checkDeserializeAdvances**|<xref:System.Xml.Serialization.XmlSerializer>의 진행률이 검사되었는지 여부를 지정합니다. 특성을 "true" 또는 "false"로 설정합니다. 기본값은 "true"입니다.|  
|**useLegacySerializationGeneration**|<xref:System.Xml.Serialization.XmlSerializer>가 C# 코드를 파일에 쓴 다음 어셈블리로 컴파일하여 어셈블리를 생성하는 레거시 serialization 생성을 사용하는지 여부를 지정합니다. 기본값은 **false**입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<system.xml.serialization> 요소](../../../docs/standard/serialization/system-xml-serialization-element.md)|<xref:System.Xml.Serialization.XmlSerializer> 및 <xref:System.Xml.Serialization.XmlSchemaImporter> 클래스에 대한 구성 설정을 포함합니다.|  
  
## <a name="remarks"></a>설명  
 기본적으로 <xref:System.Xml.Serialization.XmlSerializer>는 신뢰할 수 없는 데이터를 deserialize할 때 잠재적 서비스 거부 공격에 대한 추가 보안 계층을 제공합니다. deserialization 도중 무한 루프의 탐지를 시도하여 이러한 보안을 제공합니다. 이러한 조건이 발견 되 면 다음 메시지와 함께 예외가 throw 됩니다. "내부 오류: 기본 스트림에 대 한를 역직렬화 하지 못했습니다."  
  
 이 메시지가 반드시 서비스 거부 공격이 진행 중임을 의미하는 것은 아닙니다. 드문 경우지만 무한 루프 검색 메커니즘이 가양성(false positive)을 생성하여 적법한 들어오는 메시지에 대해 예외가 throw될 수도 있습니다. 특정 애플리케이션에서 적법한 메시지가 이러한 추가 보호 계층에 의해 거부된 경우 **checkDeserializeAdvances** 특성을 “false”로 설정합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 **checkDeserializeAdvances** 특성을 “false”로 설정합니다.  
  
```xml  
<configuration>  
  <system.xml.serialization>  
    <xmlSerializer checkDeserializeAdvances="false" />  
  </system.xml.serialization>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Xml.Serialization.XmlSerializer>
- [\<system.xml.serialization> 요소](../../../docs/standard/serialization/system-xml-serialization-element.md)
- [XML 및 SOAP serialization](../../../docs/standard/serialization/xml-and-soap-serialization.md)
