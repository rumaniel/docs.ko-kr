---
title: XML Serialization 소개
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XML serialization, about XML serialization
- ICollection interface, serializing
- XmlSerializer class, serializing
- serialization, about serialization
- DataSet class, serializing
- XML Schema, serializing
ms.assetid: 8c63200d-db63-4a03-a93d-21641623df62
ms.openlocfilehash: b1d91306c9cc9788046d19cc5de9e4712cdaa7e8
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67772539"
---
# <a name="introducing-xml-serialization"></a>XML Serialization 소개

serialization은 개체를 전송할 수 있는 형태로 변환하는 프로세스입니다. 예를 들어 개체를 serialize하고 클라이언트와 서버 사이에 HTTP를 사용하여 인터넷을 통해 전송할 수 있습니다. 반면 deserialization은 스트림에서 개체를 다시 생성합니다.

 XML serialization은 개체의 public 필드와 속성 값만 XML 스트림으로 serialize합니다. XML serialization에는 형식 정보가 포함되지 않습니다. 예를 들어 **Library** 네임스페이스에 존재하는 **Book** 개체가 있는 경우에는 같은 형식의 개체로 deserialize된다는 보장이 없습니다.

> [!NOTE]
> XML serialization은 메서드, 인덱서, 전용 필드 또는 읽기 전용 속성을 변환하지 않습니다. 단, 읽기 전용 컬렉션은 예외입니다. 공용 및 전용을 모두 포함하여 개체의 필드 및 속성을 모두 serialize하려면 XML serialization 대신 <xref:System.Runtime.Serialization.DataContractSerializer>를 사용하십시오.

 XML serialization의 핵심 클래스는 <xref:System.Xml.Serialization.XmlSerializer> 클래스이며 이 클래스에서 가장 중요한 메서드는 **직렬화** 및 **Deserialize** 메서드입니다. <xref:System.Xml.Serialization.XmlSerializer>는 C# 파일을 만들고 이를 .dll 파일로 컴파일하여 이 serialization을 수행합니다. .NET Framework 2.0에서 [XML 직렬 변환기 생성기 도구(Sgen.exe)](xml-serializer-generator-tool-sgen-exe.md)는 애플리케이션과 함께 배포하기 전에 이러한 serialization 어셈블리를 생성하고 시작 성능을 향상시키도록 디자인되었습니다. 생성 된 XML 스트림을 합니다 **XmlSerializer** World Wide Web Consortium (W3C)를 사용 하 여 규격이 [XML 스키마 정의 언어 (XSD) 1.0 권장 사항](https://www.w3.org/TR/xslt)합니다. 또한는 생성 된 데이터 형식은 호환 문서를 사용 하 여 "XML Schema Part 2: Datatypes입니다. "

 개체 내의 데이터는 클래스, 필드, 속성, 기본 형식, 배열 및 **XmlElement** 또는 **XmlAttribute** 개체 형태로 포함된 XML과 같은 프로그래밍 언어 구조를 통하여 설명됩니다. 특성으로 주석이 첨부된 클래스를 직접 만들거나, XML 스키마 정의 도구를 사용하여 기존 XML 스키마를 기반으로 클래스를 생성할 수도 있습니다.

 XML 스키마가 있는 경우, XML 스키마 정의 도구를 실행하여 스키마로 강력하게 형식화되고 주석이 첨부된 클래스 집합을 생성할 수 있습니다. 이러한 클래스의 인스턴스가 serialize될 때 생성된 XML은 XML 스키마를 준수합니다. 이러한 클래스를 사용하면 생성된 XML이 XML 스키마를 준수하도록 하면서 손쉽게 조작할 수 있는 개체 모델을 사용하여 프로그래밍할 수 있습니다. 이 방법은 **XmlReader** 및 **XmlWriter** 클래스와 같은 .NET Framework의 다른 클래스를 사용하여 XML 스트림을 구문 분석하고 쓰는 대신 사용할 수 있습니다. 자세한 내용은 [XML 문서 및 데이터](../../../docs/standard/data/xml/index.md)를 참조하세요. 이러한 클래스를 사용하면 모든 XML 스트림을 구문 분석할 수 있습니다. 반면 XML 스트림이 알려진 XML 스키마를 준수해야 하는 경우에는 **XmlSerializer**를 사용합니다.

 특성은 **XmlSerializer** 클래스로 생성된 XML 스트림을 제어하기 때문에 XML 스트림의 XML 네임스페이스, 요소 이름, 특성 이름 등을 설정할 수 있습니다. 이러한 특성에 대한 자세한 내용 및 이러한 특성이 XML serialization을 제어하는 방법에 대해서는 [특성을 사용하여 XML Serialization 제어](controlling-xml-serialization-using-attributes.md)를 참조하세요. 생성된 XML의 제어에 사용되는 특성의 표를 보려면 [XML Serialization을 제어하는 특성](attributes-that-control-xml-serialization.md)을 참조하세요.

 **XmlSerializer** 클래스는 개체를 추가적으로 직렬화하여 인코딩된 SOAP XML 스트림을 생성할 수 있습니다. 생성된 XML은 World Wide Web 컨소시엄 문서 "SOAP(Simple Object Access Protocol) 1.1"의 5단원을 따릅니다. 이 프로세스에 대 한 자세한 내용은 참조 하세요. [방법: SOAP 인코딩된 XML Stream 개체 직렬화](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)합니다. 생성된 XML을 제어하는 특성의 표를 보려면 [인코딩된 SOAP Serialization을 제어하는 특성](attributes-that-control-encoded-soap-serialization.md)을 참조하세요.

 **XmlSerializer** 클래스는 XML Web services에 의해 생성되고 XML Web services로 전달되는 SOAP 메시지를 생성합니다. SOAP 메시지를 제어하려면 XML Web services 파일(.asmx)의 클래스, 반환 값, 매개 변수 및 필드에 특성을 적용할 수 있습니다. XML Web services는 리터럴 또는 인코딩된 SOAP 스타일을 사용할 수 있으므로 "XML serialization을 제어하는 특성" 및 "인코딩된 SOAP serialization을 제어하는 특성"에 나열된 두 특성을 모두 사용할 수 있습니다. 특성을 사용하여 XML Web services에서 생성된 XML을 제어하는 방법에 대한 자세한 내용은 [XML Web Services의 XML Serialization](xml-serialization-with-xml-web-services.md)을 참조하세요. SOAP 및 XML Web services에 대 한 자세한 내용은 참조 하세요. [SOAP 메시지 형식을 사용자 지정](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dkwy2d72(v=vs.100))합니다.

