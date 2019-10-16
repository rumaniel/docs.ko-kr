---
title: 데이터 계약의 컬렉션 형식
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- collection types [WCF], data contracts
- data contracts [WCF], collection types
- collection types [WCF]
ms.assetid: 9b45b28e-0a82-4ea3-8c33-ec0094aff9d5
ms.openlocfilehash: 810238ee631808dac472456f910eb52f8bbf550c
ms.sourcegitcommit: 30a83efb57c468da74e9e218de26cf88d3254597
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2019
ms.locfileid: "68363821"
---
# <a name="collection-types-in-data-contracts"></a>데이터 계약의 컬렉션 형식

*컬렉션* 은 특정 형식의 항목으로 구성된 목록입니다. .NET Framework에서 이러한 목록은 배열이 나 다양 한 형식 (제네릭 목록, 제네릭 <xref:System.ComponentModel.BindingList%601>, <xref:System.Collections.Specialized.StringCollection>또는 <xref:System.Collections.ArrayList>)을 사용 하 여 나타낼 수 있습니다. 예를 들어, 컬렉션은 지정된 고객에 대한 주소 목록을 보유할 수 있습니다. 실제 형식에 관계없이 이러한 컬렉션을 *목록 컬렉션*이라고 합니다.

하나의 항목("키")과 다른 항목("값") 간의 연결을 나타내는 특별한 형태의 컬렉션이 있습니다. .NET Framework에서는 <xref:System.Collections.Hashtable> 및 제네릭 사전과 같은 형식으로 표시 됩니다. 예를 들어, 연결 컬렉션은 도시("키")를 해당 도시의 인구("값")에 매핑할 수 있습니다. 실제 형식에 관계없이 이러한 컬렉션을 *사전 컬렉션*이라고 합니다.

데이터 계약 모델에서 컬렉션은 별도로 처리됩니다.

배열 및 제네릭 컬렉션을 비롯하여 <xref:System.Collections.IEnumerable> 인터페이스를 구현하는 형식은 컬렉션으로 인식됩니다. 이 중에서 <xref:System.Collections.IDictionary> 또는 제네릭 <xref:System.Collections.Generic.IDictionary%602> 인터페이스를 구현하는 형식은 사전 컬렉션이며, 다른 모든 형식은 목록 컬렉션입니다.

메서드를 호출 `Add` 하 고 매개 변수 없는 생성자를 포함 하는 등 컬렉션 형식에 대 한 추가 요구 사항은 다음 단원에서 자세히 설명 합니다. 이렇게 하면 컬렉션 형식이 serialize되고 deserialize될 수 있습니다. 즉, 매개 변수가 없는 생성자가 없기 때문에 제네릭 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 과 같은 일부 컬렉션은 직접 지원 되지 않습니다. 이러한 제한을 해결하는 방법에 대한 자세한 내용은 이 항목의 뒷부분에 있는 "컬렉션 인터페이스 형식 및 읽기 전용 컬렉션 사용" 단원을 참조하십시오.

컬렉션에 포함된 형식은 데이터 계약 형식이거나 serialize할 수 있어야 합니다. 자세한 내용은 [데이터 계약 Serializer에서 지 원하는 형식](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)을 참조 하세요.

유효한 컬렉션 및 컬렉션을 serialize 하는 방법에 대 한 자세한 내용은이 항목의 "고급 컬렉션 규칙" 섹션에서 컬렉션을 serialize 하는 방법에 대 한 정보를 참조 하세요.

## <a name="interchangeable-collections"></a>교환 가능 컬렉션

동일한 형식의 모든 목록 컬렉션은 이 항목 뒷부분에서 설명하는 것처럼 <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 특성을 사용하여 사용자 지정되지 않는 한 동일한 데이터 계약을 가지는 것으로 간주됩니다. 예를 들어, 다음 데이터 계약은 동일합니다.

