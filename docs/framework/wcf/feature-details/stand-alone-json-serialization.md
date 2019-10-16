---
title: DataContractJsonSerializer를 사용 하는 독립 실행형 JSON Serialization
ms.date: 03/30/2017
ms.assetid: 312bd7b2-1300-4b12-801e-ebe742bd2287
ms.openlocfilehash: 65cae13d0185ea1f18bdd54cd26f703fde984f69
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72180240"
---
# <a name="stand-alone-json-serialization-using-datacontractjsonserializer"></a>DataContractJsonSerializer를 사용 하는 독립 실행형 JSON Serialization

> [!NOTE]
> 이 문서는 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>입니다. JSON 직렬화 및 역직렬화를 포함 하는 대부분의 시나리오에서는 system.xml [네임 스페이스](../../../standard/serialization/system-text-json-overview.md)의 도구를 권장 합니다. 

JSON (JavaScript Object Notation)은 브라우저 내의 웹 페이지에서 실행되는 JavaScript 코드에 의해 사용되도록 특별히 디자인된 데이터 형식이며 Windows Communication Foundation (WCF)에서 만든 ASP.NET AJAX 서비스에서 사용 하는 기본 데이터 형식입니다.

이 형식은 ASP.NET과 결합하지 않고 AJAX 서비스를 만드는 경우에도 사용할 수 있습니다. 이 경우 XML이 기본값이지만 JSON을 선택할 수 있습니다.

