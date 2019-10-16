---
title: 메시지 계약 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- message contracts [WCF]
ms.assetid: 1e19c64a-ae84-4c2f-9155-91c54a77c249
ms.openlocfilehash: 18d0ea97f1de40044d40fa85c9792c809fb73346
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69959877"
---
# <a name="using-message-contracts"></a>메시지 계약 사용
일반적으로 WCF (Windows Communication Foundation) 응용 프로그램을 빌드할 때 개발자는 데이터 구조 및 serialization 문제에 특히 주의를 기울여야 하며 데이터가 전달 되는 메시지의 구조를 고려 하지 않아도 됩니다. 이러한 애플리케이션의 경우 매개 변수 또는 반환 값에 대한 데이터 계약을 만드는 과정은 간단합니다. 자세한 내용은 [서비스 계약에서 데이터 전송 지정](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)을 참조 하세요.  
  
 그러나 SOAP 메시지의 구조를 완벽하게 제어하는 것이 SOAP 메시지의 내용을 제어하는 것만큼이나 중요한 경우도 있습니다. 특히 상호 운용성이 중요한 경우 또는 메시지나 메시지 부분의 수준에서 보안 문제를 특별히 제어해야 하는 경우에는 더욱 그렇습니다. 이러한 경우 필요한 정확한 SOAP 메시지의 구조를 지정할 수 있도록 하는 *메시지 계약* 을 만들 수 있습니다.  
  
 이 항목에서는 다양한 메시지 계약 특성을 사용하여 작업에 대한 특정 메시지 계약을 만드는 방법에 대해 설명합니다.  
  
## <a name="using-message-contracts-in-operations"></a>작업에서 메시지 계약 사용  
 WCF는 *RPC (원격 프로시저 호출) 스타일* 또는 *메시징 스타일*에서 모델링 된 작업을 지원 합니다. RPC 스타일 작업에서는 serialize할 수 있는 형식을 모두 사용할 수 있으며, 여러 매개 변수, `ref` 및 `out` 매개 변수와 같은 로컬 호출에 사용 가능한 기능을 사용할 수 있습니다. 이 스타일에서는 선택한 serialization 형식이 기본 메시지의 데이터 구조를 제어 하 고 WCF 런타임에서는 작업을 지원 하기 위한 메시지를 만듭니다. 이를 통해 SOAP 및 SOAP 메시지에 익숙하지 않은 개발자도 서비스 애플리케이션을 빠르고 쉽게 만들고 사용할 수 있습니다.  
  
 다음 코드 예제에서는 RPC 스타일로 모델링된 서비스 작업을 보여 줍니다.  
  
```csharp  
[OperationContract]  
public BankingTransactionResponse PostBankingTransaction(BankingTransaction bt);  
```  
  
 일반적으로 데이터 계약만으로도 메시지에 대한 스키마를 정의할 수 있습니다. 예를 들어 앞의 예제에서 `BankingTransaction` 및 `BankingTransactionResponse`가 기본 SOAP 메시지의 내용을 정의하기 위한 데이터 계약을 가지고 있는 경우, 대부분의 애플리케이션에서 스키마를 정의할 수 있습니다. 데이터 계약에 대 한 자세한 내용은 참조 하세요. [Using Data Contracts](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)합니다.  
  
 그러나 연결을 통해 SOAP 메시지 구조가 전송되는 방식을 정확하게 제어해야 하는 경우도 있습니다. 이를 위한 가장 일반적인 시나리오는 사용자 지정 SOAP 헤더를 삽입하는 것입니다. 또 다른 일반적인 시나리오는 메시지의 헤더 및 본문에 대한 보안 속성을 정의하는 것, 즉 이러한 요소를 디지털 서명 및 암호화할지 여부를 결정하는 것입니다. 마지막으로, 일부 타사 SOAP 스택에서는 메시지가 특정 형식이어야 합니다. 메시징 스타일 작업에서는 이 컨트롤을 제공합니다.  
  
 메시징 스타일 작업은 메시지 형식이 두 가지인 경우에 최대 하나의 매개 변수 및 하나의 반환 값만 가질 수 있습니다. 즉, 지정된 SOAP 메시지 구조로 직접 serialize됩니다. 이는 <xref:System.ServiceModel.MessageContractAttribute>로 표시된 형식 또는 <xref:System.ServiceModel.Channels.Message> 형식일 수 있습니다. 다음 코드 예제에서는 이전 RCP 스타일과 유사하지만 메시징 스타일을 사용하는 작업을 보여 줍니다.  
  
 예를 들어 `BankingTransaction` 및 `BankingTransactionResponse`가 모두 메시지 계약을 가진 형식일 경우 다음 작업의 코드는 유효합니다.  
  
```csharp  
[OperationContract]  
BankingTransactionResponse Process(BankingTransaction bt);  
[OperationContract]  
void Store(BankingTransaction bt);  
[OperationContract]  
BankingTransactionResponse GetResponse();  
```  
  
 그러나 다음 코드는 유효하지 않습니다.  
  
