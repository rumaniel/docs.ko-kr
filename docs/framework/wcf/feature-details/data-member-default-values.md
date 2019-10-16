---
title: 데이터 멤버 기본값
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data members [WCF], default values
- data members [WCF]
ms.assetid: 53a3b505-4b27-444b-b079-0eb84a97cfd8
ms.openlocfilehash: 17e73ab2aa777ae53f31596fa364a4feac297842
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962924"
---
# <a name="data-member-default-values"></a>데이터 멤버 기본값
.NET Framework에서는 형식에 *기본값*의 개념이 있습니다. 예를 들어 참조 형식의 기본값은 `null`이고 정수 형식의 기본값은 0입니다. 기본값으로 설정할 경우 serialize된 데이터에서 데이터 멤버를 생략하는 것이 좋을 수도 있습니다. 멤버에 기본값이 있기 때문에 실제 값을 serialize할 필요가 없으므로 성능이 향상됩니다.  
  
 serialize된 데이터에서 멤버를 생략하려면 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 특성의 <xref:System.Runtime.Serialization.DataMemberAttribute> 속성을 `false`로 설정합니다. 기본값은 `true`입니다.  
  
> [!NOTE]
> 상호 운용성이나 데이터 크기 축소 등 특별히 필요한 경우에만 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 속성을 `false`로 설정해야 합니다.  
  
## <a name="example"></a>예제  
 다음 코드에는 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A>가 `false`로 설정된 여러 멤버가 있습니다.  
  
 [!code-csharp[DataMemberAttribute#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/datamemberattribute/cs/overview.cs#4)]
 [!code-vb[DataMemberAttribute#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/datamemberattribute/vb/overview.vb#4)]  
  
 이 클래스의 인스턴스를 serialize하면 다음과 같은 결과가 나타납니다. `employeeName` 및 `employeeID`가 serialize됩니다. `employeeName` 값이 null이고 `employeeID` 값이 0이면 명시적으로 serialize된 데이터의 일부가 됩니다. 그러나 `position`, `salary` 및 `bonus` 멤버는 serialize되지 않습니다. 마지막으로 57800은 정수에 대한 .NET 기본값인 0과 일치하지 않으므로 `targetSalary` 속성이 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A>로 설정되어 있더라도 `false`는 평소와 같이 serialize됩니다.  
  
### <a name="xml-representation"></a>XML 표현  
 이전 예제가 XML로 serialize될 경우의 표현은 다음과 비슷합니다.  
  
```xml  
<Employee>  
   <employeeName xsi:nil="true" />  
   <employeeID>0</employeeID>  
<targetSalary>57800</targetSalary>  
</Employee>  
```  
  
 `xsi:nil` 특성은 null 값을 명시적으로 나타낼 수 있는 상호 운용 가능한 방법을 제공하는 W3C(World Wide Web Consortium) XML 스키마 인스턴스 네임스페이스의 특수 특성입니다. XML에는 지위, 급여 및 보너스 데이터 멤버에 대한 정보는 없습니다. 받는 측에서 이 값을 `null`, 0 및 `null`로 각각 해석할 수 있습니다. 타사 deserializer에서도 올바른 해석을 한다는 보장이 없으므로 이 패턴은 권장되지 않습니다. <xref:System.Runtime.Serialization.DataContractSerializer> 클래스는 누락된 값에 대해 올바른 해석을 항상 선택합니다.  
  
### <a name="interaction-with-isrequired"></a>IsRequired와의 상호 작용  
 [데이터 계약 버전 관리](../../../../docs/framework/wcf/feature-details/data-contract-versioning.md) <xref:System.Runtime.Serialization.DataMemberAttribute> 에 설명 된 대로 특성 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 에는 속성이 있습니다 (기본값 `false`은). 이 속성은 지정된 데이터 멤버가 deserialize될 때 serialize된 데이터에 있어야 하는지 여부를 나타냅니다. `IsRequired`가 `true`(값이 있어야 함을 표시)로 설정되고 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A>가 `false`(기본값으로 설정된 경우 값이 없어야 함을 표시)로 설정되어 있으면 결과가 모순될 수 있으므로 이 데이터 멤버의 기본값을 serialize할 수 없습니다. 그런 데이터 멤버를 기본값(일반적으로 `null` 또는 0)으로 설정하고 serialization을 시도하면 <xref:System.Runtime.Serialization.SerializationException>가 throw됩니다.  
  
### <a name="schema-representation"></a>스키마 표현  
 `EmitDefaultValue` 속성이 로`false` 설정 된 경우 데이터 멤버의 XSD (XML 스키마 정의 언어) 스키마 표현의 세부 정보에 대 한 자세한 내용은 [데이터 계약 스키마 참조를 참조](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)하세요. 여기서는 개요만 간략하게 설명합니다.  
  
- <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 가 로`false`설정 되 면 스키마에서 WCF (Windows Communication Foundation)에 한정 된 주석으로 표시 됩니다. 이 정보를 나타내는 상호 운용 가능한 방법은 없습니다. 특히 스키마의 "default" 특성은 이 용도로 사용되지 않고, `minOccurs` 특성은 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 설정의 영향만 받고, `nillable` 특성은 데이터 멤버 형식의 영향만 받습니다.  
  
- 사용할 실제 기본값은 스키마에 표시되지 않습니다. 따라서 수신하는 엔드포인트에서 누락된 요소를 적절하게 해석해야 합니다.  
  
 스키마 가져오기에서 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 이전에 언급 된 WCF 관련 주석이 검색 `false` 될 때마다 속성이 자동으로로 설정 됩니다. ASP.NET 웹 서비스를 사용할 `false` 때 일반적으로 발생 하는 `nillable` 특정 상호 운용성 `false` 시나리오를 지원 하기 위해 속성이로 설정 된 참조 형식에 대해서도로 설정 됩니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
