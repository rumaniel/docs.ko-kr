---
title: 데이터 멤버 순서
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data contracts [WCF], ordering members
ms.assetid: 0658a47d-b6e5-4ae0-ba72-ababc3c6ff33
ms.openlocfilehash: d717673139ba810c1593e5c60e488537426f1f64
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64754416"
---
# <a name="data-member-order"></a>데이터 멤버 순서
일부 애플리케이션에서는 serialize된 XML로 표시되는 데이터 순서와 같이 여러 데이터 멤버로부터 데이터가 전송 또는 수신되는 순서를 알고 있는 것이 좋습니다. 이 순서는 경우에 따라 변경해야 할 수 있습니다. 이 항목에서는 순서 지정 규칙에 대해 설명합니다.  
  
## <a name="basic-rules"></a>기본 규칙  
 데이터의 순서를 지정하는 기본 규칙은 다음과 같습니다.  
  
- 데이터 계약 형식이 상속 계층 구조의 일부이면 기본 형식의 데이터 멤버가 항상 첫 번째 순서입니다.  
  
- 그 다음 순서는 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> 특성 집합의 <xref:System.Runtime.Serialization.DataMemberAttribute> 속성을 갖고 있지 않은 현재 형식의 데이터 멤버(사전순)입니다.  
  
- 그리고 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> 특성 집합의 <xref:System.Runtime.Serialization.DataMemberAttribute> 속성을 가진 데이터 멤버가 그 다음 순서입니다. 이러한 멤버의 순서는 먼저 `Order` 속성 값으로 지정되고, 둘 이상의 멤버가 특정 `Order` 값을 갖고 있으면 사전순으로 지정됩니다. 순서 값을 무시할 수도 있습니다.  
  
 사전순은 <xref:System.String.CompareOrdinal%2A> 메서드 호출로 설정됩니다.  
  
## <a name="examples"></a>예제  
 다음과 같은 코드를 생각해 볼 수 있습니다.  
  
 [!code-csharp[C_DataContractNames#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#4)]
 [!code-vb[C_DataContractNames#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#4)]  
  
 XML은 다음과 유사하게 생성됩니다.  
  
```xml  
<DerivedType>  
    <!-- Zebra is a base data member, and appears first. -->  
    <zebra/>   
  
    <!-- Cat has no Order, appears alphabetically first. -->  
    <cat/>  
  
   <!-- Dog has no Order, appears alphabetically last. -->  
    <dog/>   
  
    <!-- Bird is the member with the smallest Order value -->  
    <bird/>  
  
    <!-- Albatross has the next Order value, alphabetically first. -->  
    <albatross/>  
  
    <!-- Parrot, with the next Order value, alphabetically last. -->  
     <parrot/>  
  
    <!-- Antelope is the member with the highest Order value. Note that   
    Order=2 is skipped -->  
     <antelope/>   
</DerivedType>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataContractAttribute>
- [데이터 계약 동등성](../../../../docs/framework/wcf/feature-details/data-contract-equivalence.md)
- [데이터 계약 사용](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)
