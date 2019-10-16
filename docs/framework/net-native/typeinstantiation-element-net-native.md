---
title: <TypeInstantiation>요소 (.NET 네이티브)
ms.date: 03/30/2017
ms.assetid: a5eada64-075b-4162-9655-ded84e4681f2
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 375c95a30f4f60bb711e176cb6c2d0c5fd763e2f
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049108"
---
# <a name="typeinstantiation-element-net-native"></a>\<TypeInstantiation > 요소 (.NET 네이티브)
생성된 제네릭 형식에 런타임 리플렉션 정책을 적용합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
<TypeInstantiation Name="type_name"  
                   Arguments="type_arguments"  
                   Activate="policy_type"  
                   Browse="policy_type"  
                   Dynamic="policy_type"  
                   Serialize="policy_type"  
                   DataContractSerializer="policy_setting"  
                   DataContractJsonSerializer="policy_setting"  
                   XmlSerializer="policy_setting"  
                   MarshalObject="policy_setting"  
                   MarshalDelegate="policy_setting"  
                   MarshalStructure="policy_setting" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|특성 유형|Description|  
|---------------|--------------------|-----------------|  
|`Name`|일반|필수 특성입니다. 형식 이름을 지정합니다.|  
|`Arguments`|일반|필수 특성입니다. 제네릭 형식 인수를 지정합니다. 인수가 여러 개이면 쉼표로 구분합니다.|  
|`Activate`|반사|선택적 특성입니다. 인스턴스를 활성화할 수 있도록 생성자에 대한 런타임 액세스를 제어합니다.|  
|`Browse`|반사|선택적 특성입니다. 프로그램 요소에 대한 정보 쿼리를 제어하지만 런타임 액세스를 사용하도록 설정하지는 않습니다.|  
|`Dynamic`|반사|선택적 특성입니다. 동적 프로그래밍을 수행할 수 있도록 생성자, 메서드, 필드, 속성 및 이벤트를 비롯한 모든 형식 멤버에 대한 런타임 액세스를 제어합니다.|  
|`Serialize`|Serialization|선택적 특성입니다. Newtonsoft JSON serializer 등의 라이브러리를 통해 형식 인스턴스를 serialize 및 deserialize할 수 있도록 생성자, 필드 및 속성에 대한 런타임 액세스를 제어합니다.|  
|`DataContractSerializer`|Serialization|선택적 특성입니다. <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> 클래스를 사용하는 serialization에 대한 정책을 제어합니다.|  
|`DataContractJsonSerializer`|Serialization|선택적 특성입니다. <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType> 클래스를 사용하는 JSON serialization에 대한 정책을 제어합니다.|  
|`XmlSerializer`|Serialization|선택적 특성입니다. <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> 클래스를 사용하는 XML serialization에 대한 정책을 제어합니다.|  
|`MarshalObject`|Interop|선택적 특성입니다. Windows 런타임 및 COM에 대한 참조 형식을 마샬링하는 정책을 제어합니다.|  
|`MarshalDelegate`|Interop|선택적 특성입니다. 네이티브 코드에 대한 함수 포인터로 대리자 형식을 마샬링하는 정책을 제어합니다.|  
|`MarshalStructure`|Interop|선택적 특성입니다. 구조체를 네이티브 코드로 마샬링하는 정책을 제어합니다.|  
  
## <a name="name-attribute"></a>Name 특성  
  
|값|Description|  
|-----------|-----------------|  
|*type_name*|형식 이름입니다. 이 `<TypeInstantiation>` 요소가 [\<Namespace>](namespace-element-net-native.md) 요소, [\<Type>](type-element-net-native.md) 요소 또는 다른 `<TypeInstantiation>` 요소의 자식인 경우 *type_name*은 네임스페이스가 없는 형식 이름을 지정할 수 있습니다. 그러지 않으면 *type_name*은 정규화된 형식 이름을 포함해야 합니다. 형식 이름은 데코레이팅되지 않습니다. 예를 들어 <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> 개체의 `<TypeInstantiation>` 요소는 다음과 같이 표시될 수 있습니다.<br /><br /> `\<TypeInstantiation Name=System.Collections.Generic.List Dynamic="Required Public" />`|  
  
## <a name="arguments-attribute"></a>인수 특성  
  
|값|설명|  
|-----------|-----------------|  
|*type_argument*|제네릭 형식 인수를 지정합니다. 인수가 여러 개이면 쉼표로 구분합니다. 각 인수는 정규화된 형식 이름으로 구성되어야 합니다.|  
  
## <a name="all-other-attributes"></a>기타 모든 특성  
  
