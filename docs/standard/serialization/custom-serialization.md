---
title: 사용자 지정 serialization
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- binary serialization, custom serialization
- custom serialization
- binary serialization, controlling
- OptionalFieldAttribute class, custom serialization
- ISerializable interface, custom serialization
- OnDeserializingAttribute class, custom serialization
- OnSerializedAttribute class, custom serialization
- serialization, custom serialization
- serialization, controlling
- OnDeserializedAttribute class, custom serialization
- OnSerializingAttribute class, custom serialization
ms.assetid: 12ed422d-5280-49b8-9b71-a2ed129c0384
ms.openlocfilehash: bd0010ccd3c7f6b2f4433fe8ce234bc806754260
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916237"
---
# <a name="custom-serialization"></a>사용자 지정 serialization
사용자 지정 serialization은 형식의 serialization 및 deserialization을 제어하는 프로세스입니다. serialization을 제어하면 형식의 핵심 기능에 영향을 주지 않고 다양한 형식 사이에 직렬화 및 deserialize할 수 있는 기능인 직렬화 호환성을 유지할 수 있습니다. 예를 들어 첫 번째 버전의 형식에는 두 개의 필드만 있을 수 있습니다. 다음 버전의 형식에는 몇 개의 필드가 더 추가될 수 있습니다. 하지만 응용 프로그램의 두 번째 버전에서는 여전히 두 형식을 모두 serialize 및 deserialize할 수 있어야 합니다. 다음 단원에서는 serialization을 제어하는 방법에 대해 설명합니다.

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]
  
> [!IMPORTANT]
> .NET Framework 4.0 이전 버전에서는 부분적으로 신뢰할 수 있는 어셈블리의 사용자 지정 사용자 데이터를 serialization하는 데 GetObjectData가 사용되었습니다. 버전 4.0부터 이 메서드는 부분적으로 신뢰할 수 있는 어셈블리에서 실행하지 못하도록 하는 <xref:System.Security.SecurityCriticalAttribute> 특성으로 표시됩니다. 이 문제를 해결하려면 <xref:System.Runtime.Serialization.ISafeSerializationData> 인터페이스를 구현합니다.  
  
## <a name="running-custom-methods-during-and-after-serialization"></a>serialization 도중 및 이후에 사용자 지정 메서드 실행  
 가장 효과적이고 쉬운 방법(.NET Framework의 버전 2.0에서 소개된 방법)은 serialization 도중과 이후에 데이터를 수정하는 데 사용되는 메서드에 다음 특성을 적용하는 것입니다.  
  
- <xref:System.Runtime.Serialization.OnDeserializedAttribute>  
  
- <xref:System.Runtime.Serialization.OnDeserializingAttribute>  
  
- <xref:System.Runtime.Serialization.OnSerializedAttribute>  
  
- <xref:System.Runtime.Serialization.OnSerializingAttribute>  
  
 이러한 특성을 통해 형식은 serialization 및 deserialization 프로세스의 네 단계 중 하나 또는 모두에 참여할 수 있습니다. 특성은 각 단계에서 호출되어야 하는 형식의 메서드를 지정합니다. 메서드는 serialization 스트림에 액세스할 수 없지만 대신 serialization 이전과 이후 또는 deserialization 이전과 이후에 개체를 변경할 수 있도록 허용합니다. 특성은 형식 상속 계층의 모든 수준에 적용될 수 있으며 각 메서드는 계층 구조의 기본부터 가장 많이 파생된 단계까지 호출됩니다. 이 메커니즘에서는 가장 많이 파생된 구현에서 serialization 및 deserialization을 담당하도록 하여 <xref:System.Runtime.Serialization.ISerializable> 인터페이스의 구현으로 인한 모든 문제와 복잡성을 피합니다. 또한 포맷터는 이 메커니즘을 통해 필드의 입력과 serialization 스트림에서의 검색을 무시할 수 있습니다. serialization 및 deserialization 제어에 대한 자세한 내용과 예제를 보려면 이전 링크를 클릭하십시오.  
  
 또한 새 필드를 기존 serialize 가능한 형식에 추가할 때 <xref:System.Runtime.Serialization.OptionalFieldAttribute> 특성을 필드에 적용합니다. <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 및 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>는 새 필드가 없는 스트림이 처리될 때 필드가 없어도 이를 무시합니다.  
  
## <a name="implementing-the-iserializable-interface"></a>ISerializable 인터페이스 구현  
 serialization을 제어하는 다른 방법은 개체에 <xref:System.Runtime.Serialization.ISerializable> 인터페이스를 구현하는 것입니다. 하지만 이전 단원의 메서드가 이 메서드를 대체하여 serialization을 제어합니다.  
  
 또한 [Serializable](xref:System.SerializableAttribute) 특성으로 표시되어 있으며 클래스 수준 또는 생성자에 선언적 또는 명령적 보안이 있는 클래스에는 기본 serialization을 사용하지 않아야 합니다. 대신 이러한 클래스는 항상 <xref:System.Runtime.Serialization.ISerializable> 인터페이스를 구현해야 합니다.  
  
 <xref:System.Runtime.Serialization.ISerializable> 구현에는 개체가 deserialize될 때 사용되는 특별한 생성자 및 `GetObjectData` 메서드가 포함되어 있습니다. 다음 샘플 코드에서는 이전 단원의 <xref:System.Runtime.Serialization.ISerializable> 클래스에서 `MyObject`을 구현하는 방법을 보여 줍니다.  
  
