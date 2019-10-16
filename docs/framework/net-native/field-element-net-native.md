---
title: <Field>요소 (.NET 네이티브)
ms.date: 03/30/2017
ms.assetid: 6a14125f-1a8d-41a1-8a32-659ca0ad12de
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6dfb6a07f9733ab1a01a1ce9917c6a4bb4ce793b
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049771"
---
# <a name="field-element-net-native"></a>\<Field > 요소 (.NET 네이티브)
런타임 리플렉션 정책을 필드에 적용합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
<Field Name="field_name"  
       Browse="policy_type"  
       Dynamic="policy_type"  
       Serialize="policy_type" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|특성 유형|설명|  
|---------------|--------------------|-----------------|  
|`Name`|일반|필수 특성입니다. 필드 이름을 지정합니다.|  
|`Browse`|반사|선택적 특성입니다. 필드에 대한 정보 쿼리 또는 필드 열거는 제어하지만 런타임에 동적 호출을 사용하도록 설정하지는 않습니다.|  
|`Dynamic`|반사|선택적 특성입니다. 동적 프로그래밍을 수행할 수 있도록 필드에 대한 런타임 액세스를 제어합니다. 이 정책을 통해 런타임에 필드를 동적으로 설정하거나 검색할 수 있습니다.|  
|`Serialize`|Serialization|선택적 특성입니다. Newtonsoft JSON serializer 등의 라이브러리를 통해 형식 인스턴스를 serialize하거나 데이터 바인딩에 사용할 수 있도록 필드에 대한 런타임 액세스를 제어합니다.|  
  
## <a name="name-attribute"></a>Name 특성  
  
|값|Description|  
|-----------|-----------------|  
|*method_name*|필드 이름입니다. 필드의 형식은 부모 [\<Type>](type-element-net-native.md) 또는 [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 요소로 정의됩니다.|  
  
## <a name="all-other-attributes"></a>기타 모든 특성  
  
|값|Description|  
|-----------|-----------------|  
|*policy_setting*|필드에 대해 이 정책 형식에 적용할 설정입니다. 가능한 값은 `Auto`, `Excluded`, `Included` 및 `Required`입니다. 자세한 내용은 [런타임 지시문 정책 설정](runtime-directive-policy-settings.md)을 참조하세요.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<Type>](type-element-net-native.md)|형식 및 모든 해당 멤버에 리플렉션 정책을 적용합니다.|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|생성된 제네릭 형식 및 모든 해당 멤버에 리플렉션 정책을 적용합니다.|  
  
## <a name="remarks"></a>설명  
 필드의 정책이 명시적으로 정의되어 있지 않으면 부모 요소의 런타임 정책을 상속합니다.  
  
## <a name="see-also"></a>참고자료

- [런타임 지시문 요소](runtime-directive-elements.md)
- [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)
- [런타임 지시문 정책 설정](runtime-directive-policy-settings.md)
