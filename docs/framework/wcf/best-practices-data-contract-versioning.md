---
title: '모범 사례: 데이터 계약 버전 관리'
ms.date: 03/30/2017
helpviewer_keywords:
- data contracts
- service contracts
- best practices [WCF], data contract versioning
- Windows Communication Foundation, data contracts
ms.assetid: bf0ab338-4d36-4e12-8002-8ebfdeb346cb
ms.openlocfilehash: a56111796b1e301862dcbd9e76a6294c709ea06f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64652149"
---
# <a name="best-practices-data-contract-versioning"></a>모범 사례: 데이터 계약 버전 관리
이 항목에서는 시간 경과에 따라 쉽게 발전할 수 있는 데이터 계약을 만드는 최선의 방법을 보여 줍니다. 데이터 계약에 대 한 자세한 내용은의 항목을 참조 하세요 [Using Data Contracts](../../../docs/framework/wcf/feature-details/using-data-contracts.md)합니다.  
  
## <a name="note-on-schema-validation"></a>스키마 유효성 검사에 대한 참고  
 가 데이터 계약 버전 관리를 설명할 때는, Windows Communication Foundation (WCF)에서 내보낸 데이터 계약 스키마 버전 관리 지원, 기본적으로 요소가 옵션으로 표시 된다는 사실 제외 하지 않았는지 확인 해야 합니다.  
  
 이는 새 데이터 멤버 추가 같은 가장 일반적인 버전 관리 시나리오도 지정된 스키마와 관련해서 매끄럽게 구현할 수 없음을 의미합니다. 예를 들어 새 데이터 멤버가 있는 최신 버전의 데이터 계약은 이전 스키마를 사용하여 유효성이 검사되지 않습니다.  
  
 그러나 엄격한 스키마 준수가 필요하지 않은 많은 시나리오가 있습니다. ASP.NET을 사용 하 여 만든 WCF 및 XML Web services를 비롯 한 많은 웹 서비스 플랫폼에 기본적으로 스키마 유효성 검사를 수행 하지 않으며 따라서 스키마에서 설명 되지 않은 추가 요소를 허용 합니다. 이러한 플랫폼에서 작업할 때는 많은 버전 관리 시나리오를 보다 쉽게 구현할 수 있습니다.  
  
 따라서 데이터 계약 버전 관리 지침에는 엄격한 스키마 유효성이 중요한 시나리오에 대한 집합과 중요하지 않은 시나리오에 대한 집합의 두 가지 집합이 있습니다.  
  