```csharp  
[OperationContract]  
bool Validate(BankingTransaction bt);  
// Invalid, the return type is not a message contract.  
[OperationContract]  
void Reconcile(BankingTransaction bt1, BankingTransaction bt2);  
// Invalid, there is more than one parameter.  
```  
  
 메시지 계약 형식이 포함되어 있지만 유효한 패턴 중 하나를 따르지 않는 모든 작업에 대해서는 예외가 throw됩니다. 물론 메시지 계약 형식이 포함되지 않은 작업에는 이러한 제한이 적용되지 않습니다.  
  
 한 형식이 메시지 계약과 데이터 계약을 둘 다 가진 경우에는 메시지 계약만 작업에서 해당 형식을 사용할 때 고려됩니다.  
  
## <a name="defining-message-contracts"></a>메시지 계약 정의  
 형식에 대한 메시지 계약을 정의하려면, 즉 형식과 SOAP 봉투 간의 매핑을 정의하려면 해당 형식에 <xref:System.ServiceModel.MessageContractAttribute>를 적용합니다. 그런 다음 <xref:System.ServiceModel.MessageHeaderAttribute>를 SOAP 헤더로 만들려는 형식의 멤버에 적용하고, <xref:System.ServiceModel.MessageBodyMemberAttribute>를 메시지의 SOAP 본문 부분으로 만들려는 멤버에 적용합니다.  
  
 다음 코드에서는 메시지 계약을 사용하는 예를 보여 줍니다.  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public Operation operation;  
  [MessageHeader] public DateTime transactionDate;  
  [MessageBodyMember] private Account sourceAccount;  
  [MessageBodyMember] private Account targetAccount;  
  [MessageBodyMember] public int amount;  
}  
```  
  
 이 형식을 작업 매개 변수로 사용할 경우 다음 SOAP 봉투가 발생됩니다.  
  
```xml  
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
  <s:Header>  
    <h:operation xmlns:h="http://tempuri.org/" xmlns="http://tempuri.org/">Deposit</h:operation>  
    <h:transactionDate xmlns:h="http://tempuri.org/" xmlns="http://tempuri.org/">2012-02-16T16:10:00</h:transactionDate>  
  </s:Header>  
  <s:Body xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <BankingTransaction xmlns="http://tempuri.org/">  
      <amount>0</amount>  
      <sourceAccount xsi:nil="true"/>  
      <targetAccount xsi:nil="true"/>  
    </BankingTransaction>  
  </s:Body>  
</s:Envelope>  
```  
  
 `operation` 및 `transactionDate`는 SOAP 헤더로 나타나고 SOAP 본문은 `BankingTransaction`, `sourceAccount` 및 `targetAccount`가 포함된 래퍼 요소 `amount`으로 구성됩니다.  
  
 <xref:System.ServiceModel.MessageHeaderAttribute> 및 <xref:System.ServiceModel.MessageBodyMemberAttribute>는 public, private, protected, internal 중 무엇인지 관계없이 모든 필드, 속성 및 이벤트에 적용할 수 있습니다.  
  
 <xref:System.ServiceModel.MessageContractAttribute>를 사용하면 SOAP 메시지 본문에서 래퍼 요소의 이름을 제어하는 WrapperName 및 WrapperNamespace 특성을 지정할 수 있습니다. 기본적으로 메시지 계약 형식의 이름이 래퍼로 사용되며 메시지 계약이 정의된 네임스페이스 `http://tempuri.org/`가 기본 네임스페이스로 사용됩니다.  
  
> [!NOTE]
> <xref:System.Runtime.Serialization.KnownTypeAttribute> 특성은 메시지 계약에서 무시됩니다. <xref:System.Runtime.Serialization.KnownTypeAttribute>가 필요할 경우 해당 메시지 계약을 사용 중인 작업에 포함시킵니다.  
  
