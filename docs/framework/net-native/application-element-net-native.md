---
title: <Application>요소 (.NET 네이티브)
ms.date: 03/30/2017
ms.assetid: b4e9b37a-059b-4076-8f56-cb3f9cef0cd9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2183a64f4e30a5188940abd5108a7ca1bddfe120
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049926"
---
# <a name="application-element-net-native"></a>\<응용 프로그램 > 요소 (.NET 네이티브)
런타임에 메타데이터를 리플렉션에 사용할 수 있는 애플리케이션 수준 형식 및 형식 멤버의 컨테이너로 사용되며, 앱의 모든 프로그램 요소에 대해 런타임 리플렉션 정책을 적용합니다.  
  
 \<Directives> 요소  
\<Application> 요소(rd.xml)  
  
## <a name="syntax"></a>구문  
  
```xml  
<Application Activate="policy_setting"  
             Browse="policy_setting"  
             Dynamic="policy_setting"  
             Serialize="policy_setting"  
             DataContractSerializer="policy_setting"  
             DataContractJsonSerializer="policy_setting"  
             XmlSerializer="policy_setting"  
             MarshalObject="policy_setting"  
             MarshalDelegate="policy_setting"  
             MarshalStructure="policy_setting" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다. 자식 요소 표에서 정책은 런타임에 특정 프로그램 요소에 대해 제공되는 메타데이터의 종류를 참조합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|특성 유형|Description|  
|---------------|--------------------|-----------------|  
|`Activate`|반사|선택적 특성입니다. 인스턴스를 활성화할 수 있도록 생성자에 대한 런타임 액세스를 제어합니다.|  
|`Browse`|반사|선택적 특성입니다. 형식에 대한 정보 쿼리 또는 형식 열거는 제어하지만 런타임에 동적 호출을 사용하도록 설정하지는 않습니다.|  
|`Dynamic`|반사|선택적 특성입니다. 동적 프로그래밍을 수행할 수 있도록 생성자, 메서드, 필드, 속성 및 이벤트를 비롯한 모든 형식 멤버에 대한 런타임 액세스를 제어합니다.|  
|`Serialize`|Serialization|선택적 특성입니다. Newtonsoft JSON serializer 등의 라이브러리를 통해 형식 인스턴스를 serialize 및 deserialize할 수 있도록 생성자, 필드 및 속성에 대한 런타임 액세스를 제어합니다.|  
|`DataContractSerializer`|Serialization|선택적 특성입니다. <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> 클래스를 사용하는 serialization에 대한 정책을 제어합니다.|  
|`DataContractJsonSerializer`|Serialization|선택적 특성입니다. <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType> 클래스를 사용하는 JSON serialization에 대한 정책을 제어합니다.|  
|`XmlSerializer`|Serialization|선택적 특성입니다. <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> 클래스를 사용하는 XML serialization에 대한 정책을 제어합니다.|  
|`MarshalObject`|Interop|선택적 특성입니다. Windows 런타임 및 COM에 대한 참조 형식을 마샬링하는 정책을 제어합니다.|  
|`MarshalDelegate`|Interop|선택적 특성입니다. 네이티브 코드에 대한 함수 포인터로 대리자 형식을 마샬링하는 정책을 제어합니다.|  
|`MarshalStructure`|Interop|선택적 특성입니다. 구조체를 네이티브 코드로 마샬링하는 정책을 제어합니다.|  
  
## <a name="all-attributes"></a>모든 특성  
  
|값|Description|  
|-----------|-----------------|  
|*policy_setting*|앱의 형식에 적용할 이 정책에 대한 설정입니다. 가능한 값은 `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` 및 `Required All`입니다. 자세한 내용은 [런타임 지시문 정책 설정](runtime-directive-policy-settings.md)을 참조하세요.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<Assembly>](assembly-element-net-native.md)|특정 어셈블리의 모든 형식에 정책을 적용합니다.|  
|[\<Namespace>](namespace-element-net-native.md)|특정 네임스페이스의 모든 형식에 정책을 적용합니다.|  
|[\<Type>](type-element-net-native.md)|클래스 또는 구조체와 같은 특정 형식에 정책을 적용합니다.|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|생성된 제네릭 형식에 정책을 적용합니다. 예를 들어 [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 요소를 사용하면 `List<String>` 형식에 대한 정책을 정의할 수 있습니다.|  
|[\<Method>](method-element-net-native.md)|특정 형식에 대한 메서드에 정책을 적용합니다.|  
|[\<MethodInstantiation>](methodinstantiation-element-net-native.md)|생성된 제네릭 메서드에 정책을 적용합니다.|  
|[\<Property>](property-element-net-native.md)|특정 형식에 대한 속성에 정책을 적용합니다.|  
|[\<Field>](field-element-net-native.md)|특정 형식에 대한 필드에 정책을 적용합니다.|  
|[\<Event>](event-element-net-native.md)|특정 형식의 이벤트에 정책을 적용합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<Directives>](directives-element-net-native.md)|런타임 지시문 파일의 루트 요소입니다.|  
  
## <a name="remarks"></a>설명  
 [\<Directives>](directives-element-net-native.md) 요소는 `<Application>` 요소를 포함하지 않을 수도 있고 하나 포함할 수도 있습니다. 단일 리플렉션 지시문 파일에 여러 `<Application>` 요소를 포함할 수는 없습니다.  
  
 `<Application>` 요소는 다음 두 가지 방법 중 하나로 사용할 수 있습니다.  
  
- 런타임에 해당 메타데이터가 필요한 프로그램 요소를 정의하는 컨테이너로 사용. 이 경우에는 `<Application>` 요소에 특성이 없어도 됩니다. 컴파일 타임에 컴파일러 도구는 .NET Framework 핵심 라이브러리를 비롯한 모든 라이브러리에서 `<Application>` 요소의 자식 요소가 식별한 프로그램 요소를 검색합니다. 반면 [\<Library>](library-element-net-native.md) 요소로 지정된 라이브러리에서는 [\<Library>](library-element-net-native.md) 요소의 자식 요소가 식별한 프로그램 요소만 검색합니다.  
  
- 리플렉션, serialization 및 interop에 대한 애플리케이션 수준 정책을 설정하는 요소로 사용. `<Application>` 요소의 특성은 애플리케이션 수준 정책을 정의하며, 이 정책은 `<Application>` 또는 [\<Library&gt;](library-element-net-native.md) 요소로 정의된 자식 요소에 의해 재정의될 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [\<Library > 요소](library-element-net-native.md)
- [\<지시문 > 요소](directives-element-net-native.md)
- [런타임 지시문 요소](runtime-directive-elements.md)
- [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)
