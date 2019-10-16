---
title: 서비스 계약 디자인
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- service contracts [WCF]
ms.assetid: 8e89cbb9-ac84-4f0d-85ef-0eb6be0022fd
ms.openlocfilehash: a764b18cc3016610b8a149631b4de89923a7a5b4
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70040626"
---
# <a name="designing-service-contracts"></a>서비스 계약 디자인
이 항목에서는 서비스 계약의 정의, 서비스 계약을 정의하는 방법, 사용 가능한 작업(및 기본 메시지 교환에 미치는 영향), 사용되는 데이터 형식 및 시나리오 요구 사항을 만족하는 작업을 디자인하는 데 도움이 되는 기타 문제에 대해 설명합니다.  
  
## <a name="creating-a-service-contract"></a>서비스 계약 만들기  
 서비스는 여러 연산을 노출합니다. WCF (Windows Communication Foundation) 응용 프로그램에서 메서드를 만들고 <xref:System.ServiceModel.OperationContractAttribute> 특성으로 표시 하 여 작업을 정의 합니다. 그런 다음 서비스 계약을 만들려면 <xref:System.ServiceModel.ServiceContractAttribute> 특성으로 표시한 인터페이스 내에 작업을 선언하거나 같은 특성으로 표시된 클래스에 작업을 정의하여 작업을 함께 그룹화합니다. (기본 예제를 보려면 [방법: 서비스 계약](../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md)을 정의 합니다.)  
  
 <xref:System.ServiceModel.OperationContractAttribute> 특성이 없는 메서드는 서비스 작업이 아니고 WCF 서비스에 의해 노출 되지 않습니다.  
  
 이 항목에서는 다음과 같이 서비스 계약을 디자인할 때의 결정 사항에 대해 설명합니다.  
  
- 클래스 또는 인터페이스 사용 여부  
  
- 교환할 데이터 형식 지정 방법  
  
- 사용할 수 있는 교환 패턴 형식  
  
- 계약의 명시적 보안 요구 사항 부분을 만들 수 있는지 여부  
  
- 작업 입력 및 출력에 대한 제한  
  
## <a name="classes-or-interfaces"></a>클래스 또는 인터페이스  
 클래스와 인터페이스는 모두 기능 그룹화를 나타내므로 WCF 서비스 계약을 정의 하는 데 사용할 수 있습니다. 그러나 인터페이스는 서비스 계약을 직접 모델링하므로 인터페이스를 사용하는 것이 좋습니다. 구현을 사용하지 않으면 인터페이스는 특정 서명이 있는 메서드 그룹화만 정의합니다. 서비스 계약 인터페이스를 구현 하 고 WCF 서비스를 구현 했습니다.  
  
 관리되는 인터페이스의 모든 장점이 서비스 계약 인터페이스에 적용됩니다.  
  
- 서비스 계약 인터페이스는 다른 여러 서비스 계약 인터페이스를 확장할 수 있습니다.  
  
- 단일 클래스는 그러한 서비스 계약 인터페이스를 구현하여 원하는 만큼 서비스 계약을 구현할 수 있습니다.  
  
- 인터페이스 구현을 변경하여 서비스 계약의 구현을 수정할 수 있지만 서비스 계약은 그대로 유지됩니다.  
  
- 기존 인터페이스와 새 인터페이스를 구현하여 서비스에 버전을 지정할 수 있습니다. 기존 클라이언트는 원래 버전에 연결하며, 새 클라이언트는 새 버전에 연결합니다.  
  
