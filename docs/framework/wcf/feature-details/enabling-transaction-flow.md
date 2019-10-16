---
title: 트랜잭션 흐름 사용
ms.date: 03/30/2017
helpviewer_keywords:
- transactions [WCF], enabling flow
ms.assetid: a03f5041-5049-43f4-897c-e0292d4718f7
ms.openlocfilehash: 2443e82dd9c6d8b5447c2fa16b537a9feed8ddaf
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70895163"
---
# <a name="enabling-transaction-flow"></a>트랜잭션 흐름 사용
WCF (Windows Communication Foundation)는 트랜잭션 흐름을 제어 하기 위한 매우 유연한 옵션을 제공 합니다. 특성 및 구성을 조합하여 서비스의 트랜잭션 흐름 설정을 나타낼 수 있습니다.  
  
## <a name="transaction-flow-settings"></a>트랜잭션 흐름 설정  
 서비스 엔드포인트에 대한 트랜잭션 흐름 설정은 다음 세 가지 값의 교집합 결과로서 생성됩니다.  
  
- 서비스 계약의 각 메서드에 지정된 <xref:System.ServiceModel.TransactionFlowAttribute> 특성  
  
- 특정 바인딩의 `TransactionFlow` 바인딩 속성  
  
- 특정 바인딩의 `TransactionFlowProtocol` 바인딩 속성 `TransactionFlowProtocol` binding 속성을 사용하면 트랜잭션을 이동하는 데 사용할 수 있는 서로 다른 두 가지 트랜잭션 프로토콜 중에서 선택할 수 있습니다. 다음 단원에서는 각 트랜잭션 프로토콜에 대해 간단하게 설명합니다.  
  
### <a name="ws-atomictransaction-protocol"></a>WS-AtomicTransaction 프로토콜  
 타사 프로토콜 스택과의 상호 운용성이 필요한 시나리오의 경우에는 WS-AT(WS-AtomicTransaction) 프로토콜이 유용합니다.  
  
### <a name="oletransactions-protocol"></a>OleTransactions 프로토콜  
 타사 프로토콜 스택과의 상호 운용성이 필요하지 않고, 서비스 배포자가 WS-AT 프로토콜 서비스를 로컬에서 사용할 수 없거나 기존 네트워크 토폴로지에서 WS-AT를 사용할 수 없음을 사전에 알고 있는 시나리오의 경우에는 OleTransactions 프로토콜이 유용합니다.  
  
 다음 표에서는 이러한 여러 조합을 사용하여 생성할 수 있는 서로 다른 형식의 트랜잭션 흐름을 보여 줍니다.  
  
|TransactionFlow<br /><br /> 바인딩(binding)|TransactionFlow 바인딩 속성|TransactionFlowProtocol 바인딩 프로토콜|트랜잭션 흐름 형식|  
|---------------------------------|--------------------------------------|----------------------------------------------|------------------------------|  
|필수|true|WS-AT|트랜잭션이 상호 운용할 수 있는 WS-AT 형식으로 이동해야 합니다.|  
|필수|true|OleTransactions|트랜잭션은 WCF OleTransactions 형식으로 이동 해야 합니다.|  
|필수|false|해당 사항 없음|이 구성이 잘못되었으므로 사용할 수 없습니다.|  
|Allowed|true|WS-AT|트랜잭션이 상호 운용할 수 있는 WS-AT 형식으로 이동할 수 있습니다.|  
|Allowed|true|OleTransactions|트랜잭션은 WCF OleTransactions 형식으로 이동 될 수 있습니다.|  
|Allowed|false|모든 값|트랜잭션이 이동하지 않습니다.|  
|NotAllowed|모든 값|모든 값|트랜잭션이 이동하지 않습니다.|  
  
 다음 표에서는 메시지 처리 결과를 요약하여 설명합니다.  
  
