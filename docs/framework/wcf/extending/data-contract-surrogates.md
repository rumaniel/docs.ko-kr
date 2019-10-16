---
title: 데이터 계약 서로게이트
ms.date: 03/30/2017
helpviewer_keywords:
- data contracts [WCF], surrogates
ms.assetid: 8c31134c-46c5-4ed7-94af-bab0ac0dfce5
ms.openlocfilehash: cc0772cbb35f7c149af7eac04239d7349fa79f27
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70797207"
---
# <a name="data-contract-surrogates"></a>데이터 계약 서로게이트
데이터 계약 *서로게이트* 는 데이터 계약 모델을 기반으로 하는 고급 기능입니다. 이 기능은 사용자가 형식을 메타데이터에 나타내거나 serialize 또는 deserialize하는 방식을 변경하려는 경우 형식 사용자 지정 및 대체에 사용하도록 디자인되었습니다. 서로게이트는 데이터 계약이 형식에 대해 지정되지 않은 경우, 필드와 속성에 <xref:System.Runtime.Serialization.DataMemberAttribute> 특성이 표시되지 않은 경우 또는 사용자가 스키마 변형을 동적으로 만들려는 경우 사용할 수 있습니다.  
  
 serialization 및 deserialization은 <xref:System.Runtime.Serialization.DataContractSerializer>를 사용하여 .NET Framework로부터 XML과 같은 적합한 형식으로 변환할 때 데이터 계약 서로게이트를 통해 수행됩니다. 데이터 계약 서로게이트는 XSD(XML 스키마 문서)와 같은 메타데이터 표현을 생성할 때 형식에 대해 내보낸 메타데이터를 수정하는 데 사용될 수도 있습니다. 가져오기를 수행할 때 코드는 메타데이터에서 만들어지고 이 경우 서로게이트는 생성된 코드를 사용자 지정하는 데 사용될 수도 있습니다.  
  
