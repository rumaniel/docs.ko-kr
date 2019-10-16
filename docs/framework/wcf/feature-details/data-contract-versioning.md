---
title: 데이터 계약 버전 관리
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- versioning [WCF], data contracts
- versioning [WCF]
- data contracts [WCF], versioning
ms.assetid: 4a0700cb-5f5f-4137-8705-3a3ecf06461f
ms.openlocfilehash: 309cd891fd2d764314060e49a401bd1d8f7b8d32
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963261"
---
# <a name="data-contract-versioning"></a>데이터 계약 버전 관리
애플리케이션이 발전하면서 서비스가 사용하는 데이터 계약을 변경해야 할 수도 있습니다. 이 항목에서는 데이터 계약의 버전 관리 방법에 대해 설명합니다. 이 항목에서는 데이터 계약 버전 관리 메커니즘에 대해 설명합니다. 전체 개요 및 규정 된 버전 관리 지침은 모범 사례 [를 참조 하세요. 데이터 계약 버전](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md)관리  
  
## <a name="breaking-vs-nonbreaking-changes"></a>주요 변경 내용 및 주요하지 않은 변경 내용 비교  
 데이터 계약에 대한 변경은 주요 변경 사항이거나 주요 변경 사항이 아닐 수 있습니다. 데이터 계약을 주요 변경 사항이 아닌 것으로 변경할 경우 이전 버전의 계약을 사용하는 애플리케이션은 새 버전을 사용하는 애플리케이션과 통신할 수 있으며, 새 버전의 계약을 사용하는 애플리케이션은 이전 버전을 사용하는 애플리케이션과 통신할 수 있습니다. 반면에 주요 변경 사항은 단방향 또는 양방향으로의 통신을 금지합니다.  
  
 전송 및 수신 방법에 영향을 주지 않는 형식으로의 모든 변경은 주요 변경 사항이 아닙니다. 이러한 변경은 데이터 계약을 변경하지 않고 기본 형식만 변경합니다. 예를 들어 <xref:System.Runtime.Serialization.DataMemberAttribute.Name%2A>의 <xref:System.Runtime.Serialization.DataMemberAttribute> 속성을 이전 버전 이름으로 설정한 경우 주요 변경이 아닌 방법으로 필드 이름을 변경할 수 있습니다. 다음 코드에서는 버전 1의 데이터 계약을 보여 줍니다.  
  
 [!code-csharp[C_DataContractVersioning#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractversioning/cs/source.cs#1)]
 [!code-vb[C_DataContractVersioning#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractversioning/vb/source.vb#1)]  
  
 다음 코드에서는 주요 변경에 해당하지 않는 변경을 보여 줍니다.  
  
 [!code-csharp[C_DataContractVersioning#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractversioning/cs/source.cs#2)]
 [!code-vb[C_DataContractVersioning#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractversioning/vb/source.vb#2)]  
  
 일부 변경은 전송된 데이터를 수정할 수 있지만 주요 변경 사항이거나 아닐 수 있습니다. 다음 변경은 항상 주요 변경 사항입니다.  
  
- 데이터 계약의 <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> 또는 <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A> 값 변경.  
  
- <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A>의 <xref:System.Runtime.Serialization.DataMemberAttribute> 속성을 사용하여 데이터 멤버 순서 변경.  
  
- 데이터 멤버 이름 바꾸기.  
  
- 데이터 멤버의 데이터 계약 변경. 예를 들어 데이터 멤버의 형식을 정수에서 문자열로 변경하거나 "Customer"라는 이름의 데이터 계약 형식을 "Person"이라는 이름의 데이터 계약 형식으로 변경을 말합니다.  
  
 또한 다음 변경도 가능합니다.  
  
## <a name="adding-and-removing-data-members"></a>데이터 멤버 추가 및 제거  
 대부분의 경우 엄격한 스키마 유효성 검사(기존 스키마에 대한 새 인스턴스 유효성 검사)가 필요하지 않는 한 데이터 멤버 추가 또는 제거는 주요 변경 사항이 아닙니다.  
  
 추가 필드의 형식을 누락된 필드의 형식으로 deserialize하는 경우 추가 정보는 무시됩니다. 라운드트립 용으로 저장 될 수도 있습니다. 자세한 내용은 [전방 호환 데이터 계약](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)을 참조 하세요.  
  
 누락된 필드의 형식을 추가 필드 형식으로 deserialize하는 경우 추가 필드는 일반적으로 0 또는 `null`인 기본값으로 지정됩니다. 기본값은 변경 될 수 있습니다. 자세한 내용은 [버전 허용 Serialization 콜백](../../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md)을 참조 하세요.  
  
 예를 들어 클라이언트에서 `CarV1` 클래스를 사용하고 서비스에서 `CarV2` 클래스를 사용하거나, 서비스에서 `CarV1` 클래스를 사용하고 클라이언트에서 `CarV2` 클래스를 사용할 수 있습니다.  
  
 [!code-csharp[C_DataContractVersioning#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractversioning/cs/source.cs#3)]
 [!code-vb[C_DataContractVersioning#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractversioning/vb/source.vb#3)]  
  
 버전 2 엔드포인트가 데이터를 버전 1 엔드포인트에 성공적으로 보낼 수 있습니다. `Car` 데이터 계약의 버전 2를 직렬화하면 다음과 유사한 XML이 생성됩니다.  
  
```xml  
<Car>  
    <Model>Porsche</Model>  
    <HorsePower>300</HorsePower>  
</Car>  
```  
  
 V1에 대한 deserialization 엔진은 `HorsePower` 필드에서 일치하는 데이터 멤버를 찾지 못하고 해당 데이터를 삭제합니다.  
  
 또한 버전 1 엔드포인트가 데이터를 버전 2 엔드포인트에 보낼 수 있습니다. `Car` 데이터 계약의 버전 1을 Serialize하면 다음과 유사하게 XML을 생성합니다.  
  
```xml  
<Car>  
    <Model>Porsche</Model>  
</Car>  
```  
  
 버전 2 deserializer는 들어오는 XML에서 일치하는 데이터가 없기 때문에 `HorsePower` 필드에 설정된 값을 인식하지 못합니다. 대신 해당 필드가 기본값 0으로 설정됩니다.  
  
## <a name="required-data-members"></a>필수 데이터 멤버  
 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A>의 <xref:System.Runtime.Serialization.DataMemberAttribute> 속성을 `true`로 설정하여 데이터 멤버를 필수 항목으로 표시할 수 있습니다. deserialize하는 동안 필수 데이터가 누락되는 경우 데이터 멤버를 기본값으로 설정하는 대신 예외가 throw됩니다.  
  
 필수 데이터 멤버 추가는 주요 변경 사항입니다. 즉, 새 형식을 계속해서 이전 형식의 엔드포인트에 보낼 수 있지만 그 반대의 경우는 수행할 수 없습니다. 또한 이전 모든 버전에서 필수 항목으로 표시된 데이터 멤버 제거도 주요 변경 사항입니다.  
  
 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 속성 값을 `true`에서 `false`로 변경하는 것은 주요 변경 사항이 아니지만, `false`에서 `true`로의 변경은 이전 버전의 형식에 해당 데이터 멤버가 없는 경우 주요 변경 사항이 될 수 있습니다.  
  
> [!NOTE]
> <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 속성을 `true`로 설정하더라도 들어오는 데이터가 null 또는 0이 될 수 있으며 이 가능성을 처리하기 위해 형식을 준비해야 합니다. 잘못된 들어오는 데이터로부터 보호하기 위해 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A>를 보안 메커니즘으로 사용하지 마십시오.  
  
## <a name="omitted-default-values"></a>생략된 기본값  
 `EmitDefaultValue` [데이터 멤버 기본값](../../../../docs/framework/wcf/feature-details/data-member-default-values.md)에 설명 된 대로 DataMemberAttribute 특성의 속성을로 `false`설정 하는 것은 권장 되지 않지만 가능 합니다. 이 설정이 `false`인 경우 데이터 멤버가 기본값(일반적으로 null 또는 0)으로 설정되면 내보내지 않습니다. 이것은 다음 두 가지 방법으로 서로 다른 버전에서 필수 데이터 멤버와 호환되지 않습니다.  
  
- 특정 버전에서 필요한 데이터 멤버를 가진 데이터 계약은 다른 버전에서 `EmitDefaultValue`가 `false`로 설정된 데이터 멤버의 기본(null 또는 0) 데이터를 받을 수 없습니다.  
  
- `EmitDefaultValue`가 `false`로 설정된 필수 데이터 멤버는 기본(null 또는 0) 값을 serialize하는 데 사용할 수 없지만 deserialization 시 이러한 값을 받을 수 있습니다. 이 경우 라운드트립 문제가 발생합니다(데이터를 읽을 수 있지만 동일한 데이터를 작성할 수 없음). 따라서 특정 버전에서 `IsRequired`가 `true`이고 `EmitDefaultValue`가 `false`인 경우, 특정 버전의 데이터 계약이 라운드트립이 발생되지 않는 값을 생성할 수 없도록 다른 모든 버전에 대해 동일한 조합이 적용되어야 합니다.  
  
## <a name="schema-considerations"></a>스키마 고려 사항  
 데이터 계약 형식에 대해 생성 되는 스키마에 대 한 자세한 내용은 [데이터 계약 스키마 참조](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)를 참조 하세요.  
  
 WCF가 데이터 계약 형식에 대해 생성 하는 스키마는 버전 관리를 위한 프로 비전을 수행 하지 않습니다. 즉, 특정 버전 형식에서 내보낸 스키마는 해당 버전에 존재하는 데이터 멤버만 포함합니다. <xref:System.Runtime.Serialization.IExtensibleDataObject> 인터페이스를 구현하더라도 특정 형식의 스키마는 변경되지 않습니다.  
  
 기본적으로 데이터 멤버를 선택적 요소로 스키마에 내보냅니다. 즉, `minOccurs`(XML 특성) 값이 0으로 설정됩니다. 필수 데이터 멤버는 `minOccurs`가 1로 설정된 상태에서 내보냅니다.  
  
 주요 변경이 아닌 것으로 판단되는 많은 변경 사항은 스키마를 엄격하게 적용해야 하는 경우 실제 주요 변경 사항이 됩니다. 이전 예제에서 `CarV1` 요소만 있는 `Model` 인스턴스는 `CarV2` 스키마(`Model` 및 `Horsepower`를 둘 다 포함하지만 모두 선택 사항)에 대해 유효성을 검사합니다. 그러나 그 반대는 성립하지 않습니다. `CarV2` 인스턴스는 `CarV1` 스키마에 대한 유효성 검사에 실패합니다.  
  
 라운드트립에서는 또한 몇 가지 추가로 고려해야 할 사항이 있습니다. 자세한 내용은 [전방 호환 데이터 계약](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)의 "스키마 고려 사항" 섹션을 참조 하세요.  
  
### <a name="other-permitted-changes"></a>기타 허용된 변경 사항  
 <xref:System.Runtime.Serialization.IExtensibleDataObject> 인터페이스 구현은 주요 변경에 해당하지 않습니다. 그러나 <xref:System.Runtime.Serialization.IExtensibleDataObject>를 구현한 버전보다 이전 형식의 버전에는 라운드트립이 지원되지 않습니다. 자세한 내용은 [호환 가능한 데이터 계약](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)을 참조하세요.  
  
## <a name="enumerations"></a>열거형  
 열거형 멤버 추가 또는 제거는 주요 변경 사항입니다. 열거형 멤버 이름 변경은 `EnumMemberAttribute` 특성을 사용하여 계약 이름을 이전 버전과 동일하게 유지하지 않는 한 주요 변경 사항입니다. 자세한 내용은 [데이터 계약의 열거형 형식](../../../../docs/framework/wcf/feature-details/enumeration-types-in-data-contracts.md)을 참조 하세요.  
  
## <a name="collections"></a>컬렉션  
 대부분의 컬렉션 형식이 데이터 계약 모델에서 서로 간에 상호 변경이 가능하기 때문에 대부분의 컬렉션 변경은 주요 변경 사항이 아닙니다. 그러나 사용자 지정되지 않은 컬렉션을 사용자 지정하거나 그 반대로 할 경우 주요 변경 사항이 됩니다. 또한 컬렉션의 사용자 지정 설정 변경은 주요 변경 사항입니다. 즉, 데이터 계약 이름 및 네임스페이스 변경, 요소 이름, 주요 요소 이름 및 값 요소 이름 반복은 주요 변경 사항입니다. 컬렉션 사용자 지정에 대 한 자세한 내용은 [데이터 계약의 컬렉션 형식](../../../../docs/framework/wcf/feature-details/collection-types-in-data-contracts.md)을 참조 하세요.  
기본적으로 컬렉션 콘텐츠 중 데이터 계약 변경(예: 정수 목록에서 문자열 목록으로 변경)은 주요 변경 사항입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataMemberAttribute.Name%2A>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A>
- <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>
- <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A>
- <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A>
- <xref:System.Runtime.Serialization.SerializationException>
- <xref:System.Runtime.Serialization.IExtensibleDataObject>
- [버전 독립적 Serialization 콜백](../../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md)
- [모범 사례: 데이터 계약 버전 관리](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md)
- [데이터 계약 사용](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)
- [데이터 계약 동등성](../../../../docs/framework/wcf/feature-details/data-contract-equivalence.md)
- [이후 버전과 호환되는 데이터 계약](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)