|들어오는 메시지|TransactionFlow 설정|트랜잭션 헤더|메시지 처리 결과|  
|----------------------|-----------------------------|------------------------|-------------------------------|  
|트랜잭션이 예상 프로토콜 형식과 일치합니다.|Allowed 또는 Mandatory|`MustUnderstand`가 `true`와 같습니다.|프로세스|  
|트랜잭션이 예상 프로토콜 형식과 일치하지 않습니다.|필수|`MustUnderstand`가 `false`와 같습니다.|트랜잭션이 필요하므로 거부되었습니다.|  
|트랜잭션이 예상 프로토콜 형식과 일치하지 않습니다.|Allowed|`MustUnderstand`가 `false`와 같습니다.|헤더를 인식할 수 없으므로 거부되었습니다.|  
|모든 프로토콜 형식을 사용하는 트랜잭션입니다.|NotAllowed|`MustUnderstand`가 `false`와 같습니다.|헤더를 인식할 수 없으므로 거부되었습니다.|  
|트랜잭션이 없습니다.|필수|해당 사항 없음|트랜잭션이 필요하므로 거부되었습니다.|  
|트랜잭션이 없습니다.|Allowed|해당 사항 없음|프로세스|  
|트랜잭션이 없습니다.|NotAllowed|해당 사항 없음|프로세스|  
  
 계약의 각 메서드에는 다른 트랜잭션 흐름 요구 사항이 있을 수 있지만, 트랜잭션 흐름 프로토콜 설정의 범위는 바인딩 수준으로 지정됩니다. 즉, 동일한 엔드포인트를 공유하는 모든 메서드는 동일한 바인딩을 공유하므로 필요 시 동일한 트랜잭션 프로토콜뿐만 아니라 트랜잭션 흐름을 필요로 하거나 허용하는 동일한 정책도 공유합니다.  
  
## <a name="enabling-transaction-flow-at-the-method-level"></a>메서드 수준에서 트랜잭션 흐름 사용  
 트랜잭션 흐름 요구 사항이 서비스 계약의 모든 메서드에 대해 동일하지 않은 경우도 있습니다. 따라서 WCF는 각 메서드의 트랜잭션 흐름 기본 설정을 표현할 수 있는 특성 기반 메커니즘을 제공 합니다. 이 작업은 서비스 운영에서 트랜잭션 헤더를 허용하는 수준을 지정하는 <xref:System.ServiceModel.TransactionFlowAttribute>를 사용하여 수행합니다. 트랜잭션 흐름을 사용하려면 이 특성을 갖는 서비스 계약 메서드를 표시해야 합니다. 이 특성은 <xref:System.ServiceModel.TransactionFlowOption> 열거형 값 중 하나를 사용하며, 기본값은 <xref:System.ServiceModel.TransactionFlowOption.NotAllowed>입니다. <xref:System.ServiceModel.TransactionFlowOption.NotAllowed>를 제외한 모든 값을 지정하는 경우 메서드는 단방향이 아니어야 합니다. 개발자는 이 특성을 사용하여 디자인 타임에 메서드 수준의 트랜잭션 흐름 요구 사항이나 제약 조건을 지정할 수 있습니다.  
  
## <a name="enabling-transaction-flow-at-the-endpoint-level"></a>엔드포인트 수준에서 트랜잭션 흐름 사용  
 WCF는 특성이 제공 하는 <xref:System.ServiceModel.TransactionFlowAttribute> 메서드 수준 트랜잭션 흐름 설정 외에도 트랜잭션 흐름에 대해 끝점 수준 설정을 제공 하 여 관리자가 더 높은 수준에서 트랜잭션 흐름을 제어할 수 있도록 합니다.  
  
 이 작업은 <xref:System.ServiceModel.Channels.TransactionFlowBindingElement>를 사용하여 수행할 수 있습니다. 이를 통해 엔드포인트의 바인딩 설정에서 들어오는 트랜잭션 흐름을 사용하거나 사용하지 않도록 설정할 수 있을 뿐 아니라 들어오는 트랜잭션에 대해 원하는 트랜잭션 프로토콜 형식을 지정할 수 있습니다.  
  
 바인딩에서 트랜잭션 흐름을 사용하지 않지만 서비스 계약의 작업 중 하나에 들어오는 트랜잭션이 필요한 경우 서비스 시작 시 유효성 검사 예외가 throw됩니다.  
  
 WCF에서 제공 하는 대부분의 바인딩에 `transactionFlow` 는 `transactionProtocol` 들어오는 트랜잭션을 허용 하도록 특정 바인딩을 구성할 수 있는 및 특성이 포함 되어 있습니다. 구성 요소를 설정 하는 방법에 대 한 자세한 내용은 [ \<binding >](../../../../docs/framework/misc/binding.md)을 참조 하세요.  
  
 관리자나 배포자는 구성 파일을 사용하여 배포 시 트랜잭션 흐름 요구 사항이나 제약 조건을 구성하는 데 엔드포인트 수준의 트랜잭션 흐름을 사용할 수 있습니다.  
  
