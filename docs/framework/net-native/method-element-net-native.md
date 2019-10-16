---
title: <Method>요소 (.NET 네이티브)
ms.date: 03/30/2017
ms.assetid: 348b49e5-589d-4eb2-a597-d6ff60ab52d1
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d741f51abf02f4bfda2b007efd4c859027e54d9b
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049579"
---
# <a name="method-element-net-native"></a>\<메서드 > 요소 (.NET 네이티브)
생성자 또는 메서드에 런타임 리플렉션 정책을 적용합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
<Method Name="method_name"  
        Signature="method_signature"  
        Browse="policy_type"  
        Dynamic="policy_type" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|특성 유형|Description|  
|---------------|--------------------|-----------------|  
|`Name`|일반|필수 특성입니다. 메서드 이름을 지정합니다.|  
|`Signature`|일반|선택적 특성입니다. 메서드 시그니처를 지정합니다. 매개 변수가 여러 개이면 쉼표로 구분합니다. 예를 들어 다음 `<Method>` 요소는 <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29> 메서드에 대한 정책을 정의합니다.<br /><br /> `<Type Name="System.DateTime">    <Method Name="ToString" Signature="System.String,System.IFormatProvider"            Dynamic="Required" /> </Type>`<br /><br /> 특성이 없으면 런타임 지시문은 메서드의 모든 오버로드에 적용됩니다.|  
|`Browse`|반사|선택적 특성입니다. 메서드에 대한 정보 쿼리 또는 메서드 열거는 제어하지만 런타임에 동적 호출을 사용하도록 설정하지는 않습니다.|  
|`Dynamic`|반사|선택적 특성입니다. 동적 프로그래밍을 수행할 수 있도록 생성자 또는 메서드에 대한 런타임 액세스를 제어합니다. 이 정책을 사용하면 런타임에 멤버를 동적으로 호출할 수 있습니다.|  
  
## <a name="name-attribute"></a>Name 특성  
  
|값|Description|  
|-----------|-----------------|  
|*method_name*|메서드 이름입니다. 메서드의 형식은 부모 [\<Type>](type-element-net-native.md) 또는 [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 요소로 정의됩니다.|  
  
## <a name="signature-attribute"></a>시그니처 특성  
  
|값|설명|  
|-----------|-----------------|  
|*method_signature*|메서드 시그니처를 구성하는 매개 변수 형식입니다. 매개 변수가 여러 개이면 `"System.String,System.Int32,System.Int32)"`와 같이 쉼표로 구분합니다. 매개 변수 형식 이름은 정규화해야 합니다.|  
  
## <a name="all-other-attributes"></a>기타 모든 특성  
  
|값|Description|  
|-----------|-----------------|  
|*policy_setting*|이 정책 형식에 적용할 설정입니다. 가능한 값은 `Auto`, `Excluded`, `Included` 및 `Required`입니다. 자세한 내용은 [런타임 지시문 정책 설정](runtime-directive-policy-settings.md)을 참조하세요.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<Parameter>](parameter-element-net-native.md)|메서드에 전달된 인수의 형식에 정책을 적용합니다.|  
|[\<GenericParameter>](genericparameter-element-net-native.md)|제네릭 형식 또는 메서드의 매개 변수 형식에 정책을 적용합니다.|  
|[\<ImpliesType>](impliestype-element-net-native.md)|포함 `<Method>` 요소가 나타내는 메서드에 정책이 적용된 경우 형식에 해당 정책을 적용합니다.|  
|[\<TypeParameter>](typeparameter-element-net-native.md)|메서드로 전달된 <xref:System.Type> 인수가 나타내는 형식에 정책을 적용합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<Type>](type-element-net-native.md)|형식 및 모든 해당 멤버에 리플렉션 정책을 적용합니다.|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|생성된 제네릭 형식 및 모든 해당 멤버에 리플렉션 정책을 적용합니다.|  
  
