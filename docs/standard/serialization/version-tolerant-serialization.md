---
title: 버전 독립적 Serialization
ms.date: 08/08/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- version tolerant serialization
- serialization, custom serialization
- serialization, version tolerant
- serialization, controlling
- versions and serialization
- BinaryFormatter class, samples
- serialization, attributes
ms.assetid: bea0ffe3-2708-4a16-ac7d-e586ed6b8e8d
ms.openlocfilehash: a61fa5a3f87c534574d7265dfdc16365c0afbbe0
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64644860"
---
# <a name="version-tolerant-serialization"></a>버전 독립적 Serialization
.NET Framework의 버전 1.0과 1.1에서는 버전이 다른 애플리케이션에서 재사용할 수 있는 serialize 가능한 형식을 만드는 작업에 문제가 있었습니다. 추가 필드를 추가하여 형식을 수정하면 다음 문제가 발생합니다.  
  
- 이전 형식의 새 버전을 deserialize하도록 요청하면 애플리케이션의 이전 버전이 예외를 throw합니다.  
  
- 데이터가 누락된 형식의 이전 버전을 deserialize할 때 애플리케이션의 새 버전이 예외를 throw합니다.  
  
 VTS(버전 독립적 Serialization)는 .NET Framework 2.0에 추가된 기능 집합으로, serialize 가능한 형식을 시간이 지남에 따라 더 쉽게 수정할 수 있게 해 줍니다. 특히 VTS 기능은 제네릭 형식을 비롯하여 <xref:System.SerializableAttribute> 특성이 적용된 클래스에 사용할 수 있습니다. VTS를 사용하면 형식의 다른 버전과의 호환성을 휴지하면서 해당 클래스에 새 필드를 추가할 수 있습니다. 작동하는 애플리케이션 예제는 [버전 독립적 serialization 기술 샘플](../../../docs/standard/serialization/version-tolerant-serialization-technology-sample.md)을 참조하세요.  
  
 VTS 기능은 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>를 사용할 때 활성화됩니다. 또한 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>를 사용할 때 잘못 사용된 데이터 허용 범위를 제외한 모든 기능도 활성화됩니다. serialization에 이러한 클래스를 사용하는 방법에 대한 자세한 내용은 [이진 serialization](binary-serialization.md)을 참조하세요.  
  
[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]

## <a name="feature-list"></a>기능 목록  
 이러한 기능 집합에는 다음이 포함됩니다.  
  
- 잘못 사용된 또는 예기치 않은 데이터의 허용 범위. 이를 통해 형식의 새 버전이 데이터를 이전 버전으로 전송할 수 있습니다.  
  
- 누락된 선택적 데이터의 허용 범위입니다. 이전 버전이 새 버전에 데이터를 전송할 수 있게 합니다.  
  
- 콜백 serialization. 이를 통해 데이터가 누락되었을 때 지능적으로 기본값을 설정할 수 있습니다.  
  
 또한 새 선택적 필드가 추가되었을 때 선언하기 위한 기능이 있습니다. 이것은 <xref:System.Runtime.Serialization.OptionalFieldAttribute.VersionAdded%2A> 특성의 <xref:System.Runtime.Serialization.OptionalFieldAttribute> 속성  
  
 이 기능은 아래에서 자세히 설명합니다.  
  
## <a name="tolerance-of-extraneous-or-unexpected-data"></a>잘못 사용된 또는 예기치 않은 데이터의 허용치  
 과거에는 deserialization 도중 모든 잘못 사용된 데이터나 예기치 않은 데이터로 인해 예외를 throw하는 경우가 있었습니다. VTS를 사용하면 같은 상황에서 잘못 사용된 데이터나 예기치 않은 데이터가 예외를 throw하는 대신 무시됩니다. 이를 통해 형식의 새 버전(즉, 더 많은 필드가 포함된 버전)을 사용하는 애플리케이션이 같은 형식의 이전 버전으로 예상되는 애플리케이션에 정보를 전송할 수 있습니다.  
  
 다음 예제에서는 이전 애플리케이션이 새 버전을 deserialize할 때 `CountryField` 클래스 버전 2.0의 `Address`에 포함된 추가 데이터가 무시됩니다.  
  
```csharp  
// Version 1 of the Address class.  
[Serializable]  
public class Address  
{  
    public string Street;  
    public string City;  
}  
// Version 2.0 of the Address class.  
[Serializable]  
public class Address  
{  
    public string Street;  
    public string City;  
    // The older application ignores this data.  
    public string CountryField;  
}  
```  
  
```vb  
' Version 1 of the Address class.  
<Serializable> _  
Public Class Address  
    Public Street As String  
    Public City As String  
End Class  
  
' Version 2.0 of the Address class.  
<Serializable> _  
Public Class Address  
    Public Street As String  
    Public City As String  
    ' The older application ignores this data.  
    Public CountryField As String  
End Class  
```  
  