마지막으로 JSON 지원이 필요하지만 AJAX 서비스는 만들지 않을 경우 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>를 사용하면 .NET 개체를 JSON 데이터로 serialize하고 다시 .NET 형식의 인스턴스로 직접 해당 데이터를 deserialize할 수 있습니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 [How to: JSON 데이터 Serialize 및 Deserialize @ no__t-0.

JSON으로 작업할 경우 몇 가지 예외를 제외하고는 <xref:System.Runtime.Serialization.DataContractSerializer>에서 지원하는 것과 같은 .NET 형식이 지원됩니다. 지원 되는 형식 목록은 [데이터 계약 Serializer에서 지 원하는 형식](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)을 참조 하세요. 여기에는 대부분의 기본 형식, 대부분의 배열 및 컬렉션 형식뿐만 아니라 <xref:System.Runtime.Serialization.DataContractAttribute> 및 <xref:System.Runtime.Serialization.DataMemberAttribute>를 사용하는 복합 형식도 포함됩니다.

## <a name="mapping-net-types-to-json-types"></a>JSON 형식에 .NET 형식 매핑

다음 표에서는 serialization 및 deserialization 절차를 통해 매핑될 때 .NET 형식과 JSON/JavaScript 형식 간의 대응 관계를 보여 줍니다.

|.NET 형식|JSON/JavaScript|참고|
|----------------|----------------------|-----------|
|모든 숫자 형식. 예: <xref:System.Int32>, <xref:System.Decimal> 또는 <xref:System.Double>|Number|`Double.NaN`, `Double.PositiveInfinity` 및 `Double.NegativeInfinity`와 같은 특수한 값은 지원되지 않으므로 잘못된 JSON이 됩니다.|
|<xref:System.Enum>|Number|이 항목의 뒷부분에 있는 "열거 및 JSON"을 참조하십시오.|
|<xref:System.Boolean>|Boolean|--|
|<xref:System.String>, <xref:System.Char>|문자열|--|
|<xref:System.TimeSpan>, <xref:System.Guid>, <xref:System.Uri>|문자열|JSON에서 이러한 형식의 형식은 XML에서와 동일 합니다 (기본적으로 ISO 8601 기간 형식의 TimeSpan, "12345678-1234567890AB의 GUID," http://www.example.com "과 같이 자연 문자열 형식으로 된 URI). 자세한 내용은 [데이터 계약 스키마 참조](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)를 참조 하세요.|
|<xref:System.Xml.XmlQualifiedName>|문자열|형식은 "name:namespace"이며 첫 번째 콜론 앞에 오는 것이 이름입니다. 이름 또는 네임스페이스가 없는 경우도 있습니다. 네임스페이스가 없는 경우 콜론도 생략할 수 있습니다.|
|<xref:System.Array>의 <xref:System.Byte> 형식입니다.|숫자 배열|각 숫자는 1바이트 값을 나타냅니다.|
|<xref:System.DateTime>|날짜/시간 또는 문자열|이 항목의 뒷부분에 있는 날짜/시간 및 JSON을 참조하십시오.|
|<xref:System.DateTimeOffset>|복합 형식|이 항목의 뒷부분에 있는 날짜/시간 및 JSON을 참조하십시오.|
|XML 및 ADO.NET 형식(<xref:System.Xml.XmlElement>,<br /><br /> <xref:System.Xml.Linq.XElement>. <xref:System.Xml.XmlNode>의 배열,<br /><br /> <xref:System.Runtime.Serialization.ISerializable>,<br /><br /> <xref:System.Data.DataSet>).|문자열|이 항목의 XML 형식 및 JSON 단원을 참조하십시오.|
|<xref:System.DBNull>|빈 복합 형식|--|
|컬렉션, 사전 및 배열|String|이 항목의 컬렉션, 사전 및 배열 단원을 참조하십시오.|
|복합 형식(<xref:System.Runtime.Serialization.DataContractAttribute> 또는 <xref:System.SerializableAttribute> 적용)|복합 형식|데이터 멤버는 JavaScript 복합 형식의 멤버가 됩니다.|
|<xref:System.Runtime.Serialization.ISerializable> 인터페이스를 구현하는 복합 형식)|복합 형식|다른 복합 형식과 같지만 일부 <xref:System.Runtime.Serialization.ISerializable> 형식이 지원되지 않습니다. 이 항목의 고급 정보 단원에 있는 ISerializable 지원 부분을 참조하십시오.|
|모든 형식에 대해 `Null` 값|Null|Nullable 형식은 nullable이 아닌 형식과 같은 방식으로 지원되고 JSON에 매핑됩니다.|

### <a name="enumerations-and-json"></a>열거 및 JSON

열거형 멤버 값은 JSON에서 숫자로 처리되며 이는 열거형 멤버 값이 멤버 이름으로 포함되는 데이터 계약에서의 처리 방식과 다릅니다. 데이터 계약 처리에 대 한 자세한 내용은 [데이터 계약의 열거형 형식](../../../../docs/framework/wcf/feature-details/enumeration-types-in-data-contracts.md)을 참조 하세요.

- 예를 들어, `public enum Color {red, green, blue, yellow, pink}`가 있을 경우 `yellow`를 serialize하면 문자열 "yellow"가 아닌 숫자 3이 생성됩니다.

- 모든 `enum` 멤버는 serialize할 수 있습니다. <xref:System.Runtime.Serialization.EnumMemberAttribute> 및 <xref:System.NonSerializedAttribute> 특성은 사용될 경우 무시됩니다.

- 존재하지 않는 `enum` 값을 deserialize할 수 있습니다. 예를 들어, 해당 색 이름이 정의되어 있지 않더라도 값 87을 이전 Color 열거형으로 deserialize할 수 있습니다.

- 플래그 `enum`은 특수한 플래그가 아니며 `enum`과 동일하게 처리됩니다.

### <a name="datestimes-and-json"></a>날짜/시간 및 JSON

JSON 형식은 날짜 및 시간을 직접적으로 지원하지 않습니다. 그러나 매우 일반적으로 사용되며 ASP.NET AJAX는 이러한 형식을 특수한 방식으로 지원합니다. ASP.NET AJAX 프록시를 사용할 경우 .NET의 <xref:System.DateTime> 형식은 JavaScrip의 `DateTime` 형식과 완전히 일치합니다.

- ASP.NET을 사용하지 않을 경우 <xref:System.DateTime> 형식은 JSON에서 이 항목의 고급 정보 단원에 설명된 특수 형식의 문자열로 표시됩니다.

- <xref:System.DateTimeOffset>은 JSON에 복합 형식 {"DateTime":dateTime,"OffsetMinutes":offsetMinutes}로 표현됩니다. `offsetMinutes` 멤버는 GMT(그리니치 표준시)의 현지 시간 오프셋으로, 관련 이벤트의 위치와 연관된 UTC(세계 협정시)라고도 합니다. `dateTime` 멤버는 관련 이벤트가 발행했을 때의 시간 인스턴스를 나타내며, ASP.NET AJAX를 사용할 때는 JavaScript에서 `DateTime`이 되고 사용하지 않을 때는 문자열이 됩니다. serialization 시 `dateTime` 멤버는 항상 GMT로 serialize됩니다. 따라서 뉴욕 시간으로 오전 3시인 경우 `dateTime` 시간 구성 요소는 오전 8시이고 `offsetMinutes`는 300(GMT에서 300분 또는 5시간을 뺀 값)입니다.

  > [!NOTE]
  > JSON으로 serialize한 경우 <xref:System.DateTime> 및 <xref:System.DateTimeOffset> 개체는 밀리초 수준의 정보만 유지합니다. 서브-밀리초 값(마이크로초/나노초)은 serialization 중에 손실됩니다.

### <a name="xml-types-and-json"></a>XML 형식 및 JSON

XML 형식은 JSON 문자열이 됩니다.

- 예를 들어 XElement 형식의 데이터 멤버 "q"에 \<abc/>가 포함 된 경우 JSON은 {"q": "\<abc/>"}입니다.

- XML 래핑 방법을 지정하는 몇 가지 특수한 규칙이 있습니다. 자세한 내용은 이 항목의 뒷부분에 있는 고급 정보 단원을 참조하십시오.

- ASP.NET AJAX를 사용 중인 경우 JavaScript에서 문자열을 사용하는 대신 XML DOM을 사용하려면 <xref:System.ServiceModel.Web.WebGetAttribute.ResponseFormat%2A>에서<xref:System.ServiceModel.Web.WebGetAttribute> 속성을 XML로 설정하거나 <xref:System.ServiceModel.Web.WebInvokeAttribute.ResponseFormat%2A>에서 <xref:System.ServiceModel.Web.WebInvokeAttribute> 속성을 XML로 설정합니다.

### <a name="collections-dictionaries-and-arrays"></a>컬렉션, 사전 및 배열

모든 컬렉션, 사전 및 배열은 JSON에서 배열로 표시됩니다.

- <xref:System.Runtime.Serialization.CollectionDataContractAttribute>를 사용하는 모든 사용자 지정은 JSON 표현에서 무시됩니다.

- 사전은 JSON에 직접 사용할 수 있는 방식이 아닙니다. 사전 @ no__t-0string, object >은 다른 JSON 기술 작업에서 예상 되는 것과 동일한 방식으로 WCF에서 지원 되지 않을 수 있습니다. 예를 들어 "abc"가 "xyz"로 매핑되고 "def"가 사전의 42로 매핑되는 경우 JSON 표현은 {"abc":"xyz","def":42}가 아니라 [{"Key":"abc","Value":"xyz"},{"Key":"def","Value":42}]입니다.

- JSON으로 직접 작업하려는 경우(엄격한 계약을 미리 정의하지 않고 키 및 값에 동적으로 액세스하는 경우) 다음과 같은 몇 가지 옵션이 있습니다.

  - [약한 형식의 JSON Serialization (AJAX)](../../../../docs/framework/wcf/samples/weakly-typed-json-serialization-sample.md) 샘플을 사용 하는 것이 좋습니다.

  - <xref:System.Runtime.Serialization.ISerializable> 인터페이스와 deserialization 생성자를 사용합니다. 이 두 메커니즘을 사용하면 serialization과 deserialization 시 각각 JSON 키/값 쌍에 액세스할 수 있지만 부분 신뢰 시나리오에서 작업할 수 없습니다.

  - Serializer를 사용 하는 대신 [JSON과 XML 간의 매핑으로](../../../../docs/framework/wcf/feature-details/mapping-between-json-and-xml.md) 작업 하는 것이 좋습니다.

  - Serialization 컨텍스트의 *다형성* 은 기본 형식이 필요한 경우 파생 형식을 serialize 하는 기능을 의미 합니다. 예를 들어 컬렉션을 <xref:System.Object>에 할당할 때처럼 컬렉션을 다형적으로 사용하는 경우 특수한 JSON 관련 규칙이 있습니다. 이러한 내용은 이 항목의 뒷부분에 있는 고급 정보 단원에 자세히 설명되어 있습니다.

## <a name="additional-details"></a>추가 정보

### <a name="order-of-data-members"></a>데이터 멤버 순서

JSON을 사용할 때 데이터 멤버의 순서는 중요하지 않습니다. 특히 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A>가 설정된 경우에도 JSON 데이터를 원하는 순서로 deserialize할 수 있습니다.

### <a name="json-types"></a>JSON 형식

deserialization 시 JSON 형식은 위의 표와 일치하지 않아도 됩니다. 예를 들어 `Int`는 일반적으로 JSON 숫자로 매핑되지만 JSON 문자열에 유효한 숫자가 있으면 이 문자열에서 deserialize할 수도 있습니다. 즉, "q"라고 하는 `Int` 데이터 멤버가 있는 경우 {"q":42} 및 {"q":"42"}는 유효합니다.

### <a name="polymorphism"></a>다형성

다형 serialization은 기본 형식이 필요한 경우에 파생 형식을 serialize하는 기능으로 구성됩니다. 이는 XML serialization이 지원 되는 방식과 비교할 수 있는 WCF의 JSON serialization에 대해 지원 됩니다. 예를 들어 `MyBaseType`이 예상 되는 `MyDerivedType`을 serialize 하거나 `Object`이 필요한 `Int`를 직렬화 할 수 있습니다.

복합 형식을 deserialize하지 않는 한 기본 형식이 필요한 경우에 파생 형식을 deserialize하면 형식 정보가 손실될 수도 있습니다. 예를 들어 <xref:System.Uri>가 필요한 경우 <xref:System.Object>를 serialize하면 JSON 문자열이 됩니다. 이 문자열을 다시 <xref:System.Object>로 deserialize하면 .NET <xref:System.String>이 반환됩니다. deserializer는 문자열이 처음에 <xref:System.Uri> 형식이었음을 인식하지 못합니다. 일반적으로 <xref:System.Object>가 필요한 경우 실제 원본 형식에 관계없이 모든 JSON 문자열은 .NET 문자열로 deserialize되고 .NET 컬렉션, 사전 및 배열을 serialize하는 데 사용되는 모든 JSON 배열은 <xref:System.Array> 형식의 .NET <xref:System.Object>로 deserialize됩니다. JSON 부울은 .NET <xref:System.Boolean>로 매핑됩니다. 그러나 <xref:System.Object>가 필요한 경우 JSON 숫자는 .NET <xref:System.Int32>, <xref:System.Decimal> 또는 <xref:System.Double>로 deserialize되며, 이때 가장 적합한 형식이 자동으로 선택됩니다.

<xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>는 인터페이스 형식으로 deserialize될 때 선언된 형식이 개체인 것처럼 deserialize됩니다.

사용자 고유의 기본 형식 및 파생 형식으로 작업하는 경우에는 일반적으로 <xref:System.Runtime.Serialization.KnownTypeAttribute>, <xref:System.ServiceModel.ServiceKnownTypeAttribute> 또는 이와 동등한 메커니즘을 사용해야 합니다. 예를 들어 `Animal` 반환 값을 포함 하는 작업을 실제로 반환 하 고 `Cat`의 인스턴스를 반환 하는 경우 (`Animal`에서 파생 됨) <xref:System.Runtime.Serialization.KnownTypeAttribute>을 `Animal` 형식에 적용 하 고 <xref:System.ServiceModel.ServiceKnownTypeAttribute>를 작업에 적용 하 여 이러한 특성 자세한 내용은 [데이터 계약 알려진 형식을](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)합니다.

다형 serialization 작동 방식에 대한 자세한 내용 및 다형 serialization 사용 시 고려해야 할 제한 사항에 대한 설명은 이 항목의 뒷부분에 있는 고급 정보 단원을 참조하십시오.

### <a name="versioning"></a>버전 관리

JSON에서는 <xref:System.Runtime.Serialization.IExtensibleDataObject> 인터페이스를 포함한 데이터 계약 버전 관리 기능이 완벽하게 지원됩니다. 또한 대부분의 경우에 형식을 한 가지 형식(예: XML)으로 deserialize한 다음 다른 형식(예: JSON)으로 serialize할 수 있으며 이 경우 데이터를 <xref:System.Runtime.Serialization.IExtensibleDataObject>에 유지할 수 있습니다. 자세한 내용은 [호환 가능한 데이터 계약](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)을 참조하세요. JSON은 순서가 지정되지 않으므로 순서 정보가 손실됩니다. 또한 JSON은 키 이름이 같은 여러 키/값 쌍을 지원하지 않습니다. 마지막으로, <xref:System.Runtime.Serialization.IExtensibleDataObject>의 모든 작업은 원래 다형적입니다. 즉, 모든 형식의 기본 형식인 <xref:System.Object>에 파생 형식이 할당됩니다.

## <a name="json-in-urls"></a>URL의 JSON

ASP.NET AJAX 엔드포인트를 <xref:System.ServiceModel.Web.WebGetAttribute> 특성을 사용하는 HTTP GET 동사와 함께 사용하는 경우 요청 URL에 메시지 본문 대신 들어오는 매개 변수가 표시됩니다. JSON은 요청 URL 에서도 지원 되므로 "number" 라는 `Int`을 사용 하 고 "p" 라는 `Person` 복합 형식을 사용 하는 작업이 있는 경우 URL은 다음 URL과 유사할 수 있습니다.

```
http://example.com/myservice.svc/MyOperation?number=7&p={"name":"John","age":42}
```

ASP.NET AJAX Script Manager 컨트롤 및 프록시를 사용하여 서비스를 호출하는 경우 프록시에 의해 이 URL이 자동으로 생성되지만 표시되지는 않습니다. JSON은 ASP.NET AJAX가 아닌 엔드포인트에 있는 URL에서 사용할 수 없습니다.

## <a name="advanced-information"></a>고급 정보

### <a name="iserializable-support"></a>ISerializable 지원

#### <a name="supported-and-unsupported-iserializable-types"></a>지원되는 ISerializable 형식과 지원되지 않는 ISerializable 형식

일반적으로 <xref:System.Runtime.Serialization.ISerializable> 인터페이스를 구현하는 형식은 JSON을 serialize하거나 deserialize할 때 완전히 지원됩니다. 그러나 이러한 형식 중에는 JSON 관련 serialization의 영향을 받으면 deserialize하지 않도록 구현되는 형식(일부 .NET Framework 형식 포함)도 있습니다.

- <xref:System.Runtime.Serialization.ISerializable>을 사용하면 개별 데이터 멤버의 형식을 미리 알 수 없습니다. 따라서 다형적 상황은 형식을 개체로 deserialize하는 상황과 유사합니다. 앞서 설명한 바와 같이 이로 인해 JSON에서 형식 정보가 손실될 수 있습니다. 예를 들어, 해당 `enum` 구현에서 <xref:System.Runtime.Serialization.ISerializable>을 serialize한 형식이 적절한 캐스팅 없이 바로 `enum`으로 다시 deserialize를 시도하는 경우 실패하게 됩니다. 이는 `enum`이 JSON에서 숫자를 사용하여 serialize되고 JSON 숫자는 기본 제공 .NET 숫자 형식(Int32, Decimal 또는 Double)으로 deserialize되기 때문입니다. 따라서 `enum` 값으로 사용된 숫자가 손실됩니다.

- 대부분의 JSON은 특정 순서를 보장하지 않기 때문에 해당 deserialization 생성자에서 특정 deserialization 순서에 의존하는 <xref:System.Runtime.Serialization.ISerializable> 형식도 일부 JSON 데이터를 deserialize하지 못할 수 있습니다.

#### <a name="factory-types"></a>팩터리 형식

<xref:System.Runtime.Serialization.IObjectReference> 인터페이스는 일반적으로 JSON에서 지원되지만, 인터페이스를 구현하는 형식과 다른 형식의 인스턴스를 <xref:System.Runtime.Serialization.IObjectReference.GetRealObject%28System.Runtime.Serialization.StreamingContext%29>에서 반환하는 "팩터리 형식" 기능을 필요로 하는 형식은 지원되지 않습니다.

### <a name="datetime-wire-format"></a>DateTime 통신 형식

<xref:System.DateTime> 값은 "/Date(700000+0500)/" 형식의 JSON 문자열로 표시됩니다. 여기서 첫 번째 숫자(이 예제에서는 700000)는 1970년 1월 1일 자정부터의 정규 시간(일광 절약 시간이 아님)인 GMT 시간대의 시간(밀리초)입니다. 이 숫자는 이보다 이전 시간을 나타낼 경우 음수가 될 수 있습니다. 예제에서 "+0500"으로 구성된 부분은 선택적 요소이며, 시간이 <xref:System.DateTimeKind.Local> 종류, 즉 deserialization 시 현지 시간대로 변환되어야 함을 나타냅니다. 이 부분이 없으면 시간은 <xref:System.DateTimeKind.Utc>로 deserialize됩니다. 실제 숫자(이 예제에서는 "0500")와 해당 기호(+ 또는 -)는 무시됩니다.

<xref:System.DateTime>을 serialize하는 경우 <xref:System.DateTimeKind.Local> 및 <xref:System.DateTimeKind.Unspecified> 시간은 오프셋과 함께 기록되고 <xref:System.DateTimeKind.Utc>는 오프셋 없이 기록됩니다.

ASP.NET AJAX 클라이언트 JavaScript 코드는 이러한 문자열을 JavaScript `DateTime` 인스턴스로 자동으로 변환합니다. .NET에 <xref:System.DateTime> 형식이 아닌 유사한 형식을 지닌 다른 문자열이 있는 경우 이 문자열 또한 변환됩니다.

변환은 "/" 문자가 이스케이프 되는 경우에만 발생 합니다. 즉, JSON은 "\\/날짜 (700000 + 0500) \\/")로 표시 되며,이 때문에 WCF의 JSON 인코더 (<xref:System.ServiceModel.WebHttpBinding>에서 사용 하도록 설정 됨)는 항상 "/" 문자를 이스케이프 합니다.

