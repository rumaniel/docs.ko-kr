---
title: 데이터 계약 알려진 형식
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data contracts [WCF], known types
- KnownTypeAttribute [WCF]
- KnownTypes [WCF]
ms.assetid: 1a0baea1-27b7-470d-9136-5bbad86c4337
ms.openlocfilehash: 2ab0a41e87a9b14d1beac9fb0c39586f0ea16a4a
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70040192"
---
# <a name="data-contract-known-types"></a>데이터 계약 알려진 형식
<xref:System.Runtime.Serialization.KnownTypeAttribute> 클래스를 사용하면 고려 사항에 포함해야 하는 형식을 deserialization을 수행하는 동안 미리 지정할 수 있습니다. 작업 예제는 [Known Types](../../../../docs/framework/wcf/samples/known-types.md) 예제를 참조하십시오.  
  
 일반적으로 클라이언트와 서비스 간에 매개 변수와 반환 값을 전달할 때 두 끝점은 전송할 데이터의 모든 데이터 계약을 공유합니다. 그러나 다음과 같은 경우는 그렇지 않습니다.  
  
- 보낸 데이터 계약은 필요한 데이터 계약에서 파생됩니다. 자세한 내용은 [데이터 계약 동등성](../../../../docs/framework/wcf/feature-details/data-contract-equivalence.md)의 상속에 대 한 섹션을 참조 하세요. 이 경우 전송한 데이터에는 수신하는 끝점에서 필요한 것과 동일한 데이터 계약이 없습니다.  
  
- 전송할 정보에 대해 선언된 형식은 클래스, 구조체 또는 열거형이 아니라 인터페이스입니다. 따라서 인터페이스를 구현하는 형식을 실제로 보냈는지 미리 알 수 없으므로 수신하는 끝점에서 전송된 데이터에 대한 데이터 계약을 미리 확인할 수 없습니다.  
  
- 전송할 정보에 대해 선언된 형식은 <xref:System.Object>입니다. 모든 형식은 <xref:System.Object>에서 상속되며 실제로 보낸 형식을 미리 알 수 없으므로 수신하는 끝점에서 전송된 데이터에 대한 데이터 계약을 미리 확인할 수 없습니다. 이는 첫 번째 항목의 특별 한 경우입니다. 모든 데이터 계약은에 대해 <xref:System.Object>생성 되는 빈 데이터 계약 인 기본값에서 파생 됩니다.  
  
- .NET Framework 형식을 포함 하는 일부 형식에는 앞의 세 범주 중 하나에 있는 멤버가 있습니다. 예를 들어 <xref:System.Collections.Hashtable> 은 <xref:System.Object> 를 사용하여 해시 테이블에 실제 개체를 저장합니다. 이러한 형식을 serialize할 때 받는 쪽에서 이러한 멤버에 대한 데이터 계약을 미리 확인할 수 없습니다.  
  
## <a name="the-knowntypeattribute-class"></a>KnownTypeAttribute 클래스  
 데이터가 수신 끝점에 도착 하면 WCF 런타임에서는 CLR (공용 언어 런타임) 형식의 인스턴스로 데이터를 deserialize 하려고 합니다. deserialization을 위해 인스턴스화되는 형식은 메시지 내용이 따르는 데이터 계약을 확인하도록 들어오는 메시지를 먼저 검사하여 선택됩니다. 그런 다음 deserialization 엔진은 메시지 내용과 호환되는 데이터 계약을 구현하는 CLR 형식을 찾습니다. 이 프로세스 중에 deserialization 엔진에서 허용하는 후보 형식 집합을 deserializer의 "알려진 형식" 집합이라고 합니다.  
  
 deserialization 엔진에 형식을 알리는 한 가지 방법은 <xref:System.Runtime.Serialization.KnownTypeAttribute>를 사용하는 것입니다. 특성은 개별 데이터 멤버에 적용될 수 없고 전체 데이터 계약 형식에만 적용될 수 있습니다. 특성은 클래스 또는 구조체일 수 있는 *외부 형식* 에 적용됩니다. 가장 기본적인 사용법에서 특성을 적용하면 형식이 "알려진 형식"으로 지정됩니다. 이렇게 하면 외부 형식의 개체 또는 해당 멤버를 통해 참조되는 개체가 deserialize될 때마다 알려진 형식이 알려진 형식 집합의 일부가 됩니다. 두 개 이상의 <xref:System.Runtime.Serialization.KnownTypeAttribute> 특성을 같은 형식에 적용할 수 있습니다.  
  
## <a name="known-types-and-primitives"></a>알려진 형식 및 기본 형식  
 기본 형식과 기본 형식으로 처리되는 특정 형식(예: <xref:System.DateTime> 및 <xref:System.Xml.XmlElement>)은 항상 "알려진" 형식이므로 이 메커니즘을 통해 추가되지 않아도 됩니다. 그러나 기본 형식 배열은 명시적으로 추가되어야 합니다. 대부분의 컬렉션은 배열과 동일한 것으로 간주됩니다. 제네릭이 아닌 컬렉션은 <xref:System.Object>의 배열과 동일한 것으로 간주됩니다. 기본 형식, 기본 배열 및 기본 컬렉션 사용 예제는 예제 4를 참조하십시오.  
  
