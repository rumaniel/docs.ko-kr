---
title: 데이터 계약 이름
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data contracts [WCF], naming
ms.assetid: 31f87e6c-247b-48f5-8e94-b9e1e33d8d09
ms.openlocfilehash: 16a42a2808104a77e56e93564a679dfc578e73f6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61857286"
---
# <a name="data-contract-names"></a>데이터 계약 이름

때때로 클라이언트와 서비스는 동일한 형식을 공유하지 않습니다. 그래도 양쪽의 데이터 계약이 동일하면 서로 데이터를 전달할 수 있습니다. [데이터 계약 동등성](data-contract-equivalence.md) 데이터 계약 및 데이터 멤버 이름을 기반으로 형식 및 멤버 이름에 매핑할 메커니즘을 따라서 제공 됩니다. 이 항목에서는 이름을 만들 경우 Windows Communication Foundation (WCF) 인프라의 기본 동작 뿐만 아니라 데이터 계약 명명 규칙을 설명 합니다.

## <a name="basic-rules"></a>기본 규칙
데이터 계약 이름 지정과 관련된 기본 규칙에는 다음이 포함됩니다.

- 정규화된 데이터 계약 이름은 네임스페이스와 이름으로 구성됩니다.

- 데이터 멤버에는 이름만 있으며, 네임스페이스는 없습니다.

- 데이터 계약을 처리할 때 WCF 인프라는 네임 스페이스와 데이터 계약 및 데이터 멤버의 이름은 대/소문자를 구분 합니다.

## <a name="data-contract-namespaces"></a>데이터 계약 네임스페이스
데이터 계약 네임스페이스는 URI(Uniform Resource Identifier)의 형식을 사용합니다. 절대 URI나 상대 URI일 수 있습니다. 기본적으로 특정 형식에 대한 데이터 계약은 해당 형식의 CLR(공용 언어 런타임) 네임스페이스로부터 가져오는 네임스페이스에 할당됩니다.

기본적으로 주어진된 CLR 네임 스페이스 (형식에서 *Clr.Namespace*)는 네임 스페이스에 매핑되는 `http://schemas.datacontract.org/2004/07/Clr.Namespace`합니다. 이 기본값을 재정의하려면 전체 모듈 또는 어셈블리에 <xref:System.Runtime.Serialization.ContractNamespaceAttribute> 특성을 적용합니다. 또는 각 형식에 대해 데이터 계약 네임스페이스를 제어하려면 <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>의 <xref:System.Runtime.Serialization.DataContractAttribute> 속성을 설정합니다.

> [!NOTE]
> `http://schemas.microsoft.com/2003/10/Serialization` 네임 스페이스 예약 되며 데이터 계약 네임 스페이스를 사용할 수 없습니다.

> [!NOTE]
> `delegate` 선언을 포함하는 데이터 계약 형식에서 기본 네임스페이스를 재정의할 수 없습니다.

## <a name="data-contract-names"></a>데이터 계약 이름
주어진 형식에 대한 데이터 계약의 기본 이름은 해당 형식의 이름입니다. 기본값을 재정의하려면 <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A>의 <xref:System.Runtime.Serialization.DataContractAttribute> 속성을 대체 이름으로 설정합니다. 제네릭 형식에 대한 특정 규칙은 이 항목의 뒷부분에 있는 "제네릭 형식에 대한 데이터 계약 이름"에서 설명합니다.

## <a name="data-member-names"></a>데이터 멤버 이름
주어진 필드 또는 속성에 대한 데이터 멤버의 기본 이름은 해당 필드 또는 속성의 이름입니다. 기본값을 재정의하려면 <xref:System.Runtime.Serialization.DataMemberAttribute.Name%2A>의 <xref:System.Runtime.Serialization.DataMemberAttribute> 속성을 대체 값으로 설정합니다.

### <a name="examples"></a>예제
다음 예제에서는 데이터 계약 및 데이터 멤버의 기본 이름 지정 동작을 재정의할 수 있는 방법을 보여 줍니다.