## <a name="controlling-header-and-body-part-names-and-namespaces"></a>헤더와 본문 부분의 이름 및 네임스페이스 제어  
 메시지 계약의 SOAP 표현에서 각 헤더 및 본문 부분은 하나의 이름과 하나의 네임스페이스를 가진 XML 요소로 매핑됩니다.  
  
 기본적으로 네임스페이스는 메시지가 참여 중인 서비스 계약의 네임스페이스와 동일하며, 이름은 <xref:System.ServiceModel.MessageHeaderAttribute> 또는 <xref:System.ServiceModel.MessageBodyMemberAttribute> 특성이 적용되는 멤버 이름에 의해 결정됩니다.  
  
 <xref:System.ServiceModel.MessageContractMemberAttribute.Name%2A?displayProperty=nameWithType> 및 <xref:System.ServiceModel.MessageContractMemberAttribute.Namespace%2A?displayProperty=nameWithType> 특성의 부모 클래스에서 <xref:System.ServiceModel.MessageHeaderAttribute> 및 <xref:System.ServiceModel.MessageBodyMemberAttribute>를 조작함으로써 이러한 기본값을 변경할 수 있습니다.  
  
 다음과 같은 코드의 클래스를 예로 들어 볼 수 있습니다.  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public Operation operation;  
  [MessageHeader(Namespace="http://schemas.contoso.com/auditing/2005")] public bool IsAudited;  
  [MessageBodyMember(Name="transactionData")] public BankingTransactionData theData;  
}  
```  
  
 이 예제에서는 `IsAudited` 헤더가 코드에서 지정된 네임스페이스에 있으며, `theData` 멤버를 나타내는 본문 부분은 이름 `transactionData`와 함께 XML 요소로 표시됩니다. 다음 예제에서는 이 메시지 계약에 대해 생성된 XML을 보여 줍니다.  
  
```xml  
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
  <s:Header>  
    <h:IsAudited xmlns:h="http://schemas.contoso.com/auditing/2005" xmlns="http://schemas.contoso.com/auditing/2005">false</h:IsAudited>  
    <h:operation xmlns:h="http://tempuri.org/" xmlns="http://tempuri.org/">Deposit</h:operation>  
  </s:Header>  
  <s:Body xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <AuditedBankingTransaction xmlns="http://tempuri.org/">  
      <transactionData/>  
    </AuditedBankingTransaction>  
  </s:Body>  
</s:Envelope>  
```  
  
## <a name="controlling-whether-the-soap-body-parts-are-wrapped"></a>SOAP 본문 부분의 래핑 여부 제어  
 기본적으로 SOAP 본문 부분은 래핑된 요소 내부에서 serialize됩니다. 예를 들어 다음 코드에서는 `HelloGreetingMessage` 메시지에 대한 메시지 계약에서 <xref:System.ServiceModel.MessageContractAttribute> 형식의 이름으로부터 생성된 `HelloGreetingMessage` 래퍼 요소를 보여 줍니다.  
  
[!code-csharp[MessageHeaderAttribute#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/messageheaderattribute/cs/services.cs#3)]
[!code-vb[MessageHeaderAttribute#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/messageheaderattribute/vb/services.vb#3)]  
  
 래퍼 요소를 표시하지 않으려면 <xref:System.ServiceModel.MessageContractAttribute.IsWrapped%2A> 속성을 `false`로 설정합니다. 래퍼 요소의 이름 및 네임스페이스를 제어하려면 <xref:System.ServiceModel.MessageContractAttribute.WrapperName%2A> 및 <xref:System.ServiceModel.MessageContractAttribute.WrapperNamespace%2A> 속성을 사용합니다.  
  
> [!NOTE]
> 래핑되지 않은 메시지에 메시지 본문 부분이 두 개 이상이면 WS-I Basic Profile 1.1과 호환되지 않으므로, 새 메시지 계약을 디자인할 때는 이러한 경우를 피해야 합니다. 그러나 특정 상호 운용성 시나리오에서는 래핑되지 않은 메시지 본문 부분이 두 개 이상이어야 할 경우도 있습니다. 메시지 본문에서 두 개 이상의 데이터를 전송하려는 경우 기본(래핑된) 모드를 사용하는 것이 좋습니다. 래핑되지 않은 메시지에 메시지 헤더가 두 개 이상 있는 것도 전적으로 허용됩니다.  
  
## <a name="using-custom-types-inside-message-contracts"></a>메시지 계약에 사용자 지정 형식 사용  
 개별 메시지 헤더 및 메시지 본문 부분은 메시지를 사용하는 서비스 계약에 대해 선택한 serialization 엔진을 사용하여 serialize됩니다(XML로 변경됨). 기본 serialization 엔진인 `XmlFormatter`는 데이터 계약을 가지고 있는 모든 형식을 명시적으로(<xref:System.Runtime.Serialization.DataContractAttribute?displayProperty=nameWithType>를 가짐으로써) 또는 암시적으로(<xref:System.SerializableAttribute?displayProperty=nameWithType> 등을 사용하는 기본 형식이 됨으로써) 처리할 수 있습니다. 자세한 내용은 [데이터 계약 사용](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)을 참조 하세요.  
  
 앞의 예제에서는 `Operation`이 기본 형식이고 따라서 암시적 데이터 계약을 가지므로 `BankingTransactionData` 및 `transactionDate` 형식은 데이터 계약을 가져야 하며 <xref:System.DateTime>는 serialize할 수 있어야 합니다.  
  
 그러나 `XmlSerializer`라는 다른 serialization 엔진으로 전환할 수 있습니다. 이와 같은 전환을 수행할 경우에는 메시지 헤더 및 본문 부분에 사용하는 모든 형식이 `XmlSerializer`를 사용하여 serialize할 수 있어야 합니다.  
  
## <a name="using-arrays-inside-message-contracts"></a>메시지 계약에 배열 사용  
 메시지 계약에 반복되는 요소의 배열을 두 가지 방식으로 사용할 수 있습니다.  
  
 첫 번째 방법은 <xref:System.ServiceModel.MessageHeaderAttribute> 또는 <xref:System.ServiceModel.MessageBodyMemberAttribute>를 배열에서 직접 사용하는 것입니다. 이 경우에는 모든 배열이 여러 자식 요소와 함께 하나의 요소, 즉 하나의 헤더 또는 하나의 본문 부분으로 serialize됩니다. 다음과 같은 클래스를 예로 들어 볼 수 있습니다.  
  
```csharp  
[MessageContract]  
public class BankingDepositLog  
{  
  [MessageHeader] public int numRecords;  
  [MessageHeader] public DepositRecord[] records;  
  [MessageHeader] public int branchID;  
}  
```  
  
 이로 인해 SOAP 헤더는 다음과 유사합니다.  
  
```xml  
<BankingDepositLog>  
<numRecords>3</numRecords>  
<records>  
  <DepositRecord>Record1</DepositRecord>  
  <DepositRecord>Record2</DepositRecord>  
  <DepositRecord>Record3</DepositRecord>  
