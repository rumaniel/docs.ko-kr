---
title: 서비스 버전 관리
ms.date: 03/30/2017
ms.assetid: 37575ead-d820-4a67-8059-da11a2ab48e2
ms.openlocfilehash: f3cb01531c594df5262963567438b47cbbed58a2
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923012"
---
# <a name="service-versioning"></a>서비스 버전 관리
서비스 및 서비스가 노출하는 엔드포인트는 비즈니스 요구의 변경, 정보 기술의 요구 사항 또는 다른 문제 해결 등의 다양한 이유 때문에 최초로 배포된 후, 수명 동안 여러 차례에 걸쳐 변경되어야 할 수 있습니다. 각 변경 작업에는 새 버전의 서비스가 도입됩니다. 이 항목에서는 WCF (Windows Communication Foundation)에서 버전 관리를 고려 하는 방법에 대해 설명 합니다.  
  
## <a name="four-categories-of-service-changes"></a>서비스 변경의 네 가지 범주  
 변경될 수 있는 서비스는 다음과 같이 네 가지 범주로 분류할 수 있습니다.  
  
- 계약 변경 내용: 예를 들어 작업이 추가 되거나 메시지의 데이터 요소가 추가 되거나 변경 될 수 있습니다.  
  
- 주소 변경: 예를 들어 서비스는 끝점에 새 주소가 있는 다른 위치로 이동 합니다.  
  
- 바인딩 변경 내용: 예를 들어 보안 메커니즘이 변경 되거나 설정이 변경 됩니다.  
  
- 구현 변경 내용: 예를 들어 내부 메서드 구현이 변경 되는 경우입니다.  
  
 이러한 변경 중 일부는 "주요" 변경 내용이고, 나머지는 "주요하지 않은" 변경 내용입니다. 이전 버전에서 성공적으로 처리 된 모든 메시지가 새 버전에서 성공적으로 처리 되 면 변경 내용이 *줄 바꿈하지* 않습니다. 이 조건을 충족 하지 않는 변경 내용은 *주요* 변경 내용입니다.  
  
## <a name="service-orientation-and-versioning"></a>서비스 방향 및 버전 관리  
 서비스 방향의 개념 중 하나는 서비스와 클라이언트가 자율적 또는 독립적이라는 것입니다. 특히, 이는 서비스 개발자가 모든 서비스 클라이언트를 제어한다거나, 심지어 알고 있다고도 가정할 수 없음을 의미합니다. 이로 인해 서비스의 버전이 변경될 때 모든 클라이언트를 다시 빌드하고 다시 배포할 수 없습니다. 이 항목에서는 서비스가 이러한 개념을 따르기 때문에 해당 클라이언트와 독립적으로 변경되거나 "버전 관리"되어야 한다고 가정합니다.  
  
 예기치 않게 주요 내용이 변경되고 이를 피할 수 없는 경우, 애플리케이션에서는 이 개념을 무시하도록 선택할 수 있으며, 서비스의 새 버전으로 클라이언트가 다시 빌드되고 다시 배포되도록 만들 수 있습니다.  
  
## <a name="contract-versioning"></a>계약 버전 관리  
 클라이언트에서 사용하는 계약과 서비스에서 사용하는 계약이 동일해야 할 필요는 없습니다. 이 둘을 호환할 수만 있으면 됩니다.  
  
 서비스 계약의 경우, 호환성이란 서비스에 의해 노출되는 새 작업을 추가할 수는 있지만 기존 작업을 제거하거나 의미상 변경할 수는 없다는 것을 뜻합니다.  
  
 데이터 계약의 경우, 호환성은 새 스키마 형식의 정의를 추가할 수는 있지만 기존 스키마 형식의 정의를 주요한 방법으로 변경할 수는 없다는 것을 뜻합니다. 주요 변경 내용에는 데이터 멤버를 제거하거나 데이터 형식을 호환되지 않게 변경하는 것이 포함됩니다. 이 기능을 사용하면 서비스가 클라이언트를 중단시키지 않고도 해당 계약의 버전을 일부 변경할 수 있습니다. 다음 두 섹션에서는 WCF 데이터 및 서비스 계약에 적용할 수 있는 줄 바꿈하지 않는 변경 내용 및 주요 변경 내용에 대해 설명 합니다.  
  