## <a name="how-the-surrogate-works"></a>서로게이트 작동 방식  
 서로게이트는 한 형식("원래" 형식)에서 다른 형식("서로게이트된" 형식)에 매핑하여 수행됩니다. 다음 예제에서는 원래 형식 `Inventory`와 새 서로게이트 `InventorySurrogated` 형식을 보여 줍니다. `Inventory` 형식은 serialize할 수 없지만 `InventorySurrogated` 형식은 serialize할 수 있습니다.  
  
 [!code-csharp[C_IDataContractSurrogate#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#1)]  
  
 데이터 계약이 이 클래스에 대해 정의되지 않았기 때문에 해당 클래스를 데이터 계약이 있는 서로게이트 클래스로 변환합니다. 서로게이트된 클래스가 아래 예제에 나와 있습니다.  
  
 [!code-csharp[C_IDataContractSurrogate#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#2)]  
  
## <a name="implementing-the-idatacontractsurrogate"></a>IDataContractSurrogate 구현  
 데이터 계약 서로게이트를 사용하려면 <xref:System.Runtime.Serialization.IDataContractSurrogate> 인터페이스를 구현합니다.  
  
 다음은 구현이 가능한 <xref:System.Runtime.Serialization.IDataContractSurrogate>의 각 메서드에 대한 개요입니다.  
  
### <a name="getdatacontracttype"></a>GetDataContractType  
 <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDataContractType%2A> 메서드는 특정 형식을 다른 형식에 매핑합니다. 이 메서드는 serialization, deserialization, 가져오기 및 내보내기에 필요합니다.  
  
 첫 번째 작업은 다른 형식에 매핑할 형식을 정의하는 것입니다. 예를 들어:  
  
 [!code-csharp[C_IDataContractSurrogate#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#3)]  
  
- serialization 시 이 메서드에서 반환되는 매핑은 <xref:System.Runtime.Serialization.IDataContractSurrogate.GetObjectToSerialize%2A> 메서드를 호출하여 이후에 원래 인스턴스를 서로게이트된 인스턴스로 변형하는 데 사용됩니다.  
  
- deserialization 시 이 메서드에서 반환되는 매핑은 serializer가 서로게이트 형식의 인스턴스로 deserialize하는 데 사용합니다. 그런 다음 <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDeserializedObject%2A>를 호출하여 서로게이트된 인스턴스를 원래 형식의 인스턴스로 변환합니다.  
  
- 내보내기를 수행할 때 이 메서드에서 반환되는 서로게이트 형식은 메타데이터 생성에 사용할 데이터 계약을 가져오는 데 반영됩니다.  
  
- 가져오기를 수행할 때 초기 형식은 지원 참조 등의 목적에 사용할 데이터 계약을 가져오는 데 반영되는 서로게이트 형식으로 변경됩니다.  
  
 <xref:System.Type> 매개 변수는 serialize, deserialize, 가져오기 또는 내보내기 중인 개체의 형식입니다. <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDataContractType%2A> 메서드는 서로게이트가 입력 형식을 처리하지 않을 경우 해당 입력 형식을 반환해야 합니다. 그렇지 않으면 서로게이트된 해당 형식을 반환합니다. 서로게이트 형식이 여러 개인 경우 이 메서드에 여러 가지 매핑을 정의할 수 있습니다.  
  
 <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDataContractType%2A> 또는 <xref:System.Int32>과 같은 기본 제공 데이터 계약 기본 형식에 대해 <xref:System.String> 메서드는 호출되지 않습니다. 배열, 사용자 정의 형식 및 기타 데이터 구조 등 다른 형식의 경우 이 메서드는 각 형식에 대해 호출됩니다.  
  
 앞의 예제에서 메서드는 `type` 매개 변수와 `Inventory`가 호환되는지 여부를 확인합니다. 호환되는 경우 메서드는 해당 형식을 `InventorySurrogated`에 매핑합니다. serialization, deserialization, 스키마 가져오기 또는 내보내기가 호출될 때마다 이 함수가 먼저 호출되어 형식 간의 매핑을 확인합니다.  
  
### <a name="getobjecttoserialize-method"></a>GetObjectToSerialize 메서드  
 <xref:System.Runtime.Serialization.IDataContractSurrogate.GetObjectToSerialize%2A> 메서드는 원래 형식 인스턴스를 서로게이트된 형식 인스턴스로 변환합니다. 이 메서드는 serialization에 필요합니다.  
  
 다음 단계는 <xref:System.Runtime.Serialization.IDataContractSurrogate.GetObjectToSerialize%2A> 메서드를 구현하여 물리적 데이터를 원래 인스턴스에서 서로게이트에 매핑하는 방식을 정의하는 것입니다. 예를 들어:  
  
 [!code-csharp[C_IDataContractSurrogate#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#4)]  
  
 <xref:System.Runtime.Serialization.IDataContractSurrogate.GetObjectToSerialize%2A> 메서드는 개체가 serialize되면 호출됩니다. 이 메서드는 원래 형식에서 서로게이트된 형식의 필드로 데이터를 전송합니다. 필드를 직접 서로게이트 필드에 매핑하거나 원래 데이터 조작 내용을 서로게이트에 저장할 수 있습니다. 필드를 직접 매핑하고, 서로게이트된 필드에 저장할 데이터에 대한 작업을 수행하거나 서로게이트된 필드에 원래 형식의 XML을 저장하는 등 일부 작업이 가능합니다.  
  
 `targetType` 매개 변수는 멤버의 선언된 형식을 참조합니다. 이 매개 변수는 <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDataContractType%2A> 메서드에서 반환되는 서로게이트된 형식입니다. serializer는 반환된 개체를 이 형식에 할당할 수 있도록 지정하지 않습니다. `obj` 매개 변수는 serialize 할 개체 이며 필요한 경우 해당 서로게이트로 변환 됩니다. 이 메서드는 서로게이트된 메서드가 입력 개체를 처리하지 않을 경우 해당 입력 개체를 반환해야 합니다. 그렇지 않으면 새 서로게이트 개체가 반환됩니다. 서로게이트는 개체가 null이면 호출되지 않습니다. 이 메서드 내에 다른 인스턴스에 대한 서로게이트 매핑을 여러 개 정의할 수 있습니다.  
  
 <xref:System.Runtime.Serialization.DataContractSerializer>를 만들 때 개체 참조를 유지하도록 지시할 수 있습니다. 자세한 내용은 [Serialization 및 Deserialization](../feature-details/serialization-and-deserialization.md)을 참조 하세요. 이 작업을 수행하려면 해당 생성자의 `preserveObjectReferences` 매개 변수를 `true`로 설정합니다. 이 경우 이후의 모든 serialization이 스트림에 참조를 작성하므로 서로게이트는 개체에 대해 한 번만 호출됩니다. `preserveObjectReferences`가 `false`로 설정된 경우 인스턴스가 나타날 때마다 서로게이트가 호출됩니다.  
  
 serialize된 인스턴스의 형식이 선언된 형식과 다르면 형식 정보가 스트림에 작성됩니다. 예를 들어 `xsi:type`을 사용하면 다른 쪽 끝에서 인스턴스를 deserialize할 수 있습니다. 이 프로세스는 개체가 서로게이트되는지 여부에 따라 발생합니다.  
  
 위의 예제에서는 `Inventory` 인스턴스의 데이터를 `InventorySurrogated`의 데이터로 변환합니다. 개체의 형식을 확인하고 서로게이트된 형식으로 변환하는 데 필요한 조작 작업을 수행합니다. 이 경우 `Inventory` 클래스의 필드는 `InventorySurrogated` 클래스 필드로 직접 복사됩니다.  
  
### <a name="getdeserializedobject-method"></a>GetDeserializedObject 메서드  
 <xref:System.Runtime.Serialization.IDataContractSurrogate.GetDeserializedObject%2A> 메서드는 서로게이트된 형식 인스턴스를 원래 형식 인스턴스로 변환합니다. 이 메서드는 deserialization에 필요합니다.  
  
 다음 작업은 물리적 데이터를 서로게이트 인스턴스에서 원래 인스턴스에 매핑하는 방식을 정의하는 것입니다. 예를 들어:  
  
 [!code-csharp[C_IDataContractSurrogate#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#5)]  
  
 이 메서드는 개체의 deserialization 중에만 호출됩니다. 해당 메서드는 deserialization을 위해 서로게이트 형식에서 다시 원래 형식으로의 데이터 매핑을 취소합니다. `GetObjectToSerialize` 메서드와 비슷한 방식으로 필드 데이터를 직접 교환하고, 데이터에 대한 작업을 수행하며 XML 데이터를 저장하는 등 일부 작업이 가능합니다. deserialize할 때 데이터 변환에서의 조작으로 인해 원래 형식으로부터 정확한 데이터 값을 얻지 못할 수도 있습니다.  
  
 `targetType` 매개 변수는 멤버의 선언된 형식을 참조합니다. 이 매개 변수는 `GetDataContractType` 메서드에서 반환되는 서로게이트된 형식입니다. 매개 `obj` 변수는 deserialize 된 개체를 참조 합니다. 개체가 서로게이트되는 경우 원래 형식으로 다시 변환될 수 있습니다. 이 메서드는 서로게이트가 입력 개체를 처리하지 않을 경우 해당 입력 개체를 반환합니다. 그렇지 않은 경우 변환이 완료되면 deserialize된 개체를 반환합니다. 여러 개의 서로게이트 형식이 존재하는 경우 각 형식과 해당 변환을 나타내어 각 데이터에 대한 서로게이트 형식에서 기본 형식으로 데이터를 변환할 수도 있습니다.  
  
 개체를 반환할 때 내부 개체 테이블은 이 서로게이트에서 반환하는 개체로 업데이트됩니다. 이후의 모든 인스턴스에 대한 참조는 개체 테이블에서 서로게이트된 인스턴스를 가져옵니다.  
  
 앞의 예제에서는 `InventorySurrogated`형식의 개체를 다시 초기 형식 `Inventory`로 변환합니다. 이 경우 데이터는 다시 `InventorySurrogated`에서 `Inventory`의 해당 필드로 직접 전송됩니다. 데이터의 조작된 사항이 없기 때문에 각 멤버 필드에 serialization 전과 같은 값이 포함됩니다.  
  
### <a name="getcustomdatatoexport-method"></a>GetCustomDataToExport 메서드  
 스키마를 내보낼 때 <xref:System.Runtime.Serialization.IDataContractSurrogate.GetCustomDataToExport%2A> 메서드는 선택 사항입니다. 해당 메서드는 내보낸 스키마에 추가 데이터나 힌트를 삽입하는 데 사용됩니다. 추가 데이터는 멤버 수준 또는 형식 수준에서 삽입될 수 있습니다. 예:  
  
 [!code-csharp[C_IDataContractSurrogate#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#6)]  
  
 이 메서드(두 개의 오버로드 사용)를 통해 추가 정보를 멤버 수준 또는 형식 수준의 메타데이터에 포함할 수 있습니다. 멤버가 공용인지 또는 전용인지에 대한 힌트와 스키마 내보내기 및 가져오기를 통해 유지되는 사항에 대한 주석을 포함할 수 있습니다. 그러한 정보는 이 메서드를 사용하지 않을 경우 손실됩니다. 이 메서드로 인해 멤버나 형식이 삽입되거나 삭제되지는 않지만 해당 수준 중 한 수준의 스키마에 데이터가 추가됩니다.  
  
 메서드는 오버로드되고 `Type`(`clrtype` 매개 변수) 또는 <xref:System.Reflection.MemberInfo>(`memberInfo` 매개 변수)를 사용할 수 있습니다. 두 번째 매개 변수는 항상 `Type`(`dataContractType` 매개 변수)입니다. 이 메서드는 서로게이트된 `dataContractType` 형식 및 모든 멤버에 대해 호출됩니다.  
  
 이러한 오버로드 중 하나는 `null` 또는 serialize할 수 있는 개체를 반환해야 합니다. null이 아닌 개체는 내보낸 스키마에 주석으로 serialize됩니다. `Type` 오버로드의 경우 스키마로 내보낸 각 형식은 `dataContractType` 매개 변수로 서로게이트된 형식과 함께 첫 번째 매개 변수의 이 메서드에 보내집니다. `MemberInfo` 오버로드의 경우 스키마로 내보낸 각 멤버는 두 번째 매개 변수의 서로게이트된 형식과 함께 `memberInfo` 매개 변수로 해당 정보를 보냅니다.  
  
#### <a name="getcustomdatatoexport-method-type-type"></a>GetCustomDataToExport 메서드(Type, Type)  
 <xref:System.Runtime.Serialization.IDataContractSurrogate.GetCustomDataToExport%28System.Type%2CSystem.Type%29?displayProperty=nameWithType> 메서드는 모든 형식 정의에 대한 스키마 내보내기 중에 호출됩니다. 이 메서드는 내보낼 때 스키마 내의 형식에 정보를 추가합니다. 스키마에 포함해야 하는 추가 데이터가 있는지 여부를 결정하기 위해 정의된 각 형식이 이 메서드에 보내집니다.  
  
#### <a name="getcustomdatatoexport-method-memberinfo-type"></a>GetCustomDataToExport 메서드(MemberInfo, Type)  
 <xref:System.Runtime.Serialization.IDataContractSurrogate.GetCustomDataToExport%28System.Reflection.MemberInfo%2CSystem.Type%29?displayProperty=nameWithType>는 내보낸 형식의 모든 멤버에 대한 내보내기 중에 호출됩니다. 이 기능을 사용하면 내보낼 때 스키마에 포함되는 멤버에 대한 주석을 사용자 지정할 수 있습니다. 스키마에 다른 데이터를 추가해야 하는지 여부를 확인하기 위해 클래스 내의 모든 멤버에 대한 정보는 이 메서드에 보내집니다.  
  
 위의 예제에서는 서로게이트의 각 멤버에 대한 `dataContractType`을 검색합니다. 그런 다음 각 필드에 적합한 액세스 한정자를 반환합니다. 이 사용자 지정 작업을 수행하지 않으면 액세스 한정자의 기본값은 공용입니다. 따라서 모든 멤버는 실제 액세스 제한에 관계없이 내보낸 스키마를 사용하여 생성된 코드에서 공용으로 정의됩니다. 이 구현을 사용하지 않을 때 멤버 `numpens`는 서로게이트에 전용으로 정의되어 있지만 내보낸 스키마에서는 공용이 됩니다. 이러한 메서드를 사용하면 내보낸 스키마에서 액세스 한정자는 전용으로 생성될 수 있습니다.  
  
### <a name="getreferencedtypeonimport-method"></a>GetReferencedTypeOnImport 메서드  
 이 메서드는 서로게이트의 <xref:System.Type>을 원래 형식에 매핑합니다. 스키마 가져오기에서 이 메서드는 선택 사항입니다.  
  
 스키마를 가져오고 이에 대한 코드를 생성하는 서로게이트를 만들 때 다음 작업은 서로게이트 인스턴스의 형식을 원래 형식으로 정의하는 것입니다.  
  
 생성된 코드가 기존 사용자 형식을 참조해야 하는 경우 <xref:System.Runtime.Serialization.IDataContractSurrogate.GetReferencedTypeOnImport%2A> 메서드를 구현합니다.  
  
 스키마를 가져올 때 이 메서드가 모든 형식 선언에 대해 호출되어 서로게이트된 데이터 계약이 형식에 매핑됩니다. 문자열 매개 변수 `typeName` 및 `typeNamespace`는 서로게이트 형식의 이름과 네임스페이스를 정의합니다. <xref:System.Runtime.Serialization.IDataContractSurrogate.GetReferencedTypeOnImport%2A>에 대한 반환 값은 새 형식을 생성해야 하는지 여부를 결정하는 데 사용됩니다. 이 메서드는 유효한 형식이나 null을 반환해야 합니다. 유효한 형식의 경우 반환된 형식이 생성된 코드에서 참조된 형식으로 사용됩니다. null이 반환되면 형식이 참조되지 않고 새 형식을 만들어야 합니다. 여러 개의 서로게이트가 있는 경우 각 서로게이트 형식을 다시 초기 형식으로 매핑할 수 있습니다.  
  
 `customData` 매개 변수는 <xref:System.Runtime.Serialization.IDataContractSurrogate.GetCustomDataToExport%2A>에서 처음 반환된 개체입니다. 이 `customData`는 서로게이트 작성자가 코드를 생성하기 위해 가져오기를 수행하는 중에 사용할 메타데이터에 추가 데이터/힌트를 삽입할 때 사용됩니다.  
  
### <a name="processimportedtype-method"></a>ProcessImportedType 메서드  
 <xref:System.Runtime.Serialization.IDataContractSurrogate.ProcessImportedType%2A> 메서드는 스키마 가져오기에서 만들어진 모든 형식을 사용자 지정합니다. 이 메서드는 선택 사항입니다.  
  
 스키마를 가져올 때 이 메서드를 사용하면 가져온 형식 및 컴파일 정보를 사용자 지정할 수 있습니다. 예:  
  
 [!code-csharp[C_IDataContractSurrogate#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#7)]  
  
 가져오기 중에 이 메서드는 생성된 모든 형식에 대해 호출됩니다. 지정된 <xref:System.CodeDom.CodeTypeDeclaration>을 변경하거나 <xref:System.CodeDom.CodeCompileUnit>을 수정합니다. 이때 `CodeTypeDeclaration`의 이름, 멤버, 특성 및 기타 여러 속성이 변경됩니다. `CodeCompileUnit`을 처리하여 지시문, 네임스페이스, 참조된 어셈블리 및 기타 여러 특징을 수정할 수 있습니다.  
  
 `CodeTypeDeclaration` 매개 변수에 코드 DOM 형식 선언이 포함됩니다. `CodeCompileUnit` 매개 변수를 사용하면 코드 처리를 수정할 수 있습니다.  `null`을 반환하면 형식 선언이 무시됩니다. 반대로 `CodeTypeDeclaration`을 반환하면 수정 사항이 유지됩니다.  
  
 사용자 지정 데이터를 메타데이터 내보내기 중에 삽입하는 경우에는 가져오기 중에 사용자에게 제공되어야 해당 데이터를 사용할 수 있습니다. 이 사용자 지정 데이터는 모델 힌트 또는 기타 주석을 프로그래밍하는 데 사용할 수 있습니다. 각 `CodeTypeDeclaration` 및 <xref:System.CodeDom.CodeTypeMember> 인스턴스에는 <xref:System.CodeDom.CodeObject.UserData%2A> 형식으로 캐스팅된 `IDataContractSurrogate` 속성으로 사용자 지정 데이터가 포함됩니다.  
  
 위의 예제에서는 가져온 스키마를 일부 변경합니다. 코드는 서로게이트를 사용하여 원래 형식의 전용 멤버를 유지합니다. 스키마를 가져올 때 기본 액세스 한정자는 `public`입니다. 따라서 서로게이트 스키마의 모든 멤버는 이 예제에서처럼 수정하지 않은 경우에 공용이 됩니다. 내보내기 중에 사용자 지정 데이터는 전용 멤버에 대한 메타데이터에 삽입됩니다. 이 예제에서는 사용자 지정 데이터를 찾고, 액세스 한정자가 전용인지 확인한 다음 멤버의 특성을 설정하여 해당 멤버를 전용으로 수정합니다. 이 사용자 지정 작업을 수행하지 않으면 `numpens` 멤버는 전용이 아닌 공용으로 정의됩니다.  
  
### <a name="getknowncustomdatatypes-method"></a>GetKnownCustomDataTypes 메서드  
 이 메서드는 스키마에서 정의된 사용자 지정 데이터 형식을 가져옵니다. 스키마 가져오기에서 이 메서드는 선택 사항입니다.  
  
 해당 메서드는 스키마 내보내기 및 가져오기를 시작할 때 호출됩니다. 이 메서드는 내보내거나 가져온 스키마에 사용되는 사용자 지정 데이터 형식을 반환합니다. 이 메서드는 형식의 컬렉션인 <xref:System.Collections.ObjectModel.Collection%601>(`customDataTypes` 매개 변수)에 전달됩니다. 메서드는 알려진 추가 형식을 이 컬렉션에 추가해야 합니다. 알려진 사용자 지정 데이터 형식은 <xref:System.Runtime.Serialization.DataContractSerializer>를 사용하여 사용자 지정 데이터의 serialization 및 deserialization을 활성화하는 데 필요합니다. 자세한 내용은 [데이터 계약 알려진 형식을](../feature-details/data-contract-known-types.md)합니다.  
  
## <a name="implementing-a-surrogate"></a>서로게이트 구현  
 WCF 내에서 데이터 계약 서로게이트를 사용 하려면 몇 가지 특수 프로시저를 수행 해야 합니다.  
  
### <a name="to-use-a-surrogate-for-serialization-and-deserialization"></a>Serialization 및 Deserialization에 서로게이트를 사용하려면  
 <xref:System.Runtime.Serialization.DataContractSerializer>를 사용하여 서로게이트를 통해 데이터의 serialization 및 deserialization을 수행합니다. <xref:System.Runtime.Serialization.DataContractSerializer>는 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>에 의해 만들어집니다. 서로게이트도 지정해야 합니다.  
  
##### <a name="to-implement-serialization-and-deserialization"></a>serialization 및 deserialization을 구현하려면  
  
1. 서비스에 대한 <xref:System.ServiceModel.ServiceHost>의 인스턴스를 만듭니다. 자세한 지침은 [기본 WCF 프로그래밍](../basic-wcf-programming.md)을 참조 하세요.  
  
2. 지정된 서비스 호스트의 모든 <xref:System.ServiceModel.Description.ServiceEndpoint>에 대해 해당 <xref:System.ServiceModel.Description.OperationDescription>을 찾습니다.  
  
3. <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>의 인스턴스가 있는지 여부를 확인하려면 작업 동작을 검색합니다.  
  
4. <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>가 있는 경우 해당 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.DataContractSurrogate%2A> 속성을 서로게이트의 새 인스턴스로 설정합니다. <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>가 없는 경우 새 인스턴스를 만들고 새 동작의 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.DataContractSurrogate%2A> 멤버를 서로게이트의 새 인스턴스로 설정합니다.  
  
5. 마지막으로 다음 예제처럼 이 새 동작을 현재 작업 동작에 추가합니다.  
  
     [!code-csharp[C_IDataContractSurrogate#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#8)]  
  
### <a name="to-use-a-surrogate-for-metadata-import"></a>메타데이터 가져오기에 서로게이트를 사용하려면  
 클라이언트 측 코드를 생성하기 위해 WSDL 및 XSD와 같은 메타데이터를 가져올 때 XSD 스키마 <xref:System.Runtime.Serialization.XsdDataContractImporter>로부터 코드를 생성하는 구성 요소에 서로게이트를 추가해야 합니다. 이 작업을 수행하려면 메타데이터 가져오기에 사용된 <xref:System.ServiceModel.Description.WsdlImporter>를 직접 수정합니다.  
  
##### <a name="to-implement-a-surrogate-for-metadata-importation"></a>메타데이터 가져오기를 위해 서로게이트를 구현하려면  
  
1. <xref:System.ServiceModel.Description.WsdlImporter> 클래스를 사용하여 메타데이터를 가져옵니다.  
  
2. <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> 메서드를 사용하여 <xref:System.Runtime.Serialization.XsdDataContractImporter>가 정의되었는지 확인합니다.  
  
3. <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> 메서드가 `false`를 반환하는 경우 새 <xref:System.Runtime.Serialization.XsdDataContractImporter>를 만들고 해당 <xref:System.Runtime.Serialization.XsdDataContractImporter.Options%2A> 속성을 <xref:System.Runtime.Serialization.ImportOptions> 클래스의 새 인스턴스로 설정합니다. 그렇지 않으면 `out` 메서드의 <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> 매개 변수에서 반환되는 가져오기를 사용합니다.  
  
4. <xref:System.Runtime.Serialization.XsdDataContractImporter>에 <xref:System.Runtime.Serialization.ImportOptions>가 정의되지 않은 경우 속성을 <xref:System.Runtime.Serialization.ImportOptions> 클래스의 새 인스턴스로 설정합니다.  
  
5. <xref:System.Runtime.Serialization.ImportOptions.DataContractSurrogate%2A>의 <xref:System.Runtime.Serialization.ImportOptions>에 대한 <xref:System.Runtime.Serialization.XsdDataContractImporter> 속성을 서로게이트의 새 인스턴스로 설정합니다.  
  
6. <xref:System.Runtime.Serialization.XsdDataContractImporter>(<xref:System.ServiceModel.Description.MetadataExporter.State%2A> 클래스에서 상속됨)의 <xref:System.ServiceModel.Description.WsdlImporter> 속성에서 반환되는 컬렉션에 <xref:System.ServiceModel.Description.MetadataExporter>를 추가합니다.  
  
7. <xref:System.ServiceModel.Description.WsdlImporter.ImportAllContracts%2A>의 <xref:System.ServiceModel.Description.WsdlImporter> 메서드를 사용하여 스키마 내에 모든 데이터 계약을 가져옵니다. 마지막 단계에서 서로게이트로 호출하여 로드된 스키마에서 코드가 생성됩니다.  
  
     [!code-csharp[C_IDataContractSurrogate#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#9)]  
  
### <a name="to-use-a-surrogate-for-metadata-export"></a>메타데이터 내보내기에 서로게이트를 사용하려면  
 기본적으로 WCF에서 서비스에 대 한 메타 데이터를 내보내는 경우 WSDL 및 XSD 스키마를 모두 생성 해야 합니다. 데이터 계약 형식, <xref:System.Runtime.Serialization.XsdDataContractExporter>에 대한 XSD 스키마를 생성하는 구성 요소에 서로게이트를 추가해야 합니다. 이 작업을 수행하려면 <xref:System.ServiceModel.Description.IWsdlExportExtension>을 구현하는 동작을 사용하여 <xref:System.ServiceModel.Description.WsdlExporter>를 수정하거나 메타데이터 내보내기에 사용된 <xref:System.ServiceModel.Description.WsdlExporter>를 직접 수정합니다.  
  
##### <a name="to-use-a-surrogate-for-metadata-export"></a>메타데이터 내보내기에 서로게이트를 사용하려면  
  
1. 새 <xref:System.ServiceModel.Description.WsdlExporter>를 만들거나 `wsdlExporter` 메서드에 전달된 <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportContract%2A> 매개 변수를 사용합니다.  
  
2. <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> 함수를 사용하여 <xref:System.Runtime.Serialization.XsdDataContractExporter>가 정의되었는지 확인합니다.  
  
3. <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A>가 `false`를 반환하면 <xref:System.Runtime.Serialization.XsdDataContractExporter>에서 생성된 XML 스키마로 새 <xref:System.ServiceModel.Description.WsdlExporter>를 만든 다음 <xref:System.ServiceModel.Description.MetadataExporter.State%2A>의 <xref:System.ServiceModel.Description.WsdlExporter> 속성에서 반환되는 컬렉션에 추가합니다. 그렇지 않으면 `out` 메서드의 <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> 매개 변수에서 반환되는 내보내기를 사용합니다.  
  
4. <xref:System.Runtime.Serialization.XsdDataContractExporter>에 <xref:System.Runtime.Serialization.ExportOptions>가 정의되지 않은 경우 <xref:System.Runtime.Serialization.XsdDataContractExporter.Options%2A> 속성을 <xref:System.Runtime.Serialization.ExportOptions> 클래스의 새 인스턴스로 설정합니다.  
  
5. <xref:System.Runtime.Serialization.ExportOptions.DataContractSurrogate%2A>의 <xref:System.Runtime.Serialization.ExportOptions>에 대한 <xref:System.Runtime.Serialization.XsdDataContractExporter> 속성을 서로게이트의 새 인스턴스로 설정합니다. 메타데이터 내보내기에 대한 이후 단계에서는 변경하지 않아도 됩니다.  
  
     [!code-csharp[C_IDataContractSurrogate#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_idatacontractsurrogate/cs/source.cs#10)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Runtime.Serialization.IDataContractSurrogate>
- <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>
- <xref:System.Runtime.Serialization.ImportOptions>
- <xref:System.Runtime.Serialization.ExportOptions>
- [데이터 계약 사용](../feature-details/using-data-contracts.md)
