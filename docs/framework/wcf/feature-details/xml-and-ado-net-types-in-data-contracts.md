---
title: 데이터 계약의 XML 및 ADO.NET 형식
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c2ce8461-3c15-4c41-8c81-1cb78f5b59a6
ms.openlocfilehash: 0d052c0f178c2dc6e2eb5a740faa42239fb91068
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64637226"
---
# <a name="xml-and-adonet-types-in-data-contracts"></a>데이터 계약의 XML 및 ADO.NET 형식
Windows Communication Foundation (WCF) 데이터 계약 모델에는 직접 XML을 나타내는 특정 형식을 지원 합니다. 이러한 형식이 XML에 serialize되면 serializer는 추가 처리 없이 이러한 형식의 XML 콘텐츠를 씁니다. 지원되는 형식에는 <xref:System.Xml.XmlElement>을 구현하는 형식, <xref:System.Xml.XmlNode> 및 `XmlNode`의 배열이 있습니다. 단, <xref:System.Xml.Serialization.IXmlSerializable> 형식 자체는 지원되지 않습니다. <xref:System.Data.DataSet> 및 <xref:System.Data.DataTable> 형식은 형식화된 데이터 세트과 마찬가지로 데이터베이스 프로그래밍에 자주 사용됩니다. 이러한 형식은 `IXmlSerializable` 인터페이스를 구현하므로 데이터 계약 모델에서 serialize할 수 있습니다. 이러한 형식에 대한 몇 가지 특별한 고려 사항은 이 항목의 끝부분에 나와 있습니다.  
  
## <a name="xml-types"></a>XML 형식  
  
