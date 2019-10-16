---
title: 상호 운영 가능한 개체 참조
ms.date: 04/15/2019
ms.assetid: cb8da4c8-08ca-4220-a16b-e04c8f527f1b
ms.openlocfilehash: ada9084f6ac3c97dc641571c0cb8379a2fac68a8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61918972"
---
# <a name="interoperable-object-references"></a>상호 운영 가능한 개체 참조
기본적으로 <xref:System.Runtime.Serialization.DataContractSerializer> 값으로 개체를 serialize 합니다. 사용할 수는 <xref:System.Runtime.Serialization.DataContractAttribute.IsReference%2A> 개체를 직렬화 할 때 개체 참조를 유지 하기 위해 데이터 계약 serializer를 지시 하는 속성입니다.  
  
## <a name="generated-xml"></a>생성된 XML  
 예를 들어 다음과 같은 개체를 살펴보세요.  
  
```csharp  
[DataContract]  
public class X  
{  
    SomeClass someInstance = new SomeClass();  
    [DataMember]  
    public SomeClass A = someInstance;  
    [DataMember]  
    public SomeClass B = someInstance;  
}  
  
public class SomeClass   
{  
}  
```  
  
 <xref:System.Runtime.Serialization.DataContractSerializer.PreserveObjectReferences%2A>를 `false`(기본값)로 설정하면 다음 XML이 생성됩니다.  
  
```xml  
<X>  
   <A>contents of someInstance</A>  
   <B>contents of someInstance</B>  
</X>  
```  
  
 <xref:System.Runtime.Serialization.DataContractSerializer.PreserveObjectReferences%2A>를 `true`로 설정하면 다음 XML이 생성됩니다.  
  
```xml  
<X>  
   <A id="1">contents of someInstance</A>  
   <B ref="1"></B>  
</X>  
```  
  
 그러나 <xref:System.Runtime.Serialization.XsdDataContractExporter> 설명 하지 않습니다는 `id` 및 `ref` 자체의 스키마에서 특성 경우에 합니다 `preserveObjectReferences` 속성이 `true`.  
  
## <a name="using-isreference"></a>IsReference 사용  
 설명 하는 스키마에 따라 유효한 개체 참조 정보를 생성 하려면 적용 합니다 <xref:System.Runtime.Serialization.DataContractAttribute> 특성을 형식 및 설정 합니다 <xref:System.Runtime.Serialization.DataContractAttribute.IsReference%2A> 플래그를 `true`입니다. 다음 예제에서는 클래스를 수정 `X` 를 추가 하 여 이전 예제의 `IsReference`:  
  
```csharp
[DataContract(IsReference=true)]
public class X   
{  
     SomeClass someInstance = new SomeClass(); 
     [DataMember]
     public SomeClass A = someInstance;
     [DataMember] 
     public SomeClass B = someInstance;
}
  
public class SomeClass 
{   
}  
````

 생성되는 XML은 다음과 같습니다.  

```xml
<X>  
    <A id="1">
        <Value>contents of A</Value>  
    </A> 
    <B ref="1"></B>  
</X>
```  
  
 `IsReference`를 사용하면 메시지 라운드트립이 준수됩니다. 없으면 형식이 스키마에서 생성 된 경우 XML 출력에 대 한는 유형을 반드시 원래 가정 된 스키마를 사용 하 여 호환 되지 않습니다. 즉, `id` 및 `ref` 특성이 serialize되었더라도 원래 스키마 때문에 이러한 특성 또는 모든 특성이 XML에서 발생하지 않았을 수 있습니다. 사용 하 여 `IsReference` 데이터 멤버에 적용 되는 계속 해 서로 인식 되도록 *참조 가능한* 때 라운드트립 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.CollectionDataContractAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute.IsReference?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.CollectionDataContractAttribute.IsReference?displayProperty=nameWithType>