[!code-csharp[C_DataContractNames#1](~/samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#1)]
[!code-vb[C_DataContractNames#1](~/samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#1)]

## <a name="data-contract-names-for-generic-types"></a>제네릭 형식에 대한 데이터 계약 이름
제네릭 형식에 대한 데이터 계약 이름을 결정하는 데 특별한 규칙이 있습니다. 이러한 규칙은 동일한 제네릭 형식의 폐쇄형 두 개의 제네릭 형식 간에 데이터 계약 이름이 충돌하는 것을 막도록 도와줍니다.

기본적으로 데이터 계약 이름 뒤에 "Of", 문자열 형식의 이름인 제네릭 형식에 대 한 제네릭 매개 변수 뒤에 데이터 계약 이름 뒤에 *해시* 의 데이터 계약 네임 스페이스를 사용 하 여 계산 제네릭 매개 변수입니다. 해시는 데이터 조각을 고유하게 식별하는 "지문"의 역할을 하는 수학 함수의 결과입니다. 모든 제네릭 매개 변수가 기본 형식인 경우 해시는 생략됩니다.

예를 들어 다음 예제의 형식을 참조하십시오.

[!code-csharp[C_DataContractNames#2](~/samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#2)]
[!code-vb[C_DataContractNames#2](~/samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#2)]

이 예제에서 `Drawing<Square,RegularRedBrush>` 형식의 데이터 계약 이름은 "DrawingOfSquareRedBrush5HWGAU6h"이며, 여기서 "5HWGAU6h"는 "urn:shapes" 및 "urn:default" 네임스페이스의 해시입니다. `Drawing<Square,SpecialRedBrush>` 형식의 데이터 계약 이름은 "DrawingOfSquareRedBrushjpB5LgQ_S"이며, 여기서 "jpB5LgQ_S"는 "urn:shapes" 및 "urn:special" 네임스페이스의 해시입니다. 해시를 사용하지 않으면 두 이름이 동일하므로 이름이 충돌합니다.

## <a name="customizing-data-contract-names-for-generic-types"></a>제네릭 형식에 대 한 사용자 지정 데이터 계약 이름

위에서 설명한 것과 같이 제네릭 형식에 대해 생성된 데이터 계약 이름이 허용되지 않는 경우도 있습니다. 예를 들어 이름 충돌이 발생하지 않도록 하려면 해시를 제거해야 할 수 있습니다. 이 경우 사용할 수 있습니다는 <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A?displayProperty=nameWithType> 이름을 생성 하는 다른 방법을 지정 하는 속성입니다. 제네릭 매개 변수의 데이터 계약 이름을 참조하기 위해 `Name` 속성 내에서 중괄호 안에 숫자를 사용할 수 있습니다. 예를 들어 0은 첫 번째 매개 변수를 참조하고, 1은 두 번째 매개 변수를 참조합니다. 해시를 참조하기 위해 중괄호 안에 숫자(#) 기호를 사용할 수 있습니다. 이러한 각각의 참조를 여러 번 사용하거나 전혀 사용하지 않을 수 있습니다.

예를 들어 이전 제네릭 `Drawing` 형식은 다음 예제와 같이 선언되었을 수 있습니다.

[!code-csharp[c_DataContractNames#3](~/samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#3)]
[!code-vb[c_DataContractNames#3](~/samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#3)]

이 경우에는 `Drawing<Square,RegularRedBrush>` 형식의 데이터 계약 이름이 "Drawing_using_RedBrush_brush_and_Square_shape"입니다. <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> 속성에 "{#}"이 있으면 해시가 이름의 일부가 아니므로 형식의 이름을 지정할 때 충돌이 발생하기 쉽습니다. 예를 들어 `Drawing<Square,SpecialRedBrush>` 형식의 데이터 계약 이름이 동일할 수 있습니다.

## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- <xref:System.Runtime.Serialization.ContractNamespaceAttribute>
- [데이터 계약 사용](using-data-contracts.md)
- [데이터 계약 동등성](data-contract-equivalence.md)
- [데이터 계약 이름](data-contract-names.md)
- [데이터 계약 버전 관리](data-contract-versioning.md)