### <a name="xml-in-json-strings"></a>JSON 문자열의 XML

#### <a name="xmlelement"></a>XmlElement

<xref:System.Xml.XmlElement>는 래핑 없이 그대로 serialize됩니다. 예를 들어 \<abc/>를 포함 하는 <xref:System.Xml.XmlElement> 형식의 데이터 멤버 "x"는 다음과 같이 표시 됩니다.

```json
{"x":"<abc/>"}
```

#### <a name="arrays-of-xmlnode"></a>XmlNode 배열

<xref:System.Array> 형식의 <xref:System.Xml.XmlNode> 개체는 형식에 대한 표준 데이터 계약 네임스페이스에서 ArrayOfXmlNode라는 요소에 래핑됩니다. "x"가 "value"와 빈 요소 노드 "M"을 포함하는 네임스페이스 "ns"에 특성 노드 "N"을 포함하는 배열인 경우 해당 표현은 다음과 같습니다.

```json
{"x":"<ArrayOfXmlNode xmlns=\"http://schemas.datacontract.org/2004/07/System.Xml\" a:N=\"value\" xmlns:a=\"ns\"><M/></ArrayOfXmlNode>"}
```

 XmlNode 배열의 시작 부분(다른 요소들 앞)에서 빈 네임스페이스의 특성은 지원되지 않습니다.