## <a name="versioning-when-schema-validation-is-required"></a>스키마 유효성 검사가 필요한 경우의 버전 관리  
 엄격한 스키마 유효성이 모든 방향(새 버전에서 이전 버전으로 및 이전 버전에서 새 버전으로)에서 필요한 경우 데이터 계약을 변경 불가능한 것으로 간주해야 합니다. 버전 관리가 필요하면 다른 이름이나 네임스페이스로 새 데이터 계약을 만들어야 하며, 해당 데이터 형식을 사용한 서비스 계약의 버전을 적절하게 관리해야 합니다.  
  
 예를 들어 `PoProcessing` 데이터 계약을 준수하는 매개 변수를 사용하는 `PostPurchaseOrder` 작업으로 `PurchaseOrder`이라는 구매 주문 처리 서비스 계약을 가정해 보세요. `PurchaseOrder` 계약을 변경해야 하는 경우 변경 내용을 포함하는 새 데이터 계약 `PurchaseOrder2`를 만들어야 합니다. 그런 다음 서비스 계약 수준에서 버전 관리를 처리해야 합니다. 예를 들어 `PostPurchaseOrder2` 매개 변수를 사용하는 `PurchaseOrder2` 작업을 만들거나 `PoProcessing2` 작업이 `PostPurchaseOrder` 데이터 계약을 사용하는 `PurchaseOrder2` 서비스 계약을 만들어 작업을 수행합니다.  
  
 다른 데이터 계약에서 참조하는 데이터 계약의 변경 내용도 서비스 모델 계층으로 확장됩니다. 예를 들어 이전 시나리오에서 `PurchaseOrder` 데이터 계약을 변경할 필요가 없다고 가정합니다. 그러나 이 데이터 계약에 `Customer` 데이터 계약의 데이터 멤버가 포함되어 있고, 여기에는 변경해야 하는 `Address` 데이터 계약의 데이터 멤버가 들어 있다고 가정합니다. 이 경우 필요한 변경 내용이 포함된 `Address2` 데이터 계약, `Customer2` 데이터 멤버가 포함된 `Address2` 데이터 계약, `PurchaseOrder2` 데이터 멤버가 포함된 `Customer2` 데이터 계약을 만들어야 합니다. 이전 경우와 같이 서비스 계약의 버전을 관리해야 합니다.  
  
 이러한 예제에서는 "2"를 추가하여 이름이 변경되지만 버전 번호나 날짜가 포함된 새 네임스페이스를 추가하여 이름 대신 네임스페이스를 변경하는 것이 좋습니다. 예를 들어 `http://schemas.contoso.com/2005/05/21/PurchaseOrder` 데이터 계약은 `http://schemas.contoso.com/2005/10/14/PurchaseOrder` 데이터 계약으로 변경됩니다.  
  
 자세한 내용은 모범 사례를 참조 하세요. [서비스 버전 관리](../../../docs/framework/wcf/service-versioning.md)합니다.  
  
 경우에 따라 애플리케이션이 보낸 메시지에서 엄격한 스키마 준수를 보장해야 하지만 들어오는 메시지가 엄격하게 스키마를 준수한다고 확신할 수 없습니다. 이 경우 들어오는 메시지에 잘못 사용된 데이터가 포함될 위험이 있습니다. 불필요 한 값이 저장 되 고 WCF에 의해 반환 되므로 스키마에 맞지 않는 메시지가 전송 되 고 있습니다. 이 문제를 방지하려면 왕복 기능을 해제해야 합니다. 그런 경우 두 가지 방법이 있습니다.  
  
- 아무 형식에도 <xref:System.Runtime.Serialization.IExtensibleDataObject> 인터페이스를 구현하지 않습니다.  
  
- <xref:System.ServiceModel.ServiceBehaviorAttribute> 속성을 <xref:System.ServiceModel.ServiceBehaviorAttribute.IgnoreExtensionDataObject%2A>로 설정하여 `true` 특성을 서비스 계약에 적용합니다.  
  
 왕복에 대 한 자세한 내용은 참조 하세요. [이후 버전과 호환 데이터 계약](../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)합니다.  
  
## <a name="versioning-when-schema-validation-is-not-required"></a>스키마 유효성 검사가 필요하지 않은 경우의 버전 관리  
 엄격한 스키마 준수는 거의 필요하지 않습니다. 많은 플랫폼에서 스키마가 설명하지 않는 추가 요소를 허용합니다. 기능의 전체 집합을 설명으로 허용 되는이 [데이터 계약 버전 관리](../../../docs/framework/wcf/feature-details/data-contract-versioning.md) 하 고 [이후 버전과 호환 데이터 계약](../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md) 사용할 수 있습니다. 다음 지침을 따르는 것이 좋습니다.  
  
 이전 버전이 필요한 경우에 새 버전의 형식을 보내거나 새 버전이 필요한 경우에 이전 버전의 형식을 보내려면 일부 지침을 정확하게 따라야 합니다. 다른 지침은 엄격하게 따르지 않아도 되지만 이후 스키마 버전 관리에서 영향을 받을 수 있으므로 여기에 나열되어 있습니다.  
  
1. 형식 상속으로 데이터 계약의 버전을 관리하지 마세요. 이후 버전을 만들려면 기존 형식의 데이터 계약을 변경하거나 관련 없는 새 형식을 만듭니다.  
  
2. 상속이 버전 관리 메커니즘으로 사용되지 않으며 특정 규칙을 따르는 경우 데이터 계약에 상속을 사용할 수 있습니다. 형식이 특정 기본 형식에서 파생되는 경우 동일한 데이터 계약이 없으면 이후 버전에서 해당 형식이 다른 기본 형식에서 파생되게 하지 마세요. 단, 한 가지 예외가 있습니다. 데이터 계약 형식과 기본 형식 간의 계층 구조에 형식을 삽입할 수 있지만 계층 구조에 있는 가능한 모든 다른 형식 버전의 다른 멤버와 동일한 이름을 가진 데이터 멤버가 포함되지 않은 경우에만 삽입할 수 있습니다. 일반적으로 동일한 상속 계층 구조의 여러 수준에서 동일한 이름을 가진 데이터 멤버를 사용하면 심각한 버전 관리 문제가 발생할 수 있으므로 사용하지 않도록 해야 합니다.  
  