> [!NOTE]
> 다른 서비스 계약 인터페이스에서 상속할 때 이름 또는 네임스페이스와 같은 작업 속성은 재정의할 수 없습니다. 재정의하려면 현재 서비스 계약에 새 작업을 만듭니다.  
  
 인터페이스를 사용 하 여 서비스 계약 [을 만드는 방법에 대 한 예제는 방법: 계약 인터페이스](../../../docs/framework/wcf/feature-details/how-to-create-a-service-with-a-contract-interface.md)를 사용 하 여 서비스를 만듭니다.  
  
 하지만 클래스를 사용하여 서비스 계약을 정의하고 그 계약을 구현할 수도 있습니다. <xref:System.ServiceModel.ServiceContractAttribute> 및 <xref:System.ServiceModel.OperationContractAttribute>를 클래스와 클래스의 메서드에 각각 직접 적용하여 서비스를 만들면 빠르고 간편하다는 장점이 있습니다. 단점은 관리되는 클래스가 여러 상속을 지원하지 않으므로 따라서 한 번에 하나의 서비스 계약만 구현할 수 있다는 것입니다. 또한 클래스 또는 메서드 서명을 수정하면 해당 서비스에 대한 공용 계약이 수정되므로 수정되지 않은 클라이언트는 서비스를 사용할 수 없습니다. 자세한 내용은 [서비스 계약 구현](../../../docs/framework/wcf/implementing-service-contracts.md)을 참조 하세요.  
  
 클래스를 사용 하 여 서비스 계약을 만들고 동시에 구현 하는 예제를 보려면 [방법: 계약 클래스](../../../docs/framework/wcf/feature-details/how-to-create-a-wcf-contract-with-a-class.md)를 사용 하 여 서비스를 만듭니다.  
  
 이때 인터페이스를 사용하여 서비스 계약을 정의하는 경우와 클래스를 사용하여 서비스 계약을 정의하는 경우의 차이를 알아야 합니다. 다음 단계에서는 서비스와 클라이언트 간에 주고받을 수 있는 데이터를 결정합니다.  
  
## <a name="parameters-and-return-values"></a>매개 변수 및 반환 값  
 각 작업마다 반환 값과 매개 변수가 있으며, 값이 `void`인 경우에도 값은 존재합니다. 그러나 개체 간에 개체에 대한 참조를 전달할 수 있는 로컬 메서드와 달리 서비스 작업은 개체에 대한 참조를 전달하지 않습니다. 대신 개체 복사본을 전달합니다.  
  
 매개 변수 또는 반환 값에 사용되는 각 형식이 serialize될 수 있어야 하므로 이것은 중요한 사항입니다. 즉, 해당 형식의 개체를 바이트 스트림으로 변환하고 바이트 스트림에서 개체로 변환할 수 있어야 합니다.  
  
 .NET Framework에 여러 가지 형식이 있으므로 기본적으로 기본 형식을 serialize할 수 있습니다.  
  
> [!NOTE]
> 작업 서명의 매개 변수 이름 값은 계약의 일부이며 대/소문자를 구분합니다. 같은 매개 변수 이름을 로컬로 사용하지만 게시된 메타데이터에서 이름을 수정하려면 <xref:System.ServiceModel.MessageParameterAttribute?displayProperty=nameWithType>를 참조하십시오.  
  