[!code-csharp[c_collection_types_in_data_contracts#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#0)]
[!code-vb[c_collection_types_in_data_contracts#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#0)]

두 데이터 계약 모두 다음 코드와 유사한 XML이 됩니다.

```xml
<PurchaseOrder>
    <customerName>...</customerName>
    <items>
        <Item>...</Item>
        <Item>...</Item>
        <Item>...</Item>
        ...
    </items>
    <comments>
        <string>...</string>
        <string>...</string>
        <string>...</string>
        ...
    </comments>
</PurchaseOrder>
```

예를 들어, 컬렉션 교환 가능성을 통해 서버의 성능에 맞게 최적화된 컬렉션 형식 및 클라이언트의 사용자 인터페이스 구성 요소에 바인딩되도록 디자인된 컬렉션 형식을 사용할 수 있습니다.

목록 컬렉션과 마찬가지로 동일한 키 및 값 형식이 있는 모든 사전 컬렉션은 <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 특성을 사용하여 사용자 지정되지 않는 한 동일한 데이터 계약을 가지는 것으로 간주됩니다.

컬렉션 일치에 있어서는 .NET 형식이 아닌 데이터 계약 형식만 중요합니다. 즉, Type1 및 Type2에 동일한 데이터 계약이 있는 경우 Type1의 컬렉션과 Type2의 컬렉션이 동일하다고 간주합니다.

제네릭이 아닌 컬렉션에는 `Object`형식의 제네릭 컬렉션과 동일한 데이터 계약이 있는 것으로 간주합니다. 예를 들어, <xref:System.Collections.ArrayList> 의 데이터 계약 및 <xref:System.Collections.Generic.List%601> 의 제네릭 `Object` 은 동일합니다.

## <a name="using-collection-interface-types-and-read-only-collections"></a>컬렉션 인터페이스 형식 및 읽기 전용 컬렉션 사용

또한 컬렉션 인터페이스 형식(<xref:System.Collections.IEnumerable>, <xref:System.Collections.IDictionary>, 제네릭 <xref:System.Collections.Generic.IDictionary%602>또는 이러한 인터페이스에서 파생된 인터페이스)에는 실제 컬렉션 형식의 컬렉션 데이터 계약과 동일한 컬렉션 데이터 계약이 있는 것으로 간주합니다. 따라서 serialize되는 형식을 컬렉션 인터페이스 형식으로 선언할 수 있으며, 결과는 실제 컬렉션 형식을 사용한 것과 동일합니다. 예를 들어, 다음 데이터 계약은 동일합니다.

[!code-csharp[c_collection_types_in_data_contracts#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#1)]
[!code-vb[c_collection_types_in_data_contracts#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#1)]

serialization을 수행하는 동안 선언된 형식이 인터페이스인 경우 사용된 실제 인스턴스 형식은 해당 인터페이스를 구현하는 모든 형식이 될 수 있습니다. 앞에서 설명한 제한 사항 (매개 변수가 없는 생성자 `Add` 와 메서드 포함)은 적용 되지 않습니다. 예를 들어, 제네릭 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 형식의 데이터 멤버를 직접 선언할 수 없는 경우에도 Customer2의 주소를 제네릭 주소 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>의 인스턴스로 설정할 수 있습니다

deserialization을 수행하는 동안 선언된 형식이 인터페이스인 경우 serialization 엔진은 선언된 인터페이스를 구현하는 형식을 선택하고, 해당 형식은 인스턴스화됩니다. 알려진 형식 메커니즘 ( [데이터 계약 알려진 형식](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)에 설명 됨)은 여기에 영향을 주지 않습니다. 선택할 수 있는 형식은 WCF에 기본 제공 됩니다.

## <a name="customizing-collection-types"></a>컬렉션 형식 사용자 지정

여러 용도로 사용되는 <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 특성을 사용하여 컬렉션 형식을 사용자 지정할 수 있습니다.

컬렉션 형식을 사용자 지정하면 컬렉션 교환 가능성이 낮아지므로 가능하면 이 특성을 적용하지 않는 것이 좋습니다. 이 문제에 대 한 자세한 내용은이 항목의 뒷부분에 나오는 "고급 컬렉션 규칙" 단원을 참조 하십시오.

### <a name="collection-data-contract-naming"></a>컬렉션 데이터 계약 명명

컬렉션 형식의 명명 규칙은 [Data Contract Names](../../../../docs/framework/wcf/feature-details/data-contract-names.md)에서 설명한 대로 일반 데이터 계약 형식의 명명 규칙과 유사하지만, 다음과 같은 중요한 차이점이 몇 개 있습니다.

- <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 특성은 <xref:System.Runtime.Serialization.DataContractAttribute> 특성 대신 이름을 사용자 지정하는 데 사용됩니다. 또한 <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 특성에는 `Name` 및 `Namespace` 속성이 있습니다.

- <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 특성이 적용되지 않는 경우 컬렉션 형식의 기본 이름 및 네임스페이스는 컬렉션에 포함된 형식의 이름 및 네임스페이스에 따라 다릅니다. 컬렉션 형식의 이름 및 네임스페이스 자체는 컬렉션에 포함된 형식의 이름 및 네임스페이스에 영향을 주지 않습니다. @FSHO1@예를 보려면 다음 형식을 참조하십시오.

  ```csharp
  public CustomerList1 : Collection<string> {}
  public StringList1 : Collection<string> {}
  ```

두 형식의 데이터 계약 이름이 모두 "ArrayOfstring"이고 "CustomerList1" 또는 "StringList1"이 아닙니다. 즉, 루트 수준의 이러한 형식 중 하나를 serialize하면 다음 코드와 유사한 XML이 생성됩니다.

```xml
<ArrayOfstring>
    <string>...</string>
    <string>...</string>
    <string>...</string>
    ...
</ArrayOfstring>
```

문자열의 목록을 나타내는 사용자 지정되지 않은 형식에 동일한 데이터 계약 및 XML 표현이 있도록 이 명명 규칙을 선택했습니다. 이렇게 하면 컬렉션 교환이 가능하게 됩니다. 이 예제에서 CustomerList1과 StringList1은 완벽하게 교환 가능합니다.

그러나 <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 특성이 적용된 경우 속성을 특성에 설정하지 않아도 컬렉션은 사용자 지정된 컬렉션 데이터 계약이 됩니다. 따라서 컬렉션 데이터 계약의 이름 및 네임스페이스는 컬렉션 형식 자체에 따라 달라집니다. 예를 보려면 다음 형식을 참조하십시오.

[!code-csharp[c_collection_types_in_data_contracts#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#2)]
[!code-vb[c_collection_types_in_data_contracts#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#2)]

serialize된 결과 XML은 다음과 유사합니다.

```xml
<CustomerList2>
    <string>...</string>
    <string>...</string>
    <string>...</string>
    ...
</CustomerList2>
```

결과 XML은 사용자 지정되지 않은 형식의 XML 표현과 더 이상 동일하지 않습니다.

- `Name` 및 `Namespace` 속성을 사용하여 명명을 추가로 사용자 지정할 수 있습니다. 다음 클래스를 참조하십시오.

  [!code-csharp[c_collection_types_in_data_contracts#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#3)]
  [!code-vb[c_collection_types_in_data_contracts#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#3)]

결과 XML은 다음과 유사합니다.

```xml
<cust_list>
    <string>...</string>
    <string>...</string>
    <string>...</string>
    ...
</cust_list>
```

자세한 내용은이 항목의 뒷부분에 나오는 "고급 컬렉션 규칙" 단원을 참조 하십시오.

### <a name="customizing-the-repeating-element-name-in-list-collections"></a>목록 컬렉션의 반복되는 요소 이름 사용자 지정

목록 컬렉션에는 반복되는 항목이 있습니다. 일반적으로 반복되는 각 항목은 컬렉션에 포함된 형식의 데이터 계약 이름에 따라 명명된 요소로 표시됩니다.

`CustomerList` 예제에서 컬렉션에는 문자열이 있습니다. 문자열 기본 형식에 대 한 데이터 계약 이름은 "string" 이므로 반복 되는 요소는 "\<string >"입니다.

그러나 <xref:System.Runtime.Serialization.CollectionDataContractAttribute.ItemName%2A> 특성의 <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 속성을 사용하여 이 반복되는 요소 이름을 사용자 지정할 수 있습니다. 예를 보려면 다음 형식을 참조하십시오.

[!code-csharp[c_collection_types_in_data_contracts#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#4)]
[!code-vb[c_collection_types_in_data_contracts#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#4)]

결과 XML은 다음과 유사합니다.

```xml
<CustomerList4>
    <customer>...</customer>
    <customer>...</customer>
    <customer>...</customer>
    ...
</CustomerList4>
```

반복되는 요소의 네임스페이스는 앞에서 설명한 대로 `Namespace` 속성을 사용하여 사용자 지정할 수 있는 컬렉션 데이터 계약의 네임스페이스와 항상 같습니다.

### <a name="customizing-dictionary-collections"></a>사전 컬렉션 사용자 지정

사전 컬렉션은 기본적으로 항목의 목록이며 각 항목에는 키 다음에 값이 있습니다. 일반 목록과 마찬가지로 <xref:System.Runtime.Serialization.CollectionDataContractAttribute.ItemName%2A> 속성을 사용하여 반복되는 요소에 해당하는 요소 이름을 변경할 수 있습니다.

또한 <xref:System.Runtime.Serialization.CollectionDataContractAttribute.KeyName%2A> 및 <xref:System.Runtime.Serialization.CollectionDataContractAttribute.ValueName%2A> 속성을 사용하여 키 및 값을 나타내는 요소 이름을 변경할 수 있습니다. 이러한 요소의 네임스페이스는 컬렉션 데이터 계약의 네임스페이스와 같습니다.

예를 보려면 다음 형식을 참조하십시오.

[!code-csharp[c_collection_types_in_data_contracts#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#5)]
[!code-vb[c_collection_types_in_data_contracts#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#5)]

serialize된 결과 XML은 다음과 유사합니다.

```xml
<CountriesOrRegionsWithCapitals>
    <entry>
        <countryorregion>USA</countryorregion>
        <capital>Washington</capital>
    </entry>
    <entry>
        <countryorregion>France</countryorregion>
        <capital>Paris</capital>
    </entry>
    ...
</CountriesOrRegionsWithCapitals>
```

사전 컬렉션에 대 한 자세한 내용은이 항목의 뒷부분에 나오는 "고급 컬렉션 규칙" 단원을 참조 하십시오.

## <a name="collections-and-known-types"></a>컬렉션 및 알려진 형식

컬렉션 형식을 다른 컬렉션이나 컬렉션 인터페이스 대신 다형적으로 사용하는 경우 알려진 형식에 추가할 필요는 없습니다. 예를 들어, <xref:System.Collections.IEnumerable> 형식의 데이터 멤버를 선언하고 이를 사용하여 <xref:System.Collections.ArrayList>의 인스턴스를 보내는 경우 <xref:System.Collections.ArrayList> 를 알려진 형식에 추가할 필요가 없습니다.

비컬렉션 형식 대신 다형적으로 컬렉션을 사용하는 경우에는 알려진 형식에 추가해야 합니다. 예를 들어, `Object` 형식의 데이터 멤버를 선언하고 이를 사용하여 <xref:System.Collections.ArrayList>의 인스턴스를 보내는 경우 알려진 형식에 <xref:System.Collections.ArrayList> 를 추가합니다.

그러나 동일한 컬렉션을 다형적으로 serialize할 수는 없습니다. 예를 들어, <xref:System.Collections.ArrayList> 를 위 예제의 알려진 형식의 목록에 추가하는 경우 해당 목록에 동일한 데이터 계약이 있더라도 `Array of Object` 클래스를 할당할 수 없습니다. 따라서 비컬렉션 형식에 대한 serialization에서 알려진 형식의 일반 동작과 차이는 없지만, 컬렉션이 동일한 경우가 매우 일반적이기 때문에 컬렉션의 경우 이 동작을 이해하는 것이 특히 중요합니다.

serialization을 수행하는 동안 지정된 데이터 계약의 지정된 범위에서 하나의 형식만을 알 수 있으며 모든 동일한 컬렉션에는 같은 데이터 계약이 있습니다. 따라서 위 예제에서 <xref:System.Collections.ArrayList> 및 `Array of Object` 모두를 같은 범위의 알려진 형식에 추가할 수 없습니다. 이 동작은 비컬렉션 형식에 대한 알려진 형식 동작과 동일하지만, 컬렉션의 경우 이를 이해하는 것이 특히 중요합니다.

알려진 형식은 또한 컬렉션의 내용에 필요합니다. 예를 들어, <xref:System.Collections.ArrayList> 에 `Type1` 및 `Type2`의 인스턴스가 실제로 있는 경우 이 두 가지 형식 모두 알려진 형식에 추가해야 합니다.

다음 예제에서는 컬렉션 및 알려진 형식을 사용하여 올바르게 생성된 개체 그래프를 보여 줍니다. 일반적으로 실제 애플리케이션에서는 다음 데이터 멤버를 `Object`로 정의하지 않고 알려진 형식/다형성 문제가 없기 때문에 이 예제는 실제와 다소 거리가 있습니다.

[!code-csharp[c_collection_types_in_data_contracts#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#6)]
[!code-vb[c_collection_types_in_data_contracts#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#6)]

deserialization에서 선언된 형식이 컬렉션 형식이면 실제로 보낸 형식과 관계없이 선언된 형식이 인스턴스화됩니다. 선언된 형식이 컬렉션 인터페이스이면 deserializer에서는 알려진 형식과 관계없이 인스턴스화할 형식을 선택합니다.

또한 deserialization에서 선언된 형식이 컬렉션 형식은 아니지만 컬렉션 형식을 보내는 경우 일치하는 컬렉션 형식이 알려진 형식 목록에서 선택됩니다. deserialization에서 컬렉션 인터페이스 형식을 알려진 형식 목록에 추가할 수 있습니다. 이 경우 deserialization 엔진은 인스턴스화할 형식을 다시 선택합니다.

## <a name="collections-and-the-netdatacontractserializer-class"></a>컬렉션 및 NetDataContractSerializer 클래스

<xref:System.Runtime.Serialization.NetDataContractSerializer> 클래스가 사용 중인 경우 배열이 아닌 사용자 지정되지 않은 컬렉션 형식( <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 특성이 없는 컬렉션)은 원래의 특수한 의미를 잃게 됩니다.

<xref:System.SerializableAttribute> 특성으로 표시된 사용자 지정되지 않은 컬렉션 형식은 <xref:System.Runtime.Serialization.NetDataContractSerializer> 특성이나 <xref:System.SerializableAttribute> 인터페이스 규칙에 따라 <xref:System.Runtime.Serialization.ISerializable> 클래스로 여전히 serialize할 수 있습니다.

사용자 지정된 컬렉션 형식, 컬렉션 인터페이스 및 배열은 <xref:System.Runtime.Serialization.NetDataContractSerializer> 클래스가 사용 중인 경우에도 컬렉션으로서 계속 처리됩니다.

## <a name="collections-and-schema"></a>컬렉션 및 스키마

모든 동일한 컬렉션에는 동일한 표현의 XSD(XML 스키마 정의 언어) 스키마가 있습니다. 이 때문에 일반적으로 서버의 컬렉션 형식과 동일한 컬렉션 형식을 생성된 클라이언트 코드에서 얻을 수 없습니다. 예를 들어, 서버에서 정수 데이터 멤버의 제네릭 <xref:System.Collections.Generic.List%601> 와 함께 데이터 계약을 사용할 수 있지만, 생성된 클라이언트 코드에서 동일한 데이터 멤버가 정수 배열이 될 수 있습니다.

사전 컬렉션은 사전 임을 나타내는 WCF 관련 스키마 주석으로 표시 됩니다. 그렇지 않은 경우에는 키와 값이 포함 된 항목을 포함 하는 단순 목록에서 구별할 수 없습니다. 데이터 계약 스키마에서 컬렉션이 표시되는 방법에 대한 정확한 설명은 [Data Contract Schema Reference](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)를 참조하십시오.

기본적으로 가져온 코드의 사용자 지정되지 않은 컬렉션에 대해서는 형식이 생성되지 않습니다. 목록 컬렉션 형식의 데이터 멤버는 배열로 가져오며, 사전 컬렉션 형식의 데이터 멤버는 제네릭 사전으로 가져옵니다.

그러나 사용자 지정된 컬렉션의 경우 <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 특성으로 표시되는 별도의 형식이 생성됩니다. 스키마에서 사용자 지정된 컬렉션 형식은 기본 네임스페이스, 이름, 반복되는 요소 이름 또는 키/값 요소 이름을 사용하지 않습니다. 이러한 형식은 목록 형식의 경우 제네릭 <xref:System.Collections.Generic.List%601>에서 파생되고, 사전 형식의 경우 제네릭 사전에서 파생되는 빈 형식입니다.

예를 들어, 서버에 다음 형식이 있을 수 있습니다.

[!code-csharp[c_collection_types_in_data_contracts#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#7)]
[!code-vb[c_collection_types_in_data_contracts#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#7)]

스키마를 내보내고 다시 가져온 경우 생성되는 클라이언트 코드는 다음과 유사합니다. 읽기 용이하도록 속성 대신 필드가 표시되어 있습니다.

[!code-csharp[c_collection_types_in_data_contracts#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#8)]
[!code-vb[c_collection_types_in_data_contracts#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#8)]

생성된 코드에서 기본 형식 대신 다른 형식을 사용해야 하는 경우가 있습니다. 예를 들어, 사용자 인터페이스 구성 요소에 쉽게 바인딩할 수 있도록 데이터 멤버의 일반 배열 대신 제네릭 <xref:System.ComponentModel.BindingList%601> 를 사용해야 하는 경우입니다.

생성할 컬렉션 형식을 선택하려면 스키마를 가져올 때 사용할 컬렉션 형식의 목록을 <xref:System.Runtime.Serialization.ImportOptions.ReferencedCollectionTypes%2A> 개체의 <xref:System.Runtime.Serialization.ImportOptions> 속성에 전달합니다. 이러한 형식을 *참조된 컬렉션 형식*이라고 합니다.

제네릭 형식을 참조할 때 해당 제네릭 형식은 완전 개방형 제네릭 형식 또는 완전 폐쇄형 제네릭 형식이어야 합니다.

> [!NOTE]
> Svcutil.exe 도구를 사용하는 경우 **/collectionType** 명령줄 스위치(약식: **/ct**)를 사용하여 이 참조를 수행할 수 있습니다. 또한 **/reference** 스위치(약식: **/r**)를 사용하여 참조된 컬렉션 형식에 대한 어셈블리를 지정해야 합니다. 형식이 제네릭이면 뒤에는 역따옴표 및 제네릭 매개 변수의 수가 와야 합니다. 큰따옴표 (\`)는 작은따옴표 (') 문자와 혼동 하지 않아야 합니다. **/collectionType** 스위치를 두 번 이상 사용하여 여러 개의 참조된 컬렉션 형식을 지정할 수 있습니다.

예를 들어, 모든 목록을 제네릭 <xref:System.Collections.Generic.List%601>로 가져오려면 다음을 사용합니다.

```console
svcutil.exe MyService.wsdl MyServiceSchema.xsd /r:C:\full_path_to_system_dll\System.dll /ct:System.Collections.Generic.List`1
```

컬렉션을 가져올 때 이 참조된 컬렉션 형식 목록을 검색한 다음 사용자 지정되지 않은 컬렉션의 경우 데이터 멤버 형식으로 컬렉션을 찾거나, 사용자 지정된 컬렉션의 경우 파생될 기본 형식으로 컬렉션을 찾아 가장 일치하는 컬렉션을 사용합니다. 사전은 사전에 대해서만 일치하며 목록은 목록에 대해서만 일치합니다.

예를 들어, 제네릭 <xref:System.ComponentModel.BindingList%601> 및 <xref:System.Collections.Hashtable> 을 참조된 형식 목록에 추가하면 앞의 예제에서 생성된 클라이언트 코드는 다음과 유사합니다.

[!code-csharp[c_collection_types_in_data_contracts#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#9)]
[!code-vb[c_collection_types_in_data_contracts#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#9)]

컬렉션 인터페이스 형식을 참조된 컬렉션 형식의 일부로 지정할 수 있지만 `Add` 메서드 또는 public 생성자가 없는 컬렉션 형식과 같은 잘못된 컬렉션 형식을 지정할 수는 없습니다.

폐쇄형 제네릭이 가장 일치하는 항목으로 간주됩니다. 제네릭이 아닌 형식은 `Object`의 폐쇄형 제네릭과 동일한 것으로 간주됩니다. 예를 들어, <xref:System.Collections.Generic.List%601> 의 제네릭 <xref:System.DateTime>, 제네릭 <xref:System.ComponentModel.BindingList%601> (개방형 제네릭) 및 <xref:System.Collections.ArrayList> 형식이 참조된 컬렉션 형식이면 다음이 생성됩니다.

[!code-csharp[c_collection_types_in_data_contracts#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#10)]
[!code-vb[c_collection_types_in_data_contracts#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#10)]

목록 컬렉션에서는 다음 표에 있는 것과 같은 경우만 지원됩니다.

|참조된 형식|참조된 형식으로 구현된 인터페이스|예제|처리되는 형식|
|---------------------|----------------------------------------------|-------------|----------------------|
|제네릭이 아닌 형식 또는 폐쇄형 제네릭 형식(매개 변수 수에는 제한 없음)|제네릭이 아닌 형식|`MyType : IList`<br /><br /> 또는<br /><br /> `MyType<T> : IList`<br /><br /> 여기서 T= `int`|`Object` 의 폐쇄형 제네릭 형식(예: `IList<object>`)|
|제네릭이 아닌 형식 또는 폐쇄형 제네릭 형식(컬렉션 형식과 일치하지 않아도 되는 임의의 수의 매개 변수)|폐쇄형 제네릭 형식|`MyType : IList<string>`<br /><br /> 또는<br /><br /> `MyType<T> : IList<string>` 여기서 T=`int`|폐쇄형 제네릭 형식(예: `IList<string>`)|
|여러 개의 매개 변수가 있는 폐쇄형 제네릭 형식|형식의 매개 변수 중 하나를 사용하는 개방형 제네릭 형식|`MyType<T,U,V> : IList<U>`<br /><br /> 여기서 T=`int`, U=`string`, V=`bool`|폐쇄형 제네릭 형식(예: `IList<string>`)|
|하나의 매개 변수가 있는 개방형 제네릭 형식|형식의 매개 변수를 사용하는 개방형 제네릭 형식|`MyType<T> : IList<T>`, T는 개방형|개방형 제네릭 형식(예: `IList<T>`)|

형식에서 두 개 이상의 목록 컬렉션 인터페이스를 구현하는 경우 다음 제한 사항이 적용됩니다.

- 형식에서 제네릭 <xref:System.Collections.Generic.IEnumerable%601> 또는 파생된 인터페이스를 다른 형식으로 여러 번 구현하는 경우 해당 형식은 유효한 참조된 컬렉션 형식으로 간주되지 않고 무시됩니다. 일부 구현이 잘못된 경우 또는 개방형 제네릭을 사용하는 경우에도 마찬가지입니다. 예를 들어, <xref:System.Collections.Generic.IEnumerable%601> 의 제네릭 `int` 및 T의 제네릭 <xref:System.Collections.Generic.IEnumerable%601> 을 구현하는 형식은 `int` 를 허용하는 `Add` 메서드, T 형식의 매개 변수를 허용하는 `int` 메서드 또는 두 메서드 모두가 해당 형식에 있는지 여부와 관계없이 `Add` 또는 다른 형식의 참조된 컬렉션으로 사용되지 않습니다.

- 형식에서 <xref:System.Collections.IList>및 제네릭 컬렉션 인터페이스를 구현하는 경우 제네릭 컬렉션 인터페이스가 <xref:System.Object>형식의 폐쇄형 제네릭이 아니면 해당 형식은 참조된 컬렉션 형식으로 사용되지 않습니다.

사전 컬렉션에서는 다음 표에 있는 것과 같은 경우만 지원됩니다.

|참조된 형식|참조된 형식으로 구현된 인터페이스|예제|처리되는 형식|
|---------------------|----------------------------------------------|-------------|---------------------|
|제네릭이 아닌 형식 또는 폐쇄형 제네릭 형식(매개 변수 수에는 제한 없음)|<xref:System.Collections.IDictionary>|`MyType : IDictionary`<br /><br /> 또는<br /><br /> `MyType<T> : IDictionary` 여기서 T=`int`|폐쇄형 제네릭 형식(예: `IDictionary<object,object>`)|
|폐쇄형 제네릭 형식(여러 개의 매개 변수)|<xref:System.Collections.Generic.IDictionary%602>, 폐쇄형|`MyType<T> : IDictionary<string, bool>` 여기서 T=`int`|폐쇄형 제네릭 형식(예: `IDIctionary<string,bool>`)|
|폐쇄형 제네릭 형식(여러 개의 매개 변수)|제네릭 <xref:System.Collections.Generic.IDictionary%602>, 값 또는 키 중 하나가 폐쇄형이며, 나머지 하나는 개방형이고 형식의 매개 변수 중 하나를 사용|`MyType<T,U,V> : IDictionary<string,V>` 여기서 T=`int`, U=`float`, V=`bool`<br /><br /> 또는<br /><br /> `MyType<Z> : IDictionary<Z,bool>` 여기서 Z=`string`|폐쇄형 제네릭 형식(예: `IDictionary<string,bool>`)|
|폐쇄형 제네릭 형식(여러 개의 매개 변수)|제네릭 <xref:System.Collections.Generic.IDictionary%602>, 키와 값 모두 개방형이고 각각은 형식의 매개 변수 중 하나를 사용|`MyType<T,U,V> : IDictionary<V,U>` 여기서 T=`int`, U=`bool`, V=`string`|폐쇄형 제네릭 형식(예: `IDictionary<string,bool>`)|
|개방형 제네릭 형식(두 개의 매개 변수)|제네릭 <xref:System.Collections.Generic.IDictionary%602>, 개방형, 형식의 제네릭 매개 변수가 나타나는 순서대로 두 개의 매개 변수 모두 사용|`MyType<K,V> : IDictionary<K,V>`, K와 V 모두 개방형|개방형 제네릭 형식(예: `IDictionary<K,V>`)|

형식에서 <xref:System.Collections.IDictionary> 및 제네릭 <xref:System.Collections.Generic.IDictionary%602>를 모두 구현하는 경우 제네릭 <xref:System.Collections.Generic.IDictionary%602> 만 고려됩니다.

부분 제네릭 형식의 참조는 지원되지 않습니다.

예를 들어, 중복은 허용되지 않으므로 <xref:System.Collections.Generic.List%601> 의 제네릭 `Integer` 및 `Integer` 의 제네릭 컬렉션을 <xref:System.Runtime.Serialization.ImportOptions.ReferencedCollectionTypes%2A>에 모두 추가할 수는 없습니다. 이는 정수 목록이 스키마에 있는 경우 사용할 대상을 결정할 수 없기 때문입니다. 중복 문제를 노출하는 형식이 스키마에 있는 경우에만 중복이 감지됩니다. 예를 들어, 가져오는 스키마에 정수 목록이 없는 경우 <xref:System.Collections.Generic.List%601> 의 제네릭 `Integer` 및 `Integer` 에 있는 <xref:System.Runtime.Serialization.ImportOptions.ReferencedCollectionTypes%2A>의 제네릭 컬렉션을 모두 포함할 수 있지만 둘 다 영향을 주지 않습니다.

## <a name="advanced-collection-rules"></a>고급 컬렉션 규칙

### <a name="serializing-collections"></a>컬렉션 serialize

컬렉션 serialization 규칙 목록은 다음과 같습니다.

- 컬렉션의 컬렉션이 있는 컬렉션 형식의 결합이 허용됩니다. 가변 배열은 컬렉션의 컬렉션으로 처리됩니다. 다차원 배열은 지원되지 않습니다.

- 바이트의 배열 및 <xref:System.Xml.XmlNode> 의 배열은 컬렉션이 아닌 기본 형식으로 처리되는 특수 배열 형식입니다. 바이트의 배열을 serialize하면 각 바이트에 대한 별도의 요소 대신 Base64 인코딩된 데이터의 청크가 포함된 하나의 XML 요소가 됩니다. 의 <xref:System.Xml.XmlNode> 배열을 처리 하는 방법에 대 한 자세한 내용은 [데이터 계약의 XML 및 ADO.NET 형식](../../../../docs/framework/wcf/feature-details/xml-and-ado-net-types-in-data-contracts.md)을 참조 하세요. 물론 이러한 특수 형식은 컬렉션에 참여할 수 있습니다. 바이트 배열의 배열은 여러 XML 요소가 되며 각 요소는 Base64 인코딩된 데이터의 청크를 포함합니다.

- <xref:System.Runtime.Serialization.DataContractAttribute> 특성이 컬렉션 형식에 적용되는 경우 해당 형식은 컬렉션이 아닌 일반 데이터 계약 형식으로 처리됩니다.

- 컬렉션 형식이 <xref:System.Xml.Serialization.IXmlSerializable> 인터페이스를 구현하는 경우 `myType:IList<string>, IXmlSerializable`형식이 지정된 다음 규칙이 적용됩니다.

  - 선언된 형식이 `IList<string>`인 경우 형식이 목록으로 serialize됩니다.

  - 선언된 형식이 `myType`인 경우 형식이 `IXmlSerializable`로 serialize됩니다.

  - 선언된 형식이 `IXmlSerializable`인 경우 `IXmlSerializable`로 serialize되지만 `myType` 을 알려진 형식 목록에 추가하는 경우에만 적용됩니다.

- 컬렉션은 다음 표에 나와 있는 메서드를 사용하여 serialize되고 deserialize됩니다.

|컬렉션 형식에서 구현하는 인터페이스|serialization에서 호출된 메서드|deserialization에서 호출된 메서드|
|--------------------------------|-----------------------------------------|-------------------------------------------|
|제네릭 <xref:System.Collections.Generic.IDictionary%602>|`get_Keys`, `get_Values`|제네릭 Add|
|<xref:System.Collections.IDictionary>|`get_Keys`, `get_Values`|`Add`|
|제네릭 <xref:System.Collections.Generic.IList%601>|제네릭 <xref:System.Collections.Generic.IList%601> 인덱서|제네릭 Add|
|제네릭 <xref:System.Collections.Generic.ICollection%601>|열거자|제네릭 Add|
|<xref:System.Collections.IList>|<xref:System.Collections.IList> 인덱서|`Add`|
|제네릭 <xref:System.Collections.Generic.IEnumerable%601>|`GetEnumerator`|적절한 형식(제네릭 매개 변수의 형식 또는 기본 형식 중 하나)의 매개 변수 하나를 사용하는 `Add`라는 비정적 메서드가 호출됩니다. 해당 메서드는 serialization 및 deserialization을 수행하는 동안 serializer에서 컬렉션 형식을 컬렉션으로 처리하도록 존재해야 합니다.|
|<xref:System.Collections.IEnumerable> 및 여기서 파생된 <xref:System.Collections.ICollection>|`GetEnumerator`|`Add` 형식의 매개 변수 하나를 사용하는 `Object`라는 비정적 메서드가 호출됩니다. 해당 메서드는 serialization 및 deserialization을 수행하는 동안 serializer에서 컬렉션 형식을 컬렉션으로 처리하도록 존재해야 합니다.|

위 표에는 컬렉션 인터페이스의 우선 순위가 내림차순으로 나열되어 있습니다. 예를 들어, 형식에서 <xref:System.Collections.IList> 및 제네릭 <xref:System.Collections.Generic.IEnumerable%601>을 모두 구현하는 경우 컬렉션은 다음과 같은 <xref:System.Collections.IList> 규칙에 따라 serialize되고 deserialize됩니다.

- Deserialization을 수행 하는 경우 모든 컬렉션은 먼저 매개 변수가 없는 생성자를 호출 하 여 형식의 인스턴스를 만듭니다 .이 생성자는 직렬화를 수행 하는 동안 열거자가 컬렉션 형식을 컬렉션으로 처리 하는 데 존재 해야 합니다. 역직렬화.

- 동일한 제네릭 컬렉션 인터페이스가 두 번 이상 구현되고(예를 들어, 형식이 <xref:System.Collections.Generic.ICollection%601> 의 제네릭 `Integer` 및 <xref:System.Collections.Generic.ICollection%601> 의 제네릭 <xref:System.String>을 모두 구현하는 경우), 우선 순위가 더 높은 인터페이스가 없는 경우 컬렉션은 유효한 컬렉션으로 처리되지 않습니다.

- 컬렉션 형식은 이 컬렉션 형식에 적용된 <xref:System.SerializableAttribute> 특성을 가질 수 있으며, <xref:System.Runtime.Serialization.ISerializable> 인터페이스를 구현할 수 있습니다. 이 특성 및 인터페이스가 모두 무시됩니다. 그러나 `Add` 메서드가 없는 경우와 같이 형식에서 컬렉션 형식 요구 사항을 충분히 충족하지 않는 경우 형식은 컬렉션 형식으로 간주되지 않으므로 <xref:System.SerializableAttribute> 특성 및 <xref:System.Runtime.Serialization.ISerializable> 인터페이스에 의해 형식이 serialize될 수 있는지 여부가 결정됩니다.

- 컬렉션을 사용자 지정하기 위해 <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 특성을 컬렉션에 적용하면 위의 <xref:System.SerializableAttribute> 대체 메커니즘이 제거됩니다. 대신 사용자 지정된 컬렉션에서 컬렉션 형식 요구 사항을 충족하지 않는 경우 <xref:System.Runtime.Serialization.InvalidDataContractException> 예외가 throw됩니다. 예외 문자열에는 지정 된 형식이 유효한 컬렉션으로 간주 되지 않는 이유를 설명 하는 정보 ( `Add` 메서드 없음, 매개 변수가 없는 생성자 등)가 포함 되어 있으므로 디버깅을 위해 <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 특성을 적용 하는 것이 유용한 경우가 많습니다. 것.

### <a name="collection-naming"></a>컬렉션 명명

컬렉션 명명 규칙 목록은 다음과 같습니다.

- 모든 사전 컬렉션 데이터 계약의 기본 네임 스페이스와 기본 형식이 포함 된 목록 컬렉션 데이터 계약의 기본 네임 스페이스는 네임 `http://schemas.microsoft.com/2003/10/Serialization/Arrays` 스페이스를 사용 하 여 재정의 되지 않는 한입니다. `char`, `Timespan`및 `Guid` 형식과 함께 기본 제공 XSD 형식에 매핑되는 형식은 이러한 목적으로 기본 형식으로 간주됩니다.

- 기본 형식이 아닌 형식이 포함된 컬렉션 형식의 기본 네임스페이스는 Namespace를 사용하여 재정의되지 않는 한 컬렉션에 포함된 형식의 데이터 계약 네임스페이스와 동일합니다.

- 목록 컬렉션 데이터 계약의 기본 이름은 Name을 사용하여 재정의되지 않는 한 컬렉션에 포함된 형식의 데이터 계약 이름과 결합된 문자열인 "ArrayOf"입니다. 예를 들어, 정수의 제네릭 목록에 대한 데이터 계약 이름은 "ArrayOfint"입니다. `Object` 의 데이터 계약 이름은 "anyType"이므로 <xref:System.Collections.ArrayList> 와 같은 제네릭이 아닌 목록의 데이터 계약 이름은 "ArrayOfanyType"입니다.

사전 컬렉션 데이터 계약의 기본 이름은 `Name`을 사용하여 재정의되지 않는 한 값 형식의 데이터 계약 이름 앞에 나오는 키 형식의 데이터 계약 이름과 결합된 문자열 "ArrayOfKeyValueOf"입니다. 예를 들어, 문자열 및 정수의 제네릭 사전에 대한 데이터 계약 이름은 "ArrayOfKeyValueOfstringint"입니다. 또한 키 또는 값 형식 중 하나가 기본 형식이 아닌 경우 키 및 값 형식의 데이터 계약 네임스페이스의 네임스페이스 해시가 이름에 추가됩니다. 네임 스페이스 해시에 대 한 자세한 내용은 [데이터 계약 이름](../../../../docs/framework/wcf/feature-details/data-contract-names.md)을 참조 하세요.

각 사전 컬렉션 데이터 계약에는 사전에 있는 하나의 항목을 나타내는 도우미 데이터 계약이 있습니다. 이 계약의 이름은 "ArrayOf" 접두사를 제외하고 사전 데이터 계약과 동일하며 네임스페이스는 사전 데이터 계약과 동일합니다. 예를 들어, "ArrayOfKeyValueOfstringint" 사전 데이터 계약의 경우 "KeyValueofstringint" 데이터 계약은 사전에 있는 하나의 항목을 나타냅니다. 다음 단원에서 설명한 대로 `ItemName` 속성을 사용하여 이 데이터 계약의 이름을 사용자 지정할 수 있습니다.

제네릭 형식 명명 규칙은 [Data Contract Names](../../../../docs/framework/wcf/feature-details/data-contract-names.md)에서 설명한 대로 컬렉션 형식에 완전히 적용됩니다. 즉, 이름 내에 중괄호를 사용하여 제네릭 형식 매개 변수를 나타낼 수 있습니다. 그러나 괄호 내의 수는 컬렉션 내에 포함된 형식이 아닌 제네릭 매개 변수를 가리킵니다.

## <a name="collection-customization"></a>컬렉션 사용자 지정

<xref:System.Runtime.Serialization.CollectionDataContractAttribute> 특성은 다음과 같이 사용할 수 없으며, 다음과 같이 사용된 경우 <xref:System.Runtime.Serialization.InvalidDataContractException> 예외가 발생합니다.

- <xref:System.Runtime.Serialization.DataContractAttribute> 특성을 <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 특성이 적용된 형식이나 파생 형식 중 하나에 적용

- <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 특성을 <xref:System.Xml.Serialization.IXmlSerializable> 인터페이스를 구현하는 형식에 적용

- <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 특성을 비컬렉션 형식에 적용

- 사전이 아닌 형식에 적용된 <xref:System.Runtime.Serialization.CollectionDataContractAttribute.KeyName%2A> 특성에 <xref:System.Runtime.Serialization.CollectionDataContractAttribute.ValueName%2A> 또는 <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 을 설정하려는 경우

### <a name="polymorphism-rules"></a>다형성 규칙

이미 설명한 바와 같이 <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 특성을 사용하여 컬렉션을 사용자 지정하면 컬렉션 교환 가능성에 방해가 될 수 있습니다. 사전 컬렉션에서 키 및 값 이름뿐만 아니라 사전 컬렉션의 이름, 네임스페이스, 항목 이름이 일치하는 경우에만 사용자 지정된 두 개의 컬렉션 형식을 동일한 것으로 간주할 수 있습니다.

사용자 지정으로 인해 두 개 중 한 컬렉션 데이터 계약이 필요한 곳에 다른 나머지 컬렉션 데이터 계약을 잘못 사용할 수 있습니다. 이러한 경우가 발생해서는 안 됩니다. 다음 형식을 참조하십시오.

[!code-csharp[c_collection_types_in_data_contracts#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_collection_types_in_data_contracts/cs/program.cs#11)]
[!code-vb[c_collection_types_in_data_contracts#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_collection_types_in_data_contracts/vb/program.vb#11)]

이 경우 `Marks1` 의 인스턴스는 `testMarks`에 할당될 수 있습니다. 그러나 데이터 계약이 `Marks2` 데이터 계약과 동일하지 않으므로 `IList<int>` 를 사용해서는 안 됩니다. 데이터 계약 이름은 "arrayofint"가 아니라 "Marks2"이 고, 반복 되는 요소 이름은 "\<\<int >"이 아닌 "mark >"입니다.

다음 표의 규칙은 컬렉션의 다형적 할당에 적용됩니다.

|선언된 형식|사용자 지정되지 않은 컬렉션 할당|사용자 지정된 컬렉션 할당|
|-------------------|--------------------------------------------|---------------------------------------|
|Object|계약 이름이 serialize되어 있습니다.|계약 이름이 serialize되어 있습니다.<br /><br /> 사용자 지정이 사용됩니다.|
|컬렉션 인터페이스|계약 이름이 serialize되어 있지 않습니다.|계약 이름이 serialize되어 있지 않습니다.<br /><br /> 사용자 지정은 사용 되지 않습니다.\*|
|사용자 지정되지 않은 컬렉션|계약 이름이 serialize되어 있지 않습니다.|계약 이름이 serialize되어 있습니다.<br /><br /> 사용자 지정이 사용됩니다.**|
|사용자 지정된 컬렉션|계약 이름이 serialize되어 있습니다. 사용자 지정은 사용 되지 않습니다.\*\*|계약 이름이 serialize되어 있습니다.<br /><br /> 할당 된 형식의 사용자 지정이 사용 됩니다.\*\*|

\*이 경우 <xref:System.Runtime.Serialization.NetDataContractSerializer> 클래스를 사용 하 여 사용자 지정을 사용 합니다. 또한 <xref:System.Runtime.Serialization.NetDataContractSerializer> 클래스는 이 경우의 실제 형식 이름을 serialize하므로 deserialization이 예상대로 작동합니다.

\*\*이러한 경우 스키마에 맞지 않는 인스턴스가 발생 하므로이를 피해 야 합니다.

계약 이름이 serialize된 경우에는 할당된 컬렉션 형식이 알려진 형식 목록에 있어야 합니다. 반대의 경우도 마찬가지입니다. 이름이 serialize되지 않은 경우에는 형식을 알려진 형식 목록에 추가할 필요가 없습니다.

파생 형식의 배열은 기본 형식의 배열에 할당될 수 있습니다. 이 경우 파생 형식의 계약 이름이 반복되는 각 요소에 serialize됩니다. 예를 들어, `Book` 형식이 `LibraryItem`형식에서 파생되는 경우 `Book` 의 배열을 `LibraryItem`의 배열에 할당할 수 있습니다. 이는 다른 컬렉션 형식에 적용되지 않습니다. 예를 들어, `Generic List of Book` 을 `Generic List of LibraryItem`에 할당할 수 없습니다. 그러나 `Generic List of LibraryItem` 인스턴스를 포함하는 `Book` 을 할당할 수는 있습니다. 배열인 경우든 배열이 아닌 경우든 `Book` 은 알려진 형식 목록에 있어야 합니다.

## <a name="collections-and-object-reference-preservation"></a>컬렉션 및 개체 참조 유지

serializer가 개체 참조를 유지하는 모드에서 작동하는 경우 개체 참조 유지도 컬렉션에 적용됩니다. 특히 개체 ID는 전체 컬렉션 및 컬렉션에 포함된 개별 항목 모두에 대해 유지됩니다. 사전의 경우 개체 ID는 키/값 쌍 개체, 개별 키 개체 및 값 개체 모두에 대해 유지됩니다.

## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.CollectionDataContractAttribute>