3. 데이터 계약의 첫 번째 버전부터 시작하여 항상 <xref:System.Runtime.Serialization.IExtensibleDataObject>를 구현하여 라운드트립을 활성화합니다. 자세한 내용은 [호환 가능한 데이터 계약](../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)을 참조하세요. 이 인터페이스를 구현하지 않고 형식의 버전을 하나 이상 해제한 경우 형식의 다음 버전에서 구현합니다.  
  
4. 이후 버전에서 데이터 계약 이름이나 네임스페이스를 변경하지 마세요. 데이터 계약의 원본으로 사용되는 형식의 이름이나 네임스페이스를 변경하는 경우 <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A>의 <xref:System.Runtime.Serialization.DataContractAttribute> 속성 같은 적절한 메커니즘을 사용하여 데이터 계약 이름과 네임스페이스를 유지해야 합니다. 이름 지정에 대 한 자세한 내용은 참조 하세요. [Data Contract Names](../../../docs/framework/wcf/feature-details/data-contract-names.md)합니다.  
  
5. 이후 버전에서 데이터 멤버의 이름을 변경하지 마세요. 데이터 멤버의 원본으로 사용되는 필드, 속성 또는 이벤트의 이름을 변경하는 경우 `Name`의 <xref:System.Runtime.Serialization.DataMemberAttribute> 속성을 사용하여 기존 데이터 멤버 이름을 유지합니다.  
  
6. 이후 버전에서 데이터 멤버의 원본으로 사용되는 필드, 속성 또는 이벤트의 형식을 변경하지 마세요. 해당 데이터 멤버의 결과 데이터 계약이 변경됩니다. 필요한 데이터 계약을 확인하려면 인터페이스 형식이 <xref:System.Object>와 같다는 것에 주의합니다.  
  
7. 이후 버전에서 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> 특성의 <xref:System.Runtime.Serialization.DataMemberAttribute> 속성을 조정하여 기존 데이터 멤버의 순서를 변경하지 마세요.  
  
8. 이후 버전에서 새 데이터 멤버를 추가할 수 있습니다. 항상 다음 규칙을 따라야 합니다.  
  
    1. <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 속성은 항상 기본값 `false`로 유지되어야 합니다.  
  
    2. 멤버에 대해 기본값 `null` 또는 0을 허용할 수 없는 경우 <xref:System.Runtime.Serialization.OnDeserializingAttribute>로 콜백 메서드를 제공하여 들어오는 스트림에 멤버가 없는 경우 적절한 기본값을 제공해야 합니다. 콜백에 대 한 자세한 내용은 참조 하세요. [버전 독립적 Serialization 콜백](../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md)합니다.  
  
    3. <xref:System.Runtime.Serialization.DataMemberAttribute.Order?displayProperty=nameWithType> 새로 추가 된 데이터 멤버의 모든 기존 데이터 멤버 이후에 표시 되도록 속성을 사용 해야 합니다. 이 작업을 수행 하는 권장된 방법은 아래와 같습니다. 데이터 계약의 첫 번째 버전의 데이터 멤버 없음 있어야 해당 `Order` 속성 집합입니다. 데이터 계약의 버전 2에서 추가된 모든 데이터 멤버의 `Order` 속성을 2로 설정해야 하며 데이터 계약의 버전 3에서 추가된 모든 데이터 멤버의 `Order` 속성을 3으로 설정해야 합니다. 둘 이상의 데이터 멤버를 동일한 `Order` 번호로 설정해도 됩니다.  
  
9. 이전 버전에서 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 속성이 기본값 `false`로 설정된 경우에도 이후 버전에서 데이터 멤버를 제거하지 마세요.  
  
10. 기존 데이터 멤버의 `IsRequired` 속성을 버전 간에 변경하지 마세요.  
  
11. 필수 데이터 멤버의 경우(`IsRequired`가 `true`인 경우) `EmitDefaultValue` 속성을 버전 간에 변경하지 마세요.  
  