## <a name="data-contract-versioning"></a>데이터 계약 버전 관리  
 이 단원에서는 <xref:System.Runtime.Serialization.DataContractSerializer> 및 <xref:System.Runtime.Serialization.DataContractAttribute> 클래스를 사용할 때의 데이터 버전 관리에 대해 설명합니다.  
  
### <a name="strict-versioning"></a>엄격한 버전 관리  
 버전 변경이 문제가 되는 많은 시나리오에서 서비스 개발자는 클라이언트를 제어할 수 있는 권한이 없습니다. 따라서 메시지 XML 또는 스키마에서의 변경 내용에 대응하는 방법을 가정할 수 없습니다. 이러한 경우, 다음 두 가지 이유로 새 메시지가 기존 스키마에 대해 유효성을 검사할 수 있어야 합니다.  
  
- 이전 버전의 클라이언트는 스키마가 변경되지 않는다는 가정 하에 개발되었습니다. 이전 버전의 클라이언트는 개발 시에 처리할 수 있도록 설정된 메시지 외에는 메시지를 처리하지 못할 수도 있습니다.  
  
- 이전 클라이언트는 메시지를 처리하려고 시도하기 전에 이전 스키마에 대해 스키마 유효성 검사를 수행할 수 있습니다.  
  
 이러한 시나리오에서는 기존 데이터 계약을 변경할 수 없는 것으로 간주하고, 정규화된 고유 XML 이름을 가진 새 항목을 만드는 것이 좋습니다. 그런 다음 서비스 개발자는 기존 서비스 계약에 새 메서드를 추가하거나, 새 데이터 계약을 사용하는 메서드로 새 서비스 계약을 만들 수 있습니다.  
  
 서비스 개발자가 데이터 계약의 모든 버전에서 실행해야 하는 비즈니스 논리를 작성하고, 이와 함께 계약의 각 버전별로 실행해야 하는 비즈니스 코드를 작성해야 하는 경우에 이러한 방법이 많이 사용됩니다. 이 항목의 끝에 있는 부록에서는 인터페이스를 사용하여 이와 같은 경우를 처리하는 방법에 대해 설명합니다.  
  
### <a name="lax-versioning"></a>Lax 버전 관리  
 다른 여러 시나리오에서 서비스 개발자는 새 선택적 멤버를 데이터 계약에 추가해도 기존 클라이언트가 중지되지 않는다고 가정할 수 있습니다. 이를 위해서 서비스 개발자는 기존 클라이언트가 스키마 유효성 검사를 수행하지 않고 있으며, 알려지지 않은 데이터 멤버를 무시하는지를 조사해야 합니다. 이러한 시나리오에서는 주요하지 않은 변경 방법으로 새 멤버를 추가하기 위해 데이터 계약 기능을 활용할 수 있습니다. 서비스 개발자는 버전 관리를 위한 데이터 계약 기능을 이미 서비스의 첫 번째 버전에 대해 사용한 경우 안전하게 이렇게 가정할 수 있습니다.  
  
 WCF, ASP.NET 웹 서비스 및 기타 많은 웹 서비스 스택은 *느슨한 버전 관리*를 지원 합니다. 즉, 수신 된 데이터에서 알 수 없는 새 데이터 멤버에 대 한 예외를 throw 하지 않습니다.  
  
 새 멤버를 추가해도 기존 클라이언트가 중지되지 않을 것이라고 잘못 생각할 수도 있습니다. 모든 클라이언트가 lax 버전 관리를 처리할 수 있는지 확신할 수 없는 경우에는 엄격한 버전 관리 지침을 사용하고, 데이터 계약을 변경할 수 없는 것으로 간주하는 것이 좋습니다.  
  
 데이터 계약의 느슨한 버전과 엄격한 버전 관리에 대 한 자세한 지침은 모범 [사례를 참조 하세요. 데이터 계약 버전](../../../docs/framework/wcf/best-practices-data-contract-versioning.md)관리  
  