#### <a name="ixmlserializable-types-including-xelement-and-dataset"></a>XElement 및 DataSet을 포함한 IXmlSerializable 형식

<xref:System.Runtime.Serialization.ISerializable> 형식은 "콘텐츠 형식", "DataSet 형식" 및 "요소 형식"으로 나누어집니다. 이러한 형식에 대 한 정의는 [데이터 계약의 XML 및 ADO.NET 형식](../../../../docs/framework/wcf/feature-details/xml-and-ado-net-types-in-data-contracts.md)을 참조 하세요.

"콘텐츠" 및 "DataSet" 형식은 이전 단원에서 설명한 <xref:System.Array>의 <xref:System.Xml.XmlNode> 개체와 비슷하게 serialize됩니다. "콘텐츠" 및 "DataSet" 형식은 이름과 네임스페이스가 해당 형식의 데이터 계약 이름과 네임스페이스에 해당하는 요소에 래핑됩니다.

<xref:System.Xml.Linq.XElement>와 같은 "요소" 형식은 이 항목의 앞에서 설명한 <xref:System.Xml.XmlElement>와 비슷하게 그대로 serialize됩니다.

### <a name="polymorphism"></a>다형성

#### <a name="preserving-type-information"></a>형식 정보 유지

위에서 설명한 것처럼 다형성은 JSON에서 지원되지만 몇 가지 제한 사항이 있습니다. JavaScript는 약한 형식의 언어이며 형식 일치는 일반적으로 문제가 되지 않습니다. 그러나 JSON을 사용하여 강력한 형식 시스템(.NET)과 약한 형식 시스템(JavaScript) 간에 통신하는 경우에는 형식 일치를 유지하는 것이 좋습니다. 예를 들어 데이터 계약 이름이 "Shape"인 형식에서 데이터 계약 이름이 "Square"와 "Circle"인 형식이 파생됩니다. "Circle"을 .NET에서 JavaScript로 보낸 다음 나중에 "Shape"이 필요한 .NET 메서드에 반환하는 경우 .NET 측에서 해당 개체가 원래 "Circle"이었음을 알고 있는 것이 좋습니다. 그렇지 않으면 파생 형식에 특정한 정보(예: "Circle"의 "radius" 데이터 멤버)가 손실될 수도 있습니다.

