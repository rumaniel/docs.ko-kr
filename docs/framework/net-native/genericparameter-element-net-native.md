---
title: <GenericParameter>요소 (.NET 네이티브)
ms.date: 03/30/2017
ms.assetid: cbd49732-3615-49a5-a900-f96947cdc3e6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2898d804f7a351045b2fbce42042f9fd322ebb0a
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049754"
---
# <a name="genericparameter-element-net-native"></a>\<GenericParameter > 요소 (.NET 네이티브)
제네릭 형식 또는 메서드의 매개 변수 형식에 정책을 적용합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
<GenericParameter Name="generic_parameter_name"  
                  Activate="policy_type"  
                  Browse="policy_type"  
                  Dynamic="policy_type"  
                  Serialize="policy_type"  
                  DataContractSerializer="policy_type"  
                  DataContractJsonSerializer="policy_type"  
                  XmlSerializer="policy_type"  
                  MarshalObject="policy_type"  
                  MarshalDelegate="policy_type"  
                  MarshalStructure="policy_type"  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|특성 유형|설명|  
|---------------|--------------------|-----------------|  
|`Name`|일반|필수 특성입니다. 제네릭 매개 변수의 이름입니다. 예를 들어 <xref:System.Func%603> 제네릭 대리자의 경우 런타임 정책을 대리자의 반환 값에 적용할 수 있도록 `Name` 특성의 값은 "TResult"입니다.|  
|`Activate`|반사|선택적 특성입니다. 인스턴스를 활성화할 수 있도록 생성자에 대한 런타임 액세스를 제어합니다.|  
|`Browse`|반사|선택적 특성입니다. 프로그램 요소에 대한 정보 쿼리를 제어하지만 런타임 액세스를 사용하도록 설정하지는 않습니다.|  
|`Dynamic`|반사|선택적 특성입니다. 동적 프로그래밍을 수행할 수 있도록 생성자, 메서드, 필드, 속성 및 이벤트를 비롯한 모든 형식 멤버에 대한 런타임 액세스를 제어합니다.|  
|`Serialize`|Serialization|선택적 특성입니다. Newtonsoft JSON serializer 등의 라이브러리를 통해 형식 인스턴스를 serialize 및 deserialize할 수 있도록 생성자, 필드 및 속성에 대한 런타임 액세스를 제어합니다.|  
|`DataContractSerializer`|Serialization|선택적 특성입니다. <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> 클래스를 사용하는 serialization에 대한 정책을 제어합니다.|  
|`DataContractJsonSerializer`|Serialization|선택적 특성입니다. <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType> 클래스를 사용하는 JSON serialization에 대한 정책을 제어합니다.|  
|`XmlSerializer`|Serialization|선택적 특성입니다. <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> 클래스를 사용하는 XML serialization에 대한 정책을 제어합니다.|  
|`MarshalObject`|Interop|선택적 특성입니다. Windows 런타임 및 COM에 대한 참조 형식을 마샬링하는 정책을 제어합니다.|  
|`MarshalDelegate`|Interop|선택적 특성입니다. 네이티브 코드에 대한 함수 포인터로 대리자 형식을 마샬링하는 정책을 제어합니다.|  
|`MarshalStructure`|Interop|선택적 특성입니다. 값 형식을 네이티브 코드로 마샬링하는 정책을 제어합니다.|  
  
## <a name="name-attribute"></a>Name 특성  
  
|값|Description|  
|-----------|-----------------|  
|*generic_parameter_name*|필수 특성입니다. 제네릭 형식 매개 변수의 이름입니다. 예를 들어 <xref:System.Func%603> 제네릭 대리자의 경우 *generic_parameter_name*의 값이 “TResult”이면 런타임 정책이 대리자의 반환 값에 적용됩니다.|  
  
## <a name="all-other-attributes"></a>기타 모든 특성  
  
|값|Description|  
|-----------|-----------------|  
|*policy_setting*|이 정책 형식에 적용할 설정입니다. 가능한 값은 `All`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` 및 `Required All`입니다. 자세한 내용은 [런타임 지시문 정책 설정](runtime-directive-policy-settings.md)을 참조하세요.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<Method>](method-element-net-native.md)|생성자 또는 메서드에 런타임 리플렉션 정책을 적용합니다.|  
|[\<Type>](type-element-net-native.md)|클래스 또는 구조체와 같은 특정 형식에 런타임 리플렉션 정책을 적용합니다.|  
  
## <a name="remarks"></a>설명  
 `<GenericParameter>` 요소는 [\<Method>](method-element-net-native.md) 또는 [\<Type>](type-element-net-native.md) 요소의 자식이며, 제네릭 형식 또는 메서드 시그니처에서 해당 이름으로 지정되는 특정 제네릭 형식 매개 변수에 정책을 적용하는 데 사용됩니다.  
  
 `<GenericParameter>` 요소는 serializer와 함께 사용하면 가장 유용합니다. 다음 예제에서는 `<GenericParameter>` 요소를 사용하여 NewtonSoft JSON 직렬 변환기의 [JsonConvert.DeserializeObject\<T>(String)](https://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_JsonConvert_DeserializeObject__1.htm) 메서드 오버로드에 대한 호출에서 `T` 형식에 정책을 적용합니다.  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <Type Name="Newtonsoft.Json.JsonConvert" >  
      <Method Name="DeserializeObject{T}">  
         <GenericParameter Name="T" Serialize="Required All" />  
      </Method>  
   </Type>  
</Directives>  
```  
  
## <a name="see-also"></a>참고자료

- [\<Method> 요소](method-element-net-native.md)
- [\<형식 > 요소](type-element-net-native.md)
- [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)
- [런타임 지시문 정책 설정](runtime-directive-policy-settings.md)
- [런타임 지시문 요소](runtime-directive-elements.md)
