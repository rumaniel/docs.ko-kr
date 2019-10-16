---
title: 데이터 계약의 열거형 형식
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data contracts [WCF], enumeration types
ms.assetid: b5d694da-68cb-4b74-a5fb-75108a68ec3b
ms.openlocfilehash: f8d399859e4f861158ab74db9ed410aec280dbe2
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65586681"
---
# <a name="enumeration-types-in-data-contracts"></a>데이터 계약의 열거형 형식
데이터 계약 모델에 열거형을 표현할 수 있습니다. 이 항목에서는 프로그래밍 모델을 설명하는 여러 예를 살펴봅니다.  
  
## <a name="enumeration-basics"></a>열거형 기본 사항  
 데이터 계약 모델에 열거형 형식을 사용하는 방법 중 하나는 형식에 <xref:System.Runtime.Serialization.DataContractAttribute> 특성을 적용하는 것입니다. 그런 다음 데이터 계약에 포함할 각 멤버에 대해 <xref:System.Runtime.Serialization.EnumMemberAttribute> 특성을 적용해야 합니다.  
  
 다음 예제에서는 두 개의 클래스가 나옵니다. 첫 번째 클래스에서는 열거형을 사용하고, 두 번째 클래스에서는 열거형을 정의합니다.  
  
 [!code-csharp[c_DataContractEnumerations#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#1)]
 [!code-vb[c_DataContractEnumerations#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#1)]  
  
 `Car` 클래스의 인스턴스는 `condition` 필드가 `New`, `Used` 또는 `Rental` 값 중 하나로 설정된 경우에만 보내고 받을 수 있습니다. `condition`이 `Broken` 또는 `Stolen`이면 <xref:System.Runtime.Serialization.SerializationException>이 throw됩니다.  
  
 열거형 데이터 계약에도 보통 때와 같이 <xref:System.Runtime.Serialization.DataContractAttribute> 속성(<xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> 및 <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>)을 사용할 수 있습니다.  
  
### <a name="enumeration-member-values"></a>열거형 멤버 값  
 일반적으로 데이터 계약에는 숫자 값이 아닌 열거형 멤버 이름이 포함됩니다. 그러나 경우 받는 쪽이 WCF 클라이언트 데이터 계약 모델을 사용 하는 경우 내보낸된 스키마는 숫자 값을 유지 합니다. 이 되지 경우 사용 하는 경우는 [XmlSerializer 클래스를 사용 하 여](../../../../docs/framework/wcf/feature-details/using-the-xmlserializer-class.md)입니다.  
  
 앞의 예에서 `condition`이 `Used`로 설정되어 있고 데이터가 XML로 serialize된 경우 결과 XML은 `<condition>Used</condition>`이며 `<condition>1</condition>`이 아닙니다. 따라서 다음 데이터 계약은 `CarConditionEnum`의 데이터 계약에 해당됩니다.  
  
 [!code-csharp[c_DataContractEnumerations#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#2)]
 [!code-vb[c_DataContractEnumerations#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#2)]  
  
 예를 들어, 보내는 쪽에 `CarConditionEnum`을 사용하고 받는 쪽에 `CarConditionWithNumbers`를 사용할 수 있습니다. 보내는 쪽에서는 `Used`에 값 "1"을 사용하고 받는 쪽에서는 값 "20"을 사용하지만 XML 표현은 양쪽 모두 `<condition>Used</condition>`입니다.  
  
 데이터 계약에 포함되려면 <xref:System.Runtime.Serialization.EnumMemberAttribute> 특성을 적용해야 합니다. 항상.NET Framework는 모든 열거형에 대 한 기본 값을 열거형에 특수 값 0 (영)을 적용할 수 있습니다. 하지만 이 특수 값 0도 <xref:System.Runtime.Serialization.EnumMemberAttribute> 특성으로 표시하지 않으면 serialize할 수 없습니다.  
  
 여기에는 두 가지 예외 사항이 있습니다.  
  
- 플래그 열거형(이 항목의 뒷부분에서 설명).  
  
- <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 속성이 `false`로 설정된 열거형 데이터 멤버. 이 경우 값이 0인 열거형은 serialize할 데이터에서 생략됩니다.  
  
### <a name="customizing-enumeration-member-values"></a>열거형 멤버 값 사용자 지정  
 <xref:System.Runtime.Serialization.EnumMemberAttribute.Value%2A> 특성의 <xref:System.Runtime.Serialization.EnumMemberAttribute> 속성을 사용하여 데이터 계약의 일부를 구성하는 열거형 멤버 값을 사용자 지정할 수 있습니다.  
  
 예를 들어, 다음 데이터 계약도 `CarConditionEnum`의 데이터 계약에 해당됩니다.  
  
 [!code-csharp[c_DataContractEnumerations#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#3)]
 [!code-vb[c_DataContractEnumerations#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#3)]  
  
 serialize된 `PreviouslyOwned` 값의 XML 표현은 `<condition>Used</condition>`입니다.  
  
## <a name="simple-enumerations"></a>단순 열거형  
 <xref:System.Runtime.Serialization.DataContractAttribute> 특성이 적용되지 않은 열거형 형식을 serialize할 수도 있습니다. 그러한 열거형 형식은 위 설명과 완전히 같은 방식으로 취급되지만, <xref:System.NonSerializedAttribute> 특성이 적용되지 않은 모든 멤버가 <xref:System.Runtime.Serialization.EnumMemberAttribute> 특성이 적용된 것처럼 취급된다는 점이 다릅니다. 예를 들어, 다음 열거형에는 위의 `CarConditionEnum` 예제에 해당되는 데이터 계약이 암시적으로 존재합니다.  
  
 [!code-csharp[c_DataContractEnumerations#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#6)]
 [!code-vb[c_DataContractEnumerations#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#6)]  
  
 열거형의 데이터 계약 이름 및 네임스페이스와 열거형 멤버 값을 사용자 지정할 필요가 없는 경우 단순 열거형을 사용할 수 있습니다.  
  
#### <a name="notes-on-simple-enumerations"></a>단순 열거형에 대한 참고 사항  
 <xref:System.Runtime.Serialization.EnumMemberAttribute> 특성을 단순 열거형에 적용해도 아무 영향이 없습니다.  
  
 <xref:System.SerializableAttribute> 특성이 열거형에 적용되었는지 여부도 관계 없습니다.  
  
 <xref:System.Runtime.Serialization.DataContractSerializer> 클래스에서 열거형 멤버에 적용된 <xref:System.NonSerializedAttribute> 특성을 따른다는 점은 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 및 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>의 동작과 다릅니다. 이 두 가지 serializer는 모두 <xref:System.NonSerializedAttribute> 특성을 무시합니다.  
  
## <a name="flag-enumerations"></a>플래그 열거형  
 <xref:System.FlagsAttribute> 특성을 열거형에 적용할 수 있습니다. 이 경우 0개 이상의 열거형 값 목록을 동시에 보내거나 받을 수 있습니다.  
  
 그러려면 플래그 열거형에 <xref:System.Runtime.Serialization.DataContractAttribute> 특성을 적용한 다음 2의 거듭제곱에 해당되는 모든 멤버를 <xref:System.Runtime.Serialization.EnumMemberAttribute> 특성으로 표시합니다. 플래그 열거형을 사용하려면 2의 거듭제곱이 끊어지지 않고 순서대로 진행되어야 합니다(예: 1, 2, 4, 8, 16, 32, 64).  
  
 다음 단계는 플래그의 열거형 값을 보내는 경우에 적용됩니다.  
  
1. 숫자 값에 매핑되는 열거형 멤버를 찾아 봅니다(<xref:System.Runtime.Serialization.EnumMemberAttribute> 특성 적용). 찾은 경우 해당 멤버만 포함하는 목록을 보냅니다.  
  
2. 합의 각 부분에 매핑되는 열거형 멤버가 있는(각각 <xref:System.Runtime.Serialization.EnumMemberAttribute> 특성 적용) 숫자 값을 합으로 정리해 봅니다. 해당되는 모든 멤버의 목록을 보냅니다. 합니다 *greedy 알고리즘* 를 사용 하 여 그런 합을 찾이 되며 따라서 합계를 찾을 수 있는 경우에 보장할 수 없습니다. 이 문제를 방지하려면 열거형 멤버의 숫자 값이 2의 거듭제곱이어야 합니다.  
  
3. 앞의 두 단계가 실패한 경우 숫자 값이 0이 아니면 <xref:System.Runtime.Serialization.SerializationException>이 throw됩니다. 숫자 값이 0이면 빈 목록을 보냅니다.  
  
### <a name="example"></a>예제  
 다음 열거형 예는 플래그 작업에 사용할 수 있습니다.  
  
 [!code-csharp[c_DataContractEnumerations#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#4)]
 [!code-vb[c_DataContractEnumerations#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#4)]  
  
 다음 예제의 값은 표시된 대로 serialize됩니다.  
  
 [!code-csharp[c_DataContractEnumerations#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#5)]
 [!code-vb[c_DataContractEnumerations#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#5)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataContractSerializer>
- [데이터 계약 사용](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)
- [서비스 계약에서 데이터 전송 지정](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)