형식 일치를 유지하려면 복합 형식을 JSON으로 serialize할 때 "형식 힌트"를 추가하면 deserializer가 힌트를 인식하고 적절히 작동할 수 있습니다. "형식 힌트"는 키 이름이 "\_ @ no__t-1 형식" 인 JSON 키/값 쌍입니다 (두 개의 밑줄 뒤에 "type" 단어가 옴). 값은 "DataContractName:DataContractNamespace"(첫 번째 콜론까지는 이름) 형식의 JSON 문자열입니다. 앞의 예제를 사용하면 "Circle"은 다음과 같이 serialize될 수 있습니다.

```json
{"__type":"Circle:http://example.com/myNamespace","x":50,"y":70,"radius":10}
```

형식 암시는 XML 스키마 인스턴스 표준을 통해 정의되고 XML을 serialize/deserialize할 때 사용되는 `xsi:type` 특성과 매우 비슷합니다.

"@No__t-0 @ no__t-1type" 이라는 데이터 멤버는 형식 힌트와의 잠재적 충돌로 인해 사용할 수 없습니다.

#### <a name="reducing-the-size-of-type-hints"></a>형식 암시 크기 줄이기

JSON 메시지의 크기를 줄이기 위해 기본 데이터 계약 네임 스페이스 접두사 (`http://schemas.datacontract.org/2004/07/`)는 "#" 문자로 바뀝니다. 이 대체를 되돌릴 수 있도록 하기 위해 이스케이프 규칙이 사용 됩니다. 네임 스페이스가 "#" 또는 "\\" 문자로 시작 하는 경우 추가 "\\" 문자가 추가 됩니다. 따라서 "Circle"이 .NET 네임 스페이스 "MyApp. Shapes"의 형식인 경우 기본 데이터 계약 네임 스페이스는 `http://schemas.datacontract.org/2004/07/MyApp`입니다. Shapes와 JSON 표현은 다음과 같습니다.