</records>  
<branchID>20643</branchID>  
</BankingDepositLog>  
```  
  
 이에 대한 대체 방법은 <xref:System.ServiceModel.MessageHeaderArrayAttribute>를 사용하는 것입니다. 이 경우에는 각 배열 요소가 개별적으로 serialize되기 때문에 각 배열 요소가 다음과 유사한 헤더를 하나씩 가집니다.  
  
```xml  
<numRecords>3</numRecords>  
<records>Record1</records>  
<records>Record2</records>  
<records>Record3</records>  
<branchID>20643</branchID>  
```  
  
 배열 항목의 기본 이름은 <xref:System.ServiceModel.MessageHeaderArrayAttribute> 특성이 적용되는 멤버의 이름입니다.  
  
 <xref:System.ServiceModel.MessageHeaderArrayAttribute> 특성은 <xref:System.ServiceModel.MessageHeaderAttribute>에서 상속됩니다. 이 특성은 배열이 아닌 특성과 동일한 기능 집합을 가집니다. 예를 들어 단일 헤더에 대해 설정하는 것과 동일한 방식으로 헤더의 배열에 대해 순서, 이름 및 네임스페이스를 설정할 수 있습니다. 배열에서 `Order` 속성을 사용하면 해당 속성이 전체 배열에 적용됩니다.  
  
 컬렉션이 아닌 배열에만 <xref:System.ServiceModel.MessageHeaderArrayAttribute>를 적용할 수 있습니다.  
  
## <a name="using-byte-arrays-in-message-contracts"></a>메시지 계약에 바이트 배열 사용  
 바이트 배열은 배열이 아닌 특성(<xref:System.ServiceModel.MessageBodyMemberAttribute> 및 <xref:System.ServiceModel.MessageHeaderAttribute>)과 함께 사용할 때 배열로 처리되는 것이 아니라 결과 XML에서 Base64로 인코딩된 데이터로 표시되는 특별한 기본 형식으로 처리됩니다.  
  
 바이트 배열을 배열 특성 <xref:System.ServiceModel.MessageHeaderArrayAttribute>와 함께 사용할 때 결과는 사용하는 serializer에 따라 달라집니다. 기본 serializer를 사용하면 배열이 각 바이트에 대해 개별 항목으로 표시됩니다. 그러나 `XmlSerializer`를 선택하면(서비스 계약에서 <xref:System.ServiceModel.XmlSerializerFormatAttribute> 사용) 배열 특성을 사용하는지 또는 배열이 아닌 특성을 사용하는지에 관계없이 바이트 배열이 Base64 데이터로 처리됩니다.  
  
## <a name="signing-and-encrypting-parts-of-the-message"></a>메시지 부분의 서명 및 암호화  
 메시지 계약에서는 메시지 헤더 및/또는 메시지 본문을 디지털 서명 및 암호화해야 하는지 여부를 지정할 수 있습니다.  
  
 이렇게 하려면 <xref:System.ServiceModel.MessageContractMemberAttribute.ProtectionLevel%2A?displayProperty=nameWithType> 및 <xref:System.ServiceModel.MessageHeaderAttribute> 특성에서 <xref:System.ServiceModel.MessageBodyMemberAttribute> 속성을 설정합니다. 속성은 <xref:System.Net.Security.ProtectionLevel?displayProperty=nameWithType> 형식의 열거형이며, <xref:System.Net.Security.ProtectionLevel.None>(암호화 또는 서명 없음), <xref:System.Net.Security.ProtectionLevel.Sign>(디지털 서명만 수행) 또는 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>(암호화 및 디지털 서명 모두 수행)으로 설정할 수 있습니다. 기본값은 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>입니다.  
  
 이러한 보안 기능이 작동하려면 바인딩 및 동작을 적절히 구성해야 합니다. 이러한 보안 기능을 제대로 구성하지 않고 사용하면(예를 들어 자격 증명을 제공하지 않고 메시지를 서명하려는 경우) 유효성을 검사할 때 예외가 throw됩니다.  
  
 메시지 헤더의 경우 보호 수준은 각 헤더에 대해 별도로 결정됩니다.  
  
 메시지 본문 부분의 경우 보호 수준을 "최소 보호 수준"으로 간주합니다. 본문 부분의 수에 관계없이 본문에는 보호 수준이 하나만 있습니다. 본문의 보호 수준은 모든 본문 부분 중 가장 높은 <xref:System.ServiceModel.MessageContractMemberAttribute.ProtectionLevel%2A> 속성 설정에 따라 결정됩니다. 그러나 각 본문 부분의 보호 수준을 실제로 필요한 최소 보호 수준으로 설정해야 합니다.  
  
 다음과 같은 코드의 클래스를 예로 들어 볼 수 있습니다.  
  
```csharp  
[MessageContract]  
public class PatientRecord  
{  
   [MessageHeader(ProtectionLevel=None)] public int recordID;  
   [MessageHeader(ProtectionLevel=Sign)] public string patientName;  
   [MessageHeader(ProtectionLevel=EncryptAndSign)] public string SSN;  
   [MessageBodyMember(ProtectionLevel=None)] public string comments;  
   [MessageBodyMember(ProtectionLevel=Sign)] public string diagnosis;  
   [MessageBodyMember(ProtectionLevel=EncryptAndSign)] public string medicalHistory;  
}  
```  
  
 이 예제에서는 `recordID` 헤더가 보호되지 않고, `patientName`이 `signed`이고, `SSN`이 암호화되고 서명됩니다. 주석 및 진단 본문 부분에서 보호 수준을 더 낮게 지정하더라도 `medicalHistory`을 적용하는 본문 부분인 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>가 적어도 하나는 있으므로 전체 메시지 본문에 대해 암호화 및 서명이 수행됩니다.  
  
## <a name="soap-action"></a>SOAP 동작  
 SOAP 및 관련 웹 서비스 표준은 보낸 모든 SOAP 메시지에 대해 표시할 수 있는 `Action`이라는 속성을 정의합니다. 작업의 <xref:System.ServiceModel.OperationContractAttribute.Action%2A?displayProperty=nameWithType> 및 <xref:System.ServiceModel.OperationContractAttribute.ReplyAction%2A?displayProperty=nameWithType> 속성이 이 속성의 값을 제어합니다.  
  
## <a name="soap-header-attributes"></a>SOAP 헤더 특성  
 SOAP 표준은 헤더에 있을 수 있는 다음 특성을 정의합니다.  
  
- `Actor/Role`(SOAP 1.1에서는 `Actor`, SOAP 1.2에서는 `Role`)  
  
- `MustUnderstand`  
  
- `Relay`  
  
 `Actor` 또는 `Role` 특성은 지정된 헤더를 사용할 노드의 URI(Uniform Resource Identifier)를 지정합니다. `MustUnderstand` 특성은 헤더에서 노드 처리를 인식해야 하는지 여부를 지정합니다. `Relay` 특성은 헤더를 다운스트림 노드로 릴레이할지 여부를 지정합니다. WCF는이 항목의 뒷부분에 나오는 "메시지 계약 버전 관리" 단원에 `MustUnderstand` 지정 된 대로 특성을 제외 하 고 들어오는 메시지에 대해 이러한 특성의 처리를 수행 하지 않습니다. 그러나 다음 설명에서와 같이 필요에 따라 이러한 특성을 읽고 쓸 수 있습니다.  
  
 메시지를 보낼 때 이러한 특성은 기본적으로 내보내지 않습니다. 다음 두 가지 방법으로 이를 변경할 수 있습니다. 첫 번째 방법은 다음 코드 예제에서처럼 <xref:System.ServiceModel.MessageHeaderAttribute.Actor%2A?displayProperty=nameWithType>, <xref:System.ServiceModel.MessageHeaderAttribute.MustUnderstand%2A?displayProperty=nameWithType>, 및 <xref:System.ServiceModel.MessageHeaderAttribute.Relay%2A?displayProperty=nameWithType> 속성을 변경함으로써 원하는 값으로 정적으로 특성을 설정할 수 있습니다. (`Role` 속성은 없으며, <xref:System.ServiceModel.MessageHeaderAttribute.Actor%2A> 속성을 설정하면 SOAP 1.2를 사용할 경우 `Role` 특성을 내보냅니다.)  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader(Actor="http://auditingservice.contoso.com", MustUnderstand=true)] public bool IsAudited;  
  [MessageHeader] public Operation operation;  
  [MessageBodyMember] public BankingTransactionData theData;  
}  
```  
  
 이러한 특성을 제어하는 두 번째 방법은 코드를 통한 동적인 방법입니다. <xref:System.ServiceModel.MessageHeader%601> 형식에서 원하는 헤더 형식을 래핑하고(이 형식을 제네릭이 아닌 버전과 혼동하지 않기 위해), 해당 형식을 <xref:System.ServiceModel.MessageHeaderAttribute>와 함께 사용함으로써 이를 수행할 수 있습니다. 그런 다음, 다음 코드 예제에서처럼 <xref:System.ServiceModel.MessageHeader%601>에서 속성을 사용하여 SOAP 특성을 설정할 수 있습니다.  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public MessageHeader<bool> IsAudited;  
  [MessageHeader] public Operation operation;  
  [MessageBodyMember] public BankingTransactionData theData;  
}  
// application code:  
BankingTransaction bt = new BankingTransaction();  
bt.IsAudited = new MessageHeader<bool>();  
bt.IsAudited.Content = false; // Set IsAudited header value to "false"  
bt.IsAudited.Actor="http://auditingservice.contoso.com";  
bt.IsAudited.MustUnderstand=true;  
```  
  
 동적 및 정적 제어 메커니즘을 모두 사용할 경우 정적 설정이 기본값으로 사용되지만 다음 코드에서처럼 동적 메커니즘을 사용하여 나중에 재정의할 수도 있습니다.  
  
```csharp  
[MessageHeader(MustUnderstand=true)] public MessageHeader<Person> documentApprover;  
// later on in the code:  
BankingTransaction bt = new BankingTransaction();  
bt.documentApprover = new MessageHeader<Person>();  
bt.documentApprover.MustUnderstand = false; // override the static default of 'true'  
```  
  
 다음 코드에서처럼 동적 특성 제어로 반복되는 헤더를 만들 수 있습니다.  
  
```csharp  
[MessageHeaderArray] public MessageHeader<Person> documentApprovers[];  
```  
  
 해당 형식으로 헤더에 <xref:System.ServiceModel.MessageHeader%601> 클래스를 사용하는 경우 받는 쪽에서는 이러한 SOAP 특성을 읽을 수만 있습니다. 받은 메시지에서 특성 설정을 검색하려면 `Actor` 형식 헤더의 `Relay`, `MustUnderstand` 또는 <xref:System.ServiceModel.MessageHeader%601> 속성을 검사합니다.  
  
 메시지를 받은 다음 다시 보내면 SOAP 특성 설정은 <xref:System.ServiceModel.MessageHeader%601> 형식의 헤더에 대해서 라운드트립만 수행합니다.  
  
## <a name="order-of-soap-body-parts"></a>SOAP 본문 부분의 순서  
 본문 부분의 순서를 제어해야 하는 경우가 있습니다. 기본적으로 본문 요소의 순서는 사전순이지만 <xref:System.ServiceModel.MessageBodyMemberAttribute.Order%2A?displayProperty=nameWithType> 속성을 사용하여 제어할 수 있습니다. 이 속성은 상속 시나리오에서의 동작을 제외하고는 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A?displayProperty=nameWithType> 속성과 동일한 의미 체계를 가집니다. 메시지 계약에서는 파생 형식 본문 멤버 앞에 기본 형식 본문 멤버가 정렬되지 않습니다. 자세한 내용은 [데이터 멤버 순서](../../../../docs/framework/wcf/feature-details/data-member-order.md)합니다.  
  
 다음 예제에서 `amount`는 사전순으로 처음이기 때문에 일반적인 경우에는 처음에 나와야 합니다. 그러나 이 경우에는 <xref:System.ServiceModel.MessageBodyMemberAttribute.Order%2A> 속성 때문에 세 번째 위치에 옵니다.  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public Operation operation;  
  [MessageBodyMember(Order=1)] public Account sourceAccount;  
  [MessageBodyMember(Order=2)] public Account targetAccount;  
  [MessageBodyMember(Order=3)] public int amount;  
}  
```  
  