## <a name="security"></a>보안  
 시스템 보안 및 무결성을 보장하려면 애플리케이션 간에 트랜잭션을 이동할 때 메시지 교환을 보호해야 합니다. 트랜잭션 정보를 동일한 트랜잭션에 참여하도록 허용되지 않은 애플리케이션에 노출하거나 이동해서는 안 됩니다.  
  
 메타 데이터 교환을 사용 하 여 알 수 없거나 신뢰할 수 없는 웹 서비스에 대 한 WCF 클라이언트를 생성할 때 이러한 웹 서비스에 대 한 작업을 호출 하면 현재 트랜잭션이 표시 되지 않습니다 (가능한 경우). 다음 예제에서는 이 작업을 수행하는 방법을 보여 줍니다.  
  
```csharp
//client code which has an ambient transaction  
using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Suppress))  
{  
    // No transaction will flow to this operation  
    untrustedProxy.Operation1(...);  
    scope.Complete();  
}  
//remainder of client code  
```  
  
 또한 인증되고 권한이 부여된 클라이언트에서만 들어오는 트랜잭션을 허용하도록 서비스를 구성해야 합니다. 들어오는 트랜잭션은 신뢰 수준이 높은 클라이언트에서 온 경우에만 허용해야 합니다.  
  
## <a name="policy-assertions"></a>정책 어설션  
 WCF는 정책 어설션을 사용 하 여 트랜잭션 흐름을 제어 합니다. 정책 어설션은 서비스의 정책 문서에 있으며 계약, 구성 및 특성을 집계하여 생성됩니다. 클라이언트에서는 HTTP GET 또는 WS-MetadataExchange 요청-회신을 사용하여 서비스의 정책 문서를 가져올 수 있습니다. 그런 다음 클라이언트에서 정책 문서를 처리하여 트랜잭션 흐름을 지원하거나 요구하는 서비스 계약의 작업을 결정할 수 있습니다.  
  
 트랜잭션 흐름 정책 어설션은 트랜잭션을 나타내기 위해 클라이언트가 서비스에 보내야 하는 SOAP 헤더를 지정하여 트랜잭션 흐름에 영향을 줍니다. 모든 트랜잭션 헤더는 `MustUnderstand`로 설정된 `true`로 표시해야 합니다. 이와 다르게 표시된 헤더가 있는 모든 메시지는 SOAP 오류와 함께 거부됩니다.  
  
 하나의 트랜잭션 관련 정책 어설션만이 단일 작업에 있을 수 있습니다. 작업에 대해 둘 이상의 트랜잭션 어설션이 있는 정책 문서는 잘못 된 것으로 간주 되어 WCF에서 거부 됩니다. 또한 단일 트랜잭션 프로토콜만이 각 포트 형식 내에 있을 수 있습니다. 단일 포트 형식 내에서 둘 이상의 트랜잭션 프로토콜을 참조 하는 작업을 포함 하는 정책 문서는 잘못 된 것으로 간주 되며 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)에서 거부 됩니다. 트랜잭션 어설션이 출력 메시지나 단방향 입력 메시지에 있는 정책 문서도 잘못된 것으로 간주됩니다.
