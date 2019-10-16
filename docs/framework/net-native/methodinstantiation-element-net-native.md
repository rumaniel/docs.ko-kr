---
title: <MethodInstantiation>요소 (.NET 네이티브)
ms.date: 03/30/2017
ms.assetid: a3355d78-2a88-4109-8521-830d7cae260a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f2c0354853e4725ba3e673fb9142c4a7a85d2121
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049616"
---
# <a name="methodinstantiation-element-net-native"></a>\<MethodInstantiation > 요소 (.NET 네이티브)
생성된 제네릭 메서드에 런타임 리플렉션 정책을 적용합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
<MethodInstantiation Name="method_name"  
                     Signature="method_signature"  
                     Arguments="method_arguments"  
                     Browse="policy_type"  
                     Dynamic="policy_type" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|특성 유형|설명|  
|---------------|--------------------|-----------------|  
|`Name`|일반|필수 특성입니다. 메서드 이름을 지정합니다.|  
|`Signature`|일반|선택적 특성입니다. 메서드의 명명된 매개 변수를 지정합니다. 명명된 매개 변수가 여러 개이면 쉼표로 구분합니다. `Signature` 특성은 오버로드된 메서드를 구별하는 데 사용됩니다.|  
|`Arguments`|일반|필수 특성입니다. 제네릭 형식 인수를 지정합니다. 인수가 여러 개이면 쉼표로 구분합니다.|  
|`Browse`|반사|선택적 특성입니다. 메서드에 대한 정보 쿼리 또는 메서드 열거는 제어하지만 런타임에 동적 호출을 사용하도록 설정하지는 않습니다.|  
|`Dynamic`|반사|선택적 특성입니다. 동적 프로그래밍을 수행할 수 있도록 생성자 또는 메서드에 대한 런타임 액세스를 제어합니다. 이 정책을 사용하면 런타임에 멤버를 동적으로 호출할 수 있습니다.|  
  
## <a name="name-attribute"></a>Name 특성  
  
|값|Description|  
|-----------|-----------------|  
|*method_name*|메서드 이름입니다. 메서드의 형식은 부모 [\<Type>](type-element-net-native.md) 또는 [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 요소로 정의됩니다.|  
  
## <a name="signature-attribute"></a>시그니처 특성  
  
|값|Description|  
|-----------|-----------------|  
|*method_signature*|메서드의 명명된 매개 변수를 지정합니다. 매개 변수가 여러 개이면 쉼표로 구분합니다.|  
  
## <a name="arguments-attribute"></a>인수 특성  
  
|값|Description|  
|-----------|-----------------|  
|*method_arguments*|제네릭 형식 인수를 지정합니다. 인수가 여러 개이면 쉼표로 구분합니다. 각 인수는 정규화된 형식 이름으로 구성되어야 합니다.|  
  
## <a name="all-other-attributes"></a>기타 모든 특성  
  
|값|Description|  
|-----------|-----------------|  
|*policy_setting*|메서드에 대해 이 정책 형식에 적용할 설정입니다. 가능한 값은 `Auto`, `Excluded`, `Included` 및 `Required`입니다. 자세한 내용은 [런타임 지시문 정책 설정](runtime-directive-policy-settings.md)을 참조하세요.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<Type>](type-element-net-native.md)|형식 및 모든 해당 멤버에 리플렉션 정책을 적용합니다.|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|생성된 제네릭 형식 및 모든 해당 멤버에 리플렉션 정책을 적용합니다.|  
  
## <a name="remarks"></a>설명  
 `<MethodInstantiation>` 요소는 해당 개방형 제네릭 메서드의 런타임 리플렉션 정책을 재정의합니다.  
  
## <a name="see-also"></a>참고자료

- [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)
- [런타임 지시문 요소](runtime-directive-elements.md)
- [런타임 지시문 정책 설정](runtime-directive-policy-settings.md)
- [\<Method> 요소](method-element-net-native.md)
