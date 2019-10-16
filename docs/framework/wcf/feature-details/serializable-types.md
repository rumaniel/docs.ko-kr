---
title: 직렬화 가능 형식
ms.date: 03/30/2017
ms.assetid: f1c8539a-6a79-4413-b294-896f0957b2cd
ms.openlocfilehash: 0913d523e93505934b1cf231284e356baba5ded3
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591665"
---
# <a name="serializable-types"></a>직렬화 가능 형식
기본적으로 <xref:System.Runtime.Serialization.DataContractSerializer>는 모든 공개 형식을 serialize합니다. 이 경우 형식의 모든 공개 읽기/쓰기 속성과 필드가 serialize됩니다.  
  
 <xref:System.Runtime.Serialization.DataContractAttribute> 및 <xref:System.Runtime.Serialization.DataMemberAttribute> 특성을 형식 및 멤버에 적용하여 기본 동작을 변경할 수 있습니다. 이 기능은 제어할 수 없거나 특성을 추가하도록 수정할 수 없는 형식이 있는 경우 유용할 수 있습니다. <xref:System.Runtime.Serialization.DataContractSerializer>는 이러한 "표시되지 않은" 형식을 인식합니다.  
  
## <a name="serialization-defaults"></a>Serialization 기본값  
 <xref:System.Runtime.Serialization.DataContractAttribute> 및 <xref:System.Runtime.Serialization.DataMemberAttribute> 특성을 적용하여 형식 및 멤버의 serialization을 명시적으로 제어하거나 사용자 지정할 수 있습니다. 또한 이러한 특성을 전용 필드에 적용할 수 있습니다. 그러나 이러한 특성으로 표시되지 않은 형식도 serialize 및 deserialize할 수 있습니다. 다음과 같은 규칙 및 예외가 적용됩니다.  
  
- <xref:System.Runtime.Serialization.DataContractSerializer>는 새로 만든 형식의 기본 속성을 사용하여 특성 없이 형식에서 데이터 계약을 유추합니다.  
  
- `get` 특성을 멤버에 적용하지 않으면 모든 공용 필드 및 공용 `set` 및 <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute>메서드가 있는 속성이 serialize됩니다.  
  
- serialization 의미 체계는 <xref:System.Xml.Serialization.XmlSerializer>의 의미 체계와 유사합니다.  
  
- 표시되지 않은 형식에서는 매개 변수를 사용하지 않는 생성자가 있는 공용 형식만 serialize됩니다. 이 규칙의 예외는 <xref:System.Runtime.Serialization.ExtensionDataObject> 인터페이스와 함께 사용되는 <xref:System.Runtime.Serialization.IExtensibleDataObject>입니다.  
  
- 읽기 전용 필드, `get` 또는 `set` 메서드가 없는 속성, 내부 또는 전용 `set` 또는 `get` 메서드가 있는 속성은 serialize되지 않습니다. 이러한 속성은 무시되고 예외가 throw되지 않습니다. get-only 컬렉션의 경우는 예외입니다.  
  
- <xref:System.Xml.Serialization.XmlSerializer> 특성(`XmlElement`, `XmlAttribute`, `XmlIgnore`, `XmlInclude` 등)이 무시됩니다.  
  
- 지정된 형식에 <xref:System.Runtime.Serialization.DataContractAttribute> 특성을 적용하지 않는 경우 serializer는 <xref:System.Runtime.Serialization.DataMemberAttribute> 특성이 적용되는 형식의 모든 멤버를 무시합니다.  
  
- <xref:System.Runtime.Serialization.DataContractSerializer.KnownTypes%2A> 속성은 <xref:System.Runtime.Serialization.DataContractAttribute> 특성으로 표시되지 않는 형식으로 지원됩니다. 여기에는 표시되지 않은 형식에 대한 <xref:System.Runtime.Serialization.KnownTypeAttribute> 특성 지원이 포함됩니다.  
  
- 공용 멤버, 속성 또는 필드에 대한 serialization 프로세스를 "취소"하려면 <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute> 특성을 해당 멤버에 적용합니다.  
  
## <a name="inheritance"></a>상속  
 표시되지 않은 형식(<xref:System.Runtime.Serialization.DataContractAttribute> 특성이 없는 형식)은 이러한 특성을 포함하는 형식에서 상속할 수 있지만 반대의 경우, 즉 특성을 포함하는 형식이 표시되지 않은 형식에서 상속할 수는 없습니다. 이 규칙은 이전 버전의.NET Framework에서 작성 된 코드를 사용 하 여 이전 버전과 호환성에 주로 적용 됩니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- <xref:System.Xml.Serialization.XmlSerializer>
- [데이터 계약 직렬 변환기에서 지원하는 형식](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)
