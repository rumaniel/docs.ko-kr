---
title: 버전 독립적 Serialization 콜백
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- OnDeserializedAttribute [WCF]
- OnDeserializingAttribute [WCF]
- OnSerializingAttribute [WCF]
- serialization [WCF], setting default values
- OnSerializedAttribute [WCF]
ms.assetid: aa4a3a6f-05ec-4efd-bdbf-2181e13e6468
ms.openlocfilehash: 0736f94b1fe1a91b20ee76da673e0bc139aa802a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69959563"
---
# <a name="version-tolerant-serialization-callbacks"></a>버전 독립적 Serialization 콜백
데이터 계약 프로그래밍 모델에서는 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 및 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> 클래스에서 지원하는 버전 독립적 serialization 콜백 메서드를 완전히 지원합니다.  
  
## <a name="version-tolerant-attributes"></a>버전 독립적 특성  
 4개의 콜백 특성이 있습니다. 각 특성은 다양한 시기에 serialization/deserialization 엔진에서 호출하는 메서드에 적용할 수 있습니다. 다음 표에서는 각 특성을 사용하는 시기에 대해 설명합니다.  
  
|특성|해당 메서드를 호출하는 시기|  
|---------------|---------------------------------------------|  
|<xref:System.Runtime.Serialization.OnSerializingAttribute>|형식을 serialize하기 전에 호출됩니다.|  
|<xref:System.Runtime.Serialization.OnSerializedAttribute>|형식을 serialize한 후에 호출됩니다.|  
|<xref:System.Runtime.Serialization.OnDeserializingAttribute>|형식을 deserialize하기 전에 호출됩니다.|  
|<xref:System.Runtime.Serialization.OnDeserializedAttribute>|형식을 deserialize한 후에 호출됩니다.|  
  
 메서드에서는 <xref:System.Runtime.Serialization.StreamingContext> 매개 변수를 받아야 합니다.  
  
 이 메서드는 주로 버전 지정 또는 초기화에 사용됩니다. deserialization을 수행하는 동안에는 생성자가 호출되지 않습니다. 따라서 들어오는 스트림에 이러한 멤버의 데이터가 없는 경우(예: 데이터가 일부 데이터 멤버가 없는 이전 버전의 형식으로부터 오는 경우) 데이터 멤버가 의도한 기본값으로 올바르게 초기화되지 않을 수 있습니다. 이 문제를 해결하려면 다음 예제처럼 <xref:System.Runtime.Serialization.OnDeserializingAttribute>로 표시된 콜백 메서드를 사용합니다.  
  
 위의 각 콜백 특성에서 형식 당 1개의 메서드만 표시할 수 있습니다.  
  
### <a name="example"></a>예제  
 [!code-csharp[C_DataContract#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#9)]
 [!code-vb[C_DataContract#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#9)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.OnSerializingAttribute>
- <xref:System.Runtime.Serialization.OnSerializedAttribute>
- <xref:System.Runtime.Serialization.OnDeserializingAttribute>
- <xref:System.Runtime.Serialization.OnDeserializedAttribute>
- <xref:System.Runtime.Serialization.StreamingContext>
- [버전 독립적 serialization](../../../standard/serialization/version-tolerant-serialization.md)