```csharp
[Serializable]
public class MyObject : ISerializable
{
    public int n1;
    public int n2;
    public String str;

    public MyObject()
    {
    }

    protected MyObject(SerializationInfo info, StreamingContext context)
    {
      n1 = info.GetInt32("i");
      n2 = info.GetInt32("j");
      str = info.GetString("k");
    }

    [SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter = true)]
    public virtual void GetObjectData(SerializationInfo info, StreamingContext context)
    {
        info.AddValue("i", n1);
        info.AddValue("j", n2);
        info.AddValue("k", str);
    }
}
```

```vb
<Serializable()>  _
Public Class MyObject
    Implements ISerializable
    Public n1 As Integer
    Public n2 As Integer
    Public str As String

    Public Sub New()
    End Sub

    Protected Sub New(ByVal info As SerializationInfo, ByVal context As StreamingContext)
        n1 = info.GetInt32("i")
        n2 = info.GetInt32("j")
        str = info.GetString("k")
    End Sub 'New

    <SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter := True)> _
    Public Overridable Sub GetObjectData(ByVal info As SerializationInfo, ByVal context As StreamingContext)
        info.AddValue("i", n1)
        info.AddValue("j", n2)
        info.AddValue("k", str)
    End Sub
End Class
```  
  
 serialization 도중 **GetObjectData**가 호출될 때는 메서드 호출과 함께 제공된 <xref:System.Runtime.Serialization.SerializationInfo>를 채워야 합니다. 이름 및 값 쌍으로 serialize될 변수를 추가합니다. 모든 텍스트를 이름으로 사용할 수 있습니다. deserialization 도중 개체를 복원하기 위한 충분한 데이터가 serialize된 경우 <xref:System.Runtime.Serialization.SerializationInfo>에 추가되는 멤버 변수를 자유롭게 결정할 수 있습니다. 이 멤버 변수가 <xref:System.Runtime.Serialization.ISerializable>을 구현하는 경우 파생 클래스는 기본 개체의 **GetObjectData** 메서드를 호출해야 합니다.  
  
 serialization을 통해 다른 코드가 일반적으로 액세스할 수 없는 개체 인스턴스 데이터를 보거나 수정할 수 있습니다. 따라서 serialization을 수행하는 코드에는 <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter> 플래그가 지정된 [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute)이 필요합니다. 기본 정책에 따라 이 권한은 인터넷에서 다운로드한 코드나 인트라넷 코드에는 부여되지 않고 로컬 컴퓨터에 있는 코드에만 부여됩니다. <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter> 플래그가 지정된 [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute)을 요청하거나 전용 데이터 보호에 특별히 도움이 되는 다른 권한을 요청하여 **GetObjectData** 메서드를 명시적으로 보호해야 합니다.  
  
 전용 필드에 민감한 정보가 저장된 경우 데이터를 보호하려면 **GetObjectData**에 대한 적절한 권한을 요청해야 합니다. **SerializationFormatter** 플래그가 지정된 [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute)이 부여된 코드는 전용 필드에 저장된 데이터를 보고 수정할 수 있습니다. 이 [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute)이 부여된 악의적 호출자가 숨겨진 디렉터리 위치나 부여된 권한 등의 데이터를 볼 수 있으며 데이터를 사용하여 컴퓨터의 보안 취약성을 악용할 수 있습니다. 지정할 수 있는 보안 권한 플래그의 전체 목록은 [SecurityPermissionFlag 열거형](xref:System.Security.Permissions.SecurityPermissionFlag)을 참조하세요.  
  
 <xref:System.Runtime.Serialization.ISerializable>을 클래스에 추가한 경우 **GetObjectData** 및 특수 생성자를 모두 구현해야 합니다. **GetObjectData**가 누락되면 컴파일러가 이를 경고합니다. 하지만 생성자의 구현을 강제할 수 없기 때문에 생성자가 없는 경우에는 경고가 제공되지 않으며 생성자 없이 클래스를 deserialize하려고 하면 예외가 throw됩니다.  
  
 잠재적 보안 문제와 버전 관리 문제를 해결하기 위해 <xref:System.Runtime.Serialization.ISerializationSurrogate.SetObjectData%2A> 메서드 대신 현재 디자인을 사용하는 것이 좋습니다. 예를 들어 `SetObjectData` 메서드는 인터페이스의 일부로 정의된 경우 public이어야 합니다. 따라서 사용자는 **SetObjectData** 메서드가 여러 번 호출되는 것을 막기 위한 코드를 작성해야 합니다. 그러지 않으면 작업을 실행하는 프로세스에서 개체에 대해 **SetObjectData** 메서드를 호출하는 악의적 애플리케이션으로 인해 문제가 발생할 수 있습니다.  
  
 deserialization 도중 <xref:System.Runtime.Serialization.SerializationInfo>가 이런 목적으로 제공되는 생성자를 사용하여 클래스로 전달됩니다. 생성자에 적용된 모든 표시 제약 조건은 개체가 deserialize될 때 무시됩니다. 따라서 클래스를 public, protected, internal 또는 private로 표시할 수 있습니다. 하지만 클래스가 sealed가 아니면 생성자를 보호하는 것이 좋으며, 이 경우 생성자를 private로 표시해야 합니다. 또한 생성자는 엄격한 입력 유효성 검사를 수행해야 합니다. 악의적 코드에 의해 오용되는 것을 피하기 위해 생성자는 다른 모든 생성자를 사용하여 클래스의 인스턴스를 얻는 데 필요한 것과 동일한 보안 검사 및 권한을 적용해야 합니다. 이 권장 사항을 따르지 않으면 악의적 코드가 개체를 미리 직렬화하고, <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter> 플래그가 지정된 [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute)을 가진 컨트롤을 가져오고, public 생성자를 사용한 표준 인스턴스 생성 도중 적용된 모든 보안을 우회하여 클라이언트 컴퓨터의 개체를 deserialize할 수 있습니다.  
  
 개체의 상태를 복원하려면 serialization 도중 사용된 이름을 사용하여 <xref:System.Runtime.Serialization.SerializationInfo>에서 변수의 값을 검색하면 됩니다. 기본 클래스가 <xref:System.Runtime.Serialization.ISerializable>을 구현하는 경우 기본 생성자를 호출하여 기본 개체가 변수를 복원할 수 있도록 해야 합니다.  
  
 <xref:System.Runtime.Serialization.ISerializable>을 구현하는 클래스에서 새 클래스를 파생하는 경우 파생 클래스는 직렬화되어야 하는 변수가 있는 경우 **GetObjectData** 메서드뿐만 아니라 생성자도 구현해야 합니다. 다음 코드 예제에서는 이전에 보여 준 `MyObject` 클래스를 사용하여 이 작업을 수행하는 방법을 보여 줍니다.  
  