## <a name="tolerance-of-missing-data"></a>누락된 데이터의 허용치  
 필드에 <xref:System.Runtime.Serialization.OptionalFieldAttribute> 특성을 적용하여 해당 필드를 선택 사항으로 표시할 수 있습니다. deserialization 도중 선택적 데이터가 누락된 경우 serialization 엔진은 이를 무시하고 예외를 throw하지 않습니다. 따라서 형식의 이전 버전이 필요한 애플리케이션은 같은 형식의 새 버전이 필요한 애플리케이션에 데이터를 전송할 수 있습니다.  
  
 다음 예제에서는 `Address` 필드가 선택 사항으로 표시된 `CountryField` 클래스의 버전 2.0을 보여 줍니다. 이전 애플리케이션이 버전 2.0이 필요한 새 애플리케이션에 버전 1을 전송하면 데이터의 부재가 무시됩니다.  
  
```csharp  
[Serializable]  
public class Address  
{  
    public string Street;  
    public string City;  
  
    [OptionalField]  
    public string CountryField;  
}  
```  
  
```vb  
<Serializable> _  
Public Class Address  
    Public Street As String  
    Public City As String  
  
    <OptionalField> _  
    Public CountryField As String  
End Class  
```  
  
## <a name="serialization-callbacks"></a>serialization 콜백  
 콜백 serialization은 네 지점에서 serialization/deserialization 프로세스에 대한 후킹을 제공하는 메커니즘입니다.  
  
|특성|연결된 메서드가 호출된 경우|일반적인 용도|  
|---------------|------------------------------------------|-----------------|  
|<xref:System.Runtime.Serialization.OnDeserializingAttribute>|deserialization 이전*|선택적 필드에 대한 기본 값을 초기화합니다.|  
|<xref:System.Runtime.Serialization.OnDeserializedAttribute>|deserialization 후|선택된 필드 값을 다른 필드의 내용에 따라 수정합니다.|  
|<xref:System.Runtime.Serialization.OnSerializingAttribute>|serialization 이전|serialization을 준비합니다. 예를 들어 선택적 데이터 구조를 만듭니다.|  
|<xref:System.Runtime.Serialization.OnSerializedAttribute>|serialization 이후|serialization 이벤트를 로그합니다.|  
  
 \* 이 콜백은 deserialization 생성자(있는 경우)보다 먼저 호출됩니다.  
  
### <a name="using-callbacks"></a>콜백 사용  
 콜백을 사용하려면 <xref:System.Runtime.Serialization.StreamingContext> 매개 변수를 받는 메서드에 적절한 특성을 적용해야 합니다. 클래스당 하나의 메서드만 이들 각 속성으로 표시될 수 있습니다. 예를 들면 다음과 같습니다.  
  
```csharp  
[OnDeserializing]  
private void SetCountryRegionDefault(StreamingContext sc)  
{  
    CountryField = "Japan";  
}  
```  
  
```vb  
<OnDeserializing>  
Private Sub SetCountryRegionDefault(StreamingContext sc)  
    CountryField = "Japan";  
End Sub  
```  
  
 이 메서드의 용도 중에는 버전 관리 기능이 포함됩니다. deserialization 도중 필드에 대한 데이터가 없으면 선택적 필드가 올바르게 초기화되지 않을 수 있습니다. 이 문제는 올바른 값을 할당하는 메서드를 만들고 **OnDeserializingAttribute** 또는 **OnDeserializedAttribute** 특성을 메서드에 적용하여 수정할 수 있습니다.  
  
 다음 예제에서는 형식의 컨텍스트에서 메서드를 보여 줍니다. 애플리케이션의 이전 버전이 `Address` 클래스의 인스턴스를 애플리케이션의 새 버전으로 전송하면 `CountryField` 필드 데이터가 누락됩니다. 하지만 deserialization 이후에는 필드가 기본값인 "Japan"으로 설정됩니다.  
  
```csharp  
[Serializable]  
public class Address  
{  
    public string Street;  
    public string City;  
    [OptionalField]  
    public string CountryField;  
  
    [OnDeserializing]  
    private void SetCountryRegionDefault (StreamingContext sc)  
    {  
        CountryField = "Japan";  
    }  
}  
```  
  
```vb  
<Serializable> _  
Public Class Address  
    Public Street As String  
    Public City As String  
    <OptionalField> _  
    Public CountryField As String  
  
    <OnDeserializing> _  
    Private Sub SetCountryRegionDefault(StreamingContext sc)  
        CountryField = "Japan";  
    End Sub  
End Class  
```  
  
## <a name="the-versionadded-property"></a>VersionAdded 속성  
 **OptionalFieldAttribute**에는 **VersionAdded** 속성이 있습니다. .NET Framework의 버전 2.0에서는 이 속성이 사용되지 않습니다. 하지만 형식이 미래의 serialization 엔진과 호환되도록 이 속성을 올바르게 설정하는 것이 중요합니다.  
  
 속성은 해당 필드가 추가된 형식의 버전을 나타냅니다. 다음 예제처럼 형식이 수정될 때마다 1씩(2부터 시작) 증가되어야 합니다.  
  
