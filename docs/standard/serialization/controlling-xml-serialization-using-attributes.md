---
title: 특성을 사용하여 XML Serialization 제어
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- classes, serializing
- XML serialization, examples
- derived classes, serializing
- arrays, serializing
- XML serialization, attributes
- preventing serialization
- attributes [.NET Framework], XML serialization
- serialization, examples
- serialization, attributes
ms.assetid: 47d4c39d-30e1-4c7b-8a2e-301325390647
ms.openlocfilehash: 54660244c1b3cca8cb75539edbe23628b370afd5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61934509"
---
# <a name="controlling-xml-serialization-using-attributes"></a>특성을 사용하여 XML Serialization 제어

특성을 사용하여 개체의 XML serialization을 제어하거나 동일한 클래스 집합에서 대체 XML 스트림을 만들 수 있습니다. 대체 XML 스트림 만들기에 대 한 자세한 내용은 참조 하세요. [방법: XML Stream에 대 한 대체 요소 이름 지정](how-to-specify-an-alternate-element-name-for-an-xml-stream.md)합니다.

> [!NOTE]
> 생성 된 XML은 World Wide Web Consortium (W3C) 문서의 5 단원을 따라야 하는 경우 [단순 개체 액세스 프로토콜 (SOAP) 1.1](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/)에 나열 된 특성을 사용 하 여 [특성은 제어 인코딩된 SOAP Serialization](attributes-that-control-encoded-soap-serialization.md)합니다.

기본적으로 XML 요소 이름은 클래스 또는 멤버 이름으로 결정됩니다. `Book`이라는 간단한 클래스의 경우 이름이 `ISBN`인 필드는 다음 예제처럼 XML 요소 태그 \<ISBN>을 생성합니다.

```vb
Public Class Book
    Public ISBN As String
End Class
' When an instance of the Book class is serialized, it might
' produce this XML:
' <ISBN>1234567890</ISBN>.
```

```csharp
public class Book
{
    public string ISBN;
}
// When an instance of the Book class is serialized, it might
// produce this XML:
// <ISBN>1234567890</ISBN>.
```

요소에 새 이름을 지정하려면 이 기본 동작을 변경할 수 있습니다. 다음 코드에서는 <xref:System.Xml.Serialization.XmlElementAttribute.ElementName%2A>의 <xref:System.Xml.Serialization.XmlElementAttribute> 속성을 설정하여 특성을 통해 기본 동작을 변경하는 방법을 보여 줍니다.

```vb
Public Class TaxRates
   < XmlElement(ElementName = "TaxRate")> _
    Public ReturnTaxRate As Decimal
End Class
```

```csharp
public class TaxRates {
    [XmlElement(ElementName = "TaxRate")]
    public decimal ReturnTaxRate;
}
```

특성에 대한 자세한 내용은 [특성](../../../docs/standard/attributes/index.md)을 참조하세요. XML serialization을 제어하는 특성의 목록은 [XML Serialization을 제어하는 특성](attributes-that-control-xml-serialization.md)을 참조하세요.

## <a name="controlling-array-serialization"></a>배열 serialization 제어

<xref:System.Xml.Serialization.XmlArrayAttribute> 및 <xref:System.Xml.Serialization.XmlArrayItemAttribute> 특성은 배열의 serialization을 제어하도록 디자인되었습니다. 이러한 특성을 사용 하 여 제어할 수 있습니다 요소 이름, 네임 스페이스 및 XML 스키마 (XSD) 데이터 형식 (World Wide Web 컨소시엄 [www.w3.org] 문서에 정의 된 대로 "XML Schema Part 2: Datatypes ")입니다. 또한 배열에 포함될 수 있는 형식을 지정할 수도 있습니다.

<xref:System.Xml.Serialization.XmlArrayAttribute>는 배열이 serialize될 때 발생하는 바깥쪽 XML 요소의 속성을 결정합니다. 예를 들어 기본적으로 아래 배열을 serialize하면 `Employees`라는 이름의 XML 요소가 생성됩니다. `Employees` 요소에는 배열 형식 `Employee`를 따라 이름이 지정된 일련의 요소가 포함됩니다.

```vb
Public Class Group
    Public Employees() As Employee
End Class
Public Class Employee
    Public Name As String
End Class
```

```csharp
public class Group {
    public Employee[] Employees;
}
public class Employee {
    public string Name;
}
```

serialize된 인스턴스는 다음과 같을 수 있습니다.

```xml
<Group>
<Employees>
    <Employee>
        <Name>Haley</Name>
    </Employee>
</Employees>
</Group>
```

<xref:System.Xml.Serialization.XmlArrayAttribute>를 적용하여 다음과 같이 XML 요소의 이름을 변경할 수 있습니다.

```vb
Public Class Group
    <XmlArray("TeamMembers")> _
    Public Employees() As Employee
End Class
```