12. 분기된 버전 관리 계층 구조를 만들지 마세요. 즉, 이러한 지침에서 허용하는 변경 내용만 사용하여 특정 버전에서 다른 버전으로 적어도 한 방향의 경로가 항상 있어야 합니다.  
  
     예를 들어 Person 데이터의 버전 1에 Name 데이터 멤버만 포함된 경우 Age 멤버만 추가하여 계약의 2a 버전과 Address 멤버만 추가하여 2b 버전을 만들면 안 됩니다. 2a에서 2b로 이동하려면 Age를 제거하고 Address를 추가해야 하며, 반대 방향으로 이동하려면 Address를 제거하고 Age를 추가해야 합니다. 멤버 제거는 이러한 지침에서 허용되지 않습니다.  
  
13. 일반적으로 애플리케이션의 새 버전에서 기존 데이터 계약 형식의 새 하위 형식을 만들면 안 됩니다. 마찬가지로 Object 또는 인터페이스 형식으로 선언된 데이터 멤버 대신 사용할 새 데이터 계약을 만들면 안 됩니다. 이전 애플리케이션의 모든 인스턴스의 알려진 형식 목록에 새 형식을 추가할 수 있는 경우에만 이러한 새 클래스를 만들 수 있습니다. 예를 들어 애플리케이션의 버전 1에서는 Book 및 Newspaper 데이터 계약 하위 형식이 포함된 LibraryItem 데이터 계약 형식이 있을 수 있습니다. LibraryItem은 Book 및 Newspaper를 포함하는 알려진 형식 목록을 갖습니다. 이제 LibraryItem의 하위 형식인 Magazine 형식을 버전 2에 추가한다고 가정합니다. Magazine 인스턴스를 버전 2에서 버전 1로 보내는 경우 Magazine 데이터 계약이 알려진 형식 목록에 없으며 예외가 throw됩니다.  
  
14. 버전 간에 열거형 멤버를 추가하거나 제거하면 안 됩니다. 또한 `EnumMemberAttribute` 특성의 Name 속성을 사용하여 데이터 계약 모델의 이름을 동일하게 유지하지 않는 한 열거형 멤버의 이름을 바꾸면 안 됩니다.  
  
15. 컬렉션 데이터 계약 모델에 설명 된 대로 서로 [데이터 계약의 컬렉션 형식](../../../docs/framework/wcf/feature-details/collection-types-in-data-contracts.md)합니다. 이 경우 유연성이 증가합니다. 그러나 버전 간에 상호 교환할 수 없는 방식으로 컬렉션 형식을 실수로 변경하지 않도록 해야 합니다. 예를 들어 사용자 지정되지 않은 컬렉션(즉, `CollectionDataContractAttribute` 특성이 없는 컬렉션)에서 사용자 지정 컬렉션으로 변경하거나 그 반대로 변경하지 마세요. 또한 버전 간에 `CollectionDataContractAttribute`의 속성을 변경하지 마세요. 허용되는 유일한 변경은 내장 컬렉션 형식의 이름 또는 네임스페이스가 변경되었으며 데이터 계약 이름과 네임스페이스를 이전 버전과 동일하게 만들어야 하는 경우의 Name 또는 Namespace 속성 추가입니다.  
  
 특별한 경우 여기에 나열된 일부 지침을 무시해도 됩니다. 지침을 벗어나기 전에 관련된 serialization, deserialization 및 스키마 메커니즘을 완전히 이해해야 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A>
- <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A>
- <xref:System.Runtime.Serialization.IExtensibleDataObject>
- <xref:System.ServiceModel.ServiceBehaviorAttribute>
- <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A>
- <xref:System.Runtime.Serialization.ExtensionDataObject>
- <xref:System.Runtime.Serialization.OnDeserializingAttribute>
- [데이터 계약 사용](../../../docs/framework/wcf/feature-details/using-data-contracts.md)
- [데이터 계약 버전 관리](../../../docs/framework/wcf/feature-details/data-contract-versioning.md)
- [데이터 계약 이름](../../../docs/framework/wcf/feature-details/data-contract-names.md)
- [이후 버전과 호환되는 데이터 계약](../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)
- [버전 독립적 Serialization 콜백](../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md)