## <a name="security-considerations-for-xmlserializer-applications"></a>XmlSerializer 애플리케이션에 대한 보안 고려 사항

**XmlSerializer**를 사용하는 응용 프로그램을 만들 때 다음과 같은 항목 및 해당 구현에 대해 알고 있어야 합니다.

- **XmlSerializer**는 C# 파일(.cs)을 만들어서 TEMP 환경 변수에 의해 이름 지정된 디렉터리의 .dll 파일로 컴파일합니다. 이 DLL을 사용하여 serialization이 수행됩니다.

  > [!NOTE]
  > 이러한 serialization 어셈블리는 SGen.exe 도구를 사용하여 미리 생성하고 서명할 수 있습니다. 웹 서비스의 서버에는 작동하지 않습니다. 즉, 클라이언트 및 수동 serialization 전용입니다.

  코드 및 DLL은 생성 및 컴파일 시점에서 악의적 프로세스에 취약합니다. Microsoft Windows NT 4.0 이상을 실행하는 컴퓨터에서 사용할 때는 둘 이상의 사용자가 TEMP 디렉터리를 공유할 수 있습니다. 두 계정의 보안 권한이 서로 다르고 높은 권한의 계정이 **XmlSerializer**를 사용하여 애플리케이션을 실행하는 경우 TEMP 디렉터리를 공유하는 것이 위험합니다. 이 경우 한 사용자가 컴파일된 .cs 또는 .dll 파일을 바꿔 컴퓨터의 보안을 침해할 수 있습니다. 이런 문제를 방지하기 위해 항상 컴퓨터의 각 계정마다 자체 프로필을 사용하도록 하십시오. 기본적으로 TEMP 환경 변수는 각 계정마다 서로 다른 디렉터리를 가리킵니다.

- 악의적 사용자가 XML 데이터의 연속 스트림을 웹 서버에 전송하면(서비스 거부 공격) **XmlSerializer**는 컴퓨터 리소스가 부족해질 때까지 데이터를 계속 처리합니다.

  IIS(인터넷 정보 서비스)를 실행하는 컴퓨터를 사용하여 애플리케이션이 IIS 내에서 실행되는 경우에는 이러한 종류의 공격이 제거됩니다. IIS에는 설정된 길이(기본값은 4KB)보다 긴 스트림은 처리하지 않는 기능이 있습니다. IIS를 사용하지 않는 애플리케이션을 만들고 **XmlSerializer**로 deserialize하는 경우에는 서비스 거부 공격을 차단하는 이와 비슷한 기능을 구현해야 합니다.