```csharp
public class Group {
    [XmlArray("TeamMembers")]
    public Employee[] Employees;
}
```

결과 XML은 다음과 같을 수 있습니다.

```xml
<Group>
<TeamMembers>
    <Employee>
        <Name>Haley</Name>
    </Employee>
</TeamMembers>
</Group>
```

반면 <xref:System.Xml.Serialization.XmlArrayItemAttribute>는 배열에 포함된 항목을 serialize하는 방법을 제어합니다. 특성은 배열을 반환하는 필드에 적용됩니다.

```vb
Public Class Group
    <XmlArrayItem("MemberName")> _
    Public Employee() As Employees
End Class
```

```csharp
public class Group {
    [XmlArrayItem("MemberName")]
    public Employee[] Employees;
}
```

결과 XML은 다음과 같을 수 있습니다.

```xml
<Group>
<Employees>
    <MemberName>Haley</MemberName>
</Employees>
</Group>
```

## <a name="serializing-derived-classes"></a>파생 클래스 serialize

<xref:System.Xml.Serialization.XmlArrayItemAttribute>의 다른 용도는 파생 클래스의 serialize를 가능하게 하는 것입니다. 예를 들어 `Manager`에서 파생되는 `Employee`라는 다른 클래스를 이전 예제에 추가할 수 있습니다. <xref:System.Xml.Serialization.XmlArrayItemAttribute>를 적용하지 않으면 파생된 클래스 형식이 인식되지 않기 때문에 코드는 런타임에 실패합니다. 이를 해결하려면 사용 가능한 각 형식(기본 및 파생)에 대해 <xref:System.Xml.Serialization.XmlArrayItemAttribute.Type%2A> 속성을 설정할 때마다 특성을 적용하여 두 번 적용합니다.

```vb
Public Class Group
    <XmlArrayItem(Type:=GetType(Employee)), _
    XmlArrayItem(Type:=GetType(Manager))> _
    Public Employees() As Employee
End Class
Public Class Employee
    Public Name As String
End Class
Public Class Manager
Inherits Employee
    Public Level As Integer
End Class
```

```csharp
public class Group {
    [XmlArrayItem(Type = typeof(Employee)),
    XmlArrayItem(Type = typeof(Manager))]
    public Employee[] Employees;
}
public class Employee {
    public string Name;
}
public class Manager:Employee {
    public int Level;
}
```

serialize된 인스턴스는 다음과 같을 수 있습니다.

```xml
<Group>
<Employees>
    <Employee>
        <Name>Haley</Name>
    </Employee>
    <Employee xsi:type = "Manager">
        <Name>Ann</Name>
        <Level>3</Level>
    <Employee>
</Employees>
</Group>
```

## <a name="serializing-an-array-as-a-sequence-of-elements"></a>배열을 요소 시퀀스로 serialize

다음과 같이 배열을 반환하는 필드에 <xref:System.Xml.Serialization.XmlElementAttribute>를 적용하여 배열을 XML 요소의 평면 시퀀스로 serialize할 수도 있습니다.

```vb
Public Class Group
    <XmlElement> _
    Public Employees() As Employee
End Class
```

```csharp
public class Group {
    [XmlElement]
    public Employee[] Employees;
}
```

serialize된 인스턴스는 다음과 같을 수 있습니다.

```xml
<Group>
<Employees>
    <Name>Haley</Name>
</Employees>
<Employees>
    <Name>Noriko</Name>
</Employees>
<Employees>
    <Name>Marco</Name>
</Employees>
</Group>
```

두 XML 스트림을 구분하는 다른 방법은 XML 스키마 정의 도구를 사용하여 컴파일된 코드에서 XML 스키마(XSD) 문서를 생성하는 것입니다. 도구 사용에 대한 자세한 내용은 [XML 스키마 정의 도구 및 XML serialization](the-xml-schema-definition-tool-and-xml-serialization.md)을 참조하세요. 필드에 특성이 적용되지 않은 경우 스키마는 다음 방식으로 요소를 설명합니다.

```xml
<xs:element minOccurs="0" maxOccurs ="1" name="Employees" type="ArrayOfEmployee" />
```

<xref:System.Xml.Serialization.XmlElementAttribute>가 필드에 적용되는 경우 결과 스키마는 다음과 같이 요소를 설명합니다.

```xml
<xs:element minOccurs="0" maxOccurs="unbounded" name="Employees" type="Employee" /> 
```

## <a name="serializing-an-arraylist"></a>ArrayList serialize

