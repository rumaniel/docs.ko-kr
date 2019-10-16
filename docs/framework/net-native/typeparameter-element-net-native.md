---
title: <TypeParameter>요소 (.NET 네이티브)
ms.date: 03/30/2017
ms.assetid: d37bb1b7-1ddc-4c6d-8ecf-583f804a2479
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0de00b9313b60b3a527dd0380ae90d82731a8c02
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049057"
---
# <a name="typeparameter-element-net-native"></a>\<TypeParameter > 요소 (.NET 네이티브)
메서드로 전달된 Type 인수가 나타내는 형식에 정책을 적용합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
<Parameter Name="parameter_name"  
           Activate="policy_type"  
           Browse="policy_type"  
           Dynamic="policy_type"  
           Serialize="policy_type"  
           DataContractSerializer="policy_type"  
           DataContractJsonSerializer="policy_type"  
           XmlSerializer="policy_type"  
           MarshalObject="policy_type"  
           MarshalDelegate="policy_type"  
           MarshalStructure="policy_type" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|특성 유형|설명|  
|---------------|--------------------|-----------------|  
|`Name`|일반|필수 특성입니다. <xref:System.Type> 형식의 매개 변수 이름입니다. 예를 들어 메서드 시그니처 `Type.GetInterfaceMap(Type interfaceType)`의 경우 `Name` 특성의 값은 "interfaceType"입니다.|  
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
  
|값|설명|  
|-----------|-----------------|  
|*parameter_name*|<xref:System.Type> 형식의 매개 변수 이름입니다. 예를 들어 메서드 시그니처 `Type.GetInterfaceMap(Type interfaceType)`의 경우 `Name` 특성의 값은 "interfaceType"입니다.|  
  
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
  
## <a name="remarks"></a>설명  
 `<TypeParameter>` 요소는 <xref:System.Type> 형식 매개 변수에만 적용할 수 있다는 점을 제외하면 [\<Parameter>](parameter-element-net-native.md) 요소와 비슷합니다. 이 요소는 `Name` 특성으로 지정된 형식 인수에 의해 런타임에 표시되는 형식에 정책을 적용합니다.  
  
 예를 들어 NewtonSoft JSON serializer는 정적 `JsonConvert.DeserializeObject(String value, Type type)` 메서드를 포함합니다. 다음 리플렉션 지시문은  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <Type Name="Newtonsoft.Json.JsonConvert" >  
      <Method Name="DeserializeObject">  
         <GenericParameter Name="type" Serialize="Required All" />  
      </Method>  
   </Type>  
</Directives>  
```  
  
 `type` 인수가 나타내는 런타임 형식에 대한 메타데이터를 serialization에 사용할 수 있도록 제공해야 함을 지정합니다. 이러한 런타임 지시문이 다음 소스 코드를 포함하는 프로젝트에 적용되는 경우  
  
```csharp  
Type t = typeof(StockQuote);  
Object obj = JsonConvert.DeserializeObject(data, t);  
```  
  
 리플렉션 지시문은 런타임에 `StockQuote` 형식의 메타데이터를 NewtonSoft JSON serializer에 제공합니다.  
  
## <a name="see-also"></a>참고자료

- [\<Method> 요소](method-element-net-native.md)
- [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)
- [런타임 지시문 정책 설정](runtime-directive-policy-settings.md)
- [런타임 지시문 요소](runtime-directive-elements.md)