## <a name="message-contract-versioning"></a>메시지 계약 버전 관리  
 필요에 따라 메시지 계약을 변경해야 할 수 있습니다. 예를 들어 사용자 애플리케이션의 새 버전은 메시지에 헤더를 추가할 수 있습니다. 그런 다음 새 버전에서 이전 버전으로 보낼 때 시스템에서는 추가 헤더뿐 아니라 다른 방향으로 전송할 때 누락된 헤더도 처리해야 합니다.  
  
 헤더 버전 관리를 위해 다음 규칙을 적용합니다.  
  
- WCF는 누락 된 헤더에 대 한 개체를 나타내지 않습니다. 해당 멤버는 기본값을 그대로 유지 합니다.  
  
- 또한 WCF는 예기치 않은 추가 헤더를 무시 합니다. 이 규칙에 대한 한 가지 예외는 들어오는 SOAP 메시지에서 추가 헤더가 `MustUnderstand`로 설정된 `true` 특성을 가진 경우입니다. 이 경우 인식되어야 하는 헤더를 처리할 수 없으므로 예외가 throw됩니다.  
  
 메시지 본문은 유사한 버전 관리 규칙을 가지며, 누락된 메시지 본문 부분과 추가 메시지 본문 부분은 모두 무시됩니다.  
  