|값|설명|  
|-----------|-----------------|  
|*policy_setting*|생성된 제네릭 형식에 대해 이 정책 형식에 적용할 설정입니다. 가능한 값은 `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` 및 `Required All`입니다. 자세한 내용은 [런타임 지시문 정책 설정](runtime-directive-policy-settings.md)을 참조하세요.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<Event>](event-element-net-native.md)|이 형식에 속하는 이벤트에 리플렉션 정책을 적용합니다.|  
|[\<Field>](field-element-net-native.md)|이 형식에 속하는 필드에 리플렉션 정책을 적용합니다.|  
|[\<ImpliesType>](impliestype-element-net-native.md)|포함 `<TypeInstantiation>` 요소가 나타내는 형식에 정책이 적용된 경우 형식에 해당 정책을 적용합니다.|  
|[\<Method>](method-element-net-native.md)|이 형식에 속하는 메서드에 리플렉션 정책을 적용합니다.|  
|[\<MethodInstantiation>](methodinstantiation-element-net-native.md)|이 형식에 속하는 생성된 제네릭 메서드에 리플렉션 정책을 적용합니다.|  
|[\<Property>](property-element-net-native.md)|이 형식에 속하는 속성에 리플렉션 정책을 적용합니다.|  
|[\<Type>](type-element-net-native.md)|중첩된 형식에 리플렉션 정책을 적용합니다.|  
|`<TypeInstantiation>`|생성된 중첩 제네릭 형식에 리플렉션 정책을 적용합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<Application>](application-element-net-native.md)|런타임에 해당 메타데이터를 리플렉션에 사용할 수 있는 애플리케이션 수준 형식 및 형식 멤버에 대한 컨테이너로 사용됩니다.|  
|[\<Assembly>](assembly-element-net-native.md)|지정된 어셈블리의 모든 형식에 리플렉션 정책을 적용합니다.|  
|[\<Library>](library-element-net-native.md)|런타임에 해당 메타데이터를 리플렉션에 사용할 수 있는 형식 및 형식 멤버가 포함된 어셈블리를 정의합니다.|  
|[\<Namespace>](namespace-element-net-native.md)|네임스페이스의 모든 형식에 리플렉션 정책을 적용합니다.|  
|[\<Type>](type-element-net-native.md)|형식 및 모든 해당 멤버에 리플렉션 정책을 적용합니다.|  
|`<TypeInstantiation>`|생성된 제네릭 형식 및 모든 해당 멤버에 리플렉션 정책을 적용합니다.|  
  
## <a name="remarks"></a>설명  
 리플렉션, serialization 및 interop 특성은 모두 선택 사항입니다. 그러나 이러한 특성이 하나 이상 있어야 합니다.  
  
 `<TypeInstantiation>` 요소는 [\<Assembly>](assembly-element-net-native.md), [\<Namespace>](namespace-element-net-native.md) 또는 [\<Type>](type-element-net-native.md) 요소의 자식인 경우 부모 요소가 정의하는 정책 설정을 재정의합니다. [\<Type>](type-element-net-native.md) 요소가 해당 제네릭 형식 정의를 정의하는 경우 `<TypeInstantiation>` 요소는 지정한 생성된 제네릭 형식의 인스턴스화에 대해서만 런타임 리플렉션 정책을 재정의합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 리플렉션을 사용하여 생성된 <xref:System.Collections.Generic.Dictionary%602> 개체에서 제네릭 형식 정의를 검색합니다. 또한 리플렉션을 사용하여 생성된 제네릭 형식 및 제네릭 형식 정의를 나타내는 <xref:System.Type> 개체에 대한 정보를 표시합니다. `b` 예제의<xref:Windows.UI.Xaml.Controls.TextBlock> 변수는 컨트롤입니다.  
  
 [!code-csharp[ProjectN_Reflection#2](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/makegenerictype1.cs#2)]  
  
 .NET 네이티브 도구 체인을 사용하여 컴파일한 후 예제에서는 메서드 <xref:System.Type.GetGenericTypeDefinition%2A?displayProperty=nameWithType>를 호출하는 줄에서 [MissingMetadataException](missingmetadataexception-class-net-native.md) 예외를 throw합니다. 다음 `<TypeInstantiation>` 요소를 런타임 지시문 파일에 추가하면 예외를 방지하고 필요한 메타데이터를 제공할 수 있습니다.  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Application>  
    <Assembly Name="*Application*" Dynamic="Required All" />  
     <TypeInstantiation Name="System.Collections.Generic.Dictionary"  
                        Arguments="System.String,GenericType.Example"  
                        Dynamic="Required Public" />  
  </Application>  
</Directives>  
```  
  
## <a name="see-also"></a>참고자료

- [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)
- [런타임 지시문 요소](runtime-directive-elements.md)
- [런타임 지시문 정책 설정](runtime-directive-policy-settings.md)