```json
{"__type":"Circle:#MyApp.Shapes","x":50,"y":70,"radius":10}
```

잘린 (#MyApp 셰이프)와 전체 (0 @no__t 이름 모두 deserialization에서 인식 됩니다.

#### <a name="type-hint-position-in-json-objects"></a>JSON 개체의 형식 힌트 위치

형식 힌트는 JSON 표현에서 맨 처음에 와야 합니다. 이 경우에만 JSON 처리에서 키/값 쌍의 순서가 중요합니다. 예를 들어 다음은 형식 힌트를 지정하는 올바른 방법이 아닙니다.

```json
{"x":50,"y":70,"radius":10,"__type":"Circle:#MyApp.Shapes"}
```

WCF 및 ASP.NET AJAX 클라이언트 페이지에서 사용 하는 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>은 항상 형식 힌트를 먼저 내보냅니다.

#### <a name="type-hints-apply-only-to-complex-types"></a>형식 힌트는 복합 형식에만 적용

복합 형식이 아닌 경우에는 형식 힌트를 내보낼 수 없습니다. 예를 들어, 작업에 <xref:System.Object> 반환 형식이 있지만 Circle을 반환하는 경우 JSON 표현은 앞에서 보여 준 것과 같을 수 있으며 형식 정보는 유지됩니다. 그러나 URI가 반환되는 경우 JSON 표현은 문자열이고 URI를 표현하는 데 사용된 문자열은 손실됩니다. 이것은 기본 형식뿐 아니라 컬렉션 및 배열에도 적용됩니다.

#### <a name="when-are-type-hints-emitted"></a>형식 힌트를 내보내는 시기

형식 힌트는 메시지 크기를 상당히 증가시킬 수 있습니다. 이 문제를 완화하기 위한 한 가지 방법은 가능한 경우 더 짧은 데이터 계약 네임스페이스를 사용하는 것입니다. 따라서 다음 규칙에 따라 형식 힌트를 내보낼지 여부가 결정됩니다.

- ASP.NET AJAX를 사용하는 경우, 기본/파생 할당이 없을 때(예를 들어 Circle이 Circle에 할당된 경우)에도 가능하면 항상 형식 힌트를 내보냅니다. 이는 정보의 큰 손실 없이 약한 형식 JSON 환경에서 강력한 형식 .NET 환경으로 호출하는 프로세스를 완벽하게 지원하기 위해 필요합니다.

- ASP.NET과 통합되지 않은 AJAX 서비스를 사용하는 경우에는 기본/파생 할당이 있는 경우에만 형식 힌트를 내보냅니다. 즉, Circle이 Shape 또는 <xref:System.Object>에 할당되었지만 Circle에는 할당되지 않은 경우에 형식 힌트를 내보냅니다. 이를 통해 JavaScript 클라이언트를 올바르게 구현하는 데 필요한 최소 정보가 제공되므로 성능이 향상되지만 잘못 디자인된 클라이언트의 경우 형식 정보 손실을 방지할 수 없습니다. 클라이언트에서 이 문제를 처리하지 않으려면 서버에 기본/파생 할당이 없도록 해야 합니다.

- <xref:System.Runtime.Serialization.DataContractSerializer> 형식을 사용하는 경우 `alwaysEmitTypeInformation` 생성자 매개 변수를 사용하면 기본값을 "`false`"(필요한 경우에만 형식 힌트를 내보냄)로 설정하여 앞의 두 모드 간에 선택할 수 있습니다.

#### <a name="duplicate-data-member-names"></a>중복 데이터 멤버 이름

파생 형식 정보는 기본 형식 정보와 함께 동일한 JSON 개체에 있으며 순서에 구애 받지 않습니다. 예를 들어 `Shape`은 다음과 같이 나타낼 수 있습니다.

```json
{"__type":"Shape:#MyApp.Shapes","x":50,"y":70}
```

반면 Circle은 다음과 같이 표시될 수 있습니다.

```json
{"__type":"Circle:#MyApp.Shapes","x":50, "radius":10,"y":70}
```

기본 `Shape` 형식에 "`radius`" 이라는 데이터 멤버가 포함 된 경우 JSON 개체는 반복 키 이름을 가질 수 없기 때문에 serialization에서 충돌을 발생 시킵니다. "radius"가 `Shape.radius` @no__ 또는을 참조 하는지 여부는 명확 하지 않기 때문입니다. t-3). 그러므로 데이터 계약 클래스에서 "속성 숨기기"(기본 클래스와 파생 클래스에서 동일한 이름의 데이터 멤버)는 일반적으로 권장되지 않으며 JSON의 경우에는 금지됩니다.

