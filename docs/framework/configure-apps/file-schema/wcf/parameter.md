---
title: <parameter>
ms.date: 03/30/2017
ms.assetid: 0fb41e2d-64f7-44ab-993e-05892eac6d82
ms.openlocfilehash: 07fa410109a7bd2fa315132c4737301698bb3a93
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70400105"
---
# <a name="parameter"></a>\<parameter>
선언된 형식이 제네릭 형식이면 제네릭 매개 변수를 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<>를 직렬화 합니다.** ](system-runtime-serialization.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<dataContractSerializer >** ](datacontractserializer.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<declaredTypes >** ](declaredtypes.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<> 추가**](add-of-declaredtypes-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<knownType >** ](knowntype.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<매개 변수 >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<parameter index="Integer"
           type="String" />
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|인덱스|선언된 형식이 제네릭 형식이면 알려진 형식을 반환하는 제네릭 매개 변수를 지정합니다.|  
|type|serialization 및 deserialization에 사용되는 알려진 형식을 설명하는 문자열입니다.|  
  
## <a name="index-attribute"></a>index 특성  
  
|값|Description|  
|-----------|-----------------|  
|"0"|제네릭 형식의 첫 번째 매개 변수입니다. 예를 들어, <xref:System.Collections.Generic.List%601>에는 하나의 매개 변수만 있습니다. 이 형식이 선언된 형식으로 사용되면 index가 "0"으로 설정됩니다.|  
|"1"|제네릭 형식의 두 번째 매개 변수입니다. 예를 들어, <xref:System.Collections.Generic.Dictionary%602>에는 두 개의 매개 변수가 있습니다. 이 알려진 형식이 두 번째 매개 변수에서 반환되면 index 특성을 "1"로 설정합니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<knownType>](knowntype.md)|선언된 형식의 필드 또는 속성에서 반환될 수 있는 알려진 형식을 지정합니다.|  
  
## <a name="remarks"></a>설명  
 알려진 형식에 대 한 자세한 내용은 [데이터 계약 알려진 형식](../../../wcf/feature-details/data-contract-known-types.md) 및 <xref:System.Runtime.Serialization.DataContractSerializer>을 참조 하십시오.  
  
 이 요소를 사용 하는 예제는 [ \<dataContractSerializer >](datacontractserializer-element.md) 를 참조 하세요.  
  
 이 구성 요소는 두 가지 특성을 동시에 가질 수 없습니다. 두 가지 특성이 모두 설정되면 <xref:System.Configuration.ConfigurationErrorsException>이 발생합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataContractSerializer>
- [데이터 계약 알려진 형식](../../../wcf/feature-details/data-contract-known-types.md)
- [\<dataContractSerializer>](datacontractserializer-element.md)
- [\<add>](add-of-declaredtypes-element.md)