### <a name="distinguishing-between-data-contract-and-net-types"></a>데이터 계약과 .NET 형식 구별  
 <xref:System.Runtime.Serialization.DataContractAttribute> 특성을 클래스에 적용해서 .NET 클래스 또는 구조를 데이터 계약으로 나타낼 수 있습니다. .NET 형식 및 해당 데이터 계약 프로젝션은 서로 다른 별개의 문제입니다. 여러 .NET 형식에서 동일한 데이터 계약 프로젝션을 사용할 수 있습니다. 이러한 구분은 특히 표시된 데이터 계약을 유지 관리하여 엄밀한 의미에서 기존 클라이언트와의 호환성을 유지하기 위하여 .NET 형식을 변경할 때 유용합니다. .NET 형식과 데이터 계약의 이러한 구분을 유지하기 위해서는 다음 두 가지 사항을 항상 수행해야 합니다.  
  
- <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> 및 <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>를 지정합니다. 사용자의 .NET 형식 이름 및 네임스페이스가 계약에서 노출되지 않도록 하려면 데이터 계약의 이름 및 네임스페이스를 항상 지정해야 합니다. 이 방법으로 .NET 네임스페이스 또는 형식 이름을 나중에 변경하려는 경우 데이터 계약은 동일하게 유지됩니다.  
  
- <xref:System.Runtime.Serialization.DataMemberAttribute.Name%2A>을 지정합니다. 사용자의 .NET 멤버 이름이 계약에서 노출되지 않도록 하려면 데이터 멤버의 이름을 항상 지정해야 합니다. 이 방법으로 멤버의 .NET 이름을 나중에 변경하려는 경우 데이터 계약은 동일하게 유지됩니다.  
  
### <a name="changing-or-removing-members"></a>멤버 변경 또는 제거  
 멤버의 이름이나 데이터 형식을 변경하거나 데이터 멤버를 제거하는 것은 lax 버전 관리가 허용되어 있더라도 주요 변경 내용입니다. 이러한 변경이 필요하면 새 데이터 계약을 만들어야 합니다.  
  
 서비스 호환성이 매우 중요할 경우 사용자 코드에서 사용되지 않는 데이터 멤버를 무시하고 이를 그대로 남겨두는 것을 고려해 볼 수 있습니다. 하나의 데이터 멤버를 여러 멤버로 분할하는 경우, 하위 수준의 클라이언트(최신 버전으로 업그레이드 되지 않는 클라이언트)에 대해 필수 분할 및 재집계를 수행할 수 있는 속성으로 기존 멤버를 그대로 남겨두는 것을 고려할 수 있습니다.  
  
 마찬가지로 데이터 계약의 이름 또는 네임스페이스를 변경하는 것은 주요한 변경 내용입니다.  
  
### <a name="round-trips-of-unknown-data"></a>알 수 없는 데이터의 라운드트립  
 일부 시나리오에서는 새 버전에 추가된 멤버의 알 수 없는 데이터를 "라운드트립"해야 할 수 있습니다. 예를 들어 "versionNew" 서비스는 일부 새로 추가된 멤버와 함께 데이터를 "versionOld" 클라이언트로 보냅니다. 클라이언트는 메시지를 처리할 때 새로 추가된 멤버를 무시하지만, 새로 추가된 멤버를 포함하여 동일한 데이터를 versionNew 서비스로 다시 보냅니다. 이에 대한 일반 시나리오는 데이터를 서비스에서 검색하고, 변경하고, 반환하는 데이터 업데이트입니다.  
  
 특정 형식의 라운드트립을 사용하려면 형식이 <xref:System.Runtime.Serialization.IExtensibleDataObject> 인터페이스를 구현해야 합니다. 인터페이스에는 <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> 형식을 반환하는 속성 중 하나인 <xref:System.Runtime.Serialization.ExtensionDataObject>가 포함되어 있습니다. 속성은 현재 버전에서는 알 수 없는 이후 버전 데이터 계약의 모든 데이터를 저장하는 데 사용됩니다. 이 데이터는 클라이언트에 불분명하지만 인스턴스가 serialize될 때 <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> 속성의 콘텐츠는 데이터 계약 멤버의 나머지 데이터와 함께 작성됩니다.  
  
 사용자의 모든 형식이 이 인터페이스를 구현하여 이후의 알 수 없는 새 멤버를 수용하는 것이 좋습니다.  
  