## <a name="inheritance-considerations"></a>상속 고려 사항  
 메시지 계약 형식은 기본 형식에도 메시지 계약이 있는 한 다른 형식으로부터 상속될 수 있습니다.  
  
 다른 메시지 계약 형식으로부터 상속되는 메시지 계약 형식을 사용하여 메시지를 만들거나 액세스할 때는 다음 규칙을 적용하십시오.  
  
- 상속 계층 구조에서는 모든 메시지 헤더가 함께 수집되어 메시지에 대한 전체 헤더 집합을 형성합니다.  
  
- 상속 계층 구조에서는 모든 메시지 본문 부분이 함께 수집되어 전체 메시지 본문을 형성합니다. 본문 부분의 순서는 상속 계층 구조에서의 위치와 상관없이 일반 순서 지정 규칙에 따라 <xref:System.ServiceModel.MessageBodyMemberAttribute.Order%2A?displayProperty=nameWithType> 속성별로 지정된 다음 사전순으로 지정됩니다. 메시지 본문 부분이 상속 트리의 여러 수준에 표시되면 메시지 계약 상속을 사용하지 않는 것이 좋습니다. 기본 클래스 및 파생 클래스가 헤더 또는 본문 부분을 동일한 이름으로 정의하는 경우 해당 헤더 또는 본문 부분의 값을 저장하기 위해 기본-최상 클래스의 멤버가 사용됩니다.  
  
 다음과 같은 코드의 클래스를 예로 들어 볼 수 있습니다.  
  
