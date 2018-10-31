---
title: '&lt;속성&gt; 요소(.NET 네이티브)'
ms.date: 03/30/2017
ms.assetid: ad4ba56d-3bcb-4c10-ba90-1cc66e2175a1
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1b4541bc5a878739c17179576739fbe33384445d
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50205213"
---
# <a name="ltpropertygt-element-net-native"></a>&lt;속성&gt; 요소(.NET 네이티브)
런타임 리플렉션 정책을 속성에 적용합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
<Property Name="property_name"  
          Browse="policy_type"  
          Dynamic="policy_type"  
          Serialize="policy_type" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|특성 형식|설명|  
|---------------|--------------------|-----------------|  
|`Name`|일반|필수 특성입니다. 속성 이름을 지정합니다.|  
|`Browse`|반사|선택적 특성입니다. 속성에 대한 정보 쿼리 또는 속성 열거는 제어하지만 런타임에 동적 호출을 사용하도록 설정하지는 않습니다.|  
|`Dynamic`|반사|선택적 특성입니다. 동적 프로그래밍을 수행할 수 있도록 속성에 대한 런타임 액세스를 제어합니다. 이 정책을 통해 런타임에 속성을 동적으로 설정하거나 검색할 수 있습니다.|  
|`Serialize`|Serialization|선택적 특성입니다. Newtonsoft JSON serializer 등의 라이브러리를 통해 형식 인스턴스를 serialize하거나 데이터 바인딩에 사용할 수 있도록 속성에 대한 런타임 액세스를 제어합니다.|  
  
## <a name="name-attribute"></a>Name 특성  
  
|값|설명|  
|-----------|-----------------|  
|*method_name*|속성 이름입니다. 속성의 형식은 부모 [\<Type>](../../../docs/framework/net-native/type-element-net-native.md) 또는 [\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) 요소로 정의됩니다.|  
  
## <a name="all-other-attributes"></a>기타 모든 특성  
  
|값|설명|  
|-----------|-----------------|  
|*policy_setting*|속성에 대해 이 정책 형식에 적용할 설정입니다. 가능한 값은 `Auto`, `Excluded`, `Included` 및 `Required`입니다. 자세한 내용은 [런타임 지시문 정책 설정](../../../docs/framework/net-native/runtime-directive-policy-settings.md)을 참조하세요.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<Type>](../../../docs/framework/net-native/type-element-net-native.md)|형식 및 모든 해당 멤버에 리플렉션 정책을 적용합니다.|  
|[\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|생성된 제네릭 형식 및 모든 해당 멤버에 리플렉션 정책을 적용합니다.|  
  
## <a name="remarks"></a>설명  
 속성의 정책이 명시적으로 정의되어 있지 않으면 부모 요소의 런타임 정책을 상속합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 리플렉션을 사용하여 `Book` 개체를 인스턴스화하고 해당 속성 값을 표시합니다. 프로젝트의 원본 default.rd.xml 파일은 다음과 같이 표시됩니다.  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <Application>  
      <Namespace Name="LibraryApplications"  Browse="Required Public" >  
         <Type Name="Book"   Activate="All" />  
      </Namespace>  
   </Application>  
</Directives>  
```  
  
 이 파일은 `All` 클래스에 대해 `Activate` 값을 `Book` 정책에 적용합니다. 따라서 리플렉션을 통해 클래스 생성자에 액세스할 수 있습니다. `Browse`에 대한 `Book` 정책은 부모 네임스페이스에서 상속됩니다. 이 정책은 런타임에 메타데이터를 사용할 수 있도록 하는 `Required Public`으로 설정됩니다.  
  
 다음은 예제의 소스 코드입니다. 합니다 `outputBlock` 변수 나타냅니다는 <xref:Windows.UI.Xaml.Controls.TextBlock> 제어 합니다.  
  
 [!code-csharp[ProjectN_Reflection#6](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/property1.cs#6)]  
  
 그러나 이 예제를 컴파일하고 실행하면 [MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md) 예외가 throw됩니다. `Book` 형식에 대해 메타데이터는 제공했지만 속성 getter의 구현은 동적으로 제공하지 못했기 때문입니다. 두 가지 방법 중 하나를 사용하여 이 오류를 해결할 수 있습니다.  
  
-   `Book` 형식에 대해 [\<Type>](../../../docs/framework/net-native/type-element-net-native.md) 요소에서 `Dynamic` 정책을 정의합니다.  
  
-   다음 default.rd.xml 파일에서와 같이 getter를 호출할 각 속성에 대해 중첩된 [\<Property>](../../../docs/framework/net-native/property-element-net-native.md) 요소를 추가합니다.  
  
    ```xml  
    <Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
       <Application>  
          <Namespace Name="LibraryApplications"  Browse="Required Public" >  
             <Type Name="Book"   Activate="All" >  
                <Property Name="Title" Dynamic="Required" />  
                <Property Name="Author" Dynamic="Required" />  
                  <Property Name="ISBN" Dynamic="Required" />  
             </Type>  
          </Namespace>  
       </Application>  
    </Directives>  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [런타임 지시문(rd.xml) 구성 파일 참조](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)  
 [런타임 지시문 요소](../../../docs/framework/net-native/runtime-directive-elements.md)  
 [런타임 지시문 정책 설정](../../../docs/framework/net-native/runtime-directive-policy-settings.md)