- **XmlSerializer**에서는 데이터를 직렬화하고 주어진 모든 형식을 사용하여 코드를 실행합니다.

  악의적 개체가 위협을 초래하는 방법에는 두 가지가 있습니다. 즉, 악의적 코드를 실행하거나 **XmlSerializer**에서 만들어진 C# 파일에 악의적 코드를 삽입할 수 있습니다. 첫 번째 경우 악의적 개체가 안전하지 않은 절차의 실행을 시도하면 코드 액세스 보안이 이러한 행위로 인한 손상 예방에 도움을 줍니다. 두 번째 경우 이론적으로는 악의적 개체가 **XmlSerializer**에서 만들어진 C# 파일에 코드를 삽입할 수 있는 가능성이 있습니다. 이 문제는 철저하게 검사되었고 이러한 공격이 수행될 가능성도 거의 없지만 알려지지 않은 형식과 신뢰할 수 없는 형식으로 데이터를 serialize하지 않아야 합니다.

- serialize된 중요한 데이터가 취약할 수 있습니다.

  후 합니다 **XmlSerializer** 데이터를 serialize XML 파일이 나 다른 데이터 저장소를 저장할 수 있습니다. 데이터 저장소를 다른 프로세스가 사용할 수 있거나 인트라넷 또는 인터넷에서 볼 수 있는 경우에는 데이터가 도난당하여 해로운 목적으로 사용될 수 있습니다. 예를 들어 신용카드 번호가 포함된 주문을 serialize하는 애플리케이션을 만드는 경우에는 데이터가 매우 중요합니다. 이런 문제를 방지하기 위해 항상 데이터 저장소를 보호하고 공개되지 않도록 조치를 취해야 합니다.

## <a name="serialization-of-a-simple-class"></a>간단한 클래스의 serialization

다음 코드 예제에서는 public 필드가 있는 기본 클래스를 보여 줍니다.

```vb
Public Class OrderForm
    Public OrderDate As DateTime
End Class
```

```csharp
public class OrderForm
{
    public DateTime OrderDate;
}
```

이 클래스의 인스턴스를 serialize하면 다음과 같을 수 있습니다.

```xml
<OrderForm>
    <OrderDate>12/12/01</OrderDate>
</OrderForm>
```

Serialization에 대한 다른 예제를 보려면 [XML Serialization 예제](examples-of-xml-serialization.md)를 참조하세요.

## <a name="items-that-can-be-serialized"></a>serialize할 수 있는 항목

**XmLSerializer** 클래스를 사용하여 직렬화할 수 있는 항목은 다음과 같습니다.

- 공용 클래스의 공용 읽기/쓰기 속성 및 필드

- **ICollection** 또는 **IEnumerable**을 구현하는 클래스

  > [!NOTE]
  > public 속성이 아니라 컬렉션만 serialize됩니다.

- **XmlElement** 개체

- **XmlNode** 개체

- **DataSet** 개체

 직렬화 또는 개체를 역직렬화 하는 방법에 대 한 자세한 내용은 참조 하세요. [방법: 개체를 직렬화](how-to-serialize-an-object.md) 고 [방법: 개체를 deserialize](how-to-deserialize-an-object.md)합니다.

## <a name="advantages-of-using-xml-serialization"></a>XML serialization 사용의 장점

합니다 **XmlSerializer** 클래스를 사용 하면 완료 하 고 융통성 있는 제어 개체를 XML로 serialize 할 때입니다. XML Web services를 만드는 경우 XML 출력이 특정 스키마를 따르도록 serialization을 제어하는 특성을 클래스와 멤버에 적용할 수 있습니다.

예를 들어 **XmlSerializer**를 사용하여 다음을 수행할 수 있습니다.

- 필드 또는 속성을 특성 또는 요소로 인코딩할 것인지 여부를 지정합니다.

- 사용할 XML 네임스페이스를 지정합니다.

- 필드 또는 속성 이름이 부적절한 경우 요소 또는 특성의 이름을 지정합니다.

XML serialization의 다른 장점은 생성되는 XML 스트림이 지정된 스키마를 따르기만 하면 개발하는 애플리케이션에 대한 제약 조건이 없다는 점입니다. 책을 설명하는 데 사용되는 스키마를 예로 들어보겠습니다. 이 경우 제목, 저자, 출판사 및 ISBN 번호 요소가 사용됩니다. XML 데이터를 책 주문 또는 책 재고 관리 등과 같은 원하는 방식으로 처리하는 애플리케이션을 개발할 수 있습니다. 두 경우 모두 유일한 요구 사항은 XML 스트림이 지정된 XSD(XML 스키마 정의 언어) 스키마를 준수해야 한다는 점입니다.

## <a name="xml-serialization-considerations"></a>XML serialization 고려 사항

다음은 **XmlSerializer** 클래스를 사용할 때 고려해야 할 사항입니다.

- Sgen.exe 도구는 최적의 성능을 위해 serialization 어셈블리를 생성하도록 디자인되었습니다.

- serialize된 데이터에는 데이터 자체와 클래스의 구조만 포함됩니다. 형식 ID와 어셈블리 정보는 포함되지 않습니다.