```csharp  
[MessageContract]  
public class PersonRecord  
{  
  [MessageHeader(Name="ID")] public int personID;  
  [MessageBodyMember] public string patientName;  
}  
  
[MessageContract]  
public class PatientRecord : PersonRecord  
{  
  [MessageHeader(Name="ID")] public int patientID;  
  [MessageBodyMember] public string diagnosis;  
}  
```  
  
 `PatientRecord` 클래스는 `ID`라는 하나의 헤더로 메시지를 설명합니다. 기본-최상 멤버를 선택했으므로 헤더는 `personID` 멤버가 아닌 `patientID`에 해당합니다. 따라서 이 경우에는 `patientID` 필드가 필요하지 않습니다. 사전순이므로 메시지 본문에는 `diagnosis` 요소가 `patientName` 요소보다 먼저 포함됩니다. 예제에서는 사용해서는 안 되는 패턴을 보여 줍니다. 기본 메시지 계약 및 파생 메시지 계약에는 모두 메시지 본문 부분이 있습니다.  
  
## <a name="wsdl-considerations"></a>WSDL 고려 사항  
 메시지 계약을 사용하는 서비스로부터 WSDL(웹 서비스 기술 언어) 계약을 생성할 때는 메시지 계약 기능 중 일부가 결과 WSDL에서 반영되지 않을 수 있다는 점을 기억해야 합니다. 다음 사항을 고려하십시오.  
  
- WSDL은 헤더 배열의 개념을 표현할 수 없습니다. <xref:System.ServiceModel.MessageHeaderArrayAttribute>를 사용하여 헤더 배열과 함께 메시지를 만들 때 결과 WSDL은 배열 대신 하나의 헤더만 반영합니다.  
  
- 결과 WSDL 문서는 일부 보호 수준 정보를 반영하지 않을 수 있습니다.  
  
- WSDL에서 생성된 메시지 형식은 메시지 계약 형식의 클래스 이름과 동일한 이름을 가집니다.  
  
- 여러 작업에서 동일한 메시지 계약을 사용할 때 여러 메시지 유형이 WSDL 문서에서 생성됩니다. 다음에 사용할 때에는 숫자 "2", "3" 등을 추가함으로써 고유한 이름을 만듭니다. WSDL을 다시 가져올 때 여러 메시지 계약 형식이 만들어지며 이름을 제외하고는 동일합니다.  
  
## <a name="soap-encoding-considerations"></a>SOAP 인코딩 고려 사항  
 WCF를 사용 하면 XML의 레거시 SOAP 인코딩 스타일을 사용할 수 있지만 사용 하지 않는 것이 좋습니다. 이 스타일을 사용할 때(서비스 계약에 적용된 `Use`에서 `Encoded` 속성을 <xref:System.ServiceModel.XmlSerializerFormatAttribute?displayProperty=nameWithType>로 설정), 다음 추가 사항을 고려해야 합니다.  
  