## <a name="remarks"></a>설명  
 제네릭 메서드의 `<Method>` 요소는 자체 정책이 없는 모든 인스턴스화에 해당 정책을 적용합니다.  
  
 `Signature` 특성을 사용하여 특정 메서드 오버로드에 대한 정책을 지정할 수 있습니다. `Signature` 특성이 없는 경우 런타임 지시문은 메서드의 모든 오버로드에 적용됩니다.  
  
 `<Method>` 요소를 사용하여 생성자에 대해 런타임 리플렉션 정책을 정의할 수는 없습니다. 대신 [\<Assembly>](assembly-element-net-native.md), [\<Namespace>](namespace-element-net-native.md), [\<Type>](type-element-net-native.md) 또는 [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 요소의 `Activate` 특성을 사용합니다.  
  
## <a name="example"></a>예제  
 다음 예제의 `Stringify` 메서드는 리플렉션을 사용하여 개체를 문자열 표현으로 변환하는 범용 서식 지정 메서드입니다. 이 메서드는 개체의 기본 `ToString` 메서드를 호출할 수 있을 뿐 아니라 개체의 `ToString` 메서드에 서식 문자열이나 <xref:System.IFormatProvider> 구현 중 하나 또는 둘 다를 전달하여 서식이 지정된 결과 문자열을 생성할 수도 있습니다. 또한 숫자를 이진, 16진수 또는 8진수 표현으로 변환하는 <xref:System.Convert.ToString%2A?displayProperty=nameWithType> 오버로드 중 하나를 호출할 수도 있습니다.  
  
 [!code-csharp[ProjectN_Reflection#7](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/method1.cs#7)]  
  
 다음과 같은 코드를 통해 `Stringify` 메서드를 호출할 수 있습니다.  
  
 [!code-csharp[ProjectN_Reflection#7](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/method1.cs#7)]  
  
 그러나 이 예제를 .NET 네이티브에서 컴파일하면 런타임에 <xref:System.NullReferenceException> 및 [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md) 예외를 비롯한 여러 예외가 throw될 수 있습니다. 이러한 예외가 throw되는 이유는, `Stringify` 메서드는 기본적으로 .NET Framework 클래스 라이브러리의 기본 형식에 대한 동적 서식 지정을 지원하는 데 사용되는데 기본 지시문 파일이 해당 메타데이터를 제공하지 않기 때문입니다. 그러나 메타데이터가 제공되더라도 위의 예제에서는 [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md) 예외가 throw됩니다. 적절한 `ToString` 구현이 네이티브 코드에 포함되지 않았기 때문입니다.  
  
 [\<Type>](type-element-net-native.md) 요소를 사용하여 해당 메타데이터가 있어야 하는 형식을 정의하고, `<Method>` 요소를 추가하여 동적으로 호출 가능한 메서드 오버로드 구현도 있도록 지정하면 이러한 예외를 방지할 수 있습니다. 다음은 이러한 예외를 방지하고 예제가 오류 없이 실행되도록 하는 default.rd.xml 파일입니다.  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Application>  
     <Assembly Name="*Application*" Dynamic="Required All" />  
  
     <Type Name = "System.Convert" Browse="Required Public" Dynamic="Required Public" >  
        <Method Name="ToString"    Dynamic ="Required" />  
     </Type>  
     <Type Name="System.Double" Browse="Required Public">  
        <Method Name="ToString" Dynamic="Required" />  
     </Type>  
     <Type Name ="System.Int32" Browse="Required Public" >  
        <Method Name="ToString" Dynamic="Required" />  
     </Type>  
     <Type Name ="System.Int64" Browse="Required Public" >  
        <Method Name="ToString" Dynamic="Required" />  
     </Type>  
     <Namespace Name="System" >  
        <Type Name="Byte" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="DateTime" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="Decimal" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="Guid" Browse ="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="Int16" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="SByte" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="Single" Browse="Required Public" >  
          <Method Name="ToString" Dynamic="Required" />           
        </Type>  
        <Type Name="TimeSpan" Browse="Required Public" >  
          <Method Name="ToString" Dynamic="Required" />           
        </Type>  
        <Type Name="UInt16" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="UInt32" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="UInt64" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
     </Namespace>  
  </Application>  
</Directives>  
```  
  
## <a name="see-also"></a>참고자료

- [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)
- [런타임 지시문 요소](runtime-directive-elements.md)
- [런타임 지시문 정책 설정](runtime-directive-policy-settings.md)
- [\<MethodInstantiation> 요소](methodinstantiation-element-net-native.md)