### <a name="data-contract-libraries"></a>데이터 계약 라이브러리  
 계약이 중앙 리포지토리에 게시되고 서비스 및 형식 구현자가 해당 리포지토리로부터 데이터 계약을 구현하고 노출하는 데이터 계약의 라이브러리가 있을 수 있습니다. 이 경우에는 사용자가 리포지토리에 데이터 계약을 게시할 때 이를 구현하는 형식을 만드는 사람을 제어할 수 있는 권한이 없습니다. 그러므로 계약이 게시되고 나면 변경할 수 없도록 효과적으로 계약을 렌더링하므로 수정할 수 없습니다.  
  
### <a name="when-using-the-xmlserializer"></a>XmlSerializer를 사용하는 경우  
 <xref:System.Xml.Serialization.XmlSerializer> 클래스를 사용할 때는 동일한 버전 관리 원칙이 적용됩니다. 엄격한 버전 관리가 필요할 경우 데이터 계약을 변할 수 없는 것으로 간주하고, 새 버전에 대한 정규화된 고유 이름을 가진 새 데이터 계약을 만들어야 합니다. lax 버전 관리를 사용할 수 있는 경우 serialize할 수 있는 새 멤버를 새 버전에 추가할 수 있지만 기존 멤버를 변경하거나 제거할 수는 없습니다.  
  
> [!NOTE]
> <xref:System.Xml.Serialization.XmlSerializer>에서는 <xref:System.Xml.Serialization.XmlAnyElementAttribute> 및 <xref:System.Xml.Serialization.XmlAnyAttributeAttribute> 특성을 사용하여 알 수 없는 데이터의 라운드트립을 지원합니다.  
  
## <a name="message-contract-versioning"></a>메시지 계약 버전 관리  
 메시지 계약 버전 관리에 대한 지침은 데이터 계약 버전 관리와 매우 유사합니다. 엄격한 버전 관리가 필요할 경우 메시지 본문을 변경하는 대신 정규화된 고유 이름을 가진 새 메시지 계약을 만들어야 합니다. lax 버전 지정을 사용할 수 있는 경우에는 새 메시지 본문 부분을 추가할 수 있지만 기존 부분을 변경하거나 제거할 수 없습니다. 이 지침은 기본 메시지 계약과 래핑된 메시지 계약 둘 다에 적용됩니다.  
  
 메시지 헤더는 항상 추가할 수 있습니다. 이는 엄격한 버전 관리를 사용 중인 경우에도 해당합니다. MustUnderstand 플래그가 버전 관리에 영향을 줄 수 있습니다. 일반적으로 WCF의 헤더에 대 한 버전 관리 모델은 SOAP 사양에 설명 된 것과 같습니다.  
  
## <a name="service-contract-versioning"></a>서비스 계약 버전 관리  
 데이터 계약 버전 관리와 마찬가지로 서비스 계약 버전 관리에는 작업 추가, 변경 및 제거가 포함됩니다.  
  
### <a name="specifying-name-namespace-and-action"></a>이름, 네임스페이스 및 동작 지정  
 기본적으로 서비스 계약의 이름은 인터페이스의 이름입니다. 기본 네임 스페이스는 "http://tempuri.org"이 고 각 작업의 작업은 "http://tempuri.org/contractname/methodname"입니다. 서비스 계약에 대 한 이름 및 네임 스페이스를 명시적으로 지정 하는 것이 좋으며, "http://tempuri.org"를 사용 하지 않고 인터페이스 및 메서드 이름이 서비스의 계약에서 노출 되지 않도록 방지 하기 위한 작업입니다.  
  
### <a name="adding-parameters-and-operations"></a>매개 변수 및 작업 추가  
 서비스에 의해 노출된 서비스 작업을 추가하는 것은 주요하지 않은 변경 내용입니다. 이러한 새 작업에서는 기존 클라이언트의 요구를 고려하지 않아도 되기 때문입니다.  
  
> [!NOTE]
> 작업을 이중 콜백 계약에 추가하는 것은 주요 변경 내용입니다.  
  