- 메시지 헤더는 지원되지 않습니다. 이는 특성 <xref:System.ServiceModel.MessageHeaderAttribute> 및 배열 특성 <xref:System.ServiceModel.MessageHeaderArrayAttribute>가 SOAP 인코딩과 호환되지 않음을 의미합니다.  
  
- 메시지 계약이 래핑되지 않으면, 즉 <xref:System.ServiceModel.MessageContractAttribute.IsWrapped%2A> 속성이 `false`로 설정되면 메시지 계약에는 하나의 본문 부분만 있을 수 있습니다.  
  
- 요청 메시지 계약에 대한 래퍼 요소의 이름은 작업 이름과 일치해야 합니다. 이름을 일치시키려면 메시지 계약의 `WrapperName` 속성을 사용하십시오.  
  
- 응답 메시지 계약에 대한 래퍼 요소의 이름은 접미사가 'Response'인 작업의 이름과 동일해야 합니다. 이름을 일치시키려면 메시지 계약의 <xref:System.ServiceModel.MessageContractAttribute.WrapperName%2A> 속성을 사용하십시오.  
  
- SOAP 인코딩은 개체 참조를 유지합니다. 예를 들어, 다음과 같은 코드를 생각해 볼 수 있습니다.  
  
    ```csharp  
    [MessageContract(WrapperName="updateChangeRecord")]  
    public class ChangeRecordRequest  
    {  
      [MessageBodyMember] Person changedBy;  
      [MessageBodyMember] Person changedFrom;  
      [MessageBodyMember] Person changedTo;  
    }  
  
    [MessageContract(WrapperName="updateChangeRecordResponse")]  
    public class ChangeRecordResponse  
    {  
      [MessageBodyMember] Person changedBy;  
      [MessageBodyMember] Person changedFrom;  
      [MessageBodyMember] Person changedTo;  
    }  
  
    // application code:  
    ChangeRecordRequest cr = new ChangeRecordRequest();  
    Person p = new Person("John Doe");  
    cr.changedBy=p;  
    cr.changedFrom=p;  
    cr.changedTo=p;  
    ```  
  
 SOAP 인코딩을 사용하여 메시지를 serialize한 후에 `changedFrom` 및 `changedTo`는 `p`의 자체 복사본을 포함하지 않으며, 대신 `changedBy` 요소 내의 복사본을 가리킵니다.  
  
## <a name="performance-considerations"></a>성능 고려 사항  
 모든 메시지 헤더 및 메시지 본문 부분이 나머지에 대해 각각 serialize됩니다. 그러므로 각 헤더 및 본문 부분에 대해 동일한 네임스페이스를 다시 선언할 수 있습니다. 성능을 향상시키기 위해 통신 중에 특히 메시지의 크기를 기준으로 여러 헤더와 본문 부분을 단일 헤더 또는 본문 부분으로 통합합니다. 예를 들면 다음 코드 대신  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public Operation operation;  
  [MessageBodyMember] public Account sourceAccount;  
  [MessageBodyMember] public Account targetAccount;  
  [MessageBodyMember] public int amount;  
}  
```  
  
 아래와 같은 코드를 사용합니다.  
  
```csharp  
[MessageContract]  
public class BankingTransaction  
{  
  [MessageHeader] public Operation operation;  
  [MessageBodyMember] public OperationDetails details;  
}  
  
[DataContract]  
public class OperationDetails  
{  
  [DataMember] public Account sourceAccount;  
  [DataMember] public Account targetAccount;  
  [DataMember] public int amount;  
}  
```  
  
### <a name="event-based-asynchronous-and-message-contracts"></a>이벤트 기반 비동기 및 메시지 계약  
 이벤트 기반 비동기 모델에 대한 디자인 지침에 따르면 둘 이상의 값이 반환될 경우 그 중 하나는 `Result` 속성으로 반환되고 나머지 값은 <xref:System.EventArgs> 개체의 속성으로 반환됩니다. 따라서 클라이언트가 이벤트 기반 비동기 명령 옵션을 사용하여 메타데이터를 가져오고 작업이 둘 이상의 값을 반환할 경우 기본 <xref:System.EventArgs> 개체는 그 중 하나를 `Result` 속성으로 반환하고, 나머지 값은 <xref:System.EventArgs> 개체의 속성이 됩니다.  
  
 메시지 개체를 `Result` 속성으로 수신하고 반환된 값을 해당 개체의 속성으로 포함하려면 `/messageContract` 명령 옵션을 사용합니다. 이렇게 하면 응답 메시지를 `Result` 개체의 <xref:System.EventArgs> 속성으로 반환하는 서명이 생성됩니다. 모든 내부 반환 값은 응답 메시지 개체의 속성이 됩니다.  
  
## <a name="see-also"></a>참고자료

- [데이터 계약 사용](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)
- [서비스 디자인 및 구현](../../../../docs/framework/wcf/designing-and-implementing-services.md)