```csharp  
// Version 1.0  
[Serializable]  
public class Person  
{  
    public string FullName;  
}  
  
// Version 2.0  
[Serializable]  
public class Person  
{  
    public string FullName;  
  
    [OptionalField(VersionAdded = 2)]  
    public string NickName;  
    [OptionalField(VersionAdded = 2)]  
    public DateTime BirthDate;  
}  
  
// Version 3.0  
[Serializable]  
public class Person  
{  
    public string FullName;  
  
    [OptionalField(VersionAdded=2)]  
    public string NickName;  
    [OptionalField(VersionAdded=2)]  
    public DateTime BirthDate;  
  
    [OptionalField(VersionAdded=3)]  
    public int Weight;  
}  
```  
  
```vb  
' Version 1.0  
<Serializable> _  
Public Class Person  
    Public FullName  
End Class  
  
' Version 2.0  
<Serializable> _  
Public Class Person  
    Public FullName As String  
  
    <OptionalField(VersionAdded := 2)> _  
    Public NickName As String  
    <OptionalField(VersionAdded := 2)> _  
    Public BirthDate As DateTime  
End Class  
  
' Version 3.0  
<Serializable> _  
Public Class Person  
    Public FullName As String  
  
    <OptionalField(VersionAdded := 2)> _  
    Public NickName As String  
    <OptionalField(VersionAdded := 2)> _  
    Public BirthDate As DateTime  
  
    <OptionalField(VersionAdded := 3)> _  
    Public Weight As Integer  
End Class  
```  
  
## <a name="serializationbinder"></a>SerializationBinder  
 서버와 클라이언트에서 서로 다른 버전의 클래스를 필요로 하므로 일부 사용자는 serialize 및 deserialize할 클래스를 제어해야 할 수 있습니다. <xref:System.Runtime.Serialization.SerializationBinder>는 serialization 및 deserialization 중에 사용되는 실제 형식을 제어하는 데 사용되는 추상 클래스입니다.  이 클래스를 사용하려면 <xref:System.Runtime.Serialization.SerializationBinder>에서 클래스를 파생시키고 <xref:System.Runtime.Serialization.SerializationBinder.BindToName%2A> 및 <xref:System.Runtime.Serialization.SerializationBinder.BindToType%2A> 메서드를 재정의합니다. 자세한 내용은 [serializationbinder를 사용 하 여 제어 하는 Serialization 및 Deserialization](../../../docs/framework/wcf/feature-details/controlling-serialization-and-deserialization-with-serializationbinder.md)합니다.  
  
## <a name="best-practices"></a>최선의 구현 방법  
 적절한 버전 관리 동작을 구현하려면 버전 간에 형식을 수정할 때 다음과 같은 규칙을 따릅니다.  
  
- serialize된 필드를 제거하지 마십시오.  
  
- 특성이 이전 버전에서 필드에 적용되지 않은 경우에는 <xref:System.NonSerializedAttribute> 특성을 필드에 적용하지 마십시오.  
  
- serialize된 필드의 이름이나 형식을 변경하지 마십시오.  
  
- 새 직렬화된 필드를 추가할 때 **OptionalFieldAttribute** 특성을 적용합니다.  
  
- **NonSerializedAttribute** 특성을 필드에서 제거할 때(이전 버전에서는 직렬화할 수 없었음) **OptionalFieldAttribute** 특성을 적용합니다.  
  
- 모든 선택적 필드에 대해 0 또는 **null**을 기본값으로 사용할 수 있는 경우 이외에는 serialization 콜백을 사용하여 의미 있는 기본값을 설정합니다.  
  
 형식이 미래의 serialization 엔진과 호환되도록 이 속성을 올바르게 설정하는 것이 중요합니다.  
  
- 항상 **OptionalFieldAttribute** 특성의 **VersionAdded** 속성을 올바르게 설정합니다.  
  
- 버전 관리 침해 방지  
  
## <a name="see-also"></a>참고자료

- <xref:System.SerializableAttribute>
- <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>
- <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>
- <xref:System.Runtime.Serialization.OptionalFieldAttribute.VersionAdded%2A>
- <xref:System.Runtime.Serialization.OptionalFieldAttribute>
- <xref:System.Runtime.Serialization.OnDeserializingAttribute>
- <xref:System.Runtime.Serialization.OnDeserializedAttribute>
- <xref:System.Runtime.Serialization.OnDeserializingAttribute>
- <xref:System.Runtime.Serialization.OnSerializedAttribute>
- <xref:System.Runtime.Serialization.StreamingContext>
- <xref:System.NonSerializedAttribute>
- [이진 serialization](binary-serialization.md)