- public 속성 및 필드만 serialize될 수 있습니다. 속성에는 public 접근자(get 및 set 메서드)가 있어야 합니다. 공용이 아닌 데이터를 serialize해야 하는 경우에는 XML serialization이 아닌 <xref:System.Runtime.Serialization.DataContractSerializer> 클래스를 사용하십시오.

- 클래스를 serialize 할 수 매개 변수가 없는 생성자가 있어야 **XmlSerializer**합니다.

- 메서드는 serialize될 수 없습니다.

- **XmlSerializer**는 다음과 같이 특정 요구 사항을 충족하는 경우 **IEnumerable** 또는 **ICollection**을 서로 다르게 구현하는 클래스를 처리할 수 있습니다.

  **IEnumerable**을 구현하는 클래스는 단일 매개 변수를 사용하는 공용 **Add** 메서드를 구현해야 합니다. **Add** 메서드의 매개 변수는 **GetEnumerator** 메서드에서 반환된 **IEnumerator.Current** 속성에서 반환된 형식과 일관되어야 합니다(다형성).

  **IEnumerable**(예: **CollectionBase**) 이외에 **ICollection**을 구현하는 클래스에는 정수를 받는 공용 **Item**이 인덱싱된 속성(C#에서는 인덱서)이 있어야 하며 **integer** 형식의 공용 **Count** 속성이 있어야 합니다. **Add** 메서드로 전달되는 매개 변수는 **Item** 속성에서 반환된 형식과 같거나, 해당 기본 형식 중 하나여야 합니다.

  **ICollection**을 구현하는 클래스의 경우, 직렬화되는 값은 **GetEnumerator**를 호출하는 대신 인덱싱된 **Item** 속성에서 검색됩니다. 또한 다른 컬렉션 클래스(**ICollection**을 구현하는 클래스)를 반환하는 public 필드를 제외하고 public 필드와 속성은 직렬화되지 않습니다. 예제를 보려면 [XML Serialization 예제](examples-of-xml-serialization.md)를 참조하세요.

## <a name="xsd-data-type-mapping"></a>XSD 데이터 형식 매핑

W3C 문서 [XML Schema Part 2: Datatypes](https://www.w3.org/TR/xmlschema-2/) XML 스키마 정의 언어 (XSD) 스키마에서 허용 되는 간단한 데이터 형식을 지정 합니다. 이러한 형식(예: **int** 및 **decimal**)은 대부분 .NET Framework에 해당 데이터 형식이 있습니다. 하지만 일부 XML 데이터 형식에는 .NET Framework에 해당 데이터 형식이 없습니다(예: **NMTOKEN** 데이터 형식). 이러한 경우 [XML 스키마 정의 도구(Xsd.exe)](xml-schema-definition-tool-xsd-exe.md)를 사용하여 스키마에서 클래스를 생성하면 문자열 형식의 멤버에 적절한 특성이 적용되며 해당 **DataType** 속성이 XML 데이터 형식 이름으로 설정됩니다. 예를 들어 스키마에 XML 데이터 형식 **NMTOKEN**의 “MyToken” 요소가 포함된 경우, 다음 예제처럼 생성되는 클래스에 멤버가 포함될 수 있습니다.

```vb
<XmlElement(DataType:="NMTOKEN")> _
Public MyToken As String
```

```csharp
[XmlElement(DataType = "NMTOKEN")]
public string MyToken;
```

마찬가지로 특정 XML 스키마(XSD)를 준수해야 하는 클래스를 만드는 경우 적절한 특성을 적용하고 해당 **DataType** 속성을 원하는 XML 데이터 형식 이름으로 설정해야 합니다.

형식 매핑의 전체 목록에 대해서는 다음 특성 클래스에 대한 **DataType** 속성을 참조하세요.

- <xref:System.Xml.Serialization.SoapAttributeAttribute>

- <xref:System.Xml.Serialization.SoapElementAttribute>

- <xref:System.Xml.Serialization.XmlArrayItemAttribute>

- <xref:System.Xml.Serialization.XmlAttributeAttribute>

- <xref:System.Xml.Serialization.XmlElementAttribute>

- <xref:System.Xml.Serialization.XmlRootAttribute>

## <a name="see-also"></a>참고자료

- <xref:System.Xml.Serialization.XmlSerializer>
- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.IO.FileStream>
- [XML 및 SOAP serialization](xml-and-soap-serialization.md)
- [이진 serialization](binary-serialization.md)
- [serialization](index.md)
- <xref:System.Xml.Serialization.XmlSerializer>
- [XML serialization 예제](examples-of-xml-serialization.md)
- [방법: 개체 serialize](how-to-serialize-an-object.md)
- [방법: 개체 deserialize](how-to-deserialize-an-object.md)