<xref:System.Collections.ArrayList> 클래스에는 다양한 개체의 컬렉션이 포함될 수 있습니다. 따라서 <xref:System.Collections.ArrayList>는 배열을 사용할 때 여러 번 사용할 수 있습니다. 하지만 형식화된 개체의 배열을 반환하는 필드를 만드는 대신 단일 <xref:System.Collections.ArrayList>를 반환하는 필드를 만들 수 있습니다. 하지만 배열과 마찬가지로 <xref:System.Xml.Serialization.XmlSerializer>에 포함된 개체 형식을 <xref:System.Collections.ArrayList>에 알려야 합니다. 이렇게 하려면 다음 예제처럼 <xref:System.Xml.Serialization.XmlElementAttribute>의 여러 인스턴스를 필드에 할당합니다.

```vb
Public Class Group
    <XmlElement(Type:=GetType(Employee)), _
    XmlElement(Type:=GetType(Manager))> _
    Public Info As ArrayList
End Class
```

```csharp
public class Group {
    [XmlElement(Type = typeof(Employee)), 
    XmlElement(Type = typeof(Manager))]
    public ArrayList Info;
}
```

## <a name="controlling-serialization-of-classes-using-xmlrootattribute-and-xmltypeattribute"></a>XmlRootAttribute 및 XmlTypeAttribute를 사용하여 클래스의 serialization 제어

클래스에 적용할 수 있는(클래스에만 적용 가능) <xref:System.Xml.Serialization.XmlRootAttribute> 및 <xref:System.Xml.Serialization.XmlTypeAttribute>의 두 특성이 있습니다. 이 두 특성은 매우 유사합니다. <xref:System.Xml.Serialization.XmlRootAttribute>는 serialize되었을 때 XML 문서의 열기 및 닫기 요소(즉, 루트 요소)를 나타내는 클래스인 하나의 클래스에만 적용될 수 있습니다. 반면 <xref:System.Xml.Serialization.XmlTypeAttribute>는 루트 클래스를 포함한 모든 클래스에 적용할 수 있습니다.

예를 들어 이전 예제에서 `Group` 클래스는 루트 클래스이며 이 클래스의 모든 public 필드와 속성은 XML 문서에서 찾을 수 있는 XML 요소가 됩니다. 따라서 하나의 루트 클래스만 있을 수 있습니다. <xref:System.Xml.Serialization.XmlRootAttribute>를 적용하면 <xref:System.Xml.Serialization.XmlSerializer>로 생성된 XML 스트림을 제어할 수 있습니다. 예를 들어 요소 이름과 네임스페이스를 변경할 수 있습니다.

<xref:System.Xml.Serialization.XmlTypeAttribute>를 사용하면 생성된 XML의 스키마를 제어할 수 있습니다. 이 기능은 XML Web services를 통해 스키마를 게시해야 할 때 유용합니다. 다음 예제에서는 <xref:System.Xml.Serialization.XmlTypeAttribute> 및 <xref:System.Xml.Serialization.XmlRootAttribute>를 같은 클래스에 적용합니다.

```vb
<XmlRoot("NewGroupName"), _
XmlType("NewTypeName")> _
Public Class Group
    Public Employees() As Employee
End Class
```

```csharp
[XmlRoot("NewGroupName")]
[XmlType("NewTypeName")]
public class Group {
    public Employee[] Employees;
}
```

이 클래스가 컴파일되고 XML 스키마 정의 도구가 스키마 생성에 사용되는 경우 `Group`을 설명하는 다음 XML을 볼 수 있습니다.

```xml
<xs:element name="NewGroupName" type="NewTypeName">
```

이와 반대로 클래스의 인스턴스를 serialize하면 `NewGroupName`이 XML 문서에 나타납니다.

```xml
<NewGroupName>
    . . .
</NewGroupName>
```

## <a name="preventing-serialization-with-the-xmlignoreattribute"></a>XmlIgnoreAttribute로 serialization 방지

public 속성이나 필드를 serialize할 필요가 없는 상황이 있을 수 있습니다. 예를 들어 메타데이터를 포함하기 위해 필드나 속성을 사용할 수 있습니다. 이러한 경우에는 <xref:System.Xml.Serialization.XmlIgnoreAttribute>를 필드 또는 속성에 적용하면 <xref:System.Xml.Serialization.XmlSerializer>가 이를 건너뜁니다.

## <a name="see-also"></a>참고자료

- [XML serialization을 제어하는 특성](attributes-that-control-xml-serialization.md)
- [인코딩된 SOAP serialization을 제어하는 특성](attributes-that-control-encoded-soap-serialization.md)
- [XML serialization 소개](introducing-xml-serialization.md)
- [XML serialization 예제](examples-of-xml-serialization.md)
- [방법: XML Stream에 대 한 대체 요소 이름 지정](how-to-specify-an-alternate-element-name-for-an-xml-stream.md)
- [방법: 개체 serialize](how-to-serialize-an-object.md)
- [방법: 개체 deserialize](how-to-deserialize-an-object.md)