#### <a name="polymorphism-and-ixmlserializable-types"></a>다형성 및 IXmlSerializable 형식

<xref:System.Xml.Serialization.IXmlSerializable> 형식은 보통 일반 데이터 계약 규칙에 따라 알려진 형식 요구 사항을 충족하는 한 서로 다형적으로 할당될 수 있습니다. 그러나 <xref:System.Xml.Serialization.IXmlSerializable> 대신 <xref:System.Object> 형식을 serialize하면 JSON 문자열이 되므로 형식 정보가 손실됩니다.

#### <a name="polymorphism-and-certain-interface-types"></a>다형성 및 특정 인터페이스 형식

컬렉션 형식 또는 <xref:System.Xml.Serialization.IXmlSerializable>이 아닌 비컬렉션 형식(<xref:System.Xml.Serialization.IXmlSerializable> 예외)이 필요한 <xref:System.Object>을 구현하는 형식은 serialize할 수 없습니다. 예를 들어 `IMyInterface` 이라는 사용자 지정 인터페이스와 `int` 및 @no__t 형식의 <xref:System.Collections.Generic.IEnumerable%601>를 모두 구현 하는 형식 `MyType`입니다. 반환 형식이 `IMyInterface` 인 작업에서 `MyType`을 반환할 수 없습니다. 이는 `MyType`은 JSON 배열로 serialize 되어야 하며 형식 힌트가 필요 하기 때문입니다. 앞에서 설명한 것 처럼 복합 형식만 포함 하 여 배열에 형식 힌트를 포함할 수 없기 때문입니다.