```csharp
[Serializable]
public class ObjectTwo : MyObject
{
    public int num;

    public ObjectTwo()
      : base()
    {
    }

    protected ObjectTwo(SerializationInfo si, StreamingContext context)
      : base(si, context)
    {
        num = si.GetInt32("num");
    }

    [SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter = true)]
    public override void GetObjectData(SerializationInfo si, StreamingContext context)
    {
        base.GetObjectData(si,context);
        si.AddValue("num", num);
    }
}
```

```vb
<Serializable()>  _
Public Class ObjectTwo
    Inherits MyObject
    Public num As Integer

    Public Sub New()

    End Sub

    Protected Sub New(ByVal si As SerializationInfo, _
    ByVal context As StreamingContext)
        MyBase.New(si, context)
        num = si.GetInt32("num")
    End Sub

    <SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter := True)> _
    Public Overrides Sub GetObjectData(ByVal si As SerializationInfo, ByVal context As StreamingContext)
        MyBase.GetObjectData(si, context)
        si.AddValue("num", num)
    End Sub
End Class
```  
  
 deserialization 생성자에서 반드시 기본 클래스를 호출해야 합니다. 이렇게 하지 않으면 기본 클래스의 생성자가 호출되지 않으며 deserialization 후 개체가 완전히 생성되지 않습니다.  
  
 개체는 내부에서 외부로 재생성됩니다. deserialization 도중 메서드를 호출하면 원하지 않는 파생 효과가 발생할 수 있습니다. 호출된 메서드가 호출 시점에서 deserialize되지 않은 개체 참조를 참조할 수 있기 때문입니다. deserialize되는 클래스가 <xref:System.Runtime.Serialization.IDeserializationCallback>을 구현하는 경우 전체 개체 그래프가 deserialize될 때 <xref:System.Runtime.Serialization.IDeserializationCallback.OnDeserialization*> 메서드가 자동으로 호출됩니다. 이 시점에서 참조된 모든 자식 개체가 완전히 복원됩니다. 해시 테이블은 이벤트 수신기를 사용하지 않고 deserialize하기 어려운 클래스의 예입니다. deserialization 도중 키와 값 쌍을 검색하는 것은 쉽지만, 해시 테이블에서 파생된 클래스가 deserialize되었다는 보장이 없기 때문에 해당 개체를 다시 해시 테이블에 추가하면 문제가 발생할 수 있습니다. 따라서 이 단계에서 해시 테이블에 대해 메서드를 호출하지 않는 것이 좋습니다.  
  
## <a name="see-also"></a>참고자료

- [이진 serialization](binary-serialization.md)
- [XML 및 SOAP serialization](xml-and-soap-serialization.md)
- [보안 및 Serialization](../../../docs/framework/misc/security-and-serialization.md)