### <a name="xml-element"></a>XML 요소  
 `XmlElement` 형식은 XML 콘텐츠를 사용하여 serialize됩니다. 예를 들어, 다음 형식을 사용할 수 있습니다.  
  
 [!code-csharp[DataContractAttribute#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/datacontractattribute/cs/overview.cs#4)]
 [!code-vb[DataContractAttribute#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/datacontractattribute/vb/overview.vb#4)]  
  
 이 형식은 다음과 같이 XML로 serialize됩니다.  
  
```xml  
<MyDataContract xmlns="http://schemas.contoso.com">  
    <myDataMember>  
        <myElement xmlns="" myAttribute="myValue">  
            myContents  
        </myElement>  
    </myDataMember>  
</MyDataContract>  
```  
  
 래퍼 데이터 멤버 요소 `<myDataMember>`가 여전히 있음을 알 수 있습니다. 데이터 계약 모델에서 이 요소를 제거할 수 있는 방법은 없으며, 이 모델을 처리하는 serializer(<xref:System.Runtime.Serialization.DataContractSerializer> 및 <xref:System.Runtime.Serialization.NetDataContractSerializer>)가 특수 특성을 이 래퍼 요소로 내보낼 수 있습니다. 이러한 특성에는 표준 XML 스키마 인스턴스 "nil" 특성(`XmlElement`가 `null`인 경우 허용) 및 "type" 특성(`XmlElement`가 다형적으로 사용되는 경우 허용)이 포함됩니다. 또한 다음 XML 특성은 WCF에 따라 다릅니다. "Id", "Ref", "Type" 및 "Assembly"를 선택 합니다. 이러한 특성을 내보내서 개체 그래프 유지 모드가 활성화된 상태로 또는 `XmlElement`로 <xref:System.Runtime.Serialization.NetDataContractSerializer> 사용을 지원할 수 있습니다. (개체 그래프 유지 모드에 대 한 자세한 내용은 참조 하세요. [Serialization 및 Deserialization](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md).)  
  
 `XmlElement`의 배열 또는 컬렉션이 허용되며 다른 배열이나 컬렉션과 같이 처리됩니다. 즉, 전체 컬렉션에 대한 래퍼 요소와 배열의 각 `<myDataMember>`에 대한 개별 래퍼 요소(이전 예제의 `XmlElement`와 유사)가 있습니다.  
  
 deserialize할 때 deserializer는 들어오는 XML에서 `XmlElement`를 만듭니다. 또한 deserializer는 유효한 부모 <xref:System.Xml.XmlDocument>를 제공합니다.  
  
 `XmlElement`로 deserialize되는 XML 단편은 사용할 모든 접두사를 정의하고 상위 요소의 접두사 정의를 사용하지 않습니다. 이는 `DataContractSerializer`를 사용하여 `DataContractSerializer`가 아닌 다른 소스의 XML에 액세스하는 경우에만 문제가 됩니다.  
  
 와 함께 사용할 경우는 `DataContractSerializer`는 `XmlElement` 형식의 데이터 멤버에만 다형적으로 할당할 수 있습니다 <xref:System.Object>합니다. <xref:System.Collections.IEnumerable>가 `XmlElement`을 구현할지라도 이를 컬렉션 형식으로 사용할 수 없으며 <xref:System.Collections.IEnumerable> 데이터 멤버에 할당할 수 없습니다. 모든 다형적 할당과 마찬가지로 합니다 `DataContractSerializer` 내보내는 데이터 계약 이름 결과 XML이 예에서는 "XmlElement"에 "http://schemas.datacontract.org/2004/07/System.Xml" 네임 스페이스입니다.  
  
 `NetDataContractSerializer`에서는 `XmlElement` 또는 `Object`에 대한 `IEnumerable`의 모든 유효한 다형적 할당이 지원됩니다.  
  
 다형적으로 할당되는지 여부에 관계없이 이러한 serializer를 `XmlElement`에서 파생된 형식과 함께 사용하지 마세요.  
  
### <a name="array-of-xmlnode"></a>XmlNode 배열  
 <xref:System.Xml.XmlNode> 배열의 사용 방식은 `XmlElement` 사용 방식과 매우 유사합니다. `XmlNode`의 배열을 사용하면 `XmlElement`를 사용할 때보다 유연성이 향상됩니다. 데이터 멤버 래핑 요소 내에 여러 개의 요소를 쓸 수 있습니다. 또한 데이터 멤버 래핑 요소 내에 요소 이외의 콘텐츠(예: XML 주석)를 삽입할 수도 있으며, 마지막으로 래핑 데이터 멤버 요소에 특성을 삽입할 수 있습니다. 이러한 작업은 `XmlNode`의 배열을 `XmlNode`의 특정 파생 클래스(예: <xref:System.Xml.XmlAttribute>, `XmlElement` 또는 <xref:System.Xml.XmlComment>)로 채워서 수행할 수 있습니다. 예를 들어, 다음 형식을 사용할 수 있습니다.  
  
 [!code-csharp[DataContractAttribute#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/datacontractattribute/cs/overview.cs#5)]
 [!code-vb[DataContractAttribute#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/datacontractattribute/vb/overview.vb#5)]  
  
 serialize한 후의 결과 XML은 다음 코드와 유사합니다.  
  
```xml  
<MyDataContract xmlns="http://schemas.contoso.com">  
  <myDataMember myAttribute="myValue">  
     <!--myComment-->  
     <myElement xmlns="" myAttribute="myValue">  
 myContents  
     </myElement>  
     <myElement xmlns="" myAttribute="myValue">  
       myContents  
     </myElement>  
  </myDataMember>  
</MyDataContract>  
```  
  
 데이터 멤버 래퍼 요소 `<myDataMember>`에는 특성, 주석 및 두 개의 요소가 포함되어 있습니다. 이들은 serialize된 4개의 `XmlNode` 인스턴스입니다.  
  
 잘못된 XML을 생성하는 `XmlNode` 배열은 serialize할 수 없습니다. 예를 들어 첫 번째 인스턴스가 `XmlNode`이고 두 번째 인스턴스가 `XmlElement`인 두 <xref:System.Xml.XmlAttribute> 인스턴스의 배열은 이 시퀀스가 올바른 XML 인스턴스에 해당하지 않고 특성을 연결할 위치가 없으므로 잘못되었습니다.  
  
 `XmlNode` 배열을 deserialize하면 노드가 만들어지고 들어오는 XML의 정보로 채워집니다. 또한 deserializer는 유효한 부모 <xref:System.Xml.XmlDocument>를 제공합니다. 래퍼 데이터 멤버 요소의 모든 특성을 포함 하 여 모든 노드가 deserialize 됩니다 있지만 WCF 직렬 변환기 (예: 다형적 할당을 나타내는 데 사용 되는 특성)에서 배치 특성을 제외 합니다. XML 단편에서 모든 네임스페이스 접두사를 정의하는 방법에 대한 경고가 `XmlNode`를 deserialize하는 경우와 마찬가지로 `XmlElement` 배열의 deserialization에 적용됩니다.  
  
 개체 그래프 유지가 설정된 상태로 serializer를 사용하는 경우 개별 `XmlNode` 인스턴스가 아니라 `XmlNode` 배열 수준에서만 개체 동일성이 유지됩니다.  
  
 노드 중 하나 이상이 `XmlNode`로 설정된 `null` 배열은 serialize하지 마세요. 전체 배열 멤버가 `null`일 수는 있지만 배열에 포함된 개별 `XmlNode`가 null일 수는 없습니다. 전체 배열 멤버가 null이면 래퍼 데이터 멤버 요소에 null임을 나타내는 특수 특성이 포함됩니다. deserialize할 때는 전체 배열 멤버가 null이 됩니다.  
  
 `XmlNode`의 일반 배열만 serializer에서 특별하게 처리됩니다. `XmlNode`가 포함된 다른 컬렉션 형식으로 선언된 데이터 멤버 또는 `XmlNode`에서 파생된 형식의 배열로 선언된 데이터 멤버는 특별하게 처리되지 않습니다. 따라서 이러한 데이터 멤버가 serialization에 대한 다른 조건 중 하나를 충족하지 않으면 일반적으로 데이터 멤버를 serialize할 수 없습니다.  
  
 `XmlNode` 배열이나 배열의 컬렉션은 허용됩니다. 전체 컬렉션에 대한 래퍼 요소와 외부 배열 또는 컬렉션의 각 `<myDataMember>` 배열의 개별 래퍼 요소(이전 예제의 `XmlNode`와 유사)가 있습니다.  
  
 <xref:System.Array>의 `Object` 형식이나 `Array`의 `IEnumerable` 형식 데이터 멤버를 `XmlNode` 인스턴스로 채우면 데이터 멤버가 `Array` 인스턴스의 `XmlNode`로 처리되지 않습니다. 각 배열 멤버는 개별적으로 serialize됩니다.  
  
 `DataContractSerializer`와 함께 사용되는 경우 `XmlNode`는 `Object` 형식의 데이터 멤버에만 다형적으로 할당할 수 있습니다. `IEnumerable`가 `XmlNode`을 구현할지라도 이 배열을 컬렉션 형식으로 사용할 수 없으며 `IEnumerable` 데이터 멤버에 할당할 수 없습니다. 모든 다형적 할당과 마찬가지로 합니다 `DataContractSerializer` 내보내는 데이터 계약 이름은 결과 XML이 예에서는 "ArrayOfXmlNode"에 "http://schemas.datacontract.org/2004/07/System.Xml" 네임 스페이스입니다. 와 함께 사용할 경우는 `NetDataContractSerializer`, 모든 유효한 할당이 `XmlNode` 배열이 지원 됩니다.  
  
### <a name="schema-considerations"></a>스키마 고려 사항  
 XML 형식의 스키마 매핑에 대 한 자세한 내용은 참조 하세요 [데이터 계약 스키마 참조](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)합니다. 이 단원에서는 중요한 사항을 요약하여 설명합니다.  
  
 `XmlElement` 형식의 데이터 멤버는 다음 익명 형식을 사용하여 정의된 요소에 매핑됩니다.  
  
```xml  
<xsd:complexType>  
   <xsd:sequence>  
      <xsd:any minOccurs="0" processContents="lax" />  
   </xsd:sequence>  
</xsd:complexType>  
```  
  
 `XmlNode`의 Array 형식 데이터 멤버는 다음 익명 형식을 사용하여 정의된 요소에 매핑됩니다.  
  
```xml  
<xsd:complexType mixed="true">  
   <xsd:sequence>  
      <xsd:any minOccurs="0" maxOccurs="unbounded" processContents="lax" />  
   </xsd:sequence>  
   <xsd:anyAttribute/>  
</xsd:complexType>  
```  
  
## <a name="types-implementing-the-ixmlserializable-interface"></a>IXmlSerializable 인터페이스를 구현하는 형식  
 `IXmlSerializable` 인터페이스를 구현하는 형식은 `DataContractSerializer`에서 완전히 지원됩니다. 이러한 형식의 스키마를 제어하려면 <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> 특성을 항상 이러한 형식에 적용해야 합니다.  
  
 `IXmlSerializable`을 구현하는 형식에는 임의의 콘텐츠를 나타내는 형식, 단일 요소를 나타내는 형식 및 레거시 <xref:System.Data.DataSet> 형식 등 세 가지가 있습니다.  
  
- 콘텐츠 형식은 `XmlSchemaProviderAttribute` 특성에 지정된 스키마 공급자 메서드를 사용합니다. 이 메서드는 `null`을 반환하지 않으며 특성의 <xref:System.Xml.Serialization.XmlSchemaProviderAttribute.IsAny%2A> 속성은 기본값인 `false`로 유지됩니다. 이는 `IXmlSerializable` 형식의 가장 일반적인 사용입니다.  
  
- 요소 형식은 `IXmlSerializable` 형식이 루트 요소 이름을 제어해야 하는 경우에 사용됩니다. 형식을 요소 형식으로 표시하려면 <xref:System.Xml.Serialization.XmlSchemaProviderAttribute.IsAny%2A> 특성의 <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> 속성을 `true`로 설정하거나 스키마 공급자 메서드의 null을 반환합니다. 스키마 공급자 메서드 사용은 요소 형식의 옵션이며 `XmlSchemaProviderAttribute`에 메서드 이름 대신 null을 지정할 수 있습니다. 그러나 `IsAny`가 `true`이고 스키마 공급자 메서드가 지정된 경우 메서드는 null을 반환해야 합니다.  
  
- 레거시 <xref:System.Data.DataSet> 형식은 `IXmlSerializable` 특성으로 표시되지 않은 `XmlSchemaProviderAttribute` 형식입니다. 대신 이러한 형식은 스키마 생성 시 <xref:System.Xml.Serialization.IXmlSerializable.GetSchema%2A> 메서드를 사용합니다. 이 패턴은 `DataSet` 형식에 사용되고 해당 형식화된 데이터 세트은 이전 버전의 .NET Framework에서는 클래스를 파생하지만 현재는 더 이상 사용되지 않으며 레거시 용도로만 지원됩니다. 이 패턴을 사용하는 대신 `XmlSchemaProviderAttribute`를 항상 `IXmlSerializable` 형식에 적용하세요.  
  
### <a name="ixmlserializable-content-types"></a>IXmlSerializable 콘텐츠 형식  
 이전에 정의한 콘텐츠 형식이며 `IXmlSerializable`을 구현하는 형식의 데이터 멤버를 serialize할 때 serializer는 데이터 멤버의 래퍼 요소를 쓰고 제어를 <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> 메서드에 전달합니다. <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> 구현은 특성을 래퍼 요소에 추가하는 것을 포함하여 모든 XML을 쓸 수 있습니다. `WriteXml`이 완료되면 serializer는 요소를 닫습니다.  
  
 `IXmlSerializable`을 구현하고 이전에 정의된 콘텐츠 형식인 형식의 데이터 멤버를 deserialize할 때 deserializer는 데이터 멤버의 래퍼 요소에 XML 판독기를 배치하고 제어를 <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> 메서드에 전달합니다. 메서드는 시작 및 끝 태그를 비롯하여 전체 요소를 읽어야 합니다. `ReadXml` 코드는 요소가 비어 있는 경우를 처리해야 합니다. 또한 `ReadXml` 구현은 래퍼 요소의 이름이 특정한 방식으로 지정되는 데 의존해서는 안 됩니다. serializer에서 선택되는 이름은 다양할 수 있습니다.  
  
 `IXmlSerializable` 형식의 데이터 멤버 등에 다형적으로 <xref:System.Object> 콘텐츠 형식을 할당할 수 있습니다. 또한 형식 인스턴스는 null일 수 있습니다. 마지막으로 개체 그래프 유지가 활성화된 상태 및 `IXmlSerializable`로 <xref:System.Runtime.Serialization.NetDataContractSerializer>을 사용할 수 있습니다. 이러한 모든 기능은 필요한 특정 특성을 래퍼 요소에 연결 하는 WCF serializer ("nil" 및 "type" XML 스키마 인스턴스 네임 스페이스 및 "Id", "Ref", "Type" 및 "Assembly"의 WCF 관련 네임 스페이스에서).  
  
#### <a name="attributes-to-ignore-when-implementing-readxml"></a>ReadXml을 구현할 때 무시할 특성  
 제어를 `ReadXml` 코드에 전달하기 전에 deserializer는 XML 요소를 검사하고 이러한 특수 XML 특성을 검색하여 작업을 수행합니다. 예를 들어 "nil"이 `true`이면 null 값이 deserialize되고 `ReadXml`은 호출되지 않습니다. 다형성이 검색되면 요소의 콘텐츠가 다른 형식인 것처럼 deserialize됩니다. 다형적으로 할당된 형식의 `ReadXml` 구현이 호출됩니다. 어떤 경우에든 이러한 특수 특성은 deserializer에 의해 처리되므로 `ReadXml` 구현에서는 해당 특수 특성을 무시해야 합니다.  
  
### <a name="schema-considerations-for-ixmlserializable-content-types"></a>IXmlSerializable 콘텐츠 형식의 스키마 고려 사항  
 스키마를 `IXmlSerializable` 콘텐츠 형식으로 내보내면 스키마 공급자 메서드가 호출됩니다. <xref:System.Xml.Schema.XmlSchemaSet>가 스키마 공급자 메서드로 전달됩니다. 메서드는 유효한 스키마를 모두 스키마 집합에 추가할 수 있습니다. 스키마 집합에는 스키마를 내보낼 때 이미 알려진 스키마가 포함됩니다. 스키마 공급자 메서드는 스키마 집합에 항목을 추가해야 하는 경우 해당 네임스페이스를 가진 <xref:System.Xml.Schema.XmlSchema>가 집합에 이미 있는지 확인해야 합니다. 이미 있으면 스키마 공급자 메서드는 기존 `XmlSchema`에 새 항목을 추가해야 합니다. 없는 경우에는 새 `XmlSchema` 인스턴스를 만들어야 합니다. 이 기능은 `IXmlSerializable` 형식의 배열을 사용하는 경우에 중요합니다. 예를 들어 "B" 네임스페이스에 "A" 형식으로 내보내지는 `IXmlSerializable` 형식이 있는 경우 스키마 공급자 메서드가 호출될 때까지 스키마 집합에 "ArrayOfA" 형식을 보유할 "B"의 스키마가 이미 포함될 수 있습니다.  
  
 <xref:System.Xml.Schema.XmlSchemaSet>에 형식을 추가하는 것 외에 콘텐츠 형식의 스키마 공급자 메서드는 null이 아닌 값을 반환해야 합니다. 이 메서드는 지정된 <xref:System.Xml.XmlQualifiedName> 형식에 사용할 스키마 형식의 이름을 지정하는 `IXmlSerializable`을 반환할 수 있습니다. 이 정규화된 이름은 형식의 데이터 계약 이름과 네임스페이스로도 사용됩니다. 스키마 공급자 메서드가 반환될 때 즉시 스키마 집합에 없는 형식을 반환할 수 있습니다. 그러나 관련된 모든 형식을 내보낼 때까지, 즉 <xref:System.Runtime.Serialization.XsdDataContractExporter.Export%2A>의 모든 관련 형식에 대해 <xref:System.Runtime.Serialization.XsdDataContractExporter> 메서드가 호출되고 <xref:System.Runtime.Serialization.XsdDataContractExporter.Schemas%2A> 속성에 액세스할 때까지 형식은 스키마 집합에 있습니다. 관련된 `Schemas` 호출을 수행하기 전에 `Export` 속성에 액세스하면 <xref:System.Xml.Schema.XmlSchemaException>이 발생할 수 있습니다. 내보내기 프로세스에 대 한 자세한 내용은 참조 하세요. [클래스에서 스키마 내보내기](../../../../docs/framework/wcf/feature-details/exporting-schemas-from-classes.md)합니다.  
  
 스키마 공급자 메서드는 또한 사용할 <xref:System.Xml.Schema.XmlSchemaType>을 반환할 수도 있습니다. 형식은 익명이거나 익명이 아닐 수 있습니다. 익명인 경우 `IXmlSerializable` 형식을 데이터 멤버로 사용할 때마다 `IXmlSerializable` 형식의 스키마가 익명 형식으로 내보내집니다. `IXmlSerializable` 형식에 여전히 데이터 계약 이름과 네임스페이스가 있습니다. (에 설명 된 대로이 확인할 [Data Contract Names](../../../../docs/framework/wcf/feature-details/data-contract-names.md) 점을 제외 하 고는 <xref:System.Runtime.Serialization.DataContractAttribute> 특성 이름에 맞게 사용할 수 없습니다.) 익명이 아닌 경우 `XmlSchemaSet`의 형식 중 하나여야 합니다. 이 경우는 형식의 `XmlQualifiedName`을 반환하는 것과 같습니다.  
  
 또한 전역 요소 선언이 형식에 대해 내보내집니다. 형식에 <xref:System.Xml.Serialization.XmlRootAttribute> 특성이 적용되지 않은 경우 요소가 데이터 계약과 동일한 이름 및 네임스페이스를 갖게 되며 "nillable" 속성이 true가 됩니다. 유일한 예외는 스키마 네임 스페이스 ("http://www.w3.org/2001/XMLSchema")-스키마 네임 스페이스에 새 요소를 추가할 수는 없으므로 해당 전역 요소가 빈 네임 스페이스에는 형식의 데이터 계약이이 네임 스페이스의 경우. 형식에 `XmlRootAttribute` 특성이 적용되어 있으면 전역 요소 선언이 <xref:System.Xml.Serialization.XmlRootAttribute.ElementName%2A>, <xref:System.Xml.Serialization.XmlRootAttribute.Namespace%2A> 및 <xref:System.Xml.Serialization.XmlRootAttribute.IsNullable%2A> 속성을 사용하여 내보내집니다. `XmlRootAttribute`가 적용된 경우의 기본값은 데이터 계약 이름, 빈 네임스페이스 및 true인 "nillable"입니다.  
  
 레거시 데이터 세트 형식에도 동일한 전역 요소 선언 규칙이 적용됩니다. `XmlRootAttribute`는 사용자 지정 코드를 통해 추가된, 즉 스키마 공급자 메서드를 사용하거나 레거시 데이터 세트 형식의 경우 `XmlSchemaSet`를 통해 `GetSchema`에 추가된 전역 요소 선언을 재정의할 수 없습니다.  
  
### <a name="ixmlserializable-element-types"></a>IXmlSerializable 요소 형식  
 `IXmlSerializable` 요소 형식은 `IsAny` 속성이 `true`로 설정되어 있거나 스키마 공급자 메서드가 `null`을 반환하도록 합니다.  
  
 요소 형식의 serialize 및 deserialize는 콘텐츠 형식의 serialize 및 deserialize와 유사합니다. 그러나 다음과 같은 중요한 차이가 있습니다.  
  
- `WriteXml` 구현은 정확히 하나의 요소를 씁니다. 물론 이 요소는 여러 개의 자식 요소를 포함할 수 있습니다. 이 단일 요소, 여러 개의 형제 요소 또는 혼합 콘텐츠 외부의 특성을 쓰면 안 됩니다. 요소는 비어 있을 수 있습니다.  
  
- `ReadXml` 구현은 래퍼 요소를 읽어서는 안 됩니다. `WriteXml`에서 생성하는 하나의 요소를 읽습니다.  
  
- 예를 들어 데이터 계약의 데이터 멤버로 정기적으로 요소 형식을 serialize하는 경우 serializer는 콘텐츠 형식과 마찬가지로 `WriteXml`을 호출하기 전에 래퍼 요소를 출력합니다. 그러나 최상위 수준에서 요소 형식을 serialize할 때 serializer는 일반적으로 `WriteXml` 또는 `DataContractSerializer` 생성자에서 serializer를 생성할 때 루트 이름과 네임스페이스를 명시적으로 지정하지 않은 경우 `NetDataContractSerializer`에서 쓰는 요소를 둘러싼 래퍼 요소를 출력하지 않습니다. 자세한 내용은 [Serialization 및 Deserialization](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md)합니다.  
  
- 생성 시 루트 이름과 네임스페이스를 지정하지 않고 최상위 수준에서 요소 형식을 serialize하는 경우 <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteStartObject%2A> 및 <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteEndObject%2A>에서 아무 작업도 수행하지 않으며 <xref:System.Runtime.Serialization.XmlObjectSerializer.WriteObjectContent%2A>는 `WriteXml`을 호출합니다. 이 모드에서 serialize되는 개체는 null일 수 없으며 다형적으로 할당할 수 없습니다. 또한 개체 그래프 유지를 활성화할 수 없고 `NetDataContractSerializer`를 사용할 수 없습니다.  
  
- 생성 시 루트 이름과 네임스페이스를 지정하지 않고 최상위 수준에서 요소 형식을 deserialize하는 경우 <xref:System.Runtime.Serialization.XmlObjectSerializer.IsStartObject%2A>가 임의 요소의 시작 부분을 찾으면 `true`를 반환합니다. <xref:System.Runtime.Serialization.XmlObjectSerializer.ReadObject%2A> 매개 변수를 `verifyObjectName`로 설정한 `true`는 실제로 개체를 읽기 전에 `IsStartObject`와 같은 방식으로 동작합니다. 그런 다음 `ReadObject`는 컨트롤을 `ReadXml` 메서드로 전달합니다.  
  
 요소 형식과 관련해서 내보낸 스키마는 스키마 공급자 메서드가 `XmlElement`에 다른 스키마를 추가할 수 있다는 점을 제외하고 이전 단원에서 설명한 대로 <xref:System.Xml.Schema.XmlSchemaSet> 형식에 대해 콘텐츠 형식과 동일합니다. 요소 형식에 `XmlRootAttribute` 특성을 사용할 수 없으며 이러한 형식에 대해 전역 요소 선언을 내보내지 않습니다.  
  
### <a name="differences-from-the-xmlserializer"></a>XmlSerializer와의 차이점  
 `IXmlSerializable` 인터페이스와 `XmlSchemaProviderAttribute` 및 `XmlRootAttribute` 특성도 <xref:System.Xml.Serialization.XmlSerializer>에서 인식됩니다. 그러나 데이터 계약 모델에서 처리되는 방법에 차이가 있습니다. 아래에 중요한 차이가 요약되어 있습니다.  
  
- `XmlSerializer`에서 사용할 수 있으려면 스키마 공급자 메서드가 public이어야 하지만 public이 아니어도 데이터 계약 모델에서 사용할 수 있습니다.  
  
- 데이터 계약 모델에서 `IsAny`가 true일 때는 스키마 공급자 메서드가 호출되지만 `XmlSerializer`를 사용할 때는 호출되지 않습니다.  
  
- 콘텐츠 또는 레거시 데이터 세트 형식에 `XmlRootAttribute` 특성이 없으면 `XmlSerializer`는 빈 네임스페이스에 전역 요소 선언을 내보냅니다. 데이터 계약 모델에서 사용되는 네임스페이스는 일반적으로 앞에서 설명한 데이터 계약 네임스페이스입니다.  
  
 두 가지 serialization 기술에서 모두 사용할 형식을 만드는 경우 이러한 차이에 주의하세요.  
  
### <a name="importing-ixmlserializable-schema"></a>IXmlSerializable 스키마 가져오기  
 `IXmlSerializable` 형식에서 생성된 스키마를 가져오는 경우 다음과 같은 몇 가지 가능성이 있습니다.  
  
- 생성된 된 스키마에 설명 된 대로 올바른 데이터 계약 스키마를 수 있습니다 [데이터 계약 스키마 참조](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)합니다. 이 경우 스키마를 일반적인 방법으로 가져올 수 있으며 일반 데이터 계약 형식이 생성됩니다.  
  
- 생성된 스키마가 올바른 데이터 계약 스키마가 아닐 수 있습니다. 예를 들어 스키마 공급자 메서드가 데이터 계약 모델에서 지원되지 않는 XML 특성과 관련된 스키마를 생성할 수 있습니다. 이 경우 스키마를 `IXmlSerializable` 형식으로 가져올 수 있습니다. 이 가져오기 모드는 기본적으로 설정 되지 않지만 쉽게 – 예를 들어와 함께 사용할 수는 `/importXmlTypes` 명령줄 스위치를 합니다 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)합니다. 이에 자세히 설명 되어는 [스키마를 생성 하는 클래스를 가져와서](../../../../docs/framework/wcf/feature-details/importing-schema-to-generate-classes.md)합니다. 형식 인스턴스에 대한 XML로 직접 작업해야 합니다. 보다 넓은 범위의 스키마를 지원하는 다른 serialization 기술을 사용할 수도 있습니다. `XmlSerializer` 사용에 대한 항목을 참조하세요.  
  
- 새 형식을 생성하는 대신 프록시의 기존 `IXmlSerializable` 형식을 다시 사용할 수 있습니다. 이 경우 스키마를 가져와서 형식 생성 항목에서 설명하는 참조된 형식 기능을 사용하여 다시 사용할 형식을 나타낼 수 있습니다. 이는 다시 사용할 형식이 포함된 어셈블리를 지정하는 svcutil.exe에 `/reference` 스위치를 사용하는 것에 같습니다.  
  
## <a name="representing-arbitrary-xml-in-data-contracts"></a>데이터 계약에 임의 XML 표현  
 `XmlElement`, `XmlNode` 배열 및 `IXmlSerializable` 형식을 사용하여 임의 XML을 데이터 계약 모델에 삽입할 수 있습니다. `DataContractSerializer` 및 `NetDataContractSerializer`는 프로세스에 간섭하지 않고 사용 중인 XML 작성기에 이 XML 콘텐츠를 전달합니다. 그러나 XML 작성기는 작성하는 XML에 특정 제한을 적용할 수 있습니다. 특히 중요한 예는 다음과 같습니다.  
  
- XML 작성기는 XML 문서 선언 일반적으로 허용 하지 않습니다 (예를 들어 \<? xml 버전 ='1.0 '? >) 다른 문서를 작성 하는 중입니다. 전체 XML 문서를 사용하여 `Array` 데이터 멤버의 `XmlNode`로 serialize할 수 없습니다. 이렇게 하려면 문서 선언을 제거하거나 고유의 인코딩 체계를 사용하여 문서 선언을 나타내야 합니다.  
  
- XML 처리 명령이 거부 모든 WCF와 함께 제공 된 XML 작성기 (\<? … ? >)과 문서 형식 정의 (\<! … >)는 SOAP 메시지에서 허용 되지 않으므로 합니다. 자체 인코딩 메커니즘을 사용하여 이 제한을 해결할 수도 있습니다. 결과 XML에 이러한 요소를 포함해야 하는 경우 이를 지원하는 XML 작성기를 사용하는 사용자 지정 인코더를 작성할 수 있습니다.  
  
- `WriteXml`을 구현할 때 XML 작성기에서 <xref:System.Xml.XmlWriter.WriteRaw%2A> 메서드를 호출하지 마세요. 다양 한 XML 인코딩 (바이너리 포함)을 사용 하 여 WCF를 사용 하기가 매우 어렵거나 `WriteRaw` 결과 모든 인코딩을 사용할 수 있도록 합니다.  
  
- 구현 하는 경우 `WriteXml`를 사용 하지 않도록 합니다 <xref:System.Xml.XmlWriter.WriteEntityRef%2A> 및 <xref:System.Xml.XmlWriter.WriteNmToken%2A> WCF와 함께 제공 된 XML 작성기에서 지원 되지 않는 메서드.  
  
## <a name="using-dataset-typed-dataset-and-datatable"></a>DataSet, 형식화된 DataSet 및 DataTable 사용  
 이러한 형식 사용은 데이터 계약 모델에서 완전히 지원됩니다. 이 형식을 사용할 때는 다음 사항을 고려하세요.  
  
- 이러한 형식에 대 한 스키마 (특히 <xref:System.Data.DataSet> 및 해당 형식화 된 파생 클래스) 일부 WCF 이외의 플랫폼과 상호 운용 가능한 수 없거나 이러한 플랫폼과 함께 사용할 때 유용성이 저하 될 수 있습니다. 또한 `DataSet` 형식을 사용하면 성능에 영향을 줄 수도 있습니다. 마지막으로 이후에 애플리케이션의 버전 관리가 더 어려워질 수 있습니다. 계약에 `DataSet` 형식 대신 명시적으로 정의된 데이터 계약 형식을 사용하세요.  
  
- `DataSet` 또는 `DataTable` 스키마를 가져올 때는 이러한 형식을 참조하는 것이 중요합니다. Svcutil.exe 명령줄 도구를 사용 하 여 이렇게 System.Data.dll 어셈블리 이름을 전달 하 여는 `/reference` 전환 합니다. 형식화된 데이터 세트 스키마를 가져오는 경우 형식화된 데이터 세트의 형식을 참조해야 합니다. Svcutil.exe를 사용 하 여 형식화 된 데이터 집합의 어셈블리의 위치를 전달 합니다 `/reference` 전환 합니다. 참조 형식에 대 한 자세한 내용은 참조는 [스키마를 생성 하는 클래스를 가져와서](../../../../docs/framework/wcf/feature-details/importing-schema-to-generate-classes.md)합니다.  
  
 데이터 계약 모델에서 형식화된 데이터 세트에 대한 지원은 제한되어 있습니다. 형식화된 데이터 세트은 serialize 및 deserialize할 수 있으며 스키마를 내보낼 수 있습니다. 하지만 데이터 계약 스키마 가져오기에서는 스키마로부터 형식화된 데이터 세트 형식을 새로 생성할 수 없고 기존 형식을 다시 사용할 수만 있습니다. Svcutil.exe에 `/r` 스위치를 사용하면 형식화된 기존 데이터 세트을 가리킬 수 있습니다. 형식화된 데이터 세트을 사용하는 서비스에서 `/r` 스위치 없이 Svcutil.exe를 사용하려 하면 대체 serializer(XmlSerializer)가 자동으로 선택됩니다. DataContractSerializer를 사용해야 하며 스키마에서 데이터 세트을 생성해야 하는 경우에는 다음 절차를 사용할 수 있습니다. 서비스에서 `/d` 스위치와 함께 Xsd.exe 도구를 사용하여 형식화된 데이터 세트 형식을 생성한 다음 Svcutil.exe에서 `/r` 스위치를 사용하여 가리킵니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Xml.Serialization.IXmlSerializable>
- [데이터 계약 사용](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)
- [데이터 계약 직렬 변환기에서 지원하는 형식](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)