#### <a name="data-contracts"></a>데이터 계약  
 WCF (Windows Communication Foundation) 응용 프로그램과 같은 서비스 지향 응용 프로그램은 Microsoft 및 Microsoft 이외의 플랫폼에서 가장 광범위 하 게 사용할 수 있는 클라이언트 응용 프로그램과 상호 운용 되도록 디자인 되었습니다. 광범위한 상호 운용을 위해 <xref:System.Runtime.Serialization.DataContractAttribute> 및 <xref:System.Runtime.Serialization.DataMemberAttribute> 특성으로 형식을 표시하여 서비스 작업이 교환하는 데이터를 설명하는 서비스 계약의 부분인 데이터 계약을 만드는 것이 좋습니다.  
  
 데이터 계약은 옵트인 스타일 계약입니다. 데이터 계약 특성을 명시적으로 적용 하지 않으면 형식이 나 데이터 멤버가 serialize 되지 않습니다. 데이터 계약은 관리 코드의 액세스 범위와 관련이 없습니다. 전용 데이터 멤버를 serialize 하 고 다른 곳에서 전송 하 여 공개적으로 액세스할 수 있습니다. (데이터 계약의 기본 예제를 보려면 [방법: 클래스 또는 구조체](../../../docs/framework/wcf/feature-details/how-to-create-a-basic-data-contract-for-a-class-or-structure.md)에 대 한 기본 데이터 계약을 만듭니다. WCF는 작업의 기능을 사용할 수 있도록 하는 기본 SOAP 메시지의 정의와 메시지 본문의 데이터 형식에 대 한 serialization을 처리 합니다. 데이터 형식을 serialize할 수 있다면 작업을 디자인할 때 기본 메시지 교환 인프라에 대해 고려하지 않아도 됩니다.  
  
 일반적인 WCF 응용 프로그램에서는 <xref:System.Runtime.Serialization.DataContractAttribute> 및 <xref:System.Runtime.Serialization.DataMemberAttribute> 특성을 사용 하 여 작업에 대 한 데이터 계약을 만들기는 하지만 다른 serialization 메커니즘을 사용할 수 있습니다. 표준 <xref:System.Runtime.Serialization.ISerializable>, <xref:System.SerializableAttribute> 및 <xref:System.Xml.Serialization.IXmlSerializable> 메커니즘은 모두 응용 프로그램 간에 데이터 형식을 전달하는 기본 SOAP 메시지에 데이터 형식의 serialization을 처리하는 작업을 수행합니다. 데이터 형식에 특별 지원이 필요할 경우 더 많은 serialization 전략을 채택할 수 있습니다. WCF 응용 프로그램에서 데이터 형식의 serialization을 위한 선택 사항에 대 한 자세한 내용은 [서비스 계약의 데이터 전송 지정](../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)을 참조 하세요.  
  
#### <a name="mapping-parameters-and-return-values-to-message-exchanges"></a>메시지 교환에 매개 변수 및 반환 값 매핑  
 서비스 작업은 응용 프로그램 데이터뿐만 아니라 응용 프로그램이 특정 표준 보안, 트랜잭션 및 세션 관련 기능을 지원하는 데 필요한 데이터를 주고받는 SOAP 메시지의 기본 교환에 의해 지원됩니다. 이 경우 서비스 작업의 서명은 데이터 전송 및 작업에 필요한 기능을 지원할 수 있는 특정 기본 mep ( *메시지 교환 패턴* )를 결정 합니다. WCF 프로그래밍 모델에서 요청/회신, 단방향 및 이중 메시지 패턴의 세 가지 패턴을 지정할 수 있습니다.  
  
##### <a name="requestreply"></a>요청/회신  
 요청/회신 패턴은 요청 발신자(클라이언트 응용 프로그램)가 요청과 상호 관련된 회신을 받는 패턴입니다. 이 패턴은 하나 이상의 매개 변수가 작업에 전달되고 반환값이 다시 호출자에게 전달되는 작업을 지원하므로 기본 MEP입니다. 예를 들어, 다음 C# 코드 예제에서는 문자열 하나를 사용하여 문자열을 반환하는 기본적인 서비스 작업을 보여 줍니다.  
  
```csharp  
[OperationContractAttribute]  
string Hello(string greeting);  
```  
  
 @FSHO1@다음은 해당하는 Visual Basic 코드입니다.  
  
```vb  
<OperationContractAttribute()>  
Function Hello (ByVal greeting As String) As String  
```  
  
 이 작업 서명은 기본 메시지 교환 형식을 지정합니다. 상관 관계가 없는 경우 WCF는 반환 값이 의도 한 작업을 확인할 수 없습니다.  
  
 다른 기본 메시지 패턴을 지정 하지 않을 경우 ( `void` `Nothing` Visual Basic)을 반환 하는 서비스 작업은 요청/회신 메시지 교환입니다. 작업 결과, 클라이언트가 작업을 비동기적으로 호출하지 않으면 일반적인 경우 메시지가 비어 있어도 클라이언트가 반환 메시지를 받을 때까지 처리를 중지합니다. 다음 C# 코드 예제에서는 클라이언트가 빈 메시지를 응답으로 받을 때까지 반환되지 않는 작업을 보여 줍니다.  
  
```csharp  
[OperationContractAttribute]  
void Hello(string greeting);  
```  
  
 @FSHO1@다음은 해당하는 Visual Basic 코드입니다.  
  
```vb  
<OperationContractAttribute()>  
Sub Hello (ByVal greeting As String)  
```  
  
 앞의 예제에서는 작업을 수행하는 데 시간이 오래 걸릴 경우 클라이언트 성능 및 응답성이 저하될 수 있지만 `void`를 반환하는 경우에도 요청/회신 작업에 이점이 있습니다. 명백한 점은 통신에서든 처리 중에든 일부 서비스 관련 오류 조건이 발생했음을 나타내는 응답 메시지에 SOAP 오류가 반환될 수 있다는 것입니다. 서비스 계약에 지정된 SOAP 오류는 클라이언트 응용 프로그램에 <xref:System.ServiceModel.FaultException%601> 개체로 전달됩니다. 여기서 형식 매개 변수는 서비스 계약에 지정된 형식입니다. 이렇게 하면 클라이언트에 WCF 서비스의 오류 조건에 대 한 정보를 쉽게 알릴 수 있습니다. 예외, SOAP 오류 및 오류 처리에 대 한 자세한 내용은 [계약 및 서비스에서 오류 지정 및 처리](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)를 참조 하세요. 요청/회신 서비스 및 클라이언트 [의 예를 보려면 방법: 요청-회신 계약](../../../docs/framework/wcf/feature-details/how-to-create-a-request-reply-contract.md)을 만듭니다. 요청-회신 패턴의 문제에 대 한 자세한 내용은 [요청-회신 서비스](../../../docs/framework/wcf/feature-details/request-reply-services.md)를 참조 하세요.  
  
##### <a name="one-way"></a>단방향  
 WCF 서비스 응용 프로그램의 클라이언트가 작업이 완료 될 때까지 기다리지 않고 SOAP 오류를 처리 하지 않으면 작업에서 단방향 메시지 패턴을 지정할 수 있습니다. 단방향 작업은 클라이언트에서 작업을 호출 하 고 WCF가 네트워크에 메시지를 쓴 후 처리를 계속 하는 것입니다. 일반적으로 아웃바운드 메시지에 보내는 데이터가 아주 크지 않은 경우 데이터를 보내는 데 문제가 없다면 클라이언트가 바로 계속해서 실행됩니다. 이러한 형식의 메시지 교환 패턴은 클라이언트에서 서비스 응용 프로그램으로 이벤트와 비슷한 동작을 지원합니다.  
  
 메시지를 보내지만 반환되는 메시지가 없는 메시지 교환은 `void` 이외의 반환 값을 지정하는 서비스 작업을 지원할 수 없습니다. 이 경우 <xref:System.InvalidOperationException> 예외가 throw됩니다.  
  
 반환 메시지가 없다는 것은 처리 또는 통신 오류를 나타내는 SOAP 오류가 반환되지 않았음을 의미합니다. 단방향 작업인 경우 통신 오류 정보에 이중 메시지 교환 패턴이 필요합니다.  
  
 `void`를 반환하는 작업에 단방향 메시지 교환을 지정하려면 다음 C# 코드 예제처럼 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 속성을 `true`로 설정합니다.  
  
```csharp  
[OperationContractAttribute(IsOneWay=true)]  
void Hello(string greeting);  
```  
  
 @FSHO1@다음은 해당하는 Visual Basic 코드입니다.  
  
```vb  
<OperationContractAttribute(IsOneWay := True)>  
Sub Hello (ByVal greeting As String)  
```  
  
 이 메서드는 앞의 요청/회신 예제와 동일하지만 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 속성을 `true`로 설정한다는 것은 메서드는 같지만 서비스 작업에서 반환 메시지를 보내지 않으며 아웃바운드 메시지가 채널 계층에 전달되면 바로 클라이언트가 반환된다는 것을 의미합니다. 예는 [방법: 단방향 계약](../../../docs/framework/wcf/feature-details/how-to-create-a-one-way-contract.md)을 만듭니다. 단방향 패턴에 대 한 자세한 내용은 단방향 [서비스](../../../docs/framework/wcf/feature-details/one-way-services.md)를 참조 하세요.  
  
##### <a name="duplex"></a>이중  
 이중 패턴의 특징은 단방향 메시징을 사용하든 요청/회신 메시징을 사용하든 관계없이 서비스와 클라이언트 모두 서로 독립적으로 메시지를 보낼 수 있는 기능입니다. 이와 같은 형식의 양방향 통신은 클라이언트와 직접 통신해야 하는 서비스에 유용하며, 메시지를 교환하는 양측에 이벤트와 유사한 동작을 비롯하여 비동기 환경을 제공하는 데도 유용합니다.  
  
 이중 패턴은 클라이언트와 통신하기 위한 추가 메커니즘 때문에 요청/회신 또는 단방향 패턴보다 조금 복잡합니다.  
  
 이중 계약을 디자인하려면 콜백 계약도 디자인하고 서비스 계약을 표시하는 <xref:System.ServiceModel.ServiceContractAttribute.CallbackContract%2A> 특성의 <xref:System.ServiceModel.ServiceContractAttribute> 속성에 해당 콜백 계약의 형식을 지정해야 합니다.  
  
 이중 패턴을 구현하려면 클라이언트에서 호출되는 메서드 선언을 포함하는 다른 인터페이스를 만들어야 합니다.  
  
 서비스 및 해당 서비스 [에 액세스 하는 클라이언트를 만드는 방법에 대 한 예제는 방법: 이중 계약](../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md) [을 만들고 방법: 이중 계약](../../../docs/framework/wcf/feature-details/how-to-access-services-with-a-duplex-contract.md)을 사용 하 여 서비스에 액세스 합니다. 작업 샘플은 [이중](../../../docs/framework/wcf/samples/duplex.md)을 참조 하세요. 이중 계약을 사용 하는 문제에 대 한 자세한 내용은 [이중 서비스](../../../docs/framework/wcf/feature-details/duplex-services.md)를 참조 하세요.  
  
> [!CAUTION]
> 서비스가 이중 메시지를 받으면 들어오는 해당 메시지에서 `ReplyTo` 요소를 확인하여 회신을 보낼 위치를 결정합니다. 메시지를 받는 데 사용되는 채널이 보안되지 않으면 신뢰할 수 없는 클라이언트가 대상 컴퓨터의 `ReplyTo`를 사용하여 악의적인 메시지를 보낼 수 있으므로 해당 대상 컴퓨터의 서비스 거부(DOS)가 발생할 수 있습니다.  
  
##### <a name="out-and-ref-parameters"></a>Out 및 Ref 매개 변수  
 대부분의 경우 매개 `in` 변수 (`ByVal` Visual Basic) 및 `out` 및 `ref` 매개 변수 (`ByRef` Visual Basic)를 사용할 수 있습니다. `out` 및 `ref` 매개 변수 모두 데이터가 작업에서 반환됨을 나타내기 때문에 다음과 같은 작업 서명은 작업 서명이 `void`를 반환해도 요청/회신 작업이 필요하도록 지정합니다.  
  
```csharp  
[ServiceContractAttribute]  
public interface IMyContract  
{  
  [OperationContractAttribute]  
  public void PopulateData(ref CustomDataType data);  
}  
```  
  
 @FSHO1@다음은 해당하는 Visual Basic 코드입니다.  
  
```vb  
<ServiceContractAttribute()> _  
Public Interface IMyContract  
  <OperationContractAttribute()> _  
  Public Sub PopulateData(ByRef data As CustomDataType)  
End Interface  
```  
  
 서명에 특정한 구조가 있는 경우는 예외입니다. 예를 들어, 작업을 선언하는 데 사용된 메서드가 <xref:System.ServiceModel.NetMsmqBinding>를 반환하는 경우에만 `void` 바인딩을 사용하여 클라이언트와 통신할 수 있습니다. 반환 값이든 `ref` 또는 `out` 매개 변수든 출력 값이 없을 수 있습니다.  
  
 또한 `out` 또는 `ref` 매개 변수를 사용하려면 작업에 수정된 개체를 다시 전달할 기본 응답 메시지가 있어야 합니다. 단방향 작업인 경우 런타임에 <xref:System.InvalidOperationException> 예외가 throw됩니다.  
  
### <a name="specify-message-protection-level-on-the-contract"></a>계약에 메시지 보호 수준 지정  
 계약을 디자인할 때 계약을 구현하는 서비스의 메시지 보호 수준도 결정해야 합니다. 이 작업은 메시지 보안이 계약의 엔드포인트에 있는 바인딩에 적용되는 경우에만 필요합니다. 바인딩에 보안이 해제된 경우(시스템 제공 바인딩이 <xref:System.ServiceModel.SecurityMode?displayProperty=nameWithType>를 <xref:System.ServiceModel.SecurityMode.None?displayProperty=nameWithType> 값으로 설정한 경우) 계약에 대한 메시지 보호 수준을 결정하지 않아도 됩니다. 대부분의 경우 적용된 메시지 수준 보안과 함께 시스템 제공 바인딩은 충분한 보호 수준을 제공하므로 작업별 또는 메시지별로 보호 수준을 고려하지 않아도 됩니다.  
  
 보호 수준은 서비스를 지원하는 메시지(또는 메시지 부분)가 서명되어 있는지, 서명 및 암호화되어 있는지 또는 서명이나 암호화 없이 보내졌는지를 지정하는 값입니다. 보호 수준은 다음과 같은 다양 한 범위에서 설정할 수 있습니다. 서비스 수준에서 특정 작업의 경우 해당 작업 내의 메시지 또는 메시지 부분입니다. 한 범위에 설정된 값은 명시적으로 재정의되지 않는 한 더 작은 범위의 기본값이 됩니다. 바인딩 구성에서 계약에 필요한 최소 보호 수준을 제공할 수 없으면 예외가 throw됩니다. 또한 보호 수준 값이 계약에 명시적으로 설정되어 있지 않을 때 바인딩에 메시지 보안이 있는 경우에는 바인딩 구성이 모든 메시지에 대한 보호 수준을 제어합니다. 이는 기본 동작입니다.  
  
> [!IMPORTANT]
> 계약의 여러 범위를 명시적으로 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign?displayProperty=nameWithType>의 전체 보호 수준보다 낮게 설정할 것인지를 결정하는 것은 일반적으로 향상된 성능의 보안 정도를 절충하는 결정입니다. 이러한 경우 사용자는 작업과 관련된 사항을 확인하고 작업에서 교환하는 데이터 값을 확인해야 합니다. 자세한 내용은 [Securing Services](../../../docs/framework/wcf/securing-services.md)합니다.  
  
 예를 들어, 다음 코드 예제는 <xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> 또는 <xref:System.ServiceModel.OperationContractAttribute.ProtectionLevel%2A> 속성을 계약에 설정하지 않습니다.  
  
```csharp  
[ServiceContract]  
public interface ISampleService  
{  
  [OperationContractAttribute]  
  public string GetString();  
  
  [OperationContractAttribute]  
  public int GetInt();    
}  
```  
  
 @FSHO1@다음은 해당하는 Visual Basic 코드입니다.  
  
```vb  
<ServiceContractAttribute()> _  
Public Interface ISampleService  
  
  <OperationContractAttribute()> _  
  Public Function GetString()As String  
  
  <OperationContractAttribute()> _  
  Public Function GetData() As Integer  
  
End Interface  
```  
  
 기본 `ISampleService`(<xref:System.ServiceModel.WSHttpBinding>인 기본 <xref:System.ServiceModel.SecurityMode?displayProperty=nameWithType>)을 사용하여 엔드포인트의 <xref:System.ServiceModel.SecurityMode.Message> 구현과 상호 작용할 때 이것이 기본 보호 수준이므로 모든 메시지가 암호화되고 서명됩니다. 그러나 `ISampleService` 서비스가 기본 <xref:System.ServiceModel.BasicHttpBinding>(<xref:System.ServiceModel.SecurityMode>인 기본 <xref:System.ServiceModel.SecurityMode.None>)과 함께 사용되면 이 바인딩에 대한 보안이 없으므로 보호 수준이 무시되기 때문에(메시지가 암호화되거나 서명되지 않으므로) 모든 메시지가 텍스트로 전송됩니다. <xref:System.ServiceModel.SecurityMode>가 <xref:System.ServiceModel.SecurityMode.Message>로 변경된 경우에는 바인딩의 기본 보호 수준이 되므로 이러한 메시지가 암호화되고 서명됩니다.  
  
 계약에 대한 보호 요구 사항을 명시적으로 지정하거나 조정하려면 <xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> 속성(또는 더 작은 범위의 `ProtectionLevel` 속성 중 하나)을 서비스 계약에서 필요로 하는 수준으로 설정합니다. 이 경우 명시적 설정을 사용하려면 사용된 범위에 대해 최소한 해당 설정을 지원할 바인딩이 필요합니다. 예를 들어, 다음 코드 예제에서는 <xref:System.ServiceModel.OperationContractAttribute.ProtectionLevel%2A> 작업에 대해 하나의 `GetGuid` 값을 명시적으로 지정합니다.  
  
```csharp  
[ServiceContract]  
public interface IExplicitProtectionLevelSampleService  
{  
  [OperationContractAttribute]  
  public string GetString();  
  
  [OperationContractAttribute(ProtectionLevel=ProtectionLevel.None)]  
  public int GetInt();    
  [OperationContractAttribute(ProtectionLevel=ProtectionLevel.EncryptAndSign)]  
  public int GetGuid();    
}  
```  
  
 @FSHO1@다음은 해당하는 Visual Basic 코드입니다.  
  
```vb  
<ServiceContract()> _   
Public Interface IExplicitProtectionLevelSampleService   
    <OperationContract()> _   
    Public Function GetString() As String   
    End Function   
  
    <OperationContract(ProtectionLevel := ProtectionLevel.None)> _   
    Public Function GetInt() As Integer   
    End Function   
  
    <OperationContractAttribute(ProtectionLevel := ProtectionLevel.EncryptAndSign)> _   
    Public Function GetGuid() As Integer   
    End Function   
  
End Interface  
```  
  
 이 `IExplicitProtectionLevelSampleService` 계약을 구현하고 기본 <xref:System.ServiceModel.WSHttpBinding>(<xref:System.ServiceModel.SecurityMode?displayProperty=nameWithType>인 기본 <xref:System.ServiceModel.SecurityMode.Message>)을 사용하는 엔드포인트가 있는 서비스는 다음과 같이 동작합니다.  
  
- `GetString` 작업 메시지가 암호화되고 서명됩니다.  
  
- `GetInt` 작업 메시지는 암호화되지 않고 서명되지 않은(일반 텍스트) 텍스트로 전송됩니다.  
  
- `GetGuid` 작업 <xref:System.Guid?displayProperty=nameWithType>는 암호화되고 서명된 메시지에 반환됩니다.  
  
 보호 수준 및 사용 방법에 대 한 자세한 내용은 [보호 수준 이해](../../../docs/framework/wcf/understanding-protection-level.md)를 참조 하세요. 보안에 대 한 자세한 내용은 [서비스](../../../docs/framework/wcf/securing-services.md)보안 설정을 참조 하세요.  
  
##### <a name="other-operation-signature-requirements"></a>기타 작업 서명 요구 사항  
 일부 응용 프로그램 기능에는 특정한 종류의 작업 서명이 필요합니다. 예를 들어, <xref:System.ServiceModel.NetMsmqBinding> 바인딩은 응용 프로그램이 통신 중에 다시 시작할 수 있으며 메시지를 누락하지 않고 중지된 지점을 선택할 수 있는 영속 서비스 및 클라이언트를 지원합니다. 자세한 내용은 [WCF의 큐](../../../docs/framework/wcf/feature-details/queues-in-wcf.md)를 참조 하십시오. 그러나 영속 작업에서는 하나의 `in` 매개 변수만 사용하고 반환 값이 없어야 합니다.  
  
 또 다른 예제는 작업에 <xref:System.IO.Stream> 형식을 사용하는 것입니다. <xref:System.IO.Stream> 매개 변수에 전체 메시지 본문이 포함되므로 입력 또는 출력(`ref` 매개 변수, `out` 매개 변수 또는 반환 값)이 <xref:System.IO.Stream> 형식이면 작업에 지정된 입력 또는 출력이어야 합니다. 또한 매개 변수나 반환 형식이 <xref:System.IO.Stream>, <xref:System.ServiceModel.Channels.Message?displayProperty=nameWithType> 또는 <xref:System.Xml.Serialization.IXmlSerializable?displayProperty=nameWithType>이어야 합니다. 스트림에 대 한 자세한 내용은 [대량 데이터 및 스트리밍](../../../docs/framework/wcf/feature-details/large-data-and-streaming.md)을 참조 하세요.  
  
##### <a name="names-namespaces-and-obfuscation"></a>이름, 네임스페이스 및 난독 처리  
 계약을 WSDL로 변환하고 계약 메시지를 만들어 보낼 때는 계약 및 작업에 대한 정의에서 .NET 형식의 이름 및 네임스페이스가 중요합니다. 따라서 `Name`, `Namespace`, <xref:System.ServiceModel.ServiceContractAttribute>,  <xref:System.ServiceModel.OperationContractAttribute> 및 다른 계약 특성과 같은 지원되는 모든 계약 특성의 <xref:System.Runtime.Serialization.DataContractAttribute> 및 <xref:System.Runtime.Serialization.DataMemberAttribute> 속성을 사용하여 서비스 계약 이름 및 네임스페이스를 명시적으로 설정하는 것이 좋습니다.  
  
 이름과 네임스페이스를 명시적으로 설정하지 않는 경우 어셈블리에서 IL 난독 처리를 사용하면 계약 형식 이름과 네임스페이스가 변경되고 WSDL 및 통신 교환이 수정되어 일반적으로 실패하게 됩니다. 계약 이름과 네임스페이스를 명시적으로 설정하지 않고 난독 처리를 사용하려면 <xref:System.Reflection.ObfuscationAttribute> 및 <xref:System.Reflection.ObfuscateAssemblyAttribute> 특성을 사용하여 계약 형식 이름 및 네임스페이스가 수정되지 않게 합니다.  
  
## <a name="see-also"></a>참고자료

- [방법: 요청-회신 계약 만들기](../../../docs/framework/wcf/feature-details/how-to-create-a-request-reply-contract.md)
- [방법: 단방향 계약 만들기](../../../docs/framework/wcf/feature-details/how-to-create-a-one-way-contract.md)
- [방법: 이중 계약 만들기](../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)
- [서비스 계약에서 데이터 전송 지정](../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)
- [계약 및 서비스에서 오류 지정 및 처리](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)
- [세션 사용](../../../docs/framework/wcf/using-sessions.md)
- [동기 및 비동기 작업](../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md)
- [신뢰할 수 있는 서비스](../../../docs/framework/wcf/reliable-services.md)
- [서비스 및 트랜잭션](../../../docs/framework/wcf/services-and-transactions.md)