### <a name="changing-operation-parameter-or-return-types"></a>작업 매개 변수 또는 반환 형식 변경  
 기존 형식에서 구현한 데이터 계약을 새 형식에서 동일하게 구현하지 않는 경우, 매개 변수 또는 반환 형식을 변경하는 것은 일반적으로 주요한 변경 내용입니다. 이러한 변경을 위해서 새 작업을 서비스 계약에 추가하거나 새 서비스 계약을 정의합니다.  
  
### <a name="removing-operations"></a>제거 작업  
 제거 작업도 주요한 변경 내용입니다. 이러한 변경을 위해서 새 서비스 계약을 정의하고 이를 새 엔드포인트에서 노출합니다.  
  
### <a name="fault-contracts"></a>오류 계약  
 서비스 계약 개발자는 <xref:System.ServiceModel.FaultContractAttribute> 특성을 사용하여 계약 작업에서 반환될 수 있는 오류의 정보를 지정할 수 있습니다.  
  
 서비스 계약에 설명된 오류 목록은 전체 목록으로 간주되지 않습니다. 어떤 경우에든 작업은 해당 계약에 설명되어 있지 않은 오류를 반환할 수 있습니다. 그러므로 계약에서 설명된 오류 집합을 변경하는 것은 주요한 변경 내용으로 간주되지 않습니다. <xref:System.ServiceModel.FaultContractAttribute>를 사용하여 새 오류를 계약에 추가하거나, 계약으로부터 기존 오류를 제거하는 것을 예로 들 수 있습니다.  
  
### <a name="service-contract-libraries"></a>서비스 계약 라이브러리  
 조직에서는 계약 라이브러리를 가질 수 있으며, 여기서 계약은 중앙 리포지토리에 게시되고 서비스 구현자는 해당 리포지토리로부터 계약을 구현합니다. 이 경우에는 사용자가 리포지토리에 서비스 계약을 게시할 때 이를 구현하는 서비스를 만드는 사람을 제어할 수 있는 권한이 없습니다. 그러므로 서비스 계약이 게시되고 나면 변경할 수 없도록 서비스 계약이 효과적으로 렌더링되어 수정할 수 없습니다. WCF는 기존 계약을 확장 하는 새 계약을 만드는 데 사용할 수 있는 계약 상속을 지원 합니다. 이 기능을 사용하려면 이전 서비스 계약 인터페이스로부터 상속된 새 서비스 계약 인터페이스를 정의한 다음 새 인터페이스에 메서드를 추가합니다. 그런 다음 이전 계약을 구현하는 서비스를 변경하여 새 계약을 구현하고, "versionOld" 엔드포인트 정의를 변경하여 새 계약을 사용합니다. 엔드포인트는 "versionOld" 클라이언트에 대해서는 "versionOld" 계약을 노출하면서 계속 표시되고, "versionNew" 클라이언트에 대해서는 "versionNew" 계약을 노출하기 위해 표시됩니다.  
  
## <a name="address-and-binding-versioning"></a>주소 및 바인딩 버전 관리  
 클라이언트에서 새 엔드포인트 주소 또는 바인딩을 동적으로 검색할 수 없는 경우, 엔드포인트 주소 및 바인딩에 대한 변경 내용은 주요 변경 내용입니다. 이 기능을 구현하는 메커니즘 중 하나는 UDDI(Universal Description, Discovery, and Integration) 레지스트리 및 UDDI 호출 패턴을 사용하는 것입니다. 여기서 클라이언트는 엔드포인트와 통신하려고 시도하며, 실패 시 현재 엔드포인트 메타데이터에 대해 잘 알려진 UDDI 레지스트리를 쿼리합니다. 그런 다음 클라이언트는 이 메타데이터의 주소 및 바인딩을 사용하여 엔드포인트와 통신합니다. 이 통신이 성공하면 클라이언트는 나중에 사용할 수 있도록 주소 및 바인딩 정보를 캐시합니다.  
  