#### <a name="known-types-and-configuration"></a>알려진 형식 및 구성

<xref:System.Runtime.Serialization.DataContractSerializer>에서 사용되는 알려진 형식 메커니즘은 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>에서도 동일한 방식으로 모두 지원됩니다. 두 serializer는 동일한 구성 요소인 [\<dataContractSerializer >](../../../../docs/framework/configure-apps/file-schema/wcf/datacontractserializer-of-system-runtime-serialization.md) 를 [\<bdbs >](../../../../docs/framework/configure-apps/file-schema/wcf/system-runtime-serialization.md)에 읽고 구성 파일을 통해 추가 된 알려진 형식을 검색 합니다.

#### <a name="collections-assigned-to-object"></a>개체에 할당된 컬렉션

개체에 할당된 컬렉션은 <xref:System.Collections.Generic.IEnumerable%601>을 구현하는 컬렉션인 것처럼 serialize됩니다(복합 형식인 경우 각 항목에 형식 힌트가 있는 JSON 배열). 예를 들어 <xref:System.Object>에 할당 된 @no__t 형식의 <xref:System.Collections.Generic.List%601>은 다음과 같습니다.

```json
[{"__type":"Shape:#MyApp.Shapes","x":50,"y":70},
{"__type":"Shape:#MyApp.Shapes","x":58,"y":73},
{"__type":"Shape:#MyApp.Shapes","x":41,"y":32}]
```

<xref:System.Object>로 다시 deserialize하는 경우:

- `Shape`은 알려진 형식 목록에 있어야 합니다. 알려진 형식에서-1 @no__t 형식의 <xref:System.Collections.Generic.List%601> 인 경우에는 영향을 주지 않습니다. 이 경우에는 serialization에서 알려진 형식에 `Shape`을 추가할 필요가 없습니다 .이 작업은 자동으로 수행 됩니다.

- 컬렉션은 `Shape` 인스턴스를 포함 하는 <xref:System.Object> 형식의 <xref:System.Array>으로 deserialize 됩니다.

#### <a name="derived-collections-assigned-to-base-collections"></a>기본 컬렉션에 할당된 파생 컬렉션

파생 컬렉션을 기본 컬렉션에 할당하면, 일반적으로 기본 형식의 컬렉션인 것처럼 컬렉션이 serialize됩니다. 그러나 파생 컬렉션의 항목 형식을 기본 컬렉션의 항목 형식에 할당할 수 없는 경우 예외가 throw됩니다.

#### <a name="type-hints-and-dictionaries"></a>형식 힌트 및 사전

사전을 <xref:System.Object>에 할당하면 사전의 각 Key 및 Value 항목이 <xref:System.Object>에 할당된 것처럼 처리되고 형식 힌트를 가져옵니다.

사전 형식을 serialize하는 경우 "Key" 및 "Value" 멤버를 포함하는 JSON 개체는 `alwaysEmitTypeInformation` 설정의 영향을 받지 않고 이전 컬렉션 규칙에서 요구하는 경우에만 형식 힌트를 포함합니다.

### <a name="valid-json-key-names"></a>유효한 JSON 키 이름

serializer는 유효한 XML 이름이 아닌 키 이름을 XML 인코딩합니다. 예를 들어 이름이 "123" 인 데이터 멤버에는 "123"가 잘못 된 XML 요소 이름 (숫자로 시작) 이기 때문에 "\_x0031 @ no__t-1 @ no__t-2x0032 @ no__t-3 @ no__t-4x0033 @ no__t-5"와 같이 인코딩된 이름이 포함 됩니다. XML 이름에 유효하지 않은 일부 국제 문자 집합이 포함되는 경우에도 비슷한 상황이 발생할 수 있습니다. JSON 처리의 이러한 XML 효과에 대 한 설명은 [json과 Xml 간의 매핑](../../../../docs/framework/wcf/feature-details/mapping-between-json-and-xml.md)을 참조 하세요.

## <a name="see-also"></a>참조

- [JSON 및 기타 데이터 전송 형식에 대한 지원](../../../../docs/framework/wcf/feature-details/support-for-json-and-other-data-transfer-formats.md)