> [!NOTE]
> 다른 기본 형식과 달리 <xref:System.DateTimeOffset> 구조체는 기본적으로 알려진 형식이 아니므로 이 형식을 알려진 형식 목록에 수동으로 추가해야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예제에서는 사용 중인 <xref:System.Runtime.Serialization.KnownTypeAttribute> 클래스를 보여 줍니다.  
  
#### <a name="example-1"></a>예제 1  
 상속 관계가 있는 세 클래스가 있습니다.  
  
 [!code-csharp[C_KnownTypeAttribute#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#1)]
 [!code-vb[C_KnownTypeAttribute#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#1)]  
  
 `CompanyLogo` 멤버가 `ShapeOfLogo` 또는 `CircleType` 개체로 설정된 경우 deserialization 엔진이 데이터 계약 이름 "Circle" 또는 "Triangle"을 포함하는 형식을 인식하지 않으므로 다음 `TriangleType` 클래스를 serialize할 수 있지만 deserialize할 수는 없습니다.  
  
 [!code-csharp[C_KnownTypeAttribute#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#2)]
 [!code-vb[C_KnownTypeAttribute#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#2)]  
  
 `CompanyLogo` 형식을 쓰는 올바른 방법은 다음 코드에 나와 있습니다.  
  
 [!code-csharp[C_KnownTypeAttribute#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#3)]
 [!code-vb[C_KnownTypeAttribute#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#3)]  
  
 외부 형식 `CompanyLogo2` 가 deserialize될 때마다 deserialization 엔진이 `CircleType` 및 `TriangleType` 에 대해 알고 있으므로, "Circle" 및 "Triangle" 데이터 계약에 일치하는 형식을 찾을 수 있습니다.  
  
#### <a name="example-2"></a>예제 2  
 다음 예제에서 `CustomerTypeA` 및 `CustomerTypeB` 에 모두 `Customer` 데이터 계약이 있어도 `CustomerTypeB` 만 deserialization 엔진에 알려지므로 `PurchaseOrder` 가 deserialize될 때마다 `CustomerTypeB` 의 인스턴스가 만들어집니다.  
  
 [!code-csharp[C_KnownTypeAttribute#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#4)]
 [!code-vb[C_KnownTypeAttribute#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#4)]  
  
#### <a name="example-3"></a>예제 3  
 다음 예제에서 <xref:System.Collections.Hashtable> 은 해당 콘텐츠를 내부적으로 <xref:System.Object>로 저장합니다. 해시 테이블을 성공적으로 deserialize하려면 deserialization 엔진이 해시 테이블에서 발생할 수 있는 가능한 형식 집합을 알고 있어야 합니다. 이 경우 `Book` 및 `Magazine` 개체만 `Catalog`에 저장되므로 이러한 개체가 <xref:System.Runtime.Serialization.KnownTypeAttribute> 특성을 사용하여 추가된다는 것을 미리 알고 있습니다.  
  
 [!code-csharp[C_KnownTypeAttribute#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#5)]
 [!code-vb[C_KnownTypeAttribute#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#5)]  
  
#### <a name="example-4"></a>예제 4  
 다음 예제에서 데이터 계약은 숫자와 숫자에 수행할 작업을 저장합니다. `Numbers` 데이터 멤버는 정수, 정수 배열 또는 정수를 포함하는 <xref:System.Collections.Generic.List%601> 일 수 있습니다.  
  
> [!CAUTION]
> 이는 SVCUTIL.EXE를 사용하여 WCF 프록시를 생성하는 경우 클라이언트 쪽에서만 작동합니다. SVCUTIL.EXE는 서비스에서 알려진 형식을 비롯한 메타데이터를 검색합니다. 이 정보가 없으면 클라이언트가 형식을 deserialize할 수 없게 됩니다.  
  
 [!code-csharp[C_KnownTypeAttribute#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#6)]
 [!code-vb[C_KnownTypeAttribute#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#6)]  
  
 이것은 애플리케이션 코드입니다.  
  
 [!code-csharp[C_KnownTypeAttribute#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#7)]
 [!code-vb[C_KnownTypeAttribute#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#7)]  
  
## <a name="known-types-inheritance-and-interfaces"></a>알려진 형식, 상속 및 인터페이스  
 알려진 형식이 `KnownTypeAttribute` 특성을 사용하여 특정 형식과 연결되면 이 알려진 형식은 해당 형식의 모든 파생 형식과도 연결됩니다. 예를 들어 다음과 같은 코드를 참조하십시오.  
  
 [!code-csharp[C_KnownTypeAttribute#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#8)]
 [!code-vb[C_KnownTypeAttribute#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#8)]  
  
 `DoubleDrawing` 필드에서 `KnownTypeAttribute` 및 `Square` 을 사용할 `Circle` 특성이 기본 클래스( `AdditionalShape` )에 이미 적용되었기 때문에`Drawing`클래스에는 이러한 특성이 필요하지 않습니다.  
  
 알려진 형식은 인터페이스가 아닌 클래스와 구조체에만 연결할 수 있습니다.  
  
## <a name="known-types-using-open-generic-methods"></a>개방형 제네릭 메서드를 사용한 알려진 형식  
 제네릭 형식을 알려진 형식으로 추가해야 할 수 있습니다. 하지만 개방형 제네릭 형식은 `KnownTypeAttribute` 특성에 대한 매개 변수로 전달될 수 없습니다.  
  
 이 문제는 대체 메커니즘을 사용 하 여 해결할 수 있습니다. 알려진 형식 컬렉션에 추가할 형식 목록을 반환 하는 메서드를 작성 합니다. 그런 다음 몇 가지 제한 사항으로 인해 이 메서드 이름이 `KnownTypeAttribute` 특성에 대한 문자열 인수로 지정됩니다.  
  
 이 메서드는 `KnownTypeAttribute` 특성이 적용되는 형식에 있어야 하고, static 메서드여야 하며, 매개 변수를 취하지 않아야 하고, <xref:System.Collections.IEnumerable> 의 <xref:System.Type>에 할당될 수 있는 개체를 반환해야 합니다.  
  
 `KnownTypeAttribute` 특성을 메서드 이름과 결합하거나 `KnownTypeAttribute` 특성을 같은 형식의 실제 형식과 결합할 수 없습니다. 또한 메서드 이름이 있는 두 개 이상의 `KnownTypeAttribute` 를 같은 형식에 적용할 수 없습니다.  
  
 다음 클래스를 참조하십시오.  
  
 [!code-csharp[C_KnownTypeAttribute#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#9)]
 [!code-vb[C_KnownTypeAttribute#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#9)]  
  
 `theDrawing` 필드에는 제네릭 클래스 `ColorDrawing` 과 제네릭 클래스 `BlackAndWhiteDrawing`의 인스턴스가 포함되어 있으며, 모두 제네릭 클래스 `Drawing`에서 상속됩니다. 일반적으로 두 클래스 모두 알려진 형식에 추가해야 하지만 다음 예제는 올바른 특성 구문이 아닙니다.  
  
```csharp  
// Invalid syntax for attributes:  
// [KnownType(typeof(ColorDrawing<T>))]  
// [KnownType(typeof(BlackAndWhiteDrawing<T>))]  
```  
  
```vb  
' Invalid syntax for attributes:  
' <KnownType(GetType(ColorDrawing(Of T))), _  
' KnownType(GetType(BlackAndWhiteDrawing(Of T)))>  
```  
  
 그러므로 이러한 형식을 반환할 메서드를 만들어야 합니다. 이 형식을 쓰는 올바른 방법은 다음 코드에 나와 있습니다.  
  
 [!code-csharp[C_KnownTypeAttribute#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_knowntypeattribute/cs/source.cs#10)]
 [!code-vb[C_KnownTypeAttribute#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_knowntypeattribute/vb/source.vb#10)]  
  
## <a name="additional-ways-to-add-known-types"></a>알려진 형식을 추가하는 다른 방법  
 또한 구성 파일을 통해 알려진 형식을 추가할 수 있습니다. 이는 WCF (Windows Communication Foundation)에서 타사 형식 라이브러리를 사용 하는 경우와 같이 적절 한 deserialization에 알려진 형식이 필요한 형식을 제어 하지 않을 때 유용 합니다.  
  
 다음 구성 파일에서는 구성 파일에 알려진 형식을 지정하는 방법을 보여 줍니다.  
  
 `<configuration>`  
  
 `<system.runtime.serialization>`  
  
 `<dataContractSerializer>`  
  
 `<declaredTypes>`  
  
 `<add type="MyCompany.Library.Shape,`  
  
 `MyAssembly, Version=2.0.0.0, Culture=neutral,`  
  
 `PublicKeyToken=XXXXXX, processorArchitecture=MSIL">`  
  
 `<knownType type="MyCompany.Library.Circle,`  
  
 `MyAssembly, Version=2.0.0.0, Culture=neutral,`  
  
 `PublicKeyToken=XXXXXX, processorArchitecture=MSIL"/>`  
  
 `</add>`  
  
 `</declaredTypes>`  
  
 `</dataContractSerializer>`  
  
 `</system.runtime.serialization>`  
  
 `</configuration>`  
  
 앞의 구성 파일에서는 `MyCompany.Library.Shape` 라는 데이터 계약 형식이 `MyCompany.Library.Circle` 을 알려진 형식으로 포함하도록 선언되었습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.KnownTypeAttribute>
- <xref:System.Collections.Hashtable>
- <xref:System.Object>
- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Runtime.Serialization.DataContractSerializer.KnownTypes%2A>
- [알려진 형식](../../../../docs/framework/wcf/samples/known-types.md)
- [데이터 계약 동등성](../../../../docs/framework/wcf/feature-details/data-contract-equivalence.md)
- [서비스 계약 디자인](../../../../docs/framework/wcf/designing-service-contracts.md)