## <a name="routing-service-and-versioning"></a>라우팅 서비스 및 버전 관리  
 서비스 변경이 주요한 변경이고 서로 다른 버전의 서비스를 두 개 이상 동시에 실행해야 하면 WCF 라우팅 서비스를 사용하여 적절한 서비스 인스턴스에 메시지를 라우팅할 수 있습니다. WCF 라우팅 서비스는 콘텐츠 기반 라우팅을 사용합니다. 즉, 메시지 내의 정보를 사용하여 메시지를 라우팅할 위치를 확인합니다. WCF 라우팅 서비스에 대 한 자세한 내용은 [라우팅 서비스](../../../docs/framework/wcf/feature-details/routing-service.md)를 참조 하세요. 서비스 버전 관리 [를 위해 WCF 라우팅 서비스를 사용 하는 방법에 대 한 예제는 방법: 서비스 버전](../../../docs/framework/wcf/feature-details/how-to-service-versioning.md)관리.  
  
## <a name="appendix"></a>부록  
 엄격한 버전 관리가 필요한 경우 일반 데이터 계약 버전 관리 지침을 변경 불가능한 데이터 계약으로 간주하고, 변경이 필요한 경우 새 항목을 만듭니다. 새로운 각 데이터 계약에 대해 새 클래스를 만들어야 하므로 이전 데이터 계약 클래스의 측면에서 작성된 기존 코드를 사용하지 않고, 새 데이터 계약 클래스의 측면에서 코드를 새로 작성하기 위한 메커니즘이 필요합니다.  
  
 이러한 메커니즘 중 하나는 인터페이스를 사용하여 각 데이터 계약의 멤버를 정의하고, 해당 인터페이스를 구현하는 데이터 계약 클래스가 아닌 인터페이스 측면의 내부 구현 코드를 작성하는 것입니다. 서비스의 버전 1에 대한 다음 코드에서는 `IPurchaseOrderV1` 인터페이스와 `PurchaseOrderV1`을 보여 줍니다.  
  
```  
public interface IPurchaseOrderV1  
{  
    string OrderId { get; set; }  
    string CustomerId { get; set; }  
}  
  
[DataContract(  
Name = "PurchaseOrder",  
Namespace = "http://examples.microsoft.com/WCF/2005/10/PurchaseOrder")]  
public class PurchaseOrderV1 : IPurchaseOrderV1  
{  
    [DataMember(...)]  
    public string OrderId {...}  
    [DataMember(...)]  
    public string CustomerId {...}  
}  
```  
  
 서비스 계약 작업은 `PurchaseOrderV1`의 측면에서 작성되지만, 실제 비즈니스 논리는 `IPurchaseOrderV1`의 측면에서 작성됩니다. 그런 다음, 버전 2에서는 다음 코드에서처럼 새 `IPurchaseOrderV2` 인터페이스와 새 `PurchaseOrderV2` 클래스가 있을 수 있습니다.  
  
```  
public interface IPurchaseOrderV2  
{  
    DateTime OrderDate { get; set; }  
}

[DataContract(   
Name = "PurchaseOrder",  
Namespace = "http://examples.microsoft.com/WCF/2006/02/PurchaseOrder")]  
public class PurchaseOrderV2 : IPurchaseOrderV1, IPurchaseOrderV2  
{  
    [DataMember(...)]  
    public string OrderId {...}  
    [DataMember(...)]  
    public string CustomerId {...}  
    [DataMember(...)]  
    public DateTime OrderDate { ... }  
}  
```  
  
 서비스 계약이 업데이트되어 `PurchaseOrderV2`의 측면에서 작성되는 새 작업을 포함할 수 있습니다. `IPurchaseOrderV1`의 측면에서 작성된 기존 비즈니스 논리라도 `PurchaseOrderV2`에 대한 작업을 계속할 수 있으며, `OrderDate` 속성을 필요로 하는 새 비즈니스 논리도 `IPurchaseOrderV2`의 측면에서 작성될 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A>
- <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>
- <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A>
- <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A>
- <xref:System.Runtime.Serialization.IExtensibleDataObject>
- <xref:System.Runtime.Serialization.ExtensionDataObject>
- <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A>
- <xref:System.Xml.Serialization.XmlSerializer>
- [데이터 계약 동등성](../../../docs/framework/wcf/feature-details/data-contract-equivalence.md)
- [버전 독립적 Serialization 콜백](../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md)
